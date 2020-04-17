---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: AJAX コントロール ツールキット コントロールとコントロール エクステンダ (VB) を使用する |マイクロソフトドキュメント
author: rick-anderson
description: AJAX コントロール ツールキット コントロールとエクステンダーをASP.NET ページに追加する方法について説明します。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 129d6841bc4db62ecbe5f26c4830d1ce2f199bff
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540013"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a><span data-ttu-id="f505d-103">AJAX Control Toolkit のコントロールとコントロール エクステンダーを使用する (VB)</span><span class="sxs-lookup"><span data-stu-id="f505d-103">Using AJAX Control Toolkit Controls and Control Extenders (VB)</span></span>

<span data-ttu-id="f505d-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f505d-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="f505d-105">AJAX コントロール ツールキット コントロールとエクステンダーをASP.NET ページに追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f505d-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>

<span data-ttu-id="f505d-106">AJAX コントロール ツールキットには、コントロールとコントロール エクステンダのセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f505d-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="f505d-107">この簡単なチュートリアルでは、コントロールとコントロール エクステンダの両方をASP.NET ページに追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f505d-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f505d-108">AJAX コントロール ツールキットをインストールし、AJAX コントロール ツールキットを Visual Studio/Visual Web 開発者ツールボックスに追加する手順については[、「AJAX コントロール ツールキットの概要](get-started-with-the-ajax-control-toolkit-vb.md)」のチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="f505d-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb.md).</span></span>

## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="f505d-109">AJAX コントロール ツールキット コントロールの使用</span><span class="sxs-lookup"><span data-stu-id="f505d-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="f505d-110">AJAX コントロール ツールキット コントロールは、通常のASP.NET コントロールと同じように機能します。</span><span class="sxs-lookup"><span data-stu-id="f505d-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="f505d-111">ツールボックスからASP.NETページにコントロールをドラッグできます。</span><span class="sxs-lookup"><span data-stu-id="f505d-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="f505d-112">デザイン ビューまたはソース ビューで、ページにコントロールを追加できます。</span><span class="sxs-lookup"><span data-stu-id="f505d-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="f505d-113">AJAX コントロール ツールキットのコントロールを使用する場合、1 つの特別な要件があります。</span><span class="sxs-lookup"><span data-stu-id="f505d-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="f505d-114">ページには、スクリプト マネージャー コントロールが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="f505d-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="f505d-115">コントロールは、AJAX コントロール ツールキット コントロールに必要なすべての必要な JavaScript を含める役割を担います。</span><span class="sxs-lookup"><span data-stu-id="f505d-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="f505d-116">たとえば、AJAX コントロール ツールキット タブには、エディター コントロールという名前のコントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f505d-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="f505d-117">このコントロールは、リッチ HTML エディターを表示します。</span><span class="sxs-lookup"><span data-stu-id="f505d-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="f505d-118">エディター コントロールをページに追加するには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="f505d-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="f505d-119">ShowEditor.aspx という名前の新しいASP.NET ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="f505d-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="f505d-120">ツールボックスの [AJAX 拡張] タブの下にある ScriptManager コントロールを選択し、コントロールをページにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="f505d-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="f505d-121">ツールボックスの [AJAX コントロール ツールキット] タブの下にある [エディター] コントロールを選択し、コントロールをページにドラッグします (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="f505d-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="f505d-122">デザイナーは図 2 のようになります。</span><span class="sxs-lookup"><span data-stu-id="f505d-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="f505d-123">メニュー オプションの **[デバッグ]、[デバッグの開始] を**選択するか、または F5 キーを押して、Web サイトを実行します。</span><span class="sxs-lookup"><span data-stu-id="f505d-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="f505d-124">図 3 にページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f505d-124">You should see the page in Figure 3.</span></span>

<span data-ttu-id="f505d-125">[![HTML エディター コントロールの選択](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f505d-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)</span></span>

<span data-ttu-id="f505d-126">**図 01**: HTML エディタ コントロールの選択 ([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="f505d-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))</span></span>

<span data-ttu-id="f505d-127">[![スクリプト マネージャーと編集コントロールを使用したビジュアル スタジオ デザイナー](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="f505d-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)</span></span>

<span data-ttu-id="f505d-128">**図 02**: スクリプト マネージャーと編集コントロールを持つ Visual Studio デザイナー ([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png)します )</span><span class="sxs-lookup"><span data-stu-id="f505d-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))</span></span>

<span data-ttu-id="f505d-129">[![表示エディター.aspx ページ](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="f505d-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)</span></span>

<span data-ttu-id="f505d-130">**図 03**: DisplayEditor.aspx ページ ([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png)します )</span><span class="sxs-lookup"><span data-stu-id="f505d-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))</span></span>

## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="f505d-131">AJAX コントロール ツールキット コントロール エクステンダの使用</span><span class="sxs-lookup"><span data-stu-id="f505d-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="f505d-132">AJAX コントロール ツールキットには、コントロール エクステンダも含まれています。</span><span class="sxs-lookup"><span data-stu-id="f505d-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="f505d-133">名前が示すように、コントロール エクステンダは既存のコントロールの機能を拡張します。</span><span class="sxs-lookup"><span data-stu-id="f505d-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="f505d-134">たとえば、ConfirmButton コントロール エクステンダーは、標準のASP.NET ボタン コントロールを拡張します。</span><span class="sxs-lookup"><span data-stu-id="f505d-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="f505d-135">エクステンダは、ボタン コントロールの動作を変更して、ボタンをクリックすると確認ダイアログボックスが表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="f505d-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="f505d-136">コントロール エクステンダは、AJAX コントロール ツールキット コントロールと同様に、ScriptManager コントロールを必要とします。</span><span class="sxs-lookup"><span data-stu-id="f505d-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="f505d-137">ページでコントロール エクステンダーを使用する前に、ページに ScriptManager コントロールを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f505d-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="f505d-138">確認ボタン コントロール エクステンダーを使用するには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="f505d-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="f505d-139">という名前の新しいASP.NET ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="f505d-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="f505d-140">コントロールをページにドラッグして、ページに ScriptManager コントロールを追加する、 AJAX 拡張機能タブ。</span><span class="sxs-lookup"><span data-stu-id="f505d-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="f505d-141">ツールボックスの [標準] タブの下にある [ボタン] をデザイナー画面にドラッグして、標準の Button コントロールをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="f505d-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="f505d-142">エクス**テンダーの追加**タスク オプションをクリックします (図 4 を参照)。</span><span class="sxs-lookup"><span data-stu-id="f505d-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="f505d-143">[エクステンダの選択] ダイアログで、[ボタンエクステンダーの確認] (図 5 を参照) を選択し、[OK] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f505d-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="f505d-144">デザイナーでボタン コントロールを選択し、プロパティ ウィンドウでエクステン\_ダー、ボタン 1 確認ボタンエクステンダー ノードを展開します (図 6 を参照)。</span><span class="sxs-lookup"><span data-stu-id="f505d-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="f505d-145">値を *[本当に?* ] プロパティに代入します。</span><span class="sxs-lookup"><span data-stu-id="f505d-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="f505d-146">メニュー オプション[**デバッグ]、[デバッグの開始]、** または [F5 キー] をクリックして、ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="f505d-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>

<span data-ttu-id="f505d-147">[![エクステンダーの追加タスク オプション](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f505d-147">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)</span></span>

<span data-ttu-id="f505d-148">**図 04**: エクステンダーの追加タスク オプション ([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="f505d-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))</span></span>

<span data-ttu-id="f505d-149">[![確認ボタン コントロール エクステンダーの選択](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="f505d-149">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)</span></span>

<span data-ttu-id="f505d-150">**図 05**: ConfirmButton コントロール エクステンダの選択 ([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="f505d-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))</span></span>

<span data-ttu-id="f505d-151">[![プロパティを設定する](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="f505d-151">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)</span></span>

<span data-ttu-id="f505d-152">**図 06**: ConfirmButton プロパティの設定 ([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png)します)</span><span class="sxs-lookup"><span data-stu-id="f505d-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))</span></span>

<span data-ttu-id="f505d-153">ページが開くと、ボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f505d-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="f505d-154">ボタンをクリックすると、図 7 の確認ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f505d-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>

<span data-ttu-id="f505d-155">[![確認ダイアログの表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="f505d-155">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)</span></span>

<span data-ttu-id="f505d-156">**図07**: 確認ダイアログを表示する([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="f505d-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))</span></span>

<span data-ttu-id="f505d-157">通常は、コントロール エクステンダをページにドラッグしないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f505d-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="f505d-158">代わりに、**エクステンダーの追加**タスク オプションを使用して、ページに既に追加したコントロールにエクステンダを追加します。</span><span class="sxs-lookup"><span data-stu-id="f505d-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="f505d-159">さらに、拡張するコントロールのプロパティ シートを開いて、コントロール エクステンダープロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="f505d-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="f505d-160">複数のコントロール エクステンダによって、1 つのASP.NET コントロールを拡張できます。</span><span class="sxs-lookup"><span data-stu-id="f505d-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="f505d-161">拡張されるコントロールのプロパティ シートには、コントロールに関連付けられているすべてのコントロール エクステンダが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f505d-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f505d-162">[前へ](get-started-with-the-ajax-control-toolkit-vb.md)
> [次へ](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f505d-162">[Previous](get-started-with-the-ajax-control-toolkit-vb.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)</span></span>
