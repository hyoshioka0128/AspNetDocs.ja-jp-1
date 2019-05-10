---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: 相互に排他的なチェック ボックス (c#) を作成する |Microsoft Docs
author: wenz
description: 一連のオプションの 1 つだけが選択されるときに、オプション ボタンが通常使用されます。 ただし、欠点があります。1 回 1 つのオプション ボタン グループが選択されて、.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: c8fd0f6af612f99e14679b04554a8d1585af44b0
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115363"
---
# <a name="creating-mutually-exclusive-checkboxes-c"></a><span data-ttu-id="c7fe7-104">相互に排他的なチェックボックスを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="c7fe7-104">Creating Mutually Exclusive Checkboxes (C#)</span></span>

<span data-ttu-id="c7fe7-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c7fe7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c7fe7-106">[コードのダウンロード](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip)または[PDF のダウンロード](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="c7fe7-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span></span>

> <span data-ttu-id="c7fe7-107">一連のオプションの 1 つだけが選択されるときに、オプション ボタンが通常使用されます。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="c7fe7-108">ただし、欠点があります。グループ内の 1 つのオプション ボタンを選択すると、すべてのオプション ボタンをオフにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="c7fe7-109">チェック ボックスは、ただし相互に排他的ではありません、いつでもチェックできます。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="c7fe7-110">このチュートリアルでは、両方のアプローチの最適な: チェック ボックスは相互に排他的です。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="overview"></a><span data-ttu-id="c7fe7-111">概要</span><span class="sxs-lookup"><span data-stu-id="c7fe7-111">Overview</span></span>

<span data-ttu-id="c7fe7-112">一連のオプションの 1 つだけが選択されるときに、オプション ボタンが通常使用されます。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="c7fe7-113">ただし、欠点があります。グループ内の 1 つのオプション ボタンを選択すると、すべてのオプション ボタンをオフにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="c7fe7-114">チェック ボックスは、ただし相互に排他的ではありません、いつでもチェックできます。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="c7fe7-115">このチュートリアルでは、両方のアプローチの最適な: チェック ボックスは相互に排他的です。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="c7fe7-116">手順</span><span class="sxs-lookup"><span data-stu-id="c7fe7-116">Steps</span></span>

<span data-ttu-id="c7fe7-117">ASP.NET AJAX Control Toolkit には、MutuallyExclusiveCheckBox エクステンダーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="c7fe7-118">これにより、プログラマはグループ名にすべてのチェック ボックスを割り当てる (`Key`属性)。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="c7fe7-119">同じグループ内のすべてのチェック ボックスは、1 つだけを一度に選択できます。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="c7fe7-120">新しい ASP.NET ページに 2 つのチェック ボックスを配置することから始めましょう。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="c7fe7-121">以上、存在することができますが、原則を示すためにそのうち 2 つで十分です。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

<span data-ttu-id="c7fe7-122">両方のチェック ボックスのページに MutuallyExclusiveCheckBoxExtender コントロールを配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="c7fe7-123">両方のキー属性は、HTML ラジオ ボタンの要素の属性は、所属するグループを示すのと同じである必要があります値と同様、同じ値を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="c7fe7-124">エクステンダーの TargetControlID プロパティは、チェック ボックスの ID を指します。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

<span data-ttu-id="c7fe7-125">最後に、ASP.NET AJAX を含める`ScriptManager`ASP.NET AJAX Control Toolkit のすべての要素で必要です。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

<span data-ttu-id="c7fe7-126">保存し、ページを実行します。確認し、両方のチェック ボックスをオフにします。 ただしない時に両方のチェック ボックス チェックできます。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>

<span data-ttu-id="c7fe7-127">[![一度に 1 つだけのチェック ボックスをオンすることができます。](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c7fe7-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span></span>

<span data-ttu-id="c7fe7-128">一度に 1 つだけのチェック ボックスをオンすることができます ([フルサイズの画像を表示する をクリックします](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="c7fe7-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c7fe7-129">次へ</span><span class="sxs-lookup"><span data-stu-id="c7fe7-129">Next</span></span>](creating-mutually-exclusive-checkboxes-vb.md)
