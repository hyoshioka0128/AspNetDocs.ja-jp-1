---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR トラブルシューティング (SignalR 1.x) |マイクロソフトドキュメント
author: bradygaster
description: この資料では、SignalR アプリケーションの開発に関する一般的な問題について説明します。
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543094"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>SignalR トラブルシューティング (SignalR 1.x)

[パトリック・フレッチャー](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このドキュメントでは、SignalR に関する一般的なトラブルシューティングの問題について説明します。

このドキュメントには、次のセクションが含まれています。

- [クライアントとサーバー間のメソッドの呼び出しがサイレント で失敗する](#connection)
- [その他の接続の問題](#other)
- [コンパイルおよびサーバー側エラー](#server)
- [ビジュアルスタジオの問題](#vs)
- [インターネット インフォメーション サービスの問題](#iis)
- [Azure の問題](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>クライアントとサーバー間のメソッドの呼び出しがサイレント で失敗する

このセクションでは、クライアントとサーバー間のメソッド呼び出しが、意味のあるエラー メッセージなしで失敗する原因について説明します。 SignalR アプリケーションでは、サーバーはクライアントが実装するメソッドに関する情報を持っていません。サーバーがクライアント メソッドを呼び出すと、メソッド名とパラメーター データがクライアントに送信され、サーバーが指定した形式で存在する場合にのみメソッドが実行されます。 クライアントで一致するメソッドが見つからない場合は、何も起こらず、サーバー上でエラー メッセージは発生しません。

呼び出されないクライアント メソッドをさらに調査するには、ハブで start メソッドを呼び出す前にログ記録を有効にして、サーバーからどのような呼び出しが発生しているかを確認できます。 JavaScript アプリケーションでのログ記録を有効にするには、「[クライアント側のログを有効にする方法 (JavaScript クライアント バージョン)」](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)を参照してください。 .NET クライアント アプリケーションでログを有効にするには、「[クライアント側のログ記録を有効にする方法 (.NET クライアント バージョン)」](../guide-to-the-api/hubs-api-guide-net-client.md#logging)を参照してください。

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>メソッドのスペルが間違っている、メソッドシグネチャが正しくない、またはハブ名が正しくない

呼び出されたメソッドの名前またはシグネチャがクライアントの適切なメソッドと完全に一致しない場合、呼び出しは失敗します。 サーバーによって呼び出されたメソッド名が、クライアント上のメソッドの名前と一致することを確認します。 また、SignalR は、JavaScript で適切にキャメルケース メソッドを使用してハブ プロキシを作成するため`SendMessage`、サーバーで呼び出`sendMessage`されるメソッドはクライアント プロキシで呼び出されます。 サーバー側コードで`HubName`属性を使用する場合は、使用される名前がクライアント上のハブの作成に使用された名前と一致することを確認します。 属性を`HubName`使用しない場合は、JavaScript クライアントのハブの名前が、ChatHub ではなく chatHub などのキャメルケースであることを確認します。

### <a name="duplicate-method-name-on-client"></a>クライアント上のメソッド名が重複しています

大文字と小文字の違いだけが異なるメソッドがクライアントに重複していないことを確認します。 クライアント アプリケーションに という`sendMessage`メソッドがある場合は、 メソッドも呼び出`SendMessage`されていないことを確認します。

### <a name="missing-json-parser-on-the-client"></a>クライアントで JSON パーサーが見つからない

SignalR は、サーバーとクライアント間の呼び出しをシリアル化するために、JSON パーサーが存在する必要があります。 クライアントに組み込みの JSON パーサー (Internet Explorer 7 など) がない場合は、アプリケーションに JSON パーサーを含める必要があります。 JSON パーサーは[ここから](http://nuget.org/packages/json2)ダウンロードできます。

### <a name="mixing-hub-and-persistentconnection-syntax"></a>ハブと永続接続の構文を混在させる

SignalR は、ハブと永続接続の 2 つの通信モデルを使用します。 クライアント コードでは、これら 2 つの通信モデルを呼び出す構文が異なります。 サーバー コードにハブを追加した場合は、すべてのクライアント コードで適切なハブ構文が使用されていることを確認します。

**クライアントで永続的な接続を作成する JavaScript クライアント コード**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**JavaScript クライアントでハブ プロキシを作成する JavaScript クライアント コード**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**ルートを永続的な接続にマップする C# サーバー コード**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**ハブへのルートをマップする C# サーバー コード、または複数のアプリケーションがある場合は複数のハブにルーティングする**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>サブスクリプションが追加される前に接続が開始されました

サーバーから呼び出すことができるメソッドがプロキシに追加される前にハブの接続が開始された場合、メッセージは受信されません。 次の JavaScript コードは、ハブを正しく起動しません。

**ハブ メッセージの受信を許可しない不正な JavaScript クライアント コード**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

代わりに、Start を呼び出す前にメソッド サブスクリプションを追加します。

**ハブにサブスクリプションを正しく追加する JavaScript クライアント コード**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>ハブ プロキシにメソッド名がありません

サーバーで定義されているメソッドがクライアントでサブスクライブされていることを確認します。 サーバーがメソッドを定義しても、クライアント プロキシに追加する必要があります。 メソッドは、次の方法でクライアント プロキシに追加できます (メソッドはハブの`client`メンバーに直接追加されません)。

**ハブ プロキシにメソッドを追加する JavaScript クライアント コード**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>パブリックとして宣言されていないハブまたはハブ メソッド

クライアントで表示するには、ハブの実装とメソッドを`public`として宣言する必要があります。

### <a name="accessing-hub-from-a-different-application"></a>別のアプリケーションからハブにアクセスする

SignalR ハブは、SignalR クライアントを実装するアプリケーションを介してのみアクセスできます。 SignalR は、他の通信ライブラリ (SOAP や WCF Web サービスなど) と相互運用できません。ターゲット プラットフォームで使用できる SignalR クライアントがない場合は、サーバーのエンドポイントに直接アクセスできません。

### <a name="manually-serializing-data"></a>データの手動シリアル化

SignalR は自動的に JSON を使用してメソッドのパラメーターをシリアル化します。

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>リモート ハブ メソッドが OnDisconnected 関数のクライアントで実行されない

この動作は仕様です。 呼`OnDisconnected`び出されると、ハブは既に状態`Disconnected`に入っており、それ以上のハブ メソッドを呼び出す必要はありません。

**OnDisconnected イベントでコードを正しく実行する C# サーバー コード**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>接続の制限に達しました

Windows 7 のようなクライアント オペレーティング システムで IIS のフル バージョンを使用する場合、10 接続の制限が課されます。 クライアント OS を使用する場合は、代わりに IIS Express を使用してこの制限を回避します。

### <a name="cross-domain-connection-not-set-up-properly"></a>クロスドメイン接続が正しく設定されていません

クロスドメイン接続 (SignalR URL がホスト ページと同じドメインにない接続) が正しく設定されていない場合、エラー メッセージが表示されずに接続が失敗する可能性があります。 クロスドメイン通信を有効にする方法については、クロス[ドメイン接続を確立する方法を](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)参照してください。

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>NET クライアントで NTLM (アクティブ ディレクトリ) を使用した接続が機能しない

ドメイン セキュリティを使用する .NET クライアント アプリケーションの接続は、接続が正しく構成されていないと失敗することがあります。 ドメイン環境で SignalR を使用するには、次のように必要な接続プロパティを設定します。

**接続資格情報を実装する C# クライアント コード**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>その他の接続の問題

ここでは、接続中に発生する特定の現象やエラー メッセージの原因と解決策について説明します。

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>「データを送信する前に Start を呼び出す必要があります」エラー

このエラーは、接続が開始される前にコードが SignalR オブジェクトを参照している場合に一般的に発生します。 サーバーで定義されたメソッドを呼び出すハンドラなどのワイヤアップは、接続の完了後に追加する必要があります。 呼`Start`び出しは非同期であるため、呼び出しの完了前に呼び出し後のコードが実行される可能性があることに注意してください。 接続が完全に開始された後にハンドラーを追加する最善の方法は、start メソッドにパラメーターとして渡されるコールバック関数にハンドラーを追加することです。

**SignalR オブジェクトを参照するイベント ハンドラーを正しく追加する JavaScript クライアント コード**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

このエラーは、SignalR オブジェクトが参照されている間に接続が停止した場合にも表示されます。

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>「301 永久に移動」または「302 一時的に移動」エラー

このエラーは、プロジェクトに SignalR という名前のフォルダーが含まれている場合に表示され、自動的に作成されたプロキシに干渉します。 このエラーを回避するには、アプリケーションで呼び出`SignalR`されるフォルダーを使用したり、自動プロキシ生成をオフにしたりしないでください。 詳細については[、「生成されたプロキシと、そのプロキシがあなたのために何をするのか](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)」を参照してください。

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>NET または Silverlight クライアントで "403 禁止" エラーが発生しました

このエラーは、ドメイン間通信が適切に有効になっていないドメイン間の環境で発生する可能性があります。 クロスドメイン通信を有効にする方法については、クロス[ドメイン接続を確立する方法を](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)参照してください。 Silverlight クライアントでドメイン間接続を確立するには[、「Silverlight クライアントからのドメイン間接続](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)」を参照してください。

### <a name="404-not-found-error"></a>"404 見つかりません" エラー

この問題には、いくつかの原因があります。 次のすべてを確認します。

- **ハブ プロキシ アドレス参照が正しくフォーマットされていません:** このエラーは、生成されたハブ プロキシ アドレスへの参照が正しくフォーマットされていない場合に一般的に発生します。 ハブ アドレスへの参照が正しく行われたことを確認します。 詳細については、[動的に生成されたプロキシを参照する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)を参照してください。
- **ハブ ルートを追加する前に、アプリケーションにルートを追加します。** アプリケーションで他のルートを使用する場合は、最初に追加されたルートが`MapHubs`への呼び出しであることを確認します。

### <a name="500-internal-server-error"></a>"500 内部サーバー エラー"

これは、さまざまな原因を持つ可能性のある非常に一般的なエラーです。 エラーの詳細は、サーバーのイベント ログに記録されるか、サーバーのデバッグを通じて見つけることができます。 サーバーの詳細なエラーをオンにすることで、より詳細なエラー情報を取得できます。 詳細については、「 [Hub クラスのエラーを処理する方法](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)」を参照してください。

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>"型エラー:&lt;ハブ&gt;の型が定義されていません" エラー

このエラーは、呼び出し`MapHubs`が正しく行われなかった場合に発生します。 詳細については[、SignalR ルートを登録し、SignalR オプションを構成する方法](../guide-to-the-api/hubs-api-guide-server.md#route)を参照してください。

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>ユーザー コードによって処理されませんでした。

メソッドに送信するパラメーターにシリアル化できない型 (ファイル ハンドルやデータベース接続など) が含まれていないことを確認します。 クライアントに送信したくないサーバー側オブジェクトのメンバーを使用する必要がある場合 (セキュリティまたはシリアル化の理由から) 属性を使用します`JSONIgnore`。

### <a name="protocol-error-unknown-transport-error"></a>「プロトコル エラー: 不明なトランスポート」エラー

このエラーは、クライアントが SignalR が使用するトランスポートをサポートしていない場合に発生することがあります。 SignalR で使用できるブラウザーの詳細については、[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)を参照してください。

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"JavaScript ハブ プロキシの生成が無効になっています。

このエラーは、`DisableJavaScriptProxies`で動的に生成されたプロキシへの参照を含む間に設定`signalr/hubs`されている場合に発生します。 プロキシを手動で作成する方法の詳細については、「[生成されたプロキシと、そのプロキシが何を行うか」を](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)参照してください。

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>「接続 ID の形式が正しくありません」または「アクティブな SignalR 接続中にユーザー ID を変更することはできません」エラー

このエラーは、認証が使用されている場合に表示され、クライアントは接続が停止する前にログアウトされます。 解決策は、クライアントをログアウトする前に SignalR 接続を停止することです。

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"キャッチされないエラー: シグナル: jQuery が見つかりません。 「SignalR.js ファイル」エラーの前に jQuery が参照されていることを確認してください。

シグナル・クライアントを実行するには jQuery が必要です。 jQuery への参照が正しいこと、使用されるパスが有効であること、および jQuery への参照が SignalR への参照より前にあることを確認します。

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>"キャッチされていない型エラー: 未定義の&lt;プロパティ&gt;' プロパティ ' を読み取ることができません" エラー

このエラーは、jQuery またはハブ プロキシが正しく参照されなかった場合に発生します。 jQuery とハブ プロキシへの参照が正しいこと、使用されるパスが有効であること、および jQuery への参照がハブ プロキシへの参照より前であることを確認します。 ハブ プロキシへの既定の参照は、次のようになります。

**ハブ プロキシを正しく参照する HTML クライアント側コード**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>"ユーザー コードによって処理されませんでした" エラー

このエラーは、誤ったオーバーロードが使用`Hub.On`されている場合に発生することがあります。 メソッドに戻り値がある場合、戻り値の型はジェネリック型パラメーターとして指定する必要があります。

**クライアントで定義されたメソッド (生成されたプロキシなし)**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>接続 ID が一致しないか、ページ読み込み間の接続が中断される

この動作は仕様です。 ハブ オブジェクトはページ オブジェクトでホストされるため、ページが更新されるとハブは破棄されます。 複数ページのアプリケーションでは、ページ読み込み間で一貫性を持たることができるように、ユーザーと接続 ID の間の関連付けを維持する必要があります。 接続 ID は、`ConcurrentDictionary`オブジェクトまたはデータベースのサーバーに格納できます。

### <a name="value-cannot-be-null-error"></a>"値を null にすることはできません" エラー

オプション パラメータを持つサーバー側メソッドは現在サポートされていません。省略可能なパラメーターを省略すると、メソッドは失敗します。 詳細については、「オプション[パラメータ](https://github.com/SignalR/SignalR/issues/324)」を参照してください。

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>「Firefox はアドレス&lt;&gt;でサーバーへの接続を確立できません」 Firebug のエラー

このエラー メッセージは、WebSocket トランスポートのネゴシエーションが失敗し、代わりに別のトランスポートが使用された場合に Firebug で表示されます。 この動作は仕様です。

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>NET クライアント アプリケーションでエラー「検証手順に従ってリモート証明書が無効です」

サーバーにカスタム クライアント証明書が必要な場合は、要求を行う前に接続に x509certificate を追加できます。 を使用して`Connection.AddClientCertificate`接続に証明書を追加します。

### <a name="connection-drops-after-authentication-times-out"></a>認証がタイムアウトした後に接続が切断される

この動作は仕様です。 接続がアクティブな間は認証資格情報を変更できません。資格情報を更新するには、接続を停止して再起動する必要があります。

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>オンコネクテッドは、jQueryモバイルを使用しているときに2回呼び出されます

jQuery Mobileの`initializePage`関数は、各ページのスクリプトを強制的に再実行し、2つ目の接続を作成します。 この問題の解決策は次のとおりです。

- JavaScript ファイルの前に jQuery モバイルへの参照を含めます。
- を設定`initializePage``$.mobile.autoInitializePage = false`して機能を無効にします。
- 接続を開始する前に、ページの初期化が完了するまで待ちます。

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>サーバー送信イベントを使用して Silverlight アプリケーションでメッセージが遅延する

サーバーが Silverlight でイベントを送信した場合、メッセージが遅延します。 代わりに長いポーリングを使用するには、接続を開始するときに次の方法を使用します。

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>フォーエバー フレーム プロトコルを使用して "アクセス許可が拒否されました"

これは、ここで説明する既知の問題[です](https://github.com/SignalR/SignalR/issues/1963)。 この現象は最新の JQuery ライブラリを使用して発生することがあります。回避策は、アプリケーションを JQuery 1.8.2 にダウングレードすることです。

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>コンパイルおよびサーバー側エラー

 次のセクションでは、コンパイラとサーバー側のランタイム エラーに対する可能な解決策について説明します。 

### <a name="reference-to-hub-instance-is-null"></a>ハブ インスタンスへの参照が null です

ハブ インスタンスは接続ごとに作成されるため、コード内にハブのインスタンスを自分で作成することはできません。 ハブ自体の外部からハブのメソッドを呼び出す場合は、「ハブ コンテキストへの参照を取得する方法について、[ハブ クラス外からクライアント メソッドを呼び出し、グループを管理する方法](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)」を参照してください。

### <a name="httpcontextcurrentsession-is-null"></a>セッションが null です。

この動作は仕様です。 セッション状態を有効にすると双方向メッセージングが中断されるため、SignalR はASP.NETセッション状態をサポートしません。

### <a name="no-suitable-method-to-override"></a>オーバーライドする適切なメソッドがありません

古いドキュメントやブログのコードを使用している場合、このエラーが表示されることがあります。 変更または非推奨のメソッドの名前を参照していないことを確認します (など`OnConnectedAsync`)。

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>をクリックします。

この動作は仕様です。 このメンバーは非推奨であるため、使用しないでください。

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>"signalr.hubs' という名前のルートは既にルート コレクションにあります」エラー

このエラーは、アプリケーションによって`MapHubs`2 回呼び出された場合に表示されます。 一部のアプリケーション`MapHubs`例では、グローバル アプリケーション ファイル内で直接呼び出します。他のクラスはラッパークラスで呼び出しを行います。 アプリケーションが両方とも実行しないことを確認します。

<a id="vs"></a>

## <a name="visual-studio-issues"></a>ビジュアルスタジオの問題

このセクションでは、Visual Studio で発生する問題について説明します。

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>ソリューション エクスプローラーに [スクリプト ドキュメント] ノードが表示されない

いくつかのチュートリアルでは、デバッグ中にソリューション エクスプローラーの "スクリプト ドキュメント" ノードに移動します。 このノードは JavaScript デバッガーによって生成され、Internet Explorer でブラウザー クライアントをデバッグしている間のみ表示されます。クロムまたは Firefox を使用している場合、ノードは表示されません。 また、別のクライアント デバッガー (Silverlight デバッガーなど) が実行されている場合、JavaScript デバッガーも実行されません。

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>信号は、Visual Studio 2008 以前では動作しません。

この動作は仕様です。 SignalR は .NET Framework 4 以降を必要とします。このためには、Visual Studio 2010 以降で SignalR アプリケーションを開発する必要があります。

<a id="iis"></a>

## <a name="iis-issues"></a>IIS の問題

ここでは、インターネット インフォメーション サービスに関する問題について説明します。

### <a name="web-site-crashes-after-maphubs-call"></a>MapHubs 呼び出し後に Web サイトがクラッシュする

この問題は、SignalR の最新バージョンで修正されました。 NuGet を使用してインストールを更新して、最新のリリース バージョンの SignalR を使用していることを確認します。

<a id="azure"></a>

## <a name="azure-issues"></a>Azure の問題

このセクションには、Azure に関する問題が含まれています。

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>トピック名を変更した後、Azure バックプレーンを通じてメッセージが受信されない

Azure バックプレーンで使用されるトピックは、ユーザーが構成できるように意図されていません。
