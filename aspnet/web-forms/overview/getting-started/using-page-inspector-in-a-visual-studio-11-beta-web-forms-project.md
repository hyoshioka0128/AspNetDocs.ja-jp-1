---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: ASP.NET Web Forms | で Visual Studio 2012 の Page Inspector を使用するMicrosoft Docs
author: rick-anderson
description: Visual Studio 2012 の Page Inspector は、統合されたブラウザーを備えた web 開発ツールです。 統合ブラウザーで任意の要素を選択し、Page Inspector...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: c165bbea505b4cb8eae1312cdd587f4ed36541a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464944"
---
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a><span data-ttu-id="38fc0-104">ASP.NET Web フォームで Visual Studio 2012 の Page Inspector を使用する</span><span class="sxs-lookup"><span data-stu-id="38fc0-104">Using Page Inspector for Visual Studio 2012 in ASP.NET Web Forms</span></span>

<span data-ttu-id="38fc0-105">Tim Ammann</span><span class="sxs-lookup"><span data-stu-id="38fc0-105">by Tim Ammann</span></span>

> <span data-ttu-id="38fc0-106">Visual Studio 2012 の Page Inspector は、統合されたブラウザーを備えた web 開発ツールです。</span><span class="sxs-lookup"><span data-stu-id="38fc0-106">Page Inspector for Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="38fc0-107">統合ブラウザーで任意の要素を選択すると、Page Inspector 要素のソースと CSS が瞬時に強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="38fc0-108">アプリケーション内の任意のページを参照したり、表示されたマークアップのソースをすばやく検索したり、Visual Studio 環境内でブラウザーツールを使用したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-108">You can browse any page in your application, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> <span data-ttu-id="38fc0-109">このチュートリアルでは、検査モードを有効にし、web プロジェクト内の CSS ルールとテキストをすばやく検索および編集する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-109">This tutorial shows how to enable Inspection Mode and then quickly locate and edit CSS rules and text within your web project.</span></span> <span data-ttu-id="38fc0-110">このチュートリアルでは Web フォームアプリケーションプロジェクトを使用しますが、Web サイトプロジェクトおよび[MVC](https://go.microsoft.com/?linkid=9802002)アプリケーションに Page Inspector を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-110">The tutorial uses a Web Forms Application Project, but you can also use Page Inspector for Web Site projects and [MVC](https://go.microsoft.com/?linkid=9802002) applications.</span></span>
> 
> <span data-ttu-id="38fc0-111">このチュートリアルには、次のセクションがあります。</span><span class="sxs-lookup"><span data-stu-id="38fc0-111">The tutorial has the following sections:</span></span>
> 
> [<span data-ttu-id="38fc0-112">前提条件</span><span class="sxs-lookup"><span data-stu-id="38fc0-112">Prerequisites</span></span>](#_1_prerequisites)
> 
> [<span data-ttu-id="38fc0-113">Web アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="38fc0-113">Create a Web Application</span></span>](#_2_creating_a)
> 
> [<span data-ttu-id="38fc0-114">Page Inspector を使用してアプリケーションを表示する</span><span class="sxs-lookup"><span data-stu-id="38fc0-114">Use Page Inspector to View the Application</span></span>](#_3_using_page)
> 
> [<span data-ttu-id="38fc0-115">検査モードを有効にする</span><span class="sxs-lookup"><span data-stu-id="38fc0-115">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> 
> [<span data-ttu-id="38fc0-116">Page Inspector を使用してマークアップを変更する</span><span class="sxs-lookup"><span data-stu-id="38fc0-116">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> 
> [<span data-ttu-id="38fc0-117">検査モードと HTML ウィンドウ</span><span class="sxs-lookup"><span data-stu-id="38fc0-117">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> 
> <span data-ttu-id="38fc0-118">[[スタイル] ウィンドウでの CSS の変更のプレビュー](#_7_previewing_css)</span><span class="sxs-lookup"><span data-stu-id="38fc0-118">[Preview CSS Changes in the Styles Window](#_7_previewing_css)</span></span>
> 
> [<span data-ttu-id="38fc0-119">CSS 自動同期</span><span class="sxs-lookup"><span data-stu-id="38fc0-119">CSS Auto Sync</span></span>](#css_auto_sync)
> 
> [<span data-ttu-id="38fc0-120">CSS カラーピッカーの使用</span><span class="sxs-lookup"><span data-stu-id="38fc0-120">Using the CSS Color Picker</span></span>](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="38fc0-121">前提条件</span><span class="sxs-lookup"><span data-stu-id="38fc0-121">Prerequisites</span></span>

- <span data-ttu-id="38fc0-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11)または[Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。</span><span class="sxs-lookup"><span data-stu-id="38fc0-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="38fc0-123">最新バージョンの Page Inspector を取得するには、 [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386)を使用して Azure SDK for .net 2.0 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-123">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="38fc0-124">Page Inspector は Microsoft Web Developer Tools にバンドルされています。</span><span class="sxs-lookup"><span data-stu-id="38fc0-124">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="38fc0-125">最新バージョンは1.3 です。</span><span class="sxs-lookup"><span data-stu-id="38fc0-125">The latest version is 1.3.</span></span> <span data-ttu-id="38fc0-126">使用しているバージョンを確認するには、Visual Studio を実行し、 **[ヘルプ]** メニューから バージョン **[情報 Microsoft Visual Studio]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-126">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="38fc0-127">Web アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="38fc0-127">Create a Web Application</span></span>

<span data-ttu-id="38fc0-128">まず、で Page Inspector 使用する web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-128">First, you will create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="38fc0-129">Visual Studio で、[**ファイル**&gt;**新しいプロジェクト**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-129">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="38fc0-130">左側で **[ C#ビジュアル]** を展開し、 **[web]** を選択して、 **[ASP.NET web フォームアプリケーション]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-130">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET Web Forms Application**.</span></span>

![新しい Web フォームアプリケーション](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

<span data-ttu-id="38fc0-132">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-132">Click **OK**.</span></span>

<span data-ttu-id="38fc0-133">アプリケーションが**ソース**ビューで開きます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-133">The application opens in **Source** view.</span></span>

![ソースビューの新しい Web フォームアプリケーション](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

<span data-ttu-id="38fc0-135">アプリケーションを操作できるようになったので、Page Inspector を使用して確認し、変更することができます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-135">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a><span data-ttu-id="38fc0-136">Page Inspector を使用してアプリケーションを表示する</span><span class="sxs-lookup"><span data-stu-id="38fc0-136">Use Page Inspector to View the Application</span></span>

<span data-ttu-id="38fc0-137">次に、Page Inspector でアプリケーションを表示します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-137">Next, you will view the application with Page Inspector.</span></span> <span data-ttu-id="38fc0-138">**ソリューションエクスプローラー**で、プロジェクトを右クリックし、 **[Page Inspector で表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-138">In **Solution Explorer**, right click the project, and then choose **View in Page Inspector**.</span></span>

![Page Inspector で表示](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

<span data-ttu-id="38fc0-140">既定では Page Inspector 初めて起動されるときに、Visual Studio 環境の左側にナローウィンドウとしてドッキングされます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-140">By default, when Page Inspector launches for the first time, it is docked as a narrow window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="38fc0-141">左側にドッキングしたままにして、快適な幅に設定するか、上部、下部、または右にあるツール領域のいずれかにドッキングします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-141">Leave it docked on the left side and set it to a width that is comfortable for you, or dock it in one of the tool areas on the top, bottom, or right:</span></span>

![ドッキング位置の Page Inspector](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

<span data-ttu-id="38fc0-143">[Page Inspector] ウィンドウをドッキング解除する場合は、Visual Studio の外部に配置するか、2つ目のモニター (存在する場合) に配置することもできます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-143">If you undock the Page Inspector window, you can place it outside Visual Studio, or even on a second monitor if you have one.</span></span> <span data-ttu-id="38fc0-144">ただし、Page Inspector ウィンドウがドッキング解除されているときに、Page Inspector と Visual Studio の間で ALT + TAB キーを押すには、[&gt;**ツール**]、 **[オプション]** 、[&gt;**環境**&gt; タブ**とウィンドウ**] の順に移動し、 **[タブウェル]** で **[フローティングツールウィンドウを常にメインウィンドウの上部に]** 表示する チェックボックスをオフにします</span><span class="sxs-lookup"><span data-stu-id="38fc0-144">However, in order to ALT+TAB between Page Inspector and Visual Studio when the Page Inspector window is undocked, go to **Tools** &gt; **Options** &gt; **Environment** &gt; **Tabs and Windows**, and under **Tab Well**, clear the check box called **Floating tool windows always stay on top of the main window**:</span></span>

![Visual Studio と [ドッキング解除された Page Inspector] ウィンドウの間で ALT + TAB キーを押してフローティングツールウィンドウのチェックボックスをオフにする](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

<span data-ttu-id="38fc0-146">[Page Inspector] ウィンドウの上部ペインに、ブラウザーウィンドウに現在のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-146">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="38fc0-147">下部のペインには、左側に HTML マークアップのページが表示されます。また、右側には、ページのさまざまな側面を調べるためのタブが表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-147">The bottom pane shows the page in HTML markup on the left, and some tabs on the right that let you inspect different aspects of the page.</span></span> <span data-ttu-id="38fc0-148">下のウィンドウは、Internet Explorer の[F12 開発者ツール](https://msdn.microsoft.com/ie/aa740478)に似ています。</span><span class="sxs-lookup"><span data-stu-id="38fc0-148">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span> <span data-ttu-id="38fc0-149">(ただし、開発者ツールとは異なり、Visual Studio 内で Page Inspector 権限を使用できます)。</span><span class="sxs-lookup"><span data-stu-id="38fc0-149">(However, unlike the developer tools, you can use Page Inspector right within Visual Studio.)</span></span>

![Page Inspector](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

<span data-ttu-id="38fc0-151">このチュートリアルでは、Page Inspector ブラウザー ウィンドウと  **HTML** タブと **スタイル** タブを使用して、アプリケーションにすばやく移動し、変更を加えることができます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-151">In this tutorial, you will use the Page Inspector browser pane, and the **HTML** and **Styles** tabs to help you rapidly navigate and make changes to the application.</span></span>

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a><span data-ttu-id="38fc0-152">検査モードを有効にする</span><span class="sxs-lookup"><span data-stu-id="38fc0-152">Enable Inspection Mode</span></span>

<span data-ttu-id="38fc0-153">次に、Page Inspector の検査モードのしくみについて説明します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-153">Next, you will see how Page Inspector's Inspection Mode works.</span></span> <span data-ttu-id="38fc0-154">Page Inspector ウィンドウで、**検査** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-154">In the Page Inspector window, click the **Inspect** button.</span></span>

![要素の検査](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

<span data-ttu-id="38fc0-156">検査モードが動作していることを確認するには、Page Inspector ブラウザーウィンドウ内のページのさまざまな部分にマウスを移動します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-156">To see inspection mode in action, move your mouse over different parts of the page within the Page Inspector browser window.</span></span> <span data-ttu-id="38fc0-157">この操作を行うと、マウスポインターが大きなプラス記号に変わり、下の要素が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-157">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Div にカーソルを合わせる-ラッパー](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

<span data-ttu-id="38fc0-159">マウスポインターを移動すると、</span><span class="sxs-lookup"><span data-stu-id="38fc0-159">As you move the mouse pointer, note that</span></span>

- <span data-ttu-id="38fc0-160">**ソース**ビューの内容が変更され、ページ上の選択した要素に対応するマークアップが表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-160">The content in **Source** view changes to show the markup corresponding to the selected element on the page.</span></span> <span data-ttu-id="38fc0-161">関連するマークアップが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-161">The relevant markup is highlighted.</span></span> <span data-ttu-id="38fc0-162">ソースが別のファイルにある場合は、そのファイルがソースビューで開き、関連するマークアップが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-162">If the source is in another file, that file is opened in Source view with the relevant markup highlighted.</span></span>

- <span data-ttu-id="38fc0-163">Page Inspector の **[HTML]** タブに表示されるマークアップも、ページ上の選択した要素に対応するように変更されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-163">The markup displayed in the **HTML** tab in Page Inspector also changes to correspond to the selected element on the page.</span></span> <span data-ttu-id="38fc0-164">**[HTML]** タブには、関連するマークアップの概要が示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-164">In the **HTML** tab, the relevant markup is outlined.</span></span>

- <span data-ttu-id="38fc0-165">**[スタイル]** タブには、現在の選択に関連する CSS ルールが表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-165">The **Styles** tab shows the CSS rules relevant to the current selection.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="38fc0-166">Page Inspector を使用してマークアップを変更する</span><span class="sxs-lookup"><span data-stu-id="38fc0-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="38fc0-167">ここでは、Page Inspector を使用して、場所がすぐにわからない可能性があるマークアップやテキストを検索し、変更を加える方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-167">Now you will see how you can use Page Inspector to find and make changes to markup or text whose location might not be immediately obvious.</span></span>

<span data-ttu-id="38fc0-168">Page Inspector を検査モードに配置し、ホームページの一番下までスクロールします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-168">Put Page Inspector in Inspection Mode and then scroll to the bottom of the home page.</span></span>

<span data-ttu-id="38fc0-169">フッター領域を入力するとすぐに、他のタブの右側にある一時的なタブの **[ソース]** ビューにある [Page Inspector の*マスター*レイアウトファイル] が開き、選択したマスターページのセクションが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-169">As soon as you enter the footer area, Page Inspector opens the *Site.Master* layout file in **Source** view in a temporary tab to the right of the other tabs and highlights the section of the master page that you have selected.</span></span> <span data-ttu-id="38fc0-170">ここでは、Page Inspector が、最初に開いたファイルとは別のファイルから取得したコンテンツを検索して表示する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-170">This shows you how Page Inspector can find and display content on a page that might actually come from a different file than the one you originally opened.</span></span>

![検査モードでのフッターの強調表示](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

<span data-ttu-id="38fc0-172">Page Inspector ブラウザーウィンドウで、著作権<a id="a"></a>に関する通知を含む行の上にマウスポインターを移動します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-172">In the Page Inspector browser window, move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span>

<span data-ttu-id="38fc0-173">[ *.Master* ] ページで、対応する行が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-173">In the *Site.Master* page, the corresponding line is highlighted.</span></span>

![フッターの著作権線が強調表示されます](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

<span data-ttu-id="38fc0-175">*サイトのマスター*ファイル内の行の末尾にテキストを追加します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-175">Add some text to the end of the line in the *Site.Master* file.</span></span>

<span data-ttu-id="38fc0-176">&lt;p&gt;&amp;コピーです。&lt;%: DateTime. 今年%&gt;-My ASP.NET アプリケーションがありません。&lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="38fc0-176">&lt;p&gt;&amp;copy; &lt;%: DateTime.Now.Year %&gt; - My ASP.NET Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="38fc0-177">ここで、Ctrl + Alt + Enter キーを押すか、更新バーをクリックして Page Inspector ブラウザーウィンドウに結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-177">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![私の ASP.NET アプリケーションは岩を持っています。](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

<span data-ttu-id="38fc0-179">フッターは*default.aspx*ページにあると思ったかもしれませんが、[マスターレイアウト] ページに表示されるようになったので、それを見つける Page Inspector ます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-179">You might have thought that the footer was on the *Default.aspx* page, but it turned out to be in the master layout page, and Page Inspector found it for you.</span></span>

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="38fc0-180">検査モードと HTML ウィンドウ</span><span class="sxs-lookup"><span data-stu-id="38fc0-180">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="38fc0-181">次に、HTML ウィンドウと、要素をどのようにマップするかを簡単に説明します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-181">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="38fc0-182">検査モードに Page Inspector を配置します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-182">Put Page Inspector in Inspection Mode.</span></span>

![要素の検査](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

<span data-ttu-id="38fc0-184">ページの一番上の部分をクリックします。 [ここにロゴを入力してください] と表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-184">Click the top part of the page that says "your logo here".</span></span> <span data-ttu-id="38fc0-185">特定の要素を詳細に調べているため、マウスポインターを移動しても、ブラウザーウィンドウの表示が変更されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="38fc0-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="38fc0-186">次に、マウスポインターを**HTML**ウィンドウに移動します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="38fc0-187">マウスポインターを移動すると、Page Inspector **HTML**ウィンドウ内の要素のアウトラインが表示され、ブラウザーウィンドウ内の対応する要素が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML ウィンドウ](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

<span data-ttu-id="38fc0-189">以前と同様に、Page Inspector は、一時的なタブで、*サイトのマスター*ファイルを開きます。 [] タブをクリックすると、対応するマークアップが &lt;ヘッダー&gt; セクションで強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-189">As before, Page Inspector opens the *Site.Master* file for you in a temporary tab. Click the Site.Master tab, and the corresponding markup is highlighted in the &lt;header&gt; section:</span></span>

![強調表示されたマークアップ](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="38fc0-191">[スタイル] ウィンドウでの CSS の変更のプレビュー</span><span class="sxs-lookup"><span data-stu-id="38fc0-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="38fc0-192">次に、[Page Inspector**スタイル**] ウィンドウを使用して、CSS の変更をプレビューする方法を確認します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-192">Next, you will see how you can use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="38fc0-193">**[検査]** ボタンをクリックして、検査モードに Page Inspector を配置します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-193">Click the **Inspect** button to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="38fc0-194">Page Inspector ブラウザーウィンドウで、ホームページ セクションの上にマウスポインターを移動し、 **div** と表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![要素の上にマウスポインターを置く](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

<span data-ttu-id="38fc0-196">Div のコンテンツラッパーセクション内を1回クリックし、マウスポインターを **[スタイル]** ウィンドウに移動します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="38fc0-197">[... コンテンツラッパークラスセレクター] で、[背景色] プロパティのチェックボックスをオフにして選択します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-197">Under the .featured .content-wrapper class selector, clear and select the checkbox for the background-color property.</span></span>

![背景色のクリア](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

<span data-ttu-id="38fc0-199">Page Inspector ブラウザーウィンドウに変更がすぐに表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-199">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="38fc0-200">もう一度チェックボックスをオンにし、プロパティ値をダブルクリックして、`red`に変更します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-200">Select the checkbox again, then double-click the property value and change it to `red`.</span></span> <span data-ttu-id="38fc0-201">変更はすぐに表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-201">The change shows immediately:</span></span>

![赤の背景色](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

<span data-ttu-id="38fc0-203">**[スタイル]** ウィンドウを使用すると、スタイルシート自体に変更をコミットする前に、CSS の変更を簡単にテストおよびプレビューできます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-203">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="38fc0-204">CSS 自動同期</span><span class="sxs-lookup"><span data-stu-id="38fc0-204">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="38fc0-205">この機能には Page Inspector のバージョン1.3 が必要です。</span><span class="sxs-lookup"><span data-stu-id="38fc0-205">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="38fc0-206">CSS 自動同期機能を使用すると、CSS ファイルを直接編集し、Page Inspector ブラウザーですぐに変更を確認することができます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-206">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="38fc0-207">**[検査]** をクリックして、検査モードに Page Inspector を配置します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-207">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="38fc0-208">Page Inspector ブラウザーで、[ホームページ] セクションの上にマウスポインターを移動**します。このラベルが**表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-208">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="38fc0-209">この要素を選択するには、[1 回] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-209">Click once to select this element.</span></span>

<span data-ttu-id="38fc0-210">**[スタイル]** ウィンドウには、この要素のすべての CSS ルールが表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-210">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="38fc0-211">下にスクロールして、... コンテンツラッパークラスセレクターを見つけます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-211">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="38fc0-212">[... コンテンツ-ラッパー] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-212">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="38fc0-213">Page Inspector によって、このスタイル (.css) を定義する CSS ファイルが開き、対応する CSS スタイルが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-213">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![CSS ファイル](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

<span data-ttu-id="38fc0-215">次に、`background-color` の値を "red" に変更します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-215">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="38fc0-216">変更は、Page Inspector ブラウザーに直ちに表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-216">The change appears immediately in the Page Inspector browser.</span></span>

![Page Inspector ブラウザー](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a><span data-ttu-id="38fc0-218">CSS カラーピッカーの使用</span><span class="sxs-lookup"><span data-stu-id="38fc0-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="38fc0-219">次に、Page Inspector を使用して、既定のアプリケーションで強調表示されているテキストの CSS をすばやく検索して変更する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-219">Next, you'll learn how to use Page Inspector to quickly find and change the CSS for highlighted text in the default application.</span></span> <span data-ttu-id="38fc0-220">この例では、青の強調表示を希望せず、別の色に変更することを決定しました。</span><span class="sxs-lookup"><span data-stu-id="38fc0-220">In this example, you've decided that you don't like the blue highlighting and want to change it to another color.</span></span>

<span data-ttu-id="38fc0-221">**[検査]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-221">Click the **Inspect** button.</span></span>

![要素の検査](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

<span data-ttu-id="38fc0-223">Page Inspector ブラウザーウィンドウで、強調表示されている "ビデオ、チュートリアル、サンプル" テキストの上にマウスポインターを移動し、CSS の "mark" ラベルが表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-223">In the Page Inspector browser window, move the mouse pointer over the highlighted "videos, tutorials, and samples" text so that the CSS "mark" label appears.</span></span>

![マーク要素にマウスポインターを合わせる](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

<span data-ttu-id="38fc0-225">テキストをクリックして選択します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-225">Click the text to select it.</span></span> <span data-ttu-id="38fc0-226">対応する CSS マークセレクターが **[スタイル]** ウィンドウの下部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-226">The corresponding CSS mark selector appears at the bottom of the **Styles** window.</span></span>

![[スタイル] ウィンドウのマークセレクター](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

<span data-ttu-id="38fc0-228">[マーク] セレクターをクリックします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-228">Click the mark selector.</span></span> <span data-ttu-id="38fc0-229">これにより、web アプリケーションの *.css*ファイルが開きます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-229">This opens the *Site.css* file for the web application.</span></span> <span data-ttu-id="38fc0-230">[.Css] タブをクリックすると、セレクターに対応する CSS が強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-230">Click the Site.css tab, and the corresponding CSS for the selector is highlighted:</span></span>

![スタイルシートのマークセレクター](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

<span data-ttu-id="38fc0-232">背景色のプロパティを使用して、線を選択して削除します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-232">Select and remove the line with the background-color property.</span></span>

<span data-ttu-id="38fc0-233">新しい Visual Studio 2012 CSS カラーピッカーを使用し**て、[背景色**の設定] プロパティに新しい色を選択できるようになります。</span><span class="sxs-lookup"><span data-stu-id="38fc0-233">You will now use the new Visual Studio 2012 CSS color picker to choose a new color for the **mark** background-color property.</span></span>

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a><span data-ttu-id="38fc0-234">Visual Studio 2012 CSS カラーピッカーの使用</span><span class="sxs-lookup"><span data-stu-id="38fc0-234">Using the Visual Studio 2012 CSS Color Picker</span></span>

<span data-ttu-id="38fc0-235">Visual Studio 2012 の CSS エディターには、色の選択と挿入を簡単に行うことができるカラーピッカーが用意されています。</span><span class="sxs-lookup"><span data-stu-id="38fc0-235">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="38fc0-236">簡易カラーバーと "ポップアップ" ピッカーが用意されており、より細かい制御ができます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-236">It has a simple color bar and a "pop-down" picker that offers finer control.</span></span>

<span data-ttu-id="38fc0-237">カラーピッカーには標準の色パレットが含まれており、標準の色の名前、ハッシュコード、RGB、RGBA、HSL、および HSLA の色をサポートし、ドキュメントで最近使用した色の一覧を保持します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-237">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="38fc0-238">背景色のプロパティがの行で、「bc」と入力し、下矢印を1回押します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-238">On the line where the background-color property was, type "bc" and press the down arrow once.</span></span>

<span data-ttu-id="38fc0-239">ハイフンで区切られた各単語の最初の文字を "背景色" のようなプロパティに入力すると、IntelliSense によってリストがフィルター処理され、一致するプロパティのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-239">When you type the first character of each word in a hyphen-separated property like "background-color", IntelliSense filters the list for you to show only the properties that match:</span></span>

![Intellisense のフィルター処理された値](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

<span data-ttu-id="38fc0-241">ここで、コロンを入力します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-241">Now type a colon.</span></span> <span data-ttu-id="38fc0-242">この操作を行うと、完全な背景色のプロパティ名が挿入されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-242">When you do, the full background-color property name is inserted.</span></span> <span data-ttu-id="38fc0-243">「 **#** または**rgb (** )」と入力すると、カラーピッカーバーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-243">Type **#** or **rgb(**, and the color picker bar appears:</span></span>

![CSS カラーピッカーバー](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

<span data-ttu-id="38fc0-245">カラーピッカーバーがどのように動作するかを確認するには、マウスポインターで色をクリックするか、下方向キーを押してから、左右の方向キーを使用して色を走査します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-245">To see how the color picker bar works, click its colors with the mouse pointer, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="38fc0-246">色にアクセスすると、背景色のプロパティに対応する値がプレビューされます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-246">When you visit a color, the corresponding value for the background-color property is previewed:</span></span>

![背景色のプロパティ値のプレビュー](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

<span data-ttu-id="38fc0-248">この時点で、enter キーを押して値を選択し、セミコロン (;)を入力して、CSS エントリを完成させます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-248">At this point, you could press Enter to select the value and then a semicolon (;) to complete the CSS entry.</span></span> <span data-ttu-id="38fc0-249">ここでは、カラーピッカーのポップアップがどのように機能するかを確認できるように、次のセクションに進んでください。</span><span class="sxs-lookup"><span data-stu-id="38fc0-249">For now, go on to the next section so that you can see how the color picker pop-down works.</span></span>

#### <a name="using-the-color-picker-pop-down"></a><span data-ttu-id="38fc0-250">カラーピッカーのポップアップを使用する</span><span class="sxs-lookup"><span data-stu-id="38fc0-250">Using the Color Picker Pop-Down</span></span>

<span data-ttu-id="38fc0-251">カラーバーに探している色が正確でない場合は、カラーピッカーのポップアップを使用できます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-251">When the color bar doesn't have the exact color that you're looking for, you can use the color picker pop-down.</span></span>

<span data-ttu-id="38fc0-252">これを開くには、カラーバーの右端にある二重シェブロンをクリックするか、キーボードの下方向キーを1回または2回押します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-252">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS カラーピッカーのポップアップ](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

<span data-ttu-id="38fc0-254">右側の垂直バーから色をクリックします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-254">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="38fc0-255">これにより、メインウィンドウにその色のグラデーションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-255">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="38fc0-256">Enter キーを押して縦棒から直接色を選択するか、メインウィンドウ内の任意のポイントをクリックして有効桁数を高くします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-256">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="38fc0-257">使用する色がコンピューターの画面に表示される場合は (Visual Studio のユーザーインターフェイス内に存在する必要はありません)、右下にあるスポイトツールを使用して値をキャプチャできます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-257">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="38fc0-258">カラーピッカーの下部にあるスライダーを動かすことで、色の不透明度を変更することもできます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-258">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="38fc0-259">これにより、RGBA 形式は不透明度を表すことができるため、色の値が RGBA 値に変更されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-259">Doing so changes color values to RGBA values because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="38fc0-260">色を選択したら、enter キーを押し、セミコロンを入力して、*サイトの .css*ファイルの背景色のエントリを完成させます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-260">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="38fc0-261">Page Inspector 更新バー</span><span class="sxs-lookup"><span data-stu-id="38fc0-261">The Page Inspector Update Bar</span></span>

<span data-ttu-id="38fc0-262">Page Inspector は、直ちに、*サイトの .css*ファイル (またはアプリケーション内の任意のファイル) に対する変更を検出し、更新バーにアラートを表示します。</span><span class="sxs-lookup"><span data-stu-id="38fc0-262">Page Inspector immediately detects the change to the *Site.css* file (or to any file in the application) and displays an alert in an update bar.</span></span>

![更新バー](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

<span data-ttu-id="38fc0-264">すべてのファイルを保存して Page Inspector ブラウザーを更新するには、Ctrl + Alt + Enter キーを押すか、更新バーをクリックします。</span><span class="sxs-lookup"><span data-stu-id="38fc0-264">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="38fc0-265">強調表示色の変更がブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-265">The change in the highlight color appears in the browser:</span></span>

![強調表示色の変更](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a><span data-ttu-id="38fc0-267">Visual Studio 環境内から Page Inspector ブラウザーをすぐに更新することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="38fc0-267">Notice that you conveniently refreshed the Page Inspector browser right from within the Visual Studio environment.</span></span> <span data-ttu-id="38fc0-268">外部ブラウザーではなく Page Inspector を使用すると、web アプリケーションを開発するときにエディターを使用したままにすることができます。</span><span class="sxs-lookup"><span data-stu-id="38fc0-268">Using Page Inspector instead of an external browser lets you stay in the editor when you develop your web applications.</span></span>

## <a name="see-also"></a><span data-ttu-id="38fc0-269">参照</span><span class="sxs-lookup"><span data-stu-id="38fc0-269">See Also</span></span>

<span data-ttu-id="38fc0-270">[Page Inspector の概要](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector)(Channel 9 ビデオ)</span><span class="sxs-lookup"><span data-stu-id="38fc0-270">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 video)</span></span>

<span data-ttu-id="38fc0-271">[Page Inspector のエラーメッセージ](https://go.microsoft.com/?linkid=9813062)(MSDN)</span><span class="sxs-lookup"><span data-stu-id="38fc0-271">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
