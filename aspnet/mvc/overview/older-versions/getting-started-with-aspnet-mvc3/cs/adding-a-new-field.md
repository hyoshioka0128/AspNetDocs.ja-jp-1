---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: 新しいフィールドを追加する Movie モデルとテーブル (c#) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1、これを使用して ASP.NET MVC Web アプリケーションの構築の基礎を説明しています.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: acac3ade54cc51c8004f9ea5f0ee4157d15251e5
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130188"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table-c"></a><span data-ttu-id="dbf46-103">Movie モデルとテーブルに新しいフィールドを追加する (C#)</span><span class="sxs-lookup"><span data-stu-id="dbf46-103">Adding a New Field to the Movie Model and Table (C#)</span></span>

<span data-ttu-id="dbf46-104">によって[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="dbf46-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> > [!NOTE]
> > <span data-ttu-id="dbf46-105">このチュートリアルの更新バージョンが利用可能な[ここ](../../../getting-started/introduction/getting-started.md)ASP.NET MVC 5 と Visual Studio 2013 を使用します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="dbf46-106">より安全ではるかに簡単に従うしより多くの機能を示します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="dbf46-107">このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1、Microsoft Visual Studio の無料版であるを使用して ASP.NET MVC Web アプリケーションの構築の基礎を説明します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="dbf46-108">始める前に、以下の前提条件がインストールされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="dbf46-109">次のリンクをクリックして、それらのすべてをインストールできます。[Web プラットフォーム インストーラー](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="dbf46-110">または、次のリンクを使用して、前提条件を個別にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="dbf46-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="dbf46-111">Visual Studio Web Developer Express SP1 の前提条件</span><span class="sxs-lookup"><span data-stu-id="dbf46-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="dbf46-112">ASP.NET MVC 3 Tools Update します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="dbf46-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイムとツールのサポート)</span><span class="sxs-lookup"><span data-stu-id="dbf46-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="dbf46-114">Visual Web Developer 2010 ではなく Visual Studio 2010 を使用する場合は、次のリンクをクリックして、前提条件をインストールします。[Visual Studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="dbf46-115">C# ソース コードでの Visual Web Developer プロジェクトは、このトピックと共に使用できます。</span><span class="sxs-lookup"><span data-stu-id="dbf46-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="dbf46-116">[C# バージョンをダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="dbf46-117">Visual Basic を使用する場合に切り替えて、 [Visual Basic バージョン](../vb/intro-to-aspnet-mvc-3.md)このチュートリアルの。</span><span class="sxs-lookup"><span data-stu-id="dbf46-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="dbf46-118">このセクションではモデル クラスにいくつかの変更を加えるし、モデルの変更に合わせてデータベース スキーマを更新する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-118">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="dbf46-119">ムービー モデルへの評価プロパティの追加</span><span class="sxs-lookup"><span data-stu-id="dbf46-119">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="dbf46-120">まず、新しい追加`Rating`プロパティを既存の`Movie`クラス。</span><span class="sxs-lookup"><span data-stu-id="dbf46-120">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="dbf46-121">開く、 *Movie.cs*追加ファイルを開き、`Rating`次のようなプロパティ。</span><span class="sxs-lookup"><span data-stu-id="dbf46-121">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="dbf46-122">完全な`Movie`今のような次のコードをクラスします。</span><span class="sxs-lookup"><span data-stu-id="dbf46-122">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

<span data-ttu-id="dbf46-123">アプリケーションを使用して、再コンパイル、**デバッグ** &gt;**ビルド ムービー**メニュー コマンド。</span><span class="sxs-lookup"><span data-stu-id="dbf46-123">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="dbf46-124">更新した、`Model`クラスもする必要がある更新、 *\Views\Movies\Index.cshtml* と *\Views\Movies\Create.cshtml* 新しいをサポートするためにテンプレートを表示`Rating`プロパティ。</span><span class="sxs-lookup"><span data-stu-id="dbf46-124">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="dbf46-125">開く、 *\Views\Movies\Index.cshtml*追加ファイルを開き、`<th>Rating</th>`直後の列ヘッダー、**価格**列。</span><span class="sxs-lookup"><span data-stu-id="dbf46-125">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="dbf46-126">追加し、`<td>`をレンダリングするテンプレートの末尾付近の列、`@item.Rating`値。</span><span class="sxs-lookup"><span data-stu-id="dbf46-126">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="dbf46-127">以下はどのような更新*Index.cshtml*ビュー テンプレートのようになります。</span><span class="sxs-lookup"><span data-stu-id="dbf46-127">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

<span data-ttu-id="dbf46-128">次に、開く、 *\Views\Movies\Create.cshtml*ファイルを開き、フォームの末尾付近の次のマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-128">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="dbf46-129">これにより、新しいムービーの作成時に、評価を指定できるように、テキスト ボックスを表示します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-129">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="dbf46-130">モデルとデータベース スキーマの相違点を管理します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-130">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="dbf46-131">新しいをサポートするアプリケーション コードを更新するようになりました`Rating`プロパティ。</span><span class="sxs-lookup"><span data-stu-id="dbf46-131">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="dbf46-132">これで、アプリケーションを実行しに移動し、 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="dbf46-132">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="dbf46-133">ただし、これを行うときに、次のエラーを表示されます。</span><span class="sxs-lookup"><span data-stu-id="dbf46-133">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="dbf46-134">ため、このエラーが表示されている更新された`Movie`アプリケーションでモデル クラスは、スキーマの異なる、`Movie`既存のデータベースのテーブル。</span><span class="sxs-lookup"><span data-stu-id="dbf46-134">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="dbf46-135">(データベース テーブルに `Rating` 列はありません)。</span><span class="sxs-lookup"><span data-stu-id="dbf46-135">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="dbf46-136">既定を使用する Entity Framework Code First のデータベースを自動的に作成するように、このチュートリアルで前に行ったときに Code First テーブル データベースに追加して、データベースのスキーマはから生成されたモデル クラスと同期されているかどうかを追跡できます。</span><span class="sxs-lookup"><span data-stu-id="dbf46-136">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="dbf46-137">同期していない、Entity Framework は、エラーをスローします。</span><span class="sxs-lookup"><span data-stu-id="dbf46-137">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="dbf46-138">これにより、表示されている可能性がありますそれ以外の場合のみ (原因不明のエラー) を実行時に、開発時に問題を追跡しやすくします。</span><span class="sxs-lookup"><span data-stu-id="dbf46-138">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="dbf46-139">同期チェック機能は、原因は何を表示するエラー メッセージがあります。</span><span class="sxs-lookup"><span data-stu-id="dbf46-139">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="dbf46-140">エラーを解決する 2 つの方法はあります。</span><span class="sxs-lookup"><span data-stu-id="dbf46-140">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="dbf46-141">Entity Framework に、新しいモデル クラス スキーマに基づいてデータベースを自動的にドロップさせ、再作成させます。</span><span class="sxs-lookup"><span data-stu-id="dbf46-141">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="dbf46-142">この方法は非常に便利な場合、テスト データベースでアクティブな開発を行うため、簡単にまとめてモデルとデータベース スキーマを進化させることができます。</span><span class="sxs-lookup"><span data-stu-id="dbf46-142">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="dbf46-143">短所は、データベース内の既存のデータが失われる-ようにする*しない*実稼働データベースでこのアプローチを使用する!</span><span class="sxs-lookup"><span data-stu-id="dbf46-143">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="dbf46-144">モデル クラスに一致するように、既存のデータベースのスキーマを明示的に変更します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-144">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="dbf46-145">この手法の長所は、データが維持されることです。</span><span class="sxs-lookup"><span data-stu-id="dbf46-145">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="dbf46-146">この変更は手動で行うことも、データベース変更スクリプトを作成して行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="dbf46-146">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="dbf46-147">このチュートリアルでは、最初のアプローチを使用します:、Entity Framework Code First 自動的にモデルを変更するたびにデータベースを再作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dbf46-147">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="dbf46-148">モデルの変更のデータベースを自動的に再作成</span><span class="sxs-lookup"><span data-stu-id="dbf46-148">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="dbf46-149">Code First 自動的に削除し、アプリケーションのモデルを変更するたびに、データベースを再作成できるようにアプリケーションを更新してみましょう。</span><span class="sxs-lookup"><span data-stu-id="dbf46-149">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="dbf46-150">**警告**を自動的に削除して、開発またはテスト データベースを使用している場合にのみ、データベースを再作成するには、この方法を有効にする必要がありますと*決して*実際のデータを格納している実稼働データベースでします。</span><span class="sxs-lookup"><span data-stu-id="dbf46-150">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="dbf46-151">実稼働サーバー上で使用すると、データ損失につながることができます。</span><span class="sxs-lookup"><span data-stu-id="dbf46-151">Using it on a production server can lead to data loss.</span></span>

<span data-ttu-id="dbf46-152">**ソリューション エクスプ ローラー**を右クリックして、*モデル*フォルダーで、**追加**、し、**クラス**します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-152">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="dbf46-153">"MovieInitializer"クラスの名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="dbf46-153">Name the class "MovieInitializer".</span></span> <span data-ttu-id="dbf46-154">更新プログラム、`MovieInitializer`クラスに次のコードを含めます。</span><span class="sxs-lookup"><span data-stu-id="dbf46-154">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="dbf46-155">`MovieInitializer`クラスは、モデルによって使用されるデータベースを削除してモデル クラスを変更する場合を自動的に再作成することを指定します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-155">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="dbf46-156">コードが含まれています、`Seed`時間がいくつか既定のデータを自動的にデータベースに追加する、いずれかを指定するメソッドが作成 (または再作成) します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-156">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="dbf46-157">これは、モデルを変更するたびに手動で設定することがなく、データベースにいくつかサンプル データを設定する便利な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-157">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="dbf46-158">定義したところ、`MovieInitializer`クラスに確認するように、アプリケーションが実行されるたびに、モデル クラスが、データベース内のスキーマと異なるかどうかを接続する必要あります。</span><span class="sxs-lookup"><span data-stu-id="dbf46-158">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="dbf46-159">その場合は、モデルと一致し、サンプル データをデータベースにデータベースを再作成する初期化子を実行できます。</span><span class="sxs-lookup"><span data-stu-id="dbf46-159">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="dbf46-160">開く、 *Global.asax*ファイルのルートにある、`MvcMovies`プロジェクト。</span><span class="sxs-lookup"><span data-stu-id="dbf46-160">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

<span data-ttu-id="dbf46-161">*Global.asax*ファイルが含まれています、プロジェクトの完全なアプリケーションを定義するクラスが含まれています、`Application_Start`初回起動時にアプリケーションを実行しているイベント ハンドラー。</span><span class="sxs-lookup"><span data-stu-id="dbf46-161">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="dbf46-162">2 つ追加してみましょうファイルの先頭にステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-162">Let's add two using statements to the top of the file.</span></span> <span data-ttu-id="dbf46-163">最初は、Entity Framework の名前空間を参照し、2 つ目は、名前空間を参照場所、`MovieInitializer`生活がどれほどのクラスします。</span><span class="sxs-lookup"><span data-stu-id="dbf46-163">The first references the Entity Framework namespace, and the second references the namespace where our `MovieInitializer` class lives:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

<span data-ttu-id="dbf46-164">検索し、`Application_Start`メソッド呼び出しを追加および`Database.SetInitializer`次に示すよう、メソッドの先頭。</span><span class="sxs-lookup"><span data-stu-id="dbf46-164">Then find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

<span data-ttu-id="dbf46-165">`Database.SetInitializer`ステートメントを追加したが、データベースを使用することを示します、`MovieDBContext`インスタンスは自動的に削除してスキーマとデータベースが一致しない場合を再作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dbf46-165">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="dbf46-166">で指定されているサンプル データでデータベースが設定されますも学習したように、`MovieInitializer`クラス。</span><span class="sxs-lookup"><span data-stu-id="dbf46-166">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="dbf46-167">閉じる、 *Global.asax*ファイル。</span><span class="sxs-lookup"><span data-stu-id="dbf46-167">Close the *Global.asax* file.</span></span>

<span data-ttu-id="dbf46-168">アプリケーションを再実行しに移動し、 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="dbf46-168">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="dbf46-169">アプリケーションの起動時には、モデル構造に、データベース スキーマが一致しなくを検出します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-169">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="dbf46-170">自動的に、新しいモデルの構造と一致するデータベースを再作成および、サンプルのムービーのデータベースを設定します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-170">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

<span data-ttu-id="dbf46-172">をクリックして、**新規作成**のリンクを新しいムービーを追加します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-172">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="dbf46-173">評価を追加できることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="dbf46-173">Note that you can add a rating.</span></span>

<span data-ttu-id="dbf46-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="dbf46-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span></span>

<span data-ttu-id="dbf46-175">**[作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="dbf46-175">Click **Create**.</span></span> <span data-ttu-id="dbf46-176">評価を含む、新しいムービーに表示されるビデオを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="dbf46-176">The new movie, including the rating, now shows up in the movies listing:</span></span>

<span data-ttu-id="dbf46-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="dbf46-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span></span>

<span data-ttu-id="dbf46-178">このセクションでは、モデル オブジェクトを変更し、データベースの変更との同期を維持する方法を説明しました。</span><span class="sxs-lookup"><span data-stu-id="dbf46-178">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="dbf46-179">シナリオを試すことができますので、サンプル データを使って新しく作成したデータベースを設定する方法も学習しました。</span><span class="sxs-lookup"><span data-stu-id="dbf46-179">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="dbf46-180">次に、高度な検証ロジックはモデル クラスを追加し、いくつかのビジネス ルールを適用するを有効にする方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="dbf46-180">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dbf46-181">[前へ](examining-the-edit-methods-and-edit-view.md)
> [次へ](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="dbf46-181">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
