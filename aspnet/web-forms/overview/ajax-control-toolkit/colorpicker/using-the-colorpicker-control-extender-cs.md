---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
title: カラーピッカー コントロール エクステンダ (C#) の使用 |マイクロソフトドキュメント
author: rick-anderson
description: ColorPicker は、ポップアップ コントロールの UI を使用してクライアント側の色を選択する機能を提供する AJAX エクステンダASP.NETです。 それは任意のASP.NETに取り付けることができます。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0d86a1e7-a910-4ab2-b85c-7a9ea6906c39
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 63b6bc58d36fdfcb5ee0a1c97988091e8d35505b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543133"
---
# <a name="using-the-colorpicker-control-extender-c"></a><span data-ttu-id="28a7d-104">カラーピッカー コントロール エクステンダーの使用 (C#)</span><span class="sxs-lookup"><span data-stu-id="28a7d-104">Using the ColorPicker Control Extender (C#)</span></span>

<span data-ttu-id="28a7d-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="28a7d-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="28a7d-106">ColorPicker は、ポップアップ コントロールの UI を使用してクライアント側の色を選択する機能を提供する AJAX エクステンダASP.NETです。</span><span class="sxs-lookup"><span data-stu-id="28a7d-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="28a7d-107">任意のASP.NET TextBox コントロールにアタッチできます。</span><span class="sxs-lookup"><span data-stu-id="28a7d-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="28a7d-108">それ。</span><span class="sxs-lookup"><span data-stu-id="28a7d-108">It.</span></span>

<span data-ttu-id="28a7d-109">このチュートリアルの目的は、AJAX コントロール ツールキット ColorPicker コントロール エクステンダーを使用する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="28a7d-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="28a7d-110">ColorPicker コントロール エクステンダは、色を選択できるポップアップ ダイアログを表示します。</span><span class="sxs-lookup"><span data-stu-id="28a7d-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="28a7d-111">ColorPicker は、ユーザーが色を選択するための直感的なユーザー インターフェイスを提供する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="28a7d-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="28a7d-112">カラー ピッカー コントロール エクステンダを使用したテキスト ボックス コントロールの拡張</span><span class="sxs-lookup"><span data-stu-id="28a7d-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="28a7d-113">たとえば、訪問者がカスタマイズされた名刺を作成できる Web サイトを作成するとします。</span><span class="sxs-lookup"><span data-stu-id="28a7d-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="28a7d-114">来場者は名刺のテキストを入力し、色を選択することができます。</span><span class="sxs-lookup"><span data-stu-id="28a7d-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="28a7d-115">リスト 1 のASP.NET ページには、txtCardText と txtCardColor という名前の 2 つのテキスト ボックス コントロールがあります。</span><span class="sxs-lookup"><span data-stu-id="28a7d-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="28a7d-116">フォームを送信すると、選択した値が表示されます (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="28a7d-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>

<span data-ttu-id="28a7d-117">[![名刺を作成するための簡単なフォーム](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="28a7d-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)</span></span>

<span data-ttu-id="28a7d-118">**図 01**: 名刺を作成するための簡易フォーム ([フルサイズの画像を表示する をクリック](using-the-colorpicker-control-extender-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="28a7d-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image2.png))</span></span>

<span data-ttu-id="28a7d-119">**リスト 1 - カードの作成.aspx**</span><span class="sxs-lookup"><span data-stu-id="28a7d-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample1.aspx)]

<span data-ttu-id="28a7d-120">リスト 1 のフォームは機能しますが、優れたユーザー エクスペリエンスを提供しません。</span><span class="sxs-lookup"><span data-stu-id="28a7d-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="28a7d-121">ユーザーはテキストボックスに色を入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="28a7d-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="28a7d-122">ユーザーが特殊な色(例えば、エンドウ豆の緑のちょうど右の色合い)を望む場合、ユーザーは何の助けもなくHTMLカラーコードを把握する必要があります。</span><span class="sxs-lookup"><span data-stu-id="28a7d-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="28a7d-123">ColorPicker コントロール エクステンダーを使用すると、より優れたユーザー エクスペリエンスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="28a7d-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="28a7d-124">ColorPicker は、テキスト ボックス コントロールにフォーカスを移動するときに色のダイアログボックスを表示します (図 2 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="28a7d-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>

<span data-ttu-id="28a7d-125">[![カラーピッカー コントロール エクステンダ](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="28a7d-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)</span></span>

<span data-ttu-id="28a7d-126">**図 02**: ColorPicker コントロール エクステンダ ([フルサイズの画像を表示する をクリック](using-the-colorpicker-control-extender-cs/_static/image4.png)します )</span><span class="sxs-lookup"><span data-stu-id="28a7d-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image4.png))</span></span>

<span data-ttu-id="28a7d-127">ColorPicker コントロール エクステンダをリスト 1 のフォームで使用するには、次の 2 つの手順を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="28a7d-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="28a7d-128">ページにスクリプト マネージャー コントロールを追加する</span><span class="sxs-lookup"><span data-stu-id="28a7d-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="28a7d-129">ページに ColorPicker コントロール エクステンダーを追加します。</span><span class="sxs-lookup"><span data-stu-id="28a7d-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="28a7d-130">カラー ピッカーを使用する前に、ページにスクリプト マネージャーを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="28a7d-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="28a7d-131">ScriptManager を追加する適切な場所は、サーバー側&lt;フォーム&gt;タグの開始のすぐ下にあります。</span><span class="sxs-lookup"><span data-stu-id="28a7d-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="28a7d-132">ツールボックスからページに ScriptManager をドラッグできます (ScriptManager は AJAX 拡張機能タブの下にあります)。</span><span class="sxs-lookup"><span data-stu-id="28a7d-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="28a7d-133">または、サーバー側フォームの開始タグの下にあるソースビューに次のタグを入力することもできます。</span><span class="sxs-lookup"><span data-stu-id="28a7d-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="28a7d-134">&lt;asp:スクリプトマネージャー ID="スクリプトマネージャー1" ランサット="サーバー" /&gt;</span><span class="sxs-lookup"><span data-stu-id="28a7d-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="28a7d-135">ColorPicker コントロール エクステンダーをページに追加する最も簡単な方法は、デザイン ビューです。</span><span class="sxs-lookup"><span data-stu-id="28a7d-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="28a7d-136">txtCardColor テキスト ボックスの上にマウス ポインタを置くと、スマート タスク オプションが表示され、エクステンダを追加できます (図 3 参照)。</span><span class="sxs-lookup"><span data-stu-id="28a7d-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="28a7d-137">このオプションを選択すると、エクステンダー ウィザードが表示されます (図 4 参照)。</span><span class="sxs-lookup"><span data-stu-id="28a7d-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>

<span data-ttu-id="28a7d-138">[![エクステンダーの追加](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="28a7d-138">[![Adding an extender](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)</span></span>

<span data-ttu-id="28a7d-139">**図 03**: エクステンダの追加 ([フルサイズの画像を表示する をクリック](using-the-colorpicker-control-extender-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="28a7d-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image6.png))</span></span>

<span data-ttu-id="28a7d-140">[![エクステンダー ウィザードを使用したコントロール エクステンダの選択](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="28a7d-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)</span></span>

<span data-ttu-id="28a7d-141">**図 04**: エクステンダ ウィザードでコントロール エクステンダを選択する ([フルサイズのイメージを表示する をクリック](using-the-colorpicker-control-extender-cs/_static/image8.png)して )</span><span class="sxs-lookup"><span data-stu-id="28a7d-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image8.png))</span></span>

<span data-ttu-id="28a7d-142">カラー ピッカー エクステンダーを選択して、カラー ピッカー エクステンダーを使用して txtCardColor テキスト ボックスを拡張できます。</span><span class="sxs-lookup"><span data-stu-id="28a7d-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="28a7d-143">[OK] をクリックしてダイアログ ボックスを閉じます。</span><span class="sxs-lookup"><span data-stu-id="28a7d-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="28a7d-144">これらの変更を行うと、ページのソースはリスト 2 のようになります。</span><span class="sxs-lookup"><span data-stu-id="28a7d-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="28a7d-145">リスト 2 - CreateCard.aspx (カラーピッカーを使用)</span><span class="sxs-lookup"><span data-stu-id="28a7d-145">Listing 2 - CreateCard.aspx (with ColorPicker)</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample2.aspx)]

<span data-ttu-id="28a7d-146">ページには、テキスト ボックスのテキスト ボックスコントロールの真下に表示される ColorPickerExtender コントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="28a7d-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="28a7d-147">コントロールは、カラー ピッカー ダイアログを表示するように、txtCardColor コントロールを拡張します。</span><span class="sxs-lookup"><span data-stu-id="28a7d-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="28a7d-148">ボタンを使用してカラー ピッカー ダイアログを起動する</span><span class="sxs-lookup"><span data-stu-id="28a7d-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="28a7d-149">カラー ピッカー エクステンダーは、次のプロパティをサポートします。</span><span class="sxs-lookup"><span data-stu-id="28a7d-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="28a7d-150">PopupButtonId - カラー ピッカー ダイアログを表示するページのボタンの ID。</span><span class="sxs-lookup"><span data-stu-id="28a7d-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="28a7d-151">ポップアップ位置 - カラー ピッカー ダイアログのターゲット コントロールを基準とした位置。</span><span class="sxs-lookup"><span data-stu-id="28a7d-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="28a7d-152">指定できる値は、絶対値、中心、左下、左下、左、右上、右、左(デフォルトは下左)です。</span><span class="sxs-lookup"><span data-stu-id="28a7d-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="28a7d-153">サンプル コントロール Id - 選択した色を表示するコントロールの ID。</span><span class="sxs-lookup"><span data-stu-id="28a7d-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="28a7d-154">選択された色 - カラー ピッカーによって選択された初期色。</span><span class="sxs-lookup"><span data-stu-id="28a7d-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="28a7d-155">これらのプロパティを使用して、カラー ピッカー ダイアログの表示方法と選択した色の表示方法をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="28a7d-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="28a7d-156">リスト 3 のページでは、これらのプロパティの使用方法を示します。</span><span class="sxs-lookup"><span data-stu-id="28a7d-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="28a7d-157">**リスト 3 - カードボタンを作成します。**</span><span class="sxs-lookup"><span data-stu-id="28a7d-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample3.aspx)]

<span data-ttu-id="28a7d-158">リスト 3 のページには、[色の選択] ボタンが含まれています (図 5 を参照)。</span><span class="sxs-lookup"><span data-stu-id="28a7d-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="28a7d-159">このボタンをクリックすると、テキスト ボックスの上にカラー ピッカー ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="28a7d-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="28a7d-160">ダイアログボックスから色を選択すると、選択した色が lblSample Label コントロールの背景色として表示されます。</span><span class="sxs-lookup"><span data-stu-id="28a7d-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="28a7d-161">プロパティは、色の選択ボタンを ColorPicker エクステンダーに関連付けるために使用されます。</span><span class="sxs-lookup"><span data-stu-id="28a7d-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="28a7d-162">PopupButtonID プロパティの値を指定すると、ターゲット コントロールにフォーカスがあるときに、カラー ピッカー ダイアログが表示されなくなります。</span><span class="sxs-lookup"><span data-stu-id="28a7d-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="28a7d-163">ダイアログを表示するには、ボタンをクリックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="28a7d-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="28a7d-164">プロパティは、選択した色を表示するコントロールを ColorPicker に関連付けるために使用されます。</span><span class="sxs-lookup"><span data-stu-id="28a7d-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="28a7d-165">ColorPicker は、このコントロールの背景色を現在選択されている色に変更します。</span><span class="sxs-lookup"><span data-stu-id="28a7d-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>

<span data-ttu-id="28a7d-166">[![ボタンを使用したカラー ピッカー ダイアログの表示](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="28a7d-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)</span></span>

<span data-ttu-id="28a7d-167">**図 05**: ボタンを使用してカラー ピッカー ダイアログを表示する ([フルサイズの画像を表示する をクリック](using-the-colorpicker-control-extender-cs/_static/image10.png)して)</span><span class="sxs-lookup"><span data-stu-id="28a7d-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image10.png))</span></span>

## <a name="summary"></a><span data-ttu-id="28a7d-168">まとめ</span><span class="sxs-lookup"><span data-stu-id="28a7d-168">Summary</span></span>

<span data-ttu-id="28a7d-169">このチュートリアルでは、ColorPicker コントロール エクステンダーを使用してポップアップカラー ピッカー ダイアログを表示する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="28a7d-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="28a7d-170">まず、フォーカスが TextBox コントロールに移動したときにダイアログを表示する方法を調べました。</span><span class="sxs-lookup"><span data-stu-id="28a7d-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="28a7d-171">次に、ボタンがクリックされたときにカラー ピッカー ダイアログを表示するボタンを作成する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="28a7d-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="28a7d-172">次へ</span><span class="sxs-lookup"><span data-stu-id="28a7d-172">Next</span></span>](using-the-colorpicker-control-extender-vb.md)
