---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: アニメーションをトリガーするもう 1 つコントロール (VB) |Microsoft Docs
author: wenz
description: アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。 一般に、起動する.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: cc27e44ae42865eebbf67da69dbe1aa43a57a4d7
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65128170"
---
# <a name="triggering-an-animation-in-another-control-vb"></a><span data-ttu-id="7e4c6-104">別のコントロールでアニメーションをトリガーする (VB)</span><span class="sxs-lookup"><span data-stu-id="7e4c6-104">Triggering an Animation in another Control (VB)</span></span>

<span data-ttu-id="7e4c6-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7e4c6-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7e4c6-106">[コードのダウンロード](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip)または[PDF のダウンロード](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7e4c6-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span></span>

> <span data-ttu-id="7e4c6-107">アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7e4c6-108">一般に、アニメーションの起動は、同じコントロールでのユーザー操作によってトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-108">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="7e4c6-109">ただしも別のコントロールを 1 つのコントロールと、アニメーションと対話することです。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-109">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="overview"></a><span data-ttu-id="7e4c6-110">概要</span><span class="sxs-lookup"><span data-stu-id="7e4c6-110">Overview</span></span>

<span data-ttu-id="7e4c6-111">アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7e4c6-112">一般に、アニメーションの起動は、同じコントロールでのユーザー操作によってトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-112">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="7e4c6-113">ただしも別のコントロールを 1 つのコントロールと、アニメーションと対話することです。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-113">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="steps"></a><span data-ttu-id="7e4c6-114">手順</span><span class="sxs-lookup"><span data-stu-id="7e4c6-114">Steps</span></span>

<span data-ttu-id="7e4c6-115">まず、含める、 `ScriptManager` ; ページで次に、ASP.NET AJAX ライブラリが読み込まれる Control Toolkit を使用すること。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

<span data-ttu-id="7e4c6-116">次のようなテキストのパネルに、アニメーションが適用されます。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-116">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

<span data-ttu-id="7e4c6-117">パネルの関連付けられている CSS クラス、便利な背景色を定義し、パネルの固定幅の設定も。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-117">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

<span data-ttu-id="7e4c6-118">パネルをアニメーション化を開始するには、HTML ボタンが使用されます。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-118">In order to start animating the panel, an HTML button is used.</span></span> <span data-ttu-id="7e4c6-119">なお`<input type="button" />`をお勧め`<asp:Button />`ためたくないポストバック、ユーザーがそのボタンをクリックするとにします。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-119">Note that `<input type="button" />` is favoured over `<asp:Button />` since we do not want a postback when the user clicks on that button.</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

<span data-ttu-id="7e4c6-120">次に、追加、 `AnimationExtender` 、ページを提供する、 `ID`、`TargetControlID`属性と、変更を加える`runat="server"`。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-120">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`.</span></span> <span data-ttu-id="7e4c6-121">設定することが重要`TargetControlID`ボタン (アニメーションをトリガーする要素) の ID に、パネル (アニメーション化されている要素) の ID にありません</span><span class="sxs-lookup"><span data-stu-id="7e4c6-121">It is important to set `TargetControlID` to the ID of the button (the element triggering the animation), not to the ID of the panel (the element being animated)</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

<span data-ttu-id="7e4c6-122">内で、`<Animations>`ノードで、通常どおりの場所のアニメーション。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-122">Within the `<Animations>` node, place animations as usual.</span></span> <span data-ttu-id="7e4c6-123">パネルを変更するには、するには、ボタンの設定、`AnimationTarget`内のすべてのアニメーション要素の属性`AnimationExtender`します。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-123">In order to make them change the panel, not the button, set the `AnimationTarget` attribute for every animation element within `AnimationExtender`.</span></span> <span data-ttu-id="7e4c6-124">値は、`AnimationTarget`パネルの ID をもちろんです。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-124">The value for `AnimationTarget` is the ID of the panel, of course.</span></span> <span data-ttu-id="7e4c6-125">そうすること、アニメーションにトリガーを起動するボタンではなく、パネルで発生します。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-125">That way, the animations happen with the panel, not with the triggering button.</span></span> <span data-ttu-id="7e4c6-126">ここでは、`AnimationExtender`このシナリオのマークアップ。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-126">Here is the `AnimationExtender` markup for this scenario:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

<span data-ttu-id="7e4c6-127">個々 のアニメーションを表示する特別な順序に注意してください。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-127">Note the special order in which the individual animations appear.</span></span> <span data-ttu-id="7e4c6-128">まず、アニメーションの実行後に、ボタンが非アクティブ化を取得します。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-128">First of all, the button gets deactivated once the animation runs.</span></span> <span data-ttu-id="7e4c6-129">あるためありません`AnimationTarget`属性、`<EnableAction>`要素をこのアニメーションは、元のコントロールに適用される: ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-129">Since there is no `AnimationTarget` attribute in the `<EnableAction>` element, this animation is applied to the originating control: the button.</span></span> <span data-ttu-id="7e4c6-130">次の 2 つのアニメーションのステップを並列で実行されます (`<Parallel>`要素)。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-130">The next two animation steps shall be carried out in parallel (`<Parallel>` element).</span></span> <span data-ttu-id="7e4c6-131">両方が、`AnimationTarget`属性に設定`"Panel1"`、そのため、パネル、[not] ボタンをアニメーション化します。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-131">Both have their `AnimationTarget` attributes set to `"Panel1"`, thus animating the panel, not the button.</span></span>

<span data-ttu-id="7e4c6-132">[![パネル アニメーションを開始するボタンにマウスのクリック](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7e4c6-132">[![A mouse click on the button starts the panel animation](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="7e4c6-133">ボタンをマウスのクリックは、パネルのアニメーションを開始 ([フルサイズの画像を表示する をクリックします](triggering-an-animation-in-another-control-vb/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="7e4c6-133">A mouse click on the button starts the panel animation ([Click to view full-size image](triggering-an-animation-in-another-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7e4c6-134">[前へ](disabling-actions-during-animation-vb.md)
> [次へ](modifying-animations-from-the-server-side-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7e4c6-134">[Previous](disabling-actions-during-animation-vb.md)
[Next](modifying-animations-from-the-server-side-vb.md)</span></span>
