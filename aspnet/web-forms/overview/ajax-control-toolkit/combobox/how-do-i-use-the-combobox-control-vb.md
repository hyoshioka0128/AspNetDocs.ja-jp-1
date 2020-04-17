---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
title: コンボ ボックス コントロールを使用する方法 (VB) |マイクロソフトドキュメント
author: rick-anderson
description: コンボ ボックスは、ユーザーが選択できるオプションのリストとテキスト ボックスの柔軟性を組み合わせたASP.NET AJAX コントロールです。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: e887e7b2-a6e7-4a28-a134-ba334494badb
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 237e3ef864238c11fc1fb49239c3f6fa3f75537d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543068"
---
# <a name="how-do-i-use-the-combobox-control-vb"></a><span data-ttu-id="2c89a-104">コンボ ボックス コントロールを使用する方法</span><span class="sxs-lookup"><span data-stu-id="2c89a-104">How do I use the ComboBox Control?</span></span> <span data-ttu-id="2c89a-105">(VB)</span><span class="sxs-lookup"><span data-stu-id="2c89a-105">(VB)</span></span>

<span data-ttu-id="2c89a-106">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2c89a-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="2c89a-107">コンボ ボックスは、ユーザーが選択できるオプションのリストとテキスト ボックスの柔軟性を組み合わせたASP.NET AJAX コントロールです。</span><span class="sxs-lookup"><span data-stu-id="2c89a-107">ComboBox is an ASP.NET AJAX control that combines the flexibility of a TextBox with a list of options from which users can choose.</span></span>

<span data-ttu-id="2c89a-108">このチュートリアルの目的は、AJAX コントロール ツールキットコンボ ボックス コントロールについて説明することです。</span><span class="sxs-lookup"><span data-stu-id="2c89a-108">The goal of this tutorial is to explain the AJAX Control Toolkit ComboBox control.</span></span> <span data-ttu-id="2c89a-109">コンボ ボックスは、標準のASP.NETドロップダウン リスト コントロールとテキスト ボックス コントロールの組み合わせのように機能します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-109">The ComboBox works like a combination between a standard ASP.NET DropDownList control and a TextBox control.</span></span> <span data-ttu-id="2c89a-110">既存の項目リストから選択するか、新しい項目を入力することができます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-110">You can either select from a pre-existing list of items or enter a new item.</span></span>

<span data-ttu-id="2c89a-111">ComboBox はオートコンプリート コントロール エクステンダに似ていますが、コントロールはさまざまなシナリオで使用されます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-111">The ComboBox is similar to the AutoComplete control extender, but the controls are used in different scenarios.</span></span> <span data-ttu-id="2c89a-112">オートコンプリート エクステンダは、Web サービスに対して一致するエントリを取得するクエリを実行します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-112">The AutoComplete extender queries a web service to get matching entries.</span></span> <span data-ttu-id="2c89a-113">これに対し、ComboBox コントロールは項目のセットで初期化されます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-113">The ComboBox control, in contrast, is initialized with a set of items.</span></span> <span data-ttu-id="2c89a-114">オートコンプリート エクステンダを使用すると、コンボ ボックス コントロールを使用しながら、大量のデータ セット (数百万台の自動車部品) を操作する場合に意味があります。</span><span class="sxs-lookup"><span data-stu-id="2c89a-114">Using the AutoComplete extender makes sense when you are working with a large set of data (millions of car parts) while using the ComboBox control makes sense when working with a small set of data (dozens of car parts).</span></span>

## <a name="selecting-from-a-static-list-of-items"></a><span data-ttu-id="2c89a-115">アイテムの静的リストからの選択</span><span class="sxs-lookup"><span data-stu-id="2c89a-115">Selecting from a Static List of Items</span></span>

<span data-ttu-id="2c89a-116">コンボ ボックス コントロールの使用の簡単なサンプルから始めましょう。</span><span class="sxs-lookup"><span data-stu-id="2c89a-116">Let�s start with a simple sample of using the ComboBox control.</span></span> <span data-ttu-id="2c89a-117">ドロップダウン リストに項目の静的な一覧を表示するとします。</span><span class="sxs-lookup"><span data-stu-id="2c89a-117">Imagine that you want to display a static list of items in a dropdown list.</span></span> <span data-ttu-id="2c89a-118">ただし、リストが完全でない可能性を開いたままにしておきたい場合は、次の手順に示します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-118">However, you want to leave open the possibility that the list is not complete.</span></span> <span data-ttu-id="2c89a-119">ユーザーがリストにカスタム値を入力できるようにする場合。</span><span class="sxs-lookup"><span data-stu-id="2c89a-119">You want to allow a user to enter a custom value into the list.</span></span>

<span data-ttu-id="2c89a-120">新しい web フォーム ページASP.NET作成し、ページでコンボ ボックス コントロールを使用します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-120">We�ll create a new ASP.NET Web Forms page and use the ComboBox control in the page.</span></span> <span data-ttu-id="2c89a-121">新しいASP.NET ページをプロジェクトに追加し、デザイン ビューに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-121">Add the new ASP.NET page to your project and switch to Design view.</span></span>

<span data-ttu-id="2c89a-122">ページで ComboBox コントロールを使用する場合は、ページに ScriptManager コントロールを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c89a-122">If you want to use the ComboBox control in the page then you must add a ScriptManager control to the page.</span></span> <span data-ttu-id="2c89a-123">ScriptManager コントロールを [AJAX 拡張機能] タブの下からデザイナー画面にドラッグします。</span><span class="sxs-lookup"><span data-stu-id="2c89a-123">Drag the ScriptManager control from beneath the AJAX Extensions tab onto the Designer surface.</span></span> <span data-ttu-id="2c89a-124">ページの上部に ScriptManager コントロールを追加する必要があります。開いているサーバー側&lt;フォーム&gt;タグのすぐ下に追加できます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-124">You should add the ScriptManager control at the top of the page; you can add it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="2c89a-125">次に、コンボ ボックス コントロールをページにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="2c89a-125">Next, drag the ComboBox control onto the page.</span></span> <span data-ttu-id="2c89a-126">他の AJAX コントロール ツールキット コントロールとコントロール エクステンダ (図 1 を参照) と共に、ツールボックスで ComboBox コントロールを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-126">You can find the ComboBox control in the Toolbox with the other AJAX Control Toolkit controls and control extenders (see figure1).</span></span>

<span data-ttu-id="2c89a-127">[![名刺を作成するための簡単なフォーム](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2c89a-127">[![Simple form for creating a business card](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="2c89a-128">**図 01**: ツールボックスから ComboBox コントロールを選択する ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-vb/_static/image2.png)します)</span><span class="sxs-lookup"><span data-stu-id="2c89a-128">**Figure 01**: Selecting the ComboBox control from the toolbox ([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image2.png))</span></span>

<span data-ttu-id="2c89a-129">コンボ ボックス コントロールを使用して、選択肢の静的な一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-129">We�ll use the ComboBox control to display a static list of choices.</span></span> <span data-ttu-id="2c89a-130">ユーザーは、マイルド、ミディアム、ホットの 3 つの選択肢から、食品の特定のレベルのスパイシーを選択できます (図 2 参照)。</span><span class="sxs-lookup"><span data-stu-id="2c89a-130">The user can select a particular level of spiciness for their food from a list of three choices: Mild, Medium, and Hot (see Figure 2).</span></span>

<span data-ttu-id="2c89a-131">[![項目の静的リストからの選択](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2c89a-131">[![Selecting from a static list of items](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)</span></span>

<span data-ttu-id="2c89a-132">**図 02**: 項目の静的な一覧から選択する ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-vb/_static/image4.png)して)</span><span class="sxs-lookup"><span data-stu-id="2c89a-132">**Figure 02**: Selecting from a static list of items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image4.png))</span></span>

<span data-ttu-id="2c89a-133">これらの選択肢を ComboBox コントロールに追加するには、2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="2c89a-133">There are two ways that you can add these choices to the ComboBox control.</span></span> <span data-ttu-id="2c89a-134">まず、デザイン ビューでコントロールの上にマウス を置くときに[オプションの編集]タスク オプションを選択し、アイテム エディタを開きます (図 3 参照)。</span><span class="sxs-lookup"><span data-stu-id="2c89a-134">First, you select the Edit Options task option when hovering your mouse over the control in Design view and open the Item Editor (see Figure 3).</span></span>

<span data-ttu-id="2c89a-135">[![コンボ ボックス項目の編集](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="2c89a-135">[![Editing ComboBox items](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)</span></span>

<span data-ttu-id="2c89a-136">**図 03**: コンボ ボックス項目の編集 ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="2c89a-136">**Figure 03**: Editing ComboBox items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image6.png))</span></span>

<span data-ttu-id="2c89a-137">2 番目のオプションは、ソース ビューで、開始と終了&lt;の間の項目の&gt;リストを追加します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-137">The second option is to add the list of items in between the opening and closing &lt;asp:ComboBox&gt; tags in Source view.</span></span> <span data-ttu-id="2c89a-138">リスト 1 のページには、項目の一覧を含む更新された ComboBox が含まれています。</span><span class="sxs-lookup"><span data-stu-id="2c89a-138">The page in Listing 1 contains the updated ComboBox that has the list of items.</span></span>

<span data-ttu-id="2c89a-139">**リスト 1 - 静的.aspx**</span><span class="sxs-lookup"><span data-stu-id="2c89a-139">**Listing 1 - Static.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample1.aspx)]

<span data-ttu-id="2c89a-140">リスト 1 でページを開くと、コンボ ボックスから既存のオプションのいずれかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-140">When you open the page in Listing 1, you can select one of the pre-existing options from the ComboBox.</span></span> <span data-ttu-id="2c89a-141">つまり、コンボ ボックスは、ドロップダウン リスト コントロールと同じように機能します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-141">In other words, the ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="2c89a-142">ただし、既存のリストにない新しい選択肢 (スーパースパイシーなど) を入力することもできます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-142">However, you also have the option of entering a new choice (for example, Super Spicy) that is not in the existing list.</span></span> <span data-ttu-id="2c89a-143">したがって、コンボ ボックスもテキスト ボックス コントロールのように動作します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-143">So, the ComboBox also works like a TextBox control.</span></span>

<span data-ttu-id="2c89a-144">既存のアイテムを選択するか、カスタム アイテムを入力するかにかかわらず、フォームを送信すると、選択した項目がラベル コントロールに表示されます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-144">Regardless of whether you pick a pre-existing item or you enter a custom item, when you submit the form, your choice appears in the label control.</span></span> <span data-ttu-id="2c89a-145">フォームを送信すると、btnSubmit\_Click ハンドラが実行され、ラベルが更新されます (図 4 参照)。</span><span class="sxs-lookup"><span data-stu-id="2c89a-145">When you submit the form, the btnSubmit\_Click handler executes and updates the label (see Figure 4).</span></span>

<span data-ttu-id="2c89a-146">[![選択した項目の表示](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="2c89a-146">[![Displaying the selected item](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)</span></span>

<span data-ttu-id="2c89a-147">**図04**: 選択した項目を表示する ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="2c89a-147">**Figure 04**: Displaying the selected item([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image8.png))</span></span>

<span data-ttu-id="2c89a-148">コンボ ボックス (ComboBox) コントロールは、フォームの送信後に選択した項目を取得するための DropDownList コントロールと同じプロパティをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="2c89a-148">The ComboBox supports the same properties as the DropDownList control for retrieving the selected item after a form is submitted:</span></span>

- <span data-ttu-id="2c89a-149">選択項目.テキスト - 選択した項目の Text プロパティの値を表示します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-149">SelectedItem.Text - Displays the value of the Text property of the selected item.</span></span>
- <span data-ttu-id="2c89a-150">SelectedItem.Value - 選択した項目の Value プロパティの値を表示するか、コンボ ボックスに入力されたテキストを表示します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-150">SelectedItem.Value - Displays the value of the Value property of the selected item or displays the text typed into the ComboBox.</span></span>
- <span data-ttu-id="2c89a-151">選択値 - このプロパティを使用して、既定の (初期) 選択された項目を指定できる点を除いて、SelectedItem.Value と同じです。</span><span class="sxs-lookup"><span data-stu-id="2c89a-151">SelectedValue - Same as SelectedItem.Value except that this property enables you to specify the default (initial) selected item.</span></span>

<span data-ttu-id="2c89a-152">コンボ ボックスにカスタム選択を入力すると、カスタムの選択肢が SelectedItem.Text プロパティと SelectedItem.Value プロパティの両方に割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-152">If you type a custom choice into the ComboBox then the custom choice is assigned to both the SelectedItem.Text and SelectedItem.Value properties.</span></span>

## <a name="selecting-the-list-of-items-from-the-database"></a><span data-ttu-id="2c89a-153">データベースから項目のリストを選択する</span><span class="sxs-lookup"><span data-stu-id="2c89a-153">Selecting the List of Items from the Database</span></span>

<span data-ttu-id="2c89a-154">コンボ ボックス (ComboBox) コントロールに表示される項目の一覧をデータベースから取得できます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-154">You can retrieve the list of items that the ComboBox displays from a database.</span></span> <span data-ttu-id="2c89a-155">たとえば、コンボ ボックスを SqlDataSource コントロール、オブジェクトデータ ソース コントロール、LinqDataSource、またはエンティティデータ ソースにバインドできます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-155">For example, you can bind the ComboBox to a SqlDataSource control, an ObjectDataSource control, a LinqDataSource, or an EntityDataSource.</span></span>

<span data-ttu-id="2c89a-156">コンボ ボックス (ComboBox) コントロールに映画の一覧を表示するとします。</span><span class="sxs-lookup"><span data-stu-id="2c89a-156">Imagine that you want to display a list of movies in a ComboBox.</span></span> <span data-ttu-id="2c89a-157">映画の一覧を Movies データベース テーブルから取得する場合。</span><span class="sxs-lookup"><span data-stu-id="2c89a-157">You want to retrieve the list of movies from the Movies database table.</span></span> <span data-ttu-id="2c89a-158">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="2c89a-158">Follow these steps:</span></span>

1. <span data-ttu-id="2c89a-159">という名前のページを作成します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-159">Create a page named Movies.aspx</span></span>
2. <span data-ttu-id="2c89a-160">ツールボックスの [AJAX 拡張機能] タブの下にあるページに ScriptManager をドラッグして、ScriptManager コントロールをページに追加します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-160">Add a ScriptManager control to the page by dragging the ScriptManager from under the AJAX Extensions tab in the Toolbox onto the page.</span></span>
3. <span data-ttu-id="2c89a-161">ページにコンボ ボックス (ComboBox) コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-161">Add a ComboBox control to the page by dragging the ComboBox onto the page.</span></span>
4. <span data-ttu-id="2c89a-162">デザイン ビューで、コンボ ボックス コントロールの上にマウス を移動し、[**データ ソースの選択]** タスク オプションを選択します (図 5 参照)。</span><span class="sxs-lookup"><span data-stu-id="2c89a-162">In Design view, hover your mouse over the ComboBox control and select the **Choose Data Source** task option (see Figure 5).</span></span> <span data-ttu-id="2c89a-163">データ ソース構成ウィザードが起動します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-163">The Data Source Configuration Wizard is launched.</span></span>
5. <span data-ttu-id="2c89a-164">[**データ ソースの選択]** の手順&lt;で、[新&gt;しいデータ ソース] オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-164">In the **Choose a Data Source** step, select the &lt;New data source�&gt; option.</span></span>
6. <span data-ttu-id="2c89a-165">[**データ ソースの種類の選択]** ステップで、[データベース] を選択します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-165">In the **Choose a Data Source Type** step, select Database.</span></span>
7. <span data-ttu-id="2c89a-166">[**データ接続の選択]** ステップで、データベース (例: MoviesDB.mdf) を選択します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-166">In the **Choose Your Data Connection** step, select your database (for example, MoviesDB.mdf).</span></span>
8. <span data-ttu-id="2c89a-167">[**接続文字列をアプリケーション構成ファイルに保存する**] ステップで、接続文字列を保存するオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-167">In the **Save the Connection String to the Application Configuration File** step, select the option to save your connection string.</span></span>
9. <span data-ttu-id="2c89a-168">「**ステートメントの選択」ステップで**、Movies データベース表を選択し、すべての列を選択します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-168">In the **Configure the Select Statement** step, select the Movies database table and select all of the columns.</span></span>
10. <span data-ttu-id="2c89a-169">**[クエリのテスト**] ステップで、[完了] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="2c89a-169">In the **Test Query** step, click the Finish button.</span></span>
11. <span data-ttu-id="2c89a-170">データ**ソースの選択**手順に戻り、表示するフィールドの [タイトル] 列とデータ フィールドの [Id] 列を選択します (図を参照)。</span><span class="sxs-lookup"><span data-stu-id="2c89a-170">Back in the **Choose Data Source** step, select the Title column for the field to display and the Id column for the data field (see Figure).</span></span>
12. <span data-ttu-id="2c89a-171">[OK] をクリックしてウィザードを閉じます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-171">Click the OK button to close the wizard.</span></span>

<span data-ttu-id="2c89a-172">[![データ ソースの選択](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="2c89a-172">[![Choosing a data source](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)</span></span>

<span data-ttu-id="2c89a-173">**図 05**: データ ソースの選択 ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="2c89a-173">**Figure 05**: Choosing a data source([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image10.png))</span></span>

<span data-ttu-id="2c89a-174">[![データテキストと値フィールドの選択](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="2c89a-174">[![Choosing the data text and value fields](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)</span></span>

<span data-ttu-id="2c89a-175">**図 06**: データ テキストと値のフィールドを選択する ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-vb/_static/image12.png)して )</span><span class="sxs-lookup"><span data-stu-id="2c89a-175">**Figure 06**: Choosing the data text and value fields([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image12.png))</span></span>

<span data-ttu-id="2c89a-176">上記の手順を完了すると、コンボ ボックスは、ムービー データベース テーブルから映画を表す SqlDataSource コントロールにバインドされます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-176">After you complete the steps above, the ComboBox is bound to a SqlDataSource control that represents the movies from the Movies database table.</span></span> <span data-ttu-id="2c89a-177">ページのソースはリスト 2 のようになります (書式設定を少しクリーンアップしました)。</span><span class="sxs-lookup"><span data-stu-id="2c89a-177">The source for the page looks like Listing 2 (I cleaned up the formatting a little bit).</span></span>

<span data-ttu-id="2c89a-178">**リスト 2 - 映画.aspx**</span><span class="sxs-lookup"><span data-stu-id="2c89a-178">**Listing 2 - Movies.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample2.aspx)]

<span data-ttu-id="2c89a-179">コントロールには、コントロールを指すデータ ソース ID プロパティがあることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="2c89a-179">Notice that the ComboBox control has a DataSourceID property that points to the SqlDataSource control.</span></span> <span data-ttu-id="2c89a-180">ブラウザーでページを開くと、データベースからムービーの一覧が表示されます (図 7 参照)。</span><span class="sxs-lookup"><span data-stu-id="2c89a-180">When you open the page in a browser, the list of movies from the database is displayed (see Figure 7).</span></span> <span data-ttu-id="2c89a-181">リストからムービーを選択するか、または ComboBox にムービーを入力して新しいムービーを入力できます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-181">You can either a pick a movie from the list or enter a new movie by typing the movie into the ComboBox.</span></span>

<span data-ttu-id="2c89a-182">[![映画の一覧を表示する](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="2c89a-182">[![Displaying a list of movies](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)</span></span>

<span data-ttu-id="2c89a-183">**図 07**: 動画の一覧を表示する ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="2c89a-183">**Figure 07**: Displaying a list of movies([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image14.png))</span></span>

## <a name="setting-the-dropdownstyle"></a><span data-ttu-id="2c89a-184">ドロップダウンスタイルの設定</span><span class="sxs-lookup"><span data-stu-id="2c89a-184">Setting the DropDownStyle</span></span>

<span data-ttu-id="2c89a-185">コンボ ボックス の動作を変更するには、コンボ ボックスのドロップダウンスタイルプロパティを使用できます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-185">You can use the ComboBox DropDownStyle property to change the behavior of the ComboBox.</span></span> <span data-ttu-id="2c89a-186">このプロパティは、次の値を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="2c89a-186">This property accepts there possible values:</span></span>

- <span data-ttu-id="2c89a-187">ドロップダウン - (既定値) コンボ ボックス (ComboBox) 矢印をクリックすると、ドロップダウン リストが表示され、カスタム値を入力できます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-187">DropDown - (default value) The ComboBox displays a dropdown list when you click the arrow and you can enter a custom value.</span></span>
- <span data-ttu-id="2c89a-188">シンプル - コンボボックスは、自動的にドロップダウンリストを表示し、カスタム値を入力することができます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-188">Simple - The ComboBox displays a dropdown list automatically and you can enter a custom value.</span></span>
- <span data-ttu-id="2c89a-189">ドロップダウン リスト - コンボ ボックスは、ドロップダウン リスト コントロールと同じように機能します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-189">DropDownList - The ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="2c89a-190">ドロップダウンとシンプルの違いは、項目のリストが表示される場合です。</span><span class="sxs-lookup"><span data-stu-id="2c89a-190">The different between DropDown and Simple is when the list of items is displayed.</span></span> <span data-ttu-id="2c89a-191">Simple の場合、コンボ ボックスにフォーカスを移動すると、すぐにリストが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-191">In the case of Simple, the list is displayed immediately when you move focus to the ComboBox.</span></span> <span data-ttu-id="2c89a-192">ドロップダウンの場合は、矢印をクリックして項目の一覧を表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c89a-192">In the case of DropDown, you must click the arrow to see the list of items.</span></span>

<span data-ttu-id="2c89a-193">ドロップダウン リストの値を使用すると、コンボ ボックス コントロールは標準のドロップダウン リスト コントロールと同じように動作します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-193">The DropDownList value causes the ComboBox control to work just like a standard DropDownList control.</span></span> <span data-ttu-id="2c89a-194">しかし、ここで重要な違いがあります。</span><span class="sxs-lookup"><span data-stu-id="2c89a-194">However, there is an important difference here.</span></span> <span data-ttu-id="2c89a-195">古いバージョンの Internet Explorer では、無限の z インデックスを持つ DropDownList コントロールが表示されるため、コントロールはその前に配置されたコントロールの前に表示されます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-195">Older versions of Internet Explorer display a DropDownList control with an infinite z-index so the control will appear in front of any control placed in front of it.</span></span> <span data-ttu-id="2c89a-196">コンボ ボックス&lt;は HTML&gt;&lt;選択&gt;タグの代わりに HTML div タグを表示するため、コンボ ボックスは z の順序を正しく考慮します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-196">Because the ComboBox renders an HTML &lt;div&gt; tag instead of an HTML &lt;select&gt; tag, the ComboBox correctly respects z-ordering.</span></span>

## <a name="setting-the-autocompletemode"></a><span data-ttu-id="2c89a-197">オートコンプリートモードの設定</span><span class="sxs-lookup"><span data-stu-id="2c89a-197">Setting the AutoCompleteMode</span></span>

<span data-ttu-id="2c89a-198">コンボ ボックスのオートコンプリート モード プロパティを使用して、コンボ ボックスにテキストを入力したときに発生する動作を指定します。</span><span class="sxs-lookup"><span data-stu-id="2c89a-198">You use the ComboBox AutoCompleteMode property to specify what happens when someone types text into the ComboBox.</span></span> <span data-ttu-id="2c89a-199">このプロパティは、次の値を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="2c89a-199">This property accepts the following possible values:</span></span>

- <span data-ttu-id="2c89a-200">なし - (既定値) コンボ ボックス (ComboBox) はオートコンプリート動作を提供しません。</span><span class="sxs-lookup"><span data-stu-id="2c89a-200">None - (default value) The ComboBox does not provide any auto-complete behavior.</span></span>
- <span data-ttu-id="2c89a-201">提案 - コンボ ボックス (ComboBox) コントロールは一覧を表示し、一致する項目をリストに強調表示します (図 8 参照)。</span><span class="sxs-lookup"><span data-stu-id="2c89a-201">Suggest - The ComboBox displays the list and it highlights the matching item in the list (see Figure 8).</span></span>
- <span data-ttu-id="2c89a-202">追加 - ComboBox はリストを表示せず、入力した項目に一致する項目をリストから追加します (図 9 参照)。</span><span class="sxs-lookup"><span data-stu-id="2c89a-202">Append - The ComboBox does not display the list and it appends the matching item from the list onto what you have typed (see Figure 9).</span></span>
- <span data-ttu-id="2c89a-203">SuggestAppend - コンボ ボックス (ComboBox) コントロールは、リストを表示し、入力した項目に一致する項目をリストから追加します (図 10 参照)。</span><span class="sxs-lookup"><span data-stu-id="2c89a-203">SuggestAppend - The ComboBox both displays the list and appends the matching item from the list onto what you have typed (see Figure 10).</span></span>

<span data-ttu-id="2c89a-204">[![コンボボックスが提案を行います](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="2c89a-204">[![The ComboBox makes a suggestion](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)</span></span>

<span data-ttu-id="2c89a-205">**図08**: コンボボックスが提案を行う([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="2c89a-205">**Figure 08**: The ComboBox makes a suggestion([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image16.png))</span></span>

<span data-ttu-id="2c89a-206">[![一致するテキストを追加するコンボ ボックス](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="2c89a-206">[![ComboBox appends matching text](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)</span></span>

<span data-ttu-id="2c89a-207">**図 09**: ComboBox が一致するテキストを追加します ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-vb/_static/image18.png)します)</span><span class="sxs-lookup"><span data-stu-id="2c89a-207">**Figure 09**: ComboBox appends matching text([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image18.png))</span></span>

<span data-ttu-id="2c89a-208">[![コンボ ボックス (コンボ ボックス) の提案と追加](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="2c89a-208">[![The ComboBox suggests and appends](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)</span></span>

<span data-ttu-id="2c89a-209">**図10**: コンボボックスの提案と追加([フルサイズの画像を表示するをクリック](how-do-i-use-the-combobox-control-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="2c89a-209">**Figure 10**: The ComboBox suggests and appends([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image20.png))</span></span>

## <a name="summary"></a><span data-ttu-id="2c89a-210">まとめ</span><span class="sxs-lookup"><span data-stu-id="2c89a-210">Summary</span></span>

<span data-ttu-id="2c89a-211">このチュートリアルでは、ComboBox コントロールを使用して、固定された項目のセットを表示する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="2c89a-211">In this tutorial, you learned how to use the ComboBox control to display a fixed set of items.</span></span> <span data-ttu-id="2c89a-212">ComboBox コントロールを静的な項目セットとデータベース テーブルの両方にバインドしました。</span><span class="sxs-lookup"><span data-stu-id="2c89a-212">We bound the ComboBox control both to a static set of items and to a database table.</span></span> <span data-ttu-id="2c89a-213">最後に、コンボ ボックスの動作を変更する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="2c89a-213">Finally, you learned how to modify the behavior of the ComboBox by setting its DropDownStyle and AutoCompleteMode properties.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2c89a-214">前へ</span><span class="sxs-lookup"><span data-stu-id="2c89a-214">Previous</span></span>](how-do-i-use-the-combobox-control-cs.md)
