---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: データベース データ (VB) のテーブルを表示する |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルでは、データベース レコードのセットを表示する 2 つの方法を示します。 HTML ta.. でデータベースレコードのセットをフォーマットする 2 つの方法を示します。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 9b03e6a0d2bf7d2bf59ba4dca3076fa306d3fed4
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541898"
---
# <a name="displaying-a-table-of-database-data-vb"></a><span data-ttu-id="10ee1-104">データベース データの表を表示する (VB)</span><span class="sxs-lookup"><span data-stu-id="10ee1-104">Displaying a Table of Database Data (VB)</span></span>

<span data-ttu-id="10ee1-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="10ee1-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="10ee1-106">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="10ee1-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> <span data-ttu-id="10ee1-107">このチュートリアルでは、データベース レコードのセットを表示する 2 つの方法を示します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="10ee1-108">HTML テーブルのデータベース レコードのセットを書式設定する 2 つの方法を示します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="10ee1-109">まず、ビュー内で直接データベース レコードを書式設定する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="10ee1-110">次に、データベース レコードの書式設定時に部分を利用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>

<span data-ttu-id="10ee1-111">このチュートリアルの目的は、ASP.NET MVC アプリケーションでデータベース データの HTML テーブルを表示する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="10ee1-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="10ee1-112">まず、Visual Studio に含まれるスキャフォールディング ツールを使用して、レコードのセットを自動的に表示するビューを生成する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="10ee1-113">次に、データベース レコードの書式設定時に部分をテンプレートとして使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="10ee1-114">モデル クラスの作成</span><span class="sxs-lookup"><span data-stu-id="10ee1-114">Create the Model Classes</span></span>

<span data-ttu-id="10ee1-115">映画データベーステーブルからレコードのセットを表示します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="10ee1-116">Movies データベース テーブルには、次の列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="10ee1-116">The Movies database table contains the following columns:</span></span>

<a id="0.4_table01"></a>

| <span data-ttu-id="10ee1-117">**列名**</span><span class="sxs-lookup"><span data-stu-id="10ee1-117">**Column Name**</span></span> | <span data-ttu-id="10ee1-118">**[データ型]**</span><span class="sxs-lookup"><span data-stu-id="10ee1-118">**Data Type**</span></span> | <span data-ttu-id="10ee1-119">**NULL を許可する**</span><span class="sxs-lookup"><span data-stu-id="10ee1-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10ee1-120">Id</span><span class="sxs-lookup"><span data-stu-id="10ee1-120">Id</span></span> | <span data-ttu-id="10ee1-121">int</span><span class="sxs-lookup"><span data-stu-id="10ee1-121">Int</span></span> | <span data-ttu-id="10ee1-122">False</span><span class="sxs-lookup"><span data-stu-id="10ee1-122">False</span></span> |
| <span data-ttu-id="10ee1-123">タイトル</span><span class="sxs-lookup"><span data-stu-id="10ee1-123">Title</span></span> | <span data-ttu-id="10ee1-124">ンヴァルチャル(200)</span><span class="sxs-lookup"><span data-stu-id="10ee1-124">Nvarchar(200)</span></span> | <span data-ttu-id="10ee1-125">False</span><span class="sxs-lookup"><span data-stu-id="10ee1-125">False</span></span> |
| <span data-ttu-id="10ee1-126">ディレクター</span><span class="sxs-lookup"><span data-stu-id="10ee1-126">Director</span></span> | <span data-ttu-id="10ee1-127">NVarchar(50)</span><span class="sxs-lookup"><span data-stu-id="10ee1-127">NVarchar(50)</span></span> | <span data-ttu-id="10ee1-128">False</span><span class="sxs-lookup"><span data-stu-id="10ee1-128">False</span></span> |
| <span data-ttu-id="10ee1-129">日付リリース済</span><span class="sxs-lookup"><span data-stu-id="10ee1-129">DateReleased</span></span> | <span data-ttu-id="10ee1-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="10ee1-130">DateTime</span></span> | <span data-ttu-id="10ee1-131">False</span><span class="sxs-lookup"><span data-stu-id="10ee1-131">False</span></span> |

<span data-ttu-id="10ee1-132">ASP.NET MVC アプリケーションで Movies テーブルを表すために、モデル クラスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10ee1-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="10ee1-133">このチュートリアルでは、Microsoft エンティティ フレームワークを使用して、モデル クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="10ee1-134">このチュートリアルでは、マイクロソフト エンティティ フレームワークを使用します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="10ee1-135">ただし、LINQ to SQL、NHibernate、またはADO.NETを含む ASP.NET MVC アプリケーションからデータベースを操作するには、さまざまなテクノロジを使用できることを理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="10ee1-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>

<span data-ttu-id="10ee1-136">エンティティ データ モデル ウィザードを起動するには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="10ee1-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="10ee1-137">ソリューション エクスプローラ ウィンドウで Models フォルダを右クリックし、メニュー オプションの **[追加]、[新しい項目]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="10ee1-138">**[データ**] カテゴリを選択し **、[ADO.NET エンティティ データ モデル]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="10ee1-139">データ モデルに*MoviesDBModel.edmx*という名前を付け、[**追加**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="10ee1-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="10ee1-140">[追加] ボタンをクリックすると、エンティティ データ モデル ウィザードが表示されます (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="10ee1-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="10ee1-141">ウィザードを完了するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="10ee1-142">[**モデル コンテンツの選択]** ステップで、[**データベースから生成**] オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="10ee1-143">[**データ接続の選択]** ステップで *、MoviesDB.mdf*データ接続と、接続設定の*名前を*使用します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="10ee1-144">**[次へ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="10ee1-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="10ee1-145">[**データベース オブジェクトの選択]** ステップで、[テーブル] ノードを展開し、[Movies] テーブルを選択します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="10ee1-146">*名前空間のモデル*を入力し、[**完了**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="10ee1-146">Enter the namespace *Models* and click the **Finish** button.</span></span>

<span data-ttu-id="10ee1-147">[![LINQ to SQL クラスの作成](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="10ee1-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)</span></span>

<span data-ttu-id="10ee1-148">**図 01**: LINQ to SQL クラスの作成 ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image2.png)して )</span><span class="sxs-lookup"><span data-stu-id="10ee1-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image2.png))</span></span>

<span data-ttu-id="10ee1-149">エンティティ データ モデル ウィザードを完了すると、エンティティ データ モデル デザイナーが開きます。</span><span class="sxs-lookup"><span data-stu-id="10ee1-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="10ee1-150">デザイナーは、Movies エンティティを表示する必要があります (図 2 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="10ee1-150">The Designer should display the Movies entity (see Figure 2).</span></span>

<span data-ttu-id="10ee1-151">[![エンティティ データ モデル デザイナー](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="10ee1-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)</span></span>

<span data-ttu-id="10ee1-152">**図 02**: エンティティ データ モデル デザイナ ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image4.png)します )</span><span class="sxs-lookup"><span data-stu-id="10ee1-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image4.png))</span></span>

<span data-ttu-id="10ee1-153">続行する前に、1 つの変更を加える必要があります。</span><span class="sxs-lookup"><span data-stu-id="10ee1-153">We need to make one change before we continue.</span></span> <span data-ttu-id="10ee1-154">エンティティ データ ウィザードは *、Movies*データベース テーブルを表す Movies という名前のモデル クラスを生成します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="10ee1-155">映画クラスを使用して特定のムービーを表現するため、クラスの名前を*映画*ではなく*ムービー* (複数形ではなく単数形) に変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="10ee1-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="10ee1-156">デザイナー画面でクラスの名前をダブルクリックし、クラスの名前を映画からムービーに変更します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="10ee1-157">この変更を行った後、**保存**ボタン (フロッピー ディスクのアイコン) をクリックしてムービー クラスを生成します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="10ee1-158">映画コントローラを作成する</span><span class="sxs-lookup"><span data-stu-id="10ee1-158">Create the Movies Controller</span></span>

<span data-ttu-id="10ee1-159">データベースレコードを表現する方法ができたので、ムービーのコレクションを返すコントローラを作成できます。</span><span class="sxs-lookup"><span data-stu-id="10ee1-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="10ee1-160">Visual Studio ソリューション エクスプローラー ウィンドウで、[コントローラー] フォルダーを右クリックし、メニュー オプション**の [追加]、[コント ローラー** ] を選択します (図 3 参照)。</span><span class="sxs-lookup"><span data-stu-id="10ee1-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>

<span data-ttu-id="10ee1-161">[![[コントローラーの追加] メニュー](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="10ee1-161">[![The Add Controller Menu](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)</span></span>

<span data-ttu-id="10ee1-162">**図 03**: コントローラの追加メニュー ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="10ee1-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image6.png))</span></span>

<span data-ttu-id="10ee1-163">[**コントローラの追加**] ダイアログが表示されたら、コントローラ名を MovieController に入力します (図 4 を参照)。</span><span class="sxs-lookup"><span data-stu-id="10ee1-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="10ee1-164">[**追加**]ボタンをクリックして、新しいコントローラを追加します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-164">Click the **Add** button to add the new controller.</span></span>

<span data-ttu-id="10ee1-165">[![[コントローラの追加] ダイアログ](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="10ee1-165">[![The Add Controller dialog](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)</span></span>

<span data-ttu-id="10ee1-166">**図 04**: [コントローラの追加] ダイアログボックス ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="10ee1-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image8.png))</span></span>

<span data-ttu-id="10ee1-167">ムービーコントローラが公開する Index() アクションを変更して、データベースレコードのセットを返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="10ee1-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="10ee1-168">リスト 1 のコントローラーのように見えるコントローラーを変更します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="10ee1-169">**リスト 1 - コントローラ\ムービーコントローラー.vb**</span><span class="sxs-lookup"><span data-stu-id="10ee1-169">**Listing 1 – Controllers\MovieController.vb**</span></span>

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

<span data-ttu-id="10ee1-170">リスト 1 では、MoviesDBEntities クラスを使用して、MoviesDB データベースを表します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="10ee1-171">式*エンティティ。ムービーセット.ToList()は*、映画データベーステーブルからすべてのムービーのセットを返します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-171">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="10ee1-172">ビューの作成</span><span class="sxs-lookup"><span data-stu-id="10ee1-172">Create the View</span></span>

<span data-ttu-id="10ee1-173">HTML テーブルに一連のデータベース レコードを表示する最も簡単な方法は、Visual Studio によって提供されるスキャフォールディングを利用することです。</span><span class="sxs-lookup"><span data-stu-id="10ee1-173">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="10ee1-174">メニュー オプションの [**ビルド]、[ ソリューションのビルド**] の順に選択してアプリケーションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="10ee1-174">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="10ee1-175">**[ビューの追加]** ダイアログを開く前にアプリケーションをビルドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="10ee1-175">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="10ee1-176">Index() アクションを右クリックし、メニュー オプションの**ビューの追加**を選択します (図 5 を参照)。</span><span class="sxs-lookup"><span data-stu-id="10ee1-176">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>

<span data-ttu-id="10ee1-177">[![ビューの追加](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="10ee1-177">[![Adding a view](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)</span></span>

<span data-ttu-id="10ee1-178">**図 05**: ビューの追加 ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="10ee1-178">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image10.png))</span></span>

<span data-ttu-id="10ee1-179">[**ビューの追加]** ダイアログで、[厳密に**型指定されたビューを作成**する] チェック ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="10ee1-179">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="10ee1-180">**ビュー データ**クラスとして Movie クラスを選択します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-180">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="10ee1-181">**ビューの内容**として *[リスト]* を選択します (図 6 を参照)。</span><span class="sxs-lookup"><span data-stu-id="10ee1-181">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="10ee1-182">これらのオプションを選択すると、ムービーの一覧を表示する厳密に型指定されたビューが生成されます。</span><span class="sxs-lookup"><span data-stu-id="10ee1-182">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>

<span data-ttu-id="10ee1-183">[![[ビューの追加] ダイアログ](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="10ee1-183">[![The Add View dialog](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)</span></span>

<span data-ttu-id="10ee1-184">**図 06**: [ビューの追加] ダイアログボックス ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="10ee1-184">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image12.png))</span></span>

<span data-ttu-id="10ee1-185">**[追加**] ボタンをクリックすると、リスト 2 のビューが自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="10ee1-185">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="10ee1-186">このビューには、ムービーのコレクションを反復処理し、ムービーの各プロパティを表示するために必要なコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="10ee1-186">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="10ee1-187">**リスト 2 - ビュー\ムービー\インデックス.aspx**</span><span class="sxs-lookup"><span data-stu-id="10ee1-187">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

<span data-ttu-id="10ee1-188">アプリケーションを実行するには、メニュー オプションの **[デバッグ]、[デバッグの開始**] を選択します (または F5 キーを押します)。</span><span class="sxs-lookup"><span data-stu-id="10ee1-188">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="10ee1-189">アプリケーションを実行すると、インターネット エクスプローラが起動します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-189">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="10ee1-190">/Movie URL に移動すると、図 7 のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="10ee1-190">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>

<span data-ttu-id="10ee1-191">[![映画のテーブル](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="10ee1-191">[![A table of movies](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)</span></span>

<span data-ttu-id="10ee1-192">**図07**: 動画の表 ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="10ee1-192">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image14.png))</span></span>

<span data-ttu-id="10ee1-193">図 7 のデータベース レコードのグリッドの外観について何も気に入らない場合は、インデックス ビューを変更するだけです。</span><span class="sxs-lookup"><span data-stu-id="10ee1-193">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="10ee1-194">たとえば、インデックス ビューを変更して *、DateReleased*ヘッダーを *[リリース日]* に変更できます。</span><span class="sxs-lookup"><span data-stu-id="10ee1-194">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="10ee1-195">部分を含むテンプレートを作成する</span><span class="sxs-lookup"><span data-stu-id="10ee1-195">Create a Template with a Partial</span></span>

<span data-ttu-id="10ee1-196">ビューが複雑になりすぎる場合は、ビューをパーシャルに分割することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="10ee1-196">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="10ee1-197">パーシャルを使用すると、ビューの理解と維持が容易になります。</span><span class="sxs-lookup"><span data-stu-id="10ee1-197">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="10ee1-198">ムービー データベースの各レコードを書式設定するテンプレートとして使用できる部分を作成します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-198">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="10ee1-199">部分を作成するには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="10ee1-199">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="10ee1-200">[ビュー]\Movie フォルダを右クリックし、メニュー オプションの [**ビューの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-200">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="10ee1-201">*[部分ビューの作成 (.ascx)]* というラベルの付いたチェック ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="10ee1-201">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="10ee1-202">部分的な*ムービーテンプレートに名前を付けます*。</span><span class="sxs-lookup"><span data-stu-id="10ee1-202">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="10ee1-203">[**厳密に型指定されたビューを作成する**] チェック ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="10ee1-203">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="10ee1-204">ビュー データ*クラス*として [ムービー] を選択します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-204">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="10ee1-205">*ビューのコンテンツ*として [空] を選択します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-205">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="10ee1-206">[**追加**] ボタンをクリックして、部分をプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-206">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="10ee1-207">これらの手順を完了したら、ムービー テンプレートの一部をリスト 3 のように変更します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-207">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="10ee1-208">**リスト 3 – ビュー\ムービー\ムービーテンプレート.ascx**</span><span class="sxs-lookup"><span data-stu-id="10ee1-208">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

<span data-ttu-id="10ee1-209">リスト 3 の部分には、1 行のレコードのテンプレートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="10ee1-209">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="10ee1-210">リスト 4 の変更されたインデックス ビューでは、ムービー テンプレートの部分を使用します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-210">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="10ee1-211">**リスト 4 - ビュー\ムービー\インデックス.aspx**</span><span class="sxs-lookup"><span data-stu-id="10ee1-211">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

<span data-ttu-id="10ee1-212">リスト 4 のビューには、すべてのムービーを反復処理する For Each ループが含まれています。</span><span class="sxs-lookup"><span data-stu-id="10ee1-212">The view in Listing 4 contains a For Each loop that iterates through all of the movies.</span></span> <span data-ttu-id="10ee1-213">ムービーごとに、ムービーテンプレートの部分を使用してムービーのフォーマットを設定します。</span><span class="sxs-lookup"><span data-stu-id="10ee1-213">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="10ee1-214">レンダリングテンプレートは、ヘルパー メソッドを呼び出すことによってレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="10ee1-214">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="10ee1-215">変更されたインデックス ビューでは、データベース レコードの HTML テーブルとまったく同じものがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="10ee1-215">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="10ee1-216">しかし、ビューは大幅に簡略化されました。</span><span class="sxs-lookup"><span data-stu-id="10ee1-216">However, the view has been greatly simplified.</span></span>

<span data-ttu-id="10ee1-217">RenderPartial() メソッドは文字列を返さないため、他のほとんどのヘルパー メソッドとは異なります。</span><span class="sxs-lookup"><span data-stu-id="10ee1-217">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="10ee1-218">したがって、%= Html.RenderPartial() &lt;% の&gt;&lt;代わりに % Html.RenderPartial() % を&gt;使用して RenderPartial() メソッドを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="10ee1-218">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial() %&gt; instead of &lt;%= Html.RenderPartial() %&gt;.</span></span>

## <a name="summary"></a><span data-ttu-id="10ee1-219">まとめ</span><span class="sxs-lookup"><span data-stu-id="10ee1-219">Summary</span></span>

<span data-ttu-id="10ee1-220">このチュートリアルの目的は、HTML テーブルにデータベース レコードのセットを表示する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="10ee1-220">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="10ee1-221">最初に、Microsoft エンティティ フレームワークを利用して、コントローラー アクションからデータベース レコードのセットを返す方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="10ee1-221">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="10ee1-222">次に、Visual Studio スキャフォールディングを使用して、項目のコレクションを自動的に表示するビューを生成する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="10ee1-222">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="10ee1-223">最後に、部分を利用してビューを簡略化する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="10ee1-223">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="10ee1-224">各データベース レコードを書式設定できるように、部分をテンプレートとして使用する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="10ee1-224">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="10ee1-225">[前へ](creating-model-classes-with-linq-to-sql-vb.md)
> [次へ](performing-simple-validation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="10ee1-225">[Previous](creating-model-classes-with-linq-to-sql-vb.md)
[Next](performing-simple-validation-vb.md)</span></span>
