---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET SignalR ハブ API ガイド - .NET クライアント (C#) |マイクロソフトドキュメント
author: bradygaster
description: このドキュメントでは、Windows ストア (WinRT)、WPF、シルバーライト、および短所などの .NET クライアントで SignalR バージョン 2 のハブ API を使用する方法の概要を示します。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675929"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a>ASP.NET SignalR ハブ API ガイド - .NET クライアント (C#)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このドキュメントでは、Windows ストア (WinRT)、WPF、Silverlight、コンソール アプリケーションなどの .NET クライアントで SignalR バージョン 2 のハブ API を使用する方法の概要を示します。
>
> SignalR Hubs API を使用すると、サーバーから接続されたクライアント、およびクライアントからサーバーへのリモート プロシージャ コール (RPC) を作成できます。 サーバー コードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行されるメソッドを呼び出します。 クライアント コードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出します。 SignalR は、クライアントからサーバーへのすべての配管を処理します。
>
> SignalR は、固定接続と呼ばれる下位レベルの API も提供します。 SignalR、ハブ、および永続的接続の概要、または完全な SignalR アプリケーションを構築する方法を示すチュートリアルについては[、「SignalR - はじめに](../getting-started/index.md)」を参照してください。
>
> ## <a name="software-versions-used-in-this-topic"></a>このトピックで使用するソフトウェアバージョン
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
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

- [クライアントのセットアップ](#clientsetup)
- [接続を確立する方法](#establishconnection)

    - [シルバーライト クライアントからのドメイン間接続](#slcrossdomain)
- [接続の構成方法](#configureconnection)

    - [WPF クライアントで同時接続の最大数を設定する方法](#maxconnections)
    - [クエリ文字列パラメーターの指定方法](#querystring)
    - [トランスポート方法の指定方法](#transport)
    - [HTTP ヘッダーの指定方法](#httpheaders)
    - [クライアント証明書の指定方法](#clientcertificate)
- [ハブ プロキシを作成する方法](#proxy)
- [サーバーが呼び出すことができるクライアント上のメソッドを定義する方法](#callclient)

    - [パラメータを持たないメソッド](#clientmethodswithoutparms)
    - [パラメーターを持つメソッド, パラメーターの型を指定します。](#clientmethodswithparmtypes)
    - [パラメータを持つメソッド、パラメータの動的オブジェクトを指定する](#clientmethodswithdynamparms)
    - [ハンドラを削除する方法](#removehandler)
- [クライアントからサーバー メソッドを呼び出す方法](#callserver)
- [接続の有効期間イベントを処理する方法](#connectionlifetime)
- [エラーの処理方法](#handleerrors)
- [クライアント側のログを有効にする方法](#logging)
- [サーバーが呼び出すことができるクライアント メソッドの WPF、Silverlight、およびコンソール アプリケーションのコード サンプル](#wpfsl)

サンプル .NET クライアント プロジェクトについては、次のリソースを参照してください。

- [GitHub.com上のグスタボ-アルメンタ/ SignalR-サンプル](https://github.com/gustavo-armenta/SignalR-Samples)(WinRT、シルバーライト、コンソール アプリの例)。
- [ダミアンエドワーズ / シグナル伝達機動図形デモ / GitHub.com上の図形の移動.デスクトップ](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop)(WPF の例)。
- GitHub.com上のシグナル / [Microsoft.AspNet.SignalR.Client.サンプル](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples)(コンソール アプリの例)。

サーバーまたは JavaScript クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。

- [シグナルハブ API ガイド - サーバー](hubs-api-guide-server.md)
- [シグナルハブ API ガイド - JavaScript クライアント](hubs-api-guide-javascript-client.md)

API リファレンストピックへのリンクは、API の .NET 4.5 バージョンに関するトピックです。 .NET 4 を使用している場合は[、API のトピックの .NET 4 バージョンを](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)参照してください。

<a id="clientsetup"></a>

## <a name="client-setup"></a>クライアントのセットアップ

[パッケージではなく、Microsoft.AspNet.SignalR.クライアント](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client)の NuGet[Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)パッケージをインストールします。 このパッケージは、.NET 4 と .NET 4.5 の両方に対して、WinRT、シルバーライト、WPF、コンソール アプリケーション、および Windows Phone クライアントをサポートします。

クライアント上の SignalR のバージョンがサーバー上のバージョンと異なる場合、SignalR は多くの場合、その違いに適応できます。 たとえば、SignalR バージョン 2 を実行しているサーバーは、1.1.x がインストールされているクライアントと、バージョン 2 がインストールされているクライアントをサポートします。 サーバー上のバージョンとクライアントのバージョンの違いが大きすぎる場合、またはクライアントがサーバーよりも新しい場合、SignalR はクライアントが接続を確立`InvalidOperationException`しようとしたときに例外をスローします。 エラー メッセージは`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`" " です。

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>接続を確立する方法

接続を確立する前に、`HubConnection`オブジェクトを作成してプロキシを作成する必要があります。 接続を確立するには、オブジェクトの`Start`メソッドを`HubConnection`呼び出します。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> JavaScript クライアントの場合は、`Start`接続を確立するためにメソッドを呼び出す前に、少なくとも 1 つのイベント ハンドラーを登録する必要があります。 これは .NET クライアントには必要ありません。 JavaScript クライアントの場合、生成されたプロキシ コードは、サーバー上に存在するすべてのハブのプロキシを自動的に作成し、ハンドラーを登録すると、クライアントが使用する対象のハブを示す方法が示されます。 しかし、.NET クライアントの場合はハブ プロキシを手動で作成するので、SignalR はプロキシを作成するハブを使用すると想定します。

サンプル コードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。 別のベース URL を指定する方法については、「 [signalr Hubs API ガイド ASP.NET - サーバー - /signalr URL](hubs-api-guide-server.md#signalrurl)」を参照してください。

メソッド`Start`は非同期的に実行されます。 接続が確立されるまで以降のコード行が実行されないようにするには、ASP.NET 4.5 非同期`await`メソッドまたは`.Wait()`同期メソッドで使用します。 WinRT クライアント`.Wait()`では使用しないでください。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>シルバーライト クライアントからのドメイン間接続

Silverlight クライアントからのドメイン間接続を有効にする方法については、「[ドメイン境界を越えてサービスを利用できるようにする](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)」を参照してください。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>接続の構成方法

接続を確立する前に、次のオプションを指定できます。

- 同時接続数の制限。
- クエリ文字列パラメーター。
- トランスポート方法。
- HTTP ヘッダー。
- クライアント証明書。

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>WPF クライアントで同時接続の最大数を設定する方法

WPF クライアントでは、同時接続の最大数を既定値の 2 から増やす必要がある場合があります。 推奨値は 10 です。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

詳細については、「サービス[ポイント マネージャー.既定の接続制限](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)」を参照してください。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>クエリ文字列パラメーターの指定方法

クライアントが接続するときにサーバーにデータを送信する場合は、接続オブジェクトにクエリ文字列パラメーターを追加できます。 クライアント コードでクエリ文字列パラメーターを設定する方法を次の例に示します。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

サーバー コードでクエリ文字列パラメーターを読み取る方法を次の例に示します。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>トランスポート方法の指定方法

SignalR クライアントは、接続プロセスの一部として、通常、サーバーとネゴシエートして、サーバーとクライアントの両方でサポートされている最適なトランスポートを決定します。 使用するトランスポートが既にわかっている場合は、このネゴシエーション プロセスをバイパスできます。 トランスポート メソッドを指定するには、トランスポート オブジェクトを Start メソッドに渡します。 クライアント コードでトランスポート メソッドを指定する方法を次の例に示します。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

名前空間[には、トランスポート](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)を指定するために使用できる次のクラスが含まれています。

- [ロングポーリングトランスポート](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [トランスポート](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocket トランスポート](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx)(サーバーとクライアントの両方が .NET 4.5 を使用する場合にのみ使用できます)。
- [自動トランスポート](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx)(クライアントとサーバーの両方でサポートされている最適なトランスポートを自動的に選択します。 これがデフォルトのトランスポートです。 メソッドにこれを`Start`渡すことは、何も渡さないのと同じ効果があります)。

ForeverFrame トランスポートはブラウザーでのみ使用されるため、このリストには含まれません。

サーバー コードでトランスポート メソッドを確認する方法については、「 [ASP.NET SignalR Hubs API ガイド - サーバー - Context プロパティからクライアントに関する情報を取得する方法](hubs-api-guide-server.md#contextproperty)」を参照してください。 トランスポートとフォールバックの詳細については、「 [SignalR の概要 - トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>HTTP ヘッダーの指定方法

HTTP ヘッダーを設定するには、接続`Headers`オブジェクトのプロパティを使用します。 HTTP ヘッダーを追加する方法を次の例に示します。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>クライアント証明書の指定方法

クライアント証明書を追加するには、接続オブジェクト`AddClientCertificate`でメソッドを使用します。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>ハブ プロキシを作成する方法

ハブがサーバーから呼び出すことができるクライアント上のメソッドを定義し、サーバーのハブでメソッドを呼び出すには、接続オブジェクトを呼び出`CreateHubProxy`すことによってハブのプロキシを作成します。 渡す`CreateHubProxy`文字列は、ハブ クラスの名前、またはサーバーで使用されている場合は`HubName`、属性で指定された名前です。 名前が一致するかどうかを判断する際、大文字と小文字は区別されません。

**サーバー上のハブ クラス**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**ハブ クラスのクライアント プロキシを作成する**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

属性を使用してハブ クラスを修飾`HubName`する場合は、その名前を使用します。

**サーバー上のハブ クラス**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**ハブ クラスのクライアント プロキシを作成する**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

同じ`HubConnection.CreateHubProxy`で複数回呼び出`hubName`すと、同じキャッシュ オブジェクト`IHubProxy`が取得されます。

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>サーバーが呼び出すことができるクライアント上のメソッドを定義する方法

サーバーが呼び出すことができるメソッドを定義するには、プロキシの`On`メソッドを使用してイベント ハンドラーを登録します。

メソッド名の一致は大文字と小文字を区別しません。 たとえば、`Clients.All.UpdateStockPrice`サーバー上で、 、 `updateStockPrice` `updatestockprice`、または`UpdateStockPrice`をクライアントで実行します。

クライアント プラットフォームによって、UI を更新するメソッド コードの記述方法に関する要件が異なります。 表示される例は、WinRT (Windows ストア .NET) クライアント用です。 WPF、Silverlight、およびコンソール アプリケーションの例については、[このトピックの後半で説明します](#wpfsl)。

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>パラメータを持たないメソッド

処理するメソッドにパラメーターがない場合は、メソッドの非ジェネリック オーバーロードを`On`使用します。

**パラメータを指定せずにクライアント メソッドを呼び出すサーバー コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**パラメーターを指定せずにサーバーから呼び出されるメソッドの WinRT クライアント コード ([このトピックの後半の「 WPF および Silverlight](#wpfsl)の例 」 を参照してください ) 。**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>パラメーターを持つメソッド(パラメーターの型を指定する)

処理するメソッドにパラメーターがある場合は、パラメーターの型を`On`メソッドのジェネリック型として指定します。 最大 8 個の`On`パラメーター (Windows Phone 7 では 4) を指定できるようにするメソッドのジェネリック オーバーロードがあります。 次の例では、1 つのパラメーターがメソッド`UpdateStockPrice`に送信されます。

**パラメーターを使用してクライアント メソッドを呼び出すサーバー コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**パラメータに使用される Stock クラス**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**パラメーターを使用してサーバーから呼び出されるメソッドの WinRT クライアント コード ([このトピックの後半の WPF および Silverlight の例を参照](#wpfsl)してください)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>パラメータを持つメソッド、パラメータの動的オブジェクトを指定する

`On`メソッドのジェネリック型としてパラメーターを指定する代わりに、動的オブジェクトとしてパラメーターを指定できます。

**パラメーターを使用してクライアント メソッドを呼び出すサーバー コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**パラメータに使用される Stock クラス**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**パラメーターに動的オブジェクトを使用して、パラメーターを使用してサーバーから呼び出されるメソッドの WinRT クライアント コード ([WPF および Silverlight](#wpfsl)の例を参照してください ) 。**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>ハンドラを削除する方法

ハンドラーを削除するには、そのメソッド`Dispose`を呼び出します。

**サーバーから呼び出されたメソッドのクライアント コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**ハンドラを削除するクライアント コード**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>クライアントからサーバー メソッドを呼び出す方法

サーバー上のメソッドを呼び出す場合`Invoke`は、ハブ プロキシでメソッドを使用します。

サーバー メソッドに戻り値がない場合は、メソッドの非ジェネリック オーバーロード`Invoke`を使用します。

**戻り値のないメソッドのサーバー コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**戻り値のないメソッドを呼び出すクライアント コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

サーバー メソッドに戻り値がある場合は、`Invoke`戻り値の型をメソッドのジェネリック型として指定します。

**戻り値を持ち、複合型パラメーターを受け取るメソッドのサーバー コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**パラメータと戻り値に使用される Stock クラス**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**ASP.NET 4.5 非同期メソッドで、戻り値を持ち、複合型パラメーターを受け取るメソッドを呼び出すクライアント コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**クライアント コード呼び出しメソッドの戻り値を持ち、複合型パラメーターを受け取るメソッドを同期メソッドで受け取ります。**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

この`Invoke`メソッドは非同期的に実行され`Task`、オブジェクトを返します。 または`await``.Wait()`を指定しない場合、呼び出すメソッドの実行が完了する前に、次のコード行が実行されます。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>接続の有効期間イベントを処理する方法

SignalR は、次の接続有効期間イベントを処理できます。

- `Received`: 接続でデータが受信されたときに発生します。 受信したデータを提供します。
- `ConnectionSlow`: クライアントが低速または頻繁に切断する接続を検出したときに発生します。
- `Reconnecting`: 基になるトランスポートの再接続が開始されたときに発生します。
- `Reconnected`: 基になるトランスポートが再接続されたときに発生します。
- `StateChanged`: 接続状態が変化したときに発生します。 古い状態と新しい状態を提供します。 接続状態の値の詳細については、「[接続状態の列挙 」](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)を参照してください。
- `Closed`: 接続が切断されたときに発生します。

たとえば、致命的ではないが断続的な接続の問題 (接続の低速化や頻繁な切断など) を引き起こすエラーに関する警告メッセージ`ConnectionSlow`を表示する場合は、イベントを処理します。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](handling-connection-lifetime-events.md)」を参照してください。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>エラーの処理方法

サーバーで詳細なエラー メッセージを明示的に有効にしない場合、SignalR がエラーの後に返す例外オブジェクトには、エラーに関する最小限の情報が含まれます。 たとえば、呼び出しが`newContosoChatMessage`失敗した場合、エラー オブジェクトのエラー メッセージ`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`には、セキュリティ上の理由から、運用環境のクライアントに詳細なエラー メッセージを送信することは推奨されませんが、トラブルシューティングの目的で詳細なエラー メッセージを有効にする場合は、サーバーで次のコードを使用します。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

SignalR が発生するエラーを処理するには、接続オブジェクトのイベントの`Error`ハンドラーを追加できます。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

メソッド呼び出しのエラーを処理するには、コードを try-catch ブロックでラップします。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>クライアント側のログを有効にする方法

クライアント側のログを有効にするには、接続`TraceLevel`オブジェクト`TraceWriter`の プロパティと プロパティを設定します。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>サーバーが呼び出すことができるクライアント メソッドの WPF、Silverlight、およびコンソール アプリケーションのコード サンプル

サーバーが呼び出すことができるクライアント メソッドを定義するコード サンプルは、WinRT クライアントに適用されます。 次のサンプルは、WPF、Silverlight、およびコンソール アプリケーション クライアントの同等のコードを示しています。

### <a name="methods-without-parameters"></a>パラメータを持たないメソッド

**パラメーターを指定せずにサーバーから呼び出されるメソッドの WPF クライアント コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**パラメータを指定せずにサーバーから呼び出されるメソッドの Silverlight クライアント コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**パラメーターを指定せずにサーバーから呼び出されるメソッドのコンソール アプリケーション クライアント コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>パラメーターを持つメソッド(パラメーターの型を指定する)

**パラメーターを指定してサーバーから呼び出されるメソッドの WPF クライアント コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**パラメーターを指定してサーバーから呼び出されるメソッドの Silverlight クライアント コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**パラメーターを指定してサーバーから呼び出されるメソッドのコンソール アプリケーション クライアント コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>パラメータを持つメソッド、パラメータの動的オブジェクトを指定する

**パラメーターに動的オブジェクトを使用して、パラメーターを使用してサーバーから呼び出されるメソッドの WPF クライアント コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**パラメータを使用してサーバーから呼び出されるメソッドの Silverlight クライアント コードで、パラメータに動的オブジェクトを使用します。**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**パラメーターに対する動的オブジェクトを使用して、パラメーターを指定してサーバーから呼び出されるメソッドのコンソール アプリケーション クライアント コード**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
