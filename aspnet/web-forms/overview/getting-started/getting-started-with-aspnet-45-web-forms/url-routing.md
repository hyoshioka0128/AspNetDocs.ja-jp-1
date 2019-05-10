---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL ルーティング |Microsoft Docs
author: Erikre
description: このチュートリアル シリーズでは、私たちの ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォーム アプリケーションの構築の基礎を説明しています.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: f8a374be79a41b34dc8f17fa8d44c6e0680984d7
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65108624"
---
# <a name="url-routing"></a><span data-ttu-id="34540-103">URL ルーティング</span><span class="sxs-lookup"><span data-stu-id="34540-103">URL Routing</span></span>

<span data-ttu-id="34540-104">によって[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="34540-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="34540-105">[Wingtip Toys のサンプル プロジェクト (C#) をダウンロード](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)または[電子書籍 (PDF) をダウンロード](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="34540-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="34540-106">このチュートリアル シリーズでは、Web 用 ASP.NET 4.5 と Microsoft Visual Studio Express 2013 を使用して ASP.NET Web フォーム アプリケーションの構築の基礎を説明します。</span><span class="sxs-lookup"><span data-stu-id="34540-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="34540-107">Visual Studio 2013[プロジェクトと C# ソース コード](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)このチュートリアル シリーズをと共に使用できます。</span><span class="sxs-lookup"><span data-stu-id="34540-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="34540-108">このチュートリアルでは、URL ルーティングをサポートするために、Wingtip Toys のサンプル アプリケーションを変更します。</span><span class="sxs-lookup"><span data-stu-id="34540-108">In this tutorial, you will modify the Wingtip Toys sample application to support URL routing.</span></span> <span data-ttu-id="34540-109">ルーティングは、検索エンジンによってサポートされているより、覚えやすくわかりやすい Url を使用する web アプリケーションを使用します。</span><span class="sxs-lookup"><span data-stu-id="34540-109">Routing enables your web application to use URLs that are friendly, easier to remember, and better supported by search engines.</span></span> <span data-ttu-id="34540-110">このチュートリアルでは、「メンバーシップと管理」の前のチュートリアルに基づいており、Wingtip Toys のチュートリアル シリーズのパートです。</span><span class="sxs-lookup"><span data-stu-id="34540-110">This tutorial builds on the previous tutorial "Membership and Administration" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="34540-111">学習内容。</span><span class="sxs-lookup"><span data-stu-id="34540-111">What you'll learn:</span></span>

- <span data-ttu-id="34540-112">ASP.NET Web フォーム アプリケーション用のルートを登録する方法。</span><span class="sxs-lookup"><span data-stu-id="34540-112">How to register routes for an ASP.NET Web Forms application.</span></span>
- <span data-ttu-id="34540-113">Web ページにルートを追加する方法。</span><span class="sxs-lookup"><span data-stu-id="34540-113">How to add routes to a web page.</span></span>
- <span data-ttu-id="34540-114">ルートをサポートするために、データベースからデータを選択する方法。</span><span class="sxs-lookup"><span data-stu-id="34540-114">How to select data from a database to support routes.</span></span>

## <a name="aspnet-routing-overview"></a><span data-ttu-id="34540-115">ASP.NET ルーティングの概要</span><span class="sxs-lookup"><span data-stu-id="34540-115">ASP.NET Routing Overview</span></span>

<span data-ttu-id="34540-116">URL ルーティングを使用すると、そのまま使用するアプリケーションを構成する物理ファイルにマップされていない Url を要求します。</span><span class="sxs-lookup"><span data-stu-id="34540-116">URL routing allows you to configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="34540-117">要求 URL は、ユーザーが web サイトのページの検索に、ブラウザーに入力 URL だけです。</span><span class="sxs-lookup"><span data-stu-id="34540-117">A request URL is simply the URL a user enters into their browser to find a page on your web site.</span></span> <span data-ttu-id="34540-118">ルーティングを使用して、検索エンジン最適化 (SEO) に役立つことができ、意味的意味のあるユーザーになっている Url を定義します。</span><span class="sxs-lookup"><span data-stu-id="34540-118">You use routing to define URLs that are semantically meaningful to users and that can help with search-engine optimization (SEO).</span></span>

<span data-ttu-id="34540-119">既定では、Web フォーム テンプレートが含まれます[ASP.NET Friendly Url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)します。</span><span class="sxs-lookup"><span data-stu-id="34540-119">By default, the Web Forms template includes [ASP.NET Friendly URLs](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/).</span></span> <span data-ttu-id="34540-120">基本的なルーティング作業の多くを使用して実装*フレンドリな Url*します。</span><span class="sxs-lookup"><span data-stu-id="34540-120">Much of the basic routing work will be implemented by using *Friendly URLs*.</span></span> <span data-ttu-id="34540-121">ただし、このチュートリアルでは、カスタマイズされたルーティング機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="34540-121">However, in this tutorial you will add customized routing capabilities.</span></span>

<span data-ttu-id="34540-122">URL ルーティングをカスタマイズする前に、Wingtip Toys のサンプル アプリケーションは、次の URL を使用して製品にリンクできます。</span><span class="sxs-lookup"><span data-stu-id="34540-122">Before customizing URL routing, the Wingtip Toys sample application can link to a product using the following URL:</span></span>

`https://localhost:44300/ProductDetails.aspx?productID=2`

<span data-ttu-id="34540-123">URL ルーティングをカスタマイズするには、Wingtip Toys のサンプル アプリケーションに URL を読みやすいを使用して、同じ製品にリンクされます。</span><span class="sxs-lookup"><span data-stu-id="34540-123">By customizing URL routing, the Wingtip Toys sample application will link to the same product using an easier to read URL:</span></span>

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a><span data-ttu-id="34540-124">ルート</span><span class="sxs-lookup"><span data-stu-id="34540-124">Routes</span></span>

<span data-ttu-id="34540-125">ルートは、ハンドラーにマップされている URL パターンです。</span><span class="sxs-lookup"><span data-stu-id="34540-125">A route is a URL pattern that is mapped to a handler.</span></span> <span data-ttu-id="34540-126">ハンドラーは、Web フォーム アプリケーションで .aspx ファイルなどの物理ファイルを指定できます。</span><span class="sxs-lookup"><span data-stu-id="34540-126">The handler can be a physical file, such as an .aspx file in a Web Forms application.</span></span> <span data-ttu-id="34540-127">ハンドラーは、要求を処理するクラスもできます。</span><span class="sxs-lookup"><span data-stu-id="34540-127">A handler can also be a class that processes the request.</span></span> <span data-ttu-id="34540-128">ルートを定義するには、URL パターン、ハンドラー、および必要に応じて、ルートの名前を指定することで、ルート クラスのインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="34540-128">To define a route, you create an instance of the Route class by specifying the URL pattern, the handler, and optionally a name for the route.</span></span>

<span data-ttu-id="34540-129">アプリケーションに追加することで、ルートを追加する、`Route`オブジェクトを静的な`Routes`のプロパティ、`RouteTable`クラス。</span><span class="sxs-lookup"><span data-stu-id="34540-129">You add the route to the application by adding the `Route` object to the static `Routes` property of the `RouteTable` class.</span></span> <span data-ttu-id="34540-130">ルートのプロパティは、`RouteCollection`アプリケーションのすべてのルートを格納するオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="34540-130">The Routes property is a `RouteCollection` object that stores all the routes for the application.</span></span>

### <a name="url-patterns"></a><span data-ttu-id="34540-131">URL パターン</span><span class="sxs-lookup"><span data-stu-id="34540-131">URL Patterns</span></span>

<span data-ttu-id="34540-132">URL パターンは、リテラル値と変数のプレース ホルダー (URL パラメーターと呼ばれます) に含めることができます。</span><span class="sxs-lookup"><span data-stu-id="34540-132">A URL pattern can contain literal values and variable placeholders (referred to as URL parameters).</span></span> <span data-ttu-id="34540-133">リテラルとプレース ホルダーは、スラッシュで区切られた URL のセグメントである (`/`) 文字。</span><span class="sxs-lookup"><span data-stu-id="34540-133">The literals and placeholders are located in segments of the URL which are delimited by the slash (`/`) character.</span></span>

<span data-ttu-id="34540-134">Web アプリケーションへの要求が行われたときに、URL はセグメントとプレース ホルダーに解析され、変数の値が、要求ハンドラーを提供します。</span><span class="sxs-lookup"><span data-stu-id="34540-134">When a request to your web application is made, the URL is parsed into segments and placeholders, and the variable values are provided to the request handler.</span></span> <span data-ttu-id="34540-135">このプロセスは、クエリ文字列内のデータを解析および要求ハンドラーに渡される方法に似ています。</span><span class="sxs-lookup"><span data-stu-id="34540-135">This process is similar to the way the data in a query string is parsed and passed to the request handler.</span></span> <span data-ttu-id="34540-136">どちらの場合も、変数の情報は、URL に含まれ、キー/値ペアの形式でハンドラーに渡されます。</span><span class="sxs-lookup"><span data-stu-id="34540-136">In both cases, variable information is included in the URL and passed to the handler in the form of key-value pairs.</span></span> <span data-ttu-id="34540-137">クエリ文字列の場合、キーと値の両方が、URL には。</span><span class="sxs-lookup"><span data-stu-id="34540-137">For query strings, both the keys and the values are in the URL.</span></span> <span data-ttu-id="34540-138">ルートの場合、キーは、URL パターンで定義されているプレース ホルダー名と値のみが url に含めています。</span><span class="sxs-lookup"><span data-stu-id="34540-138">For routes, the keys are the placeholder names defined in the URL pattern, and only the values are in the URL.</span></span>

<span data-ttu-id="34540-139">URL パターンは、中かっこで囲み、プレース ホルダーを定義する (`{`と`}`)。</span><span class="sxs-lookup"><span data-stu-id="34540-139">In a URL pattern, you define placeholders by enclosing them in braces ( `{` and `}` ).</span></span> <span data-ttu-id="34540-140">セグメントで 1 つ以上のプレース ホルダーを定義できますが、プレース ホルダーをリテラル値で区切る必要があります。</span><span class="sxs-lookup"><span data-stu-id="34540-140">You can define more than one placeholder in a segment, but the placeholders must be separated by a literal value.</span></span> <span data-ttu-id="34540-141">たとえば、`{language}-{country}/{action}`は有効なルート パターンです。</span><span class="sxs-lookup"><span data-stu-id="34540-141">For example, `{language}-{country}/{action}` is a valid route pattern.</span></span> <span data-ttu-id="34540-142">ただし、`{language}{country}/{action}`リテラル値またはプレース ホルダーの間の区切り記号がないために、有効なパターンではありません。</span><span class="sxs-lookup"><span data-stu-id="34540-142">However, `{language}{country}/{action}` is not a valid pattern, because there is no literal value or delimiter between the placeholders.</span></span> <span data-ttu-id="34540-143">そのため、ルーティングと、国のプレース ホルダーの値からの言語のプレース ホルダーの値を分離する場所が決定することはできません。</span><span class="sxs-lookup"><span data-stu-id="34540-143">Therefore, routing cannot determine where to separate the value for the language placeholder from the value for the country placeholder.</span></span>

### <a name="mapping-and-registering-routes"></a><span data-ttu-id="34540-144">マッピングとルートを登録します。</span><span class="sxs-lookup"><span data-stu-id="34540-144">Mapping and Registering Routes</span></span>

<span data-ttu-id="34540-145">Wingtip Toys のサンプル アプリケーションのページへのルートを含めることができます、前に、アプリケーションの起動時に、ルートを登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34540-145">Before you can include routes to pages of the Wingtip Toys sample application, you must register the routes when the application starts.</span></span> <span data-ttu-id="34540-146">ルートを登録するには、変更、`Application_Start`イベント ハンドラー。</span><span class="sxs-lookup"><span data-stu-id="34540-146">To register the routes, you will modify the `Application_Start` event handler.</span></span>

1. <span data-ttu-id="34540-147">**ソリューション エクスプ ローラー**、Visual Studio の検索して開く、 *Global.asax.cs*ファイル。</span><span class="sxs-lookup"><span data-stu-id="34540-147">In **Solution Explorer**of Visual Studio, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="34540-148">黄色で強調表示されているコードを追加、 *Global.asax.cs*ファイルの次のようにします。</span><span class="sxs-lookup"><span data-stu-id="34540-148">Add the code highlighted in yellow to the *Global.asax.cs* file as follows:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

<span data-ttu-id="34540-149">Wingtip Toys のサンプル アプリケーションの起動時、ときに呼び出す、`Application_Start`イベント ハンドラー。</span><span class="sxs-lookup"><span data-stu-id="34540-149">When the Wingtip Toys sample application starts, it calls the `Application_Start` event handler.</span></span> <span data-ttu-id="34540-150">このイベント ハンドラーの最後に、`RegisterCustomRoutes`メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="34540-150">At the end of this event handler, the `RegisterCustomRoutes` method is called.</span></span> <span data-ttu-id="34540-151">`RegisterCustomRoutes`メソッドを呼び出して各ルートを追加する、`MapPageRoute`のメソッド、`RouteCollection`オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="34540-151">The `RegisterCustomRoutes` method adds each route by calling the `MapPageRoute` method of the `RouteCollection` object.</span></span> <span data-ttu-id="34540-152">ルートを定義するには、ルート URL と物理的な URL とルート名を使用します。</span><span class="sxs-lookup"><span data-stu-id="34540-152">Routes are defined using a route name, a route URL and a physical URL.</span></span>

<span data-ttu-id="34540-153">最初のパラメーター ("`ProductsByCategoryRoute`") は、ルートの名前です。</span><span class="sxs-lookup"><span data-stu-id="34540-153">The first parameter ("`ProductsByCategoryRoute`") is the route name.</span></span> <span data-ttu-id="34540-154">ルートを呼び出す必要がある場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="34540-154">It is used to call the route when it is needed.</span></span> <span data-ttu-id="34540-155">2 番目のパラメーター ("`Category/{categoryName}`") フレンドリ交換コードに基づいて動的なことができる URL を定義します。</span><span class="sxs-lookup"><span data-stu-id="34540-155">The second parameter ("`Category/{categoryName}`") defines the friendly replacement URL that can be dynamic based on code.</span></span> <span data-ttu-id="34540-156">生成されるデータに基づいたリンクを使用して、データ コントロールを作成する場合は、このルートを使用します。</span><span class="sxs-lookup"><span data-stu-id="34540-156">You use this route when you are populating a data control with links that are generated based on data.</span></span> <span data-ttu-id="34540-157">ルートが表示されます。</span><span class="sxs-lookup"><span data-stu-id="34540-157">A route is shown as follows:</span></span>

[!code-csharp[Main](url-routing/samples/sample2.cs)]

<span data-ttu-id="34540-158">ルートの 2 番目のパラメーターには、中かっこで指定された、動的な値が含まれています (`{ }`)。</span><span class="sxs-lookup"><span data-stu-id="34540-158">The second parameter of the route includes a dynamic value specified by braces (`{ }`).</span></span> <span data-ttu-id="34540-159">ここで、`categoryName`は適切なルーティング パスを決定するために使用する変数です。</span><span class="sxs-lookup"><span data-stu-id="34540-159">In this case, the `categoryName` is a variable that will be used to determine the proper routing path.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="34540-160">**Optional**</span><span class="sxs-lookup"><span data-stu-id="34540-160">**Optional**</span></span>
> 
> <span data-ttu-id="34540-161">移動することによって、コードを管理しやすい検索可能性があります、`RegisterCustomRoutes`メソッドを別のクラスにします。</span><span class="sxs-lookup"><span data-stu-id="34540-161">You might find it easier to manage your code by moving the `RegisterCustomRoutes` method to a separate class.</span></span> <span data-ttu-id="34540-162">*ロジック*フォルダーを個別に作成`RouteActions`クラス。</span><span class="sxs-lookup"><span data-stu-id="34540-162">In the *Logic* folder, create a separate `RouteActions` class.</span></span> <span data-ttu-id="34540-163">上移動`RegisterCustomRoutes`からメソッド、 *Global.asax.cs*ファイルを新しい`RoutesActions`クラス。</span><span class="sxs-lookup"><span data-stu-id="34540-163">Move the above `RegisterCustomRoutes` method from the *Global.asax.cs* file into the new `RoutesActions` class.</span></span> <span data-ttu-id="34540-164">使用して、`RoleActions`クラスおよび`createAdmin`メソッドを呼び出す方法の例として、`RegisterCustomRoutes`からメソッド、 *Global.asax.cs*ファイル。</span><span class="sxs-lookup"><span data-stu-id="34540-164">Use the `RoleActions` class and the `createAdmin` method as an example of how to call the `RegisterCustomRoutes` method from the *Global.asax.cs* file.</span></span>

<span data-ttu-id="34540-165">お気付きかもしれません、`RegisterRoutes`メソッドの呼び出しを使用して、`RouteConfig`の先頭にあるオブジェクト、`Application_Start`イベント ハンドラー。</span><span class="sxs-lookup"><span data-stu-id="34540-165">You may also have noticed the `RegisterRoutes` method call using the `RouteConfig` object at the beginning of the `Application_Start` event handler.</span></span> <span data-ttu-id="34540-166">この呼び出しは、既定のルーティングを実装するために行われます。</span><span class="sxs-lookup"><span data-stu-id="34540-166">This call is made to implement default routing.</span></span> <span data-ttu-id="34540-167">Visual Studio の Web フォーム テンプレートを使用してアプリケーションを作成したときに既定のコードとしては含まれています。</span><span class="sxs-lookup"><span data-stu-id="34540-167">It was included as default code when you created the application using Visual Studio's Web Forms template.</span></span>

## <a name="retrieving-and-using-route-data"></a><span data-ttu-id="34540-168">取得して、ルート データを使用します。</span><span class="sxs-lookup"><span data-stu-id="34540-168">Retrieving and Using Route Data</span></span>

<span data-ttu-id="34540-169">前述のように、ルートを定義することができます。</span><span class="sxs-lookup"><span data-stu-id="34540-169">As mentioned above, routes can be defined.</span></span> <span data-ttu-id="34540-170">追加したコード、`Application_Start`内のイベント ハンドラー、 *Global.asax.cs*ファイルが定義可能なルートを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="34540-170">The code that you added to the `Application_Start` event handler in the *Global.asax.cs* file loads the definable routes.</span></span>

### <a name="setting-routes"></a><span data-ttu-id="34540-171">ルートの設定</span><span class="sxs-lookup"><span data-stu-id="34540-171">Setting Routes</span></span>

<span data-ttu-id="34540-172">ルートでは、追加のコードを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34540-172">Routes require you to add additional code.</span></span> <span data-ttu-id="34540-173">このチュートリアルでは、取得するモデル バインドを使用します、`RouteValueDictionary`データ コントロールからのデータを使用してルートを生成するときに使用されるオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="34540-173">In this tutorial, you will use model binding to retrieve a `RouteValueDictionary` object that is used when generating the routes using data from a data control.</span></span> <span data-ttu-id="34540-174">`RouteValueDictionary`オブジェクトは、特定の製品カテゴリに属する製品名の一覧が格納されます。</span><span class="sxs-lookup"><span data-stu-id="34540-174">The `RouteValueDictionary` object will contain a list of product names that belong to a specific category of products.</span></span> <span data-ttu-id="34540-175">データとルートに基づいて、各製品のリンクが作成されます。</span><span class="sxs-lookup"><span data-stu-id="34540-175">A link is created for each product based on the data and route.</span></span>

#### <a name="enable-routes-for-categories-and-products"></a><span data-ttu-id="34540-176">カテゴリと製品のルートを有効にします。</span><span class="sxs-lookup"><span data-stu-id="34540-176">Enable Routes for Categories and Products</span></span>

<span data-ttu-id="34540-177">次に、使用するアプリケーションを更新、`ProductsByCategoryRoute`各製品カテゴリのリンクを含めることが適切なルートを決定します。</span><span class="sxs-lookup"><span data-stu-id="34540-177">Next, you'll update the application to use the `ProductsByCategoryRoute` to determine the correct route to include for each product category link.</span></span> <span data-ttu-id="34540-178">更新しても、 *ProductList.aspx*ページに各製品のルーティング リンクが含まれます。</span><span class="sxs-lookup"><span data-stu-id="34540-178">You'll also update the *ProductList.aspx* page to include a routed link for each product.</span></span> <span data-ttu-id="34540-179">リンクが表示されます、変更前に、と同様に、リンクは URL ルーティングを使用してようになりました。</span><span class="sxs-lookup"><span data-stu-id="34540-179">The links will be displayed as they were before the change, however the links will now use URL routing.</span></span>

1. <span data-ttu-id="34540-180">**ソリューション エクスプ ローラー**、オープン、 *Site.Master*ページがまだ開いていない場合。</span><span class="sxs-lookup"><span data-stu-id="34540-180">In **Solution Explorer**, open the *Site.Master* page if it is not already open.</span></span>
2. <span data-ttu-id="34540-181">更新プログラム、 **ListView**という名前のコントロール"`categoryList`"黄色で強調表示の変更により、そのため、マークアップように表示されます。</span><span class="sxs-lookup"><span data-stu-id="34540-181">Update the **ListView** control named "`categoryList`" with the changes highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. <span data-ttu-id="34540-182">**ソリューション エクスプ ローラー**、オープン、 *ProductList.aspx*ページ。</span><span class="sxs-lookup"><span data-stu-id="34540-182">In **Solution Explorer**, open the *ProductList.aspx* page.</span></span>
4. <span data-ttu-id="34540-183">更新プログラム、`ItemTemplate`の要素、 *ProductList.aspx*ページ マークアップが次のように表示されるように、黄色で強調表示されている更新プログラムを使用します。</span><span class="sxs-lookup"><span data-stu-id="34540-183">Update the `ItemTemplate` element of the *ProductList.aspx* page with the updates highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. <span data-ttu-id="34540-184">分離コードを開く*ProductList.aspx.cs*黄色で強調表示されている次の名前空間を追加します。</span><span class="sxs-lookup"><span data-stu-id="34540-184">Open the code-behind of *ProductList.aspx.cs* and add the following namespace as highlighted in yellow:</span></span>  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. <span data-ttu-id="34540-185">置換、`GetProducts`分離コードのメソッド (*ProductList.aspx.cs*) を次のコード。</span><span class="sxs-lookup"><span data-stu-id="34540-185">Replace the `GetProducts` method of the code-behind (*ProductList.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a><span data-ttu-id="34540-186">製品の詳細のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="34540-186">Add Code for Product Details</span></span>

<span data-ttu-id="34540-187">ここでは、分離コードを更新 (*ProductDetails.aspx.cs*) の*ProductDetails.aspx*ルート データを使用するページ。</span><span class="sxs-lookup"><span data-stu-id="34540-187">Now, update the code-behind (*ProductDetails.aspx.cs*) for the *ProductDetails.aspx* page to use route data.</span></span> <span data-ttu-id="34540-188">注意して、新しい`GetProduct`メソッドもユーザーがブックマーク リンク、古い非対応でないルーティングの URL を使用してケースのクエリ文字列値を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="34540-188">Notice that the new `GetProduct` method also accepts a query string value for the case where the user has a link bookmarked that uses the older non-friendly, non-routed URL.</span></span>

1. <span data-ttu-id="34540-189">置換、`GetProduct`分離コードのメソッド (*ProductDetails.aspx.cs*) を次のコード。</span><span class="sxs-lookup"><span data-stu-id="34540-189">Replace the `GetProduct` method of the code-behind (*ProductDetails.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a><span data-ttu-id="34540-190">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="34540-190">Running the Application</span></span>

<span data-ttu-id="34540-191">更新されたルートを表示するようになりましたアプリケーションを実行することができます。</span><span class="sxs-lookup"><span data-stu-id="34540-191">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="34540-192">キーを押して**F5** Wingtip Toys のサンプル アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="34540-192">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="34540-193">ブラウザーが開きを示しています、 *Default.aspx*ページ。</span><span class="sxs-lookup"><span data-stu-id="34540-193">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="34540-194">をクリックして、**製品**ページの上部にあるリンクです。</span><span class="sxs-lookup"><span data-stu-id="34540-194">Click the **Products** link at the top of the page.</span></span>  
 <span data-ttu-id="34540-195">すべての製品が表示されます、 *ProductList.aspx*ページ。</span><span class="sxs-lookup"><span data-stu-id="34540-195">All products are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="34540-196">(実際のポート番号を使用して) 次の URL がブラウザーの表示されます。</span><span class="sxs-lookup"><span data-stu-id="34540-196">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/ProductList`
3. <span data-ttu-id="34540-197">次に、クリックして、**自動車**ページの上部にあるカテゴリのリンク。</span><span class="sxs-lookup"><span data-stu-id="34540-197">Next, click the **Cars** category link near the top of the page.</span></span>  
 <span data-ttu-id="34540-198">Cars のみが表示されます、 *ProductList.aspx*ページ。</span><span class="sxs-lookup"><span data-stu-id="34540-198">Only cars are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="34540-199">(実際のポート番号を使用して) 次の URL がブラウザーの表示されます。</span><span class="sxs-lookup"><span data-stu-id="34540-199">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Category/Cars`
4. <span data-ttu-id="34540-200">最初の自動車の名前を含むリンクは、ページに表示 をクリックします ("**変換可能な自動車**")、製品の詳細を表示します。</span><span class="sxs-lookup"><span data-stu-id="34540-200">Click the link containing the name of the first car listed on the page ("**Convertible Car**") to display the product details.</span></span>  
 <span data-ttu-id="34540-201">(実際のポート番号を使用して) 次の URL がブラウザーの表示されます。</span><span class="sxs-lookup"><span data-stu-id="34540-201">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Product/Convertible%20Car`
5. <span data-ttu-id="34540-202">次に、ブラウザーに (実際のポート番号を使用して) 次の非ルーティング URL を入力します。</span><span class="sxs-lookup"><span data-stu-id="34540-202">Next, enter the following non-routed URL (using your port number) into the browser:</span></span>  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 <span data-ttu-id="34540-203">コードでは、ユーザーがブックマーク リンクを持つケースのクエリ文字列を含む URL は認識します。</span><span class="sxs-lookup"><span data-stu-id="34540-203">The code still recognizes a URL that includes a query string, for the case where a user has a link bookmarked.</span></span>

## <a name="summary"></a><span data-ttu-id="34540-204">まとめ</span><span class="sxs-lookup"><span data-stu-id="34540-204">Summary</span></span>

<span data-ttu-id="34540-205">このチュートリアルでは、カテゴリおよび製品用のルートを追加しました。</span><span class="sxs-lookup"><span data-stu-id="34540-205">In this tutorial, you have added routes for categories and products.</span></span> <span data-ttu-id="34540-206">モデル バインディングを使用するデータ コントロールとルートを統合する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="34540-206">You have learned how routes can be integrated with data controls that use model binding.</span></span> <span data-ttu-id="34540-207">次のチュートリアルでは、グローバル エラー処理を実装します。</span><span class="sxs-lookup"><span data-stu-id="34540-207">In the next tutorial, you will implement global error handling.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34540-208">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="34540-208">Additional Resources</span></span>

[<span data-ttu-id="34540-209">ASP.NET Friendly Url</span><span class="sxs-lookup"><span data-stu-id="34540-209">ASP.NET Friendly URLs</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[<span data-ttu-id="34540-210">Azure App Service へのメンバーシップ、OAuth、SQL Database を使用したセキュリティで保護された ASP.NET Web フォーム アプリをデプロイします。</span><span class="sxs-lookup"><span data-stu-id="34540-210">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="34540-211">Microsoft Azure の無料試用版</span><span class="sxs-lookup"><span data-stu-id="34540-211">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> <span data-ttu-id="34540-212">[前へ](membership-and-administration.md)
> [次へ](aspnet-error-handling.md)</span><span class="sxs-lookup"><span data-stu-id="34540-212">[Previous](membership-and-administration.md)
[Next](aspnet-error-handling.md)</span></span>
