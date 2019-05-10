---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC アプリケーション (10 の 8) で、Entity Framework による継承の実装 |Microsoft Docs
author: tdykstra
description: Contoso University のサンプルの web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法について説明しています.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d61d02e23bbcaf9eff910613880ac49f79c15cac
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65112389"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a><span data-ttu-id="edc38-103">ASP.NET MVC アプリケーション (10 の 8) で、Entity Framework による継承の実装</span><span class="sxs-lookup"><span data-stu-id="edc38-103">Implementing Inheritance with the Entity Framework in an ASP.NET MVC Application (8 of 10)</span></span>

<span data-ttu-id="edc38-104">によって[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="edc38-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="edc38-105">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="edc38-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="edc38-106">Contoso University のサンプルの web アプリケーションでは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="edc38-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="edc38-107">チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="edc38-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="edc38-108">チュートリアルのシリーズを開始するには、最初からまたは[この章のスタート プロジェクトをダウンロード](building-the-ef5-mvc4-chapter-downloads.md)し、ここから始めてください。</span><span class="sxs-lookup"><span data-stu-id="edc38-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="edc38-109">を解決できない問題が生じた場合[章では、完了したダウンロード](building-the-ef5-mvc4-chapter-downloads.md)の問題を再現しようとします。</span><span class="sxs-lookup"><span data-stu-id="edc38-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="edc38-110">問題の解決策は、完成したコードにコードを比較することによって一般的に見つかります。</span><span class="sxs-lookup"><span data-stu-id="edc38-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="edc38-111">一般的なエラーとその解決方法は、次を参照してください。[エラーと回避策。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="edc38-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="edc38-112">前のチュートリアルでは、同時実行例外を処理します。</span><span class="sxs-lookup"><span data-stu-id="edc38-112">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="edc38-113">このチュートリアルでは、データ モデルで継承を実装する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="edc38-113">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="edc38-114">オブジェクト指向プログラミングでは、冗長なコードを排除するのに継承を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="edc38-114">In object-oriented programming, you can use inheritance to eliminate redundant code.</span></span> <span data-ttu-id="edc38-115">このチュートリアルでは、`Instructor` と `Student` クラスを `Person` 基底クラスから派生するように変更します。この基底クラスはインストラクターと受講者の両方に共通な `LastName` などのプロパティを含んでいます。</span><span class="sxs-lookup"><span data-stu-id="edc38-115">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="edc38-116">どの Web ページも追加または変更しませんが、コードの一部を変更し、それらの変更はデータベースに自動的に反映されます。</span><span class="sxs-lookup"><span data-stu-id="edc38-116">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="edc38-117">テーブルの型ごとの継承とテーブルは階層ごと</span><span class="sxs-lookup"><span data-stu-id="edc38-117">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="edc38-118">オブジェクト指向プログラミングでの関連クラスを使用しやすく継承を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="edc38-118">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="edc38-119">たとえば、`Instructor`と`Student`クラス、`School`データ モデルを共有コードが冗長になるいくつかのプロパティ。</span><span class="sxs-lookup"><span data-stu-id="edc38-119">For example, the `Instructor` and `Student` classes in the `School` data model share several properties, which results in redundant code:</span></span>

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

<span data-ttu-id="edc38-121">`Instructor` エンティティと `Student` エンティティで共有されるプロパティの冗長なコードを削除すると仮定します。</span><span class="sxs-lookup"><span data-stu-id="edc38-121">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="edc38-122">作成することが、`Person`基本クラスがそれらの共有プロパティだけが含まれているようにして、`Instructor`と`Student`エンティティは、次の図に示すように、その基本クラスから継承します。</span><span class="sxs-lookup"><span data-stu-id="edc38-122">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

<span data-ttu-id="edc38-124">データベースでこの継承構造を表すことができるいくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="edc38-124">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="edc38-125">割り当てることも、`Person`受講者とインストラクターによる 1 つのテーブルの両方に関する情報が含まれるテーブル。</span><span class="sxs-lookup"><span data-stu-id="edc38-125">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="edc38-126">インストラクターのみに適用の一部の列 (`HireDate`)、受講者のみに (`EnrollmentDate`)、一部には、両方 (`LastName`、 `FirstName`)。</span><span class="sxs-lookup"><span data-stu-id="edc38-126">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="edc38-127">通常があります、*識別子*各行を入力するかを示す列を表します。</span><span class="sxs-lookup"><span data-stu-id="edc38-127">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="edc38-128">たとえば、識別子列にインストラクターを示す "Instructor" と受講者を示す "Student" がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="edc38-128">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![テーブル-hierarchy_example ごと](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

<span data-ttu-id="edc38-130">単一のデータベース テーブルからエンティティの継承構造を生成するには、このパターンと呼ばれます *- table-per-hierarchy* (TPH) 継承します。</span><span class="sxs-lookup"><span data-stu-id="edc38-130">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="edc38-131">代わりに、継承構造と同じように見えるデータベースを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="edc38-131">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="edc38-132">など名前フィールドのみがある可能性があります、`Person`テーブルいて個別`Instructor`と`Student`日付フィールドを持つテーブル。</span><span class="sxs-lookup"><span data-stu-id="edc38-132">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Table-per-type_inheritance](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

<span data-ttu-id="edc38-134">各エンティティ クラスと呼ばれる、データベース テーブルを作成するこのパターン*table-per-type* (TPT) 継承します。</span><span class="sxs-lookup"><span data-stu-id="edc38-134">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="edc38-135">TPH 継承パターンは、TPT パターンが複雑な結合クエリのため一般にパフォーマンスを向上させると、TPT 継承パターンよりも、Entity Framework で提供します。</span><span class="sxs-lookup"><span data-stu-id="edc38-135">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="edc38-136">このチュートリアルでは、TPH 継承の実装方法を示します。</span><span class="sxs-lookup"><span data-stu-id="edc38-136">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="edc38-137">次の手順を実行することによってを実行してみましょう。</span><span class="sxs-lookup"><span data-stu-id="edc38-137">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="edc38-138">作成、`Person`クラスし、変更、`Instructor`と`Student`クラスから派生する`Person`します。</span><span class="sxs-lookup"><span data-stu-id="edc38-138">Create a `Person` class and change the `Instructor` and `Student` classes to derive from `Person`.</span></span>
- <span data-ttu-id="edc38-139">データベースへのモデルのマッピング コードをデータベース コンテキスト クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="edc38-139">Add model-to-database mapping code to the database context class.</span></span>
- <span data-ttu-id="edc38-140">変更`InstructorID`と`StudentID`参照をプロジェクト全体にわたって`PersonID`します。</span><span class="sxs-lookup"><span data-stu-id="edc38-140">Change `InstructorID` and `StudentID` references throughout the project to `PersonID`.</span></span>

## <a name="creating-the-person-class"></a><span data-ttu-id="edc38-141">Person クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="edc38-141">Creating the Person Class</span></span>

 <span data-ttu-id="edc38-142">メモ:これらのクラスを使用するコント ローラーを更新するまでは、次のクラスを作成した後、プロジェクトをコンパイルすることはできません。</span><span class="sxs-lookup"><span data-stu-id="edc38-142">Note: You won't be able to compile the project after creating the classes below until you update the controllers that uses these classes.</span></span> 

<span data-ttu-id="edc38-143">*モデル*フォルダー作成*Person.cs*テンプレート コードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="edc38-143">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="edc38-144">*Instructor.cs*、派生、`Instructor`クラスから、`Person`クラスし、キーと名前のフィールドを削除します。</span><span class="sxs-lookup"><span data-stu-id="edc38-144">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="edc38-145">コードは次の例のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="edc38-145">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="edc38-146">同様に変更する*Student.cs*します。</span><span class="sxs-lookup"><span data-stu-id="edc38-146">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="edc38-147">`Student`クラスは次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="edc38-147">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a><span data-ttu-id="edc38-148">Person エンティティ型をモデルに追加します。</span><span class="sxs-lookup"><span data-stu-id="edc38-148">Adding the Person Entity Type to the Model</span></span>

<span data-ttu-id="edc38-149">*SchoolContext.cs*、追加、`DbSet`プロパティを`Person`エンティティの種類。</span><span class="sxs-lookup"><span data-stu-id="edc38-149">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="edc38-150">Table-per-Hierarchy 継承を構成するために Entity Framework に必要なのことはこれですべてです。</span><span class="sxs-lookup"><span data-stu-id="edc38-150">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="edc38-151">わかる、データベースが再作成すると、`Person`テーブルの代わりに、`Student`と`Instructor`テーブル。</span><span class="sxs-lookup"><span data-stu-id="edc38-151">As you'll see, when the database is re-created, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="changing-instructorid-and-studentid-to-personid"></a><span data-ttu-id="edc38-152">PersonID に InstructorID と学生 Id を変更します。</span><span class="sxs-lookup"><span data-stu-id="edc38-152">Changing InstructorID and StudentID to PersonID</span></span>

<span data-ttu-id="edc38-153">*SchoolContext.cs*、インストラクター コース マッピング ステートメントで次のように変更します`MapRightKey("InstructorID")`に`MapRightKey("PersonID")`:。</span><span class="sxs-lookup"><span data-stu-id="edc38-153">In *SchoolContext.cs*, in the Instructor-Course mapping statement, change `MapRightKey("InstructorID")` to `MapRightKey("PersonID")`:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

<span data-ttu-id="edc38-154">この変更が必要です。多対多の結合テーブルで InstructorID 列の名前を変更するだけです。</span><span class="sxs-lookup"><span data-stu-id="edc38-154">This change isn't required; it just changes the name of the InstructorID column in the many-to-many join table.</span></span> <span data-ttu-id="edc38-155">InstructorID と名前のままの場合、アプリケーションが正しく機能もします。</span><span class="sxs-lookup"><span data-stu-id="edc38-155">If you left the name as InstructorID, the application would still work correctly.</span></span> <span data-ttu-id="edc38-156">ここでは、完成した*SchoolContext.cs*:</span><span class="sxs-lookup"><span data-stu-id="edc38-156">Here is the completed *SchoolContext.cs*:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

<span data-ttu-id="edc38-157">次を変更する必要があります`InstructorID`に`PersonID`と`StudentID`に`PersonID`プロジェクト全体にわたって***を除く***内の移行のタイムスタンプ付きのファイルで、*移行*フォルダー。</span><span class="sxs-lookup"><span data-stu-id="edc38-157">Next you need to change `InstructorID` to `PersonID` and `StudentID` to `PersonID` throughout the project ***except*** in the time-stamped migrations files in the *Migrations* folder.</span></span> <span data-ttu-id="edc38-158">そのために検索して、変更する必要のあるファイルのみを開くし、開いているファイルのグローバルな変更を実行します。</span><span class="sxs-lookup"><span data-stu-id="edc38-158">To do that you'll find and open only the files that need to be changed, then perform a global change on the opened files.</span></span> <span data-ttu-id="edc38-159">唯一のファイル、*移行*フォルダーを変更する必要がありますが*migrations \configuration.cs します。*</span><span class="sxs-lookup"><span data-stu-id="edc38-159">The only file in the *Migrations* folder you should change is *Migrations\Configuration.cs.*</span></span>

1. > [!IMPORTANT]
   > <span data-ttu-id="edc38-160">Visual Studio で開いているすべてのファイルを閉じることから始めます。</span><span class="sxs-lookup"><span data-stu-id="edc38-160">Begin by closing all the open files in Visual Studio.</span></span>
2. <span data-ttu-id="edc38-161">をクリックして**検索し置換--すべてのファイルを検索する**で、**編集**メニューのおよびプロジェクトが含まれているすべてのファイルを検索`InstructorID`します。</span><span class="sxs-lookup"><span data-stu-id="edc38-161">Click **Find and Replace -- Find all Files** in the **Edit** menu, and then search for all files in the project that contain `InstructorID`.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. <span data-ttu-id="edc38-162">内の各ファイルを開き、**検索結果**ウィンドウ***を除く***、&lt;タイムスタンプ&gt;*\_.cs* で移行ファイル*移行*フォルダー、ファイルごとに 1 つの線をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="edc38-162">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. <span data-ttu-id="edc38-163">開く、**ファイル内の置換**ダイアログと変更**検索**に**すべての開いているドキュメント**。</span><span class="sxs-lookup"><span data-stu-id="edc38-163">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
5. <span data-ttu-id="edc38-164">使用して、**ファイル内の置換**すべて変更するためのダイアログ`InstructorID`に `PersonID.`</span><span class="sxs-lookup"><span data-stu-id="edc38-164">Use the **Replace in Files** dialog to change all `InstructorID` to `PersonID.`</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. <span data-ttu-id="edc38-165">プロジェクトが含まれているすべてのファイルを検索`StudentID`します。</span><span class="sxs-lookup"><span data-stu-id="edc38-165">Find all the files in the project that contain `StudentID`.</span></span>
7. <span data-ttu-id="edc38-166">内の各ファイルを開き、**検索結果**ウィンドウ***を除く***、&lt;タイムスタンプ&gt;*\_\*.cs*移行ファイル*移行*フォルダー、ファイルごとに 1 つの線をダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="edc38-166">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_\*.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. <span data-ttu-id="edc38-167">開く、**ファイル内の置換**ダイアログと変更**検索**に**すべての開いているドキュメント**。</span><span class="sxs-lookup"><span data-stu-id="edc38-167">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
9. <span data-ttu-id="edc38-168">使用して、**ファイル内の置換**すべて変更するためのダイアログ`StudentID`に`PersonID`します。</span><span class="sxs-lookup"><span data-stu-id="edc38-168">Use the **Replace in Files** dialog to change all `StudentID` to `PersonID`.</span></span>   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. <span data-ttu-id="edc38-169">プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="edc38-169">Build the project.</span></span>

<span data-ttu-id="edc38-170">(これを示す注を*欠点*の`classnameID`主キーの名前付けパターン。</span><span class="sxs-lookup"><span data-stu-id="edc38-170">(Note that this demonstrates a *disadvantage* of the `classnameID` pattern for naming primary keys.</span></span> <span data-ttu-id="edc38-171">場合は、クラス名をプレフィックスとしてせず主キーの ID をという名前が*ありません*名前を変更する必要があるとようになりました)。</span><span class="sxs-lookup"><span data-stu-id="edc38-171">If you had named primary keys ID without prefixing the class name, *no* renaming would be necessary now.)</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="edc38-172">作成し、移行ファイルを更新</span><span class="sxs-lookup"><span data-stu-id="edc38-172">Create and Update a Migrations File</span></span>

<span data-ttu-id="edc38-173">パッケージ マネージャー コンソール (PMC) では、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="edc38-173">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="edc38-174">実行、 `Update-Database` PMC でコマンド。</span><span class="sxs-lookup"><span data-stu-id="edc38-174">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="edc38-175">移行が処理する方法を認識しない既存のデータがあるので、コマンドはこの時点で失敗します。</span><span class="sxs-lookup"><span data-stu-id="edc38-175">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="edc38-176">次のエラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="edc38-176">You get the following error:</span></span>

<span data-ttu-id="edc38-177">*ALTER TABLE ステートメントと競合して外部キー制約"FK\_dbo します。部門\_dbo します。Person\_PersonID"。競合が発生したデータベース"ContosoUniversity"テーブル"dbo します。Person"です。 列 'PersonID'。*</span><span class="sxs-lookup"><span data-stu-id="edc38-177">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Department\_dbo.Person\_PersonID". The conflict occurred in database "ContosoUniversity", table "dbo.Person", column 'PersonID'.*</span></span>

<span data-ttu-id="edc38-178">開いている*移行\&lt; タイムスタンプ&gt;\_Inheritance.cs*と置換、`Up`メソッドを次のコード。</span><span class="sxs-lookup"><span data-stu-id="edc38-178">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

<span data-ttu-id="edc38-179">実行、`update-database`コマンドを再実行します。</span><span class="sxs-lookup"><span data-stu-id="edc38-179">Run the `update-database` command again.</span></span>

> [!NOTE]
> <span data-ttu-id="edc38-180">データとスキーマの変更を移行するときにその他のエラーが発生することになります。</span><span class="sxs-lookup"><span data-stu-id="edc38-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="edc38-181">移行エラーが発生する場合は解決できない場合、接続文字列を変更することで、チュートリアルを続けることができます、 *Web.config*ファイルまたはデータベースを削除します。</span><span class="sxs-lookup"><span data-stu-id="edc38-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or deleting the database.</span></span> <span data-ttu-id="edc38-182">データベースの名前を変更する最も簡単なアプローチとしては、 *Web.config*ファイル。</span><span class="sxs-lookup"><span data-stu-id="edc38-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="edc38-183">CU へ、データベース名を変更するなど、\_の次の例に示すようにテストします。</span><span class="sxs-lookup"><span data-stu-id="edc38-183">For example, change the database name to CU\_test as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> <span data-ttu-id="edc38-184">新しいデータベースを移行するデータがないと、`update-database`コマンドがエラーなしで完了する可能性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="edc38-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="edc38-185">データベースを削除する方法の詳細については、次を参照してください。 [Visual Studio 2012 からデータベースを削除する方法](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)します。</span><span class="sxs-lookup"><span data-stu-id="edc38-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="edc38-186">チュートリアルを続行するにはこの方法を実行する場合、配置サイトの移行を自動的に実行時に同じエラーが発生があるために、このチュートリアルの最後に配置手順をスキップします。</span><span class="sxs-lookup"><span data-stu-id="edc38-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial, since the deployed site would get the same error when it runs migrations automatically.</span></span> <span data-ttu-id="edc38-187">移行エラーのトラブルシューティングを行う場合は、最適なリソースは、Entity Framework のフォーラムまたは StackOverflow.com のいずれか。</span><span class="sxs-lookup"><span data-stu-id="edc38-187">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="testing"></a><span data-ttu-id="edc38-188">テスト</span><span class="sxs-lookup"><span data-stu-id="edc38-188">Testing</span></span>

<span data-ttu-id="edc38-189">サイトを実行し、さまざまなページをお試しください。</span><span class="sxs-lookup"><span data-stu-id="edc38-189">Run the site and try various pages.</span></span> <span data-ttu-id="edc38-190">すべてが前と同じように動作します。</span><span class="sxs-lookup"><span data-stu-id="edc38-190">Everything works the same as it did before.</span></span>

<span data-ttu-id="edc38-191">**サーバー エクスプ ローラー**展開**SchoolContext**し**テーブル**、ことを確認して、**学生**と**インストラクター**テーブルに置換された、 **Person**テーブル。</span><span class="sxs-lookup"><span data-stu-id="edc38-191">In **Server Explorer,** expand **SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="edc38-192">展開、 **Person**テーブルとするすべてに使用されていた列があるを参照してください、**学生**と**インストラクター**テーブル。</span><span class="sxs-lookup"><span data-stu-id="edc38-192">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="edc38-194">Person テーブルを右クリックし、**[テーブル データの表示]** をクリックして識別子列を表示します。</span><span class="sxs-lookup"><span data-stu-id="edc38-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="edc38-195">次の図は、新しい School データベースの構造を示しています。</span><span class="sxs-lookup"><span data-stu-id="edc38-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a><span data-ttu-id="edc38-197">まとめ</span><span class="sxs-lookup"><span data-stu-id="edc38-197">Summary</span></span>

<span data-ttu-id="edc38-198">Table-per-hierarchy 継承が実装されているようになりました、 `Person`、 `Student`、および`Instructor`クラス。</span><span class="sxs-lookup"><span data-stu-id="edc38-198">Table-per-hierarchy inheritance has now been implemented for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="edc38-199">これと他の継承構造の詳細については、次を参照してください。[継承のマッピング方法](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx)Morteza Manavi のブログ。</span><span class="sxs-lookup"><span data-stu-id="edc38-199">For more information about this and other inheritance structures, see [Inheritance Mapping Strategies](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) on Morteza Manavi's blog.</span></span> <span data-ttu-id="edc38-200">次のチュートリアルでは、リポジトリと unit of work パターンを実装するためにいくつかの点を確認します。</span><span class="sxs-lookup"><span data-stu-id="edc38-200">In the next tutorial you'll see some ways to implement the repository and unit of work patterns.</span></span>

<span data-ttu-id="edc38-201">その他の Entity Framework リソースへのリンクが記載されて、 [ASP.NET データ アクセス コンテンツ マップ](../../../../whitepapers/aspnet-data-access-content-map.md)します。</span><span class="sxs-lookup"><span data-stu-id="edc38-201">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="edc38-202">[前へ](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [次へ](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="edc38-202">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span></span>
