---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: MVC 実行プロセスASP.NETについて |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NET MVC フレームワークがブラウザー要求を段階的に処理する方法について説明します。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541027"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="b229a-103">ASP.NET MVC 実行プロセスを理解する</span><span class="sxs-lookup"><span data-stu-id="b229a-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="b229a-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b229a-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b229a-105">ASP.NET MVC フレームワークがブラウザー要求を段階的に処理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b229a-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="b229a-106">MVC ベースの web アプリケーション ASP.NETへの要求は、まず HTTP モジュールである**UrlRoutingModule**オブジェクトを通過します。</span><span class="sxs-lookup"><span data-stu-id="b229a-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="b229a-107">このモジュールは、要求を解析してルートの選択を行います。</span><span class="sxs-lookup"><span data-stu-id="b229a-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="b229a-108">オブジェクト**は**、現在の要求に一致する最初のルート オブジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="b229a-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="b229a-109">(ルート オブジェクトは**RouteBase**を実装するクラスで、通常は**Route**クラスのインスタンスです)。一致するルートがない場合 **、UrlRoutingModule**オブジェクトは何も行わないので、要求は通常のASP.NETまたは IIS 要求の処理にフォールバックします。</span><span class="sxs-lookup"><span data-stu-id="b229a-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="b229a-110">選択した**ルート**オブジェクトから **、UrlRoutingModule**オブジェクトは、**ルート**オブジェクトに関連付けられている**IRouteHandler**オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="b229a-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="b229a-111">通常、MVC アプリケーションでは、これは**MvcRouteHandler**のインスタンスになります。</span><span class="sxs-lookup"><span data-stu-id="b229a-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="b229a-112">インスタンス**は\*\*\*\*、IHttpHandler**オブジェクトを作成し、それを**渡**します。</span><span class="sxs-lookup"><span data-stu-id="b229a-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="b229a-113">既定では、MVC の**IHttpHandler**インスタンスは**MvcHandler**オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="b229a-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="b229a-114">**MvcHandler**オブジェクトは、最終的に要求を処理するコント ローラーを選択します。</span><span class="sxs-lookup"><span data-stu-id="b229a-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="b229a-115">ASP.NET MVC Web アプリケーションを IIS 7.0 で実行する場合、MVC プロジェクトにファイル名の拡張子は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="b229a-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="b229a-116">IIS 6.0 で実行する場合は、ファイル名の拡張子 .mvc を ASP.NET ISAPI DLL に関連付ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="b229a-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="b229a-117">モジュールとハンドラーは、ASP.NET MVC フレームワークへのエントリ ポイントです。</span><span class="sxs-lookup"><span data-stu-id="b229a-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="b229a-118">これらは次のアクションを実行します。</span><span class="sxs-lookup"><span data-stu-id="b229a-118">They perform the following actions:</span></span>

- <span data-ttu-id="b229a-119">MVC Web アプリケーションの適切なコントローラーを選択する。</span><span class="sxs-lookup"><span data-stu-id="b229a-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="b229a-120">特定のコントローラー インスタンスを取得する。</span><span class="sxs-lookup"><span data-stu-id="b229a-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="b229a-121">コントローラの**Execute**メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b229a-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="b229a-122">MVC Web プロジェクトの実行の段階を次に示します。</span><span class="sxs-lookup"><span data-stu-id="b229a-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="b229a-123">アプリケーションへの最初の要求を受け取る</span><span class="sxs-lookup"><span data-stu-id="b229a-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="b229a-124">グローバル.asax ファイルでは、**ルート**オブジェクトが**RouteTable**オブジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="b229a-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="b229a-125">ルーティングを実行する</span><span class="sxs-lookup"><span data-stu-id="b229a-125">Perform routing</span></span> 

    - <span data-ttu-id="b229a-126">モジュール**は\*\*\*\*、RouteTable**コレクション内の最初に一致する**Route**オブジェクトを使用して**RouteData**オブジェクトを作成し、そのオブジェクトを使用して**要求コンテキスト**(**IHttpContext**) オブジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="b229a-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="b229a-127">MVC 要求ハンドラーを作成する</span><span class="sxs-lookup"><span data-stu-id="b229a-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="b229a-128">オブジェクト**は\*\*\*\*、MvcHandler**クラスのインスタンスを作成し、**それを渡す、要求コンテキスト**インスタンスです。</span><span class="sxs-lookup"><span data-stu-id="b229a-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="b229a-129">コントローラーを作成する</span><span class="sxs-lookup"><span data-stu-id="b229a-129">Create controller</span></span> 

    - <span data-ttu-id="b229a-130">**MvcHandler**オブジェクトは、**コント**ローラー インスタンスを作成する**IControllerFactory**オブジェクト (通常は **、クラス**のインスタンス) を識別するインスタンスを使用します。</span><span class="sxs-lookup"><span data-stu-id="b229a-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="b229a-131">コント ローラーの実行 - **MvcHandler**インスタンスは、コント ローラーの**Execute**メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b229a-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="b229a-132">アクションを呼び出す</span><span class="sxs-lookup"><span data-stu-id="b229a-132">Invoke action</span></span> 

    - <span data-ttu-id="b229a-133">ほとんどのコントローラは、**コントローラ**の基本クラスから継承します。</span><span class="sxs-lookup"><span data-stu-id="b229a-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="b229a-134">コントローラーを呼び出すコント ローラーに関連付けられているコント ローラー**アクション呼び出**しオブジェクトは、呼び出すコント ローラー クラスのアクション メソッドを決定し、そのメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b229a-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="b229a-135">結果を実行する</span><span class="sxs-lookup"><span data-stu-id="b229a-135">Execute result</span></span> 

    - <span data-ttu-id="b229a-136">一般的なアクション メソッドでは、ユーザー入力を受け取り、適切な応答データを準備し、結果の型を返して結果を実行します。</span><span class="sxs-lookup"><span data-stu-id="b229a-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="b229a-137">実行できる組み込み結果の型には、**次**のものが含**JsonResult\*\*\*\*まれます。** **RedirectToRouteResult** **RedirectResult** **ContentResult**</span><span class="sxs-lookup"><span data-stu-id="b229a-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
