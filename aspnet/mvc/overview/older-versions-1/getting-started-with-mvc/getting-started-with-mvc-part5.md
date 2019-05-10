---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: コント ローラーからモデルのデータへのアクセス |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 読み取りと書き込みをデータベースから単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65122889"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="fc494-104">コントローラーからモデルのデータにアクセスする</span><span class="sxs-lookup"><span data-stu-id="fc494-104">Accessing your Model's Data from a Controller</span></span>

<span data-ttu-id="fc494-105">[Scott Hanselman](https://github.com/shanselman)による</span><span class="sxs-lookup"><span data-stu-id="fc494-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="fc494-106">これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="fc494-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="fc494-107">読み取りと書き込みをデータベースから単純な web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="fc494-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="fc494-108">参照してください、 [ASP.NET MVC ラーニング センター](../../../index.md)チュートリアルとサンプルは、その他の ASP.NET MVC を検索します。</span><span class="sxs-lookup"><span data-stu-id="fc494-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="fc494-109">このセクションでは、新しい MoviesController クラスを作成し、映画のデータを取得し、ビュー テンプレートを使用して、ブラウザーに表示するコードを作成するでしょう。</span><span class="sxs-lookup"><span data-stu-id="fc494-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="fc494-110">Controllers フォルダーを右クリックし、新しい MoviesController を作成します。</span><span class="sxs-lookup"><span data-stu-id="fc494-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="fc494-111">[![コント ローラーを追加します。](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fc494-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="fc494-112">これにより、プロジェクト内で、\Controllers フォルダーの下に新しい"MoviesController.cs"ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="fc494-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="fc494-113">新しく設定されたデータベースからムービーの一覧を取得する MovieController を更新してみましょう。</span><span class="sxs-lookup"><span data-stu-id="fc494-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="fc494-114">1984 年の夏の後にリリースされた映画のみ取得できるように LINQ クエリを実行しています。</span><span class="sxs-lookup"><span data-stu-id="fc494-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="fc494-115">ビュー テンプレートの映画に戻るには、この一覧を表示、そこでメソッドで右クリックし、それを作成するには、ビューの追加を選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fc494-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="fc494-116">ビューの追加 ダイアログ ボックスで指定するリストを渡している&lt;Movies.Models.Movie&gt;テンプレートの表示にします。</span><span class="sxs-lookup"><span data-stu-id="fc494-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="fc494-117">前の時間ビューの追加 ダイアログを使用して、「空」のテンプレートを作成することを選択とは異なりこの時間を指定する Visual Studio で自動的に「スキャフォールディング」ビュー テンプレートの既定のコンテンツとします。</span><span class="sxs-lookup"><span data-stu-id="fc494-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="fc494-118">"ビューのコンテンツのドロップダウン メニュー内の"List"項目を選択してこれは。</span><span class="sxs-lookup"><span data-stu-id="fc494-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="fc494-119">ただしがある場合、作成された新しいクラス ビューの追加 ダイアログに表示するアプリケーションをコンパイルする必要があります。</span><span class="sxs-lookup"><span data-stu-id="fc494-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![ビューを追加します。](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="fc494-121">追加 をクリックし、システムはムービーの一覧を表示するためビューのコードを自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="fc494-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="fc494-122">これは、変更すると良い、 &lt;h2&gt; Hello World ビューで以前に行ったように"マイ Movie List"のように向かっています。</span><span class="sxs-lookup"><span data-stu-id="fc494-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="fc494-123">[![ビデオ - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="fc494-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="fc494-124">アプリケーションを実行し、アドレス バーに/Movies を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fc494-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="fc494-125">ここで、コント ローラー内での基本的なクエリを使用してデータベースからデータを取得したし、映画について認識しているビューにデータが返されます。</span><span class="sxs-lookup"><span data-stu-id="fc494-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="fc494-126">そのビューは、ムービーのリストをループ処理し、私たちのデータのテーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="fc494-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="fc494-127">[![ムービーの一覧 - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="fc494-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="fc494-128">私たちはありませんする機能を実装する編集、詳細、削除 - このアプリケーションでのスキャフォールディング テンプレートが作成された既定のリンクしない必要があります。</span><span class="sxs-lookup"><span data-stu-id="fc494-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="fc494-129">/Movies/Index.aspx ファイルを開き、それらを削除します。</span><span class="sxs-lookup"><span data-stu-id="fc494-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="fc494-130">次に、更新されたテンプレートの表示がどのようにこれらの変更を行った後のソース コードを示します。</span><span class="sxs-lookup"><span data-stu-id="fc494-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="fc494-131">この例には削除されますので必要はありませんが、あるリンクを作成します。</span><span class="sxs-lookup"><span data-stu-id="fc494-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="fc494-132">次へ を、新規作成 が保持されます。</span><span class="sxs-lookup"><span data-stu-id="fc494-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="fc494-133">削除する列で、アプリがどのようにを次に示します。</span><span class="sxs-lookup"><span data-stu-id="fc494-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="fc494-134">[![ムービーの一覧 - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="fc494-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="fc494-135">ムービー データの単純なリストがあるようになりました。</span><span class="sxs-lookup"><span data-stu-id="fc494-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="fc494-136">ただし、"新規作成 リンクをクリックすると場合、そのように接続されていないエラーが発生しましたします!</span><span class="sxs-lookup"><span data-stu-id="fc494-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="fc494-137">作成アクション メソッドを実装して、データベースに新しい映画を入力するユーザーを有効にします。</span><span class="sxs-lookup"><span data-stu-id="fc494-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fc494-138">[前へ](getting-started-with-mvc-part4.md)
> [次へ](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="fc494-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
