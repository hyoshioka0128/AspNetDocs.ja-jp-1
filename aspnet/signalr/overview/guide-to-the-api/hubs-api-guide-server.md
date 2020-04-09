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
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="57d63-103">ASP.NET SignalR ハブ API ガイド - サーバー (C#)</span><span class="sxs-lookup"><span data-stu-id="57d63-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="57d63-104">[パトリック・フレッチャー](https://github.com/pfletcher),[トム・ダイクストラ](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="57d63-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="57d63-105">このドキュメントでは、一般的なオプションを示すコード サンプルを含む、signalR バージョン 2 の ASP.NET SignalR Hubs API のサーバー側のプログラミングの概要を示します。</span><span class="sxs-lookup"><span data-stu-id="57d63-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="57d63-106">SignalR Hubs API を使用すると、サーバーから接続されたクライアント、およびクライアントからサーバーへのリモート プロシージャ コール (RPC) を作成できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="57d63-107">サーバー コードでは、クライアントから呼び出すことができるメソッドを定義し、クライアントで実行されるメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="57d63-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="57d63-108">クライアント コードでは、サーバーから呼び出すことができるメソッドを定義し、サーバーで実行されるメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="57d63-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="57d63-109">SignalR は、クライアントからサーバーへのすべての配管を処理します。</span><span class="sxs-lookup"><span data-stu-id="57d63-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="57d63-110">SignalR は、固定接続と呼ばれる下位レベルの API も提供します。</span><span class="sxs-lookup"><span data-stu-id="57d63-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="57d63-111">SignalR、ハブ、および固定接続の概要については[、SignalR 2 の概要を](../getting-started/introduction-to-signalr.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="57d63-112">このトピックで使用するソフトウェアバージョン</span><span class="sxs-lookup"><span data-stu-id="57d63-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="57d63-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="57d63-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="57d63-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="57d63-114">.NET 4.5</span></span>
> - <span data-ttu-id="57d63-115">シグナル・バージョン 2</span><span class="sxs-lookup"><span data-stu-id="57d63-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="57d63-116">トピックのバージョン</span><span class="sxs-lookup"><span data-stu-id="57d63-116">Topic versions</span></span>
> 
> <span data-ttu-id="57d63-117">SignalR の以前のバージョンについては[、SignalR の古いバージョン](../older-versions/index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="57d63-118">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="57d63-118">Questions and comments</span></span>
> 
> <span data-ttu-id="57d63-119">このチュートリアルを気に入った方法と、ページの下部にあるコメントで改善できる内容についてのフィードバックを残してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="57d63-120">チュートリアルに直接関連しない質問がある場合は[、ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="57d63-121">概要</span><span class="sxs-lookup"><span data-stu-id="57d63-121">Overview</span></span>

<span data-ttu-id="57d63-122">このドキュメントは、次のトピックに分かれています。</span><span class="sxs-lookup"><span data-stu-id="57d63-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="57d63-123">SignalR ミドルウェアを登録する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="57d63-124">/シグナルの URL</span><span class="sxs-lookup"><span data-stu-id="57d63-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="57d63-125">シグナル・オプションの構成</span><span class="sxs-lookup"><span data-stu-id="57d63-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="57d63-126">ハブ クラスを作成して使用する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="57d63-127">ハブ オブジェクトの有効期間</span><span class="sxs-lookup"><span data-stu-id="57d63-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="57d63-128">JavaScript クライアントにおけるハブ名のキャメルケーシング</span><span class="sxs-lookup"><span data-stu-id="57d63-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="57d63-129">複数のハブ</span><span class="sxs-lookup"><span data-stu-id="57d63-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="57d63-130">厳密に型指定されたハブ</span><span class="sxs-lookup"><span data-stu-id="57d63-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="57d63-131">クライアントが呼び出すことができるハブ クラスでメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="57d63-132">JavaScript クライアントにおけるメソッド名のキャメル・ケーシング</span><span class="sxs-lookup"><span data-stu-id="57d63-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="57d63-133">非同期で実行する場合</span><span class="sxs-lookup"><span data-stu-id="57d63-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="57d63-134">オーバーロードの定義</span><span class="sxs-lookup"><span data-stu-id="57d63-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="57d63-135">ハブ メソッド呼び出しからの進行状況のレポート</span><span class="sxs-lookup"><span data-stu-id="57d63-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="57d63-136">ハブ クラスからクライアント メソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="57d63-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="57d63-137">RPC を受信するクライアントの選択</span><span class="sxs-lookup"><span data-stu-id="57d63-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="57d63-138">メソッド名のコンパイル時検証なし</span><span class="sxs-lookup"><span data-stu-id="57d63-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="57d63-139">大文字と小文字を区別しないメソッド名の一致</span><span class="sxs-lookup"><span data-stu-id="57d63-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="57d63-140">非同期実行</span><span class="sxs-lookup"><span data-stu-id="57d63-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="57d63-141">ハブ クラスからグループ メンバーシップを管理する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="57d63-142">Add メソッドと Remove メソッドの非同期実行</span><span class="sxs-lookup"><span data-stu-id="57d63-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="57d63-143">グループ メンバーシップの永続性</span><span class="sxs-lookup"><span data-stu-id="57d63-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="57d63-144">シングルユーザー グループ</span><span class="sxs-lookup"><span data-stu-id="57d63-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="57d63-145">ハブ クラスで接続の有効期間イベントを処理する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="57d63-146">オン接続、オン・オンライン切断、およびオン再接続が呼び出された場合</span><span class="sxs-lookup"><span data-stu-id="57d63-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="57d63-147">呼び出し元の状態が入力されていません</span><span class="sxs-lookup"><span data-stu-id="57d63-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="57d63-148">Context プロパティからクライアントに関する情報を取得する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="57d63-149">クライアントとハブ クラスの間で状態を渡す方法</span><span class="sxs-lookup"><span data-stu-id="57d63-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="57d63-150">ハブ クラスのエラーを処理する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="57d63-151">ハブ クラスの外部からクライアント メソッドを呼び出し、グループを管理する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="57d63-152">クライアント メソッドの呼び出し</span><span class="sxs-lookup"><span data-stu-id="57d63-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="57d63-153">グループ メンバーシップの管理</span><span class="sxs-lookup"><span data-stu-id="57d63-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="57d63-154">トレースを有効にする方法</span><span class="sxs-lookup"><span data-stu-id="57d63-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="57d63-155">ハブ パイプラインをカスタマイズする方法</span><span class="sxs-lookup"><span data-stu-id="57d63-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="57d63-156">クライアントのプログラミング方法に関するドキュメントについては、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="57d63-157">シグナルハブ API ガイド - JavaScript クライアント</span><span class="sxs-lookup"><span data-stu-id="57d63-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="57d63-158">SignalR ハブ API ガイド - .NET クライアント</span><span class="sxs-lookup"><span data-stu-id="57d63-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="57d63-159">SignalR 2 のサーバー コンポーネントは、.NET 4.5 でのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="57d63-160">NET 4.0 を実行しているサーバーは、SignalR v1.x を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="57d63-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="57d63-161">SignalR ミドルウェアを登録する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-161">How to register SignalR middleware</span></span>

<span data-ttu-id="57d63-162">クライアントがハブへの接続に使用するルートを定義するには、アプリケーションの起動時`MapSignalR`にメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="57d63-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="57d63-163">`MapSignalR`は、クラスの[拡張メソッド](https://msdn.microsoft.com/library/vstudio/bb383977.aspx)です`OwinExtensions`。</span><span class="sxs-lookup"><span data-stu-id="57d63-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="57d63-164">次の例は、OWIN スタートアップ クラスを使用して SignalR ハブ ルートを定義する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="57d63-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="57d63-165">ASP.NET MVC アプリケーションに SignalR 機能を追加する場合は、SignalR ルートが他のルートの前に追加されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="57d63-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="57d63-166">詳細については、「[チュートリアル: SignalR 2 と MVC 5 の概要](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="57d63-167">/シグナルの URL</span><span class="sxs-lookup"><span data-stu-id="57d63-167">The /signalr URL</span></span>

<span data-ttu-id="57d63-168">デフォルトでは、クライアントがハブへの接続に使用するルート URL は"/signalr"です。</span><span class="sxs-lookup"><span data-stu-id="57d63-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="57d63-169">(この URL を、自動生成された JavaScript ファイル用の "/signalr/hubs" URL と混同しないでください。</span><span class="sxs-lookup"><span data-stu-id="57d63-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="57d63-170">生成されたプロキシの詳細については[、SignalR Hubs API ガイド - JavaScript クライアント - 生成されたプロキシと、それがあなたのために何をするのか](hubs-api-guide-javascript-client.md#genproxy)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="57d63-171">このベース URL を SignalR で使用できないという特別な状況が発生する可能性があります。たとえば、プロジェクト内に*signalr*という名前のフォルダーがあり、名前を変更したくないとします。</span><span class="sxs-lookup"><span data-stu-id="57d63-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="57d63-172">その場合は、次の例に示すように、ベース URL を変更できます (サンプル コードの "/signalr" を目的の URL に置き換えます)。</span><span class="sxs-lookup"><span data-stu-id="57d63-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="57d63-173">**URL を指定するサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="57d63-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="57d63-174">**URL を指定する JavaScript クライアント コード (生成されたプロキシを使用)**</span><span class="sxs-lookup"><span data-stu-id="57d63-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="57d63-175">**URL を指定する JavaScript クライアント コード (生成されたプロキシを除く)**</span><span class="sxs-lookup"><span data-stu-id="57d63-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="57d63-176">**URL を指定する .NET クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="57d63-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="57d63-177">シグナル・オプションの構成</span><span class="sxs-lookup"><span data-stu-id="57d63-177">Configuring SignalR Options</span></span>

<span data-ttu-id="57d63-178">`MapSignalR`メソッドのオーバーロードを使用すると、カスタム URL、カスタム依存関係リゾルバー、および次のオプションを指定できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="57d63-179">ブラウザー クライアントからの CORS または JSONP を使用して、クロスドメイン呼び出しを有効にします。</span><span class="sxs-lookup"><span data-stu-id="57d63-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="57d63-180">通常、ブラウザが から`http://contoso.com`ページを読み込む場合、SignalR 接続は`http://contoso.com/signalr`同じドメインの で、 で行われます。</span><span class="sxs-lookup"><span data-stu-id="57d63-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="57d63-181">ページが に`http://contoso.com`接続する`http://fabrikam.com/signalr`場合、これはドメイン間接続です。</span><span class="sxs-lookup"><span data-stu-id="57d63-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="57d63-182">セキュリティ上の理由から、ドメイン間の接続は既定で無効になっています。</span><span class="sxs-lookup"><span data-stu-id="57d63-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="57d63-183">詳細については[、「ASP.NET SignalR Hubs API ガイド - JavaScript クライアント - クロスドメイン接続を確立する方法」](hubs-api-guide-javascript-client.md#crossdomain)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="57d63-184">詳細なエラー メッセージを有効にします。</span><span class="sxs-lookup"><span data-stu-id="57d63-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="57d63-185">エラーが発生した場合、SignalR の既定の動作では、何が起きたかについての詳細を通知メッセージをクライアントに送信します。</span><span class="sxs-lookup"><span data-stu-id="57d63-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="57d63-186">悪意のあるユーザーがアプリケーションに対する攻撃で情報を使用する可能性があるため、クライアントに詳細なエラー情報を送信することは推奨されません。</span><span class="sxs-lookup"><span data-stu-id="57d63-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="57d63-187">トラブルシューティングのために、このオプションを使用して、より有益なエラー報告を一時的に有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="57d63-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="57d63-188">自動生成された JavaScript プロキシ ファイルを無効にします。</span><span class="sxs-lookup"><span data-stu-id="57d63-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="57d63-189">デフォルトでは、ハブクラスのプロキシを持つ JavaScript ファイルは、URL "/signalr/hubs" に応答して生成されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="57d63-190">JavaScript プロキシを使用しない場合、またはこのファイルを手動で生成してクライアントの物理ファイルを参照する場合は、このオプションを使用してプロキシ生成を無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="57d63-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="57d63-191">詳細については、「 [SignalR ハブ API ガイド - JavaScript クライアント - SignalR で生成されたプロキシの物理ファイルを作成する方法](hubs-api-guide-javascript-client.md#manualproxy)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="57d63-192">次の例は、SignalR 接続 URL と、メソッドの呼び出し`MapSignalR`でこれらのオプションを指定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="57d63-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="57d63-193">カスタム URL を指定するには、例の 「/signalr」を使用する URL に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="57d63-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="57d63-194">ハブ クラスを作成して使用する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-194">How to create and use Hub classes</span></span>

<span data-ttu-id="57d63-195">ハブを作成するには、から派生するクラス[を](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)作成します。</span><span class="sxs-lookup"><span data-stu-id="57d63-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="57d63-196">チャット アプリケーションの単純な Hub クラスの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="57d63-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="57d63-197">この例では、接続されたクライアントがメソッドを`NewContosoChatMessage`呼び出し、呼び出すと、受信したデータが接続されているすべてのクライアントにブロードキャストされます。</span><span class="sxs-lookup"><span data-stu-id="57d63-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="57d63-198">ハブ オブジェクトの有効期間</span><span class="sxs-lookup"><span data-stu-id="57d63-198">Hub object lifetime</span></span>

<span data-ttu-id="57d63-199">ハブ クラスをインスタンス化したり、サーバー上の独自のコードからそのメソッドを呼び出したりしないでください。SignalR ハブ パイプラインによって行われるすべてのことを示します。</span><span class="sxs-lookup"><span data-stu-id="57d63-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="57d63-200">SignalR は、クライアントがサーバーに対して接続、切断、またはメソッド呼び出しを行う場合など、ハブの操作を処理する必要があるたびに、ハブ クラスの新しいインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="57d63-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="57d63-201">Hub クラスのインスタンスは一時的なものであるため、メソッド呼び出しから次のメソッド呼び出しの状態を維持するために使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="57d63-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="57d63-202">サーバーがクライアントからメソッド呼び出しを受け取るたびに、ハブ クラスの新しいインスタンスがメッセージを処理します。</span><span class="sxs-lookup"><span data-stu-id="57d63-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="57d63-203">複数の接続とメソッド呼び出しを通じて状態を維持するには、データベース、ハブ クラスの静的変数、または から`Hub`派生していない別のクラスなど、他のメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="57d63-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="57d63-204">データをメモリに保持する場合、ハブ クラスの静的変数などのメソッドを使用すると、アプリ ドメインがリサイクルされるときにデータが失われます。</span><span class="sxs-lookup"><span data-stu-id="57d63-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="57d63-205">ハブ クラスの外部で実行される独自のコードからクライアントにメッセージを送信する場合は、ハブ クラスインスタンスをインスタンス化して送信することはできませんが、ハブ クラスの SignalR コンテキスト オブジェクトへの参照を取得することで送信できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="57d63-206">詳細については、このトピックの後半の[「Hub クラスの外部からクライアント メソッドを呼び出し、グループを管理する方法](#callfromoutsidehub)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="57d63-207">JavaScript クライアントにおけるハブ名のキャメルケーシング</span><span class="sxs-lookup"><span data-stu-id="57d63-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="57d63-208">デフォルトでは、JavaScript クライアントはキャメルケースバージョンのクラス名を使用してハブを参照します。</span><span class="sxs-lookup"><span data-stu-id="57d63-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="57d63-209">SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。</span><span class="sxs-lookup"><span data-stu-id="57d63-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="57d63-210">前の例は JavaScript`contosoChatHub`コードと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="57d63-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="57d63-211">**[サーバー]**</span><span class="sxs-lookup"><span data-stu-id="57d63-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="57d63-212">**生成されたプロキシを使用した JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="57d63-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="57d63-213">クライアントが使用する別の名前を指定する場合は、属性を`HubName`追加します。</span><span class="sxs-lookup"><span data-stu-id="57d63-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="57d63-214">属性を`HubName`使用する場合、JavaScript クライアントでキャメル ケースに名前が変更されません。</span><span class="sxs-lookup"><span data-stu-id="57d63-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="57d63-215">**[サーバー]**</span><span class="sxs-lookup"><span data-stu-id="57d63-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="57d63-216">**生成されたプロキシを使用した JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="57d63-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="57d63-217">複数のハブ</span><span class="sxs-lookup"><span data-stu-id="57d63-217">Multiple Hubs</span></span>

<span data-ttu-id="57d63-218">アプリケーションでは、複数のハブ クラスを定義できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="57d63-219">これを行うと、接続は共有されますが、グループは別々になります。</span><span class="sxs-lookup"><span data-stu-id="57d63-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="57d63-220">すべてのクライアントは、サービスとの SignalR 接続 (指定した場合は "signalr" またはカスタム URL) を確立するために同じ URL を使用し、その接続はサービスによって定義されたすべてのハブに使用されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="57d63-221">1 つのクラスですべてのハブ機能を定義するのと比較して、複数のハブのパフォーマンスの違いはありません。</span><span class="sxs-lookup"><span data-stu-id="57d63-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="57d63-222">すべてのハブは同じ HTTP 要求情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="57d63-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="57d63-223">すべてのハブが同じ接続を共有するため、サーバーが取得する唯一の HTTP 要求情報は、SignalR 接続を確立する元の HTTP 要求に含まれるものになります。</span><span class="sxs-lookup"><span data-stu-id="57d63-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="57d63-224">接続要求を使用してクエリ文字列を指定してクライアントからサーバーに情報を渡す場合、異なるクエリ文字列を異なるハブに提供することはできません。</span><span class="sxs-lookup"><span data-stu-id="57d63-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="57d63-225">すべてのハブは同じ情報を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="57d63-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="57d63-226">生成された JavaScript プロキシ ファイルには、1 つのファイル内のすべてのハブのプロキシが含まれます。</span><span class="sxs-lookup"><span data-stu-id="57d63-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="57d63-227">JavaScript プロキシの詳細については、「 [SignalR Hubs API ガイド - JavaScript クライアント - 生成されたプロキシと、それがあなたのために何をするのか](hubs-api-guide-javascript-client.md#genproxy)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="57d63-228">グループはハブ内で定義されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="57d63-229">SignalR では、接続されたクライアントのサブセットにブロードキャストする名前付きグループを定義できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="57d63-230">グループは、ハブごとに個別に管理されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="57d63-231">たとえば、"Administrators" という名前のグループには`ContosoChatHub`、クラスのクライアントのセットが 1 つ含まれ、同じグループ名がクラスの異なる`StockTickerHub`クライアント セットを参照します。</span><span class="sxs-lookup"><span data-stu-id="57d63-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="57d63-232">厳密に型指定されたハブ</span><span class="sxs-lookup"><span data-stu-id="57d63-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="57d63-233">クライアントが参照できるハブ メソッドのインターフェイスを定義し (ハブ メソッドで Intellisense を有効にする)、ハブを (SignalR 2.1`Hub`で紹介) ではなくから`Hub<T>`派生させるには、</span><span class="sxs-lookup"><span data-stu-id="57d63-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="57d63-234">クライアントが呼び出すことができるハブ クラスでメソッドを定義する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="57d63-235">クライアントから呼び出し可能にするメソッドをハブで公開するには、次の例に示すように、パブリック メソッドを宣言します。</span><span class="sxs-lookup"><span data-stu-id="57d63-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="57d63-236">C# メソッドの場合と同様に、複合型や配列を含む戻り値の型とパラメーターを指定できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="57d63-237">パラメーターで受け取ったデータや呼び出し元に返されるデータは、JSON を使用してクライアントとサーバー間で通信され、SignalR は複雑なオブジェクトとオブジェクトの配列のバインドを自動的に処理します。</span><span class="sxs-lookup"><span data-stu-id="57d63-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="57d63-238">JavaScript クライアントにおけるメソッド名のキャメル・ケーシング</span><span class="sxs-lookup"><span data-stu-id="57d63-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="57d63-239">デフォルトでは、JavaScript クライアントは、キャメルケースバージョンのメソッド名を使用してハブメソッドを参照します。</span><span class="sxs-lookup"><span data-stu-id="57d63-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="57d63-240">SignalR は、JavaScript コードが JavaScript の規則に準拠できるように、この変更を自動的に行います。</span><span class="sxs-lookup"><span data-stu-id="57d63-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="57d63-241">**[サーバー]**</span><span class="sxs-lookup"><span data-stu-id="57d63-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="57d63-242">**生成されたプロキシを使用した JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="57d63-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="57d63-243">クライアントが使用する別の名前を指定する場合は、属性を`HubMethodName`追加します。</span><span class="sxs-lookup"><span data-stu-id="57d63-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="57d63-244">**[サーバー]**</span><span class="sxs-lookup"><span data-stu-id="57d63-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="57d63-245">**生成されたプロキシを使用した JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="57d63-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="57d63-246">非同期で実行する場合</span><span class="sxs-lookup"><span data-stu-id="57d63-246">When to execute asynchronously</span></span>

<span data-ttu-id="57d63-247">メソッドが長時間実行される場合、またはデータベースの参照や Web サービスの呼び出しなど、待機する作業を実行する必要がある場合は、戻り値の代わりに Task オブジェクトまたは[&lt;Task&gt; T](https://msdn.microsoft.com/library/dd321424.aspx)オブジェクトを`T`返してハブ メソッドを非同期にします (戻り値の[Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)`void`型の代わりに)。</span><span class="sxs-lookup"><span data-stu-id="57d63-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="57d63-248">メソッドからオブジェクトを`Task`返すと、SignalR は完了`Task`するまで待機し、ラップされていない結果をクライアントに返すため、クライアントでのメソッド呼び出しのコーディング方法に違いはありません。</span><span class="sxs-lookup"><span data-stu-id="57d63-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="57d63-249">ハブ メソッドを非同期にすると、WebSocket トランスポートを使用する場合に接続がブロックされないようにします。</span><span class="sxs-lookup"><span data-stu-id="57d63-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="57d63-250">ハブ メソッドが同期的に実行され、トランスポートが WebSocket の場合、ハブ メソッドが完了するまで、同じクライアントからハブ上のメソッドの後続の呼び出しがブロックされます。</span><span class="sxs-lookup"><span data-stu-id="57d63-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="57d63-251">同期または非同期で実行するコードと同じメソッドの後に、いずれかのバージョンを呼び出すために機能する JavaScript クライアント コードを次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="57d63-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="57d63-252">**同期**</span><span class="sxs-lookup"><span data-stu-id="57d63-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="57d63-253">**非同期**</span><span class="sxs-lookup"><span data-stu-id="57d63-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="57d63-254">**生成されたプロキシを使用した JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="57d63-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="57d63-255">ASP.NET 4.5 で非同期メソッドを使用する方法の詳細については[、「ASP.NET MVC 4 での非同期メソッドの使用](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="57d63-256">オーバーロードの定義</span><span class="sxs-lookup"><span data-stu-id="57d63-256">Defining Overloads</span></span>

<span data-ttu-id="57d63-257">メソッドのオーバーロードを定義する場合は、各オーバーロードのパラメーター数が異なる必要があります。</span><span class="sxs-lookup"><span data-stu-id="57d63-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="57d63-258">異なるパラメーター型を指定するだけでオーバーロードを区別する場合、ハブ クラスはコンパイルされますが、クライアントがいずれかのオーバーロードを呼び出そうとする実行時に SignalR サービスによって例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="57d63-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="57d63-259">ハブ メソッド呼び出しからの進行状況のレポート</span><span class="sxs-lookup"><span data-stu-id="57d63-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="57d63-260">SignalR 2.1 では、.NET 4.5 で導入された[進行状況レポート パターン](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx)のサポートが追加されました。</span><span class="sxs-lookup"><span data-stu-id="57d63-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="57d63-261">進捗レポートを実装するには、`IProgress<T>`クライアントがアクセスできるハブ メソッドのパラメーターを定義します。</span><span class="sxs-lookup"><span data-stu-id="57d63-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="57d63-262">実行時間の長いサーバー メソッドを記述する場合は、ハブ スレッドをブロックするのではなく、非同期プログラミング パターンを使用することが重要です。</span><span class="sxs-lookup"><span data-stu-id="57d63-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="57d63-263">ハブ クラスからクライアント メソッドを呼び出す方法</span><span class="sxs-lookup"><span data-stu-id="57d63-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="57d63-264">サーバーからクライアント メソッドを呼び出す`Clients`場合は、Hub クラスのメソッドでプロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="57d63-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="57d63-265">接続されているすべてのクライアントで呼び出す`addNewMessageToPage`サーバー コードと、JavaScript クライアントでメソッドを定義するクライアント コードの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="57d63-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="57d63-266">**[サーバー]**</span><span class="sxs-lookup"><span data-stu-id="57d63-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="57d63-267">クライアント メソッドの呼び出しは非同期操作であり`Task`、 を返します。</span><span class="sxs-lookup"><span data-stu-id="57d63-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="57d63-268">`await` を使用して次のことを行います。</span><span class="sxs-lookup"><span data-stu-id="57d63-268">Use `await`:</span></span>

* <span data-ttu-id="57d63-269">メッセージがエラーなしで送信されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="57d63-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="57d63-270">try-catch ブロックでエラーのキャッチと処理を有効にします。</span><span class="sxs-lookup"><span data-stu-id="57d63-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="57d63-271">**生成されたプロキシを使用した JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="57d63-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="57d63-272">クライアント メソッドから戻り値を取得することはできません。構文が機能`int x = Clients.All.add(1,1)`しないなどの構文。</span><span class="sxs-lookup"><span data-stu-id="57d63-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="57d63-273">パラメーターには、複合型と配列を指定できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="57d63-274">メソッド パラメーターで複合型をクライアントに渡す例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="57d63-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="57d63-275">**複雑なオブジェクトを使用してクライアント メソッドを呼び出すサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="57d63-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="57d63-276">**複合オブジェクトを定義するサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="57d63-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="57d63-277">**生成されたプロキシを使用した JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="57d63-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="57d63-278">RPC を受信するクライアントの選択</span><span class="sxs-lookup"><span data-stu-id="57d63-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="57d63-279">プロパティは、RPC を受信するクライアントを指定するためのいくつかのオプションを提供する[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="57d63-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="57d63-280">接続されたすべてのクライアント。</span><span class="sxs-lookup"><span data-stu-id="57d63-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="57d63-281">呼び出し元クライアントのみ。</span><span class="sxs-lookup"><span data-stu-id="57d63-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="57d63-282">呼び出し元のクライアントを除くすべてのクライアント。</span><span class="sxs-lookup"><span data-stu-id="57d63-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="57d63-283">接続 ID で識別される特定のクライアント。</span><span class="sxs-lookup"><span data-stu-id="57d63-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="57d63-284">この例では`addContosoChatMessageToPage`、呼び出し元のクライアントを呼び`Clients.Caller`出し、使用するのと同じ効果があります。</span><span class="sxs-lookup"><span data-stu-id="57d63-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="57d63-285">接続 ID で識別される、指定されたクライアントを除くすべての接続クライアント。</span><span class="sxs-lookup"><span data-stu-id="57d63-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="57d63-286">指定したグループ内のすべての接続クライアント。</span><span class="sxs-lookup"><span data-stu-id="57d63-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="57d63-287">指定されたグループ内のすべての接続クライアント (接続 ID で識別される指定されたクライアントを除く)。</span><span class="sxs-lookup"><span data-stu-id="57d63-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="57d63-288">呼び出し元のクライアントを除き、指定されたグループ内のすべての接続済みクライアント。</span><span class="sxs-lookup"><span data-stu-id="57d63-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="57d63-289">ユーザー ID によって識別される特定のユーザー。</span><span class="sxs-lookup"><span data-stu-id="57d63-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="57d63-290">既定では、これは`IPrincipal.Identity.Name`ですが、これは[IUserIdProvider の実装をグローバル ホストに登録](mapping-users-to-connections.md#IUserIdProvider)することで変更できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="57d63-291">接続 ID のリスト内のすべてのクライアントとグループ。</span><span class="sxs-lookup"><span data-stu-id="57d63-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="57d63-292">グループのリスト。</span><span class="sxs-lookup"><span data-stu-id="57d63-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="57d63-293">名前によるユーザー。</span><span class="sxs-lookup"><span data-stu-id="57d63-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="57d63-294">ユーザー名のリスト (SignalR 2.1 で導入)。</span><span class="sxs-lookup"><span data-stu-id="57d63-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="57d63-295">メソッド名のコンパイル時検証なし</span><span class="sxs-lookup"><span data-stu-id="57d63-295">No compile-time validation for method names</span></span>

<span data-ttu-id="57d63-296">指定したメソッド名は動的オブジェクトとして解釈されるため、IntelliSense またはコンパイル時の検証はありません。</span><span class="sxs-lookup"><span data-stu-id="57d63-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="57d63-297">式は実行時に評価されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="57d63-298">メソッド呼び出しが実行されると、SignalR はメソッド名とパラメーター値をクライアントに送信し、クライアントに名前と一致するメソッドがある場合は、そのメソッドが呼び出され、パラメーター値が渡されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="57d63-299">クライアントで一致するメソッドが見つからない場合、エラーは発生しません。</span><span class="sxs-lookup"><span data-stu-id="57d63-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="57d63-300">クライアント メソッドを呼び出すときに、SignalR がクライアントに送信するデータの形式については[、「SignalR の概要](../getting-started/introduction-to-signalr.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="57d63-301">大文字と小文字を区別しないメソッド名の一致</span><span class="sxs-lookup"><span data-stu-id="57d63-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="57d63-302">メソッド名の一致は大文字と小文字を区別しません。</span><span class="sxs-lookup"><span data-stu-id="57d63-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="57d63-303">たとえば、`Clients.All.addContosoChatMessageToPage`サーバー上で、 、 `AddContosoChatMessageToPage` `addcontosochatmessagetopage`、または`addContosoChatMessageToPage`をクライアントで実行します。</span><span class="sxs-lookup"><span data-stu-id="57d63-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="57d63-304">非同期実行</span><span class="sxs-lookup"><span data-stu-id="57d63-304">Asynchronous execution</span></span>

<span data-ttu-id="57d63-305">呼び出すメソッドは非同期的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="57d63-306">メソッドの呼び出し後に発生するコードは、メソッドの完了を待つ必要があるコードの行を指定しない限り、SignalR がクライアントにデータを送信するのを待たずにすぐに実行されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="57d63-307">2 つのクライアント メソッドを順番に実行する方法を次のコード例に示します。</span><span class="sxs-lookup"><span data-stu-id="57d63-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="57d63-308">**アウェイトの使用 (.NET 4.5)**</span><span class="sxs-lookup"><span data-stu-id="57d63-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="57d63-309">クライアント メソッド`await`が次のコード行が実行される前に終了するまで待機する場合、クライアントが実際に次のコード行を実行する前にメッセージを受信するわけではありません。</span><span class="sxs-lookup"><span data-stu-id="57d63-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="57d63-310">クライアント メソッド呼び出しの "完了" は、SignalR がメッセージの送信に必要な処理をすべて行ったことを意味します。</span><span class="sxs-lookup"><span data-stu-id="57d63-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="57d63-311">クライアントがメッセージを受信したことを確認する必要がある場合は、そのメカニズムを自分でプログラミングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="57d63-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="57d63-312">たとえば、ハブでメソッドを`MessageReceived`コーディングし、クライアントで必要な作業を`addContosoChatMessageToPage`行った後に呼び出`MessageReceived`すことができるクライアントのメソッドを作成できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="57d63-313">ハブ`MessageReceived`では、実際のクライアントの受信と元のメソッド呼び出しの処理に依存する任意の作業を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="57d63-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="57d63-314">メソッド名として文字列変数を使用する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="57d63-315">文字列変数をメソッド名として使用してクライアント メソッドを呼び出す場合は、 `Clients.All` `Clients.Others` `Clients.Caller` `IClientProxy` [Invoke(メソッド名、args.)をキャストし、Invoke(メソッド名、args.)を](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)呼び出します。</span><span class="sxs-lookup"><span data-stu-id="57d63-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="57d63-316">ハブ クラスからグループ メンバーシップを管理する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="57d63-317">SignalR のグループは、接続されたクライアントの指定されたサブセットにメッセージをブロードキャストするためのメソッドを提供します。</span><span class="sxs-lookup"><span data-stu-id="57d63-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="57d63-318">グループには任意の数のクライアントを持たることができ、クライアントは任意の数のグループのメンバーになることができます。</span><span class="sxs-lookup"><span data-stu-id="57d63-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="57d63-319">グループ メンバーシップを管理するには、Hub[Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)クラスの`Groups`プロパティによって提供される[Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)メソッドと Remove メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="57d63-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="57d63-320">クライアント コードによって呼`Groups.Add`び`Groups.Remove`出されるハブ メソッドと、それらを呼び出す JavaScript クライアント コードで使用されるメソッドの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="57d63-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="57d63-321">**[サーバー]**</span><span class="sxs-lookup"><span data-stu-id="57d63-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="57d63-322">**生成されたプロキシを使用した JavaScript クライアント**</span><span class="sxs-lookup"><span data-stu-id="57d63-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="57d63-323">グループを明示的に作成する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="57d63-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="57d63-324">実際には、グループは、 への`Groups.Add`呼び出しで初めて名前を指定したときに自動的に作成され、最後の接続をそのメンバーのメンバーシップから削除すると削除されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="57d63-325">グループメンバーシップリストまたはグループのリストを取得するための API はありません。</span><span class="sxs-lookup"><span data-stu-id="57d63-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="57d63-326">SignalR は[、 pub/sub モデル](http://en.wikipedia.org/wiki/Publish/subscribe)に基づいてクライアントとグループにメッセージを送信しますが、サーバーはグループまたはグループ メンバーシップの一覧を保持しません。</span><span class="sxs-lookup"><span data-stu-id="57d63-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="57d63-327">これにより、ノードを Web ファームに追加するたびに、SignalR が維持するすべての状態を新しいノードに伝達する必要があるため、スケーラビリティを最大限に高めます。</span><span class="sxs-lookup"><span data-stu-id="57d63-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="57d63-328">Add メソッドと Remove メソッドの非同期実行</span><span class="sxs-lookup"><span data-stu-id="57d63-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="57d63-329">メソッド`Groups.Add`と`Groups.Remove`メソッドは非同期で実行されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="57d63-330">クライアントをグループに追加し、そのグループを使用してすぐにクライアントにメッセージを送信する場合は、`Groups.Add`メソッドが最初に終了することを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="57d63-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="57d63-331">次のコード例は、その方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="57d63-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="57d63-332">**グループへのクライアントの追加と、そのクライアントのメッセージング**</span><span class="sxs-lookup"><span data-stu-id="57d63-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="57d63-333">グループ メンバーシップの永続性</span><span class="sxs-lookup"><span data-stu-id="57d63-333">Group membership persistence</span></span>

<span data-ttu-id="57d63-334">SignalR はユーザーではなく接続を追跡するため、ユーザーが接続を確立するたびに同じグループにユーザーを入れてもらいたい場合は、ユーザーが新しい`Groups.Add`接続を確立するたびに呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="57d63-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="57d63-335">接続が一時的に切断された後、SignalR が接続を自動的に復元できることがあります。</span><span class="sxs-lookup"><span data-stu-id="57d63-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="57d63-336">その場合、SignalR は、新しい接続を確立せず、同じ接続を復元するため、クライアントのグループ メンバーシップが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="57d63-337">これは、一時的な中断がサーバーの再起動または障害の結果である場合でも可能です。</span><span class="sxs-lookup"><span data-stu-id="57d63-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="57d63-338">サーバーがダウンし、接続がタイムアウトする前に新しいサーバーに置き換えられた場合、クライアントは自動的に新しいサーバーに再接続し、そのサーバーがメンバーになっているグループに再登録できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="57d63-339">接続が切断された後に接続を自動的に復元できない場合、または接続がタイムアウトしたとき、またはクライアントが切断されたとき (たとえば、ブラウザーが新しいページに移動した場合など) は、グループ メンバーシップが失われます。</span><span class="sxs-lookup"><span data-stu-id="57d63-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="57d63-340">次回ユーザーが接続すると、新しい接続になります。</span><span class="sxs-lookup"><span data-stu-id="57d63-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="57d63-341">同じユーザーが新しい接続を確立したときにグループ メンバーシップを維持するには、アプリケーションはユーザーとグループの関連付けを追跡し、ユーザーが新しい接続を確立するたびにグループ メンバーシップを復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="57d63-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="57d63-342">接続と再接続の詳細については、このトピックの後の[「ハブ クラスで接続の有効期間イベントを処理する方法](#connectionlifetime)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="57d63-343">シングルユーザー グループ</span><span class="sxs-lookup"><span data-stu-id="57d63-343">Single-user groups</span></span>

<span data-ttu-id="57d63-344">SignalR を使用するアプリケーションは、通常、ユーザーと接続の間の関連付けを追跡して、メッセージを送信したユーザーと、どのユーザーがメッセージを受信する必要があるかを把握する必要があります。</span><span class="sxs-lookup"><span data-stu-id="57d63-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="57d63-345">グループは、その目的で一般的に使用される 2 つのパターンのいずれかで使用されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="57d63-346">シングルユーザー グループ。</span><span class="sxs-lookup"><span data-stu-id="57d63-346">Single-user groups.</span></span>

    <span data-ttu-id="57d63-347">グループ名としてユーザー名を指定し、ユーザーが接続または再接続するたびに、グループに現在の接続 ID を追加できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="57d63-348">グループに送信するユーザーにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="57d63-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="57d63-349">この方法の欠点は、グループがユーザーがオンラインかオフラインかを調べる方法を提供しないということです。</span><span class="sxs-lookup"><span data-stu-id="57d63-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="57d63-350">ユーザー名と接続 ID の間の関連付けを追跡します。</span><span class="sxs-lookup"><span data-stu-id="57d63-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="57d63-351">各ユーザー名と 1 つ以上の接続 ID の間の関連付けをディクショナリーまたはデータベースに保管し、ユーザーが接続または切断するたびに保管データを更新することができます。</span><span class="sxs-lookup"><span data-stu-id="57d63-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="57d63-352">ユーザーにメッセージを送信するには、接続 ID を指定します。</span><span class="sxs-lookup"><span data-stu-id="57d63-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="57d63-353">この方法の欠点は、メモリを多く取る点です。</span><span class="sxs-lookup"><span data-stu-id="57d63-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="57d63-354">ハブ クラスで接続の有効期間イベントを処理する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="57d63-355">接続の有効期間イベントを処理する一般的な理由は、ユーザーが接続されているかどうかを追跡し、ユーザー名と接続 ID の間の関連付けを追跡することです。</span><span class="sxs-lookup"><span data-stu-id="57d63-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="57d63-356">クライアントが接続または切断するときに独自のコードを実行するには、`OnConnected`次`OnDisconnected`の例`OnReconnected`に示すように、Hub クラスの 、、および 仮想メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="57d63-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="57d63-357">オン接続、オン・オンライン切断、およびオン再接続が呼び出された場合</span><span class="sxs-lookup"><span data-stu-id="57d63-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="57d63-358">ブラウザが新しいページに移動するたびに、新しい接続を確立`OnDisconnected``OnConnected`する必要があります。</span><span class="sxs-lookup"><span data-stu-id="57d63-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="57d63-359">SignalR は、新しい接続が確立されると、常に新しい接続 ID を作成します。</span><span class="sxs-lookup"><span data-stu-id="57d63-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="57d63-360">この`OnReconnected`メソッドは、接続がタイムアウトする前にケーブルが一時的に切断され、再接続された場合など、SignalR が自動的に回復できる接続に一時的な中断が発生した場合に呼び出されます。この`OnDisconnected`メソッドは、クライアントが切断され、ブラウザーが新しいページに移動した場合など、SignalR が自動的に再接続できない場合に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="57d63-361">したがって、特定のクライアントに対して可能な一連`OnConnected`の`OnReconnected`イベント`OnDisconnected`は、 、 、 、 、 、または`OnConnected` `OnDisconnected`、 をクリックします。</span><span class="sxs-lookup"><span data-stu-id="57d63-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="57d63-362">指定された接続のシーケンス`OnConnected`、`OnDisconnected`は`OnReconnected`表示されません。</span><span class="sxs-lookup"><span data-stu-id="57d63-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="57d63-363">サーバー`OnDisconnected`がダウンしたり、App Domain がリサイクルされたりした場合など、一部のシナリオではこのメソッドは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="57d63-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="57d63-364">別のサーバーがオンラインに接続されたり、App Domain がリサイクルを完了したりすると、一部のクライアントが`OnReconnected`再接続してイベントを発生させる場合があります。</span><span class="sxs-lookup"><span data-stu-id="57d63-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="57d63-365">詳細については、「 [SignalR での接続の有効期間イベントの理解と処理](handling-connection-lifetime-events.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="57d63-366">呼び出し元の状態が入力されていません</span><span class="sxs-lookup"><span data-stu-id="57d63-366">Caller state not populated</span></span>

<span data-ttu-id="57d63-367">接続有効期間イベント ハンドラ メソッドはサーバーから呼び出されるため、クライアント上の`state`オブジェクトに配置した状態は、サーバーの`Caller`プロパティに設定されません。</span><span class="sxs-lookup"><span data-stu-id="57d63-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="57d63-368">オブジェクトと`Caller`プロパティの`state`詳細については、このトピックの後半の[「クライアントとハブ クラス間で状態を渡す方法](#passstate)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="57d63-369">Context プロパティからクライアントに関する情報を取得する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="57d63-370">クライアントに関する情報を取得するには、Hub クラスの`Context`プロパティを使用します。</span><span class="sxs-lookup"><span data-stu-id="57d63-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="57d63-371">プロパティ`Context`は、次の情報へのアクセスを提供する[HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx)オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="57d63-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="57d63-372">呼び出し元クライアントの接続 ID。</span><span class="sxs-lookup"><span data-stu-id="57d63-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="57d63-373">接続 ID は、SignalR によって割り当てられる GUID です (独自のコードで値を指定することはできません)。</span><span class="sxs-lookup"><span data-stu-id="57d63-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="57d63-374">接続ごとに 1 つの接続 ID があり、アプリケーションに複数のハブがある場合は、すべてのハブで同じ接続 ID が使用されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="57d63-375">HTTP ヘッダー データ。</span><span class="sxs-lookup"><span data-stu-id="57d63-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="57d63-376">HTTP ヘッダーを から`Context.Headers`取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="57d63-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="57d63-377">同じものに対する複数の参照が最初`Context.Headers`に作成された理由は`Context.Request`、プロパティが後で追加`Context.Headers`され、下位互換性のために保持されたためです。</span><span class="sxs-lookup"><span data-stu-id="57d63-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="57d63-378">クエリ文字列データ。</span><span class="sxs-lookup"><span data-stu-id="57d63-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="57d63-379">クエリ文字列データを から`Context.QueryString`取得することもできます。</span><span class="sxs-lookup"><span data-stu-id="57d63-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="57d63-380">このプロパティで取得するクエリ文字列は、SignalR 接続を確立した HTTP 要求で使用された文字列です。</span><span class="sxs-lookup"><span data-stu-id="57d63-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="57d63-381">クライアントからサーバーにクライアントにデータを渡す便利な方法である接続を構成することで、クライアントにクエリ文字列パラメーターを追加できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="57d63-382">次の例は、生成されたプロキシを使用するときに JavaScript クライアントにクエリ文字列を追加する方法の 1 つを示しています。</span><span class="sxs-lookup"><span data-stu-id="57d63-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="57d63-383">クエリ文字列パラメーターの設定の詳細については[、JavaScript](hubs-api-guide-javascript-client.md)クライアントと[.NET](hubs-api-guide-net-client.md)クライアントの API ガイドを参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="57d63-384">クエリ文字列データで接続に使用されるトランスポート 方法と、SignalR によって内部的に使用されるその他の値を見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="57d63-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="57d63-385">の`transportMethod`値は、「ウェブソケット」、「サーバーSentイベント」、「フォーエバーフレーム」または「ロングポーリング」になります。</span><span class="sxs-lookup"><span data-stu-id="57d63-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="57d63-386">イベント ハンドラー メソッドでこの値を`OnConnected`チェックする場合、場合によっては、最初に接続の最終的なネゴシエートされたトランスポート 方法ではないトランスポート値を取得する場合があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="57d63-387">その場合、メソッドは例外をスローし、最終的なトランスポート メソッドが確立されたときに、後で再度呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="57d63-388">クッキー。</span><span class="sxs-lookup"><span data-stu-id="57d63-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="57d63-389">からクッキーを取得することもできます`Context.RequestCookies`。</span><span class="sxs-lookup"><span data-stu-id="57d63-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="57d63-390">ユーザー情報。</span><span class="sxs-lookup"><span data-stu-id="57d63-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="57d63-391">要求の HttpContext オブジェクト:</span><span class="sxs-lookup"><span data-stu-id="57d63-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="57d63-392">SignalR 接続のオブジェクト`HttpContext.Current`を取得する`HttpContext`代わりに、このメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="57d63-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="57d63-393">クライアントとハブ クラスの間で状態を渡す方法</span><span class="sxs-lookup"><span data-stu-id="57d63-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="57d63-394">クライアント プロキシは、`state`メソッド呼び出しごとにサーバーに転送するデータを格納できるオブジェクトを提供します。</span><span class="sxs-lookup"><span data-stu-id="57d63-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="57d63-395">サーバーでは、クライアントから呼び出されるハブ`Clients.Caller`メソッドのプロパティでこのデータにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="57d63-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="57d63-396">接続`Clients.Caller`有効期間イベント ハンドラー メソッド`OnConnected`、、`OnDisconnected`および`OnReconnected`のプロパティは設定されません。</span><span class="sxs-lookup"><span data-stu-id="57d63-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="57d63-397">オブジェクトとプロパティのデータの`state`作成または更新は`Clients.Caller`、両方向で機能します。</span><span class="sxs-lookup"><span data-stu-id="57d63-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="57d63-398">サーバーの値を更新すると、値はクライアントに渡されます。</span><span class="sxs-lookup"><span data-stu-id="57d63-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="57d63-399">次の例は、すべてのメソッド呼び出しでサーバーに送信するための状態を格納する JavaScript クライアント コードを示しています。</span><span class="sxs-lookup"><span data-stu-id="57d63-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="57d63-400">NET クライアントの同等のコードの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="57d63-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="57d63-401">ハブ クラスでは、`Clients.Caller`このデータにプロパティからアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="57d63-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="57d63-402">前の例で参照されている状態を取得するコードを次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="57d63-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="57d63-403">状態を永続化するためのこのメカニズムは、`state`または`Clients.Caller`プロパティに入れるすべてのメソッド呼び出しでラウンド トリップされるため、大量のデータを対象としていません。</span><span class="sxs-lookup"><span data-stu-id="57d63-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="57d63-404">ユーザー名やカウンターなどの小さな項目に便利です。</span><span class="sxs-lookup"><span data-stu-id="57d63-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="57d63-405">VB.NETまたは厳密に型指定されたハブでは、呼び出し元の状態オブジェクトにアクセス`Clients.Caller`できません。代わりに、(SignalR 2.1 で導入)を使用`Clients.CallerState`してください:</span><span class="sxs-lookup"><span data-stu-id="57d63-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="57d63-406">**C での呼び出し元状態の使用#**</span><span class="sxs-lookup"><span data-stu-id="57d63-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="57d63-407">**呼び出し元の使用状態を Visual Basic で使用する**</span><span class="sxs-lookup"><span data-stu-id="57d63-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="57d63-408">ハブ クラスのエラーを処理する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="57d63-409">ハブ クラス のメソッドで発生するエラーを処理するには、まず、 を使用`await`して非同期操作 (クライアント メソッドの呼び出しなど) からの例外を "監視" することを確認します。</span><span class="sxs-lookup"><span data-stu-id="57d63-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="57d63-410">次に、次の 1 つ以上の方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="57d63-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="57d63-411">メソッド コードを try-catch ブロックにラップし、例外オブジェクトをログに記録します。</span><span class="sxs-lookup"><span data-stu-id="57d63-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="57d63-412">デバッグの目的で、例外をクライアントに送信できますが、セキュリティ上の理由から、運用環境でクライアントに詳細情報を送信することはお勧めできません。</span><span class="sxs-lookup"><span data-stu-id="57d63-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="57d63-413">[メソッドを](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)処理するハブ パイプライン モジュールを作成します。</span><span class="sxs-lookup"><span data-stu-id="57d63-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="57d63-414">次の例は、エラーをログに記録するパイプライン モジュールを示し、その後にモジュールを Hubs パイプラインに挿入するコードをStartup.csに示します。</span><span class="sxs-lookup"><span data-stu-id="57d63-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="57d63-415">クラスを`HubException`使用します (SignalR 2 で導入されました)。</span><span class="sxs-lookup"><span data-stu-id="57d63-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="57d63-416">このエラーは、どのハブ呼び出しからでもスローできます。</span><span class="sxs-lookup"><span data-stu-id="57d63-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="57d63-417">コンストラクター`HubError`は、文字列メッセージと、余分なエラー データを格納するオブジェクトを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="57d63-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="57d63-418">SignalR は、例外を自動シリアル化してクライアントに送信します。</span><span class="sxs-lookup"><span data-stu-id="57d63-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="57d63-419">次のコード サンプルは、ハブ呼`HubException`び出し中に スローする方法と、JavaScript クライアントと .NET クライアントで例外を処理する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="57d63-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="57d63-420">**クラスを示すサーバー コード**</span><span class="sxs-lookup"><span data-stu-id="57d63-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="57d63-421">**ハブでのハブ例外のスローに対する応答を示す JavaScript クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="57d63-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="57d63-422">**ハブでのハブ例外のスローに対する応答を示す .NET クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="57d63-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="57d63-423">ハブ パイプライン モジュールの詳細については、このトピックの[「Hubs パイプラインをカスタマイズする方法](#hubpipeline)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="57d63-424">トレースを有効にする方法</span><span class="sxs-lookup"><span data-stu-id="57d63-424">How to enable tracing</span></span>

<span data-ttu-id="57d63-425">サーバー側トレースを有効にするには、次の例に示すように、Web.config ファイルに system.diagnostics 要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="57d63-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="57d63-426">Visual Studio でアプリケーションを実行すると、**出力**ウィンドウでログを表示できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="57d63-427">ハブ クラスの外部からクライアント メソッドを呼び出し、グループを管理する方法</span><span class="sxs-lookup"><span data-stu-id="57d63-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="57d63-428">ハブ クラスとは異なるクラスからクライアント メソッドを呼び出す場合は、ハブの SignalR コンテキスト オブジェクトへの参照を取得し、それを使用してクライアントのメソッドを呼び出すか、グループを管理します。</span><span class="sxs-lookup"><span data-stu-id="57d63-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="57d63-429">次のサンプル`StockTicker`クラスは、コンテキスト オブジェクトを取得し、クラスのインスタンスに格納し、クラス インスタンスを静的プロパティに格納し、シングルトン クラス インスタンスのコンテキストを`updateStockPrice`使用して、という名前`StockTickerHub`の Hub に接続されているクライアントのメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="57d63-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="57d63-430">長命オブジェクトでコンテキストを複数回使用する必要がある場合は、参照を 1 回取得して、毎回再び取得するのではなく、それを保存します。</span><span class="sxs-lookup"><span data-stu-id="57d63-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="57d63-431">コンテキストを取得すると、SignalR は、ハブ メソッドがクライアント メソッドを呼び出すのと同じ順序でクライアントにメッセージを送信します。</span><span class="sxs-lookup"><span data-stu-id="57d63-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="57d63-432">ハブの SignalR コンテキストを使用する方法を示すチュートリアルについては、「 [ASP.NET SignalR を使用したサーバー ブロードキャスト](../getting-started/tutorial-server-broadcast-with-signalr.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="57d63-433">クライアント メソッドの呼び出し</span><span class="sxs-lookup"><span data-stu-id="57d63-433">Calling client methods</span></span>

<span data-ttu-id="57d63-434">RPC を受信するクライアントを指定できますが、ハブ クラスから呼び出す場合よりも少ないオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="57d63-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="57d63-435">これは、コンテキストがクライアントからの特定の呼び出しに関連付けられていないため、現在の接続 ID`Clients.Others`に関する情報を必要とするメソッド (、`Clients.Caller`または`Clients.OthersInGroup`など) は使用できないからです。</span><span class="sxs-lookup"><span data-stu-id="57d63-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="57d63-436">次のオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-436">The following options are available:</span></span>

- <span data-ttu-id="57d63-437">接続されたすべてのクライアント。</span><span class="sxs-lookup"><span data-stu-id="57d63-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="57d63-438">接続 ID で識別される特定のクライアント。</span><span class="sxs-lookup"><span data-stu-id="57d63-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="57d63-439">接続 ID で識別される、指定されたクライアントを除くすべての接続クライアント。</span><span class="sxs-lookup"><span data-stu-id="57d63-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="57d63-440">指定したグループ内のすべての接続クライアント。</span><span class="sxs-lookup"><span data-stu-id="57d63-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="57d63-441">指定されたグループ内のすべての接続クライアント (接続 ID で識別される指定されたクライアントを除く)。</span><span class="sxs-lookup"><span data-stu-id="57d63-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="57d63-442">ハブ クラスのメソッドから非ハブ クラスを呼び出す場合は、現在の接続`Clients.Client`ID を渡して、 、、`Clients.AllExcept`または`Clients.Group`、 `Clients.Caller` `Clients.Others`、、`Clients.OthersInGroup`または を使用して、 、 、または を使用できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="57d63-443">次の例では、クラス`MoveShapeHub`がシミュレートできるように、`Broadcaster`クラスに接続 ID を`Broadcaster`渡`Clients.Others`します。</span><span class="sxs-lookup"><span data-stu-id="57d63-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="57d63-444">グループ メンバーシップの管理</span><span class="sxs-lookup"><span data-stu-id="57d63-444">Managing group membership</span></span>

<span data-ttu-id="57d63-445">グループの管理には、ハブ クラスで行うのと同じオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="57d63-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="57d63-446">グループにクライアントを追加する</span><span class="sxs-lookup"><span data-stu-id="57d63-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="57d63-447">グループからクライアントを削除する</span><span class="sxs-lookup"><span data-stu-id="57d63-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="57d63-448">ハブ パイプラインをカスタマイズする方法</span><span class="sxs-lookup"><span data-stu-id="57d63-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="57d63-449">SignalR を使用すると、ハブ パイプラインに独自のコードを挿入できます。</span><span class="sxs-lookup"><span data-stu-id="57d63-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="57d63-450">次の例は、クライアントから受信した各受信メソッド呼び出しと、クライアントで呼び出された送信メソッド呼び出しを記録するカスタム ハブ パイプライン モジュールを示しています。</span><span class="sxs-lookup"><span data-stu-id="57d63-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="57d63-451">*Startup.cs*ファイルの次のコードは、ハブ パイプラインで実行するモジュールを登録します。</span><span class="sxs-lookup"><span data-stu-id="57d63-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="57d63-452">オーバーライドできるメソッドは多数あります。</span><span class="sxs-lookup"><span data-stu-id="57d63-452">There are many different methods that you can override.</span></span> <span data-ttu-id="57d63-453">完全なリストについては、「[ハブパイプライン モジュール メソッド](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="57d63-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
