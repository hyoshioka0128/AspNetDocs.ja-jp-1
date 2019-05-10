---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: データベースのデータ (c#) の表を表示する |Microsoft Docs
author: microsoft
description: このチュートリアルでは、一連のデータベース レコードを表示する 2 つの方法を紹介します。 書式設定、HTML でのデータベース レコードのセットを ta の 2 つの方法を紹介しています.
ms.author: riande
ms.date: 10/07/2008
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: c5ee59873468b4928b45ec586386e28cbe94c728
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65122434"
---
# <a name="displaying-a-table-of-database-data-c"></a><span data-ttu-id="16606-104">データベース データの表を表示する (C#)</span><span class="sxs-lookup"><span data-stu-id="16606-104">Displaying a Table of Database Data (C#)</span></span>

<span data-ttu-id="16606-105">によって[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="16606-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="16606-106">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="16606-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> <span data-ttu-id="16606-107">このチュートリアルでは、一連のデータベース レコードを表示する 2 つの方法を紹介します。</span><span class="sxs-lookup"><span data-stu-id="16606-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="16606-108">一連の HTML テーブルのデータベース レコードを書式設定の 2 つの方法を紹介します。</span><span class="sxs-lookup"><span data-stu-id="16606-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="16606-109">最初に、ビュー内で直接、データベース レコードの書式を設定する方法を紹介します。</span><span class="sxs-lookup"><span data-stu-id="16606-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="16606-110">次に、方法を利用するパーシャルのデータベース レコードを書式設定時に紹介します。</span><span class="sxs-lookup"><span data-stu-id="16606-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>

<span data-ttu-id="16606-111">このチュートリアルの目的では、ASP.NET MVC アプリケーションでデータベースのデータの HTML テーブルを表示する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="16606-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="16606-112">まず、Visual Studio に含まれるスキャフォールディング ツールを使用して、一連のレコードを自動的に表示するビューを生成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="16606-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="16606-113">次に、データベース レコードを書式設定時に一部のテンプレートとして使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="16606-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="16606-114">モデル クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="16606-114">Create the Model Classes</span></span>

<span data-ttu-id="16606-115">ここ、映画データベース テーブルからのレコードのセットを表示します。</span><span class="sxs-lookup"><span data-stu-id="16606-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="16606-116">映画データベース テーブルには、次の列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="16606-116">The Movies database table contains the following columns:</span></span>

<a id="0.3_table01"></a>

| <span data-ttu-id="16606-117">**列名**</span><span class="sxs-lookup"><span data-stu-id="16606-117">**Column Name**</span></span> | <span data-ttu-id="16606-118">**[データ型]**</span><span class="sxs-lookup"><span data-stu-id="16606-118">**Data Type**</span></span> | <span data-ttu-id="16606-119">**Null を許容します。**</span><span class="sxs-lookup"><span data-stu-id="16606-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16606-120">ID</span><span class="sxs-lookup"><span data-stu-id="16606-120">Id</span></span> | <span data-ttu-id="16606-121">Int</span><span class="sxs-lookup"><span data-stu-id="16606-121">Int</span></span> | <span data-ttu-id="16606-122">False</span><span class="sxs-lookup"><span data-stu-id="16606-122">False</span></span> |
| <span data-ttu-id="16606-123">Title</span><span class="sxs-lookup"><span data-stu-id="16606-123">Title</span></span> | <span data-ttu-id="16606-124">Nvarchar(200)</span><span class="sxs-lookup"><span data-stu-id="16606-124">Nvarchar(200)</span></span> | <span data-ttu-id="16606-125">False</span><span class="sxs-lookup"><span data-stu-id="16606-125">False</span></span> |
| <span data-ttu-id="16606-126">ディレクター</span><span class="sxs-lookup"><span data-stu-id="16606-126">Director</span></span> | <span data-ttu-id="16606-127">Nvarchar (50)</span><span class="sxs-lookup"><span data-stu-id="16606-127">NVarchar(50)</span></span> | <span data-ttu-id="16606-128">False</span><span class="sxs-lookup"><span data-stu-id="16606-128">False</span></span> |
| <span data-ttu-id="16606-129">DateReleased</span><span class="sxs-lookup"><span data-stu-id="16606-129">DateReleased</span></span> | <span data-ttu-id="16606-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="16606-130">DateTime</span></span> | <span data-ttu-id="16606-131">False</span><span class="sxs-lookup"><span data-stu-id="16606-131">False</span></span> |

<span data-ttu-id="16606-132">ASP.NET MVC アプリケーションで映画のテーブルを表すためには、モデル クラスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="16606-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="16606-133">このチュートリアルでは、モデル クラスを作成するのに Microsoft Entity Framework を使用します。</span><span class="sxs-lookup"><span data-stu-id="16606-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="16606-134">このチュートリアルでは、Microsoft Entity Framework を使用します。</span><span class="sxs-lookup"><span data-stu-id="16606-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="16606-135">ただし、LINQ to SQL、NHibernate、または ADO.NET を含む、ASP.NET MVC アプリケーションからデータベースと対話する多様なテクノロジを使用することができますを理解しておく必要です。</span><span class="sxs-lookup"><span data-stu-id="16606-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>

<span data-ttu-id="16606-136">エンティティ データ モデル ウィザードを起動する次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="16606-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="16606-137">ソリューション エクスプ ローラー ウィンドウおよびメニュー オプションを選択して、モデル フォルダーを右クリックして**追加、新しい項目の**します。</span><span class="sxs-lookup"><span data-stu-id="16606-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="16606-138">選択、**データ**カテゴリと選択、 **ADO.NET Entity Data Model**テンプレート。</span><span class="sxs-lookup"><span data-stu-id="16606-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="16606-139">データ モデルに名前を付けます*MoviesDBModel.edmx*  をクリックし、**追加**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16606-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="16606-140">[追加] ボタンをクリックした後、Entity Data Model ウィザードでは、(図 1 参照) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="16606-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="16606-141">ウィザードの次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="16606-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="16606-142">**モデルのコンテンツの選択**手順で、**データベースから生成**オプション。</span><span class="sxs-lookup"><span data-stu-id="16606-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="16606-143">**データ接続の選択**ステップで、使用、 *MoviesDB.mdf*データ接続と名前*MoviesDBEntities*接続の設定。</span><span class="sxs-lookup"><span data-stu-id="16606-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="16606-144">をクリックして、**次**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16606-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="16606-145">**データベース オブジェクトの選択**ステップ、[テーブル] ノードを展開し、映画のテーブルを選択します。</span><span class="sxs-lookup"><span data-stu-id="16606-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="16606-146">名前空間を入力*モデル* をクリックし、**完了**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16606-146">Enter the namespace *Models* and click the **Finish** button.</span></span>

<span data-ttu-id="16606-147">[![LINQ to SQL クラスを作成](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="16606-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span></span>

<span data-ttu-id="16606-148">**図 01**:LINQ to SQL クラスを作成 ([フルサイズの画像を表示する をクリックします](displaying-a-table-of-database-data-cs/_static/image2.png))。</span><span class="sxs-lookup"><span data-stu-id="16606-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image2.png))</span></span>

<span data-ttu-id="16606-149">Entity Data Model ウィザードを完了すると、Entity Data Model のデザイナーが開きます。</span><span class="sxs-lookup"><span data-stu-id="16606-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="16606-150">デザイナーは、ムービー エンティティを表示する必要があります (図 2 参照)。</span><span class="sxs-lookup"><span data-stu-id="16606-150">The Designer should display the Movies entity (see Figure 2).</span></span>

<span data-ttu-id="16606-151">[![Entity Data Model デザイナー](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="16606-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span></span>

<span data-ttu-id="16606-152">**図 02**:Entity Data Model デザイナー ([フルサイズの画像を表示する をクリックします](displaying-a-table-of-database-data-cs/_static/image4.png))。</span><span class="sxs-lookup"><span data-stu-id="16606-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image4.png))</span></span>

<span data-ttu-id="16606-153">続行する前に 1 つの変更を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="16606-153">We need to make one change before we continue.</span></span> <span data-ttu-id="16606-154">という名前のモデル クラスを生成するエンティティのデータ ウィザード*映画*映画データベース テーブルを表します。</span><span class="sxs-lookup"><span data-stu-id="16606-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="16606-155">映画クラスを使用して、特定のムービーを表す、ためにクラスの名前を変更する必要があります*ムービー*の代わりに*映画*(単数形ではなく複数形)。</span><span class="sxs-lookup"><span data-stu-id="16606-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="16606-156">デザイナー画面で、クラスの名前をダブルクリックし、ムービーからムービーにクラスの名前を変更します。</span><span class="sxs-lookup"><span data-stu-id="16606-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="16606-157">この変更を加えたら、 をクリックして、**保存**ムービー クラスを生成する (フロッピー ディスクのアイコン) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="16606-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="16606-158">ムービー コント ローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="16606-158">Create the Movies Controller</span></span>

<span data-ttu-id="16606-159">あるので、データベース レコードを表す方法、映画のコレクションを返すコント ローラーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="16606-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="16606-160">Visual Studio ソリューション エクスプ ローラー ウィンドウで、Controllers フォルダーを右クリックし、メニュー オプションを選択します**追加、コント ローラー** (図 3 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="16606-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>

<span data-ttu-id="16606-161">[![コント ローラーのメニューに追加します。](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="16606-161">[![The Add Controller Menu](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span></span>

<span data-ttu-id="16606-162">**図 03**:コント ローラーの追加 メニュー ([フルサイズの画像を表示する をクリックします](displaying-a-table-of-database-data-cs/_static/image6.png))。</span><span class="sxs-lookup"><span data-stu-id="16606-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image6.png))</span></span>

<span data-ttu-id="16606-163">ときに、**コント ローラーの追加**ダイアログが表示されたら、MovieController コント ローラー名を入力します (図 4 参照)。</span><span class="sxs-lookup"><span data-stu-id="16606-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="16606-164">をクリックして、**追加**新しいコント ローラーを追加するボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16606-164">Click the **Add** button to add the new controller.</span></span>

<span data-ttu-id="16606-165">[![コント ローラーの追加 ダイアログ](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="16606-165">[![The Add Controller dialog](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span></span>

<span data-ttu-id="16606-166">**図 04**:コント ローラーの追加 ダイアログ ([フルサイズの画像を表示する をクリックします](displaying-a-table-of-database-data-cs/_static/image8.png))。</span><span class="sxs-lookup"><span data-stu-id="16606-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image8.png))</span></span>

<span data-ttu-id="16606-167">データベースのレコードのセットを返すように、ムービー コント ローラーによって公開される Index() アクションを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="16606-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="16606-168">コント ローラーを変更して、リスト 1 でコント ローラーのように見えます。</span><span class="sxs-lookup"><span data-stu-id="16606-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="16606-169">**Listing 1 – Controllers\MovieController.cs**</span><span class="sxs-lookup"><span data-stu-id="16606-169">**Listing 1 – Controllers\MovieController.cs**</span></span>

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

<span data-ttu-id="16606-170">リストの 1 では、MoviesDBEntities クラスを使用してを MoviesDB データベースを表します。</span><span class="sxs-lookup"><span data-stu-id="16606-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="16606-171">このクラスを使用するには、このような MvcApplication1.Models 名前空間をインポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="16606-171">To use this class, you need to import the MvcApplication1.Models namespace like this:</span></span>

<span data-ttu-id="16606-172">MvcApplication1.Models; を使用します。</span><span class="sxs-lookup"><span data-stu-id="16606-172">using MvcApplication1.Models;</span></span>

<span data-ttu-id="16606-173">式*エンティティ。MovieSet.ToList()* 映画データベース テーブルからすべての映画のセットを返します。</span><span class="sxs-lookup"><span data-stu-id="16606-173">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="16606-174">ビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="16606-174">Create the View</span></span>

<span data-ttu-id="16606-175">HTML テーブルの一連のデータベース レコードを表示する最も簡単な方法は、Visual Studio によって提供されるスキャフォールディングを活用するためにです。</span><span class="sxs-lookup"><span data-stu-id="16606-175">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="16606-176">メニュー オプションを選択して、アプリケーションをビルド**ソリューションのビルドをビルドします。** します。</span><span class="sxs-lookup"><span data-stu-id="16606-176">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="16606-177">開始する前に、アプリケーションをビルドする必要があります、**ビューの追加**ダイアログや、データ クラスは、ダイアログ ボックスに表示されません。</span><span class="sxs-lookup"><span data-stu-id="16606-177">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="16606-178">Index() アクションを右クリックし、メニュー オプションを選択**ビューの追加**(図 5 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="16606-178">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>

<span data-ttu-id="16606-179">[![ビューの追加](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="16606-179">[![Adding a view](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span></span>

<span data-ttu-id="16606-180">**図 05**:ビューの追加 ([フルサイズの画像を表示する をクリックします](displaying-a-table-of-database-data-cs/_static/image10.png))。</span><span class="sxs-lookup"><span data-stu-id="16606-180">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image10.png))</span></span>

<span data-ttu-id="16606-181">**ビューの追加**ダイアログ ボックスで、チェック ボックスをラベル付け**厳密に型指定されたビューを作成**。</span><span class="sxs-lookup"><span data-stu-id="16606-181">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="16606-182">としてムービー クラスの選択、**データ クラスを表示**します。</span><span class="sxs-lookup"><span data-stu-id="16606-182">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="16606-183">選択*一覧*として、**コンテンツを表示**(図 6 参照)。</span><span class="sxs-lookup"><span data-stu-id="16606-183">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="16606-184">これらのオプションを選択すると、ムービーの一覧を表示する厳密に型指定されたビューが生成されます。</span><span class="sxs-lookup"><span data-stu-id="16606-184">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>

<span data-ttu-id="16606-185">[![ビューの追加 ダイアログ](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="16606-185">[![The Add View dialog](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span></span>

<span data-ttu-id="16606-186">**図 06**:ビューの追加 ダイアログ ([フルサイズの画像を表示する をクリックします](displaying-a-table-of-database-data-cs/_static/image12.png))。</span><span class="sxs-lookup"><span data-stu-id="16606-186">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image12.png))</span></span>

<span data-ttu-id="16606-187">クリックした後、**追加**ボタン、リスト 2 でビューが自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="16606-187">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="16606-188">このビューには、映画のコレクションを反復処理し、各ビデオのプロパティの表示に必要なコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="16606-188">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="16606-189">**2 – Views\Movie\Index.aspx を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="16606-189">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

<span data-ttu-id="16606-190">アプリケーションを実行するには、メニュー オプションを選択して**デバッグ、デバッグの開始** (または、F5 キー)。</span><span class="sxs-lookup"><span data-stu-id="16606-190">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="16606-191">アプリケーションを実行すると、Internet Explorer が起動します。</span><span class="sxs-lookup"><span data-stu-id="16606-191">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="16606-192">/Movie URL に移動すると、図 7 ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="16606-192">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>

<span data-ttu-id="16606-193">[![映画のテーブル](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="16606-193">[![A table of movies](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span></span>

<span data-ttu-id="16606-194">**図 07**:映画のテーブル ([フルサイズの画像を表示する をクリックします](displaying-a-table-of-database-data-cs/_static/image14.png))。</span><span class="sxs-lookup"><span data-stu-id="16606-194">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image14.png))</span></span>

<span data-ttu-id="16606-195">図 7 内のデータベース レコードのグリッドの外観について何も満足できない場合は、インデックス ビューだけ変更できます。</span><span class="sxs-lookup"><span data-stu-id="16606-195">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="16606-196">たとえば、変更、 *DateReleased*ヘッダーを*リリース日*インデックス ビューを変更することで。</span><span class="sxs-lookup"><span data-stu-id="16606-196">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="16606-197">一部のテンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="16606-197">Create a Template with a Partial</span></span>

<span data-ttu-id="16606-198">ビューは、複雑すぎるようですは、パーシャル、ビューに分割を開始することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="16606-198">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="16606-199">パーシャルを使用すると、ビューの理解および保守簡単です。</span><span class="sxs-lookup"><span data-stu-id="16606-199">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="16606-200">部分を作成します各ムービー データベース レコードを書式設定するテンプレートとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="16606-200">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="16606-201">部分を作成する次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="16606-201">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="16606-202">Views\Movie フォルダーを右クリックし、メニュー オプションを選択**ビューの追加**します。</span><span class="sxs-lookup"><span data-stu-id="16606-202">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="16606-203">チェック ボックスをオンというラベルの付いた*部分ビュー (.ascx) を作成*です。</span><span class="sxs-lookup"><span data-stu-id="16606-203">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="16606-204">部分的な名前を付けます*MovieTemplate*します。</span><span class="sxs-lookup"><span data-stu-id="16606-204">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="16606-205">チェック ボックスをラベル付け**厳密に型指定されたビューを作成する**します。</span><span class="sxs-lookup"><span data-stu-id="16606-205">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="16606-206">としてムービーを選択して、*データ クラスを表示*します。</span><span class="sxs-lookup"><span data-stu-id="16606-206">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="16606-207">として空の選択、*コンテンツを表示*します。</span><span class="sxs-lookup"><span data-stu-id="16606-207">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="16606-208">をクリックして、**追加**部分をプロジェクトに追加するボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="16606-208">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="16606-209">次の手順を完了すると、リスト 3 のように部分的な MovieTemplate を変更します。</span><span class="sxs-lookup"><span data-stu-id="16606-209">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="16606-210">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span><span class="sxs-lookup"><span data-stu-id="16606-210">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

<span data-ttu-id="16606-211">リスト 3 の部分には、レコードの 1 つの行のテンプレートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="16606-211">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="16606-212">リスト 4 変更後のインデックス ビューは、部分的な MovieTemplate を使用します。</span><span class="sxs-lookup"><span data-stu-id="16606-212">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="16606-213">**Listing 4 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="16606-213">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

<span data-ttu-id="16606-214">リスト 4 のビューには、すべての映画を反復処理する foreach ループが含まれています。</span><span class="sxs-lookup"><span data-stu-id="16606-214">The view in Listing 4 contains a foreach loop that iterates through all of the movies.</span></span> <span data-ttu-id="16606-215">各ムービーの MovieTemplate 部分は、ムービーを書式設定に使用されます。</span><span class="sxs-lookup"><span data-stu-id="16606-215">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="16606-216">RenderPartial() ヘルパー メソッドを呼び出して、MovieTemplate がレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="16606-216">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="16606-217">変更したのインデックス ビューは、データベース レコードのまったく同じ HTML テーブルを表示します。</span><span class="sxs-lookup"><span data-stu-id="16606-217">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="16606-218">ただし、ビューが大幅に簡略化されました。</span><span class="sxs-lookup"><span data-stu-id="16606-218">However, the view has been greatly simplified.</span></span>

<span data-ttu-id="16606-219">RenderPartial() メソッドは、文字列を返さないため、ほとんどの他のヘルパー メソッドとは異なる。</span><span class="sxs-lookup"><span data-stu-id="16606-219">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="16606-220">RenderPartial() メソッドを使用して、呼び出す必要がありますので、 &lt;Html.RenderPartial(); %&gt;の代わりに&lt;% = Html.RenderPartial(); %&gt;します。</span><span class="sxs-lookup"><span data-stu-id="16606-220">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial(); %&gt; instead of &lt;%= Html.RenderPartial(); %&gt;.</span></span>

## <a name="summary"></a><span data-ttu-id="16606-221">まとめ</span><span class="sxs-lookup"><span data-stu-id="16606-221">Summary</span></span>

<span data-ttu-id="16606-222">このチュートリアルの目的は、HTML テーブルの一連のデータベース レコードを表示する方法を説明することでした。</span><span class="sxs-lookup"><span data-stu-id="16606-222">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="16606-223">最初に、Microsoft Entity Framework を活用して、コント ローラー アクションから一連のデータベース レコードを返す方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="16606-223">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="16606-224">次に、Visual Studio のスキャフォールディングを使用して、項目のコレクションを自動的に表示するビューを生成する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="16606-224">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="16606-225">最後に、一部を活用して、ビューを簡略化する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="16606-225">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="16606-226">データベースのレコードの書式を設定することができるように、テンプレートとして、部分的なを使用する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="16606-226">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="16606-227">[前へ](creating-model-classes-with-linq-to-sql-cs.md)
> [次へ](performing-simple-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="16606-227">[Previous](creating-model-classes-with-linq-to-sql-cs.md)
[Next](performing-simple-validation-cs.md)</span></span>
