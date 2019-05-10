---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: (VB) ModalPopup からポストバックを処理する |Microsoft Docs
author: wenz
description: AJAX Control Toolkit の ModalPopup コントロールには、クライアント側の手段を使用してモーダル ポップアップを作成する簡単な方法が用意されています。 Pos ときに、特別な注意を実行する必要が.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: 3c1951e1ae4f97982d1263dfa9dc29454f7ce55a
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132678"
---
# <a name="handling-postbacks-from-a-modalpopup-vb"></a><span data-ttu-id="403c9-104">ModalPopup からポストバックを処理する (VB)</span><span class="sxs-lookup"><span data-stu-id="403c9-104">Handling Postbacks from a ModalPopup (VB)</span></span>

<span data-ttu-id="403c9-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="403c9-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="403c9-106">[コードのダウンロード](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip)または[PDF のダウンロード](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="403c9-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)</span></span>

> <span data-ttu-id="403c9-107">AJAX Control Toolkit の ModalPopup コントロールには、クライアント側の手段を使用してモーダル ポップアップを作成する簡単な方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="403c9-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="403c9-108">ポップアップでポストバックが作成されたときに、特別な注意を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="403c9-108">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="overview"></a><span data-ttu-id="403c9-109">概要</span><span class="sxs-lookup"><span data-stu-id="403c9-109">Overview</span></span>

<span data-ttu-id="403c9-110">AJAX Control Toolkit の ModalPopup コントロールには、クライアント側の手段を使用してモーダル ポップアップを作成する簡単な方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="403c9-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="403c9-111">ポップアップでポストバックが作成されたときに、特別な注意を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="403c9-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="403c9-112">手順</span><span class="sxs-lookup"><span data-stu-id="403c9-112">Steps</span></span>

<span data-ttu-id="403c9-113">ASP.NET AJAX Control Toolkit の機能をアクティブ化するために、`ScriptManager`コントロールは、ページのどこでも配置する必要があります (ただし内、`<form>`要素)。</span><span class="sxs-lookup"><span data-stu-id="403c9-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

<span data-ttu-id="403c9-114">次に、モーダル ポップアップとして機能するパネルを追加します。</span><span class="sxs-lookup"><span data-stu-id="403c9-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="403c9-115">ユーザーは、名前と電子メール アドレスを入力できます。</span><span class="sxs-lookup"><span data-stu-id="403c9-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="403c9-116">ボタンは、ポップアップを閉じるし、情報の保存に使用されます。</span><span class="sxs-lookup"><span data-stu-id="403c9-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="403c9-117">なお、`OnClick`属性を設定すると、このボタンがクリックされたときにポストバックが発生するようにします。</span><span class="sxs-lookup"><span data-stu-id="403c9-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

<span data-ttu-id="403c9-118">ページ自体は、まったく同じ情報の 2 つのラベルで構成されています。 名前と電子メール アドレス。</span><span class="sxs-lookup"><span data-stu-id="403c9-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="403c9-119">ボタンを使用して、モーダル ポップアップをトリガーします。</span><span class="sxs-lookup"><span data-stu-id="403c9-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

<span data-ttu-id="403c9-120">ポップアップを表示するために、追加、`ModalPopupExtender`コントロール。</span><span class="sxs-lookup"><span data-stu-id="403c9-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="403c9-121">設定、`PopupControlID`パネルの id 属性と`TargetControlID`ボタンの ID に。</span><span class="sxs-lookup"><span data-stu-id="403c9-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

<span data-ttu-id="403c9-122">今すぐたびに、`Save`モーダル ポップアップ内のボタンがクリックされた、サーバー側`SaveData()`メソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="403c9-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="403c9-123">データ ストアに入力されたデータを保存する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="403c9-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="403c9-124">わかりやすくする、新しいデータのラベルにだけ出力します。</span><span class="sxs-lookup"><span data-stu-id="403c9-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

<span data-ttu-id="403c9-125">また、現在の名前と電子メールを使用モーダル ポップアップ内のテキスト ボックス コントロールを入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="403c9-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="403c9-126">ただしこれは必要な場合にのみポストバックは発生しません。</span><span class="sxs-lookup"><span data-stu-id="403c9-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="403c9-127">ポストバックの場合、ASP.NET の viewstate の機能は自動的に、テキスト ボックスに適切な値を入力します。</span><span class="sxs-lookup"><span data-stu-id="403c9-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]

<span data-ttu-id="403c9-128">[![モーダル ポップアップがポストバックを発生させる](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="403c9-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)</span></span>

<span data-ttu-id="403c9-129">モーダル ポップアップがポストバックを発生させる ([フルサイズの画像を表示する をクリックします](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="403c9-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="403c9-130">[前へ](using-modalpopup-with-a-repeater-control-vb.md)
> [次へ](positioning-a-modalpopup-vb.md)</span><span class="sxs-lookup"><span data-stu-id="403c9-130">[Previous](using-modalpopup-with-a-repeater-control-vb.md)
[Next](positioning-a-modalpopup-vb.md)</span></span>
