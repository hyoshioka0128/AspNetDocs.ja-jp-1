---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: (VB) ReorderList でポストバックを使用 |Microsoft Docs
author: wenz
description: ReorderList コントロール、AJAX Control Toolkit では、ユーザーがドラッグ アンド ドロップを使用して並べ替えることができる一覧を提供します。 一覧の順序が変更されるたびに、po.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: e2ab485d276d62518b6e7317bd76121f18d27ba8
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124721"
---
# <a name="using-postbacks-with-reorderlist-vb"></a><span data-ttu-id="ab23d-104">ReorderList でポストバックを使用する (VB)</span><span class="sxs-lookup"><span data-stu-id="ab23d-104">Using Postbacks with ReorderList (VB)</span></span>

<span data-ttu-id="ab23d-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ab23d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ab23d-106">[コードのダウンロード](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip)または[PDF のダウンロード](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="ab23d-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)</span></span>

> <span data-ttu-id="ab23d-107">ReorderList コントロール、AJAX Control Toolkit では、ユーザーがドラッグ アンド ドロップを使用して並べ替えることができる一覧を提供します。</span><span class="sxs-lookup"><span data-stu-id="ab23d-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="ab23d-108">一覧の順序が変更されるたびにポストバックの変更のサーバーに通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab23d-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="overview"></a><span data-ttu-id="ab23d-109">概要</span><span class="sxs-lookup"><span data-stu-id="ab23d-109">Overview</span></span>

<span data-ttu-id="ab23d-110">`ReorderList` AJAX Control Toolkit でコントロールには、ユーザーがドラッグ アンド ドロップを使用して並べ替えることができる一覧が用意されています。</span><span class="sxs-lookup"><span data-stu-id="ab23d-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="ab23d-111">一覧の順序が変更されるたびにポストバックの変更のサーバーに通知する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab23d-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="ab23d-112">手順</span><span class="sxs-lookup"><span data-stu-id="ab23d-112">Steps</span></span>

<span data-ttu-id="ab23d-113">いくつかのデータ ソースが、`ReorderList`コントロール。</span><span class="sxs-lookup"><span data-stu-id="ab23d-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="ab23d-114">1 つは、使用する、`XmlDataSource`コントロール。</span><span class="sxs-lookup"><span data-stu-id="ab23d-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="ab23d-115">この XML にバインドするために、`ReorderList`コントロールと有効にするポストバックでは、次の属性を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab23d-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="ab23d-116">`DataSourceID`:データ ソースの ID</span><span class="sxs-lookup"><span data-stu-id="ab23d-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="ab23d-117">`SortOrderField`:プロパティを並べ替えるには</span><span class="sxs-lookup"><span data-stu-id="ab23d-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="ab23d-118">`AllowReorder`:ユーザーがリストの要素の順序を変更できるようにするかどうか</span><span class="sxs-lookup"><span data-stu-id="ab23d-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="ab23d-119">`PostBackOnReorder`:リストが再配置されるたびに、ポストバックを作成するかどうか</span><span class="sxs-lookup"><span data-stu-id="ab23d-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="ab23d-120">コントロールの適切なマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="ab23d-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="ab23d-121">内で、`ReorderList`を使用して、コントロール、データ ソースから特定のデータを連結することも、`Eval()`メソッド。</span><span class="sxs-lookup"><span data-stu-id="ab23d-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

<span data-ttu-id="ab23d-122">ページで、任意の位置にラベルは最後の順序変更が発生したときに情報を保持します。</span><span class="sxs-lookup"><span data-stu-id="ab23d-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="ab23d-123">このラベルは、ポストバックを処理、サーバー側コード内のテキストが入力されます。</span><span class="sxs-lookup"><span data-stu-id="ab23d-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

<span data-ttu-id="ab23d-124">最後に、ASP.NET AJAX Control Toolkit の機能をアクティブ化するために、`ScriptManager`ページにコントロールを配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ab23d-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]

<span data-ttu-id="ab23d-125">[![ポストバックをトリガーするそれぞれの並べ替え](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ab23d-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="ab23d-126">ポストバックをトリガーするそれぞれの並べ替え ([フルサイズの画像を表示する をクリックします](using-postbacks-with-reorderlist-vb/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="ab23d-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ab23d-127">[前へ](drag-and-drop-via-reorderlist-cs.md)
> [次へ](drag-and-drop-via-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ab23d-127">[Previous](drag-and-drop-via-reorderlist-cs.md)
[Next](drag-and-drop-via-reorderlist-vb.md)</span></span>
