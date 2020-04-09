---
uid: signalr/overview/security/introduction-to-security
title: SignalR セキュリティの概要 |マイクロソフトドキュメント
author: bradygaster
description: SignalR アプリケーションを開発する際に考慮する必要があるセキュリティの問題について説明します。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675809"
---
# <a name="introduction-to-signalr-security"></a>SignalR セキュリティ入門

[パトリック・フレッチャー](https://github.com/pfletcher)、[トム・フィッツマッケン](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> この資料では、SignalR アプリケーションを開発する際に考慮する必要があるセキュリティの問題について説明します。
>
> ## <a name="software-versions-used-in-this-topic"></a>このトピックで使用するソフトウェアバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - シグナル・バージョン 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>このトピックの以前のバージョン
>
> SignalR の以前のバージョンについては[、SignalR の古いバージョン](../older-versions/index.md)を参照してください。
>
> ## <a name="questions-and-comments"></a>質問とコメント
>
> このチュートリアルを気に入った方法と、ページの下部にあるコメントで改善できる内容についてのフィードバックを残してください。 チュートリアルに直接関連しない質問がある場合は[、ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。

## <a name="overview"></a>概要

このドキュメントは、次のトピックに分かれています。

- [SignalR セキュリティの概念](#concepts)

    - [認証と権限承認](#authentication)
    - [接続トークン](#connectiontoken)
    - [再接続時にグループに再加入する](#rejoingroup)
- [SignalR がクロスサイトリクエストフォージェリを防ぐ方法](#csrf)
- [SignalR セキュリティに関する推奨事項](#recommendations)

    - [セキュア ソケット レイヤ (SSL) プロトコル](#ssl)
    - [セキュリティ メカニズムとしてグループを使用しない](#groupsecurity)
    - [クライアントからの入力を安全に処理する](#input)
    - [アクティブな接続によるユーザー状況の変更の調整](#reconcile)
    - [自動生成された JavaScript プロキシ ファイル](#autogen)
    - [例外](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>SignalR セキュリティの概念

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>認証と権限承認

SignalR は、ユーザーを認証するための機能を提供しません。 代わりに、アプリケーションの既存の認証構造に SignalR 機能を統合します。 アプリケーションで通常どおりにユーザーを認証し、SignalR コードで認証の結果を処理します。 たとえば、フォーム認証ASP.NETでユーザーを認証し、ハブでメソッドの呼び出しを承認するユーザーまたはロールを強制できます。 ハブでは、ユーザー名やユーザーがロールに属しているかどうかなどの認証情報をクライアントに渡すこともできます。

SignalR は、ハブまたはメソッドにアクセスできるユーザーを指定する[Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)属性を提供します。 ハブまたはハブ内の特定のメソッドのいずれかに Authorize 属性を適用します。 Authorize 属性を指定しない場合、ハブに接続されているクライアントは、ハブ上のすべてのパブリック メソッドを使用できます。 ハブの詳細については[、「SignalR Hubs の認証と承認](hub-authorization.md)」を参照してください。

この属性は`Authorize`ハブに適用しますが、永続的な接続には適用しません。 を使用するときに承認規則を適用`PersistentConnection`するには、メソッドを`AuthorizeRequest`オーバーライドする必要があります。 固定接続について詳しくは[、SignalR 持続接続の認証と承認を](persistent-connection-authorization.md)参照してください。

<a id="connectiontoken"></a>

### <a name="connection-token"></a>接続トークン

SignalR は、送信者の ID を検証することにより、悪意のあるコマンドを実行するリスクを軽減します。 要求ごとに、クライアントとサーバーは、認証されたユーザーの接続 ID とユーザー名を含む接続トークンを渡します。 接続 ID は、接続されている各クライアントを一意に識別します。 サーバーは、新しい接続が作成されたときに接続 ID をランダムに生成し、接続の間その ID を保持します。 Web アプリケーションの認証メカニズムによって、ユーザー名が提供されます。 SignalR は、暗号化とデジタル署名を使用して接続トークンを保護します。

![](introduction-to-security/_static/image2.png)

要求ごとに、サーバーはトークンの内容を検証して、要求が指定されたユーザーから送信されていることを確認します。 ユーザー名は接続 ID に対応している必要があります。SignalR は、接続 ID とユーザー名の両方を検証することにより、悪意のあるユーザーが別のユーザーを簡単に偽装することを防ぎます。 サーバーが接続トークンを検証できない場合、要求は失敗します。

![](introduction-to-security/_static/image4.png)

接続 ID は検証プロセスの一部であるため、他のユーザーへの接続 ID を明らかにしたり、クライアントに値 (Cookie など) を格納したりしないでください。

#### <a name="connection-tokens-vs-other-token-types"></a>接続トークンと他のトークンの種類

接続トークンは、セッション トークンまたは認証トークンのように見えるため、セキュリティ ツールによってフラグが付く場合があります。

SignalR の接続トークンは認証トークンではありません。 この要求を行うユーザーが接続を作成したユーザーと同じであることを確認するために使用されます。 SignalR はサーバー間ASP.NET接続を移動できるため、接続トークンが必要です。 トークンは、接続を特定のユーザーに関連付けますが、要求を行うユーザーの ID をアサートしません。 SignalR 要求を適切に認証するには、Cookie やベアラー トークンなど、ユーザーの ID をアサートする他のトークンが必要です。 ただし、接続トークン自体は、要求がそのユーザーによって行われたことを主張しません。

接続トークンは独自の認証要求を提供しないため、「セッション」または「認証」トークンとは見なされません。 要求のユーザー ID とトークンに格納されている ID が一致しないため、特定のユーザーの接続トークンを取得し、別のユーザー (または認証されていない要求) として認証された要求で再生することは失敗します。

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>再接続時にグループに再加入する

デフォルトでは、接続が切断され、接続がタイムアウトする前に再確立された場合など、一時的な中断から再接続する場合、SignalR アプリケーションはユーザーを適切なグループに自動的に再割り当てします。再接続時に、クライアントは接続 ID と割り当てられたグループを含むグループ トークンを渡します。 グループ トークンは、デジタル署名され、暗号化されます。 クライアントは再接続後も同じ接続 ID を保持します。したがって、再接続されたクライアントから渡される接続 ID は、クライアントが使用していた以前の接続 ID と一致する必要があります。 この検証により、悪意のあるユーザーが、再接続時に承認されていないグループに参加する要求を渡すことを防ぎます。

ただし、グループ トークンの有効期限が切れていないことに注意してください。 ユーザーが過去にグループに属していても、そのグループから禁止されている場合、そのユーザーは禁止されたグループを含むグループ トークンを模倣できる可能性があります。 どのユーザーがどのグループに属しているかを安全に管理する必要がある場合は、そのデータをデータベースなどのサーバーに格納する必要があります。 次に、ユーザーがグループに属しているかどうかをサーバーで確認するロジックをアプリケーションに追加します。 グループ メンバーシップの確認の例については、[グループの操作を](../guide-to-the-api/working-with-groups.md)参照してください。

自動再結合グループは、一時的な中断の後に接続が再接続された場合にのみ適用されます。 ユーザーがアプリケーションから移動して切断したり、アプリケーションが再起動した場合、アプリケーションはそのユーザーを正しいグループに追加する方法を処理する必要があります。 詳細については、[グループの操作を](../guide-to-the-api/working-with-groups.md)参照してください。

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>SignalR がクロスサイトリクエストフォージェリを防ぐ方法

クロスサイト リクエスト フォージェリ (CSRF) は、悪意のあるサイトが、ユーザーが現在ログインしている脆弱なサイトに要求を送信する攻撃です。 SignalR は、悪意のあるサイトが SignalR アプリケーションに対して有効な要求を作成する可能性が非常に低く、CSRF を防ぎます。

### <a name="description-of-csrf-attack"></a>CSRF攻撃の説明

CSRF 攻撃の例を次に示します。

1. ユーザーは、フォーム認証を使用してwww.example.comにログインします。
2. サーバーがユーザーを認証します。 サーバーからの応答には、認証 Cookie が含まれます。
3. ログアウトせずに、ユーザーは悪意のある Web サイトにアクセスします。 この悪質なサイトには、次の HTML フォームが含まれています。

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   フォーム アクションは、悪意のあるサイトではなく、脆弱なサイトに投稿されることに注意してください。 これはCSRFの「クロスサイト」部分です。
4. ユーザーが送信ボタンをクリックします。 ブラウザーには、要求と共に認証 Cookie が含まれます。
5. 要求は、ユーザーの認証コンテキストを持つexample.comサーバー上で実行され、認証されたユーザーが許可されているすべての操作を行うことができます。

この例では、ユーザーがフォーム ボタンをクリックする必要がありますが、悪意のあるページは、SignalR アプリケーションに AJAX 要求を送信するスクリプトを簡単に実行できます。 さらに、悪意のあるサイトが「https://」要求を送信する可能性があるため、SSL を使用しても CSRF 攻撃を防ぐわけではありません。

通常、CSRF攻撃は、ブラウザが宛先のWebサイトに関連するすべてのクッキーを送信するため、認証のためにクッキーを使用するWebサイトに対して可能です。 しかし、CSRF攻撃はクッキーの悪用に限られるものではありません。 たとえば、基本認証とダイジェスト認証も脆弱です。 ユーザーが基本認証またはダイジェスト認証でログインすると、ブラウザーはセッションが終了するまで資格情報を自動的に送信します。

### <a name="csrf-mitigations-taken-by-signalr"></a>シグナルR によって取られた CSRF の軽減策

SignalR は、悪意のあるサイトがアプリケーションに対して有効な要求を作成することを防ぐために、次の手順を実行します。 SignalR はデフォルトでこれらのステップを実行するため、コード内で何も操作を行う必要はありません。

- **クロス ドメイン要求を無効にする**SignalR は、ユーザーが外部ドメインから SignalR エンドポイントを呼び出すことを防ぐために、ドメイン間の要求を無効にします。 SignalR は、外部ドメインからの要求を無効と見なし、要求をブロックします。 この既定の動作はそのままにすることをお勧めします。そうしないと、悪意のあるサイトがユーザーをだましてサイトにコマンドを送信する可能性があります。 クロス ドメイン要求を使用する必要がある場合は、[クロスドメイン接続を確立する方法を](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)参照してください。
- **Cookie ではなくクエリ文字列に接続トークンを渡す**SignalR は、接続トークンをクエリ文字列値として、代わりに、Cookie として渡します。 悪意のあるコードが発生したときに、ブラウザーが誤って接続トークンを転送する可能性があるため、接続トークンを Cookie に格納することは安全ではありません。 また、クエリ文字列で接続トークンを渡すと、接続トークンが現在の接続を超えて保持されなくなります。 したがって、悪意のあるユーザーは、他のユーザーの認証資格情報で要求を行うことはできません。
- **接続トークンの確認**[「接続トークン](#connectiontoken)」セクションで説明したように、サーバーは、認証された各ユーザーに関連付けられている接続 ID を認識します。 サーバーは、ユーザー名と一致しない接続 ID からの要求を処理しません。 悪意のあるユーザーがユーザー名と現在ランダムに生成された接続 ID を知る必要があるため、悪意のあるユーザーが有効な要求を推測する可能性は低いです。接続が終了すると、その接続 ID は無効になります。 匿名ユーザーは、機密情報にアクセスできないようにする必要があります。

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR セキュリティに関する推奨事項

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>セキュア ソケット レイヤ (SSL) プロトコル

SSL プロトコルは、暗号化を使用して、クライアントとサーバー間のデータ転送を保護します。 SignalR アプリケーションがクライアントとサーバー間で機密情報を送信する場合は、トランスポートに SSL を使用します。 SSL の設定の詳細については、「 [IIS 7 で SSL をセットアップする方法](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)」を参照してください。

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>セキュリティ メカニズムとしてグループを使用しない

グループは関連ユーザーを収集する便利な方法ですが、機密情報へのアクセスを制限する安全なメカニズムではありません。 これは、ユーザーが再接続中に自動的にグループに再参加できる場合に特に当てはまります。 代わりに、特権ユーザーをロールに追加し、ハブ メソッドへのアクセスをそのロールのメンバーのみに制限することを検討してください。 ロールに基づくアクセスを制限する例については[、SignalR Hubs の認証と承認を](hub-authorization.md)参照してください。 再接続時にグループへのユーザー アクセスを確認する例については、[グループの操作を](../guide-to-the-api/working-with-groups.md)参照してください。

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>クライアントからの入力を安全に処理する

悪意のあるユーザーが他のユーザーにスクリプトを送信しないようにするには、他のクライアントへのブロードキャストを目的としたクライアントからの入力をすべてエンコードする必要があります。 SignalR アプリケーションにはさまざまな種類のクライアントが含まれているため、サーバーではなく受信側クライアントでメッセージをエンコードする必要があります。 したがって、HTML エンコーディングは Web クライアントでは機能しますが、他の種類のクライアントでは機能しません。 たとえば、チャット メッセージを表示する Web クライアント メソッドは、関数を呼び出すことによってユーザー`html()`名とメッセージを安全に処理します。

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>アクティブな接続によるユーザー状況の変更の調整

アクティブな接続が存在する間にユーザーの認証ステータスが変化すると、ユーザーは"アクティブ SignalR 接続中にユーザー ID を変更することはできません" というエラーを受け取ります。 その場合、アプリケーションは、接続 ID とユーザー名が調整されていることを確認するために、サーバーに再接続する必要があります。 たとえば、アクティブな接続が存在している間にアプリケーションがユーザーのログアウトを許可している場合、接続のユーザー名は、次の要求に渡された名前と一致しなくなります。 ユーザーがログアウトする前に接続を停止してから、接続を再開します。

ただし、ほとんどのアプリケーションは手動で接続を停止および開始する必要はありません。 Web フォーム アプリケーションや MVC アプリケーションの既定の動作など、ログアウト後にアプリケーションがユーザーを別のページにリダイレクトしたり、ログアウト後に現在のページを更新したりすると、アクティブな接続は自動的に切断され、追加の操作は必要ありません。

次の例は、ユーザーの状況が変更されたときに接続を停止および開始する方法を示しています。

[!code-html[Main](introduction-to-security/samples/sample3.html)]

または、サイトでフォーム認証でスライディング有効期限を使用し、認証 Cookie を有効に保つアクティビティがない場合、ユーザーの認証ステータスが変わることがあります。 その場合、ユーザーはログアウトされ、ユーザー名は接続トークンのユーザー名と一致しなくなります。 この問題を解決するには、認証 Cookie を有効に保つために Web サーバー上のリソースを定期的に要求するスクリプトを追加します。 次の例は、30 分ごとにリソースを要求する方法を示しています。

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>自動生成された JavaScript プロキシ ファイル

各ユーザーの JavaScript プロキシ ファイルにすべてのハブとメソッドを含めたくない場合は、ファイルの自動生成を無効にできます。 複数のハブとメソッドを使用していて、すべてのユーザーがすべてのメソッドを認識しないようにする場合は、このオプションを選択できます。 自動生成を無効にするには **、無効****に設定**します。

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

JavaScript プロキシ ファイルの詳細については、[生成されたプロキシと、そのプロキシがあなたのために何をするのかを](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)参照してください。 <a id="exceptions"></a>

### <a name="exceptions"></a>例外

オブジェクトがクライアントに機密情報を公開する可能性があるため、例外オブジェクトはクライアントに渡さないようにしてください。 代わりに、関連するエラー メッセージを表示するクライアントのメソッドを呼び出します。

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
