---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: ASP.NET MVC 実行プロセスの理解 |Microsoft Docs
author: microsoft
description: ASP.NET MVC フレームワークがステップ バイ ステップのブラウザー要求を処理する方法について説明します。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 28940947253e0af43886cf1231f8aaf4615526cc
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65125482"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="63fd8-103">ASP.NET MVC 実行プロセスを理解する</span><span class="sxs-lookup"><span data-stu-id="63fd8-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="63fd8-104">によって[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="63fd8-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="63fd8-105">ASP.NET MVC フレームワークがステップ バイ ステップのブラウザー要求を処理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="63fd8-106">ASP.NET MVC ベースの Web アプリケーションへの要求が最初に通過、 **UrlRoutingModule**オブジェクトで、HTTP モジュールです。</span><span class="sxs-lookup"><span data-stu-id="63fd8-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="63fd8-107">このモジュールは、要求を解析し、ルートの選択を実行します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="63fd8-108">**UrlRoutingModule**オブジェクトが現在の要求と一致する最初のルート オブジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="63fd8-109">(ルート オブジェクトを実装するクラスは、 **RouteBase**と通常のインスタンスでは、**ルート**クラスです)。ルートが一致しない場合、 **UrlRoutingModule**オブジェクトは、何も実行でき、フォールバックする通常の ASP.NET または IIS 要求処理要求。</span><span class="sxs-lookup"><span data-stu-id="63fd8-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="63fd8-110">選択されている**ルート**オブジェクト、 **UrlRoutingModule**オブジェクトを取得、 **IRouteHandler**オブジェクトに関連付けられている、**ルート**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="63fd8-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="63fd8-111">通常、MVC アプリケーションのこのインスタンスになります。 の**MvcRouteHandler**します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="63fd8-112">**IRouteHandler**インスタンスを作成、 **IHttpHandler**オブジェクトを渡します、 **IHttpContext**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="63fd8-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="63fd8-113">既定で、 **IHttpHandler** MVC がのインスタンス、 **MvcHandler**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="63fd8-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="63fd8-114">**MvcHandler**オブジェクトが、最終的には、要求を処理するコント ローラーを選択します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="63fd8-115">IIS 7.0 で ASP.NET MVC Web アプリケーションを実行すると、ファイル名拡張子の MVC プロジェクトの必要はありません。</span><span class="sxs-lookup"><span data-stu-id="63fd8-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="63fd8-116">ただし、IIS 6.0 では、ハンドラーが必要です、ASP.NET ISAPI DLL には、.mvc ファイル名拡張子をマップすること。</span><span class="sxs-lookup"><span data-stu-id="63fd8-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="63fd8-117">モジュールとハンドラーは、ASP.NET MVC フレームワークのエントリ ポイントです。</span><span class="sxs-lookup"><span data-stu-id="63fd8-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="63fd8-118">次の操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-118">They perform the following actions:</span></span>

- <span data-ttu-id="63fd8-119">MVC Web アプリケーションでは、適切なコント ローラーを選択します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="63fd8-120">特定のコント ローラー インスタンスを取得します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="63fd8-121">コント ローラーを呼び出す**Execute**メソッド。</span><span class="sxs-lookup"><span data-stu-id="63fd8-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="63fd8-122">MVC Web プロジェクトの実行の段階を次に示します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="63fd8-123">アプリケーションの最初の要求を受信します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="63fd8-124">Global.asax ファイルで**ルート**オブジェクトに追加されます、 **RouteTable**オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="63fd8-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="63fd8-125">ルーティングを実行します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-125">Perform routing</span></span> 

    - <span data-ttu-id="63fd8-126">**UrlRoutingModule**最初に一致するモジュールを使用して**ルート**オブジェクト、 **RouteTable**コレクションを作成する、 **RouteData**使用して、作成、オブジェクト、 **RequestContext** (**IHttpContext**) オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="63fd8-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="63fd8-127">MVC 要求ハンドラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="63fd8-128">**MvcRouteHandler**オブジェクトのインスタンスを作成する、 **MvcHandler**クラスを渡します、 **RequestContext**インスタンス。</span><span class="sxs-lookup"><span data-stu-id="63fd8-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="63fd8-129">コント ローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-129">Create controller</span></span> 

    - <span data-ttu-id="63fd8-130">**MvcHandler**オブジェクトで使用、 **RequestContext**インスタンスを識別するために、 **IControllerFactory**オブジェクト (通常のインスタンス、 **DefaultControllerFactory**クラス) を使用して、コント ローラー インスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="63fd8-131">Execute のコント ローラー -、 **MvcHandler**インスタンスが s コント ローラーを呼び出す**Execute**メソッド。</span><span class="sxs-lookup"><span data-stu-id="63fd8-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="63fd8-132">アクションを呼び出す</span><span class="sxs-lookup"><span data-stu-id="63fd8-132">Invoke action</span></span> 

    - <span data-ttu-id="63fd8-133">継承するほとんどのコント ローラー、**コント ローラー**基本クラス。</span><span class="sxs-lookup"><span data-stu-id="63fd8-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="63fd8-134">それを実行するコント ローラー、 **ControllerActionInvoker**コント ローラーに関連付けられているオブジェクトが呼び出すために、コント ローラー クラスのアクション メソッドを決定し、そのメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="63fd8-135">結果を実行します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-135">Execute result</span></span> 

    - <span data-ttu-id="63fd8-136">一般的なアクション メソッドでは、ユーザー入力を受け取る、適切な応答データを準備、および結果型を返すことによって、結果を実行可能性があります。</span><span class="sxs-lookup"><span data-stu-id="63fd8-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="63fd8-137">実行できる組み込みの結果型を以下に示します。**ViewResult** (ビューをレンダリングし、は、最もよく使用される結果型です)、 **RedirectToRouteResult**、 **RedirectResult**、 **ContentResult**、 **JsonResult**、および**EmptyResult**します。</span><span class="sxs-lookup"><span data-stu-id="63fd8-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
