---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: コントローラとビューを使用してリスト/詳細 UI を実装する |マイクロソフトドキュメント
author: rick-anderson
description: 手順 4 では、モデルを利用してユーザーにデータの一覧/詳細ナビゲーション エクスペリエンスを提供するコントローラーをアプリケーションに追加する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 49c7dc977477a4edbfcfc68b166ae7ea3fa22f2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541313"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a><span data-ttu-id="b3ecd-103">コントローラーとビューを使用し、リスティング/詳細 UI を実装する</span><span class="sxs-lookup"><span data-stu-id="b3ecd-103">Use Controllers and Views to Implement a Listing/Details UI</span></span>

<span data-ttu-id="b3ecd-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b3ecd-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="b3ecd-105">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="b3ecd-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="b3ecd-106">これは、mvc 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NETの手順 4 です。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-106">This is step 4 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="b3ecd-107">手順 4 では、NerdDinner サイトでディナーのデータ一覧/詳細ナビゲーション エクスペリエンスをユーザーに提供するために、モデルを利用するアプリケーションに Controller を追加する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-107">Step 4 shows how to add a Controller to the application that takes advantage of our model to provide users with a data listing/details navigation experience for dinners on our NerdDinner site.</span></span>
> 
> <span data-ttu-id="b3ecd-108">mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-4-controllers-and-views"></a><span data-ttu-id="b3ecd-109">NerdDinner ステップ 4: コントローラーとビュー</span><span class="sxs-lookup"><span data-stu-id="b3ecd-109">NerdDinner Step 4: Controllers and Views</span></span>

<span data-ttu-id="b3ecd-110">従来の Web フレームワーク (従来の ASP、PHP、ASP.NET Web フォームなど) では、通常、受信 URL はディスク上のファイルにマップされます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-110">With traditional web frameworks (classic ASP, PHP, ASP.NET Web Forms, etc), incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="b3ecd-111">たとえば、"/Products.aspx" や "/Products.php" などの URL の要求は、"Products.aspx" または "Products.php" ファイルで処理される場合があります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="b3ecd-112">Web ベースの MVC フレームワークは、URL をサーバー コードに対して少し異なる方法でマップします。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="b3ecd-113">受信 URL をファイルにマップする代わりに、URL をクラスのメソッドにマップします。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="b3ecd-114">これらのクラスは「コントローラ」と呼ばれ、着信 HTTP 要求の処理、ユーザー入力の処理、データの取得と保存、クライアントに返送する応答の決定 (HTML の表示、ファイルのダウンロード、別の URL へのリダイレクトなど) を担当します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc).</span></span>

<span data-ttu-id="b3ecd-115">NerdDinnerアプリケーションの基本モデルを構築したので、次のステップは、それを利用して、私たちのサイト上のDinnersのデータリスト/詳細ナビゲーション体験をユーザーに提供するアプリケーションにコントローラを追加することです。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-115">Now that we have built up a basic model for our NerdDinner application, our next step will be to add a Controller to the application that takes advantage of it to provide users with a data listing/details navigation experience for Dinners on our site.</span></span>

### <a name="adding-a-dinnerscontroller-controller"></a><span data-ttu-id="b3ecd-116">ディナーコントローラコントローラの追加</span><span class="sxs-lookup"><span data-stu-id="b3ecd-116">Adding a DinnersController Controller</span></span>

<span data-ttu-id="b3ecd-117">まず、Web プロジェクト内の "コントローラー" フォルダーを右クリックし、**コント&gt;ローラー**メニューコマンドを選択します (Ctrl-M、Ctrl-C を入力してこのコマンドを実行することもできます)。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-117">We'll begin by right-clicking on the "Controllers" folder within our web project, and then select the **Add-&gt;Controller** menu command (you can also execute this command by typing Ctrl-M, Ctrl-C):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

<span data-ttu-id="b3ecd-118">これにより、「コントローラの追加」ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-118">This will bring up the "Add Controller" dialog:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

<span data-ttu-id="b3ecd-119">新しいコントローラに「DinnersController」という名前を付け、[追加]ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-119">We'll name the new controller "DinnersController" and click the "Add" button.</span></span> <span data-ttu-id="b3ecd-120">次に、\Controllers ディレクトリの下にDinnersController.csファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-120">Visual Studio will then add a DinnersController.cs file under our \Controllers directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

<span data-ttu-id="b3ecd-121">また、コード エディター内で新しい DinnersController クラスを開きます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-121">It will also open up the new DinnersController class within the code-editor.</span></span>

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a><span data-ttu-id="b3ecd-122">DinnersController クラスへの Index() および Details() アクションメソッドの追加</span><span class="sxs-lookup"><span data-stu-id="b3ecd-122">Adding Index() and Details() Action Methods to the DinnersController Class</span></span>

<span data-ttu-id="b3ecd-123">私たちは、今後のディナーのリストを閲覧するために私たちのアプリケーションを使用して訪問者を有効にし、彼らはそれについての具体的な詳細を見るためにリスト内の任意のディナーをクリックできるようにしたいと考えています。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-123">We want to enable visitors using our application to browse a list of upcoming dinners, and allow them to click on any Dinner in the list to see specific details about it.</span></span> <span data-ttu-id="b3ecd-124">これを行うには、アプリケーションから次の URL を公開します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-124">We'll do this by publishing the following URLs from our application:</span></span>

| <span data-ttu-id="b3ecd-125">**URL**</span><span class="sxs-lookup"><span data-stu-id="b3ecd-125">**URL**</span></span> | <span data-ttu-id="b3ecd-126">**目的**</span><span class="sxs-lookup"><span data-stu-id="b3ecd-126">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="b3ecd-127">*/ディナー/*</span><span class="sxs-lookup"><span data-stu-id="b3ecd-127">*/Dinners/*</span></span> | <span data-ttu-id="b3ecd-128">今後のディナーの HTML リストを表示する</span><span class="sxs-lookup"><span data-stu-id="b3ecd-128">Display an HTML list of upcoming dinners</span></span> |
| <span data-ttu-id="b3ecd-129">*/ディナー/詳細/[id]*</span><span class="sxs-lookup"><span data-stu-id="b3ecd-129">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="b3ecd-130">URL に埋め込まれた "id" パラメータで示される特定のディナーに関する詳細を表示します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-130">Display details about a specific dinner indicated by an "id" parameter embedded within the URL – which will match the DinnerID of the dinner in the database.</span></span> <span data-ttu-id="b3ecd-131">たとえば、/Dinners/Details/2 には、DinnerID 値が 2 のディナーに関する詳細を HTML ページに表示します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-131">For example: /Dinners/Details/2 would display an HTML page with details about the Dinner whose DinnerID value is 2.</span></span> |

<span data-ttu-id="b3ecd-132">以下のような DinnersController クラスに 2 つのパブリックな "アクション メソッド" を追加することで、これらの URL の初期実装を公開します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-132">We will publish initial implementations of these URLs by adding two public "action methods" to our DinnersController class like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

<span data-ttu-id="b3ecd-133">次に NerdDinner アプリケーションを実行し、ブラウザーを使用して呼び出します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-133">We'll then run the NerdDinner application and use our browser to invoke them.</span></span> <span data-ttu-id="b3ecd-134">*"/Dinners/"* URL を入力すると *、Index()* メソッドが実行され、次の応答が返されます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-134">Typing in the *"/Dinners/"* URL will cause our *Index()* method to run, and it will send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

<span data-ttu-id="b3ecd-135">*"/ディナー/詳細/2"* URL を入力すると*Details()* メソッドが実行され、次の応答が返されます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-135">Typing in the *"/Dinners/Details/2"* URL will cause our *Details()* method to run, and send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

<span data-ttu-id="b3ecd-136">あなたは疑問に思うかもしれません - mvcASP.NET DinnersControllerクラスを作成し、それらのメソッドを呼び出すためにどのように知っていましたか?</span><span class="sxs-lookup"><span data-stu-id="b3ecd-136">You might be wondering - how did ASP.NET MVC know to create our DinnersController class and invoke those methods?</span></span> <span data-ttu-id="b3ecd-137">それを理解するために、ルーティングのしくみを簡単に見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-137">To understand that let's take a quick look at how routing works.</span></span>

### <a name="understanding-aspnet-mvc-routing"></a><span data-ttu-id="b3ecd-138">MVC ルーティングASP.NETについて</span><span class="sxs-lookup"><span data-stu-id="b3ecd-138">Understanding ASP.NET MVC Routing</span></span>

<span data-ttu-id="b3ecd-139">ASP.NET MVC には強力な URL ルーティング エンジンが含まれており、URL をコントローラ クラスにマップする方法を柔軟に制御できます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-139">ASP.NET MVC includes a powerful URL routing engine that provides a lot of flexibility in controlling how URLs are mapped to controller classes.</span></span> <span data-ttu-id="b3ecd-140">これにより、MVC ASP.NET がどのコントローラクラスを作成するか、どのメソッドを呼び出すのかを選択する方法を完全にカスタマイズできるだけでなく、変数を URL/Querystring から自動的に解析し、パラメータ引数としてメソッドに渡すさまざまな方法を構成できます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-140">It allows us to completely customize how ASP.NET MVC chooses which controller class to create, which method to invoke on it, as well as configure different ways that variables can be automatically parsed from the URL/Querystring and passed to the method as parameter arguments.</span></span> <span data-ttu-id="b3ecd-141">SEO (検索エンジン最適化) のサイトを完全に最適化し、アプリケーションから必要な URL 構造を公開する柔軟性を提供します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-141">It delivers the flexibility to totally optimize a site for SEO (search engine optimization) as well as publish any URL structure we want from an application.</span></span>

<span data-ttu-id="b3ecd-142">既定では、新しいASP.NET MVC プロジェクトには、既に登録されている URL ルーティング 規則の事前構成されたセットが付属しています。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-142">By default, new ASP.NET MVC projects come with a preconfigured set of URL routing rules already registered.</span></span> <span data-ttu-id="b3ecd-143">これにより、明示的に何も設定しなくても、アプリケーションを簡単に開始できます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-143">This enables us to easily get started on an application without having to explicitly configure anything.</span></span> <span data-ttu-id="b3ecd-144">既定のルーティング ルールの登録は、プロジェクトの "アプリケーション" クラス内にあります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-144">The default routing rule registrations can be found within the "Application" class of our projects – which we can open by double-clicking the "Global.asax" file in the root of our project:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

<span data-ttu-id="b3ecd-145">MVC ルーティング 規則ASP.NET既定の規則は、このクラスの "RegisterRoutes" メソッド内に登録されます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-145">The default ASP.NET MVC routing rules are registered within the "RegisterRoutes" method of this class:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

<span data-ttu-id="b3ecd-146">「ルート。上記の MapRoute()"メソッド呼び出しは、URL 形式を使用して着信 URL をコントローラー クラスにマップする既定のルーティング ルールを登録します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-146">The "routes.MapRoute()" method call above registers a default routing rule that maps incoming URLs to controller classes using the URL format: "/{controller}/{action}/{id}" – where "controller" is the name of the controller class to instantiate, "action" is the name of a public method to invoke on it, and "id" is an optional parameter embedded within the URL that can be passed as an argument to the method.</span></span> <span data-ttu-id="b3ecd-147">"MapRoute()" メソッド呼び出しに渡される 3 番目のパラメーターは、URL に存在しない場合にコントローラー/アクション/id 値に使用する一連の既定値です (コントローラー = "ホーム"、アクション="インデックス"、Id=" )。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-147">The third parameter passed to the "MapRoute()" method call is a set of default values to use for the controller/action/id values in the event that they are not present in the URL (Controller = "Home", Action="Index", Id="").</span></span>

<span data-ttu-id="b3ecd-148">次の表は、既定の "<em>/{コントローラー}/{action}/{id}"</em>ルート規則を使用してさまざまな URL がマップされる方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-148">Below is a table that demonstrates how a variety of URLs are mapped using the default "<em>/{controllers}/{action}/{id}"</em>route rule:</span></span>

| <span data-ttu-id="b3ecd-149">**URL**</span><span class="sxs-lookup"><span data-stu-id="b3ecd-149">**URL**</span></span> | <span data-ttu-id="b3ecd-150">**コントローラクラス**</span><span class="sxs-lookup"><span data-stu-id="b3ecd-150">**Controller Class**</span></span> | <span data-ttu-id="b3ecd-151">**アクション メソッド**</span><span class="sxs-lookup"><span data-stu-id="b3ecd-151">**Action Method**</span></span> | <span data-ttu-id="b3ecd-152">**渡されたパラメータ**</span><span class="sxs-lookup"><span data-stu-id="b3ecd-152">**Parameters Passed**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b3ecd-153">*/ディナー/詳細/2*</span><span class="sxs-lookup"><span data-stu-id="b3ecd-153">*/Dinners/Details/2*</span></span> | <span data-ttu-id="b3ecd-154">ディナーズコントローラー</span><span class="sxs-lookup"><span data-stu-id="b3ecd-154">DinnersController</span></span> | <span data-ttu-id="b3ecd-155">詳細(id)</span><span class="sxs-lookup"><span data-stu-id="b3ecd-155">Details(id)</span></span> | <span data-ttu-id="b3ecd-156">id=2</span><span class="sxs-lookup"><span data-stu-id="b3ecd-156">id=2</span></span> |
| <span data-ttu-id="b3ecd-157">*/ディナー/編集/5*</span><span class="sxs-lookup"><span data-stu-id="b3ecd-157">*/Dinners/Edit/5*</span></span> | <span data-ttu-id="b3ecd-158">ディナーズコントローラー</span><span class="sxs-lookup"><span data-stu-id="b3ecd-158">DinnersController</span></span> | <span data-ttu-id="b3ecd-159">編集(id)</span><span class="sxs-lookup"><span data-stu-id="b3ecd-159">Edit(id)</span></span> | <span data-ttu-id="b3ecd-160">id=5</span><span class="sxs-lookup"><span data-stu-id="b3ecd-160">id=5</span></span> |
| <span data-ttu-id="b3ecd-161">*/ディナー/作成*</span><span class="sxs-lookup"><span data-stu-id="b3ecd-161">*/Dinners/Create*</span></span> | <span data-ttu-id="b3ecd-162">ディナーズコントローラー</span><span class="sxs-lookup"><span data-stu-id="b3ecd-162">DinnersController</span></span> | <span data-ttu-id="b3ecd-163">Create()</span><span class="sxs-lookup"><span data-stu-id="b3ecd-163">Create()</span></span> | <span data-ttu-id="b3ecd-164">該当なし</span><span class="sxs-lookup"><span data-stu-id="b3ecd-164">N/A</span></span> |
| <span data-ttu-id="b3ecd-165">*/ディナー*</span><span class="sxs-lookup"><span data-stu-id="b3ecd-165">*/Dinners*</span></span> | <span data-ttu-id="b3ecd-166">ディナーズコントローラー</span><span class="sxs-lookup"><span data-stu-id="b3ecd-166">DinnersController</span></span> | <span data-ttu-id="b3ecd-167">インデックス()</span><span class="sxs-lookup"><span data-stu-id="b3ecd-167">Index()</span></span> | <span data-ttu-id="b3ecd-168">該当なし</span><span class="sxs-lookup"><span data-stu-id="b3ecd-168">N/A</span></span> |
| <span data-ttu-id="b3ecd-169">*/home*</span><span class="sxs-lookup"><span data-stu-id="b3ecd-169">*/Home*</span></span> | <span data-ttu-id="b3ecd-170">ホームコントローラー</span><span class="sxs-lookup"><span data-stu-id="b3ecd-170">HomeController</span></span> | <span data-ttu-id="b3ecd-171">インデックス()</span><span class="sxs-lookup"><span data-stu-id="b3ecd-171">Index()</span></span> | <span data-ttu-id="b3ecd-172">該当なし</span><span class="sxs-lookup"><span data-stu-id="b3ecd-172">N/A</span></span> |
| */* | <span data-ttu-id="b3ecd-173">ホームコントローラー</span><span class="sxs-lookup"><span data-stu-id="b3ecd-173">HomeController</span></span> | <span data-ttu-id="b3ecd-174">インデックス()</span><span class="sxs-lookup"><span data-stu-id="b3ecd-174">Index()</span></span> | <span data-ttu-id="b3ecd-175">該当なし</span><span class="sxs-lookup"><span data-stu-id="b3ecd-175">N/A</span></span> |

<span data-ttu-id="b3ecd-176">最後の 3 行は、使用されている既定値 (コントローラー = ホーム、アクション = インデックス、ID = "") を示します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-176">The last three rows show the default values (Controller = Home, Action = Index, Id = "") being used.</span></span> <span data-ttu-id="b3ecd-177">"Index" メソッドが指定されていない場合はデフォルトのアクション名として登録されるため、"/Dinners" および "/Home" URL によって、コントローラ クラスで Index() アクション メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-177">Because the "Index" method is registered as the default action name if one isn't specified, the "/Dinners" and "/Home" URLs cause the Index() action method to be invoked on their Controller classes.</span></span> <span data-ttu-id="b3ecd-178">"Home" コントローラが指定されていない場合は既定のコントローラとして登録されるため、"/" URL によって HomeController が作成され、そのコントローラに対する Index() アクション メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-178">Because the "Home" controller is registered as the default controller if one isn't specified, the "/" URL causes the HomeController to be created, and the Index() action method on it to be invoked.</span></span>

<span data-ttu-id="b3ecd-179">これらのデフォルトのURLルーティングルールが気に入らない場合は、変更が簡単です - 上記のRegisterRoutesメソッド内で編集するだけです。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-179">If you don't like these default URL routing rules, the good news is that they are easy to change - just edit them within the RegisterRoutes method above.</span></span> <span data-ttu-id="b3ecd-180">しかし、NerdDinnerアプリケーションでは、デフォルトのURLルーティングルールを変更するのではなく、そのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-180">For our NerdDinner application, though, we aren't going to change any of the default URL routing rules – instead we'll just use them as-is.</span></span>

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a><span data-ttu-id="b3ecd-181">私たちのディナーコントローラからディナーリポジトリを使用する</span><span class="sxs-lookup"><span data-stu-id="b3ecd-181">Using the DinnerRepository from our DinnersController</span></span>

<span data-ttu-id="b3ecd-182">DinnersController の Index() アクションメソッドと Details() アクションメソッドの現在の実装を、モデルを使用する実装に置き換えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-182">Let's now replace our current implementation of the DinnersController's Index() and Details() action methods with implementations that use our model.</span></span>

<span data-ttu-id="b3ecd-183">この動作を実装するために、先ほど構築した DinnerRepository クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-183">We'll use the DinnerRepository class we built earlier to implement the behavior.</span></span> <span data-ttu-id="b3ecd-184">まず、"NerdDinner.Models" 名前空間を参照する "using" ステートメントを追加し、DinnerController クラスのフィールドとして DinnerRepository のインスタンスを宣言します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-184">We'll begin by adding a "using" statement that references the "NerdDinner.Models" namespace, and then declare an instance of our DinnerRepository as a field on our DinnerController class.</span></span>

<span data-ttu-id="b3ecd-185">この章の後半では、「依存関係の注入」という概念を紹介し、より良い単体テストを可能にする DinnerRepository への参照をコントローラが取得する別の方法を示します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-185">Later in this chapter we'll introduce the concept of "Dependency Injection" and show another way for our Controllers to obtain a reference to a DinnerRepository that enables better unit testing – but for right now we'll just create an instance of our DinnerRepository inline like below.</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

<span data-ttu-id="b3ecd-186">これで、取得したデータ モデル オブジェクトを使用して HTML 応答を生成する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-186">Now we are ready to generate a HTML response back using our retrieved data model objects.</span></span>

### <a name="using-views-with-our-controller"></a><span data-ttu-id="b3ecd-187">コントローラでビューを使用する</span><span class="sxs-lookup"><span data-stu-id="b3ecd-187">Using Views with our Controller</span></span>

<span data-ttu-id="b3ecd-188">アクションメソッド内でコードを記述して HTML をアセンブルし *、Response.Write()* ヘルパーメソッドを使用してクライアントに送り返す方法は可能ですが、このアプローチは非常に簡単に扱いにくくなります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-188">While it is possible to write code within our action methods to assemble HTML and then use the *Response.Write()* helper method to send it back to the client, that approach becomes fairly unwieldy quickly.</span></span> <span data-ttu-id="b3ecd-189">より優れたアプローチは、DinnersController アクション メソッド内でアプリケーションロジックとデータロジックを実行し、HTML 応答をレンダリングするために必要なデータを、HTML 表現を出力する独立した "ビュー" テンプレートに渡す方法です。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-189">A much better approach is for us to only perform application and data logic inside our DinnersController action methods, and to then pass the data needed to render a HTML response to a separate "view" template that is responsible for outputting the HTML representation of it.</span></span> <span data-ttu-id="b3ecd-190">ここですぐにわかるように、「ビュー」テンプレートは、HTML マークアップと埋め込みレンダリング コードの組み合わせを含むテキスト ファイルです。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-190">As we'll see in a moment, a "view" template is a text file that typically contains a combination of HTML markup and embedded rendering code.</span></span>

<span data-ttu-id="b3ecd-191">コント ローラー ロジックをビュー レンダリングから分離すると、いくつかの大きな利点があります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-191">Separating our controller logic from our view rendering brings several big benefits.</span></span> <span data-ttu-id="b3ecd-192">特に、アプリケーション コードと UI の書式設定/レンダリング コードの間に明確な "懸念事項の分離" を強制するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-192">In particular it helps enforce a clear "separation of concerns" between the application code and UI formatting/rendering code.</span></span> <span data-ttu-id="b3ecd-193">これにより、UI レンダリング ロジックから切り離してアプリケーション ロジックを単体テストする方がはるかに簡単になります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-193">This makes it much easier to unit-test application logic in isolation from UI rendering logic.</span></span> <span data-ttu-id="b3ecd-194">アプリケーション コードを変更しなくても、UI レンダリング テンプレートを後で簡単に変更できます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-194">It makes it easier to later modify the UI rendering templates without having to make application code changes.</span></span> <span data-ttu-id="b3ecd-195">また、開発者とデザイナーが共同でプロジェクトに対して共同作業を行いやすくなります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-195">And it can make it easier for developers and designers to collaborate together on projects.</span></span>

<span data-ttu-id="b3ecd-196">DinnersController クラスを更新して、2 つのアクション メソッドのメソッド シグネチャを "void" の戻り値の型から "ActionResult" の戻り値の型に変更することで、ビュー テンプレートを使用して HTML UI 応答を返すことを示すことができます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-196">We can update our DinnersController class to indicate that we want to use a view template to send back an HTML UI response by changing the method signatures of our two action methods from having a return type of "void" to instead have a return type of "ActionResult".</span></span> <span data-ttu-id="b3ecd-197">次に、コント ローラーの基本クラスで*View()* ヘルパー メソッドを呼び出して、次のような "ViewResult" オブジェクトを返すことができます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-197">We can then call the *View()* helper method on the Controller base class to return back a "ViewResult" object like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

<span data-ttu-id="b3ecd-198">上記で使用している*View()* ヘルパー メソッドのシグネチャは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-198">The signature of the *View()* helper method we are using above looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

<span data-ttu-id="b3ecd-199">*View()* ヘルパー メソッドの最初のパラメーターは、HTML 応答のレンダリングに使用するビュー テンプレート ファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-199">The first parameter to the *View()* helper method is the name of the view template file we want to use to render the HTML response.</span></span> <span data-ttu-id="b3ecd-200">2 番目のパラメーターは、HTML 応答をレンダリングするためにビュー テンプレートが必要とするデータを含むモデル オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-200">The second parameter is a model object that contains the data that the view template needs in order to render the HTML response.</span></span>

<span data-ttu-id="b3ecd-201">Index() アクションメソッド内で*View()* ヘルパーメソッドを呼び出し、「インデックス」ビューテンプレートを使用してディナーの HTML リストをレンダリングすることを示しています。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-201">Within our Index() action method we are calling the *View()* helper method and indicating that we want to render an HTML listing of dinners using an "Index" view template.</span></span> <span data-ttu-id="b3ecd-202">ここでは、ビュー テンプレートに Dinner オブジェクトのシーケンスを渡して、リストを生成します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-202">We are passing the view template a sequence of Dinner objects to generate the list from:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

<span data-ttu-id="b3ecd-203">Details() アクションメソッド内では、URL 内で指定された ID を使用して Dinner オブジェクトを取得しようとします。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-203">Within our Details() action method we attempt to retrieve a Dinner object using the id provided within the URL.</span></span> <span data-ttu-id="b3ecd-204">有効な Dinner が見つかった場合は *、View()* ヘルパー メソッドを呼び出し、取得した Dinner オブジェクトをレンダリングするために "Details" ビュー テンプレートを使用することを示します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-204">If a valid Dinner is found we call the *View()* helper method, indicating we want to use a "Details" view template to render the retrieved Dinner object.</span></span> <span data-ttu-id="b3ecd-205">無効なディナーが要求された場合、"NotFound" ビュー テンプレート (およびテンプレート名を受け取るオーバーロードされたバージョンの*View()* ヘルパー メソッド) を使用して、Dinner が存在しないことを示す、役立つエラー メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-205">If an invalid dinner is requested, we render a helpful error message that indicates that the Dinner doesn't exist using a "NotFound" view template (and an overloaded version of the *View()* helper method that just takes the template name):</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

<span data-ttu-id="b3ecd-206">次に、"NotFound"、"詳細"、および "インデックス" ビュー テンプレートを実装してみましょう。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-206">Let's now implement the "NotFound", "Details", and "Index" view templates.</span></span>

### <a name="implementing-the-notfound-view-template"></a><span data-ttu-id="b3ecd-207">"NotFound" ビュー テンプレートの実装</span><span class="sxs-lookup"><span data-stu-id="b3ecd-207">Implementing the "NotFound" View Template</span></span>

<span data-ttu-id="b3ecd-208">まず、要求されたディナーが見つからないことを示すわかりやすいエラー メッセージを表示する "NotFound" ビュー テンプレートを実装します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-208">We'll begin by implementing the "NotFound" view template – which displays a friendly error message indicating that the requested dinner can't be found.</span></span>

<span data-ttu-id="b3ecd-209">コント ローラー アクション メソッド内でテキスト カーソルを配置して新しいビュー テンプレートを作成し、右クリックして [ビューの追加] メニュー コマンドを選択します (Ctrl-M、Ctrl-V を入力してこのコマンドを実行することもできます)。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-209">We'll create a new view template by positioning our text cursor within a controller action method, and then right click and choose the "Add View" menu command (we can also execute this command by typing Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

<span data-ttu-id="b3ecd-210">これにより、以下のような「ビューの追加」ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-210">This will bring up an "Add View" dialog like below.</span></span> <span data-ttu-id="b3ecd-211">既定では、ダイアログが起動されたときのカーソルが含まれるアクション メソッドの名前 (この場合は "Details" ) に合わせて作成するビューの名前があらかじめ入力されます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-211">By default the dialog will pre-populate the name of the view to create to match the name of the action method the cursor was in when the dialog was launched (in this case "Details").</span></span> <span data-ttu-id="b3ecd-212">最初に "NotFound" テンプレートを実装する必要があるため、このビュー名をオーバーライドし、"NotFound" に設定します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-212">Because we want to first implement the "NotFound" template, we'll override this view name and set it to instead be "NotFound":</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

<span data-ttu-id="b3ecd-213">[追加] ボタンをクリックすると、Visual Studio は "\Views\Dinners" ディレクトリ内に新しい "NotFound.aspx" ビュー テンプレートを作成します (ディレクトリがまだ存在しない場合にも作成されます)。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-213">When we click the "Add" button, Visual Studio will create a new "NotFound.aspx" view template for us within the "\Views\Dinners" directory (which it will also create if the directory doesn't already exist):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

<span data-ttu-id="b3ecd-214">また、コード エディター内で新しい "NotFound.aspx" ビュー テンプレートを開きます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-214">It will also open up our new "NotFound.aspx" view template within the code-editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

<span data-ttu-id="b3ecd-215">ビュー テンプレートには、既定でコンテンツとコードを追加できる 2 つの "コンテンツ領域" があります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-215">View templates by default have two "content regions" where we can add content and code.</span></span> <span data-ttu-id="b3ecd-216">最初の方法では、返送される HTML ページの "タイトル" をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-216">The first allows us to customize the "title" of the HTML page sent back.</span></span> <span data-ttu-id="b3ecd-217">2つ目は、返送されるHTMLページの「メインコンテンツ」をカスタマイズすることができます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-217">The second allows us to customize the "main content" of the HTML page sent back.</span></span>

<span data-ttu-id="b3ecd-218">"NotFound" ビュー テンプレートを実装するには、基本的なコンテンツをいくつか追加します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-218">To implement our "NotFound" view template we'll add some basic content:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

<span data-ttu-id="b3ecd-219">その後、ブラウザ内で試すことができます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-219">We can then try it out within the browser.</span></span> <span data-ttu-id="b3ecd-220">これを行うには *、「ディナー/詳細/9999」URLを*リクエストしましょう。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-220">To do this let's request the *"/Dinners/Details/9999"* URL.</span></span> <span data-ttu-id="b3ecd-221">これは、現在データベースに存在しないディナーを参照し、DinnersController.Details() アクションメソッドが "NotFound" ビューテンプレートをレンダリングする原因となります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-221">This will refer to a dinner that doesn't currently exist in the database, and will cause our DinnersController.Details() action method to render our "NotFound" view template:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

<span data-ttu-id="b3ecd-222">上記のスクリーン ショットで気づくことの 1 つは、基本的なビュー テンプレートが、画面上のメイン コンテンツを囲む HTML の束を継承していることです。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-222">One thing you'll notice in the screen-shot above is that our basic view template has inherited a bunch of HTML that surrounds the main content on the screen.</span></span> <span data-ttu-id="b3ecd-223">これは、ビュー テンプレートがサイト上のすべてのビューに一貫したレイアウトを適用できる "マスター ページ" テンプレートを使用しているためです。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-223">This is because our view-template is using a "master page" template that enables us to apply a consistent layout across all views on the site.</span></span> <span data-ttu-id="b3ecd-224">マスター ページの動作については、このチュートリアルの後半で説明します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-224">We'll discuss how master pages work more in a later part of this tutorial.</span></span>

### <a name="implementing-the-details-view-template"></a><span data-ttu-id="b3ecd-225">"詳細" ビュー テンプレートの実装</span><span class="sxs-lookup"><span data-stu-id="b3ecd-225">Implementing the "Details" View Template</span></span>

<span data-ttu-id="b3ecd-226">ここでは、単一の Dinner モデル用に HTML を生成する"詳細" ビュー テンプレートを実装しましょう。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-226">Let's now implement the "Details" view template – which will generate HTML for a single Dinner model.</span></span>

<span data-ttu-id="b3ecd-227">これを行うには、テキストカーソルを Details アクションメソッド内に配置し、右クリックして [ビューの追加] メニュー コマンド (または Ctrl+M、Ctrl-V キーを押します) を選択します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-227">We'll do this by positioning our text cursor within the Details action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

<span data-ttu-id="b3ecd-228">これにより、[ビューの追加] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-228">This will bring up the "Add View" dialog.</span></span> <span data-ttu-id="b3ecd-229">既定のビュー名 (「詳細」) をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-229">We'll keep the default view name ("Details").</span></span> <span data-ttu-id="b3ecd-230">ダイアログで[厳密に型指定されたビューを作成]チェックボックスを選択し、コントローラからビューに渡すモデルタイプの名前を選択します(コンボボックスのドロップダウンを使用)。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-230">We'll also select the "Create a strongly-typed View" checkbox in the dialog and select (using the combobox dropdown) the name of the model type we are passing from the Controller to the View.</span></span> <span data-ttu-id="b3ecd-231">このビューでは、Dinner オブジェクトを渡しています (この型の完全修飾名は "NerdDinner.Models.Dinner"です)。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-231">For this view we are passing a Dinner object (the fully qualified name for this type is: "NerdDinner.Models.Dinner"):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

<span data-ttu-id="b3ecd-232">「空のビュー」を作成することを選択した前のテンプレートとは異なり、今回は「詳細」テンプレートを使用してビューを自動的に「スキャフォールディング」することを選択します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-232">Unlike the previous template, where we chose to create an "Empty View", this time we will choose to automatically "scaffold" the view using a "Details" template.</span></span> <span data-ttu-id="b3ecd-233">このことを示すには、上記のダイアログで「コンテンツの表示」ドロップダウンを変更します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-233">We can indicate this by changing the "View content" drop-down in the dialog above.</span></span>

<span data-ttu-id="b3ecd-234">「スキャフォールディング」は、私たちが渡すDinnerオブジェクトに基づいて、詳細ビューテンプレートの初期実装を生成します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-234">"Scaffolding" will generate an initial implementation of our details view template based on the Dinner object we are passing to it.</span></span> <span data-ttu-id="b3ecd-235">これにより、ビュー テンプレートの実装を簡単に開始できます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-235">This provides an easy way for us to quickly get started on our view template implementation.</span></span>

<span data-ttu-id="b3ecd-236">[追加] ボタンをクリックすると、Visual Studio は "\Views\Dinners" ディレクトリ内に新しい "Details.aspx" ビュー テンプレート ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-236">When we click the "Add" button, Visual Studio will create a new "Details.aspx" view template file for us within our "\Views\Dinners" directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

<span data-ttu-id="b3ecd-237">また、コード エディター内で新しい "Details.aspx" ビュー テンプレートを開きます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-237">It will also open up our new "Details.aspx" view template within the code-editor.</span></span> <span data-ttu-id="b3ecd-238">このファイルには、Dinner モデルに基づく詳細ビューの初期スキャフォールディング実装が含まれます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-238">It will contain an initial scaffold implementation of a details view based on a Dinner model.</span></span> <span data-ttu-id="b3ecd-239">スキャフォールディング エンジンは、.NET リフレクションを使用して、渡されたクラスで公開されているパブリック プロパティを調べ、見つかった各型に基づいて適切なコンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-239">The scaffolding engine uses .NET reflection to look at the public properties exposed on the class passed it, and will add appropriate content based on each type it finds:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

<span data-ttu-id="b3ecd-240">*"/Dinners/Details/1"* URL をリクエストすると、この "詳細" スキャフォールディングの実装がブラウザでどのようなものであるかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-240">We can request the *"/Dinners/Details/1"* URL to see what this "details" scaffold implementation looks like in the browser.</span></span> <span data-ttu-id="b3ecd-241">この URL を使用すると、最初に作成したときに手動でデータベースに追加したディナーのいずれかが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-241">Using this URL will display one of the dinners we manually added to our database when we first created it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

<span data-ttu-id="b3ecd-242">これにより、すぐに起動して実行し、Details.aspx ビューの初期実装を提供します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-242">This gets us up and running quickly, and provides us with an initial implementation of our Details.aspx view.</span></span> <span data-ttu-id="b3ecd-243">その後、UIをカスタマイズして満足するように調整することができます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-243">We can then go and tweak it to customize the UI to our satisfaction.</span></span>

<span data-ttu-id="b3ecd-244">詳細を見ると、 Details.aspx テンプレートは、静的 HTML だけでなく、埋め込まれたレンダリング コードが含まれていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-244">When we look at the Details.aspx template more closely, we'll find that it contains static HTML as well as embedded rendering code.</span></span> <span data-ttu-id="b3ecd-245">&lt;%&gt;コード ナゲットはビュー テンプレートのレンダリング時にコードを&lt;実行し、%= %&gt;コード ナゲットは、その中に含まれるコードを実行し、その結果をテンプレートの出力ストリームにレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-245">&lt;% %&gt; code nuggets execute code when the view template renders, and &lt;%= %&gt; code nuggets execute the code contained within them and then render the result to the output stream of the template.</span></span>

<span data-ttu-id="b3ecd-246">厳密に型指定された "Model" プロパティを使用して、コントローラーから渡された "Dinner" モデル オブジェクトにアクセスするコードを View 内に記述できます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-246">We can write code within our View that accesses the "Dinner" model object that was passed from our controller using a strongly-typed "Model" property.</span></span> <span data-ttu-id="b3ecd-247">Visual Studio では、エディター内でこの "モデル" プロパティにアクセスする際に、完全なコードインテッラーセンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-247">Visual Studio provides us with full code-intellisense when accessing this "Model" property within the editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

<span data-ttu-id="b3ecd-248">最終的な詳細ビュー テンプレートのソースが次のようになるように、いくつかの調整を行いましょう。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-248">Let's make some tweaks so that the source for our final Details view template looks like below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

<span data-ttu-id="b3ecd-249">*「/ディナー/詳細/1」URL*に再びアクセスすると、次のようにレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-249">When we access the *"/Dinners/Details/1"* URL again it will now render like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a><span data-ttu-id="b3ecd-250">"インデックス" ビュー テンプレートの実装</span><span class="sxs-lookup"><span data-stu-id="b3ecd-250">Implementing the "Index" View Template</span></span>

<span data-ttu-id="b3ecd-251">今度は、今後のディナーのリストを生成する「インデックス」ビューテンプレートを実装しましょう。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-251">Let's now implement the "Index" view template – which will generate a listing of upcoming Dinners.</span></span> <span data-ttu-id="b3ecd-252">これを行うには、テキストカーソルをインデックスアクションメソッド内に配置し、右クリックして[ビューの追加]メニューコマンド(またはCtrl-M、Ctrl-Vを押す)を選択します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-252">To-do this we'll position our text cursor within the Index action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V).</span></span>

<span data-ttu-id="b3ecd-253">[ビューの追加] ダイアログでは、"Index" という名前のビュー テンプレートを保持し、[厳密に型指定されたビューを作成する] チェック ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-253">Within the "Add View" dialog we'll keep the view template named "Index" and select the "Create a strongly-typed view" checkbox.</span></span> <span data-ttu-id="b3ecd-254">今回は、"List" ビュー テンプレートを自動的に生成し、ビューに渡されるモデルタイプとして "NerdDinner.Models.Dinner" を選択します (これは、"List" スキャフォールドを作成すると、コントローラからビューに Dinner オブジェクトのシーケンスを渡すことを前提にビューの追加ダイアログが表示されます)。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-254">This time we will choose to automatically generate a "List" view template, and select "NerdDinner.Models.Dinner" as the model type passed to the view (which because we have indicated we are creating a "List" scaffold will cause the Add View dialog to assume we are passing a sequence of Dinner objects from our Controller to the View):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

<span data-ttu-id="b3ecd-255">[追加] ボタンをクリックすると、Visual Studio は "\Views\Dinners" ディレクトリ内に新しい "Index.aspx" ビュー テンプレート ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-255">When we click the "Add" button, Visual Studio will create a new "Index.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="b3ecd-256">ビューに渡す Dinners の HTML テーブル リストを提供する初期実装を "スキャフォールディング" します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-256">It will "scaffold" an initial implementation within it that provides an HTML table listing of the Dinners we pass to the view.</span></span>

<span data-ttu-id="b3ecd-257">アプリケーションを実行し *、"/Dinners/"* URL にアクセスすると、次のようにディナーのリストがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-257">When we run the application and access the *"/Dinners/"* URL it will render our list of dinners like so:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

<span data-ttu-id="b3ecd-258">上記のテーブルソリューションは、私たちのDinnerデータのグリッドのようなレイアウトを提供します - それは私たちが私たちの消費者がDinnerリストに直面している場合に望むものではありません。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-258">The table solution above gives us a grid-like layout of our Dinner data – which isn't quite what we want for our consumer facing Dinner listing.</span></span> <span data-ttu-id="b3ecd-259">Index.aspx ビュー テンプレートを更新し、データの列数を少なくするように変更し&lt;、ul&gt;要素を使用して次のコードを使用してテーブルの代わりにレンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-259">We can update the Index.aspx view template and modify it to list fewer columns of data, and use a &lt;ul&gt; element to render them instead of a table using the code below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

<span data-ttu-id="b3ecd-260">モデルの各ディナーをループ処理するときに、上記の foreach ステートメント内で "var" キーワードを使用しています。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-260">We are using the "var" keyword within the above foreach statement as we loop over each dinner in our Model.</span></span> <span data-ttu-id="b3ecd-261">C# 3.0 に慣れていない人は、"var" を使用すると、dinner オブジェクトが遅延バインディングされていることを意味すると考えるかもしれません。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-261">Those unfamiliar with C# 3.0 might think that using "var" means that the dinner object is late-bound.</span></span> <span data-ttu-id="b3ecd-262">これは、コンパイラが厳密に型指定された "Model" プロパティ ("IEnumerable&lt;Dinner " という型) に&gt;対して型推論を使用し、ローカルの "dinner" 変数を Dinner 型としてコンパイルしていることを意味します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-262">It instead means that the compiler is using type-inference against the strongly typed "Model" property (which is of type "IEnumerable&lt;Dinner&gt;") and compiling the local "dinner" variable as a Dinner type – which means we get full intellisense and compile-time checking for it within code blocks:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

<span data-ttu-id="b3ecd-263">ブラウザの */Dinners* URL で更新を行うと、更新されたビューは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-263">When we hit refresh on the */Dinners* URL in our browser our updated view now looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

<span data-ttu-id="b3ecd-264">これは見栄えが良いですが、まだ完全にそこにはありません。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-264">This is looking better – but isn't entirely there yet.</span></span> <span data-ttu-id="b3ecd-265">最後の手順は、エンドユーザーがリスト内の個々の Dinner をクリックして、その詳細を確認できるようにすることです。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-265">Our last step is to enable end-users to click individual Dinners in the list and see details about them.</span></span> <span data-ttu-id="b3ecd-266">これを実装するには、DinnersController の詳細アクション メソッドにリンクする HTML ハイパーリンク要素をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-266">We'll implement this by rendering HTML hyperlink elements that link to the Details action method on our DinnersController.</span></span>

<span data-ttu-id="b3ecd-267">これらのハイパーリンクは、2 つの方法のいずれかでインデックス ビュー内に生成できます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-267">We can generate these hyperlinks within our Index view in one of two ways.</span></span> <span data-ttu-id="b3ecd-268">1 つ目は、以下&lt;のような&gt;要素を手動で作成し、HTML&gt;要素内に&lt;&gt; % % ブロックを埋め込みます。 &lt;</span><span class="sxs-lookup"><span data-stu-id="b3ecd-268">The first is to manually create HTML &lt;a&gt; elements like below, where we embed &lt;% %&gt; blocks within the &lt;a&gt; HTML element:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

<span data-ttu-id="b3ecd-269">別の方法として、コントローラ上の別のアクション メソッドにリンクする&lt;&gt;要素をプログラムで HTML の作成をサポートする、ASP.NET MVC 内の組み込みの "Html.ActionLink() " ヘルパー メソッドを利用する方法もあります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-269">An alternative approach we can use is to take advantage of the built-in "Html.ActionLink()" helper method within ASP.NET MVC that supports programmatically creating an HTML &lt;a&gt; element that links to another action method on a Controller:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

<span data-ttu-id="b3ecd-270">Html.ActionLink() ヘルパー メソッドの最初のパラメーターは、表示するリンク テキスト (この場合は、dinner のタイトル) で、2 番目のパラメーターはリンクを生成する Controller アクション名 (この場合は Details メソッド) であり、3 番目のパラメーターはアクションに送信する一連のパラメーターです (プロパティ名/値を持つ匿名型として実装されます)。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-270">The first parameter to the Html.ActionLink() helper method is the link-text to display (in this case the title of the dinner), the second parameter is the Controller action name we want to generate the link to (in this case the Details method), and the third parameter is a set of parameters to send to the action (implemented as an anonymous type with property name/values).</span></span> <span data-ttu-id="b3ecd-271">この場合、リンクするディナーの "id" パラメーターを指定し、ASP.NET MVC の既定の URL ルーティング ルールは "{Controller}/{アクション}/{id}" であるため、Html.ActionLink() ヘルパー メソッドは次の出力を生成します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-271">In this case we are specifying the "id" parameter of the dinner we want to link to, and because the default URL routing rule in ASP.NET MVC is "{Controller}/{Action}/{id}" the Html.ActionLink() helper method will generate the following output:</span></span>

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

<span data-ttu-id="b3ecd-272">Index.aspx ビューでは、Html.ActionLink() ヘルパー メソッドのアプローチを使用し、リスト内の各ディナーを適切な詳細 URL にリンクします。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-272">For our Index.aspx view we'll use the Html.ActionLink() helper method approach and have each dinner in the list link to the appropriate details URL:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

<span data-ttu-id="b3ecd-273">そして今、私たちは */Dinners* URLをヒットすると、私たちのディナーリストは以下のようになります:</span><span class="sxs-lookup"><span data-stu-id="b3ecd-273">And now when we hit the */Dinners* URL our dinner list looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

<span data-ttu-id="b3ecd-274">リスト内のディナーのいずれかをクリックすると、その詳細を表示するために移動します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-274">When we click any of the Dinners in the list we'll navigate to see details about it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a><span data-ttu-id="b3ecd-275">規約ベースの名前付けと \Views ディレクトリ構造</span><span class="sxs-lookup"><span data-stu-id="b3ecd-275">Convention-based naming and the \Views directory structure</span></span>

<span data-ttu-id="b3ecd-276">ASP.NET MVC アプリケーションでは、既定で、ビュー テンプレートを解決するときに、規則に基づいたディレクトリの名前付け構造を使用します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-276">ASP.NET MVC applications by default use a convention-based directory naming structure when resolving view templates.</span></span> <span data-ttu-id="b3ecd-277">これにより、開発者は Controller クラス内からビューを参照するときに、場所のパスを完全に修飾する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-277">This allows developers to avoid having to fully-qualify a location path when referencing views from within a Controller class.</span></span> <span data-ttu-id="b3ecd-278">既定では、ASP.NET MVC は、アプリケーションの下にある \*\Views\[ControllerName]\*ディレクトリ内のビュー テンプレート ファイルを探します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-278">By default ASP.NET MVC will look for the view template file within the \*\Views\[ControllerName]\* directory underneath the application.</span></span>

<span data-ttu-id="b3ecd-279">たとえば、DinnersController クラスに取り組んできましたが、このクラスは、"インデックス"、"詳細"、"NotFound" の 3 つのビュー テンプレートを明示的に参照します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-279">For example, we've been working on the DinnersController class – which explicitly references three view templates: "Index", "Details" and "NotFound".</span></span> <span data-ttu-id="b3ecd-280">ASP.NET MVC は、既定では、アプリケーションのルート ディレクトリの下にある*\Views\Dinners*ディレクトリ内でこれらのビューを探します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-280">ASP.NET MVC will by default look for these views within the *\Views\Dinners* directory underneath our application root directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

<span data-ttu-id="b3ecd-281">プロジェクト内に現在3つのコントローラクラスがある方法に注意してください (DinnersController、 HomeControllerとAccountController - 最後の2つは、プロジェクトを作成したときにデフォルトで追加されました)、\Viewsディレクトリ内に3つのサブディレクトリ(コントローラごとに1つ)があります。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-281">Notice above how there are currently three controller classes within the project (DinnersController, HomeController and AccountController – the last two were added by default when we created the project), and there are three sub-directories (one for each controller) within the \Views directory.</span></span>

<span data-ttu-id="b3ecd-282">ホーム および アカウント コントローラから参照されるビューは、それぞれの*\Views\Home*ディレクトリおよび*\Views\Account*ディレクトリからビュー テンプレートを自動的に解決します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-282">Views referenced from the Home and Accounts controllers will automatically resolve their view templates from the respective *\Views\Home* and *\Views\Account* directories.</span></span> <span data-ttu-id="b3ecd-283">*\Views\Shared*サブディレクトリには、アプリケーション内の複数のコントローラで再利用されるビュー テンプレートを格納する方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-283">The *\Views\Shared* sub-directory provides a way to store view templates that are re-used across multiple controllers within the application.</span></span> <span data-ttu-id="b3ecd-284">ASP.NETMVC がビュー テンプレートを解決しようとすると、最初に*\Views\[Controller]* の特定のディレクトリ内でチェックされ、ビュー テンプレートが見つからない場合は*\Views\Shared*ディレクトリ内に表示されます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-284">When ASP.NET MVC attempts to resolve a view template, it will first check within the *\Views\[Controller]* specific directory, and if it can't find the view template there it will look within the *\Views\Shared* directory.</span></span>

<span data-ttu-id="b3ecd-285">個々のビュー テンプレートに名前を付ける場合は、ビュー テンプレートがレンダリングの原因となったアクション メソッドと同じ名前を共有することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-285">When it comes to naming individual view templates, the recommended guidance is to have the view template share the same name as the action method that caused it to render.</span></span> <span data-ttu-id="b3ecd-286">たとえば、上記の "Index" アクション メソッドは、"Index" ビューを使用してビューの結果を表示し、"Details" アクション メソッドは "Details" ビューを使用して結果を表示しています。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-286">For example, above our "Index" action method is using the "Index" view to render the view result, and the "Details" action method is using the "Details" view to render its results.</span></span> <span data-ttu-id="b3ecd-287">これにより、各アクションに関連付けられているテンプレートをすばやく確認できます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-287">This makes it easy to quickly see which template is associated with each action.</span></span>

<span data-ttu-id="b3ecd-288">ビュー テンプレートがコントローラで呼び出されるアクション メソッドと同じ名前を持っている場合、開発者はビュー テンプレート名を明示的に指定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-288">Developers do not need to explicitly specify the view template name when the view template has the same name as the action method being invoked on the controller.</span></span> <span data-ttu-id="b3ecd-289">代わりに、モデル オブジェクトを "View()" ヘルパー メソッドに渡すだけで (ビュー名を指定せずに)ASP.NET、MVC は自動的にディスク上の*ビュー\[テンプレートを\[* 使用してレンダリングすることを推測します。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-289">We can instead just pass the model object to the "View()" helper method (without specifying the view name), and ASP.NET MVC will automatically infer that we want to use the *\Views\[ControllerName]\[ActionName]* view template on disk to render it.</span></span>

<span data-ttu-id="b3ecd-290">これにより、コントローラコードを少しクリーンアップし、コード内で名前を二度複製することを避けられます。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-290">This allows us to clean up our controller code a little, and avoid duplicating the name twice in our code:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

<span data-ttu-id="b3ecd-291">上記のコードは、サイトの素敵なディナーリスト/詳細エクスペリエンスを実装するために必要なすべてです。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-291">The above code is all that is needed to implement a nice Dinner listing/details experience for the site.</span></span>

#### <a name="next-step"></a><span data-ttu-id="b3ecd-292">次の手順</span><span class="sxs-lookup"><span data-stu-id="b3ecd-292">Next Step</span></span>

<span data-ttu-id="b3ecd-293">私たちは今、構築された素敵なディナーブラウジング体験を持っています。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-293">We now have a nice Dinner browsing experience built.</span></span>

<span data-ttu-id="b3ecd-294">今すぐ CRUD (作成、読み取り、更新、削除) データフォーム編集のサポートを有効にしましょう。</span><span class="sxs-lookup"><span data-stu-id="b3ecd-294">Let's now enable CRUD (Create, Read, Update, Delete) data form editing support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b3ecd-295">[前へ](build-a-model-with-business-rule-validations.md)
> [次へ](provide-crud-create-read-update-delete-data-form-entry-support.md)</span><span class="sxs-lookup"><span data-stu-id="b3ecd-295">[Previous](build-a-model-with-business-rule-validations.md)
[Next](provide-crud-create-read-update-delete-data-form-entry-support.md)</span></span>
