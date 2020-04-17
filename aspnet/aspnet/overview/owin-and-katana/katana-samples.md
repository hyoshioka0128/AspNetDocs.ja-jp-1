---
uid: aspnet/overview/owin-and-katana/katana-samples
title: 片方のサンプル |マイクロソフトドキュメント
author: rick-anderson
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 15cc1084b16db2619f2295ee21dec4f49eb2e354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540442"
---
# <a name="katana-samples"></a><span data-ttu-id="2028e-102">Katana サンプル</span><span class="sxs-lookup"><span data-stu-id="2028e-102">Katana Samples</span></span>

<span data-ttu-id="2028e-103">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2028e-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="2028e-104">Katana サンプル</span><span class="sxs-lookup"><span data-stu-id="2028e-104">Katana Samples</span></span>

<span data-ttu-id="2028e-105">**ASP.NETルートサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="2028e-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="2028e-106">アプリケーションによっては、Asp.Netルート テーブル内の OWIN コンポーネントを非 OWIN コンポーネントと並べてフックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2028e-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="2028e-107">このサンプルでは、ルートコレクション拡張メソッドを使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="2028e-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="2028e-108">**分岐パイプラインのサンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="2028e-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="2028e-109">OWIN 要求処理パイプラインは線形である必要はありません。</span><span class="sxs-lookup"><span data-stu-id="2028e-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="2028e-110">このサンプルでは、要求パスまたはヘッダーなどの他の要求データに基づいて分岐パイプラインを構築する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="2028e-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="2028e-111">これらのコンポーネントは、Microsoft.Owin.Mapping の nuget パッケージで使用できます。</span><span class="sxs-lookup"><span data-stu-id="2028e-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="2028e-112">**カスタム サーバー サンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="2028e-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="2028e-113">OWIN を自己ホストする場合にカスタム OWIN サーバーを使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="2028e-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="2028e-114">**埋め込みサンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="2028e-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="2028e-115">OWIN サーバーの中には、独自のプロセス (&quot;自己ホスト&quot;型 ) の内部で実行できるものもあります。</span><span class="sxs-lookup"><span data-stu-id="2028e-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="2028e-116">このサンプルでは、Microsoft.Owin.Hosting の nuget パッケージによって提供されるツールを使用して OWIN アプリケーションを起動する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="2028e-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="2028e-117">**ハローワールドサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="2028e-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="2028e-118">OWIN は、さまざまなサーバー間でアプリケーションの移植性を可能にする HTTP サーバー API の抽象化です。</span><span class="sxs-lookup"><span data-stu-id="2028e-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="2028e-119">このサンプルでは、生の OWIN 抽象化を単純**なラッパー**で使用して Hello World アプリケーションを作成し、ASP.NETのような Web サーバー上で実行する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="2028e-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="2028e-120">**ハローワールド生のOWINサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="2028e-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="2028e-121">このサンプルでは、**生**の OWIN 抽象化を使用して Hello World アプリケーションを作成し、Asp.Netのような Web サーバー上で実行する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="2028e-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="2028e-122">**SignalR サンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="2028e-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="2028e-123">OWIN /カタナを使用して SignalR を自己ホストする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="2028e-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="2028e-124">自己ホスト型 SignalR について詳しくは、「[チュートリアル: SignalR セルフ ホスト](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2028e-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="2028e-125">**静的ファイルのサンプル** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="2028e-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="2028e-126">OWIN / Katana を使用して静的ファイルの HTTP 要求をサポートする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="2028e-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="2028e-127">**Web API** | [ソース コード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="2028e-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="2028e-128">このサンプルでは、IIS で OWIN をホストし、OWIN パイプラインに Web API を追加する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="2028e-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="2028e-129">**Web ソケットサンプル** | [ソースコード](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="2028e-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="2028e-130">クラスを使用して OWIN で Web[ソケットをサポートする方法を示します](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="2028e-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
