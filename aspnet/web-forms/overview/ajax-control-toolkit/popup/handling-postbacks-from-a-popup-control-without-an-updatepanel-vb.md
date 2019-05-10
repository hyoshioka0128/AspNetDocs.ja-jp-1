---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: UpdatePanel (VB) なしのポップアップ コントロールからポストバックを処理する |Microsoft Docs
author: wenz
description: AJAX Control Toolkit で PopupControl エクステンダーには、その他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法が用意されています。 Su でポストバックが発生する.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: c0535ee78bf3ee5133d73749e8376f4b771f4d3c
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115105"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a><span data-ttu-id="4668d-104">ポップアップ コントロールからポストバックを処理する (UpdatePanel なし) (VB)</span><span class="sxs-lookup"><span data-stu-id="4668d-104">Handling Postbacks from A Popup Control Without an UpdatePanel (VB)</span></span>

<span data-ttu-id="4668d-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4668d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4668d-106">[コードのダウンロード](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip)または[PDF のダウンロード](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="4668d-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)</span></span>

> <span data-ttu-id="4668d-107">AJAX Control Toolkit で PopupControl エクステンダーには、その他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="4668d-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="4668d-108">このようなパネルで、ポストバックが発生して、ページ上のパネルがある場合は、パネルがクリックしてされたかを判断する困難です。</span><span class="sxs-lookup"><span data-stu-id="4668d-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="overview"></a><span data-ttu-id="4668d-109">概要</span><span class="sxs-lookup"><span data-stu-id="4668d-109">Overview</span></span>

<span data-ttu-id="4668d-110">AJAX Control Toolkit で PopupControl エクステンダーには、その他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="4668d-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="4668d-111">このようなパネルで、ポストバックが発生して、ページ上のパネルがある場合は、パネルがクリックしてされたかを判断する困難です。</span><span class="sxs-lookup"><span data-stu-id="4668d-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="4668d-112">手順</span><span class="sxs-lookup"><span data-stu-id="4668d-112">Steps</span></span>

<span data-ttu-id="4668d-113">使用する場合、 `PopupControl` 、ポストバックがしなくても、 `UpdatePanel`  ページで、Control Toolkit は提供していませんクライアント要素がさらに、ポストバックの原因となったポップアップをトリガーを決定する方法。</span><span class="sxs-lookup"><span data-stu-id="4668d-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="4668d-114">ただし小規模なトリックは、このシナリオの回避策を提供します。</span><span class="sxs-lookup"><span data-stu-id="4668d-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="4668d-115">まず、基本的なセットアップを示します。 どちらも、同じポップアップ カレンダーをトリガーする 2 つのテキスト ボックス。</span><span class="sxs-lookup"><span data-stu-id="4668d-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="4668d-116">2 つ`PopupControlExtenders`テキスト ボックスとポップアップをまとめて表示します。</span><span class="sxs-lookup"><span data-stu-id="4668d-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="4668d-117">基本的な考え方が隠しフォーム フィールドを追加するには、 &lt; `form` &gt;起動ポップアップ テキスト ボックスを保持する要素。</span><span class="sxs-lookup"><span data-stu-id="4668d-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="4668d-118">ページが読み込まれるときに JavaScript コードには、両方のテキスト ボックスに、イベント ハンドラーが追加されます。ユーザーがテキスト ボックスをクリックすると、その名前が隠しフォーム フィールドに書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="4668d-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

<span data-ttu-id="4668d-119">サーバー側のコードでは、非表示フィールドの値を読み取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="4668d-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="4668d-120">隠しフォーム フィールドは、操作は簡単であるために、非表示の値の検証にホワイト リスト アプローチが必要です。</span><span class="sxs-lookup"><span data-stu-id="4668d-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="4668d-121">適切なテキスト ボックスが識別されると、カレンダーから日付がそこに書き込まれます。</span><span class="sxs-lookup"><span data-stu-id="4668d-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]

<span data-ttu-id="4668d-122">[![カレンダーは、テキスト ボックスに、ユーザーがクリックしたときに表示されます。](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4668d-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="4668d-123">テキスト ボックスに、ユーザーがクリックしたときに、カレンダーが表示されます ([フルサイズの画像を表示する をクリックします](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="4668d-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))</span></span>

<span data-ttu-id="4668d-124">[![テキスト ボックス内に配置する日付をクリックすると](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="4668d-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="4668d-125">テキスト ボックス内に配置する日付をクリックすると ([フルサイズの画像を表示する をクリックします](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))。</span><span class="sxs-lookup"><span data-stu-id="4668d-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4668d-126">前へ</span><span class="sxs-lookup"><span data-stu-id="4668d-126">Previous</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
