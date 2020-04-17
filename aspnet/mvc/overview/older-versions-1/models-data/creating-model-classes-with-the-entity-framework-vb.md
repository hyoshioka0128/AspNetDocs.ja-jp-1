---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
title: エンティティ フレームワーク (VB) を使用してモデル クラスを作成する |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルでは、マイクロソフト エンティティ フレームワークASP.NET MVC を使用する方法を学習します。 エンティティ ウィザードを使用して ADO.NET エンティティ Da.. を作成する方法を学習します。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: ff8322c9-12f3-4e24-aba6-a38046b9bb0d
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
msc.type: authoredcontent
ms.openlocfilehash: cdba91969a6ed9c02965999bbc48d5c5cdea140d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542652"
---
# <a name="creating-model-classes-with-the-entity-framework-vb"></a><span data-ttu-id="44ca7-104">Entity Framework でモデル クラスを作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="44ca7-104">Creating Model Classes with the Entity Framework (VB)</span></span>

<span data-ttu-id="44ca7-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="44ca7-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="44ca7-106">このチュートリアルでは、マイクロソフト エンティティ フレームワークASP.NET MVC を使用する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-106">In this tutorial, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="44ca7-107">エンティティ ウィザードを使用して、ADO.NET エンティティ データ モデルを作成する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-107">You learn how to use the Entity Wizard to create an ADO.NET Entity Data Model.</span></span> <span data-ttu-id="44ca7-108">このチュートリアルでは、Entity Framework を使用してデータベース データを選択、挿入、更新、および削除する方法を示す Web アプリケーションを構築します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-108">Over the course of this tutorial, we build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>

<span data-ttu-id="44ca7-109">このチュートリアルの目的は、mvc アプリケーションをビルドするときに Microsoft エンティティ フレームワークを使用してデータ アクセス クラスを作成する方法ASP.NET説明することです。</span><span class="sxs-lookup"><span data-stu-id="44ca7-109">The goal of this tutorial is to explain how you can create data access classes using the Microsoft Entity Framework when building an ASP.NET MVC application.</span></span> <span data-ttu-id="44ca7-110">このチュートリアルでは、マイクロソフト エンティティ フレームワークの以前の知識がないことを前提としています。</span><span class="sxs-lookup"><span data-stu-id="44ca7-110">This tutorial assumes no previous knowledge of the Microsoft Entity Framework.</span></span> <span data-ttu-id="44ca7-111">このチュートリアルの最後に、Entity Framework を使用してデータベース レコードを選択、挿入、更新、および削除する方法を理解します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-111">By the end of this tutorial, you'll understand how to use the Entity Framework to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="44ca7-112">Microsoft エンティティ フレームワークは、データベースからデータ アクセス層を自動的に生成できるオブジェクト リレーショナル マッピング (O/RM) ツールです。</span><span class="sxs-lookup"><span data-stu-id="44ca7-112">The Microsoft Entity Framework is an Object Relational Mapping (O/RM) tool that enables you to generate a data access layer from a database automatically.</span></span> <span data-ttu-id="44ca7-113">Entity Framework を使用すると、データ アクセス クラスを手作業で構築する手間のかたえのある作業を回避できます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-113">The Entity Framework enables you to avoid the tedious work of building your data access classes by hand.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="44ca7-114">ASP.NET MVC とマイクロソフト エンティティ フレームワークの間に不可欠な関係はありません。</span><span class="sxs-lookup"><span data-stu-id="44ca7-114">There is no essential connection between ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="44ca7-115">mvc で使用できる Entity Framework にはいくつかの代替手段ASP.NET用意されています。</span><span class="sxs-lookup"><span data-stu-id="44ca7-115">There are several alternatives to the Entity Framework that you can use with ASP.NET MVC.</span></span> <span data-ttu-id="44ca7-116">たとえば、MICROSOFT LINQ to SQL、NHibernate、または SubSonic などの他の O/RM ツールを使用して、MVC モデル クラスを構築できます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-116">For example, you can build your MVC Model classes using other O/RM tools such as Microsoft LINQ to SQL, NHibernate, or SubSonic.</span></span>

<span data-ttu-id="44ca7-117">ASP.NET MVC で Microsoft エンティティ フレームワークを使用する方法を説明するために、簡単なサンプル アプリケーションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="44ca7-117">In order to illustrate how you can use the Microsoft Entity Framework with ASP.NET MVC, we'll build a simple sample application.</span></span> <span data-ttu-id="44ca7-118">ムービー データベース レコードを表示および編集できるムービー データベース アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-118">We'll create a Movie Database application that enables you to display and edit movie database records.</span></span>

<span data-ttu-id="44ca7-119">このチュートリアルでは、サービス パック 1 を使用して Visual Studio 2008 またはビジュアル Web 開発者 2008 を使用していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="44ca7-119">This tutorial assumes that you have Visual Studio 2008 or Visual Web Developer 2008 with Service Pack 1.</span></span> <span data-ttu-id="44ca7-120">エンティティ フレームワークを使用するには、サービス パック 1 が必要です。</span><span class="sxs-lookup"><span data-stu-id="44ca7-120">You need Service Pack 1 in order to use the Entity Framework.</span></span> <span data-ttu-id="44ca7-121">次のアドレスから、Visual Studio 2008 サービス パック 1 またはサービス パック 1 を使用したビジュアル Web 開発者をダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-121">You can download Visual Studio 2008 Service Pack 1 or Visual Web Developer with Service Pack 1 from the following address:</span></span>

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

## <a name="creating-the-movie-sample-database"></a><span data-ttu-id="44ca7-122">ムービー サンプル データベースの作成</span><span class="sxs-lookup"><span data-stu-id="44ca7-122">Creating the Movie Sample Database</span></span>

<span data-ttu-id="44ca7-123">ムービー データベース アプリケーションでは、次の列を含む Movies という名前のデータベース テーブルを使用します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-123">The Movie Database application uses a database table named Movies that contains the following columns:</span></span>

| <span data-ttu-id="44ca7-124">列名</span><span class="sxs-lookup"><span data-stu-id="44ca7-124">Column Name</span></span> | <span data-ttu-id="44ca7-125">データ型</span><span class="sxs-lookup"><span data-stu-id="44ca7-125">Data Type</span></span> | <span data-ttu-id="44ca7-126">Null を許可しますか?</span><span class="sxs-lookup"><span data-stu-id="44ca7-126">Allow Nulls?</span></span> | <span data-ttu-id="44ca7-127">主キーですか?</span><span class="sxs-lookup"><span data-stu-id="44ca7-127">Is Primary Key?</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="44ca7-128">Id</span><span class="sxs-lookup"><span data-stu-id="44ca7-128">Id</span></span> | <span data-ttu-id="44ca7-129">INT</span><span class="sxs-lookup"><span data-stu-id="44ca7-129">int</span></span> | <span data-ttu-id="44ca7-130">False</span><span class="sxs-lookup"><span data-stu-id="44ca7-130">False</span></span> | <span data-ttu-id="44ca7-131">True</span><span class="sxs-lookup"><span data-stu-id="44ca7-131">True</span></span> |
| <span data-ttu-id="44ca7-132">タイトル</span><span class="sxs-lookup"><span data-stu-id="44ca7-132">Title</span></span> | <span data-ttu-id="44ca7-133">nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="44ca7-133">nvarchar(100)</span></span> | <span data-ttu-id="44ca7-134">False</span><span class="sxs-lookup"><span data-stu-id="44ca7-134">False</span></span> | <span data-ttu-id="44ca7-135">False</span><span class="sxs-lookup"><span data-stu-id="44ca7-135">False</span></span> |
| <span data-ttu-id="44ca7-136">ディレクター</span><span class="sxs-lookup"><span data-stu-id="44ca7-136">Director</span></span> | <span data-ttu-id="44ca7-137">nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="44ca7-137">nvarchar(100)</span></span> | <span data-ttu-id="44ca7-138">False</span><span class="sxs-lookup"><span data-stu-id="44ca7-138">False</span></span> | <span data-ttu-id="44ca7-139">False</span><span class="sxs-lookup"><span data-stu-id="44ca7-139">False</span></span> |

<span data-ttu-id="44ca7-140">次の手順に従って、このテーブルを ASP.NET MVC プロジェクトに追加できます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-140">You can add this table to an ASP.NET MVC project by following these steps:</span></span>

1. <span data-ttu-id="44ca7-141">ソリューション エクスプローラー ウィンドウ\_で [アプリ データ] フォルダーを右クリックし、メニュー オプション**の [追加]、[新しい項目]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-141">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item.**</span></span>
2. <span data-ttu-id="44ca7-142">[**新しい項目の追加]** ダイアログ ボックスで **、[SQL Server データベース**] を選択し、データベース名 MoviesDB.mdf を指定して、[**追加**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="44ca7-142">From the **Add New Item** dialog box, select **SQL Server Database**, give the database the name MoviesDB.mdf, and click the **Add** button.</span></span>
3. <span data-ttu-id="44ca7-143">MoviesDB.mdf ファイルをダブルクリックして、サーバー エクスプローラ/データベース エクスプローラ ウィンドウを開きます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-143">Double-click the MoviesDB.mdf file to open the Server Explorer/Database Explorer window.</span></span>
4. <span data-ttu-id="44ca7-144">MoviesDB.mdf データベース接続を展開し、テーブル フォルダーを右クリックし、メニュー オプション**の新しいテーブルの追加**を選択します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-144">Expand the MoviesDB.mdf database connection, right-click the Tables folder, and select the menu option **Add New Table**.</span></span>
5. <span data-ttu-id="44ca7-145">テーブル デザイナーで、ID、タイトル、およびディレクターの列を追加します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-145">In the Table Designer, add the Id, Title, and Director columns.</span></span>
6. <span data-ttu-id="44ca7-146">[**保存**] ボタン (フロッピーのアイコンが表示されています) をクリックして、新しいテーブルを Movies という名前で保存します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-146">Click the **Save** button (it has the icon of the floppy) to save the new table with the name Movies.</span></span>

<span data-ttu-id="44ca7-147">Movies データベース テーブルを作成した後、サンプル データをテーブルに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44ca7-147">After you create the Movies database table, you should add some sample data to the table.</span></span> <span data-ttu-id="44ca7-148">Movies テーブルを右クリックし、メニュー オプションの [**テーブル データを表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-148">Right-click the Movies table and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="44ca7-149">表示されるグリッドに偽のムービーデータを入力できます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-149">You can enter fake movie data into the grid that appears.</span></span>

## <a name="creating-the-adonet-entity-data-model"></a><span data-ttu-id="44ca7-150">ADO.NET エンティティ データ モデルの作成</span><span class="sxs-lookup"><span data-stu-id="44ca7-150">Creating the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="44ca7-151">エンティティ フレームワークを使用するには、エンティティ データ モデルを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44ca7-151">In order to use the Entity Framework, you need to create an Entity Data Model.</span></span> <span data-ttu-id="44ca7-152">Visual Studio エンティティ データ*モデル ウィザード*を利用して、データベースからエンティティ データ モデルを自動的に生成できます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-152">You can take advantage of the Visual Studio *Entity Data Model Wizard* to generate an Entity Data Model from a database automatically.</span></span>

<span data-ttu-id="44ca7-153">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="44ca7-153">Follow these steps:</span></span>

1. <span data-ttu-id="44ca7-154">ソリューション エクスプローラ ウィンドウで Models フォルダを右クリックし、メニュー オプションの **[追加]、[新しい項目]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-154">Right-click the Models folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="44ca7-155">[**新しい項目の追加]** ダイアログで、[データ] カテゴリを選択します (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="44ca7-155">In the **Add New Item** dialog, select the Data category (see Figure 1).</span></span>
3. <span data-ttu-id="44ca7-156">**[エンティティ データ モデルADO.NETテンプレートを**選択し、エンティティ データ モデルに MoviesDBModel.edmx という名前を付け、[**追加**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="44ca7-156">Select the **ADO.NET Entity Data Model** template, give the Entity Data Model the name MoviesDBModel.edmx, and click the **Add** button.</span></span> <span data-ttu-id="44ca7-157">**[追加**] ボタンをクリックすると、データ モデル ウィザードが起動します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-157">Clicking the **Add** button launches the Data Model Wizard.</span></span>
4. <span data-ttu-id="44ca7-158">[**モデルコンテンツの選択]** ステップで、[**データベースから生成**] オプションを選択し、[**次へ**] ボタンをクリックします (図 2 を参照)。</span><span class="sxs-lookup"><span data-stu-id="44ca7-158">In the **Choose Model Contents** step, choose the **Generate from a database** option and click the **Next** button (see Figure 2).</span></span>
5. <span data-ttu-id="44ca7-159">[**データ接続の選択]** ステップで、MoviesDB.mdf データベース接続を選択し、エンティティ接続設定名を入力して、次**へ**ボタンをクリックします (図 3 を参照)。</span><span class="sxs-lookup"><span data-stu-id="44ca7-159">In the **Choose Your Data Connection** step, select the MoviesDB.mdf database connection, enter the entities connection settings name MoviesDBEntities, and click the **Next** button (see Figure 3).</span></span>
6. <span data-ttu-id="44ca7-160">[**データベース オブジェクトの選択]** ステップで、ムービー データベース テーブルを選択し、[**完了**] ボタンをクリックします (図 4 参照)。</span><span class="sxs-lookup"><span data-stu-id="44ca7-160">In the **Choose Your Database Objects** step, select the Movie database table and click the **Finish** button (see Figure 4).</span></span>

<span data-ttu-id="44ca7-161">これらの手順を完了すると、ADO.NET エンティティ データ モデル デザイナー (エンティティ デザイナー) が開きます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-161">After you complete these steps, the ADO.NET Entity Data Model Designer (Entity Designer) opens.</span></span>

<span data-ttu-id="44ca7-162">**図 1 – 新しいエンティティ データ モデルの作成**</span><span class="sxs-lookup"><span data-stu-id="44ca7-162">**Figure 1 – Creating a new Entity Data Model**</span></span>

![clip_image002](creating-model-classes-with-the-entity-framework-vb/_static/image1.jpg)

<span data-ttu-id="44ca7-164">**図 2 – モデルコンテンツの選択ステップ**</span><span class="sxs-lookup"><span data-stu-id="44ca7-164">**Figure 2 – Choose Model Contents Step**</span></span>

![clip_image004](creating-model-classes-with-the-entity-framework-vb/_static/image2.jpg)

<span data-ttu-id="44ca7-166">**図 3 – データ接続の選択**</span><span class="sxs-lookup"><span data-stu-id="44ca7-166">**Figure 3 – Choose Your Data Connection**</span></span>

![clip_image006](creating-model-classes-with-the-entity-framework-vb/_static/image3.jpg)

<span data-ttu-id="44ca7-168">**図 4 – データベース オブジェクトの選択**</span><span class="sxs-lookup"><span data-stu-id="44ca7-168">**Figure 4 – Choose Your Database Objects**</span></span>

![clip_image008](creating-model-classes-with-the-entity-framework-vb/_static/image4.jpg)

## <a name="modifying-the-adonet-entity-data-model"></a><span data-ttu-id="44ca7-170">ADO.NET エンティティ データ モデルの変更</span><span class="sxs-lookup"><span data-stu-id="44ca7-170">Modifying the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="44ca7-171">エンティティ データ モデルを作成した後、エンティティ デザイナーを利用してモデルを変更できます (図 5 参照)。</span><span class="sxs-lookup"><span data-stu-id="44ca7-171">After you create an Entity Data Model, you can modify the model by taking advantage of the Entity Designer (see Figure 5).</span></span> <span data-ttu-id="44ca7-172">エンティティ デザイナーは、ソリューション エクスプローラー ウィンドウ内のモデル フォルダーに含まれている MoviesDBModel.edmx ファイルをダブルクリックして、いつでも開くことができます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-172">You can open the Entity Designer at any time by double-clicking the MoviesDBModel.edmx file contained in the Models folder within the Solution Explorer window.</span></span>

<span data-ttu-id="44ca7-173">**図 5 – エンティティ データ モデル デザイナーADO.NET**</span><span class="sxs-lookup"><span data-stu-id="44ca7-173">**Figure 5 – The ADO.NET Entity Data Model Designer**</span></span>

![clip_image010](creating-model-classes-with-the-entity-framework-vb/_static/image5.jpg)

<span data-ttu-id="44ca7-175">たとえば、エンティティ デザイナーを使用して、エンティティ モデル データ ウィザードによって生成されるクラスの名前を変更できます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-175">For example, you can use the Entity Designer to change the names of the classes that the Entity Model Data Wizard generates.</span></span> <span data-ttu-id="44ca7-176">ウィザードは、Movies という名前の新しいデータ アクセス クラスを作成しました。</span><span class="sxs-lookup"><span data-stu-id="44ca7-176">The Wizard created a new data access class named Movies.</span></span> <span data-ttu-id="44ca7-177">つまり、ウィザードはクラスにデータベーステーブルとまったく同じ名前を付けたのです。</span><span class="sxs-lookup"><span data-stu-id="44ca7-177">In other words, the Wizard gave the class the very same name as the database table.</span></span> <span data-ttu-id="44ca7-178">このクラスを使用して特定のムービーインスタンスを表すため、クラスの名前を「ムービー」から「ムービー」に変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44ca7-178">Because we will use this class to represent a particular Movie instance, we should rename the class from Movies to Movie.</span></span>

<span data-ttu-id="44ca7-179">エンティティ クラスの名前を変更する場合は、エンティティ デザイナーでクラス名をダブルクリックし、新しい名前を入力します (図 6 参照)。</span><span class="sxs-lookup"><span data-stu-id="44ca7-179">If you want to rename an entity class, you can double-click on the class name in the Entity Designer and enter a new name (see Figure 6).</span></span> <span data-ttu-id="44ca7-180">または、エンティティ デザイナーでエンティティを選択した後で、[プロパティ] ウィンドウでエンティティの名前を変更できます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-180">Alternatively, you can change the name of an entity in the Properties window after selecting an entity in the Entity Designer.</span></span>

<span data-ttu-id="44ca7-181">**図 6 – エンティティ名の変更**</span><span class="sxs-lookup"><span data-stu-id="44ca7-181">**Figure 6 – Changing an entity name**</span></span>

![clip_image012](creating-model-classes-with-the-entity-framework-vb/_static/image6.jpg)

<span data-ttu-id="44ca7-183">変更を行った後、保存ボタン (フロッピー ディスクのアイコン) をクリックして、エンティティ データ モデルを保存することを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="44ca7-183">Remember to save your Entity Data Model after making a modification by clicking the Save button (the icon of the floppy disk).</span></span> <span data-ttu-id="44ca7-184">エンティティ デザイナーは、背後で Visual Basic .NET クラスのセットを生成します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-184">Behind the scenes, the Entity Designer generates a set of Visual Basic .NET classes.</span></span> <span data-ttu-id="44ca7-185">これらのクラスを表示するには、ソリューション エクスプローラー ウィンドウから MoviesDBModel.Designer.vb ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-185">You can view these classes by opening the MoviesDBModel.Designer.vb file from the Solution Explorer window.</span></span>

<span data-ttu-id="44ca7-186">次にエンティティ デザイナーを使用するときに変更が上書きされるため、Designer.vb ファイルのコードは変更しないでください。</span><span class="sxs-lookup"><span data-stu-id="44ca7-186">Don't modify the code in the Designer.vb file since your changes will be overwritten the next time you use the Entity Designer.</span></span> <span data-ttu-id="44ca7-187">Designer.vb ファイルで定義されているエンティティークラスの機能を拡張する場合は、*部分クラス*を別々のファイルに作成できます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-187">If you want to extend the functionality of the entity classes defined in the Designer.vb file then you can create *partial classes* in separate files.</span></span>

#### <a name="selecting-database-records-with-the-entity-framework"></a><span data-ttu-id="44ca7-188">エンティティ フレームワークを使用したデータベース レコードの選択</span><span class="sxs-lookup"><span data-stu-id="44ca7-188">Selecting Database Records with the Entity Framework</span></span>

<span data-ttu-id="44ca7-189">ムービーレコードのリストを表示するページを作成して、ムービーデータベースアプリケーションの構築を開始しましょう。</span><span class="sxs-lookup"><span data-stu-id="44ca7-189">Let's start building our Movie Database application by creating a page that displays a list of movie records.</span></span> <span data-ttu-id="44ca7-190">リスト 1 のホーム コントローラは Index() という名前のアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-190">The Home controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="44ca7-191">Index() アクションは、エンティティ フレームワークを利用して、ムービー データベース テーブルからすべてのムービー レコードを返します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-191">The Index() action returns all of the movie records from the Movie database table by taking advantage of the Entity Framework.</span></span>

<span data-ttu-id="44ca7-192">**リスト 1 - コントローラ\ホームコントローラー.vb**</span><span class="sxs-lookup"><span data-stu-id="44ca7-192">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample1.vb)]

<span data-ttu-id="44ca7-193">リスト 1 のコントローラーにはコンストラクターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="44ca7-193">Notice that the controller in Listing 1 includes a constructor.</span></span> <span data-ttu-id="44ca7-194">コンストラクターは、db というクラス レベルの\_フィールドを初期化します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-194">The constructor initializes a class-level field named \_db.</span></span> <span data-ttu-id="44ca7-195">db\_フィールドは、Microsoft エンティティ フレームワークによって生成されたデータベース エンティティを表します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-195">The \_db field represents the database entities generated by the Microsoft Entity Framework.</span></span> <span data-ttu-id="44ca7-196">\_db フィールドは、エンティティ デザイナーによって生成された MoviesDBEntities クラスのインスタンスです。</span><span class="sxs-lookup"><span data-stu-id="44ca7-196">The \_db field is an instance of the MoviesDBEntities class that was generated by the Entity Designer.</span></span>

<span data-ttu-id="44ca7-197">db\_フィールドは、Movies データベーステーブルからレコードを取得するために、Index() アクション内で使用されます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-197">The \_db field is used within the Index() action to retrieve the records from the Movies database table.</span></span> <span data-ttu-id="44ca7-198">式\_db。ムービーセットは、ムービーデータベーステーブルからのすべてのレコードを表します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-198">The expression \_db.MovieSet represents all of the records from the Movies database table.</span></span> <span data-ttu-id="44ca7-199">ToList() メソッドは、ムービーのセットをムービーオブジェクトの汎用コレクションに変換するために使用されます: リスト(ムービーの)。</span><span class="sxs-lookup"><span data-stu-id="44ca7-199">The ToList() method is used to convert the set of movies into a generic collection of Movie objects: List( Of Movie).</span></span>

<span data-ttu-id="44ca7-200">ムービー レコードは、エンティティへの LINQ の助けを借りて取得されます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-200">The movie records are retrieved with the help of LINQ to Entities.</span></span> <span data-ttu-id="44ca7-201">リスト 1 の Index() アクションでは、LINQ*メソッド構文*を使用してデータベース レコードのセットを取得します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-201">The Index() action in Listing 1 uses LINQ *method syntax* to retrieve the set of database records.</span></span> <span data-ttu-id="44ca7-202">必要に応じて、代わりに LINQ*クエリ構文*を使用できます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-202">If you prefer, you can use LINQ *query syntax* instead.</span></span> <span data-ttu-id="44ca7-203">次の 2 つのステートメントは、まったく同じ処理を行います。</span><span class="sxs-lookup"><span data-stu-id="44ca7-203">The following two statements do the very same thing:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample2.vb)]

<span data-ttu-id="44ca7-204">最も直感的にわかる LINQ 構文 (メソッド構文またはクエリ構文) を使用します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-204">Use whichever LINQ syntax – method syntax or query syntax – that you find most intuitive.</span></span> <span data-ttu-id="44ca7-205">2 つのアプローチの間にパフォーマンスに違いはありません– 唯一の違いはスタイルです。</span><span class="sxs-lookup"><span data-stu-id="44ca7-205">There is no difference in performance between the two approaches – the only difference is style.</span></span>

<span data-ttu-id="44ca7-206">リスト 2 のビューは、ムービーレコードを表示するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-206">The view in Listing 2 is used to display the movie records.</span></span>

<span data-ttu-id="44ca7-207">**リスト 2 - ビュー\ホーム\インデックス.aspx**</span><span class="sxs-lookup"><span data-stu-id="44ca7-207">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample3.aspx)]

<span data-ttu-id="44ca7-208">リスト 2 のビューには **、** 各ムービー レコードを反復処理し、ムービー レコードのタイトルとディレクターのプロパティの値を表示する For Each ループが含まれています。</span><span class="sxs-lookup"><span data-stu-id="44ca7-208">The view in Listing 2 contains a **For Each** loop that iterates through each movie record and displays the values of the movie record's Title and Director properties.</span></span> <span data-ttu-id="44ca7-209">各レコードの横に [編集] と [削除] リンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-209">Notice that an Edit and Delete link is displayed next to each record.</span></span> <span data-ttu-id="44ca7-210">さらに、ビューの下部に [ムービーの追加] リンクが表示されます (図 7 参照)。</span><span class="sxs-lookup"><span data-stu-id="44ca7-210">Furthermore, an Add Movie link appears at the bottom of the view (see Figure 7).</span></span>

<span data-ttu-id="44ca7-211">**図 7 – インデックス ビュー**</span><span class="sxs-lookup"><span data-stu-id="44ca7-211">**Figure 7 – The Index view**</span></span>

![clip_image014](creating-model-classes-with-the-entity-framework-vb/_static/image7.jpg)

<span data-ttu-id="44ca7-213">インデックス ビューは *、型付きビュー*です。</span><span class="sxs-lookup"><span data-stu-id="44ca7-213">The Index view is a *typed view*.</span></span> <span data-ttu-id="44ca7-214">インデックス ビューには、&lt;継承属性を含&gt;む %@ ページ % ディレクティブがあります。</span><span class="sxs-lookup"><span data-stu-id="44ca7-214">The Index view has a &lt;%@ Page %&gt; directive that includes an Inherits attribute.</span></span> <span data-ttu-id="44ca7-215">Inherits 属性は、ムービー オブジェクトの厳密に型指定された一般的なリスト コレクションに ViewData.Model プロパティをキャストするリスト (ムービーの) です。</span><span class="sxs-lookup"><span data-stu-id="44ca7-215">The Inherits attribute casts the ViewData.Model property to a strongly typed generic List collection of Movie objects – a List(Of Movie).</span></span>

## <a name="inserting-database-records-with-the-entity-framework"></a><span data-ttu-id="44ca7-216">エンティティ フレームワークを使用したデータベース レコードの挿入</span><span class="sxs-lookup"><span data-stu-id="44ca7-216">Inserting Database Records with the Entity Framework</span></span>

<span data-ttu-id="44ca7-217">Entity Framework を使用すると、データベース テーブルに新しいレコードを簡単に挿入できます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-217">You can use the Entity Framework to make it easy to insert new records into a database table.</span></span> <span data-ttu-id="44ca7-218">リスト 3 には、ムービー データベース テーブルに新しいレコードを挿入するために使用できるホーム コントローラー クラスに追加された 2 つの新しいアクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="44ca7-218">Listing 3 contains two new actions added to the Home controller class that you can use to insert new records into the Movie database table.</span></span>

<span data-ttu-id="44ca7-219">**リスト 3 - コントローラー\ホームコントローラー.vb (メソッドの追加)**</span><span class="sxs-lookup"><span data-stu-id="44ca7-219">**Listing 3 – Controllers\HomeController.vb (Add methods)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample4.vb)]

<span data-ttu-id="44ca7-220">最初の Add() アクションはビューを返すだけです。</span><span class="sxs-lookup"><span data-stu-id="44ca7-220">The first Add() action simply returns a view.</span></span> <span data-ttu-id="44ca7-221">ビューには、新しいムービー データベース レコードを追加するためのフォームが含まれています (図 8 参照)。</span><span class="sxs-lookup"><span data-stu-id="44ca7-221">The view contains a form for adding a new movie database record (see Figure 8).</span></span> <span data-ttu-id="44ca7-222">フォームを送信すると、2 番目の Add() アクションが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-222">When you submit the form, the second Add() action is invoked.</span></span>

<span data-ttu-id="44ca7-223">2 番目の Add() アクションは AcceptVerbs 属性で修飾されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="44ca7-223">Notice that the second Add() action is decorated with the AcceptVerbs attribute.</span></span> <span data-ttu-id="44ca7-224">このアクションは、HTTP POST 操作を実行する場合にのみ呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-224">This action can be invoked only when performing an HTTP POST operation.</span></span> <span data-ttu-id="44ca7-225">つまり、このアクションは HTML フォームを投稿するときにのみ呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-225">In other words, this action can only be invoked when posting an HTML form.</span></span>

<span data-ttu-id="44ca7-226">2 番目の Add() アクションは、ASP.NET MVC TryUpdateModel() メソッドの助けを借りて、エンティティ フレームワーク ムービー クラスの新しいインスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-226">The second Add() action creates a new instance of the Entity Framework Movie class with the help of the ASP.NET MVC TryUpdateModel() method.</span></span> <span data-ttu-id="44ca7-227">メソッドは、Add() メソッドに渡された FormCollection 内のフィールドを受け取り、これらの HTML フォームフィールドの値をムービークラスに割り当てます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-227">The TryUpdateModel() method takes the fields in the FormCollection passed to the Add() method and assigns the values of these HTML form fields to the Movie class.</span></span>

<span data-ttu-id="44ca7-228">エンティティ フレームワークを使用する場合は、TryUpdateModel または UpdateModel メソッドを使用してエンティティ クラスのプロパティを更新するときに、プロパティの "ホワイト リスト" を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44ca7-228">When using the Entity Framework, you must supply a "white list" of properties when using the TryUpdateModel or UpdateModel methods to update the properties of an entity class.</span></span>

<span data-ttu-id="44ca7-229">次に、Add() アクションは、いくつかの簡単なフォーム検証を実行します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-229">Next, the Add() action performs some simple form validation.</span></span> <span data-ttu-id="44ca7-230">このアクションは、タイトルとディレクターの両方のプロパティに値があることを確認します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-230">The action verifies that both the Title and Director properties have values.</span></span> <span data-ttu-id="44ca7-231">検証エラーがある場合は、検証エラー メッセージが ModelState に追加されます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-231">If there is a validation error, then a validation error message is added to ModelState.</span></span>

<span data-ttu-id="44ca7-232">検証エラーがない場合は、Entity Framework の助けを借りて、新しいムービー レコードが Movies データベース テーブルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-232">If there are no validation errors then a new movie record is added to the Movies database table with the help of the Entity Framework.</span></span> <span data-ttu-id="44ca7-233">新しいレコードは、次の 2 行のコードでデータベースに追加されます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-233">The new record is added to the database with the following two lines of code:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample5.vb)]

<span data-ttu-id="44ca7-234">コードの最初の行は、エンティティ フレームワークによって追跡されているムービーのセットに新しいムービー エンティティを追加します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-234">The first line of code adds the new Movie entity to the set of movies being tracked by the Entity Framework.</span></span> <span data-ttu-id="44ca7-235">2 行目のコードは、追跡対象の Movies に対して行われた変更を、基になるデータベースに保存します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-235">The second line of code saves whatever changes have been made to the Movies being tracked back to the underlying database.</span></span>

<span data-ttu-id="44ca7-236">**図 8 – [追加] ビュー**</span><span class="sxs-lookup"><span data-stu-id="44ca7-236">**Figure 8 – The Add view**</span></span>

![clip_image016](creating-model-classes-with-the-entity-framework-vb/_static/image8.jpg)

## <a name="updating-database-records-with-the-entity-framework"></a><span data-ttu-id="44ca7-238">エンティティ フレームワークを使用したデータベース レコードの更新</span><span class="sxs-lookup"><span data-stu-id="44ca7-238">Updating Database Records with the Entity Framework</span></span>

<span data-ttu-id="44ca7-239">新しいデータベース レコードを挿入する方法として、Entity Framework でデータベース レコードを編集するのとほぼ同じアプローチに従うことができます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-239">You can follow almost the same approach to edit a database record with the Entity Framework as the approach that we just followed to insert a new database record.</span></span> <span data-ttu-id="44ca7-240">リスト 4 には、Edit() という名前の 2 つの新しいコントローラ アクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="44ca7-240">Listing 4 contains two new controller actions named Edit().</span></span> <span data-ttu-id="44ca7-241">最初の Edit() アクションは、ムービーレコードを編集するための HTML フォームを返します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-241">The first Edit() action returns an HTML form for editing a movie record.</span></span> <span data-ttu-id="44ca7-242">2 番目の Edit() アクションは、データベースの更新を試みます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-242">The second Edit() action attempts to update the database.</span></span>

<span data-ttu-id="44ca7-243">**リスト 4 - コントローラー\ホームコントローラー.vb (メソッドの編集)**</span><span class="sxs-lookup"><span data-stu-id="44ca7-243">**Listing 4 – Controllers\HomeController.vb (Edit methods)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample6.vb)]

<span data-ttu-id="44ca7-244">2 番目の Edit() アクションは、編集中のムービーの ID に一致するデータベースからムービーレコードを取得することから始まります。</span><span class="sxs-lookup"><span data-stu-id="44ca7-244">The second Edit() action starts by retrieving the Movie record from the database that matches the Id of the movie being edited.</span></span> <span data-ttu-id="44ca7-245">次の LINQ to Entities ステートメントは、特定の ID に一致する最初のデータベース レコードを取得します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-245">The following LINQ to Entities statement grabs the first database record that matches a particular Id:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample7.vb)]

<span data-ttu-id="44ca7-246">次に、TryUpdateModel() メソッドを使用して、HTML フォーム フィールドの値をムービー エンティティのプロパティに割り当てます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-246">Next, the TryUpdateModel() method is used to assign the values of the HTML form fields to the properties of the movie entity.</span></span> <span data-ttu-id="44ca7-247">更新する正確なプロパティを指定するホワイト リストが提供されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="44ca7-247">Notice that a white list is supplied to specify the exact properties to update.</span></span>

<span data-ttu-id="44ca7-248">次に、ムービータイトルとディレクターの両方のプロパティに値が設定されていることを確認するために、いくつかの簡単な検証が実行されます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-248">Next, some simple validation is performed to verify that both the Movie Title and Director properties have values.</span></span> <span data-ttu-id="44ca7-249">いずれかのプロパティに値がない場合は、検証エラー メッセージが ModelState および ModelState.IsValid に追加され、値が false を返します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-249">If either property is missing a value, then a validation error message is added to ModelState and ModelState.IsValid returns the value false.</span></span>

<span data-ttu-id="44ca7-250">検証エラーがない場合は、SaveChanges() メソッドを呼び出すことによって、基になる Movies データベース テーブルが変更によって更新されます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-250">Finally, if there are no validation errors, then the underlying Movies database table is updated with any changes by calling the SaveChanges() method.</span></span>

<span data-ttu-id="44ca7-251">データベース レコードを編集する場合は、編集中のレコードの ID を、データベースの更新を実行するコントローラー アクションに渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="44ca7-251">When editing database records, you need to pass the Id of the record being edited to the controller action that performs the database update.</span></span> <span data-ttu-id="44ca7-252">それ以外の場合、コントローラー アクションは、基になるデータベースで更新するレコードを認識しません。</span><span class="sxs-lookup"><span data-stu-id="44ca7-252">Otherwise, the controller action will not know which record to update in the underlying database.</span></span> <span data-ttu-id="44ca7-253">リスト 5 に含まれる編集ビューには、編集中のデータベース レコードの ID を表す非表示フォーム フィールドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="44ca7-253">The Edit view, contained in Listing 5, includes a hidden form field that represents the Id of the database record being edited.</span></span>

<span data-ttu-id="44ca7-254">**リスト 5 - ビュー\ホーム\編集.aspx**</span><span class="sxs-lookup"><span data-stu-id="44ca7-254">**Listing 5 – Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a><span data-ttu-id="44ca7-255">エンティティ フレームワークを使用したデータベース レコードの削除</span><span class="sxs-lookup"><span data-stu-id="44ca7-255">Deleting Database Records with the Entity Framework</span></span>

<span data-ttu-id="44ca7-256">このチュートリアルで取り組む必要がある最終的なデータベース操作は、データベースレコードを削除することです。</span><span class="sxs-lookup"><span data-stu-id="44ca7-256">The final database operation, which we need to tackle in this tutorial, is deleting database records.</span></span> <span data-ttu-id="44ca7-257">リスト 6 のコントローラー アクションを使用して、特定のデータベース レコードを削除できます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-257">You can use the controller action in Listing 6 to delete a particular database record.</span></span>

<span data-ttu-id="44ca7-258">**リスト 6 -- \コントローラー\ホームコントローラー.vb (削除アクション)**</span><span class="sxs-lookup"><span data-stu-id="44ca7-258">**Listing 6 -- \Controllers\HomeController.vb (Delete action)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample9.vb)]

<span data-ttu-id="44ca7-259">Delete() アクションは、最初にアクションに渡された ID に一致するムービーエンティティを取得します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-259">The Delete() action first retrieves the Movie entity that matches the Id passed to the action.</span></span> <span data-ttu-id="44ca7-260">次に、ムービーは DeleteObject() メソッドを呼び出した後に SaveChanges() メソッドを呼び出してデータベースから削除されます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-260">Next, the movie is deleted from the database by calling the DeleteObject() method followed by the SaveChanges() method.</span></span> <span data-ttu-id="44ca7-261">最後に、ユーザーはインデックス ビューにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="44ca7-261">Finally, the user is redirected back to the Index view.</span></span>

## <a name="summary"></a><span data-ttu-id="44ca7-262">まとめ</span><span class="sxs-lookup"><span data-stu-id="44ca7-262">Summary</span></span>

<span data-ttu-id="44ca7-263">このチュートリアルの目的は、MVC と Microsoft エンティティ フレームワークASP.NETを利用して、データベース駆動型の web アプリケーションを構築する方法を示すことでした。</span><span class="sxs-lookup"><span data-stu-id="44ca7-263">The purpose of this tutorial was to demonstrate how you can build database-driven web applications by taking advantage of ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="44ca7-264">データベース レコードの選択、挿入、更新、および削除を可能にするアプリケーションの構築方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="44ca7-264">You learned how to build an application that enables you to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="44ca7-265">最初に、エンティティ データ モデル ウィザードを使用して、Visual Studio 内からエンティティ データ モデルを生成する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="44ca7-265">First, we discussed how you can use the Entity Data Model Wizard to generate an Entity Data Model from within Visual Studio.</span></span> <span data-ttu-id="44ca7-266">次に、LINQ to Entities を使用してデータベース テーブルからデータベース レコードのセットを取得する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="44ca7-266">Next, you learn how to use LINQ to Entities to retrieve a set of database records from a database table.</span></span> <span data-ttu-id="44ca7-267">最後に、Entity Framework を使用してデータベース レコードの挿入、更新、および削除を行いました。</span><span class="sxs-lookup"><span data-stu-id="44ca7-267">Finally, we used the Entity Framework to insert, update, and delete database records.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="44ca7-268">[前へ](validation-with-the-data-annotation-validators-cs.md)
> [次へ](creating-model-classes-with-linq-to-sql-vb.md)</span><span class="sxs-lookup"><span data-stu-id="44ca7-268">[Previous](validation-with-the-data-annotation-validators-cs.md)
[Next](creating-model-classes-with-linq-to-sql-vb.md)</span></span>
