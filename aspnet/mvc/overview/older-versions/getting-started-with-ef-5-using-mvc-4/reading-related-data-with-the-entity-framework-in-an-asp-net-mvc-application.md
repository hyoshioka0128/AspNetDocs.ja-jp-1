---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC アプリケーションでの Entity Framework を使用した関連データの読み取り (5/10) |Microsoft Docs
author: tdykstra
description: Contoso 大学のサンプル web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: e1752022b66952783039fbea0c2880e2f9be6ef8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595209"
---
# <a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a><span data-ttu-id="c55a3-103">ASP.NET MVC アプリケーションでの Entity Framework を使用した関連データの読み取り (5/10)</span><span class="sxs-lookup"><span data-stu-id="c55a3-103">Reading Related Data with the Entity Framework in an ASP.NET MVC Application (5 of 10)</span></span>

<span data-ttu-id="c55a3-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c55a3-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="c55a3-105">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="c55a3-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="c55a3-106">Contoso 大学のサンプル web アプリケーションは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="c55a3-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="c55a3-107">チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c55a3-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="c55a3-108">チュートリアルシリーズは、最初から開始するか、[この章のスタートプロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)して開始することができます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="c55a3-109">解決できない問題が発生した場合は、完成した[章をダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、問題の再現を試みてください。</span><span class="sxs-lookup"><span data-stu-id="c55a3-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="c55a3-110">一般に、コードと完成したコードを比較することで、問題の解決策を見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="c55a3-111">一般的なエラーとその解決方法については、「[エラーと回避策](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c55a3-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="c55a3-112">前のチュートリアルでは、School データモデルを完成しました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-112">In the previous tutorial you completed the School data model.</span></span> <span data-ttu-id="c55a3-113">このチュートリアルでは、関連データ (Entity Framework がナビゲーションプロパティに読み込むデータ) の読み取りと表示を行います。</span><span class="sxs-lookup"><span data-stu-id="c55a3-113">In this tutorial you'll read and display related data — that is, data that the Entity Framework loads into navigation properties.</span></span>

<span data-ttu-id="c55a3-114">以下の図は、使用するページを示しています。</span><span class="sxs-lookup"><span data-stu-id="c55a3-114">The following illustrations show the pages that you'll work with.</span></span>

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a><span data-ttu-id="c55a3-116">関連データの遅延、一括、明示的な読み込み</span><span class="sxs-lookup"><span data-stu-id="c55a3-116">Lazy, Eager, and Explicit Loading of Related Data</span></span>

<span data-ttu-id="c55a3-117">Entity Framework がエンティティのナビゲーションプロパティに関連データを読み込むには、いくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-117">There are several ways that the Entity Framework can load related data into the navigation properties of an entity:</span></span>

- <span data-ttu-id="c55a3-118">*遅延読み込み*。</span><span class="sxs-lookup"><span data-stu-id="c55a3-118">*Lazy loading*.</span></span> <span data-ttu-id="c55a3-119">エンティティが最初に読み込まれるときに、関連データは取得されません。</span><span class="sxs-lookup"><span data-stu-id="c55a3-119">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="c55a3-120">ただし、ナビゲーション プロパティに初めてアクセスしようとすると、そのナビゲーション プロパティに必要なデータが自動的に取得されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-120">However, the first time you attempt to access a navigation property, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="c55a3-121">この結果、複数のクエリがデータベースに送信されます。1つはエンティティ自体に対して、もう1つはエンティティの関連データを取得する必要があるときです。</span><span class="sxs-lookup"><span data-stu-id="c55a3-121">This results in multiple queries sent to the database — one for the entity itself and one each time that related data for the entity must be retrieved.</span></span> 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- <span data-ttu-id="c55a3-123">*一括読み込み*。</span><span class="sxs-lookup"><span data-stu-id="c55a3-123">*Eager loading*.</span></span> <span data-ttu-id="c55a3-124">エンティティが読み取られるときに、関連データがエンティティと共に取得されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-124">When the entity is read, related data is retrieved along with it.</span></span> <span data-ttu-id="c55a3-125">これは通常、必要なすべてのデータを取得する 1 つの結合クエリになります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-125">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="c55a3-126">一括読み込みは、`Include` メソッドを使用して指定します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-126">You specify eager loading by using the `Include` method.</span></span>

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- <span data-ttu-id="c55a3-128">*明示的読み込み*。</span><span class="sxs-lookup"><span data-stu-id="c55a3-128">*Explicit loading*.</span></span> <span data-ttu-id="c55a3-129">これは、コード内の関連データを明示的に取得する点を除いて、遅延読み込みに似ています。ナビゲーションプロパティにアクセスしても、自動的には発生しません。</span><span class="sxs-lookup"><span data-stu-id="c55a3-129">This is similar to lazy loading, except that you explicitly retrieve the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="c55a3-130">関連データを手動で読み込むには、エンティティのオブジェクト状態マネージャーエントリを取得し、コレクションの `Collection.Load` メソッドを呼び出すか、1つのエンティティを保持するプロパティの `Reference.Load` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-130">You load related data manually by getting the object state manager entry for an entity and calling the `Collection.Load` method for collections or the `Reference.Load` method for properties that hold a single entity.</span></span> <span data-ttu-id="c55a3-131">(次の例では、管理者ナビゲーションプロパティを読み込む場合は、`Collection(x => x.Courses)` を `Reference(x => x.Administrator)`に置き換えます)。</span><span class="sxs-lookup"><span data-stu-id="c55a3-131">(In the following example, if you wanted to load the Administrator navigation property, you'd replace `Collection(x => x.Courses)` with `Reference(x => x.Administrator)`.)</span></span>

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

<span data-ttu-id="c55a3-133">遅延読み込みと明示的な読み込みは、すぐにプロパティ値を取得しないため、*遅延読み込み*とも呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-133">Because they don't immediately retrieve the property values, lazy loading and explicit loading are also both known as *deferred loading*.</span></span>

<span data-ttu-id="c55a3-134">一般に、取得したすべてのエンティティに関連データが必要であることがわかっている場合は、一括読み込みで最高のパフォーマンスが得られます。これは、データベースに送信される単一のクエリは、通常、取得されたエンティティごとに個別のクエリよりも効率的であるためです。</span><span class="sxs-lookup"><span data-stu-id="c55a3-134">In general, if you know you need related data for every entity retrieved, eager loading offers the best performance, because a single query sent to the database is typically more efficient than separate queries for each entity retrieved.</span></span> <span data-ttu-id="c55a3-135">たとえば、上記の例では、各部門に関連コースが10個あるとします。</span><span class="sxs-lookup"><span data-stu-id="c55a3-135">For example, in the above examples, suppose that each department has ten related courses.</span></span> <span data-ttu-id="c55a3-136">一括読み込みの例では、単一の (結合) クエリと、データベースへの1回のラウンドトリップだけが発生します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-136">The eager loading example would result in just a single (join) query and a single round trip to the database.</span></span> <span data-ttu-id="c55a3-137">遅延読み込みと明示的な読み込みの例では、両方とも11個のクエリと、データベースへの11回のラウンドトリップが発生します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-137">The lazy loading and explicit loading examples would both result in eleven queries and eleven round trips to the database.</span></span> <span data-ttu-id="c55a3-138">データベースとの余分なラウンド トリップは、特に待ち時間が長いときのパフォーマンスに悪影響をもたらします。</span><span class="sxs-lookup"><span data-stu-id="c55a3-138">The extra round trips to the database are especially detrimental to performance when latency is high.</span></span>

<span data-ttu-id="c55a3-139">一方、シナリオによっては、遅延読み込みの方が効率的です。</span><span class="sxs-lookup"><span data-stu-id="c55a3-139">On the other hand, in some scenarios lazy loading is more efficient.</span></span> <span data-ttu-id="c55a3-140">一括読み込みでは、非常に複雑な結合が生成される可能性がありますが、SQL Server は効率的に処理できません。</span><span class="sxs-lookup"><span data-stu-id="c55a3-140">Eager loading might cause a very complex join to be generated, which SQL Server can't process efficiently.</span></span> <span data-ttu-id="c55a3-141">また、処理している一連のエンティティのサブセットに対してのみエンティティのナビゲーションプロパティにアクセスする必要がある場合は、一括読み込みで必要以上のデータを取得するため、遅延読み込みの方がパフォーマンスが向上する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-141">Or if you need to access an entity's navigation properties only for a subset of a set of entities you're processing, lazy loading might perform better because eager loading would retrieve more data than you need.</span></span> <span data-ttu-id="c55a3-142">パフォーマンスが重要な場合、最適な選択を行うために、両方の方法でパフォーマンスをテストすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c55a3-142">If performance is critical, it's best to test performance both ways in order to make the best choice.</span></span>

<span data-ttu-id="c55a3-143">通常、明示的な読み込みは、遅延読み込みを無効にした場合にのみ使用します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-143">Typically you'd use explicit loading only when you've turned lazy loading off.</span></span> <span data-ttu-id="c55a3-144">遅延読み込みをオフにする必要があるシナリオの1つは、シリアル化時です。</span><span class="sxs-lookup"><span data-stu-id="c55a3-144">One scenario when you should turn lazy loading off is during serialization.</span></span> <span data-ttu-id="c55a3-145">遅延読み込みとシリアル化は十分に混同されていません。注意を払っていない場合は、遅延読み込みが有効になっている場合よりもはるかに多くのデータを照会できます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-145">Lazy loading and serialization don't mix well, and if you aren't careful you can end up querying significantly more data than you intended when lazy loading is enabled.</span></span> <span data-ttu-id="c55a3-146">通常、シリアル化は、型のインスタンスの各プロパティにアクセスすることによって機能します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-146">Serialization generally works by accessing each property on an instance of a type.</span></span> <span data-ttu-id="c55a3-147">プロパティアクセスは遅延読み込みをトリガーし、それらの遅延読み込みされたエンティティをシリアル化します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-147">Property access triggers lazy loading, and those lazy loaded entities are serialized.</span></span> <span data-ttu-id="c55a3-148">次に、シリアル化プロセスは、遅延読み込みされたエンティティの各プロパティにアクセスします。これにより、さらに遅延読み込みとシリアル化が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-148">The serialization process then accesses each property of the lazy-loaded entities, potentially causing even more lazy loading and serialization.</span></span> <span data-ttu-id="c55a3-149">この実行後のチェーンの反応を回避するには、エンティティをシリアル化する前に遅延読み込みをオフにします。</span><span class="sxs-lookup"><span data-stu-id="c55a3-149">To prevent this run-away chain reaction, turn lazy loading off before you serialize an entity.</span></span>

<span data-ttu-id="c55a3-150">既定では、データベースコンテキストクラスは遅延読み込みを実行します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-150">The database context class performs lazy loading by default.</span></span> <span data-ttu-id="c55a3-151">遅延読み込みを無効にするには、次の2つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-151">There are two ways to disable lazy loading:</span></span>

- <span data-ttu-id="c55a3-152">特定のナビゲーションプロパティについては、プロパティを宣言するときに `virtual` キーワードを省略します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-152">For specific navigation properties, omit the `virtual` keyword when you declare the property.</span></span>
- <span data-ttu-id="c55a3-153">すべてのナビゲーションプロパティについて、`LazyLoadingEnabled` を `false`に設定します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-153">For all navigation properties, set `LazyLoadingEnabled` to `false`.</span></span> <span data-ttu-id="c55a3-154">たとえば、コンテキストクラスのコンストラクターに次のコードを配置できます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-154">For example, you can put the following code in the constructor of your context class:</span></span> 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="c55a3-155">遅延読み込みでは、パフォーマンスの問題を引き起こすコードをマスクできます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-155">Lazy loading can mask code that causes performance problems.</span></span> <span data-ttu-id="c55a3-156">たとえば、一括または明示的な読み込みを指定せずに大量のエンティティを処理し、各イテレーションで複数のナビゲーションプロパティを使用するコードは、データベースへのラウンドトリップが多くなるため、非常に非効率になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-156">For example, code that doesn't specify eager or explicit loading but processes a high volume of entities and uses several navigation properties in each iteration might be very inefficient (because of many round trips to the database).</span></span> <span data-ttu-id="c55a3-157">オンプレミスの SQL server を使用して開発を正常に実行するアプリケーションでは、待機時間の増加と遅延読み込みのために Azure SQL Database に移動したときにパフォーマンスの問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-157">An application that performs well in development using an on premise SQL server might have performance problems when moved to Azure SQL Database due to the increased latency and lazy loading.</span></span> <span data-ttu-id="c55a3-158">現実的なテスト負荷を使用してデータベースクエリをプロファイルすると、遅延読み込みが適切かどうかを判断するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-158">Profiling the database queries with a realistic test load will help you determine if lazy loading is appropriate.</span></span> <span data-ttu-id="c55a3-159">詳細については、「 [Demystifying Entity Framework 方法: 関連データの読み込み](https://msdn.microsoft.com/magazine/hh205756.aspx)」と「 [Entity Framework を使用したネットワーク待機 SQL Azure 時間の短縮](https://msdn.microsoft.com/magazine/gg309181.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c55a3-159">For more information see [Demystifying Entity Framework Strategies: Loading Related Data](https://msdn.microsoft.com/magazine/hh205756.aspx) and [Using the Entity Framework to Reduce Network Latency to SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).</span></span>

## <a name="create-a-courses-index-page-that-displays-department-name"></a><span data-ttu-id="c55a3-160">学科名を表示するコースのインデックスページを作成する</span><span class="sxs-lookup"><span data-stu-id="c55a3-160">Create a Courses Index Page That Displays Department Name</span></span>

<span data-ttu-id="c55a3-161">`Course` エンティティには、コースが割り当てられている部署の `Department` エンティティを含むナビゲーションプロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c55a3-161">The `Course` entity includes a navigation property that contains the `Department` entity of the department that the course is assigned to.</span></span> <span data-ttu-id="c55a3-162">割り当てられた部門の名前をコースの一覧に表示するには、`Course.Department` ナビゲーションプロパティにある `Department` エンティティから `Name` プロパティを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-162">To display the name of the assigned department in a list of courses, you need to get the `Name` property from the `Department` entity that is in the `Course.Department` navigation property.</span></span>

<span data-ttu-id="c55a3-163">次の図に示すように、前に `Student` コントローラーで行ったのと同じオプションを使用して、`Course` エンティティ型の `CourseController` という名前のコントローラーを作成します (イメージとは異なり、コンテキストクラスは、モデルの名前空間ではなく、DAL 名前空間にあります)。</span><span class="sxs-lookup"><span data-stu-id="c55a3-163">Create a controller named `CourseController` for the `Course` entity type, using the same options that you did earlier for the `Student` controller, as shown in the following illustration (except unlike the image, your context class is in the DAL namespace, not the Models namespace):</span></span>

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

<span data-ttu-id="c55a3-165">*Controllers\CourseController.cs*を開き、`Index` メソッドを確認します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-165">Open *Controllers\CourseController.cs* and look at the `Index` method:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="c55a3-166">自動スキャフォールディングでは、`Include` メソッドを使って、`Department` ナビゲーション プロパティに一括読み込みを指定しています。</span><span class="sxs-lookup"><span data-stu-id="c55a3-166">The automatic scaffolding has specified eager loading for the `Department` navigation property by using the `Include` method.</span></span>

<span data-ttu-id="c55a3-167">*Views\Course\Index.cshtml*を開き、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-167">Open *Views\Course\Index.cshtml* and replace the existing code with the following code.</span></span> <span data-ttu-id="c55a3-168">変更が強調表示されています。</span><span class="sxs-lookup"><span data-stu-id="c55a3-168">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

<span data-ttu-id="c55a3-169">スキャフォールディング コードに、次の変更を行いました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-169">You've made the following changes to the scaffolded code:</span></span>

- <span data-ttu-id="c55a3-170">見出しを **[インデックス]** から **[コース]** に変更しました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-170">Changed the heading from **Index** to **Courses**.</span></span>
- <span data-ttu-id="c55a3-171">行のリンクを左に移動しました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-171">Moved the row links to the left.</span></span>
- <span data-ttu-id="c55a3-172">`CourseID` プロパティ値を示す列が見出し**番号**の下に追加されました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-172">Added a column under the heading **Number** that shows the `CourseID` property value.</span></span> <span data-ttu-id="c55a3-173">(既定では、主キーは、通常、エンドユーザーにとって意味がないため、スキャフォールディングされません。</span><span class="sxs-lookup"><span data-stu-id="c55a3-173">(By default, primary keys aren't scaffolded because normally they are meaningless to end users.</span></span> <span data-ttu-id="c55a3-174">ただし、この場合、主キーは意味があり、表示する必要があります)。</span><span class="sxs-lookup"><span data-stu-id="c55a3-174">However, in this case the primary key is meaningful and you want to show it.)</span></span>
- <span data-ttu-id="c55a3-175">最後の列見出しを**DepartmentID** (外部 `Department` キーの名前) から**Department**に変更しました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-175">Changed the last column heading from **DepartmentID** (the name of the foreign key to the `Department` entity) to **Department**.</span></span>

<span data-ttu-id="c55a3-176">最後の列では、スキャフォールディングコードによって、`Department` ナビゲーションプロパティに読み込まれる `Department` エンティティの `Name` プロパティが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-176">Notice that for the last column, the scaffolded code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

<span data-ttu-id="c55a3-177">ページを実行します (Contoso 大学のホームページの **[コース]** タブを選択します)。部署名の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-177">Run the page (select the **Courses** tab on the Contoso University home page) to see the list with department names.</span></span>

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a><span data-ttu-id="c55a3-179">コースと加入契約を示す講師用のインデックスページを作成する</span><span class="sxs-lookup"><span data-stu-id="c55a3-179">Create an Instructors Index Page That Shows Courses and Enrollments</span></span>

<span data-ttu-id="c55a3-180">このセクションでは、インストラクターのインデックスページを表示するために、`Instructor` エンティティのコントローラーとビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-180">In this section you'll create a controller and view for the `Instructor` entity in order to display the Instructors Index page:</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="c55a3-182">このページは、次の方法で関連データを読み取って表示します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-182">This page reads and displays related data in the following ways:</span></span>

- <span data-ttu-id="c55a3-183">インストラクターの一覧には、`OfficeAssignment` エンティティの関連データが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-183">The list of instructors displays related data from the `OfficeAssignment` entity.</span></span> <span data-ttu-id="c55a3-184">`Instructor` エンティティと `OfficeAssignment` エンティティは、一対ゼロまたは一対一のリレーションシップです。</span><span class="sxs-lookup"><span data-stu-id="c55a3-184">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="c55a3-185">`OfficeAssignment` エンティティに一括読み込みを使用します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-185">You'll use eager loading for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="c55a3-186">前述のように、通常、一括読み込みは、主テーブルで取得したすべての行の関連データが必要なときにより効率的です。</span><span class="sxs-lookup"><span data-stu-id="c55a3-186">As explained earlier, eager loading is typically more efficient when you need the related data for all retrieved rows of the primary table.</span></span> <span data-ttu-id="c55a3-187">このケースでは、割り当てられたすべてのインストラクターのオフィスの割り当てを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-187">In this case, you want to display office assignments for all displayed instructors.</span></span>
- <span data-ttu-id="c55a3-188">ユーザーがインストラクターを選択すると、関連する `Course` エンティティが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-188">When the user selects an instructor, related `Course` entities are displayed.</span></span> <span data-ttu-id="c55a3-189">`Instructor` エンティティと `Course` エンティティは多対多リレーションシップです。</span><span class="sxs-lookup"><span data-stu-id="c55a3-189">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="c55a3-190">`Course` エンティティとそれに関連する `Department` エンティティに一括読み込みを使用します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-190">You'll use eager loading for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="c55a3-191">この場合、選択したインストラクターのコースのみが必要になるため、遅延読み込みの方が効率的な場合があります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-191">In this case, lazy loading might be more efficient because you need courses only for the selected instructor.</span></span> <span data-ttu-id="c55a3-192">ただし、この例では、ナビゲーション プロパティにあるエンティティ内のナビゲーション プロパティに一括読み込みを使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-192">However, this example shows how to use eager loading for navigation properties within entities that are themselves in navigation properties.</span></span>
- <span data-ttu-id="c55a3-193">ユーザーがコースを選択すると、`Enrollments` エンティティセットの関連データが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-193">When the user selects a course, related data from the `Enrollments` entity set is displayed.</span></span> <span data-ttu-id="c55a3-194">`Course` エンティティと `Enrollment` エンティティは一対多リレーションシップです。</span><span class="sxs-lookup"><span data-stu-id="c55a3-194">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span> <span data-ttu-id="c55a3-195">`Enrollment` エンティティとそれに関連する `Student` エンティティに対して明示的な読み込みを追加します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-195">You'll add explicit loading for `Enrollment` entities and their related `Student` entities.</span></span> <span data-ttu-id="c55a3-196">(遅延読み込みが有効になっているため、明示的な読み込みは必要ありませんが、これは明示的な読み込みを行う方法を示しています)。</span><span class="sxs-lookup"><span data-stu-id="c55a3-196">(Explicit loading isn't necessary because lazy loading is enabled, but this shows how to do explicit loading.)</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="c55a3-197">インストラクターのインデックスビューのビューモデルを作成する</span><span class="sxs-lookup"><span data-stu-id="c55a3-197">Create a View Model for the Instructor Index View</span></span>

<span data-ttu-id="c55a3-198">インストラクターのインデックスページには、3つの異なるテーブルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-198">The Instructor Index page shows three different tables.</span></span> <span data-ttu-id="c55a3-199">そのため、テーブルの 1 つにデータを保持するごとに、3 つのプロパティを含むビュー モデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-199">Therefore, you'll create a view model that includes three properties, each holding the data for one of the tables.</span></span>

<span data-ttu-id="c55a3-200">*Viewmodel*フォルダーで、 *InstructorIndexData.cs*を作成し、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-200">In the *ViewModels* folder, create *InstructorIndexData.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a><span data-ttu-id="c55a3-201">選択した行のスタイルを追加する</span><span class="sxs-lookup"><span data-stu-id="c55a3-201">Adding a Style for Selected Rows</span></span>

<span data-ttu-id="c55a3-202">選択した行をマークするには、別の背景色が必要です。</span><span class="sxs-lookup"><span data-stu-id="c55a3-202">To mark selected rows you need a different background color.</span></span> <span data-ttu-id="c55a3-203">この UI のスタイルを指定するには、次に示すように、次の強調表示されているコードを*contentsiteの*`/* info and errors */` セクションに追加します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-203">To provide a style for this UI, add the following highlighted code to the section `/* info and errors */` in *Content\Site.css*, as shown below:</span></span>

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a><span data-ttu-id="c55a3-204">インストラクターのコントローラーとビューの作成</span><span class="sxs-lookup"><span data-stu-id="c55a3-204">Creating the Instructor Controller and Views</span></span>

<span data-ttu-id="c55a3-205">次の図に示すように、`InstructorController` コントローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-205">Create an `InstructorController` controller as shown in the following illustration:</span></span>

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

<span data-ttu-id="c55a3-207">*Controllers\InstructorController.cs*を開き、`ViewModels` 名前空間の `using` ステートメントを追加します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-207">Open *Controllers\InstructorController.cs* and add a `using` statement for the `ViewModels` namespace:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="c55a3-208">`Index` メソッドのスキャフォールディングコードは、`OfficeAssignment` ナビゲーションプロパティに対してのみ一括読み込みを指定します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-208">The scaffolded code in the `Index` method specifies eager loading only for the `OfficeAssignment` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="c55a3-209">`Index` メソッドを次のコードに置き換えて、追加の関連データを読み込み、ビューモデルに配置します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-209">Replace the `Index` method with the following code to load additional related data and put it in the view model:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="c55a3-210">メソッドは、オプションのルートデータ (`id`) と、選択したインストラクターと選択したコースの ID 値を提供するクエリ文字列パラメーター (`courseID`) を受け取り、必要なすべてのデータをビューに渡します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-210">The method accepts optional route data (`id`) and a query string parameter (`courseID`) that provide the ID values of the selected instructor and selected course, and passes all of the required data to the view.</span></span> <span data-ttu-id="c55a3-211">パラメーターは、ページの **Select** ハイパーリンクによって指定されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-211">The parameters are provided by the **Select** hyperlinks on the page.</span></span>

> [!TIP]
> 
> <span data-ttu-id="c55a3-212">**ルートデータ**</span><span class="sxs-lookup"><span data-stu-id="c55a3-212">**Route data**</span></span>
> 
> <span data-ttu-id="c55a3-213">Route data は、モデルバインダーがルーティングテーブルで指定された URL セグメントで見つかったデータです。</span><span class="sxs-lookup"><span data-stu-id="c55a3-213">Route data is data that the model binder found in a URL segment specified in the routing table.</span></span> <span data-ttu-id="c55a3-214">たとえば、既定のルートでは、`controller`、`action`、および `id` セグメントが指定されています。</span><span class="sxs-lookup"><span data-stu-id="c55a3-214">For example, the default route specifies `controller`, `action`, and `id` segments:</span></span>
> 
> ```csharp
> routes.MapRoute(  
>  name: "Default",  
>  url: "{controller}/{action}/{id}",  
>  defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }  
> );
> ```
> 
> <span data-ttu-id="c55a3-215">次の URL では、既定のルートは、`Instructor` を `controller`としてマップし、`Index` `action` として、1を `id`としてマップします。これらはルートデータ値です。</span><span class="sxs-lookup"><span data-stu-id="c55a3-215">In the following URL, the default route maps `Instructor` as the `controller`, `Index` as the `action` and 1 as the `id`; these are route data values.</span></span>
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> <span data-ttu-id="c55a3-216">"? courseID = 2021" はクエリ文字列値です。</span><span class="sxs-lookup"><span data-stu-id="c55a3-216">"?courseID=2021" is a query string value.</span></span> <span data-ttu-id="c55a3-217">モデルバインダーは、`id` をクエリ文字列値として渡す場合にも機能します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-217">The model binder will also work if you pass the `id` as a query string value:</span></span>
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> <span data-ttu-id="c55a3-218">Url は、Razor ビューの `ActionLink` ステートメントによって作成されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-218">The URLs are created by `ActionLink` statements in the Razor view.</span></span> <span data-ttu-id="c55a3-219">次のコードでは、`id` パラメーターが既定のルートと一致するため、`id` がルートデータに追加されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-219">In the following code, the `id` parameter matches the default route, so `id` is added to the route data.</span></span>
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> <span data-ttu-id="c55a3-220">次のコードでは、`courseID` が既定のルートのパラメーターと一致しないため、クエリ文字列として追加されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-220">In the following code, `courseID` doesn't match a parameter in the default route, so it's added as a query string.</span></span>
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

<span data-ttu-id="c55a3-221">このコードは、ビュー モデルのインスタンスを作成し、インストラクターのリストに配置することから始めます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-221">The code begins by creating an instance of the view model and putting in it the list of instructors.</span></span> <span data-ttu-id="c55a3-222">このコードでは、`Instructor.OfficeAssignment` と `Instructor.Courses` ナビゲーションプロパティの一括読み込みを指定します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-222">The code specifies eager loading for the `Instructor.OfficeAssignment` and the `Instructor.Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

<span data-ttu-id="c55a3-223">2番目の `Include` メソッドは、コースを読み込み、読み込まれた各コースで `Course.Department` ナビゲーションプロパティの一括読み込みを行います。</span><span class="sxs-lookup"><span data-stu-id="c55a3-223">The second `Include` method loads Courses, and for each Course that is loaded it does eager loading for the `Course.Department` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="c55a3-224">前述のように、一括読み込みは必要ありませんが、パフォーマンスを向上させるために行われます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-224">As mentioned previously, eager loading is not required but is done to improve performance.</span></span> <span data-ttu-id="c55a3-225">ビューには常に `OfficeAssignment` エンティティが必要であるため、同じクエリでフェッチする方が効率的です。</span><span class="sxs-lookup"><span data-stu-id="c55a3-225">Since the view always requires the `OfficeAssignment` entity, it's more efficient to fetch that in the same query.</span></span> <span data-ttu-id="c55a3-226">`Course` エンティティは、web ページでインストラクターが選択されている場合に必要になります。したがって、[なし] を選択した場合に比べて、ページがより頻繁に表示される場合のみ、一括読み込みの方が遅延読み込みより優れています。</span><span class="sxs-lookup"><span data-stu-id="c55a3-226">`Course` entities are required when an instructor is selected in the web page, so eager loading is better than lazy loading only if the page is displayed more often with a course selected than without.</span></span>

<span data-ttu-id="c55a3-227">[インストラクター ID] が選択されている場合は、選択したインストラクターがビューモデルのインストラクターの一覧から取得されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-227">If an instructor ID was selected, the selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="c55a3-228">次に、ビューモデルの `Courses` プロパティが、そのインストラクターの `Courses` ナビゲーションプロパティからの `Course` エンティティと共に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-228">The view model's `Courses` property is then loaded with the `Course` entities from that instructor's `Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="c55a3-229">`Where` メソッドはコレクションを返しますが、この場合は、そのメソッドに渡された条件によって返されるのは、1つの `Instructor` エンティティだけになります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-229">The `Where` method returns a collection, but in this case the criteria passed to that method result in only a single `Instructor` entity being returned.</span></span> <span data-ttu-id="c55a3-230">`Single` メソッドは、コレクションを1つの `Instructor` エンティティに変換します。これにより、そのエンティティの `Courses` プロパティにアクセスできるようになります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-230">The `Single` method converts the collection into a single `Instructor` entity, which gives you access to that entity's `Courses` property.</span></span>

<span data-ttu-id="c55a3-231">コレクションに項目が1つしかないことがわかっている場合は、コレクションに対して[1 つ](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)のメソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-231">You use the [Single](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) method on a collection when you know the collection will have only one item.</span></span> <span data-ttu-id="c55a3-232">`Single` メソッドは、渡されたコレクションが空である場合、または複数の項目がある場合に、例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="c55a3-232">The `Single` method throws an exception if the collection passed to it is empty or if there's more than one item.</span></span> <span data-ttu-id="c55a3-233">別の方法としては[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)があります。これは、コレクションが空の場合に既定値 (この場合は`null`) を返します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-233">An alternative is [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), which returns a default value (`null` in this case) if the collection is empty.</span></span> <span data-ttu-id="c55a3-234">ただし、この場合も例外が発生します (`null` 参照の `Courses` プロパティを見つけようとする)。例外メッセージは、問題の原因を明確に示すものではありません。</span><span class="sxs-lookup"><span data-stu-id="c55a3-234">However, in this case that would still result in an exception (from trying to find a `Courses` property on a `null` reference), and the exception message would less clearly indicate the cause of the problem.</span></span> <span data-ttu-id="c55a3-235">`Single` メソッドを呼び出すと、`Where` メソッドを個別に呼び出す代わりに、`Where` 条件を渡すこともできます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-235">When you call the `Single` method, you can also pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="c55a3-236">次の代わりに、</span><span class="sxs-lookup"><span data-stu-id="c55a3-236">Instead of:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="c55a3-237">次に、コースが選択された場合、選択したコースはビュー モデルのコースのリストから取得されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-237">Next, if a course was selected, the selected course is retrieved from the list of courses in the view model.</span></span> <span data-ttu-id="c55a3-238">次に、ビューモデルの `Enrollments` プロパティが、そのコースの `Enrollments` ナビゲーションプロパティからの `Enrollment` エンティティと共に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-238">Then the view model's `Enrollments` property is loaded with the `Enrollment` entities from that course's `Enrollments` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a><span data-ttu-id="c55a3-239">インストラクターのインデックスビューの変更</span><span class="sxs-lookup"><span data-stu-id="c55a3-239">Modifying the Instructor Index View</span></span>

<span data-ttu-id="c55a3-240">*Views\Instructor\Index.cshtml*で、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-240">In *Views\Instructor\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="c55a3-241">変更が強調表示されています。</span><span class="sxs-lookup"><span data-stu-id="c55a3-241">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

<span data-ttu-id="c55a3-242">既存のコードに次の変更を行いました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-242">You've made the following changes to the existing code:</span></span>

- <span data-ttu-id="c55a3-243">モデル クラスが `InstructorIndexData` に変更されました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-243">Changed the model class to `InstructorIndexData`.</span></span>
- <span data-ttu-id="c55a3-244">**Index** のページ タイトルが **Instructors** に変更されました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-244">Changed the page title from **Index** to **Instructors**.</span></span>
- <span data-ttu-id="c55a3-245">行リンク列を左に移動しました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-245">Moved the row link columns to the left.</span></span>
- <span data-ttu-id="c55a3-246">**FullName**列が削除されました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-246">Removed the **FullName** column.</span></span>
- <span data-ttu-id="c55a3-247">`item.OfficeAssignment` が null でない場合にのみ `item.OfficeAssignment.Location` を表示する**Office**列を追加しました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-247">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` is not null.</span></span> <span data-ttu-id="c55a3-248">(これは一対ゼロまたは一対一のリレーションシップであるため、関連する `OfficeAssignment` エンティティが存在しない可能性があります)。</span><span class="sxs-lookup"><span data-stu-id="c55a3-248">(Because this is a one-to-zero-or-one relationship, there might not be a related `OfficeAssignment` entity.)</span></span> 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- <span data-ttu-id="c55a3-249">選択したインストラクターの `tr` 要素に `class="selectedrow"` を動的に追加するコードを追加しました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-249">Added code that will dynamically add `class="selectedrow"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="c55a3-250">これにより、前に作成した CSS クラスを使用して、選択した行の背景色が設定されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-250">This sets a background color for the selected row using the CSS class that you created earlier.</span></span> <span data-ttu-id="c55a3-251">(`valign` 属性は、テーブルに複数行の列を追加するときに、次のチュートリアルで役に立ちます)。</span><span class="sxs-lookup"><span data-stu-id="c55a3-251">(The `valign` attribute will be useful in the following tutorial when you add a multi-row column to the table.)</span></span> 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- <span data-ttu-id="c55a3-252">各行の [その他のリンクの直前に**選択する]** というラベルの新しい `ActionLink` が追加されました。選択したインストラクター ID が `Index` メソッドに送信されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-252">Added a new `ActionLink` labeled **Select** immediately before the other links in each row, which causes the selected instructor ID to be sent to the `Index` method.</span></span>

<span data-ttu-id="c55a3-253">アプリケーションを実行し、 **[インストラクター]** タブを選択します。このページには、関連する `OfficeAssignment` エンティティの [`Location`] プロパティと、関連する `OfficeAssignment` エンティティが存在しない場合の空のテーブルセルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-253">Run the application and select the **Instructors** tab. The page displays the `Location` property of related `OfficeAssignment` entities and an empty table cell when there's no related `OfficeAssignment` entity.</span></span>

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="c55a3-255">*Views\Instructor\Index.cshtml*ファイルで、終了 `table` 要素 (ファイルの末尾) の後に、次の強調表示されたコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-255">In the *Views\Instructor\Index.cshtml* file, after the closing `table` element (at the end of the file), add the following highlighted code.</span></span> <span data-ttu-id="c55a3-256">インストラクターが選択されている場合に、インストラクターに関連するコースの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-256">This displays a list of courses related to an instructor when an instructor is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

<span data-ttu-id="c55a3-257">このコードでは、ビュー モデルの `Courses` プロパティを読み取り、コースのリストを表示します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-257">This code reads the `Courses` property of the view model to display a list of courses.</span></span> <span data-ttu-id="c55a3-258">また、選択したコースの ID を `Index` アクションメソッドに送信する `Select` ハイパーリンクも用意されています。</span><span class="sxs-lookup"><span data-stu-id="c55a3-258">It also provides a `Select` hyperlink that sends the ID of the selected course to the `Index` action method.</span></span>

> [!NOTE]
> <span data-ttu-id="c55a3-259">*.Css*ファイルは、ブラウザーによってキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-259">The *.css* file is cached by browsers.</span></span> <span data-ttu-id="c55a3-260">アプリケーションの実行時に変更が表示されない場合は、(CTRL キーを押しながら **[更新]** ボタンをクリックするか、ctrl キーを押しながら F5 キーを押す)、ハード更新を行います。</span><span class="sxs-lookup"><span data-stu-id="c55a3-260">If you don't see the changes when you run the application, do a hard refresh (hold down the CTRL key while clicking the **Refresh** button, or press CTRL+F5).</span></span>

<span data-ttu-id="c55a3-261">ページを実行し、インストラクターを選択します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-261">Run the page and select an instructor.</span></span> <span data-ttu-id="c55a3-262">選択したインストラクターに割り当てられたコースを表示するグリッドを表示し、各コースに割り当てられた部門の名前を表示します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-262">Now you see a grid that displays courses assigned to the selected instructor, and for each course you see the name of the assigned department.</span></span>

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="c55a3-264">追加したコード ブロックの後に、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-264">After the code block you just added, add the following code.</span></span> <span data-ttu-id="c55a3-265">このコードは、コースを選択したときに、コースに登録されている受講者のリストを表示します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-265">This displays a list of the students who are enrolled in a course when that course is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

<span data-ttu-id="c55a3-266">このコードは、コースに登録されている学生の一覧を表示するために、ビューモデルの `Enrollments` プロパティを読み取ります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-266">This code reads the `Enrollments` property of the view model in order to display a list of students enrolled in the course.</span></span>

<span data-ttu-id="c55a3-267">ページを実行し、インストラクターを選択します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-267">Run the page and select an instructor.</span></span> <span data-ttu-id="c55a3-268">次に、コースを選択して、登録済みの受講者とその成績のリストを表示します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-268">Then select a course to see the list of enrolled students and their grades.</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a><span data-ttu-id="c55a3-270">明示的な読み込みの追加</span><span class="sxs-lookup"><span data-stu-id="c55a3-270">Adding Explicit Loading</span></span>

<span data-ttu-id="c55a3-271">*InstructorController.cs*を開き、選択したコースの登録の一覧を `Index` メソッドがどのように取得するかを確認します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-271">Open *InstructorController.cs* and look at how the `Index` method gets the list of enrollments for a selected course:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="c55a3-272">インストラクターのリストを取得したときに、`Courses` ナビゲーションプロパティの一括読み込みを指定し、各コースの `Department` プロパティを指定しました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-272">When you retrieved the list of instructors, you specified eager loading for the `Courses` navigation property and for the `Department` property of each course.</span></span> <span data-ttu-id="c55a3-273">次に、ビューモデルに `Courses` コレクションを配置します。これで、そのコレクション内の1つのエンティティから `Enrollments` ナビゲーションプロパティにアクセスしています。</span><span class="sxs-lookup"><span data-stu-id="c55a3-273">Then you put the `Courses` collection in the view model, and now you're accessing the `Enrollments` navigation property from one entity in that collection.</span></span> <span data-ttu-id="c55a3-274">`Course.Enrollments` ナビゲーションプロパティに一括読み込みを指定しなかったため、遅延読み込みの結果として、そのプロパティのデータがページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-274">Because you didn't specify eager loading for the `Course.Enrollments` navigation property, the data from that property is appearing in the page as a result of lazy loading.</span></span>

<span data-ttu-id="c55a3-275">他の方法でコードを変更せずに遅延読み込みを無効にした場合、実際に存在していた登録数に関係なく、`Enrollments` プロパティは null になります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-275">If you disabled lazy loading without changing the code in any other way, the `Enrollments` property would be null regardless of how many enrollments the course actually had.</span></span> <span data-ttu-id="c55a3-276">この場合、`Enrollments` プロパティを読み込むには、一括読み込みまたは明示的な読み込みのいずれかを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c55a3-276">In that case, to load the `Enrollments` property, you'd have to specify either eager loading or explicit loading.</span></span> <span data-ttu-id="c55a3-277">一括読み込みを実行する方法については既に説明しました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-277">You've already seen how to do eager loading.</span></span> <span data-ttu-id="c55a3-278">明示的な読み込みの例を表示するには、`Index` メソッドを次のコードに置き換えます。このコードは、`Enrollments` プロパティを明示的に読み込みます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-278">In order to see an example of explicit loading, replace the `Index` method with the following code, which explicitly loads the `Enrollments` property.</span></span> <span data-ttu-id="c55a3-279">変更されたコードが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-279">The code changed are highlighted.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

<span data-ttu-id="c55a3-280">選択した `Course` エンティティを取得すると、新しいコードによってそのコースの `Enrollments` ナビゲーションプロパティが明示的に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-280">After getting the selected `Course` entity, the new code explicitly loads that course's `Enrollments` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="c55a3-281">次に、`Enrollment` エンティティに関連する各 `Student` エンティティを明示的に読み込みます。</span><span class="sxs-lookup"><span data-stu-id="c55a3-281">Then it explicitly loads each `Enrollment` entity's related `Student` entity:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="c55a3-282">`Collection` メソッドを使用してコレクションプロパティを読み込むことに注意してくださいが、1つのエンティティのみを保持するプロパティの場合は、`Reference` メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-282">Notice that you use the `Collection` method to load a collection property, but for a property that holds just one entity, you use the `Reference` method.</span></span> <span data-ttu-id="c55a3-283">ここで [講師用のインデックス] ページを実行すると、データの取得方法を変更しても、ページに表示される内容に違いはありません。</span><span class="sxs-lookup"><span data-stu-id="c55a3-283">You can run the Instructor Index page now and you'll see no difference in what's displayed on the page, although you've changed how the data is retrieved.</span></span>

## <a name="summary"></a><span data-ttu-id="c55a3-284">要約</span><span class="sxs-lookup"><span data-stu-id="c55a3-284">Summary</span></span>

<span data-ttu-id="c55a3-285">これで、3つのすべての方法 (lazy、一括、および explicit) を使用して、関連するデータをナビゲーションプロパティに読み込むことができました。</span><span class="sxs-lookup"><span data-stu-id="c55a3-285">You've now used all three ways (lazy, eager, and explicit) to load related data into navigation properties.</span></span> <span data-ttu-id="c55a3-286">次のチュートリアルでは、関連データの更新方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="c55a3-286">In the next tutorial you'll learn how to update related data.</span></span>

<span data-ttu-id="c55a3-287">その他の Entity Framework リソースへのリンクについては、「 [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c55a3-287">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c55a3-288">[前へ](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [次へ](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="c55a3-288">[Previous](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
[Next](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
