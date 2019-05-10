---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 並べ替え、フィルター処理、および ASP.NET MVC アプリケーション (3/10) で Entity Framework でページング |Microsoft Docs
author: tdykstra
description: Contoso University のサンプルの web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法について説明しています.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9510eb8094a55346bec2e0dab2a15ee79d211c88
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65126514"
---
# <a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a><span data-ttu-id="462de-103">並べ替え、フィルター処理、および ASP.NET MVC アプリケーション (3/10) で Entity Framework でのページング</span><span class="sxs-lookup"><span data-stu-id="462de-103">Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application (3 of 10)</span></span>

<span data-ttu-id="462de-104">によって[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="462de-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="462de-105">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="462de-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="462de-106">Contoso University のサンプルの web アプリケーションでは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="462de-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="462de-107">チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="462de-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="462de-108">チュートリアルのシリーズを開始するには、最初からまたは[この章のスタート プロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、ここから始めてください。</span><span class="sxs-lookup"><span data-stu-id="462de-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="462de-109">を解決できない問題が生じた場合[章では、完了したダウンロード](building-the-ef5-mvc4-chapter-downloads.md)の問題を再現しようとします。</span><span class="sxs-lookup"><span data-stu-id="462de-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="462de-110">問題の解決策は、完成したコードにコードを比較することによって一般的に見つかります。</span><span class="sxs-lookup"><span data-stu-id="462de-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="462de-111">一般的なエラーとその解決方法は、次を参照してください。[エラーと回避策。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="462de-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="462de-112">前のチュートリアルでの基本的な CRUD 操作の web ページのセットを実装した`Student`エンティティ。</span><span class="sxs-lookup"><span data-stu-id="462de-112">In the previous tutorial you implemented a set of web pages for basic CRUD operations for `Student` entities.</span></span> <span data-ttu-id="462de-113">このチュートリアルでは、並べ替え、フィルター処理、およびページング機能を追加します、**学生**インデックス ページです。</span><span class="sxs-lookup"><span data-stu-id="462de-113">In this tutorial you'll add sorting, filtering, and paging functionality to the **Students** Index page.</span></span> <span data-ttu-id="462de-114">単純なグループ化を実行するページも作成します。</span><span class="sxs-lookup"><span data-stu-id="462de-114">You'll also create a page that does simple grouping.</span></span>

<span data-ttu-id="462de-115">次の図は、作業が終了したときにページがどのように表示されるかを示しています。</span><span class="sxs-lookup"><span data-stu-id="462de-115">The following illustration shows what the page will look like when you're done.</span></span> <span data-ttu-id="462de-116">列見出しとは、ユーザーがクリックしてその列で並べ替えを行うことができるリンクです。</span><span class="sxs-lookup"><span data-stu-id="462de-116">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="462de-117">列見出しを繰り返しクリックすると、昇順と降順の並べ替え順序が切り替えられます。</span><span class="sxs-lookup"><span data-stu-id="462de-117">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a><span data-ttu-id="462de-119">Students インデックス ページに列の並べ替えリンクを追加する</span><span class="sxs-lookup"><span data-stu-id="462de-119">Add Column Sort Links to the Students Index Page</span></span>

<span data-ttu-id="462de-120">Student インデックス ページに並べ替えを追加、変更します、`Index`のメソッド、`Student`コント ローラーのコードを追加し、`Student`ビューにインデックスします。</span><span class="sxs-lookup"><span data-stu-id="462de-120">To add sorting to the Student Index page, you'll change the `Index` method of the `Student` controller and add code to the `Student` Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="462de-121">並べ替えは Index メソッドに機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="462de-121">Add Sorting Functionality to the Index Method</span></span>

<span data-ttu-id="462de-122">*Controllers\StudentController.cs*、置換、`Index`メソッドを次のコード。</span><span class="sxs-lookup"><span data-stu-id="462de-122">In *Controllers\StudentController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="462de-123">このコードは、URL 内の文字列から `sortOrder` パラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="462de-123">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="462de-124">クエリ文字列の値は、アクション メソッドのパラメーターとして、ASP.NET MVC によって提供されます。</span><span class="sxs-lookup"><span data-stu-id="462de-124">The query string value is provided by ASP.NET MVC as a parameter to the action method.</span></span> <span data-ttu-id="462de-125">パラメータは、"Name" または "Date" という文字列で、その後に必要に応じてアンダースコアと降順を指定する文字列 "desc" が続きます。</span><span class="sxs-lookup"><span data-stu-id="462de-125">The parameter will be a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="462de-126">既定の並べ替え順序は昇順です。</span><span class="sxs-lookup"><span data-stu-id="462de-126">The default sort order is ascending.</span></span>

<span data-ttu-id="462de-127">インデックス ページが初めて要求されたときには、クエリ文字列はありません。</span><span class="sxs-lookup"><span data-stu-id="462de-127">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="462de-128">受講者がで昇順に表示される`LastName`でフォールスルー ケースによって確立されると、既定値は、`switch`ステートメント。</span><span class="sxs-lookup"><span data-stu-id="462de-128">The students are displayed in ascending order by `LastName`, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="462de-129">ユーザーが列見出しハイパーリンクをクリックすると、適切な `sortOrder` 値がクエリ文字列で提供されます。</span><span class="sxs-lookup"><span data-stu-id="462de-129">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="462de-130">2 つ`ViewBag`変数を使用するビューは、適切なクエリ文字列の値を持つ列見出しのハイパーリンクを構成できます。</span><span class="sxs-lookup"><span data-stu-id="462de-130">The two `ViewBag` variables are used so that the view can configure the column heading hyperlinks with the appropriate query string values:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="462de-131">これらは、三項ステートメントです。</span><span class="sxs-lookup"><span data-stu-id="462de-131">These are ternary statements.</span></span> <span data-ttu-id="462de-132">1 つ目の指定された場合、`sortOrder`パラメーターが null または空の場合、`ViewBag.NameSortParm`に設定する必要があります"名\_desc"、それ以外の空の文字列に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="462de-132">The first one specifies that if the `sortOrder` parameter is null or empty, `ViewBag.NameSortParm` should be set to "name\_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="462de-133">これらの 2 つのステートメントを使用して、次のようにビューで列見出しのハイパーリンクの設定することができます。</span><span class="sxs-lookup"><span data-stu-id="462de-133">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

| <span data-ttu-id="462de-134">既定の並べ替え順</span><span class="sxs-lookup"><span data-stu-id="462de-134">Current sort order</span></span> | <span data-ttu-id="462de-135">姓のハイパーリンク</span><span class="sxs-lookup"><span data-stu-id="462de-135">Last Name Hyperlink</span></span> | <span data-ttu-id="462de-136">日付のハイパーリンク</span><span class="sxs-lookup"><span data-stu-id="462de-136">Date Hyperlink</span></span> |
| --- | --- | --- |
| <span data-ttu-id="462de-137">姓の昇順</span><span class="sxs-lookup"><span data-stu-id="462de-137">Last Name ascending</span></span> | <span data-ttu-id="462de-138">descending</span><span class="sxs-lookup"><span data-stu-id="462de-138">descending</span></span> | <span data-ttu-id="462de-139">ascending</span><span class="sxs-lookup"><span data-stu-id="462de-139">ascending</span></span> |
| <span data-ttu-id="462de-140">姓の降順</span><span class="sxs-lookup"><span data-stu-id="462de-140">Last Name descending</span></span> | <span data-ttu-id="462de-141">ascending</span><span class="sxs-lookup"><span data-stu-id="462de-141">ascending</span></span> | <span data-ttu-id="462de-142">ascending</span><span class="sxs-lookup"><span data-stu-id="462de-142">ascending</span></span> |
| <span data-ttu-id="462de-143">日付の昇順</span><span class="sxs-lookup"><span data-stu-id="462de-143">Date ascending</span></span> | <span data-ttu-id="462de-144">ascending</span><span class="sxs-lookup"><span data-stu-id="462de-144">ascending</span></span> | <span data-ttu-id="462de-145">descending</span><span class="sxs-lookup"><span data-stu-id="462de-145">descending</span></span> |
| <span data-ttu-id="462de-146">日付の降順</span><span class="sxs-lookup"><span data-stu-id="462de-146">Date descending</span></span> | <span data-ttu-id="462de-147">ascending</span><span class="sxs-lookup"><span data-stu-id="462de-147">ascending</span></span> | <span data-ttu-id="462de-148">ascending</span><span class="sxs-lookup"><span data-stu-id="462de-148">ascending</span></span> |

<span data-ttu-id="462de-149">メソッドを使用して[LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx)を並べ替え列を指定します。</span><span class="sxs-lookup"><span data-stu-id="462de-149">The method uses [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) to specify the column to sort by.</span></span> <span data-ttu-id="462de-150">コードを作成、 [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx)する前に変数、`switch`ステートメントでは、変更で、`switch`ステートメント、および呼び出し、`ToList`メソッドの後、`switch`ステートメント。</span><span class="sxs-lookup"><span data-stu-id="462de-150">The code creates an [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) variable before the `switch` statement, modifies it in the `switch` statement, and calls the `ToList` method after the `switch` statement.</span></span> <span data-ttu-id="462de-151">`IQueryable` 変数を作成および変更するときに、データベースに送信されるクエリはありません。</span><span class="sxs-lookup"><span data-stu-id="462de-151">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="462de-152">変換するまで、クエリが実行されない、`IQueryable`などのメソッドを呼び出すことによって、コレクションにオブジェクト`ToList`します。</span><span class="sxs-lookup"><span data-stu-id="462de-152">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToList`.</span></span> <span data-ttu-id="462de-153">そのため、このコード結果まで実行されない 1 つのクエリ、`return View`ステートメント。</span><span class="sxs-lookup"><span data-stu-id="462de-153">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="462de-154">列見出しを Student インデックス ビューへのハイパーリンクの追加します。</span><span class="sxs-lookup"><span data-stu-id="462de-154">Add Column Heading Hyperlinks to the Student Index View</span></span>

<span data-ttu-id="462de-155">*Views\Student\Index.cshtml*、置換、`<tr>`と`<th>`見出し行を強調表示されたコードの要素。</span><span class="sxs-lookup"><span data-stu-id="462de-155">In *Views\Student\Index.cshtml*, replace the `<tr>` and `<th>` elements for the heading row with the highlighted code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

<span data-ttu-id="462de-156">このコードは、情報を使用して、`ViewBag`適切なクエリを含むハイパーリンクを設定するプロパティの文字列値。</span><span class="sxs-lookup"><span data-stu-id="462de-156">This code uses the information in the `ViewBag` properties to set up hyperlinks with the appropriate query string values.</span></span>

<span data-ttu-id="462de-157">ページを実行し、をクリックして、**姓**と**加入契約日**その並べ替えを確認する列見出しに動作します。</span><span class="sxs-lookup"><span data-stu-id="462de-157">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="462de-159">クリックした後、**姓**見出しで、学生は最後の名前の降順に表示されます。</span><span class="sxs-lookup"><span data-stu-id="462de-159">After you click the **Last Name** heading, students are displayed in descending last name order.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a><span data-ttu-id="462de-160">Students インデックス ページに検索ボックスを追加します。</span><span class="sxs-lookup"><span data-stu-id="462de-160">Add a Search Box to the Students Index Page</span></span>

<span data-ttu-id="462de-161">Students インデックス ページにフィルターを追加するには、テキスト ボックスと送信ボタンをビューに追加し、`Index` メソッドで対応する変更を行います。</span><span class="sxs-lookup"><span data-stu-id="462de-161">To add filtering to the Students Index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="462de-162">テキスト ボックスを使用して、姓と名のフィールドに検索する文字列を入力できます。</span><span class="sxs-lookup"><span data-stu-id="462de-162">The text box will let you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="462de-163">Index メソッドにフィルター処理機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="462de-163">Add Filtering Functionality to the Index Method</span></span>

<span data-ttu-id="462de-164">*Controllers\StudentController.cs*、置換、`Index`メソッドを次のコード (変更が強調表示されます)。</span><span class="sxs-lookup"><span data-stu-id="462de-164">In *Controllers\StudentController.cs*, replace the `Index` method with the following code (the changes are highlighted):</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

<span data-ttu-id="462de-165">`searchString` パラメーターを `Index` メソッドに追加しました。</span><span class="sxs-lookup"><span data-stu-id="462de-165">You've added a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="462de-166">LINQ ステートメントに追加することも、`where`名または姓を持つ検索文字列が含まれています。 学生のみを選択する句。</span><span class="sxs-lookup"><span data-stu-id="462de-166">You've also added to the LINQ statement a `where` clause that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="462de-167">インデックス ビューに追加するテキスト ボックスから検索する文字列値を受信します。ステートメントを追加する、[場所](https://msdn.microsoft.com/library/bb535040.aspx)句は、検索する値がある場合にのみ実行されます。</span><span class="sxs-lookup"><span data-stu-id="462de-167">The search string value is received from a text box that you'll add to the Index view.The statement that adds the [where](https://msdn.microsoft.com/library/bb535040.aspx) clause is executed only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="462de-168">多くの場合は、Entity Framework のエンティティ セットまたはメモリ内コレクションの拡張メソッドとして同じメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="462de-168">In many cases you can call the same method either on an Entity Framework entity set or as an extension method on an in-memory collection.</span></span> <span data-ttu-id="462de-169">結果は、通常は同じが、場合によっては異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="462de-169">The results are normally the same but in some cases may be different.</span></span> <span data-ttu-id="462de-170">.NET Framework の実装など、`Contains`メソッドが、空の文字列を渡しますが、Entity Framework provider for SQL Server Compact 4.0 は、空の文字列には、ゼロ行を返すときに、すべての行を返します。</span><span class="sxs-lookup"><span data-stu-id="462de-170">For example, the .NET Framework implementation of the `Contains` method returns all rows when you pass an empty string to it, but the Entity Framework provider for SQL Server Compact 4.0 returns zero rows for empty strings.</span></span> <span data-ttu-id="462de-171">例のコードではそのため (配置すること、`Where`内のステートメント、`if`ステートメント) は、すべてのバージョンの SQL Server と同じ結果を取得することを確認します。</span><span class="sxs-lookup"><span data-stu-id="462de-171">Therefore the code in the example (putting the `Where` statement inside an `if` statement) makes sure that you get the same results for all versions of SQL Server.</span></span> <span data-ttu-id="462de-172">.NET Framework の実装も、`Contains`メソッドは、既定では、大文字小文字の比較を実行しますが、Entity Framework の SQL Server プロバイダーは、既定では大文字の比較を実行します。</span><span class="sxs-lookup"><span data-stu-id="462de-172">Also, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but Entity Framework SQL Server providers perform case-insensitive comparisons by default.</span></span> <span data-ttu-id="462de-173">そのため、呼び出し、`ToUpper`メソッド、テストを明示的に大文字をにより返されます、リポジトリを使用するには、後でコードを変更すると、結果は変化しません、`IEnumerable`コレクションの代わりに、`IQueryable`オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="462de-173">Therefore, calling the `ToUpper` method to make the test explicitly case-insensitive ensures that results do not change when you change the code later to use a repository, which will return an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="462de-174">(`IEnumerable` コレクションに対して `Contains` メソッドを呼び出したときには、.NET Framework の実装を取得します。`IQueryable` オブジェクトに対して呼び出したときには、データベース プロバイダーの実装を取得します)。</span><span class="sxs-lookup"><span data-stu-id="462de-174">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.)</span></span>

### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="462de-175">Students インデックス ビューに [Search] ボックスを追加する</span><span class="sxs-lookup"><span data-stu-id="462de-175">Add a Search Box to the Student Index View</span></span>

<span data-ttu-id="462de-176">*Views\Student\Index.cshtml*、開始する直前に強調表示されたコードを追加`table`キャプション、テキスト ボックスを作成するにはタグと**検索**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="462de-176">In *Views\Student\Index.cshtml*, add the highlighted code immediately before the opening `table` tag in order to create a caption, a text box, and a **Search** button.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

<span data-ttu-id="462de-177">ページを実行し、検索文字列を入力し をクリックして**検索**フィルターが動作していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="462de-177">Run the page, enter a search string, and click **Search** to verify that filtering is working.</span></span>

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="462de-179">URL に「、」検索文字列、これをこのページにブックマークを設定した場合はありません一覧を取得するフィルター選択されたブックマークを使用する場合は意味が含まれていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="462de-179">Notice the URL doesn't contain the "an" search string, which means that if you bookmark this page, you won't get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="462de-180">変更を**検索**フィルター条件のチュートリアルの後半でクエリ文字列を使用するボタン。</span><span class="sxs-lookup"><span data-stu-id="462de-180">You'll change the **Search** button to use query strings for filter criteria later in the tutorial.</span></span>

## <a name="add-paging-to-the-students-index-page"></a><span data-ttu-id="462de-181">Students インデックス ページにページングを追加します。</span><span class="sxs-lookup"><span data-stu-id="462de-181">Add Paging to the Students Index Page</span></span>

<span data-ttu-id="462de-182">Students インデックス ページには、ページングを追加するをインストールして起動します、 **PagedList.Mvc** NuGet パッケージ。</span><span class="sxs-lookup"><span data-stu-id="462de-182">To add paging to the Students Index page, you'll start by installing the **PagedList.Mvc** NuGet package.</span></span> <span data-ttu-id="462de-183">その後で追加の変更、`Index`メソッドへのページングのリンクを追加し、`Index`ビュー。</span><span class="sxs-lookup"><span data-stu-id="462de-183">Then you'll make additional changes in the `Index` method and add paging links to the `Index` view.</span></span> <span data-ttu-id="462de-184">**PagedList.Mvc**優れた多くのページングと ASP.NET MVC でのパッケージの並べ替えの 1 つとここでその使用のためのものとしてその他のオプションの上の推奨事項ではなく、例としてのみです。</span><span class="sxs-lookup"><span data-stu-id="462de-184">**PagedList.Mvc** is one of many good paging and sorting packages for ASP.NET MVC, and its use here is intended only as an example, not as a recommendation for it over other options.</span></span> <span data-ttu-id="462de-185">次の図は、ページングのリンクを示します。</span><span class="sxs-lookup"><span data-stu-id="462de-185">The following illustration shows the paging links.</span></span>

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a><span data-ttu-id="462de-187">PagedList.MVC NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="462de-187">Install the PagedList.MVC NuGet Package</span></span>

<span data-ttu-id="462de-188">NuGet **PagedList.Mvc**パッケージが自動的にインストール、 **PagedList**依存関係としてパッケージします。</span><span class="sxs-lookup"><span data-stu-id="462de-188">The NuGet **PagedList.Mvc** package automatically installs the **PagedList** package as a dependency.</span></span> <span data-ttu-id="462de-189">**PagedList**パッケージのインストール、`PagedList`のコレクションの種類と拡張子メソッド`IQueryable`と`IEnumerable`コレクション。</span><span class="sxs-lookup"><span data-stu-id="462de-189">The **PagedList** package installs a `PagedList` collection type and extension methods for `IQueryable` and `IEnumerable` collections.</span></span> <span data-ttu-id="462de-190">拡張メソッドが 1 つのデータのページを作成、`PagedList`コレクションのうち、`IQueryable`または`IEnumerable`、および`PagedList`いくつかのプロパティとメソッドをページングを容易にするコレクションを提供します。</span><span class="sxs-lookup"><span data-stu-id="462de-190">The extension methods create a single page of data in a `PagedList` collection out of your `IQueryable` or `IEnumerable`, and the `PagedList` collection provides several properties and methods that facilitate paging.</span></span> <span data-ttu-id="462de-191">**PagedList.Mvc**パッケージは、ページング ボタンを表示するページング ヘルパーをインストールします。</span><span class="sxs-lookup"><span data-stu-id="462de-191">The **PagedList.Mvc** package installs a paging helper that displays the paging buttons.</span></span>

<span data-ttu-id="462de-192">**ツール**メニューの  **NuGet パッケージ マネージャー**し**ソリューションの NuGet パッケージの管理**します。</span><span class="sxs-lookup"><span data-stu-id="462de-192">From the **Tools** menu, select **NuGet Package Manager** and then **Manage NuGet Packages for Solution**.</span></span>

<span data-ttu-id="462de-193">**NuGet パッケージの管理**ダイアログ ボックスで、をクリックして、**オンライン**左側のタブし、検索ボックスに「ページ」を入力します。</span><span class="sxs-lookup"><span data-stu-id="462de-193">In the **Manage NuGet Packages** dialog box, click the **Online** tab on the left and then enter "paged" in the search box.</span></span> <span data-ttu-id="462de-194">表示された場合、 **PagedList.Mvc**パッケージで、**インストール**します。</span><span class="sxs-lookup"><span data-stu-id="462de-194">When you see the **PagedList.Mvc** package, click **Install**.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="462de-195">**プロジェクトの選択**ボックスで、 **OK**します。</span><span class="sxs-lookup"><span data-stu-id="462de-195">In the **Select Projects** box, click **OK**.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="462de-196">Index メソッドにページング機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="462de-196">Add Paging Functionality to the Index Method</span></span>

<span data-ttu-id="462de-197">*Controllers\StudentController.cs*、追加、`using`のステートメント、`PagedList`名前空間。</span><span class="sxs-lookup"><span data-stu-id="462de-197">In *Controllers\StudentController.cs*, add a `using` statement for the `PagedList` namespace:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="462de-198">`Index` メソッドを次のコードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="462de-198">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="462de-199">このコードを追加、`page`パラメーター、現在の並べ替え順序パラメーター、およびメソッドのシグネチャを次に示すように、現在のフィルター パラメーター。</span><span class="sxs-lookup"><span data-stu-id="462de-199">This code adds a `page` parameter, a current sort order parameter, and a current filter parameter to the method signature, as shown here:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="462de-200">最初にページが表示されるとき、またはユーザーがページングや並べ替えのリンクをクリックしていない場合、すべてのパラメーターは null になります。</span><span class="sxs-lookup"><span data-stu-id="462de-200">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters will be null.</span></span> <span data-ttu-id="462de-201">ページングのリンクがクリックされた場合、`page`変数を表示するページ番号が含まれます。</span><span class="sxs-lookup"><span data-stu-id="462de-201">If a paging link is clicked, the `page` variable will contain the page number to display.</span></span>

<span data-ttu-id="462de-202">`A ViewBag` プロパティは、このページングの中に同じ並べ替え順序を維持するために、ページング リンクに含める必要があるため、ビューで、現在の並べ替え順序を提供します。</span><span class="sxs-lookup"><span data-stu-id="462de-202">`A ViewBag` property provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="462de-203">別のプロパティ、 `ViewBag.CurrentFilter`、現在のフィルター文字列でビューを提供します。</span><span class="sxs-lookup"><span data-stu-id="462de-203">Another property, `ViewBag.CurrentFilter`, provides the view with the current filter string.</span></span> <span data-ttu-id="462de-204">ページング中にフィルターの設定を維持するために、ページングのリンクにこの値を含める必要があり、ページが再表示されるときに、この値をテキスト ボックスに復元する必要があります。</span><span class="sxs-lookup"><span data-stu-id="462de-204">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span> <span data-ttu-id="462de-205">ページングの中に検索文字列を変更した場合は、新しいフィルターのために別のデータが表示されるため、ページを 1 にリセットする必要があります。</span><span class="sxs-lookup"><span data-stu-id="462de-205">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="462de-206">テキスト ボックスに値を入力し、[送信] ボタンが押されたときに、検索文字列が変更されます。</span><span class="sxs-lookup"><span data-stu-id="462de-206">The search string is changed when a value is entered in the text box and the submit button is pressed.</span></span> <span data-ttu-id="462de-207">その場合は、`searchString`パラメーターが null ではありません。</span><span class="sxs-lookup"><span data-stu-id="462de-207">In that case, the `searchString` parameter is not null.</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="462de-208">メソッドの最後に、`ToPagedList`拡張メソッド、受講者を`IQueryable`オブジェクトがページングをサポートするコレクション型の受講者の 1 つのページに学生クエリを変換します。</span><span class="sxs-lookup"><span data-stu-id="462de-208">At the end of the method, the `ToPagedList` extension method on the students `IQueryable` object converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="462de-209">その学生の 1 つのページは、ビューに渡されます。</span><span class="sxs-lookup"><span data-stu-id="462de-209">That single page of students is then passed to the view:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="462de-210">`ToPagedList` メソッドは、ページ番号を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="462de-210">The `ToPagedList` method takes a page number.</span></span> <span data-ttu-id="462de-211">2 つの疑問符を表す、 [null 合体演算子](https://msdn.microsoft.com/library/ms173224.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="462de-211">The two question marks represent the [null-coalescing operator](https://msdn.microsoft.com/library/ms173224.aspx).</span></span> <span data-ttu-id="462de-212">null 合体演算子は null 許容型の既定値を定義します。式 `(page ?? 1)` は、値がある場合は `page` の値を返し、`page` が null の場合は 1 を返すことを意味します。</span><span class="sxs-lookup"><span data-stu-id="462de-212">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

### <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="462de-213">Student インデックス ビューにページングのリンクを追加します。</span><span class="sxs-lookup"><span data-stu-id="462de-213">Add Paging Links to the Student Index View</span></span>

<span data-ttu-id="462de-214">*Views\Student\Index.cshtml*、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="462de-214">In *Views\Student\Index.cshtml*, replace the existing code with the following code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

<span data-ttu-id="462de-215">ページの上部にある `@model` ステートメントは、ビューが `List` オブジェクトの代わりに `PagedList` オブジェクトを取得するようになったことを指定します。</span><span class="sxs-lookup"><span data-stu-id="462de-215">The `@model` statement at the top of the page specifies that the view now gets a `PagedList` object instead of a `List` object.</span></span>

<span data-ttu-id="462de-216">`using`ステートメント`PagedList.Mvc`ページング ボタンの MVC ヘルパーにアクセスします。</span><span class="sxs-lookup"><span data-stu-id="462de-216">The `using` statement for `PagedList.Mvc` gives access to the MVC helper for the paging buttons.</span></span>

<span data-ttu-id="462de-217">コードのオーバー ロードを使用して[BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx)することを指定する、 [FormMethod.Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)します。</span><span class="sxs-lookup"><span data-stu-id="462de-217">The code uses an overload of [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) that allows it to specify [FormMethod.Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css).</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

<span data-ttu-id="462de-218">既定の[BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx)フォーム データをパラメーターとして渡されると、URL ではなく HTTP メッセージの本文にクエリ文字列は、投稿を送信します。</span><span class="sxs-lookup"><span data-stu-id="462de-218">The default [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="462de-219">HTTP GET を指定すると、フォーム データがクエリ文字列として URL で渡され、ユーザーが URL をブックマークできるようになります。</span><span class="sxs-lookup"><span data-stu-id="462de-219">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="462de-220">[HTTP GET を使用するための W3C のガイドライン](http://www.w3.org/2001/tag/doc/whenToUseGet.html)アクションは結果として更新しない場合は、GET を使用するように指定します。</span><span class="sxs-lookup"><span data-stu-id="462de-220">The [W3C guidelines for the use of HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) specify that you should use GET when the action does not result in an update.</span></span>

<span data-ttu-id="462de-221">テキスト ボックスは、新しいページをクリックすると、現在の検索文字列を表示できるように、現在の検索文字列で初期化されます。</span><span class="sxs-lookup"><span data-stu-id="462de-221">The text box is initialized with the current search string so when you click a new page you can see the current search string.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

<span data-ttu-id="462de-222">列ヘッダーへのリンクは、フィルターの結果内でユーザーが並べ替えられるように、クエリ文字列を使用してコントローラーに現在の検索文字列を渡します。</span><span class="sxs-lookup"><span data-stu-id="462de-222">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

<span data-ttu-id="462de-223">ページの現在のページとの合計数が表示されます。</span><span class="sxs-lookup"><span data-stu-id="462de-223">The current page and total number of pages are displayed.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

<span data-ttu-id="462de-224">表示するページがない場合は、「の 0 ページ 0」が表示されます。</span><span class="sxs-lookup"><span data-stu-id="462de-224">If there are no pages to display, "Page 0 of 0" is shown.</span></span> <span data-ttu-id="462de-225">(その場合、ページ番号は、ページ数より大きいため、 `Model.PageNumber` 1 に設定されてと`Model.PageCount`は 0 です)。</span><span class="sxs-lookup"><span data-stu-id="462de-225">(In that case the page number is greater than the page count because `Model.PageNumber` is 1, and `Model.PageCount` is 0.)</span></span>

<span data-ttu-id="462de-226">によってページング ボタンが表示されます、`PagedListPager`ヘルパー。</span><span class="sxs-lookup"><span data-stu-id="462de-226">The paging buttons are displayed by the `PagedListPager` helper:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

<span data-ttu-id="462de-227">`PagedListPager`ヘルパーはさまざまな Url を含むおよびスタイル設定、カスタマイズ可能なオプションを提供します。</span><span class="sxs-lookup"><span data-stu-id="462de-227">The `PagedListPager` helper provides a number of options that you can customize, including URLs and styling.</span></span> <span data-ttu-id="462de-228">詳細については、次を参照してください。 [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 、GitHub サイトでします。</span><span class="sxs-lookup"><span data-stu-id="462de-228">For more information, see [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) on the GitHub site.</span></span>

<span data-ttu-id="462de-229">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="462de-229">Run the page.</span></span>

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="462de-231">異なる並べ替え順でページングのリンクをクリックし、ページングが機能することを確認します。</span><span class="sxs-lookup"><span data-stu-id="462de-231">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="462de-232">その後で、検索文字列を入力して、ページングをもう一度試し、並べ替えとフィルター処理を使用してもページングが正しく機能することを確認します。</span><span class="sxs-lookup"><span data-stu-id="462de-232">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a><span data-ttu-id="462de-233">作成、学生の統計情報を表示するページについて</span><span class="sxs-lookup"><span data-stu-id="462de-233">Create an About Page That Shows Student Statistics</span></span>

<span data-ttu-id="462de-234">Contoso University web サイトのページについて、登録日付ごとに登録した受講者の数を表示します。</span><span class="sxs-lookup"><span data-stu-id="462de-234">For the Contoso University website's About page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="462de-235">これには、グループ化とグループに関する簡単な計算が必要です。</span><span class="sxs-lookup"><span data-stu-id="462de-235">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="462de-236">これを実行するためには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="462de-236">To accomplish this, you'll do the following:</span></span>

- <span data-ttu-id="462de-237">ビューに渡す必要があるデータのビュー モデル クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="462de-237">Create a view model class for the data that you need to pass to the view.</span></span>
- <span data-ttu-id="462de-238">変更、`About`メソッドで、`Home`コント ローラー。</span><span class="sxs-lookup"><span data-stu-id="462de-238">Modify the `About` method in the `Home` controller.</span></span>
- <span data-ttu-id="462de-239">変更、`About`ビュー。</span><span class="sxs-lookup"><span data-stu-id="462de-239">Modify the `About` view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="462de-240">ビュー モデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="462de-240">Create the View Model</span></span>

<span data-ttu-id="462de-241">作成、 *ViewModels*フォルダー。</span><span class="sxs-lookup"><span data-stu-id="462de-241">Create a *ViewModels* folder.</span></span> <span data-ttu-id="462de-242">クラス ファイルを追加、そのフォルダー内*EnrollmentDateGroup.cs*既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="462de-242">In that folder, add a class file *EnrollmentDateGroup.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="462de-243">Home コントローラーを変更する</span><span class="sxs-lookup"><span data-stu-id="462de-243">Modify the Home Controller</span></span>

<span data-ttu-id="462de-244">*HomeController.cs*、次の追加`using`ファイルの上部にあるステートメント。</span><span class="sxs-lookup"><span data-stu-id="462de-244">In *HomeController.cs*, add the following `using` statements at the top of the file:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="462de-245">クラスの中かっこの直後に、データベース コンテキストのクラスの変数を追加します。</span><span class="sxs-lookup"><span data-stu-id="462de-245">Add a class variable for the database context immediately after the opening curly brace for the class:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

<span data-ttu-id="462de-246">`About` メソッドを次のコードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="462de-246">Replace the `About` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="462de-247">LINQ ステートメントは、登録日で受講者エンティティをグループ化し、各グループ内のエンティティの数を計算して、結果を `EnrollmentDateGroup` ビュー モデル オブジェクトのコレクションに格納します。</span><span class="sxs-lookup"><span data-stu-id="462de-247">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>

<span data-ttu-id="462de-248">追加、`Dispose`メソッド。</span><span class="sxs-lookup"><span data-stu-id="462de-248">Add a `Dispose` method:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a><span data-ttu-id="462de-249">About ビューを変更する</span><span class="sxs-lookup"><span data-stu-id="462de-249">Modify the About View</span></span>

<span data-ttu-id="462de-250">コードに置き換えます、 *Views\Home\About.cshtml*を次のコード ファイル。</span><span class="sxs-lookup"><span data-stu-id="462de-250">Replace the code in the *Views\Home\About.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

<span data-ttu-id="462de-251">アプリを実行し、をクリックして、**について**リンク。</span><span class="sxs-lookup"><span data-stu-id="462de-251">Run the app and click the **About** link.</span></span> <span data-ttu-id="462de-252">登録の日付ごとの学生の数が、テーブルに表示されます。</span><span class="sxs-lookup"><span data-stu-id="462de-252">The count of students for each enrollment date is displayed in a table.</span></span>

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a><span data-ttu-id="462de-254">省略可能:アプリを Windows Azure にデプロイします。</span><span class="sxs-lookup"><span data-stu-id="462de-254">Optional: Deploy the app to Windows Azure</span></span>

<span data-ttu-id="462de-255">これまでに、アプリケーションを実行したローカル IIS Express で開発用コンピューターにします。</span><span class="sxs-lookup"><span data-stu-id="462de-255">So far your application has been running locally in IIS Express on your development computer.</span></span> <span data-ttu-id="462de-256">他のユーザーに、インターネット経由で使用できるように、web ホスティング プロバイダーにデプロイがあります。</span><span class="sxs-lookup"><span data-stu-id="462de-256">To make it available for other people to use over the Internet, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="462de-257">このチュートリアルのオプションのセクションで展開に Windows Azure の Web サイトに。</span><span class="sxs-lookup"><span data-stu-id="462de-257">In this optional section of the tutorial you'll deploy it to a Windows Azure Web Site.</span></span>

### <a name="using-code-first-migrations-to-deploy-the-database"></a><span data-ttu-id="462de-258">Code First Migrations を使用して、データベースを展開するには</span><span class="sxs-lookup"><span data-stu-id="462de-258">Using Code First Migrations to Deploy the Database</span></span>

<span data-ttu-id="462de-259">データベースを展開するには、Code First Migrations を使用します。</span><span class="sxs-lookup"><span data-stu-id="462de-259">To deploy the database you'll use Code First Migrations.</span></span> <span data-ttu-id="462de-260">Visual Studio から展開の設定を構成するために使用する発行プロファイルを作成するときに、というラベルの付いたチェック ボックスをオンします**実行 Code First Migrations (アプリケーションの起動時に実行)** します。</span><span class="sxs-lookup"><span data-stu-id="462de-260">When you create the publish profile that you use to configure settings for deploying from Visual Studio, you'll select a check box that is labeled **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="462de-261">この設定により、自動的にアプリケーションを構成する展開プロセス*Web.config* Code First を使用するように、移行先サーバー上のファイル、`MigrateDatabaseToLatestVersion`初期化子クラス。</span><span class="sxs-lookup"><span data-stu-id="462de-261">This setting causes the deployment process to automatically configure the application *Web.config* file on the destination server so that Code First uses the `MigrateDatabaseToLatestVersion` initializer class.</span></span>

<span data-ttu-id="462de-262">Visual Studio は行いませんデータベースで何か、展開プロセス中にします。</span><span class="sxs-lookup"><span data-stu-id="462de-262">Visual Studio does not do anything with the database during the deployment process.</span></span> <span data-ttu-id="462de-263">デプロイされたアプリケーションでは、デプロイ後に最初に、データベースにアクセス、Code First 自動的にデータベースを作成またはデータベース スキーマを最新バージョンに更新します。</span><span class="sxs-lookup"><span data-stu-id="462de-263">When the deployed application accesses the database for the first time after deployment, Code First automatically creates the database or updates the database schema to the latest version.</span></span> <span data-ttu-id="462de-264">アプリケーションは、移行を実装している場合`Seed`メソッド、メソッドの実行後、データベースが作成されるか、スキーマを更新します。</span><span class="sxs-lookup"><span data-stu-id="462de-264">If the application implements a Migrations `Seed` method, the method runs after the database is created or the schema is updated.</span></span>

<span data-ttu-id="462de-265">使用して移行`Seed`メソッドは、テスト データを挿入します。</span><span class="sxs-lookup"><span data-stu-id="462de-265">Your Migrations `Seed` method inserts test data.</span></span> <span data-ttu-id="462de-266">運用環境にデプロイする、変更する必要があります、`Seed`メソッドを実稼働データベースに挿入するデータの挿入のみであるためです。</span><span class="sxs-lookup"><span data-stu-id="462de-266">If you were deploying to a production environment, you would have to change the `Seed` method so that it only inserts data that you want to be inserted into your production database.</span></span> <span data-ttu-id="462de-267">たとえば、現在のデータ モデルで開発用データベースに実際のコースが架空の受講者がある可能性があります。</span><span class="sxs-lookup"><span data-stu-id="462de-267">For example, in your current data model you might want to have real courses but fictional students in the development database.</span></span> <span data-ttu-id="462de-268">記述することができます、`Seed`メソッドは負荷が開発では、両方とも、実稼働環境に展開する前に、架空の受講者をし、コメントをします。</span><span class="sxs-lookup"><span data-stu-id="462de-268">You can write a `Seed` method to load both in development, and then comment out the fictional students before you deploy to production.</span></span> <span data-ttu-id="462de-269">したり、作成することができます、`Seed`のみのコースを読み込むし、アプリケーションの UI を使用して手動でテスト データベースで架空の受講者を入力します。</span><span class="sxs-lookup"><span data-stu-id="462de-269">Or you can write a `Seed` method to load only courses, and enter the fictional students in the test database manually by using the application's UI.</span></span>

### <a name="get-a-windows-azure-account"></a><span data-ttu-id="462de-270">Windows Azure アカウントを取得します。</span><span class="sxs-lookup"><span data-stu-id="462de-270">Get a Windows Azure account</span></span>

<span data-ttu-id="462de-271">Windows Azure アカウントが必要があります。</span><span class="sxs-lookup"><span data-stu-id="462de-271">You'll need a Windows Azure account.</span></span> <span data-ttu-id="462de-272">1 つをいない場合は、ほんの数分で無料試用版アカウントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="462de-272">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="462de-273">詳細については、次を参照してください。 [Windows Azure の無料試用版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)します。</span><span class="sxs-lookup"><span data-stu-id="462de-273">For details, see [Windows Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a><span data-ttu-id="462de-274">Windows Azure での web サイトと SQL database を作成します。</span><span class="sxs-lookup"><span data-stu-id="462de-274">Create a web site and a SQL database in Windows Azure</span></span>

<span data-ttu-id="462de-275">Windows Azure の Web サイトは、Windows Azure の他のクライアントと共有されている仮想マシン (Vm) で実行されることを意味する共有ホスティング環境で実行されます。</span><span class="sxs-lookup"><span data-stu-id="462de-275">Your Windows Azure Web Site will run in a shared hosting environment, which means it runs on virtual machines (VMs) that are shared with other Windows Azure clients.</span></span> <span data-ttu-id="462de-276">共有ホスティング環境は、クラウドで開始する低コスト方法です。</span><span class="sxs-lookup"><span data-stu-id="462de-276">A shared hosting environment is a low-cost way to get started in the cloud.</span></span> <span data-ttu-id="462de-277">後で、web トラフィックが増加すると、アプリケーションは専用 Vm 上で実行して、ニーズを満たすためにスケールできます。</span><span class="sxs-lookup"><span data-stu-id="462de-277">Later, if your web traffic increases, the application can scale to meet the need by running on dedicated VMs.</span></span> <span data-ttu-id="462de-278">複雑なアーキテクチャが必要な場合、Windows Azure のクラウド サービスに移行することができます。</span><span class="sxs-lookup"><span data-stu-id="462de-278">If you need a more complex architecture, you can migrate to a Windows Azure Cloud Service.</span></span> <span data-ttu-id="462de-279">クラウド サービスは、必要に応じて構成できる専用の Vm で実行します。</span><span class="sxs-lookup"><span data-stu-id="462de-279">Cloud services run on dedicated VMs that you can configure according to your needs.</span></span>

<span data-ttu-id="462de-280">Windows Azure SQL Database とは、SQL Server テクノロジに基づいて構築されたクラウド ベースのリレーショナル データベース サービスです。</span><span class="sxs-lookup"><span data-stu-id="462de-280">Windows Azure SQL Database is a cloud-based relational database service that is built on SQL Server technologies.</span></span> <span data-ttu-id="462de-281">ツールおよび SQL Server で動作するアプリケーションは、SQL database でも動作します。</span><span class="sxs-lookup"><span data-stu-id="462de-281">Tools and applications that work with SQL Server also work with SQL Database.</span></span>

1. <span data-ttu-id="462de-282">[Windows Azure 管理ポータル](https://manage.windowsazure.com/)、 をクリックして**Websites**で左側のタブをクリック**新規**します。</span><span class="sxs-lookup"><span data-stu-id="462de-282">In the [Windows Azure Management Portal](https://manage.windowsazure.com/), click **Web Sites** in the left tab, and then click **New**.</span></span>

    ![管理ポータルで新しいボタン](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. <span data-ttu-id="462de-284">クリックして**カスタム作成**です。</span><span class="sxs-lookup"><span data-stu-id="462de-284">Click **CUSTOM CREATE**.</span></span>

    ![管理ポータルでデータベースのリンクを作成します。](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

   <span data-ttu-id="462de-286">**新しい Web サイト - カスタム作成**ウィザードが開きます。</span><span class="sxs-lookup"><span data-stu-id="462de-286">The **New Web Site - Custom Create** wizard opens.</span></span>
3. <span data-ttu-id="462de-287">**新しい Web サイト**手順と、ウィザードの文字列を入力、 **URL**ボックス、アプリケーションの一意の URL として使用します。</span><span class="sxs-lookup"><span data-stu-id="462de-287">In the **New Web Site** step of the wizard, enter a string in the **URL** box to use as the unique URL for your application.</span></span> <span data-ttu-id="462de-288">完全な URL は、ここで入力とテキスト ボックスの横に表示されるサフィックスで構成されます。</span><span class="sxs-lookup"><span data-stu-id="462de-288">The complete URL will consist of what you enter here plus the suffix that you see next to the text box.</span></span> <span data-ttu-id="462de-289">図に、"ConU"を示しますが、別のアカウントを選択する必要がありますので、その URL が実行される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="462de-289">The illustration shows "ConU", but that URL is probably taken so you will have to choose a different one.</span></span>

    ![管理ポータルでデータベースのリンクを作成します。](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. <span data-ttu-id="462de-291">**リージョン**ドロップダウン リストで、近くのリージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="462de-291">In the **Region** drop-down list, choose a region close to you.</span></span> <span data-ttu-id="462de-292">この設定では、web サイトが実行されるデータ センターを指定します。</span><span class="sxs-lookup"><span data-stu-id="462de-292">This setting specifies which data center your web site will run in.</span></span>
5. <span data-ttu-id="462de-293">**データベース**ドロップダウン リストで、選択**無料の 20 MB SQL database を作成する**します。</span><span class="sxs-lookup"><span data-stu-id="462de-293">In the **Database** drop-down list, choose **Create a free 20 MB SQL database**.</span></span>

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. <span data-ttu-id="462de-294">**DB 接続文字列名**、入力*SchoolContext*します。</span><span class="sxs-lookup"><span data-stu-id="462de-294">In the **DB CONNECTION STRING NAME**, enter *SchoolContext*.</span></span>

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. <span data-ttu-id="462de-295">ボックスの下部にある右を指している矢印をクリックします。</span><span class="sxs-lookup"><span data-stu-id="462de-295">Click the arrow that points to the right at the bottom of the box.</span></span> <span data-ttu-id="462de-296">ウィザード、**データベース設定**手順。</span><span class="sxs-lookup"><span data-stu-id="462de-296">The wizard advances to the **Database Settings** step.</span></span>
8. <span data-ttu-id="462de-297">**名前**ボックスに、入力*ContosoUniversityDB*します。</span><span class="sxs-lookup"><span data-stu-id="462de-297">In the **Name** box, enter *ContosoUniversityDB*.</span></span>
9. <span data-ttu-id="462de-298">**Server**ボックスで、**新しい SQL Database server**します。</span><span class="sxs-lookup"><span data-stu-id="462de-298">In the **Server** box, select **New SQL Database server**.</span></span> <span data-ttu-id="462de-299">または、以前にサーバーを作成する場合は、ドロップダウン リストからそのサーバーを選択できます。</span><span class="sxs-lookup"><span data-stu-id="462de-299">Alternatively, if you previously created a server, you can select that server from the drop-down list.</span></span>
10. <span data-ttu-id="462de-300">管理者が入力**ログイン名**と**パスワード**します。</span><span class="sxs-lookup"><span data-stu-id="462de-300">Enter an administrator **LOGIN NAME** and **PASSWORD**.</span></span> <span data-ttu-id="462de-301">選択した場合**新しい SQL Database server**既存の名前とパスワードでは入力は、データベースにアクセスするときに後で使用するパスワードを今すぐを定義して新しい名前を入力してください。</span><span class="sxs-lookup"><span data-stu-id="462de-301">If you selected **New SQL Database server** you aren't entering an existing name and password here, you're entering a new name and password that you're defining now to use later when you access the database.</span></span> <span data-ttu-id="462de-302">以前に作成したサーバーを選択した場合は、そのサーバーの資格情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="462de-302">If you selected a server that you created previously, you'll enter credentials for that server.</span></span> <span data-ttu-id="462de-303">このチュートリアルでは、選択したしません、***詳細***チェック ボックスをオンします。</span><span class="sxs-lookup"><span data-stu-id="462de-303">For this tutorial, you won't select the ***Advanced*** check box.</span></span> <span data-ttu-id="462de-304">***詳細***オプションを使用するデータベースを設定する[照合順序](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)します。</span><span class="sxs-lookup"><span data-stu-id="462de-304">The ***Advanced*** options enable you to set the database [collation](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx).</span></span>
11. <span data-ttu-id="462de-305">同じ選択**リージョン**で選択した web サイト。</span><span class="sxs-lookup"><span data-stu-id="462de-305">Choose the same **Region** that you chose for the web site.</span></span>
12. <span data-ttu-id="462de-306">完了することを示すために、ボックスの右下にあるチェック マークをクリックします。</span><span class="sxs-lookup"><span data-stu-id="462de-306">Click the check mark at the bottom right of the box to indicate that you're finished.</span></span>   
  
    ![データベースの設定手順は、新しい Web サイトで-データベースとともに作成ウィザード](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

    <span data-ttu-id="462de-308">次の図は、既存の SQL Server とログインを使用します。</span><span class="sxs-lookup"><span data-stu-id="462de-308">The following image shows using an existing SQL Server and Login.</span></span>   
  
    ![データベースの設定手順は、新しい Web サイトで-データベースとともに作成ウィザード](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
    <span data-ttu-id="462de-310">管理ポータル Web サイトのページに戻り、**状態**列は、サイトが作成されていることを示しています。</span><span class="sxs-lookup"><span data-stu-id="462de-310">The Management Portal returns to the Web Sites page, and the **Status** column shows that the site is being created.</span></span> <span data-ttu-id="462de-311">(通常、1 分未満)、しばらくしてから、**状態**列は、サイトが正常に作成されたことを示しています。</span><span class="sxs-lookup"><span data-stu-id="462de-311">After a while (typically less than a minute), the **Status** column shows that the site was successfully created.</span></span> <span data-ttu-id="462de-312">自分のアカウントで所有するサイトの数を横に表示、左側のナビゲーション バーで、 **Websites**アイコン、およびデータベースの数が横に表示されます、 **SQL データベース**アイコン。</span><span class="sxs-lookup"><span data-stu-id="462de-312">In the navigation bar at the left, the number of sites you have in your account appears next to the **Web Sites** icon, and the number of databases appears next to the **SQL Databases** icon.</span></span>

## <a name="deploy-the-application-to-windows-azure"></a><span data-ttu-id="462de-313">Windows Azure へのアプリケーションをデプロイします。</span><span class="sxs-lookup"><span data-stu-id="462de-313">Deploy the application to Windows Azure</span></span>

1. <span data-ttu-id="462de-314">Visual Studio でのプロジェクトを右クリックして**ソリューション エクスプ ローラー**選択と**発行**コンテキスト メニュー。</span><span class="sxs-lookup"><span data-stu-id="462de-314">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>  
  
    ![プロジェクトのコンテキスト メニューを発行します。](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. <span data-ttu-id="462de-316">**プロファイル**のタブ、 **Web の発行**ウィザード、をクリックして**インポート**します。</span><span class="sxs-lookup"><span data-stu-id="462de-316">In the **Profile** tab of the **Publish Web** wizard, click **Import**.</span></span>  
  
    ![発行設定のインポート](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. <span data-ttu-id="462de-318">以前、Windows Azure サブスクリプションを Visual Studio に追加していない場合は、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="462de-318">If you have not previously added your Windows Azure subscription in Visual Studio, perform the following steps.</span></span> <span data-ttu-id="462de-319">これらの手順で追加、サブスクリプション下で、ドロップダウン リストを一覧表示するため**Windows Azure の web サイトからのインポート**web サイトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="462de-319">In these steps you add your subscription so that the drop-down list under **Import from a Windows Azure web site** will include your web site.</span></span>

    <span data-ttu-id="462de-320">a. </span><span class="sxs-lookup"><span data-stu-id="462de-320">a.</span></span> <span data-ttu-id="462de-321">**発行プロファイルのインポート**ダイアログ ボックスで、をクリックして**Windows Azure の web サイトからのインポート**、順にクリックします**Windows Azure サブスクリプションの追加**します。</span><span class="sxs-lookup"><span data-stu-id="462de-321">In the **Import Publish Profile** dialog box, click **Import from a Windows Azure web site**, and then click **Add Windows Azure subscription**.</span></span>

    ![Windows Azure サブスクリプションを追加します。](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    <span data-ttu-id="462de-323">b. </span><span class="sxs-lookup"><span data-stu-id="462de-323">b.</span></span> <span data-ttu-id="462de-324">**Windows Azure サブスクリプションのインポート**ダイアログ ボックスで、をクリックして**サブスクリプション ファイルのダウンロード**します。</span><span class="sxs-lookup"><span data-stu-id="462de-324">In the **Import Windows Azure Subscriptions** dialog box, click **Download subscription file**.</span></span>

    ![サブスクリプション ファイルのダウンロード](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    <span data-ttu-id="462de-326">c.</span><span class="sxs-lookup"><span data-stu-id="462de-326">c.</span></span> <span data-ttu-id="462de-327">ブラウザー ウィンドウでは、保存、 *.publishsettings*ファイル。</span><span class="sxs-lookup"><span data-stu-id="462de-327">In your browser window, save the *.publishsettings* file.</span></span>

    ![.publishsettings ファイルをダウンロードします。](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > <span data-ttu-id="462de-329">セキュリティ -、 *publishsettings*ファイルには、Windows Azure サブスクリプションとサービスの管理に使用される (エンコードされていない) 資格情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="462de-329">Security - The *publishsettings* file contains your credentials (unencoded) that are used to administer your Windows Azure subscriptions and services.</span></span> <span data-ttu-id="462de-330">このファイルのセキュリティのベスト プラクティスは、ソース ディレクトリの外に一時的に保存するため (たとえば、 *libraries \documents*フォルダー)、してから、インポートが完了したら削除します。</span><span class="sxs-lookup"><span data-stu-id="462de-330">The security best practice for this file is to store it temporarily outside your source directories (for example in the *Libraries\Documents* folder), and then delete it once the import has completed.</span></span> <span data-ttu-id="462de-331">アクセスした悪意のあるユーザー、`.publishsettings`ファイルは、編集、作成、および Windows Azure のサービスを削除します。</span><span class="sxs-lookup"><span data-stu-id="462de-331">A malicious user who gains access to the `.publishsettings` file can edit, create, and delete your Windows Azure services.</span></span>

    <span data-ttu-id="462de-332">d.</span><span class="sxs-lookup"><span data-stu-id="462de-332">d.</span></span> <span data-ttu-id="462de-333">**Windows Azure サブスクリプションのインポート**ダイアログ ボックスで、をクリックして**参照**に移動し、 *.publishsettings*ファイル。</span><span class="sxs-lookup"><span data-stu-id="462de-333">In the **Import Windows Azure Subscriptions** dialog box, click **Browse** and navigate to the *.publishsettings* file.</span></span>

    ![サブスクリプションをダウンロードします。](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    <span data-ttu-id="462de-335">e.</span><span class="sxs-lookup"><span data-stu-id="462de-335">e.</span></span> <span data-ttu-id="462de-336">**[インポート]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="462de-336">Click **Import**.</span></span>

    ![import](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. <span data-ttu-id="462de-338">**発行プロファイルのインポート**ダイアログ ボックスで、 **Windows Azure の web サイトからのインポート**ボックスの一覧から web サイトを選択し、クリックして**OK**します。</span><span class="sxs-lookup"><span data-stu-id="462de-338">In the **Import Publish Profile** dialog box, select **Import from a Windows Azure web site**, select your web site from the drop-down list, and then click **OK**.</span></span>  
  
    ![発行プロファイルのインポート](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. <span data-ttu-id="462de-340">**接続**] タブで [**接続の検証**設定が正しいことを確認します。</span><span class="sxs-lookup"><span data-stu-id="462de-340">In the **Connection** tab, click **Validate Connection** to make sure that the settings are correct.</span></span>  
  
    ![接続を検証します。](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. <span data-ttu-id="462de-342">横に緑色のチェック マークが表示、接続が検証されると、**接続の検証**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="462de-342">When the connection has been validated, a green check mark is shown next to the **Validate Connection** button.</span></span> <span data-ttu-id="462de-343">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="462de-343">Click **Next**.</span></span>  
  
    ![検証が成功した接続](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. <span data-ttu-id="462de-345">開く、**リモート接続文字列**下のドロップダウン リスト**SchoolContext**作成したデータベースの接続文字列を選択します。</span><span class="sxs-lookup"><span data-stu-id="462de-345">Open the **Remote connection string** drop-down list under **SchoolContext** and select the connection string for the database you created.</span></span>
8. <span data-ttu-id="462de-346">選択**実行 Code First Migrations (アプリケーションの起動時に実行)** します。</span><span class="sxs-lookup"><span data-stu-id="462de-346">Select **Execute Code First Migrations (runs on application start)**.</span></span>
9. <span data-ttu-id="462de-347">オフに**実行時にこの接続文字列を使用して**の**UserContext (DefaultConnection)**、このアプリケーションは、メンバーシップ データベースを使用していないためです。</span><span class="sxs-lookup"><span data-stu-id="462de-347">Uncheck **Use this connection string at runtime** for the **UserContext (DefaultConnection)**, since this application is not using the membership database.</span></span>   
  
    ![Settings tab](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. <span data-ttu-id="462de-349">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="462de-349">Click **Next**.</span></span>
11. <span data-ttu-id="462de-350">**プレビュー** ] タブで [**プレビューの開始**します。</span><span class="sxs-lookup"><span data-stu-id="462de-350">In the **Preview** tab, click **Start Preview**.</span></span>  
  
    ![[プレビュー] タブの [開始] ボタン](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
    <span data-ttu-id="462de-352">タブには、サーバーにコピーされるファイルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="462de-352">The tab displays a list of the files that will be copied to the server.</span></span> <span data-ttu-id="462de-353">プレビューを表示するアプリケーションを発行する必要はありませんが、便利な機能に注意してください。</span><span class="sxs-lookup"><span data-stu-id="462de-353">Displaying the preview isn't required to publish the application but is a useful function to be aware of.</span></span> <span data-ttu-id="462de-354">この場合、表示されるファイルの一覧に何もする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="462de-354">In this case, you don't need to do anything with the list of files that is displayed.</span></span> <span data-ttu-id="462de-355">次に、このアプリケーションをデプロイするとき、変更されたファイルのみがこの一覧になります。</span><span class="sxs-lookup"><span data-stu-id="462de-355">The next time you deploy this application, only the files that have changed will be in this list.</span></span>  
  
    ![StartPreview ファイルの出力](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. <span data-ttu-id="462de-357">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="462de-357">Click **Publish**.</span></span>  
    <span data-ttu-id="462de-358">Visual Studio では、Windows Azure サーバーにファイルをコピーするプロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="462de-358">Visual Studio begins the process of copying the files to the Windows Azure server.</span></span>
13. <span data-ttu-id="462de-359">**出力**ウィンドウが実行されたどのようなデプロイ操作を示しています。 され、展開が正常に完了を報告します。</span><span class="sxs-lookup"><span data-stu-id="462de-359">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>  
  
    ![展開の成功を示す出力ウィンドウ](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. <span data-ttu-id="462de-361">デプロイが成功、既定のブラウザーは自動的にデプロイされた web サイトの URL を開きます。</span><span class="sxs-lookup"><span data-stu-id="462de-361">Upon successful deployment, the default browser automatically opens to the URL of the deployed web site.</span></span>  
    <span data-ttu-id="462de-362">作成したアプリケーションは、クラウドで実行されているようになりました。</span><span class="sxs-lookup"><span data-stu-id="462de-362">The application you created is now running in the cloud.</span></span> <span data-ttu-id="462de-363">受講者 タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="462de-363">Click the Students tab.</span></span>  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

<span data-ttu-id="462de-365">この時点で、 *SchoolContext*を選択したので、Windows Azure SQL Database でデータベースが作成されている**実行 Code First Migrations (アプリの起動時に実行)** します。</span><span class="sxs-lookup"><span data-stu-id="462de-365">At this point your *SchoolContext* database has been created in the Windows Azure SQL Database because you selected **Execute Code First Migrations (runs on app start)**.</span></span> <span data-ttu-id="462de-366">*Web.config*デプロイされた web サイトのファイルが変更されているように、 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初期化子は、最初に、コードの読み取りまたはデータベースにデータを書き込みを実行 (選択したときに発生、**学生** タブ)。</span><span class="sxs-lookup"><span data-stu-id="462de-366">The *Web.config* file in the deployed web site has been changed so that the [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) initializer would run the first time your code reads or writes data in the database (which happened when you selected the **Students** tab):</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

<span data-ttu-id="462de-367">展開プロセスは、新しい接続文字列を作成することも *(SchoolContext\_DatabasePublish*)、データベース スキーマを更新して、データベースをシード処理を使用する Code First Migrations に対する。</span><span class="sxs-lookup"><span data-stu-id="462de-367">The deployment process also created a new connection string *(SchoolContext\_DatabasePublish*) for Code First Migrations to use for updating the database schema and seeding the database.</span></span>

![Database_Publish connection string](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

<span data-ttu-id="462de-369">*DefaultConnection* (これは、このチュートリアルでは使用しません)、メンバーシップ データベースの接続文字列です。</span><span class="sxs-lookup"><span data-stu-id="462de-369">The *DefaultConnection* connection string is for the membership database (which we are not using in this tutorial).</span></span> <span data-ttu-id="462de-370">*SchoolContext* ContosoUniversity データベースの接続文字列です。</span><span class="sxs-lookup"><span data-stu-id="462de-370">The *SchoolContext* connection string is for the ContosoUniversity database.</span></span>

<span data-ttu-id="462de-371">デプロイされたバージョンので、自分のコンピューター上の Web.config ファイルを検索する*ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*します。デプロイされているアクセスできる*Web.config* FTP を使用してファイル自体。</span><span class="sxs-lookup"><span data-stu-id="462de-371">You can find the deployed version of the Web.config file on your own computer in *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*. You can access the deployed *Web.config* file itself by using FTP.</span></span> <span data-ttu-id="462de-372">手順については、次を参照してください。 [Visual Studio を使用して ASP.NET Web 展開。コードの更新を展開する](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)します。</span><span class="sxs-lookup"><span data-stu-id="462de-372">For instructions, see [ASP.NET Web Deployment using Visual Studio: Deploying a Code Update](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md).</span></span> <span data-ttu-id="462de-373">始まる手順"、FTP ツールを使用するには、するには、次の 3 つが必要です: FTP の URL、ユーザー名、およびパスワード。"。</span><span class="sxs-lookup"><span data-stu-id="462de-373">Follow the instructions that start with "To use an FTP tool, you need three things: the FTP URL, the user name, and the password."</span></span>

> [!NOTE]
> <span data-ttu-id="462de-374">Web アプリの URL を見つけた他のユーザー データを変更できるように、セキュリティを実装しません。</span><span class="sxs-lookup"><span data-stu-id="462de-374">The web app doesn't implement security, so anyone who finds the URL can change the data.</span></span> <span data-ttu-id="462de-375">Web サイトをセキュリティで保護する方法の詳細については、次を参照してください。[メンバーシップ、OAuth、SQL Database を使用した安全な ASP.NET MVC アプリを Windows Azure の Web サイトにデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)します。</span><span class="sxs-lookup"><span data-stu-id="462de-375">For instructions on how to secure the web site, see [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to a Windows Azure Web Site](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="462de-376">他の人が、Windows Azure 管理ポータルを使用して、サイトを使用するようにまたは**サーバー エクスプ ローラー** Visual Studio で、サイトを停止します。</span><span class="sxs-lookup"><span data-stu-id="462de-376">You can prevent other people from using the site by using the Windows Azure Management Portal or **Server Explorer** in Visual Studio to stop the site.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a><span data-ttu-id="462de-377">コードの最初の初期化子</span><span class="sxs-lookup"><span data-stu-id="462de-377">Code First Initializers</span></span>

<span data-ttu-id="462de-378">展開に関するセクションで説明しました、 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初期化子が使用されています。</span><span class="sxs-lookup"><span data-stu-id="462de-378">In the deployment section you saw the [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) initializer being used.</span></span> <span data-ttu-id="462de-379">最初のコードなど、使用できるその他の初期化子を提供[CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (既定)、 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx)と[DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)します。</span><span class="sxs-lookup"><span data-stu-id="462de-379">Code First also provides other initializers that you can use, including [CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (the default), [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) and [DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx).</span></span> <span data-ttu-id="462de-380">`DropCreateAlways`初期化子は、単体テストの条件の設定に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="462de-380">The `DropCreateAlways` initializer can be useful for setting up conditions for unit tests.</span></span> <span data-ttu-id="462de-381">独自の初期化子を記述することもでき、明示的に、アプリケーションから読み取るか、データベースに書き込むまで待機するたくない場合、初期化子を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="462de-381">You can also write your own initializers, and you can call an initializer explicitly if you don't want to wait until the application reads from or writes to the database.</span></span> <span data-ttu-id="462de-382">初期化子の包括的な説明については、この書籍の第 6 章を参照してください。 [Entity Framework のプログラミング。コード ファースト](http://shop.oreilly.com/product/0636920022220.do)を Julie Lerman が Rowan Miller が。</span><span class="sxs-lookup"><span data-stu-id="462de-382">For a comprehensive explanation of initializers, see chapter 6 of the book [Programming Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) by Julie Lerman and Rowan Miller.</span></span>

## <a name="summary"></a><span data-ttu-id="462de-383">まとめ</span><span class="sxs-lookup"><span data-stu-id="462de-383">Summary</span></span>

<span data-ttu-id="462de-384">このチュートリアルでは、データ モデルを作成して、基本的な CRUD、並べ替え、フィルター、ページング、および機能をグループ化を実装する方法を説明しました。</span><span class="sxs-lookup"><span data-stu-id="462de-384">In this tutorial you've seen how to create a data model and implement basic CRUD, sorting, filtering, paging, and grouping functionality.</span></span> <span data-ttu-id="462de-385">次のチュートリアルでは、データ モデルを展開してより高度なトピックを見てが始めます。</span><span class="sxs-lookup"><span data-stu-id="462de-385">In the next tutorial you'll begin looking at more advanced topics by expanding the data model.</span></span>

<span data-ttu-id="462de-386">その他の Entity Framework リソースへのリンクが記載されて、 [ASP.NET データ アクセス コンテンツ マップ](../../../../whitepapers/aspnet-data-access-content-map.md)します。</span><span class="sxs-lookup"><span data-stu-id="462de-386">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="462de-387">[前へ](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
> [次へ](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="462de-387">[Previous](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
[Next](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)</span></span>
