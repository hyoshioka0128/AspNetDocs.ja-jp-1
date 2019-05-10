---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC ルーティング概要 (VB) |Microsoft Docs
author: StephenWalther
description: このチュートリアルでは、Stephen Walther は、ASP.NET MVC フレームワークがコント ローラー アクションへのブラウザーの要求をマップする方法を示します。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123644"
---
# <a name="aspnet-mvc-routing-overview-vb"></a><span data-ttu-id="b6544-103">ASP.NET MVC ルーティング概要 (VB)</span><span class="sxs-lookup"><span data-stu-id="b6544-103">ASP.NET MVC Routing Overview (VB)</span></span>

<span data-ttu-id="b6544-104">によって[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="b6544-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="b6544-105">このチュートリアルでは、Stephen Walther は、ASP.NET MVC フレームワークがコント ローラー アクションへのブラウザーの要求をマップする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="b6544-105">In this tutorial, Stephen Walther shows how the ASP.NET MVC framework maps browser requests to controller actions.</span></span>

<span data-ttu-id="b6544-106">このチュートリアルと呼ばれるすべての ASP.NET MVC アプリケーションの重要な機能に導入された*ASP.NET ルーティング*します。</span><span class="sxs-lookup"><span data-stu-id="b6544-106">In this tutorial, you are introduced to an important feature of every ASP.NET MVC application called *ASP.NET Routing*.</span></span> <span data-ttu-id="b6544-107">ASP.NET ルーティング モジュールは、特定の MVC コント ローラー アクションへの受信ブラウザー要求をマッピングします。</span><span class="sxs-lookup"><span data-stu-id="b6544-107">The ASP.NET Routing module is responsible for mapping incoming browser requests to particular MVC controller actions.</span></span> <span data-ttu-id="b6544-108">このチュートリアルの目的は、標準的なルート テーブルがコント ローラー アクションへの要求をマップする方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="b6544-108">By the end of this tutorial, you will understand how the standard route table maps requests to controller actions.</span></span>

## <a name="using-the-default-route-table"></a><span data-ttu-id="b6544-109">既定のルート テーブルを使用します。</span><span class="sxs-lookup"><span data-stu-id="b6544-109">Using the Default Route Table</span></span>

<span data-ttu-id="b6544-110">新しい ASP.NET MVC アプリケーションを作成するときに ASP.NET のルーティングを使用するアプリケーションが既に構成されています。</span><span class="sxs-lookup"><span data-stu-id="b6544-110">When you create a new ASP.NET MVC application, the application is already configured to use ASP.NET Routing.</span></span> <span data-ttu-id="b6544-111">ASP.NET ルーティングは、2 つの場所でのセットアップです。</span><span class="sxs-lookup"><span data-stu-id="b6544-111">ASP.NET Routing is setup in two places.</span></span>

<span data-ttu-id="b6544-112">最初に、ASP.NET ルーティングは、アプリケーションの Web 構成ファイル (web.config) で有効です。</span><span class="sxs-lookup"><span data-stu-id="b6544-112">First, ASP.NET Routing is enabled in your application's Web configuration file (Web.config file).</span></span> <span data-ttu-id="b6544-113">ルーティングに関連する構成ファイルで次の 4 つのセクションがあります: system.web.httpModules セクション、system.web.httpHandlers セクション、system.webserver.modules セクションおよび system.webserver.handlers セクション。</span><span class="sxs-lookup"><span data-stu-id="b6544-113">There are four sections in the configuration file that are relevant to routing: the system.web.httpModules section, the system.web.httpHandlers section, the system.webserver.modules section, and the system.webserver.handlers section.</span></span> <span data-ttu-id="b6544-114">これらのセクションではないルーティングは動作しないために、これらのセクションを削除しないように注意します。</span><span class="sxs-lookup"><span data-stu-id="b6544-114">Be careful not to delete these sections because without these sections routing will no longer work.</span></span>

<span data-ttu-id="b6544-115">次に、そして何よりも、ルート テーブルは、アプリケーションの Global.asax ファイルに作成されます。</span><span class="sxs-lookup"><span data-stu-id="b6544-115">Second, and more importantly, a route table is created in the application's Global.asax file.</span></span> <span data-ttu-id="b6544-116">Global.asax ファイルは、ASP.NET アプリケーションのライフ サイクル イベントのイベント ハンドラーを含む特殊なファイルです。</span><span class="sxs-lookup"><span data-stu-id="b6544-116">The Global.asax file is a special file that contains event handlers for ASP.NET application lifecycle events.</span></span> <span data-ttu-id="b6544-117">ルート テーブルは、アプリケーションの開始イベント中に作成されます。</span><span class="sxs-lookup"><span data-stu-id="b6544-117">The route table is created during the Application Start event.</span></span>

<span data-ttu-id="b6544-118">リスト 1 でファイルには、ASP.NET MVC アプリケーションの既定の Global.asax ファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b6544-118">The file in Listing 1 contains the default Global.asax file for an ASP.NET MVC application.</span></span>

<span data-ttu-id="b6544-119">**1 - Global.asax.vb を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="b6544-119">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

<span data-ttu-id="b6544-120">MVC アプリケーションを最初の起動時、アプリケーション\_Start() メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="b6544-120">When an MVC application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="b6544-121">このメソッドは、さらに、RegisterRoutes() メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b6544-121">This method, in turn, calls the RegisterRoutes() method.</span></span> <span data-ttu-id="b6544-122">RegisterRoutes() メソッドは、ルート テーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="b6544-122">The RegisterRoutes() method creates the route table.</span></span>

<span data-ttu-id="b6544-123">既定のルーティング テーブルには、Default という 1 つのルートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b6544-123">The default route table contains a single route (named Default).</span></span> <span data-ttu-id="b6544-124">既定のルートがコント ローラー名、コント ローラーのアクションへの URL は、2 番目のセグメントおよびという名前のパラメーターを 3 番目のセグメントに URL の最初のセグメントをマップ**id**します。</span><span class="sxs-lookup"><span data-stu-id="b6544-124">The Default route maps the first segment of a URL to a controller name, the second segment of a URL to a controller action, and the third segment to a parameter named **id**.</span></span>

<span data-ttu-id="b6544-125">Web ブラウザーのアドレス バーには、次の URL を入力することを想像してください。</span><span class="sxs-lookup"><span data-stu-id="b6544-125">Imagine that you enter the following URL into your web browser's address bar:</span></span>

<span data-ttu-id="b6544-126">/Home/Index/3</span><span class="sxs-lookup"><span data-stu-id="b6544-126">/Home/Index/3</span></span>

<span data-ttu-id="b6544-127">既定のルートは、この URL を次のパラメーターにマッピングされます。</span><span class="sxs-lookup"><span data-stu-id="b6544-127">The Default route maps this URL to the following parameters:</span></span>

- <span data-ttu-id="b6544-128">controller = Home</span><span class="sxs-lookup"><span data-stu-id="b6544-128">controller = Home</span></span>

- <span data-ttu-id="b6544-129">action = Index</span><span class="sxs-lookup"><span data-stu-id="b6544-129">action = Index</span></span>

- <span data-ttu-id="b6544-130">id = 3</span><span class="sxs-lookup"><span data-stu-id="b6544-130">id = 3</span></span>

<span data-ttu-id="b6544-131">URL/Home、インデックス、3 を要求するときに、次のコードが実行されます。</span><span class="sxs-lookup"><span data-stu-id="b6544-131">When you request the URL /Home/Index/3, the following code is executed:</span></span>

<span data-ttu-id="b6544-132">HomeController.Index(3)</span><span class="sxs-lookup"><span data-stu-id="b6544-132">HomeController.Index(3)</span></span>

<span data-ttu-id="b6544-133">既定のルートには、次の 3 つのすべてのパラメーターの既定値が含まれています。</span><span class="sxs-lookup"><span data-stu-id="b6544-133">The Default route includes defaults for all three parameters.</span></span> <span data-ttu-id="b6544-134">コント ローラーを指定しない場合、コント ローラー パラメーターの既定値、値**ホーム**します。</span><span class="sxs-lookup"><span data-stu-id="b6544-134">If you don't supply a controller, then the controller parameter defaults to the value **Home**.</span></span> <span data-ttu-id="b6544-135">アクション パラメーターの値に既定値アクションを指定しない場合**インデックス**します。</span><span class="sxs-lookup"><span data-stu-id="b6544-135">If you don't supply an action, the action parameter defaults to the value **Index**.</span></span> <span data-ttu-id="b6544-136">最後に、id を指定しない場合は、id パラメーターが空の文字列に既定値です。</span><span class="sxs-lookup"><span data-stu-id="b6544-136">Finally, if you don't supply an id, the id parameter defaults to an empty string.</span></span>

<span data-ttu-id="b6544-137">既定のルートがコント ローラー アクションへの Url をマップする方法の例をいくつか見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="b6544-137">Let's look at a few examples of how the Default route maps URLs to controller actions.</span></span> <span data-ttu-id="b6544-138">ブラウザーのアドレス バーには、次の URL を入力することを想像してください。</span><span class="sxs-lookup"><span data-stu-id="b6544-138">Imagine that you enter the following URL into your browser address bar:</span></span>

<span data-ttu-id="b6544-139">/Home</span><span class="sxs-lookup"><span data-stu-id="b6544-139">/Home</span></span>

<span data-ttu-id="b6544-140">既定ルート パラメーターの既定値のためこの URL を入力する、HomeController クラスの Index() メソッドを呼び出せるリスト 2 でします。</span><span class="sxs-lookup"><span data-stu-id="b6544-140">Because of the Default route parameter defaults, entering this URL will cause the Index() method of the HomeController class in Listing 2 to be called.</span></span>

<span data-ttu-id="b6544-141">**2 - HomeController.vb を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="b6544-141">**Listing 2 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

<span data-ttu-id="b6544-142">リスト 2 では、HomeController クラスに Index() という名前の id。 1 つのパラメーターを受け取るという名前のメソッドが含まれます。URL/Home はにより呼び出される値は、Id パラメーターの値として何も Index() メソッドです。</span><span class="sxs-lookup"><span data-stu-id="b6544-142">In Listing 2, the HomeController class includes a method named Index() that accepts a single parameter named Id. The URL /Home causes the Index() method to be called with the value Nothing as the value of the Id parameter.</span></span>

<span data-ttu-id="b6544-143">URL/Home には、MVC フレームワークがコント ローラー アクションを呼び出すことにより、リスト 3 のテンプレートを使用するクラスの Index() メソッドもと一致します。</span><span class="sxs-lookup"><span data-stu-id="b6544-143">Because of the way that the MVC framework invokes controller actions, the URL /Home also matches the Index() method of the HomeController class in Listing 3.</span></span>

<span data-ttu-id="b6544-144">**3 - HomeController.vb (パラメーターなしでの Index アクション) を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="b6544-144">**Listing 3 - HomeController.vb (Index action with no parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

<span data-ttu-id="b6544-145">Index() メソッドは、リスト 3 では、すべてのパラメーターは受け入れられません。</span><span class="sxs-lookup"><span data-stu-id="b6544-145">The Index() method in Listing 3 does not accept any parameters.</span></span> <span data-ttu-id="b6544-146">URL/Home をこの Index() メソッドが呼び出されるとなります。</span><span class="sxs-lookup"><span data-stu-id="b6544-146">The URL /Home will cause this Index() method to be called.</span></span> <span data-ttu-id="b6544-147">また、URL /Home/Index/3 は、(Id は無視されます) このメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b6544-147">The URL /Home/Index/3 also invokes this method (the Id is ignored).</span></span>

<span data-ttu-id="b6544-148">URL/Home には、リスト 4 HomeController クラスの Index() メソッドもと一致します。</span><span class="sxs-lookup"><span data-stu-id="b6544-148">The URL /Home also matches the Index() method of the HomeController class in Listing 4.</span></span>

<span data-ttu-id="b6544-149">**4 - HomeController.vb (null 許容パラメーターを使用してインデックスの操作) を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="b6544-149">**Listing 4 - HomeController.vb (Index action with nullable parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

<span data-ttu-id="b6544-150">Index() メソッドではリスト 4、1 つの整数パラメーターがあります。</span><span class="sxs-lookup"><span data-stu-id="b6544-150">In Listing 4, the Index() method has one Integer parameter.</span></span> <span data-ttu-id="b6544-151">パラメーターは null 許容パラメーター (値を持つことは Nothing) では、エラーを発生させず、Index() を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="b6544-151">Because the parameter is a nullable parameter (can have the value Nothing), the Index() can be called without raising an error.</span></span>

<span data-ttu-id="b6544-152">最後に、Id パラメーターから例外が発生した URL/Home でリスト 5 で Index() メソッドを呼び出す*ない*null 許容パラメーター。</span><span class="sxs-lookup"><span data-stu-id="b6544-152">Finally, invoking the Index() method in Listing 5 with the URL /Home causes an exception since the Id parameter *is not* a nullable parameter.</span></span> <span data-ttu-id="b6544-153">Index() メソッドを呼び出すしようとした場合、エラーが発生した図 1 に表示されます。</span><span class="sxs-lookup"><span data-stu-id="b6544-153">If you attempt to invoke the Index() method then you get the error displayed in Figure 1.</span></span>

<span data-ttu-id="b6544-154">**5 - HomeController.vb (Id パラメーターを使用してインデックスの操作) を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="b6544-154">**Listing 5 - HomeController.vb (Index action with Id parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

<span data-ttu-id="b6544-155">[![パラメーターの値が必要とするコント ローラー アクションの呼び出し](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b6544-155">[![Invoking a controller action that expects a parameter value](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="b6544-156">**図 01**:パラメーターの値が必要とするコント ローラー アクションの呼び出し ([フルサイズの画像を表示する をクリックします](asp-net-mvc-routing-overview-vb/_static/image2.png))。</span><span class="sxs-lookup"><span data-stu-id="b6544-156">**Figure 01**: Invoking a controller action that expects a parameter value ([Click to view full-size image](asp-net-mvc-routing-overview-vb/_static/image2.png))</span></span>

<span data-ttu-id="b6544-157">URL /Home/Index/3 は一方で、リスト 5 でインデックスのコント ローラー アクションでうまくいきます。</span><span class="sxs-lookup"><span data-stu-id="b6544-157">The URL /Home/Index/3, on the other hand, works just fine with the Index controller action in Listing 5.</span></span> <span data-ttu-id="b6544-158">要求/Home/Index/3 とにより、3 の値を持つ Id パラメーターで呼び出される Index() メソッドです。</span><span class="sxs-lookup"><span data-stu-id="b6544-158">The request /Home/Index/3 causes the Index() method to be called with an Id parameter that has the value 3.</span></span>

## <a name="summary"></a><span data-ttu-id="b6544-159">まとめ</span><span class="sxs-lookup"><span data-stu-id="b6544-159">Summary</span></span>

<span data-ttu-id="b6544-160">このチュートリアルの目的は、ASP.NET ルーティングの概要を提供することでした。</span><span class="sxs-lookup"><span data-stu-id="b6544-160">The goal of this tutorial was to provide you with a brief introduction to ASP.NET Routing.</span></span> <span data-ttu-id="b6544-161">新しい ASP.NET MVC アプリケーションで得られる既定のルーティング テーブルを調査します。</span><span class="sxs-lookup"><span data-stu-id="b6544-161">We examined the default route table that you get with a new ASP.NET MVC application.</span></span> <span data-ttu-id="b6544-162">既定のルートがコント ローラー アクションへの Url をマップする方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="b6544-162">You learned how the default route maps URLs to controller actions.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b6544-163">[前へ](creating-an-action-cs.md)
> [次へ](understanding-action-filters-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b6544-163">[Previous](creating-an-action-cs.md)
[Next](understanding-action-filters-vb.md)</span></span>
