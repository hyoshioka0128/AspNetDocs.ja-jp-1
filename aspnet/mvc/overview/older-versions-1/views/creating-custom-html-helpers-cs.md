---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: カスタム HTML ヘルパーの作成 (C#) |マイクロソフトドキュメント
author: microsoft
description: このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示します。 HTMLヘルパーを利用して.
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a2e5a5b42aa5bf267a42fef2fcad7022001ce6f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675338"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="7171e-104">カスタム HTML ヘルパーの作成 (C#)</span><span class="sxs-lookup"><span data-stu-id="7171e-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="7171e-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7171e-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="7171e-106">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="7171e-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="7171e-107">このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="7171e-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="7171e-108">HTML ヘルパーを利用することで、標準 HTML ページを作成するために実行する必要がある HTML タグの手間のかかる入力を減らすことができます。</span><span class="sxs-lookup"><span data-stu-id="7171e-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="7171e-109">このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="7171e-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="7171e-110">HTML ヘルパーを利用することで、標準 HTML ページを作成するために実行する必要がある HTML タグの手間のかかる入力を減らすことができます。</span><span class="sxs-lookup"><span data-stu-id="7171e-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="7171e-111">このチュートリアルの最初の部分では、ASP.NET MVC フレームワークに含まれている既存の HTML ヘルパーのいくつかを説明します。</span><span class="sxs-lookup"><span data-stu-id="7171e-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="7171e-112">次に、カスタム HTML ヘルパーを作成する 2 つのメソッドについて説明します: 静的メソッドを作成し、拡張メソッドを作成することによってカスタム HTML ヘルパーを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7171e-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="7171e-113">HTML ヘルパーについて</span><span class="sxs-lookup"><span data-stu-id="7171e-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="7171e-114">HTML ヘルパーは、文字列を返すメソッドにすぎません。</span><span class="sxs-lookup"><span data-stu-id="7171e-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="7171e-115">文字列は、必要な任意の種類のコンテンツを表すことができます。</span><span class="sxs-lookup"><span data-stu-id="7171e-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="7171e-116">たとえば、HTML ヘルパーを使用して、HTML`<input>`やタグなどの標準 HTML`<img>`タグをレンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="7171e-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="7171e-117">また、HTML ヘルパーを使用して、タブ ストリップやデータベース データの HTML テーブルなど、より複雑なコンテンツをレンダリングすることもできます。</span><span class="sxs-lookup"><span data-stu-id="7171e-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="7171e-118">ASP.NET MVC フレームワークには、次の標準 HTML ヘルパーのセットが含まれています (完全な一覧ではありません)。</span><span class="sxs-lookup"><span data-stu-id="7171e-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="7171e-119">アクションリンク()</span><span class="sxs-lookup"><span data-stu-id="7171e-119">Html.ActionLink()</span></span>
- <span data-ttu-id="7171e-120">を開始します。</span><span class="sxs-lookup"><span data-stu-id="7171e-120">Html.BeginForm()</span></span>
- <span data-ttu-id="7171e-121">チェックボックス()</span><span class="sxs-lookup"><span data-stu-id="7171e-121">Html.CheckBox()</span></span>
- <span data-ttu-id="7171e-122">をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7171e-122">Html.DropDownList()</span></span>
- <span data-ttu-id="7171e-123">をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7171e-123">Html.EndForm()</span></span>
- <span data-ttu-id="7171e-124">隠された()</span><span class="sxs-lookup"><span data-stu-id="7171e-124">Html.Hidden()</span></span>
- <span data-ttu-id="7171e-125">リストボックス()</span><span class="sxs-lookup"><span data-stu-id="7171e-125">Html.ListBox()</span></span>
- <span data-ttu-id="7171e-126">パスワード()</span><span class="sxs-lookup"><span data-stu-id="7171e-126">Html.Password()</span></span>
- <span data-ttu-id="7171e-127">ラジオボタン()</span><span class="sxs-lookup"><span data-stu-id="7171e-127">Html.RadioButton()</span></span>
- <span data-ttu-id="7171e-128">テキストエリア()</span><span class="sxs-lookup"><span data-stu-id="7171e-128">Html.TextArea()</span></span>
- <span data-ttu-id="7171e-129">テキストボックス()</span><span class="sxs-lookup"><span data-stu-id="7171e-129">Html.TextBox()</span></span>

<span data-ttu-id="7171e-130">たとえば、リスト 1 のフォームを考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="7171e-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="7171e-131">このフォームは、2 つの標準 HTML ヘルパーの助けを借りてレンダリングされます (図 1 を参照)。</span><span class="sxs-lookup"><span data-stu-id="7171e-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="7171e-132">このフォームでは、 `Html.BeginForm()` `Html.TextBox()`および Helper メソッドを使用して、単純な HTML フォームをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="7171e-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="7171e-133">[![HTML ヘルパーで表示されるページ](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7171e-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="7171e-134">**図 01**: HTML ヘルパーで表示されるページ ([フルサイズの画像を表示する をクリック](creating-custom-html-helpers-cs/_static/image3.png)して )</span><span class="sxs-lookup"><span data-stu-id="7171e-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="7171e-135">**リスト1 –`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="7171e-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="7171e-136">Html.BeginForm() ヘルパー メソッドは、HTML`<form>`タグの開始タグと終了タグを作成するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="7171e-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="7171e-137">`Html.BeginForm()`メソッドが using ステートメント内で呼び出されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7171e-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="7171e-138">using ステートメントは、タグ`<form>`が using ブロックの最後で閉じられることを保証します。</span><span class="sxs-lookup"><span data-stu-id="7171e-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="7171e-139">必要に応じて、使用ブロックを作成する代わりに、Html.EndForm() ヘルパー メソッドを呼び`<form>`出してタグを閉じることもできます。</span><span class="sxs-lookup"><span data-stu-id="7171e-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="7171e-140">最も直感的に見える開始タグと終了`<form>`タグを作成するには、どちらの方法を使用しても問題ありません。</span><span class="sxs-lookup"><span data-stu-id="7171e-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="7171e-141">ヘルパー`Html.TextBox()`メソッドは、リスト 1 で`<input>`HTML タグをレンダリングするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="7171e-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="7171e-142">ブラウザで [ソースの表示] を選択すると、リスト 2 に HTML ソースが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7171e-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="7171e-143">ソースに標準の HTML タグが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7171e-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7171e-144">HTML ヘルパー`Html.TextBox()`は`<%= %>``<% %>`タグではなくタグでレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="7171e-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="7171e-145">等号を含めなければ、ブラウザには何も表示されません。</span><span class="sxs-lookup"><span data-stu-id="7171e-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="7171e-146">mvc フレームワークASP.NETには、少数のヘルパーセットが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7171e-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="7171e-147">ほとんどの場合、カスタム HTML ヘルパーを使用して MVC フレームワークを拡張する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7171e-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="7171e-148">このチュートリアルの残りの部分では、カスタム HTML ヘルパーを作成する 2 つの方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="7171e-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="7171e-149">**リスト2 –`Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="7171e-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="7171e-150">静的メソッドを使用した HTML ヘルパーの作成</span><span class="sxs-lookup"><span data-stu-id="7171e-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="7171e-151">新しい HTML ヘルパーを作成する最も簡単な方法は、文字列を返す静的メソッドを作成することです。</span><span class="sxs-lookup"><span data-stu-id="7171e-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="7171e-152">たとえば、HTML`<label>`タグを表示する新しい HTML ヘルパーを作成するとします。</span><span class="sxs-lookup"><span data-stu-id="7171e-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="7171e-153">リスト 2 のクラスを使用して`<label>`、 をレンダリングできます。</span><span class="sxs-lookup"><span data-stu-id="7171e-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="7171e-154">**リスト2 –`Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="7171e-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="7171e-155">リスト 2 のクラスについて特別なことは何もありません。</span><span class="sxs-lookup"><span data-stu-id="7171e-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="7171e-156">この`Label()`メソッドは、単に文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="7171e-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="7171e-157">リスト 3 の変更されたインデックス`LabelHelper`ビューでは、`<label>`を使用して HTML タグをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="7171e-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="7171e-158">ビューには、名前空間を`<%@ imports %>`インポートするディレクティブが含まれていること`Application1.Helpers`に注意してください。</span><span class="sxs-lookup"><span data-stu-id="7171e-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="7171e-159">**リスト2 –`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="7171e-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="7171e-160">拡張メソッドを使用した HTML ヘルパーの作成</span><span class="sxs-lookup"><span data-stu-id="7171e-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="7171e-161">ASP.NET MVC フレームワークに含まれる標準の HTML ヘルパーと同じように動作する HTML ヘルパーを作成する場合は、拡張メソッドを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7171e-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="7171e-162">拡張メソッドを使用すると、既存のクラスに新しいメソッドを追加できます。</span><span class="sxs-lookup"><span data-stu-id="7171e-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="7171e-163">HTML ヘルパー メソッドを作成するときは、ビューの Html プロパティで表される HtmlHelper クラスに新しいメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="7171e-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="7171e-164">リスト 3 のクラスは、 という名前`HtmlHelper``Label()`のクラスに拡張メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="7171e-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="7171e-165">このクラスについて注意すべき点がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="7171e-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="7171e-166">まず、クラスが静的クラスであることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7171e-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="7171e-167">静的クラスを使用して拡張メソッドを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7171e-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="7171e-168">次に、`Label()`メソッドの最初のパラメータの前にキーワード`this`が付いていることに注目してください。</span><span class="sxs-lookup"><span data-stu-id="7171e-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="7171e-169">拡張メソッドの最初のパラメーターは、拡張メソッドが拡張するクラスを示します。</span><span class="sxs-lookup"><span data-stu-id="7171e-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="7171e-170">**リスト3 –`Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="7171e-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="7171e-171">拡張メソッドを作成し、アプリケーションを正常にビルドすると、クラスの他のすべてのメソッドと同様に、拡張メソッドが Visual Studio Intellisense に表示されます (図 2 参照)。</span><span class="sxs-lookup"><span data-stu-id="7171e-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="7171e-172">唯一の違いは、拡張メソッドが、その横に特別な記号 (下向き矢印のアイコン) が付いた表示です。</span><span class="sxs-lookup"><span data-stu-id="7171e-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="7171e-173">[![拡張メソッドを使用する](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="7171e-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="7171e-174">**図 02**: Html.Label() 拡張メソッドを使用して ([フルサイズの画像を表示する をクリック](creating-custom-html-helpers-cs/_static/image6.png)します)</span><span class="sxs-lookup"><span data-stu-id="7171e-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="7171e-175">リスト 4 の変更されたインデックス ビューでは、Html.Label() 拡張メソッドを`<label>`使用して、すべてのタグを表示します。</span><span class="sxs-lookup"><span data-stu-id="7171e-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="7171e-176">**リスト4 –`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="7171e-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="7171e-177">まとめ</span><span class="sxs-lookup"><span data-stu-id="7171e-177">Summary</span></span>

<span data-ttu-id="7171e-178">このチュートリアルでは、カスタム HTML ヘルパーを作成する 2 つの方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="7171e-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="7171e-179">まず、文字列を返す静的メソッドを`Label()`作成してカスタム HTML ヘルパーを作成する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="7171e-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="7171e-180">次に、クラスに拡張メソッドを作成`Label()`してカスタム HTML ヘルパー メソッドを作成`HtmlHelper`する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="7171e-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="7171e-181">このチュートリアルでは、非常に単純な HTML ヘルパー メソッドの構築に重点を置きました。</span><span class="sxs-lookup"><span data-stu-id="7171e-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="7171e-182">HTML ヘルパーは、必要に応じて複雑になる可能性があることを認識します。</span><span class="sxs-lookup"><span data-stu-id="7171e-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="7171e-183">ツリー ビュー、メニュー、データベース データのテーブルなどのリッチ コンテンツを表示する HTML ヘルパーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="7171e-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7171e-184">[前へ](asp-net-mvc-views-overview-cs.md)
> [次へ](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="7171e-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
