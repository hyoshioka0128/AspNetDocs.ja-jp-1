---
uid: signalr/overview/getting-started/introduction-to-signalr
title: シグナルR の概要 |マイクロソフトドキュメント
author: bradygaster
description: この記事では、SignalR とは何か、および作成するために設計されたソリューションの一部について説明します。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675941"
---
# <a name="introduction-to-signalr"></a><span data-ttu-id="cf969-103">SignalR 入門</span><span class="sxs-lookup"><span data-stu-id="cf969-103">Introduction to SignalR</span></span>

<span data-ttu-id="cf969-104">[パトリック・フレッチャー](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="cf969-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="cf969-105">この記事では、SignalR とは何か、および作成するために設計されたソリューションの一部について説明します。</span><span class="sxs-lookup"><span data-stu-id="cf969-105">This article describes what SignalR is, and some of the solutions it was designed to create.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="cf969-106">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="cf969-106">Questions and comments</span></span>
> 
> <span data-ttu-id="cf969-107">このチュートリアルを気に入った方法と、ページの下部にあるコメントで改善できる内容についてのフィードバックを残してください。</span><span class="sxs-lookup"><span data-stu-id="cf969-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="cf969-108">チュートリアルに直接関連しない質問がある場合は[、ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="cf969-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="cf969-109">シグナルとは何ですか?</span><span class="sxs-lookup"><span data-stu-id="cf969-109">What is SignalR?</span></span>

<span data-ttu-id="cf969-110">ASP.NET SignalR は、アプリケーションにリアルタイム Web 機能を追加するプロセスを簡略化するASP.NET開発者向けのライブラリです。</span><span class="sxs-lookup"><span data-stu-id="cf969-110">ASP.NET SignalR is a library for ASP.NET developers that simplifies the process of adding real-time web functionality to applications.</span></span> <span data-ttu-id="cf969-111">リアルタイム Web 機能とは、サーバーコードが新しいデータを要求するのを待つ代わりに、接続されたクライアントにコンテンツを即座にプッシュする機能です。</span><span class="sxs-lookup"><span data-stu-id="cf969-111">Real-time web functionality is the ability to have server code push content to connected clients instantly as it becomes available, rather than having the server wait for a client to request new data.</span></span>

<span data-ttu-id="cf969-112">SignalR を使用すると、ASP.NETアプリケーションにあらゆる種類の "リアルタイム" Web 機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="cf969-112">SignalR can be used to add any sort of "real-time" web functionality to your ASP.NET application.</span></span> <span data-ttu-id="cf969-113">チャットは例としてよく使われますが、もっと多くのことを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="cf969-113">While chat is often used as an example, you can do a whole lot more.</span></span> <span data-ttu-id="cf969-114">ユーザーが Web ページを更新して新しいデータを表示したり、ページが新しいデータを取得するために[長いポーリング](http://en.wikipedia.org/wiki/Push_technology#Long_polling)を実装したりするときはいつでも、SignalR を使用する候補になります。</span><span class="sxs-lookup"><span data-stu-id="cf969-114">Any time a user refreshes a web page to see new data, or the page implements [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_polling) to retrieve new data, it is a candidate for using SignalR.</span></span> <span data-ttu-id="cf969-115">例としては、ダッシュボードと監視アプリケーション、共同アプリケーション (ドキュメントの同時編集など)、ジョブの進捗状況の更新、リアルタイムフォームなどがあります。</span><span class="sxs-lookup"><span data-stu-id="cf969-115">Examples include dashboards and monitoring applications, collaborative applications (such as simultaneous editing of documents), job progress updates, and real-time forms.</span></span>

<span data-ttu-id="cf969-116">SignalR は、リアルタイム ゲームなど、サーバーからの高周波更新を必要とするまったく新しい種類の Web アプリケーションも有効にします。</span><span class="sxs-lookup"><span data-stu-id="cf969-116">SignalR also enables completely new types of web applications that require high frequency updates from the server, for example, real-time gaming.</span></span>

<span data-ttu-id="cf969-117">SignalR は、クライアント ブラウザー (およびその他のクライアント プラットフォーム) で JavaScript 関数を呼び出すサーバーからクライアントへのリモート プロシージャ コール (RPC) を作成するための簡単な API をサーバー側の .NET コードから提供します。</span><span class="sxs-lookup"><span data-stu-id="cf969-117">SignalR provides a simple API for creating server-to-client remote procedure calls (RPC) that call JavaScript functions in client browsers (and other client platforms) from server-side .NET code.</span></span> <span data-ttu-id="cf969-118">SignalR には、接続管理用の API (接続イベントや接続解除イベントなど) や、接続のグループ化も含まれています。</span><span class="sxs-lookup"><span data-stu-id="cf969-118">SignalR also includes API for connection management (for instance, connect and disconnect events), and grouping connections.</span></span>

![SignalR を使用したメソッドの呼び出し](introduction-to-signalr/_static/image1.png)

<span data-ttu-id="cf969-120">SignalR では、自動的に接続管理が処理され、ユーザーは、チャットルームのように、同時に接続されているすべてのクライアントにメッセージをブロードキャストすることができます。</span><span class="sxs-lookup"><span data-stu-id="cf969-120">SignalR handles connection management automatically, and lets you broadcast messages to all connected clients simultaneously, like a chat room.</span></span> <span data-ttu-id="cf969-121">また、特定のクライアントにメッセージを送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="cf969-121">You can also send messages to specific clients.</span></span> <span data-ttu-id="cf969-122">クライアントとサーバー間の接続は、通信ごとに再確立される従来の HTTP 接続とは異なり、永続的なものです。</span><span class="sxs-lookup"><span data-stu-id="cf969-122">The connection between the client and server is persistent, unlike a classic HTTP connection, which is re-established for each communication.</span></span>

<span data-ttu-id="cf969-123">SignalR は、サーバー コードがリモート プロシージャ コール (RPC) を使用してブラウザーのクライアント コードを呼び出すことができる 、Web 上で一般的な要求と応答モデルではなく、"サーバー プッシュ" 機能をサポートします。</span><span class="sxs-lookup"><span data-stu-id="cf969-123">SignalR supports "server push" functionality, in which server code can call out to client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model common on the web today.</span></span>

<span data-ttu-id="cf969-124">SignalR アプリケーションは、組み込みプロバイダーとサード パーティ製のスケールアウト プロバイダーを使用して、数千のクライアントにスケール アウトできます。</span><span class="sxs-lookup"><span data-stu-id="cf969-124">SignalR applications can scale out to thousands of clients using built-in, and third-party scale-out providers.</span></span>

<span data-ttu-id="cf969-125">組み込みプロバイダーには、次のものがあります。</span><span class="sxs-lookup"><span data-stu-id="cf969-125">Built-in providers include:</span></span>
* [<span data-ttu-id="cf969-126">Service Bus</span><span class="sxs-lookup"><span data-stu-id="cf969-126">Service Bus</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [<span data-ttu-id="cf969-127">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cf969-127">SQL Server</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [<span data-ttu-id="cf969-128">Redis</span><span class="sxs-lookup"><span data-stu-id="cf969-128">Redis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

<span data-ttu-id="cf969-129">サードパーティのプロバイダには次のものがあります。</span><span class="sxs-lookup"><span data-stu-id="cf969-129">Third-party providers include:</span></span>
* <span data-ttu-id="cf969-130">[Nキャッシュ](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span><span class="sxs-lookup"><span data-stu-id="cf969-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span></span>

<span data-ttu-id="cf969-131">SignalR はオープンソースで[、GitHub](https://github.com/signalr)を通じてアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="cf969-131">SignalR is open-source, accessible through [GitHub](https://github.com/signalr).</span></span>

## <a name="signalr-and-websocket"></a><span data-ttu-id="cf969-132">シグナルとウェブソケット</span><span class="sxs-lookup"><span data-stu-id="cf969-132">SignalR and WebSocket</span></span>

<span data-ttu-id="cf969-133">SignalR は、新しい WebSocket トランスポートを使用して、必要に応じて古いトランスポートにフォールバックします。</span><span class="sxs-lookup"><span data-stu-id="cf969-133">SignalR uses the new WebSocket transport where available and falls back to older transports where necessary.</span></span> <span data-ttu-id="cf969-134">WebSocket を直接使ってアプリを記述することは確かに可能ですが、SignalR を使用すると、実装する必要のある多くの機能が既に実行されていることを意味します。</span><span class="sxs-lookup"><span data-stu-id="cf969-134">While you could certainly write your app using WebSocket directly, using SignalR means that a lot of the extra functionality you would need to implement is already done for you.</span></span> <span data-ttu-id="cf969-135">最も重要なことは、これは、古いクライアント用に別のコード パスを作成する必要なく、WebSocket を利用するようにアプリをコーディングできることを意味します。</span><span class="sxs-lookup"><span data-stu-id="cf969-135">Most importantly, this means that you can code your app to take advantage of WebSocket without having to worry about creating a separate code path for older clients.</span></span> <span data-ttu-id="cf969-136">SignalR は、基になるトランスポートの変更をサポートするように更新されるため、WebSocket のバージョン間で一貫性のあるインターフェイスをアプリケーションに提供するため、WebSocket の更新を心配する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="cf969-136">SignalR also shields you from having to worry about updates to WebSocket, since SignalR is updated to support changes in the underlying transport, providing your application a consistent interface across versions of WebSocket.</span></span>

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a><span data-ttu-id="cf969-137">トランスポートとフォールバック</span><span class="sxs-lookup"><span data-stu-id="cf969-137">Transports and fallbacks</span></span>

<span data-ttu-id="cf969-138">SignalR は、クライアントとサーバー間でリアルタイムの作業を行うために必要なトランスポートの一部を抽象化します。</span><span class="sxs-lookup"><span data-stu-id="cf969-138">SignalR is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="cf969-139">SignalR 接続は HTTP として開始され、使用可能な場合は WebSocket 接続に昇格されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-139">A SignalR connection starts as HTTP, and is then promoted to a WebSocket connection if it is available.</span></span> <span data-ttu-id="cf969-140">WebSocket は、サーバー メモリを最も効率的に使用し、遅延が最も低く、最も基になる機能 (クライアントとサーバー間の全二重通信など) を備えていますが、最も厳しい要件もあります。</span><span class="sxs-lookup"><span data-stu-id="cf969-140">WebSocket is the ideal transport for SignalR, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: WebSocket requires the server to be using Windows Server 2012 or Windows 8, and .NET Framework 4.5.</span></span> <span data-ttu-id="cf969-141">これらの要件が満たされない場合、SignalR は他のトランスポートを使用して接続を試みます。</span><span class="sxs-lookup"><span data-stu-id="cf969-141">If these requirements are not met, SignalR will attempt to use other transports to make its connections.</span></span>

### <a name="html-5-transports"></a><span data-ttu-id="cf969-142">HTML 5 トランスポート</span><span class="sxs-lookup"><span data-stu-id="cf969-142">HTML 5 transports</span></span>

<span data-ttu-id="cf969-143">これらのトランスポートは、 HTML [5](http://en.wikipedia.org/wiki/HTML5)のサポートに依存します。</span><span class="sxs-lookup"><span data-stu-id="cf969-143">These transports depend on support for [HTML 5](http://en.wikipedia.org/wiki/HTML5).</span></span> <span data-ttu-id="cf969-144">クライアントブラウザがHTML 5標準をサポートしていない場合は、古いトランスポートが使用されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-144">If the client browser does not support the HTML 5 standard, older transports will be used.</span></span>

- <span data-ttu-id="cf969-145">**WebSocket** (サーバーとブラウザーの両方が Websocket をサポートできることを示している場合)。</span><span class="sxs-lookup"><span data-stu-id="cf969-145">**WebSocket** (if both the server and browser indicate they can support Websocket).</span></span> <span data-ttu-id="cf969-146">WebSocket は、クライアントとサーバー間の真の永続的な双方向接続を確立する唯一のトランスポートです。</span><span class="sxs-lookup"><span data-stu-id="cf969-146">WebSocket is the only transport that establishes a true persistent, two-way connection between client and server.</span></span> <span data-ttu-id="cf969-147">ただし、WebSocket には最も厳しい要件もあります。それは完全にマイクロソフトのインターネットエクスプローラ、グーグルクローム、およびMozilla Firefoxの最新バージョンでのみ完全にサポートされており、オペラやサファリなどの他のブラウザで部分的な実装のみを持っています。</span><span class="sxs-lookup"><span data-stu-id="cf969-147">However, WebSocket also has the most stringent requirements; it is fully supported only in the latest versions of Microsoft Internet Explorer, Google Chrome, and Mozilla Firefox, and only has a partial implementation in other browsers such as Opera and Safari.</span></span>
- <span data-ttu-id="cf969-148">**サーバー送信イベント**、 イベント ソースとも呼ばれます (ブラウザーがサーバー送信イベントをサポートしている場合は、基本的には Internet Explorer 以外のすべてのブラウザーです)。</span><span class="sxs-lookup"><span data-stu-id="cf969-148">**Server Sent Events**, also known as EventSource (if the browser supports Server Sent Events, which is basically all browsers except Internet Explorer.)</span></span>

### <a name="comet-transports"></a><span data-ttu-id="cf969-149">彗星輸送</span><span class="sxs-lookup"><span data-stu-id="cf969-149">Comet transports</span></span>

<span data-ttu-id="cf969-150">次のトランスポートは、クライアントが特に要求せずにクライアントにデータをプッシュするためにサーバーが使用できる、ブラウザーまたは他のクライアントが長い HTTP 要求を保持する[Comet](http://en.wikipedia.org/wiki/Comet_(programming)) Web アプリケーション モデルに基づいています。</span><span class="sxs-lookup"><span data-stu-id="cf969-150">The following transports are based on the [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web application model, in which a browser or other client maintains a long-held HTTP request, which the server can use to push data to the client without the client specifically requesting it.</span></span>

- <span data-ttu-id="cf969-151">**フォーエバーフレーム**(インターネットエクスプローラのみ)。</span><span class="sxs-lookup"><span data-stu-id="cf969-151">**Forever Frame** (for Internet Explorer only).</span></span> <span data-ttu-id="cf969-152">Forever Frame は、完了していないサーバー上のエンドポイントに要求を行う非表示の IFrame を作成します。</span><span class="sxs-lookup"><span data-stu-id="cf969-152">Forever Frame creates a hidden IFrame which makes a request to an endpoint on the server that does not complete.</span></span> <span data-ttu-id="cf969-153">その後、サーバーは、直ちに実行されるスクリプトをクライアントに送信し続け、サーバー間の一方向のリアルタイム接続を提供します。</span><span class="sxs-lookup"><span data-stu-id="cf969-153">The server then continually sends script to the client which is immediately executed, providing a one-way realtime connection from server to client.</span></span> <span data-ttu-id="cf969-154">クライアントからサーバーへの接続は、サーバーからクライアントへの接続から別々の接続を使用し、標準の HTTP 要求と同様に、送信する必要があるデータごとに新しい接続が作成されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-154">The connection from client to server uses a separate connection from the server to client connection, and like a standard HTTP request, a new connection is created for each piece of data that needs to be sent.</span></span>
- <span data-ttu-id="cf969-155">**Ajax ロングポーリング**.</span><span class="sxs-lookup"><span data-stu-id="cf969-155">**Ajax long polling**.</span></span> <span data-ttu-id="cf969-156">ロングポーリングでは、永続的な接続は作成されませんが、代わりに、サーバーが応答するまで開いたままの要求でサーバーをポーリングし、その時点で接続が閉じ、新しい接続が直ちに要求されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-156">Long polling does not create a persistent connection, but instead polls the server with a request that stays open until the server responds, at which point the connection closes, and a new connection is requested immediately.</span></span> <span data-ttu-id="cf969-157">これにより、接続がリセットされる間に、ある程度の待機時間が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="cf969-157">This may introduce some latency while the connection resets.</span></span>

<span data-ttu-id="cf969-158">どの構成でどのトランスポートがサポートされるのかの詳細については、「[サポートされるプラットフォーム](supported-platforms.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cf969-158">For more information on what transports are supported under which configurations, see [Supported Platforms](supported-platforms.md).</span></span>

### <a name="transport-selection-process"></a><span data-ttu-id="cf969-159">輸送選択プロセス</span><span class="sxs-lookup"><span data-stu-id="cf969-159">Transport selection process</span></span>

<span data-ttu-id="cf969-160">次の一覧は、SignalR が使用するトランスポートを決定するために使用する手順を示しています。</span><span class="sxs-lookup"><span data-stu-id="cf969-160">The following list shows the steps that SignalR uses to decide which transport to use.</span></span>

1. <span data-ttu-id="cf969-161">ブラウザが Internet Explorer 8 以前の場合は、ロングポーリングが使用されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-161">If the browser is Internet Explorer 8 or earlier, Long Polling is used.</span></span>
2. <span data-ttu-id="cf969-162">JSONP が構成されている場合 (つまり`jsonp`、接続の開始時`true`にパラメーターが設定されている場合)、ロングポーリングが使用されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-162">If JSONP is configured (that is, the `jsonp` parameter is set to `true` when the connection is started), Long Polling is used.</span></span>
3. <span data-ttu-id="cf969-163">クロスドメイン接続が行われている場合 (つまり、SignalR エンドポイントがホスティング ページと同じドメインにない場合)、次の条件が満たされている場合は WebSocket が使用されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-163">If a cross-domain connection is being made (that is, if the SignalR endpoint is not in the same domain as the hosting page), then WebSocket will be used if the following criteria are met:</span></span>

   - <span data-ttu-id="cf969-164">クライアントは CORS (クロスオリジンリソース共有) をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="cf969-164">The client supports CORS (Cross-Origin Resource Sharing).</span></span> <span data-ttu-id="cf969-165">CORS をサポートするクライアントの詳細については[、caniuse.comの CORS](http://www.caniuse.com/CORS)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cf969-165">For details on which clients support CORS, see [CORS at caniuse.com](http://www.caniuse.com/CORS).</span></span>
   - <span data-ttu-id="cf969-166">クライアントは Web ソケットをサポートしています</span><span class="sxs-lookup"><span data-stu-id="cf969-166">The client supports WebSocket</span></span>
   - <span data-ttu-id="cf969-167">サーバーは Web ソケットをサポートしています</span><span class="sxs-lookup"><span data-stu-id="cf969-167">The server supports WebSocket</span></span>

     <span data-ttu-id="cf969-168">これらの条件のいずれかが満たされない場合は、ロングポーリングが使用されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-168">If any of these criteria are not met, Long Polling will be used.</span></span> <span data-ttu-id="cf969-169">クロスドメイン接続の詳細については、クロス[ドメイン接続を確立する方法を](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)参照してください。</span><span class="sxs-lookup"><span data-stu-id="cf969-169">For more information on cross-domain connections, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>
4. <span data-ttu-id="cf969-170">JSONP が構成されておらず、接続がクロスドメインでない場合、クライアントとサーバーの両方がサポートしている場合は WebSocket が使用されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-170">If JSONP is not configured and the connection is not cross-domain, WebSocket will be used if both the client and server support it.</span></span>
5. <span data-ttu-id="cf969-171">クライアントまたはサーバーのいずれかが WebSocket をサポートしていない場合、サーバー送信イベントが使用可能な場合は使用されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-171">If either the client or server do not support WebSocket, Server Sent Events is used if it is available.</span></span>
6. <span data-ttu-id="cf969-172">サーバー送信イベントが使用できない場合は、フォーエバーフレームが試行されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-172">If Server Sent Events is not available, Forever Frame is attempted.</span></span>
7. <span data-ttu-id="cf969-173">フォーエバーフレームに障害が発生した場合は、ロングポーリングが使用されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-173">If Forever Frame fails, Long Polling is used.</span></span>

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a><span data-ttu-id="cf969-174">トランスポートの監視</span><span class="sxs-lookup"><span data-stu-id="cf969-174">Monitoring transports</span></span>

<span data-ttu-id="cf969-175">ハブでログを有効にし、ブラウザーでコンソール ウィンドウを開くと、アプリケーションが使用しているトランスポートを確認できます。</span><span class="sxs-lookup"><span data-stu-id="cf969-175">You can determine what transport your application is using by enabling logging on your hub, and opening the console window in your browser.</span></span>

<span data-ttu-id="cf969-176">ブラウザーでハブのイベントのログ記録を有効にするには、クライアント アプリケーションに次のコマンドを追加します。</span><span class="sxs-lookup"><span data-stu-id="cf969-176">To enable logging for your hub's events in a browser, add the following command to your client application:</span></span>

`$.connection.hub.logging = true;`

- <span data-ttu-id="cf969-177">Internet Explorer で、F12 キーを押して開発者ツールを開き、[コンソール] タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="cf969-177">In Internet Explorer, open the developer tools by pressing F12, and click the Console tab.</span></span>

    ![インターネット エクスプローラのコンソール](introduction-to-signalr/_static/image2.png)
- <span data-ttu-id="cf969-179">Chrome で、Ctrl キーを押しながら Shift キーを押しながら J キーを押してコンソールを開きます。</span><span class="sxs-lookup"><span data-stu-id="cf969-179">In Chrome, open the console by pressing Ctrl+Shift+J.</span></span>

    ![グーグルクロームのコンソール](introduction-to-signalr/_static/image3.png)

<span data-ttu-id="cf969-181">コンソールを開いてログを記録すると、SignalR によって使用されているトランスポートを確認できます。</span><span class="sxs-lookup"><span data-stu-id="cf969-181">With the console open and logging enabled, you'll be able to see which transport is being used by SignalR.</span></span>

![WebSocket トランスポートを示すインターネット エクスプローラのコンソール](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a><span data-ttu-id="cf969-183">トランスポートの指定</span><span class="sxs-lookup"><span data-stu-id="cf969-183">Specifying a transport</span></span>

<span data-ttu-id="cf969-184">トランスポートのネゴシエーションには、一定の時間とクライアント/サーバーリソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="cf969-184">Negotiating a transport takes a certain amount of time and client/server resources.</span></span> <span data-ttu-id="cf969-185">クライアント機能がわかっている場合は、クライアント接続の開始時にトランスポートを指定できます。</span><span class="sxs-lookup"><span data-stu-id="cf969-185">If the client capabilities are known, then a transport can be specified when the client connection is started.</span></span> <span data-ttu-id="cf969-186">次のコード スニペットは、クライアントが他のプロトコルをサポートしていない場合に使用される Ajax ロング ポーリング トランスポートを使用して接続を開始する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="cf969-186">The following code snippet demonstrates starting a connection using the Ajax Long Polling transport, as would be used if it was known that the client did not support any other protocol:</span></span>

`connection.start({ transport: 'longPolling' });`

<span data-ttu-id="cf969-187">クライアントが特定のトランスポートを順番に試す場合は、フォールバック順序を指定できます。</span><span class="sxs-lookup"><span data-stu-id="cf969-187">You can specify a fallback order if you want a client to try specific transports in order.</span></span> <span data-ttu-id="cf969-188">次のコード スニペットは、WebSocket を試してみて、それを失敗して、ロング ポーリングに直接行くことを示しています。</span><span class="sxs-lookup"><span data-stu-id="cf969-188">The following code snippet demonstrates trying WebSocket, and failing that, going directly to Long Polling.</span></span>

`connection.start({ transport: ['webSockets','longPolling'] });`

<span data-ttu-id="cf969-189">トランスポートを指定するための文字列定数は、次のように定義されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-189">The string constants for specifying transports are defined as follows:</span></span>

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a><span data-ttu-id="cf969-190">接続とハブ</span><span class="sxs-lookup"><span data-stu-id="cf969-190">Connections and Hubs</span></span>

<span data-ttu-id="cf969-191">SignalR API には、クライアントとサーバー間の通信用の 2 つのモデルが含まれています: 永続的な接続とハブ。</span><span class="sxs-lookup"><span data-stu-id="cf969-191">The SignalR API contains two models for communicating between clients and servers: Persistent Connections and Hubs.</span></span>

<span data-ttu-id="cf969-192">接続は、単一受信者、グループ化、またはブロードキャスト メッセージを送信するための単純なエンドポイントを表します。</span><span class="sxs-lookup"><span data-stu-id="cf969-192">A Connection represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="cf969-193">永続接続 API (PersistentConnection クラスによって .NET コードで表される) は、SignalR が公開する低レベルの通信プロトコルに開発者が直接アクセスすることを許可します。</span><span class="sxs-lookup"><span data-stu-id="cf969-193">The Persistent Connection API (represented in .NET code by the PersistentConnection class) gives the developer direct access to the low-level communication protocol that SignalR exposes.</span></span> <span data-ttu-id="cf969-194">接続通信モデルを使用すると、Windows コミュニケーション 基盤などの接続ベースの API を使用した開発者にはなじみ深いものです。</span><span class="sxs-lookup"><span data-stu-id="cf969-194">Using the Connections communication model will be familiar to developers who have used connection-based APIs such as Windows Communication Foundation.</span></span>

<span data-ttu-id="cf969-195">ハブは、クライアントとサーバーが互いに直接メソッドを呼び出すことができる、接続 API に基づいて構築されたより高レベルのパイプラインです。</span><span class="sxs-lookup"><span data-stu-id="cf969-195">A Hub is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span> <span data-ttu-id="cf969-196">SignalR は、マシン境界を越えてのディスパッチを魔法のように処理し、クライアントがローカル メソッドと同じくらい簡単にサーバー上のメソッドを呼び出すことを可能にします。</span><span class="sxs-lookup"><span data-stu-id="cf969-196">SignalR handles the dispatching across machine boundaries as if by magic, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="cf969-197">Hubs 通信モデルを使用することは、.NET リモート処理などのリモート呼び出し API を使用した開発者にとってなじみ深いものです。</span><span class="sxs-lookup"><span data-stu-id="cf969-197">Using the Hubs communication model will be familiar to developers who have used remote invocation APIs such as .NET Remoting.</span></span> <span data-ttu-id="cf969-198">ハブを使用すると、厳密に型指定されたパラメーターをメソッドに渡して、モデル バインドを有効にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="cf969-198">Using a Hub also allows you to pass strongly typed parameters to methods, enabling model binding.</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="cf969-199">アーキテクチャの図</span><span class="sxs-lookup"><span data-stu-id="cf969-199">Architecture diagram</span></span>

<span data-ttu-id="cf969-200">次の図は、ハブ、永続的接続、およびトランスポートに使用される基盤となるテクノロジの関係を示しています。</span><span class="sxs-lookup"><span data-stu-id="cf969-200">The following diagram shows the relationship between Hubs, Persistent Connections, and the underlying technologies used for transports.</span></span>

![API、トランスポート、およびクライアントを示す SignalR アーキテクチャ図](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a><span data-ttu-id="cf969-202">ハブの仕組み</span><span class="sxs-lookup"><span data-stu-id="cf969-202">How Hubs work</span></span>

<span data-ttu-id="cf969-203">サーバー側コードがクライアント上のメソッドを呼び出すと、呼び出されるメソッドの名前とパラメーターを含むアクティブなトランスポートを介してパケットが送信されます (オブジェクトがメソッド パラメーターとして送信されると、JSON を使用してシリアル化されます)。</span><span class="sxs-lookup"><span data-stu-id="cf969-203">When server-side code calls a method on the client, a packet is sent across the active transport that contains the name and parameters of the method to be called (when an object is sent as a method parameter, it is serialized using JSON).</span></span> <span data-ttu-id="cf969-204">クライアントは、クライアント側のコードで定義されたメソッドにメソッド名を一致します。</span><span class="sxs-lookup"><span data-stu-id="cf969-204">The client then matches the method name to methods defined in client-side code.</span></span> <span data-ttu-id="cf969-205">一致する場合、クライアント メソッドは逆シリアル化されたパラメーター データを使用して実行されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-205">If there is a match, the client method will be executed using the deserialized parameter data.</span></span>

<span data-ttu-id="cf969-206">メソッド呼び出しは[、Fiddler](http://fiddler2.com/)などのツールを使用して監視できます。</span><span class="sxs-lookup"><span data-stu-id="cf969-206">The method call can be monitored using tools like [Fiddler.](http://fiddler2.com/)</span></span> <span data-ttu-id="cf969-207">次の図は、Fiddler のログ ペインで SignalR サーバーから Web ブラウザー クライアントに送信されるメソッド呼び出しを示しています。</span><span class="sxs-lookup"><span data-stu-id="cf969-207">The following image shows a method call sent from a SignalR server to a web browser client in the Logs pane of Fiddler.</span></span> <span data-ttu-id="cf969-208">メソッド呼び出しは、 という`MoveShapeHub`ハブから送信され、呼び出されるメソッド`updateShape`が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-208">The method call is being sent from a hub called `MoveShapeHub`, and the method being invoked is called `updateShape`.</span></span>

![SignalR トラフィックを示すフィドラー ログのビュー](introduction-to-signalr/_static/image6.png)

<span data-ttu-id="cf969-210">この例では、ハブ名は`H`パラメーターで識別されます。メソッド名は`M`パラメーターで識別され、メソッドに送信されるデータは`A`パラメーターで識別されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-210">In this example, the hub name is identified with the `H` parameter; the method name is identified with the `M` parameter, and the data being sent to the method is identified with the `A` parameter.</span></span> <span data-ttu-id="cf969-211">このメッセージを生成したアプリケーションは、[高周波リアルタイム](tutorial-high-frequency-realtime-with-signalr.md)チュートリアルで作成されます。</span><span class="sxs-lookup"><span data-stu-id="cf969-211">The application that generated this message is created in the [High-Frequency Realtime](tutorial-high-frequency-realtime-with-signalr.md) tutorial.</span></span>

### <a name="choosing-a-communication-model"></a><span data-ttu-id="cf969-212">通信モデルの選択</span><span class="sxs-lookup"><span data-stu-id="cf969-212">Choosing a communication model</span></span>

<span data-ttu-id="cf969-213">ほとんどのアプリケーションでは、Hubs API を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cf969-213">Most applications should use the Hubs API.</span></span> <span data-ttu-id="cf969-214">接続 API は、次の状況で使用できます。</span><span class="sxs-lookup"><span data-stu-id="cf969-214">The Connections API could be used in the following circumstances:</span></span>

- <span data-ttu-id="cf969-215">実際に送信されるメッセージの形式を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cf969-215">The format of the actual message sent needs to be specified.</span></span>
- <span data-ttu-id="cf969-216">開発者は、リモート呼び出しモデルではなく、メッセージングとディスパッチ モデルを使用することを好みます。</span><span class="sxs-lookup"><span data-stu-id="cf969-216">The developer prefers to work with a messaging and dispatching model rather than a remote invocation model.</span></span>
- <span data-ttu-id="cf969-217">SignalR を使用するために、メッセージング モデルを使用する既存のアプリケーションが移植されています。</span><span class="sxs-lookup"><span data-stu-id="cf969-217">An existing application that uses a messaging model is being ported to use SignalR.</span></span>
