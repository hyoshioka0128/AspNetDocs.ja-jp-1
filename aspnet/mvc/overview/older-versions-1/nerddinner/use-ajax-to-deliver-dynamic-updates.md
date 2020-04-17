---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: AJAX を使用して動的更新を配信する |マイクロソフトドキュメント
author: rick-anderson
description: ステップ 10 は、ディナーの詳細に統合された Ajax ベースのアプローチを使用して、RSVP にログインしたユーザーがディナーに参加するサポートを実装します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541248"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="86a03-103">AJAX を使用し、動的更新を配信する</span><span class="sxs-lookup"><span data-stu-id="86a03-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="86a03-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="86a03-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="86a03-105">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="86a03-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="86a03-106">これは、MVC 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)のステップ 10 ASP.NETです。</span><span class="sxs-lookup"><span data-stu-id="86a03-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="86a03-107">ステップ 10 では、ディナーの詳細ページに統合された Ajax ベースのアプローチを使用して、RSVP にログインしたユーザーのサポートを実装します。</span><span class="sxs-lookup"><span data-stu-id="86a03-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="86a03-108">mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="86a03-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="86a03-109">NerdDinner ステップ 10: RsAP を有効にする AJAX が受け入れる</span><span class="sxs-lookup"><span data-stu-id="86a03-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="86a03-110">それでは、RSVPにログインしているユーザーが夕食会に出席することに興味を持つサポートを実装しましょう。</span><span class="sxs-lookup"><span data-stu-id="86a03-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="86a03-111">夕食の詳細ページに統合された AJAX ベースのアプローチを使用して、これを有効にします。</span><span class="sxs-lookup"><span data-stu-id="86a03-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="86a03-112">ユーザーが RSVP'd であるかどうかを示す</span><span class="sxs-lookup"><span data-stu-id="86a03-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="86a03-113">ユーザーは */Dinners/Details/[id]* URL にアクセスして、特定のディナーの詳細を確認できます。</span><span class="sxs-lookup"><span data-stu-id="86a03-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="86a03-114">Details() アクションメソッドは次のように実装されています。</span><span class="sxs-lookup"><span data-stu-id="86a03-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="86a03-115">RSVP サポートを実装する最初のステップは、(以前に構築したDinner.cs部分クラス内で) Dinner オブジェクトに "IsUserRegistered(ユーザー名)" ヘルパー メソッドを追加することです。</span><span class="sxs-lookup"><span data-stu-id="86a03-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="86a03-116">このヘルパー メソッドは、ユーザーが現在、Dinner の RSVP の有無に応じて true または false を返します。</span><span class="sxs-lookup"><span data-stu-id="86a03-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="86a03-117">その後、Details.aspx ビュー テンプレートに次のコードを追加して、ユーザーがイベントに登録されているかどうかを示す適切なメッセージを表示できます。</span><span class="sxs-lookup"><span data-stu-id="86a03-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="86a03-118">そして今、ユーザーが夕食を訪問すると、彼らはこのメッセージが表示されます:</span><span class="sxs-lookup"><span data-stu-id="86a03-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="86a03-119">そして、彼らは夕食を訪問すると、彼らは次のメッセージが表示されますのために登録されていません:</span><span class="sxs-lookup"><span data-stu-id="86a03-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="86a03-120">登録アクション メソッドの実装</span><span class="sxs-lookup"><span data-stu-id="86a03-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="86a03-121">ここで、詳細ページから、ディナーに RSVP にユーザーを有効にするために必要な機能を追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="86a03-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="86a03-122">これを実装するには、\Controllersディレクトリを右クリックし、&gt;コントローラメニューコマンドを選択して、新しい "RSVPController"クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="86a03-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="86a03-123">新しい RSVPController クラス内に、引数として Dinner の ID を取得し、適切な Dinner オブジェクトを取得し、ログインしているユーザーが現在登録しているユーザーの一覧に含まれているかどうかを確認し、RSVP オブジェクトを追加しない場合は、そのクラスに "Register" アクション メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="86a03-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="86a03-124">アクションメソッドの出力として単純な文字列を返す方法の上に注意してください。</span><span class="sxs-lookup"><span data-stu-id="86a03-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="86a03-125">このメッセージをビューテンプレートに埋め込むこともできますが、とても小さいため、コントローラの基本クラスで Content() ヘルパーメソッドを使用し、上記のような文字列メッセージを返します。</span><span class="sxs-lookup"><span data-stu-id="86a03-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="86a03-126">AJAX を使用して RSVPForEvent アクション メソッドを呼び出す</span><span class="sxs-lookup"><span data-stu-id="86a03-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="86a03-127">AJAX を使用して、詳細ビューから Register アクション メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="86a03-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="86a03-128">これを実装することは非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="86a03-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="86a03-129">最初に、2 つのスクリプト ライブラリ参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="86a03-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="86a03-130">最初のライブラリは、AJAX クライアント側スクリプト ライブラリASP.NETコアを参照します。</span><span class="sxs-lookup"><span data-stu-id="86a03-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="86a03-131">このファイルは約 24 k のサイズ (圧縮) で、コア クライアント側の AJAX 機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="86a03-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="86a03-132">2 番目のライブラリには、MVC の組み込みの AJAX ヘルパー メソッド (まもなく使用) ASP.NET統合するユーティリティ関数が含まれています。</span><span class="sxs-lookup"><span data-stu-id="86a03-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="86a03-133">その後、先ほど追加したビュー テンプレート コードを更新して、"このイベントに登録されていません" というメッセージを出力する代わりに、プッシュされたときに RSVPForEvent アクション メソッドを呼び出す AJAX 呼び出しを実行するリンクをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="86a03-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="86a03-134">上記で使用した Ajax.ActionLink() ヘルパー メソッドは、MVC ASP.NET組み込まれており、標準ナビゲーションを実行する代わりに、リンクがクリックされたときにアクション メソッドに AJAX 呼び出しを行う点を除いて、Html.ActionLink() ヘルパー メソッドに似ています。</span><span class="sxs-lookup"><span data-stu-id="86a03-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="86a03-135">上記では、「RSVP」コントローラ上の"登録"アクションメソッドを呼び出し、それに「id」パラメータとしてDinnerIDを渡しています。</span><span class="sxs-lookup"><span data-stu-id="86a03-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="86a03-136">最後に渡す AjaxOptions パラメータは、アクション メソッドから返されたコンテンツを取得し、ID が&lt;&gt; "rsvpmsg" であるページの HTML div 要素を更新することを示します。</span><span class="sxs-lookup"><span data-stu-id="86a03-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="86a03-137">そして今、ユーザーがディナーを閲覧すると、彼らはまだ登録されていません、彼らはそれのためにRSVPへのリンクが表示されます:</span><span class="sxs-lookup"><span data-stu-id="86a03-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="86a03-138">彼らは「このイベントのRSVP」リンクをクリックすると、RSVPコントローラ上の登録アクションメソッドにAJAX呼び出しを行い、それが完了すると、次のような更新されたメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="86a03-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="86a03-139">この AJAX 呼び出しを行う際に関係するネットワーク帯域幅とトラフィックは、実際には軽量です。</span><span class="sxs-lookup"><span data-stu-id="86a03-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="86a03-140">ユーザーが [このイベントの RSVP] リンクをクリックすると、次のような */Dinners/Register/1* URL に対して、小さな HTTP POST ネットワーク要求が送信されます。</span><span class="sxs-lookup"><span data-stu-id="86a03-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="86a03-141">そして、私たちの登録アクションメソッドからの応答は、単純です:</span><span class="sxs-lookup"><span data-stu-id="86a03-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="86a03-142">この軽量の呼び出しは高速であり、低速のネットワークでも動作します。</span><span class="sxs-lookup"><span data-stu-id="86a03-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="86a03-143">jQuery アニメーションの追加</span><span class="sxs-lookup"><span data-stu-id="86a03-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="86a03-144">実装した AJAX 機能は、適切かつ高速に機能します。</span><span class="sxs-lookup"><span data-stu-id="86a03-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="86a03-145">しかし、RSVP リンクが新しいテキストに置き換えられたことにユーザーが気付かないほど高速に発生する場合があります。</span><span class="sxs-lookup"><span data-stu-id="86a03-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="86a03-146">結果をもう少し明確にするために、更新メッセージに注意を引く簡単なアニメーションを追加できます。</span><span class="sxs-lookup"><span data-stu-id="86a03-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="86a03-147">既定のASP.NET MVC プロジェクト テンプレートには、優れた (そして非常に人気のある) オープンソースの JavaScript ライブラリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="86a03-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="86a03-148">jQuery は、素敵な HTML DOM の選択やエフェクトライブラリなど、多くの機能を提供します。</span><span class="sxs-lookup"><span data-stu-id="86a03-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="86a03-149">jQuery を使用するには、まずスクリプト参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="86a03-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="86a03-150">サイト内のさまざまな場所で jQuery を使用するため、Site.master マスター ページ ファイル内にスクリプト参照を追加して、すべてのページで使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="86a03-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="86a03-151">*ヒント: Vs 2008 SP1 用の JavaScript インテリセンス修正プログラムがインストールされていることを確認してください。ダウンロードは次のどこからでも行うことができます。http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="86a03-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="86a03-152">JQuery を使用して記述されたコードは、CSS セレクタを使用して 1 つ以上の HTML 要素を取得する、グローバルな "$()" JavaScript メソッドを使用することがよくあります。</span><span class="sxs-lookup"><span data-stu-id="86a03-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="86a03-153">たとえば *、$("#rsvpmsg")は*rsvpmsg の ID を持つ HTML 要素を選択し *、$(".something") は*"何か" CSS クラス名を持つすべての要素を選択します。</span><span class="sxs-lookup"><span data-stu-id="86a03-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="86a03-154">また、次のようなセレクタークエリを使用して、「チェックされたすべてのラジオボタンを返す」のようなより高度なクエリを書くことができます: *@type$("input[@checked=radio][])*</span><span class="sxs-lookup"><span data-stu-id="86a03-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="86a03-155">要素を選択したら、メソッドを呼び出して、要素を非表示にするようなアクションを実行できます *#rsvpmsg。*</span><span class="sxs-lookup"><span data-stu-id="86a03-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="86a03-156">RSVP のシナリオでは、"rsvpmsg" div&lt;&gt;を選択し、そのテキスト コンテンツのサイズをアニメーション化する"AnimateRSVPMessage"という名前の単純な JavaScript 関数を定義します。</span><span class="sxs-lookup"><span data-stu-id="86a03-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="86a03-157">次のコードは、テキストを小さく開始し、400 ミリ秒の時間枠を超えて増加させます。</span><span class="sxs-lookup"><span data-stu-id="86a03-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="86a03-158">AJAX 呼び出しが正常に完了した後に呼び出されるこの JavaScript 関数を、Ajax.ActionLink() ヘルパー メソッドに渡して (AjaxOptions "OnSuccess" イベント プロパティを使用して) ワイヤアップできます。</span><span class="sxs-lookup"><span data-stu-id="86a03-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="86a03-159">そして今、「このイベントのRSVP」リンクがクリックされ、AJAXコールが正常に完了すると、送信されたコンテンツメッセージはアニメーション化され、大きくなります。</span><span class="sxs-lookup"><span data-stu-id="86a03-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="86a03-160">"OnSuccess" イベントを提供するだけでなく、AjaxOptions オブジェクトは、処理できる OnBegin イベント、OnFailure イベント、および OnComplete イベントを公開します。</span><span class="sxs-lookup"><span data-stu-id="86a03-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="86a03-161">クリーンアップ - RSVP 部分ビューのリファクタリング</span><span class="sxs-lookup"><span data-stu-id="86a03-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="86a03-162">詳細ビュー テンプレートは少し長くなり始めていますが、残業は少し理解しにくくなります。</span><span class="sxs-lookup"><span data-stu-id="86a03-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="86a03-163">コードの読みやすさを向上させるために、詳細ページのすべての RSVP ビュー コードをカプセル化する部分ビュー RSVPStatus.ascx を作成して完了します。</span><span class="sxs-lookup"><span data-stu-id="86a03-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="86a03-164">これを行うには、\Views\Dinners フォルダを右クリックし、[追加-&gt;表示] メニュー コマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="86a03-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="86a03-165">厳密に型指定された ViewModel として Dinner オブジェクトを取得します。</span><span class="sxs-lookup"><span data-stu-id="86a03-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="86a03-166">その後、Details.aspx ビューから RSVP コンテンツをコピー/貼り付けることができます。</span><span class="sxs-lookup"><span data-stu-id="86a03-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="86a03-167">これを完了したら、編集と削除のリンク ビュー コードをカプセル化する別の部分ビュー (EditAndDeleteLinks.ascx) も作成しましょう。</span><span class="sxs-lookup"><span data-stu-id="86a03-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="86a03-168">また、Dinner オブジェクトを厳密に型指定された ViewModel として取得し、Details.aspx ビューから編集と削除のロジックをコピー/貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="86a03-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="86a03-169">詳細ビュー テンプレートには、次の 2 つの Html.RenderPartial() メソッド呼び出しを下部に含めることができます。</span><span class="sxs-lookup"><span data-stu-id="86a03-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="86a03-170">これにより、コードの読み取りや保守がきれいになります。</span><span class="sxs-lookup"><span data-stu-id="86a03-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="86a03-171">次の手順</span><span class="sxs-lookup"><span data-stu-id="86a03-171">Next Step</span></span>

<span data-ttu-id="86a03-172">ここで、AJAX をさらに活用して、アプリケーションに対話的なマッピングサポートを追加する方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="86a03-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="86a03-173">[前へ](secure-applications-using-authentication-and-authorization.md)
> [次へ](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="86a03-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
