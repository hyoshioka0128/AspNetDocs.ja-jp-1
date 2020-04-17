---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: 異なるバージョンの IIS (C#) でのASP.NET MVC の使用 |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルでは、さまざまなバージョンのインターネット インフォメーション サービスで、mvc と URL ルーティングASP.NETを使用する方法について説明します。 あなたは異なる戦略を学びます.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: 8c239c3c7cbbaae5d9c5e4dd91dc66ff4e98bcfb
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542080"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a><span data-ttu-id="6f951-104">さまざまなバージョンの IIS と共に ASP.NET MVC を使用する (C#)</span><span class="sxs-lookup"><span data-stu-id="6f951-104">Using ASP.NET MVC with Different Versions of IIS (C#)</span></span>

<span data-ttu-id="6f951-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6f951-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6f951-106">このチュートリアルでは、さまざまなバージョンのインターネット インフォメーション サービスで、mvc と URL ルーティングASP.NETを使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="6f951-106">In this tutorial, you learn how to use ASP.NET MVC, and URL Routing, with different versions of Internet Information Services.</span></span> <span data-ttu-id="6f951-107">IIS 7.0 (クラシック モード)、IIS 6.0、および以前のバージョンの IIS で MVC ASP.NET使用するためのさまざまな戦略を学習します。</span><span class="sxs-lookup"><span data-stu-id="6f951-107">You learn different strategies for using ASP.NET MVC with IIS 7.0 (classic mode), IIS 6.0, and earlier versions of IIS.</span></span>

<span data-ttu-id="6f951-108">mvc フレームワークASP.NETは、ブラウザーの要求をコントローラー アクションにルーティングするASP.NETルーティングに依存します。</span><span class="sxs-lookup"><span data-stu-id="6f951-108">The ASP.NET MVC framework depends on ASP.NET Routing to route browser requests to controller actions.</span></span> <span data-ttu-id="6f951-109">ASP.NET ルーティングを利用するには、Web サーバーで追加の構成手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-109">In order to take advantage of ASP.NET Routing, you might have to perform additional configuration steps on your web server.</span></span> <span data-ttu-id="6f951-110">このすべては、インターネット インフォメーション サービス (IIS) のバージョンと、アプリケーションの要求処理モードによって異なります。</span><span class="sxs-lookup"><span data-stu-id="6f951-110">It all depends on the version of Internet Information Services (IIS) and the request processing mode for your application.</span></span>

<span data-ttu-id="6f951-111">さまざまなバージョンの IIS の概要を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6f951-111">Here's a summary of the different versions of IIS:</span></span>

- <span data-ttu-id="6f951-112">IIS 7.0 (統合モード) - ASP.NET ルーティングを使用するために特別な構成は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="6f951-112">IIS 7.0 (integrated mode) - No special configuration necessary to use ASP.NET Routing.</span></span>
- <span data-ttu-id="6f951-113">IIS 7.0 (クラシック モード) - ASP.NET ルーティングを使用するには、特別な構成を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-113">IIS 7.0 (classic mode) - You need to perform special configuration to use ASP.NET Routing.</span></span>
- <span data-ttu-id="6f951-114">IIS 6.0 以下 - ASP.NET ルーティングを使用するには、特別な構成を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-114">IIS 6.0 or below - You need to perform special configuration to use ASP.NET Routing.</span></span>

<span data-ttu-id="6f951-115">IIS の最新バージョンはバージョン 7.5 (Win7) です。</span><span class="sxs-lookup"><span data-stu-id="6f951-115">The latest version of IIS is version 7.5 (on Win7).</span></span> <span data-ttu-id="6f951-116">IIS の IIS 7 は、Windows Server 2008 と VISTA/SP1 以降に含まれています。</span><span class="sxs-lookup"><span data-stu-id="6f951-116">IIS 7 of IIS is included with Windows Server 2008 AND VISTA/SP1 and higher.</span></span> <span data-ttu-id="6f951-117">また、ホーム ベーシック (を参照) 以外の Vista オペレーティング システムの任意の[https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)バージョンに IIS 7.0 をインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="6f951-117">You also can install IIS 7.0 on any version of the Vista operating system except Home Basic (see [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).</span></span>

<span data-ttu-id="6f951-118">IIS 7.0 では、要求を処理するための 2 つのモードがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="6f951-118">IIS 7.0 supports two modes for processing requests.</span></span> <span data-ttu-id="6f951-119">統合モードまたはクラシック モードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6f951-119">You can use integrated mode or classic mode.</span></span> <span data-ttu-id="6f951-120">統合モードで IIS 7.0 を使用する場合は、特別な構成手順を実行する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6f951-120">You don't need to perform any special configuration steps when using IIS 7.0 in integrated mode.</span></span> <span data-ttu-id="6f951-121">ただし、クラシック モードで IIS 7.0 を使用する場合は、追加の構成を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-121">However, you do need to perform additional configuration when using IIS 7.0 in classic mode.</span></span>

<span data-ttu-id="6f951-122">Windows サーバー 2003 には、IIS 6.0 が含まれています。</span><span class="sxs-lookup"><span data-stu-id="6f951-122">Microsoft Windows Server 2003 includes IIS 6.0.</span></span> <span data-ttu-id="6f951-123">Windows Server 2003 オペレーティング システムを使用している場合、IIS 6.0 を IIS 7.0 にアップグレードすることはできません。</span><span class="sxs-lookup"><span data-stu-id="6f951-123">You cannot upgrade IIS 6.0 to IIS 7.0 when using the Windows Server 2003 operating system.</span></span> <span data-ttu-id="6f951-124">IIS 6.0 を使用する場合は、追加の構成手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-124">You must perform additional configuration steps when using IIS 6.0.</span></span>

<span data-ttu-id="6f951-125">Windows XP プロフェッショナルには、IIS 5.1 が含まれています。</span><span class="sxs-lookup"><span data-stu-id="6f951-125">Microsoft Windows XP Professional includes IIS 5.1.</span></span> <span data-ttu-id="6f951-126">IIS 5.1 を使用する場合は、追加の構成手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-126">You must perform additional configuration steps when using IIS 5.1.</span></span>

<span data-ttu-id="6f951-127">最後に、Windows 2000 およびマイクロソフトの Windows 2000 プロフェッショナルには、IIS 5.0 が含まれています。</span><span class="sxs-lookup"><span data-stu-id="6f951-127">Finally, Microsoft Windows 2000 and Microsoft Windows 2000 Professional includes IIS 5.0.</span></span> <span data-ttu-id="6f951-128">IIS 5.0 を使用する場合は、追加の構成手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-128">You must perform additional configuration steps when using IIS 5.0.</span></span>

## <a name="integrated-versus-classic-mode"></a><span data-ttu-id="6f951-129">統合モードとクラシックモード</span><span class="sxs-lookup"><span data-stu-id="6f951-129">Integrated versus Classic Mode</span></span>

<span data-ttu-id="6f951-130">IIS 7.0 では、統合とクラシックの 2 つの異なる要求処理モードを使用して要求を処理できます。</span><span class="sxs-lookup"><span data-stu-id="6f951-130">IIS 7.0 can process requests using two different request processing modes: integrated and classic.</span></span> <span data-ttu-id="6f951-131">統合モードは、より良いパフォーマンスとより多くの機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="6f951-131">Integrated mode provides better performance and more features.</span></span> <span data-ttu-id="6f951-132">クラシック モードは、以前のバージョンの IIS との下位互換性を保つために用意されています。</span><span class="sxs-lookup"><span data-stu-id="6f951-132">Classic mode is included for backwards compatibility with earlier versions of IIS.</span></span>

<span data-ttu-id="6f951-133">要求処理モードは、アプリケーション プールによって決定されます。</span><span class="sxs-lookup"><span data-stu-id="6f951-133">The request processing mode is determined by the application pool.</span></span> <span data-ttu-id="6f951-134">アプリケーションに関連付けられているアプリケーション プールを決定することにより、特定の Web アプリケーションで使用されている処理モードを特定できます。</span><span class="sxs-lookup"><span data-stu-id="6f951-134">You can determine which processing mode is being used by a particular web application by determining the application pool associated with the application.</span></span> <span data-ttu-id="6f951-135">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="6f951-135">Follow these steps:</span></span>

1. <span data-ttu-id="6f951-136">インターネット インフォメーション サービス マネージャを起動する</span><span class="sxs-lookup"><span data-stu-id="6f951-136">Launch the Internet Information Services Manager</span></span>
2. <span data-ttu-id="6f951-137">[接続] ウィンドウで、アプリケーションを選択します。</span><span class="sxs-lookup"><span data-stu-id="6f951-137">In the Connections window, select an application</span></span>
3. <span data-ttu-id="6f951-138">[操作] ウィンドウで、[**基本設定]** リンクをクリックして [アプリケーションの編集] ダイアログ ボックスを開きます (図 1 を参照)。</span><span class="sxs-lookup"><span data-stu-id="6f951-138">In the Actions window, click the **Basic Settings** link to open the Edit Application dialog box (see Figure 1)</span></span>
4. <span data-ttu-id="6f951-139">選択したアプリケーション プールをメモします。</span><span class="sxs-lookup"><span data-stu-id="6f951-139">Take note of the Application pool selected.</span></span>

<span data-ttu-id="6f951-140">既定では、IIS は、2 つのアプリケーション プールをサポートするように構成されています:**既定のアプリケーション プール**と**従来の .NET アプリケーション プール**。</span><span class="sxs-lookup"><span data-stu-id="6f951-140">By default, IIS is configured to support two application pools: **DefaultAppPool** and **Classic .NET AppPool**.</span></span> <span data-ttu-id="6f951-141">DefaultAppPool が選択されている場合、アプリケーションは統合要求処理モードで実行されています。</span><span class="sxs-lookup"><span data-stu-id="6f951-141">If DefaultAppPool is selected, then your application is running in integrated request processing mode.</span></span> <span data-ttu-id="6f951-142">[従来の .NET アプリケーション プール] が選択されている場合、アプリケーションはクラシック要求処理モードで実行されています。</span><span class="sxs-lookup"><span data-stu-id="6f951-142">If Classic .NET AppPool is selected, your application is running in classic request processing mode.</span></span>

<span data-ttu-id="6f951-143">[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6f951-143">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)</span></span>

<span data-ttu-id="6f951-144">**図1**: リクエスト処理モードを検出する([フルサイズの画像を表示する をクリック](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="6f951-144">**Figure 1**: Detecting the request processing mode([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))</span></span>

<span data-ttu-id="6f951-145">[アプリケーションの編集] ダイアログ ボックスで要求処理モードを変更できることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6f951-145">Notice that you can modify the request processing mode within the Edit Application dialog box.</span></span> <span data-ttu-id="6f951-146">[選択] ボタンをクリックし、アプリケーションに関連付けられているアプリケーション プールを変更します。</span><span class="sxs-lookup"><span data-stu-id="6f951-146">Click the Select button and change the application pool associated with the application.</span></span> <span data-ttu-id="6f951-147">ASP.NETアプリケーションをクラシックモードから統合モードに変更する場合は、互換性の問題があることを認識してください。</span><span class="sxs-lookup"><span data-stu-id="6f951-147">Realize that there are compatibility issues when changing an ASP.NET application from classic to integrated mode.</span></span> <span data-ttu-id="6f951-148">詳細については、次の記事を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6f951-148">For more information, see the following articles:</span></span>

- <span data-ttu-id="6f951-149">Windows Vista および Windows Server 2008 で ASP.NET 1.1 を IIS 7.0 にアップグレードする --[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span><span class="sxs-lookup"><span data-stu-id="6f951-149">Upgrading ASP.NET 1.1 to IIS 7.0 on Windows Vista and Windows Server 2008 -- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span></span>
- <span data-ttu-id="6f951-150">ASP.NET IIS 7.0 との統合 -[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span><span class="sxs-lookup"><span data-stu-id="6f951-150">ASP.NET Integration With IIS 7.0 - [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span></span>

<span data-ttu-id="6f951-151">ASP.NETアプリケーションが DefaultAppPool を使用している場合は、ASP.NET ルーティング (ASP.NET したがって MVC) を動作させるために追加の手順を実行する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6f951-151">If an ASP.NET application is using the DefaultAppPool, then you don't need to perform any additional steps to get ASP.NET Routing (and therefore ASP.NET MVC) to work.</span></span> <span data-ttu-id="6f951-152">ただし、ASP.NET アプリケーションが従来の .NET AppPool を使用するように構成されている場合は、読み取り続ける必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-152">However, if the ASP.NET application is configured to use the Classic .NET AppPool then keep reading, you have more work to do.</span></span>

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a><span data-ttu-id="6f951-153">旧バージョンの IIS で ASP.NET MVC を使用する</span><span class="sxs-lookup"><span data-stu-id="6f951-153">Using ASP.NET MVC with Older Versions of IIS</span></span>

<span data-ttu-id="6f951-154">IIS 7.0 より古いバージョンの IIS で MVC ASP.NET使用する必要がある場合、またはクラシック モードで IIS 7.0 を使用する必要がある場合は、2 つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="6f951-154">If you need to use ASP.NET MVC with an older version of IIS than IIS 7.0, or you need to use IIS 7.0 in classic mode, then you have two options.</span></span> <span data-ttu-id="6f951-155">まず、ファイル拡張子を使用するようにルート テーブルを変更できます。</span><span class="sxs-lookup"><span data-stu-id="6f951-155">First, you can modify the route table to use file extensions.</span></span> <span data-ttu-id="6f951-156">たとえば、/Store/Details などの URL を要求する代わりに、/Store.aspx/Details などの URL を要求します。</span><span class="sxs-lookup"><span data-stu-id="6f951-156">For example, instead of requesting a URL like /Store/Details, you would request a URL like /Store.aspx/Details.</span></span>

<span data-ttu-id="6f951-157">2 つ目のオプションは、*ワイルドカード スクリプト マップ*と呼ばれるものを作成することです。</span><span class="sxs-lookup"><span data-stu-id="6f951-157">The second option is to create something called a *wildcard script map*.</span></span> <span data-ttu-id="6f951-158">ワイルドカード スクリプト マップを使用すると、すべての要求をASP.NET フレームワークにマップできます。</span><span class="sxs-lookup"><span data-stu-id="6f951-158">A wildcard script map enables you to map every request into the ASP.NET framework.</span></span>

<span data-ttu-id="6f951-159">Web サーバーにアクセスできない場合 (たとえば、ASP.NET MVC アプリケーションがインターネット サービス プロバイダーによってホストされている場合) は、最初のオプションを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-159">If you don't have access to your web server (for example, your ASP.NET MVC application is being hosted by an Internet Service Provider) then you'll need to use the first option.</span></span> <span data-ttu-id="6f951-160">URL の外観を変更する必要がない場合、Web サーバーへのアクセス権がある場合は、2 番目のオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6f951-160">If you don't want to modify the appearance of your URLs, and you have access to your web server, then you can use the second option.</span></span>

<span data-ttu-id="6f951-161">各オプションについては、以下のセクションで詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="6f951-161">We explore each option in detail in the following sections.</span></span>

## <a name="adding-extensions-to-the-route-table"></a><span data-ttu-id="6f951-162">ルート テーブルへの拡張機能の追加</span><span class="sxs-lookup"><span data-stu-id="6f951-162">Adding Extensions to the Route Table</span></span>

<span data-ttu-id="6f951-163">以前のバージョンの IIS でASP.NETルーティングを使用する最も簡単な方法は、Global.asax ファイル内のルート テーブルを変更することです。</span><span class="sxs-lookup"><span data-stu-id="6f951-163">The easiest way to get ASP.NET Routing to work with older versions of IIS is to modify your route table in the Global.asax file.</span></span> <span data-ttu-id="6f951-164">リスト 1 のデフォルトおよび変更されていない Global.asax ファイルは、デフォルト ルートという名前のルートを 1 つ設定します。</span><span class="sxs-lookup"><span data-stu-id="6f951-164">The default and unmodified Global.asax file in Listing 1 configures one route named the Default route.</span></span>

<span data-ttu-id="6f951-165">**リスト 1 - グローバル.asax (未変更)**</span><span class="sxs-lookup"><span data-stu-id="6f951-165">**Listing 1 - Global.asax (unmodified)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

<span data-ttu-id="6f951-166">リスト 1 で構成された既定のルートでは、次のような URL をルーティングできます。</span><span class="sxs-lookup"><span data-stu-id="6f951-166">The Default route configured in Listing 1 enables you to route URLs that look like this:</span></span>

<span data-ttu-id="6f951-167">/ホーム/インデックス</span><span class="sxs-lookup"><span data-stu-id="6f951-167">/Home/Index</span></span>

<span data-ttu-id="6f951-168">/製品/詳細/3</span><span class="sxs-lookup"><span data-stu-id="6f951-168">/Product/Details/3</span></span>

<span data-ttu-id="6f951-169">/Product</span><span class="sxs-lookup"><span data-stu-id="6f951-169">/Product</span></span>

<span data-ttu-id="6f951-170">残念ながら、古いバージョンの IIS では、これらの要求はASP.NET フレームワークに渡されません。</span><span class="sxs-lookup"><span data-stu-id="6f951-170">Unfortunately, older versions of IIS won't pass these requests to the ASP.NET framework.</span></span> <span data-ttu-id="6f951-171">したがって、これらの要求はコントローラーにルーティングされません。</span><span class="sxs-lookup"><span data-stu-id="6f951-171">Therefore, these requests won't get routed to a controller.</span></span> <span data-ttu-id="6f951-172">たとえば、URL /Home/Index のブラウザ要求を行うと、図 2 のエラー ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6f951-172">For example, if you make a browser request for the URL /Home/Index then you'll get the error page in Figure 2.</span></span>

<span data-ttu-id="6f951-173">[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="6f951-173">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)</span></span>

<span data-ttu-id="6f951-174">**図2**: 404 Not Found エラーが表示される ([フルサイズの画像を表示する をクリック](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="6f951-174">**Figure 2**: Receiving a 404 Not Found error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))</span></span>

<span data-ttu-id="6f951-175">古いバージョンの IIS では、特定の要求がASP.NET フレームワークにしかマップされません。</span><span class="sxs-lookup"><span data-stu-id="6f951-175">Older versions of IIS only map certain requests to the ASP.NET framework.</span></span> <span data-ttu-id="6f951-176">要求は、正しいファイル拡張子を持つ URL に対する要求である必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-176">The request must be for a URL with the right file extension.</span></span> <span data-ttu-id="6f951-177">たとえば、/SomePage.aspx の要求は、ASP.NET フレームワークにマップされます。</span><span class="sxs-lookup"><span data-stu-id="6f951-177">For example, a request for /SomePage.aspx gets mapped to the ASP.NET framework.</span></span> <span data-ttu-id="6f951-178">ただし、/SomePage.htm の要求は行われません。</span><span class="sxs-lookup"><span data-stu-id="6f951-178">However, a request for /SomePage.htm does not.</span></span>

<span data-ttu-id="6f951-179">したがって、ルーティングASP.NETを動作させるには、ASP.NETフレームワークにマップされたファイル拡張子が含まれるようにデフォルトルートを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-179">Therefore, to get ASP.NET Routing to work, we must modify the Default route so that it includes a file extension that is mapped to the ASP.NET framework.</span></span>

<span data-ttu-id="6f951-180">これは、 という名前`registermvc.wsf`のスクリプトを使用して行います。</span><span class="sxs-lookup"><span data-stu-id="6f951-180">This is done using a script named `registermvc.wsf`.</span></span> <span data-ttu-id="6f951-181">MVC 1 のリリース ASP.NET に`C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`含まれていましたが、ASP.NET 2 以降、このスクリプトは ASP.NET 先物に移動[http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)されました。</span><span class="sxs-lookup"><span data-stu-id="6f951-181">It was included with the ASP.NET MVC 1 release in `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, but as of ASP.NET 2 this script has been moved to the ASP.NET Futures, available at [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978).</span></span>

<span data-ttu-id="6f951-182">このスクリプトを実行すると、新しい .mvc 拡張機能が IIS に登録されます。</span><span class="sxs-lookup"><span data-stu-id="6f951-182">Executing this script registers a new .mvc extension with IIS.</span></span> <span data-ttu-id="6f951-183">mvc 拡張機能を登録した後、ルートが .mvc 拡張子を使用するように Global.asax ファイル内のルートを変更できます。</span><span class="sxs-lookup"><span data-stu-id="6f951-183">After you register the .mvc extension, you can modify your routes in the Global.asax file so that the routes use the .mvc extension.</span></span>

<span data-ttu-id="6f951-184">リスト 2 で変更された Global.asax ファイルは、古いバージョンの IIS で動作します。</span><span class="sxs-lookup"><span data-stu-id="6f951-184">The modified Global.asax file in Listing 2 works with older versions of IIS.</span></span>

<span data-ttu-id="6f951-185">**リスト 2 - グローバル.asax (拡張機能で変更)**</span><span class="sxs-lookup"><span data-stu-id="6f951-185">**Listing 2 - Global.asax (modified with extensions)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

<span data-ttu-id="6f951-186">**重要**: Global.asax ファイルを変更した後に、ASP.NET MVC アプリケーションを再度ビルドすることを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="6f951-186">**Important**: remember to build your ASP.NET MVC Application again after changing the Global.asax file.</span></span>

<span data-ttu-id="6f951-187">リスト 2 の Global.asax ファイルには、2 つの重要な変更があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-187">There are two important changes to the Global.asax file in Listing 2.</span></span> <span data-ttu-id="6f951-188">Global.asax で定義されたルートが 2 つあります。</span><span class="sxs-lookup"><span data-stu-id="6f951-188">There are now two routes defined in the Global.asax.</span></span> <span data-ttu-id="6f951-189">既定のルートの URL パターン(最初のルート)は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="6f951-189">The URL pattern for the Default route, the first route, now looks like:</span></span>

<span data-ttu-id="6f951-190">{コントローラー}.mvc/{アクション}/{id}</span><span class="sxs-lookup"><span data-stu-id="6f951-190">{controller}.mvc/{action}/{id}</span></span>

<span data-ttu-id="6f951-191">mvc 拡張機能を追加すると、ASP.NETルーティング モジュールがインターセプトするファイルの種類が変更されます。</span><span class="sxs-lookup"><span data-stu-id="6f951-191">The addition of the .mvc extension changes the type of files that the ASP.NET Routing module intercepts.</span></span> <span data-ttu-id="6f951-192">この変更により、ASP.NET MVC アプリケーションは、次のような要求をルーティングするようになりました。</span><span class="sxs-lookup"><span data-stu-id="6f951-192">With this change, the ASP.NET MVC application now routes requests like the following:</span></span>

<span data-ttu-id="6f951-193">/ホーム.mvc/インデックス/</span><span class="sxs-lookup"><span data-stu-id="6f951-193">/Home.mvc/Index/</span></span>

<span data-ttu-id="6f951-194">/製品.mvc/詳細/3</span><span class="sxs-lookup"><span data-stu-id="6f951-194">/Product.mvc/Details/3</span></span>

<span data-ttu-id="6f951-195">/製品.mvc/</span><span class="sxs-lookup"><span data-stu-id="6f951-195">/Product.mvc/</span></span>

<span data-ttu-id="6f951-196">2 番目のルートルートは新しいルートです。</span><span class="sxs-lookup"><span data-stu-id="6f951-196">The second route, the Root route, is new.</span></span> <span data-ttu-id="6f951-197">ルート ルートのこの URL パターンは空の文字列です。</span><span class="sxs-lookup"><span data-stu-id="6f951-197">This URL pattern for the Root route is an empty string.</span></span> <span data-ttu-id="6f951-198">このルートは、アプリケーションのルートに対して行われた要求を照合するために必要です。</span><span class="sxs-lookup"><span data-stu-id="6f951-198">This route is necessary for matching requests made against the root of your application.</span></span> <span data-ttu-id="6f951-199">たとえば、ルート ルートは次のような要求と一致します。</span><span class="sxs-lookup"><span data-stu-id="6f951-199">For example, the Root route will match a request that looks like this:</span></span>

[http://www.YourApplication.com/](http://www.YourApplication.com/)

<span data-ttu-id="6f951-200">ルート テーブルにこれらの変更を加えた後、アプリケーション内のすべてのリンクがこれらの新しい URL パターンと互換性があることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-200">After making these modifications to your route table, you'll need to make sure that all of the links in your application are compatible with these new URL patterns.</span></span> <span data-ttu-id="6f951-201">つまり、すべてのリンクに .mvc 拡張子が含まれているか確認してください。</span><span class="sxs-lookup"><span data-stu-id="6f951-201">In other words, make sure that all of your links include the .mvc extension.</span></span> <span data-ttu-id="6f951-202">Html.ActionLink() ヘルパー メソッドを使用してリンクを生成する場合は、変更を加える必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6f951-202">If you use the Html.ActionLink() helper method to generate your links, then you should not need to make any changes.</span></span>

<span data-ttu-id="6f951-203">registermvc.wcf スクリプトを使用する代わりに、手作業でASP.NET フレームワークにマップされている IIS に新しい拡張機能を追加できます。</span><span class="sxs-lookup"><span data-stu-id="6f951-203">Instead of using the registermvc.wcf script, you can add a new extension to IIS that is mapped to the ASP.NET framework by hand.</span></span> <span data-ttu-id="6f951-204">新しい拡張子を自分で追加する場合は、[**ファイルが存在することを確認**する] チェック ボックスがオンになっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="6f951-204">When adding a new extension yourself, make sure that the checkbox labeled **Verify that file exists** is not checked.</span></span>

## <a name="hosted-server"></a><span data-ttu-id="6f951-205">ホストされるサーバー</span><span class="sxs-lookup"><span data-stu-id="6f951-205">Hosted Server</span></span>

<span data-ttu-id="6f951-206">Web サーバーにアクセスできる必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6f951-206">You don't always have access to your web server.</span></span> <span data-ttu-id="6f951-207">たとえば、インターネット ホスティング プロバイダーを使用して ASP.NET MVC アプリケーションをホストしている場合、必ずしも IIS にアクセスできるわけではありません。</span><span class="sxs-lookup"><span data-stu-id="6f951-207">For example, if you are hosting your ASP.NET MVC application using an Internet Hosting Provider, then you won't necessarily have access to IIS.</span></span>

<span data-ttu-id="6f951-208">その場合は、ASP.NETフレームワークにマップされている既存のファイル拡張子のいずれかを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-208">In that case, you should use one of the existing file extensions that are mapped to the ASP.NET framework.</span></span> <span data-ttu-id="6f951-209">ASP.NETにマップされたファイル拡張子の例には、.aspx、.axd、および .ashx 拡張子が含まれます。</span><span class="sxs-lookup"><span data-stu-id="6f951-209">Examples of file extensions mapped to ASP.NET include the .aspx, .axd, and .ashx extensions.</span></span>

<span data-ttu-id="6f951-210">たとえば、リスト 3 で変更された Global.asax ファイルでは、.mvc 拡張子ではなく .aspx 拡張子が使用されます。</span><span class="sxs-lookup"><span data-stu-id="6f951-210">For example, the modified Global.asax file in Listing 3 uses the .aspx extension instead of the .mvc extension.</span></span>

<span data-ttu-id="6f951-211">**リスト 3 - Global.asax (.aspx 拡張子で変更)**</span><span class="sxs-lookup"><span data-stu-id="6f951-211">**Listing 3 - Global.asax (modified with .aspx extensions)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

<span data-ttu-id="6f951-212">リスト 3 の Global.asax ファイルは、.mvc 拡張子の代わりに .aspx 拡張子を使用する点を除いて、以前の Global.asax ファイルとまったく同じです。</span><span class="sxs-lookup"><span data-stu-id="6f951-212">The Global.asax file in Listing 3 is exactly the same as the previous Global.asax file except for the fact that it uses the .aspx extension instead of the .mvc extension.</span></span> <span data-ttu-id="6f951-213">.aspx 拡張機能を使用するために、リモート Web サーバーでセットアップを実行する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="6f951-213">You don't have to perform any setup on your remote web server to use the .aspx extension.</span></span>

## <a name="creating-a-wildcard-script-map"></a><span data-ttu-id="6f951-214">ワイルドカード スクリプト マップの作成</span><span class="sxs-lookup"><span data-stu-id="6f951-214">Creating a Wildcard Script Map</span></span>

<span data-ttu-id="6f951-215">ASP.NET MVC アプリケーションの URL を変更する必要がない場合、Web サーバーにアクセスできる場合は、追加のオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="6f951-215">If you don't want to modify the URLs for your ASP.NET MVC application, and you have access to your web server, then you have an additional option.</span></span> <span data-ttu-id="6f951-216">すべての要求を web サーバーにマップするワイルドカード スクリプト マップを作成ASP.NETフレームワーク。</span><span class="sxs-lookup"><span data-stu-id="6f951-216">You can create a wildcard script map that maps all requests to the web server to the ASP.NET framework.</span></span> <span data-ttu-id="6f951-217">このようにすると、既定の ASP.NET MVC ルート テーブルを IIS 7.0 (クラシック モード) または IIS 6.0 で使用できます。</span><span class="sxs-lookup"><span data-stu-id="6f951-217">That way, you can use the default ASP.NET MVC route table with IIS 7.0 (in classic mode) or IIS 6.0.</span></span>

<span data-ttu-id="6f951-218">このオプションを使用すると、IIS は Web サーバーに対して行われた要求をすべてインターセプトすることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6f951-218">Be aware that this option causes IIS to intercept every request made against the web server.</span></span> <span data-ttu-id="6f951-219">これには、イメージ、従来の ASP ページ、および HTML ページの要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="6f951-219">This includes requests for images, classic ASP pages, and HTML pages.</span></span> <span data-ttu-id="6f951-220">したがって、ワイルドカード スクリプト マップを有効にしてASP.NETすると、パフォーマンスに影響が生じます。</span><span class="sxs-lookup"><span data-stu-id="6f951-220">Therefore, enabling a wildcard script map to ASP.NET does have performance implications.</span></span>

<span data-ttu-id="6f951-221">IIS 7.0 のワイルドカード スクリプト マップを有効にする方法を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6f951-221">Here's how you enable a wildcard script map for IIS 7.0:</span></span>

1. <span data-ttu-id="6f951-222">[接続] ウィンドウでアプリケーションを選択します。</span><span class="sxs-lookup"><span data-stu-id="6f951-222">Select your application in the Connections window</span></span>
2. <span data-ttu-id="6f951-223">**[機能]** ビューが選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="6f951-223">Make sure that the **Features** view is selected</span></span>
3. <span data-ttu-id="6f951-224">[**ハンドラー マッピング**] ボタンをダブルクリックします。</span><span class="sxs-lookup"><span data-stu-id="6f951-224">Double-click the **Handler Mappings** button</span></span>
4. <span data-ttu-id="6f951-225">[**ワイルドカード スクリプト マップの追加**] リンクをクリックします (図 3 を参照)。</span><span class="sxs-lookup"><span data-stu-id="6f951-225">Click the **Add Wildcard Script Map** link (see Figure 3)</span></span>
5. <span data-ttu-id="6f951-226">aspnet\_isapi.dll ファイルへのパスを入力します (このパスは PageHandlerFactory スクリプト マップからコピーできます)</span><span class="sxs-lookup"><span data-stu-id="6f951-226">Enter the path to the aspnet\_isapi.dll file (You can copy this path from the PageHandlerFactory script map)</span></span>
6. <span data-ttu-id="6f951-227">名前 MVC を入力してください</span><span class="sxs-lookup"><span data-stu-id="6f951-227">Enter the name MVC</span></span>
7. <span data-ttu-id="6f951-228">**[OK]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6f951-228">Click the **OK** button</span></span>

<span data-ttu-id="6f951-229">[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="6f951-229">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)</span></span>

<span data-ttu-id="6f951-230">**図 3**: IIS 7.0 を使用したワイルドカード スクリプト マップの作成 ([フルサイズの画像を表示する をクリック](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="6f951-230">**Figure 3**: Creating a wildcard script map with IIS 7.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))</span></span>

<span data-ttu-id="6f951-231">IIS 6.0 でワイルドカード スクリプト マップを作成するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="6f951-231">Follow these steps to create a wildcard script map with IIS 6.0:</span></span>

1. <span data-ttu-id="6f951-232">Web サイトを右クリックし、[プロパティ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="6f951-232">Right-click a website and select Properties</span></span>
2. <span data-ttu-id="6f951-233">**[ホーム ディレクトリ**] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="6f951-233">Select the **Home Directory** tab</span></span>
3. <span data-ttu-id="6f951-234">[**構成]** ボタン</span><span class="sxs-lookup"><span data-stu-id="6f951-234">Click the **Configuration** button</span></span>
4. <span data-ttu-id="6f951-235">[マッピング] タブ**を選択します。**</span><span class="sxs-lookup"><span data-stu-id="6f951-235">Select the **Mappings** tab</span></span>
5. <span data-ttu-id="6f951-236">[**挿入**] ボタンをクリックします (図 4 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="6f951-236">Click the **Insert** button (see Figure 4)</span></span>
6. <span data-ttu-id="6f951-237">aspnet\_isapi.dll へのパスを実行可能ファイルのフィールドに貼り付けます (.aspx ファイルのスクリプト マップからこのパスをコピーできます)。</span><span class="sxs-lookup"><span data-stu-id="6f951-237">Paste the path to the aspnet\_isapi.dll into the Executable field (you can copy this path from the script map for .aspx files)</span></span>
7. <span data-ttu-id="6f951-238">[**ファイルが存在することを確認する**] チェック ボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="6f951-238">Uncheck the checkbox labeled **Verify that file exists**</span></span>
8. <span data-ttu-id="6f951-239">**[OK]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6f951-239">Click the **OK** button</span></span>

<span data-ttu-id="6f951-240">[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="6f951-240">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)</span></span>

<span data-ttu-id="6f951-241">**図 4**: IIS 6.0 でワイルドカード スクリプト マップを作成する ([フルサイズの画像を表示する をクリック](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="6f951-241">**Figure 4**: Creating a wildcard script map with IIS 6.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))</span></span>

<span data-ttu-id="6f951-242">ワイルドカード スクリプト マップを有効にした後、Global.asax ファイル内のルート テーブルを変更してルート ルートを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-242">After you enable wildcard script maps, you need to modify the route table in the Global.asax file so that it includes a Root route.</span></span> <span data-ttu-id="6f951-243">それ以外の場合は、アプリケーションのルート ページを要求するときに、図 5 のエラー ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6f951-243">Otherwise, you'll get the error page in Figure 5 when you make a request for the root page of your application.</span></span> <span data-ttu-id="6f951-244">修正された Global.asax ファイルは、リスト 4 で使用できます。</span><span class="sxs-lookup"><span data-stu-id="6f951-244">You can use the modified Global.asax file in Listing 4.</span></span>

<span data-ttu-id="6f951-245">[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="6f951-245">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)</span></span>

<span data-ttu-id="6f951-246">**図5**:ルートルートの欠落エラー([フルサイズの画像を表示するをクリック](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="6f951-246">**Figure 5**: Missing Root route error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))</span></span>

<span data-ttu-id="6f951-247">**リスト 4 - グローバル.asax (ルートルートで変更)**</span><span class="sxs-lookup"><span data-stu-id="6f951-247">**Listing 4 - Global.asax (modified with Root route)**</span></span>

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

<span data-ttu-id="6f951-248">IIS 7.0 または IIS 6.0 のワイルドカード スクリプト マップを有効にすると、次のような既定のルート テーブルで動作する要求を作成できます。</span><span class="sxs-lookup"><span data-stu-id="6f951-248">After you enable a wildcard script map for either IIS 7.0 or IIS 6.0, you can make requests that work with the default route table that look like this:</span></span>

/

<span data-ttu-id="6f951-249">/ホーム/インデックス</span><span class="sxs-lookup"><span data-stu-id="6f951-249">/Home/Index</span></span>

<span data-ttu-id="6f951-250">/製品/詳細/3</span><span class="sxs-lookup"><span data-stu-id="6f951-250">/Product/Details/3</span></span>

<span data-ttu-id="6f951-251">/Product</span><span class="sxs-lookup"><span data-stu-id="6f951-251">/Product</span></span>

## <a name="summary"></a><span data-ttu-id="6f951-252">まとめ</span><span class="sxs-lookup"><span data-stu-id="6f951-252">Summary</span></span>

<span data-ttu-id="6f951-253">このチュートリアルの目的は、旧バージョンの IIS (またはクラシック モードで IIS 7.0) を使用するときに、mvc ASP.NET使用する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="6f951-253">The goal of this tutorial was to explain how you can use ASP.NET MVC when using an older version of IIS (or IIS 7.0 in classic mode).</span></span> <span data-ttu-id="6f951-254">以前のバージョンの IIS で作業する ASP.NET ルーティングを取得する 2 つの方法について説明しました: 既定のルート テーブルを変更する、またはワイルドカード スクリプト マップを作成します。</span><span class="sxs-lookup"><span data-stu-id="6f951-254">We discussed two methods of getting ASP.NET Routing to work with older versions of IIS: Modify the default route table or create a wildcard script map.</span></span>

<span data-ttu-id="6f951-255">最初のオプションでは、ASP.NET MVC アプリケーションで使用される URL を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f951-255">The first option requires you to modify the URLs used in your ASP.NET MVC application.</span></span> <span data-ttu-id="6f951-256">この最初のオプションの非常に大きな利点の 1 つは、ルート テーブルを変更するために Web サーバーにアクセスする必要がなされないことです。</span><span class="sxs-lookup"><span data-stu-id="6f951-256">One very significant advantage of this first option is that you do not need access to a web server in order to modify the route table.</span></span> <span data-ttu-id="6f951-257">つまり、インターネット ホスティング会社と ASP.NET MVC アプリケーションをホストしている場合でも、この最初のオプションを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6f951-257">That means that you can use this first option even when hosting your ASP.NET MVC application with an Internet hosting company.</span></span>

<span data-ttu-id="6f951-258">2 番目のオプションは、ワイルドカード スクリプト マップを作成することです。</span><span class="sxs-lookup"><span data-stu-id="6f951-258">The second option is to create a wildcard script map.</span></span> <span data-ttu-id="6f951-259">この 2 番目のオプションの利点は、URL を変更する必要がなされないことです。</span><span class="sxs-lookup"><span data-stu-id="6f951-259">The advantage of this second option is that you do not need to modify your URLs.</span></span> <span data-ttu-id="6f951-260">この 2 番目のオプションの欠点は、ASP.NET MVC アプリケーションのパフォーマンスに影響を与える可能性がある点です。</span><span class="sxs-lookup"><span data-stu-id="6f951-260">The disadvantage of this second option is that it can impact the performance of your ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6f951-261">次へ</span><span class="sxs-lookup"><span data-stu-id="6f951-261">Next</span></span>](using-asp-net-mvc-with-different-versions-of-iis-vb.md)
