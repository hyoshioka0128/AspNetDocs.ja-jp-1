---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: クライアント側コード (c#) を使用してアニメーションを実行する |Microsoft Docs
author: wenz
description: アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。 アニメーションの実行.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 23727e8f34afdd073b21aa1e7381237c48e699c4
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132718"
---
# <a name="executing-animations-using-client-side-code-c"></a><span data-ttu-id="b3688-104">クライアント側コードを使用してアニメーションを実行する (C#)</span><span class="sxs-lookup"><span data-stu-id="b3688-104">Executing Animations Using Client-Side Code (C#)</span></span>

<span data-ttu-id="b3688-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b3688-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b3688-106">[コードのダウンロード](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip)または[PDF のダウンロード](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="b3688-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span></span>

> <span data-ttu-id="b3688-107">アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="b3688-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b3688-108">カスタムのクライアント側の JavaScript コードを使用して、アニメーションの実行をトリガーも可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b3688-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="b3688-109">概要</span><span class="sxs-lookup"><span data-stu-id="b3688-109">Overview</span></span>

<span data-ttu-id="b3688-110">アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="b3688-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b3688-111">カスタムのクライアント側の JavaScript コードを使用して、アニメーションの実行をトリガーも可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b3688-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="b3688-112">手順</span><span class="sxs-lookup"><span data-stu-id="b3688-112">Steps</span></span>

<span data-ttu-id="b3688-113">まず、含める、 `ScriptManager` ; ページで次に、ASP.NET AJAX ライブラリが読み込まれる Control Toolkit を使用すること。</span><span class="sxs-lookup"><span data-stu-id="b3688-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="b3688-114">次のようなテキストのパネルに、アニメーションが適用されます。</span><span class="sxs-lookup"><span data-stu-id="b3688-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="b3688-115">パネルの関連付けられている CSS クラス、便利な背景色を定義し、パネルの固定幅の設定も。</span><span class="sxs-lookup"><span data-stu-id="b3688-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="b3688-116">次に、追加、 `AnimationExtender` 、ページを提供する、 `ID`、`TargetControlID`属性と、変更を加える`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="b3688-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="b3688-117">内で、`<Animations>`ノードを使用して`<OnClick>`パネルがクリック 1 回、ユーザーのアニメーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="b3688-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="b3688-118">並列で実行される 2 つのアニメーションを追加します。</span><span class="sxs-lookup"><span data-stu-id="b3688-118">Add two animations to be executed in parallel:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

<span data-ttu-id="b3688-119">このアニメーション (およびその他のすべてのアニメーション Control Toolkit を使用して作成) には、デモンストレーションのために、ページの実行後に、JavaScript コードを使用して実行されます。</span><span class="sxs-lookup"><span data-stu-id="b3688-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="b3688-120">最初にすべてのアクセスする必要があります、`AnimationExtender`コントロール。</span><span class="sxs-lookup"><span data-stu-id="b3688-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="b3688-121">ASP.NET AJAX ライブラリには、`$find()`このタスクの関数。</span><span class="sxs-lookup"><span data-stu-id="b3688-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

<span data-ttu-id="b3688-122">`AnimationExtender`コントロールは、XML マークアップで使用されるイベント ハンドラーと同じ名前のメソッドを含む豊富な API を公開します: `OnClick()`、`OnLoad()`など。</span><span class="sxs-lookup"><span data-stu-id="b3688-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="b3688-123">呼び出しなど、`OnClick()`メソッド内でアニメーションの実行、`<OnClick>`の要素、`AnimationExtender`コントロール。</span><span class="sxs-lookup"><span data-stu-id="b3688-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

<span data-ttu-id="b3688-124">ここでは、ページが完全に読み込まれた後に [パネル] をクリックをエミュレートする完全なクライアント側の JavaScript コードは、注意、 `pageLoad()` 1 回、ページの ASP.NET AJAX によって呼び出される関数の名前が使用され、JavaScript ライブラリであったすべて含まれます読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="b3688-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]

<span data-ttu-id="b3688-125">[![アニメーションのマウス クリックせず、すぐに実行します。](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b3688-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="b3688-126">アニメーションのマウス クリックしてせず、すぐに実行 ([フルサイズの画像を表示する をクリックします](executing-animations-using-client-side-code-cs/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="b3688-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b3688-127">[前へ](modifying-animations-from-the-server-side-cs.md)
> [次へ](changing-an-animation-using-client-side-code-cs.md)</span><span class="sxs-lookup"><span data-stu-id="b3688-127">[Previous](modifying-animations-from-the-server-side-cs.md)
[Next](changing-an-animation-using-client-side-code-cs.md)</span></span>
