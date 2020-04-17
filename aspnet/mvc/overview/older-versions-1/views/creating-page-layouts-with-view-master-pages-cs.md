---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: ビュー マスター ページを使用したページ レイアウトの作成 (C#) |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルでは、ビュー マスター ページを利用して、アプリケーション内の複数のページの共通ページ レイアウトを作成する方法を学習します。 あなたは..を使用することができます。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: d313e017d7061ae03e8dea79e611d0cf3838297d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542522"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a><span data-ttu-id="3f7ef-104">ビュー マスター ページでページ レイアウトを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="3f7ef-104">Creating Page Layouts with View Master Pages (C#)</span></span>

<span data-ttu-id="3f7ef-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3f7ef-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="3f7ef-106">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="3f7ef-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> <span data-ttu-id="3f7ef-107">このチュートリアルでは、ビュー マスター ページを利用して、アプリケーション内の複数のページの共通ページ レイアウトを作成する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="3f7ef-108">ビュー マスター ページを使用して、2 列のページ レイアウトを定義し、Web アプリケーションのすべてのページに 2 列のレイアウトを使用できます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="3f7ef-109">ビュー マスター ページを使用したページ レイアウトの作成</span><span class="sxs-lookup"><span data-stu-id="3f7ef-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="3f7ef-110">このチュートリアルでは、ビュー マスター ページを利用して、アプリケーション内の複数のページの共通ページ レイアウトを作成する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="3f7ef-111">ビュー マスター ページを使用して、2 列のページ レイアウトを定義し、Web アプリケーションのすべてのページに 2 列のレイアウトを使用できます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="3f7ef-112">また、ビュー マスター ページを利用して、アプリケーション内の複数のページで共通のコンテンツを共有することもできます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="3f7ef-113">たとえば、Web サイトのロゴ、ナビゲーション リンク、バナー広告をビュー マスター ページに配置できます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="3f7ef-114">これにより、アプリケーションのすべてのページでこのコンテンツが自動的に表示されます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="3f7ef-115">このチュートリアルでは、新しいビュー マスター ページを作成し、マスター ページに基づいて新しいビュー コンテンツ ページを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="3f7ef-116">ビュー マスター ページの作成</span><span class="sxs-lookup"><span data-stu-id="3f7ef-116">Creating a View Master Page</span></span>

<span data-ttu-id="3f7ef-117">2 列のレイアウトを定義するビュー マスター ページを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="3f7ef-118">MVC プロジェクトに新しいビュー マスター ページを追加するには、ビュー\共有フォルダーを右クリックし、メニュー オプション**の追加、新しい項目**を選択し **、MVC ビュー マスター ページ**テンプレート (図 1 参照) を選択します。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the **MVC View Master Page** template (see Figure 1).</span></span>

<span data-ttu-id="3f7ef-119">[![ビュー マスター ページの追加](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3f7ef-119">[![Adding a view master page](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span></span>

<span data-ttu-id="3f7ef-120">**図 01**: ビュー マスター ページの追加 ([フルサイズの画像を表示する をクリック](creating-page-layouts-with-view-master-pages-cs/_static/image3.png)します )</span><span class="sxs-lookup"><span data-stu-id="3f7ef-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span></span>

<span data-ttu-id="3f7ef-121">アプリケーションでは、複数のビュー マスター ページを作成できます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="3f7ef-122">各ビューマスターページは、異なるページレイアウトを定義できます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="3f7ef-123">たとえば、特定のページに 2 列のレイアウトを設定し、その他のページに 3 列のレイアウトを設定する場合があります。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="3f7ef-124">ビュー マスター ページは、MVC ビューの標準ASP.NET外観が非常に大きく似ています。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="3f7ef-125">ただし、標準ビューとは異なり、ビュー マスター ページには`<asp:ContentPlaceHolder>`1 つ以上のタグが含まれます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="3f7ef-126">タグ`<contentplaceholder>`は、個々のコンテンツ ページで上書きできるマスター ページの領域をマークするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="3f7ef-127">たとえば、リスト 1 のビュー マスター ページは、2 列のレイアウトを定義します。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="3f7ef-128">これには 2`<contentplaceholder>`つのタグが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="3f7ef-129">各`<ContentPlaceHolder>`列に 1 つずつ。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-129">One `<ContentPlaceHolder>` for each column.</span></span>

<span data-ttu-id="3f7ef-130">**リスト1 –`Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="3f7ef-130">**Listing 1 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

<span data-ttu-id="3f7ef-131">リスト 1 のビュー マスター ページの本文`<div>`には、2 つの列に対応する 2 つのタグが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="3f7ef-132">カスケード スタイル シート列クラスは、両方`<div>`のタグに適用されます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="3f7ef-133">このクラスは、マスター ページの先頭で宣言されているスタイル シートで定義されます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="3f7ef-134">デザイン ビューに切り替えると、ビュー マスター ページのレンダリング方法をプレビューできます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="3f7ef-135">ソース コード エディターの左下にある [デザイン] タブをクリックします (図 2 参照)。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>

<span data-ttu-id="3f7ef-136">[![デザイナーでのマスター ページのプレビュー](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="3f7ef-136">[![Previewing a master page in the designer](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span></span>

<span data-ttu-id="3f7ef-137">**図 02**: デザイナーでマスター ページをプレビューする ([フルサイズのイメージを表示する をクリック](creating-page-layouts-with-view-master-pages-cs/_static/image6.png)して )</span><span class="sxs-lookup"><span data-stu-id="3f7ef-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span></span>

### <a name="creating-a-view-content-page"></a><span data-ttu-id="3f7ef-138">ビュー コンテンツ ページの作成</span><span class="sxs-lookup"><span data-stu-id="3f7ef-138">Creating a View Content Page</span></span>

<span data-ttu-id="3f7ef-139">ビュー マスター ページを作成した後、ビュー マスター ページに基づいて 1 つ以上のビュー コンテンツ ページを作成できます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="3f7ef-140">たとえば、ホーム コントローラーのインデックス ビュー コンテンツ ページを作成するには、ビュー\ホーム フォルダを右クリックし **、[追加]、[新しい項目**] の順に選択し **、MVC ビュー コンテンツ ページ**テンプレートを選択して Index.aspx という名前を入力し、[**追加**] ボタンをクリックします (図 3 参照)。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the **Add** button (see Figure 3).</span></span>

<span data-ttu-id="3f7ef-141">[![ビュー コンテンツ ページの追加](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="3f7ef-141">[![Adding a view content page](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span></span>

<span data-ttu-id="3f7ef-142">**図 03**: ビュー コンテンツ ページを追加する ([フルサイズの画像を表示するには [ ] をクリック](creating-page-layouts-with-view-master-pages-cs/_static/image9.png)します )</span><span class="sxs-lookup"><span data-stu-id="3f7ef-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span></span>

<span data-ttu-id="3f7ef-143">[追加] ボタンをクリックすると、新しいダイアログが表示され、ビュー のマスター ページを選択してビュー コンテンツ ページに関連付けることができます (図 4 参照)。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="3f7ef-144">前のセクションで作成した Site.master ビュー マスター ページに移動できます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>

<span data-ttu-id="3f7ef-145">[![マスター ページの選択](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="3f7ef-145">[![Selecting a master page](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span></span>

<span data-ttu-id="3f7ef-146">**図 04**: マスタ ページの選択 ([フルサイズの画像を表示する をクリック](creating-page-layouts-with-view-master-pages-cs/_static/image12.png)します )</span><span class="sxs-lookup"><span data-stu-id="3f7ef-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span></span>

<span data-ttu-id="3f7ef-147">Site.master マスター ページに基づいて新しいビュー コンテンツ ページを作成すると、リスト 2 でファイルが取得されます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

<span data-ttu-id="3f7ef-148">**リスト2 –`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="3f7ef-148">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="3f7ef-149">このビューには、`<asp:Content>`ビュー マスター ページの各`<asp:ContentPlaceHolder>`タグに対応するタグが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="3f7ef-150">各`<asp:Content>`タグには、オーバーライドする特定`<asp:ContentPlaceHolder>`のタグを指す ContentPlaceHolderID 属性が含まれています。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="3f7ef-151">さらに、リスト 2 のコンテンツ ビュー ページには、通常の開始 HTML タグと終了 HTML タグが含まれていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="3f7ef-152">たとえば、開始タグと終了`<html>``<head>`タグは含まれません。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="3f7ef-153">通常の開始タグと終了タグはすべて、ビュー マスター ページに含まれます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="3f7ef-154">ビューコンテンツページに表示するコンテンツは、タグ内に`<asp:Content>`配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="3f7ef-155">これらのタグの外部に HTML やその他のコンテンツを配置すると、ページを表示しようとするとエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="3f7ef-156">コンテンツ ビュー ページのマスター`<asp:ContentPlaceHolder>`ページのすべてのタグを上書きする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="3f7ef-157">タグを特定のコンテンツで`<asp:ContentPlaceHolder>`置き換える場合にのみ、タグをオーバーライドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="3f7ef-158">たとえば、リスト 3 で変更したインデックス ビューには`<asp:Content>`、2 つのタグしか含めなされません。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="3f7ef-159">各タグには`<asp:Content>`、いくつかのテキストが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-159">Each of the `<asp:Content>` tags includes some text.</span></span>

<span data-ttu-id="3f7ef-160">**リスト3 –`Views\Home\Index.aspx (modified)`**</span><span class="sxs-lookup"><span data-stu-id="3f7ef-160">**Listing 3 – `Views\Home\Index.aspx (modified)`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="3f7ef-161">リスト 3 のビューが要求されると、図 5 のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="3f7ef-162">ビューは、2 つの列を持つページをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="3f7ef-163">さらに、ビュー コンテンツ ページのコンテンツがビュー マスター ページのコンテンツとマージされることにも注意してください。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page</span></span>

<span data-ttu-id="3f7ef-164">[![インデックス ビューのコンテンツ ページ](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="3f7ef-164">[![The Index view content page](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span></span>

<span data-ttu-id="3f7ef-165">**図 05**: インデックス ビューのコンテンツ ページ ([フルサイズの画像を表示する をクリック](creating-page-layouts-with-view-master-pages-cs/_static/image15.png)します )</span><span class="sxs-lookup"><span data-stu-id="3f7ef-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span></span>

### <a name="modifying-view-master-page-content"></a><span data-ttu-id="3f7ef-166">マスター ページの表示コンテンツの変更</span><span class="sxs-lookup"><span data-stu-id="3f7ef-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="3f7ef-167">ビュー マスター ページを操作するときに直ちに発生する問題の 1 つは、異なるビュー コンテンツ ページが要求されたときにビュー マスター ページのコンテンツを変更する問題です。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="3f7ef-168">たとえば、Web アプリケーションの各ページに固有のタイトルを設定します。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="3f7ef-169">ただし、タイトルはビュー のマスター ページで宣言され、ビュー コンテンツ ページでは宣言されません。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="3f7ef-170">では、各ビュー コンテンツ ページのページ タイトルをどのようにカスタマイズすればよいでしょうか。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="3f7ef-171">ビュー コンテンツ ページで表示されるタイトルを変更するには、2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="3f7ef-172">まず、ビュー コンテンツ ページの上部で宣言された`<%@ page %>`ディレクティブの title 属性にページ タイトルを割り当てます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="3f7ef-173">たとえば、ページタイトル「スーパーグレートWebサイト」をインデックスビューに割り当てる場合、インデックスビューの上部に次のディレクティブを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

<span data-ttu-id="3f7ef-174">インデックス ビューがブラウザにレンダリングされると、ブラウザのタイトル バーに目的のタイトルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>

<span data-ttu-id="3f7ef-175">[![ブラウザーのタイトル バー](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="3f7ef-175">[![Browser title bar](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span></span>

<span data-ttu-id="3f7ef-176">title 属性が機能するためにマスター ビュー ページが満たす必要がある重要な要件が 1 つあります。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="3f7ef-177">ビュー マスター ページには、`<head runat="server">`ヘッダーの通常`<head>`のタグではなく、タグが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="3f7ef-178">タグに`<head>`runat="server" 属性が含まれていない場合、タイトルは表示されません。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="3f7ef-179">既定のビュー マスター ページには`<head runat="server">`、必要なタグが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="3f7ef-180">個々のビュー コンテンツ ページからマスター ページのコンテンツを変更する別の方法として、`<asp:ContentPlaceHolder>`タグで変更する領域をラップします。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="3f7ef-181">たとえば、マスター ビュー ページによってレンダリングされるタイトルだけでなく、メタ タグも変更するとします。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="3f7ef-182">リスト 4 のマスター ビュー`<asp:ContentPlaceHolder>`ページには、`<head>`そのタグ内にタグが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

<span data-ttu-id="3f7ef-183">**リスト4 –`Views\Shared\Site2.master`**</span><span class="sxs-lookup"><span data-stu-id="3f7ef-183">**Listing 4 – `Views\Shared\Site2.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

<span data-ttu-id="3f7ef-184">リスト 4`<asp:ContentPlaceHolder>`のタグには、デフォルトのタイトルとデフォルトのメタタグのデフォルトコンテンツが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="3f7ef-185">個々のビューコンテンツページでこの`<asp:ContentPlaceHolder>`タグを上書きしない場合は、デフォルトのコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="3f7ef-186">リスト 5 のコンテンツ ビュー ページ`<asp:ContentPlaceHolder>`は、カスタム タイトルとカスタム メタ タグを表示するためにタグを上書きします。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

<span data-ttu-id="3f7ef-187">**リスト5 –`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="3f7ef-187">**Listing 5 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="3f7ef-188">まとめ</span><span class="sxs-lookup"><span data-stu-id="3f7ef-188">Summary</span></span>

<span data-ttu-id="3f7ef-189">このチュートリアルでは、マスター ページの表示とコンテンツ ページの表示に関する基本的な概要を説明しました。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="3f7ef-190">新しいビュー マスター ページを作成し、そのマスター ページに基づいてコンテンツ ページを作成する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="3f7ef-191">また、特定のビュー コンテンツ ページからビュー マスター ページのコンテンツを変更する方法についても説明しました。</span><span class="sxs-lookup"><span data-stu-id="3f7ef-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3f7ef-192">[前へ](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [次へ](passing-data-to-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="3f7ef-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
[Next](passing-data-to-view-master-pages-cs.md)</span></span>
