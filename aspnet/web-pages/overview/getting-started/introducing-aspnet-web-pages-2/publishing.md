---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: ASP.NET Web Pages の概要 - WebMatrix を使用して、サイトの発行 |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft WebMatrix と ASP.NET Web Pages を紹介するチュートリアルのセットの最終回です。 T サイトを発行する方法について説明しています.
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: 49a841dbda183bf1d59153b83f694c9f517e0b94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514384"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a><span data-ttu-id="8c624-104">WebMatrix を使用してサイトを発行する-ASP.NET Web Pages の概要</span><span class="sxs-lookup"><span data-stu-id="8c624-104">Introducing ASP.NET Web Pages - Publishing a Site by Using WebMatrix</span></span>

<span data-ttu-id="8c624-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8c624-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8c624-106">このチュートリアルでは、Microsoft WebMatrix と ASP.NET Web Pages を紹介するチュートリアルのセットの最終回です。</span><span class="sxs-lookup"><span data-stu-id="8c624-106">This tutorial is the final installment in the tutorial set that introduces ASP.NET Web Pages and Microsoft WebMatrix.</span></span> <span data-ttu-id="8c624-107">これには、他のユーザーが操作できるように、サイトをインターネットに公開する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8c624-107">It discusses how to publish your site to the Internet so that others can work with it.</span></span> <span data-ttu-id="8c624-108">[ASP.NET Web ページサイトの一貫性のある検索を作成](https://go.microsoft.com/fwlink/?LinkId=251585)することによって、シリーズを完了していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="8c624-108">It assumes you have completed the series through [Creating a Consistent Look for ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=251585).</span></span>
> 
> <span data-ttu-id="8c624-109">使用して、サイトを発行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8c624-109">You'll learn how to publish your site using:</span></span>
> 
> - <span data-ttu-id="8c624-110">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8c624-110">Microsoft Azure</span></span>
> - <span data-ttu-id="8c624-111">Web ホスティング企業</span><span class="sxs-lookup"><span data-stu-id="8c624-111">Web Hosting Company</span></span>

## <a name="about-publishing-your-site"></a><span data-ttu-id="8c624-112">サイトの発行について</span><span class="sxs-lookup"><span data-stu-id="8c624-112">About Publishing Your Site</span></span>

<span data-ttu-id="8c624-113">ここでは、最大のページをテストするなど、ローカル コンピューター上のすべての作業を行っています。</span><span class="sxs-lookup"><span data-stu-id="8c624-113">Up to now, you've done all your work on a local computer, including testing your pages.</span></span> <span data-ttu-id="8c624-114">このように、<em>cshtml</em>ページを実行するには、WebMatrix に組み込まれている web サーバー (IIS Express) を使用しました。</span><span class="sxs-lookup"><span data-stu-id="8c624-114">To run your<em>.cshtml</em> pages, you've used the web server that's built into WebMatrix, namely IIS Express.</span></span> <span data-ttu-id="8c624-115">もちろんこと以外に作成したサイトを参照していないことができます。</span><span class="sxs-lookup"><span data-stu-id="8c624-115">But of course no one can see the site you've created except you.</span></span> <span data-ttu-id="8c624-116">他のユーザーが自分のサイトを使用できるように、インターネットに公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c624-116">To let others work with your site, you have to publish it to the Internet.</span></span>

<span data-ttu-id="8c624-117">公開されている web サーバーにまだアクセスできない限り、公開とは、*クラウドプラットフォーム*または*ホスティングプロバイダー*を持つアカウントが必要であることを意味します。</span><span class="sxs-lookup"><span data-stu-id="8c624-117">Unless you have access to a public web server already, publishing means that you have to have an account with a *cloud platform* or a *hosting provider*.</span></span> <span data-ttu-id="8c624-118">Microsoft Azure などのクラウド プラットフォームでは、アプリケーションのオンデマンド インフラストラクチャを提供します。</span><span class="sxs-lookup"><span data-stu-id="8c624-118">A cloud platform, such as Microsoft Azure, provides on-demand infrastructure for your applications.</span></span> <span data-ttu-id="8c624-119">ホスティング プロバイダーは、パブリックにアクセスできる web サーバーを所有しているとをレンタルするは、企業が、サイトの領域です。</span><span class="sxs-lookup"><span data-stu-id="8c624-119">A hosting provider is a company that owns publicly accessible web servers and that will rent you space for your site.</span></span> <span data-ttu-id="8c624-120">ホスティング プランの実行、ほんの数ドルから (または無料) を何百もの商用 web サイトの高ボリューム ドルの小規模なサイトです。</span><span class="sxs-lookup"><span data-stu-id="8c624-120">Hosting plans run from a few dollars a month (or even free) for small sites to many hundreds of dollars a month for high-volume commercial websites.</span></span>

> [!NOTE]
> <span data-ttu-id="8c624-121">インターネット サービスを自宅での取得に使用するインターネット サービス プロバイダー (ISP) 経由でパブリック web サーバーへのアクセスを使用するがあります。</span><span class="sxs-lookup"><span data-stu-id="8c624-121">You might have access to a public web server via the internet service provider (ISP) that you use to get internet service at home.</span></span> <span data-ttu-id="8c624-122">ただし、ホスティング プロバイダーは、ASP.NET Web Pages をサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c624-122">However, your hosting provider must support ASP.NET Web Pages.</span></span> <span data-ttu-id="8c624-123">多くの Isp がありませんが、チェックに値するは常にします。</span><span class="sxs-lookup"><span data-stu-id="8c624-123">Many ISPs don't, but it's always worth checking.</span></span>

<span data-ttu-id="8c624-124">発行する方法の概要について付与は、このチュートリアルでします。</span><span class="sxs-lookup"><span data-stu-id="8c624-124">In this tutorial, we'll give you an overview of how to publish.</span></span> <span data-ttu-id="8c624-125">すべてのホスティング プロバイダーのプロセスが少し異なるため、すべての正確な詳細を提供する実用的ではありません。</span><span class="sxs-lookup"><span data-stu-id="8c624-125">It's not practical to provide exact details for everything, because the process differs a bit for every hosting provider.</span></span> <span data-ttu-id="8c624-126">プロセスのしくみのことをお勧めできます。</span><span class="sxs-lookup"><span data-stu-id="8c624-126">But you'll get a good idea of how the process works.</span></span>

<span data-ttu-id="8c624-127">このチュートリアルには、4 つのセクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8c624-127">This tutorial contains four sections:</span></span>

1. [<span data-ttu-id="8c624-128">既定のページの設定</span><span class="sxs-lookup"><span data-stu-id="8c624-128">Setting up the default page</span></span>](#defaultpage)
2. <span data-ttu-id="8c624-129">発行 (次のいずれかを選択)</span><span class="sxs-lookup"><span data-stu-id="8c624-129">Publishing (choose one of the following)</span></span>  
 <span data-ttu-id="8c624-130">a.</span><span class="sxs-lookup"><span data-stu-id="8c624-130">a.</span></span> [<span data-ttu-id="8c624-131">Microsoft Azure にサイトを発行する</span><span class="sxs-lookup"><span data-stu-id="8c624-131">Publishing Your Site to Microsoft Azure</span></span>](#azure)  
 <span data-ttu-id="8c624-132">b.</span><span class="sxs-lookup"><span data-stu-id="8c624-132">b.</span></span> [<span data-ttu-id="8c624-133">Web ホスティング会社へのサイトの発行</span><span class="sxs-lookup"><span data-stu-id="8c624-133">Publishing Your Site to a Web Hosting Company</span></span>](#host)
3. [<span data-ttu-id="8c624-134">ライブサイトを更新しています: 再発行</span><span class="sxs-lookup"><span data-stu-id="8c624-134">Updating the Live Site: Republishing</span></span>](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a><span data-ttu-id="8c624-135">既定のページの設定</span><span class="sxs-lookup"><span data-stu-id="8c624-135">Setting up the default page</span></span>

<span data-ttu-id="8c624-136">ユーザーは、web サイトのベース アドレスに移動して、ユーザーに、サイトの既定のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-136">When a user navigates to the base address for your web site, the default page for your site is displayed to the user.</span></span> <span data-ttu-id="8c624-137">たとえば、既定の *.htm*が `www.contoso.com`のサイトの既定のページとして設定されている場合、`www.contoso.com` への移動は `www.contoso.com/Default.htm`への移動と同じです。</span><span class="sxs-lookup"><span data-stu-id="8c624-137">For example, when *Default.htm* is set as the default page for the site at `www.contoso.com`, then navigating to `www.contoso.com` is the same as navigating to `www.contoso.com/Default.htm`.</span></span>

<span data-ttu-id="8c624-138">現在、サイトでは既定のページとして**既定の cshtml**が使用されています。</span><span class="sxs-lookup"><span data-stu-id="8c624-138">Currently, your site uses **Default.cshtml** as the default page.</span></span> <span data-ttu-id="8c624-139">このページは、既定のページでは、問題ありませんが、このチュートリアルではないコンテンツを追加した、そのページに空白のページを表示するためです。</span><span class="sxs-lookup"><span data-stu-id="8c624-139">This page is fine for your default page, but in this tutorial you have not added any content to that page so it would display a blank page.</span></span> <span data-ttu-id="8c624-140">Default.cshtml を開き、内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8c624-140">Open Default.cshtml and replace the content with the following code.</span></span>

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

<span data-ttu-id="8c624-141">次に、サイトの公開の準備は。</span><span class="sxs-lookup"><span data-stu-id="8c624-141">Now your site is ready for publication.</span></span> <span data-ttu-id="8c624-142">最初に、サイトを Azure にデプロイする方法と、web サイトをホストにデプロイする方法が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-142">First, you will see how to deploy the site to Azure, and then how to deploy it to a web hosting company.</span></span> <span data-ttu-id="8c624-143">Web サイトのいずれか オプションはのみ、展開オプションのいずれかに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c624-143">Either option works for your web site, and you only need to follow one of the deployment options.</span></span>

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a><span data-ttu-id="8c624-144">Microsoft azure サイトの発行</span><span class="sxs-lookup"><span data-stu-id="8c624-144">Publishing Your Site to Microsoft Azure</span></span>

<span data-ttu-id="8c624-145">このチュートリアルでは最初に説明する Microsoft Azure には、サイトをデプロイする方法。</span><span class="sxs-lookup"><span data-stu-id="8c624-145">This tutorial will first show you how to deploy your site to Microsoft Azure.</span></span> <span data-ttu-id="8c624-146">Microsoft アカウントをサインインすることで、Azure で最大 10 個無料サイトを作成できます。</span><span class="sxs-lookup"><span data-stu-id="8c624-146">By signing in with a Microsoft account, you can create up to 10 free sites on Azure.</span></span> <span data-ttu-id="8c624-147">これらの無料サイトでは、サイトをテストする便利な手段を提供します。</span><span class="sxs-lookup"><span data-stu-id="8c624-147">These free sites provide a convenient way to test your sites.</span></span> <span data-ttu-id="8c624-148">この例のサイトを使用してすべての無料サイトを回避するには、後でいつでも削除できます。</span><span class="sxs-lookup"><span data-stu-id="8c624-148">You can always delete this example site later to avoid using all of your free sites.</span></span> <span data-ttu-id="8c624-149">数分で無料試用版のアカウントを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="8c624-149">You can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8c624-150">詳細については、「[Azure の無料試用版サイト](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c624-150">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

<span data-ttu-id="8c624-151">WebMatrix リボンで、 **[発行]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-151">In the WebMatrix ribbon, click the **Publish** button.</span></span>

![WebMatrix リボンで、'publish' ボタン](publishing/_static/image1.png)

<span data-ttu-id="8c624-153">**[サイトの発行]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-153">The **Publish Your Site** dialog box is displayed.</span></span> <span data-ttu-id="8c624-154">Microsoft アカウントにサインインしていない場合は、ダイアログボックスに**Azure の使用を開始**するリンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-154">If you have not signed in to your Microsoft account, the dialog box will contain a **Get started with Azure** link.</span></span> <span data-ttu-id="8c624-155">このリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-155">Click this link.</span></span>

![サイトを発行します。](publishing/_static/image2.png)

<span data-ttu-id="8c624-157">サインインしていない Microsoft アカウントに場合、もう一度サインインする機会が提供されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-157">If you have not signed in to a Microsoft account, you are again given the opportunity to sign in.</span></span> <span data-ttu-id="8c624-158">Azure でサイトを発行する Microsoft アカウントにサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c624-158">You must sign in to a Microsoft account to publish your site on Azure.</span></span>

![Sign In (Azure: サインイン)](publishing/_static/image3.png)

<span data-ttu-id="8c624-160">Microsoft アカウントにサインインした後は、ダイアログ ボックスには、Azure で新しいサイトを作成または Azure 上で、既存のサイトのいずれかに接続するリンクが含まれます。</span><span class="sxs-lookup"><span data-stu-id="8c624-160">After signing in to your Microsoft account, the dialog box contains links to create a new site on Azure or connect to one of your existing sites on Azure.</span></span>

![新しいサイトを作成します。](publishing/_static/image4.png)

<span data-ttu-id="8c624-162">**[新しいサイトの作成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8c624-162">Select **Create a new site**.</span></span>

<span data-ttu-id="8c624-163">プロジェクトに**webwebpagesmovies.azurewebsites.net**という名前を付けた場合は、サイトの既定の名前が使用されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-163">If you named your project **WebPagesMovies**, the default name for your site will be **webpagesmovies.azurewebsites.net**.</span></span> <span data-ttu-id="8c624-164">この既定の名前が最も高い利用できない、赤色の感嘆符で示されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-164">This default name is most likely not available, as indicated by the red exclamation mark.</span></span>

![既定の Web サイト名](publishing/_static/image5.png)

<span data-ttu-id="8c624-166">サイト名を利用可能なものに変更し、自分の場所に近い場所を選択します。</span><span class="sxs-lookup"><span data-stu-id="8c624-166">Change the site name to something that is available, and select a location that is close to your location.</span></span>

![変更されたサイト名](publishing/_static/image6.png)

<span data-ttu-id="8c624-168">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-168">Click **OK**.</span></span>

<span data-ttu-id="8c624-169">WebMatrix performss かどうか、サーバーは、サイトとの互換性を判断するテストをします。</span><span class="sxs-lookup"><span data-stu-id="8c624-169">WebMatrix performss a test to determine if the server is compatible with your site.</span></span>

![互換性のテスト](publishing/_static/image7.png)

<span data-ttu-id="8c624-171">**[続行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-171">Select **Continue**.</span></span>

<span data-ttu-id="8c624-172">互換性テストの結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-172">The results of the compatibility test are displayed.</span></span>

![互換性の結果](publishing/_static/image8.png)

<span data-ttu-id="8c624-174">**[続行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-174">Select **Continue**.</span></span>

<span data-ttu-id="8c624-175">WebMatrix には、ファイルおよびサイトにパブリッシュされるデータベースが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-175">WebMatrix displays the files and databases that will be published to the site.</span></span> <span data-ttu-id="8c624-176">これは、サイトを発行して初めてであるため、すべてのファイルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-176">Since this is the first time you are publishing the site, all of the files are listed.</span></span> <span data-ttu-id="8c624-177">発行する準備ができているファイルをオフにすることができます。</span><span class="sxs-lookup"><span data-stu-id="8c624-177">You can uncheck a file that is not ready to be published.</span></span> <span data-ttu-id="8c624-178">後続のパブリケーションで変更されたファイルのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-178">In the subsequent publications, only the files that have changed will be displayed.</span></span> <span data-ttu-id="8c624-179">「[ライブサイトの更新: 再パブリッシュ」を](#update)参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c624-179">See [Updating the Live Site: Republishing](#update).</span></span>

![[続行]](publishing/_static/image9.png)

<span data-ttu-id="8c624-181">**[続行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-181">Select **Continue**.</span></span>

<span data-ttu-id="8c624-182">サイトは、Azure にデプロイされたが後、は、デプロイが完了しているかを示すメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-182">After the site has been deployed to Azure, a message is displayed that indicates the deployment has completed.</span></span>

![発行の完了](publishing/_static/image10.png)

<span data-ttu-id="8c624-184">サイトとデータベースを Azure にパブリッシュされは、パブリックに利用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="8c624-184">Your site and database have been published to Azure, and are now available to the public.</span></span> <span data-ttu-id="8c624-185">発行が完了したら、およびデプロイするサイトが表示されますを示すメッセージ内のリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-185">Click the link in the message indicating publishing has completed, and you will now see your deployed site.</span></span> <span data-ttu-id="8c624-186">か、インターネットにアクセスできるすべてのユーザーが追加またはデータベース内のレコードを変更できます。</span><span class="sxs-lookup"><span data-stu-id="8c624-186">You or anyone with Internet access can add or modify records in the database.</span></span>

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a><span data-ttu-id="8c624-187">Web サイトをホストするサイトの発行</span><span class="sxs-lookup"><span data-stu-id="8c624-187">Publishing Your Site to a Web Hosting Company</span></span>

<span data-ttu-id="8c624-188">Azure に発行しない場合は、web ホスティング企業に代わりに、サイトを発行できます。</span><span class="sxs-lookup"><span data-stu-id="8c624-188">If you decide to not publish to Azure, you can instead publish your site to a web hosting company.</span></span>

<span data-ttu-id="8c624-189">**[Web ホスティングの検索]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-189">Click the **Find web hosting** link.</span></span>

![発行の設定 ダイアログ ボックスで、'web ホスティングの検索' ボタン](publishing/_static/image12.png)

<span data-ttu-id="8c624-191">ページに移動するには、Microsoft サイトを ASP.NET をサポートするホスティング プロバイダーの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="8c624-191">You go to a page on the Microsoft site that lists hosting providers that support ASP.NET.</span></span>

![Microsoft のサイトをホスティング プロバイダーの一覧を表示するページ](publishing/_static/image13.png)

<span data-ttu-id="8c624-193">当然ながら、知っておく、長期間に必要なホスティング機能正確に難しいことができます。</span><span class="sxs-lookup"><span data-stu-id="8c624-193">Obviously, it can be difficult to know now exactly what hosting features you might require over the long term.</span></span> <span data-ttu-id="8c624-194">次に、いくつかの考慮事項を示します。</span><span class="sxs-lookup"><span data-stu-id="8c624-194">Here are a couple of things to consider:</span></span>

- <span data-ttu-id="8c624-195">WebPagesMovies サイトのために、SQL Server は、多くの場合、余分なコストに個別のアドオンがありません。</span><span class="sxs-lookup"><span data-stu-id="8c624-195">For purposes of the WebPagesMovies site, you don't have to have a separate add-on for SQL Server, which often costs extra.</span></span> <span data-ttu-id="8c624-196">サイトには自己完結型である SQL Server Compact Edition を使用しています。</span><span class="sxs-lookup"><span data-stu-id="8c624-196">In your site, you're using SQL Server Compact Edition, which is self-contained.</span></span> <span data-ttu-id="8c624-197">ただし、将来の web サイト作業をいくつかの SQL サーバーへのアクセスを必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c624-197">However, you might need SQL Server access for some future website work you do.</span></span> <span data-ttu-id="8c624-198">可能性がある場合は、SQL Server の機能を後で追加できることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8c624-198">If you think you might, make sure that you can add SQL Server capability later.</span></span>
- <span data-ttu-id="8c624-199">ホスティング プロバイダーが Web 配置発行プロトコルをサポートするかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="8c624-199">Check whether the hosting provider supports the Web Deploy publishing protocol.</span></span> <span data-ttu-id="8c624-200">FTP プロトコルを使用して発行することができますが、Web Deploy を使用する方が便利です。</span><span class="sxs-lookup"><span data-stu-id="8c624-200">You can publish by using FTP protocol, but it's more convenient to use Web Deploy.</span></span>

<span data-ttu-id="8c624-201">一部のサイトでは、無料の試用期間を提供します。</span><span class="sxs-lookup"><span data-stu-id="8c624-201">Some sites offer a free trial period.</span></span> <span data-ttu-id="8c624-202">無料試用版が公開してください。 に適した方法と、WebMatrix と ASP.NET Web Pages を引き続き実験をホストしている間にします。</span><span class="sxs-lookup"><span data-stu-id="8c624-202">A free trial is a good way to try publishing and hosting while you're still experimenting with WebMatrix and ASP.NET Web Pages.</span></span>

<span data-ttu-id="8c624-203">1 つを選択します。</span><span class="sxs-lookup"><span data-stu-id="8c624-203">Pick one that you like.</span></span> <span data-ttu-id="8c624-204">このチュートリアルでは、会社、チュートリアルの作成中にユーザーが数か月の無料のサイトをホストできるようにする昇格されていたために DiscountASP.NET を選択します。</span><span class="sxs-lookup"><span data-stu-id="8c624-204">For this tutorial, we selected DiscountASP.NET, because while we were creating the tutorial, that company had a promotion that let people host a site free for a few months.</span></span>

> [!NOTE]
> <span data-ttu-id="8c624-205">このチュートリアルでは、ホスティング プロバイダーの任意は、上の他の会社を推薦として解釈しないでください。</span><span class="sxs-lookup"><span data-stu-id="8c624-205">Our choice of a hosting provider for this tutorial shouldn't be interpreted as an endorsement of that company over any other.</span></span> <span data-ttu-id="8c624-206">図では、いずれかを選択する必要があるいて、DiscountASP.NET は、パブリッシング用の ASP.NET Web ページおよび Web Deploy プロトコルをサポートする多くの企業の 1 つです。</span><span class="sxs-lookup"><span data-stu-id="8c624-206">But we had to pick one for illustration, and DiscountASP.NET is one of the many companies that supports ASP.NET Web Pages and the Web Deploy protocol for publishing.</span></span>

<span data-ttu-id="8c624-207">通常、ホスティング プロバイダーにサインアップしたら後、会社を送信するユーザー名とパスワード、web サーバーの URL を含む電子メールをします。</span><span class="sxs-lookup"><span data-stu-id="8c624-207">Typically, after you've signed up with the hosting provider, the company sends you an email that contains a user name and password, the URL of the web server, and so on.</span></span> <span data-ttu-id="8c624-208">ホスティング企業は、Web Deploy プロトコルをサポートする場合を含むファイルを発行の設定、または 1 つをダウンロードすることができますを送信する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8c624-208">If the hosting company supports Web Deploy protocol, they might send you a file that contains publish settings, or let you download one.</span></span> <span data-ttu-id="8c624-209">発行設定ファイルには、プロセスが簡略化します。</span><span class="sxs-lookup"><span data-stu-id="8c624-209">A publish settings file simplifies the process for you.</span></span>

<span data-ttu-id="8c624-210">サインアップし、発行する準備ができたら、WebMatrix リボンの **[発行]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-210">When you've signed up and are ready to publish, click the **Publish** button in the WebMatrix ribbon.</span></span> <span data-ttu-id="8c624-211">**[発行の設定]** ダイアログボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-211">The **Publish Settings** dialog box is displayed.</span></span>

<span data-ttu-id="8c624-212">ホスティングプロバイダーから発行設定ファイルが送信された場合は、 **[発行設定のインポート]** リンクをクリックして、ファイルをインポートします。</span><span class="sxs-lookup"><span data-stu-id="8c624-212">If the hosting provider sent you a publish settings file, click the **Import publish settings** link and import the file.</span></span> <span data-ttu-id="8c624-213">発行設定ファイルを持っていない場合は、ホスティング企業に電子メールを送信します。 値を使用して、フィールドに入力します。</span><span class="sxs-lookup"><span data-stu-id="8c624-213">If you don't have a publish settings file, fill in the fields by using the values that the hosting company sent you in email.</span></span> <span data-ttu-id="8c624-214">完了すると、 **[発行の設定]** ダイアログボックスは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="8c624-214">Here's what the **Publish Settings** dialog box might look like when you're done:</span></span>

![発行設定の [発行の設定] ダイアログ ボックスで入力します。](publishing/_static/image14.png)

<span data-ttu-id="8c624-216">**[接続の検証]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-216">Click **Validate Connection**.</span></span> <span data-ttu-id="8c624-217">問題がなければ、ダイアログボックスは**正常に接続されて**いることを示しています。これは、ホスティングプロバイダーのサーバーと通信できることを意味します。</span><span class="sxs-lookup"><span data-stu-id="8c624-217">If everything is ok, the dialog box reports **Connected successfully**, which means it can communicate with the hosting provider's server.</span></span>

![成功した場合のメッセージの発行の設定が正しい](publishing/_static/image15.png)

<span data-ttu-id="8c624-219">問題がある場合に問題が何を通知することをお勧めは WebMatrix 実行します。</span><span class="sxs-lookup"><span data-stu-id="8c624-219">If there's a problem, WebMatrix does its best to tell you what the problem is:</span></span>

![問題がある場合、エラー メッセージ発行の設定](publishing/_static/image16.png)

<span data-ttu-id="8c624-221">**[Save]** をクリックして設定を保存します。</span><span class="sxs-lookup"><span data-stu-id="8c624-221">Click **Save** to save your settings.</span></span> <span data-ttu-id="8c624-222">WebMatrix は、ホスティング サイトと正しく通信できることを確認するテストの実行に提供します。</span><span class="sxs-lookup"><span data-stu-id="8c624-222">WebMatrix offers to perform a test to make sure that it can communicate correctly with the hosting site:</span></span>

![公開プロセスのテストを実行するよう求めるメッセージ](publishing/_static/image17.png)

<span data-ttu-id="8c624-224">**[はい]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-224">Click **Yes**.</span></span> <span data-ttu-id="8c624-225">WebMatrix は、ホスティング プロバイダーにいくつかのサンプル ファイルをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="8c624-225">WebMatrix uploads some sample files to the hosting provider.</span></span> <span data-ttu-id="8c624-226">互換性テストを完了すると、WebMatrix、結果を報告します。</span><span class="sxs-lookup"><span data-stu-id="8c624-226">When the compatibility test is done, WebMatrix reports the results:</span></span>

![公開のテストの結果](publishing/_static/image18.png)

<span data-ttu-id="8c624-228">準備ができたら、 **[続行]** をクリックして、実際の発行プロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="8c624-228">If you're ready to go, go ahead and click **Continue** to start the publish process for real.</span></span> <span data-ttu-id="8c624-229">WebMatrix は、どのようなファイルが、サイト (現在、なし)、ホスト サーバー上に既にと公開プロセスのプレビューを示しますによって判別します。</span><span class="sxs-lookup"><span data-stu-id="8c624-229">WebMatrix figures out what files are in your site and are already on the host server (right now, none) and gives you a preview of the publish process:</span></span>

![発行プロセスをアップロードするファイルのプレビュー](publishing/_static/image19.png)

<span data-ttu-id="8c624-231">発行するファイルの一覧には、*ムービー*のように作成した web ページが含まれます。</span><span class="sxs-lookup"><span data-stu-id="8c624-231">The list of files to publish includes the web pages that you've created like *Movies.cshtml*.</span></span> <span data-ttu-id="8c624-232">一覧には、ヘルパーをインストールしたが、データベースの SQL Server Compact Edition を実行するファイルのファイルも含まれています。</span><span class="sxs-lookup"><span data-stu-id="8c624-232">The list also includes files for helpers that you've installed, the files to run SQL Server Compact Edition for your database, and so on.</span></span> <span data-ttu-id="8c624-233">最初の結果として、発行プロセスが大幅にすることができます。</span><span class="sxs-lookup"><span data-stu-id="8c624-233">As a result, the initial publish process can be substantial.</span></span>

<span data-ttu-id="8c624-234">**[続行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-234">Click **Continue**.</span></span> <span data-ttu-id="8c624-235">WebMatrix は、ホスティング プロバイダーのサーバーにファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="8c624-235">WebMatrix copies your files to the hosting provider's server.</span></span> <span data-ttu-id="8c624-236">完了したら、ステータス バーで、結果が報告されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-236">When it's done, the results are reported in the status bar:</span></span>

![発行プロセスが正常に完了すると、ステータス バー メッセージ](publishing/_static/image20.png)

<span data-ttu-id="8c624-238">ライブ サイトを表示するには、ステータス バーのリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-238">To see your live site, click the link in the status bar.</span></span> <span data-ttu-id="8c624-239">URL に*ムービー*を追加すると、作成した*ムービーの cshtml*ファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c624-239">Add *Movies* to the URL, and you'll see the *Movies.cshtml* file that you created:</span></span>

![映画 ページを示すライブ サイト](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a><span data-ttu-id="8c624-241">ライブ サイトを更新しています再パブリッシュ。</span><span class="sxs-lookup"><span data-stu-id="8c624-241">Updating the Live Site: Republishing</span></span>

<span data-ttu-id="8c624-242">(Azure または web ホスティング会社のいずれかに) サイトを発行したら、コンピューター上のバージョンとサービスプロバイダーのバージョン &mdash; 2 つのコピーがあります。</span><span class="sxs-lookup"><span data-stu-id="8c624-242">Once you've published your site (to either Azure or a web hosting company), there are two copies of it &mdash; the version on your computer and the version on the service provider.</span></span> <span data-ttu-id="8c624-243">サイトの開発を続行したいでしょう (他に何もしない場合、次のチュートリアルのセットの一部として)。</span><span class="sxs-lookup"><span data-stu-id="8c624-243">You'll probably want to continue developing the site (if nothing else, as part of the next tutorial set).</span></span> <span data-ttu-id="8c624-244">実行すると、サービス プロバイダーにお使いのコンピューターからの変更をコピーするには、サイトを再発行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c624-244">When you do, you have to republish your site in order to copy changes from your computer to the service provider.</span></span> <span data-ttu-id="8c624-245">WebMatrix で、発行プロセスでは、サイトで変更されたファイルを判断でき、それらのファイルだけを公開することができます。</span><span class="sxs-lookup"><span data-stu-id="8c624-245">The publish process in WebMatrix can determine what files have changed on your site and publish just those files.</span></span>

<span data-ttu-id="8c624-246">再パブリッシュのしくみを確認するに*は、del サイトを*開き、少し変更を加えてから、ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="8c624-246">To see how republishing works, open the *Movies.cshtml* site, make some small change, and then save the file.</span></span> <span data-ttu-id="8c624-247">たとえば、タイトルを `Movies - Updated`に変更します。</span><span class="sxs-lookup"><span data-stu-id="8c624-247">For example, change the title to `Movies - Updated`.</span></span>

<span data-ttu-id="8c624-248">リボンの **[発行]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-248">Click the **Publish** button in the ribbon.</span></span> <span data-ttu-id="8c624-249">WebMatrix は、何が変更され、それを発行するファイルのプレビューが表示を決定します。</span><span class="sxs-lookup"><span data-stu-id="8c624-249">WebMatrix determines what's changed and shows you a preview of the files it will publish.</span></span>

![変更を示す [発行] ダイアログ ボックスのファイルを再パブリッシュの準備が完了します。](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> <span data-ttu-id="8c624-251">既定では、WebMatrix は、サイトを初めて発行するときにのみデータベース ( *.sdf*ファイル) を発行します。</span><span class="sxs-lookup"><span data-stu-id="8c624-251">By default, WebMatrix publishes your database (*.sdf* file) only the first time you publish the site.</span></span> <span data-ttu-id="8c624-252">サイトを発行し、ユーザーが web サイトと対話する、ライブ サイトのデータベースでは通常、サイトの実際のデータがあります。</span><span class="sxs-lookup"><span data-stu-id="8c624-252">Once your site is published and people are interacting with the website, the database on the live site typically has the site's real data.</span></span> <span data-ttu-id="8c624-253">ライブデータベースを、コンピューター上の *.sdf*ファイルで上書きしないように注意する必要があります。このファイルには、通常、テストデータのみが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8c624-253">You have to be very careful not to overwrite the live database with the *.sdf* file that's on your computer, which usually contains only test data.</span></span> <span data-ttu-id="8c624-254">このため、[発行] によって**リモートデータベースが上書きさ**れることがわかります。また、既定では、[ *web* ] のチェックボックスがオフになっています。</span><span class="sxs-lookup"><span data-stu-id="8c624-254">That's why you see the warning **Publishing will overwrite any remote databases**, and why the check box for *WebPagesMovies.sdf* is cleared by default.</span></span>

<span data-ttu-id="8c624-255">**[続行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c624-255">Click **Continue**.</span></span> <span data-ttu-id="8c624-256">WebMatrix では、変更されたファイルを発行して、最初に発行したときと同じように、成功のメッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="8c624-256">WebMatrix publishes the changed files and shows you a success message, like it did the first time you published.</span></span>

<span data-ttu-id="8c624-257">(することができますのリンクをクリック、成功メッセージがまだ表示されている場合)、ライブ サイトに移動し、変更が公開されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8c624-257">Go to the live site (you can click the link in the success message if it's still showing) and verify that your change has been published.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="8c624-258">**ファイルのリモート編集**</span><span class="sxs-lookup"><span data-stu-id="8c624-258">**Editing Files Remotely**</span></span>
> 
> <span data-ttu-id="8c624-259">代わりに、サイトを変更して、再パブリッシュし、WebMatrix で直接、リモート ファイルを編集できます。</span><span class="sxs-lookup"><span data-stu-id="8c624-259">As an alternative to changing your site and then republishing, you can edit remote files directly in WebMatrix.</span></span> <span data-ttu-id="8c624-260">このシナリオで、サービス プロバイダー上にあるファイルを開くし、WebMatrix のダウンロードを編集するためのコピー。</span><span class="sxs-lookup"><span data-stu-id="8c624-260">In this scenario, you open a file that's on the service provider, and WebMatrix downloads a copy of it for you to edit.</span></span> <span data-ttu-id="8c624-261">ファイルを保存するたびに、WebMatrix は、変更をサイトに送信します。</span><span class="sxs-lookup"><span data-stu-id="8c624-261">Every time you save the file, WebMatrix sends the changes to the site.</span></span>
> 
> <span data-ttu-id="8c624-262">ライブ サイトを変更する簡単な方法は、リモートを編集します。</span><span class="sxs-lookup"><span data-stu-id="8c624-262">Remote editing is an easy way to make changes to your live site.</span></span> <span data-ttu-id="8c624-263">ただし、この方法が行った変更は、ローカル サイト内のファイルと同期されていません。</span><span class="sxs-lookup"><span data-stu-id="8c624-263">However, the changes you make this way aren't synchronized with the files in your local site.</span></span> <span data-ttu-id="8c624-264">リモート サイトとローカルのファイルを同期するには、リモート ファイルをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="8c624-264">To synchronize the local files with the remote site, you can download the remote files.</span></span> <span data-ttu-id="8c624-265">このプロセスはように動作の公開、除く逆の順序で。</span><span class="sxs-lookup"><span data-stu-id="8c624-265">This process works much like publishing, except in reverse.</span></span>
> 
> <span data-ttu-id="8c624-266">リモート編集、およびリモート ダウンロード機能 WebMatrix のこちらの詳細については説明はしません。</span><span class="sxs-lookup"><span data-stu-id="8c624-266">We won't describe more about the remote-editing and remote-download facilities of WebMatrix here.</span></span> <span data-ttu-id="8c624-267">複数の人が別のコンピューターで同じサイトで動作する必要がある場合に非常に便利です。</span><span class="sxs-lookup"><span data-stu-id="8c624-267">They're quite useful if multiple people have to work on the same site on different computers.</span></span> <span data-ttu-id="8c624-268">詳細については、「 [WebMatrix 2 Beta を使用したリモートサイトの発行と編集](https://go.microsoft.com/fwlink/?LinkId=251591)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c624-268">For more information, see [Publish and Edit a Remote Site with WebMatrix 2 Beta](https://go.microsoft.com/fwlink/?LinkId=251591).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8c624-269">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="8c624-269">Additional Resources</span></span>

- <span data-ttu-id="8c624-270">[ASP.NET WebMatrix ASP.NET Web ページフォーラム](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages)。質問を投稿して回答を得ることができます。</span><span class="sxs-lookup"><span data-stu-id="8c624-270">[ASP.NET WebMatrix ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), a great place to post questions and get answers.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8c624-271">[[戻る]](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="8c624-271">[Previous](layouts.md)</span></span>
