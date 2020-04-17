---
uid: ajax/cdn/overview
title: マイクロソフト Ajax コンテンツ配信ネットワーク |マイクロソフトドキュメント
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 8e7efa2f321976671be321c760e2b478fe6e9e99
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540208"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="b75af-102">Microsoft Ajax Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="b75af-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="b75af-103">プロダクションアプリケーションは、CDN資産に対して厳しい依存を受けるべきではありません。</span><span class="sxs-lookup"><span data-stu-id="b75af-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="b75af-104">アプリケーションは、参照される CDN 資産をテストし、CDN が使用できない場合はフォールバック資産を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b75af-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="b75af-105">マイクロソフト Ajax CDN には、Azure CDN を使用する SLA を超える SLA はありません。</span><span class="sxs-lookup"><span data-stu-id="b75af-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="b75af-106">[この GitHub の問題](https://github.com/dotnet/AspNetDocs/issues/116)を使用して、マイクロソフト Ajax CDN に関する問題を報告します。</span><span class="sxs-lookup"><span data-stu-id="b75af-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="b75af-107">目次</span><span class="sxs-lookup"><span data-stu-id="b75af-107">Table of Contents</span></span>

<span data-ttu-id="b75af-108">**[ajax.microsoft.com名前を変更してajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="b75af-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="b75af-109">**[ビジュアル スタジオ .vsdoc サポート](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="b75af-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="b75af-110">**[CDN からのASP.NETアヤックスの使用](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="b75af-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="b75af-111">**[CDN からの jQuery の使用](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="b75af-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="b75af-112">**[CDN からの jQuery UI の使用](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="b75af-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="b75af-113">**[CDN 上のサード パーティ製ファイル](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="b75af-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="b75af-114">CDN にリリースされる jQuery</span><span class="sxs-lookup"><span data-stu-id="b75af-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="b75af-115">CDN でリリースを移行する jQuery</span><span class="sxs-lookup"><span data-stu-id="b75af-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="b75af-116">CDN での jQuery UI リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="b75af-117">CDN の jQuery 検証リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="b75af-118">CDN のモバイルリリース</span><span class="sxs-lookup"><span data-stu-id="b75af-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="b75af-119">CDN でリリースされる jQuery テンプレート</span><span class="sxs-lookup"><span data-stu-id="b75af-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="b75af-120">CDN の jQuery サイクルリリース</span><span class="sxs-lookup"><span data-stu-id="b75af-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="b75af-121">CDN でリリースされるデータテーブル</span><span class="sxs-lookup"><span data-stu-id="b75af-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="b75af-122">CDN のモダニズム リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="b75af-123">CDN に関する JS ヒント リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="b75af-124">CDN のノックアウト リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="b75af-125">CDN のリリースのグローバル化</span><span class="sxs-lookup"><span data-stu-id="b75af-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="b75af-126">CDN のリリースに応答する</span><span class="sxs-lookup"><span data-stu-id="b75af-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="b75af-127">CDN のブートストラップ リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="b75af-128">CDN のブートストラップ タッチカルーセル リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="b75af-129">CDN の Hammer.js リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="b75af-130">CDN で Web フォームと Ajax リリースをASP.NETする</span><span class="sxs-lookup"><span data-stu-id="b75af-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="b75af-131">CDN のASP.NET MVC リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="b75af-132">CDN でのASP.NETシグナル・リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="b75af-133">マイクロソフト Ajax コンテンツ配信ネットワーク (CDN) は、jQuery などの一般的なサードパーティ製の JavaScript ライブラリをホストし、Web アプリケーションに簡単に追加できるようにします。</span><span class="sxs-lookup"><span data-stu-id="b75af-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="b75af-134">たとえば、この CDN でホストされている jQuery を使用するには、ajax.aspnetcdn.comを指&lt;す&gt;スクリプト タグをページに追加するだけです。</span><span class="sxs-lookup"><span data-stu-id="b75af-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="b75af-135">CDN を利用することで、Ajax アプリケーションのパフォーマンスを大幅に向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="b75af-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="b75af-136">CDN の内容は、世界中のサーバーにキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="b75af-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="b75af-137">さらに、CDN を使用すると、異なるドメインにある Web サイトに対して、キャッシュされたサードパーティ製の JavaScript ファイルを再利用できます。</span><span class="sxs-lookup"><span data-stu-id="b75af-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="b75af-138">CDN は、セキュア ソケット レイヤを使用して Web ページを提供する必要がある場合に備えて、SSL (HTTPS) をサポートします。</span><span class="sxs-lookup"><span data-stu-id="b75af-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="b75af-139">CDN は、アップロードされた以下のサードパーティ製スクリプト ライブラリをホストし、それらのライブラリの所有者によってライセンスを取得しています。</span><span class="sxs-lookup"><span data-stu-id="b75af-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="b75af-140">jクエリ (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="b75af-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="b75af-141">jクエリ UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="b75af-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="b75af-142">jQuery モバイル (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="b75af-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="b75af-143">jクエリ検証 (https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="b75af-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="b75af-144">jクエリサイクル(www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="b75af-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="b75af-145">jクエリデータテーブル (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="b75af-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="b75af-146">マイクロソフト Ajax CDN には、マイクロソフトによってアップロードされた次のライブラリも含まれています。</span><span class="sxs-lookup"><span data-stu-id="b75af-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="b75af-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="b75af-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="b75af-148">ASP.NET MVC JavaScript ファイル</span><span class="sxs-lookup"><span data-stu-id="b75af-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="b75af-149">ASP.NETシグナルスクリプトの Java スクリプトファイル</span><span class="sxs-lookup"><span data-stu-id="b75af-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="b75af-150">マイクロソフトは、この CDN でホストされているサードパーティ製ライブラリの所有権を要求しません。</span><span class="sxs-lookup"><span data-stu-id="b75af-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="b75af-151">ライブラリの著作権所有者は、これらのライブラリをライセンスしています。</span><span class="sxs-lookup"><span data-stu-id="b75af-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="b75af-152">このようなライブラリをダウンロードして使用する権利は、それぞれの著作権所有者によってのみ付与されます。</span><span class="sxs-lookup"><span data-stu-id="b75af-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="b75af-153">マイクロソフトのライブラリではないため、マイクロソフトは、この CDN でホストされているサードパーティ製ライブラリに対して、保証や知的財産権ライセンス (黙示的な特許権を含まない) を提供しません。</span><span class="sxs-lookup"><span data-stu-id="b75af-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="b75af-154">JavaScript ライブラリを提出する場合、ライブラリが最上位の JavaScript ライブラリの 1 つhttp://trends.builtwith.com)((a) 人気のあるこれらのライブラリへの拡張/プラグインです ASP.NET。 AjaxCDNSubmission@Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="b75af-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="b75af-155">ajax.microsoft.com名前を変更してajax.aspnetcdn.com</span><span class="sxs-lookup"><span data-stu-id="b75af-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="b75af-156">CDN は、microsoft.comドメイン名を使用するために使用され、aspnetcdn.comドメイン名を使用するように変更されました。</span><span class="sxs-lookup"><span data-stu-id="b75af-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="b75af-157">この変更は、ブラウザがmicrosoft.comドメインを参照したときに、そのドメインからすべてのクッキーを各要求で送信するため、パフォーマンスを向上させるために行われました。</span><span class="sxs-lookup"><span data-stu-id="b75af-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="b75af-158">microsoft.com以外のドメイン名に名前を変更することで、パフォーマンスを 25% まで向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="b75af-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="b75af-159">ajax.microsoft.comは引き続き機能しますが、ajax.aspnetcdn.comすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b75af-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="b75af-160">旧形式:https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="b75af-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="b75af-161">新しい形式:https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="b75af-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="b75af-162">ビジュアル スタジオ .vsdoc サポート</span><span class="sxs-lookup"><span data-stu-id="b75af-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="b75af-163">Visual Studio 2008 で .vsdoc ファイルを正しく使用するには、VS 2008 SP1 がインストールされ、vsdoc ファイルの修正プログラムがインストールされていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b75af-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="b75af-164">あなたはここからこれらを得ることができます:</span><span class="sxs-lookup"><span data-stu-id="b75af-164">You can get these from here:</span></span>

- [<span data-ttu-id="b75af-165">ビジュアル スタジオ 2008 SP1 のダウンロード</span><span class="sxs-lookup"><span data-stu-id="b75af-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "ビジュアル スタジオ 2008 SP1 のダウンロード")
- [<span data-ttu-id="b75af-166">Visual Studio 2008 SP1 の .vsdoc 修正プログラムをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="b75af-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Visual Studio 2008 SP1 の .vsdoc 修正プログラムをダウンロードする")

<span data-ttu-id="b75af-167">Visual Studio 2010 では、追加の修正プログラムを適用せずに .vsdoc ファイルをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="b75af-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="b75af-168">CDN からのASP.NETアヤックスの使用</span><span class="sxs-lookup"><span data-stu-id="b75af-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="b75af-169">ASP.NET 4 を使用する場合、フレームワーク スクリプトのすべての要求ASP.NET CDN にリダイレクトできます。</span><span class="sxs-lookup"><span data-stu-id="b75af-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="b75af-170">ローカル Web サーバーではなく CDN からスクリプトを取得すると、パブリック ASP.NET Web サイトのパフォーマンスが大幅に向上します。</span><span class="sxs-lookup"><span data-stu-id="b75af-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="b75af-171">ScriptManager EnableCDN プロパティを使用して、フレームワークスクリプト要求ASP.NETすべての Microsoft Ajax CDN にリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="b75af-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="b75af-172">CDN からの jQuery の使用</span><span class="sxs-lookup"><span data-stu-id="b75af-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="b75af-173">Web アプリケーションで CDN でホストされている jQuery スクリプトを使用するには、次のスクリプト要素をページに追加します。</span><span class="sxs-lookup"><span data-stu-id="b75af-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="b75af-174">CDN には、次の要素を使用して取得できる jQuery スクリプトの縮小バージョンも含まれています。</span><span class="sxs-lookup"><span data-stu-id="b75af-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="b75af-175">CDN が利用できない場合に、ページがローカル パスから jQuery を読み込むことにフォールバックできるようにするには、CDN を参照する要素の直後に次の要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="b75af-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="b75af-176">次のサンプル ページでは、ボタンがクリックされたときに、jQuery ライブラリの CDN バージョン (ローカル コピーへのフォールバック) を使用して div 要素の内容を表示します。</span><span class="sxs-lookup"><span data-stu-id="b75af-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="b75af-177">jQuery の詳細については、jQuery の Web サイトを参照して[、jQuery](http://jquery.com/)のローカル コピーをダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="b75af-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="b75af-178">CDN からの jQuery UI の使用</span><span class="sxs-lookup"><span data-stu-id="b75af-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="b75af-179">CDN は jQuery UI ライブラリもホストします。</span><span class="sxs-lookup"><span data-stu-id="b75af-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="b75af-180">jQuery UI ライブラリには、ASP.NET アプリケーションで使用できる豊富なウィジェットと効果のセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b75af-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="b75af-181">たとえば、次のページでは、web フォーム アプリケーションのコンテキストで jQuery UI Datepicker を使用して、ポップアップ カレンダーを表示する方法を示ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="b75af-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="b75af-182">キーボードを使用してテキスト ボックスにフォーカスを移動すると、予定表が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b75af-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![日付ピッカーで作成されたポップアップ カレンダー](overview/_static/image1.png)

<span data-ttu-id="b75af-184">上記のコードには、CDN の 3 つのファイルを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="b75af-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="b75af-185">jQuery ライブラリ&mdash;jQuery UI ライブラリは jQuery ライブラリに依存します。</span><span class="sxs-lookup"><span data-stu-id="b75af-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="b75af-186">jQuery UI ライブラリを追加する前に、jQuery ライブラリをページに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b75af-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="b75af-187">jQuery UI&mdash;ライブラリ jQuery UI ライブラリには、jQuery UI エフェクトとウィジェット (上記のページで使用されている Datepicker ウィジェットなど) がすべて含まれています。</span><span class="sxs-lookup"><span data-stu-id="b75af-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="b75af-188">jQuery UI テーマ&mdash;jQuery UI は、さまざまなテーマをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="b75af-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="b75af-189">上記のページには、Redmond テーマをインポートするための CSS ファイルへのリンクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b75af-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="b75af-190">標準の jQuery UI テーマはすべて CDN でホストされます。</span><span class="sxs-lookup"><span data-stu-id="b75af-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="b75af-191">各テーマのサムネイルを表示するには、[このページ](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN の jQuery UI 1.8.10")をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b75af-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="b75af-192">jQuery UI ライブラリの詳細については、[公式 jQuery UI の web サイト](http://jQueryUI.com "jクエリ UI の Web サイト")を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b75af-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="b75af-193">CDN 上のサード パーティ製ファイル</span><span class="sxs-lookup"><span data-stu-id="b75af-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="b75af-194">CDN は、最も人気のあるサードパーティ製の JavaScript ライブラリのいくつかをホストします。</span><span class="sxs-lookup"><span data-stu-id="b75af-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="b75af-195">マイクロソフトは、この CDN でホストされているサードパーティ製ライブラリの所有権を要求しません。</span><span class="sxs-lookup"><span data-stu-id="b75af-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="b75af-196">ライブラリの著作権所有者は、これらのライブラリをライセンスしています。</span><span class="sxs-lookup"><span data-stu-id="b75af-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="b75af-197">このようなライブラリをダウンロードして使用する権利は、それぞれの著作権所有者によってのみ付与されます。</span><span class="sxs-lookup"><span data-stu-id="b75af-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="b75af-198">マイクロソフトのライブラリではないため、マイクロソフトは、この CDN でホストされているサードパーティ製ライブラリに対して、保証や知的財産権ライセンス (黙示的な特許権を含まない) を提供しません。</span><span class="sxs-lookup"><span data-stu-id="b75af-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="b75af-199">CDN にリリースされる jQuery</span><span class="sxs-lookup"><span data-stu-id="b75af-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="b75af-200">次のリリースの jQuery は CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-350"></a><span data-ttu-id="b75af-201">jQuery バージョン 3.5.0</span><span class="sxs-lookup"><span data-stu-id="b75af-201">jQuery version 3.5.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.map

#### <a name="jquery-version-341"></a><span data-ttu-id="b75af-202">jQuery バージョン 3.4.1</span><span class="sxs-lookup"><span data-stu-id="b75af-202">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="b75af-203">jQuery バージョン 3.4.0</span><span class="sxs-lookup"><span data-stu-id="b75af-203">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="b75af-204">jQuery バージョン 3.3.1</span><span class="sxs-lookup"><span data-stu-id="b75af-204">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="b75af-205">jQuery バージョン 3.2.1</span><span class="sxs-lookup"><span data-stu-id="b75af-205">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="b75af-206">jQuery バージョン 3.2.0</span><span class="sxs-lookup"><span data-stu-id="b75af-206">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="b75af-207">jクエリバージョン 3.1.1</span><span class="sxs-lookup"><span data-stu-id="b75af-207">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="b75af-208">jクエリバージョン 3.1.0</span><span class="sxs-lookup"><span data-stu-id="b75af-208">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="b75af-209">jクエリバージョン 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b75af-209">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="b75af-210">jQuery バージョン 2.2.4</span><span class="sxs-lookup"><span data-stu-id="b75af-210">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="b75af-211">jQuery バージョン 2.2.3</span><span class="sxs-lookup"><span data-stu-id="b75af-211">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="b75af-212">jQuery バージョン 2.2.2</span><span class="sxs-lookup"><span data-stu-id="b75af-212">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="b75af-213">jQuery バージョン 2.2.1</span><span class="sxs-lookup"><span data-stu-id="b75af-213">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="b75af-214">jQuery バージョン 2.2.0</span><span class="sxs-lookup"><span data-stu-id="b75af-214">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="b75af-215">jQuery バージョン 2.1.4</span><span class="sxs-lookup"><span data-stu-id="b75af-215">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="b75af-216">jQuery バージョン 2.1.3</span><span class="sxs-lookup"><span data-stu-id="b75af-216">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="b75af-217">jQuery バージョン 2.1.2</span><span class="sxs-lookup"><span data-stu-id="b75af-217">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="b75af-218">jクエリバージョン 2.1.1</span><span class="sxs-lookup"><span data-stu-id="b75af-218">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="b75af-219">jクエリバージョン 2.1.0</span><span class="sxs-lookup"><span data-stu-id="b75af-219">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="b75af-220">jQuery バージョン 2.0.3</span><span class="sxs-lookup"><span data-stu-id="b75af-220">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="b75af-221">jQuery バージョン 2.0.2</span><span class="sxs-lookup"><span data-stu-id="b75af-221">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="b75af-222">jクエリバージョン 2.0.1</span><span class="sxs-lookup"><span data-stu-id="b75af-222">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="b75af-223">jクエリバージョン 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b75af-223">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="b75af-224">jQuery バージョン 1.12.4</span><span class="sxs-lookup"><span data-stu-id="b75af-224">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="b75af-225">jQuery バージョン 1.12.3</span><span class="sxs-lookup"><span data-stu-id="b75af-225">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="b75af-226">jQuery バージョン 1.12.2</span><span class="sxs-lookup"><span data-stu-id="b75af-226">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="b75af-227">jQuery バージョン 1.12.1</span><span class="sxs-lookup"><span data-stu-id="b75af-227">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="b75af-228">jQuery バージョン 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b75af-228">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="b75af-229">jQuery バージョン 1.11.3</span><span class="sxs-lookup"><span data-stu-id="b75af-229">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="b75af-230">jQuery バージョン 1.11.2</span><span class="sxs-lookup"><span data-stu-id="b75af-230">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="b75af-231">jQuery バージョン 1.11.1</span><span class="sxs-lookup"><span data-stu-id="b75af-231">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="b75af-232">jQuery バージョン 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b75af-232">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="b75af-233">jQuery バージョン 1.10.2</span><span class="sxs-lookup"><span data-stu-id="b75af-233">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="b75af-234">jQuery バージョン 1.10.1</span><span class="sxs-lookup"><span data-stu-id="b75af-234">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="b75af-235">jQuery バージョン 1.10.0</span><span class="sxs-lookup"><span data-stu-id="b75af-235">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="b75af-236">jQuery バージョン 1.9.1</span><span class="sxs-lookup"><span data-stu-id="b75af-236">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="b75af-237">jQuery バージョン 1.9.0</span><span class="sxs-lookup"><span data-stu-id="b75af-237">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="b75af-238">jQuery バージョン 1.8.3</span><span class="sxs-lookup"><span data-stu-id="b75af-238">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="b75af-239">jQuery バージョン 1.8.2</span><span class="sxs-lookup"><span data-stu-id="b75af-239">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="b75af-240">jQuery バージョン 1.8.1</span><span class="sxs-lookup"><span data-stu-id="b75af-240">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="b75af-241">jQuery バージョン 1.8.0</span><span class="sxs-lookup"><span data-stu-id="b75af-241">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="b75af-242">jQuery バージョン 1.7.2</span><span class="sxs-lookup"><span data-stu-id="b75af-242">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="b75af-243">jQuery バージョン 1.7.1</span><span class="sxs-lookup"><span data-stu-id="b75af-243">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="b75af-244">jQuery バージョン 1.7</span><span class="sxs-lookup"><span data-stu-id="b75af-244">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="b75af-245">jQuery バージョン 1.6.4</span><span class="sxs-lookup"><span data-stu-id="b75af-245">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="b75af-246">jQuery バージョン 1.6.3</span><span class="sxs-lookup"><span data-stu-id="b75af-246">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="b75af-247">jQuery バージョン 1.6.2</span><span class="sxs-lookup"><span data-stu-id="b75af-247">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="b75af-248">jQuery バージョン 1.6.1</span><span class="sxs-lookup"><span data-stu-id="b75af-248">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="b75af-249">jクエリバージョン 1.6</span><span class="sxs-lookup"><span data-stu-id="b75af-249">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="b75af-250">jQuery バージョン 1.5.2</span><span class="sxs-lookup"><span data-stu-id="b75af-250">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="b75af-251">jQuery バージョン 1.5.1</span><span class="sxs-lookup"><span data-stu-id="b75af-251">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="b75af-252">jクエリバージョン 1.5</span><span class="sxs-lookup"><span data-stu-id="b75af-252">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="b75af-253">jQuery バージョン 1.4.4</span><span class="sxs-lookup"><span data-stu-id="b75af-253">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="b75af-254">jQuery バージョン 1.4.3</span><span class="sxs-lookup"><span data-stu-id="b75af-254">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="b75af-255">jQuery バージョン 1.4.2</span><span class="sxs-lookup"><span data-stu-id="b75af-255">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="b75af-256">jQuery バージョン 1.4.1</span><span class="sxs-lookup"><span data-stu-id="b75af-256">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="b75af-257">jQuery バージョン 1.4</span><span class="sxs-lookup"><span data-stu-id="b75af-257">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="b75af-258">jQuery バージョン 1.3.2</span><span class="sxs-lookup"><span data-stu-id="b75af-258">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="b75af-259">CDN でリリースを移行する jQuery</span><span class="sxs-lookup"><span data-stu-id="b75af-259">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="b75af-260">以下の jQuery 移行のリリースは CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-260">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="b75af-261">jQuery マイグレーション バージョン 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b75af-261">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="b75af-262">jQuery マイグレーション バージョン 1.2.1</span><span class="sxs-lookup"><span data-stu-id="b75af-262">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="b75af-263">jQuery マイグレーション バージョン 1.2.0</span><span class="sxs-lookup"><span data-stu-id="b75af-263">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="b75af-264">jQuery マイグレーション バージョン 1.1.1</span><span class="sxs-lookup"><span data-stu-id="b75af-264">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="b75af-265">jQuery マイグレーション バージョン 1.1.0</span><span class="sxs-lookup"><span data-stu-id="b75af-265">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="b75af-266">jQuery マイグレーション バージョン 1.0.0</span><span class="sxs-lookup"><span data-stu-id="b75af-266">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="b75af-267">CDN での jQuery UI リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-267">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="b75af-268">jQuery UI ライブラリの次のリリースは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-268">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="b75af-269">各リンクをクリックすると、実際のファイルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b75af-269">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b75af-270">jクエリ UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="b75af-270">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Microsoft Ajax CDN の jQuery UI 1.12.1")
- [<span data-ttu-id="b75af-271">jクエリ UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b75af-271">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Microsoft Ajax CDN の jQuery UI 1.12.0")
- [<span data-ttu-id="b75af-272">jクエリ UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="b75af-272">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Microsoft Ajax CDN の jQuery UI 1.11.4")
- [<span data-ttu-id="b75af-273">jクエリ UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="b75af-273">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Microsoft Ajax CDN の jQuery UI 1.11.3")
- [<span data-ttu-id="b75af-274">jクエリ UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="b75af-274">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Microsoft Ajax CDN の jQuery UI 1.11.2")
- [<span data-ttu-id="b75af-275">jクエリ UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="b75af-275">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Microsoft Ajax CDN の jQuery UI 1.11.1")
- [<span data-ttu-id="b75af-276">jクエリ UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b75af-276">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Microsoft Ajax CDN の jQuery UI 1.11.0")
- [<span data-ttu-id="b75af-277">jクエリ UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="b75af-277">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Microsoft Ajax CDN の jQuery UI 1.10.4")
- [<span data-ttu-id="b75af-278">jクエリ UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="b75af-278">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Microsoft Ajax CDN の jQuery UI 1.10.3")
- [<span data-ttu-id="b75af-279">jクエリ UI 1.10.2</span><span class="sxs-lookup"><span data-stu-id="b75af-279">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Microsoft Ajax CDN の jQuery UI 1.10.2")
- [<span data-ttu-id="b75af-280">jクエリ UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="b75af-280">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Microsoft Ajax CDN の jQuery UI 1.10.1")
- [<span data-ttu-id="b75af-281">jクエリ UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="b75af-281">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Microsoft Ajax CDN の jQuery UI 1.10.0")
- [<span data-ttu-id="b75af-282">jクエリ UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="b75af-282">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Microsoft Ajax CDN の jQuery UI 1.9.2")
- [<span data-ttu-id="b75af-283">jクエリ UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="b75af-283">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Microsoft Ajax CDN の jQuery UI 1.9.1")
- [<span data-ttu-id="b75af-284">jクエリ UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="b75af-284">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Microsoft Ajax CDN の jQuery UI 1.9.0")
- [<span data-ttu-id="b75af-285">jクエリ UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="b75af-285">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Microsoft Ajax CDN の jQuery UI 1.8.24")
- [<span data-ttu-id="b75af-286">jクエリ UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="b75af-286">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Microsoft Ajax CDN の jQuery UI 1.8.23")
- [<span data-ttu-id="b75af-287">jクエリ UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="b75af-287">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Microsoft Ajax CDN の jQuery UI 1.8.22")
- [<span data-ttu-id="b75af-288">jクエリ UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="b75af-288">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Microsoft Ajax CDN の jQuery UI 1.8.21")
- [<span data-ttu-id="b75af-289">jクエリ UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="b75af-289">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Microsoft Ajax CDN の jQuery UI 1.8.20")
- [<span data-ttu-id="b75af-290">jクエリ UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="b75af-290">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Microsoft Ajax CDN の jQuery UI 1.8.19")
- [<span data-ttu-id="b75af-291">jクエリ UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="b75af-291">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Microsoft Ajax CDN の jQuery UI 1.8.18")
- [<span data-ttu-id="b75af-292">jクエリ UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="b75af-292">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Microsoft Ajax CDN の jQuery UI 1.8.17")
- [<span data-ttu-id="b75af-293">jクエリ UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="b75af-293">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Microsoft Ajax CDN の jQuery UI 1.8.16")
- [<span data-ttu-id="b75af-294">jクエリ UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="b75af-294">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Microsoft Ajax CDN の jQuery UI 1.8.15")
- [<span data-ttu-id="b75af-295">jクエリ UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="b75af-295">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Microsoft Ajax CDN の jQuery UI 1.8.14")
- [<span data-ttu-id="b75af-296">jクエリ UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="b75af-296">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Microsoft Ajax CDN の jQuery UI 1.8.13")
- [<span data-ttu-id="b75af-297">jクエリ UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="b75af-297">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Microsoft Ajax CDN の jQuery UI 1.8.12")
- [<span data-ttu-id="b75af-298">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="b75af-298">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Microsoft Ajax CDN の jQuery UI 1.8.11")
- [<span data-ttu-id="b75af-299">jクエリ UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="b75af-299">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN の jQuery UI 1.8.10")
- [<span data-ttu-id="b75af-300">jクエリ UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="b75af-300">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Microsoft Ajax CDN の jQuery UI 1.8.9")
- [<span data-ttu-id="b75af-301">jクエリ UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="b75af-301">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Microsoft Ajax CDN の jQuery UI 1.8.8")
- [<span data-ttu-id="b75af-302">jクエリ UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="b75af-302">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Microsoft Ajax CDN の jQuery UI 1.8.7")
- [<span data-ttu-id="b75af-303">jクエリ UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="b75af-303">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Microsoft Ajax CDN の jQuery UI 1.8.6")
- [<span data-ttu-id="b75af-304">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="b75af-304">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="b75af-305">CDN の jQuery 検証リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-305">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="b75af-306">[jQuery 検証](https://jqueryvalidation.org/ "jQuery 検証プラグイン")プラグインの次のリリースは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-306">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="b75af-307">各リンクをクリックすると、実際のファイルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b75af-307">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b75af-308">jクエリ検証 1.19.1</span><span class="sxs-lookup"><span data-stu-id="b75af-308">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "jクエリ検証 1.19.1")
- [<span data-ttu-id="b75af-309">jクエリ検証 1.19.0</span><span class="sxs-lookup"><span data-stu-id="b75af-309">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "jクエリ検証 1.19.0")
- [<span data-ttu-id="b75af-310">jクエリ検証 1.17.0</span><span class="sxs-lookup"><span data-stu-id="b75af-310">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jクエリ検証 1.17.0")
- [<span data-ttu-id="b75af-311">jクエリ検証 1.16.0</span><span class="sxs-lookup"><span data-stu-id="b75af-311">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery Validation 1.16.0")
- [<span data-ttu-id="b75af-312">jクエリ検証 1.15.1</span><span class="sxs-lookup"><span data-stu-id="b75af-312">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery Validation 1.15.1")
- [<span data-ttu-id="b75af-313">jクエリ検証 1.15.0</span><span class="sxs-lookup"><span data-stu-id="b75af-313">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery Validation 1.15.0")
- [<span data-ttu-id="b75af-314">jクエリ検証 1.14.0</span><span class="sxs-lookup"><span data-stu-id="b75af-314">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery Validation 1.14.0")
- [<span data-ttu-id="b75af-315">jクエリ検証 1.13.1</span><span class="sxs-lookup"><span data-stu-id="b75af-315">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery Validation 1.13.1")
- [<span data-ttu-id="b75af-316">jクエリ検証 1.13.0</span><span class="sxs-lookup"><span data-stu-id="b75af-316">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery Validation 1.13.0")
- [<span data-ttu-id="b75af-317">jクエリ検証 1.12.0</span><span class="sxs-lookup"><span data-stu-id="b75af-317">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery Validation 1.12.0")
- [<span data-ttu-id="b75af-318">jクエリ検証 1.11.1</span><span class="sxs-lookup"><span data-stu-id="b75af-318">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery Validation 1.11.1")
- [<span data-ttu-id="b75af-319">jクエリ検証 1.11.0</span><span class="sxs-lookup"><span data-stu-id="b75af-319">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery Validation 1.11.0")
- [<span data-ttu-id="b75af-320">jクエリ検証 1.10.0</span><span class="sxs-lookup"><span data-stu-id="b75af-320">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery Validation 1.10.0")
- [<span data-ttu-id="b75af-321">jクエリ検証 1.9</span><span class="sxs-lookup"><span data-stu-id="b75af-321">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate バージョン 1.9")
- [<span data-ttu-id="b75af-322">jクエリ検証 1.8.1</span><span class="sxs-lookup"><span data-stu-id="b75af-322">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate バージョン 1.8.1")
- [<span data-ttu-id="b75af-323">jクエリ検証 1.8</span><span class="sxs-lookup"><span data-stu-id="b75af-323">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate バージョン 1.8")
- [<span data-ttu-id="b75af-324">jクエリ検証 1.7</span><span class="sxs-lookup"><span data-stu-id="b75af-324">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate バージョン 1.7")
- [<span data-ttu-id="b75af-325">jQuery Validate 1.6</span><span class="sxs-lookup"><span data-stu-id="b75af-325">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery Validate 1.6")
- [<span data-ttu-id="b75af-326">jQuery Validate 1.5.5</span><span class="sxs-lookup"><span data-stu-id="b75af-326">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery Validate 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="b75af-327">CDN のモバイルリリース</span><span class="sxs-lookup"><span data-stu-id="b75af-327">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="b75af-328">jQuery モバイル ライブラリの次のリリースは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-328">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="b75af-329">各リンクをクリックすると、実際のファイルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b75af-329">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b75af-330">jQueryモバイル 1.4.5</span><span class="sxs-lookup"><span data-stu-id="b75af-330">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "Microsoft Ajax CDN の jQuery Mobile 1.4.5")
- [<span data-ttu-id="b75af-331">jQueryモバイル 1.4.2</span><span class="sxs-lookup"><span data-stu-id="b75af-331">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "Microsoft Ajax CDN の jQuery Mobile 1.4.2")
- [<span data-ttu-id="b75af-332">jQueryモバイル 1.4.1</span><span class="sxs-lookup"><span data-stu-id="b75af-332">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "Microsoft Ajax CDN の jQuery Mobile 1.4.1")
- [<span data-ttu-id="b75af-333">jQueryモバイル 1.4.0</span><span class="sxs-lookup"><span data-stu-id="b75af-333">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "Microsoft Ajax CDN の jQuery Mobile 1.4.0")
- [<span data-ttu-id="b75af-334">jQueryモバイル 1.3.2</span><span class="sxs-lookup"><span data-stu-id="b75af-334">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "Microsoft Ajax CDN の jQuery Mobile 1.3.2")
- [<span data-ttu-id="b75af-335">jQueryモバイル 1.3.1</span><span class="sxs-lookup"><span data-stu-id="b75af-335">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "Microsoft Ajax CDN の jQuery Mobile 1.3.1")
- [<span data-ttu-id="b75af-336">jQueryモバイル 1.3.0</span><span class="sxs-lookup"><span data-stu-id="b75af-336">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "Microsoft Ajax CDN の jQuery Mobile 1.3.0")
- [<span data-ttu-id="b75af-337">jQueryモバイル 1.2.0</span><span class="sxs-lookup"><span data-stu-id="b75af-337">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "Microsoft Ajax CDN の jQuery Mobile 1.2.0")
- [<span data-ttu-id="b75af-338">jQueryモバイル 1.1.2</span><span class="sxs-lookup"><span data-stu-id="b75af-338">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "Microsoft Ajax CDN の jQuery Mobile 1.1.2")
- [<span data-ttu-id="b75af-339">jQueryモバイル 1.1.1</span><span class="sxs-lookup"><span data-stu-id="b75af-339">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "Microsoft Ajax CDN の jQuery Mobile 1.1.1")
- [<span data-ttu-id="b75af-340">jQueryモバイル 1.1.0</span><span class="sxs-lookup"><span data-stu-id="b75af-340">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "Microsoft Ajax CDN の jQuery Mobile 1.1.0")
- [<span data-ttu-id="b75af-341">jQueryモバイル 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="b75af-341">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "Microsoft Ajax CDN の jQuery Mobile 1.1.0 RC2")
- [<span data-ttu-id="b75af-342">jQueryモバイル 1.0.1</span><span class="sxs-lookup"><span data-stu-id="b75af-342">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "Microsoft Ajax CDN の jQuery Mobile 1.0.1")
- [<span data-ttu-id="b75af-343">jQueryモバイル 1.0</span><span class="sxs-lookup"><span data-stu-id="b75af-343">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "Microsoft Ajax CDN の jQuery Mobile 1.0")
- [<span data-ttu-id="b75af-344">jQueryモバイル1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="b75af-344">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN の jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="b75af-345">jQueryモバイル1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="b75af-345">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN の jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="b75af-346">jQueryモバイル1.0ベータ3</span><span class="sxs-lookup"><span data-stu-id="b75af-346">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN の jQuery Mobile 1.0 Beta 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="b75af-347">CDN でリリースされる jQuery テンプレート</span><span class="sxs-lookup"><span data-stu-id="b75af-347">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="b75af-348">jQuery テンプレート プラグインの次のリリースは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-348">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="b75af-349">各リンクをクリックすると、実際のファイルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b75af-349">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b75af-350">jQuery Templates Beta 1</span><span class="sxs-lookup"><span data-stu-id="b75af-350">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery Templates Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="b75af-351">CDN の jQuery サイクルリリース</span><span class="sxs-lookup"><span data-stu-id="b75af-351">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="b75af-352">jQuery サイクルプラグインの次のリリースは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-352">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="b75af-353">各リンクをクリックすると、実際のファイルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b75af-353">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b75af-354">jクエリサイクル 2.99</span><span class="sxs-lookup"><span data-stu-id="b75af-354">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="b75af-355">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="b75af-355">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="b75af-356">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="b75af-356">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="b75af-357">CDN でリリースされるデータテーブル</span><span class="sxs-lookup"><span data-stu-id="b75af-357">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="b75af-358">jQuery データテーブル プラグインの次のリリースは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-358">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="b75af-359">各リンクをクリックすると、実際のファイルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b75af-359">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b75af-360">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="b75af-360">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="b75af-361">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="b75af-361">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="b75af-362">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="b75af-362">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="b75af-363">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="b75af-363">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="b75af-364">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="b75af-364">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="b75af-365">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="b75af-365">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="b75af-366">データテーブル 1.9.0</span><span class="sxs-lookup"><span data-stu-id="b75af-366">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="b75af-367">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="b75af-367">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="b75af-368">CDN のモダニズム リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-368">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="b75af-369">次のリリースの[Modernizr](http://www.modernizr.com "Modernizr")は CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-369">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="b75af-370">CDN に関する JS ヒント リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-370">JSHint Releases on the CDN</span></span>

<span data-ttu-id="b75af-371">[JSHint](http://www.jshint.com "JSヒント")の次のリリースは CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-371">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="b75af-372">CDN のノックアウト リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-372">Knockout Releases on the CDN</span></span>

<span data-ttu-id="b75af-373">次のリリースの[ノックアウト](http://www.knockoutjs.com "ノックアウト")は CDN でホストされます。</span><span class="sxs-lookup"><span data-stu-id="b75af-373">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="b75af-374">CDN のリリースのグローバル化</span><span class="sxs-lookup"><span data-stu-id="b75af-374">Globalize Releases on the CDN</span></span>

<span data-ttu-id="b75af-375">以下のリリースの[Globalize](https://github.com/jquery/globalize "グローバライズ")は CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-375">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="b75af-376">バージョン 1.0.0 をグローバル化する</span><span class="sxs-lookup"><span data-stu-id="b75af-376">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="b75af-377">バージョン 0.1.1 のグローバリゼーション</span><span class="sxs-lookup"><span data-stu-id="b75af-377">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="b75af-378">すべての文化</span><span class="sxs-lookup"><span data-stu-id="b75af-378">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="b75af-379">"{カルチャ コード}" を目的のカルチャ コードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="b75af-379">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="b75af-380">CDN のリリースに応答する</span><span class="sxs-lookup"><span data-stu-id="b75af-380">Respond Releases on the CDN</span></span>

<span data-ttu-id="b75af-381">[応答](https://github.com/scottjehl/Respond "対応")の次のリリースは、CDN でホストされます。</span><span class="sxs-lookup"><span data-stu-id="b75af-381">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="b75af-382">応答バージョン 1.4.2</span><span class="sxs-lookup"><span data-stu-id="b75af-382">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="b75af-383">応答バージョン 1.4.1</span><span class="sxs-lookup"><span data-stu-id="b75af-383">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="b75af-384">応答バージョン 1.4.0</span><span class="sxs-lookup"><span data-stu-id="b75af-384">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="b75af-385">応答バージョン 1.3.0</span><span class="sxs-lookup"><span data-stu-id="b75af-385">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="b75af-386">応答バージョン 1.2.0</span><span class="sxs-lookup"><span data-stu-id="b75af-386">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="b75af-387">CDN のブートストラップ リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-387">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="b75af-388">次のリリースの[getbootstrap.com](http://getbootstrap.com "getbootstrap.com")ブートストラップは CDN でホストされます。</span><span class="sxs-lookup"><span data-stu-id="b75af-388">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-441"></a><span data-ttu-id="b75af-389">ブートストラップバージョン 4.4.1</span><span class="sxs-lookup"><span data-stu-id="b75af-389">Bootstrap version 4.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-431"></a><span data-ttu-id="b75af-390">ブートストラップバージョン 4.3.1</span><span class="sxs-lookup"><span data-stu-id="b75af-390">Bootstrap version 4.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-421"></a><span data-ttu-id="b75af-391">ブートストラップバージョン 4.2.1</span><span class="sxs-lookup"><span data-stu-id="b75af-391">Bootstrap version 4.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a><span data-ttu-id="b75af-392">ブートストラップバージョン 4.1.1</span><span class="sxs-lookup"><span data-stu-id="b75af-392">Bootstrap version 4.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a><span data-ttu-id="b75af-393">ブートストラップバージョン 4.0.0</span><span class="sxs-lookup"><span data-stu-id="b75af-393">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-341"></a><span data-ttu-id="b75af-394">ブートストラップバージョン 3.4.1</span><span class="sxs-lookup"><span data-stu-id="b75af-394">Bootstrap version 3.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-340"></a><span data-ttu-id="b75af-395">ブートストラップバージョン 3.4.0</span><span class="sxs-lookup"><span data-stu-id="b75af-395">Bootstrap version 3.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="b75af-396">ブートストラップバージョン 3.3.7</span><span class="sxs-lookup"><span data-stu-id="b75af-396">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="b75af-397">ブートストラップバージョン 3.3.6</span><span class="sxs-lookup"><span data-stu-id="b75af-397">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="b75af-398">ブートストラップバージョン 3.3.5</span><span class="sxs-lookup"><span data-stu-id="b75af-398">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="b75af-399">ブートストラップバージョン 3.3.4</span><span class="sxs-lookup"><span data-stu-id="b75af-399">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="b75af-400">ブートストラップバージョン 3.3.2</span><span class="sxs-lookup"><span data-stu-id="b75af-400">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="b75af-401">ブートストラップバージョン 3.3.1</span><span class="sxs-lookup"><span data-stu-id="b75af-401">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="b75af-402">ブートストラップバージョン 3.3.0</span><span class="sxs-lookup"><span data-stu-id="b75af-402">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="b75af-403">ブートストラップバージョン 3.2.0</span><span class="sxs-lookup"><span data-stu-id="b75af-403">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="b75af-404">ブートストラップバージョン 3.1.1</span><span class="sxs-lookup"><span data-stu-id="b75af-404">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="b75af-405">ブートストラップバージョン 3.1.0</span><span class="sxs-lookup"><span data-stu-id="b75af-405">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="b75af-406">ブートストラップバージョン 3.0.3</span><span class="sxs-lookup"><span data-stu-id="b75af-406">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="b75af-407">ブートストラップバージョン 3.0.2</span><span class="sxs-lookup"><span data-stu-id="b75af-407">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="b75af-408">ブートストラップバージョン 3.0.1</span><span class="sxs-lookup"><span data-stu-id="b75af-408">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="b75af-409">ブートストラップバージョン 3.0.0</span><span class="sxs-lookup"><span data-stu-id="b75af-409">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="b75af-410">ブートストラップバージョン 2.3.2</span><span class="sxs-lookup"><span data-stu-id="b75af-410">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="b75af-411">ブートストラップバージョン 2.3.1</span><span class="sxs-lookup"><span data-stu-id="b75af-411">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="b75af-412">CDN のブートストラップ タッチカルーセル リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-412">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="b75af-413">ブートストラップタッチカ[https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel")ルーセルリリースの次のリリースは、CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-413">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="b75af-414">ブートストラップ タッチカルーセル バージョン 0.8.0</span><span class="sxs-lookup"><span data-stu-id="b75af-414">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="b75af-415">CDN の Hammer.js リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-415">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="b75af-416">以下のリリースの[http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/")Hammer.js は CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-416">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="b75af-417">ハンマー.js バージョン 2.0.4</span><span class="sxs-lookup"><span data-stu-id="b75af-417">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="b75af-418">CDN で Web フォームと Ajax リリースをASP.NETする</span><span class="sxs-lookup"><span data-stu-id="b75af-418">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="b75af-419">以下のリリースの ajax ライブラリASP.NETは CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-419">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="b75af-420">各リンクをクリックすると、実際のファイルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b75af-420">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="b75af-421">ASP.NET Web フォームおよび Ajax バージョン 4.5.2</span><span class="sxs-lookup"><span data-stu-id="b75af-421">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web フォームと Ajax 4.5.2")
- [<span data-ttu-id="b75af-422">ASP.NET Web フォームおよび Ajax バージョン 4</span><span class="sxs-lookup"><span data-stu-id="b75af-422">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web Forms および Ajax 4")
- [<span data-ttu-id="b75af-423">ASP.NET Ajax バージョン 3.5</span><span class="sxs-lookup"><span data-stu-id="b75af-423">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="b75af-424">CDN のASP.NET MVC リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-424">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="b75af-425">次のASP.NET MVC JavaScript ファイルは、この CDN でホストされています。</span><span class="sxs-lookup"><span data-stu-id="b75af-425">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="b75af-426">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="b75af-426">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="b75af-427">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="b75af-427">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="b75af-428">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="b75af-428">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="b75af-429">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="b75af-429">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="b75af-430">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="b75af-430">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="b75af-431">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="b75af-431">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="b75af-432">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="b75af-432">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="b75af-433">CDN でのASP.NETシグナル・リリース</span><span class="sxs-lookup"><span data-stu-id="b75af-433">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="b75af-434">次のASP.NET SignalR JavaScript ファイルは、この CDN でホストされます。</span><span class="sxs-lookup"><span data-stu-id="b75af-434">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="b75af-435">ASP.NETシグナルR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="b75af-435">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="b75af-436">ASP.NETシグナルR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="b75af-436">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="b75af-437">ASP.NETシグナルR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="b75af-437">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="b75af-438">ASP.NETシグナルR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="b75af-438">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="b75af-439">ASP.NETシグナルR 2.0.3</span><span class="sxs-lookup"><span data-stu-id="b75af-439">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="b75af-440">ASP.NET信号機 2.0.2</span><span class="sxs-lookup"><span data-stu-id="b75af-440">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="b75af-441">ASP.NETシグナルR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="b75af-441">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="b75af-442">ASP.NETシグナルR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b75af-442">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="b75af-443">ASP.NET信号機 1.1.3</span><span class="sxs-lookup"><span data-stu-id="b75af-443">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="b75af-444">ASP.NET信号機 1.1.2</span><span class="sxs-lookup"><span data-stu-id="b75af-444">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="b75af-445">ASP.NETシグナルR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="b75af-445">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="b75af-446">ASP.NETシグナルR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="b75af-446">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="b75af-447">ASP.NETシグナルR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="b75af-447">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="b75af-448">CDN の使用条件については、[マイクロソフト Ajax CDN 利用規約](https://www.asp.net/terms-of-use "マイクロソフト Ajax CDN 利用規約")を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b75af-448">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
