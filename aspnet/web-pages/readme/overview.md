---
uid: web-pages/readme/overview
title: WebMatrix のリリース ノート |Microsoft Docs
author: rick-anderson
description: WebMatrix と ASP.NET Web Pages (Razor) 1.0 リリースの Readme
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65133190"
---
# <a name="webmatrix-readme"></a><span data-ttu-id="c6e60-103">WebMatrix Readme</span><span class="sxs-lookup"><span data-stu-id="c6e60-103">WebMatrix Readme</span></span>

<span data-ttu-id="c6e60-104">2011 年 1 月 13日</span><span class="sxs-lookup"><span data-stu-id="c6e60-104">13 January 2011</span></span>

## <a name="contents"></a><span data-ttu-id="c6e60-105">目次</span><span class="sxs-lookup"><span data-stu-id="c6e60-105">Contents</span></span>

> [!NOTE]
> <span data-ttu-id="c6e60-106">この readme は WebMatrix の 1.0 リリースに適用されます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-106">This readme applies to the 1.0 release of WebMatrix.</span></span>

- [<span data-ttu-id="c6e60-107">概要</span><span class="sxs-lookup"><span data-stu-id="c6e60-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="c6e60-108">インストール</span><span class="sxs-lookup"><span data-stu-id="c6e60-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="c6e60-109">アプリケーションを発行する方法</span><span class="sxs-lookup"><span data-stu-id="c6e60-109">How to Publish Applications</span></span>](#InstructionsForPublishingApplications)
- [<span data-ttu-id="c6e60-110">変更点と問題</span><span class="sxs-lookup"><span data-stu-id="c6e60-110">Changes and Issues</span></span>](#ChangesAndIssues)

    - [<span data-ttu-id="c6e60-111">WebMatrix 1.0 のインストール</span><span class="sxs-lookup"><span data-stu-id="c6e60-111">WebMatrix 1.0 Installation</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="c6e60-112">ASP.NET Web ページ</span><span class="sxs-lookup"><span data-stu-id="c6e60-112">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="c6e60-113">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="c6e60-113">WebMatrix</span></span>](#Known_Issues_WebMatrix)
    - [<span data-ttu-id="c6e60-114">IIS Express</span><span class="sxs-lookup"><span data-stu-id="c6e60-114">IIS Express</span></span>](#Known_Issues_IISExpress)
    - [<span data-ttu-id="c6e60-115">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="c6e60-115">SQL Server Compact</span></span>](#Known_Issues_SQLServerCompact)
    - [<span data-ttu-id="c6e60-116">アプリケーションのインストール</span><span class="sxs-lookup"><span data-stu-id="c6e60-116">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="c6e60-117">アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="c6e60-117">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
- [<span data-ttu-id="c6e60-118">参照項目</span><span class="sxs-lookup"><span data-stu-id="c6e60-118">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="c6e60-119">概要</span><span class="sxs-lookup"><span data-stu-id="c6e60-119">Overview</span></span>

> <span data-ttu-id="c6e60-120">Microsoft WebMatrix 1.0 は、数分でインストールする無料の web 開発スタックです。</span><span class="sxs-lookup"><span data-stu-id="c6e60-120">Microsoft WebMatrix 1.0 is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="c6e60-121">データベース プログラミング フレームワークが 1 つ、統合されたエクスペリエンスを作成すると、web サーバーが統合されています。</span><span class="sxs-lookup"><span data-stu-id="c6e60-121">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="c6e60-122">WebMatrix を使用して、コーディング、テスト、および独自の ASP.NET または PHP web のサイトを公開する方法を効率化、または WebMatrix を使用して、DotNetNuke、Umbraco、WordPress、Joomla などの一般的なオープン ソース アプリを使用して新しい web サイトを開始することができます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-122">You can use WebMatrix to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="c6e60-123">WebMatrix は、同じ強力な web サーバー、データベース エンジン、および円滑かつシームレスに開発から運用環境への移行を使用すると、インターネット上の web サイトを実行するフレームワークの環境を使用します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-123">WebMatrix uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="c6e60-124">インストール</span><span class="sxs-lookup"><span data-stu-id="c6e60-124">Installation</span></span>

> <span data-ttu-id="c6e60-125">WebMatrix 1.0 をインストールする必要があります最初にインストールする、 [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-125">To install WebMatrix 1.0, you must first install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="c6e60-126">Web Platform Installer をインストールした後は、WebMatrix のインストールに使用できます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-126">After you've installed the Web Platform Installer, you can use it to install WebMatrix.</span></span>
> 
> <span data-ttu-id="c6e60-127">インストール中に問題がある場合を参照してください[Microsoft Web Platform Installer に関する問題をトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=196212)します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-127">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a><span data-ttu-id="c6e60-128">アプリケーションを発行する方法</span><span class="sxs-lookup"><span data-stu-id="c6e60-128">How to Publish Applications</span></span>

> <span data-ttu-id="c6e60-129">参照してください[でアプリケーションを公開する手順](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="c6e60-129">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a><span data-ttu-id="c6e60-130">変更点と問題</span><span class="sxs-lookup"><span data-stu-id="c6e60-130">Changes and Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a><span data-ttu-id="c6e60-131">WebMatrix 1.0 のインストールに関する問題</span><span class="sxs-lookup"><span data-stu-id="c6e60-131">WebMatrix 1.0 Installation Issues</span></span>

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="c6e60-132">問題:WebMatrix 1.0 は Microsoft .NET Framework 4 をサポートするプラットフォームでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-132">Issue: WebMatrix 1.0 is available only on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="c6e60-133">.NET Framework version 4 が WebMatrix に必要です。</span><span class="sxs-lookup"><span data-stu-id="c6e60-133">The .NET Framework version 4 is required for WebMatrix.</span></span> <span data-ttu-id="c6e60-134">場合によっては、WebMatrix 1.0 インストーラーができます、サポートされている構成セットの一部ではないプラットフォームをインストールしようとしています。</span><span class="sxs-lookup"><span data-stu-id="c6e60-134">In certain cases, the WebMatrix 1.0 installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="c6e60-135">具体的には、Windows Vista SP1 更新プログラムがないと、WebMatrix のインストールを開始するが、.NET Framework 4 のコンポーネントは失敗し、インストールをブロックします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-135">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="c6e60-136">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-136">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-137">含む、サポートされているプラットフォームにインストールします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-137">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="c6e60-138">Windows 7</span><span class="sxs-lookup"><span data-stu-id="c6e60-138">Windows 7</span></span>
> - <span data-ttu-id="c6e60-139">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="c6e60-139">Windows Server 2008</span></span>
> - <span data-ttu-id="c6e60-140">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c6e60-140">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="c6e60-141">Windows Vista SP1 以降</span><span class="sxs-lookup"><span data-stu-id="c6e60-141">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="c6e60-142">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="c6e60-142">Windows XP SP3</span></span>
> - <span data-ttu-id="c6e60-143">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="c6e60-143">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="c6e60-144">問題:Microsoft Visual Studio 2008 SP1 がない場合に Microsoft Visual Studio 2008 がインストールされている場合、WebMatrix 1.0 をインストールことはできません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-144">Issue: Cannot install WebMatrix 1.0 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="c6e60-145">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-145">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-146">インストール[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) Microsoft ダウンロード センターから。</span><span class="sxs-lookup"><span data-stu-id="c6e60-146">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="c6e60-147">問題:SQL Server Compact 4.0 の一部のアセンブリが GAC にインストールされていません</span><span class="sxs-lookup"><span data-stu-id="c6e60-147">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="c6e60-148">64 ビット コンピューターで SQL Server Compact 4.0 をインストールして、コンピューターにのみ、.NET Framework 3.5 SP1 Client Profile インストールされているときに、SQL Server Compact 4.0 のマネージ アセンブリがグローバル アセンブリ キャッシュ (GAC) に配置されていません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-148">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="c6e60-149">マネージ アセンブリを GAC にインストールされていない次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="c6e60-149">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="c6e60-150">*System.Data.SqlServerCe.dll* (ADO.NET プロバイダー)</span><span class="sxs-lookup"><span data-stu-id="c6e60-150">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="c6e60-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span><span class="sxs-lookup"><span data-stu-id="c6e60-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="c6e60-152">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-152">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-153">アンインストールの SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="c6e60-153">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="c6e60-154">ダウンロードして、次の場所から、フル バージョンの .NET Framework 3.5 SP1 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-154">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="c6e60-155">Microsoft .NET Framework 3.5 Service pack 1 (フル パッケージ)</span><span class="sxs-lookup"><span data-stu-id="c6e60-155">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="c6e60-156">SQL Server Compact 4.0 を再インストールします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-156">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="c6e60-157">問題:SQL Server Compact のコマンドラインを使用してアンインストールできません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-157">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="c6e60-158">SQL Server Compact のコマンド ライン オプションを使用してのアンインストールは、このリリースでは機能しません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-158">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="c6e60-159">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-159">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-160">使用*プログラムと機能*Windows コントロール パネルの Microsoft SQL Server Compact 4.0 をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-160">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="c6e60-161">ASP.NET Web ページ</span><span class="sxs-lookup"><span data-stu-id="c6e60-161">ASP.NET Web Pages</span></span>

<span data-ttu-id="c6e60-162">ドキュメントのこのセクションでは、新機能、変更、および Razor 構文を使用して ASP.NET Web Pages の 1.0 リリースの既知の問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-162">This section of the document describes new features, changes, and known issues with the 1.0 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="c6e60-163">新機能</span><span class="sxs-lookup"><span data-stu-id="c6e60-163">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="c6e60-164">変更</span><span class="sxs-lookup"><span data-stu-id="c6e60-164">Changes</span></span>](#Changes)
- [<span data-ttu-id="c6e60-165">問題</span><span class="sxs-lookup"><span data-stu-id="c6e60-165">Issues</span></span>](#Issues)

#### <a id="NewFeatures"></a>  <span data-ttu-id="c6e60-166">新機能</span><span class="sxs-lookup"><span data-stu-id="c6e60-166">New Features</span></span>

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a><span data-ttu-id="c6e60-167">新規 : パッケージ マネージャーを無効にする構成設定の追加</span><span class="sxs-lookup"><span data-stu-id="c6e60-167">New: Configuration setting added to disable the package manager</span></span>

> <span data-ttu-id="c6e60-168">新しい`asp:AdminManagerEnabled`キーが利用可能、`<appSettings>`内の要素、 *web.config*ファイルで、パッケージ マネージャーを完全に無効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-168">A new `asp:AdminManagerEnabled` key is available for the `<appSettings>` element in the *web.config* file, which lets you completely disable the package manager.</span></span> <span data-ttu-id="c6e60-169">この要素の既定値は true、存在してしない場合、つまり、 *web.config*ファイル、パッケージ マネージャーを有効にします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-169">The default value for this element is true, meaning that if it is not included in the *web.config* file, the package manager is enabled.</span></span> <span data-ttu-id="c6e60-170">パッケージ マネージャーを無効にするには、次の要素を追加、 *web.config* web サイトのルートにあるファイル。</span><span class="sxs-lookup"><span data-stu-id="c6e60-170">To disable the package manager, add the following element to the *web.config* file in the root of the website:</span></span>
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a>  <span data-ttu-id="c6e60-171">変更</span><span class="sxs-lookup"><span data-stu-id="c6e60-171">Changes</span></span>

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a><span data-ttu-id="c6e60-172">変更:"webPages:AdminFolderVirtualPath"キーを"Asp:adminfoldervirtualpath"に変更されました</span><span class="sxs-lookup"><span data-stu-id="c6e60-172">Change: "webPages:AdminFolderVirtualPath" key renamed to "asp:AdminFolderVirtualPath"</span></span>

> <span data-ttu-id="c6e60-173">`webPages:AdminFolderVirtualPath`キーに追加することができますが、 *web.config*を使用して、パッケージ マネージャーの場所を指定するファイルの名前は、`asp:`名前空間の代わりに、`webPages`名前空間。</span><span class="sxs-lookup"><span data-stu-id="c6e60-173">The `webPages:AdminFolderVirtualPath` key that can be added to the *web.config* file to specify the location of the package manager has been renamed to use the `asp:` namespace instead of the `webPages` namespace.</span></span> <span data-ttu-id="c6e60-174">この要素を使用している場合は、構成ファイルで変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-174">If you have used this element, you must rename it in the configuration file.</span></span>

#### <a id="Issues"></a>  <span data-ttu-id="c6e60-175">既知の問題</span><span class="sxs-lookup"><span data-stu-id="c6e60-175">Known Issues</span></span>

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a><span data-ttu-id="c6e60-176">問題:認識されないメンバーシップ ユーザーのパスワード</span><span class="sxs-lookup"><span data-stu-id="c6e60-176">Issue: Passwords for membership users no longer recognized</span></span>

> <span data-ttu-id="c6e60-177">安全な作成とメンバーシップ (ログイン) パスワードを格納するためのアルゴリズムが変更されました。</span><span class="sxs-lookup"><span data-stu-id="c6e60-177">The algorithm for creating and storing membership (login) passwords has been changed to be more secure.</span></span> <span data-ttu-id="c6e60-178">その結果、ASP.NET Razor のベータ版で作成されたメンバー (ユーザー) に格納されているパスワードは認識されません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-178">As a result, the passwords stored for members (users) created in Beta versions of ASP.NET Razor will not be recognized.</span></span> 
> 
> <span data-ttu-id="c6e60-179">**回避策**サイトが運用環境にまだ配置されていない場合は、メンバーシップ データベースからユーザー レコードを削除します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-179">**Workaround** If the site has not yet been put into production, remove the user records from the membership database.</span></span> <span data-ttu-id="c6e60-180">データベースがライブの場合は、プログラムでメンバーシップ データベース内の既存のパスワードを再生成します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-180">If database is live, programmatically regenerate existing passwords in the membership database.</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="c6e60-181">問題:メンバーシップのカスタム ユーザー テーブルを使用する場合、予期しない動作</span><span class="sxs-lookup"><span data-stu-id="c6e60-181">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="c6e60-182">ASP.NET Razor の web サイトのメンバーシップ プロバイダーを初期化するために呼び出す、`WebSecurity.InitializeDatabaseConnection`メソッド。</span><span class="sxs-lookup"><span data-stu-id="c6e60-182">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="c6e60-183">(WebMatrix で、スターター サイト テンプレートには、このメソッドの呼び出しが含まれています、  *\_AppStart.cshtml*ファイルです)。場合、`autoCreateTables`このメソッドのパラメーターの設定を true に (に既定では、設定は、スターター サイト テンプレートの場合は true)、メソッドがエラーをスローしない場合は、認識できないテーブル名は、(2 番目のパラメーター) のメソッドに渡されます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-183">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="c6e60-184">代わりに、テーブルを自動的に作成します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-184">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="c6e60-185">これをカスタム ユーザー テーブルを使用して、メンバーシップが間違ったテーブル名を渡すする場合、問題になることができます、`WebSecurity.InitializeDatabaseConnection`メソッド。</span><span class="sxs-lookup"><span data-stu-id="c6e60-185">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="c6e60-186">メソッドは既定では、エラーは発生を指定するテーブルが存在しない場合、代わりに新しいテーブルを作成するため、アプリケーションが動作して表示できます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-186">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="c6e60-187">ただし、カスタム ユーザー テーブル (および内のフィールド) に依存しているアプリケーション コード最終的に予期しないエラーで失敗します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-187">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="c6e60-188">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-188">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-189">渡された名前を確認、`InitializeDatabaseConnection`メソッドと一致するユーザー プロファイル、メンバーシップ データベースにテーブルまたはことを確認、`autoCreateTables`パラメーターが false に設定します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-189">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-error-message-the-admin-module-requires-access-to-appdata"></a><span data-ttu-id="c6e60-190">問題:エラー メッセージ"Admin モジュールでは、~/App へのアクセスを必要と\_データ"</span><span class="sxs-lookup"><span data-stu-id="c6e60-190">Issue: Error message "The Admin Module requires access to ~/App\_Data"</span></span>

> <span data-ttu-id="c6e60-191">状況によっては、ユーザーを作成したり、それ以外の場合、ASP.NET メンバーシップ システムを使用しようとした可能性があります、エラーを表示するページ*Admin モジュールでは、~/App へのアクセスを必要と\_データ*します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-191">Under some circumstances, trying to create users or otherwise work with the ASP.NET membership system can cause the page to display the error *The Admin Module requires access to ~/App\_Data*.</span></span> <span data-ttu-id="c6e60-192">これは、IIS または IIS Express を実行しているアカウントが作成およびへの書き込みアクセス許可を持たない場合に発生します、*アプリ\_データ*web サイトのルートの下のフォルダー。</span><span class="sxs-lookup"><span data-stu-id="c6e60-192">This occurs if the account that IIS or IIS Express is running under does not have permissions to create and write to the *App\_Data* folder under the website root.</span></span> 
> 
> <span data-ttu-id="c6e60-193">**回避策**を手動で作成、*アプリ\_データ*web サイトのフォルダー。</span><span class="sxs-lookup"><span data-stu-id="c6e60-193">**Workaround** Manually create an *App\_Data* folder for the website.</span></span> <span data-ttu-id="c6e60-194">(通常は NETWORK SERVICE) でアプリケーションを実行する Windows アカウントが、アプリケーションのルート フォルダーとサブフォルダー アプリなどの読み取り/書き込みアクセス許可を持っているかどうかを確認して\_データ。</span><span class="sxs-lookup"><span data-stu-id="c6e60-194">Then make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as App\_Data.</span></span> <span data-ttu-id="c6e60-195">詳細については、サポート技術情報の記事で使用可能な[SQL Server Express ユーザー インスタンスと ASP.net Web アプリケーション プロジェクトに関する問題を](https://support.microsoft.com/kb/2002980)します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-195">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="c6e60-196">問題:「SQL Server のユーザー インスタンスの生成に失敗しました」エラー</span><span class="sxs-lookup"><span data-stu-id="c6e60-196">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="c6e60-197">WebMatrix Web アプリケーションが SQL Server Express を使用して、Windows 7 または Windows Server 2008 R2 に IIS 7.5 を実行している場合は、SQL Server が実行時にユーザーのローカル アプリケーション パスを取得できませんかを示すエラーが表示可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-197">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="c6e60-198">**回避策**(通常は NETWORK SERVICE) でアプリケーションを実行する Windows アカウントが、アプリケーションのルート フォルダーとサブフォルダーの読み取り/書き込みアクセス許可をなどがあるかどうかを確認*アプリ\_データ*.</span><span class="sxs-lookup"><span data-stu-id="c6e60-198">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="c6e60-199">詳細については、サポート技術情報の記事で使用可能な[SQL Server Express ユーザー インスタンスと ASP.net Web アプリケーション プロジェクトに関する問題を](https://support.microsoft.com/kb/2002980)します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-199">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a><span data-ttu-id="c6e60-200">問題:パッケージ マネージャーのリソースまたはパッケージ マネージャーのパスワードを含むファイルが IIS 6.0 で提供され、以前</span><span class="sxs-lookup"><span data-stu-id="c6e60-200">Issue: Files that contains package-manager resources or package-manager passwords are servable under IIS 6.0 and earlier</span></span>

> <span data-ttu-id="c6e60-201">RC2 リリースを使用して構築された ASP.NET Web Pages (Razor) アプリケーションをデプロイする場合と、アプリケーションが含まれている場合、 *password.txt*または*packagesources.txt*ファイル */App\_データ/管理者*、IIS 6.0 は要求されると、パッケージ マネージャー インスタンスのパスワードを公開する可能性がある場合は、ファイルにサービスを提供します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-201">If you deploy an ASP.NET Web Pages (Razor) application that was built using the RC2 release, and if the application contains a *password.txt* or *packagesources.txt* file under */App\_Data/admin*, IIS 6.0 will serve the file if requested, potentially exposing the passwords for your package manager instance.</span></span> 
> 
> <span data-ttu-id="c6e60-202">**回避策**の名前を変更、 *password.txt*または*packagesources.txt*ファイルを*password.config*または*packagesources.configに変更します*.既定では、IIS 6.0 ファイルを処理しませんが、 *.config*拡張機能。</span><span class="sxs-lookup"><span data-stu-id="c6e60-202">**Workaround** Rename the *password.txt* or *packagesources.txt* file to *password.config* or *packagesources.config*. By default, IIS 6.0 does not serve files that have the *.config* extension.</span></span> <span data-ttu-id="c6e60-203">(IIS 7 でのファイルはありません、*アプリ\_データ*フォルダーが提供されるは、ので、ファイルの名前を変更する必要はありません)。</span><span class="sxs-lookup"><span data-stu-id="c6e60-203">(In IIS 7, no files in the *App\_Data* folder are served, so you do not need to rename the files.)</span></span>

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a><span data-ttu-id="c6e60-204">問題:Beta 3 リリースを使用してインストールされているパッケージをアンインストールしても、パッケージのコンポーネントは完全に削除しません</span><span class="sxs-lookup"><span data-stu-id="c6e60-204">Issue: Uninstalling packages installed using the Beta 3 release does not completely remove package components</span></span>

> <span data-ttu-id="c6e60-205">ベータ 3 リリースでは、パッケージ マネージャーを使用してパッケージをインストールしてから、現在のリリースを使用してアンインストールを再試行してください。 場合、パッケージは完全にアンインストールされません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-205">If you installed a package using the package manager in the Beta 3 release and then try to uninstall it using the current release, the package is not completely uninstalled.</span></span> <span data-ttu-id="c6e60-206">パッケージ マネージャーの使用**アンインストール**ボタンの一部のコンポーネントを削除しますが、パッケージのライブラリ コードし、は更新されません、 *package.config*ファイル。</span><span class="sxs-lookup"><span data-stu-id="c6e60-206">Using the package manager's **Uninstall** button removes some components, but leaves the package's library code and does not update the *package.config* file.</span></span>
> 
> <span data-ttu-id="c6e60-207">**回避策** </span><span class="sxs-lookup"><span data-stu-id="c6e60-207">**Workaround** </span></span>  
> <span data-ttu-id="c6e60-208">これらの手順に従います。</span><span class="sxs-lookup"><span data-stu-id="c6e60-208">Perform these steps:</span></span>  
> 1. <span data-ttu-id="c6e60-209">削除、*アプリ\_Data\packages*フォルダー。</span><span class="sxs-lookup"><span data-stu-id="c6e60-209">Delete the *App\_Data\packages* folder.</span></span> <span data-ttu-id="c6e60-210">これには、すべてのパッケージが削除されます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-210">This removes all packages.</span></span>   
> 2. <span data-ttu-id="c6e60-211">削除、 *packages.config* web サイトのルートにあるファイル。</span><span class="sxs-lookup"><span data-stu-id="c6e60-211">Delete the *packages.config* file in the root of the website.</span></span>

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a><span data-ttu-id="c6e60-212">問題:Visual Studio で、web ベースのパッケージ マネージャーを呼び出すはアプリケーションをオフライン</span><span class="sxs-lookup"><span data-stu-id="c6e60-212">Issue: In Visual Studio, invoking the web-based package manager takes the application offline</span></span>

> <span data-ttu-id="c6e60-213">Visual Studio (WebMatrix ではなく) で作業しているを使用したかどうか、 *\_管理者*パッケージ マネージャー Visual Studio を起動する機能、アプリケーションをオフラインにして、投稿、*アプリ\_offline.htm*を web サイトのルートに、パッケージ マネージャーを使用する機能を中断されます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-213">If you are working in Visual Studio (not WebMatrix) and use the *\_admin* functionality to start the package manager, Visual Studio takes the application offline and posts the *app\_offline.htm* into the website root, which disrupts your ability to use the package manager.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="c6e60-214">同じ動作には、追加、削除、または内のファイルを変更する場合に発生しますが、通常、web ベースのパッケージ マネージャーのインターフェイスを使用する場合は、この動作を確認した、*アプリ\_データ*フォルダー。</span><span class="sxs-lookup"><span data-stu-id="c6e60-214">Although you would most typically see this behavior when using the web-based package manager interface, the same behavior occurs if you add, remove, or modify any files in the *App\_Data* folder.</span></span>
> 
> <span data-ttu-id="c6e60-215">**回避策** </span><span class="sxs-lookup"><span data-stu-id="c6e60-215">**Workaround** </span></span>  
> <span data-ttu-id="c6e60-216">Visual Studio でパッケージを使用するには、web ベースのパッケージ マネージャーではなく、NuGet 拡張機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-216">To work with packages in Visual Studio, use the NuGet extension instead of the web-based package manager.</span></span> <span data-ttu-id="c6e60-217">詳しくは、次を参照してください。、 [NuGet のドキュメント](https://docs.microsoft.com/nuget/)します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-217">For information, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span> <span data-ttu-id="c6e60-218">他のファイルを使用している場合、*アプリ\_データ*フォルダー、この問題を回避するために別の場所でファイルを残すようにしてください。</span><span class="sxs-lookup"><span data-stu-id="c6e60-218">If you are working with other files in the *App\_Data* folder, consider keeping the files elsewhere to avoid this issue.</span></span> <span data-ttu-id="c6e60-219">ですが実用的でない場合は、削除、*アプリ\_offline.htm*ファイルを手動でまたは自動的に (既定では、30 秒後) で、サイトがオンラインに戻るまで待機します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-219">If that's not practical, delete the *app\_offline.htm* file manually or wait until the site comes back online automatically (by default, after 30 seconds).</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="c6e60-220">問題:Visual Studio IntelliSense およびプロジェクトで使用できるテンプレートのみ ASP.NET MVC version 3</span><span class="sxs-lookup"><span data-stu-id="c6e60-220">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="c6e60-221">ASP.NET Web Pages をインストールすることもはインストールされません tools for Visual Studio ASP.NET Web Pages アプリケーション用の IntelliSense およびプロジェクトのテンプレートなど。</span><span class="sxs-lookup"><span data-stu-id="c6e60-221">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="c6e60-222">**回避策**を Visual Studio での ASP.NET Web Pages アプリケーション用の IntelliSense およびプロジェクト テンプレートを使用するインストール ASP.NET MVC 3 RC、Web Platform Installer を使用するか、または[スタンドアロン インストーラー](https://go.microsoft.com/fwlink/?LinkID=191797)します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-222">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="c6e60-223">問題:読み取りフィードまたはプロキシ サーバー経由で他の外部データ</span><span class="sxs-lookup"><span data-stu-id="c6e60-223">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="c6e60-224">プロキシ情報を構成する必要がありますが、サイトを実行しているサーバーがプロキシ サーバーの背後にある場合は、 *web.config*ファイルをサイトの外部から送信される情報を読み取ることができるようにします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-224">If the server running the site is behind a proxy server, you might need to configure proxy information in the *web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="c6e60-225">たとえば、使用する場合、`ReCaptcha`ヘルパー、ヘルパーは、reCAPTCHA サービスと通信がプロキシ サーバーによってブロックされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-225">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="c6e60-226">同様に、フィード、パッケージ マネージャーによって使用されているフィードなどの ASP.NET Web Pages を使用するには、プロキシ構成を必要があります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-226">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="c6e60-227">外部サービスの操作またはパッケージ フィードの操作で問題が発生する場合は、アプリケーションのルートに、次の要素を配置*web.config*ファイル。</span><span class="sxs-lookup"><span data-stu-id="c6e60-227">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *web.config* file:</span></span>
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> <span data-ttu-id="c6e60-228">プロキシ サーバーを構成する方法の詳細については、次を参照してください。 [&lt;プロキシ&gt;要素 (ネットワーク設定)](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN Web サイト。</span><span class="sxs-lookup"><span data-stu-id="c6e60-228">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="c6e60-229">問題:.NET Framework version 4 をアンインストールする Razor 構文を使用して ASP.NET Web ページを無効にします</span><span class="sxs-lookup"><span data-stu-id="c6e60-229">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="c6e60-230">.NET Framework version 4 をアンインストールし、再インストールして、Razor 構文を使用して ASP.NET Web Pages は無効になります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-230">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="c6e60-231">ページで、 *.cshtml*拡張機能が正常に動作しません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-231">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="c6e60-232">ASP.NET Web ページには、マシン ルートのアセンブリが登録されます*web.config*ファイル、および .NET Framework の削除は、そのファイルを削除します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-232">ASP.NET Web Pages registers an assembly in the machine root *web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="c6e60-233">.NET Framework を再インストール、構成ファイルの新しいバージョンがインストールされますが、ASP.NET Web Pages アセンブリの参照を追加できません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-233">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="c6e60-234">**回避策**.NET Framework を再インストール後に Razor 構文を使用する ASP.NET Web ページを再インストールします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-234">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="c6e60-235">次の要素が追加されます、 *web.config*マシンのルートには、通常、次の場所にファイル。</span><span class="sxs-lookup"><span data-stu-id="c6e60-235">This adds the following element to the *web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="c6e60-236">問題:拡張子のない Url に IIS 7 または IIS 7.5.cshtml/.vbhtml ファイルが見つからない</span><span class="sxs-lookup"><span data-stu-id="c6e60-236">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="c6e60-237">IIS 7 または IIS 7.5 では、次のような URL を使用して要求をできないがページを検索、 *.cshtml*または *.vbhtml*拡張機能。</span><span class="sxs-lookup"><span data-stu-id="c6e60-237">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="c6e60-238">この問題は、URL リライトが有効でない既定で IIS 7 または IIS 7.5 のために発生します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-238">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="c6e60-239">考えられるシナリオでは、IIS Express を使用してローカルでテストするときに問題は表示されないが、web サイトをホスティング web サイトにデプロイするときに発生することです。</span><span class="sxs-lookup"><span data-stu-id="c6e60-239">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="c6e60-240">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-240">**Workaround**</span></span>
> 
> - <span data-ttu-id="c6e60-241">インストールで説明されている更新プログラムをサーバー コンピューターの場合は、サーバー コンピューター上のコントロールがある場合は、 [、更新プログラムを処理するために IIS 7.0 または IIS 7.5 のハンドラーは要求 Url を特定できますが、期間で終わっていない利用可能な](https://support.microsoft.com/kb/980368)します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-241">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="c6e60-242">サーバー コンピューター上のコントロールがいないかどうか (たとえばを展開しているホスティング web サイトに) 次に、web サイトの追加*web.config*ファイル。</span><span class="sxs-lookup"><span data-stu-id="c6e60-242">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *web.config* file:</span></span> 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="c6e60-243">問題:SQL Server Compact がインストールされていないコンピューターにアプリケーションを展開します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-243">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="c6e60-244">SQL Server Compact データベースを含むアプリケーションは、SQL Server Compact がインストールされていないコンピューターで実行できます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-244">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="c6e60-245">Microsoft WebMatrix 1.0 は自動的がこれらのバイナリをコピーし、適切な実行*web.config*ファイルの変換。</span><span class="sxs-lookup"><span data-stu-id="c6e60-245">Microsoft WebMatrix 1.0 automatically copies these binaries for you and performs the appropriate *web.config* file transforms.</span></span>
> 
> <span data-ttu-id="c6e60-246">**回避策**これらのファイルをコピーする必要がある場合、 *web.config*ファイルの変更を手動で、次の操作します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-246">**Workaround** If you need to copy these files and make the *web.config* file changes manually, do the following:</span></span>
> 
> 1. <span data-ttu-id="c6e60-247">データベース エンジン アセンブリをコピー、 *Bin*ターゲット コンピューター上のアプリケーションのフォルダー (とサブフォルダー)。</span><span class="sxs-lookup"><span data-stu-id="c6e60-247">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span>  
> 
>    - <span data-ttu-id="c6e60-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span><span class="sxs-lookup"><span data-stu-id="c6e60-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span></span>  
>      <span data-ttu-id="c6e60-249">**to** *\Bin*</span><span class="sxs-lookup"><span data-stu-id="c6e60-249">**to** *\Bin*</span></span>
>    - <span data-ttu-id="c6e60-250">コピー *C:\Program files \microsoft SQL Server Compact Edition\v4.0\Private\x86\\*  **に** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="c6e60-250">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **to** *\Bin\x86*</span></span>
>    - <span data-ttu-id="c6e60-251">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="c6e60-251">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 
> 2. <span data-ttu-id="c6e60-252">Web サイトのルート フォルダーに作成または開き、 *web.config*ファイル。</span><span class="sxs-lookup"><span data-stu-id="c6e60-252">In the root folder of the website, create or open a *web.config* file.</span></span> <span data-ttu-id="c6e60-253">(WebMatrix 1.0 では、このファイルの種類がクリックした場合に使用可能な**すべて**で、**ファイルの種類を選択** ダイアログ ボックス)。</span><span class="sxs-lookup"><span data-stu-id="c6e60-253">(In WebMatrix 1.0, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="c6e60-254">子として次の要素を追加、`<configuration>`要素 (内部ではなく、`<system.web>`要素)。</span><span class="sxs-lookup"><span data-stu-id="c6e60-254">Add the following element as a child of the `<configuration>` element (not inside the `<system.web>` element):</span></span>
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="c6e60-255">問題:"Database"と"の WebGrid"ヘルパーは、Visual Basic で中程度の信頼では機能しません</span><span class="sxs-lookup"><span data-stu-id="c6e60-255">Issue: "Database" and "WebGrid" helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="c6e60-256">Visual Basic を使用している場合 (作成 *.vbhtml*ファイル)、`Database`と`WebGrid`中程度の信頼を使用するアプリケーションが設定されている場合、ヘルパーは機能しません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-256">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="c6e60-257">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-257">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-258">Visual Studio 2010 を使用する場合は、Service Pack 1 リリースをインストールすることによってこの問題を解決できます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-258">If you use Visual Studio 2010, you can resolve this problem by installing the Service Pack 1 release.</span></span> <span data-ttu-id="c6e60-259">SP1 のベータ版をダウンロードするには、SP1 のリリースの最終バージョンが利用されるまで、 [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) Microsoft ダウンロード センター ページ。</span><span class="sxs-lookup"><span data-stu-id="c6e60-259">Until the final version of the SP1 release is available, you can download the Beta version of SP1 from the [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) page on the Microsoft Download Center.</span></span>   
>   
> <span data-ttu-id="c6e60-260">これは実用的ではないかを一時的に Visual Studio 2010 を使用しない場合は、完全な信頼を使用するアプリケーションを設定します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-260">If this is not practical, or if you do not use Visual Studio 2010, you can temporarily set the application to use Full Trust.</span></span>

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a><span data-ttu-id="c6e60-261">問題:"ApplicationPart"リソースにアクセスできる外部</span><span class="sxs-lookup"><span data-stu-id="c6e60-261">Issue: "ApplicationPart" resources are externally accessible</span></span>

> <span data-ttu-id="c6e60-262">アセンブリから派生したオブジェクトに含まれる場合、`ApplicationPart`クラスによって、アセンブリのリソースが公開されること、`ResourceRouteHandler`クラス。</span><span class="sxs-lookup"><span data-stu-id="c6e60-262">If an assembly contains objects that derives from the `ApplicationPart` class, that assembly's resources are exposed by the `ResourceRouteHandler` class.</span></span> <span data-ttu-id="c6e60-263">たとえば、次のような URL があるとします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-263">For example, consider the following URL:</span></span>  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> <span data-ttu-id="c6e60-264">この要求は、リソースの文字列のすべてをダウンロード、 *System.Web.WebPages.Administration.dll*アセンブリ。</span><span class="sxs-lookup"><span data-stu-id="c6e60-264">This request downloads all of the resource strings in the *System.Web.WebPages.Administration.dll* assembly.</span></span> <span data-ttu-id="c6e60-265">すべての埋め込みリソース (もしない静的なコンテンツとして提供することを意図したもの) がダウンロードされます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-265">All of the embedded resources (even those that are not intended to be served as static content) are downloaded.</span></span> <span data-ttu-id="c6e60-266">埋め込みリソースに機密情報が含まれている場合は、セキュリティ上のリスクを表すこのことができます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-266">If the embedded resources contain sensitive information, this can represent a security risk.</span></span> 
> 
> <span data-ttu-id="c6e60-267">**回避策** </span><span class="sxs-lookup"><span data-stu-id="c6e60-267">**Workaround** </span></span>  
> <span data-ttu-id="c6e60-268">作成する場合、 **ApplicationPart**オブジェクト、その埋め込みリソースが関連付けられていることを確認**ApplicationPart**オブジェクトのアセンブリには機密情報が含まれていません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-268">If you create an **ApplicationPart** object, make sure that the embedded resources associated with that **ApplicationPart** object's assembly do not contain sensitive information.</span></span>

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a><span data-ttu-id="c6e60-269">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="c6e60-269">WebMatrix</span></span>

> [!NOTE]
> <span data-ttu-id="c6e60-270">WebMatrix のインストールの問題については、次を参照してください。 [WebMatrix のインストールに関する問題](#Known_Issues_Installation)この文書で前述しました。</span><span class="sxs-lookup"><span data-stu-id="c6e60-270">For information about installation issues for WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

<span data-ttu-id="c6e60-271">ドキュメントのこのセクションでは、WebMatrix 開発環境の既知の問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-271">This section of the document describes known issues for the WebMatrix development environment.</span></span>

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a><span data-ttu-id="c6e60-272">問題:データベース ワークスペースにユーザー名または web.config ファイル内のデータベース接続文字列のパスワードの変更は反映されません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-272">Issue: Changes in the username or password of a database connection string in a web.config file are not reflected in the Databases workspace</span></span>

> <span data-ttu-id="c6e60-273">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-273">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="c6e60-274">*Web.config*ファイルで、接続文字列でデータベース名を変更する (これには、「1」を追加など)。</span><span class="sxs-lookup"><span data-stu-id="c6e60-274">In the *web.config* file, change the database name in the connection string (for example, add "1" to it).</span></span>
> 2. <span data-ttu-id="c6e60-275">保存、 *web.config*ファイル。</span><span class="sxs-lookup"><span data-stu-id="c6e60-275">Save the *web.config* file.</span></span>
> 3. <span data-ttu-id="c6e60-276">クリックして**データベース**を更新します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-276">Click **Databases** and refresh.</span></span>
> 4. <span data-ttu-id="c6e60-277">接続文字列でデータベース名を変更、 *web.config*ファイルを再度元のデータベース名。</span><span class="sxs-lookup"><span data-stu-id="c6e60-277">Change the database name in the connection string in the *web.config* file back to the original database name.</span></span>
> 5. <span data-ttu-id="c6e60-278">保存、 *web.config*ファイル。</span><span class="sxs-lookup"><span data-stu-id="c6e60-278">Save the *web.config* file.</span></span>
> 6. <span data-ttu-id="c6e60-279">クリックして**データベース**を更新します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-279">Click **Databases** and refresh.</span></span>

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a><span data-ttu-id="c6e60-280">問題:WebMatrix で作成されたフォルダーを削除できません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-280">Issue: Folders created by WebMatrix cannot be deleted</span></span>

> <span data-ttu-id="c6e60-281">WebMatrix では、昇格されたアクセス許可を使用して実行している場合 (WebMatrix を使用して開始した、**管理者として実行**Windows オプション)、Windows エクスプ ローラーを使用して WebMatrix で作成されるフォルダーを削除できません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-281">If WebMatrix is running using elevated permissions (that is, you started WebMatrix using the **Run as Administrator** option in Windows), folders that are created by WebMatrix cannot be deleted using Windows Explorer.</span></span>
> 
> <span data-ttu-id="c6e60-282">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-282">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-283">昇格されたアクセス許可を使用して Windows エクスプ ローラーを実行します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-283">Run Windows Explorer using elevated permissions.</span></span> <span data-ttu-id="c6e60-284">この場合は、以下の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="c6e60-284">Follow these steps:</span></span>  
> 
> 1. <span data-ttu-id="c6e60-285">Windows、 をクリックして**開始**します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-285">In Windows, click **Start**.</span></span>
> 2. <span data-ttu-id="c6e60-286">[Windows エクスプ ローラー] を入力し、エントリを右クリックして**Windows エクスプ ローラー**します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-286">Enter "Windows Explorer" and right-click the entry for **Windows Explorer**.</span></span>
> 3. <span data-ttu-id="c6e60-287">クリックして**管理者として実行**します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-287">Click **Run as Administrator**.</span></span> <span data-ttu-id="c6e60-288">フォルダーを削除することができます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-288">You can then delete the folders.</span></span>

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="c6e60-289">問題:WebMatrix 1.0 は昇格が必要な特定のタスクを実行できません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-289">Issue: WebMatrix 1.0 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="c6e60-290">WebMatrix 1.0 では、次の状況で追加コンポーネントのインストールなどの昇格が必要な特定のタスクを実行できません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-290">WebMatrix 1.0 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="c6e60-291">Windows Vista または Windows 7 では、管理者特権がないアカウントを使用してログオンして、ユーザー アカウント制御 (UAC) が無効になっています。</span><span class="sxs-lookup"><span data-stu-id="c6e60-291">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="c6e60-292">Microsoft Windows XP または Microsoft Windows Server 2003 を使用しています。</span><span class="sxs-lookup"><span data-stu-id="c6e60-292">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="c6e60-293">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-293">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-294">WebMatrix 1.0 のほとんどのタスクでは、管理アクセス許可は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-294">Most tasks in WebMatrix 1.0 do not require administrative permission.</span></span> <span data-ttu-id="c6e60-295">該当するには、管理者は、操作を実行するか、これらの手順に従います。</span><span class="sxs-lookup"><span data-stu-id="c6e60-295">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="c6e60-296">Windows Vista または Windows 7 で UAC を有効にします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-296">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="c6e60-297">Windows xp では、Administrators セキュリティ グループにユーザーを追加します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-297">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="c6e60-298">問題:「Web ギャラリーからサイト」は無効です。</span><span class="sxs-lookup"><span data-stu-id="c6e60-298">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="c6e60-299">**Web ギャラリーからのサイト**Web Platform Installer 3.0 がインストールされていない場合に、オプションが無効になっています。</span><span class="sxs-lookup"><span data-stu-id="c6e60-299">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="c6e60-300">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-300">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-301">インストール、 [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-301">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="c6e60-302">問題:Google Chrome を実行 オプションとしてご利用いただけません</span><span class="sxs-lookup"><span data-stu-id="c6e60-302">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="c6e60-303">Google Chrome が ブラウザーの一覧に表示されない**実行**上、**ホーム**タブ。</span><span class="sxs-lookup"><span data-stu-id="c6e60-303">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="c6e60-304">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-304">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-305">Google Chrome の一部のバージョンを登録しないで自体正しく Windows の既定のプログラム機能。</span><span class="sxs-lookup"><span data-stu-id="c6e60-305">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="c6e60-306">この問題を回避するには、Google Chrome を開始 をクリックして、*カスタマイズと制御 Google Chrome*  メニューのをクリックして*オプション*、順にクリックします*Make Google Chrome、既定のブラウザー*します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-306">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="c6e60-307">問題:「外部キー」ダイアログ ボックスは、プライマリ キーを入力できません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-307">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="c6e60-308">**Foreign Key**  ダイアログ ボックスは、主キー テーブルから主キーの名前を入力することを許可しません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-308">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="c6e60-309">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-309">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-310">これは意図的なものであり、</span><span class="sxs-lookup"><span data-stu-id="c6e60-310">This is intentional.</span></span> <span data-ttu-id="c6e60-311">主キー テーブルの主キーの名前を入力する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-311">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a><span data-ttu-id="c6e60-312">問題:IntelliSense が Razor 構文では、WebMatrix でご利用いただけませんC#、または Visual Basic</span><span class="sxs-lookup"><span data-stu-id="c6e60-312">Issue: IntelliSense is not available in WebMatrix for Razor syntax, C#, or Visual Basic</span></span>

> <span data-ttu-id="c6e60-313">WebMatrix で、HTML および CSS の IntelliSense がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="c6e60-313">IntelliSense is supported in WebMatrix for HTML and CSS.</span></span> <span data-ttu-id="c6e60-314">ただし、他の言語でご利用いただけません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-314">However, it is not available for other languages.</span></span> 
> 
> <span data-ttu-id="c6e60-315">**回避策** </span><span class="sxs-lookup"><span data-stu-id="c6e60-315">**Workaround** </span></span>  
> <span data-ttu-id="c6e60-316">なし。</span><span class="sxs-lookup"><span data-stu-id="c6e60-316">None.</span></span>

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a><span data-ttu-id="c6e60-317">問題:IntelliSense の HTML と CSS の提案がコンテキストに応じて適切でない要素</span><span class="sxs-lookup"><span data-stu-id="c6e60-317">Issue: IntelliSense for HTML and CSS suggests elements that are not contextually appropriate</span></span>

> <span data-ttu-id="c6e60-318">WebMatrix のマークアップの IntelliSense サポートを使用して HTML、 [XHTML 1.0 Transitional スキーマ](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional)と CSS を使用して、 [CSS 2.1 スキーマ](http://www.w3.org/TR/CSS2/)します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-318">IntelliSense for markup in WebMatrix supports HTML using the [XHTML 1.0 Transitional schema](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) and CSS using the [CSS 2.1 schema](http://www.w3.org/TR/CSS2/).</span></span> <span data-ttu-id="c6e60-319">IntelliSense は、これらの特定のスキーマに基づいているため、特定のタグ、属性、またはプロパティが提案の現在のページまたはスタイルの定義に不適切な。</span><span class="sxs-lookup"><span data-stu-id="c6e60-319">Because IntelliSense is based on these specific schemas, certain tags, attributes, or properties might be suggested that are not appropriate for the current page or style definition.</span></span> <span data-ttu-id="c6e60-320">HTML の可能性もあります (たとえば、タグが閉じられていません) の形式が正しくない XHTML として解釈される可能性がありますコンテンツで予期しない候補にします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-320">For HTML, it can also lead to unexpected suggestions in content that might be interpreted as malformed XHTML (for example, when tags are not closed).</span></span> <span data-ttu-id="c6e60-321">この問題は、カーソルが; 不完全なタグ内にある場合に顕著な可能性があります。その場合は、IntelliSense は、新しいタグの開始をお勧めします。 または、他の不適切な提案を提供します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-321">This issue might be more noticeable if the insertion point is inside an incomplete tag; in that case, IntelliSense might suggest new opening tags or offer other incorrect suggestions.</span></span> 
> 
> <span data-ttu-id="c6e60-322">**回避策** </span><span class="sxs-lookup"><span data-stu-id="c6e60-322">**Workaround** </span></span>  
> <span data-ttu-id="c6e60-323">HTML、適切な形式で、完全な XHTML ページ内で作業していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-323">For HTML, make sure that you are working within a well-formed, complete XHTML page.</span></span> <span data-ttu-id="c6e60-324">CSS、回避策はありません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-324">For CSS, there is no workaround.</span></span>

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a><span data-ttu-id="c6e60-325">問題:入力するときに、IntelliSense は呼び出されません</span><span class="sxs-lookup"><span data-stu-id="c6e60-325">Issue: IntelliSense is not invoked while you type</span></span>

> <span data-ttu-id="c6e60-326">HTML や CSS がエディターに入力されているように IntelliSense が呼び出されません可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-326">At times, IntelliSense might not be invoked as HTML or CSS is being entered in the editor.</span></span> <span data-ttu-id="c6e60-327">具体的には、カーソルが別の要素の横にある、またはファイルの最後に、これが発生可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-327">In particular, this might happen when the insertion point is directly next to another element or at the end of a file.</span></span> 
> 
> <span data-ttu-id="c6e60-328">**回避策** </span><span class="sxs-lookup"><span data-stu-id="c6e60-328">**Workaround** </span></span>  
> <span data-ttu-id="c6e60-329">カーソルを前後に空白があることと、カーソルがファイルの末尾でないことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="c6e60-329">Make sure that there is whitespace around the insertion point and that the insertion point is not at the end of a file.</span></span> <span data-ttu-id="c6e60-330">Ctrl キーを押しながら Space キーを押して手動で IntelliSense を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-330">You can also invoke IntelliSense manually by pressing Ctrl+Space.</span></span>

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a><span data-ttu-id="c6e60-331">問題:IntelliSense を無効にするために使用可能な UI がありません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-331">Issue: No UI is available for disabling IntelliSense</span></span>

> <span data-ttu-id="c6e60-332">WebMatrix 1.0 は UI またはジェスチャを IntelliSense を無効にします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-332">WebMatrix 1.0 provides no UI or gesture for disabling IntelliSense.</span></span> 
> 
> <span data-ttu-id="c6e60-333">**回避策** </span><span class="sxs-lookup"><span data-stu-id="c6e60-333">**Workaround** </span></span>  
> <span data-ttu-id="c6e60-334">IntelliSense を無効にするスイッチを含む次のコマンドを使用して WebMatrix を起動します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-334">Start WebMatrix using the following command, which includes a switch that disables IntelliSense:</span></span>  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a><span data-ttu-id="c6e60-335">IIS Express</span><span class="sxs-lookup"><span data-stu-id="c6e60-335">IIS Express</span></span>

<span data-ttu-id="c6e60-336">IIS Express には、次の URL で利用可能な独自の readme ファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-336">IIS Express has its own readme file, which is available at the following URL:</span></span>

[<span data-ttu-id="c6e60-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="c6e60-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span></span>](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a><span data-ttu-id="c6e60-338">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="c6e60-338">SQL Server Compact</span></span>

<span data-ttu-id="c6e60-339">SQL Server Compact では、次の URL で利用可能な独自の readme ファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-339">SQL Server Compact has its own readme file, which is available at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

<span data-ttu-id="c6e60-340">WebMatrix の一部として SQL Server Compact のインストールに関連する問題については、次を参照してください。 [WebMatrix のインストールに関する問題](#Known_Issues_Installation)この文書で前述しました。</span><span class="sxs-lookup"><span data-stu-id="c6e60-340">For information about issues that involve installing SQL Server Compact as part of WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

### <a id="Known_Issues_Installing_Applications"></a>  <span data-ttu-id="c6e60-341">アプリケーションのインストール</span><span class="sxs-lookup"><span data-stu-id="c6e60-341">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="c6e60-342">問題:アプリケーションをインストールすることができます、長い時間がかかる場合は、ユーザーのマイ ドキュメント フォルダーはネットワーク共有にリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-342">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="c6e60-343">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-343">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-344">なし。</span><span class="sxs-lookup"><span data-stu-id="c6e60-344">None.</span></span> <span data-ttu-id="c6e60-345">アプリケーションをインストールするにはしばらくかかる場合がありますが、正常にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-345">The application might take a while to install, but will install correctly.</span></span>

### <a id="Known_Issues_Publishing_Applications"></a>  <span data-ttu-id="c6e60-346">アプリケーションの発行</span><span class="sxs-lookup"><span data-stu-id="c6e60-346">Publishing Applications</span></span>

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a><span data-ttu-id="c6e60-347">問題:SQL Compact データベースを発行するときに「必須のアクセス許可を取得できません」エラー</span><span class="sxs-lookup"><span data-stu-id="c6e60-347">Issue: "Required permissions cannot be acquired" error when publishing a SQL Compact Database</span></span>

> <span data-ttu-id="c6e60-348">WebMatrix は完全にサポートしていません中程度の信頼の構成で .NET Framework version 3.5 を実行しているサーバーに SQL Server Compact のサポートのバイナリを展開します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-348">WebMatrix does not fully support deploying supporting binaries for SQL Server Compact to a server that is running .NET Framework version 3.5 with a medium trust configuration.</span></span>
> 
> <span data-ttu-id="c6e60-349">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-349">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-350">推奨される回避策では、サーバーで、.NET Framework 4 をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-350">The preferred workaround is to install the .NET Framework 4 on the server.</span></span> <span data-ttu-id="c6e60-351">または、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="c6e60-351">Alternatively, do the following:</span></span>
> 
> 1. <span data-ttu-id="c6e60-352">次の要素を追加、`SecurityClasses`セクション*Web\_MediumTrust.config*ファイル。</span><span class="sxs-lookup"><span data-stu-id="c6e60-352">Add the following elements to the `SecurityClasses` section in *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. <span data-ttu-id="c6e60-353">新しいアクセス許可のセットを作成、 *Web\_MediumTrust.config*次の必要なアクセス許可を持つファイル。</span><span class="sxs-lookup"><span data-stu-id="c6e60-353">Create a new permission set in the *Web\_MediumTrust.config* file with the following required permissions:</span></span>
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. <span data-ttu-id="c6e60-354">次の要素を配置することで、SQL Server Compact に設定するアクセス許可の適用、 *Web\_MediumTrust.config*ファイル。</span><span class="sxs-lookup"><span data-stu-id="c6e60-354">Apply the permission set to SQL Server Compact by putting the following elements in the *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a><span data-ttu-id="c6e60-355">問題:ギャラリーおよび PhpBB の web アプリケーションの発行後に「サービスは利用できません」エラーを表示します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-355">Issue: Gallery and PhpBB web applications display a "Service is unavailable" error after publishing</span></span>

> <span data-ttu-id="c6e60-356">状況によっては、アプリケーションを公開すると、「サービスは利用できません」エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-356">Under some circumstances, publishing an application causes a "service is unavailable" error.</span></span>
> 
> <span data-ttu-id="c6e60-357">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-357">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-358">WebMatrix で、追加の円記号 (\)でサーバー名の末尾に、**発行設定**ウィンドウし、もう一度アプリケーションを発行します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-358">In WebMatrix, add a backslash (\) to the end of the server name in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a><span data-ttu-id="c6e60-359">問題:Moodle web サイトのレイアウトとリンクが破損している発行した後</span><span class="sxs-lookup"><span data-stu-id="c6e60-359">Issue: Moodle website layout and links are broken after publishing</span></span>

> <span data-ttu-id="c6e60-360">Moodle アプリケーションを発行した後、アプリケーションが正しく機能しません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-360">After you publish a Moodle application, the application does not work correctly.</span></span>
> 
> <span data-ttu-id="c6e60-361">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-361">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-362">WebMatrix の末尾にスラッシュ (/) を追加、**サイト名**フィールドに、**発行設定**ウィンドウし、もう一度アプリケーションを発行します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-362">In WebMatrix, add a slash (/) to the end of the **Site Name** field in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a><span data-ttu-id="c6e60-363">問題:発行 nopCommerce は、データベース エラーで失敗します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-363">Issue: Publishing nopCommerce fails with a database error</span></span>

> <span data-ttu-id="c6e60-364">NopCommerce の発行が失敗しのようなデータベース エラーの報告"します nop 挿入\_ログ table は失敗しました"。</span><span class="sxs-lookup"><span data-stu-id="c6e60-364">Publishing nopCommerce fails and reports a database error like "Insert into the nop\_log table failed."</span></span>
> 
> <span data-ttu-id="c6e60-365">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-365">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="c6e60-366">WebMatrix で、次のようにクリックします。**実行**nopCommerce をローカルで起動します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-366">In WebMatrix, click **Run** to launch nopCommerce locally.</span></span>
> 2. <span data-ttu-id="c6e60-367">[管理] ページにログインします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-367">Log into the administration page.</span></span>
> 3. <span data-ttu-id="c6e60-368">をクリックして、**システム**メニュー。</span><span class="sxs-lookup"><span data-stu-id="c6e60-368">Click the **System** menu.</span></span>
> 4. <span data-ttu-id="c6e60-369">をクリックして、**ログ**オプション。</span><span class="sxs-lookup"><span data-stu-id="c6e60-369">Click the **Log** option.</span></span>
> 5. <span data-ttu-id="c6e60-370">をクリックして、**ログの消去**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-370">Click the **Clear Log** button.</span></span>
> 6. <span data-ttu-id="c6e60-371">NopCommerce をもう一度発行します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-371">Publish nopCommerce again.</span></span>

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a><span data-ttu-id="c6e60-372">問題:Silverstripe CMS では、発行されたサイトをダウンロードするときに「HTTP 500 PHP FCGI エラー」が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-372">Issue: Silverstripe CMS displays a "HTTP 500 PHP FCGI Error" when you download a published site</span></span>

> <span data-ttu-id="c6e60-373">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-373">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-374">クリックした後**ダウンロード サイトに発行**、スキップ`silverstripe-cache/manifest_main`で**発行のプレビュー**します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-374">After you click **Download published site**, skip `silverstripe-cache/manifest_main` in **Publish Preview**.</span></span> <span data-ttu-id="c6e60-375">このファイルは、キャッシュのために使用あり、各コンピューターに固有です。</span><span class="sxs-lookup"><span data-stu-id="c6e60-375">This file is used for caching purposes and is specific to each computer.</span></span>

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a><span data-ttu-id="c6e60-376">問題:サブ文字列には、「サーバー エラーは '/' アプリケーションで」が表示されます発行されたサイトをダウンロードするときに。</span><span class="sxs-lookup"><span data-stu-id="c6e60-376">Issue: Subtext displays "Server Error in '/' Application" when you download a published site</span></span>

> <span data-ttu-id="c6e60-377">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-377">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-378">サイトの開く*web.config*ファイルを開き、ユーザー ID とパスワード、データベース接続文字列で SQL Server 管理者の資格情報 ("sa"の資格情報) に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c6e60-378">Open the site's *web.config* file and replace the user ID and password in the database connection string with the SQL Server administrator credentials (the "sa" credentials).</span></span>
> 
> <span data-ttu-id="c6e60-379">または、次の手順をログインに使用したユーザー アカウントを付与するには`db_owner`アクセス許可。</span><span class="sxs-lookup"><span data-stu-id="c6e60-379">Alternatively, follow these steps in order to give the user account you are logged in with `db_owner` permissions:</span></span>
> 
> 1. <span data-ttu-id="c6e60-380">Web Platform Installer を使用して SQL Server Management Studio をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-380">Install SQL Server Management Studio using the Web Platform Installer.</span></span>
> 2. <span data-ttu-id="c6e60-381">ローカルの SQL Server Express インスタンスに接続 (既定では、 `.\SQLEXPRESS`)。</span><span class="sxs-lookup"><span data-stu-id="c6e60-381">Connect to the local SQL Server Express instance (by default, `.\SQLEXPRESS`).</span></span>
> 3. <span data-ttu-id="c6e60-382">クリックして**データベース** &gt; *[localSubtextDatabase]* &gt; **セキュリティ** &gt; **ユーザー**&gt; *[localSubtextUser*] (既定値は`subtextuser`] を右クリックし、クリック**プロパティ**します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-382">Click **Databases** &gt; *[localSubtextDatabase]* &gt; **Security** &gt; **Users** &gt; *[localSubtextUser*] (default is `subtextuser`], right-click, and click **Properties**.</span></span>
> 4. <span data-ttu-id="c6e60-383">選択**db\_所有者**ロール メンバーシップのセクションでします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-383">Select **db\_owner** in the role membership section.</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="c6e60-384">問題:サイトが"送信先 URL"フィールドが http:// または https:// でプレフィックスが付いていない場合に発行した後に機能しません。</span><span class="sxs-lookup"><span data-stu-id="c6e60-384">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="c6e60-385">**公開設定**ダイアログ ボックスで、リンク先の URL で始まらない場合`http://`または`https://`デプロイ後に、サイトが機能しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-385">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="c6e60-386">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-386">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-387">確認して、サイトでリンク先の URL を発行する前に、**発行設定** ダイアログ ボックスが始まる`http://`または`https://`します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-387">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="c6e60-388">問題:"データベースを発行できませんでしたエラーで失敗 MySQL データベースのパブリッシュします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-388">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="c6e60-389">これは、場合に発生、リモート データベースは、スクリプトを実行できません。"</span><span class="sxs-lookup"><span data-stu-id="c6e60-389">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="c6e60-390">さまざまな理由からこのエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-390">The error can occur for a number of reasons.</span></span> <span data-ttu-id="c6e60-391">このエラーが表示できる理由の 1 つは、データベース スクリプトには、単一引用符文字 (') が含まれているし、対象の MySQL データベースの既定の文字セットを utf-8 ではないです。</span><span class="sxs-lookup"><span data-stu-id="c6e60-391">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="c6e60-392">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-392">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-393">既定の文字が utf-8 に、リモートの MySQL データベースの設定を設定します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-393">Set the default character set for the remote MySQL database to UTF-8.</span></span>

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a><span data-ttu-id="c6e60-394">問題:一部のリンクが表示されない DotNetNuke の発行や、サイトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="c6e60-394">Issue: Some links are not visible in DotNetNuke after publishing or downloading the site</span></span>

> <span data-ttu-id="c6e60-395">パブリッシュまたは DotNetNuke サイトをダウンロードする場合は、サイトに表示される新しいリンクを取得するキャッシュをクリアする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-395">If you publish or download a DotNetNuke site, you might need to clear the cache to get the new links to appear on the site.</span></span>
> 
> <span data-ttu-id="c6e60-396">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-396">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="c6e60-397">"Host"としてログインします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-397">Log in as "Host".</span></span>
> 2. <span data-ttu-id="c6e60-398">[ホスト] メニューに移動し、選択**ホスト設定**します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-398">Go to the host menu and select **Host Settings**.</span></span>
> 3. <span data-ttu-id="c6e60-399">スクロール ダウンし、**詳細設定**、展開**パフォーマンス設定**します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-399">Scroll down and under **Advanced Settings**, expand **Performance Settings**.</span></span>
> 4. <span data-ttu-id="c6e60-400">をクリックして、**キャッシュのクリア**ページのリンク。</span><span class="sxs-lookup"><span data-stu-id="c6e60-400">Click the **Clear Cache** link for pages.</span></span>
> 5. <span data-ttu-id="c6e60-401">ページの下部に移動し、アプリケーションを再起動します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-401">Go to the bottom of the page and restart the application.</span></span>

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a><span data-ttu-id="c6e60-402">問題:発行されたサイトをダウンロードした後、AtomSite でいくつかのリンクが壊れています</span><span class="sxs-lookup"><span data-stu-id="c6e60-402">Issue: Some links in AtomSite are broken after you download a published site</span></span>

> <span data-ttu-id="c6e60-403">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-403">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-404">*Service.config*ファイル、 *users.config*ファイル、およびすべて *.xml*ファイル、URL 文字列に置き換えます (たとえば、 `http://myhost.com/atomsite`) ローカル サイトの (たとえば、 `http://localhost:1239`).</span><span class="sxs-lookup"><span data-stu-id="c6e60-404">In the *service.config* file, *users.config* file, and all *.xml* files, replace the URL string (for example, `http://myhost.com/atomsite`) with the local one (for example, `http://localhost:1239`).</span></span>

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a><span data-ttu-id="c6e60-405">問題:WordPress のように MySQL ベースのアプリケーションが発行し、データベース エラーの報告に失敗します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-405">Issue: MySQL-based applications like WordPress fail to publish and report a database error</span></span>

> <span data-ttu-id="c6e60-406">既定では、WebMatrix は、utf-8 文字セットで MySQL をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-406">By default, WebMatrix installs MySQL with the UTF-8 character set.</span></span> <span data-ttu-id="c6e60-407">自分で MySQL をインストールして、文字セットが utf-8 ではない場合 (たとえば、これはラテン語-1 の場合)、データベースの発行プロセスが失敗する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-407">If you install MySQL on your own, and the character set is not UTF-8 (for example, it is Latin1), the publish process for databases might fail.</span></span>
> 
> <span data-ttu-id="c6e60-408">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-408">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="c6e60-409">MySQL への utf-8 の文字セットを変更します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-409">Change the character set for MySQL to UTF-8.</span></span> <span data-ttu-id="c6e60-410">(詳細については、次を参照してください[Server 文字セットと照合順序](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html)、MySQL の web サイトです。)。</span><span class="sxs-lookup"><span data-stu-id="c6e60-410">(For details, see [Server Character Set and Collation](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) on the MySQL website.)</span></span>
> 2. <span data-ttu-id="c6e60-411">アプリケーションを再インストールします。</span><span class="sxs-lookup"><span data-stu-id="c6e60-411">Reinstall the application.</span></span>
> 3. <span data-ttu-id="c6e60-412">アプリケーションを再発行します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-412">Republish the application.</span></span>

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a><span data-ttu-id="c6e60-413">問題:アプリケーションでブラウザー ベースのセットアップが失敗した"公開済みのサイトをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="c6e60-413">Issue: "Download published site" fails for applications that have browser-based setup</span></span>

> <span data-ttu-id="c6e60-414">一部のアプリケーション (たとえば、Kentico CMS) では、データベースを作成するなど、インストール後セットアップを実行するには、ブラウザーで起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-414">Some applications (for example, Kentico CMS) require you to launch them in the browser in order to perform post-installation setup such as creating a database.</span></span> <span data-ttu-id="c6e60-415">ブラウザー ベースのセットアップを完了しなくてもこのようなアプリケーションを発行すると、リモート サーバーから、同じサイトのダウンロードを試みては失敗します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-415">If you publish an application like this without completing the browser-based setup, attempting to download the same site from a remote server will fail.</span></span>
> 
> <span data-ttu-id="c6e60-416">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-416">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-417">サイトを発行する前に、ブラウザー ベースのセットアップを完了します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-417">Finish browser-based setup before publishing the site.</span></span>

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a><span data-ttu-id="c6e60-418">問題:DotNetNuke と Kooboo CMS のデータベース エラーで失敗"公開済みのサイトをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="c6e60-418">Issue: "Download published site" fails with a database error for DotNetNuke and Kooboo CMS</span></span>

> <span data-ttu-id="c6e60-419">サーバーからアプリケーションをダウンロードしようとして、管理者の資格情報がデータベース接続文字列であるかどうか、**発行設定**ダイアログ ボックスで、発行ログには、次のエラーを表示可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c6e60-419">If you try to download an application from a server and you have administrator credentials in the database connection string in the **Publish Settings** dialog, you might see the following error in the publish log:</span></span>
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> <span data-ttu-id="c6e60-420">**回避策**</span><span class="sxs-lookup"><span data-stu-id="c6e60-420">**Workaround**</span></span>  
> <span data-ttu-id="c6e60-421">可能であれば、サイトを再パブリッシュ (または公開する) データベースの非管理者の資格情報を使用します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-421">If practical, republish the site (or have it published) using non-administrator credentials for the database.</span></span>

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="c6e60-422">参照項目</span><span class="sxs-lookup"><span data-stu-id="c6e60-422">For More Information</span></span>

<span data-ttu-id="c6e60-423">WebMatrix 1.0 の詳細については、次の web サイトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c6e60-423">For more information about WebMatrix 1.0, see the following websites:</span></span>

- [<span data-ttu-id="c6e60-424">IIS.net</span><span class="sxs-lookup"><span data-stu-id="c6e60-424">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="c6e60-425">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c6e60-425">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="c6e60-426">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="c6e60-426">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

<span data-ttu-id="c6e60-427">© 2011 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="c6e60-427">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="c6e60-428">All Rights Reserved.</span><span class="sxs-lookup"><span data-stu-id="c6e60-428">All Rights Reserved.</span></span> <span data-ttu-id="c6e60-429">[利用規約](https://msdn.microsoft.cos/cc300389.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="c6e60-429">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
