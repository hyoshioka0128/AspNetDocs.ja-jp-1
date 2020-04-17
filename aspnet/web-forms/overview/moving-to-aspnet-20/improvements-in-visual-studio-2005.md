---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Visual Studio 2005 の機能強化 |マイクロソフトドキュメント
author: rick-anderson
description: Visual Studio 2005 では、Web アプリケーション開発者に Web プロジェクトの機能強化と機能強化の一覧が提供されています。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: e98771614bf4e0095f8ff596e7cdb26c8c9de1ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542990"
---
# <a name="improvements-in-visual-studio-2005"></a><span data-ttu-id="34cb9-103">Visual Studio 2005 の機能強化</span><span class="sxs-lookup"><span data-stu-id="34cb9-103">Improvements in Visual Studio 2005</span></span>

<span data-ttu-id="34cb9-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="34cb9-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="34cb9-105">Visual Studio 2005 では、Web アプリケーション開発者に Web プロジェクトの機能強化と機能強化の一覧が提供されています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-105">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span>

<span data-ttu-id="34cb9-106">Visual Studio 2005 では、Web アプリケーション開発者に Web プロジェクトの機能強化と機能強化の一覧が提供されています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-106">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span> <span data-ttu-id="34cb9-107">Visual Studio .NET 2002 および 2003 と同様に強力な Web プロジェクトの処理方法に多くの不満がありました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-107">As powerful as Visual Studio .NET 2002 and 2003 are, there were many complaints in the way that Web projects were handled.</span></span> <span data-ttu-id="34cb9-108">Visual Studio 2005 では、これらの苦情に対処するために、多数の新機能が追加されています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-108">Visual Studio 2005 adds a significant number of new features in order to address these complaints.</span></span> <span data-ttu-id="34cb9-109">Visual Studio .NET 2003 が Web アプリケーションのコンパイルを処理する方法を好むユーザーは、「 [Web アプリケーション プロジェクト](https://go.microsoft.com/fwlink/?LinkId=57870)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="34cb9-109">For those who prefer the way that Visual Studio .NET 2003 handled compilation of Web applications, see [Web Application Projects](https://go.microsoft.com/fwlink/?LinkId=57870).</span></span>

<span data-ttu-id="34cb9-110">このモジュールでは、Web プロジェクトの作成、管理、および開発の改善点について説明します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-110">In this module, well cover improvements in Web project creation, management, and development.</span></span> <span data-ttu-id="34cb9-111">後のモジュールでは、Web プロジェクトの構築と配置の改善についてよく説明します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-111">In a later module, well cover improvements in building Web projects and deploying them.</span></span>

## <a name="frontpage-server-extensions"></a><span data-ttu-id="34cb9-112">FrontPage サーバー拡張</span><span class="sxs-lookup"><span data-stu-id="34cb9-112">FrontPage Server Extensions</span></span>

<span data-ttu-id="34cb9-113">Visual Studio .NET 2002 および 2003 では、Web プロジェクトを作成またはビルドするために、このボックスに FrontPage サーバー拡張機能が必要でした。</span><span class="sxs-lookup"><span data-stu-id="34cb9-113">Visual Studio .NET 2002 and 2003 required FrontPage Server Extensions on the box in order to create or build Web projects.</span></span> <span data-ttu-id="34cb9-114">開発者は、2 つの異なるアクセス モード (FrontPage サーバー拡張機能またはファイル アクセス モード) の中から選択し、両方の FrontPage サーバー拡張機能を使用して、IIS でアプリケーション ルートを設定するなどのタスクを実行しました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-114">Developers did have a choice between two different access modes (FrontPage Server Extensions or File access mode), both used FrontPage Server Extensions to perform tasks such as setting the application root in IIS, etc.</span></span>

<span data-ttu-id="34cb9-115">Visual Studio 2005 では、ローカル プロジェクトの FrontPage サーバー拡張機能への依存が削除されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-115">Visual Studio 2005 removes the reliance on FrontPage Server Extensions for local projects.</span></span> <span data-ttu-id="34cb9-116">Visual Studio 2005 は、フロント ページサーバー拡張機能を使用する代わりに、IIS メタベースに直接アクセスするようになりました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-116">Visual Studio 2005 now accesses the IIS metabase directly instead of using the FrontPage Server Extensions.</span></span> <span data-ttu-id="34cb9-117">また、Visual Studio 2005 では、フロント ページのサーバー拡張機能を必要とせずに、リモート プロジェクト アクセスを可能にする FTP のサポートも追加されています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-117">Visual Studio 2005 also adds support for FTP which allows for remote project access without requiring FrontPage Server Extensions.</span></span>

<span data-ttu-id="34cb9-118">プロジェクトで FrontPage サーバー拡張機能を使用する開発者は、このオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-118">For those developers who want to use FrontPage Server Extensions in their projects, the option is still available.</span></span> <span data-ttu-id="34cb9-119">ただし、ASP.NET開発者コミュニティからの強いフィードバックに基づいて、それは必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-119">However, based upon strong feedback from the ASP.NET developer community, it is not a requirement.</span></span>

> [!NOTE]
> <span data-ttu-id="34cb9-120">リモート プロジェクトの作成や開くなどの場合は、FrontPage サーバー拡張機能が必要です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-120">FrontPage Server Extensions are still required for remote project creation, opening, etc.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="34cb9-121">ASP.NET 開発サーバー</span><span class="sxs-lookup"><span data-stu-id="34cb9-121">ASP.NET Development Server</span></span>

<span data-ttu-id="34cb9-122">Visual Studio 2005 には、開発サーバーと呼ばれる新しい Web サーバーASP.NET付属しています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-122">Visual Studio 2005 ships with a new Web server called ASP.NET Development Server.</span></span> <span data-ttu-id="34cb9-123">(この Web サーバーは以前はカッシーニと呼ばれていた。</span><span class="sxs-lookup"><span data-stu-id="34cb9-123">(This Web server was previously known as Cassini.)</span></span>

<span data-ttu-id="34cb9-124">ASP.NET開発サーバーには、いくつかの利点があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-124">There are several benefits of the ASP.NET Development Server.</span></span>

- <span data-ttu-id="34cb9-125">管理者以外のユーザーが Web サーバーに対して開発およびデバッグできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-125">It is now possible for non-Administrators to develop and debug against a Web server.</span></span>
- <span data-ttu-id="34cb9-126">ASP.NET開発サーバーは、仮想ディレクトリをファイル システム内の任意の場所に動的にマップし、柔軟なプロジェクトの場所を指定できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-126">The ASP.NET Development Server dynamically maps virtual directories to any location in the file system allowing for flexible project locations.</span></span>
- <span data-ttu-id="34cb9-127">既に IIS を使用している Windows XP Professional のユーザーは、IIS の既定の Web サイトのファイルやフォルダ構造に影響を与えない新しい Web アプリケーションを作成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-127">Users on Windows XP Professional who are already using IIS will now be able to create new Web applications that will not affect the file or folder structure of their Default Web Site in IIS.</span></span>

<span data-ttu-id="34cb9-128">ASP.NET開発サーバーを利用するために特別な構成は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-128">No special configuration is required to take advantage of the ASP.NET Development Server.</span></span> <span data-ttu-id="34cb9-129">ファイル システムでホストされている Web プロジェクトがデバッグまたは参照されると、Visual Studio 2005 は要求を処理するために、ランダムなポートでASP.NET開発サーバーのインスタンスを自動的に起動します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-129">When a Web project that is hosted on the file system is debugged or browsed, Visual Studio 2005 will automatically start an instance of the ASP.NET Development Server on a random port to service the request.</span></span>

<span data-ttu-id="34cb9-130">詳細については、このモジュールの後半でASP.NET開発サーバーで説明します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-130">More information will be covered on the ASP.NET Development Server later in this module.</span></span>

## <a name="improved-file-management"></a><span data-ttu-id="34cb9-131">ファイル管理の改善</span><span class="sxs-lookup"><span data-stu-id="34cb9-131">Improved File Management</span></span>

<span data-ttu-id="34cb9-132">Visual Studio 2002 および 2003 では、プロジェクト ファイル (VB.NET の場合は .vbproj、C# の場合は .csproj) が、Web アプリケーション内のすべてのファイルに関する情報を格納しました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-132">In Visual Studio 2002 and 2003, a project file (.vbproj for VB.NET and .csproj for C#) stored information on all files in the Web application.</span></span> <span data-ttu-id="34cb9-133">ソリューション エクスプローラの表示は、プロジェクト ファイル内のファイル情報に基づいています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-133">The Solution Explorer display is based upon the file information in the project file.</span></span> <span data-ttu-id="34cb9-134">このため、外部エディターを使用した場合、ソリューション エクスプローラーには不正確な情報が表示されることがよくあります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-134">Because of this, the Solution Explorer would often display inaccurate information in cases where external editors were used.</span></span> <span data-ttu-id="34cb9-135">Visual Studio 2002 および 2003 では、ファイルの変更が上書きされたり、最新バージョンのファイルが表示されない場合があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-135">Visual Studio 2002 and 2003 would often overwrite file changes or not display the most recent version of files.</span></span>

<span data-ttu-id="34cb9-136">Visual Studio 2005 では、プロジェクト ファイルが使用されないほどです。</span><span class="sxs-lookup"><span data-stu-id="34cb9-136">Visual Studio 2005 does away with the project file.</span></span> <span data-ttu-id="34cb9-137">代わりに、ファイルとフォルダーの情報をディスクから直接読み取り、プロジェクト内のファイルを正確に表示します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-137">Instead, it reads the file and folder information directly from the disk, resulting in an accurate display of the files in your project.</span></span> <span data-ttu-id="34cb9-138">Visual Studio 2002 および 2003 の [参照] フォルダーは Web アプリケーションの実際のフォルダーを表していないため、Visual Studio 2005 ではソリューション エクスプローラーから [参照設定] フォルダーも削除されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-138">Because the References folder in Visual Studio 2002 and 2003 does not represent an actual folder in your Web application, Visual Studio 2005 also removes the References folder from Solution Explorer.</span></span> <span data-ttu-id="34cb9-139">Visual Studio 2005 でプロジェクトの参照にアクセスするには、プロジェクトの [プロパティ] ページを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-139">To access the references for your project in Visual Studio 2005, you should use the Property pages for the project.</span></span>

## <a name="creating-web-projects"></a><span data-ttu-id="34cb9-140">Web プロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="34cb9-140">Creating Web Projects</span></span>

<span data-ttu-id="34cb9-141">Web 開発者は、Visual Studio 2005 でプロジェクトを作成するために使用できる多くの新しいオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-141">Web developers have many new options available for project creation in Visual Studio 2005.</span></span> <span data-ttu-id="34cb9-142">これで、Web サイトはファイル システム内の任意の場所に作成でき、新しいASP.NET開発サーバーを使用してデバッグまたは参照できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-142">Web sites can now be created anywhere in the file system and can then be debugged or browsed using the new ASP.NET Development Server.</span></span> <span data-ttu-id="34cb9-143">開発者は、FTP を使用して新しい Web サイトを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-143">Developers can also create new Web sites using FTP.</span></span>

<span data-ttu-id="34cb9-144">ここをクリックして、Visual Studio 2005 での Web プロジェクトの作成に関するビデオ チュートリアルを表示します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-144">Click here to view a video walkthrough of creating Web projects in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image1.png)

[<span data-ttu-id="34cb9-145">フルスクリーンビデオを開く</span><span class="sxs-lookup"><span data-stu-id="34cb9-145">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a><span data-ttu-id="34cb9-146">ファイル システム プロジェクト</span><span class="sxs-lookup"><span data-stu-id="34cb9-146">File System Projects</span></span>

<span data-ttu-id="34cb9-147">ビデオ チュートリアルで説明したように、ローカル コンピューター上またはファイル共有を介してリモートの場所で、ファイル システム上に Web サイトを作成できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-147">As you saw in the video walkthrough, you can choose to create Web sites on the file system either on the local machine or on a remote location via a file share.</span></span> <span data-ttu-id="34cb9-148">ファイル システム上に作成された Web サイトは、ASP.NET開発サーバーを使用して参照およびデバッグされます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-148">Web sites that are created on the file system are browsed and debugged using the ASP.NET Development Server.</span></span>

> [!NOTE]
> <span data-ttu-id="34cb9-149">ASP.NET開発サーバーは、お客様に混乱を招く可能性があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-149">The ASP.NET Development Server may cause some confusion for customers.</span></span> <span data-ttu-id="34cb9-150">ファイル システム上で ISs ディレクトリ構造 (c:/inetpub/wwwroot) に Web プロジェクトが作成された場合、Visual Studio 2005 内から起動すると、Web サイトはASP.NET開発サーバーを介して引き続き参照されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-150">If a Web project is created on the file system in IISs directory structure (i.e. c:/inetpub/wwwroot), the Web site will still be browsed via the ASP.NET Development Server when launched from within Visual Studio 2005.</span></span> <span data-ttu-id="34cb9-151">したがって、IIS の構成 (認証方法) は適用されません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-151">Therefore, any IIS configuration (i.e. authentication methods) is not applicable.</span></span>

<span data-ttu-id="34cb9-152">既定の Web プロジェクトでは、Default.aspx ページ、default.cs ファイル、およびアプリ/_Data フォルダーのみが含まれるだけで、多くのオーバーヘッドが削除されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-152">The default web project also removes a lot of the overhead by only includes a Default.aspx page, default.cs file, and an App/_Data folder.</span></span> <span data-ttu-id="34cb9-153">web.config および特殊フォルダー (アプリ/_codeなど) は、必要に応じて追加されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-153">The web.config and special folders (i.e. app/_code) are added as they are needed.</span></span> <span data-ttu-id="34cb9-154">Web プロジェクトには、必要なファイルとフォルダーのみが含まれます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-154">Your web project only includes the files and folders that you need.</span></span>

### <a name="http-projects"></a><span data-ttu-id="34cb9-155">HTTP プロジェクト</span><span class="sxs-lookup"><span data-stu-id="34cb9-155">HTTP Projects</span></span>

<span data-ttu-id="34cb9-156">HTTP プロジェクトは、ローカル IIS Web サイトまたはリモート Web サイトで作成されたプロジェクトのいずれかです。</span><span class="sxs-lookup"><span data-stu-id="34cb9-156">HTTP projects can either be projects that are created on a local IIS Web site or on a remote Web site.</span></span> <span data-ttu-id="34cb9-157">既定のプロジェクトの場所`http://localhost`は です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-157">The default project location is `http://localhost`.</span></span> <span data-ttu-id="34cb9-158">[参照] ボタンをクリックすると、2 つの HTTP オプション (ローカル IIS とリモート サイト) があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-158">If you click the Browse button, there are two HTTP options: Local IIS and Remote Site.</span></span> <span data-ttu-id="34cb9-159">この 2 つのオプションの主な違いは、Web サイト情報が [場所の選択] ダイアログに表示される方法と、ファイルを Web サーバーにコピーする方法です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-159">The main difference in these two options is the method in which the web site information is displayed in the Choose Location dialog and in how the files are copied to the Web server.</span></span>

<span data-ttu-id="34cb9-160">ローカル IIS オプションは、ローカル コンピューター上のメタベースからサイト情報を読み取り、ファイル システムを使用してファイルがコピーされます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-160">The Local IIS option reads the site information from the metabase on the local machine and files are copied using the file system.</span></span> <span data-ttu-id="34cb9-161">[リモート サイト] オプションでは、FrontPage サーバー拡張機能を使用し、サイト情報とファイルは HTTP および FrontPage サーバー拡張機能 RPC 呼び出しを使用してコピーされます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-161">The Remote Site option uses the FrontPage Server Extensions and the site information and files are copied using HTTP and FrontPage Server Extensions RPC calls.</span></span>

> [!NOTE]
> <span data-ttu-id="34cb9-162">バージョン情報を確認するために vs###/_tmp.htm ファイルと取得/_aspx/_ver.aspx が使用されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-162">The vs###/_tmp.htm file and get/_aspx/_ver.aspx are no longer used to determine version information.</span></span>

<span data-ttu-id="34cb9-163">既定の HTTP オプションはローカル IIS です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-163">The default HTTP option is Local IIS.</span></span> <span data-ttu-id="34cb9-164">このオプションは、IIS メタベースを読み取って、使用可能なサイトとコンテンツを作成する場所を決定します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-164">This option reads the IIS Metabase to determine which sites are available and the location in which to create content.</span></span> <span data-ttu-id="34cb9-165">ツリー ビューで別のフォルダまたは仮想ディレクトリを選択して選択できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-165">You can select a different folder or virtual directory by selecting it in the tree view.</span></span> <span data-ttu-id="34cb9-166">また、新しい仮想ディレクトリを作成したり、フォルダをアプリケーションとしてマークしたり、このダイアログ ボックスから既存の仮想ディレクトリを削除したりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-166">You can also create a new virtual directory, mark folders as applications, as well as delete existing virtual directories from this dialog box.</span></span>

![[場所の選択]ダイアログ](improvements-in-visual-studio-2005/_static/image1.gif)

<span data-ttu-id="34cb9-168">**図1**: [場所の選択] ダイアログ</span><span class="sxs-lookup"><span data-stu-id="34cb9-168">**Figure 1**: The Choose Location Dialog</span></span>

<span data-ttu-id="34cb9-169">以前のバージョンの Visual Studio とは異なり、[**セキュリティで保護されたソケット レイヤーを使用**する] チェック ボックスをオンにし、SSL 証明書が参照している URL と一致しない場合は、続行するかどうかを確認する [セキュリティの警告] ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-169">Unlike in earlier versions of Visual Studio, if you check the **Use Secure Sockets Layer** checkbox and the SSL certificate does not match the URL you are browsing, you will be presented with a Security Alert dialog asking you if you would like to proceed.</span></span> <span data-ttu-id="34cb9-170">Visual Studio .NET 2003 を使用すると、証明書が一致しない場合、プロジェクトの作成は失敗します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-170">Using Visual Studio .NET 2003, if the certificate was not a matching one, creating the project would fail.</span></span>

![SSL 証明書に関するセキュリティ アラート](improvements-in-visual-studio-2005/_static/image2.gif)

<span data-ttu-id="34cb9-172">**図2**: SSL 証明書に関するセキュリティ警告</span><span class="sxs-lookup"><span data-stu-id="34cb9-172">**Figure 2**: Security Alert Regarding SSL Certificate</span></span>

### <a name="note-on-host-headers"></a><span data-ttu-id="34cb9-173">ホスト ヘッダーに関する注意</span><span class="sxs-lookup"><span data-stu-id="34cb9-173">Note on Host Headers</span></span>

<span data-ttu-id="34cb9-174">特定の IP にバインドされたサイト上に Web アプリケーションを作成する場合は、ホスト ヘッダーが構成されていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-174">If you are creating a Web application on a site bound to a specific IP, you will need to ensure that a host header is configured.</span></span> <span data-ttu-id="34cb9-175">それ以外の場合、Visual Studio`http://localhost`は サイトを に作成しますが、サイトが IDE 内から参照またはデバッグされると、IP アドレスが正しく解決されません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-175">Otherwise, Visual Studio will create the site at `http://localhost`, but the IP address will not resolve correctly when the site is browsed or debugged from within the IDE.</span></span>

<span data-ttu-id="34cb9-176">[リモート サイト] オプションを選択すると、新しい Web サイトのリンク先 URL を入力できるようにダイアログ ボックスが変更されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-176">If you select the Remote Site option, the dialog changes to allow you to enter the destination URL for the new Web site.</span></span> <span data-ttu-id="34cb9-177">この URL は、FrontPage サーバー拡張機能が有効になっているサーバー上になければなりません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-177">This URL must be on a server that has the FrontPage Server Extensions enabled.</span></span> <span data-ttu-id="34cb9-178">FrontPage サーバー拡張機能を使用してローカル Web サーバーを操作する場合は、[リモート サイト] オプションを使用してローカル URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-178">If you want to work with your local Web server using the FrontPage Server Extensions, you can use the Remote Site option and specify a local URL.</span></span>

![リモート サーバー上に Web サイトを作成する](improvements-in-visual-studio-2005/_static/image1.jpg)

<span data-ttu-id="34cb9-180">**図 3**: リモート サーバー上に Web サイトを作成する</span><span class="sxs-lookup"><span data-stu-id="34cb9-180">**Figure 3**: Creating a Web Site on a Remote Server</span></span>

<span data-ttu-id="34cb9-181">SSL を使用してリモート サイトにアプリケーションを作成する場合、SSL 証明書が一致しない場合、確認ダイアログは、ローカル IIS オプションを使用する場合に表示されるダイアログボックスとは若干異なります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-181">When creating an application on a remote site via SSL, if the SSL certificate does not match, the confirmation dialog is slightly different than the dialog displayed when using the Local IIS option.</span></span>

![リモート サイトのセキュリティ警告](improvements-in-visual-studio-2005/_static/image3.gif)

<span data-ttu-id="34cb9-183">**図 4**: リモート サイトのセキュリティ警告</span><span class="sxs-lookup"><span data-stu-id="34cb9-183">**Figure 4**: The Remote Site Security Alert</span></span>

<a id="_Toc116100243"></a>

#### <a name="ftp"></a><span data-ttu-id="34cb9-184">FTP</span><span class="sxs-lookup"><span data-stu-id="34cb9-184">FTP</span></span>

<span data-ttu-id="34cb9-185">Visual Studio 2005 では、FTP を使用して Web サイトを作成するオプションが導入されています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-185">Visual Studio 2005 introduces the option to create Web sites via FTP.</span></span> <span data-ttu-id="34cb9-186">このオプションを使用すると、IDE はユーザーの一時フォルダにファイルをローカルに作成し、FTP を使用して FTP の場所にファイルを移動します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-186">When you use this option, the IDE creates the files locally in the users temp folder and then uses FTP to move the files to the FTP location.</span></span>

> [!NOTE]
> <span data-ttu-id="34cb9-187">一時フォルダの場所は c:/ドキュメントと&lt;設定&gt;/ユーザー/ローカル設定/一時/VWDWebCache/&lt;サーバー&gt;/_&lt;アプリケーション名です&gt;</span><span class="sxs-lookup"><span data-stu-id="34cb9-187">The temp folder location is c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="34cb9-188">FTP オプションを使用すると、[場所の選択] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-188">When using the FTP option, you will be presented with a Choose Location dialog.</span></span> <span data-ttu-id="34cb9-189">以下に示すように、このダイアログに必要な FTP 接続情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-189">You enter the required FTP connection information into this dialog as shown below.</span></span>

![FTP の [場所の選択] ダイアログ](improvements-in-visual-studio-2005/_static/image2.jpg)

<span data-ttu-id="34cb9-191">**図5**: FTP の場所の選択ダイアログ</span><span class="sxs-lookup"><span data-stu-id="34cb9-191">**Figure 5**: The Choose Location Dialog for FTP</span></span>

## <a name="lab-setup-ftp-site-and-create-a-project"></a><span data-ttu-id="34cb9-192">演習 : FTP サイトをセットアップしてプロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="34cb9-192">Lab: Setup FTP site and create a project</span></span>

<span data-ttu-id="34cb9-193">次の手順では、FTP サイトを構成して、FTP 経由でアップロードできる場所をユーザーに設定します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-193">The following steps configure the FTP site so that a user has a location that only they can upload to via FTP.</span></span>

### <a name="install-the-ftp-service"></a><span data-ttu-id="34cb9-194">FTP サービスのインストール</span><span class="sxs-lookup"><span data-stu-id="34cb9-194">Install the FTP Service</span></span>

1. <span data-ttu-id="34cb9-195">[プログラムの追加] を開き、[Windows コンポーネントの追加と削除] を選択します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-195">Open Add Remove Programs, select Add/Remove Windows Components</span></span>
2. <span data-ttu-id="34cb9-196">[インターネット インフォメーション サービス (Windows 2003 のアプリケーション サーバー)] を選択し、[**詳細**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-196">Select Internet Information Services (Application Server on Windows 2003) and click **Details**.</span></span>
3. <span data-ttu-id="34cb9-197">**ファイル転送プロトコル (FTP) サービスを**確認し **、[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-197">Check **File Transfer Protocol (FTP) Service** and click **OK**.</span></span>
4. <span data-ttu-id="34cb9-198">[**次へ**] をクリックして、FTP サービスをインストールします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-198">Click **Next** to install the FTP service.</span></span>

### <a name="create-a-new-folder-for-content"></a><span data-ttu-id="34cb9-199">コンテンツ用の新しいフォルダを作成する</span><span class="sxs-lookup"><span data-stu-id="34cb9-199">Create a New Folder for Content</span></span>

1. <span data-ttu-id="34cb9-200">エクスプローラで、c:/inetpub/wwwroot の内部**に User1**という名前の新しいフォルダを作成します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-200">In Windows Explorer, create a new folder called **User1** inside of c:/inetpub/wwwroot.</span></span>

#### <a name="configure-folders-and-permissions-on-folders"></a><span data-ttu-id="34cb9-201">フォルダとフォルダのアクセス許可を構成する。</span><span class="sxs-lookup"><span data-stu-id="34cb9-201">Configure folders and permissions on folders.</span></span>

1. <span data-ttu-id="34cb9-202">[管理ツール] から [インターネット インフォメーション サービス] スナップインを開きます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-202">Open the Internet Information Services snap-in from Administrative Tools.</span></span> <span data-ttu-id="34cb9-203">これで、コンピュータ名ノードの下に FTP サイト フォルダが作成されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-203">You will now have an FTP Sites folder under the computer name node.</span></span>
2. <span data-ttu-id="34cb9-204">[FTP**サイト]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-204">Expand **FTP Sites**.</span></span>
3. <span data-ttu-id="34cb9-205">[既定の**FTP サイト**] を右クリックし、[**新規作成**] をクリックし、[**仮想ディレクトリ**] をクリックして、[**次へ**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-205">Right-click the **Default FTP Site**, select **New**, then **Virtual Directory**, then click **Next**.</span></span>
4. <span data-ttu-id="34cb9-206">仮想ディレクトリ名として**User1**と入力し、[**次へ**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-206">Enter **User1** for the virtual directory name and click **Next**.</span></span>
5. <span data-ttu-id="34cb9-207">パスに**c:/inetpub/wwwroot/User1**と入力し、[**次へ**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-207">Enter **c:/inetpub/wwwroot/User1** for the path and click **Next**.</span></span>
6. <span data-ttu-id="34cb9-208">[**次へ**] をクリックし、[**完了] を**クリックしてウィザードを完了します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-208">Click **Next** and then **Finish** to complete the wizard.</span></span>
7. <span data-ttu-id="34cb9-209">[既定の FTP サイト] の下にある**User1**仮想ディレクトリを右クリックし、[**プロパティ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-209">Right-click the **User1** virtual directory under Default FTP Site and select **Properties**.</span></span>
8. <span data-ttu-id="34cb9-210">**[書き込み**]チェックボックスをオンにし **、[OK]** をクリックしてダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-210">Check the **Write** checkbox and click **OK** to close the dialog.</span></span>
9. <span data-ttu-id="34cb9-211">**[既定の FTP サイト**] を右クリックし、[**プロパティ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-211">Right-click **Default FTP Site** and select **Properties**.</span></span>
10. <span data-ttu-id="34cb9-212">[**セキュリティ アカウント**] タブで、[**匿名接続を許可する**] チェック ボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-212">On the **Security Accounts** tab, uncheck **Allow Anonymous Connections**.</span></span>
11. <span data-ttu-id="34cb9-213">続行するかどうかを確認するダイアログで[**はい**]をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-213">Click **Yes** in the dialog asking if you want to continue.</span></span>
12. <span data-ttu-id="34cb9-214">[**OK**] をクリックしてダイアログ ボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-214">Click **OK** to close the dialog.</span></span>
13. <span data-ttu-id="34cb9-215">[Web**サイト]** ノードの下にある [既定の**Web サイト] を**展開します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-215">Expand the **Default Web Site** under the **Web Sites** node.</span></span>
14. <span data-ttu-id="34cb9-216">**User1**ディレクトリを右クリックし、[**プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-216">Right-click the **User1** directory and select **Properties**</span></span>
15. <span data-ttu-id="34cb9-217">[**アプリケーション設定]** セクションで、[**作成**] をクリックして、フォルダをアプリケーションとしてマークします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-217">In the **Application Settings** section, click **Create** to mark the folder as an application.</span></span>
16. <span data-ttu-id="34cb9-218">[**OK**] をクリックしてダイアログ ボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-218">Click **OK** to close the dialog.</span></span>
17. <span data-ttu-id="34cb9-219">インターネット インフォメーション サービス スナップインを閉じます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-219">Close the Internet Information Services snap-in.</span></span>

### <a name="create-web-project"></a><span data-ttu-id="34cb9-220">Web プロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="34cb9-220">Create web project</span></span>

1. <span data-ttu-id="34cb9-221">Visual Studio 2005 を開きます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-221">Open Visual Studio 2005.</span></span>
2. <span data-ttu-id="34cb9-222">[**ファイル]** メニューの [**新しい Web サイト**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-222">From the **File** menu, select **New Web Site**.</span></span>
3. <span data-ttu-id="34cb9-223">[**場所**] ドロップダウンで **、[FTP]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-223">In the **Location** dropdown, select **FTP**.</span></span>
4. <span data-ttu-id="34cb9-224">**[参照]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-224">Click **Browse**.</span></span>
5. <span data-ttu-id="34cb9-225">**「サーバー」** テキストボックスに**localhost**と入力します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-225">Enter **localhost** in the **Server** textbox.</span></span>
6. <span data-ttu-id="34cb9-226">[ディレクトリ] テキスト ボックスに **「User1」** と入力します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-226">Enter **User1** in the Directory textbox.</span></span>
7. <span data-ttu-id="34cb9-227">**[開く]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-227">Click **Open**.</span></span> <span data-ttu-id="34cb9-228">FTP の場所は、[新しい Web サイト] ダイアログに入力されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-228">The FTP location will be entered into the New Web Site dialog.</span></span>
8. <span data-ttu-id="34cb9-229">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-229">Click **OK**.</span></span>
9. <span data-ttu-id="34cb9-230">[FTP ログオン] ダイアログ で [**匿名**ログオン] をオフにし、資格情報を入力して **[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-230">Uncheck **Anonymous log on** in the FTP Log On dialog, enter your credentials, and click **OK**.</span></span>
10. <span data-ttu-id="34cb9-231">プロジェクトの URL は何ですか?</span><span class="sxs-lookup"><span data-stu-id="34cb9-231">What is the URL for the project?</span></span> <span data-ttu-id="34cb9-232">(プロジェクトの URL がソリューション エクスプローラーに表示されます)。</span><span class="sxs-lookup"><span data-stu-id="34cb9-232">(The URL for the project will be displayed in Solution Explorer.)</span></span>
11. <span data-ttu-id="34cb9-233">[**ビルド**] メニューの **[Web サイトのビルド**] または [**ソリューションのビルド**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-233">From the **Build** menu, select **Build Web Site** or **Build Solution**.</span></span>
12. <span data-ttu-id="34cb9-234">ソリューション エクスプローラで Default.aspx を右クリックし、[**ブラウザで表示]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-234">Right-click on Default.aspx in Solution Explorer and select **View in Browser**.</span></span>
13. <span data-ttu-id="34cb9-235">[Web サイトの URL が`http://localhost/user1`必要] ダイアログで、URL を入力し **、[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-235">In the Web Site URL Required dialog, enter `http://localhost/user1` for the URL and click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="34cb9-236">タイプ /_Default を読み込めないというエラーが表示された場合は、以前のバージョンではなく、Web サイトで ASP.NET 2.0 を実行していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="34cb9-236">If you get a error indicating an inability to load the type /_Default, make sure that you are running ASP.NET 2.0 on your Web site and not an earlier version.</span></span> <span data-ttu-id="34cb9-237">インターネット インフォメーション サービスの [ASP.NET] タブから実行できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-237">You can do that from the ASP.NET tab in Internet Information Services.</span></span>

## <a name="opening-web-projects"></a><span data-ttu-id="34cb9-238">Web プロジェクトを開く</span><span class="sxs-lookup"><span data-stu-id="34cb9-238">Opening Web Projects</span></span>

<span data-ttu-id="34cb9-239">Web プロジェクトを開く方法は、プロジェクトの作成と似ています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-239">Opening Web projects is similar to creating projects.</span></span> <span data-ttu-id="34cb9-240">以下のセクションでは、IDE 内で作業している間に注意を向ける領域を示します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-240">The following sections call out areas to keep an eye out for while working within the IDE.</span></span> <span data-ttu-id="34cb9-241">また、HTTP および FTP を使用した Web プロジェクトの操作についても説明します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-241">It also covers working with Web projects using HTTP and FTP.</span></span>

<span data-ttu-id="34cb9-242">Web プロジェクトを開くには、[ファイル] メニューの [Web サイトを開く] を選択します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-242">To open a Web project, select Open Web Site from the File menu.</span></span> <span data-ttu-id="34cb9-243">前に説明した[場所の選択]ダイアログ ボックスが表示され、ファイル システム、ローカル IIS、FTP、リモート サイトの 4 つのオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-243">You will be prompted with the same Choose Location dialog covered previously and you have the same four options available to you: File System, Local IIS, FTP, and Remote Site.</span></span>

<a id="_Toc116100245"></a>

## <a name="file-system"></a><span data-ttu-id="34cb9-244">ファイル システム</span><span class="sxs-lookup"><span data-stu-id="34cb9-244">File System</span></span>

<span data-ttu-id="34cb9-245">このモジュールで既に説明したように、Visual Studio ではプロジェクト ファイルが使用されなくなります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-245">As indicated previously in this module, Visual Studio no longer uses a project file.</span></span> <span data-ttu-id="34cb9-246">したがって、ファイル システムから Web サイトを開く場合、選択したフォルダーが Visual Studio で最初に Web プロジェクトとして作成されていない場合でも、必要なフォルダーを選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-246">Therefore, if you choose to open a Web site from the file system, you actually have the option of choosing any folder that you wish, even if the folder you choose was not created as a Web project initially in Visual Studio.</span></span> <span data-ttu-id="34cb9-247">たとえば、Web サイトとして [マイ ドキュメント] フォルダを開くことを選択すると、Visual Studio は次のように、このフォルダを開いてファイルを表示します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-247">For example, you can choose to open the My Documents folder as a Web site and Visual Studio will happily open it and display your files as shown below.</span></span>

![Web サイトとして開かれたマイ ドキュメント](improvements-in-visual-studio-2005/_static/image3.jpg)

<span data-ttu-id="34cb9-249">**図 6**: Web サイトとして開かれた*マイ ドキュメント*</span><span class="sxs-lookup"><span data-stu-id="34cb9-249">**Figure 6**: *My Documents* Opened As a Web Site</span></span>

<span data-ttu-id="34cb9-250">Visual Studio では、必要な場合に追加のファイルとフォルダーが作成されるだけなので、開いた場所に追加のファイルやフォルダーは追加されません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-250">Because Visual Studio only creates additional files and folders when necessary, no additional files or folders are added to the location you open.</span></span> <span data-ttu-id="34cb9-251">このアーキテクチャの副作用は、Web サイトをファイル システムにネストできないことです。</span><span class="sxs-lookup"><span data-stu-id="34cb9-251">A side-effect of this architecture is that it prevents you from nesting Web sites on the file system.</span></span> <span data-ttu-id="34cb9-252">たとえば、次のディレクトリ構造を考えます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-252">For example, consider the following directory structure.</span></span>

<span data-ttu-id="34cb9-253">C:/MyWebサイトのWebプロジェクト</span><span class="sxs-lookup"><span data-stu-id="34cb9-253">Web project at C:/MyWebSite</span></span>

<span data-ttu-id="34cb9-254">C:/MyWebサイト/ネストされた別のWebプロジェクト</span><span class="sxs-lookup"><span data-stu-id="34cb9-254">Another web project at C:/MyWebSite/Nested</span></span>

<span data-ttu-id="34cb9-255">C:/MyWebSite で Web サイトを開くと、ネストされたフォルダは、そのアプリケーションのサブフォルダーとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-255">When you open the Web site at c:/MyWebSite, the Nested folder will appear as a sub-folder of that application.</span></span>

<a id="_Toc116100246"></a>

## <a name="http"></a><span data-ttu-id="34cb9-256">HTTP</span><span class="sxs-lookup"><span data-stu-id="34cb9-256">HTTP</span></span>

<span data-ttu-id="34cb9-257">HTTP を介して Web サイトを開くとき、設定は IIS メタベース (ローカル IIS) または FrontPage サーバー拡張機能 (リモート サイト) を使用して読み取られます。入れ子になった Web アプリケーションがある場合、これらはアプリケーションとして識別するアイコンと共に表示されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-257">When opening Web sites via HTTP, settings are read either from the IIS metabase (Local IIS) or using FrontPage Server Extensions (Remote Site.) If there are nested web applications, these are displayed as well with an icon identifying them as an application.</span></span> <span data-ttu-id="34cb9-258">FrontPage で Web アプリケーションを操作する方法に精通している場合は、Visual Studio 2005 の動作も同様です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-258">If you are familiar with working with web applications in FrontPage, the behavior in Visual Studio 2005 is similar.</span></span>

<span data-ttu-id="34cb9-259">Visual Studio では、IDE 内で現在開いているアプリケーションの下に入れ子になっているアプリケーションのアイコンが表示されますが、展開してコンテンツを表示することはできません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-259">Even though Visual Studio will display an icon for applications that are nested beneath the application that is currently opened within the IDE, it will not allow you to expand them to see their content.</span></span> <span data-ttu-id="34cb9-260">ただし、それらをダブルクリックして開くことができます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-260">You can, however, double-click on them to open them.</span></span> <span data-ttu-id="34cb9-261">その場合は、Web アプリケーションを開く (および現在開いているソリューションを置き換える) か、現在のソリューションに Web アプリケーションを追加するかを確認するダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-261">When you do, you will be presented with a dialog prompting you to either open the web application (and replace the currently open solution) or add the Web application to your current solution.</span></span>

![ネストされたアプリケーションアイコンをダブルクリックすると、このダイアログボックスが表示されます。](improvements-in-visual-studio-2005/_static/image4.jpg)

<span data-ttu-id="34cb9-263">**図 7**: ネストされたアプリケーション アイコンをダブルクリックすると、このダイアログ ボックスが表示されます</span><span class="sxs-lookup"><span data-stu-id="34cb9-263">**Figure 7**: Double-clicking a nested application icon presents you with this dialog</span></span>

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a><span data-ttu-id="34cb9-264">FTP サイト</span><span class="sxs-lookup"><span data-stu-id="34cb9-264">FTP Site</span></span>

<span data-ttu-id="34cb9-265">FTP 経由でサイトを開くと、ファイルはすべてローカルで一時フォルダにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-265">When you open a site via FTP, the files are all copied locally to your temp folder.</span></span> <span data-ttu-id="34cb9-266">ローカルストレージの場所のフルパスがプロジェクトの[プロパティ]ペインに表示され、次の形式で作成されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-266">The full path for the local storage location is displayed in the Properties pane for the project and is created using the following format.</span></span>

<span data-ttu-id="34cb9-267">C:/ドキュメントと設定/&lt;ユーザー&gt;/ローカル設定/一時&lt;/VWDWebCache/&gt;サーバー&lt;/_ アプリケーション名&gt;</span><span class="sxs-lookup"><span data-stu-id="34cb9-267">C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="34cb9-268">FTP を使用する場合、Visual Studio はプロジェクトのベース URL を指定して、次に示すように参照できるようにします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-268">When using FTP, Visual Studio will need to specify the base URL for your project so that you can browse it as shown below.</span></span> <span data-ttu-id="34cb9-269">ベース URL を指定しない場合、Web サイトで初めてページを参照しようとしたときに、その URL を指定するように要求されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-269">If you do not specify a base URL, Visual Studio will ask you for it the first time you attempt to browse a page in the Web site.</span></span>

![FTP サイトのベース URL の指定](improvements-in-visual-studio-2005/_static/image5.jpg)

<span data-ttu-id="34cb9-271">**図 8**: FTP サイトのベース URL の指定</span><span class="sxs-lookup"><span data-stu-id="34cb9-271">**Figure 8**: Specifying a Base URL for FTP Sites</span></span>

## <a name="improvements-in-compilation"></a><span data-ttu-id="34cb9-272">コンパイルの改善</span><span class="sxs-lookup"><span data-stu-id="34cb9-272">Improvements in Compilation</span></span>

<span data-ttu-id="34cb9-273">Visual Studio 2005 で Web アプリケーションを使用した作業は、以前のバージョンよりも大幅に高速です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-273">Working with Web applications in Visual Studio 2005 is noticeably faster than previous versions.</span></span> <span data-ttu-id="34cb9-274">これは、コンパイル アーキテクチャの変更に少なからず起因しています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-274">This is due in no small part to the changes in compilation architecture.</span></span>

<span data-ttu-id="34cb9-275">Visual Studio 2002 および 2003 では、Web アプリケーションは 、/bin フォルダーに存在する 1 つのプライマリ アセンブリにコンパイルされました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-275">In Visual Studio 2002 and 2003, Web applications were compiled into one primary assembly residing in the /bin folder.</span></span> <span data-ttu-id="34cb9-276">Visual Studio 2005 では、アプリケーション/_Code フォルダーが追加されました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-276">In Visual Studio 2005, an App/_Code folder was added.</span></span> <span data-ttu-id="34cb9-277">クラスおよびその他の非 UI コードは、App/_Code フォルダーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-277">Classes and other non-UI code are added to the App/_Code folder.</span></span> <span data-ttu-id="34cb9-278">Visual Studio によってプロジェクトがビルドされると、アプリケーション/_Code フォルダー内のすべてのファイルが 1 つの App/_Code.dll ファイルにコンパイルされます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-278">When Visual Studio builds the project, all files in the App/_Code folder are compiled into a single App/_Code.dll file.</span></span> <span data-ttu-id="34cb9-279">この変更の結果、後続のビルドは以前のバージョンよりもずっと高速になります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-279">The result of this change is that subsequent builds are much faster than in previous versions.</span></span>

> [!NOTE]
> <span data-ttu-id="34cb9-280">MSBuild コマンド ライン ユーティリティは、ASP.NET Web アプリケーションをビルドするためにも使用できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-280">The MSBuild command line utility can also be used to build ASP.NET Web applications.</span></span> <span data-ttu-id="34cb9-281">このツールはモジュール 9 で説明します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-281">That tool will be covered in module 9.</span></span>

<span data-ttu-id="34cb9-282">もう 1 つのコンパイルの機能強化は、[ビルド] メニューの新しい [ビルド ページ] オプションです。</span><span class="sxs-lookup"><span data-stu-id="34cb9-282">Another compilation enhancement is the new Build Page option on the Build menu.</span></span> <span data-ttu-id="34cb9-283">この機能を使用すると、開発者は現在のページ (もちろん依存関係と共に) だけを再構築して、変更をより迅速にコンパイルできます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-283">This feature allows a developer to rebuild only the current page (along with, of course, and dependencies) so that changes can be compiled more quickly.</span></span> <span data-ttu-id="34cb9-284">C# では IntelliSense などを更新する目的でバックグラウンド コンパイルが提供されないため、単一のページを再構築するだけで IntelliSense を迅速に更新できるため、この機能のメリットは大きくなります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-284">Because C# does not offer background compilation for purposes of updating IntelliSense, etc., they will benefit immensely from this feature because it will allow for IntelliSense to be updated quickly by simply rebuilding a single page.</span></span>

<span data-ttu-id="34cb9-285">プロジェクトの Build プロパティを使用すると、スタートアップ ページが実行される前に発生するビルドの種類を構成できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-285">The Build properties for a project allow you to configure the type of build that occurs before the startup page is executed.</span></span> <span data-ttu-id="34cb9-286">開発者は、Visual Studio がコードの変更後にアプリケーションのデバッグを迅速に開始できるように、現在のページのみをビルドするように選択できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-286">Developers can choose to only build the current page so that Visual Studio can start debugging applications more quickly after code changes.</span></span>

![ビルド ページの開始アクション](improvements-in-visual-studio-2005/_static/image6.jpg)

<span data-ttu-id="34cb9-288">**図 9**: ビルド ページの開始アクション</span><span class="sxs-lookup"><span data-stu-id="34cb9-288">**Figure 9**: The Build Page Start Action</span></span>

<span data-ttu-id="34cb9-289">Visual Studio とASP.NET アーキテクチャのもう 1 つの優れた機能強化は、編集と続行の領域にあります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-289">Another great enhancement to Visual Studio and the ASP.NET architecture is in the area of edit and continue.</span></span> <span data-ttu-id="34cb9-290">Visual Studio 2005 では、開発者は、デバッガーをデタッチせずにプロジェクトのデバッグを開始し、プロジェクトでコードを変更できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-290">In Visual Studio 2005, developers can start debugging a project and make code changes on the project without detaching the debugger.</span></span> <span data-ttu-id="34cb9-291">実際には、文字通り、プロジェクトのデバッグを開始し、新しいクラスを追加し、そのクラスにコードを追加し、そのクラスの新しいインスタンスを作成し、すべてのデバッガーをデタッチすることなく、クラスのメソッドを実行するコードを追加できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-291">In fact, you can literally start debugging a project, add a new class, add code to that class, add code to your page that creates a new instance of that class and execute a method of the class, all without detaching the debugger.</span></span> <span data-ttu-id="34cb9-292">新しいコードを実行することは、ブラウザを更新するのと同じくらい簡単です!</span><span class="sxs-lookup"><span data-stu-id="34cb9-292">Executing the new code is literally as easy as refreshing the browser!</span></span>

<span data-ttu-id="34cb9-293">ここをクリックして、Visual Studio 2005 のエディット コンティニュ機能のビデオ チュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="34cb9-293">Click here to see a video walkthrough of the edit and continue feature in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image2.png)

[<span data-ttu-id="34cb9-294">フルスクリーンビデオを開く</span><span class="sxs-lookup"><span data-stu-id="34cb9-294">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

<span data-ttu-id="34cb9-295">ASP.NET 2.0 および Visual Studio 2005 の堅牢なエディット アンド コンティニュ機能は、ASP.NET アプリケーションのアーキテクチャの変更によるものです。</span><span class="sxs-lookup"><span data-stu-id="34cb9-295">The robust edit and continue functionality in ASP.NET 2.0 and Visual Studio 2005 is due to an architectural change for ASP.NET applications.</span></span> <span data-ttu-id="34cb9-296">ASP.NET 1.x では、Visual Studio 2002/2003 で作成されたアプリケーションは、/bin フォルダに格納されたプライマリ アセンブリにコンパイルされました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-296">In ASP.NET 1.x, applications created in Visual Studio 2002/2003 were compiled into a primary assembly that was stored in the /bin folder.</span></span> <span data-ttu-id="34cb9-297">アプリケーションのすべてのクラス、ページ、その 1 つの DLL にコンパイルされました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-297">All classes, pages, etc. for the application were compiled into that one DLL.</span></span> <span data-ttu-id="34cb9-298">その後、実行時に、ページ内のすべてのコントロール、マークアップ、およびASP.NETコードをコンパイルし、それらの DLL をASP.NET一時フォルダーにコピーASP.NET。</span><span class="sxs-lookup"><span data-stu-id="34cb9-298">Then at runtime, ASP.NET would compile all of the controls, markup, and ASP.NET code within pages and copy those DLLs into the ASP.NET temporary folder.</span></span>

<span data-ttu-id="34cb9-299">visual Studio 2005 では、ASP.NET 2.0 を使用して、上記の 2 つのコンパイル モデル (Visual Studio 用と実行時にASP.NET用) が 1 つの共通コンパイル モデルにマージされました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-299">In Visual Studio 2005 using ASP.NET 2.0, the two compilation models outline above (one for Visual Studio and one for ASP.NET at runtime) have been merged into one common compilation model.</span></span> <span data-ttu-id="34cb9-300">つまり、すべてのコンパイルの問題は、実行時ではなく開発段階でキャッチされます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-300">That means that all compilation issues are now caught during the development stage instead of at runtime.</span></span> <span data-ttu-id="34cb9-301">また、ユーザー コントロールやマスター ページなどの機能に対するデザイナーおよび IntelliSense のサポートも可能です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-301">It also allows for designer and IntelliSense support for features such as user controls and master pages.</span></span>

<span data-ttu-id="34cb9-302">ここをクリックすると、ユーザー コントロールのデザイナー サポートのビデオ チュートリアルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-302">Click here to see a video walkthrough of designer support for user controls.</span></span>

![](improvements-in-visual-studio-2005/_static/image3.png)

[<span data-ttu-id="34cb9-303">フルスクリーンビデオを開く</span><span class="sxs-lookup"><span data-stu-id="34cb9-303">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> <span data-ttu-id="34cb9-304">ユーザー コントロールがページから削除された場合、@Registerディレクティブはマークアップに残るため、ユーザー コントロールが Web サイトから削除された場合にパーサー エラーが発生しないように手動で削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-304">When a user control is removed from a page, the @Register directive remains in the markup and should be removed manually in order to avoid parser errors if the user control is deleted from the Web site.</span></span>

<span data-ttu-id="34cb9-305">Visual Studio コンパイル モデルのもう 1 つの改善点は、Web サイトの発行機能です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-305">Another improvement in the Visual Studio compilation model is the Publish Web Site feature.</span></span> <span data-ttu-id="34cb9-306">発行機能は Web サイトをプリコンパイルするので、開発者は要求に応じて何もコンパイルする必要がなくなるため、パフォーマンスを向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-306">Because the Publish feature precompiles the Web site, developers can enjoy the added performance of not having to compile anything on demand.</span></span> <span data-ttu-id="34cb9-307">また、App/_Code フォルダー内のすべてのソース コードを DLL にプリコンパイルして、ソース コードをデプロイする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-307">It also precompiles all source code in the App/_Code folder into a DLL so that no source code has to be deployed.</span></span>

![[Web サイトの発行] ダイアログ](improvements-in-visual-studio-2005/_static/image7.jpg)

<span data-ttu-id="34cb9-309">**図 10**: [Web サイトの発行] ダイアログ</span><span class="sxs-lookup"><span data-stu-id="34cb9-309">**Figure 10**: The Publish Web Site Dialog</span></span>

> [!NOTE]
> <span data-ttu-id="34cb9-310">aspnet/_compile.exe ユーティリティを使用して、ASP.NET Web アプリケーションをプリコンパイルすることもできます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-310">The aspnet/_compile.exe utility can also be used to pre-compile an ASP.NET Web application.</span></span> <span data-ttu-id="34cb9-311">このツールはモジュール 9 で説明します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-311">That tool will be covered in module 9.</span></span>

<span data-ttu-id="34cb9-312">Web サイトを発行すると、次に示すように、プリコンパイル済みファイルは一時ASP.NETファイル フォルダーに格納されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-312">When you Publish a Web site, the precompiled files are stored in the Temporary ASP.NET Files folder as shown below.</span></span> <span data-ttu-id="34cb9-313">*コンパイルされた*ファイル拡張子を持つファイルは、特定の DLL の依存関係を定義する XML ファイルです。</span><span class="sxs-lookup"><span data-stu-id="34cb9-313">Files with a *.compiled* file extension are XML files that define dependencies for particular DLLs.</span></span> <span data-ttu-id="34cb9-314">Web フォームコントロールまたはユーザーコントロールは *、App/_Web/_* で始まるランダムな DLL にコンパイルされます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-314">Any Webform or user controls are compiled into random DLLs that begin with *App/_Web/_*.</span></span>

<span data-ttu-id="34cb9-315">*このプリコンパイル済みサイトを更新可能にする*] チェック ボックスをオンのままにすると、Web フォームおよびユーザー コントロール内のマークアップは、配置後に変更を加えられるように、DLL にプリコンパイルされません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-315">If you leave the *Allow this precompiled site to be updatable* checkbox checked, markup inside of your Webforms and user controls will not be pre-compiled into a DLL allowing you to make changes after deployment.</span></span> <span data-ttu-id="34cb9-316">配置されたコンテンツへの変更が許可されないようにマークアップをロックする場合は、このボックスのチェックを外します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-316">If you would prefer to lock down the markup so that changes to the deployed content are not allowed, uncheck this box.</span></span>

<span data-ttu-id="34cb9-317">[*固定名前付けと単一ページ のアセンブリを使用する]* チェック ボックスを使用すると、バッチ コンパイルを無効にして、各ページを固定名のアセンブリにコンパイルできます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-317">The *Use fixed naming and single page assemblies* checkbox allows you to disable batch compilation so that each page is compiled into a fixed-named assembly.</span></span> <span data-ttu-id="34cb9-318">このボックスをオフにしたままにしておくと、バッチ コンパイルを利用できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-318">Leaving this box unchecked allows you to take advantage of batch compilation.</span></span>

<span data-ttu-id="34cb9-319">[*プリコンパイル済みアセンブリで厳密な名前を付ける*] チェック ボックスをオンにすると、プリコンパイル済みアセンブリに厳密な名前を付けられます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-319">The *Enable strong naming on precompiled assemblies* checkbox allows you to strong-name your precompiled assemblies.</span></span>

> [!NOTE]
> <span data-ttu-id="34cb9-320">ASP.NET 1.x では、厳密な名前のアセンブリをグローバル アセンブリ キャッシュ (GAC) にインストールする必要がありました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-320">In ASP.NET 1.x, strong-named assemblies had to be installed into the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="34cb9-321">ASP.NET 2.0 では、厳密な名前付きアセンブリを GAC にインストールする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-321">In ASP.NET 2.0, you are not required to install strong-named assemblies into the GAC.</span></span>

![ASP.NETアプリケーションのプリコンパイル済みファイル](improvements-in-visual-studio-2005/_static/image8.jpg)

<span data-ttu-id="34cb9-323">**図 11**: ASP.NET アプリケーションのプリコンパイル済みファイル</span><span class="sxs-lookup"><span data-stu-id="34cb9-323">**Figure 11**: An ASP.NET Applications Pre-Compiled Files</span></span>

> [!NOTE]
> <span data-ttu-id="34cb9-324">上記のアプリケーションには、web.config ファイルはありませんでした。</span><span class="sxs-lookup"><span data-stu-id="34cb9-324">In the application above, there was no web.config file.</span></span> <span data-ttu-id="34cb9-325">存在する場合は、Web サイトの発行プロセスの後*にプリコンパイル済み App.config*と呼ばれるでしょう。</span><span class="sxs-lookup"><span data-stu-id="34cb9-325">If there had been, it would have been called *PrecompiledApp.config* after the Publish Web site process.</span></span>

## <a name="improvements-in-deployment"></a><span data-ttu-id="34cb9-326">展開の改善</span><span class="sxs-lookup"><span data-stu-id="34cb9-326">Improvements in Deployment</span></span>

<span data-ttu-id="34cb9-327">Visual Studio 2002 および 2003 と同様に、Visual Studio 2005 にはプロジェクトのコピー機能が用意されています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-327">As with Visual Studio 2002 and 2003, Visual Studio 2005 offers a Copy Project feature.</span></span> <span data-ttu-id="34cb9-328">ただし、この機能は Visual Studio 2005 で強化され、現在は Web サイトのコピーと呼ばれています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-328">However, the feature has been beefed up in Visual Studio 2005 and is now called Copy Web Site.</span></span>

<span data-ttu-id="34cb9-329">[Web サイトのコピー] ダイアログは、左のフレームと右のフレームに分割されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-329">The Copy Web Site dialog is split into a left frame and a right frame.</span></span> <span data-ttu-id="34cb9-330">左側のフレームはソース Web サイトと呼ばれ、右側のフレームはリモート Web サイトと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-330">The left frame is called the Source Web Site and the right frame is called the Remote Web Site.</span></span> <span data-ttu-id="34cb9-331">一部の開発者を混乱させる可能性のある 1 つの点は、正しいフレームに表示されるサイトが必ずしもリモート サイトではないということです。</span><span class="sxs-lookup"><span data-stu-id="34cb9-331">One thing that may confuse some developers is that the site displayed in the right frame is not necessarily a remote site.</span></span> <span data-ttu-id="34cb9-332">ローカル ファイル システム上のサイト、または IIS のローカル インスタンスのサイトである可能性があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-332">It could be a site on the local file system or on the local instance of IIS.</span></span> <span data-ttu-id="34cb9-333">また、ダイアログ ボックスではリモート Web サイトからソース Web サイトに発行できるため、左側のフレーム*に*表示されるサイトが必ずしもソース Web サイトであるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-333">Additionally, the site displayed in the left frame is not necessarily the source Web site because the dialog allows you to publish from the remote Web site *to* the source Web site.</span></span>

<span data-ttu-id="34cb9-334">プロジェクトをリモート Web サイトにコピーする場合は、そのサイトに FrontPage サーバー拡張機能がインストールされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-334">If you are copying a project to a remote Web site, that site must have the FrontPage Server Extensions installed on it.</span></span> <span data-ttu-id="34cb9-335">接続していない場合は、FTP を使用して接続する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-335">If it does not, you will need to connect using FTP.</span></span> <span data-ttu-id="34cb9-336">一方、プロジェクトをローカル IIS インスタンスにコピーする場合は、FrontPage サーバー拡張機能は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-336">On the other hand, if you are copying a project to the local IIS instance, FrontPage Server Extensions are not required.</span></span>

> [!NOTE]
> <span data-ttu-id="34cb9-337">ローカル IIS インスタンスに新しい Web サイトを作成しようとしたときに、FrontPage 2002 サーバー拡張機能がインストールされている場合、SharePoint サーバーで Web サイトの作成がサポートされないことを示すエラー メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-337">If you try to create a new Web site on the local IIS instance and the FrontPage 2002 Server Extensions are installed, you will get an error message telling you that creating Web sites is not supported on a SharePoint server.</span></span> <span data-ttu-id="34cb9-338">その場合は、FrontPage 2000 サーバー拡張機能をインストールするか、または FrontPage サーバー拡張機能を削除するかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-338">In that case, you have the option of installing the FrontPage 2000 Server Extensions or removing the FrontPage Server Extensions.</span></span>

<span data-ttu-id="34cb9-339">Web サイトのコピー機能のビデオ チュートリアルについては、ここをクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="34cb9-339">Click here for a video walkthrough of the Copy Web Site feature.</span></span>

![](improvements-in-visual-studio-2005/_static/image4.png)

[<span data-ttu-id="34cb9-340">フルスクリーンビデオを開く</span><span class="sxs-lookup"><span data-stu-id="34cb9-340">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a><span data-ttu-id="34cb9-341">デバッグの改善</span><span class="sxs-lookup"><span data-stu-id="34cb9-341">Improvements in Debugging</span></span>

<span data-ttu-id="34cb9-342">Visual Studio 2005 のデバッグには、4 つの主要な機能強化があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-342">There are four key improvements in debugging in Visual Studio 2005.</span></span>

- <span data-ttu-id="34cb9-343">管理者以外のユーザーとしてローカルでデバッグすることは、すぐに可能です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-343">Debugging locally as a non-administrator is possible out of the box.</span></span>
- <span data-ttu-id="34cb9-344">コンパイル要素のデバッグ属性は、既定では false です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-344">The Debug attribute for the Compilation element is now false by default.</span></span>
- <span data-ttu-id="34cb9-345">リモート デバッグのセットアップと構成は以前よりも簡単です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-345">Remote debugging setup and configuration is easier than before.</span></span>
- <span data-ttu-id="34cb9-346">FTP の場所を介して開かれた Web サイトをデバッグできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-346">You can now debug a Web site opened via an FTP location.</span></span>

## <a name="debugging-as-a-non-administrator"></a><span data-ttu-id="34cb9-347">非管理者としてのデバッグ</span><span class="sxs-lookup"><span data-stu-id="34cb9-347">Debugging as a Non-Administrator</span></span>

<span data-ttu-id="34cb9-348">開発サーバーASP.NETを追加すると、管理者以外のユーザーは、すぐにASP.NETアプリケーションを簡単にデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-348">The addition of the ASP.NET Development Server allows non-administrators to easily debug ASP.NET applications right out of the box.</span></span> <span data-ttu-id="34cb9-349">ローカル ファイル システムで実行されているASP.NET アプリケーションがデバッグされると、Visual Studio は、ログオンしているユーザーのコンテキストでASP.NET開発サーバーを起動します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-349">When an ASP.NET application running on the local file system is debugged, Visual Studio launches the ASP.NET Development Server under the context of the logged-on user.</span></span> <span data-ttu-id="34cb9-350">その後、そのユーザーは、追加の構成なしでそのアプリケーションをデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-350">That user can then debug that application without any additional configuration.</span></span>

## <a name="debug-is-false-by-default"></a><span data-ttu-id="34cb9-351">デバッグはデフォルトで False です</span><span class="sxs-lookup"><span data-stu-id="34cb9-351">Debug is False by Default</span></span>

<span data-ttu-id="34cb9-352">ASP.NET 1.x では、web.config ファイルの*コンパイル*要素の*デバッグ*属性が既定で*true*に設定されています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-352">In ASP.NET 1.x, the *debug* attribute in the *compilation* element of the web.config file was set to *true* by default.</span></span> <span data-ttu-id="34cb9-353">開発者は、アプリケーションを運用環境に展開する前に、この属性を*false*に設定しておくことを常に推奨されていますが、ほとんどの開発者は debug 属性を true に設定したままにしておくと、その結果を完全に理解していないため、そのままにしておくことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="34cb9-353">It has always been recommended that developers set this attribute to *false* before deploying an application to production, but because most developers don't fully understand the consequences of leaving the debug attribute set to true, they simply left it as-is.</span></span>

<span data-ttu-id="34cb9-354">デバッグ属性を true に設定する場合の最も重大な問題は、ASP.NETs バッチ コンパイル モデルが無効になっているということです。</span><span class="sxs-lookup"><span data-stu-id="34cb9-354">The most severe problem with having the debug attribute set to true is that it disables ASP.NETs batch compilation model.</span></span> <span data-ttu-id="34cb9-355">したがって、各ページは個別の DLL にコンパイルされます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-355">Therefore, each page is compiled into a separate DLL.</span></span> <span data-ttu-id="34cb9-356">Web アプリケーションが何千ものページで構成されている場合 (決して前代未聞ではない)、そのアプリケーションによって数千の小さな DLL が作成されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-356">If a Web application consists of thousands of pages (not unheard of by any means), that means several thousand small DLLs will be created by that application.</span></span> <span data-ttu-id="34cb9-357">これらの DLL のサイズは小さいですが、メモリ内の特定の場所には読み込まれません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-357">While these DLLs are small in size, they are not loaded into any particular location in memory.</span></span> <span data-ttu-id="34cb9-358">したがって、システム メモリで断片化が発生し、OutOfMemoryException の発生に影響を与える可能性があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-358">Therefore, they cause fragmentation in system memory and can contribute to OutOfMemoryException occurrences.</span></span>

<span data-ttu-id="34cb9-359">ASP.NET 2.0 では、デバッグ属性はデフォルトで false に設定されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-359">In ASP.NET 2.0, the debug attribute is set to false by default.</span></span> <span data-ttu-id="34cb9-360">既に説明したように、開発者が Visual Studio 2005 でASP.NET アプリケーションをデバッグするときに、デバッグを有効にした web.config ファイルを追加するように求められます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-360">As you have already seen, when a developer debugs an ASP.NET application in Visual Studio 2005, they are prompted to add a web.config file with debugging enabled.</span></span> <span data-ttu-id="34cb9-361">これを行うと、ASP.NET 1.x に存在していたのと同じ欠点が発生しますが、アプリケーションを運用環境に移動する前に属性を false にリセットする必要があることを開発者が明確に警告しています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-361">Doing so incurs the same drawbacks that were present in ASP.NET 1.x, but now the developer is clearly warned that the attribute should be reset to false before moving the application to production.</span></span>

## <a name="remote-debugging-setup-and-configuration"></a><span data-ttu-id="34cb9-362">リモート デバッグのセットアップと構成</span><span class="sxs-lookup"><span data-stu-id="34cb9-362">Remote Debugging Setup and Configuration</span></span>

<span data-ttu-id="34cb9-363">Visual Studio 2002/2003 では、リモート デバッグはマシン デバッグ マネージャー (mdm.exe) と vs7jit.exe プロセスに依存していました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-363">In Visual Studio 2002/2003, remote debugging relied on the Machine Debug Manager (mdm.exe) and the vs7jit.exe process.</span></span> <span data-ttu-id="34cb9-364">そのため、リモート デバッグの問題のトラブルシューティングは、多くの場合、顧客にとってブラック ボックスであり、PSS にとってはそれほど優れたものではなかった。</span><span class="sxs-lookup"><span data-stu-id="34cb9-364">Because of that, troubleshooting remote debugging problems was often a black box for customers and it was often not much better for PSS.</span></span>

<span data-ttu-id="34cb9-365">2005 年の場合、mdm.exe および vs7jit.exe プロセスへの依存がなくなります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-365">Visual Studio 2005 removes the reliance on the mdm.exe and vs7jit.exe processes.</span></span> <span data-ttu-id="34cb9-366">代わりに、リモート デバッグ モニター サービス (msvsmon.exe) を使用するようになりました。</span><span class="sxs-lookup"><span data-stu-id="34cb9-366">Instead, it now uses the Remote Debug Monitor service (msvsmon.exe.)</span></span>

<span data-ttu-id="34cb9-367">Visual Studio 2005 でリモートでデバッグするための要件は非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-367">The requirement for debugging in Visual Studio 2005 remotely is quite simple.</span></span> <span data-ttu-id="34cb9-368">デバッグを行う前に、リモート サーバーで msvsmon.exe を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-368">You need to run msvsmon.exe on the remote server prior to debugging.</span></span> <span data-ttu-id="34cb9-369">リモート デバッグ モニターは、Visual Studio CD からインストールすることも、Web サーバーに何もインストールせずに共有から msvsmon.exe を実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-369">You can install the Remote Debug Monitor from the Visual Studio CD or you can simply run msvsmon.exe from a share without installing anything at all on the Web server.</span></span>

<span data-ttu-id="34cb9-370">msvsmon.exe を実行すると、リモート デバッグのためにポートがブロックされているという問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-370">When you run msvsmon.exe, it is likely that it will complain about ports being blocked for remote debugging.</span></span> <span data-ttu-id="34cb9-371">さいわい、次に示すように、警告ダイアログ内からポートのブロックを解除することができます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-371">Fortunately, you can easily unblock the ports from right within the warning dialog as shown below.</span></span>

![Windows ファイアウォールがリモート デバッグをブロックしていることを通知する](improvements-in-visual-studio-2005/_static/image9.jpg)

<span data-ttu-id="34cb9-373">**図 12**: Windows ファイアウォールがリモート デバッグをブロックしていることを示す通知</span><span class="sxs-lookup"><span data-stu-id="34cb9-373">**Figure 12**: Notification that Windows Firewall is Blocking Remote Debugging</span></span>

<span data-ttu-id="34cb9-374">デバッグに必要なポートのブロックを解除すると、次に示すようにリモート デバッグ モニターが表示されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-374">Once you have unblocked the ports necessary for debugging, you will see the Remote Debugging Monitor as shown below.</span></span> <span data-ttu-id="34cb9-375">このインターフェイスから、接続を監視し、デバッグのアクセス許可を簡単に変更できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-375">From this interface, you can monitor connections and change debugging permissions easily.</span></span>

![リモート デバッグ モニター](improvements-in-visual-studio-2005/_static/image10.jpg)

<span data-ttu-id="34cb9-377">**図 13**: リモート デバッグ モニタ</span><span class="sxs-lookup"><span data-stu-id="34cb9-377">**Figure 13**: The Remote Debugging Monitor</span></span>

<span data-ttu-id="34cb9-378">FTP 経由で開かれた Web アプリケーションをリモートでデバッグすることもできます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-378">It is also possible to remotely debug a Web application opened via FTP.</span></span> <span data-ttu-id="34cb9-379">手順は、以前に説明したものと同じです。</span><span class="sxs-lookup"><span data-stu-id="34cb9-379">The steps are the same as those previously covered.</span></span> <span data-ttu-id="34cb9-380">ただし、このモジュールで前述したように、FTP プロジェクトを参照するためのベース URL を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-380">However, you will need to specify a base URL for browsing the FTP project as outlined earlier in this module.</span></span>

## <a name="lab-2"></a><span data-ttu-id="34cb9-381">ラボ 2</span><span class="sxs-lookup"><span data-stu-id="34cb9-381">Lab 2</span></span>

## <a name="remote-debugging-with-visual-studio-2005"></a><span data-ttu-id="34cb9-382">Visual Studio 2005 を使用したリモート デバッグ</span><span class="sxs-lookup"><span data-stu-id="34cb9-382">Remote Debugging with Visual Studio 2005</span></span>

<span data-ttu-id="34cb9-383">このラボでは、Visual Studio 2005 を使用したリモート デバッグについて説明します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-383">This lab will walk you through remote debugging with Visual Studio 2005.</span></span>

<span data-ttu-id="34cb9-384">このラボのビデオ チュートリアルについては、ここをクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="34cb9-384">Click here for a video walkthrough of this lab.</span></span>

![](improvements-in-visual-studio-2005/_static/image5.png)

[<span data-ttu-id="34cb9-385">フルスクリーンビデオを開く</span><span class="sxs-lookup"><span data-stu-id="34cb9-385">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

<span data-ttu-id="34cb9-386">このラボでは、2 台のコンピューターを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-386">This lab requires you to have two machines, one running Visual Studio 2005 and the other running IIS 5 or greater.</span></span>

1. <span data-ttu-id="34cb9-387">Visual Studio 2005 を開き、リモート サーバー上に新しい Web サイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-387">Open Visual Studio 2005 and create a new Web site on the remote server.</span></span>

> [!NOTE]
> <span data-ttu-id="34cb9-388">リモート IIS インスタンスまたは FTP を使用して Web サイトを作成できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-388">You can create the Web site on a remote IIS instance or via FTP.</span></span>

1. <span data-ttu-id="34cb9-389">リモート Web サーバーから、開発マシン上の msvsmon.exe を UNC パスで探し、実行します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-389">From the remote Web server, locate msvsmon.exe on the development machine using a UNC path and execute it.</span></span>  
 <span data-ttu-id="34cb9-390">msvsmon.exe の既定の場所は、//サーバー/c$/プログラム ファイル/マイクロソフト Visual Studio 8/コモン7/IDE/リモート デバッガ/x86 です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-390">The default location for msvsmon.exe is //server/c$/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.</span></span>
2. <span data-ttu-id="34cb9-391">リモート デバッグ用にポートのブロックを解除するように求められた場合は、ブロックを解除します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-391">If prompted to unblock ports for remote debugging, do so.</span></span>
3. <span data-ttu-id="34cb9-392">開発マシンから Default.aspx の分離コードを開き、ページ/_Load メソッドにブレークポイントを設定します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-392">From the development machine, open the code-behind for Default.aspx and set a breakpoint in the Page/_Load method.</span></span>
4. <span data-ttu-id="34cb9-393">開発マシンからデバッグを開始します。</span><span class="sxs-lookup"><span data-stu-id="34cb9-393">Start debugging from the development machine.</span></span>

<span data-ttu-id="34cb9-394">期待どおりにブレークポイントをヒットする必要があります。</span><span class="sxs-lookup"><span data-stu-id="34cb9-394">You should hit the breakpoint as expected.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="34cb9-395">ASP.NET 開発サーバー</span><span class="sxs-lookup"><span data-stu-id="34cb9-395">ASP.NET Development Server</span></span>

<span data-ttu-id="34cb9-396">既に説明したように、Visual Studio 2005 には、ASP.NET開発サーバーと呼ばれる Web サーバーが付属しています。</span><span class="sxs-lookup"><span data-stu-id="34cb9-396">As we've already discussed, Visual Studio 2005 ships with a Web server called the ASP.NET Development Server.</span></span> <span data-ttu-id="34cb9-397">(ASP.NET開発サーバーは、カッシーニと呼ばれることもあります。この Web サーバーは、ファイル システム上で実行されている Web アプリケーションを参照およびデバッグするのに便利な手段です。</span><span class="sxs-lookup"><span data-stu-id="34cb9-397">(The ASP.NET Development Server is sometimes referred to as Cassini.) This Web server is a convenient means to browse and debug Web applications running on the file system.</span></span>

<span data-ttu-id="34cb9-398">ASP.NET開発サーバーは制限付き Web サーバーです。</span><span class="sxs-lookup"><span data-stu-id="34cb9-398">The ASP.NET Development Server is a restricted Web server.</span></span> <span data-ttu-id="34cb9-399">リモート接続は許可されず、Web サーバーを起動したユーザー以外のユーザーからの要求は許可されません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-399">It does not allow remote connections, it does not allow any requests from any user other than the user who started the Web server.</span></span> <span data-ttu-id="34cb9-400">また、ASP ページを提供する機能も持っていません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-400">It also does not have the capability of serving ASP pages.</span></span> <span data-ttu-id="34cb9-401">ASP.NETリソースとHTMLリソース(画像、CSSファイルなど)のみが提供されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-401">Only ASP.NET resources and HTML resources (including images, CSS files, etc.) are served.</span></span>

<span data-ttu-id="34cb9-402">ASP.NET開発サーバーは、c:/Windows/Net/Framework/v2.0./*/*/*/*/\*にある WebDev.WebServer.exe ファイルを実行することで、コマンド ラインを介して起動できます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-402">The ASP.NET Development Server can be launched via the command line by running the WebDev.WebServer.exe file located at c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/\*.</span></span> <span data-ttu-id="34cb9-403">次のダイアログボックスには、使用可能なパラメータが表示されます。</span><span class="sxs-lookup"><span data-stu-id="34cb9-403">The following dialog displays the parameters that are available.</span></span>

![](improvements-in-visual-studio-2005/_static/image11.jpg)

<span data-ttu-id="34cb9-404">**図 14**</span><span class="sxs-lookup"><span data-stu-id="34cb9-404">**Figure 14**</span></span>

> [!NOTE]
> <span data-ttu-id="34cb9-405">ASP.NET開発サーバは、コマンドラインを介して明示的に起動した場合はサポートされません。</span><span class="sxs-lookup"><span data-stu-id="34cb9-405">The ASP.NET Development Server is not supported when launched explicitly via the command line.</span></span>
