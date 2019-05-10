---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: (C#) の検証コントロールと共に TextBoxWatermark を使用 |Microsoft Docs
author: wenz
description: AJAX Control Toolkit で TextBoxWatermark コントロールでは、テキスト ボックスを拡張するので、ボックス内でテキストが表示されます。 ボックスに、ユーザーがクリックしたときに.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 6ed3777e72adbb1a648a6f5215820d597a13bc92
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124502"
---
# <a name="using-textboxwatermark-with-validation-controls-c"></a><span data-ttu-id="ee323-104">検証コントロールと共に TextBoxWatermark を使用する (C#)</span><span class="sxs-lookup"><span data-stu-id="ee323-104">Using TextBoxWatermark With Validation Controls (C#)</span></span>

<span data-ttu-id="ee323-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ee323-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ee323-106">[コードのダウンロード](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip)または[PDF のダウンロード](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ee323-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)</span></span>

> <span data-ttu-id="ee323-107">AJAX Control Toolkit で TextBoxWatermark コントロールでは、テキスト ボックスを拡張するので、ボックス内でテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ee323-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="ee323-108">ボックスに、ユーザーがクリックするは空になります。</span><span class="sxs-lookup"><span data-stu-id="ee323-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="ee323-109">ユーザーがテキストを入力しなくても、ボックスのまま、指定済みのテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ee323-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="ee323-110">これは、同じ ページで、ASP.NET 検証コントロールと衝突する可能性がありますが、これらの問題を克服することがあります。</span><span class="sxs-lookup"><span data-stu-id="ee323-110">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="overview"></a><span data-ttu-id="ee323-111">概要</span><span class="sxs-lookup"><span data-stu-id="ee323-111">Overview</span></span>

<span data-ttu-id="ee323-112">`TextBoxWatermark`ボックス内でテキストが表示されるように、AJAX Control Toolkit のコントロールがテキスト ボックスを拡張します。</span><span class="sxs-lookup"><span data-stu-id="ee323-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="ee323-113">ボックスに、ユーザーがクリックするは空になります。</span><span class="sxs-lookup"><span data-stu-id="ee323-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="ee323-114">ユーザーがテキストを入力しなくても、ボックスのまま、指定済みのテキストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ee323-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="ee323-115">これは、同じ ページで、ASP.NET 検証コントロールと衝突する可能性がありますが、これらの問題を克服することがあります。</span><span class="sxs-lookup"><span data-stu-id="ee323-115">This may collide with ASP.NET Validation Controls on the same page, but these issues may be overcome.</span></span>

## <a name="steps"></a><span data-ttu-id="ee323-116">手順</span><span class="sxs-lookup"><span data-stu-id="ee323-116">Steps</span></span>

<span data-ttu-id="ee323-117">サンプルの基本的なセットアップは、次:`TextBox`を使用してコントロールを透かし、`TextBoxWatermarkExtender`コントロール。</span><span class="sxs-lookup"><span data-stu-id="ee323-117">The basic setup of the sample is the following: a `TextBox` control is watermarked using a `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="ee323-118">ボタンは、ポストバックをトリガーし、後で、ページの検証コントロールのトリガーに使用されます。</span><span class="sxs-lookup"><span data-stu-id="ee323-118">A button triggers a postback and will later be used to trigger the validation controls on the page.</span></span> <span data-ttu-id="ee323-119">また、`ScriptManager`コントロールが ASP.NET AJAX を初期化するために必要です。</span><span class="sxs-lookup"><span data-stu-id="ee323-119">Also, a `ScriptManager` control is required to initialize ASP.NET AJAX:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="ee323-120">ここで追加、`RequiredFieldValidator`かどうかにテキストが、フィールド、フォームが送信されたときにチェックするコントロール。</span><span class="sxs-lookup"><span data-stu-id="ee323-120">Now add a `RequiredFieldValidator` control that checks whether there is text in the field when the form is submitted.</span></span> <span data-ttu-id="ee323-121">`InitialValue`検証コントロールのプロパティで使用されているのと同じ値に設定する必要があります、`TextBoxWatermarkExtender`コントロール。フォームが送信されたときに、変更されていないテキスト ボックスの値はその中の基準値に。</span><span class="sxs-lookup"><span data-stu-id="ee323-121">The `InitialValue` property of the validator must be set to the same value that is used in the `TextBoxWatermarkExtender` control: When the form is submitted, the value of an unchanged textbox is the watermark value within it:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="ee323-122">ただしこのアプローチの 1 つの問題があります。場合は、クライアントは、JavaScript を無効化、テキスト フィールドがないあらかじめ入力されています、透かしテキストをそのため、`RequiredFieldValidator`エラー メッセージは発生しません。</span><span class="sxs-lookup"><span data-stu-id="ee323-122">However there is one problem with this approach: If the client disables JavaScript, the text field is not prefilled with the watermark text, therefore the `RequiredFieldValidator` does not trigger an error message.</span></span> <span data-ttu-id="ee323-123">そのため、2 つ目`RequiredFieldValidator`コントロールが必要ですが、空のテキスト ボックスを確認します (省略すると、`InitialValue`属性)。</span><span class="sxs-lookup"><span data-stu-id="ee323-123">Therefore, a second `RequiredFieldValidator` control is required which checks for an empty text box (omitting the `InitialValue` attribute).</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="ee323-124">両方の検証コントロールを使用しているため`Display` = `"Dynamic"`、エンドユーザーが発生した、この 2 つの検証コントロールの外観から区別できません。 代わりに、ように見えますが、1 つだけです。</span><span class="sxs-lookup"><span data-stu-id="ee323-124">Since both validators use `Display`=`"Dynamic"`, the end user cannot distinguish from the visual appearance which of the two validators was fired; instead, it looks like there was only one of them.</span></span>

<span data-ttu-id="ee323-125">最後に、検証コントロールには、エラー メッセージ発行いない場合、フィールド内のテキストを出力するいくつかのサーバー側コードを追加します。</span><span class="sxs-lookup"><span data-stu-id="ee323-125">Finally, add some server-side code to output the text in the field if no validator issued an error message:</span></span>

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="ee323-126">[![検証コントロール文句を言う フィールドにテキストがないこと](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ee323-126">[![The validator complains that there is no text in the field](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="ee323-127">検証コントロール文句を言う フィールドにテキストがないこと ([フルサイズの画像を表示する をクリックします](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="ee323-127">The validator complains that there is no text in the field ([Click to view full-size image](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ee323-128">[前へ](using-textboxwatermark-in-a-formview-cs.md)
> [次へ](using-textboxwatermark-in-a-formview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ee323-128">[Previous](using-textboxwatermark-in-a-formview-cs.md)
[Next](using-textboxwatermark-in-a-formview-vb.md)</span></span>
