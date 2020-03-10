---
uid: overview
title: ASP.NET の概要 |Microsoft Docs
author: rick-anderson
description: ASP.NET、web サイト、web アプリケーション、および web API を作成するための無償のフレームワークを紹介します。
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.author: riande
ms.date: 08/10/2019
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: aa4f627bca99f0a7ffbbb53ea45ebdcf0850fd89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431878"
---
# <a name="aspnet-overview"></a><span data-ttu-id="f26e6-103">ASP.NET 概要</span><span class="sxs-lookup"><span data-stu-id="f26e6-103">ASP.NET overview</span></span>

<span data-ttu-id="f26e6-104">ASP.NET は、HTML、CSS、および JavaScript を使用して優れた web サイトや web アプリケーションを構築するための無料の web フレームワークです。</span><span class="sxs-lookup"><span data-stu-id="f26e6-104">ASP.NET is a free web framework for building great websites and web applications using HTML, CSS, and JavaScript.</span></span> <span data-ttu-id="f26e6-105">Web API を作成し、Web ソケットなどのリアルタイム テクノロジを使用できます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-105">You can also create Web APIs and use real-time technologies like Web Sockets.</span></span>

<span data-ttu-id="f26e6-106">[ASP.NET Core](https://docs.microsoft.com/aspnet/core/)は、ASP.NET の代わりになります。</span><span class="sxs-lookup"><span data-stu-id="f26e6-106">[ASP.NET Core](https://docs.microsoft.com/aspnet/core/) is an alternative to ASP.NET.</span></span>  <span data-ttu-id="f26e6-107">[ASP.NET と ASP.NET Core のどちらを選択するかについ](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework)ては、ガイダンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f26e6-107">See the [guidance on how to choose between ASP.NET and ASP.NET Core](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework).</span></span>

## <a name="get-started"></a><span data-ttu-id="f26e6-108">はじめに</span><span class="sxs-lookup"><span data-stu-id="f26e6-108">Get started</span></span>

<span data-ttu-id="f26e6-109">Windows 上の ASP.NET 用の無料の IDE である[Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019) Community edition をインストールします。</span><span class="sxs-lookup"><span data-stu-id="f26e6-109">Install [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019) Community edition, a free IDE for ASP.NET on Windows.</span></span>

## <a name="websites-and-web-applications"></a><span data-ttu-id="f26e6-110">Web サイトと web アプリケーション</span><span class="sxs-lookup"><span data-stu-id="f26e6-110">Websites and web applications</span></span>

 <span data-ttu-id="f26e6-111">ASP.NET には、web アプリケーションを作成するための3つのフレームワーク (Web フォーム、ASP.NET MVC、および ASP.NET Web ページ) が用意されています。</span><span class="sxs-lookup"><span data-stu-id="f26e6-111">ASP.NET offers three frameworks for creating web applications: Web Forms, ASP.NET MVC, and ASP.NET Web Pages.</span></span> <span data-ttu-id="f26e6-112">この3つのフレームワークはすべて安定して成熟しており、いずれのフレームワークでも優れた web アプリケーションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-112">All three frameworks are stable and mature, and you can create great web applications with any of them.</span></span> <span data-ttu-id="f26e6-113">どのようなフレームワークを選択しても、どこにいても ASP.NET のすべての利点と機能が得られます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-113">No matter what framework you choose, you will get all the benefits and features of ASP.NET everywhere.</span></span>

<span data-ttu-id="f26e6-114">各フレームワークは、別の開発スタイルを対象としています。</span><span class="sxs-lookup"><span data-stu-id="f26e6-114">Each framework targets a different development style.</span></span> <span data-ttu-id="f26e6-115">どちらを選択するかは、プログラミングアセット (知識、スキル、および開発エクスペリエンス) の組み合わせ、作成するアプリケーションの種類、および使い慣れた開発アプローチによって異なります。</span><span class="sxs-lookup"><span data-stu-id="f26e6-115">The one you choose depends on a combination of your programming assets (knowledge, skills, and development experience), the type of application you're creating, and the development approach you're comfortable with.</span></span>

<span data-ttu-id="f26e6-116">各フレームワークの概要と、それらを選択する方法に関するいくつかのアイデアを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="f26e6-116">Below is an overview of each of the frameworks and some ideas for how to choose between them.</span></span> <span data-ttu-id="f26e6-117">ビデオの概要については、「 [ASP.NET を使用した Web サイトの作成](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET)」および「 [Web ツールとは](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f26e6-117">If you prefer a video introduction, see [Making Websites with ASP.NET](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) and [What is Web Tools?](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)</span></span>

|   | <span data-ttu-id="f26e6-118">の経験がある場合</span><span class="sxs-lookup"><span data-stu-id="f26e6-118">If you have experience in</span></span> | <span data-ttu-id="f26e6-119">開発スタイル</span><span class="sxs-lookup"><span data-stu-id="f26e6-119">Development style</span></span> | <span data-ttu-id="f26e6-120">家</span><span class="sxs-lookup"><span data-stu-id="f26e6-120">Expertise</span></span> |
|-----------|----------------------|-----------------------------------------------------|----------------|
| <span data-ttu-id="f26e6-121">Web フォーム</span><span class="sxs-lookup"><span data-stu-id="f26e6-121">Web Forms</span></span> | <span data-ttu-id="f26e6-122">Win フォーム、WPF、.NET</span><span class="sxs-lookup"><span data-stu-id="f26e6-122">Win Forms, WPF, .NET</span></span> | <span data-ttu-id="f26e6-123">HTML マークアップをカプセル化するコントロールの豊富なライブラリを使用した迅速な開発</span><span class="sxs-lookup"><span data-stu-id="f26e6-123">Rapid development using a rich library of controls that encapsulate HTML markup</span></span> | <span data-ttu-id="f26e6-124">ミッドレベル、高度な RAD</span><span class="sxs-lookup"><span data-stu-id="f26e6-124">Mid-Level, Advanced RAD</span></span> |
| <span data-ttu-id="f26e6-125">MVC</span><span class="sxs-lookup"><span data-stu-id="f26e6-125">MVC</span></span>       | <span data-ttu-id="f26e6-126">Ruby on Rails、.NET</span><span class="sxs-lookup"><span data-stu-id="f26e6-126">Ruby on Rails, .NET</span></span>  | <span data-ttu-id="f26e6-127">HTML マークアップ、コードとマークアップの分離、およびテストの記述を簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-127">Full control over HTML markup, code and markup separated, and easy to write tests.</span></span> <span data-ttu-id="f26e6-128">モバイルアプリケーションとシングルページアプリケーション (SPA) に最適な選択肢です。</span><span class="sxs-lookup"><span data-stu-id="f26e6-128">The best choice for mobile and single-page applications (SPA).</span></span> | <span data-ttu-id="f26e6-129">ミッドレベル、詳細</span><span class="sxs-lookup"><span data-stu-id="f26e6-129">Mid-Level, Advanced</span></span> |
| <span data-ttu-id="f26e6-130">Web ページ</span><span class="sxs-lookup"><span data-stu-id="f26e6-130">Web Pages</span></span>  | <span data-ttu-id="f26e6-131">Classic ASP、PHP</span><span class="sxs-lookup"><span data-stu-id="f26e6-131">Classic ASP, PHP</span></span>     | <span data-ttu-id="f26e6-132">同じファイル内の HTML マークアップとコードの組み合わせ</span><span class="sxs-lookup"><span data-stu-id="f26e6-132">HTML markup and your code together in the same file</span></span> | <span data-ttu-id="f26e6-133">新規、中間レベル</span><span class="sxs-lookup"><span data-stu-id="f26e6-133">New, Mid-Level</span></span> |

### <a name="web-forms"></a><span data-ttu-id="f26e6-134">Web フォーム</span><span class="sxs-lookup"><span data-stu-id="f26e6-134">Web Forms</span></span>

<span data-ttu-id="f26e6-135">ASP.NET Web フォームを使用すると、使い慣れたドラッグアンドドロップのイベントドリブンモデルを使用して、動的な web サイトを構築できます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-135">With ASP.NET Web Forms, you can build dynamic websites using a familiar drag-and-drop, event-driven model.</span></span> <span data-ttu-id="f26e6-136">デザイン サーフェスや数百あるコントロールとコンポーネントを利用し、洗練された強力な UI 駆動型サイトとデータ アクセスを短時間で構築できます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-136">A design surface and hundreds of controls and components let you rapidly build sophisticated, powerful UI-driven sites with data access.</span></span>

[<span data-ttu-id="f26e6-137">Web フォームについての詳細情報</span><span class="sxs-lookup"><span data-stu-id="f26e6-137">Learn more about Web Forms</span></span>](web-forms/index.md)

### <a name="mvc"></a><span data-ttu-id="f26e6-138">MVC</span><span class="sxs-lookup"><span data-stu-id="f26e6-138">MVC</span></span>

<span data-ttu-id="f26e6-139">ASP.NET MVC には、動的な Web サイトを構築するための強力なパターン ベースの方法が用意されており、楽しみながら迅速に開発できるように、問題を完全に切し離しマークアップを自由に制御できます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-139">ASP.NET MVC gives you a powerful, patterns-based way to build dynamic websites that enables a clean separation of concerns and that gives you full control over markup for enjoyable, agile development.</span></span> <span data-ttu-id="f26e6-140">ASP.NET MVC には、高速な TDD 対応の開発環境で、最新の Web 規格を使用する高度なアプリケーションを作成できる数多くの機能があります。</span><span class="sxs-lookup"><span data-stu-id="f26e6-140">ASP.NET MVC includes many features that enable fast, TDD-friendly development for creating sophisticated applications that use the latest web standards.</span></span>

[<span data-ttu-id="f26e6-141">MVC の詳細情報</span><span class="sxs-lookup"><span data-stu-id="f26e6-141">Learn more about MVC</span></span>](mvc/index.md)

### <a name="aspnet-web-pages"></a><span data-ttu-id="f26e6-142">ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="f26e6-142">ASP.NET Web Pages</span></span>

<span data-ttu-id="f26e6-143">ASP.NET Web ページと Razor 構文は、サーバーコードと HTML を組み合わせて動的な Web コンテンツを作成するための高速でわかりやすく、軽量な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="f26e6-143">ASP.NET Web Pages and the Razor syntax provide a fast, approachable, and lightweight way to combine server code with HTML to create dynamic web content.</span></span> <span data-ttu-id="f26e6-144">データベースに接続し、ビデオを追加し、ソーシャルネットワーキングサイトにリンクします。また、最新の web 標準に準拠した美しいサイトの作成に役立つ多くの機能が追加されています。</span><span class="sxs-lookup"><span data-stu-id="f26e6-144">Connect to databases, add video, link to social networking sites, and include many more features that help you create beautiful sites that conform to the latest web standards.</span></span>

[<span data-ttu-id="f26e6-145">Web ページについての詳細情報</span><span class="sxs-lookup"><span data-stu-id="f26e6-145">Learn more about Web Pages</span></span>](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a><span data-ttu-id="f26e6-146">Web フォーム、MVC、および Web ページに関する注意事項</span><span class="sxs-lookup"><span data-stu-id="f26e6-146">Notes about Web Forms, MVC, and Web Pages</span></span>

<span data-ttu-id="f26e6-147">3つの ASP.NET フレームワークはすべて、.NET と ASP.NET の .NET Framework と共有のコア機能をベースとしています。</span><span class="sxs-lookup"><span data-stu-id="f26e6-147">All three ASP.NET frameworks are based on the .NET Framework and share core functionality of .NET and of ASP.NET.</span></span> <span data-ttu-id="f26e6-148">たとえば、3つのすべてのフレームワークでは、メンバーシップに基づいたログインセキュリティモデルが提供されます。また、3つすべては、コア ASP.NET 機能の一部である要求の管理、セッションの処理などのために同じ機能を共有します。</span><span class="sxs-lookup"><span data-stu-id="f26e6-148">For example, all three frameworks offer a login security model based around membership, and all three share the same facilities for managing requests, handling sessions, and so on that are part of the core ASP.NET functionality.</span></span>

<span data-ttu-id="f26e6-149">また、3つのフレームワークは完全に独立しているわけではなく、どちらを選択しても、別のフレームワークを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="f26e6-149">In addition, the three frameworks are not entirely independent, and choosing one does not preclude using another.</span></span> <span data-ttu-id="f26e6-150">フレームワークは同じ web アプリケーション内に共存できるため、異なるフレームワークを使用して記述されたアプリケーションの個々のコンポーネントを確認することは珍しくありません。</span><span class="sxs-lookup"><span data-stu-id="f26e6-150">Since the frameworks can coexist in the same web application, it's not uncommon to see individual components of applications written using different frameworks.</span></span> <span data-ttu-id="f26e6-151">たとえば、データ アクセスと管理の部分はデータ コントロールと単純なデータ アクセスを活用するために Web フォームで開発中に、マークアップを最適化するために MVC アプリの顧客向けの部分を開発する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f26e6-151">For example, customer-facing portions of an app might be developed in MVC to optimize the markup, while the data access and administrative portions are developed in Web Forms to take advantage of data controls and simple data access.</span></span>

## <a name="web-apis"></a><span data-ttu-id="f26e6-152">Web API</span><span class="sxs-lookup"><span data-stu-id="f26e6-152">Web APIs</span></span>

<span data-ttu-id="f26e6-153">ASP.NET Web API は、ブラウザーやモバイル デバイスなどを含む多様なクライアントに提供できる HTTP サービスの構築が容易になるフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="f26e6-153">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="f26e6-154">ASP.NET Web API は、.NET Framework 上で RESTful アプリケーションを構築するためのプラットフォームとして理想的です。</span><span class="sxs-lookup"><span data-stu-id="f26e6-154">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

[<span data-ttu-id="f26e6-155">Web API の詳細</span><span class="sxs-lookup"><span data-stu-id="f26e6-155">Learn more about Web API</span></span>](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a><span data-ttu-id="f26e6-156">リアルタイムテクノロジ</span><span class="sxs-lookup"><span data-stu-id="f26e6-156">Real-time technologies</span></span>

<span data-ttu-id="f26e6-157">ASP.NET SignalR は、リアルタイム web 機能の開発を容易にする ASP.NET 開発者向けの新しいライブラリです。</span><span class="sxs-lookup"><span data-stu-id="f26e6-157">ASP.NET SignalR is a new library for ASP.NET developers that makes developing real-time web functionality easier.</span></span> <span data-ttu-id="f26e6-158">SignalR を使用すると、サーバーとクライアント間で双方向通信を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-158">SignalR allows bi-directional communication between server and client.</span></span> <span data-ttu-id="f26e6-159">サーバーは、使用可能になったらすぐに、接続されているクライアントにコンテンツをプッシュできます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-159">Servers can push content to connected clients instantly as it becomes available.</span></span> <span data-ttu-id="f26e6-160">SignalR は Web ソケットをサポートしており、以前のブラウザーと互換性のある他の手法にフォールバックします。</span><span class="sxs-lookup"><span data-stu-id="f26e6-160">SignalR supports Web Sockets, and falls back to other compatible techniques for older browsers.</span></span> <span data-ttu-id="f26e6-161">SignalR には接続管理用の API が含まれています (接続し、切断イベントなど)、接続、および承認をグループ化します。</span><span class="sxs-lookup"><span data-stu-id="f26e6-161">SignalR includes APIs for connection management (for instance, connect and disconnect events), grouping connections, and authorization.</span></span>

[<span data-ttu-id="f26e6-162">SignalR についての詳細情報</span><span class="sxs-lookup"><span data-stu-id="f26e6-162">Learn more about SignalR</span></span>](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a><span data-ttu-id="f26e6-163">モバイルアプリとサイト</span><span class="sxs-lookup"><span data-stu-id="f26e6-163">Mobile apps and sites</span></span>

<span data-ttu-id="f26e6-164">ASP.NET では、Web API バックエンドを使用してネイティブモバイルアプリを作成できます。また、Twitter ブートストラップなどの応答性の高い設計フレームワークを使用してモバイル Web サイトを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-164">ASP.NET can power native mobile apps with a Web API back end, as well as mobile web sites using responsive design frameworks like Twitter Bootstrap.</span></span> <span data-ttu-id="f26e6-165">ネイティブモバイルアプリを構築している場合は、アプリのデータアクセス、認証、およびプッシュ通知を処理するための JSON ベースの Web API を簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-165">If you are building a native mobile app, it's easy to create a JSON-based Web API to handle data access, authentication, and push notifications for your app.</span></span> <span data-ttu-id="f26e6-166">応答性の高いモバイルサイトを構築する場合は、任意の CSS フレームワークを使用するか、好みのグリッドシステムを開くか、jQuery Mobile や Sencha などの強力なモバイルシステムと PhoneGap を使用した優れたモバイルアプリケーションを選択することができます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-166">If you are building a responsive mobile site, you can use any CSS framework or open grid system you prefer, or select a powerful mobile system like jQuery Mobile or Sencha and great mobile applications with PhoneGap.</span></span>

[<span data-ttu-id="f26e6-167">モバイルアプリとサイト開発の詳細情報</span><span class="sxs-lookup"><span data-stu-id="f26e6-167">Learn more about mobile app and site development</span></span>](mobile/overview.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a><span data-ttu-id="f26e6-168">シングルページ アプリケーション</span><span class="sxs-lookup"><span data-stu-id="f26e6-168">Single-page applications</span></span>

<span data-ttu-id="f26e6-169">ASP.NET Single Page Application (SPA) を使用すると、HTML 5、CSS 3、および JavaScript を使用したクライアント側の重要な相互作用を含むアプリケーションを構築できます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-169">ASP.NET Single Page Application (SPA) helps you build applications that include significant client-side interactions using HTML 5, CSS 3 and JavaScript.</span></span> <span data-ttu-id="f26e6-170">Visual Studio には、ノックアウトと ASP.NET Web API を使用してシングルページアプリケーションを構築するためのテンプレートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f26e6-170">Visual Studio includes a template for building single page applications using knockout.js and ASP.NET Web API.</span></span> <span data-ttu-id="f26e6-171">組み込みの SPA テンプレートに加えて、コミュニティによって作成された SPA テンプレートをダウンロードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-171">In addition to the built-in SPA template, community-created SPA templates are also available for download.</span></span>

[<span data-ttu-id="f26e6-172">シングルページアプリの開発についての詳細情報</span><span class="sxs-lookup"><span data-stu-id="f26e6-172">Learn more about single-page app development</span></span>](single-page-application/index.md)

## <a name="webhooks"></a><span data-ttu-id="f26e6-173">WebHook</span><span class="sxs-lookup"><span data-stu-id="f26e6-173">WebHooks</span></span>

<span data-ttu-id="f26e6-174">Webhook は、Web API と SaaS サービスをまとめて配線の単純なパブリッシュ/サブスクライブ モデルを提供する軽量な HTTP パターンです。</span><span class="sxs-lookup"><span data-stu-id="f26e6-174">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="f26e6-175">サービスでイベントが発生すると、登録されたサブスクライバーに対して HTTP POST 要求の形式で通知が送信されます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-175">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="f26e6-176">POST 要求には、イベントに関する情報が含まれています。これにより、受信側がそれに応じて動作できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f26e6-176">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="f26e6-177">Webhook は、Dropbox、GitHub、Instagram、MailChimp、PayPal、余裕、Trello など、多数のサービスによって公開されています。</span><span class="sxs-lookup"><span data-stu-id="f26e6-177">WebHooks are exposed by a large number of services including Dropbox, GitHub, Instagram, MailChimp, PayPal, Slack, Trello, and many more.</span></span> <span data-ttu-id="f26e6-178">たとえば、WebHook は、Dropbox でファイルが変更されたこと、またはコード変更が GitHub でコミットされたか、または PayPal で支払いが開始されたか、または Trello でカードが作成されたことを示すことができます。</span><span class="sxs-lookup"><span data-stu-id="f26e6-178">For example, a WebHook can indicate that a file has changed in Dropbox, or a code change has been committed in GitHub, or a payment has been initiated in PayPal, or a card has been created in Trello.</span></span>

[<span data-ttu-id="f26e6-179">Webhook に関する詳細情報</span><span class="sxs-lookup"><span data-stu-id="f26e6-179">Learn more about WebHooks</span></span>](webhooks/index.md)

<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->
