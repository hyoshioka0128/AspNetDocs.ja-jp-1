---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: 評価コントロールを作成 (c#) |Microsoft Docs
author: wenz
description: 多くの web サイトから e コマース、コミュニティ サイトにユーザーは、レート記事や項目を提供します。 これは、通常コーディング上の工夫が必要ですが、ので、.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 1fde131086d4fb29c499f7f7c6281153c2766166
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65125058"
---
# <a name="creating-a-rating-control-c"></a><span data-ttu-id="3219b-104">評価コントロールを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="3219b-104">Creating a Rating Control (C#)</span></span>

<span data-ttu-id="3219b-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="3219b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3219b-106">[コードのダウンロード](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip)または[PDF のダウンロード](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3219b-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="3219b-107">多くの web サイトから e コマース、コミュニティ サイトにユーザーは、レート記事や項目を提供します。</span><span class="sxs-lookup"><span data-stu-id="3219b-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="3219b-108">通常はコーディング上の工夫が必要ですが、Control Toolkit、破棄する必要は。</span><span class="sxs-lookup"><span data-stu-id="3219b-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="overview"></a><span data-ttu-id="3219b-109">概要</span><span class="sxs-lookup"><span data-stu-id="3219b-109">Overview</span></span>

<span data-ttu-id="3219b-110">多くの web サイトから e コマース、コミュニティ サイトにユーザーは、レート記事や項目を提供します。</span><span class="sxs-lookup"><span data-stu-id="3219b-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="3219b-111">通常はコーディング上の工夫が必要ですが、Control Toolkit、破棄する必要は。</span><span class="sxs-lookup"><span data-stu-id="3219b-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="3219b-112">手順</span><span class="sxs-lookup"><span data-stu-id="3219b-112">Steps</span></span>

<span data-ttu-id="3219b-113">最初に、すべての必要な (少なくとも) 2 つのイメージ: 塗りつぶしのいずれかの項目の評価、および評価が空の項目に 1 つ。</span><span class="sxs-lookup"><span data-stu-id="3219b-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="3219b-114">評価の項目は、通常、星または、スマイリーです。</span><span class="sxs-lookup"><span data-stu-id="3219b-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="3219b-115">このシナリオでは、このチュートリアルでは、ソース コードのダウンロードの一部として 3 つのファイル、smiley.png と empty.png およびスマイリー done.png を検索します。</span><span class="sxs-lookup"><span data-stu-id="3219b-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="3219b-116">次に、新しい ASP.NET ファイルを作成し、追加の開始、`ScriptManager`コントロールを。</span><span class="sxs-lookup"><span data-stu-id="3219b-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="3219b-117">次に、追加、 `Rating` ASP.NET AJAX Control toolkit コントロール。</span><span class="sxs-lookup"><span data-stu-id="3219b-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="3219b-118">次の属性は、この例で設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3219b-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="3219b-119">`CurrentRating` 使用する初期の評価</span><span class="sxs-lookup"><span data-stu-id="3219b-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="3219b-120">`MaxRating` 最大年齢区分</span><span class="sxs-lookup"><span data-stu-id="3219b-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="3219b-121">`EmptyStarCssClass` 評価のアイテム (star) は空にするときに使用する CSS クラス</span><span class="sxs-lookup"><span data-stu-id="3219b-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="3219b-122">`FilledStarCssClass` 評価の項目 (star) は、入力時に使用する CSS クラス</span><span class="sxs-lookup"><span data-stu-id="3219b-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="3219b-123">`StarCssClass` 表示される統計に使用する CSS クラス</span><span class="sxs-lookup"><span data-stu-id="3219b-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="3219b-124">`WaitingStarCssClass` 星の評価がサーバーに送信されるときに使用する CSS クラス</span><span class="sxs-lookup"><span data-stu-id="3219b-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="3219b-125">5 つで評価コントロールが作成されるマークアップは、次を [なし] が記入されます最初の項目 (スマイリー)。</span><span class="sxs-lookup"><span data-stu-id="3219b-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="3219b-126">参照されている 3 つの CSS クラス必要があります、適切なイメージ ファイルを表示するのには簡単に CSS を使用して実行できます。</span><span class="sxs-lookup"><span data-stu-id="3219b-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="3219b-127">3 つのイメージの高さと幅を指定することは、それ以外の場合、表示を少し messed なります確認します。</span><span class="sxs-lookup"><span data-stu-id="3219b-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="3219b-128">最後に、評価の結果する必要がある、ユーザーに表示されます (または、少なくともデータベースに保存)。</span><span class="sxs-lookup"><span data-stu-id="3219b-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="3219b-129">その評価フォームをサーバーにポストバックするためには、テキスト メッセージと送信ボタンの出力のラベルを追加します。</span><span class="sxs-lookup"><span data-stu-id="3219b-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="3219b-130">サーバー側のコードでアクセスを使用して評価コントロール、`ID`し、アクセス、 `CurrentRating` 0 ~ 5 の値の例では、評価を選択した項目の数であるプロパティ。</span><span class="sxs-lookup"><span data-stu-id="3219b-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="3219b-131">ページを保存し、お使いのブラウザーに読み込みます。</span><span class="sxs-lookup"><span data-stu-id="3219b-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="3219b-132">(最初は空) の評価の項目をポイントすると、JavaScript の効果が発生します。評価の変更。</span><span class="sxs-lookup"><span data-stu-id="3219b-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="3219b-133">一連の星をクリックすると、現在の評価が保持されます。</span><span class="sxs-lookup"><span data-stu-id="3219b-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="3219b-134">最後に、フォームを送信するときに、サーバー側コードは、選択した評価を出力します。</span><span class="sxs-lookup"><span data-stu-id="3219b-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>

<span data-ttu-id="3219b-135">[![最小限のコードで評価システムを作成します。](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3219b-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="3219b-136">最小限のコードで評価システムを作成する ([フルサイズの画像を表示する をクリックします](creating-a-rating-control-cs/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="3219b-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3219b-137">次へ</span><span class="sxs-lookup"><span data-stu-id="3219b-137">Next</span></span>](creating-a-rating-control-vb.md)
