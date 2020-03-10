---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: コントロールに動的に入力する (VB) |Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値を t... のターゲットコントロールに入力します。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d11320f1f89bb69afe5f62751574079716124da0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430456"
---
# <a name="dynamically-populating-a-control-vb"></a><span data-ttu-id="4bb59-103">コントロールに動的に入力する (VB)</span><span class="sxs-lookup"><span data-stu-id="4bb59-103">Dynamically Populating a Control (VB)</span></span>

<span data-ttu-id="4bb59-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="4bb59-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4bb59-105">[コードのダウンロード](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="4bb59-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span></span>

> <span data-ttu-id="4bb59-106">ASP.NET AJAX Control Toolkit の DynamicPopulate コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。</span><span class="sxs-lookup"><span data-stu-id="4bb59-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span>

## <a name="overview"></a><span data-ttu-id="4bb59-107">概要</span><span class="sxs-lookup"><span data-stu-id="4bb59-107">Overview</span></span>

<span data-ttu-id="4bb59-108">ASP.NET AJAX Control Toolkit の `DynamicPopulate` コントロールは、web サービス (またはページメソッド) を呼び出し、結果の値をページのターゲットコントロールに入力します。ページの更新は行われません。</span><span class="sxs-lookup"><span data-stu-id="4bb59-108">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="4bb59-109">このチュートリアルでは、これを設定する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4bb59-109">This tutorial shows how to set this up.</span></span>

## <a name="steps"></a><span data-ttu-id="4bb59-110">手順</span><span class="sxs-lookup"><span data-stu-id="4bb59-110">Steps</span></span>

<span data-ttu-id="4bb59-111">まず、`DynamicPopulate`によって呼び出されるメソッドを実装する ASP.NET Web サービスが必要です。</span><span class="sxs-lookup"><span data-stu-id="4bb59-111">First of all, you need an ASP.NET Web Service which implements the method to be called by `DynamicPopulate`.</span></span> <span data-ttu-id="4bb59-112">Web サービスクラスには、`Microsoft.Web.Script.Services`内で定義されている `ScriptService` 属性が必要です。それ以外の場合、ASP.NET AJAX では、web サービスのクライアント側の JavaScript プロキシを作成することはできません。これは `DynamicPopulate`によって要求されます。</span><span class="sxs-lookup"><span data-stu-id="4bb59-112">The web service class requires the `ScriptService` attribute which is defined within `Microsoft.Web.Script.Services`; otherwise ASP.NET AJAX cannot create the client-side JavaScript proxy for the web service which in turn is required by `DynamicPopulate`.</span></span>

<span data-ttu-id="4bb59-113">Web メソッドは、`contextKey`と呼ばれる文字列型の1つの引数を想定する必要があります。これは、`DynamicPopulate` コントロールが各 web サービス呼び出しに1つのコンテキスト情報を送信するためです。</span><span class="sxs-lookup"><span data-stu-id="4bb59-113">The web method must expect one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="4bb59-114">次の web サービスは、`contextKey` 引数によって表される形式で現在の日付を返します。</span><span class="sxs-lookup"><span data-stu-id="4bb59-114">The following web service returns the current date in a format represented by the `contextKey` argument:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="4bb59-115">その後、web サービスが `DynamicPopulate.vb.asmx`として保存されます。</span><span class="sxs-lookup"><span data-stu-id="4bb59-115">The web service is then saved as `DynamicPopulate.vb.asmx`.</span></span> <span data-ttu-id="4bb59-116">また、`DynamicPopulate` コントロールを使用して、実際の ASP.NET ページ内のページメソッドとして `getDate()` メソッドを実装することもできます。</span><span class="sxs-lookup"><span data-stu-id="4bb59-116">Alternatively, you could implement the `getDate()` method as a page method within the actual ASP.NET page with the `DynamicPopulate` control.</span></span>

<span data-ttu-id="4bb59-117">次の手順で、新しい ASP.NET ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="4bb59-117">In the next step, create a new ASP.NET file.</span></span> <span data-ttu-id="4bb59-118">常に、最初の手順として、現在のページに `ScriptManager` を含めて、ASP.NET AJAX ライブラリを読み込み、コントロールツールキットを機能させることができます。</span><span class="sxs-lookup"><span data-stu-id="4bb59-118">As always, the first step is to include the `ScriptManager` in the current page to load the ASP.NET AJAX library and to make the Control Toolkit work:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="4bb59-119">次に、label コントロール (同じ名前の HTML コントロールを使用する場合は、web サービス呼び出しの結果を後で表示する場合は &lt;`asp:Label` /&gt; web コントロール) を追加します。</span><span class="sxs-lookup"><span data-stu-id="4bb59-119">Then, add a label control (for instance using the HTML control of the same name, or the &lt;`asp:Label` /&gt; web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

<span data-ttu-id="4bb59-120">Html ボタン (サーバーへのポストバックを必要としないため、HTML コントロール) は、動的な作成をトリガーするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="4bb59-120">An HTML button (as an HTML control, since we do not require a postback to the server) will then be used to trigger the dynamic population:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="4bb59-121">最後に、`DynamicPopulateExtender` 制御が必要です。</span><span class="sxs-lookup"><span data-stu-id="4bb59-121">Finally, we need the `DynamicPopulateExtender` control to wire things up.</span></span> <span data-ttu-id="4bb59-122">次の属性が設定されます (明らかな属性とは別に、`ID` と `runat`=`"server"`)。</span><span class="sxs-lookup"><span data-stu-id="4bb59-122">The following attributes will be set (apart from the obvious ones, `ID` and `runat`=`"server"`):</span></span>

- <span data-ttu-id="4bb59-123">web サービス呼び出しの結果を格納する場所を `TargetControlID` します。</span><span class="sxs-lookup"><span data-stu-id="4bb59-123">`TargetControlID` where to put the result from the web service call</span></span>
- <span data-ttu-id="4bb59-124">web サービスへの `ServicePath` パス (page メソッドを使用する場合は省略)</span><span class="sxs-lookup"><span data-stu-id="4bb59-124">`ServicePath` path to the web service (omit if you want to use a page method)</span></span>
- <span data-ttu-id="4bb59-125">web メソッドまたはページメソッドの `ServiceMethod` 名</span><span class="sxs-lookup"><span data-stu-id="4bb59-125">`ServiceMethod` name of the web method or page method</span></span>
- <span data-ttu-id="4bb59-126">web サービスに送信される `ContextKey` コンテキスト情報</span><span class="sxs-lookup"><span data-stu-id="4bb59-126">`ContextKey` context information to be sent to the web service</span></span>
- <span data-ttu-id="4bb59-127">web サービス呼び出しをトリガーする `PopulateTriggerControlID` 要素</span><span class="sxs-lookup"><span data-stu-id="4bb59-127">`PopulateTriggerControlID` element which triggers the web service call</span></span>
- <span data-ttu-id="4bb59-128">web サービス呼び出し中に対象の要素を空にするかどうかを `ClearContentsDuringUpdate` します。</span><span class="sxs-lookup"><span data-stu-id="4bb59-128">`ClearContentsDuringUpdate` whether to empty the target element during the web service call</span></span>

<span data-ttu-id="4bb59-129">ご覧のように、コントロールにはいくつかの情報が必要ですが、すべてを配置するのは非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="4bb59-129">As you can see, the control requires some information but putting everything into place is quite straight-forward.</span></span> <span data-ttu-id="4bb59-130">現在のシナリオでの `DynamicPopulateExtender` コントロールのマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="4bb59-130">Here is the markup for the `DynamicPopulateExtender` control in the current scenario:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="4bb59-131">ブラウザーで ASP.NET ページを実行し、ボタンをクリックします。現在の日付が月-日-年形式で表示されます。</span><span class="sxs-lookup"><span data-stu-id="4bb59-131">Run the ASP.NET page in the browser and click on the button; you will receive the current date in month-day-year format.</span></span>

<span data-ttu-id="4bb59-132">[![ボタンをクリックすると、サーバーから日付が取得されます。](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4bb59-132">[![A click on the button retrieves the date from the server](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="4bb59-133">このボタンをクリックすると、サーバーから日付が取得されます ([クリックすると、フルサイズの画像が表示](dynamically-populating-a-control-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="4bb59-133">A click on the button retrieves the date from the server ([Click to view full-size image](dynamically-populating-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4bb59-134">[前へ](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
> [次へ](dynamically-populating-a-control-using-javascript-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="4bb59-134">[Previous](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
[Next](dynamically-populating-a-control-using-javascript-code-vb.md)</span></span>
