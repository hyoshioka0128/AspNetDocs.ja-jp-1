---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 新しいASP.NET MVC プロジェクトを作成する |マイクロソフトドキュメント
author: rick-anderson
description: 手順 1 では、NerdDinner アプリケーションの基本構造を配置する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541482"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="1799e-103">新しい ASP.NET MVC プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="1799e-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="1799e-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1799e-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="1799e-105">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="1799e-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="1799e-106">これは、mvc 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NETの手順 1 です。</span><span class="sxs-lookup"><span data-stu-id="1799e-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="1799e-107">手順 1 では、NerdDinner アプリケーションの基本構造を配置する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="1799e-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="1799e-108">mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="1799e-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="1799e-109">NerdDinner ステップ 1:&gt;ファイル - 新しいプロジェクト</span><span class="sxs-lookup"><span data-stu-id="1799e-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="1799e-110">NerdDinner アプリケーションは、Visual Studio 2008 または無料の Visual Web 開発者 2008 Express 内の **[ファイル -&gt;新しいプロジェクト**] メニュー項目を選択して開始します。</span><span class="sxs-lookup"><span data-stu-id="1799e-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="1799e-111">これにより、「新規プロジェクト」ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1799e-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="1799e-112">新しいASP.NETのMVCアプリケーションを作成するには、ダイアログの左側にある「Web」ノードを選択し、右側にある「ASP.NETMVC Webアプリケーション」プロジェクトテンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="1799e-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="1799e-113">*重要: MVC ASP.NETダウンロードしてインストールしたことを確認してください- そうでなければ、[新しいプロジェクト] ダイアログに表示されません。まだインストールしていない場合は[、Microsoft Web プラットフォーム インストーラー](https://www.microsoft.com/web/downloads/platform.aspx)の V2 を使用できます (ASP.NET MVC は「Web&gt;プラットフォーム - フレームワークとランタイム」セクションで利用できます)。*</span><span class="sxs-lookup"><span data-stu-id="1799e-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="1799e-114">新しいプロジェクトに"NerdDinner"を作成し、「OK」ボタンをクリックして作成します。</span><span class="sxs-lookup"><span data-stu-id="1799e-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="1799e-115">「OK」をクリックすると、Visual Studio は追加のダイアログを表示し、必要に応じて新しいアプリケーションの単体テスト プロジェクトを作成するよう求められます。</span><span class="sxs-lookup"><span data-stu-id="1799e-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="1799e-116">この単体テスト プロジェクトでは、アプリケーションの機能と動作を検証する自動テストを作成できます (このチュートリアルの後半で説明する方法について説明します)。</span><span class="sxs-lookup"><span data-stu-id="1799e-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="1799e-117">上記のダイアログボックスの「テストフレームワーク」ドロップダウンには、マシンにインストールされているMVC単体テストプロジェクトテンプレートASP.NET使用可能なすべてのデータが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1799e-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="1799e-118">バージョンは、NUnit、MBUnit、および XUnit 用にダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="1799e-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="1799e-119">組み込みの Visual Studio 単体テスト フレームワークもサポートされています。</span><span class="sxs-lookup"><span data-stu-id="1799e-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="1799e-120">*注: Visual Studio 単体テスト フレームワークは、Visual Studio 2008 プロフェッショナルおよび上位バージョンでのみ使用できます。VS 2008 標準版またはビジュアル Web 開発者 2008 Express を使用している場合は、このダイアログを表示するには、ASP.NET MVC 用の NUnit、MBUnit または XUnit 拡張機能をダウンロードしてインストールする必要があります。テスト フレームワークがインストールされていない場合、ダイアログは表示されません。*</span><span class="sxs-lookup"><span data-stu-id="1799e-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="1799e-121">作成するテスト プロジェクトには既定の "NerdDinner.Tests" 名を使用し、"Visual Studio 単体テスト" フレームワーク オプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="1799e-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="1799e-122">「OK」ボタンをクリックすると、Visual Studio は 2 つのプロジェクト (Web アプリケーション用と単体テスト用のプロジェクト) を含むソリューションを作成します。</span><span class="sxs-lookup"><span data-stu-id="1799e-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="1799e-123">NerdDinner ディレクトリ構造の確認</span><span class="sxs-lookup"><span data-stu-id="1799e-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="1799e-124">Visual Studio で新しい ASP.NET MVC アプリケーションを作成すると、プロジェクトにファイルとディレクトリが自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="1799e-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="1799e-125">既定では、mvc プロジェクトASP.NET 6 つの最上位ディレクトリがあります。</span><span class="sxs-lookup"><span data-stu-id="1799e-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="1799e-126">**ディレクトリ**</span><span class="sxs-lookup"><span data-stu-id="1799e-126">**Directory**</span></span> | <span data-ttu-id="1799e-127">**目的**</span><span class="sxs-lookup"><span data-stu-id="1799e-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="1799e-128">**/コントローラ**</span><span class="sxs-lookup"><span data-stu-id="1799e-128">**/Controllers**</span></span> | <span data-ttu-id="1799e-129">URL 要求を処理するコントローラー クラスを配置する場所</span><span class="sxs-lookup"><span data-stu-id="1799e-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="1799e-130">**/モデル**</span><span class="sxs-lookup"><span data-stu-id="1799e-130">**/Models**</span></span> | <span data-ttu-id="1799e-131">データを表し、操作するクラスを配置する場所</span><span class="sxs-lookup"><span data-stu-id="1799e-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="1799e-132">**/ビュー**</span><span class="sxs-lookup"><span data-stu-id="1799e-132">**/Views**</span></span> | <span data-ttu-id="1799e-133">出力のレンダリングを担当する UI テンプレート ファイルを配置する場所</span><span class="sxs-lookup"><span data-stu-id="1799e-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="1799e-134">**/スクリプト**</span><span class="sxs-lookup"><span data-stu-id="1799e-134">**/Scripts**</span></span> | <span data-ttu-id="1799e-135">JavaScript ライブラリ ファイルとスクリプト (.js) を配置する場所</span><span class="sxs-lookup"><span data-stu-id="1799e-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="1799e-136">**/コンテンツ**</span><span class="sxs-lookup"><span data-stu-id="1799e-136">**/Content**</span></span> | <span data-ttu-id="1799e-137">CSS ファイルとイメージ ファイル、およびその他の非動的/非 JavaScript コンテンツを配置する場所</span><span class="sxs-lookup"><span data-stu-id="1799e-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="1799e-138">**/アプリ\_データ**</span><span class="sxs-lookup"><span data-stu-id="1799e-138">**/App\_Data**</span></span> | <span data-ttu-id="1799e-139">読み取り/書き込み対象のデータ ファイルを格納する場所。</span><span class="sxs-lookup"><span data-stu-id="1799e-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="1799e-140">ASP.NET MVC はこの構造体を必要としません。</span><span class="sxs-lookup"><span data-stu-id="1799e-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="1799e-141">実際、大規模なアプリケーションを使用する開発者は、通常、アプリケーションを複数のプロジェクトに分割して管理しやすくします (たとえば、データ モデル クラスは、Web アプリケーションとは別のクラス ライブラリ プロジェクトに配置されることがよくあります)。</span><span class="sxs-lookup"><span data-stu-id="1799e-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="1799e-142">しかし、既定のプロジェクト構造は、アプリケーションの問題を明確に保つために使用できる既定のディレクトリ規則を提供します。</span><span class="sxs-lookup"><span data-stu-id="1799e-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="1799e-143">/Controllers ディレクトリを展開すると、Visual Studio が 2 つのコント ローラー クラスを追加していることがわかります - ホーム コント ローラーとアカウント コント ローラー - 既定では、プロジェクトに。</span><span class="sxs-lookup"><span data-stu-id="1799e-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="1799e-144">/Views ディレクトリを展開すると、3 つのサブディレクトリ (/ホーム、/アカウント、/Shared) と、その中のいくつかのテンプレート ファイルが既定でプロジェクトに追加されています。</span><span class="sxs-lookup"><span data-stu-id="1799e-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="1799e-145">/Content ディレクトリと /Scripts ディレクトリを展開すると、サイト上のすべての HTML のスタイルを設定するために使用される Site.css ファイルと、アプリケーション内で AJAX と jQuery のサポートASP.NET可能な JavaScript ライブラリが見つかります。</span><span class="sxs-lookup"><span data-stu-id="1799e-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="1799e-146">NerdDinner.Tests プロジェクトを展開すると、コントローラー クラスの単体テストを含む 2 つのクラスが見つかります。</span><span class="sxs-lookup"><span data-stu-id="1799e-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="1799e-147">Visual Studio によって追加されたこれらの既定のファイルは、作業アプリケーションの基本的な構造を提供します - ホーム ページ、ページ、アカウントログイン/ログアウト/登録ページ、および未処理のエラー ページ (すべてワイヤーアップされ、そのまま作業) を完了します。</span><span class="sxs-lookup"><span data-stu-id="1799e-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="1799e-148">NerdDinner アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="1799e-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="1799e-149">[**デバッグ開始デバッグ]&gt;** メニュー項目または [デバッグなしのデバッグ-**&gt;デバッグなしの開始**] メニュー項目を選択して、プロジェクトを実行できます。</span><span class="sxs-lookup"><span data-stu-id="1799e-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="1799e-150">これにより、Visual Studio に付属の組み込みの ASP.NET Web サーバーが起動し、アプリケーションが実行されます。</span><span class="sxs-lookup"><span data-stu-id="1799e-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="1799e-151">以下は、新しいプロジェクトのホームページ (URL: "/") を実行する場合のページです。</span><span class="sxs-lookup"><span data-stu-id="1799e-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="1799e-152">[情報] タブをクリックすると、次のページが表示されます (URL: "/ホーム/約")。</span><span class="sxs-lookup"><span data-stu-id="1799e-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="1799e-153">右上の [ログオン] リンクをクリックすると、ログイン ページに移動します (URL: "/アカウント/LogOn")</span><span class="sxs-lookup"><span data-stu-id="1799e-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="1799e-154">ログインアカウントがない場合は、登録リンク(URL:"/アカウント/登録")をクリックして作成できます。</span><span class="sxs-lookup"><span data-stu-id="1799e-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="1799e-155">新しいプロジェクトを作成するときに、上記のホーム、概要、およびログアウト/登録機能を実装するコードが既定で追加されました。</span><span class="sxs-lookup"><span data-stu-id="1799e-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="1799e-156">アプリケーションの出発点として使用します。</span><span class="sxs-lookup"><span data-stu-id="1799e-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="1799e-157">NerdDinner アプリケーションのテスト</span><span class="sxs-lookup"><span data-stu-id="1799e-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="1799e-158">プロフェッショナル エディションまたはそれ以降のバージョンの Visual Studio 2008 を使用している場合は、Visual Studio 内で組み込みの単体テスト IDE サポートを使用してプロジェクトをテストできます。</span><span class="sxs-lookup"><span data-stu-id="1799e-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="1799e-159">上記のオプションのいずれかを選択すると、IDE 内の [テスト結果] ウィンドウが開き、組み込み機能をカバーする新しいプロジェクトに含まれる 27 の単体テストで合格/不合格のステータスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1799e-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="1799e-160">このチュートリアルの後半で、自動テストについて詳しく説明し、実装するアプリケーションの機能をカバーする追加の単体テストを追加します。</span><span class="sxs-lookup"><span data-stu-id="1799e-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="1799e-161">次の手順</span><span class="sxs-lookup"><span data-stu-id="1799e-161">Next Step</span></span>

<span data-ttu-id="1799e-162">これで、基本的なアプリケーション構造が整いました。</span><span class="sxs-lookup"><span data-stu-id="1799e-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="1799e-163">それでは、アプリケーション[データを格納するデータベースを作成](create-a-database.md)しましょう。</span><span class="sxs-lookup"><span data-stu-id="1799e-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1799e-164">[前へ](introducing-the-nerddinner-tutorial.md)
> [次へ](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="1799e-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
