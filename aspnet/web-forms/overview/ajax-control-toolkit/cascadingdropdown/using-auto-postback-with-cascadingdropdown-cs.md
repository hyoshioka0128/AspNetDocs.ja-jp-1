---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: 自動ポストバックを使用する (c#) |Microsoft Docs
author: wenz
description: CascadingDropDown コントロール、AJAX Control Toolkit では、anoth 内の値が 1 つの DropDownList の読み込みの変更に関連付けられているように DropDownList コントロールを拡張しています.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 44133164d1c852fefc84a89614d306e39378ed97
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65133605"
---
# <a name="using-auto-postback-with-cascadingdropdown-c"></a><span data-ttu-id="246d9-103">CascadingDropDown で自動ポストバックを使用する (C#)</span><span class="sxs-lookup"><span data-stu-id="246d9-103">Using Auto-Postback with CascadingDropDown (C#)</span></span>

<span data-ttu-id="246d9-104">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="246d9-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="246d9-105">[コードのダウンロード](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip)または[PDF のダウンロード](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="246d9-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)</span></span>

> <span data-ttu-id="246d9-106">CascadingDropDown コントロール、AJAX Control Toolkit では、もう 1 つの DropDownList の値が 1 つの DropDownList の読み込みの変更に関連付けられているように、DropDownList コントロールを拡張します。</span><span class="sxs-lookup"><span data-stu-id="246d9-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="246d9-107">ただし、ASP CascadingDropDown コントロールを使用する場合。NET の DropDownList コントロール AutoPostBack 機能が機能しませんので、リストにデータを非同期的に読み込む自体 (不要な)、ポストバックを生成します。</span><span class="sxs-lookup"><span data-stu-id="246d9-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="246d9-108">いくつかの JavaScript コードでは、この影響を回避できます。</span><span class="sxs-lookup"><span data-stu-id="246d9-108">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="overview"></a><span data-ttu-id="246d9-109">概要</span><span class="sxs-lookup"><span data-stu-id="246d9-109">Overview</span></span>

<span data-ttu-id="246d9-110">CascadingDropDown コントロール、AJAX Control Toolkit では、もう 1 つの DropDownList の値が 1 つの DropDownList の読み込みの変更に関連付けられているように、DropDownList コントロールを拡張します。</span><span class="sxs-lookup"><span data-stu-id="246d9-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="246d9-111">(たとえば、1 つのリストは、私たちの状態の一覧を提供します。 し、[次へ] の一覧は、その状態の主な都市で埋められます)。ただし、ASP CascadingDropDown コントロールを使用する場合。NET の DropDownList コントロール AutoPostBack 機能が機能しませんので、リストにデータを非同期的に読み込む自体 (不要な)、ポストバックを生成します。</span><span class="sxs-lookup"><span data-stu-id="246d9-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="246d9-112">いくつかの JavaScript コードでは、この影響を回避できます。</span><span class="sxs-lookup"><span data-stu-id="246d9-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="246d9-113">手順</span><span class="sxs-lookup"><span data-stu-id="246d9-113">Steps</span></span>

<span data-ttu-id="246d9-114">ASP.NET AJAX Control Toolkit の機能をアクティブ化するために、`ScriptManager`コントロールは、ページのどこでも配置する必要があります (ただし内、 &lt; `form` &gt;要素)。</span><span class="sxs-lookup"><span data-stu-id="246d9-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="246d9-115">次に、DropDownList コントロールが必要です。</span><span class="sxs-lookup"><span data-stu-id="246d9-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="246d9-116">このリストの CascadingDropDown エクステンダーが追加になり、web サービスの URL とメソッドの情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="246d9-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="246d9-117">CascadingDropDown エクステンダー非同期的に呼び出して、次のメソッド シグネチャを持つ web サービス。</span><span class="sxs-lookup"><span data-stu-id="246d9-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="246d9-118">CascadingDropDown 値の型の配列を返します。</span><span class="sxs-lookup"><span data-stu-id="246d9-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="246d9-119">リスト項目のキャプションとし、値型のコンス トラクターが最初に必要です (HTML`value`属性)。</span><span class="sxs-lookup"><span data-stu-id="246d9-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="246d9-120">ブラウザーでページの読み込みが挿入されますをドロップダウン リストに 3 つのベンダーでは、あらかじめ選択されている 2 つ目。</span><span class="sxs-lookup"><span data-stu-id="246d9-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="246d9-121">また、ASP.NET の定義、 `__doPostBack()` JavaScript メソッド。</span><span class="sxs-lookup"><span data-stu-id="246d9-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="246d9-122">ページが読み込まれると、この JavaScript 呼び出しはのみにある場合の要素には、ドロップダウン リストに追加されます。</span><span class="sxs-lookup"><span data-stu-id="246d9-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="246d9-123">場合は、リスト内の要素がない、Control Toolkit が現在読み込んでいる、ため、JavaScript コードは、タイムアウトを使用し、0.5 秒後にもう一度試みます。</span><span class="sxs-lookup"><span data-stu-id="246d9-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

<span data-ttu-id="246d9-124">この方法では、ポストバックは、リスト内に実際に要素が、ユーザーがエントリを選択してにのみ実行されます。</span><span class="sxs-lookup"><span data-stu-id="246d9-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>

<span data-ttu-id="246d9-125">[![ポストバックを発生させるリスト要素の選択](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="246d9-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="246d9-126">リスト要素を選択すると、ポストバックを発生させる ([フルサイズの画像を表示する をクリックします](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="246d9-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="246d9-127">[前へ](presetting-list-entries-with-cascadingdropdown-cs.md)
> [次へ](filling-a-list-using-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="246d9-127">[Previous](presetting-list-entries-with-cascadingdropdown-cs.md)
[Next](filling-a-list-using-cascadingdropdown-vb.md)</span></span>
