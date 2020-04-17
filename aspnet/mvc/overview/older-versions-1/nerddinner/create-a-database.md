---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: データベースの作成 | Microsoft Docs
author: rick-anderson
description: 手順 2 は、NerdDinner アプリケーションのすべてのディナーと RSVP データを保持するデータベースを作成する手順を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541612"
---
# <a name="create-a-database"></a><span data-ttu-id="fdd15-103">データベースの作成</span><span class="sxs-lookup"><span data-stu-id="fdd15-103">Create a Database</span></span>

<span data-ttu-id="fdd15-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fdd15-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="fdd15-105">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="fdd15-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="fdd15-106">これは、mvc 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NETの手順 2 です。</span><span class="sxs-lookup"><span data-stu-id="fdd15-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="fdd15-107">手順 2 は、NerdDinner アプリケーションのすべてのディナーと RSVP データを保持するデータベースを作成する手順を示します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="fdd15-108">mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="fdd15-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="fdd15-109">NerdDinner ステップ 2: データベースの作成</span><span class="sxs-lookup"><span data-stu-id="fdd15-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="fdd15-110">私たちのNerdDinnerアプリケーションのすべてのディナーとRSVPデータを保存するためにデータベースを使用します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="fdd15-111">以下の手順では、無料の SQL Server Express エディションを使用してデータベースを作成する方法を示します ([これは、マイクロソフト Web プラットフォーム インストーラ](https://www.microsoft.com/web/downloads/platform.aspx)の V2 を使用して簡単にインストールできます ) 。</span><span class="sxs-lookup"><span data-stu-id="fdd15-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="fdd15-112">このコードを記述する場合は、すべて SQL Server Express と完全な SQL Server の両方で動作します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="fdd15-113">新しい SQL Server エクスプレス データベースの作成</span><span class="sxs-lookup"><span data-stu-id="fdd15-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="fdd15-114">まず、Web プロジェクトを右クリックし、[**&gt;新しい項目の追加**] メニュー コマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="fdd15-115">これにより、Visual Studio の [新しい項目の追加] ダイアログ が表示されます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="fdd15-116">"データ" カテゴリでフィルター処理し、"SQL Server データベース" 項目テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="fdd15-117">"NerdDinner.mdf" を作成する SQL Server エクスプレス データベースに名前を付け、ヒット OK を付けます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="fdd15-118">Visual Studio は、このファイルを \App\_Data ディレクトリ (既に読み取りと書き込みの両方のセキュリティ ACL を使用してセットアップされているディレクトリ) に追加するかどうか尋ねます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="fdd15-119">"はい" をクリックすると、新しいデータベースが作成され、ソリューション エクスプローラーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="fdd15-120">データベース内でのテーブルの作成</span><span class="sxs-lookup"><span data-stu-id="fdd15-120">Creating Tables within our Database</span></span>

<span data-ttu-id="fdd15-121">これで、新しい空のデータベースが作成されました。</span><span class="sxs-lookup"><span data-stu-id="fdd15-121">We now have a new empty database.</span></span> <span data-ttu-id="fdd15-122">それにいくつかのテーブルを追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="fdd15-122">Let's add some tables to it.</span></span>

<span data-ttu-id="fdd15-123">そのためには、Visual Studio 内の [サーバー エクスプローラ] タブ ウィンドウに移動します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="fdd15-124">アプリケーションの \App\_データ フォルダーに格納されている SQL Server Express データベースは、サーバー エクスプ ローラー内に自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="fdd15-125">オプションで、[サーバー エクスプローラ] ウィンドウの上部にある [データベースに接続] アイコンを使用して、SQL Server データベース (ローカルとリモートの両方) をリストに追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="fdd15-126">私たちは、私たちのNerdDinnerデータベースに2つのテーブルを追加します - 1つは私たちのディナーを保存し、もう1つはそれらにRSVPの受け入れを追跡します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="fdd15-127">データベース内の 「Tables」 フォルダーを右クリックし、「新しいテーブルの追加」メニューコマンドを選択することで、新しいテーブルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="fdd15-128">これにより、テーブルのスキーマを構成できるテーブル デザイナーが開きます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="fdd15-129">"Dinners" テーブルでは、10 列のデータを追加します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="fdd15-130">"DinnerID" 列をテーブルの一意の主キーにします。</span><span class="sxs-lookup"><span data-stu-id="fdd15-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="fdd15-131">この設定は、[DinnerID] 列を右クリックし、[主キーの設定] メニュー項目を選択することで行うことができます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="fdd15-132">DinnerID を主キーにすることに加えて、新しいデータ行がテーブルに追加されると値が自動的にインクリメントされる「ID」列として設定します (つまり、最初に挿入された Dinner 行は DinnerID が 1、2 番目に挿入された行は DinnerID が 2 になります)。</span><span class="sxs-lookup"><span data-stu-id="fdd15-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="fdd15-133">"DinnerID" 列を選択し、"列のプロパティ" エディターを使用して、列の "(Is Identity)" プロパティを "はい" に設定することでこれを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="fdd15-134">標準 ID のデフォルトを使用します (1 から始まり、新しい Dinner 行ごとに 1 ずつ増やします)。</span><span class="sxs-lookup"><span data-stu-id="fdd15-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="fdd15-135">次に、Ctrl-S を押すか、**ファイル-&gt;保存**メニューコマンドを使用して、テーブルを保存します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="fdd15-136">これにより、テーブルに名前を付けるプロンプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-136">This will prompt us to name the table.</span></span> <span data-ttu-id="fdd15-137">私たちはそれを「ディナー」と名前を付けます:</span><span class="sxs-lookup"><span data-stu-id="fdd15-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="fdd15-138">新しい Dinners テーブルは、サーバー エクスプローラのデータベース内に表示されます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="fdd15-139">次に、上記の手順を繰り返して"RSVP"テーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="fdd15-140">このテーブルには 3 つの列があります。</span><span class="sxs-lookup"><span data-stu-id="fdd15-140">This table with have 3 columns.</span></span> <span data-ttu-id="fdd15-141">RsvpID 列を主キーとして設定し、ID 列にします。</span><span class="sxs-lookup"><span data-stu-id="fdd15-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="fdd15-142">私たちはそれを保存し、名前"RSVP"を与えます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="fdd15-143">テーブル間の外部キーリレーションシップの設定</span><span class="sxs-lookup"><span data-stu-id="fdd15-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="fdd15-144">これで、データベース内に 2 つのテーブルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="fdd15-144">We now have two tables within our database.</span></span> <span data-ttu-id="fdd15-145">最後のスキーマ設計手順は、これら 2 つのテーブル間に "一対多" のリレーションシップを設定することです。</span><span class="sxs-lookup"><span data-stu-id="fdd15-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="fdd15-146">RSVP テーブルの "DinnerID" 列を構成して、"Dinners" テーブルの "DinnerID" 列と外部キーのリレーションシップを持つ場合に、これを行います。</span><span class="sxs-lookup"><span data-stu-id="fdd15-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="fdd15-147">これを行うには、サーバー エクスプローラで RSVP テーブルをダブルクリックして、テーブル デザイナ内で開きます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="fdd15-148">その中の "DinnerID" 列を選択し、右クリックして [リレーションシップ]5S を選択します。コンテキスト メニュー コマンド:</span><span class="sxs-lookup"><span data-stu-id="fdd15-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="fdd15-149">これにより、テーブル間のリレーションシップを設定するために使用できるダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="fdd15-150">[追加] ボタンをクリックして、ダイアログに新しいリレーションシップを追加します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="fdd15-151">リレーションシップを追加したら、ダイアログボックスの右側にあるプロパティグリッド内のツリービューノード「テーブルと列の仕様」を展開し、"."ボタンは右に表示されます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="fdd15-152">「.」をクリックします。ボタンを押すと、リレーションシップに関係するテーブルと列を指定したり、リレーションシップに名前を付けることができるようにする別のダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="fdd15-153">主キー テーブルを "ディナー" に変更し、ディナー テーブル内の "DinnerID" 列を主キーとして選択します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="fdd15-154">RSVP テーブルは、外部キー テーブルと RSVP になります。DinnerID 列は、外部キーとして関連付けられます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="fdd15-155">これで、RSVP テーブルの各行が Dinner テーブルの行に関連付けられます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="fdd15-156">SQL Server は参照整合性を維持し、有効な Dinner 行を指さない場合は新しい RSVP 行を追加できないようにします。</span><span class="sxs-lookup"><span data-stu-id="fdd15-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="fdd15-157">また、まだそれを参照している RSVP 行がある場合、Dinner 行を削除することもできなくなります。</span><span class="sxs-lookup"><span data-stu-id="fdd15-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="fdd15-158">テーブルへのデータの追加</span><span class="sxs-lookup"><span data-stu-id="fdd15-158">Adding Data to our Tables</span></span>

<span data-ttu-id="fdd15-159">Dinners テーブルにサンプル データを追加して、最後に終了します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="fdd15-160">サーバー エクスプローラでテーブルを右クリックし、[テーブル データの表示] コマンドを選択して、テーブルにデータを追加できます。</span><span class="sxs-lookup"><span data-stu-id="fdd15-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="fdd15-161">アプリケーションの実装を開始する際に、後で使用できる Dinner データの数行を追加します。</span><span class="sxs-lookup"><span data-stu-id="fdd15-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="fdd15-162">次の手順</span><span class="sxs-lookup"><span data-stu-id="fdd15-162">Next Step</span></span>

<span data-ttu-id="fdd15-163">データベースの作成が完了しました。</span><span class="sxs-lookup"><span data-stu-id="fdd15-163">We've finished creating our database.</span></span> <span data-ttu-id="fdd15-164">ここで、クエリと更新に使用できるモデル クラスを作成しましょう。</span><span class="sxs-lookup"><span data-stu-id="fdd15-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fdd15-165">[前へ](create-a-new-aspnet-mvc-project.md)
> [次へ](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="fdd15-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
