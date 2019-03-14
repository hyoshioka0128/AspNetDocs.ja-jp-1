---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: UpdatePanel コントロール (VB) をアニメーション化 |Microsoft Docs
author: wenz
description: アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。 内容として、.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 797ee37eb440bed261403aa0e1b68f38d3cd8ef9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054919"
---
<a name="animating-an-updatepanel-control-vb"></a><span data-ttu-id="b6d8e-104">UpdatePanel コントロールをアニメーションにする (VB)</span><span class="sxs-lookup"><span data-stu-id="b6d8e-104">Animating an UpdatePanel Control (VB)</span></span>
====================
<span data-ttu-id="b6d8e-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b6d8e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b6d8e-106">[コードのダウンロード](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip)または[PDF のダウンロード](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="b6d8e-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span></span>

> <span data-ttu-id="b6d8e-107">アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b6d8e-108">UpdatePanel の内容は、の特別なエクステンダーには、アニメーション フレームワークに大きく依存しているが存在します。UpdatePanelAnimation します。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="b6d8e-109">このチュートリアルでは、UpdatePanel のようなアニメーションを設定する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>


## <a name="overview"></a><span data-ttu-id="b6d8e-110">概要</span><span class="sxs-lookup"><span data-stu-id="b6d8e-110">Overview</span></span>

<span data-ttu-id="b6d8e-111">アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b6d8e-112">内容として、 `UpdatePanel`、アニメーション フレームワークに大きく依存している特別なエクステンダーが存在します:`UpdatePanelAnimation`します。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="b6d8e-113">このチュートリアルのようなアニメーションを設定する方法を示しています、`UpdatePanel`します。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="b6d8e-114">手順</span><span class="sxs-lookup"><span data-stu-id="b6d8e-114">Steps</span></span>

<span data-ttu-id="b6d8e-115">最初の手順は、通常どおりに含める、 `ScriptManager`  ページで、ASP.NET AJAX ライブラリが読み込まれ、Control Toolkit を使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

<span data-ttu-id="b6d8e-116">このシナリオでは、アニメーションは、ASP.NET に適用される`Wizard`内に存在する web コントロール、`UpdatePanel`します。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="b6d8e-117">(任意) の 3 つの手順では、ポストバックをトリガーするための十分なオプションを提供します。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

<span data-ttu-id="b6d8e-118">マークアップのために必要な`UpdatePanelAnimationExtender`コントロールを使用するマークアップを非常に似ていますが、`AnimationExtender`します。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="b6d8e-119">`TargetControlID`属性を提供しています、`ID`の`UpdatePanel`; をアニメーション化する内で、`UpdatePanelAnimationExtender`コントロール、`<Animations>`要素は、単位の XML マークアップを保持します。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="b6d8e-120">ただし 1 つの違いがあります。イベントとイベント ハンドラーの量が比較する限られた`AnimationExtender`します。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="b6d8e-121">`UpdatePanels`、2 つだけに存在します。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="b6d8e-122">`<OnUpdated>` UpdatePanel が更新されたとき</span><span class="sxs-lookup"><span data-stu-id="b6d8e-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="b6d8e-123">`<OnUpdating>` UpdatePanel が更新を開始する場合</span><span class="sxs-lookup"><span data-stu-id="b6d8e-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="b6d8e-124">このシナリオでは、新しいコンテンツでは、 `UpdatePanel` (ポストバック) の後、フェードインものとします。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="b6d8e-125">これは、そのために必要なマークアップです。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

<span data-ttu-id="b6d8e-126">これで、ポストバック、UpdatePanel 内で発生するたびに、パネルの新しい内容はスムーズ フェードインします。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>


<span data-ttu-id="b6d8e-127">[![ウィザードの次の手順がフェードインします。](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b6d8e-127">[![The next wizard step is fading in](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="b6d8e-128">ウィザードの次の手順がフェードイン ([フルサイズの画像を表示する をクリックします](animating-an-updatepanel-control-vb/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="b6d8e-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b6d8e-129">[前へ](changing-an-animation-using-client-side-code-vb.md)
> [次へ](dynamically-controlling-updatepanel-animations-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b6d8e-129">[Previous](changing-an-animation-using-client-side-code-vb.md)
[Next](dynamically-controlling-updatepanel-animations-vb.md)</span></span>