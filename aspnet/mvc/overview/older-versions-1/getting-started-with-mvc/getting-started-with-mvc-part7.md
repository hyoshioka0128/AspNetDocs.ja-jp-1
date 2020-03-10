---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: モデルへの検証の追加 |Microsoft Docs
author: shanselman
description: これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。 データベースを読み書きする単純な web アプリケーションを作成します。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437278"
---
# <a name="adding-validation-to-the-model"></a><span data-ttu-id="e820e-104">モデルに検証を追加する</span><span class="sxs-lookup"><span data-stu-id="e820e-104">Adding Validation to the Model</span></span>

<span data-ttu-id="e820e-105">[Scott マン Selman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="e820e-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="e820e-106">これは、ASP.NET MVC の基本を紹介する初心者向けチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="e820e-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="e820e-107">データベースを読み書きする単純な web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="e820e-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="e820e-108">他の ASP.NET MVC のチュートリアルとサンプルについては、 [ASP.NET mvc learning center](../../../index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e820e-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="e820e-109">このセクションでは、アプリケーション内で入力の検証を有効にするために必要なサポートを実装します。</span><span class="sxs-lookup"><span data-stu-id="e820e-109">In this section we are going to implement the support necessary to enable input validation within our application.</span></span> <span data-ttu-id="e820e-110">データベースの内容が常に正しいことを確認し、有効でない映画データを入力しようとすると、エンドユーザーに役立つエラーメッセージを提供します。</span><span class="sxs-lookup"><span data-stu-id="e820e-110">We'll ensure that our database content is always correct, and provide helpful error messages to end users when they try and enter Movie data which is not valid.</span></span> <span data-ttu-id="e820e-111">まず、小さな検証ロジックを Movie クラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="e820e-111">We'll begin by adding a little validation logic to the Movie class.</span></span>

<span data-ttu-id="e820e-112">モデルフォルダーを右クリックし、[クラスの追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e820e-112">Right click on the Model folder and select Add Class.</span></span> <span data-ttu-id="e820e-113">クラスムービーの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="e820e-113">Name your class Movie.</span></span>

<span data-ttu-id="e820e-114">先ほどムービーエンティティモデルを作成すると、IDE によって Movie クラスが作成されました。</span><span class="sxs-lookup"><span data-stu-id="e820e-114">When we created the Movie Entity Model earlier, the IDE created a Movie class.</span></span> <span data-ttu-id="e820e-115">実際、Movie クラスの一部を1つのファイルに配置し、別のファイルに含めることができます。</span><span class="sxs-lookup"><span data-stu-id="e820e-115">In fact, part of the Movie class can be in one file and part in another.</span></span> <span data-ttu-id="e820e-116">これを部分クラスと呼びます。</span><span class="sxs-lookup"><span data-stu-id="e820e-116">This is called a Partial Class.</span></span> <span data-ttu-id="e820e-117">ムービークラスを別のファイルから拡張します。</span><span class="sxs-lookup"><span data-stu-id="e820e-117">We're going to extend the Movie class from another file.</span></span>

<span data-ttu-id="e820e-118">ここでは、システムに検証ヒントを提供するいくつかの属性を使用して "buddy class" を指す部分的なムービークラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="e820e-118">We'll create a partial movie class that points to a "buddy class" with some attributes that will give validation hints to the system.</span></span> <span data-ttu-id="e820e-119">必要に応じてタイトルと価格を設定します。また、価格が特定の範囲内であることを要求します。</span><span class="sxs-lookup"><span data-stu-id="e820e-119">We'll mark the Title and Price as Required, and also insist that the Price be within a certain range.</span></span> <span data-ttu-id="e820e-120">[モデル] フォルダーを右クリックし、[クラスの追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e820e-120">Right click the Models folder and select Add Class.</span></span> <span data-ttu-id="e820e-121">クラスに Movie という名前を指定し、[OK] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="e820e-121">Name your class Movie and Click the OK button.</span></span> <span data-ttu-id="e820e-122">部分的なムービークラスは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="e820e-122">Here's what our partial Movie class looks like.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

<span data-ttu-id="e820e-123">アプリケーションを再実行し、100を超える価格で映画を入力してみてください。</span><span class="sxs-lookup"><span data-stu-id="e820e-123">Re-Run your application and try to enter a movie with a price over 100.</span></span> <span data-ttu-id="e820e-124">フォームを送信すると、エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e820e-124">You'll get an error after you've submitted the form.</span></span> <span data-ttu-id="e820e-125">エラーはサーバー側でキャッチされ、フォームがポストされた後に発生します。</span><span class="sxs-lookup"><span data-stu-id="e820e-125">The error is caught on the server side and occurs after the Form is POSTed.</span></span> <span data-ttu-id="e820e-126">ASP.NET MVC の組み込み HTML ヘルパーは、エラーメッセージを表示し、textbox 要素内の値を維持するのに十分であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e820e-126">Notice how ASP.NET MVC's built-in HTML helpers were smart enough to display the error message and maintain the values for us within the textbox elements:</span></span>

<span data-ttu-id="e820e-127">[![Createmoの検証](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e820e-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span></span>

<span data-ttu-id="e820e-128">これはうまく機能しますが、サーバーが関与する前に、クライアント側でユーザーに通知することもできます。</span><span class="sxs-lookup"><span data-stu-id="e820e-128">This works great, but it'd be nice if we could tell the user on the client-side, immediately, before the server gets involved.</span></span>

<span data-ttu-id="e820e-129">JavaScript でクライアント側の検証を有効にしてみましょう。</span><span class="sxs-lookup"><span data-stu-id="e820e-129">Let's enable some client-side validation with JavaScript.</span></span>

## <a name="adding-client-side-validation"></a><span data-ttu-id="e820e-130">クライアント側の検証の追加</span><span class="sxs-lookup"><span data-stu-id="e820e-130">Adding Client-Side Validation</span></span>

<span data-ttu-id="e820e-131">Movie クラスには既にいくつかの検証属性があるため、いくつかの JavaScript ファイルを作成して、クライアント側の検証を有効にするコード行を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e820e-131">Since our Movie class already has some validation attributes, we'll just need to add a few JavaScript files to our Create.aspx View template and add a line of code to enable client-side validation to take place.</span></span>

<span data-ttu-id="e820e-132">VWD 内から、Views/Movie フォルダーにアクセスして、default.aspx を開きます。</span><span class="sxs-lookup"><span data-stu-id="e820e-132">From within VWD go our Views/Movie folder and open up Create.aspx.</span></span>

<span data-ttu-id="e820e-133">ソリューションエクスプローラーで Scripts フォルダーを開き、次の3つのスクリプトを &lt;head&gt; タグ内にドラッグします。</span><span class="sxs-lookup"><span data-stu-id="e820e-133">Open up the Scripts folder in the Solution Explorer and drag the following three scripts to within the &lt;head&gt; tag.</span></span>

- <span data-ttu-id="e820e-134">Microsoftajax.js</span><span class="sxs-lookup"><span data-stu-id="e820e-134">MicrosoftAjax.js</span></span>
- <span data-ttu-id="e820e-135">MicrosoftMvcValidation.js</span><span class="sxs-lookup"><span data-stu-id="e820e-135">MicrosoftMvcValidation.js</span></span>

<span data-ttu-id="e820e-136">これらのスクリプトファイルがこの順序で表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="e820e-136">You want these script files to appear in this order.</span></span>

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

<span data-ttu-id="e820e-137">また、次の1行を Html. BeginForm の上に追加します。</span><span class="sxs-lookup"><span data-stu-id="e820e-137">Also, add this single line above the Html.BeginForm:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

<span data-ttu-id="e820e-138">IDE 内に表示されるコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="e820e-138">Here's the code shown within the IDE.</span></span>

<span data-ttu-id="e820e-139">[![映画-Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e820e-139">[![Movies - Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span></span>

<span data-ttu-id="e820e-140">アプリケーションを実行し、/Movies/Create にもう一度アクセスして、データを入力せずに [作成] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e820e-140">Run your application and visit /Movies/Create again, and click Create without entering any data.</span></span> <span data-ttu-id="e820e-141">エラーメッセージは、データをサーバーに送信するためにデータを送信するために、ページフラッシュなしですぐに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e820e-141">The error messages appear immediately without the page flash that we associate with sending data all the way back to the server.</span></span> <span data-ttu-id="e820e-142">これは、ASP.NET MVC が、(JavaScript を使用して) クライアントとサーバーの両方で入力を検証するようになったためです。</span><span class="sxs-lookup"><span data-stu-id="e820e-142">This is because ASP.NET MVC is now validating the input on both the client (using JavaScript) and on the server.</span></span>

<span data-ttu-id="e820e-143">[![作成-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="e820e-143">[![Create - Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span></span>

<span data-ttu-id="e820e-144">これは良いことです。</span><span class="sxs-lookup"><span data-stu-id="e820e-144">This is looking good!</span></span> <span data-ttu-id="e820e-145">次に、データベースに列を1つ追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="e820e-145">Let's now add one additional column to the database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e820e-146">[前へ](getting-started-with-mvc-part6.md)
> [次へ](getting-started-with-mvc-part8.md)</span><span class="sxs-lookup"><span data-stu-id="e820e-146">[Previous](getting-started-with-mvc-part6.md)
[Next](getting-started-with-mvc-part8.md)</span></span>
