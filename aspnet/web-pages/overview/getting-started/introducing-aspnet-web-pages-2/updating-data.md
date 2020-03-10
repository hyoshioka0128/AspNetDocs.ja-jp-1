---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: ASP.NET Web ページの概要-データベースデータの更新 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、ASP.NET Web ページ (Razor) を使用するときに既存のデータベースエントリを更新 (変更) する方法について説明します。 ここでは、系列を完了していることを前提としています...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: 8f8bcfb7d9d2416a2699776cadbdaae8e12415ba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463492"
---
# <a name="introducing-aspnet-web-pages---updating-database-data"></a><span data-ttu-id="82a53-104">ASP.NET Web ページの概要-データベースデータの更新</span><span class="sxs-lookup"><span data-stu-id="82a53-104">Introducing ASP.NET Web Pages - Updating Database Data</span></span>

<span data-ttu-id="82a53-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="82a53-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="82a53-106">このチュートリアルでは、ASP.NET Web ページ (Razor) を使用するときに既存のデータベースエントリを更新 (変更) する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="82a53-106">This tutorial shows you how to update (change) an existing database entry when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="82a53-107">[ASP.NET Web ページを使用してフォームを使用](entering-data.md)してデータを入力することによって、シリーズを完了していると想定しています。</span><span class="sxs-lookup"><span data-stu-id="82a53-107">It assumes you have completed the series through [Entering Data by Using Forms Using ASP.NET Web Pages](entering-data.md).</span></span>
> 
> <span data-ttu-id="82a53-108">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="82a53-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="82a53-109">`WebGrid` ヘルパーで個々のレコードを選択する方法。</span><span class="sxs-lookup"><span data-stu-id="82a53-109">How to select an individual record in the `WebGrid` helper.</span></span>
> - <span data-ttu-id="82a53-110">データベースから1つのレコードを読み取る方法。</span><span class="sxs-lookup"><span data-stu-id="82a53-110">How to read a single record from a database.</span></span>
> - <span data-ttu-id="82a53-111">データベースレコードの値を使用してフォームをプリロードする方法。</span><span class="sxs-lookup"><span data-stu-id="82a53-111">How to preload a form with values from the database record.</span></span>
> - <span data-ttu-id="82a53-112">データベース内の既存のレコードを更新する方法。</span><span class="sxs-lookup"><span data-stu-id="82a53-112">How to update an existing record in a database.</span></span>
> - <span data-ttu-id="82a53-113">ページに情報を表示せずに保存する方法。</span><span class="sxs-lookup"><span data-stu-id="82a53-113">How to store information in the page without displaying it.</span></span>
> - <span data-ttu-id="82a53-114">隠しフィールドを使用して情報を格納する方法。</span><span class="sxs-lookup"><span data-stu-id="82a53-114">How to use a hidden field to store information.</span></span>
>   
> 
> <span data-ttu-id="82a53-115">説明する機能/テクノロジ:</span><span class="sxs-lookup"><span data-stu-id="82a53-115">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="82a53-116">`WebGrid` ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="82a53-116">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="82a53-117">SQL `Update` コマンド。</span><span class="sxs-lookup"><span data-stu-id="82a53-117">The SQL `Update` command.</span></span>
> - <span data-ttu-id="82a53-118">`Database.Execute` メソッド。</span><span class="sxs-lookup"><span data-stu-id="82a53-118">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="82a53-119">隠しフィールド (`<input type="hidden">`)。</span><span class="sxs-lookup"><span data-stu-id="82a53-119">Hidden fields (`<input type="hidden">`).</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="82a53-120">作成するアプリケーション:</span><span class="sxs-lookup"><span data-stu-id="82a53-120">What You'll Build</span></span>

<span data-ttu-id="82a53-121">前のチュートリアルでは、データベースにレコードを追加する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="82a53-121">In the previous tutorial, you learned how to add a record to a database.</span></span> <span data-ttu-id="82a53-122">ここでは、編集のためにレコードを表示する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="82a53-122">Here, you'll learn how to display a record for editing.</span></span> <span data-ttu-id="82a53-123">[*ムービー* ] ページで、`WebGrid` ヘルパーを更新して、各ムービーの横に **[編集]** リンクが表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="82a53-123">In the *Movies* page, you'll update the `WebGrid` helper so that it displays an **Edit** link next to each movie:</span></span>

![各ムービーの ' Edit ' リンクを含む WebGrid 表示](updating-data/_static/image1.png)

<span data-ttu-id="82a53-125">**[編集]** リンクをクリックすると、次のような別のページに移動します。このページでは、ムービー情報が既にフォームに含まれています。</span><span class="sxs-lookup"><span data-stu-id="82a53-125">When you click the **Edit** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![編集するムービーを表示するムービーページを編集する](updating-data/_static/image2.png)

<span data-ttu-id="82a53-127">任意の値を変更できます。</span><span class="sxs-lookup"><span data-stu-id="82a53-127">You can change any of the values.</span></span> <span data-ttu-id="82a53-128">変更を送信すると、ページ内のコードによってデータベースが更新され、ムービーの一覧に戻ります。</span><span class="sxs-lookup"><span data-stu-id="82a53-128">When you submit the changes, the code in the page updates the database and takes you back to the movie listing.</span></span>

<span data-ttu-id="82a53-129">プロセスのこの部分は、前のチュートリアルで作成した*Addmovie. cshtml*ページとほぼ同じように動作するため、このチュートリアルの多くは使い慣れています。</span><span class="sxs-lookup"><span data-stu-id="82a53-129">This part of the process works almost exactly like the *AddMovie.cshtml* page you created in the previous tutorial, so much of this tutorial will be familiar.</span></span>

<span data-ttu-id="82a53-130">個々のムービーを編集する方法を実装するには、いくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="82a53-130">There are several ways you could implement a way to edit an individual movie.</span></span> <span data-ttu-id="82a53-131">この方法は、実装が簡単でわかりやすいために選択されています。</span><span class="sxs-lookup"><span data-stu-id="82a53-131">The approach shown was chosen because it's easy to implement and easy to understand.</span></span>

## <a name="adding-an-edit-link-to-the-movie-listing"></a><span data-ttu-id="82a53-132">ムービーの一覧への編集リンクの追加</span><span class="sxs-lookup"><span data-stu-id="82a53-132">Adding an Edit Link to the Movie Listing</span></span>

<span data-ttu-id="82a53-133">まず、ムービーの一覧に **[編集]** リンクが含まれるように、*ムービーページを*更新します。</span><span class="sxs-lookup"><span data-stu-id="82a53-133">To begin, you'll update the *Movies* page so that each movie listing also contains an **Edit** link.</span></span>

<span data-ttu-id="82a53-134">ムービーの*cshtml*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="82a53-134">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="82a53-135">ページの本文で、列を追加して `WebGrid` マークアップを変更します。</span><span class="sxs-lookup"><span data-stu-id="82a53-135">In the body of the page, change the `WebGrid` markup by adding a column.</span></span> <span data-ttu-id="82a53-136">変更されたマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="82a53-136">Here's the modified markup:</span></span>

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

<span data-ttu-id="82a53-137">新しい列は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="82a53-137">The new column is this one:</span></span>

[!code-html[Main](updating-data/samples/sample2.html)]

<span data-ttu-id="82a53-138">この列のポイントは、"Edit" というテキストを持つリンク (`<a>` 要素) を表示することです。</span><span class="sxs-lookup"><span data-stu-id="82a53-138">The point of this column is to show a link (`<a>` element) whose text says "Edit".</span></span> <span data-ttu-id="82a53-139">次の例では、ページの実行時に次のようなリンクを作成しています。ムービーごとに `id` 値が異なります。</span><span class="sxs-lookup"><span data-stu-id="82a53-139">What we're after is to create a link that looks like the following when the page runs, with the `id` value different for each movie:</span></span>

[!code-css[Main](updating-data/samples/sample3.css)]

<span data-ttu-id="82a53-140">このリンクを実行すると、 *Editmovie*という名前のページが呼び出され、そのページに `?id=7` クエリ文字列が渡されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-140">This link will invoke a page named *EditMovie*, and it will pass the query string `?id=7` to that page.</span></span>

<span data-ttu-id="82a53-141">新しい列の構文は少し複雑に見えるかもしれませんが、複数の要素が組み合わされているためです。</span><span class="sxs-lookup"><span data-stu-id="82a53-141">The syntax for the new column might look a bit complex, but that's only because it puts together several elements.</span></span> <span data-ttu-id="82a53-142">個々の要素は単純です。</span><span class="sxs-lookup"><span data-stu-id="82a53-142">Each individual element is straightforward.</span></span> <span data-ttu-id="82a53-143">`<a>` 要素のみに専念する場合は、次のマークアップが表示されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-143">If you concentrate on just the `<a>` element, you see this markup:</span></span>

[!code-html[Main](updating-data/samples/sample4.html)]

<span data-ttu-id="82a53-144">グリッドの動作についての背景がいくつかあります。グリッドには、各データベースレコードに対して1つずつ行が表示され、データベースレコードの各フィールドの列が表示されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-144">Some background about how the grid works: the grid displays rows, one for each database record, and it displays columns for each field in the database record.</span></span> <span data-ttu-id="82a53-145">各グリッド行が構築されている間、`item` オブジェクトには、その行のデータベースレコード (項目) が格納されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-145">While each grid row is being constructed, the `item` object contains the database record (item) for that row.</span></span> <span data-ttu-id="82a53-146">このように配置することにより、コードでその行のデータを取得できます。</span><span class="sxs-lookup"><span data-stu-id="82a53-146">This arrangement gives you a way in code to get at the data for that row.</span></span> <span data-ttu-id="82a53-147">ここに表示されているのは、現在のデータベース項目の ID 値を取得している `item.ID` 式です。</span><span class="sxs-lookup"><span data-stu-id="82a53-147">That's what you see here: the expression `item.ID` is getting the ID value of the current database item.</span></span> <span data-ttu-id="82a53-148">`item.Title`、`item.Genre`、または `item.Year`を使用すると、データベースの値 (タイトル、ジャンル、または年) を同じ方法で取得できます。</span><span class="sxs-lookup"><span data-stu-id="82a53-148">You could get any of the database values (title, genre, or year) the same way by using `item.Title`, `item.Genre`, or `item.Year`.</span></span>

<span data-ttu-id="82a53-149">式 `"~/EditMovie?id=@item.ID` は、ターゲット URL (`~/EditMovie?id=`) のハードコーディングされた部分をこの動的な派生 ID と結合します。</span><span class="sxs-lookup"><span data-stu-id="82a53-149">The expression `"~/EditMovie?id=@item.ID` combines the hard-coded part of the target URL (`~/EditMovie?id=`) with this dynamically derived ID.</span></span> <span data-ttu-id="82a53-150">(前のチュートリアルでは `~` 演算子を見ました。これは現在の web サイトルートを表す ASP.NET 演算子です)。</span><span class="sxs-lookup"><span data-stu-id="82a53-150">(You saw the `~` operator in the previous tutorial; it's an ASP.NET operator that represents the current website root.)</span></span>

<span data-ttu-id="82a53-151">結果として、列のマークアップのこの部分は、実行時に次のマークアップのようなものを生成するだけです。</span><span class="sxs-lookup"><span data-stu-id="82a53-151">The result is that this part of the markup in the column simply produces something like the following markup at run time:</span></span>

[!code-xml[Main](updating-data/samples/sample5.xml)]

<span data-ttu-id="82a53-152">当然ながら、`id` の実際の値は、行ごとに異なります。</span><span class="sxs-lookup"><span data-stu-id="82a53-152">Naturally, the actual value of `id` will be different for each row.</span></span>

## <a name="creating-a-custom-display-for-a-grid-column"></a><span data-ttu-id="82a53-153">グリッド列のカスタム表示の作成</span><span class="sxs-lookup"><span data-stu-id="82a53-153">Creating a Custom Display for a Grid Column</span></span>

<span data-ttu-id="82a53-154">ここで、グリッド列に戻ります。</span><span class="sxs-lookup"><span data-stu-id="82a53-154">Now back to the grid column.</span></span> <span data-ttu-id="82a53-155">グリッドに最初に使用した3つの列には、データ値 (タイトル、ジャンル、および年) のみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-155">The three columns you originally had in the grid displayed only data values (title, genre, and year).</span></span> <span data-ttu-id="82a53-156">この表示を指定するには、データベースの列の名前 &mdash; `grid.Column("Title")`のように指定します。</span><span class="sxs-lookup"><span data-stu-id="82a53-156">You specified this display by passing the name of the database column &mdash; for example, `grid.Column("Title")`.</span></span>

<span data-ttu-id="82a53-157">この新しい リンクの**編集**」列は異なります。</span><span class="sxs-lookup"><span data-stu-id="82a53-157">This new **Edit** link column is different.</span></span> <span data-ttu-id="82a53-158">列名を指定する代わりに、`format` パラメーターを渡します。</span><span class="sxs-lookup"><span data-stu-id="82a53-158">Instead of specifying a column name, you're passing a `format` parameter.</span></span> <span data-ttu-id="82a53-159">このパラメーターを使用すると、`WebGrid` ヘルパーがレンダリングするマークアップと `item` の値を定義して、列のデータを太字または緑または任意の形式で表示できます。</span><span class="sxs-lookup"><span data-stu-id="82a53-159">This parameter lets you define markup that the `WebGrid` helper will render along with the `item` value to display the column data as bold or green or in whatever format that you want.</span></span> <span data-ttu-id="82a53-160">たとえば、タイトルを太字で表示したい場合は、次の例のような列を作成できます。</span><span class="sxs-lookup"><span data-stu-id="82a53-160">For example, if you wanted the title to appear bold, you could create a column like this example:</span></span>

[!code-html[Main](updating-data/samples/sample6.html)]

<span data-ttu-id="82a53-161">(`format` のプロパティに表示されるさまざまな `@` 文字は、マークアップとコード値の間の切り替えをマークします)。</span><span class="sxs-lookup"><span data-stu-id="82a53-161">(The various `@` characters you see in the `format` property mark the transition between markup and a code value.)</span></span>

<span data-ttu-id="82a53-162">`format` プロパティについて理解すると、新しい [リンクの**編集**] 列がどのように組み合わされているかを理解しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="82a53-162">Once you know about the `format` property, it's easier to understand how the new **Edit** link column is put together:</span></span>

[!code-html[Main](updating-data/samples/sample7.html)]

<span data-ttu-id="82a53-163">この列は、リンクを表示するマークアップと、その行のデータベースレコードから抽出された情報 (ID)*だけ*で構成されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-163">The column consists *only* of the markup that renders the link, plus some information (the ID) that's extracted from the database record for the row.</span></span>

> [!TIP]
> 
> <span data-ttu-id="82a53-164">**メソッドの名前付きパラメーターと位置指定パラメーター**</span><span class="sxs-lookup"><span data-stu-id="82a53-164">**Named Parameters and Positional Parameters for a Method**</span></span>
> 
> <span data-ttu-id="82a53-165">メソッドを呼び出してパラメーターを渡すと、何度もパラメーター値がコンマで区切られて表示されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-165">Many times when you've called a method and passed parameters to it, you've simply listed the parameter values separated by commas.</span></span> <span data-ttu-id="82a53-166">いくつかの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="82a53-166">Here are a couple of examples:</span></span>
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> <span data-ttu-id="82a53-167">この問題については、最初にこのコードを見たときには説明しませんでしたが、いずれの場合も、パラメーターを特定の順序でメソッドに渡すことになります。つまり、そのメソッドでパラメーターが定義されている順序 &mdash; ます。</span><span class="sxs-lookup"><span data-stu-id="82a53-167">We didn't mention the issue when you first saw this code, but in each case, you're passing parameters to the methods in a specific order &mdash; namely, the order in which the parameters are defined in that method.</span></span> <span data-ttu-id="82a53-168">`db.Execute` と `Validation.RequireFields`の場合、渡す値の順序を組み合わせると、ページの実行時にエラーメッセージが表示されます。または、少なくとも奇妙な結果が返されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-168">For `db.Execute` and `Validation.RequireFields`, if you mixed up the order of the values you pass, you'd get an error message when the page runs, or at least some strange results.</span></span> <span data-ttu-id="82a53-169">具体的には、パラメーターを渡す順序を把握しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="82a53-169">Clearly, you have to know the order to pass the parameters in.</span></span> <span data-ttu-id="82a53-170">(WebMatrix では、IntelliSense を使用して、パラメーターの名前、型、および順序を理解することができます)。</span><span class="sxs-lookup"><span data-stu-id="82a53-170">(In WebMatrix, IntelliSense can help you learn figure out the name, type, and order of the parameters.)</span></span>
> 
> <span data-ttu-id="82a53-171">値を順番に渡す代わりに、*名前付きパラメーター*を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="82a53-171">As an alternative to passing values in order, you can use *named parameters*.</span></span> <span data-ttu-id="82a53-172">(パラメーターを順序どおりに渡すことは、*位置指定パラメーター*を使用すると呼ばれます)。名前付きパラメーターの場合は、その値を渡すときに、パラメーターの名前を明示的に指定します。</span><span class="sxs-lookup"><span data-stu-id="82a53-172">(Passing parameters in order is known as using *positional parameters*.) For named parameters, you explicitly include the name of the parameter when passing its value.</span></span> <span data-ttu-id="82a53-173">これらのチュートリアルでは、既に複数の名前付きパラメーターを使用しています。</span><span class="sxs-lookup"><span data-stu-id="82a53-173">You've used named parameters already a number of times in these tutorials.</span></span> <span data-ttu-id="82a53-174">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="82a53-174">For example:</span></span>
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> <span data-ttu-id="82a53-175">and</span><span class="sxs-lookup"><span data-stu-id="82a53-175">and</span></span>
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> <span data-ttu-id="82a53-176">名前付きパラメーターは、いくつかの状況で便利です。特に、メソッドが多数のパラメーターを受け取る場合です。</span><span class="sxs-lookup"><span data-stu-id="82a53-176">Named parameters are handy for a couple of situations, especially when a method takes many parameters.</span></span> <span data-ttu-id="82a53-177">1つまたは2つのパラメーターのみを渡す必要があるが、渡す値がパラメーターリスト内の最初の位置に含まれていない場合です。</span><span class="sxs-lookup"><span data-stu-id="82a53-177">One is when you want to pass only one or two parameters, but the values you want to pass are not among the first positions in the parameter list.</span></span> <span data-ttu-id="82a53-178">もう1つの状況は、ユーザーにとって最も意味のある順序でパラメーターを渡すことにより、コードを読みやすくすることです。</span><span class="sxs-lookup"><span data-stu-id="82a53-178">Another situation is when you want to make your code more readable by passing the parameters in the order that makes the most sense to you.</span></span>
> 
> <span data-ttu-id="82a53-179">名前付きパラメーターを使用するには、パラメーターの名前を把握しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="82a53-179">Obviously, to use named parameters, you have to know the names of the parameters.</span></span> <span data-ttu-id="82a53-180">WebMatrix IntelliSense では名前が*表示*されますが、現在はそれらを入力することはできません。</span><span class="sxs-lookup"><span data-stu-id="82a53-180">WebMatrix IntelliSense can *show* you the names, but it cannot currently fill them in for you.</span></span>

## <a name="creating-the-edit-page"></a><span data-ttu-id="82a53-181">編集ページの作成</span><span class="sxs-lookup"><span data-stu-id="82a53-181">Creating the Edit Page</span></span>

<span data-ttu-id="82a53-182">これで、 *Editmovie*ページを作成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="82a53-182">Now you can create the *EditMovie* page.</span></span> <span data-ttu-id="82a53-183">ユーザーが **[編集]** リンクをクリックすると、このページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-183">When users click the **Edit** link, they'll end up on this page.</span></span>

<span data-ttu-id="82a53-184">*Editmovie*という名前のページを作成し、ファイルの内容を次のマークアップに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="82a53-184">Create a page named *EditMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

<span data-ttu-id="82a53-185">このマークアップとコードは、 *Addmovie*ページと似ています。</span><span class="sxs-lookup"><span data-stu-id="82a53-185">This markup and code is similar to what you have in the *AddMovie* page.</span></span> <span data-ttu-id="82a53-186">[送信] ボタンのテキストには若干の違いがあります。</span><span class="sxs-lookup"><span data-stu-id="82a53-186">There's a small difference in the text for the submit button.</span></span> <span data-ttu-id="82a53-187">*Addmovie*ページと同様に、`Html.ValidationSummary` の呼び出しによって検証エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-187">As with the *AddMovie* page, there's an `Html.ValidationSummary` call that will display validation errors if there are any.</span></span> <span data-ttu-id="82a53-188">ここでは、エラーが検証の概要に表示されるため、`Validation.Message`を呼び出すことはありません。</span><span class="sxs-lookup"><span data-stu-id="82a53-188">This time we're leaving out calls to `Validation.Message`, since errors will be displayed in the validation summary.</span></span> <span data-ttu-id="82a53-189">前のチュートリアルで説明したように、さまざまな組み合わせで検証の概要と個々のエラーメッセージを使用できます。</span><span class="sxs-lookup"><span data-stu-id="82a53-189">As noted in the previous tutorial, you can use the validation summary and the individual error messages in various combinations.</span></span>

<span data-ttu-id="82a53-190">`<form>` 要素の `method` 属性が `post`に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="82a53-190">Notice again that the `method` attribute of the `<form>` element is set to `post`.</span></span> <span data-ttu-id="82a53-191">*Addmovie. cshtml*ページと同様に、このページではデータベースを変更します。</span><span class="sxs-lookup"><span data-stu-id="82a53-191">As with the *AddMovie.cshtml* page, this page makes changes to the database.</span></span> <span data-ttu-id="82a53-192">したがって、このフォームでは `POST` 操作を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="82a53-192">Therefore, this form should perform a `POST` operation.</span></span> <span data-ttu-id="82a53-193">(`GET` 操作と `POST` 操作の違いの詳細については、HTML フォームに関するチュートリアルの「 [GET、POST、および HTTP 動詞の安全性](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety)に関する補足記事」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="82a53-193">(For more about the difference between `GET` and `POST` operations, see the [GET, POST, and HTTP Verb Safety](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the tutorial on HTML forms.)</span></span>

<span data-ttu-id="82a53-194">前のチュートリアルで見たように、テキストボックスの `value` 属性は、事前にプリロードするために Razor コードで設定されています。</span><span class="sxs-lookup"><span data-stu-id="82a53-194">As you saw in an earlier tutorial, the `value` attributes of the text boxes are being set with Razor code in order to preload them.</span></span> <span data-ttu-id="82a53-195">ここでは、`Request.Form["title"]`ではなく、そのタスクに対して `title` や `genre` などの変数を使用しています。</span><span class="sxs-lookup"><span data-stu-id="82a53-195">This time, though, you're using variables like `title` and `genre` for that task instead of `Request.Form["title"]`:</span></span>

`<input type="text" name="title" value="@title" />`

<span data-ttu-id="82a53-196">前と同様に、このマークアップによってテキストボックスの値がムービーの値で読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="82a53-196">As before, this markup will preload the text box values with the movie values.</span></span> <span data-ttu-id="82a53-197">この時点では、`Request` オブジェクトを使用する代わりに、変数を使用すると便利です。</span><span class="sxs-lookup"><span data-stu-id="82a53-197">You'll see in a moment why it's handy to use variables this time instead of using the `Request` object.</span></span>

<span data-ttu-id="82a53-198">このページには `<input type="hidden">` 要素もあります。</span><span class="sxs-lookup"><span data-stu-id="82a53-198">There's also a `<input type="hidden">` element on this page.</span></span> <span data-ttu-id="82a53-199">この要素には、ページに表示されることなくムービー ID が格納されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-199">This element stores the movie ID without making it visible on the page.</span></span> <span data-ttu-id="82a53-200">ID が最初にページに渡されるのは、クエリ文字列の値 (`?id=7` または URL に似ています) を使用しています。</span><span class="sxs-lookup"><span data-stu-id="82a53-200">The ID is initially passed to the page by using a query string value (`?id=7` or similar in the URL).</span></span> <span data-ttu-id="82a53-201">ID 値を隠しフィールドに設定すると、そのページが呼び出された元の URL にアクセスできなくなった場合でも、フォームが送信されたときに使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="82a53-201">By putting the ID value into a hidden field, you can make sure that it's available when the form is submitted, even if you no longer have access to the original URL that the page was invoked with.</span></span>

<span data-ttu-id="82a53-202">*Addmovie*ページとは異なり、 *editmovie*ページのコードには、2つの異なる関数があります。</span><span class="sxs-lookup"><span data-stu-id="82a53-202">Unlike the *AddMovie* page, the code for the *EditMovie* page has two distinct functions.</span></span> <span data-ttu-id="82a53-203">最初の関数は、ページが初めて表示されるとき (その後*のみ*)、コードがクエリ文字列からムービー ID を取得することです。</span><span class="sxs-lookup"><span data-stu-id="82a53-203">The first function is that when the page is displayed for the first time (and *only* then), the code gets the movie ID from the query string.</span></span> <span data-ttu-id="82a53-204">次に、ID を使用して、対応するムービーをデータベースから読み取り、テキストボックスに表示 (プリロード) します。</span><span class="sxs-lookup"><span data-stu-id="82a53-204">The code then uses the ID to read the corresponding movie out of the database and display (preload) it in the text boxes.</span></span>

<span data-ttu-id="82a53-205">2番目の関数は、ユーザーが **[変更の送信]** ボタンをクリックしたときに、コードがテキストボックスの値を読み取って検証する必要があることです。</span><span class="sxs-lookup"><span data-stu-id="82a53-205">The second function is that when the user clicks the **Submit Changes** button, the code has to read the values of the text boxes and validate them.</span></span> <span data-ttu-id="82a53-206">このコードでは、データベース項目を新しい値で更新する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="82a53-206">The code also has to update the database item with the new values.</span></span> <span data-ttu-id="82a53-207">この手法は、 *Addmovie*で見たように、レコードを追加することと似ています。</span><span class="sxs-lookup"><span data-stu-id="82a53-207">This technique is similar to adding a record, as you saw in *AddMovie*.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="82a53-208">1つのムービーを読み取るコードを追加する</span><span class="sxs-lookup"><span data-stu-id="82a53-208">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="82a53-209">最初の関数を実行するには、次のコードをページの先頭に追加します。</span><span class="sxs-lookup"><span data-stu-id="82a53-209">To perform the first function, add this code to the top of the page:</span></span>

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

<span data-ttu-id="82a53-210">このコードのほとんどは、`if(!IsPost)`を開始するブロック内にあります。</span><span class="sxs-lookup"><span data-stu-id="82a53-210">Most of this code is inside a block that starts `if(!IsPost)`.</span></span> <span data-ttu-id="82a53-211">`!` 演算子は "not" を意味します。したがって、この*要求が post 送信*ではないことを意味します。これは、この要求がこの*ページが初めて実行されたときにこの要求が行われたかどうか*を示す間接的な方法です。</span><span class="sxs-lookup"><span data-stu-id="82a53-211">The `!` operator means "not," so the expression means *if this request is not a post submission*, which is an indirect way of saying *if this request is the first time that this page has been run*.</span></span> <span data-ttu-id="82a53-212">前述のように、このコードはページを初めて実行するときに*のみ*実行してください。</span><span class="sxs-lookup"><span data-stu-id="82a53-212">As noted earlier, this code should run *only* the first time the page runs.</span></span> <span data-ttu-id="82a53-213">コードを `if(!IsPost)`で囲まなかった場合は、最初にページが呼び出されるたびに、またはボタンのクリックに応答して実行されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-213">If you didn't enclose the code in `if(!IsPost)`, it would run every time the page is invoked, whether the first time or in response to a button click.</span></span>

<span data-ttu-id="82a53-214">このコードには `else` ブロックが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="82a53-214">Notice that the code includes an `else` block this time.</span></span> <span data-ttu-id="82a53-215">前述したように、`if` ブロックを導入したときに、テストしている条件が満たされない場合は、代替コードを実行することが必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="82a53-215">As we said when we introduced `if` blocks, sometimes you want to run alternative code if the condition you're testing isn't true.</span></span> <span data-ttu-id="82a53-216">ここで説明します。</span><span class="sxs-lookup"><span data-stu-id="82a53-216">That's the case here.</span></span> <span data-ttu-id="82a53-217">条件が成功した場合 (つまり、ページに渡された ID が ok である場合)、データベースから行を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="82a53-217">If the condition passes (that is, if the ID passed to the page is ok), you read a row from the database.</span></span> <span data-ttu-id="82a53-218">ただし、条件が合格しなかった場合は、`else` ブロックが実行され、コードによってエラーメッセージが設定されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-218">However, if the condition doesn't pass, the `else` block runs and the code sets an error message.</span></span>

## <a name="validating-a-value-passed-to-the-page"></a><span data-ttu-id="82a53-219">ページに渡された値を検証しています</span><span class="sxs-lookup"><span data-stu-id="82a53-219">Validating a Value Passed to the Page</span></span>

<span data-ttu-id="82a53-220">このコードでは、`Request.QueryString["id"]` を使用して、ページに渡される ID を取得します。</span><span class="sxs-lookup"><span data-stu-id="82a53-220">The code uses `Request.QueryString["id"]` to get the ID that's passed to the page.</span></span> <span data-ttu-id="82a53-221">コードを使用すると、ID に対して実際に値が渡されたことを確認できます。</span><span class="sxs-lookup"><span data-stu-id="82a53-221">The code makes sure that a value was actually passed for the ID.</span></span> <span data-ttu-id="82a53-222">値が渡されなかった場合、コードは検証エラーを設定します。</span><span class="sxs-lookup"><span data-stu-id="82a53-222">If no value was passed, the code sets a validation error.</span></span>

<span data-ttu-id="82a53-223">このコードは、情報を検証する別の方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="82a53-223">This code shows a different way to validate information.</span></span> <span data-ttu-id="82a53-224">前のチュートリアルでは、`Validation` ヘルパーを使用しました。</span><span class="sxs-lookup"><span data-stu-id="82a53-224">In the previous tutorial, you worked with the `Validation` helper.</span></span> <span data-ttu-id="82a53-225">検証するためのフィールドが登録されており、`Html.ValidationMessage` と `Html.ValidationSummary`を使用して、検証エラーと表示エラーが自動的に ASP.NET されました。</span><span class="sxs-lookup"><span data-stu-id="82a53-225">You registered fields to validate, and ASP.NET automatically did the validation and displayed errors by using `Html.ValidationMessage` and `Html.ValidationSummary`.</span></span> <span data-ttu-id="82a53-226">ただし、この例では、ユーザー入力を実際には検証していません。</span><span class="sxs-lookup"><span data-stu-id="82a53-226">In this case, however, you're not really validating user input.</span></span> <span data-ttu-id="82a53-227">代わりに、他の場所からページに渡された値を検証しています。</span><span class="sxs-lookup"><span data-stu-id="82a53-227">Instead, you're validating a value that was passed to the page from elsewhere.</span></span> <span data-ttu-id="82a53-228">`Validation` ヘルパーはこれを行いません。</span><span class="sxs-lookup"><span data-stu-id="82a53-228">The `Validation` helper doesn't do that for you.</span></span>

<span data-ttu-id="82a53-229">そのため、`if(!Request.QueryString["ID"].IsEmpty()`でテストして、自分で値を確認します。</span><span class="sxs-lookup"><span data-stu-id="82a53-229">Therefore, you check the value yourself, by testing it with `if(!Request.QueryString["ID"].IsEmpty()`).</span></span> <span data-ttu-id="82a53-230">問題が発生した場合は、`Validation` ヘルパーの場合と同様に、`Html.ValidationSummary`を使用してエラーを表示できます。</span><span class="sxs-lookup"><span data-stu-id="82a53-230">If there's a problem, you can display the error by using `Html.ValidationSummary`, as you did with the `Validation` helper.</span></span> <span data-ttu-id="82a53-231">これを行うには、`Validation.AddFormError` を呼び出し、表示するメッセージを渡します。</span><span class="sxs-lookup"><span data-stu-id="82a53-231">To do that, you call `Validation.AddFormError` and pass it a message to display.</span></span> <span data-ttu-id="82a53-232">`Validation.AddFormError` は、既に使い慣れている検証システムに関連付けられたカスタムメッセージを定義できる組み込みのメソッドです。</span><span class="sxs-lookup"><span data-stu-id="82a53-232">`Validation.AddFormError` is a built-in method that lets you define custom messages that tie in with the validation system you're already familiar with.</span></span> <span data-ttu-id="82a53-233">(このチュートリアルの後半で、この検証プロセスをもう少し堅牢にする方法について説明します)。</span><span class="sxs-lookup"><span data-stu-id="82a53-233">(Later in this tutorial we'll talk about how to make this validation process a little more robust.)</span></span>

<span data-ttu-id="82a53-234">ムービーの ID があることを確認した後、コードはデータベースを読み取り、データベースアイテムを1つだけ探します。</span><span class="sxs-lookup"><span data-stu-id="82a53-234">After making sure that there's an ID for the movie, the code reads the database, looking for only a single database item.</span></span> <span data-ttu-id="82a53-235">(データベースの操作の一般的なパターンに気付きました。データベースを開き、SQL ステートメントを定義して、ステートメントを実行してください)。今回は、SQL `Select` ステートメントに `WHERE ID = @0`が含まれています。</span><span class="sxs-lookup"><span data-stu-id="82a53-235">(You probably have noticed the general pattern for database operations: open the database, define a SQL statement, and run the statement.) This time, the SQL `Select` statement includes `WHERE ID = @0`.</span></span> <span data-ttu-id="82a53-236">ID は一意であるため、返されるレコードは1つだけです。</span><span class="sxs-lookup"><span data-stu-id="82a53-236">Because the ID is unique, only one record can be returned.</span></span>

<span data-ttu-id="82a53-237">このクエリは、`db.Query`(ムービーの一覧表示に使用したように) `db.QuerySingle` を使用して実行され、コードによって `row` 変数に結果が挿入されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-237">The query is performed by using `db.QuerySingle` (not `db.Query`, as you used for the movie listing), and the code puts the result into the `row` variable.</span></span> <span data-ttu-id="82a53-238">`row` 名前は任意です。変数には任意の名前を指定できます。</span><span class="sxs-lookup"><span data-stu-id="82a53-238">The name `row` is arbitrary; you can name the variables anything you like.</span></span> <span data-ttu-id="82a53-239">上部で初期化された変数は、これらの値がテキストボックスに表示されるように、ムービーの詳細を入力します。</span><span class="sxs-lookup"><span data-stu-id="82a53-239">The variables initialized at the top are then filled with the movie details so that these values can be displayed in the text boxes.</span></span>

## <a name="testing-the-edit-page-so-far"></a><span data-ttu-id="82a53-240">編集ページのテスト (これまで)</span><span class="sxs-lookup"><span data-stu-id="82a53-240">Testing the Edit Page (So Far)</span></span>

<span data-ttu-id="82a53-241">ページをテストする場合は、今すぐ*ムービー*ページを実行し、ムービーの横にある **[編集]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="82a53-241">If you'd like to test your page, run the *Movies* page now and click an **Edit** link next to any movie.</span></span> <span data-ttu-id="82a53-242">[ *Editmovie* ] ページが表示され、選択したムービーの詳細が入力されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-242">You'll see the *EditMovie* page with the details filled in for the movie you selected:</span></span>

![編集するムービーを表示するムービーページを編集する](updating-data/_static/image3.png)

<span data-ttu-id="82a53-244">ページの URL に `?id=10` (またはその他の数値) のようなものが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="82a53-244">Notice that the URL of the page includes something like `?id=10` (or some other number).</span></span> <span data-ttu-id="82a53-245">ここまでで、*ムービー*ページ内の**編集**リンクが機能していること、つまり、ページがクエリ文字列から ID を読み取っていること、および1つのムービーレコードを取得するためのデータベースクエリが機能していることをテストしました。</span><span class="sxs-lookup"><span data-stu-id="82a53-245">So far you've tested that **Edit** links in the *Movie* page work, that your page is reading the ID from the query string, and that the database query to get a single movie record is working.</span></span>

<span data-ttu-id="82a53-246">ムービー情報は変更できますが、 **[変更の送信]** をクリックしても何も起こりません。</span><span class="sxs-lookup"><span data-stu-id="82a53-246">You can change the movie information, but nothing happens when you click **Submit Changes**.</span></span>

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a><span data-ttu-id="82a53-247">ユーザーの変更によってムービーを更新するコードを追加する</span><span class="sxs-lookup"><span data-stu-id="82a53-247">Adding Code to Update the Movie with the User's Changes</span></span>

<span data-ttu-id="82a53-248">*Editmovie. cshtml*ファイルで、2番目の関数 (変更の保存) を実装するには、`@` ブロックの右中かっこの内側に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="82a53-248">In the *EditMovie.cshtml* file, to implement the second function (saving changes), add the following code just inside the closing brace of the `@` block.</span></span> <span data-ttu-id="82a53-249">(コードの配置場所が正確でない場合は、このチュートリアルの最後に表示される[[ムービーの編集] ページの完全なコードリスト](#Complete_Page_Listing_for_EditMovie)を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="82a53-249">(If you're not sure exactly where to put the code, you can look at the [complete code listing for the Edit Movie page](#Complete_Page_Listing_for_EditMovie) that appears at the end of this tutorial.)</span></span>

[!code-csharp[Main](updating-data/samples/sample12.cs)]

<span data-ttu-id="82a53-250">ここでも、このマークアップとコードは、 *Addmovie*のコードに似ています。</span><span class="sxs-lookup"><span data-stu-id="82a53-250">Again, this markup and code is similar to the code in *AddMovie*.</span></span> <span data-ttu-id="82a53-251">このコードは `if(IsPost)` ブロックに含まれています。このコードは、ユーザーが **[変更の送信]** ボタンをクリックしたときにのみ実行されます。その理由は、フォームがポストされたとき (およびの場合のみ) &mdash; です。</span><span class="sxs-lookup"><span data-stu-id="82a53-251">The code is in an `if(IsPost)` block, because this code runs only when the user clicks the **Submit Changes** button &mdash; that is, when (and only when) the form has been posted.</span></span> <span data-ttu-id="82a53-252">この例では、`if(IsPost && Validation.IsValid())`のようなテストを使用していません。つまり、とを使用して両方のテストを組み合わせることはありません。</span><span class="sxs-lookup"><span data-stu-id="82a53-252">In this case, you're not using a test like `if(IsPost && Validation.IsValid())`— that is, you're not combining both tests by using AND.</span></span> <span data-ttu-id="82a53-253">このページでは、最初にフォーム送信 (`if(IsPost)`) があるかどうかを確認し、次に検証用のフィールドを登録します。</span><span class="sxs-lookup"><span data-stu-id="82a53-253">In this page, you first determine whether there's a form submission (`if(IsPost)`), and only then register the fields for validation.</span></span> <span data-ttu-id="82a53-254">その後、検証結果 (`if(Validation.IsValid()`) をテストできます。</span><span class="sxs-lookup"><span data-stu-id="82a53-254">Then you can test the validation results (`if(Validation.IsValid()`).</span></span> <span data-ttu-id="82a53-255">このフローは、 *Addmovie. cshtml*ページとは少し異なりますが、効果は同じです。</span><span class="sxs-lookup"><span data-stu-id="82a53-255">The flow is slightly different than in the *AddMovie.cshtml* page, but the effect is the same.</span></span>

<span data-ttu-id="82a53-256">テキストボックスの値を取得するには、他の `<input>` 要素の `Request.Form["title"]` と同様のコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="82a53-256">You get the values of the text boxes by using `Request.Form["title"]` and similar code for the other `<input>` elements.</span></span> <span data-ttu-id="82a53-257">今回は、コードが隠しフィールド (`<input type="hidden">`) からムービー ID を取得することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="82a53-257">Notice that this time, the code gets the movie ID out of the hidden field (`<input type="hidden">`).</span></span> <span data-ttu-id="82a53-258">ページが初めて実行されたとき、コードはクエリ文字列から ID を取り出しました。</span><span class="sxs-lookup"><span data-stu-id="82a53-258">When the page ran the first time, the code got the ID out of the query string.</span></span> <span data-ttu-id="82a53-259">[非表示] フィールドから値を取得して、最初に表示されたムービーの ID を取得していることを確認します。その後、クエリ文字列が何らかの変更を加えられた場合に備えています。</span><span class="sxs-lookup"><span data-stu-id="82a53-259">You get the value from the hidden field to make sure that you're getting the ID of the movie that was originally displayed, in case the query string was somehow altered since then.</span></span>

<span data-ttu-id="82a53-260">*Addmovie*コードとこのコードの間で本当に重要な違いは、このコードでは、`Insert Into` ステートメントの代わりに SQL `Update` ステートメントを使用することです。</span><span class="sxs-lookup"><span data-stu-id="82a53-260">The really important difference between the *AddMovie* code and this code is that in this code you use the SQL `Update` statement instead of the `Insert Into` statement.</span></span> <span data-ttu-id="82a53-261">次の例は、SQL `Update` ステートメントの構文を示しています。</span><span class="sxs-lookup"><span data-stu-id="82a53-261">The following example shows the syntax of the SQL `Update` statement:</span></span>

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

<span data-ttu-id="82a53-262">任意の順序で任意の列を指定できます。また、必ずしも `Update` 操作中にすべての列を更新する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="82a53-262">You can specify any columns in any order, and you don't necessarily have to update every column during an `Update` operation.</span></span> <span data-ttu-id="82a53-263">(ID 自体を更新することはできません。これは、レコードを新しいレコードとして保存し、`Update` 操作では許可されないためです)。</span><span class="sxs-lookup"><span data-stu-id="82a53-263">(You cannot update the ID itself, because that would in effect save the record as a new record, and that's not allowed for an `Update` operation.)</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="82a53-264">**重要**ID がの `Where` 句は、どのデータベースレコードを更新するかをデータベースが認識しているため、非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="82a53-264">**Important** The `Where` clause with the ID is very important, because that's how the database knows which database record you want to update.</span></span> <span data-ttu-id="82a53-265">`Where` 句を省略した場合、データベース内の*すべて*のレコードが更新されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-265">If you left off the `Where` clause, the database would update *every* record in the database.</span></span> <span data-ttu-id="82a53-266">ほとんどの場合、障害が発生します。</span><span class="sxs-lookup"><span data-stu-id="82a53-266">In most cases, that would be a disaster.</span></span>

<span data-ttu-id="82a53-267">コードでは、更新する値はプレースホルダーを使用して SQL ステートメントに渡されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-267">In the code, the values to update are passed to the SQL statement by using placeholders.</span></span> <span data-ttu-id="82a53-268">前に説明した内容を繰り返すには: セキュリティ上の理由から、プレースホルダーを使用して SQL ステートメントに値を渡す*だけ*です。</span><span class="sxs-lookup"><span data-stu-id="82a53-268">To repeat what we've said before: for security reasons, *only* use placeholders to pass values to a SQL statement.</span></span>

<span data-ttu-id="82a53-269">コードで `db.Execute` を使用して `Update` ステートメントを実行すると、一覧ページにリダイレクトされ、変更内容が表示されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-269">After the code uses `db.Execute` to run the `Update` statement, it redirects back to the listing page, where you can see the changes.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="82a53-270">**さまざまな SQL ステートメント、異なるメソッド**</span><span class="sxs-lookup"><span data-stu-id="82a53-270">**Different SQL Statements, Different Methods**</span></span>
> 
> <span data-ttu-id="82a53-271">異なる SQL ステートメントを実行するには、少し異なる方法を使用することに気付いたかもしれません。</span><span class="sxs-lookup"><span data-stu-id="82a53-271">You might have noticed that you use slightly different methods to run different SQL statements.</span></span> <span data-ttu-id="82a53-272">複数のレコードを返す可能性のある `Select` クエリを実行するには、`Query` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="82a53-272">To run a `Select` query that potentially returns multiple records, you use the `Query` method.</span></span> <span data-ttu-id="82a53-273">データベース項目を1つだけ返すことがわかっている `Select` クエリを実行するには、`QuerySingle` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="82a53-273">To run a `Select` query that you know will return only one database item, you use the `QuerySingle` method.</span></span> <span data-ttu-id="82a53-274">変更を加えるがデータベース項目を返さないコマンドを実行するには、`Execute` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="82a53-274">To run commands that make changes but that don't return database items, you use the `Execute` method.</span></span>
> 
> <span data-ttu-id="82a53-275">`Query` と `QuerySingle`の違いについて既に説明したように、それぞれが異なる結果を返すため、異なる方法を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="82a53-275">You have to have different methods because each of them returns different results, as you saw already in the difference between `Query` and `QuerySingle`.</span></span> <span data-ttu-id="82a53-276">(`Execute` メソッドでは、実際には、コマンド &mdash; によって影響を受けたデータベース行の数 &mdash; も値を返しますが、これまでは無視しています)。</span><span class="sxs-lookup"><span data-stu-id="82a53-276">(The `Execute` method actually returns a value also &mdash; namely, the number of database rows that were affected by the command &mdash; but you've been ignoring that so far.)</span></span>
> 
> <span data-ttu-id="82a53-277">もちろん、`Query` メソッドは、1つのデータベース行だけを返す場合があります。</span><span class="sxs-lookup"><span data-stu-id="82a53-277">Of course, the `Query` method might return only one database row.</span></span> <span data-ttu-id="82a53-278">ただし、ASP.NET は常に `Query` メソッドの結果をコレクションとして扱います。</span><span class="sxs-lookup"><span data-stu-id="82a53-278">However, ASP.NET always treats the results of the `Query` method as a collection.</span></span> <span data-ttu-id="82a53-279">メソッドが1行だけを返す場合でも、コレクションからその1行を抽出する必要があります。</span><span class="sxs-lookup"><span data-stu-id="82a53-279">Even if the method returns just one row, you have to extract that single row from the collection.</span></span> <span data-ttu-id="82a53-280">したがって、1つの行だけを取得することが*わかっ*ている場合は、`QuerySingle`を使用する方がもう少し便利です。</span><span class="sxs-lookup"><span data-stu-id="82a53-280">Therefore, in situations where you *know* you'll get back only one row, it's a bit more convenient to use `QuerySingle`.</span></span>
> 
> <span data-ttu-id="82a53-281">特定の種類のデータベース操作を実行する方法は他にもいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="82a53-281">There are a few other methods that perform specific types of database operations.</span></span> <span data-ttu-id="82a53-282">データベースメソッドの一覧については、「 [ASP.NET WEB ページ API クイックリファレンス](../../api-reference/asp-net-web-pages-api-reference.md#Data)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="82a53-282">You can find a listing of database methods in the [ASP.NET Web Pages API Quick Reference](../../api-reference/asp-net-web-pages-api-reference.md#Data).</span></span>

## <a name="making-validation-for-the-id-more-robust"></a><span data-ttu-id="82a53-283">ID の検証の堅牢性を高める</span><span class="sxs-lookup"><span data-stu-id="82a53-283">Making Validation for the ID More Robust</span></span>

<span data-ttu-id="82a53-284">ページを初めて実行するときは、クエリ文字列からムービー ID を取得して、データベースからそのムービーを取得できるようにします。</span><span class="sxs-lookup"><span data-stu-id="82a53-284">The first time that the page runs, you get the movie ID from the query string so that you can go get that movie from the database.</span></span> <span data-ttu-id="82a53-285">実際には、次のコードを使用して検索する値があることを確認しました。</span><span class="sxs-lookup"><span data-stu-id="82a53-285">You made sure that there actually was a value to go look for, which you did by using this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample13.cs)]

<span data-ttu-id="82a53-286">このコードを使用し*て、最初にムービーページで*ムービーを選択せずに、 *editmovies*ページにユーザーがいた場合に、ユーザーにわかりやすいエラーメッセージが表示されるようにしています。</span><span class="sxs-lookup"><span data-stu-id="82a53-286">You used this code to make sure that if a user gets to the *EditMovies* page without first selecting a movie in the *Movies* page, the page would display a user-friendly error message.</span></span> <span data-ttu-id="82a53-287">(それ以外の場合、ユーザーには、混同される可能性のあるエラーが表示されます)。</span><span class="sxs-lookup"><span data-stu-id="82a53-287">(Otherwise, users would see an error that would probably just confuse them.)</span></span>

<span data-ttu-id="82a53-288">ただし、この検証は非常に堅牢ではありません。</span><span class="sxs-lookup"><span data-stu-id="82a53-288">However, this validation isn't very robust.</span></span> <span data-ttu-id="82a53-289">次のエラーでページが呼び出されることもあります。</span><span class="sxs-lookup"><span data-stu-id="82a53-289">The page might also be invoked with these errors:</span></span>

- <span data-ttu-id="82a53-290">ID が数値ではありません。</span><span class="sxs-lookup"><span data-stu-id="82a53-290">The ID isn't a number.</span></span> <span data-ttu-id="82a53-291">たとえば、`http://localhost:nnnnn/EditMovie?id=abc`のような URL を使用してページを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="82a53-291">For example, the page could be invoked with a URL like `http://localhost:nnnnn/EditMovie?id=abc`.</span></span>
- <span data-ttu-id="82a53-292">ID は数値ですが、存在しないムービー (`http://localhost:nnnnn/EditMovie?id=100934`など) を参照しています。</span><span class="sxs-lookup"><span data-stu-id="82a53-292">The ID is a number, but it references a movie that doesn't exist (for example, `http://localhost:nnnnn/EditMovie?id=100934`).</span></span>

<span data-ttu-id="82a53-293">これらの Url によって発生したエラーを確認するには、[*ムービー* ] ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="82a53-293">If you're curious to see the errors that result from these URLs, run the *Movies* page.</span></span> <span data-ttu-id="82a53-294">編集するムービーを選択し、[ *editmovie* ] ページの url を、アルファベット ID または存在しないムービーの id を含む url に変更します。</span><span class="sxs-lookup"><span data-stu-id="82a53-294">Select a movie to edit, and then change the URL of the *EditMovie* page to a URL that contains an alphabetic ID or the ID of a non-existent movie.</span></span>

<span data-ttu-id="82a53-295">では、どうすればよいでしょうか。</span><span class="sxs-lookup"><span data-stu-id="82a53-295">So what should you do?</span></span> <span data-ttu-id="82a53-296">最初の修正は、ページに渡される ID だけでなく、ID が整数であることを確認することです。</span><span class="sxs-lookup"><span data-stu-id="82a53-296">The first fix is to make sure that not only is an ID passed to the page, but that the ID is an integer.</span></span> <span data-ttu-id="82a53-297">`!IsPost` テストのコードを次の例のように変更します。</span><span class="sxs-lookup"><span data-stu-id="82a53-297">Change the code for the `!IsPost` test to look like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample14.cs)]

<span data-ttu-id="82a53-298">`&&` (論理 AND) にリンクされた `IsEmpty` テストに2つ目の条件を追加しました。</span><span class="sxs-lookup"><span data-stu-id="82a53-298">You've added a second condition to the `IsEmpty` test, linked with `&&` (logical AND):</span></span>

[!code-csharp[Main](updating-data/samples/sample15.cs)]

<span data-ttu-id="82a53-299">[ASP.NET Web ページプログラミング](../introducing-razor-syntax-c.md)チュートリアルの概要では、`AsInt` `AsBool` などのメソッドが文字列を他のデータ型に変換する方法について説明しています。</span><span class="sxs-lookup"><span data-stu-id="82a53-299">You might remember from the [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md) tutorial that methods like `AsBool` an `AsInt` convert a character string to some other data type.</span></span> <span data-ttu-id="82a53-300">`IsInt` メソッド (およびその他の `IsBool` や `IsDateTime`など) も似ています。</span><span class="sxs-lookup"><span data-stu-id="82a53-300">The `IsInt` method (and others, like `IsBool` and `IsDateTime`) are similar.</span></span> <span data-ttu-id="82a53-301">ただし、実際に変換を実行することなく、文字列を変換*できる*かどうかのみをテストします。</span><span class="sxs-lookup"><span data-stu-id="82a53-301">However, they test only whether you *can* convert the string, without actually performing the conversion.</span></span> <span data-ttu-id="82a53-302">ここでは、基本的に、*クエリ文字列の値を整数に変換できるかどうか*を示しています。</span><span class="sxs-lookup"><span data-stu-id="82a53-302">So here you're essentially saying *If the query string value can be converted to an integer ...*.</span></span>

<span data-ttu-id="82a53-303">もう1つの潜在的な問題は、存在しないムービーを探していることです。</span><span class="sxs-lookup"><span data-stu-id="82a53-303">The other potential problem is looking for a movie that doesn't exist.</span></span> <span data-ttu-id="82a53-304">ムービーを取得するコードは、次のコードのようになります。</span><span class="sxs-lookup"><span data-stu-id="82a53-304">The code to get a movie looks like this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample16.cs)]

<span data-ttu-id="82a53-305">実際のムービーに対応しない `QuerySingle` メソッドに `movieId` 値を渡すと、何も返されず、後続のステートメント (`title=row.Title`など) でエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="82a53-305">If you pass a `movieId` value to the `QuerySingle` method that doesn't correspond to an actual movie, nothing is returned and the statements that follow (for example, `title=row.Title`) result in errors.</span></span>

<span data-ttu-id="82a53-306">ここでも、簡単な修正があります。</span><span class="sxs-lookup"><span data-stu-id="82a53-306">Again there's an easy fix.</span></span> <span data-ttu-id="82a53-307">`db.QuerySingle` メソッドが結果を返さない場合、`row` 変数は null になります。</span><span class="sxs-lookup"><span data-stu-id="82a53-307">If the `db.QuerySingle` method returns no results, the `row` variable will be null.</span></span> <span data-ttu-id="82a53-308">そのため、`row` 変数が null であるかどうかを確認してから、値を取得することができます。</span><span class="sxs-lookup"><span data-stu-id="82a53-308">So you can check whether the `row` variable is null before you try to get values from it.</span></span> <span data-ttu-id="82a53-309">次のコードは、`row` オブジェクトから値を取得するステートメントの周囲に `if` ブロックを追加します。</span><span class="sxs-lookup"><span data-stu-id="82a53-309">The following code adds an `if` block around the statements that get the values out of the `row` object:</span></span>

[!code-csharp[Main](updating-data/samples/sample17.cs)]

<span data-ttu-id="82a53-310">この2つの追加の検証テストを使用すると、ページの行頭文字がより多くなります。</span><span class="sxs-lookup"><span data-stu-id="82a53-310">With these two additional validation tests, the page becomes more bullet-proof.</span></span> <span data-ttu-id="82a53-311">`!IsPost` のブランチの完全なコードは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="82a53-311">The complete code for the `!IsPost` branch now looks like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample18.cs)]

<span data-ttu-id="82a53-312">このタスクは、`else` ブロックに適しています。</span><span class="sxs-lookup"><span data-stu-id="82a53-312">We'll note once more that this task is a good use for an `else` block.</span></span> <span data-ttu-id="82a53-313">テストが成功しなかった場合、`else` ブロックによってエラーメッセージが設定されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-313">If the tests don't pass, the `else` blocks set error messages.</span></span>

## <a name="adding-a-link-to-return-to-the-movies-page"></a><span data-ttu-id="82a53-314">ムービーページに戻るためのリンクの追加</span><span class="sxs-lookup"><span data-stu-id="82a53-314">Adding a Link to Return to the Movies Page</span></span>

<span data-ttu-id="82a53-315">最終的に役に立つのは、*ムービー*ページにリンクを追加することです。</span><span class="sxs-lookup"><span data-stu-id="82a53-315">A final and helpful detail is to add a link back to the *Movies* page.</span></span> <span data-ttu-id="82a53-316">イベントの通常のフローでは、ユーザーは*ムービー*ページから開始し、 **[編集]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="82a53-316">In the ordinary flow of events, users will start at the *Movies* page and click an **Edit** link.</span></span> <span data-ttu-id="82a53-317">これにより、[ *Editmovie* ] ページに移動し、ムービーを編集して、ボタンをクリックすることができます。</span><span class="sxs-lookup"><span data-stu-id="82a53-317">That brings them to the *EditMovie* page, where they can edit the movie and click the button.</span></span> <span data-ttu-id="82a53-318">コードによって変更が処理された後、*ムービー*ページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="82a53-318">After the code processes the change, it redirects back to the *Movies* page.</span></span>

<span data-ttu-id="82a53-319">ただし</span><span class="sxs-lookup"><span data-stu-id="82a53-319">However:</span></span>

- <span data-ttu-id="82a53-320">ユーザーは何も変更しないことを決定する場合があります。</span><span class="sxs-lookup"><span data-stu-id="82a53-320">The user might decide not to change anything.</span></span>
- <span data-ttu-id="82a53-321">ユーザーは、最初に [*ムービー* ] ページの **[編集]** リンクをクリックすることなく、このページを取得している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="82a53-321">The user might have gotten to this page without first clicking an **Edit** link in the *Movies* page.</span></span>

<span data-ttu-id="82a53-322">どちらの方法でも、メインの一覧に簡単に戻ることができます。</span><span class="sxs-lookup"><span data-stu-id="82a53-322">Either way, you want to make it easy for them to return to the main listing.</span></span> <span data-ttu-id="82a53-323">マークアップの終了 `</form>` タグの直後に次のマークアップを追加 &mdash; と、簡単に修正できます。</span><span class="sxs-lookup"><span data-stu-id="82a53-323">It's an easy fix &mdash; add the following markup just after the closing `</form>` tag in the markup:</span></span>

[!code-html[Main](updating-data/samples/sample19.html)]

<span data-ttu-id="82a53-324">このマークアップは、他の場所で見た `<a>` 要素に同じ構文を使用します。</span><span class="sxs-lookup"><span data-stu-id="82a53-324">This markup uses the same syntax for an `<a>` element that you've seen elsewhere.</span></span> <span data-ttu-id="82a53-325">URL には、"web サイトのルート" を意味する `~` が含まれています。</span><span class="sxs-lookup"><span data-stu-id="82a53-325">The URL includes `~` to mean "root of the website."</span></span>

## <a name="testing-the-movie-update-process"></a><span data-ttu-id="82a53-326">ムービーの更新プロセスのテスト</span><span class="sxs-lookup"><span data-stu-id="82a53-326">Testing the Movie Update Process</span></span>

<span data-ttu-id="82a53-327">これで、をテストできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="82a53-327">Now you can test.</span></span> <span data-ttu-id="82a53-328">*ムービーページを*実行し、ムービーの横にある **[編集]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="82a53-328">Run the *Movies* page, and click **Edit** next to a movie.</span></span> <span data-ttu-id="82a53-329">[ *Editmovie* ] ページが表示されたら、ムービーに変更を加え、 **[変更の送信]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="82a53-329">When the *EditMovie* page appears, make changes to the movie and click **Submit Changes**.</span></span> <span data-ttu-id="82a53-330">ムービーの一覧が表示されたら、変更が表示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="82a53-330">When the movie listing appears, make sure that your changes are shown.</span></span>

<span data-ttu-id="82a53-331">検証が機能していることを確認するには、別のムービーの **[編集]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="82a53-331">To make sure that validation is working, click **Edit** for another movie.</span></span> <span data-ttu-id="82a53-332">[ *Editmovie* ] ページが表示されたら、 **[ジャンル]** フィールド (または **[Year]** フィールドまたはその両方) をオフにして、変更を送信します。</span><span class="sxs-lookup"><span data-stu-id="82a53-332">When you get to the *EditMovie* page, clear the **Genre** field (or **Year** field, or both) and try to submit your changes.</span></span> <span data-ttu-id="82a53-333">期待どおりにエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="82a53-333">You'll see an error, as you'd expect:</span></span>

![検証エラーが表示された [ムービーの編集] ページ](updating-data/_static/image4.png)

<span data-ttu-id="82a53-335">**[ムービーリストに戻る]** リンクをクリックして変更を破棄し、*ムービー*ページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="82a53-335">Click the **Return to movie listing** link to abandon your changes and return to the *Movies* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="82a53-336">次へ</span><span class="sxs-lookup"><span data-stu-id="82a53-336">Coming Up Next</span></span>

<span data-ttu-id="82a53-337">次のチュートリアルでは、ムービーレコードを削除する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="82a53-337">In the next tutorial, you'll see how to delete a movie record.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a><span data-ttu-id="82a53-338">[ムービーの完全な一覧表示] ページ (編集リンクを使用して更新)</span><span class="sxs-lookup"><span data-stu-id="82a53-338">Complete Listing for Movie Page (Updated with Edit Links)</span></span>

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a><span data-ttu-id="82a53-339">[ムービーの編集] ページの完全なページリスト</span><span class="sxs-lookup"><span data-stu-id="82a53-339">Complete Page Listing for Edit Movie Page</span></span>

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="82a53-340">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="82a53-340">Additional Resources</span></span>

- [<span data-ttu-id="82a53-341">Razor 構文を使用した ASP.NET Web プログラミングの概要</span><span class="sxs-lookup"><span data-stu-id="82a53-341">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../../getting-started/introducing-razor-syntax-c.md)
- <span data-ttu-id="82a53-342">W3Schools サイトでの[SQL UPDATE ステートメント](http://www.w3schools.com/sql/sql_update.asp)</span><span class="sxs-lookup"><span data-stu-id="82a53-342">[SQL UPDATE Statement](http://www.w3schools.com/sql/sql_update.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="82a53-343">[前へ](entering-data.md)
> [次へ](deleting-data.md)</span><span class="sxs-lookup"><span data-stu-id="82a53-343">[Previous](entering-data.md)
[Next](deleting-data.md)</span></span>
