---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
title: FormView のテンプレート (VB) を使用して |Microsoft Docs
author: rick-anderson
description: DetailsView とは異なり、FormView いないフィールドで構成されます。 代わりに、テンプレートを使用して、フォーム ビューがレンダリングされます。 このチュートリアルでは、F. の使用について説明します.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 67b25f4c-2823-42b6-b07d-1d650b3fd711
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
msc.type: authoredcontent
ms.openlocfilehash: 6d16ef7ef8a3d5fce10e0d0b88421be294e9fc8d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57055109"
---
<a name="using-the-formviews-templates-vb"></a><span data-ttu-id="fa078-105">FormView のテンプレート (VB) を使用します。</span><span class="sxs-lookup"><span data-stu-id="fa078-105">Using the FormView's Templates (VB)</span></span>
====================
<span data-ttu-id="fa078-106">によって[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="fa078-106">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="fa078-107">[サンプル アプリをダウンロード](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_14_VB.exe)または[PDF のダウンロード](using-the-formview-s-templates-vb/_static/datatutorial14vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="fa078-107">[Download Sample App](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_14_VB.exe) or [Download PDF](using-the-formview-s-templates-vb/_static/datatutorial14vb1.pdf)</span></span>

> <span data-ttu-id="fa078-108">DetailsView とは異なり、FormView いないフィールドで構成されます。</span><span class="sxs-lookup"><span data-stu-id="fa078-108">Unlike the DetailsView, the FormView is not composed of fields.</span></span> <span data-ttu-id="fa078-109">代わりに、テンプレートを使用して、フォーム ビューがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="fa078-109">Instead, the FormView is rendered using templates.</span></span> <span data-ttu-id="fa078-110">取り上げるこのチュートリアルでは、FormView コントロールを使用して、データの小さい固定表示を表示します。</span><span class="sxs-lookup"><span data-stu-id="fa078-110">In this tutorial we'll examine using the FormView control to present a less rigid display of data.</span></span>


## <a name="introduction"></a><span data-ttu-id="fa078-111">はじめに</span><span class="sxs-lookup"><span data-stu-id="fa078-111">Introduction</span></span>

<span data-ttu-id="fa078-112">最後の 2 つのチュートリアルでは、カスタマイズ TemplateFields を使用する GridView および DetailsView コントロールの出力方法を説明しました。</span><span class="sxs-lookup"><span data-stu-id="fa078-112">In the last two tutorials we saw how to customize the GridView and DetailsView controls' outputs using TemplateFields.</span></span> <span data-ttu-id="fa078-113">TemplateFields を高度にカスタマイズするには、特定のフィールドの内容を許可するが、最終的に、GridView と DetailsView が角張ったではなく、グリッドのような外観。</span><span class="sxs-lookup"><span data-stu-id="fa078-113">TemplateFields allow for the contents for a specific field to be highly customized, but in the end both the GridView and DetailsView have a rather boxy, grid-like appearance.</span></span> <span data-ttu-id="fa078-114">多くのシナリオは、このようなグリッドのようなレイアウトに最適ですより滑らかな、小さい剛体の表示が必要な時です。</span><span class="sxs-lookup"><span data-stu-id="fa078-114">For many scenarios such a grid-like layout is ideal, but at times a more fluid, less rigid display is needed.</span></span> <span data-ttu-id="fa078-115">1 つのレコードを表示するときに、このような滑らかなレイアウトは、FormView コントロールを使用する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="fa078-115">When displaying a single record, such a fluid layout is possible using the FormView control.</span></span>

<span data-ttu-id="fa078-116">DetailsView とは異なり、FormView いないフィールドで構成されます。</span><span class="sxs-lookup"><span data-stu-id="fa078-116">Unlike the DetailsView, the FormView is not composed of fields.</span></span> <span data-ttu-id="fa078-117">FormView に BoundField または TemplateField を追加することはできません。</span><span class="sxs-lookup"><span data-stu-id="fa078-117">You can't add a BoundField or TemplateField to a FormView.</span></span> <span data-ttu-id="fa078-118">代わりに、テンプレートを使用して、フォーム ビューがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="fa078-118">Instead, the FormView is rendered using templates.</span></span> <span data-ttu-id="fa078-119">含む 1 つ TemplateField DetailsView コントロールと FormView を考えます。</span><span class="sxs-lookup"><span data-stu-id="fa078-119">Think of the FormView as a DetailsView control that contains a single TemplateField.</span></span> <span data-ttu-id="fa078-120">FormView では、次のテンプレートがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="fa078-120">The FormView supports the following templates:</span></span>

- <span data-ttu-id="fa078-121">`ItemTemplate` FormView で表示される特定のレコードを表示するために使用</span><span class="sxs-lookup"><span data-stu-id="fa078-121">`ItemTemplate` used to render the particular record displayed in the FormView</span></span>
- <span data-ttu-id="fa078-122">`HeaderTemplate` 省略可能なヘッダー行を指定するために使用</span><span class="sxs-lookup"><span data-stu-id="fa078-122">`HeaderTemplate` used to specify an optional header row</span></span>
- <span data-ttu-id="fa078-123">`FooterTemplate` 省略可能なフッター行を指定するために使用</span><span class="sxs-lookup"><span data-stu-id="fa078-123">`FooterTemplate` used to specify an optional footer row</span></span>
- <span data-ttu-id="fa078-124">`EmptyDataTemplate` FormView の`DataSource`任意のレコードがない、`EmptyDataTemplate`の代わりに使用されて、`ItemTemplate`コントロールのマークアップをレンダリングするため</span><span class="sxs-lookup"><span data-stu-id="fa078-124">`EmptyDataTemplate` when the FormView's `DataSource` lacks any records, the `EmptyDataTemplate` is used in place of the `ItemTemplate` for rendering the control's markup</span></span>
- <span data-ttu-id="fa078-125">`PagerTemplate` ページングが有効になっている FormViews のページング インターフェイスをカスタマイズするために使用できます。</span><span class="sxs-lookup"><span data-stu-id="fa078-125">`PagerTemplate` can be used to customize the paging interface for FormViews that have paging enabled</span></span>
- <span data-ttu-id="fa078-126">`EditItemTemplate` / `InsertItemTemplate` このような機能をサポートする FormViews の編集インターフェイスまたは挿入のインターフェイスをカスタマイズするために使用</span><span class="sxs-lookup"><span data-stu-id="fa078-126">`EditItemTemplate` / `InsertItemTemplate` used to customize the editing interface or inserting interface for FormViews that support such functionality</span></span>

<span data-ttu-id="fa078-127">取り上げるこのチュートリアルでは、FormView コントロールを使用して、製品の小さい固定表示を表示します。</span><span class="sxs-lookup"><span data-stu-id="fa078-127">In this tutorial we'll examine using the FormView control to present a less rigid display of products.</span></span> <span data-ttu-id="fa078-128">名前、カテゴリ、供給業者とに、フォーム ビューのフィールドではなく`ItemTemplate`ヘッダー要素の組み合わせを使用してこれらの値が表示されます、 `<table>` (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="fa078-128">Rather than having fields for the name, category, supplier, and so on, the FormView's `ItemTemplate` will show these values using a combination of a header element and a `<table>` (see Figure 1).</span></span>


<span data-ttu-id="fa078-129">[![FormView は、DetailsView でグリッドのようなレイアウトのブレーク アウト](using-the-formview-s-templates-vb/_static/image2.png)](using-the-formview-s-templates-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fa078-129">[![The FormView Breaks Out of the Grid-Like Layout Seen in the DetailsView](using-the-formview-s-templates-vb/_static/image2.png)](using-the-formview-s-templates-vb/_static/image1.png)</span></span>

<span data-ttu-id="fa078-130">**図 1**:FormView が Grid-Like レイアウト表示から、DetailsView で中断されます ([フルサイズの画像を表示する をクリックします](using-the-formview-s-templates-vb/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="fa078-130">**Figure 1**: The FormView Breaks Out of the Grid-Like Layout Seen in the DetailsView ([Click to view full-size image](using-the-formview-s-templates-vb/_static/image3.png))</span></span>


## <a name="step-1-binding-the-data-to-the-formview"></a><span data-ttu-id="fa078-131">手順 1: FormView にデータをバインド</span><span class="sxs-lookup"><span data-stu-id="fa078-131">Step 1: Binding the Data to the FormView</span></span>

<span data-ttu-id="fa078-132">開く、`FormView.aspx`ページし、FormView をツールボックスからデザイナーにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="fa078-132">Open the `FormView.aspx` page and drag a FormView from the Toolbox onto the Designer.</span></span> <span data-ttu-id="fa078-133">まず、フォーム ビューを追加するときに私たちに指示する灰色のボックスとして表示される`ItemTemplate`が必要です。</span><span class="sxs-lookup"><span data-stu-id="fa078-133">When first adding the FormView it appears as a gray box, instructing us that an `ItemTemplate` is needed.</span></span>


<span data-ttu-id="fa078-134">[![ItemTemplate が提供されるまで、デザイナーで、フォーム ビューをレンダリングできません。](using-the-formview-s-templates-vb/_static/image5.png)](using-the-formview-s-templates-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="fa078-134">[![The FormView Cannot be Rendered in the Designer Until an ItemTemplate is Provided](using-the-formview-s-templates-vb/_static/image5.png)](using-the-formview-s-templates-vb/_static/image4.png)</span></span>

<span data-ttu-id="fa078-135">**図 2**:デザイナーまででレンダリング、FormView できません、`ItemTemplate`提供されます ([フルサイズの画像を表示する をクリックします](using-the-formview-s-templates-vb/_static/image6.png))。</span><span class="sxs-lookup"><span data-stu-id="fa078-135">**Figure 2**: The FormView Cannot be Rendered in the Designer Until an `ItemTemplate` is Provided ([Click to view full-size image](using-the-formview-s-templates-vb/_static/image6.png))</span></span>


<span data-ttu-id="fa078-136">`ItemTemplate` (宣言構文) を手動で作成することができますか、フォーム ビューをデザイナーによってデータ ソース コントロールにバインドすることによって自動作成をすることができます。</span><span class="sxs-lookup"><span data-stu-id="fa078-136">The `ItemTemplate` can be created by hand (through the declarative syntax) or can be auto-created by binding the FormView to a data source control through the Designer.</span></span> <span data-ttu-id="fa078-137">この自動作成`ItemTemplate`HTML、リストの各フィールドとラベルの名前を制御が含まれている`Text`プロパティ フィールドの値にバインドします。</span><span class="sxs-lookup"><span data-stu-id="fa078-137">This auto-created `ItemTemplate` contains HTML that lists the name of each field and a Label control whose `Text` property is bound to the field's value.</span></span> <span data-ttu-id="fa078-138">このアプローチも自動で作成、`InsertItemTemplate`と`EditItemTemplate`、どちらもはの各データ ソース コントロールによって返されるデータ フィールドの入力コントロールに設定されます。</span><span class="sxs-lookup"><span data-stu-id="fa078-138">This approach also auto-creates an `InsertItemTemplate` and `EditItemTemplate`, both of which are populated with input controls for each of the data fields returned by the data source control.</span></span>

<span data-ttu-id="fa078-139">追加を呼び出す新しい ObjectDataSource コントロールをフォーム ビューのスマート タグからのテンプレートを自動作成する場合、`ProductsBLL`クラスの`GetProducts()`メソッド。</span><span class="sxs-lookup"><span data-stu-id="fa078-139">If you want to auto-create the template, from the FormView's smart tag add a new ObjectDataSource control that invokes the `ProductsBLL` class's `GetProducts()` method.</span></span> <span data-ttu-id="fa078-140">これをフォーム ビューが作成されます、 `ItemTemplate`、 `InsertItemTemplate`、および`EditItemTemplate`します。</span><span class="sxs-lookup"><span data-stu-id="fa078-140">This will create a FormView with an `ItemTemplate`, `InsertItemTemplate`, and `EditItemTemplate`.</span></span> <span data-ttu-id="fa078-141">ソース ビューから削除、`InsertItemTemplate`と`EditItemTemplate`に興味がないためには、編集、またはまだ挿入をサポートする、FormView を作成します。</span><span class="sxs-lookup"><span data-stu-id="fa078-141">From the Source view, remove the `InsertItemTemplate` and `EditItemTemplate` since we're not interested in creating a FormView that supports editing or inserting yet.</span></span> <span data-ttu-id="fa078-142">次に、内のマークアップをクリアします、`ItemTemplate`から作業をクリーンな状態があるようにします。</span><span class="sxs-lookup"><span data-stu-id="fa078-142">Next, clear out the markup within the `ItemTemplate` so that we have a clean slate to work from.</span></span>

<span data-ttu-id="fa078-143">はなく構築する場合、 `ItemTemplate` 、手動で追加し、ツールボックスからデザイナーにドラッグすることによって、ObjectDataSource を構成します。</span><span class="sxs-lookup"><span data-stu-id="fa078-143">If you'd rather build up the `ItemTemplate` manually, you can add and configure the ObjectDataSource by dragging it from the Toolbox onto the Designer.</span></span> <span data-ttu-id="fa078-144">ただし、しないと、デザイナーから、フォーム ビューのデータ ソースを設定します。</span><span class="sxs-lookup"><span data-stu-id="fa078-144">However, don't set the FormView's data source from the Designer.</span></span> <span data-ttu-id="fa078-145">代わりに、ソース ビューに移動し、手動で設定する FormView の`DataSourceID`プロパティを`ID`ObjectDataSource の値。</span><span class="sxs-lookup"><span data-stu-id="fa078-145">Instead, go to the Source view and manually set the FormView's `DataSourceID` property to the `ID` value of the ObjectDataSource.</span></span> <span data-ttu-id="fa078-146">次に、手動で追加、`ItemTemplate`します。</span><span class="sxs-lookup"><span data-stu-id="fa078-146">Next, manually add the `ItemTemplate`.</span></span>

<span data-ttu-id="fa078-147">どのようなアプローチに関係なくは、するために、この時点で、フォーム ビューの宣言型マークアップを決定しました。</span><span class="sxs-lookup"><span data-stu-id="fa078-147">Regardless of what approach you decided to take, at this point your FormView's declarative markup should look like:</span></span>


[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample1.aspx)]

<span data-ttu-id="fa078-148">FormView のスマート タグでページングを有効にするチェック ボックスをオンする少しこれは追加、 `AllowPaging="True"` FormView の宣言型構文に属性します。</span><span class="sxs-lookup"><span data-stu-id="fa078-148">Take a moment to check the Enable Paging checkbox in the FormView's smart tag; this will add the `AllowPaging="True"` attribute to the FormView's declarative syntax.</span></span> <span data-ttu-id="fa078-149">また、設定、`EnableViewState`プロパティを False にします。</span><span class="sxs-lookup"><span data-stu-id="fa078-149">Also, set the `EnableViewState` property to False.</span></span>

## <a name="step-2-defining-theitemtemplates-markup"></a><span data-ttu-id="fa078-150">手順 2: 定義する、`ItemTemplate`のマークアップ</span><span class="sxs-lookup"><span data-stu-id="fa078-150">Step 2: Defining the`ItemTemplate`'s Markup</span></span>

<span data-ttu-id="fa078-151">ページングをサポートする FormView ObjectDataSource コントロールにバインドされ、構成されていると私たちのコンテンツを指定する準備ができている、`ItemTemplate`します。</span><span class="sxs-lookup"><span data-stu-id="fa078-151">With the FormView bound to the ObjectDataSource control and configured to support paging we're ready to specify the content for the `ItemTemplate`.</span></span> <span data-ttu-id="fa078-152">このチュートリアルに表示される製品の名前を持つみましょう、`<h3>`見出し。</span><span class="sxs-lookup"><span data-stu-id="fa078-152">For this tutorial, let's have the product's name displayed in an `<h3>` heading.</span></span> <span data-ttu-id="fa078-153">次に、HTML を使用してみましょう`<table>`最初と 3 番目の列には、プロパティ名が一覧表示され、2 番目と 4 番目の値の一覧の 4 つの列テーブルに製品の残りのプロパティを表示します。</span><span class="sxs-lookup"><span data-stu-id="fa078-153">Following that, let's use an HTML `<table>` to display the remaining product properties in a four-column table where the first and third columns list the property names and the second and fourth list their values.</span></span>

<span data-ttu-id="fa078-154">このマークアップは、デザイナーで FormView のテンプレートの編集インターフェイス経由で入力または宣言の構文を手動で入力できます。</span><span class="sxs-lookup"><span data-stu-id="fa078-154">This markup can be entered in through the FormView's template editing interface in the Designer or entered manually through the declarative syntax.</span></span> <span data-ttu-id="fa078-155">テンプレートを使用する場合は通常方が宣言の構文を直接操作しますが、自由に最も使い慣れている手法を使用する方が手軽です。</span><span class="sxs-lookup"><span data-stu-id="fa078-155">When working with templates I typically find it quicker to work directly with the declarative syntax, but feel free to use whatever technique you're most comfortable with.</span></span>

<span data-ttu-id="fa078-156">次のマークアップの後のフォーム ビューの宣言型マークアップを示しています、`ItemTemplate`の構造が完了します。</span><span class="sxs-lookup"><span data-stu-id="fa078-156">The following markup shows the FormView declarative markup after the `ItemTemplate`'s structure has been completed:</span></span>


[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample2.aspx)]

<span data-ttu-id="fa078-157">注意してデータ バインディング構文 -`<%# Eval("ProductName") %>`例は、テンプレートの出力に直接挿入することができます。</span><span class="sxs-lookup"><span data-stu-id="fa078-157">Notice that the databinding syntax - `<%# Eval("ProductName") %>`, for example can be injected directly into the template's output.</span></span> <span data-ttu-id="fa078-158">つまり、その必要がありますに割り当てられませんラベル コントロールの`Text`プロパティ。</span><span class="sxs-lookup"><span data-stu-id="fa078-158">That is, it need not be assigned to a Label control's `Text` property.</span></span> <span data-ttu-id="fa078-159">たとえば、ある、`ProductName`に表示される値、`<h3>`要素を使用して`<h3><%# Eval("ProductName") %></h3>`、製品の Chai としてレンダーする`<h3>Chai</h3>`します。</span><span class="sxs-lookup"><span data-stu-id="fa078-159">For example, we have the `ProductName` value displayed in an `<h3>` element using `<h3><%# Eval("ProductName") %></h3>`, which for the product Chai will render as `<h3>Chai</h3>`.</span></span>

<span data-ttu-id="fa078-160">`ProductPropertyLabel`と`ProductPropertyValue`製品プロパティの名前と値のスタイルを指定するための CSS クラス、`<table>`します。</span><span class="sxs-lookup"><span data-stu-id="fa078-160">The `ProductPropertyLabel` and `ProductPropertyValue` CSS classes are used for specifying the style of the product property names and values in the `<table>`.</span></span> <span data-ttu-id="fa078-161">これらの CSS クラスが定義されている`Styles.css`太字と右揃えであり、右のプロパティの値に余白を追加するプロパティの名前が発生するとします。</span><span class="sxs-lookup"><span data-stu-id="fa078-161">These CSS classes are defined in `Styles.css` and cause the property names to be bold and right-aligned and add a right padding to the property values.</span></span>

<span data-ttu-id="fa078-162">表示するには、フォーム ビューで使用可能な CheckBoxFields がないので、`Discontinued`値チェック ボックスとしては、独自のチェック ボックス コントロールを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fa078-162">Since there are no CheckBoxFields available with the FormView, in order to show the `Discontinued` value as a checkbox we must add our own CheckBox control.</span></span> <span data-ttu-id="fa078-163">`Enabled`プロパティが False で、読み取り専用になりますし、チェック ボックスの`Checked`プロパティの値にバインドする、`Discontinued`データ フィールド。</span><span class="sxs-lookup"><span data-stu-id="fa078-163">The `Enabled` property is set to False, making it read-only, and the CheckBox's `Checked` property is bound to the value of the `Discontinued` data field.</span></span>

<span data-ttu-id="fa078-164">`ItemTemplate`製品情報がより滑らかな方法で表示されます、完了します。</span><span class="sxs-lookup"><span data-stu-id="fa078-164">With the `ItemTemplate` complete, the product information is displayed in a much more fluid manner.</span></span> <span data-ttu-id="fa078-165">(図 4) このチュートリアルでは、FormView によって生成される出力の最後のチュートリアル (図 3) からの出力を DetailsView を比較します。</span><span class="sxs-lookup"><span data-stu-id="fa078-165">Compare the DetailsView output from the last tutorial (Figure 3) with the output generated by the FormView in this tutorial (Figure 4).</span></span>


<span data-ttu-id="fa078-166">[![剛体 DetailsView 出力](using-the-formview-s-templates-vb/_static/image8.png)](using-the-formview-s-templates-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="fa078-166">[![The Rigid DetailsView Output](using-the-formview-s-templates-vb/_static/image8.png)](using-the-formview-s-templates-vb/_static/image7.png)</span></span>

<span data-ttu-id="fa078-167">**図 3**:剛体 DetailsView 出力 ([フルサイズの画像を表示する をクリックします](using-the-formview-s-templates-vb/_static/image9.png))。</span><span class="sxs-lookup"><span data-stu-id="fa078-167">**Figure 3**: The Rigid DetailsView Output ([Click to view full-size image](using-the-formview-s-templates-vb/_static/image9.png))</span></span>


<span data-ttu-id="fa078-168">[![滑らかな FormView 出力](using-the-formview-s-templates-vb/_static/image11.png)](using-the-formview-s-templates-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="fa078-168">[![The Fluid FormView Output](using-the-formview-s-templates-vb/_static/image11.png)](using-the-formview-s-templates-vb/_static/image10.png)</span></span>

<span data-ttu-id="fa078-169">**図 4**:流体 FormView 出力 ([フルサイズの画像を表示する をクリックします](using-the-formview-s-templates-vb/_static/image12.png))。</span><span class="sxs-lookup"><span data-stu-id="fa078-169">**Figure 4**: The Fluid FormView Output ([Click to view full-size image](using-the-formview-s-templates-vb/_static/image12.png))</span></span>


## <a name="summary"></a><span data-ttu-id="fa078-170">まとめ</span><span class="sxs-lookup"><span data-stu-id="fa078-170">Summary</span></span>

<span data-ttu-id="fa078-171">GridView および DetailsView コントロールでは、カスタマイズ TemplateFields を使用して、出力を持つことができます、両方が、データ形式で表示する、グリッドのような角張ったします。</span><span class="sxs-lookup"><span data-stu-id="fa078-171">While the GridView and DetailsView controls can have their output customized using TemplateFields, both still present their data in a grid-like, boxy format.</span></span> <span data-ttu-id="fa078-172">1 つのレコードを表示する必要がある場合も低い剛体のレイアウトを使用して、FormView が最適な選択肢です。</span><span class="sxs-lookup"><span data-stu-id="fa078-172">For those times when a single record needs to be shown using a less rigid layout, the FormView is an ideal choice.</span></span> <span data-ttu-id="fa078-173">FormView、DetailsView などから 1 つのレコードを表示しますその`DataSource`DetailsView とは異なりが、テンプレートだけで構成されるありフィールドをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="fa078-173">Like the DetailsView, the FormView renders a single record from its `DataSource`, but unlike the DetailsView it is composed just of templates and does not support fields.</span></span>

<span data-ttu-id="fa078-174">このチュートリアルで説明したように、1 つのレコードを表示するときに、FormView はより柔軟なレイアウトにできます。</span><span class="sxs-lookup"><span data-stu-id="fa078-174">As we saw in this tutorial, the FormView allows for a more flexible layout when displaying a single record.</span></span> <span data-ttu-id="fa078-175">将来的に同じレベルとして、FormsView 柔軟性の提供しますが、(GridView) などの複数のレコードを表示することがその DataList と Repeater コントロールについて説明しますなるチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="fa078-175">In future tutorials we'll examine the DataList and Repeater controls, which provide the same level of flexibility as the FormsView, but are able to display multiple records (like the GridView).</span></span>

<span data-ttu-id="fa078-176">満足のプログラミングです。</span><span class="sxs-lookup"><span data-stu-id="fa078-176">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="fa078-177">執筆者紹介</span><span class="sxs-lookup"><span data-stu-id="fa078-177">About the Author</span></span>

<span data-ttu-id="fa078-178">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)、7 つ受け取りますブックおよびの創設者の著者[4GuysFromRolla.com](http://www.4guysfromrolla.com)、Microsoft Web テクノロジと 1998 年から携わっています。</span><span class="sxs-lookup"><span data-stu-id="fa078-178">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="fa078-179">Scott は、フリーのコンサルタント、トレーナー、およびライターとして動作します。</span><span class="sxs-lookup"><span data-stu-id="fa078-179">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="fa078-180">最新の著書は[ *Sams 教える自分で ASP.NET 2.0 24 時間以内に*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)します。</span><span class="sxs-lookup"><span data-stu-id="fa078-180">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="fa078-181">彼に到達できる[mitchell@4GuysFromRolla.comします。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="fa078-181">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="fa078-182">彼のブログにあるでまたは[ http://ScottOnWriting.NET](http://ScottOnWriting.NET)します。</span><span class="sxs-lookup"><span data-stu-id="fa078-182">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="fa078-183">特別なに感謝します。</span><span class="sxs-lookup"><span data-stu-id="fa078-183">Special Thanks To</span></span>

<span data-ttu-id="fa078-184">このチュートリアル シリーズは、多くの便利なレビュー担当者によってレビューされました。</span><span class="sxs-lookup"><span data-stu-id="fa078-184">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="fa078-185">このチュートリアルのレビュー担当者の潜在顧客が E.R.</span><span class="sxs-lookup"><span data-stu-id="fa078-185">Lead reviewer for this tutorial was E.R.</span></span> <span data-ttu-id="fa078-186">Gilmore します。</span><span class="sxs-lookup"><span data-stu-id="fa078-186">Gilmore.</span></span> <span data-ttu-id="fa078-187">今後、MSDN の記事を確認したいですか。</span><span class="sxs-lookup"><span data-stu-id="fa078-187">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="fa078-188">場合は、筆者に[mitchell@4GuysFromRolla.comします。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="fa078-188">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fa078-189">[前へ](using-templatefields-in-the-detailsview-control-vb.md)
> [次へ](displaying-summary-information-in-the-gridview-s-footer-vb.md)</span><span class="sxs-lookup"><span data-stu-id="fa078-189">[Previous](using-templatefields-in-the-detailsview-control-vb.md)
[Next](displaying-summary-information-in-the-gridview-s-footer-vb.md)</span></span>