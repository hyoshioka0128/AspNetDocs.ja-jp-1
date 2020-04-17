---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: ビューデータを使用してビューモデル クラスを実装する |マイクロソフトドキュメント
author: rick-anderson
description: 手順 6 では、よりリッチなフォーム編集シナリオのサポートを有効にする方法を示し、コントローラーからビューにデータを渡すために使用できる 2 つのアプローチについても説明します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 7fa2af2a55d12bbe11b29dff594823a1e5ea0152
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541105"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a><span data-ttu-id="ed72b-103">ViewData を使用し、ViewModel クラスを実装する</span><span class="sxs-lookup"><span data-stu-id="ed72b-103">Use ViewData and Implement ViewModel Classes</span></span>

<span data-ttu-id="ed72b-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ed72b-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="ed72b-105">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="ed72b-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="ed72b-106">これは、MVC 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NETの手順 6 です。</span><span class="sxs-lookup"><span data-stu-id="ed72b-106">This is step 6 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="ed72b-107">手順 6 では、よりリッチなフォーム編集シナリオのサポートを有効にする方法を示し、コントローラーからビューにデータを渡すために使用できる 2 つの方法についても説明します: ViewData と ViewModel。</span><span class="sxs-lookup"><span data-stu-id="ed72b-107">Step 6 shows how enable support for richer form editing scenarios, and also discusses two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>
> 
> <span data-ttu-id="ed72b-108">mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="ed72b-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a><span data-ttu-id="ed72b-109">オタクディナーステップ6:ビューデータとビューモデル</span><span class="sxs-lookup"><span data-stu-id="ed72b-109">NerdDinner Step 6: ViewData and ViewModel</span></span>

<span data-ttu-id="ed72b-110">フォームポストのシナリオの数を取り上げ、作成、更新、削除 (CRUD) サポートを実装する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="ed72b-110">We've covered a number of form post scenarios, and discussed how to implement create, update and delete (CRUD) support.</span></span> <span data-ttu-id="ed72b-111">DinnersController の実装をさらに進め、より充実したフォーム編集シナリオのサポートを可能にします。</span><span class="sxs-lookup"><span data-stu-id="ed72b-111">We'll now take our DinnersController implementation further and enable support for richer form editing scenarios.</span></span> <span data-ttu-id="ed72b-112">これを行う間、コント ローラーからビューにデータを渡すために使用できる 2 つのアプローチを説明します: ViewData と ViewModel.</span><span class="sxs-lookup"><span data-stu-id="ed72b-112">While doing this we'll discuss two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>

### <a name="passing-data-from-controllers-to-view-templates"></a><span data-ttu-id="ed72b-113">コントローラからビューテンプレートへのデータの受け渡し</span><span class="sxs-lookup"><span data-stu-id="ed72b-113">Passing Data from Controllers to View-Templates</span></span>

<span data-ttu-id="ed72b-114">MVC パターンの特徴の 1 つは、アプリケーションのさまざまなコンポーネント間で実施するのに役立つ厳密な "懸念事項の分離" です。</span><span class="sxs-lookup"><span data-stu-id="ed72b-114">One of the defining characteristics of the MVC pattern is the strict "separation of concerns" it helps enforce between the different components of an application.</span></span> <span data-ttu-id="ed72b-115">モデル、コントローラ、ビューはそれぞれ、明確に定義された役割と責任を持ち、互いの間で明確に定義された方法で通信します。</span><span class="sxs-lookup"><span data-stu-id="ed72b-115">Models, Controllers and Views each have well defined roles and responsibilities, and they communicate amongst each other in well defined ways.</span></span> <span data-ttu-id="ed72b-116">これにより、テストの容易性とコードの再利用が促進されます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-116">This helps promote testability and code reuse.</span></span>

<span data-ttu-id="ed72b-117">コント ローラー クラスは、クライアントに HTML 応答を返すことを決定する場合、明示的に応答をレンダリングするために必要なすべてのデータをビュー テンプレートに渡します。</span><span class="sxs-lookup"><span data-stu-id="ed72b-117">When a Controller class decides to render an HTML response back to a client, it is responsible for explicitly passing to the view template all of the data needed to render the response.</span></span> <span data-ttu-id="ed72b-118">ビュー テンプレートは、データ取得やアプリケーション ロジックを実行せず、代わりに、コントローラーによって渡されるモデル/データから追い出されるレンダリング コードのみを持つことを制限する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed72b-118">View templates should never perform any data retrieval or application logic – and should instead limit themselves to only have rendering code that is driven off of the model/data passed to it by the controller.</span></span>

<span data-ttu-id="ed72b-119">今、DinnersControllerクラスによってビューテンプレートに渡されるモデルデータは、Index() の場合はディナーオブジェクトのリスト、および詳細()、Edit()、Create()、Delete()の場合は単一のディナーオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="ed72b-119">Right now the model data being passed by our DinnersController class to our view templates is simple and straight-forward – a list of Dinner objects in the case of Index(), and a single Dinner object in the case of Details(), Edit(), Create() and Delete().</span></span> <span data-ttu-id="ed72b-120">アプリケーションに UI 機能を追加する場合、ビュー テンプレート内で HTML 応答をレンダリングするために、このデータ以外のデータを渡す必要がよくあります。</span><span class="sxs-lookup"><span data-stu-id="ed72b-120">As we add more UI capabilities to our application, we are often going to need to pass more than just this data to render HTML responses within our view templates.</span></span> <span data-ttu-id="ed72b-121">たとえば、編集ビューと作成ビューの "国" フィールドを HTML テキストボックスからドロップダウンリストに変更する場合があります。</span><span class="sxs-lookup"><span data-stu-id="ed72b-121">For example, we might want to change the "Country" field within our Edit and Create views from being an HTML textbox to a dropdownlist.</span></span> <span data-ttu-id="ed72b-122">ビュー テンプレートの国名のドロップダウン リストをハードコーディングするのではなく、動的に設定するサポート対象国のリストから生成することもできます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-122">Rather than hard-code the dropdown list of country names in the view template, we might want to generate it from a list of supported countries that we populate dynamically.</span></span> <span data-ttu-id="ed72b-123">Dinner オブジェクト*と*サポートされている国のリストを、コントローラからビュー テンプレートに渡す方法が必要です。</span><span class="sxs-lookup"><span data-stu-id="ed72b-123">We will need a way to pass both the Dinner object *and* the list of supported countries from our controller to our view templates.</span></span>

<span data-ttu-id="ed72b-124">これを達成する2つの方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="ed72b-124">Let's look at two ways we can accomplish this.</span></span>

### <a name="using-the-viewdata-dictionary"></a><span data-ttu-id="ed72b-125">ビューデータ ディクショナリの使用</span><span class="sxs-lookup"><span data-stu-id="ed72b-125">Using the ViewData Dictionary</span></span>

<span data-ttu-id="ed72b-126">コント ローラーの基本クラスは、コント ローラーからビューに追加のデータ項目を渡すために使用できる"ViewData"ディクショナリ プロパティを公開します。</span><span class="sxs-lookup"><span data-stu-id="ed72b-126">The Controller base class exposes a "ViewData" dictionary property that can be used to pass additional data items from Controllers to Views.</span></span>

<span data-ttu-id="ed72b-127">たとえば、編集ビュー内の "Country" テキスト ボックスを HTML テキストボックスからドロップダウンリストに変更するシナリオをサポートするために、国のドロップダウンリストのモデルとして使用できる SelectList オブジェクトを (Dinner オブジェクトに加えて) 渡すように Edit() アクション メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="ed72b-127">For example, to support the scenario where we want to change the "Country" textbox within our Edit view from being an HTML textbox to a dropdownlist, we can update our Edit() action method to pass (in addition to a Dinner object) a SelectList object that can be used as the model of a countries dropdownlist.</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

<span data-ttu-id="ed72b-128">上記の SelectList のコンストラクターは、ドロップダウン リストに入力する郡のリストと、現在選択されている値を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-128">The constructor of the SelectList above is accepting a list of counties to populate the drop-downlist with, as well as the currently selected value.</span></span>

<span data-ttu-id="ed72b-129">その後、前に使用した Html.TextBox() ヘルパー メソッドの代わりに Html.DropDownList() ヘルパー メソッドを使用するように Edit.aspx ビュー テンプレートを更新できます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-129">We can then update our Edit.aspx view template to use the Html.DropDownList() helper method instead of the Html.TextBox() helper method we used previously:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

<span data-ttu-id="ed72b-130">上記の Html.DropDownList() ヘルパー メソッドは、2 つのパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="ed72b-130">The Html.DropDownList() helper method above takes two parameters.</span></span> <span data-ttu-id="ed72b-131">最初の要素は、出力する HTML フォーム要素の名前です。</span><span class="sxs-lookup"><span data-stu-id="ed72b-131">The first is the name of the HTML form element to output.</span></span> <span data-ttu-id="ed72b-132">2 つ目は、ViewData ディクショナリを使用して渡した "SelectList" モデルです。</span><span class="sxs-lookup"><span data-stu-id="ed72b-132">The second is the "SelectList" model we passed via the ViewData dictionary.</span></span> <span data-ttu-id="ed72b-133">C# "as" キーワードを使用して、辞書内の型を SelectList としてキャストしています。</span><span class="sxs-lookup"><span data-stu-id="ed72b-133">We are using the C# "as" keyword to cast the type within the dictionary as a SelectList.</span></span>

<span data-ttu-id="ed72b-134">そして今、私たちのアプリケーションを実行し、ブラウザ内の */Dinners /Edit/1* URLにアクセスすると、編集UIが更新され、テキストボックスではなく国のドロップダウンリストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-134">And now when we run our application and access the */Dinners/Edit/1* URL within our browser we'll see that our edit UI has been updated to display a dropdownlist of countries instead of a textbox:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

<span data-ttu-id="ed72b-135">HTTP-POST Edit メソッドからビュー テンプレートの編集もレンダリングするため (エラーが発生した場合)、エラー シナリオでビュー テンプレートがレンダリングされるときに、このメソッドも更新して SelectList を ViewData に追加するようにします。</span><span class="sxs-lookup"><span data-stu-id="ed72b-135">Because we also render the Edit view template from the HTTP-POST Edit method (in scenarios when errors occur), we'll want to make sure that we also update this method to add the SelectList to ViewData when the view template is rendered in error scenarios:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

<span data-ttu-id="ed72b-136">そして今、私たちのディナーコントローラの編集シナリオは、ドロップダウンリストをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ed72b-136">And now our DinnersController edit scenario supports a DropDownList.</span></span>

### <a name="using-a-viewmodel-pattern"></a><span data-ttu-id="ed72b-137">ビューモデル パターンの使用</span><span class="sxs-lookup"><span data-stu-id="ed72b-137">Using a ViewModel Pattern</span></span>

<span data-ttu-id="ed72b-138">ViewData ディクショナリ アプローチには、高速で実装が簡単であるという利点があります。</span><span class="sxs-lookup"><span data-stu-id="ed72b-138">The ViewData dictionary approach has the benefit of being fairly fast and easy to implement.</span></span> <span data-ttu-id="ed72b-139">ただし、入力ミスはコンパイル時にキャッチされないエラーにつながる可能性があるため、一部の開発者は文字列ベースの辞書を使用することを好まない。</span><span class="sxs-lookup"><span data-stu-id="ed72b-139">Some developers don't like using string-based dictionaries, though, since typos can lead to errors that will not be caught at compile-time.</span></span> <span data-ttu-id="ed72b-140">型指定されていない ViewData ディクショナリでは、ビュー テンプレートで C# のような厳密に型指定された言語を使用する場合は、"as" 演算子を使用するか、キャストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed72b-140">The un-typed ViewData dictionary also requires using the "as" operator or casting when using a strongly-typed language like C# in a view template.</span></span>

<span data-ttu-id="ed72b-141">別の方法として、"ビューモデル" パターンと呼ばれる方法があります。</span><span class="sxs-lookup"><span data-stu-id="ed72b-141">An alternative approach that we could use is one often referred to as the "ViewModel" pattern.</span></span> <span data-ttu-id="ed72b-142">このパターンを使用する場合、特定のビュー シナリオに最適化され、ビュー テンプレートで必要な動的な値/コンテンツのプロパティを公開する厳密に型指定されたクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="ed72b-142">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="ed72b-143">コントローラクラスは、これらのビュー最適化クラスを設定し、使用するビューテンプレートに渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-143">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="ed72b-144">これにより、ビュー テンプレート内でのタイプ セーフ、コンパイル時チェック、およびエディターのインテリセンスが可能になります。</span><span class="sxs-lookup"><span data-stu-id="ed72b-144">This enables type-safety, compile-time checking, and editor intellisense within view templates.</span></span>

<span data-ttu-id="ed72b-145">たとえば、Dinner フォームの編集シナリオを有効にするには、次のような "DinnerFormViewModel" クラスを作成して、厳密に型指定された 2 つのプロパティ (Dinner オブジェクトと、国のドロップダウンリストに設定するために必要な SelectList モデル) を公開します。</span><span class="sxs-lookup"><span data-stu-id="ed72b-145">For example, to enable dinner form editing scenarios we can create a "DinnerFormViewModel" class like below that exposes two strongly-typed properties: a Dinner object, and the SelectList model needed to populate the countries dropdownlist:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

<span data-ttu-id="ed72b-146">その後、リポジトリから取得した Dinner オブジェクトを使用して DinnerFormViewModel を作成し、ビュー テンプレートに渡すために Edit() アクション メソッドを更新できます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-146">We can then update our Edit() action method to create the DinnerFormViewModel using the Dinner object we retrieve from our repository, and then pass it to our view template:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

<span data-ttu-id="ed72b-147">次に、edit.aspx ページの上部にある "inherits" 属性を次のように変更して、"Dinner" オブジェクトの代わりに "DinnerFormViewModel" を期待するようにビュー テンプレートを更新します。</span><span class="sxs-lookup"><span data-stu-id="ed72b-147">We'll then update our view template so that it expects a "DinnerFormViewModel" instead of a "Dinner" object by changing the "inherits" attribute at the top of the edit.aspx page like so:</span></span>

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

<span data-ttu-id="ed72b-148">これを行うと、ビュー テンプレート内の "モデル" プロパティのインテリセンスが更新され、それを渡す DinnerFormViewModel 型のオブジェクト モデルが反映されます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-148">Once we do this, the intellisense of the "Model" property within our view template will be updated to reflect the object model of the DinnerFormViewModel type we are passing it:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

<span data-ttu-id="ed72b-149">その後、ビューコードを更新して動作を回避できます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-149">We can then update our view code to work off of it.</span></span> <span data-ttu-id="ed72b-150">作成している入力要素の名前を変更しない方法に注目してください (フォーム要素は"Title","Country"という名前になります) - しかし、私たちは、DinnerFormViewModelクラスを使用して値を取得するためにHTMLヘルパーメソッドを更新しています。</span><span class="sxs-lookup"><span data-stu-id="ed72b-150">Notice below how we are not changing the names of the input elements we are creating (the form elements will still be named "Title", "Country") – but we are updating the HTML Helper methods to retrieve the values using the DinnerFormViewModel class:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

<span data-ttu-id="ed72b-151">また、エラーをレンダリングするときに DinnerFormViewModel クラスを使用するように、編集ポスト メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="ed72b-151">We'll also update our Edit post method to use the DinnerFormViewModel class when rendering errors:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

<span data-ttu-id="ed72b-152">また、Create() アクションメソッドを更新して、まったく同じ*DinnerFormViewModel*クラスを再利用して、それらの中の国々のドロップダウンリストを有効にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-152">We can also update our Create() action methods to re-use the exact same *DinnerFormViewModel* class to enable the countries DropDownList within those as well.</span></span> <span data-ttu-id="ed72b-153">以下は HTTP-GET の実装です。</span><span class="sxs-lookup"><span data-stu-id="ed72b-153">Below is the HTTP-GET implementation:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

<span data-ttu-id="ed72b-154">以下は HTTP-POST Create メソッドの実装です。</span><span class="sxs-lookup"><span data-stu-id="ed72b-154">Below is the implementation of the HTTP-POST Create method:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

<span data-ttu-id="ed72b-155">そして今、私たちの編集画面と作成画面の両方が国を選ぶためのドロップダウンリストをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ed72b-155">And now both our Edit and Create screens support drop-downlists for picking the country.</span></span>

### <a name="custom-shaped-viewmodel-classes"></a><span data-ttu-id="ed72b-156">カスタムシェイプのビューモデル クラス</span><span class="sxs-lookup"><span data-stu-id="ed72b-156">Custom-shaped ViewModel classes</span></span>

<span data-ttu-id="ed72b-157">上のシナリオでは、クラスは、サポートする SelectList モデル プロパティと共に、Dinner モデル オブジェクトをプロパティとして直接公開します。</span><span class="sxs-lookup"><span data-stu-id="ed72b-157">In the scenario above, our DinnerFormViewModel class directly exposes the Dinner model object as a property, along with a supporting SelectList model property.</span></span> <span data-ttu-id="ed72b-158">この方法は、ビュー テンプレート内に作成する HTML UI がドメイン モデル オブジェクトに比較的近い場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="ed72b-158">This approach works fine for scenarios where the HTML UI we want to create within our view template corresponds relatively closely to our domain model objects.</span></span>

<span data-ttu-id="ed72b-159">この場合に該当しないシナリオでは、オブジェクト モデルがビューで使用できるように最適化され、基になるドメイン モデル オブジェクトとはまったく異なる可能性があるカスタムシェイプの ViewModel クラスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-159">For scenarios where this isn't the case, one option that you can use is to create a custom-shaped ViewModel class whose object model is more optimized for consumption by the view – and which might look completely different from the underlying domain model object.</span></span> <span data-ttu-id="ed72b-160">たとえば、複数のモデル オブジェクトから収集されたプロパティ名や集計プロパティを公開する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ed72b-160">For example, it could potentially expose different property names and/or aggregate properties collected from multiple model objects.</span></span>

<span data-ttu-id="ed72b-161">カスタムシェイプの ViewModel クラスは、コントローラーからビューにデータを渡してレンダリングするために使用できるほか、コントローラーのアクション メソッドにポストバックされたフォーム データを処理するのにも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-161">Custom-shaped ViewModel classes can be used both to pass data from controllers to views to render, as well as to help handle form data posted back to a controller's action method.</span></span> <span data-ttu-id="ed72b-162">この後のシナリオでは、アクション メソッドで、フォームポストデータを使用して ViewModel オブジェクトを更新し、ViewModel インスタンスを使用して、実際のドメイン モデル オブジェクトをマップまたは取得する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ed72b-162">For this later scenario, you might have the action method update a ViewModel object with the form-posted data, and then use the ViewModel instance to map or retrieve an actual domain model object.</span></span>

<span data-ttu-id="ed72b-163">カスタムシェイプの ViewModel クラスは、柔軟性を高めることができ、ビュー テンプレート内のレンダリング コードやアクション メソッド内のフォームポスト コードが複雑になりすぎる場合に、いつでも調べることができます。</span><span class="sxs-lookup"><span data-stu-id="ed72b-163">Custom-shaped ViewModel classes can provide a great deal of flexibility, and are something to investigate any time you find the rendering code within your view templates or the form-posting code inside your action methods starting to get too complicated.</span></span> <span data-ttu-id="ed72b-164">これは、多くの場合、ドメイン モデルが生成する UI に明確に対応していない、および中間のカスタム型の ViewModel クラスが役立つという兆候です。</span><span class="sxs-lookup"><span data-stu-id="ed72b-164">This is often a sign that your domain models don't cleanly correspond to the UI you are generating, and that an intermediate custom-shaped ViewModel class can help.</span></span>

### <a name="next-step"></a><span data-ttu-id="ed72b-165">次の手順</span><span class="sxs-lookup"><span data-stu-id="ed72b-165">Next Step</span></span>

<span data-ttu-id="ed72b-166">ここでは、パーシャルページとマスターページを使用して、アプリケーション全体で UI を再利用して共有する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="ed72b-166">Let's now look at how we can use partials and master-pages to re-use and share UI across our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ed72b-167">[前へ](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [次へ](re-use-ui-using-master-pages-and-partials.md)</span><span class="sxs-lookup"><span data-stu-id="ed72b-167">[Previous](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Next](re-use-ui-using-master-pages-and-partials.md)</span></span>
