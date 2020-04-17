---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: アクション フィルタについて (C#) |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルの目的は、アクション フィルターについて説明することです。 アクション フィルターは、コントローラー アクションまたはコントローラー全体に適用できる属性です。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: 75ba7b1dce280a45cd092de97c464eade5f49838
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542184"
---
# <a name="understanding-action-filters-c"></a><span data-ttu-id="36f8c-104">アクション フィルターについて理解する (C#)</span><span class="sxs-lookup"><span data-stu-id="36f8c-104">Understanding Action Filters (C#)</span></span>

<span data-ttu-id="36f8c-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="36f8c-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="36f8c-106">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="36f8c-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> <span data-ttu-id="36f8c-107">このチュートリアルの目的は、アクション フィルターについて説明することです。</span><span class="sxs-lookup"><span data-stu-id="36f8c-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="36f8c-108">アクション フィルターは、コントローラー アクション (またはコントローラー全体) に適用できる属性で、アクションの実行方法を変更します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>

## <a name="understanding-action-filters"></a><span data-ttu-id="36f8c-109">アクション フィルタについて</span><span class="sxs-lookup"><span data-stu-id="36f8c-109">Understanding Action Filters</span></span>

<span data-ttu-id="36f8c-110">このチュートリアルの目的は、アクション フィルターについて説明することです。</span><span class="sxs-lookup"><span data-stu-id="36f8c-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="36f8c-111">アクション フィルターは、コントローラー アクション (またはコントローラー全体) に適用できる属性で、アクションの実行方法を変更します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="36f8c-112">ASP.NET MVC フレームワークには、いくつかのアクション フィルターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="36f8c-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="36f8c-113">OutputCache – このアクション フィルターは、指定された時間だけコントローラー アクションの出力をキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="36f8c-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="36f8c-114">HandleError – このアクション フィルターは、コント ローラー アクションの実行時に発生したエラーを処理します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="36f8c-115">[承認] – このアクション フィルターを使用すると、特定のユーザーまたはロールへのアクセスを制限できます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="36f8c-116">独自のカスタム アクション フィルターを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="36f8c-117">たとえば、カスタム認証システムを実装するためにカスタム アクション フィルターを作成する場合があります。</span><span class="sxs-lookup"><span data-stu-id="36f8c-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="36f8c-118">または、コントローラー アクションによって返されるビュー データを変更するアクション フィルターを作成する場合もあります。</span><span class="sxs-lookup"><span data-stu-id="36f8c-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="36f8c-119">このチュートリアルでは、アクション フィルターを最初から作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="36f8c-120">アクションの処理のさまざまな段階をログに記録するログ アクション フィルターを作成、 Visual Studio の出力ウィンドウ。</span><span class="sxs-lookup"><span data-stu-id="36f8c-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="36f8c-121">アクション フィルタの使用</span><span class="sxs-lookup"><span data-stu-id="36f8c-121">Using an Action Filter</span></span>

<span data-ttu-id="36f8c-122">アクション フィルターは属性です。</span><span class="sxs-lookup"><span data-stu-id="36f8c-122">An action filter is an attribute.</span></span> <span data-ttu-id="36f8c-123">ほとんどのアクションフィルタは、個々のコントローラアクションまたはコントローラ全体に適用できます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="36f8c-124">たとえば、リスト 1 のデータ コント ローラーは、`Index()`現在の時刻を返すという名前のアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="36f8c-125">このアクションは、アクション フィルター`OutputCache`で装飾されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="36f8c-126">このフィルターは、アクションによって返される値を 10 秒間キャッシュします。</span><span class="sxs-lookup"><span data-stu-id="36f8c-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="36f8c-127">**リスト1 –`Controllers\DataController.cs`**</span><span class="sxs-lookup"><span data-stu-id="36f8c-127">**Listing 1 – `Controllers\DataController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

<span data-ttu-id="36f8c-128">URL /Data/Index`Index()`をブラウザのアドレスバーに入力し、更新ボタンを複数回押してアクションを繰り返し呼び出すと、同じ時間が10秒間表示されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="36f8c-129">アクションの`Index()`出力は 10 秒間キャッシュされます (図 1 を参照)。</span><span class="sxs-lookup"><span data-stu-id="36f8c-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>

<span data-ttu-id="36f8c-130">[![キャッシュ時間](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="36f8c-130">[![Cached time](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span></span>

<span data-ttu-id="36f8c-131">**図 01**: キャッシュタイム ([フルサイズの画像を表示する をクリック](understanding-action-filters-cs/_static/image3.png)します )</span><span class="sxs-lookup"><span data-stu-id="36f8c-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-cs/_static/image3.png))</span></span>

<span data-ttu-id="36f8c-132">リスト 1 では、単一のアクション`OutputCache`フィルター (アクション フィルター `Index()` ) がメソッドに適用されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="36f8c-133">必要に応じて、同じアクションに複数のアクション フィルターを適用できます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="36f8c-134">たとえば、 と`OutputCache``HandleError`アクション フィルターの両方を同じアクションに適用できます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="36f8c-135">リスト 1 では`OutputCache`、アクション フィルターがアクション`Index()`に適用されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="36f8c-136">この属性をクラス自体に`DataController`適用することもできます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="36f8c-137">その場合、コントローラによって公開されたアクションによって返される結果は、10 秒間キャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="36f8c-138">さまざまな種類のフィルター</span><span class="sxs-lookup"><span data-stu-id="36f8c-138">The Different Types of Filters</span></span>

<span data-ttu-id="36f8c-139">ASP.NET MVC フレームワークは、4 種類のフィルターをサポートします。</span><span class="sxs-lookup"><span data-stu-id="36f8c-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="36f8c-140">承認フィルター – 属性`IAuthorizationFilter`を実装します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="36f8c-141">アクション フィルター –`IActionFilter`属性を実装します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="36f8c-142">結果フィルター – 属性`IResultFilter`を実装します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="36f8c-143">例外フィルター – 属性`IExceptionFilter`を実装します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="36f8c-144">フィルタは上記の順序で実行されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="36f8c-145">たとえば、承認フィルターは、アクション フィルターと例外フィルターが他のすべての種類のフィルターの後に常に実行される前に常に実行されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="36f8c-146">承認フィルタは、コントローラアクションの認証と承認を実装するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="36f8c-147">たとえば、承認フィルターは承認フィルターの例です。</span><span class="sxs-lookup"><span data-stu-id="36f8c-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="36f8c-148">アクション フィルターには、コントローラー アクションの実行前後に実行されるロジックが含まれます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="36f8c-149">たとえば、アクション フィルターを使用して、コントローラー アクションが返すビュー データを変更できます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="36f8c-150">結果フィルターには、ビュー結果の実行前後に実行されるロジックが含まれます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="36f8c-151">たとえば、ビューがブラウザにレンダリングされる直前にビューの結果を変更する場合があります。</span><span class="sxs-lookup"><span data-stu-id="36f8c-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="36f8c-152">例外フィルターは、最後に実行するフィルターの種類です。</span><span class="sxs-lookup"><span data-stu-id="36f8c-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="36f8c-153">例外フィルターを使用して、コントローラーアクションまたはコントローラーアクションの結果によって発生したエラーを処理できます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="36f8c-154">例外フィルターを使用してエラーをログに記録することもできます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="36f8c-155">フィルタの種類ごとに、特定の順序で実行されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="36f8c-156">同じ種類のフィルターを実行する順序を制御する場合は、フィルターの Order プロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="36f8c-157">すべてのアクション フィルターの基本クラスは`System.Web.Mvc.FilterAttribute`クラスです。</span><span class="sxs-lookup"><span data-stu-id="36f8c-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="36f8c-158">特定の種類のフィルタを実装する場合は、基本 Filter クラスから`IAuthorizationFilter`継承し、 `IActionFilter`、 、 、`IResultFilter`または`IExceptionFilter`インターフェイスの 1 つ以上を実装するクラスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="36f8c-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, or `IExceptionFilter` interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="36f8c-159">基本アクションフィルター属性クラス</span><span class="sxs-lookup"><span data-stu-id="36f8c-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="36f8c-160">カスタム アクション フィルターを簡単に実装できるようにするために、ASP.NET MVC フレームワークには基本`ActionFilterAttribute`クラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="36f8c-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="36f8c-161">このクラスは、 および`IActionFilter``IResultFilter`インターフェイスの両方を実装し`Filter`、クラスから継承します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="36f8c-162">ここでの用語は完全に一貫していません。</span><span class="sxs-lookup"><span data-stu-id="36f8c-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="36f8c-163">技術的には、ActionFilterAttribute クラスから継承するクラスは、アクション フィルターと結果フィルターの両方です。</span><span class="sxs-lookup"><span data-stu-id="36f8c-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="36f8c-164">しかし、緩い意味では、単語アクションフィルターは、ASP.NETMVCフレームワーク内の任意の種類のフィルターを参照するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="36f8c-165">基本`ActionFilterAttribute`クラスには、オーバーライドできる次のメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="36f8c-165">The base `ActionFilterAttribute` class has the following methods that you can override:</span></span>

- <span data-ttu-id="36f8c-166">OnActionExecuting – このメソッドは、コントローラー アクションが実行される前に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="36f8c-167">OnActionExecuted – このメソッドは、コント ローラー アクションが実行された後に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="36f8c-168">OnResultExecuting – このメソッドは、コントローラーアクションの結果が実行される前に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="36f8c-169">OnResultExecuted – このメソッドは、コント ローラー アクションの結果が実行された後に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="36f8c-170">次のセクションでは、これらの各メソッドを実装する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="36f8c-171">ログ アクション フィルタの作成</span><span class="sxs-lookup"><span data-stu-id="36f8c-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="36f8c-172">カスタム アクション フィルターを作成する方法を説明するために、コントローラー アクションの処理のステージを Visual Studio の [出力] ウィンドウに記録するカスタム アクション フィルターを作成します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="36f8c-173">リスト`LogActionFilter`2に含まれています。</span><span class="sxs-lookup"><span data-stu-id="36f8c-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="36f8c-174">**リスト2 –`ActionFilters\LogActionFilter.cs`**</span><span class="sxs-lookup"><span data-stu-id="36f8c-174">**Listing 2 – `ActionFilters\LogActionFilter.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

<span data-ttu-id="36f8c-175">リスト 2 では`OnActionExecuting()`、 `OnActionExecuted()` `OnResultExecuting()`、 `OnResultExecuted()` 、および メソッド`Log()`はすべてメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="36f8c-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="36f8c-176">メソッドの名前と現在のルート データがメソッドに`Log()`渡されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="36f8c-177">この`Log()`メソッドは、Visual Studio の出力ウィンドウにメッセージを書き込みます (図 2 参照)。</span><span class="sxs-lookup"><span data-stu-id="36f8c-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>

<span data-ttu-id="36f8c-178">[![[Visual Studio の出力] ウィンドウへの書き込み](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="36f8c-178">[![Writing to the Visual Studio Output window](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span></span>

<span data-ttu-id="36f8c-179">**図 02**: Visual Studio の出力ウィンドウへの書き込み ([フルサイズの画像を表示する をクリック](understanding-action-filters-cs/_static/image6.png)します )</span><span class="sxs-lookup"><span data-stu-id="36f8c-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-cs/_static/image6.png))</span></span>

<span data-ttu-id="36f8c-180">リスト 3 のホーム コントローラーは、Log アクション フィルターをコントローラー クラス全体に適用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="36f8c-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="36f8c-181">ホーム コントローラーによって公開されるアクションのいずれかが呼び出されるたびに (`Index()`メソッドまたは`About()`メソッドのいずれか)、アクションの処理のステージが Visual Studio の出力ウィンドウに記録されます。</span><span class="sxs-lookup"><span data-stu-id="36f8c-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="36f8c-182">**リスト3 –`Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="36f8c-182">**Listing 3 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a><span data-ttu-id="36f8c-183">まとめ</span><span class="sxs-lookup"><span data-stu-id="36f8c-183">Summary</span></span>

<span data-ttu-id="36f8c-184">このチュートリアルでは、MVC アクション フィルターのASP.NETについて説明しました。</span><span class="sxs-lookup"><span data-stu-id="36f8c-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="36f8c-185">4 種類のフィルターについて学習しました: 承認フィルター、アクション フィルター、結果フィルター、例外フィルター。</span><span class="sxs-lookup"><span data-stu-id="36f8c-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="36f8c-186">また、基本`ActionFilterAttribute`クラスについても学習しました。</span><span class="sxs-lookup"><span data-stu-id="36f8c-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="36f8c-187">最後に、単純なアクション フィルターを実装する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="36f8c-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="36f8c-188">コントローラー アクションの処理のステージをログに記録するログ アクション フィルターを作成、 Visual Studio の出力ウィンドウ。</span><span class="sxs-lookup"><span data-stu-id="36f8c-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="36f8c-189">[前へ](asp-net-mvc-routing-overview-cs.md)
> [次へ](improving-performance-with-output-caching-cs.md)</span><span class="sxs-lookup"><span data-stu-id="36f8c-189">[Previous](asp-net-mvc-routing-overview-cs.md)
[Next](improving-performance-with-output-caching-cs.md)</span></span>
