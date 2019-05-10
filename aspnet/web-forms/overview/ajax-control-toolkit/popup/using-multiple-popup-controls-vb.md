---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: 複数のポップアップ コントロール (VB) を使用して |Microsoft Docs
author: wenz
description: AJAX Control Toolkit で PopupControl エクステンダーには、その他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法が用意されています。 M を使用することもしています.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 6f8097ed64f81d8ad9de27e19195d9a4572a0ae7
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115090"
---
# <a name="using-multiple-popup-controls-vb"></a><span data-ttu-id="f740b-104">複数のポップアップ コントロールを使用する (VB)</span><span class="sxs-lookup"><span data-stu-id="f740b-104">Using Multiple Popup Controls (VB)</span></span>

<span data-ttu-id="f740b-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f740b-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f740b-106">[コードのダウンロード](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip)または[PDF のダウンロード](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f740b-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span></span>

> <span data-ttu-id="f740b-107">AJAX Control Toolkit で PopupControl エクステンダーには、その他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="f740b-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="f740b-108">1 ページには、複数のポップアップ コントロールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="f740b-108">It is also possible to use more than one popup control on one page.</span></span>

## <a name="overview"></a><span data-ttu-id="f740b-109">概要</span><span class="sxs-lookup"><span data-stu-id="f740b-109">Overview</span></span>

<span data-ttu-id="f740b-110">AJAX Control Toolkit で PopupControl エクステンダーには、その他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="f740b-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="f740b-111">1 ページには、複数のポップアップ コントロールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="f740b-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="f740b-112">手順</span><span class="sxs-lookup"><span data-stu-id="f740b-112">Steps</span></span>

<span data-ttu-id="f740b-113">ASP.NET AJAX Control Toolkit の機能をアクティブ化するために、`ScriptManager`コントロールは、ページのどこでも配置する必要があります (ただし内、`<form>`要素)。</span><span class="sxs-lookup"><span data-stu-id="f740b-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="f740b-114">次に、ポップアップとして機能するパネルを追加します。</span><span class="sxs-lookup"><span data-stu-id="f740b-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="f740b-115">パネルに含まれる現在のシナリオでは、`Calendar`コントロール。</span><span class="sxs-lookup"><span data-stu-id="f740b-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="f740b-116">内のパネルを配置するカレンダーのポストバックの原因となったページ更新を回避するために、`UpdatePanel`コントロール。</span><span class="sxs-lookup"><span data-stu-id="f740b-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="f740b-117">ページには、2 つのテキスト ボックスも含まれています。</span><span class="sxs-lookup"><span data-stu-id="f740b-117">The page also contains two text boxes.</span></span> <span data-ttu-id="f740b-118">各テキスト ボックスのテキスト ボックスがアクティブ化される、カレンダーのポップアップは表示されます。</span><span class="sxs-lookup"><span data-stu-id="f740b-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="f740b-119">2 つのテキスト ボックスのそれぞれを拡張するようになりました、`PopupControlExtender`します。</span><span class="sxs-lookup"><span data-stu-id="f740b-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="f740b-120">`TargetControlID`属性は、extender に関連付けられているコントロールの ID を提供します。</span><span class="sxs-lookup"><span data-stu-id="f740b-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="f740b-121">`PopupControlID`属性には、ポップアップ パネルの ID が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f740b-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="f740b-122">この場合は、両方のエクステンダーが同じのパネルを表示するが、さまざまなパネルをも可能であれば、します。</span><span class="sxs-lookup"><span data-stu-id="f740b-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="f740b-123">テキスト フィールド内でクリックしたときに、カレンダーが表示されます、フィールドの下の日付を選択することができます。</span><span class="sxs-lookup"><span data-stu-id="f740b-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="f740b-124">(テキスト ボックスに、選択した日付は戻ってきてで取り上げる別のチュートリアルです。)</span><span class="sxs-lookup"><span data-stu-id="f740b-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>

<span data-ttu-id="f740b-125">[![カレンダーは、テキスト ボックスに、ユーザーがクリックしたときに表示されます。](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f740b-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="f740b-126">テキスト ボックスに、ユーザーがクリックしたときに、カレンダーが表示されます ([フルサイズの画像を表示する をクリックします](using-multiple-popup-controls-vb/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="f740b-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f740b-127">[前へ](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [次へ](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f740b-127">[Previous](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
[Next](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span></span>
