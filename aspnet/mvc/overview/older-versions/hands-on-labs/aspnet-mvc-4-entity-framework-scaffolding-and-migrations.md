---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework スキャフォールディングと移行 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 コント ローラーのメソッドに慣れてまたは、完了したかどうか、&quot;ヘルパー、フォーム、検証&quot;ハンズオン ラボは、注意する必要が.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 2b26224390af70e19ca0593abe93a6867140f8ab
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65129723"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a><span data-ttu-id="f85c8-103">ASP.NET MVC 4 Entity Framework スキャフォールディングと移行</span><span class="sxs-lookup"><span data-stu-id="f85c8-103">ASP.NET MVC 4 Entity Framework Scaffolding and Migrations</span></span>

<span data-ttu-id="f85c8-104">によって[Web キャンプ チーム](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="f85c8-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="f85c8-105">Web のキャンプ トレーニング キットをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="f85c8-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="f85c8-106">ASP.NET MVC 4 コント ローラーのメソッドに慣れてまたは、完了したかどうか、&quot;ヘルパー、フォーム、検証&quot;ハンズオン ラボは、注意すべきことを作成するためのロジックの多くを更新、一覧表示およびこれが繰り返される任意のデータ エンティティの削除間でのアプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="f85c8-106">If you are familiar with ASP.NET MVC 4 controller methods, or have completed the &quot;Helpers, Forms and Validation&quot; Hands-On lab, you should be aware that many of the logic to create, update, list and remove any data entity it is repeated among the application.</span></span> <span data-ttu-id="f85c8-107">モデルにいくつかのクラスを操作する場合はもちろんのことを各エンティティ操作だけでなく各ビューの POST および GET アクション メソッドの記述、かなりの時間を費やす可能性ができます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-107">Not to mention that, if your model has several classes to manipulate, you will be likely to spend a considerable time writing the POST and GET action methods for each entity operation, as well as each of the views.</span></span>

<span data-ttu-id="f85c8-108">このラボでは、ASP.NET MVC 4 のスキャフォールディングを使用して、アプリケーションの CRUD (作成、読み取り、更新、削除) のベースラインを自動的に生成する方法を学びます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-108">In this lab you will learn how to use the ASP.NET MVC 4 scaffolding to automatically generate the baseline of your application's CRUD (Create, Read, Update and Delete).</span></span> <span data-ttu-id="f85c8-109">以降は、単純なモデル クラス、および、1 行のコードを記述することがなく、すべての CRUD 操作だけでなく、すべての必要なビューを含むコント ローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-109">Starting from a simple model class, and, without writing a single line of code, you will create a controller that will contain all the CRUD operations, as well as the all the necessary views.</span></span> <span data-ttu-id="f85c8-110">構築し、単純なソリューションを実行すると、生成されると、MVC のロジックとデータ操作にビューと共に、アプリケーション データベースがあります。</span><span class="sxs-lookup"><span data-stu-id="f85c8-110">After building and running the simple solution, you will have the application database generated, together with the MVC logic and views for data manipulation.</span></span>

<span data-ttu-id="f85c8-111">さらに、Entity Framework の移行を使用して、アプリケーション全体のモデルの更新プログラムを実行するがいかに簡単かを学習します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-111">In addition, you will learn how easy it is to use Entity Framework Migrations to perform model updates throughout your entire application.</span></span> <span data-ttu-id="f85c8-112">Entity Framework の移行を使用すると、簡単な手順で、モデルが変更された後に、データベースを変更できます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-112">Entity Framework Migrations will let you modify your database after the model has changed with simple steps.</span></span> <span data-ttu-id="f85c8-113">これらすべての点で、できなくをビルドして、web アプリケーションをより効率的に管理する ASP.NET MVC 4 の最新の機能を活用します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-113">With all these in mind, you will be able to build and maintain web applications more efficiently, taking advantage of the latest features of ASP.NET MVC 4.</span></span>

> [!NOTE]
> <span data-ttu-id="f85c8-114">すべてのサンプル コードとスニペットがで使用可能な Web キャンプ トレーニング キットに含まれている[Microsoft の Web/WebCampTrainingKit リリース](https://aka.ms/webcamps-training-kit)します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="f85c8-115">このラボに固有のプロジェクトは、「 [ASP.NET MVC 4 Entity Framework スキャフォールディングと移行](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-115">The project specific to this lab is available at [ASP.NET MVC 4 Entity Framework Scaffolding and Migrations](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="f85c8-116">目的</span><span class="sxs-lookup"><span data-stu-id="f85c8-116">Objectives</span></span>

<span data-ttu-id="f85c8-117">このハンズオン ラボでは、学習する方法。</span><span class="sxs-lookup"><span data-stu-id="f85c8-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="f85c8-118">コント ローラーでの CRUD 操作には、ASP.NET のスキャフォールディングを使用します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-118">Use ASP.NET scaffolding for CRUD operations in controllers.</span></span>
- <span data-ttu-id="f85c8-119">Entity Framework の移行を使用して、データベース モデルを変更します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-119">Change the database model using Entity Framework Migrations.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="f85c8-120">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="f85c8-120">Prerequisites</span></span>

<span data-ttu-id="f85c8-121">このラボを完成させるのには、次の項目が必要です。</span><span class="sxs-lookup"><span data-stu-id="f85c8-121">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="f85c8-122">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)または上位 (読み取り[付録 A](#AppendixA)をインストールする方法について)。</span><span class="sxs-lookup"><span data-stu-id="f85c8-122">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="f85c8-123">セットアップ</span><span class="sxs-lookup"><span data-stu-id="f85c8-123">Setup</span></span>

<span data-ttu-id="f85c8-124">**コード スニペットをインストールします。**</span><span class="sxs-lookup"><span data-stu-id="f85c8-124">**Installing Code Snippets**</span></span>

<span data-ttu-id="f85c8-125">便宜上、このラボに管理するコードの多くは、Visual Studio コード スニペットとして利用できます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-125">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="f85c8-126">実行コード スニペットをインストールする **.\Source\Setup\CodeSnippets.vsi**ファイル。</span><span class="sxs-lookup"><span data-stu-id="f85c8-126">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="f85c8-127">このドキュメントの付録を参照することができます、Visual Studio のコード スニペットとその使用方法を学習するに慣れていない場合&quot;[付録 b:コード スニペットを使用して](#AppendixB)&quot;します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-127">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="f85c8-128">演習</span><span class="sxs-lookup"><span data-stu-id="f85c8-128">Exercises</span></span>

<span data-ttu-id="f85c8-129">次の演習では、このハンズオン ラボを構成します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-129">The following exercise make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="f85c8-130">Entity Framework の移行と ASP.NET MVC 4 のスキャフォールディングを使用します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-130">Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>](#Exercise1)

> [!NOTE]
> <span data-ttu-id="f85c8-131">この演習が用意されており、**エンド**演習を完了した後に取得する必要があります、結果として得られるソリューションに含まれているフォルダー。</span><span class="sxs-lookup"><span data-stu-id="f85c8-131">This exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercise.</span></span> <span data-ttu-id="f85c8-132">演習を通して追加のヘルプが必要な場合は、このソリューションをガイドとして使用できます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-132">You can use this solution as a guide if you need additional help working through the exercise.</span></span>

<span data-ttu-id="f85c8-133">この演習の所要時間を推定するには。**30 分**</span><span class="sxs-lookup"><span data-stu-id="f85c8-133">Estimated time to complete this lab: **30 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a><span data-ttu-id="f85c8-134">演習 1:Entity Framework の移行と ASP.NET MVC 4 のスキャフォールディングを使用します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-134">Exercise 1: Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>

<span data-ttu-id="f85c8-135">ASP.NET MVC のスキャフォールディングにより、アプリケーションで、データベース層と対話するために必要なロジックを作成する、標準化された方法で CRUD 操作を生成する簡単な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-135">ASP.NET MVC scaffolding provides a quick way to generate the CRUD operations in a standardized way, creating the necessary logic that lets your application interact with the database layer.</span></span>

<span data-ttu-id="f85c8-136">この演習では、CRUD メソッドを作成する最初のコードを ASP.NET MVC 4 のスキャフォールディングを使用する方法を学びます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-136">In this exercise, you will learn how to use ASP.NET MVC 4 scaffolding with code first to create the CRUD methods.</span></span> <span data-ttu-id="f85c8-137">次に、Entity Framework の移行を使用してデータベースの変更を適用してモデルを更新する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-137">Then, you will learn how to update your model applying the changes in the database by using Entity Framework Migrations.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a><span data-ttu-id="f85c8-138">タスク 1-作成する新しい ASP.NET MVC 4 プロジェクトのスキャフォールディングを使用</span><span class="sxs-lookup"><span data-stu-id="f85c8-138">Task 1- Creating a new ASP.NET MVC 4 project using Scaffolding</span></span>

1. <span data-ttu-id="f85c8-139">既に開かれていない場合は開始**Visual Studio 2012**します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-139">If not already open, start **Visual Studio 2012**.</span></span>
2. <span data-ttu-id="f85c8-140">選択**ファイル |新しいプロジェクト**します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-140">Select **File | New Project**.</span></span> <span data-ttu-id="f85c8-141">[プロジェクト] ダイアログ、new、 **(Visual C#) |Web**セクションで、 **ASP.NET MVC 4 Web アプリケーション**します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-141">In the New Project dialog, under the **Visual C# | Web** section, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="f85c8-142">プロジェクトに名前を**MVC4andEFMigrations**に場所を設定および**Source\Ex1 UsingMVC4ScaffoldingEFMigrations**このラボのフォルダー。</span><span class="sxs-lookup"><span data-stu-id="f85c8-142">Name the project to **MVC4andEFMigrations** and set the location to **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** folder of this lab.</span></span> <span data-ttu-id="f85c8-143">設定、**ソリューション名**に**開始**を確認して**ソリューションのディレクトリを作成**がチェックされます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-143">Set the **Solution name** to **Begin** and ensure **Create directory for solution** is checked.</span></span> <span data-ttu-id="f85c8-144">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f85c8-144">Click **OK**.</span></span>

    <span data-ttu-id="f85c8-145">![新しい ASP.NET MVC 4 プロジェクト ダイアログ ボックス](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "新しい ASP.NET MVC 4 プロジェクト ダイアログ ボックス")</span><span class="sxs-lookup"><span data-stu-id="f85c8-145">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="f85c8-146">*新しい ASP.NET MVC 4 プロジェクト ダイアログ ボックス*</span><span class="sxs-lookup"><span data-stu-id="f85c8-146">*New ASP.NET MVC 4 Project Dialog Box*</span></span>
3. <span data-ttu-id="f85c8-147">**新しい ASP.NET MVC 4 プロジェクト**ダイアログ ボックスの 、**インターネット アプリケーション**テンプレート、ことを確認および**Razor**が、選択されている**ビュー エンジン**.</span><span class="sxs-lookup"><span data-stu-id="f85c8-147">In the **New ASP.NET MVC 4 Project** dialog box select the **Internet Application** template, and make sure that **Razor** is the selected **View engine**.</span></span> <span data-ttu-id="f85c8-148">**[OK]** をクリックして、プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-148">Click **OK** to create the project.</span></span>

    <span data-ttu-id="f85c8-149">![新しい ASP.NET MVC 4 のインターネット アプリケーション](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "新しい ASP.NET MVC 4 のインターネット アプリケーション")</span><span class="sxs-lookup"><span data-stu-id="f85c8-149">![New ASP.NET MVC 4 Internet Application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "New ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="f85c8-150">*新しい ASP.NET MVC 4 のインターネット アプリケーション*</span><span class="sxs-lookup"><span data-stu-id="f85c8-150">*New ASP.NET MVC 4 Internet Application*</span></span>
4. <span data-ttu-id="f85c8-151">ソリューション エクスプ ローラーで右クリックして**モデル**選択**追加 |クラス**単純なクラス person (POCO) を作成します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-151">In the Solution Explorer, right-click **Models** and select **Add | Class** to create a simple class person (POCO).</span></span> <span data-ttu-id="f85c8-152">名前を付けます**人** をクリック**OK**します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-152">Name it **Person** and click **OK**.</span></span>
5. <span data-ttu-id="f85c8-153">Person クラスを開き、次のプロパティを挿入します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-153">Open the Person class and insert the following properties.</span></span>

    <span data-ttu-id="f85c8-154">(コード スニペット - *ASP.NET MVC 4 と Entity Framework の移行 - Ex1 Person プロパティ*)</span><span class="sxs-lookup"><span data-stu-id="f85c8-154">(Code Snippet - *ASP.NET MVC 4 and Entity Framework Migrations - Ex1 Person Properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. <span data-ttu-id="f85c8-155">クリックして**ビルド |ソリューションをビルド**変更を保存し、プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="f85c8-155">Click **Build | Build Solution** to save the changes and build the project.</span></span>

    <span data-ttu-id="f85c8-156">![アプリケーションのビルド](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "アプリケーションを構築します。")</span><span class="sxs-lookup"><span data-stu-id="f85c8-156">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Building the application")</span></span>

    <span data-ttu-id="f85c8-157">*アプリケーションのビルド*</span><span class="sxs-lookup"><span data-stu-id="f85c8-157">*Building the Application*</span></span>
7. <span data-ttu-id="f85c8-158">ソリューション エクスプ ローラーでは、controllers フォルダーを右クリックして**追加 |コント ローラー**します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-158">In the Solution Explorer, right-click the controllers folder and select **Add | Controller**.</span></span>
8. <span data-ttu-id="f85c8-159">コント ローラーに名前*PersonController*を完了して、**スキャフォールディングのオプション**次の値。</span><span class="sxs-lookup"><span data-stu-id="f85c8-159">Name the controller *PersonController* and complete the **Scaffolding options** with the following values.</span></span>

   1. <span data-ttu-id="f85c8-160">**テンプレート**ドロップダウン リストで、**読み取り/書き込みアクションと Entity Framework を使用して、ビューがある MVC コント ローラー**オプション。</span><span class="sxs-lookup"><span data-stu-id="f85c8-160">In the **Template** drop-down list, select the **MVC controller with read/write actions and views, using Entity Framework** option.</span></span>
   2. <span data-ttu-id="f85c8-161">**モデル クラス**ドロップダウン リストで、 **Person**クラス。</span><span class="sxs-lookup"><span data-stu-id="f85c8-161">In the **Model class** drop-down list, select the **Person** class.</span></span>
   3. <span data-ttu-id="f85c8-162">**データ コンテキスト クラス**一覧で、 **&lt;新しいデータ コンテキスト.&gt;**.</span><span class="sxs-lookup"><span data-stu-id="f85c8-162">In the **Data Context class** list, select **&lt;New data context...&gt;**.</span></span> <span data-ttu-id="f85c8-163">任意の名前を選択し、クリックして**OK**します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-163">Choose any name and click **OK**.</span></span>
   4. <span data-ttu-id="f85c8-164">**ビュー**ドロップダウン リストで、ことを確認します**Razor**が選択されています。</span><span class="sxs-lookup"><span data-stu-id="f85c8-164">In the **Views** drop-down list, make sure that **Razor** is selected.</span></span>

      <span data-ttu-id="f85c8-165">![スキャフォールディングと Person のコント ローラーを追加する](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "スキャフォールディングと Person のコント ローラーを追加します。")</span><span class="sxs-lookup"><span data-stu-id="f85c8-165">![Adding the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Adding the Person controller with scaffolding")</span></span>

      <span data-ttu-id="f85c8-166">*スキャフォールディングと Person のコント ローラーを追加します。*</span><span class="sxs-lookup"><span data-stu-id="f85c8-166">*Adding the Person controller with scaffolding*</span></span>
9. <span data-ttu-id="f85c8-167">クリックして**追加**スキャフォールディングとユーザーを新しいコント ローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-167">Click **Add** to create the new controller for Person with scaffolding.</span></span> <span data-ttu-id="f85c8-168">コント ローラー アクションとビューを生成したようになりました。</span><span class="sxs-lookup"><span data-stu-id="f85c8-168">You have now generated the controller actions as well as the views.</span></span>

    <span data-ttu-id="f85c8-169">![Person コント ローラーをスキャフォールディングを作成したら](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "Person コント ローラーをスキャフォールディングで作成した後")</span><span class="sxs-lookup"><span data-stu-id="f85c8-169">![After creating the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "After creating the Person controller with scaffolding")</span></span>

    <span data-ttu-id="f85c8-170">*Person コント ローラーをスキャフォールディングで作成した後*</span><span class="sxs-lookup"><span data-stu-id="f85c8-170">*After creating the Person controller with scaffolding*</span></span>
10. <span data-ttu-id="f85c8-171">開いている**PersonController**クラス。</span><span class="sxs-lookup"><span data-stu-id="f85c8-171">Open **PersonController** class.</span></span> <span data-ttu-id="f85c8-172">完全な CRUD アクション メソッドが自動的に生成されたことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f85c8-172">Notice that the full CRUD action methods have been generated automatically.</span></span>

   <span data-ttu-id="f85c8-173">![Person コント ローラーの内部](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "内で、Person のコント ローラー")</span><span class="sxs-lookup"><span data-stu-id="f85c8-173">![Inside the Person controller](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Inside the Person controller")</span></span>

   <span data-ttu-id="f85c8-174">*Person コント ローラーの内部*</span><span class="sxs-lookup"><span data-stu-id="f85c8-174">*Inside the Person controller*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a><span data-ttu-id="f85c8-175">タスク 2-実行中のアプリケーション</span><span class="sxs-lookup"><span data-stu-id="f85c8-175">Task 2- Running the application</span></span>

<span data-ttu-id="f85c8-176">この時点では、データベースがまだ作成されていません。</span><span class="sxs-lookup"><span data-stu-id="f85c8-176">At this point, the database is not yet created.</span></span> <span data-ttu-id="f85c8-177">このタスクでは、最初にアプリケーションを実行し、CRUD 操作をテストします。</span><span class="sxs-lookup"><span data-stu-id="f85c8-177">In this task, you will run the application for the first time and test the CRUD operations.</span></span> <span data-ttu-id="f85c8-178">データベースは、Code First ですぐに作成されます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-178">The database will be created on the fly with Code First.</span></span>

1. <span data-ttu-id="f85c8-179">**F5** キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-179">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="f85c8-180">ブラウザーで、追加 **/Person**人 ページを開くための URL にします。</span><span class="sxs-lookup"><span data-stu-id="f85c8-180">In the browser, add **/Person** to the URL to open the Person page.</span></span>

    <span data-ttu-id="f85c8-181">![アプリケーションの初回実行](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "アプリケーションの初回実行")</span><span class="sxs-lookup"><span data-stu-id="f85c8-181">![Application first run](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "Application first run")</span></span>

    <span data-ttu-id="f85c8-182">*アプリケーションの場合: 最初の実行します。*</span><span class="sxs-lookup"><span data-stu-id="f85c8-182">*Application: first run*</span></span>
3. <span data-ttu-id="f85c8-183">ユーザー ページを調べ、CRUD 操作のテストはようになりました。</span><span class="sxs-lookup"><span data-stu-id="f85c8-183">You will now explore the Person pages and test the CRUD operations.</span></span>

    1. <span data-ttu-id="f85c8-184">クリックして**新規作成**新しいメンバーを追加します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-184">Click **Create New** to add a new person.</span></span> <span data-ttu-id="f85c8-185">名と姓を入力し、クリックして**作成**です。</span><span class="sxs-lookup"><span data-stu-id="f85c8-185">Enter a first name and a last name and click **Create**.</span></span>

        <span data-ttu-id="f85c8-186">![新しいユーザーを追加する](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "新しいユーザーを追加します。")</span><span class="sxs-lookup"><span data-stu-id="f85c8-186">![Adding a new person](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Adding a new person")</span></span>

        <span data-ttu-id="f85c8-187">*新しいユーザーを追加します。*</span><span class="sxs-lookup"><span data-stu-id="f85c8-187">*Adding a new person*</span></span>
    2. <span data-ttu-id="f85c8-188">ユーザーの一覧で、削除、編集または項目を追加することができます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-188">In the person's list, you can delete, edit or add items.</span></span>

        <span data-ttu-id="f85c8-189">![人物リスト](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "人物リスト")</span><span class="sxs-lookup"><span data-stu-id="f85c8-189">![person list](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "person list")</span></span>

        <span data-ttu-id="f85c8-190">*人物リスト*</span><span class="sxs-lookup"><span data-stu-id="f85c8-190">*Person list*</span></span>
    3. <span data-ttu-id="f85c8-191">クリックして**詳細**人の詳細を開きます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-191">Click **Details** to open the person's details.</span></span>

        <span data-ttu-id="f85c8-192">![ユーザーの詳細](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "人の詳細")</span><span class="sxs-lookup"><span data-stu-id="f85c8-192">![Person's details](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Person's details")</span></span>

        <span data-ttu-id="f85c8-193">*ユーザーの詳細*</span><span class="sxs-lookup"><span data-stu-id="f85c8-193">*Person's details*</span></span>
4. <span data-ttu-id="f85c8-194">ブラウザーを閉じて、Visual Studio に戻ります。</span><span class="sxs-lookup"><span data-stu-id="f85c8-194">Close the browser and return to Visual Studio.</span></span> <span data-ttu-id="f85c8-195">Person エンティティの全体の CRUD を 1 行のコードを記述しなくても、ビューに、モデルからアプリケーション全体で作成したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-195">Notice that you have created the whole CRUD for the person entity throughout your application -from the model to the views- without having to write a single line of code!</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a><span data-ttu-id="f85c8-196">タスク 3-更新の Entity Framework の移行を使用して、データベース</span><span class="sxs-lookup"><span data-stu-id="f85c8-196">Task 3- Updating the database using Entity Framework Migrations</span></span>

<span data-ttu-id="f85c8-197">このタスクでは、Entity Framework の移行を使用してデータベースを更新します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-197">In this task you will update the database using Entity Framework Migrations.</span></span> <span data-ttu-id="f85c8-198">モデルを変更し、Entity Framework の移行機能を使用して、データベースの変更が反映がいかに簡単かが検出されます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-198">You will discover how easy it is to change the model and reflect the changes in your databases by using the Entity Framework Migrations feature.</span></span>

1. <span data-ttu-id="f85c8-199">パッケージ マネージャー コンソールを開きます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-199">Open the Package Manager Console.</span></span> <span data-ttu-id="f85c8-200">選択**ツール** > **NuGet パッケージ マネージャー** > **パッケージ マネージャー コンソール**します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-200">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="f85c8-201">パッケージ マネージャー コンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-201">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="f85c8-202">PMC</span><span class="sxs-lookup"><span data-stu-id="f85c8-202">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    <span data-ttu-id="f85c8-203">![移行を有効にする](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Migrations を有効にします。")</span><span class="sxs-lookup"><span data-stu-id="f85c8-203">![Enabling Migrations](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Enabling Migrations")</span></span>

    <span data-ttu-id="f85c8-204">*移行を有効にします。*</span><span class="sxs-lookup"><span data-stu-id="f85c8-204">*Enabling migrations*</span></span>

    <span data-ttu-id="f85c8-205">移行の有効化コマンドは、作成、**移行**フォルダーで、データベースを初期化するためのスクリプトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f85c8-205">The Enable-Migration command creates the **Migrations** folder, which contains a script to initialize the database.</span></span>

    <span data-ttu-id="f85c8-206">![Migrations フォルダー](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations フォルダー")</span><span class="sxs-lookup"><span data-stu-id="f85c8-206">![Migrations folder](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations folder")</span></span>

    <span data-ttu-id="f85c8-207">*Migrations フォルダー*</span><span class="sxs-lookup"><span data-stu-id="f85c8-207">*Migrations folder*</span></span>
3. <span data-ttu-id="f85c8-208">開く、 **Configuration.cs** Migrations フォルダーにファイル。</span><span class="sxs-lookup"><span data-stu-id="f85c8-208">Open the **Configuration.cs** file in the Migrations folder.</span></span> <span data-ttu-id="f85c8-209">クラスのコンス トラクターを検索し、変更、 **AutomaticMigrationsEnabled**値を*true*します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-209">Locate the class constructor and change the **AutomaticMigrationsEnabled** value to *true*.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. <span data-ttu-id="f85c8-210">Person クラスを開き、個人のミドル ネームの属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-210">Open the Person class and add an attribute for the person's middle name.</span></span> <span data-ttu-id="f85c8-211">この新しい属性では、モデルを変更します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-211">With this new attribute, you are changing the model.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. <span data-ttu-id="f85c8-212">選択**ビルド |ソリューションをビルド**メニュー アプリケーションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="f85c8-212">Select **Build | Build Solution** on the menu to build the application.</span></span>

    <span data-ttu-id="f85c8-213">![アプリケーションのビルド](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "アプリケーションを構築します。")</span><span class="sxs-lookup"><span data-stu-id="f85c8-213">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Building the application")</span></span>

    <span data-ttu-id="f85c8-214">*アプリケーションのビルド*</span><span class="sxs-lookup"><span data-stu-id="f85c8-214">*Building the application*</span></span>
6. <span data-ttu-id="f85c8-215">パッケージ マネージャー コンソールで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-215">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="f85c8-216">PMC</span><span class="sxs-lookup"><span data-stu-id="f85c8-216">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    <span data-ttu-id="f85c8-217">このコマンドは、データ オブジェクトの変更を検索し、それに応じて、データベースを変更するために必要なコマンドを追加し、します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-217">This command will look for changes in the data objects, and then, it will add the necessary commands to modify the database accordingly.</span></span>

    <span data-ttu-id="f85c8-218">![ミドル ネームを追加する](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "ミドル ネームを追加します。")</span><span class="sxs-lookup"><span data-stu-id="f85c8-218">![Adding a middle name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "Adding a middle name")</span></span>

    <span data-ttu-id="f85c8-219">*ミドル ネームを追加します。*</span><span class="sxs-lookup"><span data-stu-id="f85c8-219">*Adding a middle name*</span></span>
7. <span data-ttu-id="f85c8-220">(省略可能)差分の更新プログラムでの SQL スクリプトを生成するには、次のコマンドを実行することができます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-220">(Optional) You can run the following command to generate a SQL script with the differential update.</span></span> <span data-ttu-id="f85c8-221">これにより、データベースを手動で更新する (この場合必要はありません)、または他のデータベースで変更を適用します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-221">This will let you update the database manually (In this case it's not necessary), or apply the changes in other databases:</span></span>

    <span data-ttu-id="f85c8-222">PMC</span><span class="sxs-lookup"><span data-stu-id="f85c8-222">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    <span data-ttu-id="f85c8-223">![SQL スクリプトを生成して](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "SQL スクリプトの生成")</span><span class="sxs-lookup"><span data-stu-id="f85c8-223">![Generating a SQL script](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "Generating a SQL script")</span></span>

    <span data-ttu-id="f85c8-224">*SQL スクリプトの生成*</span><span class="sxs-lookup"><span data-stu-id="f85c8-224">*Generating a SQL script*</span></span>

    <span data-ttu-id="f85c8-225">![SQL スクリプトの update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL スクリプトの更新")</span><span class="sxs-lookup"><span data-stu-id="f85c8-225">![SQL Script update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL Script update")</span></span>

    <span data-ttu-id="f85c8-226">*SQL スクリプトの更新*</span><span class="sxs-lookup"><span data-stu-id="f85c8-226">*SQL Script update*</span></span>
8. <span data-ttu-id="f85c8-227">パッケージ マネージャー コンソールでは、データベースを更新する次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-227">In the Package Manager Console, enter the following command to update the database:</span></span>

    <span data-ttu-id="f85c8-228">PMC</span><span class="sxs-lookup"><span data-stu-id="f85c8-228">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    <span data-ttu-id="f85c8-229">![データベースの更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "データベースの更新")</span><span class="sxs-lookup"><span data-stu-id="f85c8-229">![Updating the Database](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Updating the Database")</span></span>

    <span data-ttu-id="f85c8-230">*データベースの更新*</span><span class="sxs-lookup"><span data-stu-id="f85c8-230">*Updating the Database*</span></span>

    <span data-ttu-id="f85c8-231">これは追加、 **MiddleName**内の列、**人**の現在の定義と一致するテーブル、**人**クラス。</span><span class="sxs-lookup"><span data-stu-id="f85c8-231">This will add the **MiddleName** column in the **People** table to match the current definition of the **Person** class.</span></span>
9. <span data-ttu-id="f85c8-232">データベースを更新すると、コント ローラーのフォルダーを右クリックし **追加 |コント ローラー** Person コントをもう一度 (同じ値で完了) を追加します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-232">Once the database is updated, right-click the Controller folder and select **Add | Controller** to add the Person controller again (Complete with the same values).</span></span> <span data-ttu-id="f85c8-233">これは、既存のメソッドとビューの新しい属性を追加することで更新されます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-233">This will update the existing methods and views adding the new attribute.</span></span>

    <span data-ttu-id="f85c8-234">![コント ローラーの更新を追加する](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "コント ローラーの更新を追加します。")</span><span class="sxs-lookup"><span data-stu-id="f85c8-234">![Adding a controller update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Adding a controller update")</span></span>

    <span data-ttu-id="f85c8-235">*コント ローラーを更新しています*</span><span class="sxs-lookup"><span data-stu-id="f85c8-235">*Updating the controller*</span></span>
10. <span data-ttu-id="f85c8-236">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f85c8-236">Click **Add**.</span></span> <span data-ttu-id="f85c8-237">値を選択し、**上書き PersonController.cs**と**上書きするには、ビューが関連付けられている** をクリック**ok**します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-237">Then, select the values **Overwrite PersonController.cs** and the **Overwrite associated views** and click **OK**.</span></span>

   ![コント ローラーの上書きを追加します。](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   <span data-ttu-id="f85c8-239">*コント ローラーを更新しています*</span><span class="sxs-lookup"><span data-stu-id="f85c8-239">*Updating the controller*</span></span>

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a><span data-ttu-id="f85c8-240">Task4 - アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="f85c8-240">Task4- Running the application</span></span>

1. <span data-ttu-id="f85c8-241">**F5** キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-241">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="f85c8-242">開いている **/Person**します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-242">Open **/Person**.</span></span> <span data-ttu-id="f85c8-243">データが保持されて、ミドル ネームの列が追加されたときに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f85c8-243">Notice that the data was preserved, while the middle name column was added.</span></span>

    <span data-ttu-id="f85c8-244">![追加のミドル ネーム](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "ミドル ネームの追加")</span><span class="sxs-lookup"><span data-stu-id="f85c8-244">![Middle Name added](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "Middle Name added")</span></span>

    <span data-ttu-id="f85c8-245">*ミドル ネームの追加*</span><span class="sxs-lookup"><span data-stu-id="f85c8-245">*Middle Name added*</span></span>
3. <span data-ttu-id="f85c8-246">クリックすると**編集**、ミドル ネームを現在のユーザーに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-246">If you click **Edit**, you will be able to add a middle name to the current person.</span></span>

    <span data-ttu-id="f85c8-247">![ミドル ネーム edition](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "ミドル ネームのエディション")</span><span class="sxs-lookup"><span data-stu-id="f85c8-247">![Middle Name edition](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Middle Name edition")</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="f85c8-248">まとめ</span><span class="sxs-lookup"><span data-stu-id="f85c8-248">Summary</span></span>

<span data-ttu-id="f85c8-249">このハンズオン ラボでは、どのモデル クラスを使用して ASP.NET MVC 4 スキャフォールディングで CRUD 操作を作成する簡単な手順を説明しました。</span><span class="sxs-lookup"><span data-stu-id="f85c8-249">In this Hands-On lab, you have learned simple steps to create CRUD operations with ASP.NET MVC 4 Scaffolding using any model class.</span></span> <span data-ttu-id="f85c8-250">次に、元のデータベースのビューに、アプリケーションで Entity Framework の移行を使用してエンド ツー エンドの更新プログラムを実行する方法を説明しました。</span><span class="sxs-lookup"><span data-stu-id="f85c8-250">Then, you have learned how to perform an end to end update in your application -from the database to the views- by using Entity Framework Migrations.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="f85c8-251">付録 a:For Web Express 2012 の Visual Studio のインストール</span><span class="sxs-lookup"><span data-stu-id="f85c8-251">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="f85c8-252">インストールすることができます**Microsoft Visual Studio Express 2012 for Web**別または&quot;Express&quot;バージョンを使用して、 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="f85c8-252">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="f85c8-253">次の手順をインストールするために必要な手順をガイドします。 *Visual studio Express 2012 for Web*を使用して*Microsoft Web Platform Installer*します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-253">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="f85c8-254">[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) に移動します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-254">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="f85c8-255">または、既に Web Platform Installer をインストールした場合を開くことも、製品を検索して、 &quot; <em>Visual Studio Express 2012 for Web と Windows Azure SDK</em>&quot;します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-255">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="f85c8-256">をクリックして**を今すぐインストール**します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-256">Click on **Install Now**.</span></span> <span data-ttu-id="f85c8-257">ない場合**Web Platform Installer**をダウンロードして、最初にインストールしてリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-257">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="f85c8-258">1 回**Web Platform Installer**を開くと、クリックして**インストール**セットアップを開始します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-258">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="f85c8-259">![Visual Studio Express のインストール](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Visual Studio Express のインストール")</span><span class="sxs-lookup"><span data-stu-id="f85c8-259">![Install Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="f85c8-260">*Visual Studio Express をインストールします。*</span><span class="sxs-lookup"><span data-stu-id="f85c8-260">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="f85c8-261">すべての製品のライセンスと使用条件を読み、クリックして**同意**を続行します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-261">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![ライセンス条項に同意](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    <span data-ttu-id="f85c8-263">*ライセンス条項に同意*</span><span class="sxs-lookup"><span data-stu-id="f85c8-263">*Accepting the license terms*</span></span>
5. <span data-ttu-id="f85c8-264">ダウンロードとインストール プロセスが完了するまで待機します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-264">Wait until the downloading and installation process completes.</span></span>

    ![インストールの進行状況](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    <span data-ttu-id="f85c8-266">*インストールの進行状況*</span><span class="sxs-lookup"><span data-stu-id="f85c8-266">*Installation progress*</span></span>
6. <span data-ttu-id="f85c8-267">インストールが完了したら、クリックして**完了**します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-267">When the installation completes, click **Finish**.</span></span>

    ![インストールが完了しました](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    <span data-ttu-id="f85c8-269">*インストールが完了しました*</span><span class="sxs-lookup"><span data-stu-id="f85c8-269">*Installation completed*</span></span>
7. <span data-ttu-id="f85c8-270">クリックして**終了**Web Platform Installer を閉じます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-270">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="f85c8-271">Visual Studio Express for Web を開きするには、**開始**画面し、書き込みを開始&quot; **VS Express**&quot;、 をクリックし、 **VS Express for Web**並べて表示します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-271">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web のタイル](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    <span data-ttu-id="f85c8-273">*VS Express for Web のタイル*</span><span class="sxs-lookup"><span data-stu-id="f85c8-273">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="f85c8-274">付録 B:コード スニペットを使用</span><span class="sxs-lookup"><span data-stu-id="f85c8-274">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="f85c8-275">コードのスニペットでは、指先ひとつで必要なすべてのコードがあります。</span><span class="sxs-lookup"><span data-stu-id="f85c8-275">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="f85c8-276">ラボ ドキュメントがわかりますだけをいつ使用できる、次の図に示すようにします。</span><span class="sxs-lookup"><span data-stu-id="f85c8-276">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="f85c8-277">![Visual Studio コード スニペットを使用して、プロジェクトにコードを挿入する](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "プロジェクトにコードを挿入するコード スニペットを Visual Studio の使用")</span><span class="sxs-lookup"><span data-stu-id="f85c8-277">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="f85c8-278">*Visual Studio コード スニペットを使用して、プロジェクトにコードを挿入するには*</span><span class="sxs-lookup"><span data-stu-id="f85c8-278">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="f85c8-279">***キーボード (c# のみ) を使用するコード スニペットを追加するには***</span><span class="sxs-lookup"><span data-stu-id="f85c8-279">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="f85c8-280">コードを挿入するには、カーソルを置きます。</span><span class="sxs-lookup"><span data-stu-id="f85c8-280">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="f85c8-281">スニペットの名前 (なし、スペースやハイフン) の入力を開始します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-281">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="f85c8-282">スニペットの名前に一致する IntelliSense の表示を確認します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-282">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="f85c8-283">適切なスニペットを選択します (または全体のスニペットの名前が選択されるまで」と入力してください)。</span><span class="sxs-lookup"><span data-stu-id="f85c8-283">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="f85c8-284">カーソル位置にスニペットを挿入するには、2 回、Tab キーを押します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-284">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="f85c8-285">![スニペットの名前の入力を開始](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "スニペット名の入力を開始")</span><span class="sxs-lookup"><span data-stu-id="f85c8-285">![Start typing the snippet name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="f85c8-286">*スニペットの名前の入力を開始します。*</span><span class="sxs-lookup"><span data-stu-id="f85c8-286">*Start typing the snippet name*</span></span>

<span data-ttu-id="f85c8-287">![強調表示されているスニペットを選択して Tab キーを押して](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "キーを押してタブが強調表示されているスニペットを選択するには")</span><span class="sxs-lookup"><span data-stu-id="f85c8-287">![Press Tab to select the highlighted snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="f85c8-288">*Tab キーを押して、強調表示されているスニペットを選択します*</span><span class="sxs-lookup"><span data-stu-id="f85c8-288">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="f85c8-289">![キーを押して タブで再度とスニペットが展開](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "キーを押して タブで再度とスニペットが展開されます")</span><span class="sxs-lookup"><span data-stu-id="f85c8-289">![Press Tab again and the snippet will expand](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="f85c8-290">*キーを押して タブで再度とスニペットが展開されます。*</span><span class="sxs-lookup"><span data-stu-id="f85c8-290">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="f85c8-291">***(C#、Visual Basic および XML) にマウスを使用するコード スニペットを追加する***1。</span><span class="sxs-lookup"><span data-stu-id="f85c8-291">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="f85c8-292">コード スニペットを挿入するを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="f85c8-292">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="f85c8-293">選択**スニペットの挿入**続けて**マイ コード スニペット**します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-293">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="f85c8-294">クリックして、一覧から関連するスニペットを選択します。</span><span class="sxs-lookup"><span data-stu-id="f85c8-294">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="f85c8-295">![コード スニペットを挿入し、スニペットの挿入を選択する場所を右クリックして](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "コード スニペットを挿入し、スニペットの挿入を選択する場所を右クリック")</span><span class="sxs-lookup"><span data-stu-id="f85c8-295">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="f85c8-296">*コード スニペットを挿入して、スニペットの挿入先の選択します。*</span><span class="sxs-lookup"><span data-stu-id="f85c8-296">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="f85c8-297">![クリックして、一覧から関連するスニペットを選択](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "クリックして、一覧から関連するスニペットを選択")</span><span class="sxs-lookup"><span data-stu-id="f85c8-297">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="f85c8-298">*クリックして、一覧から関連するスニペットを選択します。*</span><span class="sxs-lookup"><span data-stu-id="f85c8-298">*Pick the relevant snippet from the list, by clicking on it*</span></span>
