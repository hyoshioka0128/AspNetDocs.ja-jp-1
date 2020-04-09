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
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="32cd5-103">ASP.NETシグナルハブ API ガイド - JavaScript クライアント</span><span class="sxs-lookup"><span data-stu-id="32cd5-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="32cd5-104">このドキュメントでは、ブラウザーや Windows ストア (WinJS) アプリケーションなどの JavaScript クライアントでの SignalR バージョン 2 のハブ API の使用の概要を説明します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="32cd5-105">SignalR Hubs API を使用すると、サーバーから接続されたクライアント、およびクライアントからサーバーへのリモート プロシージャ コール (RPC) を作成できます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="32cd5-106">サーバー コードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行されるメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="32cd5-107">クライアント コードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="32cd5-108">SignalR は、クライアントからサーバーへのすべての配管を処理します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="32cd5-109">SignalR は、固定接続と呼ばれる下位レベルの API も提供します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="32cd5-110">SignalR、ハブ、および固定接続の概要については[、SignalR の概要を](../getting-started/introduction-to-signalr.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="32cd5-111">このトピックで使用するソフトウェアバージョン</span><span class="sxs-lookup"><span data-stu-id="32cd5-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="32cd5-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="32cd5-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="32cd5-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="32cd5-113">.NET 4.5</span></span>
> - <span data-ttu-id="32cd5-114">シグナル・バージョン 2</span><span class="sxs-lookup"><span data-stu-id="32cd5-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="32cd5-115">このトピックの以前のバージョン</span><span class="sxs-lookup"><span data-stu-id="32cd5-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="32cd5-116">SignalR の以前のバージョンについては[、SignalR の古いバージョン](../older-versions/index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="32cd5-117">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="32cd5-117">Questions and comments</span></span>
>
> <span data-ttu-id="32cd5-118">このチュートリアルを気に入った方法と、ページの下部にあるコメントで改善できる内容についてのフィードバックを残してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="32cd5-119">チュートリアルに直接関連しない質問がある場合は[、ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="32cd5-120">概要</span><span class="sxs-lookup"><span data-stu-id="32cd5-120">Overview</span></span>

<span data-ttu-id="32cd5-121">このドキュメントは、次のトピックに分かれています。</span><span class="sxs-lookup"><span data-stu-id="32cd5-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="32cd5-122">生成されたプロキシと、それがあなたのために何をするのか</span><span class="sxs-lookup"><span data-stu-id="32cd5-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="32cd5-123">生成されたプロキシを使用する場合</span><span class="sxs-lookup"><span data-stu-id="32cd5-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="32cd5-124">クライアントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="32cd5-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="32cd5-125">動的に生成されたプロキシを参照する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="32cd5-126">SignalR が生成したプロキシの物理ファイルを作成する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="32cd5-127">接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="32cd5-128">ハブは、$.hubConnection()が作成するオブジェクトと同じオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="32cd5-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="32cd5-129">開始メソッドの非同期実行</span><span class="sxs-lookup"><span data-stu-id="32cd5-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="32cd5-130">ドメイン間接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="32cd5-131">接続の構成方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="32cd5-132">クエリ文字列パラメーターの指定方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="32cd5-133">トランスポート方法の指定方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="32cd5-134">ハブ クラスのプロキシを取得する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="32cd5-135">サーバーが呼び出すことができるクライアント上のメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="32cd5-136">クライアントからサーバー メソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="32cd5-137">接続の有効期間イベントを処理する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="32cd5-138">エラーの処理方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="32cd5-139">クライアント側のログを有効にする方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="32cd5-140">サーバーまたは .NET クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="32cd5-141">シグナルハブ API ガイド - サーバー</span><span class="sxs-lookup"><span data-stu-id="32cd5-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="32cd5-142">SignalR ハブ API ガイド - .NET クライアント</span><span class="sxs-lookup"><span data-stu-id="32cd5-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="32cd5-143">SignalR 2 サーバー コンポーネントは 、.NET 4.5 でのみ使用できます (ただし、.NET 4.0 の SignalR 2 用の .NET クライアントがあります)。</span><span class="sxs-lookup"><span data-stu-id="32cd5-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="32cd5-144">生成されたプロキシと、それがあなたのために何をするのか</span><span class="sxs-lookup"><span data-stu-id="32cd5-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="32cd5-145">SignalR が自動的に生成するプロキシの有無にかかわらず、SignalR サービスと通信するように JavaScript クライアントをプログラムできます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="32cd5-146">プロキシが行うことは、接続、サーバーが呼び出すメソッドの記述、およびサーバー上のメソッドの呼び出しに使用するコードの構文を簡略化することです。</span><span class="sxs-lookup"><span data-stu-id="32cd5-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="32cd5-147">サーバー メソッドを呼び出すコードを記述すると、生成されたプロキシを使用して、ローカル関数を実行しているかのように見える構文を使用できます`serverMethod(arg1, arg2)``invoke('serverMethod', arg1, arg2)`。</span><span class="sxs-lookup"><span data-stu-id="32cd5-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="32cd5-148">生成されたプロキシ構文は、サーバーメソッド名を誤って入力した場合に、即座にわかりやすく、クライアント側エラーを可能にします。</span><span class="sxs-lookup"><span data-stu-id="32cd5-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="32cd5-149">プロキシを定義するファイルを手動で作成した場合は、サーバー メソッドを呼び出すコードの記述に対する IntelliSense のサポートも取得できます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="32cd5-150">たとえば、サーバー上に次のハブ クラスがあるとします。</span><span class="sxs-lookup"><span data-stu-id="32cd5-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="32cd5-151">次のコード例は、サーバー上で`NewContosoChatMessage`メソッドを呼び出し、サーバーからメソッドの呼び出しを`addContosoChatMessageToPage`受け取る JavaScript コードの例を示しています。</span><span class="sxs-lookup"><span data-stu-id="32cd5-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="32cd5-152">**生成されたプロキシを使用する場合**</span><span class="sxs-lookup"><span data-stu-id="32cd5-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="32cd5-153">**生成されたプロキシを使用しない**</span><span class="sxs-lookup"><span data-stu-id="32cd5-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="32cd5-154">生成されたプロキシを使用する場合</span><span class="sxs-lookup"><span data-stu-id="32cd5-154">When to use the generated proxy</span></span>

<span data-ttu-id="32cd5-155">サーバーが呼び出すクライアント メソッドに対して複数のイベント ハンドラーを登録する場合は、生成されたプロキシを使用できません。</span><span class="sxs-lookup"><span data-stu-id="32cd5-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="32cd5-156">それ以外の場合は、生成されたプロキシを使用するか、コーディングの設定に基づいて使用しないようにするかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="32cd5-157">使用しない場合は、クライアント コードの要素で "signalr/hubs" URL を`script`参照する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="32cd5-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="32cd5-158">クライアントのセットアップ</span><span class="sxs-lookup"><span data-stu-id="32cd5-158">Client setup</span></span>

<span data-ttu-id="32cd5-159">JavaScript クライアントは、jQuery とシグナルのコア JavaScript ファイルへの参照を必要とします。</span><span class="sxs-lookup"><span data-stu-id="32cd5-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="32cd5-160">jQuery バージョンは、1.7.2、1.8.2、1.9.1 などの 1.6.4 またはそれ以降のメジャー バージョンである必要があります。</span><span class="sxs-lookup"><span data-stu-id="32cd5-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="32cd5-161">生成されたプロキシを使用する場合は、SignalR が生成したプロキシ JavaScript ファイルへの参照も必要です。</span><span class="sxs-lookup"><span data-stu-id="32cd5-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="32cd5-162">生成されたプロキシを使用する HTML ページでの参照の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="32cd5-163">これらの参照は、jQuery の最初、その後の SignalR コア、および SignalR プロキシの最後の順序で含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="32cd5-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="32cd5-164">動的に生成されたプロキシを参照する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="32cd5-165">前の例では、SignalR が生成したプロキシへの参照は、物理ファイルではなく、動的に生成された JavaScript コードです。</span><span class="sxs-lookup"><span data-stu-id="32cd5-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="32cd5-166">SignalR は、プロキシの JavaScript コードをその場で作成し、"/signalr/hubs" URL に応答してクライアントに提供します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="32cd5-167">メソッドでサーバー上の SignalR 接続に別のベース URL`MapSignalR`を指定した場合、動的に生成されるプロキシ ファイルの URL は、カスタム URL に "/hubs" が付加された URL です。</span><span class="sxs-lookup"><span data-stu-id="32cd5-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="32cd5-168">Windows 8 (Windows ストア) JavaScript クライアントの場合は、動的に生成されたプロキシ ファイルではなく、物理プロキシ ファイルを使用します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="32cd5-169">詳細については、このトピックの後半の[「SignalR で生成されたプロキシの物理ファイルを作成する方法](#manualproxy)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="32cd5-170">ASP.NET MVC 4 または 5 の Razor ビューでは、プロキシ ファイルの参照でアプリケーション ルートを参照するチルダを使用します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="32cd5-171">MVC 5 で SignalR を使用する方法の詳細については[、「SignalR と MVC 5 の概要](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="32cd5-172">ASP.NET MVC 3 の Razor`Url.Content`ビューで、プロキシ ファイルの参照に使用します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="32cd5-173">ASP.NET Web フォーム アプリケーションで`ResolveClientUrl`、プロキシ ファイルの参照に使用するか、またはアプリルートの相対パス (チルダから始まる) を使用して ScriptManager を使用して登録します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="32cd5-174">一般的な規則として、CSS ファイルまたは JavaScript ファイルに使用する 「/signalr/hubs」URL を指定する場合と同じ方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="32cd5-175">チルダを使用せずに URL を指定した場合、IIS Express を使用して Visual Studio でテストを行うとアプリケーションが正常に動作する場合がありますが、IIS を完全に展開すると 404 エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="32cd5-176">詳細については、MSDN サイトの「Visual Studio の[Web サーバーでの、ASP.NET Web プロジェクトの](https://msdn.microsoft.com/library/58wxa9w5.aspx)**ルート レベルのリソースへの参照の解決**」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="32cd5-177">デバッグ モードで Visual Studio 2017 で Web プロジェクトを実行し、ブラウザーとして Internet Explorer を使用する場合は、**ソリューション エクスプ ローラー**の**スクリプト**の下にプロキシ ファイルを表示できます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="32cd5-178">ファイルの内容を表示するには、**ハブ**をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="32cd5-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="32cd5-179">Visual Studio 2012 または 2013 と Internet Explorer を使用していない場合、またはデバッグ モードでない場合は、"/signalR/hubs" URL を参照してファイルの内容を取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="32cd5-180">たとえば、サイトが で`http://localhost:56699`実行されている場合は、ブラウザ`http://localhost:56699/SignalR/hubs`で に移動します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="32cd5-181">SignalR が生成したプロキシの物理ファイルを作成する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="32cd5-182">動的に生成されるプロキシの代わりに、プロキシ コードを持つ物理ファイルを作成し、そのファイルを参照することもできます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="32cd5-183">キャッシュやバンドルの動作を制御したり、サーバー メソッドへの呼び出しをコーディングするときに IntelliSense を取得したりするために、これを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="32cd5-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="32cd5-184">プロキシ ファイルを作成するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="32cd5-185">[パッケージを](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)インストールします。</span><span class="sxs-lookup"><span data-stu-id="32cd5-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="32cd5-186">コマンド プロンプトを開き、SignalR.exe ファイルが含まれている*ツール*フォルダーを参照します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="32cd5-187">ツール フォルダは次の場所にあります。</span><span class="sxs-lookup"><span data-stu-id="32cd5-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="32cd5-188">次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="32cd5-189">*.dll*へのパスは、通常、プロジェクト フォルダー内の*bin*フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="32cd5-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="32cd5-190">このコマンドは *、signalr.exe*と同じフォルダーに*server.js*という名前のファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="32cd5-191">プロジェクトの適切なフォルダーに*server.js*ファイルを配置し、アプリケーションに合わせて名前を変更し、"signalr/hubs" 参照の代わりにそのファイルへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="32cd5-192">接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-192">How to establish a connection</span></span>

<span data-ttu-id="32cd5-193">接続を確立する前に、接続オブジェクトを作成し、プロキシを作成し、サーバーから呼び出すことができるメソッドのイベント ハンドラーを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="32cd5-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="32cd5-194">プロキシ ハンドラとイベント ハンドラを設定したら、メソッドを呼び出`start`して接続を確立します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="32cd5-195">生成されたプロキシを使用している場合は、生成されたプロキシ コードが自動的に行うため、独自のコードで接続オブジェクトを作成する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="32cd5-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="32cd5-196">**(生成されたプロキシとの) 接続の確立**</span><span class="sxs-lookup"><span data-stu-id="32cd5-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="32cd5-197">**(生成されたプロキシを使用せずに) 接続を確立する**</span><span class="sxs-lookup"><span data-stu-id="32cd5-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="32cd5-198">サンプル コードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="32cd5-199">別のベース URL を指定する方法については、「 [signalr Hubs API ガイド ASP.NET - サーバー - /signalr URL](hubs-api-guide-server.md#signalrurl)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="32cd5-200">デフォルトでは、ハブの場所は現在のサーバーです。別のサーバーに接続している場合は、次の例に示すように、`start`メソッドを呼び出す前に URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="32cd5-201">通常は、メソッドを呼び出して`start`接続を確立する前に、イベント ハンドラーを登録します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="32cd5-202">接続を確立した後にイベント ハンドラーを登録する場合は、その操作を行うことができますが、メソッドを呼び出す前に、少なくとも 1`start`つのイベント ハンドラーを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="32cd5-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="32cd5-203">その理由の 1 つは、アプリケーションに多数のハブが存在する可能性がありますが、1 つのハブにしか`OnConnected`使用しない場合は、すべてのハブでイベントをトリガーしたくないということです。</span><span class="sxs-lookup"><span data-stu-id="32cd5-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="32cd5-204">接続が確立されると、ハブのプロキシにクライアント メソッドが存在すると、SignalR にイベントをトリガーするように指示されます`OnConnected`。</span><span class="sxs-lookup"><span data-stu-id="32cd5-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="32cd5-205">メソッドを呼び出す前にイベント ハンドラーを`start`登録しない場合、ハブでメソッドを呼び出すことはできますが、ハブの`OnConnected`メソッドは呼び出されず、サーバーからクライアント メソッドは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="32cd5-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="32cd5-206">ハブは、$.hubConnection()が作成するオブジェクトと同じオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="32cd5-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="32cd5-207">例からわかるように、生成されたプロキシを使用すると、`$.connection.hub`接続オブジェクトを参照します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="32cd5-208">これは、生成されたプロキシを使用していないときに呼`$.hubConnection()`び出すことによって取得するオブジェクトと同じです。</span><span class="sxs-lookup"><span data-stu-id="32cd5-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="32cd5-209">生成されたプロキシ コードは、次のステートメントを実行して接続を作成します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![生成されたプロキシ ファイルでの接続の作成](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="32cd5-211">生成されたプロキシを使用している場合、生成されたプロキシを使用していない`$.connection.hub`場合は、接続オブジェクトで実行できる操作を実行できます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="32cd5-212">開始メソッドの非同期実行</span><span class="sxs-lookup"><span data-stu-id="32cd5-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="32cd5-213">メソッド`start`は非同期的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="32cd5-214">これは、 、 、および`fail`などの`pipe`メソッドを呼び出すことによってコールバック関数を追加できることを意味する`done` [jQuery Deferred オブジェクト](http://api.jquery.com/category/deferred-object/)を返します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="32cd5-215">サーバー メソッドの呼び出しなど、接続が確立された後に実行するコードがある場合は、そのコードをコールバック関数に入れるか、コールバック関数から呼び出します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="32cd5-216">コールバック`.done`メソッドは、接続が確立された後、サーバー上の`OnConnected`イベント ハンドラー メソッド内のコードの実行が終了した後に実行されます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="32cd5-217">上記の例の "Now connected" ステートメントを`start`、メソッド呼び出しの次のコード行として (`.done`コールバックではなく)`console.log`に配置すると、次の例に示すように、接続が確立される前に行が実行されます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![接続が確立された後に実行されるコードを記述する方法が正しくない](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="32cd5-219">ドメイン間接続を確立する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="32cd5-220">通常、ブラウザが から`http://contoso.com`ページを読み込む場合、SignalR 接続は`http://contoso.com/signalr`同じドメインの で、 で行われます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="32cd5-221">ページが に`http://contoso.com`接続する`http://fabrikam.com/signalr`場合、これはドメイン間接続です。</span><span class="sxs-lookup"><span data-stu-id="32cd5-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="32cd5-222">セキュリティ上の理由から、ドメイン間の接続は既定で無効になっています。</span><span class="sxs-lookup"><span data-stu-id="32cd5-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="32cd5-223">SignalR 1.x では、クロス ドメイン要求は単一の EnableCrossDomain フラグによって制御されました。</span><span class="sxs-lookup"><span data-stu-id="32cd5-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="32cd5-224">このフラグは、JSONP 要求と CORS 要求の両方を制御しました。</span><span class="sxs-lookup"><span data-stu-id="32cd5-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="32cd5-225">柔軟性を高めるために、SignalR のサーバー コンポーネントからすべての CORS サポートが削除され (JavaScript クライアントは、ブラウザが CORS をサポートすることが検出された場合は引き続き CORS を使用します)、これらのシナリオをサポートする新しい OWIN ミドルウェアが利用可能になりました。</span><span class="sxs-lookup"><span data-stu-id="32cd5-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="32cd5-226">JSONP がクライアントで必要な場合 (古いブラウザーでクロスドメイン要求をサポートするため)、以下に示すように、`EnableJSONP``HubConfiguration`オブジェクトで を`true`に設定して明示的に有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="32cd5-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="32cd5-227">JSONP は、CORS よりも安全性が低いため、デフォルトでは無効になっています。</span><span class="sxs-lookup"><span data-stu-id="32cd5-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="32cd5-228">**プロジェクトに次の手順を実行します。** このライブラリをインストールするには、パッケージ マネージャ コンソールで次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="32cd5-229">このコマンドは、パッケージの 2.1.0 バージョンをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="32cd5-230">使用する呼び出し</span><span class="sxs-lookup"><span data-stu-id="32cd5-230">Calling UseCors</span></span>

 <span data-ttu-id="32cd5-231">次のコード スニペットは、SignalR 2 でクロス ドメイン接続を実装する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="32cd5-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="32cd5-232">**SignalR 2 でのクロスドメイン要求の実装**</span><span class="sxs-lookup"><span data-stu-id="32cd5-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="32cd5-233">次のコードは、SignalR 2 プロジェクトで CORS または JSONP を有効にする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="32cd5-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="32cd5-234">このコード サンプル`Map`では`RunSignalR``MapSignalR`、 の代わりに を使用し、CORS ミドルウェアは、(で指定されたパスのすべてのトラフィックではなく) CORS サポートを必要`MapSignalR`とする SignalR 要求に対してのみ実行されるようにします。Map は、アプリケーション全体ではなく、特定の URL プレフィックスに対して実行する必要がある他のミドルウェアにも使用できます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="32cd5-235">コード内で`jQuery.support.cors`true に設定しないでください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![jQuery.support.cors を true に設定しないでください。](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="32cd5-237">信号機は CORS の使用を処理します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="32cd5-238">true`jQuery.support.cors`に設定すると、ブラウザーが CORS をサポートしていると SignalR が想定されるため、JSONP が無効になります。</span><span class="sxs-lookup"><span data-stu-id="32cd5-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="32cd5-239">ローカル ホスト URL に接続している場合、Internet Explorer 10 はドメイン間接続とは見なされないので、サーバーでドメイン間接続を有効にしていない場合でも、アプリケーションは IE 10 でローカルに動作します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="32cd5-240">Internet Explorer 9 でのドメイン間接続の使用については、[この StackOverflow スレッド](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="32cd5-241">Chrome でのクロスドメイン接続の使用については、[この StackOverflow スレッド](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="32cd5-242">サンプル コードでは、既定の "/signalr" URL を使用して SignalR サービスに接続します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="32cd5-243">別のベース URL を指定する方法については、「 [signalr Hubs API ガイド ASP.NET - サーバー - /signalr URL](hubs-api-guide-server.md#signalrurl)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="32cd5-244">接続の構成方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-244">How to configure the connection</span></span>

<span data-ttu-id="32cd5-245">接続を確立する前に、クエリ文字列パラメーターを指定するか、トランスポートメソッドを指定できます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="32cd5-246">クエリ文字列パラメーターの指定方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-246">How to specify query string parameters</span></span>

<span data-ttu-id="32cd5-247">クライアントが接続するときにサーバーにデータを送信する場合は、接続オブジェクトにクエリ文字列パラメーターを追加できます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="32cd5-248">次の例は、クライアント コードでクエリ文字列パラメーターを設定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="32cd5-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="32cd5-249">**START メソッドを呼び出す前にクエリ文字列値を設定します (生成されたプロキシを使用)。**</span><span class="sxs-lookup"><span data-stu-id="32cd5-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="32cd5-250">**start メソッドを呼び出す前にクエリ文字列値を設定します (生成されたプロキシを使用しない場合)。**</span><span class="sxs-lookup"><span data-stu-id="32cd5-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="32cd5-251">サーバー コードでクエリ文字列パラメーターを読み取る方法を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="32cd5-252">トランスポート方法の指定方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-252">How to specify the transport method</span></span>

<span data-ttu-id="32cd5-253">SignalR クライアントは、接続プロセスの一部として、通常、サーバーとネゴシエートして、サーバーとクライアントの両方でサポートされている最適なトランスポートを決定します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="32cd5-254">使用するトランスポートが既にわかっている場合は、メソッドの呼び出し時にトランスポート メソッドを指定することで、このネゴシエーション`start`プロセスをバイパスできます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="32cd5-255">**トランスポート メソッドを指定するクライアント コード (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="32cd5-256">**転送方法を指定するクライアント コード (生成されたプロキシを使用しない)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="32cd5-257">代わりに、SignalR で試す順序で複数のトランスポート方法を指定できます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="32cd5-258">**カスタム 転送フォールバック スキームを指定するクライアント コード (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="32cd5-259">**カスタム 転送フォールバック スキームを指定するクライアント コード (生成されたプロキシを使用しない)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="32cd5-260">トランスポート方式の指定には、以下の値を使用できます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="32cd5-261">"ウェブソケット"</span><span class="sxs-lookup"><span data-stu-id="32cd5-261">"webSockets"</span></span>
- <span data-ttu-id="32cd5-262">「フォーエバーフレーム」</span><span class="sxs-lookup"><span data-stu-id="32cd5-262">"foreverFrame"</span></span>
- <span data-ttu-id="32cd5-263">"サーバー送信イベント"</span><span class="sxs-lookup"><span data-stu-id="32cd5-263">"serverSentEvents"</span></span>
- <span data-ttu-id="32cd5-264">"ロングポーリング"</span><span class="sxs-lookup"><span data-stu-id="32cd5-264">"longPolling"</span></span>

<span data-ttu-id="32cd5-265">次の例は、接続で使用されているトランスポート方法を調べる方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="32cd5-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="32cd5-266">**接続で使用されるトランスポートメソッドを表示するクライアント コード (生成されたプロキシとの)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="32cd5-267">**接続で使用されるトランスポートメソッドを表示するクライアント コード (生成されたプロキシを使用しない)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="32cd5-268">サーバー コードでトランスポート メソッドを確認する方法については、「 [ASP.NET SignalR Hubs API ガイド - サーバー - Context プロパティからクライアントに関する情報を取得する方法](hubs-api-guide-server.md#contextproperty)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="32cd5-269">トランスポートとフォールバックの詳細については、「 [SignalR の概要 - トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="32cd5-270">ハブ クラスのプロキシを取得する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="32cd5-271">作成する各接続オブジェクトは、1 つ以上のハブ クラスを含む SignalR サービスへの接続に関する情報をカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="32cd5-272">ハブ クラスと通信するには、自分で作成した (生成されたプロキシを使用していない場合) または生成されるプロキシ オブジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="32cd5-273">クライアントでは、プロキシ名はキャメル大文字バージョンのハブ クラス名です。</span><span class="sxs-lookup"><span data-stu-id="32cd5-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="32cd5-274">SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。</span><span class="sxs-lookup"><span data-stu-id="32cd5-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="32cd5-275">**サーバー上のハブ クラス**</span><span class="sxs-lookup"><span data-stu-id="32cd5-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="32cd5-276">**ハブの生成されたクライアント プロキシへの参照を取得します。**</span><span class="sxs-lookup"><span data-stu-id="32cd5-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="32cd5-277">**ハブ クラスのクライアント プロキシを作成する (プロキシを生成しない)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="32cd5-278">属性を使用してハブ クラスを`HubName`修飾する場合は、大文字と小文字を変更せずに正確な名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="32cd5-279">**ハブ名属性を持つサーバー上のハブ クラス**</span><span class="sxs-lookup"><span data-stu-id="32cd5-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="32cd5-280">**ハブの生成されたクライアント プロキシへの参照を取得します。**</span><span class="sxs-lookup"><span data-stu-id="32cd5-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="32cd5-281">**ハブ クラスのクライアント プロキシを作成する (プロキシを生成しない)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="32cd5-282">サーバーが呼び出すことができるクライアント上のメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="32cd5-283">ハブからサーバーが呼び出すことができるメソッドを定義するには、生成されたプロキシの`client`プロパティを使用してイベント ハンドラーをハブ プロキシに追加するか、生成`on`されたプロキシを使用していない場合はメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="32cd5-284">パラメーターは、複雑なオブジェクトにできます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="32cd5-285">メソッドを呼び出して接続を`start`確立する前に、イベント ハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="32cd5-286">(メソッドを呼び出した後にイベント`start`ハンドラーを追加する場合は、このドキュメントの前半の[「接続を確立する方法](#establishconnection)」の注を参照し、生成されたプロキシを使用せずにメソッドを定義する構文を使用します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="32cd5-287">メソッド名の一致は大文字と小文字を区別しません。</span><span class="sxs-lookup"><span data-stu-id="32cd5-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="32cd5-288">たとえば、`Clients.All.addContosoChatMessageToPage`サーバー上で、 、 `AddContosoChatMessageToPage` `addContosoChatMessageToPage`、または`addcontosochatmessagetopage`をクライアントで実行します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="32cd5-289">**クライアント上のメソッドの定義 (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="32cd5-290">**クライアント上でメソッドを定義する別の方法 (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="32cd5-291">**クライアントでメソッドを定義する (生成されたプロキシを使用しない、または start メソッドを呼び出した後に追加する場合)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="32cd5-292">**クライアント メソッドを呼び出すサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="32cd5-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="32cd5-293">以下の例には、メソッドパラメータとして複合オブジェクトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="32cd5-294">**複雑なオブジェクトを受け取るクライアント上のメソッドを定義する (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="32cd5-295">**複雑なオブジェクトを受け取るクライアント上のメソッドを定義する (生成されたプロキシを使用しない)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="32cd5-296">**複合オブジェクトを定義するサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="32cd5-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="32cd5-297">**複雑なオブジェクトを使用してクライアント メソッドを呼び出すサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="32cd5-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="32cd5-298">クライアントからサーバー メソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-298">How to call server methods from the client</span></span>

<span data-ttu-id="32cd5-299">クライアントからサーバー メソッドを呼び出す場合`server`は、生成されたプロキシのプロパティ`invoke`を使用するか、生成されたプロキシを使用していない場合はハブ プロキシのメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="32cd5-300">戻り値またはパラメーターは、複雑なオブジェクトにできます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="32cd5-301">ハブでメソッド名のキャメルケースバージョンを渡します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="32cd5-302">SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。</span><span class="sxs-lookup"><span data-stu-id="32cd5-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="32cd5-303">次の例は、戻り値を持たないサーバー メソッドを呼び出す方法と、戻り値を持つサーバー メソッドを呼び出す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="32cd5-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="32cd5-304">**ハブメソッド名属性を持たないサーバー メソッド**</span><span class="sxs-lookup"><span data-stu-id="32cd5-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="32cd5-305">**パラメーターで渡される複合オブジェクトを定義するサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="32cd5-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="32cd5-306">**サーバー メソッドを呼び出すクライアント コード (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="32cd5-307">**サーバー メソッドを呼び出すクライアント コード (生成されたプロキシを使用しない)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="32cd5-308">属性を使用して Hub メソッドを`HubMethodName`修飾する場合は、大文字と小文字を変更せずにその名前を使用します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="32cd5-309">属性を持つ**サーバー メソッド**</span><span class="sxs-lookup"><span data-stu-id="32cd5-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="32cd5-310">**サーバー メソッドを呼び出すクライアント コード (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="32cd5-311">**サーバー メソッドを呼び出すクライアント コード (生成されたプロキシを使用しない)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="32cd5-312">上記の例では、戻り値のないサーバー メソッドを呼び出す方法を示します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="32cd5-313">次の例は、戻り値を持つサーバー メソッドを呼び出す方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="32cd5-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="32cd5-314">**戻り値を持つメソッドのサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="32cd5-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="32cd5-315">**戻り値に使用される Stock クラス**</span><span class="sxs-lookup"><span data-stu-id="32cd5-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="32cd5-316">**サーバー メソッドを呼び出すクライアント コード (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="32cd5-317">**サーバー メソッドを呼び出すクライアント コード (生成されたプロキシを使用しない)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="32cd5-318">接続の有効期間イベントを処理する方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="32cd5-319">SignalR は、次の接続有効期間イベントを処理できます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="32cd5-320">`starting`: 接続を介してデータが送信される前に発生します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="32cd5-321">`received`: 接続でデータが受信されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="32cd5-322">受信したデータを提供します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-322">Provides the received data.</span></span>
- <span data-ttu-id="32cd5-323">`connectionSlow`: クライアントが低速または頻繁に切断する接続を検出したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="32cd5-324">`reconnecting`: 基になるトランスポートの再接続が開始されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="32cd5-325">`reconnected`: 基になるトランスポートが再接続されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="32cd5-326">`stateChanged`: 接続状態が変化したときに発生します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="32cd5-327">古い状態と新しい状態 (接続、接続、再接続、または切断) を提供します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="32cd5-328">`disconnected`: 接続が切断されたときに発生します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="32cd5-329">たとえば、接続の問題が原因で顕著な遅延が発生した場合に警告メッセージを表示する場合は、`connectionSlow`イベントを処理します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="32cd5-330">**接続を処理するSlowイベント (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="32cd5-331">**接続を処理するSlowイベント (生成されたプロキシを使用しない)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="32cd5-332">詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](handling-connection-lifetime-events.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="32cd5-333">エラーの処理方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-333">How to handle errors</span></span>

<span data-ttu-id="32cd5-334">SignalR JavaScript クライアントは`error`、ハンドラーを追加できるイベントを提供します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="32cd5-335">fail メソッドを使用して、サーバー メソッドの呼び出しによって発生するエラーのハンドラーを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="32cd5-336">サーバーで詳細なエラー メッセージを明示的に有効にしない場合、SignalR がエラーの後に返す例外オブジェクトには、エラーに関する最小限の情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="32cd5-337">たとえば、呼び出しが`newContosoChatMessage`失敗した場合、エラー オブジェクトのエラー メッセージ`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`には、セキュリティ上の理由から、運用環境のクライアントに詳細なエラー メッセージを送信することは推奨されませんが、トラブルシューティングの目的で詳細なエラー メッセージを有効にする場合は、サーバーで次のコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="32cd5-338">次の例は、エラー イベントのハンドラーを追加する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="32cd5-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="32cd5-339">**エラー ハンドラを追加する (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="32cd5-340">**エラー ハンドラを追加する (生成されたプロキシを除く)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="32cd5-341">メソッド呼び出しからのエラーを処理する方法を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="32cd5-342">**メソッド呼び出しからのエラーの処理 (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="32cd5-343">**メソッド呼び出しからのエラーの処理 (生成されたプロキシを除く)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="32cd5-344">メソッドの呼び出しが`error`失敗した場合、イベントも発生するため、`error`メソッド ハンドラーとメソッド`.fail`コールバック内のコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="32cd5-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="32cd5-345">クライアント側のログを有効にする方法</span><span class="sxs-lookup"><span data-stu-id="32cd5-345">How to enable client-side logging</span></span>

<span data-ttu-id="32cd5-346">接続でクライアント側のログを有効にするには、接続を`logging`確立するメソッドを呼び出す前`start`に、接続オブジェクトのプロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="32cd5-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="32cd5-347">**ログ記録を有効にする (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="32cd5-348">**ログを有効にする (生成されたプロキシを使用しない)**</span><span class="sxs-lookup"><span data-stu-id="32cd5-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="32cd5-349">ログを表示するには、ブラウザの開発者ツールを開き、[コンソール] タブに移動します。この方法を示す手順とスクリーン ショットを示すチュートリアルについては[、「ASP.NET Signalr を使用したサーバー ブロードキャスト - ログ記録を有効にする](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="32cd5-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>
