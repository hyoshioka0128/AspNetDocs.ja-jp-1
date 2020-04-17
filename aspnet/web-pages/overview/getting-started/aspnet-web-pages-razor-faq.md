---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET ウェブページ (カミソリ) に関するよくある質問 |マイクロソフトドキュメント
author: Rick-Anderson
description: この記事では、web ページ (Razor) と WebMatrix に関してよく寄せられる質問ASP.NET一覧を示します。 チュートリアルで使用されるソフトウェアバージョンは、Web ページASP.NET(R..
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: a312d1327bc88e721bf7fc7459e420e3f582c88d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543705"
---
# <a name="aspnet-web-pages-razor-faq"></a><span data-ttu-id="757a5-104">ASP.NET Web ページ (Razor) のよくあるご質問</span><span class="sxs-lookup"><span data-stu-id="757a5-104">ASP.NET Web Pages (Razor) FAQ</span></span>

<span data-ttu-id="757a5-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="757a5-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> > [!NOTE] 
> > <span data-ttu-id="757a5-106">WebMatrix は、web ページをASP.NETするための統合開発環境として推奨されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="757a5-106">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="757a5-107">[Visual Studio](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio)またはビジュアル[スタジオ コードを](https://code.visualstudio.com/)使用する 。</span><span class="sxs-lookup"><span data-stu-id="757a5-107">Use [Visual Studio](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
>
> <span data-ttu-id="757a5-108">この記事では、web ページ (Razor) と WebMatrix に関してよく寄せられる質問ASP.NET一覧を示します。</span><span class="sxs-lookup"><span data-stu-id="757a5-108">This article lists some frequently asked questions about ASP.NET Web Pages (Razor) and WebMatrix.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="757a5-109">チュートリアルで使用するソフトウェアバージョン</span><span class="sxs-lookup"><span data-stu-id="757a5-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="757a5-110">ASP.NET ウェブページ (カミソリ) 3</span><span class="sxs-lookup"><span data-stu-id="757a5-110">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="757a5-111">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="757a5-111">Visual Studio 2013</span></span>
> - <span data-ttu-id="757a5-112">ウェブマトリックス 3</span><span class="sxs-lookup"><span data-stu-id="757a5-112">WebMatrix 3</span></span>
>   
> 
> <span data-ttu-id="757a5-113">このチュートリアルは、web ページ 2、Web マトリックス 2、および Visual Studio 2012 ASP.NETでも動作します。</span><span class="sxs-lookup"><span data-stu-id="757a5-113">This tutorial also works with ASP.NET Web Pages 2, WebMatrix 2, and Visual Studio 2012.</span></span>

- [<span data-ttu-id="757a5-114">ASP.NET Web ページ、ASP.NET Web フォーム、および ASP.NET MVC の違いは何ですか。</span><span class="sxs-lookup"><span data-stu-id="757a5-114">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [<span data-ttu-id="757a5-115">Web ページを操作するためには、WebMatrix が必要ですか?</span><span class="sxs-lookup"><span data-stu-id="757a5-115">Do I need WebMatrix in order to work with Web Pages?</span></span>](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [<span data-ttu-id="757a5-116">Web ページ上ASP.NET Web フォーム コントロールを使用できますか。</span><span class="sxs-lookup"><span data-stu-id="757a5-116">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [<span data-ttu-id="757a5-117">WebMatrix を使用せずに、ASP.NET Web ページ サイトを展開できますか。</span><span class="sxs-lookup"><span data-stu-id="757a5-117">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [<span data-ttu-id="757a5-118">ログインをサポートするには、Web セキュリティ ヘルパーを使用する必要がありますか?</span><span class="sxs-lookup"><span data-stu-id="757a5-118">Do I have to use the WebSecurity helper to support logins?</span></span>](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [<span data-ttu-id="757a5-119">web ページASP.NET HTML5 をサポートしていますか?</span><span class="sxs-lookup"><span data-stu-id="757a5-119">Does ASP.NET Web Pages support HTML5?</span></span>](#Does_ASP.NET_Web_Pages_support_HTML5)
- [<span data-ttu-id="757a5-120">ウェブページでJavaScriptとjQueryを使用できますか?</span><span class="sxs-lookup"><span data-stu-id="757a5-120">Can I use JavaScript and jQuery with Web Pages?</span></span>](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [<span data-ttu-id="757a5-121">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="757a5-121">Additional Resources</span></span>](#AdditionalResources)

<span data-ttu-id="757a5-122">エラーやその他の問題に関する質問については[、「web ページ (Razor) トラブルシューティング ガイドASP.NET」](https://go.microsoft.com/fwlink/?LinkId=253001)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="757a5-122">For questions about errors and other issues, see the [ASP.NET Web Pages (Razor) Troubleshooting Guide](https://go.microsoft.com/fwlink/?LinkId=253001).</span></span>

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a><span data-ttu-id="757a5-123">ASP.NET Web ページ、ASP.NET Web フォーム、および ASP.NET MVC の違いは何ですか。</span><span class="sxs-lookup"><span data-stu-id="757a5-123">What's the difference between ASP.NET Web Pages, ASP.NET Web Forms, and ASP.NET MVC?</span></span>

<span data-ttu-id="757a5-124">3 つとも、動的な Web アプリケーションを作成するためのASP.NETテクノロジーです。</span><span class="sxs-lookup"><span data-stu-id="757a5-124">All three are ASP.NET technologies for creating dynamic web applications:</span></span>

- <span data-ttu-id="757a5-125">web ページASP.NET、動的な (サーバー側) コードとデータベースへのアクセスを HTML ページに追加することに重点を置き、簡単で軽量な構文を備えています。</span><span class="sxs-lookup"><span data-stu-id="757a5-125">ASP.NET Web Pages focuses on adding dynamic (server-side) code and database access to HTML pages, and features simple and lightweight syntax.</span></span>
- <span data-ttu-id="757a5-126">ASP.NET Web フォームは、ページ オブジェクト モデルと従来のウィンドウ型コントロール (ボタン、リストなど) に基づいています。</span><span class="sxs-lookup"><span data-stu-id="757a5-126">ASP.NET Web Forms is based on a page object model and traditional window-type controls (buttons, lists, etc.).</span></span> <span data-ttu-id="757a5-127">Web フォームでは、クライアント ベース (Windows フォーム) の開発に慣れたユーザーになじみのあるイベント ベースのモデルを使用します。</span><span class="sxs-lookup"><span data-stu-id="757a5-127">Web Forms uses an event-based model that's familiar to those who've worked with client-based (Windows forms) development.</span></span>
- <span data-ttu-id="757a5-128">mvc ASP.NET、ASP.NETのモデル ビュー コント ローラー パターンを実装します。</span><span class="sxs-lookup"><span data-stu-id="757a5-128">ASP.NET MVC implements the model-view-controller pattern for ASP.NET.</span></span> <span data-ttu-id="757a5-129">「懸念事項の分離」(処理、データ、および UI レイヤー)に重点が置かれています。</span><span class="sxs-lookup"><span data-stu-id="757a5-129">The emphasis is on "separation of concerns" (processing, data, and UI layers).</span></span>

<span data-ttu-id="757a5-130">3 つのフレームワークはすべて完全にサポートされており、ASP.NET チームによって引き続き開発されています。</span><span class="sxs-lookup"><span data-stu-id="757a5-130">All three frameworks are fully supported and continue to be developed by the ASP.NET team.</span></span> <span data-ttu-id="757a5-131">一般に、どのフレームワークを使用するかは、バックグラウンドとASP.NETの経験によって異なります。</span><span class="sxs-lookup"><span data-stu-id="757a5-131">In general, the choice of which framework to use depends on your background and experience with ASP.NET.</span></span>

<span data-ttu-id="757a5-132">特にASP.NET Web ページは、HTML を既に知っているユーザーが、ページにサーバー処理を簡単に追加できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="757a5-132">ASP.NET Web Pages in particular was designed to make it easy for people who already know HTML to add server processing to their pages.</span></span> <span data-ttu-id="757a5-133">プログラミングが初心者の学生、愛好家、一般的な人々には良い選択です。</span><span class="sxs-lookup"><span data-stu-id="757a5-133">It's a good choice for students, hobbyists, people in general who are new to programming.</span></span> <span data-ttu-id="757a5-134">また、non-ASP.NETの Web テクノロジの経験を持つ開発者にも適しています。</span><span class="sxs-lookup"><span data-stu-id="757a5-134">It can also be a good choice for developers who have experience with non-ASP.NET web technologies.</span></span>

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a><span data-ttu-id="757a5-135">Web ページを操作するためには、WebMatrix が必要ですか?</span><span class="sxs-lookup"><span data-stu-id="757a5-135">Do I need WebMatrix in order to work with Web Pages?</span></span>

<span data-ttu-id="757a5-136">いいえ。</span><span class="sxs-lookup"><span data-stu-id="757a5-136">No.</span></span> <span data-ttu-id="757a5-137">WebMatrix は、web ページをASP.NETするための統合開発環境として推奨されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="757a5-137">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="757a5-138">[Visual Studio](program-asp-net-web-pages-in-visual-studio.md)またはビジュアル[スタジオ コードを](https://code.visualstudio.com/)使用する 。</span><span class="sxs-lookup"><span data-stu-id="757a5-138">Use [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>

<span data-ttu-id="757a5-139">Visual Studio または Visual Studio コードを使用しない場合は[、Microsoft Web プラットフォーム インストーラー](https://www.microsoft.com/web/downloads/platform.aspx)を使用してコンポーネント製品を個別にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="757a5-139">If you don't want to use either Visual Studio or Visual Studio Code, you can install the component products individually using [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span> <span data-ttu-id="757a5-140">次の製品が必要です。</span><span class="sxs-lookup"><span data-stu-id="757a5-140">You need the following products:</span></span>

- <span data-ttu-id="757a5-141">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="757a5-141">Microsoft .NET Framework 4.5</span></span>
- <span data-ttu-id="757a5-142">ASP.NET MVC 5 (ASP.NET Web ページ フレームワークもインストール)</span><span class="sxs-lookup"><span data-stu-id="757a5-142">ASP.NET MVC 5 (which installs the ASP.NET Web Pages framework as well)</span></span>
- <span data-ttu-id="757a5-143">IIS エクスプレス (Web サーバー)</span><span class="sxs-lookup"><span data-stu-id="757a5-143">IIS Express (the web server)</span></span>
- <span data-ttu-id="757a5-144">コンパクト 4.0 (データベース)</span><span class="sxs-lookup"><span data-stu-id="757a5-144">Microsoft SQL Server Compact 4.0 (the database)</span></span>

<span data-ttu-id="757a5-145">テキスト エディターを使用して *、.cshtml* (または *.vbhtml)* ページを編集できます。</span><span class="sxs-lookup"><span data-stu-id="757a5-145">You can use a text editor to edit *.cshtml* (or *.vbhtml*) pages.</span></span>

<span data-ttu-id="757a5-146">ツールを使用せずに SQL Server コンパクト データベース *(.sdf*ファイル) を管理するのは少し難しくなります。</span><span class="sxs-lookup"><span data-stu-id="757a5-146">Managing SQL Server Compact databases (*.sdf* files) without a tool is a bit harder.</span></span> <span data-ttu-id="757a5-147">Visual Studio には *、.sdf*データベースを管理するためのツールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="757a5-147">Visual Studio containds tools for managing *.sdf* databases.</span></span> <span data-ttu-id="757a5-148">コード内で SQL コマンドを実行して、SQL Server 管理タスクを多数実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="757a5-148">You can also run SQL commands in code to perform many SQL Server management tasks.</span></span>

<span data-ttu-id="757a5-149">統合開発環境 (IDE) を使用せずに *.cshtml*ページをテストするには、ライブ サーバーに展開します。</span><span class="sxs-lookup"><span data-stu-id="757a5-149">To test *.cshtml* pages without using an integrated development environment (IDE), you can deploy them to a live server.</span></span> <span data-ttu-id="757a5-150">(WebMatrix を[使用せずに ASP.NET Web ページ サイトを展開できますか?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)</span><span class="sxs-lookup"><span data-stu-id="757a5-150">(See [Can I deploy an ASP.NET Web Pages site without using WebMatrix?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))</span></span>

### <a name="running-iis-express-without-using-an-ide"></a><span data-ttu-id="757a5-151">IDE を使用せずに IIS エクスプレスを実行する</span><span class="sxs-lookup"><span data-stu-id="757a5-151">Running IIS Express without using an IDE</span></span>

<span data-ttu-id="757a5-152">IIS Express を Web サーバーとしてコンピュータにインストールする場合は、それを使用してページをテストできます。</span><span class="sxs-lookup"><span data-stu-id="757a5-152">If you install IIS Express on your computer as a web server, you can use that to test the pages.</span></span> <span data-ttu-id="757a5-153">コマンド ラインから IIS Express を実行し、特定のポート番号に関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="757a5-153">You can run IIS Express from the command line and associate it with a specific port number.</span></span> <span data-ttu-id="757a5-154">次に、ブラウザーで *.cshtml*ファイルを要求するときに、そのポートを指定します。</span><span class="sxs-lookup"><span data-stu-id="757a5-154">You then specify that port when you request *.cshtml* files in your browser.</span></span>

<span data-ttu-id="757a5-155">Windows で、管理者特権を持つコマンド プロンプトを開き *、C:\プログラム ファイル\IIS Express*に変更します。</span><span class="sxs-lookup"><span data-stu-id="757a5-155">In Windows, open a command prompt with administrator privileges and change to *C:\Program Files\IIS Express.*</span></span> <span data-ttu-id="757a5-156">(64 ビット システムの場合は *、C:\プログラム ファイル (x86)\IIS Express フォルダーを使用します。* 次に、サイトへの実際のパスを使用して、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="757a5-156">(For 64-bit systems, use the folder *C:\Program Files (x86)\IIS Express.)* Then enter the following command, using the actual path to your site:</span></span>

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

<span data-ttu-id="757a5-157">他のプロセスによってまだ予約されていないポート番号を使用できます。</span><span class="sxs-lookup"><span data-stu-id="757a5-157">You can use any port number that isn't already reserved by some other process.</span></span> <span data-ttu-id="757a5-158">(通常、1024 を超えるポート番号は無料です)。値として`path`*、.cshtml*ファイルがある Web サイト フォルダーのパスを使用します。</span><span class="sxs-lookup"><span data-stu-id="757a5-158">(Port numbers above 1024 are typically free.) For the `path` value, use the path of the website folder where the *.cshtml* files are.</span></span>

<span data-ttu-id="757a5-159">このコマンドを実行してページを提供するように IIS Express を設定した後、ブラウザーを開いて *.cshtml*ファイルを参照できます。</span><span class="sxs-lookup"><span data-stu-id="757a5-159">After you run this command to set up IIS Express to serve your pages, you can open a browser and browse to a *.cshtml* file.</span></span> <span data-ttu-id="757a5-160">次のような URL を使用します。</span><span class="sxs-lookup"><span data-stu-id="757a5-160">Use a URL like the following:</span></span>

`http://localhost:35896/default.cshtml`

<span data-ttu-id="757a5-161">IIS Express コマンド ライン オプションの`iisexpress.exe /?`ヘルプを参照するには、コマンド ラインで入力します。</span><span class="sxs-lookup"><span data-stu-id="757a5-161">For help with IIS Express command line options, enter `iisexpress.exe /?` at the command line.</span></span>

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a><span data-ttu-id="757a5-162">Web ページ上ASP.NET Web フォーム コントロールを使用できますか。</span><span class="sxs-lookup"><span data-stu-id="757a5-162">Can I use ASP.NET Web Forms controls on a Web Pages page?</span></span>

<span data-ttu-id="757a5-163">いいえ。</span><span class="sxs-lookup"><span data-stu-id="757a5-163">No.</span></span> <span data-ttu-id="757a5-164">[CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox)コントロール、[検証コントロール](https://msdn.microsoft.com/library/bwd43d0x)[、GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview)コントロールなどの Web フォーム コントロールは、Web フォーム ページ *(.aspx*ファイル) でのみ動作します。</span><span class="sxs-lookup"><span data-stu-id="757a5-164">Web Forms controls like the [CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) control, the [validation controls](https://msdn.microsoft.com/library/bwd43d0x), and the [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) control only work in Web Forms pages (*.aspx* files).</span></span> <span data-ttu-id="757a5-165">これらのコントロールには、Web フォーム ページ フレームワークが必要です。</span><span class="sxs-lookup"><span data-stu-id="757a5-165">These controls require the Web Forms page framework.</span></span>

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a><span data-ttu-id="757a5-166">WebMatrix を使用せずに、ASP.NET Web ページ サイトを展開できますか。</span><span class="sxs-lookup"><span data-stu-id="757a5-166">Can I deploy an ASP.NET Web Pages site without using WebMatrix?</span></span>

<span data-ttu-id="757a5-167">はい。</span><span class="sxs-lookup"><span data-stu-id="757a5-167">Yes.</span></span> <span data-ttu-id="757a5-168">Web サイトファイルは、通常 FTP を使用してサーバーに手動でコピーできます。</span><span class="sxs-lookup"><span data-stu-id="757a5-168">You can manually copy website files to a server (typically by using FTP).</span></span> <span data-ttu-id="757a5-169">手動でコピーを実行する場合は、SQL Server Compact (データベース) をサポートするファイルもコピーする必要があります。</span><span class="sxs-lookup"><span data-stu-id="757a5-169">If you perform a manual copy, you also have to copy the files that support SQL Server Compact (the database).</span></span> <span data-ttu-id="757a5-170">詳細については、ブログ記事「[ツールを使用しない Web ページ アプリケーションの配置](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="757a5-170">For details, see the blog entry [Deploying Web Pages applications without a tool](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317).</span></span>

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a><span data-ttu-id="757a5-171">ログインをサポートするには、Web セキュリティ ヘルパーを使用する必要がありますか?</span><span class="sxs-lookup"><span data-stu-id="757a5-171">Do I have to use the WebSecurity helper to support logins?</span></span>

<span data-ttu-id="757a5-172">いいえ。</span><span class="sxs-lookup"><span data-stu-id="757a5-172">No.</span></span> <span data-ttu-id="757a5-173">Web`SimpleMembership`ページの一部であるプロバイダASP.NET 1 つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="757a5-173">The `SimpleMembership` provider that is part of ASP.NET Web Pages is one option.</span></span> <span data-ttu-id="757a5-174">ASP.NETに含まれるセキュリティ プロバイダ (Web フォームでの操作に使用される可能性があります) も利用できます。</span><span class="sxs-lookup"><span data-stu-id="757a5-174">The security providers that are part of ASP.NET (that you might be used to working with in Web Forms) are also available.</span></span> <span data-ttu-id="757a5-175">たとえば、Web ページの場合と同様に、フォーム認証をASP.NET Web ページで使用できます。</span><span class="sxs-lookup"><span data-stu-id="757a5-175">For example, you can use forms authentication in ASP.NET Web Pages just as you would in Web Forms.</span></span> <span data-ttu-id="757a5-176">フォーム認証の使用例については、Microsoft サポート記事[「C#.NET を使用してASP.NET アプリケーションにフォーム ベース認証を実装する方法](https://support.microsoft.com/kb/301240)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="757a5-176">For one example of how to use forms authentication, see the Microsoft Support article [How To Implement Forms-Based Authentication in Your ASP.NET Application by Using C#.NET](https://support.microsoft.com/kb/301240).</span></span> <span data-ttu-id="757a5-177">簡単な例をダウンロードするには、「[ログイン&amp;パスワード」ASP.NETバージョンを](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)参照してください。</span><span class="sxs-lookup"><span data-stu-id="757a5-177">To download a simple example, see [ASP.NET version of "Login &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).</span></span>

<span data-ttu-id="757a5-178">Windows 認証の使用方法については、ブログ記事[「ASP.NET Web ページで Windows 認証を使用](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="757a5-178">For information about how to use Windows authentication, see the blog post [Using Windows authentication in ASP.NET Web Pages](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298).</span></span>

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a><span data-ttu-id="757a5-179">web ページASP.NET HTML5 をサポートしていますか?</span><span class="sxs-lookup"><span data-stu-id="757a5-179">Does ASP.NET Web Pages support HTML5?</span></span>

<span data-ttu-id="757a5-180">はい。</span><span class="sxs-lookup"><span data-stu-id="757a5-180">Yes.</span></span> <span data-ttu-id="757a5-181">web ページ (*.cshtml*ページまたは *.vbhtml*ページ ) ASP.NET作成するページは、基本的には、ページがレンダリングされる前にサーバー上で実行されるコードも含む HTML ページです。</span><span class="sxs-lookup"><span data-stu-id="757a5-181">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are essentially HTML pages that also contain code that runs on the server, before the page is rendered.</span></span> <span data-ttu-id="757a5-182">ユーザーのブラウザーが HTML5 をサポートしている限り *、.cshtml*または *.vbhtml*ページで HTML5 要素を使用できます。</span><span class="sxs-lookup"><span data-stu-id="757a5-182">As long as the user's browser supports HTML5, you can use HTML5 elements in a *.cshtml* or *.vbhtml* page.</span></span>

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a><span data-ttu-id="757a5-183">ウェブページでJavaScriptとjQueryを使用できますか?</span><span class="sxs-lookup"><span data-stu-id="757a5-183">Can I use JavaScript and jQuery with Web Pages?</span></span>

<span data-ttu-id="757a5-184">そして、</span><span class="sxs-lookup"><span data-stu-id="757a5-184">Absolutely.</span></span> <span data-ttu-id="757a5-185">Web ページ *(.cshtml*ページまたは *.vbhtml*ページ) を使用して作成ASP.NETページは、サーバー コードが含まれる HTML ページにすぎません。</span><span class="sxs-lookup"><span data-stu-id="757a5-185">The pages you create with ASP.NET Web Pages (*.cshtml* or *.vbhtml* pages) are just HTML pages with server code in them.</span></span> <span data-ttu-id="757a5-186">したがって、JavaScript または jQuery を使用して通常の HTML ページで実行できる操作は *、.cshtml*ページまたは *.vbhtml*ページでも実行できます。</span><span class="sxs-lookup"><span data-stu-id="757a5-186">Therefore, anything you can do in a normal HTML page by using JavaScript or jQuery you can also do in a *.cshtml* or *.vbhtml* page.</span></span>

<span data-ttu-id="757a5-187">WebMatrix の**スターター サイト**テンプレートには、いくつかの jQuery ライブラリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="757a5-187">The **Starter Site** template in WebMatrix contains a number of jQuery libraries.</span></span> <span data-ttu-id="757a5-188">そのテンプレートを使用してサイトを作成する場合 *、Scripts*フォルダーには jQuery コア ライブラリ *(jquery-1.6.2.js)* と jQuery 検証用のライブラリ *(jquery.validate.js*など) が含まれます。</span><span class="sxs-lookup"><span data-stu-id="757a5-188">If you create a site by using that template, the *Scripts* folder contains a jQuery core library (*jquery-1.6.2.js)* and libraries for jQuery validation (*jquery.validate.js*, etc.).</span></span>

<span data-ttu-id="757a5-189">ASP.NET Web ページで jQuery を使用する方法を示すブログ投稿を次に示します。</span><span class="sxs-lookup"><span data-stu-id="757a5-189">Here are some blog posts that illustrate ways to use jQuery with ASP.NET Web Pages:</span></span>

- <span data-ttu-id="757a5-190">レイチェル・アペルによる[ウェブマトリックスを使用してASP.NETウェブページにjQueryの良さを追加](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/)する</span><span class="sxs-lookup"><span data-stu-id="757a5-190">[Adding jQuery Goodness to ASP.NET Web Pages using WebMatrix](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) by Rachel Appel</span></span>
- <span data-ttu-id="757a5-191">[5分: ウェブマトリックス + jQuery UI + json + jQuery テンプレート](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/)by ジョナス・エリクソン</span><span class="sxs-lookup"><span data-stu-id="757a5-191">[5 min: WebMatrix + jQuery UI + json + jQuery templates](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) by Jonas Eriksson</span></span>
- <span data-ttu-id="757a5-192">マイク・ブリンドによる[ウェブマトリックスとjQueryフォーム](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)</span><span class="sxs-lookup"><span data-stu-id="757a5-192">[WebMatrix And jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) by Mike Brind</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="757a5-193">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="757a5-193">Additional Resources</span></span>

[<span data-ttu-id="757a5-194">ASP.NET Web ページ (Razor) トラブルシューティング ガイド</span><span class="sxs-lookup"><span data-stu-id="757a5-194">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)

<span data-ttu-id="757a5-195">ASP.NET[ウェブサイト上のウェブマトリックスとASP.NETウェブページフォーラム](https://forums.asp.net/1224.aspx/1?WebMatrix)</span><span class="sxs-lookup"><span data-stu-id="757a5-195">[WebMatrix and ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix) on the ASP.NET website</span></span>
