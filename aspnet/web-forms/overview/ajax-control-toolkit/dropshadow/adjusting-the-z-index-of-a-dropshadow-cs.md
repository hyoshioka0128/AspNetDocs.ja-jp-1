---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: (C#) DropShadow の Z インデックスを調整 |Microsoft Docs
author: wenz
description: DropShadow コントロール、AJAX Control Toolkit では、影付きのパネルを拡張します。 ただし場合がありますこのシャドウがインストールの他のコントロールと競合しています.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 21ad1ec314be68f7285c044d5e90c21c201a90ef
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132158"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-c"></a><span data-ttu-id="0e6bc-104">DropShadow の Z インデックスを調整する (C#)</span><span class="sxs-lookup"><span data-stu-id="0e6bc-104">Adjusting the Z-Index of a DropShadow (C#)</span></span>

<span data-ttu-id="0e6bc-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0e6bc-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0e6bc-106">[コードのダウンロード](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip)または[PDF のダウンロード](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="0e6bc-106">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span></span>

> <span data-ttu-id="0e6bc-107">DropShadow コントロール、AJAX Control Toolkit では、影付きのパネルを拡張します。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="0e6bc-108">ただしこのシャドウは、他のコントロールでは、ASP.NET の Menu コントロールのインスタンスとも競合しています。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="0e6bc-109">ときにメニュー エントリが表示されます、ドロップ シャドウの背後に表示されます。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="overview"></a><span data-ttu-id="0e6bc-110">概要</span><span class="sxs-lookup"><span data-stu-id="0e6bc-110">Overview</span></span>

<span data-ttu-id="0e6bc-111">DropShadow コントロール、AJAX Control Toolkit では、影付きのパネルを拡張します。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="0e6bc-112">ただしこのシャドウは、他のコントロールでは、ASP.NET の Menu コントロールのインスタンスとも競合しています。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="0e6bc-113">ときにメニュー エントリが表示されます、ドロップ シャドウの背後に表示されます。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="0e6bc-114">手順</span><span class="sxs-lookup"><span data-stu-id="0e6bc-114">Steps</span></span>

<span data-ttu-id="0e6bc-115">コードは、パネルが表示される効果のための十分なテキストが含まれるように、十分なテキストを含む、パネル自体には、開始します。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

<span data-ttu-id="0e6bc-116">別のパネルが直前に配置されて、`panelShadow`パネル。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="0e6bc-117">上メニュー エントリが表示されるように水平方向のメニューが含まれている (または: )、`dropShadow`パネル)。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

<span data-ttu-id="0e6bc-118">次に、`DropShadowExtender`拡張に追加されます、`panelShadow`ドロップ シャドウ効果を使用したパネル。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

<span data-ttu-id="0e6bc-119">ASP.NET AJAX では最後に、`ScriptManager`コントロールが動作する Control Toolkit を使用します。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

<span data-ttu-id="0e6bc-120">このスクリプトを実行すると、パネルの下にあるメニュー エントリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="0e6bc-121">ただし、メニューが CSS クラスを使用して`panel`だけがある他のパネルの前に表示される要素を次の 2 つを定義します。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="0e6bc-122">相対配置</span><span class="sxs-lookup"><span data-stu-id="0e6bc-122">Relative positioning</span></span>
- <span data-ttu-id="0e6bc-123">正の z インデックス</span><span class="sxs-lookup"><span data-stu-id="0e6bc-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

<span data-ttu-id="0e6bc-124">次に、 `DropShadowExtender` Menu コントロールとコントロールが不要に競合しません。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>

<span data-ttu-id="0e6bc-125">[![以前は：メニュー エントリが表示されていません。](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0e6bc-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span></span>

<span data-ttu-id="0e6bc-126">前:メニュー エントリは表示されません ([フルサイズの画像を表示する をクリックします](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span></span>

<span data-ttu-id="0e6bc-127">[![設定後。メニュー エントリが表示されます。](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="0e6bc-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span></span>

<span data-ttu-id="0e6bc-128">後:メニュー エントリが表示されます ([フルサイズの画像を表示する をクリックします](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))。</span><span class="sxs-lookup"><span data-stu-id="0e6bc-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0e6bc-129">次へ</span><span class="sxs-lookup"><span data-stu-id="0e6bc-129">Next</span></span>](manipulating-dropshadow-properties-from-client-code-cs.md)
