---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: キャッシュされたページへの動的コンテンツの追加 (C#) |マイクロソフトドキュメント
author: rick-anderson
description: 同じページで動的コンテンツとキャッシュコンテンツを混在する方法について説明します。 ポストキャッシュ置換を使用すると、バナー広告などの動的コンテンツを表示できます。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c8cd70a15c1ae93f7cf9b0a026b37b07e489040
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542288"
---
# <a name="adding-dynamic-content-to-a-cached-page-c"></a><span data-ttu-id="829f0-104">キャッシュされたページに動的コンテンツを追加する (C#)</span><span class="sxs-lookup"><span data-stu-id="829f0-104">Adding Dynamic Content to a Cached Page (C#)</span></span>

<span data-ttu-id="829f0-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="829f0-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="829f0-106">同じページで動的コンテンツとキャッシュコンテンツを混在する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="829f0-106">Learn how to mix dynamic and cached content in the same page.</span></span> <span data-ttu-id="829f0-107">ポストキャッシュ置換を使用すると、出力キャッシュされたページ内にバナー広告やニュースアイテムなどの動的コンテンツを表示できます。</span><span class="sxs-lookup"><span data-stu-id="829f0-107">Post-cache substitution enables you to display dynamic content, such as banner advertisements or news items, within a page that has been output cached.</span></span>

<span data-ttu-id="829f0-108">出力キャッシュを利用することで、ASP.NET MVC アプリケーションのパフォーマンスを大幅に向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="829f0-108">By taking advantage of output caching, you can dramatically improve the performance of an ASP.NET MVC application.</span></span> <span data-ttu-id="829f0-109">ページが要求されるたびにページを再生成する代わりに、ページを 1 回だけ生成して、複数のユーザーのメモリにキャッシュできます。</span><span class="sxs-lookup"><span data-stu-id="829f0-109">Instead of regenerating a page each and every time the page is requested, the page can be generated once and cached in memory for multiple users.</span></span>

<span data-ttu-id="829f0-110">しかし、問題があります。</span><span class="sxs-lookup"><span data-stu-id="829f0-110">But there is a problem.</span></span> <span data-ttu-id="829f0-111">ページに動的コンテンツを表示する必要がある場合はどうでしょうか。</span><span class="sxs-lookup"><span data-stu-id="829f0-111">What if you need to display dynamic content in the page?</span></span> <span data-ttu-id="829f0-112">たとえば、ページにバナー広告を表示するとします。</span><span class="sxs-lookup"><span data-stu-id="829f0-112">For example, imagine that you want to display a banner advertisement in the page.</span></span> <span data-ttu-id="829f0-113">すべてのユーザーがまったく同じ広告を表示するように、バナー広告をキャッシュしたくない。</span><span class="sxs-lookup"><span data-stu-id="829f0-113">You don't want the banner advertisement to be cached so that every user sees the very same advertisement.</span></span> <span data-ttu-id="829f0-114">あなたはそのようにお金を稼ぐことはありません!</span><span class="sxs-lookup"><span data-stu-id="829f0-114">You wouldn't make any money that way!</span></span>

<span data-ttu-id="829f0-115">幸いなことに、簡単な解決策があります。</span><span class="sxs-lookup"><span data-stu-id="829f0-115">Fortunately, there is an easy solution.</span></span> <span data-ttu-id="829f0-116">*ポストキャッシュ置換*と呼ばれるASP.NETフレームワークの機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="829f0-116">You can take advantage of a feature of the ASP.NET framework called *post-cache substitution*.</span></span> <span data-ttu-id="829f0-117">キャッシュ後置換を使用すると、メモリにキャッシュされたページの動的コンテンツを置き換えることができます。</span><span class="sxs-lookup"><span data-stu-id="829f0-117">Post-cache substitution enables you to substitute dynamic content in a page that has been cached in memory.</span></span>

<span data-ttu-id="829f0-118">通常、[OutputCache] 属性を使用してページを出力すると、ページはサーバーとクライアント (Web ブラウザ) の両方にキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="829f0-118">Normally, when you output cache a page by using the [OutputCache] attribute, the page is cached on both the server and the client (the web browser).</span></span> <span data-ttu-id="829f0-119">キャッシュ後置換を使用すると、ページはサーバー上でのみキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="829f0-119">When you use post-cache substitution, a page is cached only on the server.</span></span>

#### <a name="using-post-cache-substitution"></a><span data-ttu-id="829f0-120">キャッシュ後置換の使用</span><span class="sxs-lookup"><span data-stu-id="829f0-120">Using Post-Cache Substitution</span></span>

<span data-ttu-id="829f0-121">キャッシュ後置換を使用するには、2 つの手順が必要です。</span><span class="sxs-lookup"><span data-stu-id="829f0-121">Using post-cache substitution requires two steps.</span></span> <span data-ttu-id="829f0-122">まず、キャッシュされたページに表示する動的コンテンツを表す文字列を返すメソッドを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="829f0-122">First, you need to define a method that returns a string that represents the dynamic content that you want to display in the cached page.</span></span> <span data-ttu-id="829f0-123">次に、ページに動的コンテンツを挿入するメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="829f0-123">Next, you call the HttpResponse.WriteSubstitution() method to inject the dynamic content into the page.</span></span>

<span data-ttu-id="829f0-124">たとえば、キャッシュされたページに異なるニュース項目をランダムに表示するとします。</span><span class="sxs-lookup"><span data-stu-id="829f0-124">Imagine, for example, that you want to randomly display different news items in a cached page.</span></span> <span data-ttu-id="829f0-125">リスト 1 のクラスは、3 つのニュース項目のリストから 1 つのニュース項目をランダムに返す RenderNews() という名前の単一のメソッドを公開します。</span><span class="sxs-lookup"><span data-stu-id="829f0-125">The class in Listing 1 exposes a single method, named RenderNews(), that randomly returns one news item from a list of three news items.</span></span>

<span data-ttu-id="829f0-126">**リスト 1 - モデル\ニュース.cs**</span><span class="sxs-lookup"><span data-stu-id="829f0-126">**Listing 1 – Models\News.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

<span data-ttu-id="829f0-127">キャッシュ後の置換を利用するには、メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="829f0-127">To take advantage of post-cache substitution, you call the HttpResponse.WriteSubstitution() method.</span></span> <span data-ttu-id="829f0-128">WriteSubstitution() メソッドは、キャッシュされたページの領域を動的コンテンツに置き換えるコードを設定します。</span><span class="sxs-lookup"><span data-stu-id="829f0-128">The WriteSubstitution() method sets up the code to replace a region of the cached page with dynamic content.</span></span> <span data-ttu-id="829f0-129">WriteSubstitution() メソッドは、リスト 2 のビューでランダムなニュース項目を表示するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="829f0-129">The WriteSubstitution() method is used to display the random news item in the view in Listing 2.</span></span>

<span data-ttu-id="829f0-130">**リスト 2 - ビュー\ホーム\インデックス.aspx**</span><span class="sxs-lookup"><span data-stu-id="829f0-130">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

<span data-ttu-id="829f0-131">メソッドは、メソッドに渡されます。</span><span class="sxs-lookup"><span data-stu-id="829f0-131">The RenderNews method is passed to the WriteSubstitution() method.</span></span> <span data-ttu-id="829f0-132">RenderNews メソッドが呼び出されないことに注意してください (かっこはありません)。</span><span class="sxs-lookup"><span data-stu-id="829f0-132">Notice that the RenderNews method is not called (there are no parentheses).</span></span> <span data-ttu-id="829f0-133">代わりに、メソッドへの参照が代入に渡されます。</span><span class="sxs-lookup"><span data-stu-id="829f0-133">Instead a reference to the method is passed to WriteSubstitution().</span></span>

<span data-ttu-id="829f0-134">インデックス ビューがキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="829f0-134">The Index view is cached.</span></span> <span data-ttu-id="829f0-135">ビューはリスト 3 のコントローラーによって返されます。</span><span class="sxs-lookup"><span data-stu-id="829f0-135">The view is returned by the controller in Listing 3.</span></span> <span data-ttu-id="829f0-136">Index() アクションは[OutputCache] 属性で修飾され、インデックス ビューが 60 秒間キャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="829f0-136">Notice that the Index() action is decorated with an [OutputCache] attribute that causes the Index view to be cached for 60 seconds.</span></span>

<span data-ttu-id="829f0-137">**リスト 3 - コントローラ\ホームコントローラー.cs**</span><span class="sxs-lookup"><span data-stu-id="829f0-137">**Listing 3 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

<span data-ttu-id="829f0-138">インデックス ビューがキャッシュされている場合でも、インデックス ページを要求すると異なるランダムなニュース項目が表示されます。</span><span class="sxs-lookup"><span data-stu-id="829f0-138">Even though the Index view is cached, different random news items are displayed when you request the Index page.</span></span> <span data-ttu-id="829f0-139">[インデックス] ページを要求すると、ページに表示される時間は 60 秒間変わりません (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="829f0-139">When you request the Index page, the time displayed by the page does not change for 60 seconds (see Figure 1).</span></span> <span data-ttu-id="829f0-140">時刻が変わらないということは、ページがキャッシュされていることを証明します。</span><span class="sxs-lookup"><span data-stu-id="829f0-140">The fact that the time does not change proves that the page is cached.</span></span> <span data-ttu-id="829f0-141">しかし、WriteSubstitution() メソッドによって挿入されたコンテンツ ( ランダムなニュース項目 ) は、要求ごとに変更されます。</span><span class="sxs-lookup"><span data-stu-id="829f0-141">However, the content injected by the WriteSubstitution() method – the random news item – changes with each request .</span></span>

<span data-ttu-id="829f0-142">**図 1 – キャッシュされたページに動的なニュース項目を挿入する**</span><span class="sxs-lookup"><span data-stu-id="829f0-142">**Figure 1 – Injecting dynamic news items in a cached page**</span></span>

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a><span data-ttu-id="829f0-144">ヘルパー メソッドでのキャッシュ後置換の使用</span><span class="sxs-lookup"><span data-stu-id="829f0-144">Using Post-Cache Substitution in Helper Methods</span></span>

<span data-ttu-id="829f0-145">キャッシュ後の置換を利用する簡単な方法は、カスタム ヘルパー メソッド内で WriteSubstitution() メソッドの呼び出しをカプセル化することです。</span><span class="sxs-lookup"><span data-stu-id="829f0-145">An easier way to take advantage of post-cache substitution is to encapsulate the call to the WriteSubstitution() method within a custom helper method.</span></span> <span data-ttu-id="829f0-146">この方法は、リスト 4 のヘルパー メソッドによって示されています。</span><span class="sxs-lookup"><span data-stu-id="829f0-146">This approach is illustrated by the helper method in Listing 4.</span></span>

<span data-ttu-id="829f0-147">**リスト4 – AdHelper.cs**</span><span class="sxs-lookup"><span data-stu-id="829f0-147">**Listing 4 – AdHelper.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

<span data-ttu-id="829f0-148">リスト 4 には、2 つのメソッドを公開する静的クラスが含まれています: レンダリングバナー() とレンダーバナー内部() 。</span><span class="sxs-lookup"><span data-stu-id="829f0-148">Listing 4 contains a static class that exposes two methods: RenderBanner() and RenderBannerInternal().</span></span> <span data-ttu-id="829f0-149">メソッドは、実際のヘルパー メソッドを表します。</span><span class="sxs-lookup"><span data-stu-id="829f0-149">The RenderBanner() method represents the actual helper method.</span></span> <span data-ttu-id="829f0-150">このメソッドは、MVC htmlHelper クラスASP.NET標準を拡張して、他のヘルパー メソッドと同じようにビューで Html.RenderBanner() を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="829f0-150">This method extends the standard ASP.NET MVC HtmlHelper class so that you can call Html.RenderBanner() in a view just like any other helper method.</span></span>

<span data-ttu-id="829f0-151">メソッドは、メソッドにメソッドを渡してメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="829f0-151">The RenderBanner() method calls the HttpResponse.WriteSubstitution() method passing the RenderBannerInternal() method to the WriteSubstitution() method.</span></span>

<span data-ttu-id="829f0-152">メソッドはプライベート メソッドです。</span><span class="sxs-lookup"><span data-stu-id="829f0-152">The RenderBannerInternal() method is a private method.</span></span> <span data-ttu-id="829f0-153">このメソッドはヘルパー メソッドとして公開されません。</span><span class="sxs-lookup"><span data-stu-id="829f0-153">This method won't be exposed as a helper method.</span></span> <span data-ttu-id="829f0-154">RenderBannerInternal() メソッドは、3 つのバナー広告イメージのリストから 1 つのバナー広告イメージをランダムに返します。</span><span class="sxs-lookup"><span data-stu-id="829f0-154">The RenderBannerInternal() method randomly returns one banner advertisement image from a list of three banner advertisement images.</span></span>

<span data-ttu-id="829f0-155">リスト 5 の変更されたインデックス ビューは、RenderBanner() ヘルパー メソッドの使用方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="829f0-155">The modified Index view in Listing 5 illustrates how you can use the RenderBanner() helper method.</span></span> <span data-ttu-id="829f0-156">MvcApplication1.Helpers 名前空間をインポートするビューの上部に追加&lt;の %@ インポート %&gt;ディレクティブが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="829f0-156">Notice that an additional &lt;%@ Import %&gt; directive is included at the top of the view to import the MvcApplication1.Helpers namespace.</span></span> <span data-ttu-id="829f0-157">この名前空間をインポートしない場合、RenderBanner() メソッドは Html プロパティのメソッドとして表示されません。</span><span class="sxs-lookup"><span data-stu-id="829f0-157">If you neglect to import this namespace, then the RenderBanner() method won't appear as a method on the Html property.</span></span>

<span data-ttu-id="829f0-158">**リスト 5 - ビュー\ホーム\インデックス.aspx (レンダーバナー()メソッドを使用)**</span><span class="sxs-lookup"><span data-stu-id="829f0-158">**Listing 5 – Views\Home\Index.aspx (with RenderBanner() method)**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

<span data-ttu-id="829f0-159">リスト 5 のビューで表示されるページを要求すると、要求ごとに異なるバナー広告が表示されます (図 2 参照)。</span><span class="sxs-lookup"><span data-stu-id="829f0-159">When you request the page rendered by the view in Listing 5, a different banner advertisement is displayed with each request (see Figure 2).</span></span> <span data-ttu-id="829f0-160">ページはキャッシュされますが、RenderBanner() ヘルパー メソッドによってバナー広告が動的に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="829f0-160">The page is cached, but the banner advertisement is injected dynamically by the RenderBanner() helper method.</span></span>

<span data-ttu-id="829f0-161">**図 2 – ランダムなバナー広告を表示するインデックス ビュー**</span><span class="sxs-lookup"><span data-stu-id="829f0-161">**Figure 2 – The Index view displaying a random banner advertisement**</span></span>

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a><span data-ttu-id="829f0-163">まとめ</span><span class="sxs-lookup"><span data-stu-id="829f0-163">Summary</span></span>

<span data-ttu-id="829f0-164">このチュートリアルでは、キャッシュされたページのコンテンツを動的に更新する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="829f0-164">This tutorial explained how you can dynamically update content in a cached page.</span></span> <span data-ttu-id="829f0-165">HttpResponse.WriteSubstitution() メソッドを使用して、キャッシュされたページに動的コンテンツを挿入できるようにする方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="829f0-165">You learned how to use the HttpResponse.WriteSubstitution() method to enable dynamic content to be injected in a cached page.</span></span> <span data-ttu-id="829f0-166">また、HTML ヘルパー メソッド内で WriteSubstitution() メソッドの呼び出しをカプセル化する方法についても学習しました。</span><span class="sxs-lookup"><span data-stu-id="829f0-166">You also learned how to encapsulate the call to the WriteSubstitution() method within an HTML helper method.</span></span>

<span data-ttu-id="829f0-167">可能な限りキャッシュを利用して、Web アプリケーションのパフォーマンスに大きな影響を与える可能性があります。</span><span class="sxs-lookup"><span data-stu-id="829f0-167">Take advantage of caching whenever possible – it can have a dramatic impact on the performance of your web applications.</span></span> <span data-ttu-id="829f0-168">このチュートリアルで説明したように、ページに動的コンテンツを表示する必要がある場合でも、キャッシュを利用できます。</span><span class="sxs-lookup"><span data-stu-id="829f0-168">As explained in this tutorial, you can take advantage of caching even when you need to display dynamic content in your pages.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="829f0-169">[前へ](improving-performance-with-output-caching-cs.md)
> [次へ](creating-a-controller-cs.md)</span><span class="sxs-lookup"><span data-stu-id="829f0-169">[Previous](improving-performance-with-output-caching-cs.md)
[Next](creating-a-controller-cs.md)</span></span>
