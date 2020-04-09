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
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="78f2f-103">ASP.NET SignalR ハブ API ガイド - .NET クライアント (C#)</span><span class="sxs-lookup"><span data-stu-id="78f2f-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="78f2f-104">このドキュメントでは、Windows ストア (WinRT)、WPF、Silverlight、コンソール アプリケーションなどの .NET クライアントで SignalR バージョン 2 のハブ API を使用する方法の概要を示します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="78f2f-105">SignalR Hubs API を使用すると、サーバーから接続されたクライアント、およびクライアントからサーバーへのリモート プロシージャ コール (RPC) を作成できます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="78f2f-106">サーバー コードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行されるメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="78f2f-107">クライアント コードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="78f2f-108">SignalR は、クライアントからサーバーへのすべての配管を処理します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="78f2f-109">SignalR は、固定接続と呼ばれる下位レベルの API も提供します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="78f2f-110">SignalR、ハブ、および永続的接続の概要、または完全な SignalR アプリケーションを構築する方法を示すチュートリアルについては[、「SignalR - はじめに](../getting-started/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="78f2f-111">このトピックで使用するソフトウェアバージョン</span><span class="sxs-lookup"><span data-stu-id="78f2f-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="78f2f-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="78f2f-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="78f2f-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="78f2f-113">.NET 4.5</span></span>
> - <span data-ttu-id="78f2f-114">シグナル・バージョン 2</span><span class="sxs-lookup"><span data-stu-id="78f2f-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="78f2f-115">このトピックの以前のバージョン</span><span class="sxs-lookup"><span data-stu-id="78f2f-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="78f2f-116">SignalR の以前のバージョンについては[、SignalR の古いバージョン](../older-versions/index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="78f2f-117">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="78f2f-117">Questions and comments</span></span>
>
> <span data-ttu-id="78f2f-118">このチュートリアルを気に入った方法と、ページの下部にあるコメントで改善できる内容についてのフィードバックを残してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="78f2f-119">チュートリアルに直接関連しない質問がある場合は[、ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="78f2f-120">概要</span><span class="sxs-lookup"><span data-stu-id="78f2f-120">Overview</span></span>

<span data-ttu-id="78f2f-121">このドキュメントは、次のトピックに分かれています。</span><span class="sxs-lookup"><span data-stu-id="78f2f-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="78f2f-122">クライアントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="78f2f-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="78f2f-123">接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="78f2f-124">シルバーライト クライアントからのドメイン間接続</span><span class="sxs-lookup"><span data-stu-id="78f2f-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="78f2f-125">接続の構成方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="78f2f-126">WPF クライアントで同時接続の最大数を設定する方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="78f2f-127">クエリ文字列パラメーターの指定方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="78f2f-128">トランスポート方法の指定方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="78f2f-129">HTTP ヘッダーの指定方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="78f2f-130">クライアント証明書の指定方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="78f2f-131">ハブ プロキシを作成する方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="78f2f-132">サーバーが呼び出すことができるクライアント上のメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="78f2f-133">パラメータを持たないメソッド</span><span class="sxs-lookup"><span data-stu-id="78f2f-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="78f2f-134">パラメーターを持つメソッド, パラメーターの型を指定します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="78f2f-135">パラメータを持つメソッド、パラメータの動的オブジェクトを指定する</span><span class="sxs-lookup"><span data-stu-id="78f2f-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="78f2f-136">ハンドラを削除する方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="78f2f-137">クライアントからサーバー メソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="78f2f-138">接続の有効期間イベントを処理する方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="78f2f-139">エラーの処理方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="78f2f-140">クライアント側のログを有効にする方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="78f2f-141">サーバーが呼び出すことができるクライアント メソッドの WPF、Silverlight、およびコンソール アプリケーションのコード サンプル</span><span class="sxs-lookup"><span data-stu-id="78f2f-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="78f2f-142">サンプル .NET クライアント プロジェクトについては、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="78f2f-143">[GitHub.com上のグスタボ-アルメンタ/ SignalR-サンプル](https://github.com/gustavo-armenta/SignalR-Samples)(WinRT、シルバーライト、コンソール アプリの例)。</span><span class="sxs-lookup"><span data-stu-id="78f2f-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="78f2f-144">[ダミアンエドワーズ / シグナル伝達機動図形デモ / GitHub.com上の図形の移動.デスクトップ](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop)(WPF の例)。</span><span class="sxs-lookup"><span data-stu-id="78f2f-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="78f2f-145">GitHub.com上のシグナル / [Microsoft.AspNet.SignalR.Client.サンプル](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples)(コンソール アプリの例)。</span><span class="sxs-lookup"><span data-stu-id="78f2f-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="78f2f-146">サーバーまたは JavaScript クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="78f2f-147">シグナルハブ API ガイド - サーバー</span><span class="sxs-lookup"><span data-stu-id="78f2f-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="78f2f-148">シグナルハブ API ガイド - JavaScript クライアント</span><span class="sxs-lookup"><span data-stu-id="78f2f-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="78f2f-149">API リファレンストピックへのリンクは、API の .NET 4.5 バージョンに関するトピックです。</span><span class="sxs-lookup"><span data-stu-id="78f2f-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="78f2f-150">.NET 4 を使用している場合は[、API のトピックの .NET 4 バージョンを](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)参照してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="78f2f-151">クライアントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="78f2f-151">Client setup</span></span>

<span data-ttu-id="78f2f-152">[パッケージではなく、Microsoft.AspNet.SignalR.クライアント](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client)の NuGet[Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="78f2f-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="78f2f-153">このパッケージは、.NET 4 と .NET 4.5 の両方に対して、WinRT、シルバーライト、WPF、コンソール アプリケーション、および Windows Phone クライアントをサポートします。</span><span class="sxs-lookup"><span data-stu-id="78f2f-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="78f2f-154">クライアント上の SignalR のバージョンがサーバー上のバージョンと異なる場合、SignalR は多くの場合、その違いに適応できます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="78f2f-155">たとえば、SignalR バージョン 2 を実行しているサーバーは、1.1.x がインストールされているクライアントと、バージョン 2 がインストールされているクライアントをサポートします。</span><span class="sxs-lookup"><span data-stu-id="78f2f-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="78f2f-156">サーバー上のバージョンとクライアントのバージョンの違いが大きすぎる場合、またはクライアントがサーバーよりも新しい場合、SignalR はクライアントが接続を確立`InvalidOperationException`しようとしたときに例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="78f2f-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="78f2f-157">エラー メッセージは`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`" " です。</span><span class="sxs-lookup"><span data-stu-id="78f2f-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="78f2f-158">接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-158">How to establish a connection</span></span>

<span data-ttu-id="78f2f-159">接続を確立する前に、`HubConnection`オブジェクトを作成してプロキシを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="78f2f-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="78f2f-160">接続を確立するには、オブジェクトの`Start`メソッドを`HubConnection`呼び出します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="78f2f-161">JavaScript クライアントの場合は、`Start`接続を確立するためにメソッドを呼び出す前に、少なくとも 1 つのイベント ハンドラーを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="78f2f-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="78f2f-162">これは .NET クライアントには必要ありません。</span><span class="sxs-lookup"><span data-stu-id="78f2f-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="78f2f-163">JavaScript クライアントの場合、生成されたプロキシ コードは、サーバー上に存在するすべてのハブのプロキシを自動的に作成し、ハンドラーを登録すると、クライアントが使用する対象のハブを示す方法が示されます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="78f2f-164">しかし、.NET クライアントの場合はハブ プロキシを手動で作成するので、SignalR はプロキシを作成するハブを使用すると想定します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="78f2f-165">サンプル コードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="78f2f-166">別のベース URL を指定する方法については、「 [signalr Hubs API ガイド ASP.NET - サーバー - /signalr URL](hubs-api-guide-server.md#signalrurl)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="78f2f-167">メソッド`Start`は非同期的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="78f2f-168">接続が確立されるまで以降のコード行が実行されないようにするには、ASP.NET 4.5 非同期`await`メソッドまたは`.Wait()`同期メソッドで使用します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="78f2f-169">WinRT クライアント`.Wait()`では使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="78f2f-170">シルバーライト クライアントからのドメイン間接続</span><span class="sxs-lookup"><span data-stu-id="78f2f-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="78f2f-171">Silverlight クライアントからのドメイン間接続を有効にする方法については、「[ドメイン境界を越えてサービスを利用できるようにする](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="78f2f-172">接続の構成方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-172">How to configure the connection</span></span>

<span data-ttu-id="78f2f-173">接続を確立する前に、次のオプションを指定できます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="78f2f-174">同時接続数の制限。</span><span class="sxs-lookup"><span data-stu-id="78f2f-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="78f2f-175">クエリ文字列パラメーター。</span><span class="sxs-lookup"><span data-stu-id="78f2f-175">Query string parameters.</span></span>
- <span data-ttu-id="78f2f-176">トランスポート方法。</span><span class="sxs-lookup"><span data-stu-id="78f2f-176">The transport method.</span></span>
- <span data-ttu-id="78f2f-177">HTTP ヘッダー。</span><span class="sxs-lookup"><span data-stu-id="78f2f-177">HTTP headers.</span></span>
- <span data-ttu-id="78f2f-178">クライアント証明書。</span><span class="sxs-lookup"><span data-stu-id="78f2f-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="78f2f-179">WPF クライアントで同時接続の最大数を設定する方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="78f2f-180">WPF クライアントでは、同時接続の最大数を既定値の 2 から増やす必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="78f2f-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="78f2f-181">推奨値は 10 です。</span><span class="sxs-lookup"><span data-stu-id="78f2f-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="78f2f-182">詳細については、「サービス[ポイント マネージャー.既定の接続制限](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="78f2f-183">クエリ文字列パラメーターの指定方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-183">How to specify query string parameters</span></span>

<span data-ttu-id="78f2f-184">クライアントが接続するときにサーバーにデータを送信する場合は、接続オブジェクトにクエリ文字列パラメーターを追加できます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="78f2f-185">クライアント コードでクエリ文字列パラメーターを設定する方法を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="78f2f-186">サーバー コードでクエリ文字列パラメーターを読み取る方法を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="78f2f-187">トランスポート方法の指定方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-187">How to specify the transport method</span></span>

<span data-ttu-id="78f2f-188">SignalR クライアントは、接続プロセスの一部として、通常、サーバーとネゴシエートして、サーバーとクライアントの両方でサポートされている最適なトランスポートを決定します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="78f2f-189">使用するトランスポートが既にわかっている場合は、このネゴシエーション プロセスをバイパスできます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="78f2f-190">トランスポート メソッドを指定するには、トランスポート オブジェクトを Start メソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="78f2f-191">クライアント コードでトランスポート メソッドを指定する方法を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="78f2f-192">名前空間[には、トランスポート](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)を指定するために使用できる次のクラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="78f2f-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="78f2f-193">[ロングポーリングトランスポート](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="78f2f-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="78f2f-194">[トランスポート](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="78f2f-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="78f2f-195">[WebSocket トランスポート](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx)(サーバーとクライアントの両方が .NET 4.5 を使用する場合にのみ使用できます)。</span><span class="sxs-lookup"><span data-stu-id="78f2f-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="78f2f-196">[自動トランスポート](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx)(クライアントとサーバーの両方でサポートされている最適なトランスポートを自動的に選択します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="78f2f-197">これがデフォルトのトランスポートです。</span><span class="sxs-lookup"><span data-stu-id="78f2f-197">This is the default transport.</span></span> <span data-ttu-id="78f2f-198">メソッドにこれを`Start`渡すことは、何も渡さないのと同じ効果があります)。</span><span class="sxs-lookup"><span data-stu-id="78f2f-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="78f2f-199">ForeverFrame トランスポートはブラウザーでのみ使用されるため、このリストには含まれません。</span><span class="sxs-lookup"><span data-stu-id="78f2f-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="78f2f-200">サーバー コードでトランスポート メソッドを確認する方法については、「 [ASP.NET SignalR Hubs API ガイド - サーバー - Context プロパティからクライアントに関する情報を取得する方法](hubs-api-guide-server.md#contextproperty)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="78f2f-201">トランスポートとフォールバックの詳細については、「 [SignalR の概要 - トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="78f2f-202">HTTP ヘッダーの指定方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-202">How to specify HTTP headers</span></span>

<span data-ttu-id="78f2f-203">HTTP ヘッダーを設定するには、接続`Headers`オブジェクトのプロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="78f2f-204">HTTP ヘッダーを追加する方法を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="78f2f-205">クライアント証明書の指定方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-205">How to specify client certificates</span></span>

<span data-ttu-id="78f2f-206">クライアント証明書を追加するには、接続オブジェクト`AddClientCertificate`でメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="78f2f-207">ハブ プロキシを作成する方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-207">How to create the Hub proxy</span></span>

<span data-ttu-id="78f2f-208">ハブがサーバーから呼び出すことができるクライアント上のメソッドを定義し、サーバーのハブでメソッドを呼び出すには、接続オブジェクトを呼び出`CreateHubProxy`すことによってハブのプロキシを作成します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="78f2f-209">渡す`CreateHubProxy`文字列は、ハブ クラスの名前、またはサーバーで使用されている場合は`HubName`、属性で指定された名前です。</span><span class="sxs-lookup"><span data-stu-id="78f2f-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="78f2f-210">名前が一致するかどうかを判断する際、大文字と小文字は区別されません。</span><span class="sxs-lookup"><span data-stu-id="78f2f-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="78f2f-211">**サーバー上のハブ クラス**</span><span class="sxs-lookup"><span data-stu-id="78f2f-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="78f2f-212">**ハブ クラスのクライアント プロキシを作成する**</span><span class="sxs-lookup"><span data-stu-id="78f2f-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="78f2f-213">属性を使用してハブ クラスを修飾`HubName`する場合は、その名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="78f2f-214">**サーバー上のハブ クラス**</span><span class="sxs-lookup"><span data-stu-id="78f2f-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="78f2f-215">**ハブ クラスのクライアント プロキシを作成する**</span><span class="sxs-lookup"><span data-stu-id="78f2f-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="78f2f-216">同じ`HubConnection.CreateHubProxy`で複数回呼び出`hubName`すと、同じキャッシュ オブジェクト`IHubProxy`が取得されます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="78f2f-217">サーバーが呼び出すことができるクライアント上のメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="78f2f-218">サーバーが呼び出すことができるメソッドを定義するには、プロキシの`On`メソッドを使用してイベント ハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="78f2f-219">メソッド名の一致は大文字と小文字を区別しません。</span><span class="sxs-lookup"><span data-stu-id="78f2f-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="78f2f-220">たとえば、`Clients.All.UpdateStockPrice`サーバー上で、 、 `updateStockPrice` `updatestockprice`、または`UpdateStockPrice`をクライアントで実行します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="78f2f-221">クライアント プラットフォームによって、UI を更新するメソッド コードの記述方法に関する要件が異なります。</span><span class="sxs-lookup"><span data-stu-id="78f2f-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="78f2f-222">表示される例は、WinRT (Windows ストア .NET) クライアント用です。</span><span class="sxs-lookup"><span data-stu-id="78f2f-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="78f2f-223">WPF、Silverlight、およびコンソール アプリケーションの例については、[このトピックの後半で説明します](#wpfsl)。</span><span class="sxs-lookup"><span data-stu-id="78f2f-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="78f2f-224">パラメータを持たないメソッド</span><span class="sxs-lookup"><span data-stu-id="78f2f-224">Methods without parameters</span></span>

<span data-ttu-id="78f2f-225">処理するメソッドにパラメーターがない場合は、メソッドの非ジェネリック オーバーロードを`On`使用します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="78f2f-226">**パラメータを指定せずにクライアント メソッドを呼び出すサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="78f2f-227">**パラメーターを指定せずにサーバーから呼び出されるメソッドの WinRT クライアント コード ([このトピックの後半の「 WPF および Silverlight](#wpfsl)の例 」 を参照してください ) 。**</span><span class="sxs-lookup"><span data-stu-id="78f2f-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="78f2f-228">パラメーターを持つメソッド(パラメーターの型を指定する)</span><span class="sxs-lookup"><span data-stu-id="78f2f-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="78f2f-229">処理するメソッドにパラメーターがある場合は、パラメーターの型を`On`メソッドのジェネリック型として指定します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="78f2f-230">最大 8 個の`On`パラメーター (Windows Phone 7 では 4) を指定できるようにするメソッドのジェネリック オーバーロードがあります。</span><span class="sxs-lookup"><span data-stu-id="78f2f-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="78f2f-231">次の例では、1 つのパラメーターがメソッド`UpdateStockPrice`に送信されます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="78f2f-232">**パラメーターを使用してクライアント メソッドを呼び出すサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="78f2f-233">**パラメータに使用される Stock クラス**</span><span class="sxs-lookup"><span data-stu-id="78f2f-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="78f2f-234">**パラメーターを使用してサーバーから呼び出されるメソッドの WinRT クライアント コード ([このトピックの後半の WPF および Silverlight の例を参照](#wpfsl)してください)**</span><span class="sxs-lookup"><span data-stu-id="78f2f-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="78f2f-235">パラメータを持つメソッド、パラメータの動的オブジェクトを指定する</span><span class="sxs-lookup"><span data-stu-id="78f2f-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="78f2f-236">`On`メソッドのジェネリック型としてパラメーターを指定する代わりに、動的オブジェクトとしてパラメーターを指定できます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="78f2f-237">**パラメーターを使用してクライアント メソッドを呼び出すサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="78f2f-238">**パラメータに使用される Stock クラス**</span><span class="sxs-lookup"><span data-stu-id="78f2f-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="78f2f-239">**パラメーターに動的オブジェクトを使用して、パラメーターを使用してサーバーから呼び出されるメソッドの WinRT クライアント コード ([WPF および Silverlight](#wpfsl)の例を参照してください ) 。**</span><span class="sxs-lookup"><span data-stu-id="78f2f-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="78f2f-240">ハンドラを削除する方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-240">How to remove a handler</span></span>

<span data-ttu-id="78f2f-241">ハンドラーを削除するには、そのメソッド`Dispose`を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="78f2f-242">**サーバーから呼び出されたメソッドのクライアント コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="78f2f-243">**ハンドラを削除するクライアント コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="78f2f-244">クライアントからサーバー メソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-244">How to call server methods from the client</span></span>

<span data-ttu-id="78f2f-245">サーバー上のメソッドを呼び出す場合`Invoke`は、ハブ プロキシでメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="78f2f-246">サーバー メソッドに戻り値がない場合は、メソッドの非ジェネリック オーバーロード`Invoke`を使用します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="78f2f-247">**戻り値のないメソッドのサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="78f2f-248">**戻り値のないメソッドを呼び出すクライアント コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="78f2f-249">サーバー メソッドに戻り値がある場合は、`Invoke`戻り値の型をメソッドのジェネリック型として指定します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="78f2f-250">**戻り値を持ち、複合型パラメーターを受け取るメソッドのサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="78f2f-251">**パラメータと戻り値に使用される Stock クラス**</span><span class="sxs-lookup"><span data-stu-id="78f2f-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="78f2f-252">**ASP.NET 4.5 非同期メソッドで、戻り値を持ち、複合型パラメーターを受け取るメソッドを呼び出すクライアント コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="78f2f-253">**クライアント コード呼び出しメソッドの戻り値を持ち、複合型パラメーターを受け取るメソッドを同期メソッドで受け取ります。**</span><span class="sxs-lookup"><span data-stu-id="78f2f-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="78f2f-254">この`Invoke`メソッドは非同期的に実行され`Task`、オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="78f2f-255">または`await``.Wait()`を指定しない場合、呼び出すメソッドの実行が完了する前に、次のコード行が実行されます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="78f2f-256">接続の有効期間イベントを処理する方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="78f2f-257">SignalR は、次の接続有効期間イベントを処理できます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="78f2f-258">`Received`: 接続でデータが受信されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="78f2f-259">受信したデータを提供します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-259">Provides the received data.</span></span>
- <span data-ttu-id="78f2f-260">`ConnectionSlow`: クライアントが低速または頻繁に切断する接続を検出したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="78f2f-261">`Reconnecting`: 基になるトランスポートの再接続が開始されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="78f2f-262">`Reconnected`: 基になるトランスポートが再接続されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="78f2f-263">`StateChanged`: 接続状態が変化したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="78f2f-264">古い状態と新しい状態を提供します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-264">Provides the old state and the new state.</span></span> <span data-ttu-id="78f2f-265">接続状態の値の詳細については、「[接続状態の列挙 」](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="78f2f-266">`Closed`: 接続が切断されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="78f2f-267">たとえば、致命的ではないが断続的な接続の問題 (接続の低速化や頻繁な切断など) を引き起こすエラーに関する警告メッセージ`ConnectionSlow`を表示する場合は、イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="78f2f-268">詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](handling-connection-lifetime-events.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="78f2f-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="78f2f-269">エラーの処理方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-269">How to handle errors</span></span>

<span data-ttu-id="78f2f-270">サーバーで詳細なエラー メッセージを明示的に有効にしない場合、SignalR がエラーの後に返す例外オブジェクトには、エラーに関する最小限の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="78f2f-271">たとえば、呼び出しが`newContosoChatMessage`失敗した場合、エラー オブジェクトのエラー メッセージ`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`には、セキュリティ上の理由から、運用環境のクライアントに詳細なエラー メッセージを送信することは推奨されませんが、トラブルシューティングの目的で詳細なエラー メッセージを有効にする場合は、サーバーで次のコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="78f2f-272">SignalR が発生するエラーを処理するには、接続オブジェクトのイベントの`Error`ハンドラーを追加できます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="78f2f-273">メソッド呼び出しのエラーを処理するには、コードを try-catch ブロックでラップします。</span><span class="sxs-lookup"><span data-stu-id="78f2f-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="78f2f-274">クライアント側のログを有効にする方法</span><span class="sxs-lookup"><span data-stu-id="78f2f-274">How to enable client-side logging</span></span>

<span data-ttu-id="78f2f-275">クライアント側のログを有効にするには、接続`TraceLevel`オブジェクト`TraceWriter`の プロパティと プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="78f2f-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="78f2f-276">サーバーが呼び出すことができるクライアント メソッドの WPF、Silverlight、およびコンソール アプリケーションのコード サンプル</span><span class="sxs-lookup"><span data-stu-id="78f2f-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="78f2f-277">サーバーが呼び出すことができるクライアント メソッドを定義するコード サンプルは、WinRT クライアントに適用されます。</span><span class="sxs-lookup"><span data-stu-id="78f2f-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="78f2f-278">次のサンプルは、WPF、Silverlight、およびコンソール アプリケーション クライアントの同等のコードを示しています。</span><span class="sxs-lookup"><span data-stu-id="78f2f-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="78f2f-279">パラメータを持たないメソッド</span><span class="sxs-lookup"><span data-stu-id="78f2f-279">Methods without parameters</span></span>

<span data-ttu-id="78f2f-280">**パラメーターを指定せずにサーバーから呼び出されるメソッドの WPF クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="78f2f-281">**パラメータを指定せずにサーバーから呼び出されるメソッドの Silverlight クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="78f2f-282">**パラメーターを指定せずにサーバーから呼び出されるメソッドのコンソール アプリケーション クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="78f2f-283">パラメーターを持つメソッド(パラメーターの型を指定する)</span><span class="sxs-lookup"><span data-stu-id="78f2f-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="78f2f-284">**パラメーターを指定してサーバーから呼び出されるメソッドの WPF クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="78f2f-285">**パラメーターを指定してサーバーから呼び出されるメソッドの Silverlight クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="78f2f-286">**パラメーターを指定してサーバーから呼び出されるメソッドのコンソール アプリケーション クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="78f2f-287">パラメータを持つメソッド、パラメータの動的オブジェクトを指定する</span><span class="sxs-lookup"><span data-stu-id="78f2f-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="78f2f-288">**パラメーターに動的オブジェクトを使用して、パラメーターを使用してサーバーから呼び出されるメソッドの WPF クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="78f2f-289">**パラメータを使用してサーバーから呼び出されるメソッドの Silverlight クライアント コードで、パラメータに動的オブジェクトを使用します。**</span><span class="sxs-lookup"><span data-stu-id="78f2f-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="78f2f-290">**パラメーターに対する動的オブジェクトを使用して、パラメーターを指定してサーバーから呼び出されるメソッドのコンソール アプリケーション クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="78f2f-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
