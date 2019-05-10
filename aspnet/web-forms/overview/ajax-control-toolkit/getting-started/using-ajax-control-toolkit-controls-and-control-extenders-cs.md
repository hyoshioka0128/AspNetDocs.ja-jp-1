---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: AJAX Control Toolkit のコントロールとコントロール エクステンダー (c#) を使用して |Microsoft Docs
author: microsoft
description: ASP.NET ページに AJAX Control Toolkit のコントロールとエクステンダーを追加する方法について説明します。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 1acafaadaf373b488b9e85b7ba31f08cd3b53e85
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65127102"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a><span data-ttu-id="60f33-103">AJAX Control Toolkit のコントロールとコントロール エクステンダーを使用する (C#)</span><span class="sxs-lookup"><span data-stu-id="60f33-103">Using AJAX Control Toolkit Controls and Control Extenders (C#)</span></span>

<span data-ttu-id="60f33-104">によって[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="60f33-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="60f33-105">ASP.NET ページに AJAX Control Toolkit のコントロールとエクステンダーを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="60f33-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>

<span data-ttu-id="60f33-106">AJAX Control Toolkit には、コントロールとコントロール エクステンダーのセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="60f33-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="60f33-107">この簡単なチュートリアルでは、ASP.NET ページにコントロールとコントロール エクステンダーの両方を追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="60f33-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="60f33-108">AJAX Control Toolkit をインストールして、AJAX Control Toolkit を Visual Studio または Visual Web Developer ツールボックスに追加する手順については、チュートリアルを参照してください。 [、AJAX Control Toolkit の概要](get-started-with-the-ajax-control-toolkit-cs.md)します。</span><span class="sxs-lookup"><span data-stu-id="60f33-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).</span></span>

## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="60f33-109">AJAX Control Toolkit のコントロールを使用します。</span><span class="sxs-lookup"><span data-stu-id="60f33-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="60f33-110">通常の ASP.NET コントロールと同様、AJAX Control Toolkit コントロールが動作します。</span><span class="sxs-lookup"><span data-stu-id="60f33-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="60f33-111">ASP.NET ページには、ツールボックスからコントロールをドラッグすることができます。</span><span class="sxs-lookup"><span data-stu-id="60f33-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="60f33-112">デザイン ビューまたはソース ビュー内のページにコントロールを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="60f33-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="60f33-113">1 つの特別な要件がある、AJAX Control Toolkit のコントロールを使用する場合。</span><span class="sxs-lookup"><span data-stu-id="60f33-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="60f33-114">ページには、ScriptManager コントロールを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="60f33-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="60f33-115">ScriptManager コントロールは、AJAX Control Toolkit コントロールに必要なために必要な JavaScript のすべてを含む責任を負います。</span><span class="sxs-lookup"><span data-stu-id="60f33-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="60f33-116">たとえば、AJAX Control Toolkit タブには、エディター コントロールをという名前のコントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="60f33-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="60f33-117">このコントロールには、リッチ HTML エディターが表示されます。</span><span class="sxs-lookup"><span data-stu-id="60f33-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="60f33-118">エディター コントロールをページに追加するのに次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="60f33-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="60f33-119">ShowEditor.aspx をという名前の新しい ASP.NET ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="60f33-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="60f33-120">ツールボックスで、[AJAX Extensions] タブの下から、ScriptManager コントロールを選択し、ページにコントロールをドラッグします。</span><span class="sxs-lookup"><span data-stu-id="60f33-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="60f33-121">ツールボックスで、AJAX Control Toolkit タブの下からエディター コントロールを選択し、ページ上にコントロールをドラッグします (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="60f33-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="60f33-122">デザイナーは、図 2 のようになります。</span><span class="sxs-lookup"><span data-stu-id="60f33-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="60f33-123">メニュー オプションを選択して、web サイトを実行**デバッグ、デバッグの開始**または F5 キーを押します。</span><span class="sxs-lookup"><span data-stu-id="60f33-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="60f33-124">図 3 のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="60f33-124">You should see the page in Figure 3.</span></span>

<span data-ttu-id="60f33-125">[![HTML エディター コントロールの選択](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="60f33-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span></span>

<span data-ttu-id="60f33-126">**図 01**:HTML エディター コントロールを選択 ([フルサイズの画像を表示する をクリックします](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))。</span><span class="sxs-lookup"><span data-stu-id="60f33-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span></span>

<span data-ttu-id="60f33-127">[![Visual Studio のデザイナーで編集して ScriptManager コントロール](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="60f33-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span></span>

<span data-ttu-id="60f33-128">**図 02**:Scriptmanager コントロールと編集コントロールでの visual Studio デザイナー ([フルサイズの画像を表示する をクリックします](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))。</span><span class="sxs-lookup"><span data-stu-id="60f33-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span></span>

<span data-ttu-id="60f33-129">[![DisplayEditor.aspx ページ](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="60f33-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span></span>

<span data-ttu-id="60f33-130">**図 03**:DisplayEditor.aspx ページ ([フルサイズの画像を表示する をクリックします](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))。</span><span class="sxs-lookup"><span data-stu-id="60f33-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span></span>

## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="60f33-131">AJAX Control Toolkit コントロール エクステンダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="60f33-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="60f33-132">AJAX Control Toolkit には、コントロール エクステンダーも含まれています。</span><span class="sxs-lookup"><span data-stu-id="60f33-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="60f33-133">その名前からわかるように、コントロール エクステンダーは、既存のコントロールの機能を拡張します。</span><span class="sxs-lookup"><span data-stu-id="60f33-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="60f33-134">たとえば、ConfirmButton コントロール エクステンダーは、標準の ASP.NET のボタン コントロールを拡張します。</span><span class="sxs-lookup"><span data-stu-id="60f33-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="60f33-135">エクステンダーは、ボタンのコントロールの動作を変更して、ボタンをクリックすると、確認のダイアログ ボックスを表示するようにします。</span><span class="sxs-lookup"><span data-stu-id="60f33-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="60f33-136">AJAX Control Toolkit コントロールと同様、コントロールのエクステンダーでは、ScriptManager コントロールが必要です。</span><span class="sxs-lookup"><span data-stu-id="60f33-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="60f33-137">ページ コントロール エクステンダーを使用する前に、ページに ScriptManager コントロールを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="60f33-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="60f33-138">ConfirmButton コントロール エクステンダーを使用して、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="60f33-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="60f33-139">ShowConfirmButton.aspx をという名前の新しい ASP.NET ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="60f33-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="60f33-140">AJAX Extensions タブの下からページにコントロールをドラッグして、ページに ScriptManager コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="60f33-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="60f33-141">デザイナー画面には、ツールボックスの [標準] タブの下から、ボタンをドラッグして、ページに標準のボタン コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="60f33-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="60f33-142">をクリックして、 **Extender の追加**タスク オプション (図 4 参照)。</span><span class="sxs-lookup"><span data-stu-id="60f33-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="60f33-143">エクステンダーの選択 ダイアログ ボックスで、ConfirmButtonExtender を選択します (図 5 を参照してください)、ok ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="60f33-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="60f33-144">デザイナーでボタン コントロールを選択し、エクステンダー、Button1 の展開\_ConfirmButtonExtender ノードで、[プロパティ] ウィンドウ (図 6 参照)。</span><span class="sxs-lookup"><span data-stu-id="60f33-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="60f33-145">値を割り当てる*本当ですか?* ConfirmText プロパティにします。</span><span class="sxs-lookup"><span data-stu-id="60f33-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="60f33-146">メニュー オプションを選択して、ページの実行**デバッグ、デバッグの開始**または F5 キーを押します。</span><span class="sxs-lookup"><span data-stu-id="60f33-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>

<span data-ttu-id="60f33-147">[![Extender の追加のタスク オプション](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="60f33-147">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span></span>

<span data-ttu-id="60f33-148">**図 04**:[Extender の追加のタスクのオプション ([フルサイズの画像を表示する] をクリックします](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))。</span><span class="sxs-lookup"><span data-stu-id="60f33-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span></span>

<span data-ttu-id="60f33-149">[![ConfirmButton コントロール エクステンダーを選択します。](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="60f33-149">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span></span>

<span data-ttu-id="60f33-150">**図 05**:ConfirmButton コントロール エクステンダーを選択すると ([フルサイズの画像を表示する をクリックします](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))。</span><span class="sxs-lookup"><span data-stu-id="60f33-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span></span>

<span data-ttu-id="60f33-151">[![ConfirmButton プロパティの設定](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="60f33-151">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span></span>

<span data-ttu-id="60f33-152">**図 06**:ConfirmButton プロパティの設定 ([フルサイズの画像を表示する をクリックします](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))。</span><span class="sxs-lookup"><span data-stu-id="60f33-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span></span>

<span data-ttu-id="60f33-153">ページが開いたら、ボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="60f33-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="60f33-154">ボタンをクリックすると、図 7 確認のダイアログ ボックスを取得します。</span><span class="sxs-lookup"><span data-stu-id="60f33-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>

<span data-ttu-id="60f33-155">[![確認のダイアログ ボックスを表示します。](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="60f33-155">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span></span>

<span data-ttu-id="60f33-156">**図 07**:確認のダイアログ ボックスを表示する ([フルサイズの画像を表示する をクリックします](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))。</span><span class="sxs-lookup"><span data-stu-id="60f33-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span></span>

<span data-ttu-id="60f33-157">通常ドラッグしないコントロール エクステンダーをページに注意してください。</span><span class="sxs-lookup"><span data-stu-id="60f33-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="60f33-158">代わりに、使用、 **Extender の追加**タスク ページに既に追加したコントロールにエクステンダーを追加するオプション。</span><span class="sxs-lookup"><span data-stu-id="60f33-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="60f33-159">さらに、設定することコントロール エクステンダー プロパティを開いて拡張されるコントロールのプロパティ シートに注意してください。</span><span class="sxs-lookup"><span data-stu-id="60f33-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="60f33-160">1 つの ASP.NET コントロールは、複数のコントロール エクステンダーによって拡張できます。</span><span class="sxs-lookup"><span data-stu-id="60f33-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="60f33-161">拡張されるコントロールのプロパティ シートでは、コントロールに関連付けられたコントロール エクステンダーのすべてを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="60f33-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="60f33-162">[前へ](get-started-with-the-ajax-control-toolkit-cs.md)
> [次へ](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span><span class="sxs-lookup"><span data-stu-id="60f33-162">[Previous](get-started-with-the-ajax-control-toolkit-cs.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span></span>
