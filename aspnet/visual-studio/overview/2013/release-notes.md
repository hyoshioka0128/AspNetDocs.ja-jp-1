---
uid: visual-studio/overview/2013/release-notes
title: Visual Studio 2013 のリリース ノートのASP.NETと Web ツール |マイクロソフトドキュメント
author: rick-anderson
description: このドキュメントでは、Visual Studio 2013 のASP.NETと Web ツールのリリースについて説明します。
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543497"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="06ab3-103">Visual Studio 2013 の ASP.NET と Web ツールのリリース ノート</span><span class="sxs-lookup"><span data-stu-id="06ab3-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>

<span data-ttu-id="06ab3-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="06ab3-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="06ab3-105">このドキュメントでは、Visual Studio 2013 のASP.NETと Web ツールのリリースについて説明します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>

## <a name="contents"></a><span data-ttu-id="06ab3-106">内容</span><span class="sxs-lookup"><span data-stu-id="06ab3-106">Contents</span></span>

- [<span data-ttu-id="06ab3-107">インストールに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="06ab3-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="06ab3-108">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="06ab3-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="06ab3-109">ソフトウェア要件</span><span class="sxs-lookup"><span data-stu-id="06ab3-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="06ab3-110">visual Studio 2013 のASP.NETおよび Web ツールの新機能</span><span class="sxs-lookup"><span data-stu-id="06ab3-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="06ab3-111">1ASP.NET</span><span class="sxs-lookup"><span data-stu-id="06ab3-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="06ab3-112">新しい Web プロジェクト エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="06ab3-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="06ab3-113">ASP.NET足場</span><span class="sxs-lookup"><span data-stu-id="06ab3-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="06ab3-114">ブラウザー リンク</span><span class="sxs-lookup"><span data-stu-id="06ab3-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="06ab3-115">ビジュアル スタジオ Web エディターの機能強化</span><span class="sxs-lookup"><span data-stu-id="06ab3-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="06ab3-116">Azure アプリ サービス Web アプリのサポート</span><span class="sxs-lookup"><span data-stu-id="06ab3-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="06ab3-117">Web 発行の機能強化</span><span class="sxs-lookup"><span data-stu-id="06ab3-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="06ab3-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="06ab3-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="06ab3-119">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="06ab3-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="06ab3-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="06ab3-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="06ab3-121">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="06ab3-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="06ab3-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="06ab3-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="06ab3-123">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="06ab3-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="06ab3-124">Microsoft OWIN コンポーネント</span><span class="sxs-lookup"><span data-stu-id="06ab3-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="06ab3-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="06ab3-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="06ab3-126">ASP.NETカミソリ3</span><span class="sxs-lookup"><span data-stu-id="06ab3-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="06ab3-127">ASP.NETアプリの中断</span><span class="sxs-lookup"><span data-stu-id="06ab3-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="06ab3-128">既知の問題と互換性に関する変更</span><span class="sxs-lookup"><span data-stu-id="06ab3-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="06ab3-129">インストールに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="06ab3-129">Installation Notes</span></span>

<span data-ttu-id="06ab3-130">Visual Studio 2013 のASP.NETと Web ツールはメイン インストーラーにバンドルされており、[ここで](https://www.asp.net/downloads)ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="06ab3-131">ドキュメント</span><span class="sxs-lookup"><span data-stu-id="06ab3-131">Documentation</span></span>

<span data-ttu-id="06ab3-132">チュートリアルとその他の Visual Studio 2013 のASP.NETと Web ツールに関する情報は[、ASP.NET Web サイト](https://www.asp.net/)から入手できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="06ab3-133">ソフトウェア要件</span><span class="sxs-lookup"><span data-stu-id="06ab3-133">Software Requirements</span></span>

<span data-ttu-id="06ab3-134">ASP.NETと Web ツールには、Visual Studio 2013 が必要です。</span><span class="sxs-lookup"><span data-stu-id="06ab3-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="06ab3-135">visual Studio 2013 のASP.NETおよび Web ツールの新機能</span><span class="sxs-lookup"><span data-stu-id="06ab3-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="06ab3-136">以下のセクションでは、リリースで導入された機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="06ab3-137">1ASP.NET</span><span class="sxs-lookup"><span data-stu-id="06ab3-137">One ASP.NET</span></span>

<span data-ttu-id="06ab3-138">Visual Studio 2013 のリリースでは、ASP.NET テクノロジを使用するエクスペリエンスを統一する一歩を踏み出しました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="06ab3-139">たとえば、MVC を使用してプロジェクトを開始し、後で Web フォーム ページをプロジェクトに簡単に追加したり、Web フォーム プロジェクトの Web API をスキャフォールディングしたりできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="06ab3-140">ASP.NETの一つは、開発者がASP.NETで好きなことをしやすくすることです。</span><span class="sxs-lookup"><span data-stu-id="06ab3-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="06ab3-141">どのテクノロジーを選択しても、信頼できる基盤となる One ASP.NETのフレームワークを構築しているという自信を持つことができます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="06ab3-142">新しい Web プロジェクト エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="06ab3-142">New Web Project Experience</span></span>

<span data-ttu-id="06ab3-143">Visual Studio 2013 で新しい Web プロジェクトを作成するエクスペリエンスが強化されました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="06ab3-144">[**新しいASP.NET Web プロジェクト**] ダイアログで、必要なプロジェクトの種類を選択し、任意のテクノロジ (Web フォーム、MVC、Web API) の組み合わせを構成し、認証オプションを構成し、単体テスト プロジェクトを追加できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![新しいASP.NET プロジェクト](release-notes/_static/image1.png)

<span data-ttu-id="06ab3-146">新しいダイアログでは、多くのテンプレートのデフォルトの認証オプションを変更できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="06ab3-147">たとえば、Web フォーム プロジェクトASP.NET作成する場合は、次のオプションのいずれかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="06ab3-148">[認証なし]</span><span class="sxs-lookup"><span data-stu-id="06ab3-148">No Authentication</span></span>
- <span data-ttu-id="06ab3-149">個人ユーザー アカウント (ASP.NET メンバーシップまたはソーシャル プロバイダーのログイン)</span><span class="sxs-lookup"><span data-stu-id="06ab3-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="06ab3-150">組織アカウント (インターネット アプリケーションの Active Directory)</span><span class="sxs-lookup"><span data-stu-id="06ab3-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="06ab3-151">Windows 認証 (イントラネット アプリケーションのアクティブ ディレクトリ)</span><span class="sxs-lookup"><span data-stu-id="06ab3-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![認証オプション](release-notes/_static/image2.png)

<span data-ttu-id="06ab3-153">Web プロジェクトを作成するための新しいプロセスの詳細については[、「Visual Studio 2013 でASP.NET Web プロジェクトを作成](creating-web-projects-in-visual-studio.md)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="06ab3-154">新しい認証オプションの詳細については、このドキュメントの[「ASP.NET ID」](#TOC8)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="06ab3-155">ASP.NET足場</span><span class="sxs-lookup"><span data-stu-id="06ab3-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="06ab3-156">ASP.NETスキャフォールディングは、ASP.NET Web アプリケーション用のコード生成フレームワークです。</span><span class="sxs-lookup"><span data-stu-id="06ab3-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="06ab3-157">これにより、データ モデルとやり取りする定型コードをプロジェクトに簡単に追加できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="06ab3-158">以前のバージョンの Visual Studio では、スキャフォールディングは MVC プロジェクトASP.NETに限定されていました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="06ab3-159">Visual Studio 2013 では、Web フォームを含む任意のASP.NET プロジェクトにスキャフォールディングを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="06ab3-160">Visual Studio 2013 は、Web フォーム プロジェクトのページの生成をサポートしていませんが、プロジェクトに MVC 依存関係を追加することで Web フォームでスキャフォールディングを使用できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="06ab3-161">Web フォームのページ生成のサポートは、今後の更新プログラムで追加される予定です。</span><span class="sxs-lookup"><span data-stu-id="06ab3-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="06ab3-162">スキャフォールディングを使用する場合、必要なすべての依存関係がプロジェクトにインストールされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="06ab3-163">たとえば、ASP.NET Web フォーム プロジェクトを使用して Web API コント ローラーを追加するのにはスキャフォールディングを使用する場合は、必要な NuGet パッケージと参照が自動的にプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="06ab3-164">Mvc スキャフォールディングを Web フォーム プロジェクトに追加するには、**新しいスキャフォールディング項目**を追加し、ダイアログ ウィンドウで**MVC 5 の依存関係**を選択します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="06ab3-165">スキャフォールディング MVC には 2 つのオプションがあります。最小限とフル。</span><span class="sxs-lookup"><span data-stu-id="06ab3-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="06ab3-166">[最小] を選択した場合は、ASP.NET MVC の NuGet パッケージと参照のみがプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="06ab3-167">[完全] オプションを選択すると、MVC プロジェクトに必要なコンテンツ ファイルと同様に、最小限の依存関係が追加されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="06ab3-168">スキャフォールディング非同期コントローラーのサポートでは、Entity Framework 6 の新しい非同期機能が使用されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="06ab3-169">詳細およびチュートリアルについては、「ASP.NET[スキャフォールディングの概要](aspnet-scaffolding-overview.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="06ab3-170">ブラウザー リンク – ブラウザーと Visual Studio の間の SignalR チャネル</span><span class="sxs-lookup"><span data-stu-id="06ab3-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="06ab3-171">新しい[ブラウザー リンク](using-browser-link.md)機能を使用すると、複数のブラウザーを Visual Studio に接続し、ツール バーのボタンをクリックしてすべてのブラウザーを更新できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="06ab3-172">モバイル エミュレーターを含む複数のブラウザーを開発サイトに接続し、[更新] をクリックすると、すべてのブラウザーを同時に更新できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="06ab3-173">また、開発者がブラウザリンク拡張機能を記述できるように API も公開します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="06ab3-174">開発者がブラウザー リンク API を利用できるようにすることで、Visual Studio と接続されているブラウザーの境界を越える非常に高度なシナリオを作成できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="06ab3-175">Web Essentials は、この API を利用して、Visual Studio とブラウザーの開発者ツール、リモート制御モバイル エミュレーターなどの間に統合されたエクスペリエンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="06ab3-176">ビジュアル スタジオ Web エディターの機能強化</span><span class="sxs-lookup"><span data-stu-id="06ab3-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="06ab3-177">Visual Studio 2013 には、Web アプリケーションの Razor ファイルと HTML ファイル用の新しい HTML エディターが含まれています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="06ab3-178">新しい HTML エディターは、HTML5 に基づく単一の統一されたスキーマを提供します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="06ab3-179">自動ブレース補完、jQuery UIとAngularJS属性IntelliSense、属性IntelliSenseグループ、IDとクラス名Intellisense、および優れたパフォーマンス、フォーマット、スマートタグなどのその他の改善があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="06ab3-180">次のスクリーンショットは、HTML エディターでブートストラップ属性 IntelliSense を使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![HTML エディタでのインテリセンス](release-notes/_static/image4.png)

<span data-ttu-id="06ab3-182">また、2013 年には、コーヒー スクリプトと LESS の両方のエディターが組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="06ab3-183">LESSエディタには、CSSエディタからのすべてのクールな機能が付属しており、チェーン内のすべてのLESSドキュメント全体の変数とミキシンのための特定のIntellisenseがあります@import。</span><span class="sxs-lookup"><span data-stu-id="06ab3-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="06ab3-184">Azure アプリ サービス Web アプリのサポート</span><span class="sxs-lookup"><span data-stu-id="06ab3-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="06ab3-185">.NET 2.2 用 Azure SDK を使用した Visual Studio 2013 では、**サーバー エクスプローラー**を使用してリモート Web アプリと直接対話できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="06ab3-186">Azure アカウントへのサインイン、新しい Web アプリの作成、アプリの構成、リアルタイム ログの表示などを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="06ab3-187">SDK 2.2 がリリースされた直後に、Azure でリモートでデバッグ モードで実行できるようになります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="06ab3-188">Azure アプリ サービス Web アプリの新機能のほとんどは、.NET 用 Azure SDK の最新リリースをインストールするときに Visual Studio 2012 でも動作します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="06ab3-189">詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="06ab3-190">Azure アプリ サービスでASP.NET Web アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="06ab3-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="06ab3-191">Visual Studio を使用した Azure App Service のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="06ab3-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="06ab3-192">Web 発行の機能強化</span><span class="sxs-lookup"><span data-stu-id="06ab3-192">Web Publish Enhancements</span></span>

<span data-ttu-id="06ab3-193">Visual Studio 2013 には、新しい Web 発行機能と強化された Web 発行機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="06ab3-194">いくつかを次に示します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-194">Here are a few of them:</span></span>

- <span data-ttu-id="06ab3-195">[Web.config ファイルの暗号化](https://go.microsoft.com/fwlink/?LinkId=325529)を簡単に自動化する 。</span><span class="sxs-lookup"><span data-stu-id="06ab3-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="06ab3-196">(このリンクと、MSDN のドキュメントへのリンクを次の 2 つ示しますが、10/17 日の遅い時間まで利用できない場合があります)。</span><span class="sxs-lookup"><span data-stu-id="06ab3-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="06ab3-197">[展開時にアプリケーションをオフラインにする作業を簡単に自動化](https://go.microsoft.com/fwlink/?LinkId=325530)する :</span><span class="sxs-lookup"><span data-stu-id="06ab3-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="06ab3-198">サーバーにコピーするファイルを決定するために[、最後に変更された日付ではなくファイル チェックサムを使用](https://go.microsoft.com/fwlink/?LinkId=325531)するように Web 配置を構成します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="06ab3-199">FTP またはファイル システムの発行方法を使用している場合や、Web 配置を使用している場合は、選択した個々のファイル (Web.config を含む) をすばやく発行します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="06ab3-200">web 展開ASP.NET詳細については、 [ASP.NET サイトを](https://go.microsoft.com/fwlink/?LinkId=322027)参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="06ab3-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="06ab3-201">NuGet 2.7</span></span>

<span data-ttu-id="06ab3-202">NuGet 2.7 には[、NuGet 2.7 リリース ノート](http://docs.nuget.org/docs/release-notes/nuget-2.7)で詳細に説明されている新機能の豊富なセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="06ab3-203">このバージョンの NuGet では、パッケージをダウンロードするために NuGet のパッケージ復元機能に明示的な同意を提供する必要もなくなります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="06ab3-204">同意 (および NuGet の基本設定ダイアログの関連するチェック ボックス) は、NuGet をインストールすることで付与されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="06ab3-205">今すぐパッケージの復元は、デフォルトで動作します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="06ab3-206">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="06ab3-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="06ab3-207">1ASP.NET</span><span class="sxs-lookup"><span data-stu-id="06ab3-207">One ASP.NET</span></span>

<span data-ttu-id="06ab3-208">Web フォーム プロジェクト テンプレートは、新しい One ASP.NET エクスペリエンスとシームレスに統合されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="06ab3-209">Web フォーム プロジェクトに MVC および Web API サポートを追加したり、1 ASP.NET プロジェクト作成ウィザードを使用して認証を構成したりできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="06ab3-210">詳細については、「 [Visual Studio 2013 での ASP.NET Web プロジェクトの作成](creating-web-projects-in-visual-studio.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="06ab3-211">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="06ab3-211">ASP.NET Identity</span></span>

<span data-ttu-id="06ab3-212">Web フォーム プロジェクト テンプレートは、新しい ASP.NET ID フレームワークをサポートします。</span><span class="sxs-lookup"><span data-stu-id="06ab3-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="06ab3-213">さらに、テンプレートは Web フォーム イントラネット プロジェクトの作成をサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="06ab3-214">詳細については **、「Visual Studio 2013 での ASP.NET Web プロジェクトの作成」の**[認証方法](creating-web-projects-in-visual-studio.md#auth)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="06ab3-215">ブートストラップ</span><span class="sxs-lookup"><span data-stu-id="06ab3-215">Bootstrap</span></span>

<span data-ttu-id="06ab3-216">Web フォーム テンプレートでは[、Bootstrap](http://twitter.github.io/bootstrap/)を使用して、簡単にカスタマイズできる、洗練された応答性の高い外観を提供します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="06ab3-217">詳細については、「 [Visual Studio 2013 Web プロジェクト テンプレートのブートストラップ](creating-web-projects-in-visual-studio.md#bootstrap)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="06ab3-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="06ab3-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="06ab3-219">1ASP.NET</span><span class="sxs-lookup"><span data-stu-id="06ab3-219">One ASP.NET</span></span>

<span data-ttu-id="06ab3-220">Web MVC プロジェクト テンプレートは、新しい One ASP.NET エクスペリエンスとシームレスに統合されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="06ab3-221">MVC プロジェクトをカスタマイズし、One ASP.NET プロジェクト作成ウィザードを使用して認証を構成できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="06ab3-222">ASP.NET MVC 5 の入門チュートリアルは[、MVC 5 の概要](../../../mvc/overview/getting-started/introduction/getting-started.md)ASP.NET で見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="06ab3-223">MVC 4 プロジェクトを MVC 5 にアップグレードする[方法については、「MVC 4 と Web API プロジェクトASP.NETを MVC 5 と Web API 2 ASP.NETにアップグレードする方法](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="06ab3-224">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="06ab3-224">ASP.NET Identity</span></span>

<span data-ttu-id="06ab3-225">認証と ID 管理に ASP.NET ID を使用するように、MVC プロジェクト テンプレートが更新されました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="06ab3-226">FacebookとGoogleの認証と新しいメンバーシップAPIをフィーチャーしたチュートリアルは[、FacebookとGoogle OAuth2とOpenIDサインオンでASP.NETMVC 5アプリを作成し](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)、[認証とSQL DBを使用してASP.NETMVCアプリを作成し、Azureアプリサービスに展開するにあります](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="06ab3-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="06ab3-227">ブートストラップ</span><span class="sxs-lookup"><span data-stu-id="06ab3-227">Bootstrap</span></span>

<span data-ttu-id="06ab3-228">MVC プロジェクト テンプレートは[、ブートストラップ](http://getbootstrap.com/)を使用して、簡単にカスタマイズできる、洗練された応答性の高い外観と操作性を提供するように更新されました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="06ab3-229">詳細については、「 [Visual Studio 2013 Web プロジェクト テンプレートのブートストラップ](creating-web-projects-in-visual-studio.md#bootstrap)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="06ab3-230">認証フィルタ</span><span class="sxs-lookup"><span data-stu-id="06ab3-230">Authentication filters</span></span>

<span data-ttu-id="06ab3-231">認証フィルターは、ASP.NET ASP.NET MVC パイプラインで承認フィルターの前に実行され、すべてのコント ローラーのアクションごとの、コント ローラーごと、またはグローバルに認証ロジックを指定できるようにする MVC の新しい種類のフィルターです。</span><span class="sxs-lookup"><span data-stu-id="06ab3-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="06ab3-232">認証フィルターは、要求内の資格情報を処理し、対応するプリンシパルを提供します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="06ab3-233">認証フィルタは、承認されていない要求に応じて認証チャレンジを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="06ab3-234">フィルタの上書き</span><span class="sxs-lookup"><span data-stu-id="06ab3-234">Filter overrides</span></span>

<span data-ttu-id="06ab3-235">オーバーライド フィルターを指定して、特定のアクション メソッドまたはコントローラーに適用するフィルターをオーバーライドできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="06ab3-236">オーバーライド フィルターは、特定のスコープ (アクションまたはコントローラー) に対して実行してはならないフィルターの種類のセットを指定します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="06ab3-237">これにより、グローバルに適用されるが、特定のアクションまたはコントローラに適用から特定のグローバル フィルタを除外するフィルタを設定できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="06ab3-238">属性ルーティング</span><span class="sxs-lookup"><span data-stu-id="06ab3-238">Attribute routing</span></span>

<span data-ttu-id="06ab3-239">ASP.NET MVC は、 の著者である Tim McCall の投稿により[http://attributerouting.net](http://attributerouting.net)、属性ルーティングをサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="06ab3-240">属性ルーティングを使用すると、アクションとコントローラにアコードを付けてルートを指定できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="06ab3-241">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="06ab3-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="06ab3-242">属性ルーティング</span><span class="sxs-lookup"><span data-stu-id="06ab3-242">Attribute routing</span></span>

<span data-ttu-id="06ab3-243">ASP.NET Web API は、 の著者である Tim McCall の投稿[http://attributerouting.net](http://attributerouting.net)により、属性ルーティングをサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="06ab3-244">属性ルーティングを使用すると、次のようにアクションとコントローラにアコードを付けて Web API ルートを指定できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="06ab3-245">属性ルーティングを使用すると、Web API の URI をより詳細に制御できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="06ab3-246">たとえば、単一の API コントローラを使用して、リソース階層を簡単に定義できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="06ab3-247">属性ルーティングでは、オプションのパラメータ、デフォルト値、およびルート制約を指定するための便利な構文も提供します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="06ab3-248">属性ルーティングの詳細については[、「Web API 2 での属性ルーティング](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="06ab3-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="06ab3-249">OAuth 2.0</span></span>

<span data-ttu-id="06ab3-250">Web API および単一ページアプリケーションのプロジェクトテンプレートで、OAuth 2.0 を使用した承認がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="06ab3-251">OAuth 2.0 は、保護されたリソースへのクライアント アクセスを承認するためのフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="06ab3-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="06ab3-252">これは、ブラウザやモバイルデバイスを含むクライアントの様々なのために動作します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="06ab3-253">OAuth 2.0 のサポートは、ベアラー認証と承認サーバーの役割の実装のために Microsoft OWIN コンポーネントによって提供される新しいセキュリティ ミドルウェアに基づいています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="06ab3-254">または、Windows Server 2012 R2 の Azure アクティブ ディレクトリや ADFS などの組織の承認サーバーを使用して、クライアントを承認することもできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="06ab3-255">OData の機能強化</span><span class="sxs-lookup"><span data-stu-id="06ab3-255">OData Improvements</span></span>

<span data-ttu-id="06ab3-256">**$select、$expand、$batch、$valueのサポート**</span><span class="sxs-lookup"><span data-stu-id="06ab3-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="06ab3-257">ASP.NET Web API OData は、$select、$expand、および$valueを完全にサポートできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="06ab3-258">また、要求のバッチ処理や変更セットの処理に$batchを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="06ab3-259">$selectおよび$expandオプションを使用すると、OData エンドポイントから返されるデータの形状を変更できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="06ab3-260">詳細については、「 [Web API OData での$selectと$expandサポートの概要](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="06ab3-261">**拡張性の向上**</span><span class="sxs-lookup"><span data-stu-id="06ab3-261">**Improved extensibility**</span></span>

<span data-ttu-id="06ab3-262">OData フォーマッタは拡張可能になりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="06ab3-263">Atom エントリ メタデータの追加、名前付きストリームおよびメディア リンク エントリのサポート、インスタンスの注釈の追加、およびリンクの生成方法のカスタマイズを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="06ab3-264">**タイプレスサポート**</span><span class="sxs-lookup"><span data-stu-id="06ab3-264">**Type-less support**</span></span>

<span data-ttu-id="06ab3-265">エンティティ型に対して CLR 型を定義しなくても、OData サービスを構築できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="06ab3-266">代わりに、OData コントローラは、シリアル化/逆シリアル化する OData フォーマッタである**IEdmObject**のインスタンスを取得または返すことができます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="06ab3-267">**既存のモデルを再利用する**</span><span class="sxs-lookup"><span data-stu-id="06ab3-267">**Reuse an existing model**</span></span>

<span data-ttu-id="06ab3-268">既存のエンティティ データ モデル (EDM) を既に使用している場合は、新しいモデルを構築する代わりに、直接再利用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="06ab3-269">たとえば、エンティティ フレームワークを使用している場合は、EF が作成する EDM を使用できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="06ab3-270">要求バッチ処理</span><span class="sxs-lookup"><span data-stu-id="06ab3-270">Request Batching</span></span>

<span data-ttu-id="06ab3-271">要求バッチ処理は、複数の操作を 1 つの HTTP POST 要求に結合して、ネットワーク トラフィックを削減し、よりスムーズで、より少ないユーザー インターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="06ab3-272">ASP.NET Web API では、要求バッチ処理のいくつかの戦略がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="06ab3-273">OData サービスの$batch エンドポイントを使用します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="06ab3-274">複数の要求を 1 つの MIME マルチパート要求にパッケージ化します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="06ab3-275">カスタム バッチ形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-275">Use a custom batching format.</span></span>

<span data-ttu-id="06ab3-276">要求バッチ処理を有効にするには、バッチ処理ハンドラーを含むルートを Web API 構成に追加するだけです。</span><span class="sxs-lookup"><span data-stu-id="06ab3-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="06ab3-277">また、要求または実行を順次に実行するか、または任意の順序で実行するかを制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="06ab3-278">ポータブル ASP.NET Web API クライアント</span><span class="sxs-lookup"><span data-stu-id="06ab3-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="06ab3-279">ASP.NET Web API クライアントを使用して、Windows ストア アプリケーションと Windows Phone 8 アプリケーションで動作するポータブル クラス ライブラリを作成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="06ab3-280">クライアントとサーバー間で共有できるポータブル フォーマッタを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="06ab3-281">テストの容易性の向上</span><span class="sxs-lookup"><span data-stu-id="06ab3-281">Improved Testability</span></span>

<span data-ttu-id="06ab3-282">Web API 2 を使用すると、API コントローラーの単体テストが大幅に容易になります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="06ab3-283">要求メッセージと構成を使用して API コントローラーをインスタンス化し、テストするアクション メソッドを呼び出すだけです。</span><span class="sxs-lookup"><span data-stu-id="06ab3-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="06ab3-284">リンク生成を実行するアクション メソッドの**UrlHelper**クラスを簡単にモックできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="06ab3-285">を返す</span><span class="sxs-lookup"><span data-stu-id="06ab3-285">IHttpActionResult</span></span>

<span data-ttu-id="06ab3-286">これで、Web API アクション メソッドの結果をカプセル化するために IHttpActionResult を実装できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="06ab3-287">Web API アクション メソッドから返された IHttpActionResult は、結果として生成される応答メッセージを生成するために、ASP.NET Web API ランタイムによって実行されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="06ab3-288">Web API の実装の単体テストを簡略化するために、任意の Web API アクションから IHttpActionResult を返すことができます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="06ab3-289">便宜上、特定のステータス コード、書式設定されたコンテンツ、またはコンテンツネゴシエーションされた応答を返す結果を含む、多数の IHttpActionResult 実装が提供されています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="06ab3-290">HttpRequestContext</span><span class="sxs-lookup"><span data-stu-id="06ab3-290">HttpRequestContext</span></span>

<span data-ttu-id="06ab3-291">新しい**HttpRequestContext**は、要求に関連付けられているが、要求からすぐには使用できない状態を追跡します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="06ab3-292">たとえば **、HttpRequestContext**を使用して、ルート データ、要求に関連付けられているプリンシパル、クライアント証明書 **、UrlHelper、** および仮想パス ルートを取得できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="06ab3-293">単体テスト用に**HttpRequestContext**を簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="06ab3-294">要求のプリンシパルは **、Thread.CurrentPrincipal**に依存するのではなく、要求と共にフローされるため、要求の有効期間中、Web API パイプライン内でプリンシパルを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="06ab3-295">CORS</span><span class="sxs-lookup"><span data-stu-id="06ab3-295">CORS</span></span>

<span data-ttu-id="06ab3-296">ブロックアレンからのもう一つの大きな貢献のおかげで、ASP.NET完全にクロスオリジンリクエスト共有(CORS)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="06ab3-297">ブラウザーのセキュリティ機能により、Web ページでは AJAX 要求を別のドメインに送信することはできません。</span><span class="sxs-lookup"><span data-stu-id="06ab3-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="06ab3-298">[CORS](http://www.w3.org/TR/cors/)は、サーバーが同じ発信元ポリシーを緩和できるようにする W3C 標準です。</span><span class="sxs-lookup"><span data-stu-id="06ab3-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="06ab3-299">CORS を使用することで、サーバーが一部のクロス オリジン要求を、その他の要求を拒否しながら、明示的に許可することができます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="06ab3-300">Web API 2 では、プリフライト要求の自動処理を含む CORS がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="06ab3-301">詳細については、 [ASP.NET Web API でのクロスオリジン要求の有効化](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)に関する文書を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="06ab3-302">認証フィルタ</span><span class="sxs-lookup"><span data-stu-id="06ab3-302">Authentication Filters</span></span>

<span data-ttu-id="06ab3-303">認証フィルターは、ASP.NET Web API パイプラインで承認フィルターの前に実行される web API ASP.NET新しい種類のフィルターであり、すべてのコントローラーに対してアクションごと、コントローラーごと、またはグローバルに認証ロジックを指定できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="06ab3-304">認証フィルターは、要求内の資格情報を処理し、対応するプリンシパルを提供します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="06ab3-305">認証フィルタは、承認されていない要求に応じて認証チャレンジを追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="06ab3-306">フィルタの上書き</span><span class="sxs-lookup"><span data-stu-id="06ab3-306">Filter Overrides</span></span>

<span data-ttu-id="06ab3-307">オーバーライド フィルターを指定して、指定したアクション メソッドまたはコントローラーに適用するフィルターをオーバーライドできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="06ab3-308">オーバーライド フィルターは、特定のスコープ (アクションまたはコントローラー) に対して実行してはならないフィルターの種類のセットを指定します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="06ab3-309">これにより、グローバルフィルタを追加できますが、特定のアクションやコントローラから除外することができます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="06ab3-310">OWIN 統合</span><span class="sxs-lookup"><span data-stu-id="06ab3-310">OWIN Integration</span></span>

<span data-ttu-id="06ab3-311">ASP.NET Web API は OWIN を完全にサポートし、OWIN 対応のホストで実行できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="06ab3-312">OWIN 認証システムとの統合を提供する**ホスト認証フィルター**も含まれています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="06ab3-313">OWIN 統合を使用すると、SignalR などの他の OWIN ミドルウェアと共に、独自のプロセスで Web API を自己ホストできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="06ab3-314">詳細については、「 [OWIN を使用して Web API を自己ホストする 」ASP.NET](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="06ab3-315">ASP.NET信号機 2.0</span><span class="sxs-lookup"><span data-stu-id="06ab3-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="06ab3-316">次のセクションでは、SignalR 2.0 の機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="06ab3-317">OWIN に構築</span><span class="sxs-lookup"><span data-stu-id="06ab3-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="06ab3-318">マップハブとマップコネクションがマップシグナルです</span><span class="sxs-lookup"><span data-stu-id="06ab3-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="06ab3-319">クロスドメインサポート</span><span class="sxs-lookup"><span data-stu-id="06ab3-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="06ab3-320">モノタッチとモノドロイドによるiOSとアンドロイドのサポート</span><span class="sxs-lookup"><span data-stu-id="06ab3-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="06ab3-321">ポータブル .NET クライアント</span><span class="sxs-lookup"><span data-stu-id="06ab3-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="06ab3-322">新しいセルフホストパッケージ</span><span class="sxs-lookup"><span data-stu-id="06ab3-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="06ab3-323">下位互換性のあるサーバーのサポート</span><span class="sxs-lookup"><span data-stu-id="06ab3-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="06ab3-324">.NET 4.0 のサーバー サポートを削除しました</span><span class="sxs-lookup"><span data-stu-id="06ab3-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="06ab3-325">クライアントとグループのリストにメッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="06ab3-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="06ab3-326">特定のユーザーへのメッセージの送信</span><span class="sxs-lookup"><span data-stu-id="06ab3-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="06ab3-327">より良いエラー処理のサポート</span><span class="sxs-lookup"><span data-stu-id="06ab3-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="06ab3-328">ハブの単体テストが容易</span><span class="sxs-lookup"><span data-stu-id="06ab3-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="06ab3-329">エラー処理</span><span class="sxs-lookup"><span data-stu-id="06ab3-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="06ab3-330">既存の 1.x プロジェクトを SignalR 2.0 にアップグレードする方法の例については[、「SignalR 1.x プロジェクトのアップグレード](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="06ab3-331">OWIN に構築</span><span class="sxs-lookup"><span data-stu-id="06ab3-331">Built on OWIN</span></span>

<span data-ttu-id="06ab3-332">SignalR 2.0 は[OWIN (.NET 用のオープン Web インターフェイス)](http://owin.org/)上で完全に構築されています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="06ab3-333">この変更により、Web ホスト型と自己ホスト型の SignalR アプリケーション間で SignalR のセットアップ プロセスの一貫性が大幅に高くなりますが、API の変更も数多く必要になりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="06ab3-334">マップハブとマップコネクションがマップシグナルです</span><span class="sxs-lookup"><span data-stu-id="06ab3-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="06ab3-335">OWIN 標準との互換性を保つために、これらのメソッド`MapSignalR`の名前は に変更されました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="06ab3-336">`MapSignalR`パラメーターなしで呼び出されると、すべてのハブが`MapHubs`マップされます (バージョン 1.x の場合と同様)。個々の**PersistentConnection**オブジェクトをマップするには、型パラメーターとして接続の種類を指定し、最初の引数として接続の URL 拡張子を指定します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="06ab3-337">この`MapSignalR`メソッドは、Owin スタートアップ クラスで呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="06ab3-338">Visual Studio 2013 には、Owin スタートアップ クラスの新しいテンプレートが含まれています。このテンプレートを使用するには、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="06ab3-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="06ab3-339">プロジェクトを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="06ab3-339">Right-click on the project</span></span>
2. <span data-ttu-id="06ab3-340">**[追加**]、[**新しいアイテム] の順に選択します。**</span><span class="sxs-lookup"><span data-stu-id="06ab3-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="06ab3-341">**[Owin スタートアップ クラス**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="06ab3-342">新しいクラスに名前**を付けるStartup.cs。**</span><span class="sxs-lookup"><span data-stu-id="06ab3-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="06ab3-343">Web**アプリケーションでは、** 以下に示すように、`MapSignalR`メソッドを含む Owin スタートアップ クラスが、Web.Config ファイルのアプリケーション設定ノードのエントリを使用して Owin のスタートアップ プロセスに追加されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="06ab3-344">**自己ホスト型アプリケーション**では、Startup クラスが`WebApp.Start`メソッドの型パラメーターとして渡されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="06ab3-345">**SignalR 1.x のハブと接続のマッピング (Web アプリケーションのグローバル アプリケーション ファイルから):**</span><span class="sxs-lookup"><span data-stu-id="06ab3-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="06ab3-346">**SignalR 2.0 内のハブと接続のマッピング (Owin スタートアップ クラス ファイルから):**</span><span class="sxs-lookup"><span data-stu-id="06ab3-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="06ab3-347">**自己ホスト型アプリケーション**では、次に示すように、Startup クラスがメソッドの`WebApp.Start`型パラメーターとして渡されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="06ab3-348">クロスドメインサポート</span><span class="sxs-lookup"><span data-stu-id="06ab3-348">Cross-Domain Support</span></span>

<span data-ttu-id="06ab3-349">SignalR 1.x では、クロス ドメイン要求は単一の EnableCrossDomain フラグによって制御されました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="06ab3-350">このフラグは、JSONP 要求と CORS 要求の両方を制御しました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="06ab3-351">柔軟性を高めるために、SignalR のサーバー コンポーネントからすべての CORS サポートが削除され (JavaScript クライアントは、ブラウザが CORS をサポートすることが検出された場合は引き続き CORS を使用します)、これらのシナリオをサポートする新しい OWIN ミドルウェアが利用可能になりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="06ab3-352">SignalR 2.0 では、JSONP がクライアントで必要な場合 (古いブラウザーでクロスドメイン要求をサポートするため)、次に示すように`EnableJSONP``HubConfiguration`、オブジェクトに対`true`して設定して明示的に有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="06ab3-353">JSONP は、CORS よりも安全性が低いため、デフォルトでは無効になっています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="06ab3-354">SignalR 2.0 で新しい CORS ミドルウェアを`Microsoft.Owin.Cors`追加するには、次のセクションに`UseCors`示すように、プロジェクトにライブラリを追加し、SignalR ミドルウェアの前に呼び出します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="06ab3-355">**プロジェクトへの Microsoft.Owin.Cors の追加**: このライブラリをインストールするには、パッケージ マネージャ コンソールで次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="06ab3-356">このコマンドを実行すると、パッケージの 2.0.0 バージョンがプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="06ab3-357">**使用する呼び出し**</span><span class="sxs-lookup"><span data-stu-id="06ab3-357">**Calling UseCors**</span></span>

<span data-ttu-id="06ab3-358">次のコード スニペットは、SignalR 1.x と 2.0 でクロスドメイン接続を実装する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="06ab3-359">**SignalR 1.x でのクロスドメイン要求の実装 (グローバル アプリケーション ファイルからの)**</span><span class="sxs-lookup"><span data-stu-id="06ab3-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="06ab3-360">**SignalR 2.0 でのクロスドメイン要求の実装 (C# コード ファイルからの)**</span><span class="sxs-lookup"><span data-stu-id="06ab3-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="06ab3-361">次のコードは、SignalR 2.0 プロジェクトで CORS または JSONP を有効にする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="06ab3-362">このコード サンプル`Map`では`RunSignalR``MapSignalR`、 の代わりに を使用し、CORS ミドルウェアは、(で指定されたパスのすべてのトラフィックではなく) CORS サポートを必要`MapSignalR`とする SignalR 要求に対してのみ実行されるようにします。`Map`また、アプリケーション全体ではなく、特定の URL プレフィックスに対して実行する必要がある他のミドルウェアにも使用できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="06ab3-363">モノタッチとモノドロイドによるiOSとアンドロイドのサポート</span><span class="sxs-lookup"><span data-stu-id="06ab3-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="06ab3-364">[Xamarin ライブラリ](https://xamarin.com/)からモノタッチと MonoDroid コンポーネントを使用して iOS と Android クライアントのサポートが追加されました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="06ab3-365">これらの使用方法の詳細については、「 [Xamarin コンポーネントの使用](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="06ab3-366">SignalR RTW リリースが利用可能な場合、これらのコンポーネントは[Xamarin ストア](https://store.xamarin.com/)で使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="06ab3-367">### ポータブル .NET クライアント</span><span class="sxs-lookup"><span data-stu-id="06ab3-367">### Portable .NET client</span></span>

<span data-ttu-id="06ab3-368">クロスプラットフォーム開発を容易にするために、Silverlight、WinRT、および Windows Phone クライアントは、次のプラットフォームをサポートする単一のポータブル .NET クライアントに置き換えられました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="06ab3-369">ネット 4.5</span><span class="sxs-lookup"><span data-stu-id="06ab3-369">NET 4.5</span></span>
- <span data-ttu-id="06ab3-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="06ab3-370">Silverlight 5</span></span>
- <span data-ttu-id="06ab3-371">Windows ストア アプリ用の .NET</span><span class="sxs-lookup"><span data-stu-id="06ab3-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="06ab3-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="06ab3-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="06ab3-373">新しいセルフホストパッケージ</span><span class="sxs-lookup"><span data-stu-id="06ab3-373">New Self-Host Package</span></span>

<span data-ttu-id="06ab3-374">SignalR セルフ ホスト (Web サーバーでホストされるのではなく、プロセスまたは他のアプリケーションでホストされている SignalR アプリケーション) を簡単に使い始めるための NuGet パッケージが用意されました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="06ab3-375">SignalR 1.x でビルドされたセルフホスト プロジェクトをアップグレードするには、Microsoft.AspNet.SignalR.Owin パッケージを削除し、パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="06ab3-376">セルフホストパッケージの概要については、「[チュートリアル: SignalR セルフホスト](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="06ab3-377">下位互換性のあるサーバーのサポート</span><span class="sxs-lookup"><span data-stu-id="06ab3-377">Backward-compatible server support</span></span>

<span data-ttu-id="06ab3-378">SignalR の以前のバージョンでは、クライアントとサーバーで使用される SignalR パッケージのバージョンは同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="06ab3-379">更新が困難なシック クライアント アプリケーションをサポートするために、SignalR 2.0 では、古いクライアントで新しいサーバー バージョンを使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="06ab3-380">**注: SignalR 2.0 は、新しいクライアントを使用して古いバージョンで構築されたサーバーをサポートしていません。**</span><span class="sxs-lookup"><span data-stu-id="06ab3-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="06ab3-381">.NET 4.0 のサーバー サポートを削除しました</span><span class="sxs-lookup"><span data-stu-id="06ab3-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="06ab3-382">SignalR 2.0 は.NET 4.0 とのサーバーの相互運用性のサポートを低下しました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="06ab3-383">NET 4.5 は SignalR 2.0 サーバーと共に使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="06ab3-384">SignalR 2.0 には.NET 4.0 クライアントがまだあります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="06ab3-385">クライアントとグループのリストにメッセージを送信する</span><span class="sxs-lookup"><span data-stu-id="06ab3-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="06ab3-386">SignalR 2.0 では、クライアント ID とグループ ID のリストを使用してメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="06ab3-387">次のコード スニペットは、この方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="06ab3-388">**永続的な接続を使用して、クライアントとグループの一覧にメッセージを送信します。**</span><span class="sxs-lookup"><span data-stu-id="06ab3-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="06ab3-389">**ハブを使用してクライアントとグループの一覧にメッセージを送信する**</span><span class="sxs-lookup"><span data-stu-id="06ab3-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="06ab3-390">特定のユーザーへのメッセージの送信</span><span class="sxs-lookup"><span data-stu-id="06ab3-390">Sending a message to a specific user</span></span>

<span data-ttu-id="06ab3-391">この機能により、ユーザーは新しいインターフェイス IUserIdProvider を介して IRequest に基づいてユーザー ID が何であるかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="06ab3-392">**インターフェイス**</span><span class="sxs-lookup"><span data-stu-id="06ab3-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="06ab3-393">既定では、ユーザー名としてユーザーのIPrincipal.Identity.Nameを使用する実装があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="06ab3-394">ハブでは、新しい API を使用してこれらのユーザーにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="06ab3-395">**クライアントの使用.ユーザー API**</span><span class="sxs-lookup"><span data-stu-id="06ab3-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="06ab3-396">より良いエラー処理のサポート</span><span class="sxs-lookup"><span data-stu-id="06ab3-396">Better Error Handling Support</span></span>

<span data-ttu-id="06ab3-397">ユーザーは、任意のハブ呼び出しから**HubException**をスローできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="06ab3-398">**HubException**のコンストラクターは、文字列メッセージとオブジェクトの追加のエラー データを受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="06ab3-399">SignalR は、例外を自動シリアル化し、ハブ メソッドの呼び出しを拒否または失敗するために使用されるクライアントに送信します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="06ab3-400">**詳細なハブ例外の**設定は、クライアントに送り返される**HubException**に関係ありません。常に送信されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="06ab3-401">**クライアントに HubException を送信する方法を示すサーバー側コード**</span><span class="sxs-lookup"><span data-stu-id="06ab3-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="06ab3-402">**サーバーから送信されたハブ例外への応答を示す JavaScript クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="06ab3-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="06ab3-403">**サーバーから送信された HubException への応答を示す .NET クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="06ab3-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="06ab3-404">ハブの単体テストが容易</span><span class="sxs-lookup"><span data-stu-id="06ab3-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="06ab3-405">SignalR 2.0 には、`IHubCallerConnectionContext`モック クライアント側呼び出しを簡単に作成できる、Hubs で呼び出されるインターフェイスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="06ab3-406">次のコード スニペットは、このインターフェイスを一般的なテスト ハーネス[xUnit.net](https://github.com/xunit/xunit)と[moq](https://code.google.com/p/moq/)で使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="06ab3-407">**xUnit.netを使用したユニットテスト信号機**</span><span class="sxs-lookup"><span data-stu-id="06ab3-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="06ab3-408">**moq を使用したユニットテストシグナルR**</span><span class="sxs-lookup"><span data-stu-id="06ab3-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="06ab3-409">エラー処理</span><span class="sxs-lookup"><span data-stu-id="06ab3-409">JavaScript error handling</span></span>

<span data-ttu-id="06ab3-410">SignalR 2.0 では、すべての JavaScript エラー処理コールバックは、生の文字列ではなく JavaScript エラー オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="06ab3-411">これにより、SignalR は、より豊富な情報をエラー ハンドラーに流すことができます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="06ab3-412">エラーのプロパティから内部例外を`source`取得できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="06ab3-413">**開始エラー例外を処理する JavaScript クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="06ab3-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="06ab3-414">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="06ab3-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="06ab3-415">新しいASP.NET会員制度</span><span class="sxs-lookup"><span data-stu-id="06ab3-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="06ab3-416">ASP.NET識別は、ASP.NETアプリケーションの新しいメンバーシップ システムです。</span><span class="sxs-lookup"><span data-stu-id="06ab3-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="06ab3-417">ASP.NET Identity を使用すると、ユーザー固有のプロファイル データをアプリケーション データに簡単に統合できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="06ab3-418">ASP.NET Identity では、アプリケーションのユーザー プロファイルの永続性モデルを選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="06ab3-419">データは、SQL Server データベースまたは別のデータ ストア (Azure ストレージ テーブルなどの NoSQL データ ストアを含む) に格納できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="06ab3-420">詳細については、「 **Visual Studio 2013 での ASP.NET Web プロジェクトの作成**」の[「個々のユーザー アカウント](creating-web-projects-in-visual-studio.md#indauth)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="06ab3-421">クレーム ベースの認証</span><span class="sxs-lookup"><span data-stu-id="06ab3-421">Claims-based authentication</span></span>

<span data-ttu-id="06ab3-422">ASP.NETは、ユーザーの ID が信頼された発行者からのクレームのセットとして表されるクレーム ベース認証をサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="06ab3-423">ユーザーは、アプリケーション データベースで管理されているユーザー名とパスワード、またはソーシャル ID プロバイダー (たとえば、Microsoft アカウント、Facebook、Google、Twitter) を使用するか、Azure Active Directory または Active Directory フェデレーション サービス (ADFS) を通じて組織アカウントを使用して認証できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="06ab3-424">Azure アクティブ ディレクトリおよび Windows サーバーのアクティブ ディレクトリとの統合</span><span class="sxs-lookup"><span data-stu-id="06ab3-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="06ab3-425">認証に Azure アクティブ ディレクトリまたは Windows サーバーのアクティブ ディレクトリ (AD) を使用するASP.NET プロジェクトを作成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="06ab3-426">詳細については、「 Visual Studio **2013 での ASP.NET Web プロジェクトの作成**」の[「組織アカウント](creating-web-projects-in-visual-studio.md#orgauth)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="06ab3-427">OWIN 統合</span><span class="sxs-lookup"><span data-stu-id="06ab3-427">OWIN Integration</span></span>

<span data-ttu-id="06ab3-428">ASP.NET認証は、OWIN ベースのホストで使用できる OWIN ミドルウェアに基づくようになりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="06ab3-429">OWIN の詳細については、次の[マイクロソフトの OWIN コンポーネントセクションを](#TOC7)参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="06ab3-430">Microsoft OWIN コンポーネント</span><span class="sxs-lookup"><span data-stu-id="06ab3-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="06ab3-431">[オープン Web インターフェイスの .NET](http://owin.org/) (OWIN) は、.NET Web サーバーと Web アプリケーション間の抽象化を定義します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="06ab3-432">OWIN は Web アプリケーションをサーバーから切り離し、Web アプリケーションをホストに依存しません。</span><span class="sxs-lookup"><span data-stu-id="06ab3-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="06ab3-433">たとえば、IIS で OWIN ベースの Web アプリケーションをホストしたり、カスタム プロセスで自己ホストしたりできます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="06ab3-434">Microsoft OWIN コンポーネント (Katana プロジェクトとも呼ばれます) で導入された変更点には、新しいサーバーコンポーネントとホスト コンポーネント、新しいヘルパー ライブラリとミドルウェア、新しい認証ミドルウェアなどがあります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="06ab3-435">OWIN とカタナの詳細については、「 [OWIN およびカタナの新機能](../../../aspnet/overview/owin-and-katana/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="06ab3-436">**注: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)アプリケーションは IIS クラシック モードでは実行できません。統合モードで実行する必要があります。**</span><span class="sxs-lookup"><span data-stu-id="06ab3-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="06ab3-437">**注: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)アプリケーションは、完全信頼で実行する必要があります。**</span><span class="sxs-lookup"><span data-stu-id="06ab3-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="06ab3-438">新しいサーバーとホスト</span><span class="sxs-lookup"><span data-stu-id="06ab3-438">New Servers and Hosts</span></span>

<span data-ttu-id="06ab3-439">このリリースでは、セルフホストシナリオを可能にする新しいコンポーネントが追加されました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="06ab3-440">これらのコンポーネントには、次の NuGet パッケージが含まれます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="06ab3-441">**マイクロソフト.Owin.ホスト.Httpリスナー**.</span><span class="sxs-lookup"><span data-stu-id="06ab3-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="06ab3-442">HTTPListener を使用して**HTTP 要求**をリッスンし、OWIN パイプラインに送信する OWIN サーバーを提供します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="06ab3-443">**コンソール**アプリケーションや Windows サービスなどのカスタム プロセスで OWIN パイプラインを自己ホストする開発者向けのライブラリを提供します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="06ab3-444">**オビンホスト**.</span><span class="sxs-lookup"><span data-stu-id="06ab3-444">**OwinHost**.</span></span> <span data-ttu-id="06ab3-445">カスタム ホスト アプリケーションを作成しなくても`Microsoft.Owin.Hosting`OWIN パイプラインをラップして自己ホストできるスタンドアロンの実行可能ファイルを提供します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="06ab3-446">さらに、このパッケージ`Microsoft.Owin.Host.SystemWeb`では、ミドルウェアが**SystemWeb**サーバーにヒントを提供できるようになったので、特定のASP.NET パイプラインステージでミドルウェアを呼び出す必要があることを示します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="06ab3-447">この機能は、ASP.NET パイプラインの初期段階で実行する必要がある認証ミドルウェアに特に便利です。</span><span class="sxs-lookup"><span data-stu-id="06ab3-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="06ab3-448">ヘルパー ライブラリとミドルウェア</span><span class="sxs-lookup"><span data-stu-id="06ab3-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="06ab3-449">OWIN 仕様の関数と型の定義のみを使用して OWIN コンポーネントを作成できますが、`Microsoft.Owin`新しいパッケージでは、よりユーザーフレンドリな抽象化セットが提供されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="06ab3-450">このパッケージは、いくつかの以前のパッケージ (たとえば、 `Owin.Extensions`)`Owin.Types`を組み合わせて、他の OWIN コンポーネントで簡単に使用できる、適切に構造化された単一のオブジェクト モデルにします。</span><span class="sxs-lookup"><span data-stu-id="06ab3-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="06ab3-451">実際、現在、大部分の OWIN コンポーネントがこのパッケージを使用しています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="06ab3-452">[OWIN](http://www.owin.org)アプリケーションは IIS クラシック モードでは実行できません。統合モードで実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="06ab3-453">[OWIN](http://www.owin.org)アプリケーションは、完全な信頼で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="06ab3-454">このリリースには、実行中の OWIN アプリケーションを検証するためのミドルウェアと、エラーの調査に役立つエラー ページミドルウェアが含まれる Microsoft.Owin.Diagnostics パッケージも含まれています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="06ab3-455">認証コンポーネント</span><span class="sxs-lookup"><span data-stu-id="06ab3-455">Authentication Components</span></span>

<span data-ttu-id="06ab3-456">次の認証コンポーネントを使用できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-456">The following authentication components are available.</span></span>

- <span data-ttu-id="06ab3-457">**マイクロソフト.Owin.セキュリティ.アクティブディレクトリ**.</span><span class="sxs-lookup"><span data-stu-id="06ab3-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="06ab3-458">オンプレミスまたはクラウドベースのディレクトリ サービスを使用した認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="06ab3-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="06ab3-459">**クッキーを**使用した認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="06ab3-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="06ab3-460">このパッケージは以前に`Microsoft.Owin.Security.Forms`という名前でした。</span><span class="sxs-lookup"><span data-stu-id="06ab3-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="06ab3-461">**Facebookの**OAuthベースのサービスを使用した認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="06ab3-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="06ab3-462">**Google の**OpenID ベースのサービスを使用した認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="06ab3-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="06ab3-463">JWT トークンを使用した**認証を有効**にします。</span><span class="sxs-lookup"><span data-stu-id="06ab3-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="06ab3-464">**マイクロソフト アカウントを**使用した認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="06ab3-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="06ab3-465">**マイクロソフト.Owin.セキュリティ.OAuth**.</span><span class="sxs-lookup"><span data-stu-id="06ab3-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="06ab3-466">ベアラー トークンを認証するためのミドルウェアと同様に、OAuth 承認サーバーを提供します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="06ab3-467">**Twitter の**OAuth ベースのサービスを使用した認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="06ab3-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="06ab3-468">このリリースには、クロス`Microsoft.Owin.Cors`オリジン HTTP 要求を処理するためのミドルウェアが含まれているパッケージも含まれています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="06ab3-469">JwT 署名のサポートは、Visual Studio 2013 の最終バージョンでは削除されました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="06ab3-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="06ab3-470">Entity Framework 6</span></span>

<span data-ttu-id="06ab3-471">Entity Framework 6 の新機能およびその他の変更の一覧については、「[エンティティ フレームワークのバージョン履歴](https://msdn.com/data/jj574253)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="06ab3-472">ASP.NETカミソリ3</span><span class="sxs-lookup"><span data-stu-id="06ab3-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="06ab3-473">ASP.NETのRazor 3には、次の新機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="06ab3-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="06ab3-474">タブ編集のサポート。</span><span class="sxs-lookup"><span data-stu-id="06ab3-474">Support for Tab editing.</span></span> <span data-ttu-id="06ab3-475">以前は、[**タブを保持**] オプションを使用する場合、Visual Studio での **[ドキュメントの書式設定**] コマンド、自動インデント、および自動書式設定が正しく機能しませんでした。</span><span class="sxs-lookup"><span data-stu-id="06ab3-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="06ab3-476">この変更により、タブの書式設定に関する Razor コードの Visual Studio の書式設定が修正されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="06ab3-477">リンク生成時の URL 書き換えルールのサポート。</span><span class="sxs-lookup"><span data-stu-id="06ab3-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="06ab3-478">透過的セキュリティ属性の削除</span><span class="sxs-lookup"><span data-stu-id="06ab3-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="06ab3-479">これは画期的な変更であり、Razor 3 は MVC4 以前と互換性がありませんが、Razor 2 は MVC5 または MVC5 に対してコンパイルされたアセンブリと互換性がありません。</span><span class="sxs-lookup"><span data-stu-id="06ab3-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="06ab3-480">プレリリース版から Visual Studio 2013 で修正された Razor 3 の問題は[、こちら](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)を見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="06ab3-481">ASP.NETアプリの中断</span><span class="sxs-lookup"><span data-stu-id="06ab3-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="06ab3-482">ASP.NETアプリケーションの中断は、1 台のコンピューターで多数のASP.NET サイトをホストするためのユーザー エクスペリエンスと経済モデルを根本的に変更する .NET Framework 4.5.1 のゲームを変更する機能です。</span><span class="sxs-lookup"><span data-stu-id="06ab3-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="06ab3-483">詳細については、「[アプリの中断 - 応答性の高い共有 .NET web ホスティング](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)」をASP.NETするを参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="06ab3-484">既知の問題と互換性に関する変更</span><span class="sxs-lookup"><span data-stu-id="06ab3-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="06ab3-485">このセクションでは、Visual Studio 2013 のASP.NETと Web ツールでの既知の問題と互換性に関する変更点について説明します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="06ab3-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="06ab3-486">NuGet</span></span>

- <span data-ttu-id="06ab3-487">[新しいパッケージの復元は、SLN ファイルを使用する場合は Mono で動作しません](https://nuget.codeplex.com/workitem/3596)- nuget.exe のダウンロードと[NuGet.CommandLine パッケージ](http://www.nuget.org/packages/NuGet.CommandLine/)の更新プログラムで修正されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="06ab3-488">[新しいパッケージの復元は Wix プロジェクトでは動作しません](https://nuget.codeplex.com/workitem/3598)- 今後の nuget.exe ダウンロードと[NuGet.CommandLine パッケージ](http://www.nuget.org/packages/NuGet.CommandLine/)の更新プログラムで修正されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="06ab3-489">[自動パッケージの復元は、ソリューション フォルダーの下のプロジェクトでは機能しません](https://nuget.codeplex.com/workitem/3625)- NuGet 2.8 で修正されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="06ab3-490">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="06ab3-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="06ab3-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)`と のサポート`IQueryable<T>`を追加したので、常に`$select`戻る`$expand`わけではありません。</span><span class="sxs-lookup"><span data-stu-id="06ab3-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="06ab3-492">以前のサンプルでは`ODataQueryOptions<T>`、戻り値が常に`ApplyTo``IQueryable<T>`から にキャストされます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="06ab3-493">以前にサポートしていたクエリ`$filter`オプション ( , , `$orderby` `$skip`)`$top`ではクエリの形状が変更されないため、これは以前に機能していました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="06ab3-494">今、私たちは`$select`サポート`$expand`し、戻`ApplyTo`り値は常`IQueryable<T>`にではありません。</span><span class="sxs-lookup"><span data-stu-id="06ab3-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="06ab3-495">以前のサンプル コードを使用している場合、クライアントが 送信しない場合は引き続`$select`き`$expand`動作します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="06ab3-496">ただし、サポート`$select`を希望し、`$expand`そのコードをこれに変更する必要がある場合は、</span><span class="sxs-lookup"><span data-stu-id="06ab3-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="06ab3-497">**バッチ要求中に、要求 URL または要求コンテキスト URL が null です。**</span><span class="sxs-lookup"><span data-stu-id="06ab3-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="06ab3-498">バッチ処理シナリオでは、要求 URL または**要求コンテキスト** **URL**からアクセスすると**UrlHelper**は null です。</span><span class="sxs-lookup"><span data-stu-id="06ab3-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="06ab3-499">この問題は現在ここで追跡されています:[バッチ処理要求の場合、Url は null です](http://aspnetwebstack.codeplex.com/workitem/1301)。</span><span class="sxs-lookup"><span data-stu-id="06ab3-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="06ab3-500">この問題の回避策は、次の例のように**UrlHelper**の新しいインスタンスを作成することです。</span><span class="sxs-lookup"><span data-stu-id="06ab3-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="06ab3-501">**Url ヘルパーの新しいインスタンスの作成**</span><span class="sxs-lookup"><span data-stu-id="06ab3-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="06ab3-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="06ab3-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="06ab3-503">MVC5 と OrgAuth を使用する場合、AntiForgerToken 検証を行うビューがある場合、ビューにデータを送信するときに次のエラーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="06ab3-504">**エラー**:</span><span class="sxs-lookup"><span data-stu-id="06ab3-504">**Error**:</span></span>

    <span data-ttu-id="06ab3-505">*'/' アプリケーションのサーバー エラーです。*</span><span class="sxs-lookup"><span data-stu-id="06ab3-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="06ab3-506"><em>指定された ClaimsId<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>に<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>'' または ' ' の型のクレームが存在しませんでした。クレームベース認証で偽造防止トークンのサポートを有効にするには、構成されたクレーム プロバイダーが、生成する ClaimsIdentity インスタンスでこれらの両方のクレームを提供していることを確認してください。構成済みのクレーム プロバイダーが一意の識別子として異なるクレームの種類を使用する場合は、静的プロパティ AntiForgeryConfig.UniqueClaimTypeIdentifier を設定することで構成できます。</em></span><span class="sxs-lookup"><span data-stu-id="06ab3-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="06ab3-507">**対応策**:</span><span class="sxs-lookup"><span data-stu-id="06ab3-507">**Workaround**:</span></span>

    <span data-ttu-id="06ab3-508">これを修正するには、Global.asax に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="06ab3-509">これは、次のリリースで修正されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="06ab3-510">MVC4 アプリを MVC5 にアップグレードした後、ソリューションをビルドして起動します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="06ab3-511">次のエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-511">You should see the following error:</span></span>

    <span data-ttu-id="06ab3-512">[A][B] システムにキャストできません。</span><span class="sxs-lookup"><span data-stu-id="06ab3-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="06ab3-513">タイプ\_A は 'System.Web.WebPages.Razor から発信されます。 バージョン=2.0.0.0,カルチャー=ニュートラル,公開鍵トークン=31bf3856ad364e35''コンテキスト'の場所'C:\windows\Net\アセンブリ\GAC MSIL\システム.Web.Webページ.Razor\v4.0\_2.0.0.31bf3856ad364e33\Web.Dll.Web.Web.Dll.Web.Web.Dll.Web.Web\_\_ページ</span><span class="sxs-lookup"><span data-stu-id="06ab3-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="06ab3-514">タイプ B は 'System.Web.WebPages.Razor, バージョン = 3.0.0.0, カルチャ =ニュートラル、 場所 'C:\Windows\NET\Framework\v4.0.30319\一時ASP.NET ファイル\ルート\6 のコンテキスト '既定' で公開キートークン=31bf3856ad364e35' d05bbd0\e8b5908e\アセンブリ\dl3\c9cbca63\f8910382\_6273ce01\システム.Web.WebPages.Razor.dll'。</span><span class="sxs-lookup"><span data-stu-id="06ab3-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="06ab3-515">上記のエラーを修正するには、プロジェクト*内のすべての*Web.config ファイル (Views フォルダー内のファイルを含む) を開き、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="06ab3-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="06ab3-516">"System.Web.Mvc" のバージョン "4.0.0.0" のすべてのオカレンスを "5.0.0.0" に更新します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="06ab3-517">「システム.Web.ヘルパー」、システム&quot;.Web.Webページ、&quot;&quot;システム.Web.WebPages.Razor&quot;のバージョン"2.0.0.0"のすべてのオカレンスを「3.0.0.0」に更新します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="06ab3-518">たとえば、上記の変更を行った後、アセンブリ バインディングは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="06ab3-519">MVC 4 プロジェクトを MVC 5 にアップグレードする[方法については、「MVC 4 と Web API プロジェクトASP.NETを MVC 5 と Web API 2 ASP.NETにアップグレードする方法](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="06ab3-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="06ab3-520">jQuery の控えめな検証でクライアント側の検証を使用する場合、検証メッセージは、型が'number' の HTML 入力要素に対して正しくない場合があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="06ab3-521">有効な数値が必要であることを示す正しいメッセージではなく、無効な数値が入力されると、必要な値の検証エラー (「年齢フィールドが必要です」) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="06ab3-522">この問題は、一般に、作成ビューと編集ビューで整数プロパティを持つモデルのスキャフォールディングされたコードで発生します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="06ab3-523">この問題を回避するには、エディター ヘルパーを次の手順で変更します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="06ab3-524">変更後:</span><span class="sxs-lookup"><span data-stu-id="06ab3-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="06ab3-525">ASP.NET MVC 5 では、部分信頼がサポートされなくなりました。</span><span class="sxs-lookup"><span data-stu-id="06ab3-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="06ab3-526">MVC または WebAPI バイナリにリンクしているプロジェクトは、[セキュリティトランスペアレント](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)属性と[AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)属性を削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="06ab3-527">これらの属性を削除すると、次のようなコンパイラ エラーが解消されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="06ab3-528">この副次的な効果として、同じアプリケーションで 4.0 および 5.0 のアセンブリを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="06ab3-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="06ab3-529">すべてのファイルを 5.0 に更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="06ab3-530">Facebookの承認を持つSPAテンプレートは、Webサイトがイントラネットゾーンでホストされている間、IEで不安定になる可能性があります</span><span class="sxs-lookup"><span data-stu-id="06ab3-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="06ab3-531">SPA テンプレートは、Facebook で外部ログインを提供します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="06ab3-532">テンプレートで作成されたプロジェクトがローカルで実行されている場合、サインインすると IE がクラッシュする可能性があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="06ab3-533">解決方法:</span><span class="sxs-lookup"><span data-stu-id="06ab3-533">Solution:</span></span>

1. <span data-ttu-id="06ab3-534">インターネット ゾーンで Web サイトをホストします。または</span><span class="sxs-lookup"><span data-stu-id="06ab3-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="06ab3-535">IE 以外のブラウザーでシナリオをテストします。</span><span class="sxs-lookup"><span data-stu-id="06ab3-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="06ab3-536">Web フォームのスキャフォールディング</span><span class="sxs-lookup"><span data-stu-id="06ab3-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="06ab3-537">Web フォームスキャフォールディングは VS2013 から削除され、Visual Studio の今後の更新プログラムで使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="06ab3-538">ただし、MVC 依存関係を追加し、MVC のスキャフォールディングを生成することで、Web フォーム プロジェクト内でスキャフォールディングを使用できます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="06ab3-539">プロジェクトには、Web フォームと MVC の組み合わせが含まれます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="06ab3-540">Mvc を Web フォーム プロジェクトに追加するには、新しいスキャフォールディングされた項目を追加し **、[MVC 5 依存関係**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="06ab3-541">スクリプトなど、すべてのコンテンツ ファイルが必要かどうかに応じて、[最小] または [完全] を選択します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="06ab3-542">次に、プロジェクト内にビューとコント ローラーを作成する MVC のスキャフォールディング項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="06ab3-543">MVC および Web API スキャフォールディング - HTTP 404、見つかりませんエラー</span><span class="sxs-lookup"><span data-stu-id="06ab3-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="06ab3-544">スキャフォールディングされた項目をプロジェクトに追加するときにエラーが発生した場合、プロジェクトが不整合な状態のままになる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="06ab3-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="06ab3-545">スキャフォールディングに加えられた変更の一部はロールバックされますが、インストールされている NuGet パッケージなどの他の変更はロールバックされません。</span><span class="sxs-lookup"><span data-stu-id="06ab3-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="06ab3-546">ルーティング構成の変更がロールバックされると、スキャフォールディングされたアイテムに移動するときに、ユーザーに HTTP 404 エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="06ab3-547">対処法:</span><span class="sxs-lookup"><span data-stu-id="06ab3-547">Workaround:</span></span>

- <span data-ttu-id="06ab3-548">MVC のこのエラーを修正するには、新しいスキャフォールディングされた項目を追加し、MVC 5 の依存関係 (最小または完全) を選択します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="06ab3-549">このプロセスにより、必要な変更がすべてプロジェクトに追加されます。</span><span class="sxs-lookup"><span data-stu-id="06ab3-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="06ab3-550">Web API でこのエラーを修正するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="06ab3-551">プロジェクトにクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="06ab3-552">次のようにして、Global.asax\_のアプリケーション開始メソッドで WebApiConfig.Register を構成します。</span><span class="sxs-lookup"><span data-stu-id="06ab3-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
