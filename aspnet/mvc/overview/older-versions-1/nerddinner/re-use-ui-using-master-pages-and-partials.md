---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: マスター ページと部分を使用して UI を再利用する |マイクロソフトドキュメント
author: rick-anderson
description: ステップ7では、部分的なビューテンプレートとマスターページを使用して、コードの重複を排除するために、ビューテンプレート内に「DRY原則」を適用する方法を見てみましょう。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f381c4424a9fa0718cd234beeb01ce41bc4ca61e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542600"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a><span data-ttu-id="48f62-103">マスター ページと部分を利用して UI を再使用する</span><span class="sxs-lookup"><span data-stu-id="48f62-103">Re-use UI Using Master Pages and Partials</span></span>

<span data-ttu-id="48f62-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="48f62-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="48f62-105">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="48f62-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="48f62-106">これは、MVC 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)の手順 7 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="48f62-106">This is step 7 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="48f62-107">ステップ7では、部分的なビューテンプレートとマスターページを使用して、コードの重複を排除するために、ビューテンプレート内の「DRY原則」を適用する方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="48f62-107">Step 7 looks at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication, using partial view templates and master pages.</span></span>
> 
> <span data-ttu-id="48f62-108">mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="48f62-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-7-partials-and-master-pages"></a><span data-ttu-id="48f62-109">NerdDinner ステップ 7: パーシャルとマスター ページ</span><span class="sxs-lookup"><span data-stu-id="48f62-109">NerdDinner Step 7: Partials and Master Pages</span></span>

<span data-ttu-id="48f62-110">MVCが受け入れるデザイン哲学ASP.NET一つは、「自分自身を繰り返さない」原則(一般的に「DRY」と呼ばれる)です。</span><span class="sxs-lookup"><span data-stu-id="48f62-110">One of the design philosophies ASP.NET MVC embraces is the "Do Not Repeat Yourself" principle (commonly referred to as "DRY").</span></span> <span data-ttu-id="48f62-111">DRY 設計はコードとロジックの重複を排除し、最終的にアプリケーションの構築を高速化し、保守が容易になります。</span><span class="sxs-lookup"><span data-stu-id="48f62-111">A DRY design helps eliminate the duplication of code and logic, which ultimately makes applications faster to build and easier to maintain.</span></span>

<span data-ttu-id="48f62-112">私たちはすでにいくつかのNerdDinnerシナリオで適用されるDRY原則を見てきました。</span><span class="sxs-lookup"><span data-stu-id="48f62-112">We've already seen the DRY principle applied in several of our NerdDinner scenarios.</span></span> <span data-ttu-id="48f62-113">いくつかの例: 検証ロジックはモデルレイヤー内に実装されており、コントローラーの編集シナリオと作成シナリオの両方に適用できます。編集、詳細、および削除アクション メソッド全体で "NotFound" ビュー テンプレートを再利用しています。ビューテンプレートで規約命名パターンを使用しています。また、編集と作成の両方のアクション シナリオに対して、DinnerFormViewModel クラスを再利用しています。</span><span class="sxs-lookup"><span data-stu-id="48f62-113">A few examples: our validation logic is implemented within our model layer, which enables it to be enforced across both edit and create scenarios in our controller; we are re-using the "NotFound" view template across the Edit, Details and Delete action methods; we are using a convention- naming pattern with our view templates, which eliminates the need to explicitly specify the name when we call the View() helper method; and we are re-using the DinnerFormViewModel class for both Edit and Create action scenarios.</span></span>

<span data-ttu-id="48f62-114">ここで、ビューテンプレート内の「DRY原則」を適用してコードの重複を排除する方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="48f62-114">Let's now look at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication there as well.</span></span>

### <a name="re-visiting-our-edit-and-create-view-templates"></a><span data-ttu-id="48f62-115">編集と作成のビュー テンプレートに再アクセスします。</span><span class="sxs-lookup"><span data-stu-id="48f62-115">Re-visiting our Edit and Create View Templates</span></span>

<span data-ttu-id="48f62-116">現在、"Edit.aspx" と "Create.aspx" という 2 つの異なるビュー テンプレートを使用して、ディナー フォームの UI を表示しています。</span><span class="sxs-lookup"><span data-stu-id="48f62-116">Currently we are using two different view templates – "Edit.aspx" and "Create.aspx" – to display our Dinner form UI.</span></span> <span data-ttu-id="48f62-117">それらの簡単な視覚的な比較は、それらがどれほど似ているかを強調します。</span><span class="sxs-lookup"><span data-stu-id="48f62-117">A quick visual comparison of them highlights how similar they are.</span></span> <span data-ttu-id="48f62-118">作成フォームは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="48f62-118">Below is what the create form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

<span data-ttu-id="48f62-119">そして、私たちの"編集"フォームは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="48f62-119">And here is what our "Edit" form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

<span data-ttu-id="48f62-120">大きな違いはありませんか?</span><span class="sxs-lookup"><span data-stu-id="48f62-120">Not much of a difference is there?</span></span> <span data-ttu-id="48f62-121">タイトルとヘッダーテキスト以外のフォームレイアウトと入力コントロールは同じです。</span><span class="sxs-lookup"><span data-stu-id="48f62-121">Other than the title and header text, the form layout and input controls are identical.</span></span>

<span data-ttu-id="48f62-122">"Edit.aspx" ビュー テンプレートと "Create.aspx" ビュー テンプレートを開くと、同じフォーム レイアウトと入力コントロール コードが含まれていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="48f62-122">If we open up the "Edit.aspx" and "Create.aspx" view templates we'll find that they contain identical form layout and input control code.</span></span> <span data-ttu-id="48f62-123">この重複は、新しいDinnerプロパティを導入または変更するたびに2回変更する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="48f62-123">This duplication means we end up having to make changes twice anytime we introduce or change a new Dinner property - which is not good.</span></span>

### <a name="using-partial-view-templates"></a><span data-ttu-id="48f62-124">部分ビュー テンプレートの使用</span><span class="sxs-lookup"><span data-stu-id="48f62-124">Using Partial View Templates</span></span>

<span data-ttu-id="48f62-125">ASP.NET MVC では、ページの部分部分のビュー レンダリング ロジックをカプセル化するために使用できる "部分ビュー" テンプレートを定義する機能がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="48f62-125">ASP.NET MVC supports the ability to define "partial view" templates that can be used to encapsulate view rendering logic for a sub-portion of a page.</span></span> <span data-ttu-id="48f62-126">"Partials" は、ビュー レンダリング ロジックを一度定義し、アプリケーション全体の複数の場所で再利用する便利な方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="48f62-126">"Partials" provide a useful way to define view rendering logic once, and then re-use it in multiple places across an application.</span></span>

<span data-ttu-id="48f62-127">Edit.aspx と Create.aspx ビュー テンプレートの重複を "DRY-up" にするため、フォーム レイアウトと両方に共通する入力要素をカプセル化する"DinnerForm.ascx" という名前の部分ビュー テンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="48f62-127">To help "DRY-up" our Edit.aspx and Create.aspx view template duplication, we can create a partial view template named "DinnerForm.ascx" that encapsulates the form layout and input elements common to both.</span></span> <span data-ttu-id="48f62-128">これを行うには、/Views/Dinnersディレクトリを右クリックし、[&gt;ビューの追加]メニューコマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="48f62-128">We'll do this by right-clicking on our /Views/Dinners directory and choosing the "Add-&gt;View" menu command:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

<span data-ttu-id="48f62-129">これにより、[ビューの追加] ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="48f62-129">This will display the "Add View" dialog.</span></span> <span data-ttu-id="48f62-130">"DinnerForm" を作成する新しいビューに名前を付け、ダイアログ内の [部分ビューを作成する] チェック ボックスをオンにして、それを DinnerFormViewModel クラスに渡すことを示します。</span><span class="sxs-lookup"><span data-stu-id="48f62-130">We'll name the new view we want to create "DinnerForm", select the "Create a partial view" checkbox within the dialog, and indicate that we will pass it a DinnerFormViewModel class:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

<span data-ttu-id="48f62-131">[追加] ボタンをクリックすると、Visual Studio は "\Views\Dinners" ディレクトリ内に新しい "DinnerForm.ascx" ビュー テンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="48f62-131">When we click the "Add" button, Visual Studio will create a new "DinnerForm.ascx" view template for us within the "\Views\Dinners" directory.</span></span>

<span data-ttu-id="48f62-132">その後、Edit.aspx/Create.aspx ビュー テンプレートから重複したフォーム レイアウト/入力コントロール コードをコピー/貼り付け、新しい "DinnerForm.ascx" 部分ビュー テンプレートに貼り付けることができます。</span><span class="sxs-lookup"><span data-stu-id="48f62-132">We can then copy/paste the duplicate form layout / input control code from our Edit.aspx/ Create.aspx view templates into our new "DinnerForm.ascx" partial view template:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

<span data-ttu-id="48f62-133">その後、編集ビューテンプレートと作成ビューテンプレートを更新して、DinnerForm 部分テンプレートを呼び出してフォームの重複を排除できます。</span><span class="sxs-lookup"><span data-stu-id="48f62-133">We can then update our Edit and Create view templates to call the DinnerForm partial template and eliminate the form duplication.</span></span> <span data-ttu-id="48f62-134">これを行うには、ビューテンプレート内でHtml.RenderPartial(「ディナーフォーム」)を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="48f62-134">We can do this by calling Html.RenderPartial("DinnerForm") within our view templates:</span></span>

##### <a name="createaspx"></a><span data-ttu-id="48f62-135">aspx を作成します。</span><span class="sxs-lookup"><span data-stu-id="48f62-135">Create.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a><span data-ttu-id="48f62-136">編集.aspx</span><span class="sxs-lookup"><span data-stu-id="48f62-136">Edit.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

<span data-ttu-id="48f62-137">Html.RenderPartial を呼び出すときに、目的の部分テンプレートのパスを明示的に修飾できます (たとえば、~ビュー/ディナー/DinnerForm.ascx")。</span><span class="sxs-lookup"><span data-stu-id="48f62-137">You can explicitly qualify the path of the partial template you want when calling Html.RenderPartial (for example: ~Views/Dinners/DinnerForm.ascx").</span></span> <span data-ttu-id="48f62-138">ただし、上記のコードでは、ASP.NET MVC 内の規約ベースの名前付けパターンを利用し、レンダリングする部分の名前として "DinnerForm" を指定しています。</span><span class="sxs-lookup"><span data-stu-id="48f62-138">In our code above, though, we are taking advantage of the convention-based naming pattern within ASP.NET MVC, and just specifying "DinnerForm" as the name of the partial to render.</span></span> <span data-ttu-id="48f62-139">これを行うときASP.NETMVCは、コンベンションベースのビューディレクトリで最初に見ます (DinnersControllerの場合、これは /Views/ディナーになります)。</span><span class="sxs-lookup"><span data-stu-id="48f62-139">When we do this ASP.NET MVC will look first in the convention-based views directory (for DinnersController this would be /Views/Dinners).</span></span> <span data-ttu-id="48f62-140">そこに部分テンプレートが見つからない場合は、/Views/Shared ディレクトリで探します。</span><span class="sxs-lookup"><span data-stu-id="48f62-140">If it doesn't find the partial template there it will then look for it in the /Views/Shared directory.</span></span>

<span data-ttu-id="48f62-141">部分ビューの名前だけを使用して Html.RenderPartial() が呼び出されると、ASP.NET MVC は、呼び出し元のビュー テンプレートで使用される同じモデルと ViewData ディクショナリ オブジェクトを部分ビューに渡します。</span><span class="sxs-lookup"><span data-stu-id="48f62-141">When Html.RenderPartial() is called with just the name of the partial view, ASP.NET MVC will pass to the partial view the same Model and ViewData dictionary objects used by the calling view template.</span></span> <span data-ttu-id="48f62-142">または、Html.RenderPartial() のオーバーロードされたバージョンがあり、これを使用して、部分ビューに使用する代替モデル オブジェクトや ViewData ディクショナリを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="48f62-142">Alternatively, there are overloaded versions of Html.RenderPartial() that enable you to pass an alternate Model object and/or ViewData dictionary for the partial view to use.</span></span> <span data-ttu-id="48f62-143">これは、完全なモデル/ビューモデルのサブセットのみを渡すシナリオに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="48f62-143">This is useful for scenarios where you only want to pass a subset of the full Model/ViewModel.</span></span>

| <span data-ttu-id="48f62-144">**サイドトピック: &lt;%=&gt; &gt;%&lt;ではなく % % が %**</span><span class="sxs-lookup"><span data-stu-id="48f62-144">**Side Topic: Why &lt;% %&gt; instead of &lt;%= %&gt;?**</span></span> |
| --- |
| <span data-ttu-id="48f62-145">上記のコードで気づいたことの 1 つは、Html.RenderPartial()&lt;を呼&gt;び出すときに&lt;%=&gt; % ブロックではなく % ブロックを使用していることです。</span><span class="sxs-lookup"><span data-stu-id="48f62-145">One of the subtle things you might have noticed with the code above is that we are using a &lt;% %&gt; block instead of a &lt;%= %&gt; block when calling Html.RenderPartial().</span></span> <span data-ttu-id="48f62-146">&lt;ASP.NETの&gt;%= % ブロックは、開発者が指定した値をレンダリングすることを示&lt;します (たとえば、%= "Hello" % が&gt;"Hello" をレンダリングします)。</span><span class="sxs-lookup"><span data-stu-id="48f62-146">&lt;%= %&gt; blocks in ASP.NET indicate that a developer wants to render a specified value (for example: &lt;%= "Hello" %&gt; would render "Hello").</span></span> <span data-ttu-id="48f62-147">&lt;%&gt;ブロックは、代わりに、開発者がコードを実行する必要があり、その中のレンダリングされた出力を明示的に実行する必要&lt;があることを示します ( たとえば、 %&gt;Response.Write("Hello") % 。</span><span class="sxs-lookup"><span data-stu-id="48f62-147">&lt;% %&gt; blocks instead indicate that the developer wants to execute code, and that any rendered output within them must be done explicitly (for example: &lt;% Response.Write("Hello") %&gt;.</span></span> <span data-ttu-id="48f62-148">上記の Html.RenderPartial&gt;コードで % ブロックを&lt;使用している理由は、Html.RenderPartial() メソッドが文字列を返さないため、代わりにコンテンツを呼び出し元のビュー テンプレートの出力ストリームに直接出力するためです。</span><span class="sxs-lookup"><span data-stu-id="48f62-148">The reason we are using a &lt;% %&gt; block with our Html.RenderPartial code above is because the Html.RenderPartial() method doesn't return a string, and instead outputs the content directly to the calling view template's output stream.</span></span> <span data-ttu-id="48f62-149">これは、パフォーマンス効率の理由から行われ、そうすることで(潜在的に非常に大きな)一時的な文字列オブジェクトを作成する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="48f62-149">It does this for performance efficiency reasons, and by doing so it avoids the need to create a (potentially very large) temporary string object.</span></span> <span data-ttu-id="48f62-150">これにより、メモリ使用量が削減され、アプリケーション全体のスループットが向上します。</span><span class="sxs-lookup"><span data-stu-id="48f62-150">This reduces memory usage and improves overall application throughput.</span></span> <span data-ttu-id="48f62-151">Html.RenderPartial() を使用する場合の一般的な誤りの 1 つは、呼び出しの末尾にセミ&lt;コロンを&gt;追加するのを忘れて % ブロック内に入るということです。</span><span class="sxs-lookup"><span data-stu-id="48f62-151">One common mistake when using Html.RenderPartial() is to forget to add a semi-colon at the end of the call when it is within a &lt;% %&gt; block.</span></span> <span data-ttu-id="48f62-152">たとえば、このコードはコンパイラ エラーを引き&lt;起こします: % Html.RenderPartial("DinnerForm")&gt; %&lt;代わりに書く必要があります。%&gt; %&gt; &lt;ブロックは自己完結型のコード ステートメントであり、C# コード ステートメントを使用する場合はセミコロンで終了する必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="48f62-152">For example, this code will cause a compiler error: &lt;% Html.RenderPartial("DinnerForm") %&gt; You instead need to write: &lt;% Html.RenderPartial("DinnerForm"); %&gt; This is because &lt;% %&gt; blocks are self-contained code statements, and when using C# code statements need to be terminated with a semi-colon.</span></span> |

### <a name="using-partial-view-templates-to-clarify-code"></a><span data-ttu-id="48f62-153">部分ビュー テンプレートを使用したコードの明確化</span><span class="sxs-lookup"><span data-stu-id="48f62-153">Using Partial View Templates to Clarify Code</span></span>

<span data-ttu-id="48f62-154">複数の場所でビューレンダリングロジックを複製することを避けるために、「DinnerForm」部分ビューテンプレートを作成しました。</span><span class="sxs-lookup"><span data-stu-id="48f62-154">We created the "DinnerForm" partial view template to avoid duplicating view rendering logic in multiple places.</span></span> <span data-ttu-id="48f62-155">これは、部分ビュー テンプレートを作成する最も一般的な理由です。</span><span class="sxs-lookup"><span data-stu-id="48f62-155">This is the most common reason to create partial view templates.</span></span>

<span data-ttu-id="48f62-156">単一の場所で呼び出されている場合でも、部分的なビューを作成することは意味があります。</span><span class="sxs-lookup"><span data-stu-id="48f62-156">Sometimes it still makes sense to create partial views even when they are only being called in a single place.</span></span> <span data-ttu-id="48f62-157">ビュー レンダリング ロジックを抽出して、1 つ以上の適切な名前の部分テンプレートに分割すると、非常に複雑なビュー テンプレートが読みやすくなります。</span><span class="sxs-lookup"><span data-stu-id="48f62-157">Very complicated view templates can often become much easier to read when their view rendering logic is extracted and partitioned into one or more well named partial templates.</span></span>

<span data-ttu-id="48f62-158">たとえば、プロジェクトの Site.master ファイルの次のコード スニペットを考えてみましょう (このコードはまもなく見ています)。</span><span class="sxs-lookup"><span data-stu-id="48f62-158">For example, consider the below code-snippet from the Site.master file in our project (which we will be looking at shortly).</span></span> <span data-ttu-id="48f62-159">このコードは、画面の右上にログイン/ログアウトリンクを表示するロジックが"LogOnUserControl"部分にカプセル化されているため、読み取りが比較的簡単です。</span><span class="sxs-lookup"><span data-stu-id="48f62-159">The code is relatively straight-forward to read – partly because the logic to display a login/logout link at the top right of the screen is encapsulated within the "LogOnUserControl" partial:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

<span data-ttu-id="48f62-160">ビュー テンプレート内の html/code マークアップを理解しようとして混乱を見つけるたびに、その一部が抽出され、適切な名前の部分ビューにリファクタリングされた場合、そのマークアップが明確にならないかどうかを検討してください。</span><span class="sxs-lookup"><span data-stu-id="48f62-160">Whenever you find yourself getting confused trying to understand the html/code markup within a view-template, consider whether it wouldn't be clearer if some of it was extracted and refactored into well-named partial views.</span></span>

### <a name="master-pages"></a><span data-ttu-id="48f62-161">マスター ページ</span><span class="sxs-lookup"><span data-stu-id="48f62-161">Master Pages</span></span>

<span data-ttu-id="48f62-162">部分的なビューをサポートするだけでなく、ASP.NET MVC は、サイトの共通のレイアウトとトップレベルの html を定義するために使用できる「マスター ページ」テンプレートを作成する機能もサポートします。</span><span class="sxs-lookup"><span data-stu-id="48f62-162">In addition to supporting partial views, ASP.NET MVC also supports the ability to create "master page" templates that can be used to define the common layout and top-level html of a site.</span></span> <span data-ttu-id="48f62-163">コンテンツ プレースホルダ コントロールをマスター ページに追加して、ビューで上書きまたは "塗りつぶし" できる置き換え可能領域を識別できます。</span><span class="sxs-lookup"><span data-stu-id="48f62-163">Content placeholder controls can then be added to the master page to identify replaceable regions that can be overridden or "filled in" by views.</span></span> <span data-ttu-id="48f62-164">これにより、アプリケーション全体に共通のレイアウトを適用する非常に効果的な (および DRY) 方法が提供されます。</span><span class="sxs-lookup"><span data-stu-id="48f62-164">This provides a very effective (and DRY) way to apply a common layout across an application.</span></span>

<span data-ttu-id="48f62-165">既定では、新しいASP.NET MVC プロジェクトには、マスター ページ テンプレートが自動的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="48f62-165">By default, new ASP.NET MVC projects have a master page template automatically added to them.</span></span> <span data-ttu-id="48f62-166">このマスター ページは "Site.master" と名付けられ、\Views\Shared\ フォルダ内にあります。</span><span class="sxs-lookup"><span data-stu-id="48f62-166">This master page is named "Site.master" and lives within the \Views\Shared\ folder:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

<span data-ttu-id="48f62-167">既定の Site.master ファイルは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="48f62-167">The default Site.master file looks like below.</span></span> <span data-ttu-id="48f62-168">これは、サイトの外側のHTMLと上部のナビゲーション用のメニューを定義します。</span><span class="sxs-lookup"><span data-stu-id="48f62-168">It defines the outer html of the site, along with a menu for navigation at the top.</span></span> <span data-ttu-id="48f62-169">このコントロールには、タイトル用と、ページのプライマリ コンテンツを置き換える場所の 2 つの置き換え可能なコンテンツ プレースホルダ コントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="48f62-169">It contains two replaceable content placeholder controls – one for the title, and the other for where the primary content of a page should be replaced:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

<span data-ttu-id="48f62-170">NerdDinner アプリケーション用に作成したすべてのビュー テンプレート (「リスト」、「詳細」、「編集」、「作成」、「NotFound」など) は、この Site.master テンプレートに基づいています。</span><span class="sxs-lookup"><span data-stu-id="48f62-170">All of the view templates we've created for our NerdDinner application ("List", "Details", "Edit", "Create", "NotFound", etc) have been based on this Site.master template.</span></span> <span data-ttu-id="48f62-171">これは、[ビューの追加] ダイアログを使用してビューを作成したときに、既定でトップ&lt;% @&gt; Page % ディレクティブに追加された "MasterPageFile" 属性によって示されます。</span><span class="sxs-lookup"><span data-stu-id="48f62-171">This is indicated via the "MasterPageFile" attribute that was added by default to the top &lt;% @ Page %&gt; directive when we created our views using the "Add View" dialog:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

<span data-ttu-id="48f62-172">つまり、Site.master コンテンツを変更し、ビュー テンプレートをレンダリングするときに変更を自動的に適用して使用することができます。</span><span class="sxs-lookup"><span data-stu-id="48f62-172">What this means is that we can change the Site.master content, and have the changes automatically be applied and used when we render any of our view templates.</span></span>

<span data-ttu-id="48f62-173">Site.master のヘッダー セクションを更新して、アプリケーションのヘッダーが "My MVC アプリケーション" ではなく "NerdDinner" になるようにします。</span><span class="sxs-lookup"><span data-stu-id="48f62-173">Let's update our Site.master's header section so that the header of our application is "NerdDinner" instead of "My MVC Application".</span></span> <span data-ttu-id="48f62-174">また、最初のタブが "夕食を検索" (HomeController の Index() アクションメソッドによって処理される) になるようにナビゲーションメニューを更新し、"夕食のホスト" という新しいタブを追加しましょう (DinnersController の Create() アクションメソッドによって処理されます)。</span><span class="sxs-lookup"><span data-stu-id="48f62-174">Let's also update our navigation menu so that the first tab is "Find a Dinner" (handled by the HomeController's Index() action method), and let's add a new tab called "Host a Dinner" (handled by the DinnersController's Create() action method):</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

<span data-ttu-id="48f62-175">Site.master ファイルを保存してブラウザを更新すると、ヘッダーの変更がアプリケーション内のすべてのビューに表示されます。</span><span class="sxs-lookup"><span data-stu-id="48f62-175">When we save the Site.master file and refresh our browser we'll see our header changes show up across all views within our application.</span></span> <span data-ttu-id="48f62-176">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="48f62-176">For example:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

<span data-ttu-id="48f62-177">そして *、/ディナー/編集/[id]URL*で:</span><span class="sxs-lookup"><span data-stu-id="48f62-177">And with the */Dinners/Edit/[id]* URL:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a><span data-ttu-id="48f62-178">次の手順</span><span class="sxs-lookup"><span data-stu-id="48f62-178">Next Step</span></span>

<span data-ttu-id="48f62-179">パーシャルページとマスターページには、ビューを整理するための非常に柔軟なオプションが用意されています。</span><span class="sxs-lookup"><span data-stu-id="48f62-179">Partials and master pages provide very flexible options that enable you to cleanly organize views.</span></span> <span data-ttu-id="48f62-180">ビューコンテンツやコードの重複を避け、ビューテンプレートを読みやすく管理しやすくすることができます。</span><span class="sxs-lookup"><span data-stu-id="48f62-180">You'll find that they help you avoid duplicating view content/ code, and make your view templates easier to read and maintain.</span></span>

<span data-ttu-id="48f62-181">ここで、先ほど作成したリストのシナリオを再検討し、スケーラブルなページングサポートを有効にしましょう。</span><span class="sxs-lookup"><span data-stu-id="48f62-181">Let's now revisit the listing scenario we built earlier and enable scalable paging support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="48f62-182">[前へ](use-viewdata-and-implement-viewmodel-classes.md)
> [次へ](implement-efficient-data-paging.md)</span><span class="sxs-lookup"><span data-stu-id="48f62-182">[Previous](use-viewdata-and-implement-viewmodel-classes.md)
[Next](implement-efficient-data-paging.md)</span></span>
