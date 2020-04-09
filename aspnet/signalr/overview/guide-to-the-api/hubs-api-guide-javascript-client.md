---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NETシグナルハブ API ガイド - JavaScript クライアント |マイクロソフトドキュメント
author: bradygaster
description: このドキュメントでは、ブラウザーや Windows ストア (WinJS) アプリなど、JavaScript クライアントで SignalR バージョン 2 のハブ API を使用する方法の概要を説明します。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675713"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NETシグナルハブ API ガイド - JavaScript クライアント

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このドキュメントでは、ブラウザーや Windows ストア (WinJS) アプリケーションなどの JavaScript クライアントでの SignalR バージョン 2 のハブ API の使用の概要を説明します。
>
> SignalR Hubs API を使用すると、サーバーから接続されたクライアント、およびクライアントからサーバーへのリモート プロシージャ コール (RPC) を作成できます。 サーバー コードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行されるメソッドを呼び出します。 クライアント コードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出します。 SignalR は、クライアントからサーバーへのすべての配管を処理します。
>
> SignalR は、固定接続と呼ばれる下位レベルの API も提供します。 SignalR、ハブ、および固定接続の概要については[、SignalR の概要を](../getting-started/introduction-to-signalr.md)参照してください。
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

- [生成されたプロキシと、それがあなたのために何をするのか](#genproxy)

    - [生成されたプロキシを使用する場合](#cantusegenproxy)
- [クライアントのセットアップ](#clientsetup)

    - [動的に生成されたプロキシを参照する方法](#dynamicproxy)
    - [SignalR が生成したプロキシの物理ファイルを作成する方法](#manualproxy)
- [接続を確立する方法](#establishconnection)

    - [ハブは、$.hubConnection()が作成するオブジェクトと同じオブジェクトです。](#connequivalence)
    - [開始メソッドの非同期実行](#asyncstart)
- [ドメイン間接続を確立する方法](#crossdomain)
- [接続の構成方法](#configureconnection)

    - [クエリ文字列パラメーターの指定方法](#querystring)
    - [トランスポート方法の指定方法](#transport)
- [ハブ クラスのプロキシを取得する方法](#getproxy)
- [サーバーが呼び出すことができるクライアント上のメソッドを定義する方法](#callclient)
- [クライアントからサーバー メソッドを呼び出す方法](#callserver)
- [接続の有効期間イベントを処理する方法](#connectionlifetime)
- [エラーの処理方法](#handleerrors)
- [クライアント側のログを有効にする方法](#logging)

サーバーまたは .NET クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。

- [シグナルハブ API ガイド - サーバー](hubs-api-guide-server.md)
- [SignalR ハブ API ガイド - .NET クライアント](hubs-api-guide-net-client.md)

SignalR 2 サーバー コンポーネントは 、.NET 4.5 でのみ使用できます (ただし、.NET 4.0 の SignalR 2 用の .NET クライアントがあります)。

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>生成されたプロキシと、それがあなたのために何をするのか

SignalR が自動的に生成するプロキシの有無にかかわらず、SignalR サービスと通信するように JavaScript クライアントをプログラムできます。 プロキシが行うことは、接続、サーバーが呼び出すメソッドの記述、およびサーバー上のメソッドの呼び出しに使用するコードの構文を簡略化することです。

サーバー メソッドを呼び出すコードを記述すると、生成されたプロキシを使用して、ローカル関数を実行しているかのように見える構文を使用できます`serverMethod(arg1, arg2)``invoke('serverMethod', arg1, arg2)`。 生成されたプロキシ構文は、サーバーメソッド名を誤って入力した場合に、即座にわかりやすく、クライアント側エラーを可能にします。 プロキシを定義するファイルを手動で作成した場合は、サーバー メソッドを呼び出すコードの記述に対する IntelliSense のサポートも取得できます。

たとえば、サーバー上に次のハブ クラスがあるとします。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

次のコード例は、サーバー上で`NewContosoChatMessage`メソッドを呼び出し、サーバーからメソッドの呼び出しを`addContosoChatMessageToPage`受け取る JavaScript コードの例を示しています。

**生成されたプロキシを使用する場合**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**生成されたプロキシを使用しない**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>生成されたプロキシを使用する場合

サーバーが呼び出すクライアント メソッドに対して複数のイベント ハンドラーを登録する場合は、生成されたプロキシを使用できません。 それ以外の場合は、生成されたプロキシを使用するか、コーディングの設定に基づいて使用しないようにするかを選択できます。 使用しない場合は、クライアント コードの要素で "signalr/hubs" URL を`script`参照する必要はありません。

<a id="clientsetup"></a>

## <a name="client-setup"></a>クライアントのセットアップ

JavaScript クライアントは、jQuery とシグナルのコア JavaScript ファイルへの参照を必要とします。 jQuery バージョンは、1.7.2、1.8.2、1.9.1 などの 1.6.4 またはそれ以降のメジャー バージョンである必要があります。 生成されたプロキシを使用する場合は、SignalR が生成したプロキシ JavaScript ファイルへの参照も必要です。 生成されたプロキシを使用する HTML ページでの参照の例を次に示します。

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

これらの参照は、jQuery の最初、その後の SignalR コア、および SignalR プロキシの最後の順序で含める必要があります。

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>動的に生成されたプロキシを参照する方法

前の例では、SignalR が生成したプロキシへの参照は、物理ファイルではなく、動的に生成された JavaScript コードです。 SignalR は、プロキシの JavaScript コードをその場で作成し、"/signalr/hubs" URL に応答してクライアントに提供します。 メソッドでサーバー上の SignalR 接続に別のベース URL`MapSignalR`を指定した場合、動的に生成されるプロキシ ファイルの URL は、カスタム URL に "/hubs" が付加された URL です。

> [!NOTE]
> Windows 8 (Windows ストア) JavaScript クライアントの場合は、動的に生成されたプロキシ ファイルではなく、物理プロキシ ファイルを使用します。 詳細については、このトピックの後半の[「SignalR で生成されたプロキシの物理ファイルを作成する方法](#manualproxy)」を参照してください。

ASP.NET MVC 4 または 5 の Razor ビューでは、プロキシ ファイルの参照でアプリケーション ルートを参照するチルダを使用します。

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

MVC 5 で SignalR を使用する方法の詳細については[、「SignalR と MVC 5 の概要](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)」を参照してください。

ASP.NET MVC 3 の Razor`Url.Content`ビューで、プロキシ ファイルの参照に使用します。

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

ASP.NET Web フォーム アプリケーションで`ResolveClientUrl`、プロキシ ファイルの参照に使用するか、またはアプリルートの相対パス (チルダから始まる) を使用して ScriptManager を使用して登録します。

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

一般的な規則として、CSS ファイルまたは JavaScript ファイルに使用する 「/signalr/hubs」URL を指定する場合と同じ方法を使用します。 チルダを使用せずに URL を指定した場合、IIS Express を使用して Visual Studio でテストを行うとアプリケーションが正常に動作する場合がありますが、IIS を完全に展開すると 404 エラーが発生します。 詳細については、MSDN サイトの「Visual Studio の[Web サーバーでの、ASP.NET Web プロジェクトの](https://msdn.microsoft.com/library/58wxa9w5.aspx)**ルート レベルのリソースへの参照の解決**」を参照してください。

デバッグ モードで Visual Studio 2017 で Web プロジェクトを実行し、ブラウザーとして Internet Explorer を使用する場合は、**ソリューション エクスプ ローラー**の**スクリプト**の下にプロキシ ファイルを表示できます。

ファイルの内容を表示するには、**ハブ**をダブルクリックします。 Visual Studio 2012 または 2013 と Internet Explorer を使用していない場合、またはデバッグ モードでない場合は、"/signalR/hubs" URL を参照してファイルの内容を取得することもできます。 たとえば、サイトが で`http://localhost:56699`実行されている場合は、ブラウザ`http://localhost:56699/SignalR/hubs`で に移動します。

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>SignalR が生成したプロキシの物理ファイルを作成する方法

動的に生成されるプロキシの代わりに、プロキシ コードを持つ物理ファイルを作成し、そのファイルを参照することもできます。 キャッシュやバンドルの動作を制御したり、サーバー メソッドへの呼び出しをコーディングするときに IntelliSense を取得したりするために、これを行う必要があります。

プロキシ ファイルを作成するには、次の手順を実行します。

1. [パッケージを](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)インストールします。
2. コマンド プロンプトを開き、SignalR.exe ファイルが含まれている*ツール*フォルダーを参照します。 ツール フォルダは次の場所にあります。

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. 次のコマンドを入力します。

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    *.dll*へのパスは、通常、プロジェクト フォルダー内の*bin*フォルダーです。

    このコマンドは *、signalr.exe*と同じフォルダーに*server.js*という名前のファイルを作成します。
4. プロジェクトの適切なフォルダーに*server.js*ファイルを配置し、アプリケーションに合わせて名前を変更し、"signalr/hubs" 参照の代わりにそのファイルへの参照を追加します。

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>接続を確立する方法

接続を確立する前に、接続オブジェクトを作成し、プロキシを作成し、サーバーから呼び出すことができるメソッドのイベント ハンドラーを登録する必要があります。 プロキシ ハンドラとイベント ハンドラを設定したら、メソッドを呼び出`start`して接続を確立します。

生成されたプロキシを使用している場合は、生成されたプロキシ コードが自動的に行うため、独自のコードで接続オブジェクトを作成する必要はありません。

<a id="nogenconnection"></a>

**(生成されたプロキシとの) 接続の確立**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**(生成されたプロキシを使用せずに) 接続を確立する**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

サンプル コードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。 別のベース URL を指定する方法については、「 [signalr Hubs API ガイド ASP.NET - サーバー - /signalr URL](hubs-api-guide-server.md#signalrurl)」を参照してください。

デフォルトでは、ハブの場所は現在のサーバーです。別のサーバーに接続している場合は、次の例に示すように、`start`メソッドを呼び出す前に URL を指定します。

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> 通常は、メソッドを呼び出して`start`接続を確立する前に、イベント ハンドラーを登録します。 接続を確立した後にイベント ハンドラーを登録する場合は、その操作を行うことができますが、メソッドを呼び出す前に、少なくとも 1`start`つのイベント ハンドラーを登録する必要があります。 その理由の 1 つは、アプリケーションに多数のハブが存在する可能性がありますが、1 つのハブにしか`OnConnected`使用しない場合は、すべてのハブでイベントをトリガーしたくないということです。 接続が確立されると、ハブのプロキシにクライアント メソッドが存在すると、SignalR にイベントをトリガーするように指示されます`OnConnected`。 メソッドを呼び出す前にイベント ハンドラーを`start`登録しない場合、ハブでメソッドを呼び出すことはできますが、ハブの`OnConnected`メソッドは呼び出されず、サーバーからクライアント メソッドは呼び出されません。

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>ハブは、$.hubConnection()が作成するオブジェクトと同じオブジェクトです。

例からわかるように、生成されたプロキシを使用すると、`$.connection.hub`接続オブジェクトを参照します。 これは、生成されたプロキシを使用していないときに呼`$.hubConnection()`び出すことによって取得するオブジェクトと同じです。 生成されたプロキシ コードは、次のステートメントを実行して接続を作成します。

![生成されたプロキシ ファイルでの接続の作成](hubs-api-guide-javascript-client/_static/image3.png)

生成されたプロキシを使用している場合、生成されたプロキシを使用していない`$.connection.hub`場合は、接続オブジェクトで実行できる操作を実行できます。

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>開始メソッドの非同期実行

メソッド`start`は非同期的に実行されます。 これは、 、 、および`fail`などの`pipe`メソッドを呼び出すことによってコールバック関数を追加できることを意味する`done` [jQuery Deferred オブジェクト](http://api.jquery.com/category/deferred-object/)を返します。 サーバー メソッドの呼び出しなど、接続が確立された後に実行するコードがある場合は、そのコードをコールバック関数に入れるか、コールバック関数から呼び出します。 コールバック`.done`メソッドは、接続が確立された後、サーバー上の`OnConnected`イベント ハンドラー メソッド内のコードの実行が終了した後に実行されます。

上記の例の "Now connected" ステートメントを`start`、メソッド呼び出しの次のコード行として (`.done`コールバックではなく)`console.log`に配置すると、次の例に示すように、接続が確立される前に行が実行されます。

![接続が確立された後に実行されるコードを記述する方法が正しくない](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>ドメイン間接続を確立する方法

通常、ブラウザが から`http://contoso.com`ページを読み込む場合、SignalR 接続は`http://contoso.com/signalr`同じドメインの で、 で行われます。 ページが に`http://contoso.com`接続する`http://fabrikam.com/signalr`場合、これはドメイン間接続です。 セキュリティ上の理由から、ドメイン間の接続は既定で無効になっています。

SignalR 1.x では、クロス ドメイン要求は単一の EnableCrossDomain フラグによって制御されました。 このフラグは、JSONP 要求と CORS 要求の両方を制御しました。 柔軟性を高めるために、SignalR のサーバー コンポーネントからすべての CORS サポートが削除され (JavaScript クライアントは、ブラウザが CORS をサポートすることが検出された場合は引き続き CORS を使用します)、これらのシナリオをサポートする新しい OWIN ミドルウェアが利用可能になりました。

JSONP がクライアントで必要な場合 (古いブラウザーでクロスドメイン要求をサポートするため)、以下に示すように、`EnableJSONP``HubConfiguration`オブジェクトで を`true`に設定して明示的に有効にする必要があります。 JSONP は、CORS よりも安全性が低いため、デフォルトでは無効になっています。

**プロジェクトに次の手順を実行します。** このライブラリをインストールするには、パッケージ マネージャ コンソールで次のコマンドを実行します。

`Install-Package Microsoft.Owin.Cors`

このコマンドは、パッケージの 2.1.0 バージョンをプロジェクトに追加します。

### <a name="calling-usecors"></a>使用する呼び出し

 次のコード スニペットは、SignalR 2 でクロス ドメイン接続を実装する方法を示しています。

**SignalR 2 でのクロスドメイン要求の実装**

次のコードは、SignalR 2 プロジェクトで CORS または JSONP を有効にする方法を示しています。 このコード サンプル`Map`では`RunSignalR``MapSignalR`、 の代わりに を使用し、CORS ミドルウェアは、(で指定されたパスのすべてのトラフィックではなく) CORS サポートを必要`MapSignalR`とする SignalR 要求に対してのみ実行されるようにします。Map は、アプリケーション全体ではなく、特定の URL プレフィックスに対して実行する必要がある他のミドルウェアにも使用できます。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - コード内で`jQuery.support.cors`true に設定しないでください。
>
>     ![jQuery.support.cors を true に設定しないでください。](hubs-api-guide-javascript-client/_static/image7.png)
>
>     信号機は CORS の使用を処理します。 true`jQuery.support.cors`に設定すると、ブラウザーが CORS をサポートしていると SignalR が想定されるため、JSONP が無効になります。
> - ローカル ホスト URL に接続している場合、Internet Explorer 10 はドメイン間接続とは見なされないので、サーバーでドメイン間接続を有効にしていない場合でも、アプリケーションは IE 10 でローカルに動作します。
> - Internet Explorer 9 でのドメイン間接続の使用については、[この StackOverflow スレッド](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)を参照してください。
> - Chrome でのクロスドメイン接続の使用については、[この StackOverflow スレッド](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)を参照してください。
> - サンプル コードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。 別のベース URL を指定する方法については、「 [signalr Hubs API ガイド ASP.NET - サーバー - /signalr URL](hubs-api-guide-server.md#signalrurl)」を参照してください。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>接続の構成方法

接続を確立する前に、クエリ文字列パラメーターを指定するか、トランスポートメソッドを指定できます。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>クエリ文字列パラメーターの指定方法

クライアントが接続するときにサーバーにデータを送信する場合は、接続オブジェクトにクエリ文字列パラメーターを追加できます。 次の例は、クライアント コードでクエリ文字列パラメーターを設定する方法を示しています。

**START メソッドを呼び出す前にクエリ文字列値を設定します (生成されたプロキシを使用)。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**start メソッドを呼び出す前にクエリ文字列値を設定します (生成されたプロキシを使用しない場合)。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

サーバー コードでクエリ文字列パラメーターを読み取る方法を次の例に示します。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>トランスポート方法の指定方法

SignalR クライアントは、接続プロセスの一部として、通常、サーバーとネゴシエートして、サーバーとクライアントの両方でサポートされている最適なトランスポートを決定します。 使用するトランスポートが既にわかっている場合は、メソッドの呼び出し時にトランスポート メソッドを指定することで、このネゴシエーション`start`プロセスをバイパスできます。

**トランスポート メソッドを指定するクライアント コード (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**転送方法を指定するクライアント コード (生成されたプロキシを使用しない)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

代わりに、SignalR で試す順序で複数のトランスポート方法を指定できます。

**カスタム 転送フォールバック スキームを指定するクライアント コード (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**カスタム 転送フォールバック スキームを指定するクライアント コード (生成されたプロキシを使用しない)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

トランスポート方式の指定には、以下の値を使用できます。

- "ウェブソケット"
- 「フォーエバーフレーム」
- "サーバー送信イベント"
- "ロングポーリング"

次の例は、接続で使用されているトランスポート方法を調べる方法を示しています。

**接続で使用されるトランスポートメソッドを表示するクライアント コード (生成されたプロキシとの)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**接続で使用されるトランスポートメソッドを表示するクライアント コード (生成されたプロキシを使用しない)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

サーバー コードでトランスポート メソッドを確認する方法については、「 [ASP.NET SignalR Hubs API ガイド - サーバー - Context プロパティからクライアントに関する情報を取得する方法](hubs-api-guide-server.md#contextproperty)」を参照してください。 トランスポートとフォールバックの詳細については、「 [SignalR の概要 - トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>ハブ クラスのプロキシを取得する方法

作成する各接続オブジェクトは、1 つ以上のハブ クラスを含む SignalR サービスへの接続に関する情報をカプセル化します。 ハブ クラスと通信するには、自分で作成した (生成されたプロキシを使用していない場合) または生成されるプロキシ オブジェクトを使用します。

クライアントでは、プロキシ名はキャメル大文字バージョンのハブ クラス名です。 SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。

**サーバー上のハブ クラス**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**ハブの生成されたクライアント プロキシへの参照を取得します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**ハブ クラスのクライアント プロキシを作成する (プロキシを生成しない)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

属性を使用してハブ クラスを`HubName`修飾する場合は、大文字と小文字を変更せずに正確な名前を使用します。

**ハブ名属性を持つサーバー上のハブ クラス**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**ハブの生成されたクライアント プロキシへの参照を取得します。**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**ハブ クラスのクライアント プロキシを作成する (プロキシを生成しない)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>サーバーが呼び出すことができるクライアント上のメソッドを定義する方法

ハブからサーバーが呼び出すことができるメソッドを定義するには、生成されたプロキシの`client`プロパティを使用してイベント ハンドラーをハブ プロキシに追加するか、生成`on`されたプロキシを使用していない場合はメソッドを呼び出します。 パラメーターは、複雑なオブジェクトにできます。

メソッドを呼び出して接続を`start`確立する前に、イベント ハンドラーを追加します。 (メソッドを呼び出した後にイベント`start`ハンドラーを追加する場合は、このドキュメントの前半の[「接続を確立する方法](#establishconnection)」の注を参照し、生成されたプロキシを使用せずにメソッドを定義する構文を使用します。

メソッド名の一致は大文字と小文字を区別しません。 たとえば、`Clients.All.addContosoChatMessageToPage`サーバー上で、 、 `AddContosoChatMessageToPage` `addContosoChatMessageToPage`、または`addcontosochatmessagetopage`をクライアントで実行します。

**クライアント上のメソッドの定義 (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**クライアント上でメソッドを定義する別の方法 (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**クライアントでメソッドを定義する (生成されたプロキシを使用しない、または start メソッドを呼び出した後に追加する場合)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**クライアント メソッドを呼び出すサーバー コード**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

以下の例には、メソッドパラメータとして複合オブジェクトが含まれます。

**複雑なオブジェクトを受け取るクライアント上のメソッドを定義する (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**複雑なオブジェクトを受け取るクライアント上のメソッドを定義する (生成されたプロキシを使用しない)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**複合オブジェクトを定義するサーバー コード**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**複雑なオブジェクトを使用してクライアント メソッドを呼び出すサーバー コード**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>クライアントからサーバー メソッドを呼び出す方法

クライアントからサーバー メソッドを呼び出す場合`server`は、生成されたプロキシのプロパティ`invoke`を使用するか、生成されたプロキシを使用していない場合はハブ プロキシのメソッドを使用します。 戻り値またはパラメーターは、複雑なオブジェクトにできます。

ハブでメソッド名のキャメルケースバージョンを渡します。 SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。

次の例は、戻り値を持たないサーバー メソッドを呼び出す方法と、戻り値を持つサーバー メソッドを呼び出す方法を示しています。

**ハブメソッド名属性を持たないサーバー メソッド**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**パラメーターで渡される複合オブジェクトを定義するサーバー コード**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**サーバー メソッドを呼び出すクライアント コード (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**サーバー メソッドを呼び出すクライアント コード (生成されたプロキシを使用しない)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

属性を使用して Hub メソッドを`HubMethodName`修飾する場合は、大文字と小文字を変更せずにその名前を使用します。

属性を持つ**サーバー メソッド**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**サーバー メソッドを呼び出すクライアント コード (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**サーバー メソッドを呼び出すクライアント コード (生成されたプロキシを使用しない)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

上記の例では、戻り値のないサーバー メソッドを呼び出す方法を示します。 次の例は、戻り値を持つサーバー メソッドを呼び出す方法を示しています。

**戻り値を持つメソッドのサーバー コード**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

**戻り値に使用される Stock クラス**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**サーバー メソッドを呼び出すクライアント コード (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**サーバー メソッドを呼び出すクライアント コード (生成されたプロキシを使用しない)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>接続の有効期間イベントを処理する方法

SignalR は、次の接続有効期間イベントを処理できます。

- `starting`: 接続を介してデータが送信される前に発生します。
- `received`: 接続でデータが受信されたときに発生します。 受信したデータを提供します。
- `connectionSlow`: クライアントが低速または頻繁に切断する接続を検出したときに発生します。
- `reconnecting`: 基になるトランスポートの再接続が開始されたときに発生します。
- `reconnected`: 基になるトランスポートが再接続されたときに発生します。
- `stateChanged`: 接続状態が変化したときに発生します。 古い状態と新しい状態 (接続、接続、再接続、または切断) を提供します。
- `disconnected`: 接続が切断されたときに発生します。

たとえば、接続の問題が原因で顕著な遅延が発生した場合に警告メッセージを表示する場合は、`connectionSlow`イベントを処理します。

**接続を処理するSlowイベント (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**接続を処理するSlowイベント (生成されたプロキシを使用しない)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](handling-connection-lifetime-events.md)」を参照してください。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>エラーの処理方法

SignalR JavaScript クライアントは`error`、ハンドラーを追加できるイベントを提供します。 fail メソッドを使用して、サーバー メソッドの呼び出しによって発生するエラーのハンドラーを追加することもできます。

サーバーで詳細なエラー メッセージを明示的に有効にしない場合、SignalR がエラーの後に返す例外オブジェクトには、エラーに関する最小限の情報が含まれます。 たとえば、呼び出しが`newContosoChatMessage`失敗した場合、エラー オブジェクトのエラー メッセージ`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`には、セキュリティ上の理由から、運用環境のクライアントに詳細なエラー メッセージを送信することは推奨されませんが、トラブルシューティングの目的で詳細なエラー メッセージを有効にする場合は、サーバーで次のコードを使用します。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

次の例は、エラー イベントのハンドラーを追加する方法を示しています。

**エラー ハンドラを追加する (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**エラー ハンドラを追加する (生成されたプロキシを除く)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

メソッド呼び出しからのエラーを処理する方法を次の例に示します。

**メソッド呼び出しからのエラーの処理 (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**メソッド呼び出しからのエラーの処理 (生成されたプロキシを除く)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

メソッドの呼び出しが`error`失敗した場合、イベントも発生するため、`error`メソッド ハンドラーとメソッド`.fail`コールバック内のコードが実行されます。

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>クライアント側のログを有効にする方法

接続でクライアント側のログを有効にするには、接続を`logging`確立するメソッドを呼び出す前`start`に、接続オブジェクトのプロパティを設定します。

**ログ記録を有効にする (生成されたプロキシを使用)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**ログを有効にする (生成されたプロキシを使用しない)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

ログを表示するには、ブラウザの開発者ツールを開き、[コンソール] タブに移動します。この方法を示す手順とスクリーン ショットを示すチュートリアルについては[、「ASP.NET Signalr を使用したサーバー ブロードキャスト - ログ記録を有効にする](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)」を参照してください。
