---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: テキスト ボックス (VB) で特定の文字のみを許可する |Microsoft Docs
author: wenz
description: ASP.NET 検証コントロールは、ユーザー入力で特定の文字だけが許可されることを保証できます。 ただしこれができない無効な入力からユーザー.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: 6e0f13140fcafd666a89c27acb829e4e762eff29
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65127457"
---
# <a name="allowing-only-certain-characters-in-a-text-box-vb"></a><span data-ttu-id="f5080-104">テキスト ボックスで特定の文字だけを許可する (VB)</span><span class="sxs-lookup"><span data-stu-id="f5080-104">Allowing Only Certain Characters in a Text Box (VB)</span></span>

<span data-ttu-id="f5080-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f5080-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f5080-106">[コードのダウンロード](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip)または[PDF のダウンロード](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f5080-106">[Download Code](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span></span>

> <span data-ttu-id="f5080-107">ASP.NET 検証コントロールは、ユーザー入力で特定の文字だけが許可されることを保証できます。</span><span class="sxs-lookup"><span data-stu-id="f5080-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="f5080-108">ただしこのままでも、ユーザーから無効な文字を入力し、フォームを送信しようとしています。</span><span class="sxs-lookup"><span data-stu-id="f5080-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="overview"></a><span data-ttu-id="f5080-109">概要</span><span class="sxs-lookup"><span data-stu-id="f5080-109">Overview</span></span>

<span data-ttu-id="f5080-110">ASP.NET 検証コントロールは、ユーザー入力で特定の文字だけが許可されることを保証できます。</span><span class="sxs-lookup"><span data-stu-id="f5080-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="f5080-111">ただしこのままでも、ユーザーから無効な文字を入力し、フォームを送信しようとしています。</span><span class="sxs-lookup"><span data-stu-id="f5080-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="f5080-112">手順</span><span class="sxs-lookup"><span data-stu-id="f5080-112">Steps</span></span>

<span data-ttu-id="f5080-113">ASP.NET AJAX Control Toolkit に含まれています、`FilteredTextBox`をテキスト ボックスを拡張するコントロール。</span><span class="sxs-lookup"><span data-stu-id="f5080-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="f5080-114">アクティブ化される、文字の特定のセットのみがフィールドに入力可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f5080-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="f5080-115">これを機能させるには、まず必要があります通常どおり、ASP.NET AJAX `ScriptManager` ASP.NET AJAX Control Toolkit で使用されるも JavaScript ライブラリが読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="f5080-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

<span data-ttu-id="f5080-116">次に、テキスト ボックス必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5080-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

<span data-ttu-id="f5080-117">最後に、`FilteredTextBoxExtender`ユーザーが入力できる文字の制限の制御を行います。</span><span class="sxs-lookup"><span data-stu-id="f5080-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="f5080-118">最初に、設定、`TargetControlID`属性を`ID`の`TextBox`コントロール。</span><span class="sxs-lookup"><span data-stu-id="f5080-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="f5080-119">使用可能ないずれかを選択し、`FilterType`値。</span><span class="sxs-lookup"><span data-stu-id="f5080-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="f5080-120">`Custom` 既定値です。有効な文字の一覧を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5080-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="f5080-121">`LowercaseLetters` 小文字のみを使用</span><span class="sxs-lookup"><span data-stu-id="f5080-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="f5080-122">`Numbers` 数字のみ</span><span class="sxs-lookup"><span data-stu-id="f5080-122">`Numbers` digits only</span></span>
- <span data-ttu-id="f5080-123">`UppercaseLetters` 大文字のみ</span><span class="sxs-lookup"><span data-stu-id="f5080-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="f5080-124">場合、`Custom FilterType`を使用する、`ValidChars`プロパティが設定されていないと、入力可能性がありますの文字の一覧を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5080-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="f5080-125">方法: テキスト ボックスにテキストを貼り付けるしようとすると、すべての無効な文字が削除されます。</span><span class="sxs-lookup"><span data-stu-id="f5080-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="f5080-126">マークアップを次に示します、`FilteredTextBoxExtender`桁のみを実行できるコントロール (何も必要であったと考えられる`FilterType="Numbers"`)。</span><span class="sxs-lookup"><span data-stu-id="f5080-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

<span data-ttu-id="f5080-127">JavaScript が有効になっている場合は、文字を入力しようと複数のページを実行するには、アプリケーションは動作しません。ただし、桁の数字は、ページに表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5080-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="f5080-128">しかし注意保護`FilteredTextBox`提供強固ではありません。JavaScript が有効になっている場合は、ASP などの追加の検証方法を使用する必要があるために、テキスト ボックスで、すべてのデータを入力する可能性があります。NET の検証コントロール。</span><span class="sxs-lookup"><span data-stu-id="f5080-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>

<span data-ttu-id="f5080-129">[![数字のみを入力することがあります。](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f5080-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span></span>

<span data-ttu-id="f5080-130">数字のみを入力することがあります ([フルサイズの画像を表示する をクリックします](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="f5080-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f5080-131">前へ</span><span class="sxs-lookup"><span data-stu-id="f5080-131">Previous</span></span>](allowing-only-certain-characters-in-a-text-box-cs.md)
