---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: 出力キャッシュ (VB) を使用したパフォーマンスの向上 |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルでは、出力キャッシュを利用して、ASP.NET MVC Web アプリケーションのパフォーマンスを劇的に向上させる方法を学習します。 あなたが。。。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: e18d4c5132d4dccc97f1465e7885c9c47a0edab1
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542691"
---
# <a name="improving-performance-with-output-caching-vb"></a><span data-ttu-id="d99dc-104">出力キャッシュでパフォーマンスを改善する (VB)</span><span class="sxs-lookup"><span data-stu-id="d99dc-104">Improving Performance with Output Caching (VB)</span></span>

<span data-ttu-id="d99dc-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d99dc-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d99dc-106">このチュートリアルでは、出力キャッシュを利用して、ASP.NET MVC Web アプリケーションのパフォーマンスを劇的に向上させる方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-106">In this tutorial, you learn how you can dramatically improve the performance of your ASP.NET MVC web applications by taking advantage of output caching.</span></span> <span data-ttu-id="d99dc-107">コントローラーアクションから返された結果をキャッシュする方法を学習し、新しいユーザーがアクションを呼び出すたびに同じコンテンツを作成する必要がないようにします。</span><span class="sxs-lookup"><span data-stu-id="d99dc-107">You learn how to cache the result returned from a controller action so that the same content does not need to be created each and every time a new user invokes the action.</span></span>

<span data-ttu-id="d99dc-108">このチュートリアルの目的は、出力キャッシュを利用して ASP.NET MVC アプリケーションのパフォーマンスを劇的に向上させる方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="d99dc-108">The goal of this tutorial is to explain how you can dramatically improve the performance of an ASP.NET MVC application by taking advantage of the output cache.</span></span> <span data-ttu-id="d99dc-109">出力キャッシュを使用すると、コントローラー アクションによって返されるコンテンツをキャッシュできます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-109">The output cache enables you to cache the content returned by a controller action.</span></span> <span data-ttu-id="d99dc-110">このように、同じコント ローラー アクションが呼び出されるたびに、同じコンテンツを生成する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="d99dc-110">That way, the same content does not need to be generated each and every time the same controller action is invoked.</span></span>

<span data-ttu-id="d99dc-111">たとえば、ASP.NET MVC アプリケーションが Index という名前のビューにデータベース レコードのリストを表示するとします。</span><span class="sxs-lookup"><span data-stu-id="d99dc-111">Imagine, for example, that your ASP.NET MVC application displays a list of database records in a view named Index.</span></span> <span data-ttu-id="d99dc-112">通常、ユーザーがインデックス ビューを返すコントローラー アクションを呼び出すたびに、データベース クエリを実行してデータベースからデータベース レコードのセットを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d99dc-112">Normally, each and every time that a user invokes the controller action that returns the Index view, the set of database records must be retrieved from the database by executing a database query.</span></span>

<span data-ttu-id="d99dc-113">一方、出力キャッシュを利用する場合は、ユーザーが同じコントローラー アクションを呼び出すたびにデータベース クエリを実行しないようにできます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-113">If, on the other hand, you take advantage of the output cache then you can avoid executing a database query every time any user invokes the same controller action.</span></span> <span data-ttu-id="d99dc-114">ビューは、コントローラー アクションから再生成されるのではなく、キャッシュから取得できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-114">The view can be retrieved from the cache instead of being regenerated from the controller action.</span></span> <span data-ttu-id="d99dc-115">キャッシュを使用すると、サーバー上で冗長な作業を行うことを回避できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-115">Caching enables you to avoid performing redundant work on the server.</span></span>

#### <a name="enabling-output-caching"></a><span data-ttu-id="d99dc-116">出力キャッシュの有効化</span><span class="sxs-lookup"><span data-stu-id="d99dc-116">Enabling Output Caching</span></span>

<span data-ttu-id="d99dc-117">出力キャッシュを有効にするには、個々&lt;のコントローラー&gt;アクションまたはコントローラー クラス全体に OutputCache 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-117">You enable output caching by adding an &lt;OutputCache&gt; attribute to either an individual controller action or an entire controller class.</span></span> <span data-ttu-id="d99dc-118">たとえば、リスト 1 のコントローラは Index() という名前のアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-118">For example, the controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="d99dc-119">Index() アクションの出力は 10 秒間キャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-119">The output of the Index() action is cached for 10 seconds.</span></span>

<span data-ttu-id="d99dc-120">**リスト 1 - コントローラ\ホームコントローラー.vb**</span><span class="sxs-lookup"><span data-stu-id="d99dc-120">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]

<span data-ttu-id="d99dc-121">ASP.NET MVC のベータ版では、出力キャッシュは、 のような[http://www.MySite.com/](http://www.mysite.com/)URL では機能しません。</span><span class="sxs-lookup"><span data-stu-id="d99dc-121">In the Beta versions of ASP.NET MVC, output caching does not work for a URL like [http://www.MySite.com/](http://www.mysite.com/).</span></span> <span data-ttu-id="d99dc-122">代わりに、 のような[http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)URL を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d99dc-122">Instead, you must enter a URL like [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index).</span></span>

<span data-ttu-id="d99dc-123">リスト 1 では、Index() アクションの出力は 10 秒間キャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-123">In Listing 1, the output of the Index() action is cached for 10 seconds.</span></span> <span data-ttu-id="d99dc-124">必要に応じて、より長いキャッシュ期間を指定できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-124">If you prefer, you can specify a much longer cache duration.</span></span> <span data-ttu-id="d99dc-125">たとえば、コントローラアクションの出力を 1 日キャッシュする場合、キャッシュ期間として 86400 秒 (60 秒\*60 分\*24 時間) を指定できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-125">For example, if you want to cache the output of a controller action for one day then you can specify a cache duration of 86400 seconds (60 seconds \* 60 minutes \* 24 hours).</span></span>

<span data-ttu-id="d99dc-126">指定した時間だけコンテンツがキャッシュされる保証はありません。</span><span class="sxs-lookup"><span data-stu-id="d99dc-126">There is no guarantee that content will be cached for the amount of time that you specify.</span></span> <span data-ttu-id="d99dc-127">メモリ リソースが少なくなると、キャッシュは自動的にコンテンツの削除を開始します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-127">When memory resources become low, the cache starts evicting content automatically.</span></span>

<span data-ttu-id="d99dc-128">リスト 1 のホーム コントローラーは、リスト 2 のインデックス ビューを返します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-128">The Home controller in Listing 1 returns the Index view in Listing 2.</span></span> <span data-ttu-id="d99dc-129">このビューには特別な何もありません。</span><span class="sxs-lookup"><span data-stu-id="d99dc-129">There is nothing special about this view.</span></span> <span data-ttu-id="d99dc-130">インデックス ビューには、現在の時刻が表示されます (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="d99dc-130">The Index view simply displays the current time (see Figure 1).</span></span>

<span data-ttu-id="d99dc-131">**リスト 2 - ビュー\ホーム\インデックス.aspx**</span><span class="sxs-lookup"><span data-stu-id="d99dc-131">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

<span data-ttu-id="d99dc-132">**図 1 – キャッシュされたインデックス ビュー**</span><span class="sxs-lookup"><span data-stu-id="d99dc-132">**Figure 1 – Cached Index view**</span></span>

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

<span data-ttu-id="d99dc-134">ブラウザのアドレスバーにURL /Home/Indexを入力し、ブラウザの「リフレッシュ/リロード」ボタンを繰り返し押してIndex()アクションを複数回呼び出すと、インデックスビューで表示される時間は10秒間変わりません。</span><span class="sxs-lookup"><span data-stu-id="d99dc-134">If you invoke the Index() action multiple times by entering the URL /Home/Index in the address bar of your browser and hitting the Refresh/Reload button in your browser repeatedly, then the time displayed by the Index view won't change for 10 seconds.</span></span> <span data-ttu-id="d99dc-135">ビューがキャッシュされているため、同じ時刻が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-135">The same time is displayed because the view is cached.</span></span>

<span data-ttu-id="d99dc-136">アプリケーションを訪問するすべてのユーザーに対して同じビューがキャッシュされることを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="d99dc-136">It is important to understand that the same view is cached for everyone who visits your application.</span></span> <span data-ttu-id="d99dc-137">Index() アクションを呼び出したユーザーは、同じキャッシュバージョンのインデックスビューを取得します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-137">Anyone who invokes the Index() action will get the same cached version of the Index view.</span></span> <span data-ttu-id="d99dc-138">つまり、Web サーバーがインデックス ビューを提供するために実行する必要がある作業の量が大幅に削減されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-138">This means that the amount of work that the web server must perform to serve the Index view is dramatically reduced.</span></span>

<span data-ttu-id="d99dc-139">リスト2のビューは、本当に簡単なことをしています。</span><span class="sxs-lookup"><span data-stu-id="d99dc-139">The view in Listing 2 happens to be doing something really simple.</span></span> <span data-ttu-id="d99dc-140">ビューには、現在の時刻が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-140">The view just displays the current time.</span></span> <span data-ttu-id="d99dc-141">ただし、一連のデータベース レコードを表示するビューを簡単にキャッシュできます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-141">However, you could just as easily cache a view that displays a set of database records.</span></span> <span data-ttu-id="d99dc-142">その場合、ビューを返すコントローラー アクションが呼び出されるたびに、データベース レコードのセットをデータベースから取得する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="d99dc-142">In that case, the set of database records would not need to be retrieved from the database each and every time the controller action that returns the view is invoked.</span></span> <span data-ttu-id="d99dc-143">キャッシュを使用すると、Web サーバーとデータベース サーバーの両方で実行する必要のある作業量を減らすことができます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-143">Caching can reduce the amount of work that both your web server and database server must perform.</span></span>

<span data-ttu-id="d99dc-144">MVC ビューでページ&lt;%@ 出力キャッシュ&gt;% ディレクティブを使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="d99dc-144">Don't use the page &lt;%@ OutputCache %&gt; directive in an MVC view.</span></span> <span data-ttu-id="d99dc-145">このディレクティブは Web フォームの世界からはじめ、ASP.NET MVC アプリケーションでは使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="d99dc-145">This directive is bleeding over from the Web Forms world and should not be used in an ASP.NET MVC application.</span></span> 

#### <a name="where-content-is-cached"></a><span data-ttu-id="d99dc-146">コンテンツがキャッシュされる場所</span><span class="sxs-lookup"><span data-stu-id="d99dc-146">Where Content is Cached</span></span>

<span data-ttu-id="d99dc-147">既定では、OutputCache&gt;属性&lt;を使用すると、コンテンツは Web サーバー、プロキシ サーバー、および Web ブラウザーの 3 つの場所にキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-147">By default, when you use the &lt;OutputCache&gt; attribute, content is cached in three locations: the web server, any proxy servers, and the web browser.</span></span> <span data-ttu-id="d99dc-148">OutputCache&gt;属性の場所プロパティを変更することで、コンテンツのキャッシュ場所を正確&lt;に制御できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-148">You can control exactly where content is cached by modifying the Location property of the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="d99dc-149">Location プロパティは、次のいずれかの値に設定できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-149">You can set the Location property to any one of the following values:</span></span>

> <span data-ttu-id="d99dc-150">·任意</span><span class="sxs-lookup"><span data-stu-id="d99dc-150">· Any</span></span>
> 
> <span data-ttu-id="d99dc-151">·クライアント</span><span class="sxs-lookup"><span data-stu-id="d99dc-151">· Client</span></span>
> 
> <span data-ttu-id="d99dc-152">·下流</span><span class="sxs-lookup"><span data-stu-id="d99dc-152">· Downstream</span></span>
> 
> <span data-ttu-id="d99dc-153">·サーバー</span><span class="sxs-lookup"><span data-stu-id="d99dc-153">· Server</span></span>
> 
> <span data-ttu-id="d99dc-154">·なし</span><span class="sxs-lookup"><span data-stu-id="d99dc-154">· None</span></span>
> 
> <span data-ttu-id="d99dc-155">·サーバーとクライアント</span><span class="sxs-lookup"><span data-stu-id="d99dc-155">· ServerAndClient</span></span>

<span data-ttu-id="d99dc-156">既定では、Location プロパティには[任意]という値が設定されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-156">By default, the Location property has the value Any.</span></span> <span data-ttu-id="d99dc-157">ただし、ブラウザー上でのみキャッシュするか、サーバー上でのみキャッシュする必要がある状況もあります。</span><span class="sxs-lookup"><span data-stu-id="d99dc-157">However, there are situations in which you might want to cache only on the browser or only on the server.</span></span> <span data-ttu-id="d99dc-158">たとえば、各ユーザー用にパーソナライズされた情報をキャッシュする場合は、サーバー上の情報をキャッシュしないでください。</span><span class="sxs-lookup"><span data-stu-id="d99dc-158">For example, if you are caching information that is personalized for each user then you should not cache the information on the server.</span></span> <span data-ttu-id="d99dc-159">異なるユーザーに異なる情報を表示する場合は、クライアント上でのみ情報をキャッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d99dc-159">If you are displaying different information to different users then you should cache the information only on the client.</span></span>

<span data-ttu-id="d99dc-160">たとえば、リスト 3 のコントローラは、現在のユーザー名を返す GetName() という名前のアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-160">For example, the controller in Listing 3 exposes an action named GetName() that returns the current user name.</span></span> <span data-ttu-id="d99dc-161">ジャックがウェブサイトにログインし、GetName() アクションを呼び出した場合、アクションは文字列 "Hi Jack" を返します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-161">If Jack logs into the website and invokes the GetName() action then the action returns the string "Hi Jack".</span></span> <span data-ttu-id="d99dc-162">その後、ジルがウェブサイトにログインし、GetName() アクションを呼び出すと、文字列 "Hi Jack" も取得されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-162">If, subsequently, Jill logs into the website and invokes the GetName() action then she also will get the string "Hi Jack".</span></span> <span data-ttu-id="d99dc-163">Jack が最初にコントローラー アクションを呼び出した後、すべてのユーザーの Web サーバーに文字列がキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-163">The string is cached on the web server for all users after Jack initially invokes the controller action.</span></span>

<span data-ttu-id="d99dc-164">**リスト 3 - コントローラ\不正なユーザーコントローラー.vb**</span><span class="sxs-lookup"><span data-stu-id="d99dc-164">**Listing 3 – Controllers\BadUserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

<span data-ttu-id="d99dc-165">一部の場合、リスト 3 のコントローラーは、目的の方法では動作しません。</span><span class="sxs-lookup"><span data-stu-id="d99dc-165">Most likely, the controller in Listing 3 does not work the way that you want.</span></span> <span data-ttu-id="d99dc-166">「ハイジャック」というメッセージをジルに表示したくない。</span><span class="sxs-lookup"><span data-stu-id="d99dc-166">You don't want to display the message "Hi Jack" to Jill.</span></span>

<span data-ttu-id="d99dc-167">パーソナライズされたコンテンツをサーバー キャッシュにキャッシュしないでください。</span><span class="sxs-lookup"><span data-stu-id="d99dc-167">You should never cache personalized content in the server cache.</span></span> <span data-ttu-id="d99dc-168">ただし、パフォーマンスを向上させるために、ブラウザー キャッシュにパーソナライズされたコンテンツをキャッシュする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="d99dc-168">However, you might want to cache the personalized content in the browser cache to improve performance.</span></span> <span data-ttu-id="d99dc-169">ブラウザーでコンテンツをキャッシュし、ユーザーが同じコントローラー アクションを複数回呼び出した場合、そのコンテンツはサーバーではなくブラウザー キャッシュから取得できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-169">If you cache content in the browser, and a user invokes the same controller action multiple times, then the content can be retrieved from the browser cache instead of the server.</span></span>

<span data-ttu-id="d99dc-170">リスト 4 の変更されたコントローラーは、GetName() アクションの出力をキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="d99dc-170">The modified controller in Listing 4 caches the output of the GetName() action.</span></span> <span data-ttu-id="d99dc-171">ただし、コンテンツはブラウザにのみキャッシュされ、サーバーにはキャッシュされません。</span><span class="sxs-lookup"><span data-stu-id="d99dc-171">However, the content is cached only on the browser and not on the server.</span></span> <span data-ttu-id="d99dc-172">このようにして、複数のユーザーが GetName() メソッドを呼び出すと、各ユーザーは自分のユーザー名を取得し、他のユーザーのユーザー名は取得しません。</span><span class="sxs-lookup"><span data-stu-id="d99dc-172">That way, when multiple users invoke the GetName() method, each person gets their own user name and not another person's user name.</span></span>

<span data-ttu-id="d99dc-173">**リスト 4 - コントローラー\ユーザーコントローラー.vb**</span><span class="sxs-lookup"><span data-stu-id="d99dc-173">**Listing 4 – Controllers\UserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

<span data-ttu-id="d99dc-174">リスト 4&lt;の&gt;OutputCache 属性には、値 OutputCacheLocation.Client に設定された場所プロパティが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="d99dc-174">Notice that the &lt;OutputCache&gt; attribute in Listing 4 includes a Location property set to the value OutputCacheLocation.Client.</span></span> <span data-ttu-id="d99dc-175">また&lt;、"&gt;出力キャッシュ" 属性には、NoStore プロパティも含まれます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-175">The &lt;OutputCache&gt; attribute also includes a NoStore property.</span></span> <span data-ttu-id="d99dc-176">NoStore プロパティは、キャッシュされたコンテンツの永続的なコピーを保存しないことをプロキシ サーバーおよびブラウザーに通知するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-176">The NoStore property is used to inform proxy servers and browsers that they should not store a permanent copy of the cached content.</span></span>

#### <a name="varying-the-output-cache"></a><span data-ttu-id="d99dc-177">出力キャッシュの変更</span><span class="sxs-lookup"><span data-stu-id="d99dc-177">Varying the Output Cache</span></span>

<span data-ttu-id="d99dc-178">状況によっては、まったく同じコンテンツのキャッシュバージョンを異なるものにしたい場合があります。</span><span class="sxs-lookup"><span data-stu-id="d99dc-178">In some situations, you might want different cached versions of the very same content.</span></span> <span data-ttu-id="d99dc-179">たとえば、マスター/詳細ページを作成しているとします。</span><span class="sxs-lookup"><span data-stu-id="d99dc-179">Imagine, for example, that you are creating a master/detail page.</span></span> <span data-ttu-id="d99dc-180">マスター ページに、映画タイトルの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-180">The master page displays a list of movie titles.</span></span> <span data-ttu-id="d99dc-181">タイトルをクリックすると、選択したムービーの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-181">When you click a title, you get details for the selected movie.</span></span>

<span data-ttu-id="d99dc-182">詳細ページをキャッシュすると、クリックしたムービーに関係なく、同じムービーの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-182">If you cache the details page, then the details for the same movie will be displayed no matter which movie you click.</span></span> <span data-ttu-id="d99dc-183">最初のユーザーが選択した最初のムービーは、今後のすべてのユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-183">The first movie selected by the first user will be displayed to all future users.</span></span>

<span data-ttu-id="d99dc-184">この問題を解決するには、出力キャッシュ&lt;&gt;属性の VaryByParam プロパティを利用します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-184">You can fix this problem by taking advantage of the VaryByParam property of the &lt;OutputCache&gt; attribute.</span></span> <span data-ttu-id="d99dc-185">このプロパティを使用すると、フォーム パラメーターまたはクエリ文字列パラメーターが異なる場合に、まったく同じコンテンツの異なるキャッシュ バージョンを作成できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-185">This property enables you to create different cached versions of the very same content when a form parameter or query string parameter varies.</span></span>

<span data-ttu-id="d99dc-186">たとえば、リスト 5 のコントローラは、Master() と Details() という名前の 2 つのアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-186">For example, the controller in Listing 5 exposes two actions named Master() and Details().</span></span> <span data-ttu-id="d99dc-187">Master() アクションはムービータイトルのリストを返し、Details() アクションは選択したムービーの詳細を返します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-187">The Master() action returns a list of movie titles and the Details() action returns the details for the selected movie.</span></span>

<span data-ttu-id="d99dc-188">**リスト 5 - コントローラー\映画コントローラー.vb**</span><span class="sxs-lookup"><span data-stu-id="d99dc-188">**Listing 5 – Controllers\MoviesController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

<span data-ttu-id="d99dc-189">Master() アクションには、値 "none" の VaryByParam プロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-189">The Master() action includes a VaryByParam property with the value "none".</span></span> <span data-ttu-id="d99dc-190">Master() アクションが呼び出されると、同じキャッシュバージョンのマスタービューが返されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-190">When the Master() action is invoked, the same cached version of the Master view is returned.</span></span> <span data-ttu-id="d99dc-191">フォーム パラメーターまたはクエリ文字列パラメーターは無視されます (図 2 を参照)。</span><span class="sxs-lookup"><span data-stu-id="d99dc-191">Any form parameters or query string parameters are ignored (see Figure 2).</span></span>

<span data-ttu-id="d99dc-192">**図 2 – /映画/マスター ビュー**</span><span class="sxs-lookup"><span data-stu-id="d99dc-192">**Figure 2 – The /Movies/Master view**</span></span>

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

<span data-ttu-id="d99dc-194">**図 3 – /映画/詳細ビュー**</span><span class="sxs-lookup"><span data-stu-id="d99dc-194">**Figure 3 – The /Movies/Details view**</span></span>

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

<span data-ttu-id="d99dc-196">Details() アクションには、値 "Id" を持つ VaryByParam プロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-196">The Details() action includes a VaryByParam property with the value "Id".</span></span> <span data-ttu-id="d99dc-197">Id パラメーターの異なる値がコントローラーアクションに渡されると、キャッシュされた別のバージョンの詳細ビューが生成されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-197">When different values of the Id parameter are passed to the controller action, different cached versions of the Details view are generated.</span></span>

<span data-ttu-id="d99dc-198">VaryByParam プロパティを使用すると、キャッシュが増え、それ以下ではなくなることを理解しておくことが重要です。</span><span class="sxs-lookup"><span data-stu-id="d99dc-198">It is important to understand that using the VaryByParam property results in more caching and not less.</span></span> <span data-ttu-id="d99dc-199">Id パラメーターのバージョンごとに異なるキャッシュされたバージョンの詳細ビューが作成されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-199">A different cached version of the Details view is created for each different version of the Id parameter.</span></span>

<span data-ttu-id="d99dc-200">次の値を設定できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-200">You can set the VaryByParam property to the following values:</span></span>

> <span data-ttu-id="d99dc-201">\*= フォームまたはクエリ文字列パラメーターが変化する場合は、別のキャッシュ バージョンを作成します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-201">\* = Create a different cached version whenever a form or query string parameter varies.</span></span>
> 
> <span data-ttu-id="d99dc-202">none = 異なるキャッシュ バージョンを作成しない</span><span class="sxs-lookup"><span data-stu-id="d99dc-202">none = Never create different cached versions</span></span>
> 
> <span data-ttu-id="d99dc-203">パラメーターのセミコロン リスト = リスト内のフォームまたはクエリ文字列パラメーターが変化する場合は、異なるキャッシュ バージョンを作成します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-203">Semicolon list of parameters = Create different cached versions whenever any of the form or query string parameters in the list varies</span></span>

#### <a name="creating-a-cache-profile"></a><span data-ttu-id="d99dc-204">キャッシュ プロファイルの作成</span><span class="sxs-lookup"><span data-stu-id="d99dc-204">Creating a Cache Profile</span></span>

<span data-ttu-id="d99dc-205">OutputCache&lt;&gt;属性のプロパティを変更して出力キャッシュ プロパティを構成する代わりに、Web 構成 (web.config) ファイルにキャッシュ プロファイルを作成できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-205">As an alternative to configuring output cache properties by modifying properties of the &lt;OutputCache&gt; attribute, you can create a cache profile in the web configuration (web.config) file.</span></span> <span data-ttu-id="d99dc-206">Web 構成ファイルにキャッシュ プロファイルを作成すると、いくつかの重要な利点があります。</span><span class="sxs-lookup"><span data-stu-id="d99dc-206">Creating a cache profile in the web configuration file offers a couple of important advantages.</span></span>

<span data-ttu-id="d99dc-207">まず、Web 構成ファイルで出力キャッシュを構成することで、コントローラーアクションがコンテンツを 1 か所にキャッシュする方法を制御できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-207">First, by configuring output caching in the web configuration file, you can control how controller actions cache content in one central location.</span></span> <span data-ttu-id="d99dc-208">1 つのキャッシュ プロファイルを作成し、そのプロファイルを複数のコントローラまたはコントローラのアクションに適用できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-208">You can create one cache profile and apply the profile to several controllers or controller actions.</span></span>

<span data-ttu-id="d99dc-209">次に、アプリケーションを再コンパイルせずに Web 構成ファイルを変更できます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-209">Second, you can modify the web configuration file without recompiling your application.</span></span> <span data-ttu-id="d99dc-210">既に実稼働環境にデプロイされているアプリケーションのキャッシュを無効にする必要がある場合は、Web 構成ファイルで定義されているキャッシュ プロファイルを変更するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-210">If you need to disable caching for an application that has already been deployed to production, then you can simply modify the cache profiles defined in the web configuration file.</span></span> <span data-ttu-id="d99dc-211">Web 構成ファイルに対する変更は自動的に検出され、適用されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-211">Any changes to the web configuration file will be detected automatically and applied.</span></span>

<span data-ttu-id="d99dc-212">たとえば、リスト&lt;6&gt;のキャッシュ Web 構成セクションでは、Cache1Hour という名前のキャッシュ プロファイルを定義します。</span><span class="sxs-lookup"><span data-stu-id="d99dc-212">For example, the &lt;caching&gt; web configuration section in Listing 6 defines a cache profile named Cache1Hour.</span></span> <span data-ttu-id="d99dc-213">キャッシュ&lt;&gt;セクションは、Web&lt;構成ファイルの&gt;system.web セクション内に表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d99dc-213">The &lt;caching&gt; section must appear within the &lt;system.web&gt; section of a web configuration file.</span></span>

<span data-ttu-id="d99dc-214">**リスト 6 - web.config のキャッシュ セクション**</span><span class="sxs-lookup"><span data-stu-id="d99dc-214">**Listing 6 – Caching section for web.config**</span></span>

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

<span data-ttu-id="d99dc-215">リスト 7 のコントローラーは、OutputCache&lt;&gt;属性を使用して、Cache1Hour プロファイルをコントローラー アクションに適用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d99dc-215">The controller in Listing 7 illustrates how you can apply the Cache1Hour profile to a controller action with the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="d99dc-216">**リスト 7 - コントローラ\プロファイルコントローラー.vb**</span><span class="sxs-lookup"><span data-stu-id="d99dc-216">**Listing 7 – Controllers\ProfileController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

<span data-ttu-id="d99dc-217">リスト 7 でコントローラによって公開される Index() アクションを呼び出すと、同じ時刻が 1 時間返されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-217">If you invoke the Index() action exposed by the controller in Listing 7 then the same time will be returned for 1 hour.</span></span>

#### <a name="summary"></a><span data-ttu-id="d99dc-218">まとめ</span><span class="sxs-lookup"><span data-stu-id="d99dc-218">Summary</span></span>

<span data-ttu-id="d99dc-219">出力キャッシュを使用すると、ASP.NET MVC アプリケーションのパフォーマンスを大幅に向上させる非常に簡単な方法が提供されます。</span><span class="sxs-lookup"><span data-stu-id="d99dc-219">Output caching provides you with a very easy method of dramatically improving the performance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="d99dc-220">このチュートリアルでは、OutputCache&lt;&gt;属性を使用してコントローラー アクションの出力をキャッシュする方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="d99dc-220">In this tutorial, you learned how to use the &lt;OutputCache&gt; attribute to cache the output of controller actions.</span></span> <span data-ttu-id="d99dc-221">また、Duration プロパティや VaryByParam プロパティなどの&lt;OutputCache&gt;属性のプロパティを変更して、コンテンツのキャッシュ方法を変更する方法についても説明しました。</span><span class="sxs-lookup"><span data-stu-id="d99dc-221">You also learned how to modify properties of the &lt;OutputCache&gt; attribute such as the Duration and VaryByParam properties to modify how content gets cached.</span></span> <span data-ttu-id="d99dc-222">最後に、Web 構成ファイルでキャッシュ プロファイルを定義する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="d99dc-222">Finally, you learned how to define cache profiles in the web configuration file.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d99dc-223">[前へ](understanding-action-filters-vb.md)
> [次へ](adding-dynamic-content-to-a-cached-page-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d99dc-223">[Previous](understanding-action-filters-vb.md)
[Next](adding-dynamic-content-to-a-cached-page-vb.md)</span></span>
