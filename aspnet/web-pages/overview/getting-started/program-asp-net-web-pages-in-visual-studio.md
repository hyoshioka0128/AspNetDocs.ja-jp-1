---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Visual Studio ASP.NET を使用した web ページ (Razor) のプログラミング |マイクロソフトドキュメント
author: Rick-Anderson
description: この付録では、Visual Studio 2010 または Visual Web 開発者 2010 Express を使用して、Razor 構文を使用して web ページASP.NETプログラムする方法について説明します。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542899"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="26636-103">Visual Studio を使用した web ページ (Razor) ASP.NETプログラミング</span><span class="sxs-lookup"><span data-stu-id="26636-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="26636-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="26636-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="26636-105">この記事では、Visual Studio または Visual Web 開発者用エクスプレスを使用して、web ページ (Razor) のwebサイトASP.NETプログラムする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="26636-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="26636-106">学習内容</span><span class="sxs-lookup"><span data-stu-id="26636-106">What you'll learn</span></span>
>
> - <span data-ttu-id="26636-107">Visual Studio のバージョンで Web ページを使用して作業ASP.NET必要なもの (どちらかといえば)</span><span class="sxs-lookup"><span data-stu-id="26636-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="26636-108">ビジュアル Web 開発者 2010 Express に ASP.NET Web ページのサポートを追加する方法。</span><span class="sxs-lookup"><span data-stu-id="26636-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="26636-109">Visual Studio の機能を使用して、IntelliSense やデバッガーを含むASP.NETの Razor ページを操作する方法。</span><span class="sxs-lookup"><span data-stu-id="26636-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="26636-110">チュートリアルで使用するソフトウェアバージョン</span><span class="sxs-lookup"><span data-stu-id="26636-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="26636-111">ASP.NET ウェブページ (カミソリ) 3</span><span class="sxs-lookup"><span data-stu-id="26636-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="26636-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="26636-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="26636-113">ウェブマトリックス 3</span><span class="sxs-lookup"><span data-stu-id="26636-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="26636-114">このチュートリアルは、web ページ 2、Visual Studio 2012、Visual Studio 2010、および WebMatrix 2 ASP.NETでも動作します。</span><span class="sxs-lookup"><span data-stu-id="26636-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="26636-115">WebMatrix やその他 ASP.NETの多くのコード エディターを使用して、Web ページを Razor 構文でプログラミングできます。</span><span class="sxs-lookup"><span data-stu-id="26636-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="26636-116">また、多くの種類のアプリケーション (Web サイトだけでなく) を作成するための強力なツール セットを提供する、フル機能の統合開発環境 (IDE) である Microsoft Visual Studio を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="26636-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="26636-117">ASP.NET の Razor ページを操作するには[、Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)を使用できます。</span><span class="sxs-lookup"><span data-stu-id="26636-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="26636-118">ASP.NET Razor Web ページを使用したプログラミングに Visual Studio が提供する、特に便利な 2 つの機能は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="26636-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="26636-119">*インテライセンス*.</span><span class="sxs-lookup"><span data-stu-id="26636-119">*IntelliSense*.</span></span> <span data-ttu-id="26636-120">Visual Studio に組み込まれている IntelliSense 機能は、WebMatrix の IntelliSense よりも包括的です。</span><span class="sxs-lookup"><span data-stu-id="26636-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="26636-121">*デバッガ*:</span><span class="sxs-lookup"><span data-stu-id="26636-121">*Debugger*.</span></span> <span data-ttu-id="26636-122">デバッガーを使用すると、実行中にプログラムを停止し、変数を調べ、コードを 1 行ずつステップ実行することで、コードのトラブルシューティングを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="26636-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="26636-123">異なるバージョンの web ページでの Visual Studio の使用ASP.NET</span><span class="sxs-lookup"><span data-stu-id="26636-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="26636-124">Visual Studio 2017 で ASP.NET Web アプリを開発するには **、ASP.NETと web 開発**ワークロードをインストールします。</span><span class="sxs-lookup"><span data-stu-id="26636-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="26636-125">Visual Studio 2012 および Visual Studio 2013 には、ASP.NET Web ページのサポートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="26636-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="26636-126">(ASP.NET Web ページをサポートするために必要なパッケージは、Visual Studio のインストール時にインストールされます)。</span><span class="sxs-lookup"><span data-stu-id="26636-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="26636-127">Visual Studio 2010 には、ASP.NET Web ページの既定のサポートは含まれていません。</span><span class="sxs-lookup"><span data-stu-id="26636-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="26636-128">Visual Studio 2010 でASP.NET Web ページを使用するには、ASP.NET MVC パッケージをインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="26636-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="26636-129">web ページ 2 ASP.NETを取得するには、mvc 4 ASP.NETインストールします。</span><span class="sxs-lookup"><span data-stu-id="26636-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="26636-130">次の表は、さまざまなバージョンの Visual Studio でのASP.NET Web ページのサポートをまとめたものです。</span><span class="sxs-lookup"><span data-stu-id="26636-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="26636-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="26636-131">Visual Studio 2010</span></span> | <span data-ttu-id="26636-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="26636-132">Visual Studio 2012</span></span> | <span data-ttu-id="26636-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="26636-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="26636-134">**ASP.NET Web ページ 2**</span><span class="sxs-lookup"><span data-stu-id="26636-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="26636-135">ASP.NET MVC 4 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="26636-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="26636-136">(含まれる)</span><span class="sxs-lookup"><span data-stu-id="26636-136">(Included)</span></span> | <span data-ttu-id="26636-137">(含まれる)</span><span class="sxs-lookup"><span data-stu-id="26636-137">(Included)</span></span> |
| <span data-ttu-id="26636-138">**ASP.NET Web ページ 3**</span><span class="sxs-lookup"><span data-stu-id="26636-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="26636-139">NuGet を使用して ASP.NET Web ページ 3 に更新します。</span><span class="sxs-lookup"><span data-stu-id="26636-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="26636-140">(含まれる)</span><span class="sxs-lookup"><span data-stu-id="26636-140">(Included)</span></span> |

<span data-ttu-id="26636-141">Visual Studio 2010 を使用するには[、「Visual Studio 2010 での ASP.NET Web ページのサポートのインストール](#vs2010support)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="26636-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="26636-142">Web マトリックスからビジュアル スタジオを起動する</span><span class="sxs-lookup"><span data-stu-id="26636-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="26636-143">WebMatrix でプロジェクトを開始し、Visual Studio に切り替える場合は、WebMatrix は、簡単に Visual Studio でプロジェクトを開くボタンを提供します。</span><span class="sxs-lookup"><span data-stu-id="26636-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="26636-144">このボタンを有効にするには、Visual Studio がコンピューターにインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="26636-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="26636-145">次の図は、WebMatrix のボタンを示しています。</span><span class="sxs-lookup"><span data-stu-id="26636-145">The following image shows the button in WebMatrix.</span></span>

![起動ビジュアル スタジオ](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="26636-147">ボタンをクリックすると、プロジェクトが Visual Studio で開かれます。</span><span class="sxs-lookup"><span data-stu-id="26636-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="26636-148">WebMatrix と Visual Studio を切り替えても問題なく切り替えることができます。</span><span class="sxs-lookup"><span data-stu-id="26636-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="26636-149">他の環境でファイルが変更された場合は、最新の変更を取得するために再ロードする必要がある場合は、通知されます。</span><span class="sxs-lookup"><span data-stu-id="26636-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="26636-150">visual Studio でASP.NETカミソリサイトを作成する</span><span class="sxs-lookup"><span data-stu-id="26636-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="26636-151">ビジュアル スタジオでASP.NETの Razor Web サイトを作成するには:</span><span class="sxs-lookup"><span data-stu-id="26636-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="26636-152">Visual Studio を開きます。</span><span class="sxs-lookup"><span data-stu-id="26636-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="26636-153">[**ファイル]** メニューの [**新しい Web サイト**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="26636-153">In the **File** menu, click **New Web Site**.</span></span>

    ![新しい Web サイトを作成する](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="26636-155">[**新しい Web サイト]** ダイアログ ボックスで、使用する言語を選択します (Visual C# または Visual Basic)。</span><span class="sxs-lookup"><span data-stu-id="26636-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="26636-156">**[ASP.NET Web サイト (Razor)]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="26636-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![カミソリサイト](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="26636-158">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="26636-158">Click **OK**.</span></span>

<span data-ttu-id="26636-159">新しいプロジェクトが存在し、作業を開始するのに役立ついくつかの既定の Web ページが設定されます。</span><span class="sxs-lookup"><span data-stu-id="26636-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="26636-160">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="26636-160">Using IntelliSense</span></span>

<span data-ttu-id="26636-161">サイトを作成したので、IntelliSense が Visual Studio でどのように機能するかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="26636-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="26636-162">作成した Web サイトで *、Default.cshtml*ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="26636-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="26636-163">ページ内`<h3>`のタグの後に、`@ServerInfo.`ドットを含むタグを入力します。</span><span class="sxs-lookup"><span data-stu-id="26636-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="26636-164">ドロップダウン リストにヘルパーに使用可能なメソッドが IntelliSense によって`ServerInfo`表示される様子に注目してください。</span><span class="sxs-lookup"><span data-stu-id="26636-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="26636-166">リストから`GetHtml`方法を選択し、Enter キーを押します。</span><span class="sxs-lookup"><span data-stu-id="26636-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="26636-167">IntelliSense はメソッドに自動的に入力します。</span><span class="sxs-lookup"><span data-stu-id="26636-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="26636-168">(C# の他のメソッドと同様に、`()`メソッドの後に文字を追加する必要があります。メソッドの完成した`GetHtml`コードは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="26636-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="26636-169">Ctrl キーを押しながら F5 キーを押してページを実行します。</span><span class="sxs-lookup"><span data-stu-id="26636-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="26636-170">ブラウザーで表示される場合のページの外観は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="26636-170">This is what the page looks like when displayed in a browser:</span></span>

    ![ブラウザの既定のページ](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="26636-172">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="26636-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="26636-173">デバッガの使用</span><span class="sxs-lookup"><span data-stu-id="26636-173">Using the Debugger</span></span>

1. <span data-ttu-id="26636-174">*Default.cshtml*ページの上部で、で始まる`Page.Title`行の後に次のコード行を追加します。</span><span class="sxs-lookup"><span data-stu-id="26636-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="26636-175">コードの左側にあるエディタの灰色の余白で、この新しい行の横をクリックして*ブレークポイント*を追加します。</span><span class="sxs-lookup"><span data-stu-id="26636-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="26636-176">ブレークポイントは、デバッガーに対して、その時点でプログラムの実行を停止し、何が起こっているかを確認できるように指示するマーカーです。</span><span class="sxs-lookup"><span data-stu-id="26636-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![ブレークポイントの設定](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="26636-178">メソッドの呼び出`ServerInfo.GetHtml`しを削除し、その代わりに`@myTime`変数への呼び出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="26636-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="26636-179">この呼び出しは、新しいコード行によって返される現在の時刻の値を表示します。</span><span class="sxs-lookup"><span data-stu-id="26636-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="26636-180">F5 キーを押して、デバッガーでページを実行します。</span><span class="sxs-lookup"><span data-stu-id="26636-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="26636-181">ページは、設定したブレークポイントで停止します。</span><span class="sxs-lookup"><span data-stu-id="26636-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="26636-182">次の図は、ブレークポイントが付いたエディターでのページの外観を示しています (黄色)。</span><span class="sxs-lookup"><span data-stu-id="26636-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![デバッグ ブレークポイント](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="26636-184">[デバッグ] ツールバーの [**ステップ**イン] ボタンをクリック (または F11 キーを押します) をクリックして、次のコード行を実行します。</span><span class="sxs-lookup"><span data-stu-id="26636-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="26636-185">このボタンをクリックするたびに、次のコード行に実行を進めます。</span><span class="sxs-lookup"><span data-stu-id="26636-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![ステップインボタン](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="26636-187">変数の値を調`myTime`べるには、マウス ポインターをその上に置くか、[**ローカル**] ウィンドウと [**呼び出し履歴**] ウィンドウに表示される値を調べます。</span><span class="sxs-lookup"><span data-stu-id="26636-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="26636-188">変数の値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="26636-188">Visual Studio display the value of the variable.</span></span>

    ![時間の値を表示する](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="26636-190">変数の検査とコードのステップ実行が完了したら、F5 キーを押して、各行で停止することなくページの実行を続けます。</span><span class="sxs-lookup"><span data-stu-id="26636-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="26636-191">すべてのコードのステップ実行が完了すると、ブラウザーにページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="26636-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="26636-192">デバッガーの詳細と Visual Studio でのコードのデバッグ方法については、「[チュートリアル: Visual Web 開発者の Web ページのデバッグ](https://msdn.microsoft.com/library/z9e7w6cs.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="26636-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="26636-193">visual Studio で ASP.NET MVC プロジェクトでの Razor の使用</span><span class="sxs-lookup"><span data-stu-id="26636-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="26636-194">Razor 構文は、ASP.NET MVC プロジェクトでも広く使用されます。</span><span class="sxs-lookup"><span data-stu-id="26636-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="26636-195">MVC は、動的な Web サイトを構築するための強力なパターン ベースの方法です。</span><span class="sxs-lookup"><span data-stu-id="26636-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="26636-196">ASP.NET Web ページ サイトの保守が困難になった場合は、そのサイトを ASP.NET MVC アプリケーションに変換することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="26636-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="26636-197">MVC アプリケーションの作成例については[、「mvc 5 の概要ASP.NET」](../../../mvc/overview/getting-started/introduction/getting-started.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="26636-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="26636-198">Visual Studio 2010 での ASP.NET Web ページのサポートのインストール</span><span class="sxs-lookup"><span data-stu-id="26636-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="26636-199">このセクションでは、Visual Web 開発者 Express 2010 と visual Studio 用の ASP.NET Web ページ ツールをインストールする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="26636-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="26636-200">Web プラットフォーム インストーラーをまだインストールしていない場合は、次の URL からダウンロードしてください。</span><span class="sxs-lookup"><span data-stu-id="26636-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="26636-201">Web プラットフォーム インストーラーを実行します。</span><span class="sxs-lookup"><span data-stu-id="26636-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="26636-202">[**製品]** タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="26636-202">Click the **Products** tab.</span></span>

    ![[WebPI 製品] タブ](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="26636-204">mvc **4 ASP.NET**検索 (ASP.NET Web ページ 2 の場合) し、[**追加**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="26636-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="26636-205">これらの製品には、ASP.NET Razor Web サイトを構築するための Visual Studio ツールが含まれます。</span><span class="sxs-lookup"><span data-stu-id="26636-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi インストール オプション](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="26636-207">[**インストール**] をクリックしてインストールを完了します。</span><span class="sxs-lookup"><span data-stu-id="26636-207">Click **Install** to complete the installation.</span></span>
