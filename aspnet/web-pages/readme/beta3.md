---
uid: web-pages/readme/beta3
title: Web Matrix and ASP.NET Web ページ (Razor) Beta 3 リリース Readme |Microsoft Docs
author: rick-anderson
description: Web Matrix と ASP.NET Web ページ (Razor) Beta 3 リリース Readme
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510340"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a><span data-ttu-id="512c8-103">Web Matrix と ASP.NET Web ページ (Razor) Beta 3 リリース Readme</span><span class="sxs-lookup"><span data-stu-id="512c8-103">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

> <span data-ttu-id="512c8-104">Web Matrix と ASP.NET Web ページ (Razor) Beta 3 リリース Readme</span><span class="sxs-lookup"><span data-stu-id="512c8-104">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

<span data-ttu-id="512c8-105">2010年11月9日</span><span class="sxs-lookup"><span data-stu-id="512c8-105">9 November 2010</span></span>

## <a name="contents"></a><span data-ttu-id="512c8-106">内容</span><span class="sxs-lookup"><span data-stu-id="512c8-106">Contents</span></span>

- [<span data-ttu-id="512c8-107">概要</span><span class="sxs-lookup"><span data-stu-id="512c8-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="512c8-108">インストール</span><span class="sxs-lookup"><span data-stu-id="512c8-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="512c8-109">ベータ3リリースの新機能、変更点、および既知の問題</span><span class="sxs-lookup"><span data-stu-id="512c8-109">New Features, Changes, and Known Issues in the Beta 3 release</span></span>](#Known_Issues)

    - [<span data-ttu-id="512c8-110">WebMatrix のインストールに関する問題</span><span class="sxs-lookup"><span data-stu-id="512c8-110">WebMatrix Installation Issues</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="512c8-111">ASP.NET Web ページ</span><span class="sxs-lookup"><span data-stu-id="512c8-111">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="512c8-112">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="512c8-112">SQL Server Compact</span></span>](#Known_Issues_SQL_Server_Compact)
    - [<span data-ttu-id="512c8-113">アプリケーションのインストール</span><span class="sxs-lookup"><span data-stu-id="512c8-113">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="512c8-114">アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="512c8-114">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
    - [<span data-ttu-id="512c8-115">その他の問題</span><span class="sxs-lookup"><span data-stu-id="512c8-115">Other Issues</span></span>](#Known_Issues_Other_Issues)
- [<span data-ttu-id="512c8-116">参照項目</span><span class="sxs-lookup"><span data-stu-id="512c8-116">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="512c8-117">概要</span><span class="sxs-lookup"><span data-stu-id="512c8-117">Overview</span></span>

> <span data-ttu-id="512c8-118">Microsoft WebMatrix Beta は無料の web 開発スタックで、数分でインストールできます。</span><span class="sxs-lookup"><span data-stu-id="512c8-118">Microsoft WebMatrix Beta is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="512c8-119">データベースとプログラミングのフレームワークに Web サーバーを組み合わせることによって、1 つの統合的な環境を実現します。</span><span class="sxs-lookup"><span data-stu-id="512c8-119">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="512c8-120">WebMatrix ベータを使用すると、独自の ASP.NET または PHP web サイトのコーディング、テスト、発行の方法を効率化することができます。また、WebMatrix ベータを使用して、DotNetNuke、Umbraco、WordPress、Joomla などの一般的なオープンソースアプリを使用して新しい web サイトを開始することもできます。</span><span class="sxs-lookup"><span data-stu-id="512c8-120">You can use WebMatrix Beta to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix Beta to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="512c8-121">WebMatrix ベータは、インターネット上で web サイトを実行するのと同じ強力な web サーバー、データベースエンジン、フレームワーク環境を使用します。これにより、開発から運用環境への移行がスムーズでシームレスになります。</span><span class="sxs-lookup"><span data-stu-id="512c8-121">WebMatrix Beta uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="512c8-122">インストール</span><span class="sxs-lookup"><span data-stu-id="512c8-122">Installation</span></span>

> <span data-ttu-id="512c8-123">WebMatrix Beta 3 をインストールするには、 [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)を使用します。</span><span class="sxs-lookup"><span data-stu-id="512c8-123">To install WebMatrix Beta 3, you use [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="512c8-124">Web Platform Installer をインストールしたら、それを使用して WebMatrix Beta 3 をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="512c8-124">After you've installed the Web Platform Installer, you can use it to install WebMatrix Beta 3.</span></span>
> 
> <span data-ttu-id="512c8-125">インストール中に問題が発生した場合は、「 [Microsoft Web Platform Installer に関する問題のトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=196212)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="512c8-125">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a><span data-ttu-id="512c8-126">アプリケーションを公開するための手順</span><span class="sxs-lookup"><span data-stu-id="512c8-126">Instructions for Publishing Applications</span></span>

> <span data-ttu-id="512c8-127">[アプリケーションを公開するための詳細な手順を確認する](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="512c8-127">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a><span data-ttu-id="512c8-128">新機能、変更点、および既知の問題</span><span class="sxs-lookup"><span data-stu-id="512c8-128">New Features, Changes, andKnown Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a><span data-ttu-id="512c8-129">WebMatrix Beta 3 のインストール</span><span class="sxs-lookup"><span data-stu-id="512c8-129">WebMatrix Beta 3 Installation</span></span>

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="512c8-130">問題点: WebMatrix Beta 3 は Microsoft .NET Framework 4 をサポートするプラットフォームでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="512c8-130">Issue: WebMatrix Beta 3 is only available on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="512c8-131">WebMatrix ベータ版には .NET Framework version 4 が必要です。</span><span class="sxs-lookup"><span data-stu-id="512c8-131">The .NET Framework version 4 is required for WebMatrix Beta.</span></span> <span data-ttu-id="512c8-132">場合によっては、WebMatrix Beta インストーラーを使用して、サポートされている構成セットに含まれていないプラットフォームにをインストールしようとすることがあります。</span><span class="sxs-lookup"><span data-stu-id="512c8-132">In certain cases, the WebMatrix Beta installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="512c8-133">特に、SP1 更新プログラムがインストールされていない Windows Vista では WebMatrix ベータ版のインストールを開始できますが、.NET Framework 4 コンポーネントは失敗し、インストールがブロックされます。</span><span class="sxs-lookup"><span data-stu-id="512c8-133">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix Beta, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="512c8-134">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-134">**Workaround**</span></span>  
> <span data-ttu-id="512c8-135">サポートされているプラットフォームにインストールします。サポート対象のプラットフォームは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="512c8-135">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="512c8-136">Windows 7</span><span class="sxs-lookup"><span data-stu-id="512c8-136">Windows 7</span></span>
> - <span data-ttu-id="512c8-137">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="512c8-137">Windows Server 2008</span></span>
> - <span data-ttu-id="512c8-138">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="512c8-138">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="512c8-139">Windows Vista SP1 以降</span><span class="sxs-lookup"><span data-stu-id="512c8-139">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="512c8-140">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="512c8-140">Windows XP SP3</span></span>
> - <span data-ttu-id="512c8-141">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="512c8-141">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="512c8-142">問題: Microsoft Visual Studio 2008 SP1 を使用せずに Microsoft Visual Studio 2008 がインストールされている場合は、WebMatrix Beta 3 をインストールできない</span><span class="sxs-lookup"><span data-stu-id="512c8-142">Issue: Cannot install WebMatrix Beta 3 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="512c8-143">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-143">**Workaround**</span></span>  
> <span data-ttu-id="512c8-144">Microsoft ダウンロードセンターから[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-144">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="512c8-145">問題: SQL Server Compact 4.0 のアセンブリの一部が GAC にインストールされない</span><span class="sxs-lookup"><span data-stu-id="512c8-145">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="512c8-146">SQL Server Compact 4.0 を 64 ビット コンピューターにインストールする際、そのコンピューターに .NET Framework 3.5 SP1 Client Profile しかインストールされていないと、SQL Server Compact 4.0 のマネージド アセンブリがグローバル アセンブリ キャッシュ (GAC) に配置されません。</span><span class="sxs-lookup"><span data-stu-id="512c8-146">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="512c8-147">GAC にインストールされないマネージド アセンブリは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="512c8-147">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="512c8-148">*System.data.sqlserverce* (ADO.NET provider) (システムプロバイダー)</span><span class="sxs-lookup"><span data-stu-id="512c8-148">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="512c8-149">*System.data.sqlserverce* (ADO.NET) (Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="512c8-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="512c8-150">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-150">**Workaround**</span></span>  
> <span data-ttu-id="512c8-151">SQL Server Compact 4.0 をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-151">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="512c8-152">次の場所から完全バージョンの .NET Framework 3.5 SP1 をダウンロードしてインストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-152">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="512c8-153">Microsoft .NET Framework 3.5 Service pack 1 (フルパッケージ)</span><span class="sxs-lookup"><span data-stu-id="512c8-153">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="512c8-154">そのうえで SQL Server Compact 4.0 を再インストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-154">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="512c8-155">問題: コマンド ラインを使用して SQL Server Compact をアンインストールすることはできない</span><span class="sxs-lookup"><span data-stu-id="512c8-155">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="512c8-156">このリリースでは、コマンド ライン オプションを使用して SQL Server Compact をアンインストールすることはできません。</span><span class="sxs-lookup"><span data-stu-id="512c8-156">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="512c8-157">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-157">**Workaround**</span></span>  
> <span data-ttu-id="512c8-158">Windows のコントロールパネルの [*プログラムと機能*] を使用して、Microsoft SQL Server Compact 4.0 をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-158">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="512c8-159">ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="512c8-159">ASP.NET Web Pages</span></span>

<span data-ttu-id="512c8-160">ドキュメントのこのセクションでは、Razor 構文による ASP.NET Web ページのベータ3リリースにおける新機能、変更点、および既知の問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="512c8-160">This section of the document describes new features, changes, and known issues with the Beta 3 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="512c8-161">新機能</span><span class="sxs-lookup"><span data-stu-id="512c8-161">New features</span></span>](#NewFeatures)
- <span data-ttu-id="512c8-162">[[変更点]](#Changes)</span><span class="sxs-lookup"><span data-stu-id="512c8-162">[Changes](#Changes)</span></span>
- [<span data-ttu-id="512c8-163">問題</span><span class="sxs-lookup"><span data-stu-id="512c8-163">Issues</span></span>](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="512c8-164">Razor 構文を使用した ASP.NET Web ページ用の Beta 3 の新機能</span><span class="sxs-lookup"><span data-stu-id="512c8-164">New Features in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a><span data-ttu-id="512c8-165">New: "Html. Raw" メソッドがエンコードマークアップをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="512c8-165">New: "Html.Raw" method renders unencoded markup</span></span>

> <span data-ttu-id="512c8-166">新しい `Html.Raw` メソッドを使用すると、エンコードされた出力を表示する代わりに、HTML マークアップをマークアップとして表示できます。</span><span class="sxs-lookup"><span data-stu-id="512c8-166">The new `Html.Raw` method lets you render HTML markup as markup instead of rendering encoded output.</span></span> <span data-ttu-id="512c8-167">(既定では、ASP.NET Razor は文字列をレンダリングする前にエンコードします)。構文は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="512c8-167">(By default, ASP.NET Razor encodes strings before rendering them.) The syntax is:</span></span>
> 
> `Html.Raw(value)`
> 
> <span data-ttu-id="512c8-168">`Html.Raw` を使用する方法を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="512c8-168">The following example shows how to use `Html.Raw`:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="512c8-169">Razor 構文を使用した ASP.NET Web ページに関する Beta 3 の変更点</span><span class="sxs-lookup"><span data-stu-id="512c8-169">Changes in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="change-hrefattribute-method-removed"></a><span data-ttu-id="512c8-170">変更: "HrefAttribute" メソッドが削除されました</span><span class="sxs-lookup"><span data-stu-id="512c8-170">Change: "HrefAttribute" method removed</span></span>

> <span data-ttu-id="512c8-171">`WebPage` クラスの `HrefAttribute` メソッドが削除されました。</span><span class="sxs-lookup"><span data-stu-id="512c8-171">The `HrefAttribute` method of the `WebPage` class has been removed.</span></span> <span data-ttu-id="512c8-172">このヘルパーは、Url 内の安全でない文字をエンコードするために使用されました。</span><span class="sxs-lookup"><span data-stu-id="512c8-172">This helper was used to encode unsafe characters in URLs.</span></span> <span data-ttu-id="512c8-173">ASP.NET Razor は文字列を自動的にエンコードするため、これは不要になりました。</span><span class="sxs-lookup"><span data-stu-id="512c8-173">It is no longer required because ASP.NET Razor automatically encodes strings.</span></span> <span data-ttu-id="512c8-174">(新しい `Html.Raw` メソッドを使用して、エンコードされていない文字列を表示します)。</span><span class="sxs-lookup"><span data-stu-id="512c8-174">(Use the new `Html.Raw` method to render unencoded strings.)</span></span>

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a><span data-ttu-id="512c8-175">変更: 宣言型の "@helper" ヘルパーの構文が変更されました</span><span class="sxs-lookup"><span data-stu-id="512c8-175">Change: Syntax for declarative "@helper" helpers changed</span></span>

> <span data-ttu-id="512c8-176">Beta 3 リリースでは、ASP.NET は、`@helper` 構文を使用して作成されたヘルパーを解析する方法を変更します。</span><span class="sxs-lookup"><span data-stu-id="512c8-176">In the Beta 3 release, ASP.NET changes how it parses helpers that are created using the `@helper` syntax.</span></span> <span data-ttu-id="512c8-177">基本的に、`@helper` 構文は、コードを含めることができるマークアップブロックとしてではなく、コードブロックとして解析されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="512c8-177">In essence, the `@helper` syntax is now parsed as a code block instead of as a block of markup that can include code.</span></span> <span data-ttu-id="512c8-178">そのため、ヘルパー内のコードを `@{ }` ブロックで囲む必要はありません。</span><span class="sxs-lookup"><span data-stu-id="512c8-178">Therefore, code inside the helper does not need to be enclosed in `@{ }` blocks.</span></span> <span data-ttu-id="512c8-179">逆に、ヘルパー内のマークアップは、HTML 要素または ASP.NET Razor `<text></text>` タグに明示的に含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-179">Conversely, markup inside the helper has to be explicitly included in HTML elements or in ASP.NET Razor `<text></text>` tags.</span></span>
> 
> <span data-ttu-id="512c8-180">たとえば、次の `@helper` 構文は、ベータ3リリースで動作します。</span><span class="sxs-lookup"><span data-stu-id="512c8-180">For example, the following `@helper` syntax works in the Beta 3 release:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> <span data-ttu-id="512c8-181">Beta 3 リリースでは、このヘルパーを次の例のように変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-181">In the Beta 3 release, this helper must be changed to look like the following example:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> <span data-ttu-id="512c8-182">ヘルパーの初期コードの周囲に `@{ }` 文字が使用されなくなったことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="512c8-182">Notice that the `@{ }` characters around the initial code in the helper is no longer used.</span></span> <span data-ttu-id="512c8-183">これは、ヘルパーの内容が既定でコードブロックとして扱われるためです。</span><span class="sxs-lookup"><span data-stu-id="512c8-183">This is because the contents of the helpers are treated as a code block by default.</span></span> <span data-ttu-id="512c8-184">ヘルパーは、開始 `<a>` タグで始まるマークアップをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="512c8-184">The helper renders markup, which starts with the opening `<a>` tag.</span></span> <span data-ttu-id="512c8-185">ヘルパーが、終了タグ (`<meta>` タグなど) を含まないプレーンテキストまたはタグをレンダリングする必要がある場合は、表示されるコンテンツが `<text></text>` タグに含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-185">If the helper must render plain text or tags that do not include a closing tag (for example, `<meta>` tags), the content to be rendered must be in `<text></text>` tags.</span></span>

#### <a name="change-webpagecontexthttpcontext-removed"></a><span data-ttu-id="512c8-186">変更: "WebPageContext. HttpContext" が削除されました</span><span class="sxs-lookup"><span data-stu-id="512c8-186">Change: "WebPageContext.HttpContext" removed</span></span>

> <span data-ttu-id="512c8-187">`WebPageContext.HttpContext` プロパティは削除されました。</span><span class="sxs-lookup"><span data-stu-id="512c8-187">The `WebPageContext.HttpContext` property has been removed.</span></span> <span data-ttu-id="512c8-188">代わりに `HttpContext.Current` を使用してください</span><span class="sxs-lookup"><span data-stu-id="512c8-188">Use `HttpContext.Current` instead.</span></span> <span data-ttu-id="512c8-189">(`WebPageContext.HttpContext` プロパティは、単純にこれをラップしたものです)。</span><span class="sxs-lookup"><span data-stu-id="512c8-189">(The `WebPageContext.HttpContext` property simply wrapped this.)</span></span>

#### <a name="change-facebook-helper-moved-to-new-package"></a><span data-ttu-id="512c8-190">変更: "Facebook" ヘルパーを新しいパッケージに移動しました</span><span class="sxs-lookup"><span data-stu-id="512c8-190">Change: "Facebook" helper moved to new package</span></span>

> <span data-ttu-id="512c8-191">`Facebook` helper は、`Facebook` のヘルパーや追加機能を含む、 *Facebook のヘルパー*ライブラリに移動されました。</span><span class="sxs-lookup"><span data-stu-id="512c8-191">The `Facebook` helper has been moved to the *Facebook.Helper* library, which includes the `Facebook` helper and additional functionality.</span></span> <span data-ttu-id="512c8-192">このライブラリを個別のパッケージとしてインストールする必要があります。詳細については、「チュートリアル[はじめに ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="512c8-192">You must install this library as a separate package, as described in "Installing Helpers with Package Manager" in the tutorial [Getting Started with ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889).</span></span>

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a><span data-ttu-id="512c8-193">変更: メンバーシップ、ロール、およびセキュリティの種類が新しいアセンブリに移動します</span><span class="sxs-lookup"><span data-stu-id="512c8-193">Change: Membership, Role, and Security types moves to new assembly</span></span>

> <span data-ttu-id="512c8-194">次の型が `WebMatrix.WebData` アセンブリに移動されました。</span><span class="sxs-lookup"><span data-stu-id="512c8-194">The following types were moved to the `WebMatrix.WebData` assembly:</span></span>
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a><span data-ttu-id="512c8-195">変更: "TagBuilder" クラスを System.web. Web ページの .dll アセンブリに移動</span><span class="sxs-lookup"><span data-stu-id="512c8-195">Change: "TagBuilder" class moved to System.Web.WebPages.dll assembly</span></span>

> <span data-ttu-id="512c8-196">`TagBuilde` r クラスは、System.web. Web ページの .dll アセンブリに移動されました。</span><span class="sxs-lookup"><span data-stu-id="512c8-196">The `TagBuilde` r class has been moved to the System.Web.WebPages.dll assembly.</span></span> <span data-ttu-id="512c8-197">以前は、これは ASP.NET MVC の一部であったアセンブリに含まれていました。</span><span class="sxs-lookup"><span data-stu-id="512c8-197">Previously, this was in an assembly that was part of ASP.NET MVC.</span></span> <span data-ttu-id="512c8-198">この変更は、`TagBuilder` クラスを使用するために ASP.NET MVC をインストールする必要がないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="512c8-198">This change means that you do not have to install ASP.NET MVC in order to use the `TagBuilder` class.</span></span>
> 
> <span data-ttu-id="512c8-199">ただし、クラスは依然として `System.Web.Mvc` 名前空間にあります。</span><span class="sxs-lookup"><span data-stu-id="512c8-199">However, the class is still in the `System.Web.Mvc` namespace.</span></span> <span data-ttu-id="512c8-200">`TagBuilder` クラス (たとえば、カスタム ASP.NET Razor ヘルパー) を使用するには、名前空間を参照する必要があります (たとえば、コードに `@using System.Web.Mvc` を追加します)。</span><span class="sxs-lookup"><span data-stu-id="512c8-200">In order to use the `TagBuilder` class (for example, in a custom ASP.NET Razor helper), you must reference the namespace (for example, by adding `@using System.Web.Mvc` to your code).</span></span>

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a><span data-ttu-id="512c8-201">変更: 要求の検証構文が変更されました。"Validation" クラスが削除されました</span><span class="sxs-lookup"><span data-stu-id="512c8-201">Change: Request validation syntax changed; "Validation" class removed</span></span>

> <span data-ttu-id="512c8-202">Beta 3 リリースでは、個別のフィールドまたはフィールドのセットの検証を無効にするために、`Validation.Exclude` メソッドを呼び出して、検証から除外するフィールドの名前または名前を渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="512c8-202">In the Beta 3 release, to disable validation for an individual field or set of fields, you can call the `Validation.Exclude` method, passing in the name or names of the fields to exclude from validation.</span></span> <span data-ttu-id="512c8-203">検証をバイパスするために、Beta 3 リリースで新しい構文を使用できます。</span><span class="sxs-lookup"><span data-stu-id="512c8-203">A new syntax is available in the Beta 3 release for bypassing validation.</span></span> <span data-ttu-id="512c8-204">Beta 3 で使用されている `Validation` 方法は削除されました。</span><span class="sxs-lookup"><span data-stu-id="512c8-204">The `Validation` method used in Beta 3 has been removed.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="512c8-205">要求の検証を無効にしない場合、ユーザーが HTML マークアップをアップロードしようとすると (たとえば、ページのリッチテキストエディターを使用して)、web サイトは危険な要求のようなエラーを報告*します。クライアントからのフォームの値が検出*され、ユーザーの入力は受け入れられません。</span><span class="sxs-lookup"><span data-stu-id="512c8-205">If you do not disable request validation, if users try to upload HTML markup (for example, by using a rich text editor on a page), the website will report an error like *A potentially dangerous Request.Form value was detected from the client* and the user input is not accepted.</span></span> <span data-ttu-id="512c8-206">要求の検証を無効にした場合は、ユーザー入力を手動で確認して、 [Microsoft のクロスサイトスクリプティングライブラリ](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)v4.0 などを使用する危険性のあるマークアップやスクリプトが含まれていないことを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-206">If you disable request validation, you must manually check user input to make sure that it does not contain potentially dangerous markup or script using something like the [Microsoft Anti-Cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span></span>
> 
> 
> <span data-ttu-id="512c8-207">自動要求の検証を無効にするには、`Request.Unvalidated` メソッドを呼び出して、要求の検証をバイパスするフィールドまたはその他の post オブジェクトの名前を渡します。</span><span class="sxs-lookup"><span data-stu-id="512c8-207">To disable automatic request validation, call the `Request.Unvalidated` method, passing it the name of the field or other post object that you want to bypass request validation for.</span></span> <span data-ttu-id="512c8-208">このメソッドを使用すると、`Form`、`QueryString`、`Cookies`、および `ServerVariables` コレクション内の項目の検証を省略できます。</span><span class="sxs-lookup"><span data-stu-id="512c8-208">You can use this method to bypass validation for any items in the `Form`, `QueryString`, `Cookies`, and `ServerVariables` collections.</span></span> <span data-ttu-id="512c8-209">次の例は、`Unvalidated` メソッドの使用方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="512c8-209">The following examples show how to use the `Unvalidated` method:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="512c8-210">Razor 構文での ASP.NET Web ページに関する既知の問題</span><span class="sxs-lookup"><span data-stu-id="512c8-210">Known Issues for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="512c8-211">問題: メンバーシップ用のカスタム ユーザー テーブルを使用しているときに予期しない動作が生じる</span><span class="sxs-lookup"><span data-stu-id="512c8-211">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="512c8-212">ASP.NET Razor web サイトのメンバーシッププロバイダーを初期化するには、`WebSecurity.InitializeDatabaseConnection` メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="512c8-212">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="512c8-213">(WebMatrix では、スターターサイトテンプレートには、 *\_該当*ファイルにこのメソッドの呼び出しが含まれています)。このメソッドの `autoCreateTables` パラメーターが true に設定されている場合 (既定では、スタートサイトテンプレートで true に設定されています)、認識できないテーブル名がメソッドに渡された場合 (2 番目のパラメーター)、メソッドはエラーをスローしません。</span><span class="sxs-lookup"><span data-stu-id="512c8-213">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="512c8-214">エラーがスローされずに、自動的にテーブルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="512c8-214">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="512c8-215">メンバーシップにカスタムユーザーテーブルを使用するが、間違ったテーブル名を `WebSecurity.InitializeDatabaseConnection` メソッドに渡す場合は、この問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-215">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="512c8-216">指定したテーブルが存在しなかったとしても、既定ではメソッドからエラーが生成されません。新しいテーブルが作成されるため、アプリケーションは一見、正常に機能しているように見えます。</span><span class="sxs-lookup"><span data-stu-id="512c8-216">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="512c8-217">しかし、最終的には、カスタム ユーザー テーブル (とそのテーブル内のフィールド) に依存しているアプリケーション コードで予期しないエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="512c8-217">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="512c8-218">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-218">**Workaround**</span></span>  
> <span data-ttu-id="512c8-219">`InitializeDatabaseConnection` メソッドで渡された名前がメンバーシップデータベースのユーザープロファイルテーブルと一致していることを確認するか、`autoCreateTables` パラメーターが false に設定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="512c8-219">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="512c8-220">問題: "SQL Server のユーザー インスタンスを生成できませんでした" というエラーが表示される</span><span class="sxs-lookup"><span data-stu-id="512c8-220">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="512c8-221">WebMatrix Web アプリケーションに SQL Server Express が使用されており、Windows 7 または Windows Server 2008 R2 で IIS 7.5 が実行されている場合、ユーザーのローカル アプリケーション パスを SQL Server が実行時に取得できないことを示すエラーが表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-221">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="512c8-222">**回避策**アプリケーションが実行されている Windows アカウント (通常は NETWORK SERVICE) に、アプリケーションのルートフォルダーと、*アプリの\_データ*などのサブフォルダーに対する読み取り/書き込みアクセス許可があることを確認します。</span><span class="sxs-lookup"><span data-stu-id="512c8-222">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="512c8-223">詳細については、サポート技術情報の記事「 [SQL Server Express ユーザーインスタンスと ASP.net Web アプリケーションプロジェクトに関する問題](https://support.microsoft.com/kb/2002980)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="512c8-223">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a><span data-ttu-id="512c8-224">問題点: Visual Studio でカスタムアセンブリ (Dll) の名前空間が自動的にインポートされない</span><span class="sxs-lookup"><span data-stu-id="512c8-224">Issue: In Visual Studio, namespaces for custom assemblies (DLLs) are not imported automatically</span></span>

> <span data-ttu-id="512c8-225">Visual Studio のプロジェクトでカスタムアセンブリを使用する場合、これらのアセンブリで宣言されている名前空間は、デザイン時に自動的にインポートされません。</span><span class="sxs-lookup"><span data-stu-id="512c8-225">If you use custom assemblies in a project in Visual Studio, the namespaces declared in those assemblies are not automatically imported at design time.</span></span> <span data-ttu-id="512c8-226">その結果、カスタム型への参照がデザイン時に認識されず、Visual Studio で認識されていないとマークされることがあります ("波線" を使用)。</span><span class="sxs-lookup"><span data-stu-id="512c8-226">As a result, references to custom types might not be recognized at design time and are marked as not recognized in Visual Studio (using a "squiggle").</span></span> <span data-ttu-id="512c8-227">この問題は、Visual Studio のデザイン時にのみ発生します。アプリケーション自体が正常に実行されます。</span><span class="sxs-lookup"><span data-stu-id="512c8-227">This problem occurs only at design time in Visual Studio; the application itself runs properly.</span></span>
> 
> <span data-ttu-id="512c8-228">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-228">**Workaround**</span></span>  
> <span data-ttu-id="512c8-229">デザイン時に認識されないエンティティを参照する `using` ステートメント (`imports` Visual Basic) を含めます。</span><span class="sxs-lookup"><span data-stu-id="512c8-229">Include a `using` statement (`imports` in Visual Basic) that references the entities that are not recognized at design time.</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="512c8-230">問題: Visual Studio IntelliSense およびプロジェクト テンプレートは ASP.NET MVC Version 3 でしか利用できない</span><span class="sxs-lookup"><span data-stu-id="512c8-230">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="512c8-231">ASP.NET Web Pages をインストールしても Visual Studio 用のツール (ASP.NET Web Pages アプリケーション用のプロジェクト テンプレート、IntelliSense など) はインストールされません。</span><span class="sxs-lookup"><span data-stu-id="512c8-231">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="512c8-232">**回避策**Visual Studio で ASP.NET Web ページアプリケーションの IntelliSense とプロジェクトテンプレートを使用するには、Web Platform Installer または[スタンドアロンインストーラー](https://go.microsoft.com/fwlink/?LinkID=191797)を使用して ASP.NET MVC 3 RC をインストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-232">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a><span data-ttu-id="512c8-233">問題: "&lt;ヘルパー&gt; クラスが見つかりません" エラー</span><span class="sxs-lookup"><span data-stu-id="512c8-233">Issue: "&lt;helper&gt; class cannot be found" error</span></span>

> <span data-ttu-id="512c8-234">Beta 3 にアップグレードすると、ヘルパークラス (`Facebook` クラスなど) が見つからないというエラーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="512c8-234">After you upgrade to Beta 3, you might see an error that a helper class (for example, the `Facebook` class) cannot not be found.</span></span> <span data-ttu-id="512c8-235">Beta 2 以降、Beta 3 では、明示的にインストールする必要があるパッケージにヘルパーが移動されました。</span><span class="sxs-lookup"><span data-stu-id="512c8-235">Starting in Beta 2 and continuing in Beta 3, helpers have been moved to packages that you must explicitly install.</span></span> <span data-ttu-id="512c8-236">既存のサイトは、これらのパッケージを含むようにアップグレードされません。これには、 *\My Documents\IISExpress*または *\My Documents\My* websites フォルダー内のサイトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="512c8-236">Existing sites are not upgraded to include these packages; this includes sites in the *\My Documents\IISExpress* or *\My Documents\My Web Sites* folders.</span></span> <span data-ttu-id="512c8-237">特に、 *[個人用サイト*(WebSite1)] で既定のサイトを使用すると、このエラーが表示されます。このサイトには、`Twitter` ヘルパーへの参照が含まれています。</span><span class="sxs-lookup"><span data-stu-id="512c8-237">In particular, you will see this error if you use the default site in *My Sites* (WebSite1), which includes a reference to the `Twitter` helper.</span></span>
> 
> <span data-ttu-id="512c8-238">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-238">**Workaround**</span></span>  
> <span data-ttu-id="512c8-239">サイト内のヘルパーへの呼び出しをコメントアウトし、[ *\_管理者*] ページを実行して、使用するヘルパーを含むパッケージまたはパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-239">Comment out calls to any helpers in the site, run the *\_Admin* page, and install the package or packages that include the helpers that you want to use.</span></span> <span data-ttu-id="512c8-240">パッケージをインストールしたら、ヘルパーを参照する行のコメントを解除できます。</span><span class="sxs-lookup"><span data-stu-id="512c8-240">After you've installed the package, you can uncomment the lines that reference helpers.</span></span>

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a><span data-ttu-id="512c8-241">問題点: Beta 3 ASP.NET Razor アセンブリを Bin フォルダーに配置すると、ホスティングサイトで機能しない場合がある</span><span class="sxs-lookup"><span data-stu-id="512c8-241">Issue: Deploying Beta 3 ASP.NET Razor assemblies to the Bin folder might not work on hosting sites</span></span>

> <span data-ttu-id="512c8-242">ASP.NET Web ページ web サイトをホストサイトに展開し、ASP.NET Razor Beta 3 アセンブリをサイトの*Bin*フォルダーに配置すると、次のようなエラーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-242">If you deploy an ASP.NET Web Pages website to a hosting site, and if you deploy the ASP.NET Razor Beta 3 assemblies to the site's *Bin* folder, you might experience errors, including the following:</span></span>
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> <span data-ttu-id="512c8-243">これは、ホスティングプロバイダーが ASP.NET Web ページ Beta 1 のアセンブリをサーバーのグローバルアプリケーションキャッシュ (GAC) にインストールしている場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-243">This can happen if the hosting provider has installed the ASP.NET Web Pages Beta 1 assemblies into the server's global application cache (GAC).</span></span> <span data-ttu-id="512c8-244">GAC 内のアセンブリは、 *Bin*フォルダーにローカルにインストールされているアセンブリよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="512c8-244">Assemblies in the GAC get precedence over assemblies installed locally in the *Bin* folder.</span></span>
> 
> <span data-ttu-id="512c8-245">**回避策**ホスティングプロバイダーに問い合わせて、発生しているエラーの原因が、プロバイダーのアセンブリのバージョン間の競合によるものであることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="512c8-245">**Workaround** Contact your hosting provider to confirm that the errors you are seeing are due to a conflict between the provider's versions of the assemblies and yours.</span></span> <span data-ttu-id="512c8-246">その場合は、ホスティングプロバイダーがサーバーの GAC 内のアセンブリを更新するように要求します。</span><span class="sxs-lookup"><span data-stu-id="512c8-246">If so, request that the hosting provider update the assemblies in the server's GAC.</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="512c8-247">問題: フィードなどの外部データをプロキシ サーバーから読み取る</span><span class="sxs-lookup"><span data-stu-id="512c8-247">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="512c8-248">サイトを実行しているサーバーがプロキシサーバーの背後にある場合は、サイトの外部からの情報を読み取ることができるよう*に、web.config ファイルに*プロキシ情報を構成することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-248">If the server running the site is behind a proxy server, you might need to configure proxy information in the *Web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="512c8-249">たとえば、`ReCaptcha` ヘルパーを使用する場合、ヘルパーは reCAPTCHA サービスと通信しますが、プロキシサーバーによってブロックされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-249">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="512c8-250">同様に、ASP.NET Web Pages で使用されているフィード (パッケージ マネージャーによって使用されているフィードなど) にもプロキシ構成が必要となることがあります。</span><span class="sxs-lookup"><span data-stu-id="512c8-250">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="512c8-251">外部サービスの操作中またはパッケージフィードの操作で問題が発生した場合は、アプリケーションのルート*web.config*ファイルに次の要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="512c8-251">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *Web.config* file:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> <span data-ttu-id="512c8-252">プロキシサーバーの構成の詳細については、MSDN Web サイトの「 [&lt;proxy&gt; 要素 (ネットワーク設定)](https://msdn.microsoft.com/library/sa91de1e.aspx) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="512c8-252">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a><span data-ttu-id="512c8-253">問題: "Microsoft Web インフラストラクチャを読み込めません" エラーが発生する</span><span class="sxs-lookup"><span data-stu-id="512c8-253">Issue: "Microsoft.Web.Infrastructure.dll cannot be loaded" error</span></span>

> <span data-ttu-id="512c8-254">ベータ1バージョンの ASP.NET Web ページを Razor 構文と共にインストールした後、Beta 3 バージョンをインストールした場合は、すべての適切なアセンブリが、 *Microsoft Web インフラストラクチャ .dll*を除く GAC にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="512c8-254">If you previously installed the Beta 1 version of ASP.NET Web Pages with Razor syntax and then install the Beta 3 version, all appropriate assemblies are installed in the GAC except *Microsoft.Web.Infrastructure.dll*.</span></span> <span data-ttu-id="512c8-255">その結果、ASP.NET Razor ページを実行すると、 *Microsoft Web インフラストラクチャ*を読み込めなかったことを示すエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="512c8-255">As a consequence, when you run ASP.NET Razor pages, you see an error that indicates that *Microsoft.Web.Infrastructure.dll* could not be loaded.</span></span>
> 
> <span data-ttu-id="512c8-256">この問題は、クリーンコンピューターでベータ3リリースを読み込んだ場合は発生しません。</span><span class="sxs-lookup"><span data-stu-id="512c8-256">This issue does not occur if you loaded the Beta 3 release on a clean computer.</span></span>
> 
> <span data-ttu-id="512c8-257">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-257">**Workaround**</span></span>  
> <span data-ttu-id="512c8-258">コントロールパネルで ASP.NET Web ページをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-258">In Control Panel, uninstall ASP.NET Web Pages.</span></span> <span data-ttu-id="512c8-259">次に、Beta 3 リリースを再インストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-259">Then reinstall the Beta 3 release.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="512c8-260">問題: .NET Framework  Version 4 をアンインストールすると Razor 構文を使用する ASP.NET Web Pages が無効になる</span><span class="sxs-lookup"><span data-stu-id="512c8-260">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="512c8-261">.NET Framework  Version 4 をアンインストールして再インストールした場合、Razor 構文を使用する ASP.NET Web Pages は無効になります。</span><span class="sxs-lookup"><span data-stu-id="512c8-261">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="512c8-262">拡張子が*cshtml*のページは正しく動作しません。</span><span class="sxs-lookup"><span data-stu-id="512c8-262">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="512c8-263">ASP.NET Web ページは、アセンブリをコンピューターのルート*web.config*ファイルに登録し、.NET Framework を削除するとそのファイルが削除されます。</span><span class="sxs-lookup"><span data-stu-id="512c8-263">ASP.NET Web Pages registers an assembly in the machine root *Web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="512c8-264">.NET Framework を再インストールすると、新しいバージョンの構成ファイルがインストールされますが、ASP.NET Web Pages アセンブリに対する参照は追加されません。</span><span class="sxs-lookup"><span data-stu-id="512c8-264">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="512c8-265">**回避策**.NET Framework を再インストールした後、Razor 構文で ASP.NET Web ページを再インストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-265">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="512c8-266">これにより、コンピュータールートの*web.config ファイルに*次の要素が追加されます。通常は次の場所にあります。</span><span class="sxs-lookup"><span data-stu-id="512c8-266">This adds the following element to the *Web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a><span data-ttu-id="512c8-267">問題: 以前に Bin フォルダー内の ASP.NET アセンブリを使用して展開されたアプリケーションでエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="512c8-267">Issue: Applications previously deployed with ASP.NET assemblies in the Bin folder experience errors</span></span>

> <span data-ttu-id="512c8-268">配置時に、ASP.NET Web ページアセンブリ (たとえば、 *Microsoft Web ページ*) のコピーをサーバー上の web サイトの*Bin*フォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="512c8-268">During deployment, copies of the ASP.NET Web Pages assemblies (for example, *Microsoft.WebPages.dll*) to the *Bin* folder of the website on the server.</span></span> <span data-ttu-id="512c8-269">(これは、配置中、または開発者によってアセンブリが明示的にコピーされたために自動的に発生した可能性があります)。ただし、Beta 3 リリースがインストールされている場合、特定の種類が見つからないエラーなど、エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="512c8-269">(This might have happened automatically during deployment or because the developer explicitly copied the assemblies.) However, when the Beta 3 release is installed, errors occurs, such as errors that certain types cannot be found.</span></span> <span data-ttu-id="512c8-270">これは、ベータ3リリース用に複数の ASP.NET Web ページ型が異なる名前空間に移動されたために発生します。</span><span class="sxs-lookup"><span data-stu-id="512c8-270">This occurs because a number of ASP.NET Web Pages types were moved into different namespaces for the Beta 3 release.</span></span>
> 
> <span data-ttu-id="512c8-271">**回避策** </span><span class="sxs-lookup"><span data-stu-id="512c8-271">**Workaround** </span></span>  
> <span data-ttu-id="512c8-272">配置されたアプリケーションの*Bin*フォルダーをクリアし、新しいアセンブリをフォルダーにコピー (またはアプリケーションを再デプロイ) してから、アプリケーションを再起動します。</span><span class="sxs-lookup"><span data-stu-id="512c8-272">Clear the *Bin* folder of the deployed application, copy the new assemblies to the folder (or redeploy the application), and then restart the application.</span></span>

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="512c8-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span><span class="sxs-lookup"><span data-stu-id="512c8-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="512c8-274">IIS 7 または IIS 7.5 では、次のような URL の要求は、拡張子が*cshtml*または*vbhtml*のページを見つけることができません。</span><span class="sxs-lookup"><span data-stu-id="512c8-274">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="512c8-275">IIS 7 または IIS 7.5 では URL の書き換えが既定で有効になっていないため、この問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="512c8-275">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="512c8-276">Likeliest シナリオでは、IIS Express を使用してローカルでテストするときに問題が発生することはありませんが、web サイトをホストする web サイトにデプロイするときにこの問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="512c8-276">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="512c8-277">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-277">**Workaround**</span></span>
> 
> - <span data-ttu-id="512c8-278">サーバーコンピューターを制御している場合は、サーバーコンピューターで、更新プログラムに記載されている更新プログラムをインストールします。この更新プログラムは[、特定の iis 7.0 または iis 7.5 ハンドラーが、url の末尾がピリオドではない要求を処理](https://support.microsoft.com/kb/980368)できるようにします。</span><span class="sxs-lookup"><span data-stu-id="512c8-278">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="512c8-279">サーバーコンピューターを制御できない場合は (たとえば、ホスティング web サイトに配置する場合)、 *web*サイトの web.config ファイルに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="512c8-279">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *Web.config* file:</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a><span data-ttu-id="512c8-280">問題点: 同じアプリケーションで Web アプリケーションプロジェクトまたは ASP.NET MVC と ASP.NET Web ページを使用する</span><span class="sxs-lookup"><span data-stu-id="512c8-280">Issue: Using Web Application Project or ASP.NET MVC and ASP.NET Web pages in the same application</span></span>

> <span data-ttu-id="512c8-281">Web アプリケーションプロジェクトまたは ASP.NET MVC アプリケーションで ASP.NET Web ページを使用していた場合、 *WebPageHttpApplication*が見つからないというエラーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="512c8-281">If you were using ASP.NET Web Pages in a Web Application project or ASP.NET MVC application, you might see an error that *WebPageHttpApplication* cannot be found.</span></span>
> 
> <span data-ttu-id="512c8-282">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-282">**Workaround**</span></span>  
> <span data-ttu-id="512c8-283">このエラーが発生した場合は、アプリケーションを派生させる基底クラスを変更します。</span><span class="sxs-lookup"><span data-stu-id="512c8-283">If you get this error, change the base class from which the application derives.</span></span> <span data-ttu-id="512c8-284">*Global.asax*ファイルで、次の行を変更します。</span><span class="sxs-lookup"><span data-stu-id="512c8-284">In the *Global.asax* file, change the following line:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> <span data-ttu-id="512c8-285">この行を次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="512c8-285">To this:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> <span data-ttu-id="512c8-286">これにより、ASP.NET Web ページのベータ1リリースで導入された変更が Razor 構文によって元に戻されます。</span><span class="sxs-lookup"><span data-stu-id="512c8-286">This in effect reverses a change that was introduced for the Beta 1 release of ASP.NET Web Pages with Razor syntax.</span></span>

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="512c8-287">問題: SQL Server Compact がインストールされていないコンピューターにアプリケーションを展開する</span><span class="sxs-lookup"><span data-stu-id="512c8-287">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="512c8-288">SQL Server Compact データベースを含むアプリケーションは、SQL Server Compact がインストールされていないコンピューターで実行できます。</span><span class="sxs-lookup"><span data-stu-id="512c8-288">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="512c8-289">Microsoft WebMatrix Beta 3 では、これらのバイナリが自動的にコピーされ *、適切な web.config ファイル*変換が実行されます。</span><span class="sxs-lookup"><span data-stu-id="512c8-289">Microsoft WebMatrix Beta 3 automatically copies these binaries for you and performs the appropriate *Web.config* file transforms.</span></span>
> 
> <span data-ttu-id="512c8-290">**回避策**これらのファイルをコピーし*て、web.config ファイルを*手動で変更する必要がある場合は、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="512c8-290">**Workaround** If you need to copy these files and make the *Web.config* file changes manually, do the following :</span></span>
> 
> 1. <span data-ttu-id="512c8-291">データベースエンジンアセンブリを、ターゲットコンピューター上のアプリケーションの*Bin*フォルダー (およびサブフォルダー) にコピーします。</span><span class="sxs-lookup"><span data-stu-id="512c8-291">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span> 
> 
>     - <span data-ttu-id="512c8-292">*SQL Server Compact C:\Program Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **を** *\bin*にコピーします。</span><span class="sxs-lookup"><span data-stu-id="512c8-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span></span>
>     - <span data-ttu-id="512c8-293">*SQL Server Compact C:\Program Edition\v4.0\Private\x86\\* \* を \Bin\x86**にコピーし**ます。</span><span class="sxs-lookup"><span data-stu-id="512c8-293">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **to** *\Bin\x86*</span></span>
>     - <span data-ttu-id="512c8-294">*SQL Server Compact C:\Program Edition\v4.0\Private\amd64\\* \* を \Bin\amd64**にコピーし**ます。</span><span class="sxs-lookup"><span data-stu-id="512c8-294">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 2. <span data-ttu-id="512c8-295">*Web*サイトのルートフォルダーで、web.config ファイルを作成するか、開きます。</span><span class="sxs-lookup"><span data-stu-id="512c8-295">In the root folder of the website, create or open a *Web.config* file.</span></span> <span data-ttu-id="512c8-296">(WebMatrix Beta 3 では、 **[ファイルの種類の選択]** ダイアログボックスで **[すべて]** をクリックすると、このファイルの種類が使用可能になります)。</span><span class="sxs-lookup"><span data-stu-id="512c8-296">(In WebMatrix Beta 3, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="512c8-297">次の要素を **&lt;configuration&gt;** 要素の子として追加します ( **&lt;system.web&gt;** 要素の内側には追加しません)。</span><span class="sxs-lookup"><span data-stu-id="512c8-297">Add the following element as a child of the **&lt;configuration&gt;** element (not inside the **&lt;system.web&gt;** element):</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="512c8-298">問題点: データベースと WebGrid のヘルパーは、Visual Basic の中程度の信頼では機能しません</span><span class="sxs-lookup"><span data-stu-id="512c8-298">Issue: Database and WebGrid helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="512c8-299">Visual Basic ( *vbhtml*ファイルの作成) を使用している場合、アプリケーションが中程度の信頼を使用するように設定されていると、`Database` と `WebGrid` のヘルパーは機能しません。</span><span class="sxs-lookup"><span data-stu-id="512c8-299">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="512c8-300">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-300">**Workaround**</span></span>  
> <span data-ttu-id="512c8-301">完全信頼を使用するようにアプリケーションを一時的に設定します。</span><span class="sxs-lookup"><span data-stu-id="512c8-301">Temporarily set the application to use Full Trust.</span></span>

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a><span data-ttu-id="512c8-302">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="512c8-302">SQL Server Compact</span></span>

#### <a name="issue-encrypt-property-is-not-recognized"></a><span data-ttu-id="512c8-303">問題: "Encrypt" プロパティが認識されない</span><span class="sxs-lookup"><span data-stu-id="512c8-303">Issue: "Encrypt" property is not recognized</span></span>

> <span data-ttu-id="512c8-304">SQL Server Compact 4.0 は `SqlCeConnection` クラスの `Encrypt` プロパティを認識しません。</span><span class="sxs-lookup"><span data-stu-id="512c8-304">SQL Server Compact 4.0 does not recognize the `Encrypt` property of the `SqlCeConnection` class.</span></span> <span data-ttu-id="512c8-305">このプロパティを使用してデータベースファイルを暗号化しないでください。</span><span class="sxs-lookup"><span data-stu-id="512c8-305">You should not use this property to encrypt database files.</span></span> <span data-ttu-id="512c8-306">`Encrypt` プロパティは SQL Server Compact 3.5 リリースでは非推奨とされており、旧バージョンとの互換性のためだけに保持されていました。</span><span class="sxs-lookup"><span data-stu-id="512c8-306">The `Encrypt` property was deprecated in SQL Server Compact 3.5 release and was retained only for backward compatibility.</span></span> 
> 
> <span data-ttu-id="512c8-307">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-307">**Workaround**</span></span>  
> <span data-ttu-id="512c8-308">`SqlCeConnection` クラスの `Encryption Mode` プロパティを使用して、SQL Server Compact 4.0 データベースファイルを暗号化します。</span><span class="sxs-lookup"><span data-stu-id="512c8-308">Use the `Encryption Mode` property of the `SqlCeConnection` class to encrypt SQL Server Compact 4.0 database files.</span></span> <span data-ttu-id="512c8-309">次の例では、`Encryption Mode` プロパティを使用して、暗号化された SQL Server Compact 4.0 データベースを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="512c8-309">The following example shows how to create an encrypted SQL Server Compact 4.0 database using the `Encryption Mode` property:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> <span data-ttu-id="512c8-310">既存の SQL Server Compact 4.0 データベースの暗号化モードを変更するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="512c8-310">To change the encryption mode of an existing SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> <span data-ttu-id="512c8-311">暗号化されていない SQL Server Compact 4.0 データベースを暗号化するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="512c8-311">To encrypt an unencrypted SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a><span data-ttu-id="512c8-312">問題: Microsoft Visual C++ 2008 ランタイムライブラリが必要です</span><span class="sxs-lookup"><span data-stu-id="512c8-312">Issue: Microsoft Visual C++ 2008 runtime libraries are required</span></span>

> <span data-ttu-id="512c8-313">SQL Server Compact 4.0 のネイティブ Dll には、Microsoft Visual C++ 2008 ランタイムライブラリ (X86、IA64、X64) Service Pack 1 が必要です。</span><span class="sxs-lookup"><span data-stu-id="512c8-313">The native DLLs of SQL Server Compact 4.0 need the Microsoft Visual C++ 2008 Runtime Libraries (x86, IA64, and x64), Service Pack 1.</span></span>
> 
> <span data-ttu-id="512c8-314">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-314">**Workaround**</span></span>  
> <span data-ttu-id="512c8-315">.NET Framework 3.5 SP1 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-315">Install the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="512c8-316">これにより、Visual C++ 2008 ランタイムライブラリ SP1 もインストールされます。</span><span class="sxs-lookup"><span data-stu-id="512c8-316">This also installs the Visual C++ 2008 Runtime Libraries SP1.</span></span> <span data-ttu-id="512c8-317">ライブラリは次の場所からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="512c8-317">You can download the libraries from the following location:</span></span>   
>   
> [<span data-ttu-id="512c8-318">Microsoft Visual C++ 2008 Service Pack 1 再頒布可能パッケージ ATL のセキュリティ更新プログラム</span><span class="sxs-lookup"><span data-stu-id="512c8-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package ATL Security Update</span></span>](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> <span data-ttu-id="512c8-319">.NET Framework 2.0、3.0、または4をインストールしても、Visual C++ 2008 RUNTIME library SP1 はインストール*されない*ことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="512c8-319">Note that installing the .NET Framework 2.0, 3.0, or 4 does *not* install the Visual C++ 2008 Runtime Libraries SP1.</span></span>

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a><span data-ttu-id="512c8-320">問題: コンピューターに .NET Framework をインストールする前に SQL Server Compact がインストールされている場合、そのプロバイダーの不変名は .NET Framework の machine.config ファイルに登録されていません。</span><span class="sxs-lookup"><span data-stu-id="512c8-320">Issue: If SQL Server Compact is installed prior to installing .NET Framework on the computer, its provider invariant name is not registered in the .NET Framework machine.config file</span></span>

> <span data-ttu-id="512c8-321">SQL Server Compact には .NET Framework が必要なため、.NET Framework がインストールされていないコンピューターに SQL Server Compact をインストールできます。</span><span class="sxs-lookup"><span data-stu-id="512c8-321">SQL Server Compact can be installed on a machine that does not have .NET Framework installed because SQL Server Compact does require the .NET framework.</span></span> <span data-ttu-id="512c8-322">SQL Server Compact をインストールする前に .NET Framework バージョン3.5 と4の両方がインストールされていない場合、SQL Server Compact セットアップでは、プロバイダーの不変名が*machine.config ファイルに*登録されません。</span><span class="sxs-lookup"><span data-stu-id="512c8-322">If neither .NET Framework version 3.5 nor 4 is installed before you install SQL Server Compact, the SQL Server Compact Setup does not register its provider invariant name in the *machine.config* file.</span></span> <span data-ttu-id="512c8-323">*Machine.config*ファイルの SQL Server Compact エントリに依存するアプリケーションはすべて失敗します。</span><span class="sxs-lookup"><span data-stu-id="512c8-323">Any application that relies on the SQL Server Compact entry in the *machine.config* file will fail.</span></span> <span data-ttu-id="512c8-324">*Machine.config*の不変名の登録エントリは、次の例のようになります。</span><span class="sxs-lookup"><span data-stu-id="512c8-324">The invariant name registration entry in *machine.config* looks like the following example:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> <span data-ttu-id="512c8-325">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-325">**Workaround**</span></span>  
> <span data-ttu-id="512c8-326">SQL Server Compact 4.0 CTP1 をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-326">Uninstall SQL Server Compact 4.0 CTP1.</span></span> <span data-ttu-id="512c8-327">次の場所から .NET Framework の完全なバージョンをダウンロードしてインストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-327">Download and install the full versions of the .NET Framework from the following location:</span></span>
> 
> [<span data-ttu-id="512c8-328">Microsoft .NET Framework 3.5 Service pack 1 (フルパッケージ)</span><span class="sxs-lookup"><span data-stu-id="512c8-328">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [<span data-ttu-id="512c8-329">Microsoft .NET Framework 4.0 リリース (完全なパッケージ)</span><span class="sxs-lookup"><span data-stu-id="512c8-329">Microsoft .NET Framework 4.0 Release (Full Package)</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> <span data-ttu-id="512c8-330">[SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)を再インストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-330">Then reinstall [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span></span>

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a><span data-ttu-id="512c8-331">アプリケーションのインストール</span><span class="sxs-lookup"><span data-stu-id="512c8-331">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="512c8-332">問題: ユーザーの [マイドキュメント] フォルダーがネットワーク共有にリダイレクトされると、アプリケーションのインストールに時間がかかることがある</span><span class="sxs-lookup"><span data-stu-id="512c8-332">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="512c8-333">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-333">**Workaround**</span></span>  
> <span data-ttu-id="512c8-334">[なし] :</span><span class="sxs-lookup"><span data-stu-id="512c8-334">None.</span></span> <span data-ttu-id="512c8-335">アプリケーションのインストールには時間がかかる場合がありますが、正しくインストールされます。</span><span class="sxs-lookup"><span data-stu-id="512c8-335">The application might take a while to install, but will install correctly.</span></span>

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a><span data-ttu-id="512c8-336">アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="512c8-336">Publishing Applications</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="512c8-337">問題: [宛先 URL] フィールドに http://または https://のプレフィックスが付いていないと、発行後にサイトが機能しない場合がある</span><span class="sxs-lookup"><span data-stu-id="512c8-337">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="512c8-338">**[発行の設定]** ダイアログボックスで、インストール先の URL が `http://` または `https://`で始まらない場合は、展開後にサイトが動作しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-338">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="512c8-339">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-339">**Workaround**</span></span>  
> <span data-ttu-id="512c8-340">サイトを発行する前に、 **[発行の設定]** ダイアログボックスの目的の URL が `http://` または `https://`で始まることを確認します。</span><span class="sxs-lookup"><span data-stu-id="512c8-340">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="512c8-341">問題点: MySQL データベースの公開が失敗し、"データベースをパブリッシュできませんでした。</span><span class="sxs-lookup"><span data-stu-id="512c8-341">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="512c8-342">これは、リモートデータベースがスクリプトを実行できない場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-342">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="512c8-343">このエラーは、さまざまな理由で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="512c8-343">The error can occur for a number of reasons.</span></span> <span data-ttu-id="512c8-344">このエラーが表示される理由の1つは、データベーススクリプトに単一引用符 (') が含まれていて、MySQL データベースの既定の文字セットが UTF-8 に設定されていない場合です。</span><span class="sxs-lookup"><span data-stu-id="512c8-344">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="512c8-345">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-345">**Workaround**</span></span>  
> <span data-ttu-id="512c8-346">リモート MySQL データベースの既定の文字セットを UTF-8 に設定します。</span><span class="sxs-lookup"><span data-stu-id="512c8-346">Set the default character set for the remote MySQL database to UTF-8.</span></span>

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a><span data-ttu-id="512c8-347">その他の問題</span><span class="sxs-lookup"><span data-stu-id="512c8-347">Other Issues</span></span>

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a><span data-ttu-id="512c8-348">問題: [グループ化] のレポートで検索/フィルターが機能しない: 問題の種類</span><span class="sxs-lookup"><span data-stu-id="512c8-348">Issue: Search/Filter does not work in Reports for Group By: Issue Type</span></span>

> <span data-ttu-id="512c8-349">サイトのレポートを実行するときに、[ *URL でフィルター* ] ボックスにテキストを入力して [*検索*] をクリックした場合、何も起こりません。</span><span class="sxs-lookup"><span data-stu-id="512c8-349">When you run a report for a site, if you enter text in the *Filter by URL* box and click *Search*, nothing happens.</span></span> <span data-ttu-id="512c8-350">これは、レポートの [*グループ化*の状態] が [*問題の種類*] (既定) に設定されている場合に、このコントロールが機能しないためです。</span><span class="sxs-lookup"><span data-stu-id="512c8-350">This is because this control is not functional while the *Group By* state of the report is set to *Issue Type*, which is the default.</span></span>
> 
> <span data-ttu-id="512c8-351">**回避策**リボンの [*グループ化*] タブで、[ *url* ] をクリックして、ソース url でエントリをグループ化します。</span><span class="sxs-lookup"><span data-stu-id="512c8-351">**Workaround** In the *Group By* tab of ribbon, click *URL* to group the entries by their source URL.</span></span> <span data-ttu-id="512c8-352">この状態では、エントリをフィルター処理するためのテキストボックスとボタンが機能します。</span><span class="sxs-lookup"><span data-stu-id="512c8-352">The text box and button to filter the entries are functional while in this state.</span></span>

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a><span data-ttu-id="512c8-353">問題: WCF アプリケーションを IIS Express で実行できない</span><span class="sxs-lookup"><span data-stu-id="512c8-353">Issue: WCF applications fail to run with IIS Express</span></span>

> <span data-ttu-id="512c8-354">WCF アプリケーションを参照すると、次のようなエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="512c8-354">Browsing to a WCF application results in an error like the following one:</span></span>
> 
> <span data-ttu-id="512c8-355">*ファイルまたはアセンブリ ' 7.0.0.0, Version =, Culture = ニュートラル, PublicKeyToken = 31bf3856ad364e35 ' またはその依存関係の1つが読み込めませんでした。指定されたファイルが見つかりません。*</span><span class="sxs-lookup"><span data-stu-id="512c8-355">*Could not load file or assembly 'Microsoft.Web.Administration, Version=7.0.0.0, Culture=neutral,PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.*</span></span>
> 
> <span data-ttu-id="512c8-356">これは IIS Express ベータリリースでは、既定では WCF がサポートされていないために発生します。</span><span class="sxs-lookup"><span data-stu-id="512c8-356">This occurs because IIS Express Beta release doesn't support WCF by default.</span></span>
> 
> <span data-ttu-id="512c8-357">**回避策**次のいずれかの回避策を使用してください (回避 #2 には、Microsoft Windows Vista 以降が必要です)。</span><span class="sxs-lookup"><span data-stu-id="512c8-357">**Workaround** Use any one of the following workarounds (workaround #2 requires Microsoft Windows Vista or higher):</span></span>
> 
> 
> 1. <span data-ttu-id="512c8-358">WebMatrix のインストール場所から、WCF アプリケーションの*bin*ディレクトリに、 *microsoft Web .dll*および*microsoft. web.config*アセンブリをコピーします。</span><span class="sxs-lookup"><span data-stu-id="512c8-358">Copy the *Microsoft.Web.dll* and *Microsoft.Web.Administration.dll* assemblies from the WebMatrix installation location to the *bin* directory of the WCF application.</span></span> <span data-ttu-id="512c8-359">既定では、WebMatrix は、システムの*Program Files*フォルダーの下にある*Microsoft webmatrix*サブフォルダーにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="512c8-359">By default, WebMatrix is installed in the *Microsoft WebMatrix* subfolder under the system's *Program Files* folder.</span></span>
> 2. <span data-ttu-id="512c8-360">Microsoft Windows Vista 以降では、次のコマンドを使用して、 *bin*ディレクトリ内のアセンブリへのシンボリックリンクを作成します。</span><span class="sxs-lookup"><span data-stu-id="512c8-360">On Microsoft Windows Vista or higher, create a symlink to the assemblies in the *bin* directory using the following commands.</span></span> <span data-ttu-id="512c8-361">(このアプローチには、アセンブリのコピーを作成しないという利点があります)。</span><span class="sxs-lookup"><span data-stu-id="512c8-361">(This approach has the advantage that it does not create a copy of the assemblies.)</span></span>
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. <span data-ttu-id="512c8-362">2つのアセンブリを GAC にインストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-362">Install the two assemblies in the GAC.</span></span> <span data-ttu-id="512c8-363">管理者特権のプロンプトで、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="512c8-363">From an elevated prompt, run the following commands:</span></span>
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="512c8-364">問題: WebMatrix Beta 3 は、昇格が必要な特定のタスクを実行できない</span><span class="sxs-lookup"><span data-stu-id="512c8-364">Issue: WebMatrix Beta 3 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="512c8-365">WebMatrix Beta 3 では、次の状況での追加コンポーネントのインストールなど、昇格が必要な特定のタスクを実行できません。</span><span class="sxs-lookup"><span data-stu-id="512c8-365">WebMatrix Beta 3 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="512c8-366">Windows Vista または Windows 7 では、管理者特権を持たないアカウントを使用してログインし、ユーザーアカウント制御 (UAC) が無効になっています。</span><span class="sxs-lookup"><span data-stu-id="512c8-366">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="512c8-367">Microsoft Windows XP または Microsoft Windows Server 2003 を使用している。</span><span class="sxs-lookup"><span data-stu-id="512c8-367">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="512c8-368">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-368">**Workaround**</span></span>  
> <span data-ttu-id="512c8-369">WebMatrix Beta 3 のほとんどのタスクには、管理者権限は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="512c8-369">Most tasks in WebMatrix Beta 3 do not require administrative permission.</span></span> <span data-ttu-id="512c8-370">そのためには、管理者として操作を実行するか、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="512c8-370">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="512c8-371">Windows Vista または Windows 7 では、UAC を有効にします。</span><span class="sxs-lookup"><span data-stu-id="512c8-371">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="512c8-372">Windows XP では、ユーザーを管理者セキュリティグループに追加します。</span><span class="sxs-lookup"><span data-stu-id="512c8-372">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="512c8-373">問題: "Web ギャラリーからのサイト" が無効になっています</span><span class="sxs-lookup"><span data-stu-id="512c8-373">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="512c8-374">Web Platform Installer 3.0 がインストールされていない場合、 **[Web ギャラリーからのサイト]** オプションは無効になっています。</span><span class="sxs-lookup"><span data-stu-id="512c8-374">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="512c8-375">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-375">**Workaround**</span></span>  
> <span data-ttu-id="512c8-376">[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)をインストールします。</span><span class="sxs-lookup"><span data-stu-id="512c8-376">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a><span data-ttu-id="512c8-377">問題: Windows Server 2003 で、管理者以外のユーザーに対して IIS Express が開始しない</span><span class="sxs-lookup"><span data-stu-id="512c8-377">Issue: On Windows Server 2003, IIS Express does not start for a non-administrative user</span></span>

> <span data-ttu-id="512c8-378">Windows Server 2003 では、ページを起動したり IIS Express を開始したりしても、IIS Express は開始されません。</span><span class="sxs-lookup"><span data-stu-id="512c8-378">On Windows Server 2003, when you launch a page or start IIS Express, IIS Express does not start.</span></span> <span data-ttu-id="512c8-379">Web ページの場合、管理者以外のユーザーによってアプリケーションが起動されたことを示すエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="512c8-379">For Web pages, an error is displayed that indicates that the application has been started by a non-administrative user.</span></span>
> 
> <span data-ttu-id="512c8-380">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-380">**Workaround**</span></span>  
> <span data-ttu-id="512c8-381">WebMatrix Beta 3 を管理ユーザーとして起動します。</span><span class="sxs-lookup"><span data-stu-id="512c8-381">Start WebMatrix Beta 3 as an administrative user.</span></span> <span data-ttu-id="512c8-382">詳細については、次のサポート技術情報を参照してください。</span><span class="sxs-lookup"><span data-stu-id="512c8-382">For more details, see the following KnowledgeBase article:</span></span>  
>   
> [<span data-ttu-id="512c8-383">管理者以外のユーザーによって起動されたアプリケーションは、Windows Vista、Windows Server 2003、または Windows XP でアプリケーションが実行されているコンピューターの HTTP トラフィックをリッスンできません。</span><span class="sxs-lookup"><span data-stu-id="512c8-383">An application that is started by a non-administrative user cannot listen to the HTTP traffic of the computer on which the application is running in Windows Vista, Windows Server 2003, or Windows XP.</span></span>](https://support.microsoft.com/kb/939786)

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="512c8-384">問題: Google Chrome は Run オプションとして使用できません</span><span class="sxs-lookup"><span data-stu-id="512c8-384">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="512c8-385">Google Chrome は、 **[ホーム]** タブの **[実行]** にあるブラウザーの一覧に表示されません。</span><span class="sxs-lookup"><span data-stu-id="512c8-385">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="512c8-386">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-386">**Workaround**</span></span>  
> <span data-ttu-id="512c8-387">Google Chrome の一部のバージョンは、Windows の既定のプログラム機能に正しく登録されません。</span><span class="sxs-lookup"><span data-stu-id="512c8-387">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="512c8-388">回避策として、Google Chrome を起動し、[ *Google chrome* ] メニューをクリックして、[*オプション*] をクリックし、[ *google chrome の既定のブラウザーを作成*する] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="512c8-388">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="512c8-389">問題点: [外部キー] ダイアログボックスで主キーを入力できない</span><span class="sxs-lookup"><span data-stu-id="512c8-389">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="512c8-390">**[外部キー]** ダイアログボックスでは、主キーテーブルの主キーの名前を入力することはできません。</span><span class="sxs-lookup"><span data-stu-id="512c8-390">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="512c8-391">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-391">**Workaround**</span></span>  
> <span data-ttu-id="512c8-392">これは意図的なものであり、</span><span class="sxs-lookup"><span data-stu-id="512c8-392">This is intentional.</span></span> <span data-ttu-id="512c8-393">主キーテーブルの主キーの名前を入力する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="512c8-393">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-the-relationships-button-is-disabled"></a><span data-ttu-id="512c8-394">問題: [リレーションシップ] ボタンが無効になっている</span><span class="sxs-lookup"><span data-stu-id="512c8-394">Issue: The "Relationships" button is disabled</span></span>

> <span data-ttu-id="512c8-395">SQL Server Compact データベースでは、 **[データベース]** ワークスペースの **[テーブル]** タブの下にある **[リレーションシップ]** ボタンは無効になっています。</span><span class="sxs-lookup"><span data-stu-id="512c8-395">The **Relationships** button under the **Table** tab in the **Databases** workspace is disabled for SQL Server Compact databases.</span></span>
> 
> <span data-ttu-id="512c8-396">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-396">**Workaround**</span></span>  
> <span data-ttu-id="512c8-397">[なし] :</span><span class="sxs-lookup"><span data-stu-id="512c8-397">None.</span></span> <span data-ttu-id="512c8-398">SQL Server Compact はテーブル間のリレーションシップをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="512c8-398">SQL Server Compact does not support relationships between tables.</span></span>

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a><span data-ttu-id="512c8-399">問題点: パラメーター化された SQL クエリで例外がスローされる</span><span class="sxs-lookup"><span data-stu-id="512c8-399">Issue: Parameterized SQL queries throw exceptions</span></span>

> <span data-ttu-id="512c8-400">SQL Server Compact 4.0 では、パラメーター化クエリのパラメーターに `SqlDbType` や `DbType` などのデータ型を指定しなかった場合、クエリの実行時に例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="512c8-400">In SQL Server Compact 4.0, if you do not specify a data type such as `SqlDbType` or `DbType` for parameters in parameterized queries, an exception is thrown when the query runs.</span></span>
> 
> <span data-ttu-id="512c8-401">**回避策**</span><span class="sxs-lookup"><span data-stu-id="512c8-401">**Workaround**</span></span>  
> <span data-ttu-id="512c8-402">`SqlDbType` や `DbType`などのパラメーターのデータ型を明示的に設定します。</span><span class="sxs-lookup"><span data-stu-id="512c8-402">Explicitly set the data type for parameters such as `SqlDbType` or `DbType`.</span></span> <span data-ttu-id="512c8-403">これは、BLOB データ型 (`image` および `ntext`) の場合に重要です。</span><span class="sxs-lookup"><span data-stu-id="512c8-403">This is critical in the case of BLOB data types (`image` and `ntext`).</span></span> <span data-ttu-id="512c8-404">次のようなコードを使用します。</span><span class="sxs-lookup"><span data-stu-id="512c8-404">Use code like the following:</span></span>
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="512c8-405">詳細情報</span><span class="sxs-lookup"><span data-stu-id="512c8-405">For More Information</span></span>

<span data-ttu-id="512c8-406">WebMatrix Beta 3 の詳細については、次の web サイトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="512c8-406">For more information about WebMatrix Beta 3, see the following websites:</span></span>

- [<span data-ttu-id="512c8-407">IIS.net</span><span class="sxs-lookup"><span data-stu-id="512c8-407">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="512c8-408">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="512c8-408">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="512c8-409">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="512c8-409">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

---

<span data-ttu-id="512c8-410">© 2010 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="512c8-410">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="512c8-411">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="512c8-411">All Rights Reserved.</span></span> <span data-ttu-id="512c8-412">[使用条件](https://msdn.microsoft.cos/cc300389.aspx)。</span><span class="sxs-lookup"><span data-stu-id="512c8-412">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
