---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: 同時に (VB) の複数のアニメーションの実行 |Microsoft Docs
author: wenz
description: アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。 これにより、落としたを実行する.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: 02eb078a4fb8fddbbac18e4631214f354388cc2f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65133410"
---
# <a name="executing-several-animations-at-the-same-time-vb"></a><span data-ttu-id="a6f15-104">(VB) と同時に複数のアニメーションを実行</span><span class="sxs-lookup"><span data-stu-id="a6f15-104">Executing Several Animations at The Same Time (VB)</span></span>

<span data-ttu-id="a6f15-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a6f15-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a6f15-106">[コードのダウンロード](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip)または[PDF のダウンロード](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a6f15-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span></span>

> <span data-ttu-id="a6f15-107">アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="a6f15-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a6f15-108">並列的に複数のアニメーションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="a6f15-108">It allows to run several animations in a parallel fashion.</span></span>

## <a name="overview"></a><span data-ttu-id="a6f15-109">概要</span><span class="sxs-lookup"><span data-stu-id="a6f15-109">Overview</span></span>

<span data-ttu-id="a6f15-110">アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="a6f15-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a6f15-111">並列的に複数のアニメーションを実行できます。</span><span class="sxs-lookup"><span data-stu-id="a6f15-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="a6f15-112">手順</span><span class="sxs-lookup"><span data-stu-id="a6f15-112">Steps</span></span>

<span data-ttu-id="a6f15-113">まず、含める、 `ScriptManager` ; ページで次に、ASP.NET AJAX ライブラリが読み込まれる Control Toolkit を使用すること。</span><span class="sxs-lookup"><span data-stu-id="a6f15-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

<span data-ttu-id="a6f15-114">次のようなテキストのパネルに、アニメーションが適用されます。</span><span class="sxs-lookup"><span data-stu-id="a6f15-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

<span data-ttu-id="a6f15-115">パネルの関連付けられている CSS クラス、便利な背景色を定義し、パネルの固定幅の設定も。</span><span class="sxs-lookup"><span data-stu-id="a6f15-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

<span data-ttu-id="a6f15-116">次に、追加、 `AnimationExtender` 、ページを提供する、 `ID`、`TargetControlID`属性と、変更を加える`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="a6f15-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

<span data-ttu-id="a6f15-117">内で、`<Animations>`ノードを使用して`<OnLoad>`ページが完全に読み込まれた後に、アニメーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="a6f15-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="a6f15-118">一般に、`<OnLoad>`アニメーションを 1 つのみを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="a6f15-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="a6f15-119">アニメーション フレームワークを使用すると、複数のアニメーションを使用して 1 つに参加させる、`<Parallel>`要素。</span><span class="sxs-lookup"><span data-stu-id="a6f15-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="a6f15-120">内のすべてのアニメーション`<Parallel>`と同時に実行されます。</span><span class="sxs-lookup"><span data-stu-id="a6f15-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="a6f15-121">ここでは、可能なマークアップを`AnimationExtender`フェードアウトし、同時に、パネルのサイズを変更するときに、コントロール。</span><span class="sxs-lookup"><span data-stu-id="a6f15-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

<span data-ttu-id="a6f15-122">実際: このスクリプトを実行すると、パネルが表示し (いったように複数の幅と高さの半分) のサイズを変更されと同時にフェードアウトします。</span><span class="sxs-lookup"><span data-stu-id="a6f15-122">And indeed: when you run this script, the panel is displayed, then resizes (more than tripling its width and halving its height) and fades out at the same time.</span></span>

<span data-ttu-id="a6f15-123">[![パネルをフェードアウトし、(ブラウザーのレンダリング エンジンに協力してくれた、そのコンテンツを含む) のサイズ変更](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a6f15-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span></span>

<span data-ttu-id="a6f15-124">パネルをフェードアウトし、(ブラウザーのレンダリング エンジンに協力してくれた、そのコンテンツを含む) のサイズ変更 ([フルサイズの画像を表示する をクリックします](executing-several-animations-at-the-same-time-vb/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="a6f15-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a6f15-125">[前へ](adding-animation-to-a-control-vb.md)
> [次へ](executing-several-animations-after-each-other-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a6f15-125">[Previous](adding-animation-to-a-control-vb.md)
[Next](executing-several-animations-after-each-other-vb.md)</span></span>
