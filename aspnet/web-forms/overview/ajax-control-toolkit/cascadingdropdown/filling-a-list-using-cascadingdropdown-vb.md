---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: 入力する (VB) を使用してリスト |Microsoft Docs
author: wenz
description: CascadingDropDown コントロール、AJAX Control Toolkit では、anoth 内の値が 1 つの DropDownList の読み込みの変更に関連付けられているように DropDownList コントロールを拡張しています.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 4cf5637eed1ecf8a09e8a98fa0193b6d162fd92b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130487"
---
# <a name="filling-a-list-using-cascadingdropdown-vb"></a><span data-ttu-id="c7030-103">CascadingDropDown を使用して一覧に入力する (VB)</span><span class="sxs-lookup"><span data-stu-id="c7030-103">Filling a List Using CascadingDropDown (VB)</span></span>

<span data-ttu-id="c7030-104">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c7030-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c7030-105">[コードのダウンロード](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip)または[PDF のダウンロード](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="c7030-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span></span>

> <span data-ttu-id="c7030-106">CascadingDropDown コントロール、AJAX Control Toolkit では、もう 1 つの DropDownList の値が 1 つの DropDownList の読み込みの変更に関連付けられているように、DropDownList コントロールを拡張します。</span><span class="sxs-lookup"><span data-stu-id="c7030-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="c7030-107">(たとえば、1 つのリストは、私たちの状態の一覧を提供します。 し、[次へ] の一覧は、その状態の主な都市で埋められます)。解決するために最初のチャレンジでは、実際にこのコントロールを使用して、ドロップダウン リストを入力します。</span><span class="sxs-lookup"><span data-stu-id="c7030-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="overview"></a><span data-ttu-id="c7030-108">概要</span><span class="sxs-lookup"><span data-stu-id="c7030-108">Overview</span></span>

<span data-ttu-id="c7030-109">CascadingDropDown コントロール、AJAX Control Toolkit では、もう 1 つの DropDownList の値が 1 つの DropDownList の読み込みの変更に関連付けられているように、DropDownList コントロールを拡張します。</span><span class="sxs-lookup"><span data-stu-id="c7030-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="c7030-110">(たとえば、1 つのリストは、私たちの状態の一覧を提供します。 し、[次へ] の一覧は、その状態の主な都市で埋められます)。解決するために最初のチャレンジでは、実際にこのコントロールを使用して、ドロップダウン リストを入力します。</span><span class="sxs-lookup"><span data-stu-id="c7030-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="c7030-111">手順</span><span class="sxs-lookup"><span data-stu-id="c7030-111">Steps</span></span>

<span data-ttu-id="c7030-112">ASP.NET AJAX Control Toolkit の機能をアクティブ化するために、`ScriptManager`コントロールは、ページのどこでも配置する必要があります (ただし内、`<form>`要素)。</span><span class="sxs-lookup"><span data-stu-id="c7030-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="c7030-113">次に、DropDownList コントロールが必要です。</span><span class="sxs-lookup"><span data-stu-id="c7030-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="c7030-114">このリストの CascadingDropDown エクステンダーが追加されます。</span><span class="sxs-lookup"><span data-stu-id="c7030-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="c7030-115">これは、一覧に表示されるエントリの一覧が返されますし、web サービスに非同期要求を送信します。</span><span class="sxs-lookup"><span data-stu-id="c7030-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="c7030-116">これを機能させるには、CascadingDropDown の次の属性を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c7030-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="c7030-117">`ServicePath`:一覧のエントリを提供する web サービスの URL</span><span class="sxs-lookup"><span data-stu-id="c7030-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="c7030-118">`ServiceMethod`:一覧のエントリを提供する web メソッド</span><span class="sxs-lookup"><span data-stu-id="c7030-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="c7030-119">`TargetControlID`:ドロップダウン リストの ID</span><span class="sxs-lookup"><span data-stu-id="c7030-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="c7030-120">`Category`:Web メソッドが呼び出されたときに送信されるカテゴリ情報</span><span class="sxs-lookup"><span data-stu-id="c7030-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="c7030-121">`PromptText`:サーバーからリスト データを非同期的に読み込むときに表示されるテキスト</span><span class="sxs-lookup"><span data-stu-id="c7030-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="c7030-122">次のマークアップに示します、`CascadingDropDown`要素。</span><span class="sxs-lookup"><span data-stu-id="c7030-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="c7030-123">C# および VB の唯一の違いは、関連付けられている web サービスの名前を示します。</span><span class="sxs-lookup"><span data-stu-id="c7030-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="c7030-124">JavaScript コード、`CascadingDropDown`エクステンダーは、次のシグネチャを持つ web サービス メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c7030-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="c7030-125">重要な側面は、メソッドが型の配列を取得する必要がある`CascadingDropDownNameValue`(ASP.NET AJAX Control Toolkit によって定義される)。</span><span class="sxs-lookup"><span data-stu-id="c7030-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="c7030-126">`CascadingDropDownNameValue`リスト エントリのテキストとし、その値を指定する必要があります、最初のコンス トラクターと同様`<option value="VALUE">NAME</option>`HTML で行います。</span><span class="sxs-lookup"><span data-stu-id="c7030-126">In the `CascadingDropDownNameValue` constructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="c7030-127">サンプル データの一部を次に示します。</span><span class="sxs-lookup"><span data-stu-id="c7030-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="c7030-128">ブラウザーでページの読み込みと、次の 3 つの仕入先を格納するリストがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="c7030-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>

<span data-ttu-id="c7030-129">[![リストが自動的に入力します。](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c7030-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="c7030-130">リストが自動的に入力されます ([フルサイズの画像を表示する をクリックします](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="c7030-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c7030-131">[前へ](using-auto-postback-with-cascadingdropdown-cs.md)
> [次へ](using-cascadingdropdown-with-a-database-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c7030-131">[Previous](using-auto-postback-with-cascadingdropdown-cs.md)
[Next](using-cascadingdropdown-with-a-database-vb.md)</span></span>
