---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET SignalR ハブ API ガイド - サーバー (C#) |マイクロソフトドキュメント
author: bradygaster
description: このドキュメントでは、SignalR バージョン 2 の ASP.NET SignalR Hubs API のサーバー側のプログラミングの概要を示します。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675803"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a>ASP.NET SignalR ハブ API ガイド - サーバー (C#)

[パトリック・フレッチャー](https://github.com/pfletcher),[トム・ダイクストラ](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このドキュメントでは、一般的なオプションを示すコード サンプルを含む、signalR バージョン 2 の ASP.NET SignalR Hubs API のサーバー側のプログラミングの概要を示します。
> 
> SignalR Hubs API を使用すると、サーバーから接続されたクライアント、およびクライアントからサーバーへのリモート プロシージャ コール (RPC) を作成できます。 サーバー コードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行されるメソッドを呼び出します。 クライアント コードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出します。 SignalR は、クライアントからサーバーへのすべての配管を処理します。
> 
> SignalR は、固定接続と呼ばれる下位レベルの API も提供します。 SignalR、ハブ、および固定接続の概要については[、SignalR 2 の概要を](../getting-started/introduction-to-signalr.md)参照してください。
> 
> ## <a name="software-versions-used-in-this-topic"></a>このトピックで使用するソフトウェアバージョン
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - シグナル・バージョン 2
>   
> 
> 
> ## <a name="topic-versions"></a>トピックのバージョン
> 
> SignalR の以前のバージョンについては[、SignalR の古いバージョン](../older-versions/index.md)を参照してください。
> 
> ## <a name="questions-and-comments"></a>質問とコメント
> 
> このチュートリアルを気に入った方法と、ページの下部にあるコメントで改善できる内容についてのフィードバックを残してください。 チュートリアルに直接関連しない質問がある場合は[、ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。

## <a name="overview"></a>概要

このドキュメントは、次のトピックに分かれています。

- [SignalR ミドルウェアを登録する方法](#route)

    - [/シグナルの URL](#signalrurl)
    - [シグナル・オプションの構成](#options)
- [ハブ クラスを作成して使用する方法](#hubclass)

    - [ハブ オブジェクトの有効期間](#transience)
    - [JavaScript クライアントにおけるハブ名のキャメルケーシング](#hubnames)
    - [複数のハブ](#multiplehubs)
    - [厳密に型指定されたハブ](#stronglytypedhubs)
- [クライアントが呼び出すことができるハブ クラスでメソッドを定義する方法](#hubmethods)

    - [JavaScript クライアントにおけるメソッド名のキャメル・ケーシング](#methodnames)
    - [非同期で実行する場合](#asyncmethods)
    - [オーバーロードの定義](#overloads)
    - [ハブ メソッド呼び出しからの進行状況のレポート](#progress)
- [ハブ クラスからクライアント メソッドを呼び出す方法](#callfromhub)

    - [RPC を受信するクライアントの選択](#selectingclients)
    - [メソッド名のコンパイル時検証なし](#dynamicmethodnames)
    - [大文字と小文字を区別しないメソッド名の一致](#caseinsensitive)
    - [非同期実行](#asyncclient)
- [ハブ クラスからグループ メンバーシップを管理する方法](#groupsfromhub)

    - [Add メソッドと Remove メソッドの非同期実行](#asyncgroupmethods)
    - [グループ メンバーシップの永続性](#grouppersistence)
    - [シングルユーザー グループ](#singleusergroups)
- [ハブ クラスで接続の有効期間イベントを処理する方法](#connectionlifetime)

    - [オン接続、オン・オンライン切断、およびオン再接続が呼び出された場合](#onreconnected)
    - [呼び出し元の状態が入力されていません](#nocallerstate)
- [Context プロパティからクライアントに関する情報を取得する方法](#contextproperty)
- [クライアントとハブ クラスの間で状態を渡す方法](#passstate)
- [ハブ クラスのエラーを処理する方法](#handleErrors)
- [ハブ クラスの外部からクライアント メソッドを呼び出し、グループを管理する方法](#callfromoutsidehub)

    - [クライアント メソッドの呼び出し](#callingclientsoutsidehub)
    - [グループ メンバーシップの管理](#managinggroupsoutsidehub)
- [トレースを有効にする方法](#tracing)
- [ハブ パイプラインをカスタマイズする方法](#hubpipeline)

クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。

- [シグナルハブ API ガイド - JavaScript クライアント](hubs-api-guide-javascript-client.md)
- [SignalR ハブ API ガイド - .NET クライアント](hubs-api-guide-net-client.md)

SignalR 2 のサーバー コンポーネントは、.NET 4.5 でのみ使用できます。 NET 4.0 を実行しているサーバーは、SignalR v1.x を使用する必要があります。

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a>SignalR ミドルウェアを登録する方法

クライアントがハブへの接続に使用するルートを定義するには、アプリケーションの起動時`MapSignalR`にメソッドを呼び出します。 `MapSignalR`は、クラスの[拡張メソッド](https://msdn.microsoft.com/library/vstudio/bb383977.aspx)です`OwinExtensions`。 次の例は、OWIN スタートアップ クラスを使用して SignalR ハブ ルートを定義する方法を示しています。

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

ASP.NET MVC アプリケーションに SignalR 機能を追加する場合は、SignalR ルートが他のルートの前に追加されていることを確認します。 詳細については、「[チュートリアル: SignalR 2 と MVC 5 の概要](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)」を参照してください。

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>/シグナルの URL

デフォルトでは、クライアントがハブへの接続に使用するルート URL は"/signalr"です。 (この URL を、自動生成された JavaScript ファイル用の "/signalr/hubs" URL と混同しないでください。 生成されたプロキシの詳細については[、SignalR Hubs API ガイド - JavaScript クライアント - 生成されたプロキシと、それがあなたのために何をするのか](hubs-api-guide-javascript-client.md#genproxy)を参照してください。

このベース URL を SignalR で使用できないという特別な状況が発生する可能性があります。たとえば、プロジェクト内に*signalr*という名前のフォルダーがあり、名前を変更したくないとします。 その場合は、次の例に示すように、ベース URL を変更できます (サンプル コードの "/signalr" を目的の URL に置き換えます)。

**URL を指定するサーバー コード**

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

**URL を指定する JavaScript クライアント コード (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

**URL を指定する JavaScript クライアント コード (生成されたプロキシを除く)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

**URL を指定する .NET クライアント コード**

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>シグナル・オプションの構成

`MapSignalR`メソッドのオーバーロードを使用すると、カスタム URL、カスタム依存関係リゾルバー、および次のオプションを指定できます。

- ブラウザー クライアントからの CORS または JSONP を使用して、クロスドメイン呼び出しを有効にします。

    通常、ブラウザが から`http://contoso.com`ページを読み込む場合、SignalR 接続は`http://contoso.com/signalr`同じドメインの で、 で行われます。 ページが に`http://contoso.com`接続する`http://fabrikam.com/signalr`場合、これはドメイン間接続です。 セキュリティ上の理由から、ドメイン間の接続は既定で無効になっています。 詳細については[、「ASP.NET SignalR Hubs API ガイド - JavaScript クライアント - クロスドメイン接続を確立する方法」](hubs-api-guide-javascript-client.md#crossdomain)を参照してください。
- 詳細なエラー メッセージを有効にします。

    エラーが発生した場合、SignalR の既定の動作では、何が起きたかについての詳細を通知メッセージをクライアントに送信します。 悪意のあるユーザーがアプリケーションに対する攻撃で情報を使用する可能性があるため、クライアントに詳細なエラー情報を送信することは推奨されません。 トラブルシューティングのために、このオプションを使用して、より有益なエラー報告を一時的に有効にすることができます。
- 自動生成された JavaScript プロキシ ファイルを無効にします。

    デフォルトでは、ハブクラスのプロキシを持つ JavaScript ファイルは、URL "/signalr/hubs" に応答して生成されます。 JavaScript プロキシを使用しない場合、またはこのファイルを手動で生成してクライアントの物理ファイルを参照する場合は、このオプションを使用してプロキシ生成を無効にすることができます。 詳細については、「 [SignalR ハブ API ガイド - JavaScript クライアント - SignalR で生成されたプロキシの物理ファイルを作成する方法](hubs-api-guide-javascript-client.md#manualproxy)」を参照してください。

次の例は、SignalR 接続 URL と、メソッドの呼び出し`MapSignalR`でこれらのオプションを指定する方法を示しています。 カスタム URL を指定するには、例の 「/signalr」を使用する URL に置き換えます。

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>ハブ クラスを作成して使用する方法

ハブを作成するには、から派生するクラス[を](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)作成します。 チャット アプリケーションの単純な Hub クラスの例を次に示します。

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

この例では、接続されたクライアントがメソッドを`NewContosoChatMessage`呼び出し、呼び出すと、受信したデータが接続されているすべてのクライアントにブロードキャストされます。

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>ハブ オブジェクトの有効期間

ハブ クラスをインスタンス化したり、サーバー上の独自のコードからそのメソッドを呼び出したりしないでください。SignalR ハブ パイプラインによって行われるすべてのことを示します。 SignalR は、クライアントがサーバーに対して接続、切断、またはメソッド呼び出しを行う場合など、ハブの操作を処理する必要があるたびに、ハブ クラスの新しいインスタンスを作成します。

Hub クラスのインスタンスは一時的なものであるため、メソッド呼び出しから次のメソッド呼び出しの状態を維持するために使用することはできません。 サーバーがクライアントからメソッド呼び出しを受け取るたびに、ハブ クラスの新しいインスタンスがメッセージを処理します。 複数の接続とメソッド呼び出しを通じて状態を維持するには、データベース、ハブ クラスの静的変数、または から`Hub`派生していない別のクラスなど、他のメソッドを使用します。 データをメモリに保持する場合、ハブ クラスの静的変数などのメソッドを使用すると、アプリ ドメインがリサイクルされるときにデータが失われます。

ハブ クラスの外部で実行される独自のコードからクライアントにメッセージを送信する場合は、ハブ クラスインスタンスをインスタンス化して送信することはできませんが、ハブ クラスの SignalR コンテキスト オブジェクトへの参照を取得することで送信できます。 詳細については、このトピックの後半の[「Hub クラスの外部からクライアント メソッドを呼び出し、グループを管理する方法](#callfromoutsidehub)」を参照してください。

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>JavaScript クライアントにおけるハブ名のキャメルケーシング

デフォルトでは、JavaScript クライアントはキャメルケースバージョンのクラス名を使用してハブを参照します。 SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。 前の例は JavaScript`contosoChatHub`コードと呼ばれます。

**[サーバー]**

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

**生成されたプロキシを使用した JavaScript クライアント**

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

クライアントが使用する別の名前を指定する場合は、属性を`HubName`追加します。 属性を`HubName`使用する場合、JavaScript クライアントでキャメル ケースに名前が変更されません。

**[サーバー]**

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

**生成されたプロキシを使用した JavaScript クライアント**

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>複数のハブ

アプリケーションでは、複数のハブ クラスを定義できます。 これを行うと、接続は共有されますが、グループは別々になります。

- すべてのクライアントは、サービスとの SignalR 接続 (指定した場合は "signalr" またはカスタム URL) を確立するために同じ URL を使用し、その接続はサービスによって定義されたすべてのハブに使用されます。

    1 つのクラスですべてのハブ機能を定義するのと比較して、複数のハブのパフォーマンスの違いはありません。
- すべてのハブは同じ HTTP 要求情報を取得します。

    すべてのハブが同じ接続を共有するため、サーバーが取得する唯一の HTTP 要求情報は、SignalR 接続を確立する元の HTTP 要求に含まれるものになります。 接続要求を使用してクエリ文字列を指定してクライアントからサーバーに情報を渡す場合、異なるクエリ文字列を異なるハブに提供することはできません。 すべてのハブは同じ情報を受け取ります。
- 生成された JavaScript プロキシ ファイルには、1 つのファイル内のすべてのハブのプロキシが含まれます。

    JavaScript プロキシの詳細については、「 [SignalR Hubs API ガイド - JavaScript クライアント - 生成されたプロキシと、それがあなたのために何をするのか](hubs-api-guide-javascript-client.md#genproxy)」を参照してください。
- グループはハブ内で定義されます。

    SignalR では、接続されたクライアントのサブセットにブロードキャストする名前付きグループを定義できます。 グループは、ハブごとに個別に管理されます。 たとえば、"Administrators" という名前のグループには`ContosoChatHub`、クラスのクライアントのセットが 1 つ含まれ、同じグループ名がクラスの異なる`StockTickerHub`クライアント セットを参照します。

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a>厳密に型指定されたハブ

クライアントが参照できるハブ メソッドのインターフェイスを定義し (ハブ メソッドで Intellisense を有効にする)、ハブを (SignalR 2.1`Hub`で紹介) ではなくから`Hub<T>`派生させるには、

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>クライアントが呼び出すことができるハブ クラスでメソッドを定義する方法

クライアントから呼び出し可能にするメソッドをハブで公開するには、次の例に示すように、パブリック メソッドを宣言します。

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

C# メソッドの場合と同様に、複合型や配列を含む戻り値の型とパラメーターを指定できます。 パラメーターで受け取ったデータや呼び出し元に返されるデータは、JSON を使用してクライアントとサーバー間で通信され、SignalR は複雑なオブジェクトとオブジェクトの配列のバインドを自動的に処理します。

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>JavaScript クライアントにおけるメソッド名のキャメル・ケーシング

デフォルトでは、JavaScript クライアントは、キャメルケースバージョンのメソッド名を使用してハブメソッドを参照します。 SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。

**[サーバー]**

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**生成されたプロキシを使用した JavaScript クライアント**

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

クライアントが使用する別の名前を指定する場合は、属性を`HubMethodName`追加します。

**[サーバー]**

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**生成されたプロキシを使用した JavaScript クライアント**

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>非同期で実行する場合

メソッドが長時間実行される場合、またはデータベースの参照や Web サービスの呼び出しなど、待機する作業を実行する必要がある場合は、戻り値の代わりに Task オブジェクトまたは[&lt;Task&gt; T](https://msdn.microsoft.com/library/dd321424.aspx)オブジェクトを`T`返してハブ メソッドを非同期にします (戻り値の[Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)`void`型の代わりに)。 メソッドからオブジェクトを`Task`返すと、SignalR は完了`Task`するまで待機し、ラップされていない結果をクライアントに返すため、クライアントでのメソッド呼び出しのコーディング方法に違いはありません。

ハブ メソッドを非同期にすると、WebSocket トランスポートを使用する場合に接続がブロックされないようにします。 ハブ メソッドが同期的に実行され、トランスポートが WebSocket の場合、ハブ メソッドが完了するまで、同じクライアントからハブ上のメソッドの後続の呼び出しがブロックされます。

同期または非同期で実行するコードと同じメソッドの後に、いずれかのバージョンを呼び出すために機能する JavaScript クライアント コードを次の例に示します。

**同期**

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

**非同期**

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**生成されたプロキシを使用した JavaScript クライアント**

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

ASP.NET 4.5 で非同期メソッドを使用する方法の詳細については[、「ASP.NET MVC 4 での非同期メソッドの使用](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)」を参照してください。

<a id="overloads"></a>

### <a name="defining-overloads"></a>オーバーロードの定義

メソッドのオーバーロードを定義する場合は、各オーバーロードのパラメーター数が異なる必要があります。 異なるパラメーター型を指定するだけでオーバーロードを区別する場合、ハブ クラスはコンパイルされますが、クライアントがいずれかのオーバーロードを呼び出そうとする実行時に SignalR サービスによって例外がスローされます。

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a>ハブ メソッド呼び出しからの進行状況のレポート

SignalR 2.1 では、.NET 4.5 で導入された[進行状況レポート パターン](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx)のサポートが追加されました。 進捗レポートを実装するには、`IProgress<T>`クライアントがアクセスできるハブ メソッドのパラメーターを定義します。

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

実行時間の長いサーバー メソッドを記述する場合は、ハブ スレッドをブロックするのではなく、非同期プログラミング パターンを使用することが重要です。

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>ハブ クラスからクライアント メソッドを呼び出す方法

サーバーからクライアント メソッドを呼び出す`Clients`場合は、Hub クラスのメソッドでプロパティを使用します。 接続されているすべてのクライアントで呼び出す`addNewMessageToPage`サーバー コードと、JavaScript クライアントでメソッドを定義するクライアント コードの例を次に示します。

**[サーバー]**

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

クライアント メソッドの呼び出しは非同期操作であり`Task`、 を返します。 `await` を使用して次のことを行います。

* メッセージがエラーなしで送信されることを確認します。 
* try-catch ブロックでエラーのキャッチと処理を有効にします。

**生成されたプロキシを使用した JavaScript クライアント**

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

クライアント メソッドから戻り値を取得することはできません。構文が機能`int x = Clients.All.add(1,1)`しないなどの構文。

パラメーターには、複合型と配列を指定できます。 メソッド パラメーターで複合型をクライアントに渡す例を次に示します。

**複雑なオブジェクトを使用してクライアント メソッドを呼び出すサーバー コード**

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

**複合オブジェクトを定義するサーバー コード**

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

**生成されたプロキシを使用した JavaScript クライアント**

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>RPC を受信するクライアントの選択

プロパティは、RPC を受信するクライアントを指定するためのいくつかのオプションを提供する[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)オブジェクトを返します。

- 接続されたすべてのクライアント。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- 呼び出し元クライアントのみ。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- 呼び出し元のクライアントを除くすべてのクライアント。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- 接続 ID で識別される特定のクライアント。

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    この例では`addContosoChatMessageToPage`、呼び出し元のクライアントを呼び`Clients.Caller`出し、使用するのと同じ効果があります。
- 接続 ID で識別される、指定されたクライアントを除くすべての接続クライアント。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- 指定したグループ内のすべての接続クライアント。

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- 指定されたグループ内のすべての接続クライアント (接続 ID で識別される指定されたクライアントを除く)。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- 呼び出し元のクライアントを除き、指定されたグループ内のすべての接続済みクライアント。

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- ユーザー ID によって識別される特定のユーザー。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    既定では、これは`IPrincipal.Identity.Name`ですが、これは[IUserIdProvider の実装をグローバル ホストに登録](mapping-users-to-connections.md#IUserIdProvider)することで変更できます。
- 接続 ID のリスト内のすべてのクライアントとグループ。

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- グループのリスト。

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- 名前によるユーザー。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- ユーザー名のリスト (SignalR 2.1 で導入)。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>メソッド名のコンパイル時検証なし

指定したメソッド名は動的オブジェクトとして解釈されるため、IntelliSense またはコンパイル時の検証はありません。 式は実行時に評価されます。 メソッド呼び出しが実行されると、SignalR はメソッド名とパラメーター値をクライアントに送信し、クライアントに名前と一致するメソッドがある場合は、そのメソッドが呼び出され、パラメーター値が渡されます。 クライアントで一致するメソッドが見つからない場合、エラーは発生しません。 クライアント メソッドを呼び出すときに、SignalR がクライアントに送信するデータの形式については[、「SignalR の概要](../getting-started/introduction-to-signalr.md)」を参照してください。

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>大文字と小文字を区別しないメソッド名の一致

メソッド名の一致は大文字と小文字を区別しません。 たとえば、`Clients.All.addContosoChatMessageToPage`サーバー上で、 、 `AddContosoChatMessageToPage` `addcontosochatmessagetopage`、または`addContosoChatMessageToPage`をクライアントで実行します。

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>非同期実行

呼び出すメソッドは非同期的に実行されます。 メソッドの呼び出し後に発生するコードは、メソッドの完了を待つ必要があるコードの行を指定しない限り、SignalR がクライアントにデータを送信するのを待たずにすぐに実行されます。 2 つのクライアント メソッドを順番に実行する方法を次のコード例に示します。

**アウェイトの使用 (.NET 4.5)**

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

クライアント メソッド`await`が次のコード行が実行される前に終了するまで待機する場合、クライアントが実際に次のコード行を実行する前にメッセージを受信するわけではありません。 クライアント メソッド呼び出しの "完了" は、SignalR がメッセージの送信に必要な処理をすべて行ったことを意味します。 クライアントがメッセージを受信したことを確認する必要がある場合は、そのメカニズムを自分でプログラミングする必要があります。 たとえば、ハブでメソッドを`MessageReceived`コーディングし、クライアントで必要な作業を`addContosoChatMessageToPage`行った後に呼び出`MessageReceived`すことができるクライアントのメソッドを作成できます。 ハブ`MessageReceived`では、実際のクライアントの受信と元のメソッド呼び出しの処理に依存する任意の作業を行うことができます。

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>メソッド名として文字列変数を使用する方法

文字列変数をメソッド名として使用してクライアント メソッドを呼び出す場合は、 `Clients.All` `Clients.Others` `Clients.Caller` `IClientProxy` [Invoke(メソッド名、args.)をキャストし、Invoke(メソッド名、args.)を](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)呼び出します。

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>ハブ クラスからグループ メンバーシップを管理する方法

SignalR のグループは、接続されたクライアントの指定されたサブセットにメッセージをブロードキャストするためのメソッドを提供します。 グループには任意の数のクライアントを持たることができ、クライアントは任意の数のグループのメンバーになることができます。

グループ メンバーシップを管理するには、Hub[Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)クラスの`Groups`プロパティによって提供される[Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)メソッドと Remove メソッドを使用します。 クライアント コードによって呼`Groups.Add`び`Groups.Remove`出されるハブ メソッドと、それらを呼び出す JavaScript クライアント コードで使用されるメソッドの例を次に示します。

**[サーバー]**

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

**生成されたプロキシを使用した JavaScript クライアント**

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

グループを明示的に作成する必要はありません。 実際には、グループは、 への`Groups.Add`呼び出しで初めて名前を指定したときに自動的に作成され、最後の接続をそのメンバーのメンバーシップから削除すると削除されます。

グループメンバーシップリストまたはグループのリストを取得するための API はありません。 SignalR は[、 pub/sub モデル](http://en.wikipedia.org/wiki/Publish/subscribe)に基づいてクライアントとグループにメッセージを送信しますが、サーバーはグループまたはグループ メンバーシップの一覧を保持しません。 これにより、ノードを Web ファームに追加するたびに、SignalR が維持するすべての状態を新しいノードに伝達する必要があるため、スケーラビリティを最大限に高めます。

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>Add メソッドと Remove メソッドの非同期実行

メソッド`Groups.Add`と`Groups.Remove`メソッドは非同期で実行されます。 クライアントをグループに追加し、そのグループを使用してすぐにクライアントにメッセージを送信する場合は、`Groups.Add`メソッドが最初に終了することを確認する必要があります。 次のコード例は、その方法を示しています。

**グループへのクライアントの追加と、そのクライアントのメッセージング**

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>グループ メンバーシップの永続性

SignalR はユーザーではなく接続を追跡するため、ユーザーが接続を確立するたびに同じグループにユーザーを入れてもらいたい場合は、ユーザーが新しい`Groups.Add`接続を確立するたびに呼び出す必要があります。

接続が一時的に切断された後、SignalR が接続を自動的に復元できることがあります。 その場合、SignalR は、新しい接続を確立せず、同じ接続を復元するため、クライアントのグループ メンバーシップが自動的に復元されます。 これは、一時的な中断がサーバーの再起動または障害の結果である場合でも可能です。 サーバーがダウンし、接続がタイムアウトする前に新しいサーバーに置き換えられた場合、クライアントは自動的に新しいサーバーに再接続し、そのサーバーがメンバーになっているグループに再登録できます。

接続が切断された後に接続を自動的に復元できない場合、または接続がタイムアウトしたとき、またはクライアントが切断されたとき (たとえば、ブラウザーが新しいページに移動した場合など) は、グループ メンバーシップが失われます。 次回ユーザーが接続すると、新しい接続になります。 同じユーザーが新しい接続を確立したときにグループ メンバーシップを維持するには、アプリケーションはユーザーとグループの関連付けを追跡し、ユーザーが新しい接続を確立するたびにグループ メンバーシップを復元する必要があります。

接続と再接続の詳細については、このトピックの後の[「ハブ クラスで接続の有効期間イベントを処理する方法](#connectionlifetime)」を参照してください。

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>シングルユーザー グループ

SignalR を使用するアプリケーションは、通常、ユーザーと接続の間の関連付けを追跡して、メッセージを送信したユーザーと、どのユーザーがメッセージを受信する必要があるかを把握する必要があります。 グループは、その目的で一般的に使用される 2 つのパターンのいずれかで使用されます。

- シングルユーザー グループ。

    グループ名としてユーザー名を指定し、ユーザーが接続または再接続するたびに、グループに現在の接続 ID を追加できます。 グループに送信するユーザーにメッセージを送信します。 この方法の欠点は、グループがユーザーがオンラインかオフラインかを調べる方法を提供しないということです。
- ユーザー名と接続 ID の間の関連付けを追跡します。

    各ユーザー名と 1 つ以上の接続 ID の間の関連付けをディクショナリーまたはデータベースに保管し、ユーザーが接続または切断するたびに保管データを更新することができます。 ユーザーにメッセージを送信するには、接続 ID を指定します。 この方法の欠点は、メモリを多く取る点です。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>ハブ クラスで接続の有効期間イベントを処理する方法

接続の有効期間イベントを処理する一般的な理由は、ユーザーが接続されているかどうかを追跡し、ユーザー名と接続 ID の間の関連付けを追跡することです。 クライアントが接続または切断するときに独自のコードを実行するには、`OnConnected`次`OnDisconnected`の例`OnReconnected`に示すように、Hub クラスの 、、および 仮想メソッドをオーバーライドします。

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>オン接続、オン・オンライン切断、およびオン再接続が呼び出された場合

ブラウザが新しいページに移動するたびに、新しい接続を確立`OnDisconnected``OnConnected`する必要があります。 SignalR は、新しい接続が確立されると、常に新しい接続 ID を作成します。

この`OnReconnected`メソッドは、接続がタイムアウトする前にケーブルが一時的に切断され、再接続された場合など、SignalR が自動的に回復できる接続に一時的な中断が発生した場合に呼び出されます。この`OnDisconnected`メソッドは、クライアントが切断され、ブラウザーが新しいページに移動した場合など、SignalR が自動的に再接続できない場合に呼び出されます。 したがって、特定のクライアントに対して可能な一連`OnConnected`の`OnReconnected`イベント`OnDisconnected`は、 、 、 、 、 、または`OnConnected` `OnDisconnected`、 をクリックします。 指定された接続のシーケンス`OnConnected`、`OnDisconnected`は`OnReconnected`表示されません。

サーバー`OnDisconnected`がダウンしたり、App Domain がリサイクルされたりした場合など、一部のシナリオではこのメソッドは呼び出されません。 別のサーバーがオンラインに接続されたり、App Domain がリサイクルを完了したりすると、一部のクライアントが`OnReconnected`再接続してイベントを発生させる場合があります。

詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](handling-connection-lifetime-events.md)」を参照してください。

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>呼び出し元の状態が入力されていません

接続有効期間イベント ハンドラ メソッドはサーバーから呼び出されるため、クライアント上の`state`オブジェクトに配置した状態は、サーバーの`Caller`プロパティに設定されません。 オブジェクトと`Caller`プロパティの`state`詳細については、このトピックの後半の[「クライアントとハブ クラス間で状態を渡す方法](#passstate)」を参照してください。

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>Context プロパティからクライアントに関する情報を取得する方法

クライアントに関する情報を取得するには、Hub クラスの`Context`プロパティを使用します。 プロパティ`Context`は、次の情報へのアクセスを提供する[HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx)オブジェクトを返します。

- 呼び出し元クライアントの接続 ID。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    接続 ID は、SignalR によって割り当てられる GUID です (独自のコードで値を指定することはできません)。 接続ごとに 1 つの接続 ID があり、アプリケーションに複数のハブがある場合は、すべてのハブで同じ接続 ID が使用されます。
- HTTP ヘッダー データ。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    HTTP ヘッダーを から`Context.Headers`取得することもできます。 同じものに対する複数の参照が最初`Context.Headers`に作成された理由は`Context.Request`、プロパティが後で追加`Context.Headers`され、下位互換性のために保持されたためです。
- クエリ文字列データ。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    クエリ文字列データを から`Context.QueryString`取得することもできます。

    このプロパティで取得するクエリ文字列は、SignalR 接続を確立した HTTP 要求で使用された文字列です。 クライアントからサーバーにクライアントにデータを渡す便利な方法である接続を構成することで、クライアントにクエリ文字列パラメーターを追加できます。 次の例は、生成されたプロキシを使用するときに JavaScript クライアントにクエリ文字列を追加する方法の 1 つを示しています。

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    クエリ文字列パラメーターの設定の詳細については[、JavaScript](hubs-api-guide-javascript-client.md)クライアントと[.NET](hubs-api-guide-net-client.md)クライアントの API ガイドを参照してください。

    クエリ文字列データで接続に使用されるトランスポート 方法と、SignalR によって内部的に使用されるその他の値を見つけることができます。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    の`transportMethod`値は、「ウェブソケット」、「サーバーSentイベント」、「フォーエバーフレーム」または「ロングポーリング」になります。 イベント ハンドラー メソッドでこの値を`OnConnected`チェックする場合、場合によっては、最初に接続の最終的なネゴシエートされたトランスポート 方法ではないトランスポート値を取得する場合があることに注意してください。 その場合、メソッドは例外をスローし、最終的なトランスポート メソッドが確立されたときに、後で再度呼び出されます。
- クッキー。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    からクッキーを取得することもできます`Context.RequestCookies`。
- ユーザー情報。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- 要求の HttpContext オブジェクト:

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    SignalR 接続のオブジェクト`HttpContext.Current`を取得する`HttpContext`代わりに、このメソッドを使用します。

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>クライアントとハブ クラスの間で状態を渡す方法

クライアント プロキシは、`state`メソッド呼び出しごとにサーバーに転送するデータを格納できるオブジェクトを提供します。 サーバーでは、クライアントから呼び出されるハブ`Clients.Caller`メソッドのプロパティでこのデータにアクセスできます。 接続`Clients.Caller`有効期間イベント ハンドラー メソッド`OnConnected`、、`OnDisconnected`および`OnReconnected`のプロパティは設定されません。

オブジェクトとプロパティのデータの`state`作成または更新は`Clients.Caller`、両方向で機能します。 サーバーの値を更新すると、値はクライアントに渡されます。

次の例は、すべてのメソッド呼び出しでサーバーに送信するための状態を格納する JavaScript クライアント コードを示しています。

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

NET クライアントの同等のコードの例を次に示します。

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

ハブ クラスでは、`Clients.Caller`このデータにプロパティからアクセスできます。 前の例で参照されている状態を取得するコードを次の例に示します。

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> 状態を永続化するためのこのメカニズムは、`state`または`Clients.Caller`プロパティに入れるすべてのメソッド呼び出しでラウンド トリップされるため、大量のデータを対象としていません。 ユーザー名やカウンターなどの小さな項目に便利です。

VB.NETまたは厳密に型指定されたハブでは、呼び出し元の状態オブジェクトにアクセス`Clients.Caller`できません。代わりに、(SignalR 2.1 で導入)を使用`Clients.CallerState`してください:

**C での呼び出し元状態の使用#**

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

**呼び出し元の使用状態を Visual Basic で使用する**

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>ハブ クラスのエラーを処理する方法

ハブ クラス のメソッドで発生するエラーを処理するには、まず、 を使用`await`して非同期操作 (クライアント メソッドの呼び出しなど) からの例外を "監視" することを確認します。 次に、次の 1 つ以上の方法を使用します。

- メソッド コードを try-catch ブロックにラップし、例外オブジェクトをログに記録します。 デバッグの目的で、例外をクライアントに送信できますが、セキュリティ上の理由から、運用環境でクライアントに詳細情報を送信することはお勧めできません。
- [メソッドを](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)処理するハブ パイプライン モジュールを作成します。 次の例は、エラーをログに記録するパイプライン モジュールを示し、その後にモジュールを Hubs パイプラインに挿入するコードをStartup.csに示します。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- クラスを`HubException`使用します (SignalR 2 で導入されました)。 このエラーは、どのハブ呼び出しからでもスローできます。 コンストラクター`HubError`は、文字列メッセージと、余分なエラー データを格納するオブジェクトを受け取ります。 SignalR は、例外を自動シリアル化してクライアントに送信します。

    次のコード サンプルは、ハブ呼`HubException`び出し中に スローする方法と、JavaScript クライアントと .NET クライアントで例外を処理する方法を示しています。

    **クラスを示すサーバー コード**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    **ハブでのハブ例外のスローに対する応答を示す JavaScript クライアント コード**

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    **ハブでのハブ例外のスローに対する応答を示す .NET クライアント コード**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

ハブ パイプライン モジュールの詳細については、このトピックの[「Hubs パイプラインをカスタマイズする方法](#hubpipeline)」を参照してください。

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>トレースを有効にする方法

サーバー側トレースを有効にするには、次の例に示すように、Web.config ファイルに system.diagnostics 要素を追加します。

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

Visual Studio でアプリケーションを実行すると、**出力**ウィンドウでログを表示できます。

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>ハブ クラスの外部からクライアント メソッドを呼び出し、グループを管理する方法

ハブ クラスとは異なるクラスからクライアント メソッドを呼び出す場合は、ハブの SignalR コンテキスト オブジェクトへの参照を取得し、それを使用してクライアントのメソッドを呼び出すか、グループを管理します。

次のサンプル`StockTicker`クラスは、コンテキスト オブジェクトを取得し、クラスのインスタンスに格納し、クラス インスタンスを静的プロパティに格納し、シングルトン クラス インスタンスのコンテキストを`updateStockPrice`使用して、という名前`StockTickerHub`の Hub に接続されているクライアントのメソッドを呼び出します。

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

長命オブジェクトでコンテキストを複数回使用する必要がある場合は、参照を 1 回取得して、毎回再び取得するのではなく、それを保存します。 コンテキストを取得すると、SignalR は、ハブ メソッドがクライアント メソッドを呼び出すのと同じ順序でクライアントにメッセージを送信します。 ハブの SignalR コンテキストを使用する方法を示すチュートリアルについては、「 [ASP.NET SignalR を使用したサーバー ブロードキャスト](../getting-started/tutorial-server-broadcast-with-signalr.md)」を参照してください。

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>クライアント メソッドの呼び出し

RPC を受信するクライアントを指定できますが、ハブ クラスから呼び出す場合よりも少ないオプションがあります。 これは、コンテキストがクライアントからの特定の呼び出しに関連付けられていないため、現在の接続 ID`Clients.Others`に関する情報を必要とするメソッド (、`Clients.Caller`または`Clients.OthersInGroup`など) は使用できないからです。 次のオプションを使用できます。

- 接続されたすべてのクライアント。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- 接続 ID で識別される特定のクライアント。

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- 接続 ID で識別される、指定されたクライアントを除くすべての接続クライアント。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- 指定したグループ内のすべての接続クライアント。

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- 指定されたグループ内のすべての接続クライアント (接続 ID で識別される指定されたクライアントを除く)。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

ハブ クラスのメソッドから非ハブ クラスを呼び出す場合は、現在の接続`Clients.Client`ID を渡して、 、、`Clients.AllExcept`または`Clients.Group`、 `Clients.Caller` `Clients.Others`、、`Clients.OthersInGroup`または を使用して、 、 、または を使用できます。 次の例では、クラス`MoveShapeHub`がシミュレートできるように、`Broadcaster`クラスに接続 ID を`Broadcaster`渡`Clients.Others`します。

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>グループ メンバーシップの管理

グループの管理には、ハブ クラスで行うのと同じオプションがあります。

- グループにクライアントを追加する

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- グループからクライアントを削除する

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>ハブ パイプラインをカスタマイズする方法

SignalR を使用すると、ハブ パイプラインに独自のコードを挿入できます。 次の例は、クライアントから受信した各受信メソッド呼び出しと、クライアントで呼び出された送信メソッド呼び出しを記録するカスタム ハブ パイプライン モジュールを示しています。

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

*Startup.cs*ファイルの次のコードは、ハブ パイプラインで実行するモジュールを登録します。

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

オーバーライドできるメソッドは多数あります。 完全なリストについては、「[ハブパイプライン モジュール メソッド](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)」を参照してください。
