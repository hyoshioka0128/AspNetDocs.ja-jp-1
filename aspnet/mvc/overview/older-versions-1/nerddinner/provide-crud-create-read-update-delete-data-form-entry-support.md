---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: CRUD (作成、読み取り、更新、削除) データフォームエントリのサポートを提供 |マイクロソフトドキュメント
author: rick-anderson
description: 手順 5 では、Dinners クラスを編集、作成、およびディナーを削除するためのサポートを有効にして、DinnersController クラスをさらに進める方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 2b75a7eda8bce4baa25d92626639f4d904eb363a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542626"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a><span data-ttu-id="f4e79-103">CRUD (作成、読み取り、更新、削除) データ フォーム エントリ サポートを提供する</span><span class="sxs-lookup"><span data-stu-id="f4e79-103">Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support</span></span>

<span data-ttu-id="f4e79-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f4e79-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f4e79-105">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="f4e79-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="f4e79-106">これは、MVC 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NETの手順 5 です。</span><span class="sxs-lookup"><span data-stu-id="f4e79-106">This is step 5 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="f4e79-107">手順 5 では、Dinners クラスを編集、作成、およびディナーを削除するためのサポートを有効にして、DinnersController クラスをさらに進める方法を示します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-107">Step 5 shows how to take our DinnersController class further by enable support for editing, creating and deleting Dinners with it as well.</span></span>
> 
> <span data-ttu-id="f4e79-108">mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a><span data-ttu-id="f4e79-109">NerdDinner ステップ 5: フォームのシナリオを作成、更新、削除する</span><span class="sxs-lookup"><span data-stu-id="f4e79-109">NerdDinner Step 5: Create, Update, Delete Form Scenarios</span></span>

<span data-ttu-id="f4e79-110">コントローラーとビューを導入し、それらを使用して、Dinners のサイトでのリスト/詳細エクスペリエンスを実装する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="f4e79-110">We've introduced controllers and views, and covered how to use them to implement a listing/details experience for Dinners on site.</span></span> <span data-ttu-id="f4e79-111">次のステップは、DinnersController クラスをさらに進めて、Dinners の編集、作成、および削除のサポートも有効にすることです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-111">Our next step will be to take our DinnersController class further and enable support for editing, creating and deleting Dinners with it as well.</span></span>

### <a name="urls-handled-by-dinnerscontroller"></a><span data-ttu-id="f4e79-112">ディナーコントローラによって処理される URL</span><span class="sxs-lookup"><span data-stu-id="f4e79-112">URLs handled by DinnersController</span></span>

<span data-ttu-id="f4e79-113">以前は、2 つの URL のサポートを実装した DinnersController にアクション メソッドを追加しました: */Dinners*と */Dinners/詳細/[id]*。</span><span class="sxs-lookup"><span data-stu-id="f4e79-113">We previously added action methods to DinnersController that implemented support for two URLs: */Dinners* and */Dinners/Details/[id]*.</span></span>

| <span data-ttu-id="f4e79-114">**URL**</span><span class="sxs-lookup"><span data-stu-id="f4e79-114">**URL**</span></span> | <span data-ttu-id="f4e79-115">**動詞**</span><span class="sxs-lookup"><span data-stu-id="f4e79-115">**VERB**</span></span> | <span data-ttu-id="f4e79-116">**目的**</span><span class="sxs-lookup"><span data-stu-id="f4e79-116">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4e79-117">*/ディナー/*</span><span class="sxs-lookup"><span data-stu-id="f4e79-117">*/Dinners/*</span></span> | <span data-ttu-id="f4e79-118">GET</span><span class="sxs-lookup"><span data-stu-id="f4e79-118">GET</span></span> | <span data-ttu-id="f4e79-119">今後のディナーの HTML リストを表示します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-119">Display an HTML list of upcoming dinners.</span></span> |
| <span data-ttu-id="f4e79-120">*/ディナー/詳細/[id]*</span><span class="sxs-lookup"><span data-stu-id="f4e79-120">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="f4e79-121">GET</span><span class="sxs-lookup"><span data-stu-id="f4e79-121">GET</span></span> | <span data-ttu-id="f4e79-122">特定のディナーに関する詳細を表示します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-122">Display details about a specific dinner.</span></span> |

<span data-ttu-id="f4e79-123">次に、3 つの URL を実装するアクション メソッドを追加します: */Dinners/Edit/[id]* *、/ディナー/作成*、および */Dinners/Delete/[id]*。</span><span class="sxs-lookup"><span data-stu-id="f4e79-123">We will now add action methods to implement three additional URLs: */Dinners/Edit/[id]*, */Dinners/Create*, and */Dinners/Delete/[id]*.</span></span> <span data-ttu-id="f4e79-124">これらの URL により、既存のディナーの編集、新しいディナーの作成、ディナーの削除がサポートされます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-124">These URLs will enable support for editing existing Dinners, creating new Dinners, and deleting Dinners.</span></span>

<span data-ttu-id="f4e79-125">これらの新しい URL と HTTP GET と HTTP POST の両方の動詞の相互作用をサポートします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-125">We will support both HTTP GET and HTTP POST verb interactions with these new URLs.</span></span> <span data-ttu-id="f4e79-126">これらの URL に対する HTTP GET 要求は、データの最初の HTML ビュー ("編集" の場合は Dinner データが入力されたフォーム、「作成」の場合は空白のフォーム、削除の場合は削除確認画面) を表示します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-126">HTTP GET requests to these URLs will display the initial HTML view of the data (a form populated with the Dinner data in the case of "edit", a blank form in the case of "create", and a delete confirmation screen in the case of "delete").</span></span> <span data-ttu-id="f4e79-127">これらの URL に対する HTTP POST 要求は、Dinner リポジトリ (およびそこからデータベース) のディナー データを保存/更新/削除します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-127">HTTP POST requests to these URLs will save/update/delete the Dinner data in our DinnerRepository (and from there to the database).</span></span>

| <span data-ttu-id="f4e79-128">**URL**</span><span class="sxs-lookup"><span data-stu-id="f4e79-128">**URL**</span></span> | <span data-ttu-id="f4e79-129">**動詞**</span><span class="sxs-lookup"><span data-stu-id="f4e79-129">**VERB**</span></span> | <span data-ttu-id="f4e79-130">**目的**</span><span class="sxs-lookup"><span data-stu-id="f4e79-130">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4e79-131">*/ディナー/編集/[id]*</span><span class="sxs-lookup"><span data-stu-id="f4e79-131">*/Dinners/Edit/[id]*</span></span> | <span data-ttu-id="f4e79-132">GET</span><span class="sxs-lookup"><span data-stu-id="f4e79-132">GET</span></span> | <span data-ttu-id="f4e79-133">Dinner データが設定された編集可能な HTML フォームを表示します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-133">Display an editable HTML form populated with Dinner data.</span></span> |
| <span data-ttu-id="f4e79-134">POST</span><span class="sxs-lookup"><span data-stu-id="f4e79-134">POST</span></span> | <span data-ttu-id="f4e79-135">特定の Dinner のフォームの変更をデータベースに保存します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-135">Save the form changes for a particular Dinner to the database.</span></span> |
| <span data-ttu-id="f4e79-136">*/ディナー/作成*</span><span class="sxs-lookup"><span data-stu-id="f4e79-136">*/Dinners/Create*</span></span> | <span data-ttu-id="f4e79-137">GET</span><span class="sxs-lookup"><span data-stu-id="f4e79-137">GET</span></span> | <span data-ttu-id="f4e79-138">ユーザーが新しいディナーを定義できる空の HTML フォームを表示します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-138">Display an empty HTML form that allows users to define new Dinners.</span></span> |
| <span data-ttu-id="f4e79-139">POST</span><span class="sxs-lookup"><span data-stu-id="f4e79-139">POST</span></span> | <span data-ttu-id="f4e79-140">新しい Dinner を作成し、データベースに保存します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-140">Create a new Dinner and save it in the database.</span></span> |
| <span data-ttu-id="f4e79-141">*/ディナー/削除/[id]*</span><span class="sxs-lookup"><span data-stu-id="f4e79-141">*/Dinners/Delete/[id]*</span></span> | <span data-ttu-id="f4e79-142">GET</span><span class="sxs-lookup"><span data-stu-id="f4e79-142">GET</span></span> | <span data-ttu-id="f4e79-143">削除確認画面を表示します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-143">Display delete confirmation screen.</span></span> |
| <span data-ttu-id="f4e79-144">POST</span><span class="sxs-lookup"><span data-stu-id="f4e79-144">POST</span></span> | <span data-ttu-id="f4e79-145">指定されたディナーをデータベースから削除します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-145">Deletes the specified dinner from the database.</span></span> |

### <a name="edit-support"></a><span data-ttu-id="f4e79-146">サポートの編集</span><span class="sxs-lookup"><span data-stu-id="f4e79-146">Edit Support</span></span>

<span data-ttu-id="f4e79-147">まず、「編集」シナリオを実装します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-147">Let's begin by implementing the "edit" scenario.</span></span>

#### <a name="the-http-get-edit-action-method"></a><span data-ttu-id="f4e79-148">HTTP-GET 編集アクション メソッド</span><span class="sxs-lookup"><span data-stu-id="f4e79-148">The HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="f4e79-149">まず、編集アクションメソッドの HTTP "GET" 動作を実装します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-149">We'll start by implementing the HTTP "GET" behavior of our edit action method.</span></span> <span data-ttu-id="f4e79-150">このメソッドは *、/Dinners/Edit/[id]* URL が要求されたときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-150">This method will be invoked when the */Dinners/Edit/[id]* URL is requested.</span></span> <span data-ttu-id="f4e79-151">実装は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-151">Our implementation will look like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

<span data-ttu-id="f4e79-152">上記のコードでは、Dinner リポジトリを使用して Dinner オブジェクトを取得しています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-152">The code above uses the DinnerRepository to retrieve a Dinner object.</span></span> <span data-ttu-id="f4e79-153">次に、Dinner オブジェクトを使用してビュー テンプレートをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-153">It then renders a View template using the Dinner object.</span></span> <span data-ttu-id="f4e79-154">テンプレート名を*View()* ヘルパー メソッドに明示的に渡していないので、ビュー テンプレートを解決するために、規則ベースの既定のパスを使用します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-154">Because we haven't explicitly passed a template name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Edit.aspx.</span></span>

<span data-ttu-id="f4e79-155">次に、このビュー テンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-155">Let's now create this view template.</span></span> <span data-ttu-id="f4e79-156">これは、Edit メソッド内で右クリックし、コンテキスト メニューの [ビューの追加] をクリックして行います。</span><span class="sxs-lookup"><span data-stu-id="f4e79-156">We will do this by right-clicking within the Edit method and selecting the "Add View" context menu command:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

<span data-ttu-id="f4e79-157">[ビューの追加] ダイアログでは、Dinner オブジェクトをモデルとしてビュー テンプレートに渡すことを示し、"Edit" テンプレートを自動スキャフォールディングすることを選択します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-157">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to auto-scaffold an "Edit" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

<span data-ttu-id="f4e79-158">[追加] ボタンをクリックすると、Visual Studio は "\ビュー\Dinners" ディレクトリ内に新しい "Edit.aspx" ビュー テンプレート ファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-158">When we click the "Add" button, Visual Studio will add a new "Edit.aspx" view template file for us within the "\Views\Dinners" directory.</span></span> <span data-ttu-id="f4e79-159">また、コード エディター内の新しい "Edit.aspx" ビュー テンプレートが開きます 。</span><span class="sxs-lookup"><span data-stu-id="f4e79-159">It will also open up the new "Edit.aspx" view template within the code-editor – populated with an initial "Edit" scaffold implementation like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

<span data-ttu-id="f4e79-160">生成されるデフォルトの「編集」スキャフォールドに対していくつかの変更を加え、編集ビューテンプレートを更新して以下の内容を含めます (これは、公開したくないプロパティの一部を削除します)。</span><span class="sxs-lookup"><span data-stu-id="f4e79-160">Let's make a few changes to the default "edit" scaffold generated, and update the edit view template to have the content below (which removes a few of the properties we don't want to expose):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

<span data-ttu-id="f4e79-161">アプリケーションを実行して *"/ディナー/編集/1"URL*をリクエストすると、次のページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-161">When we run the application and request the *"/Dinners/Edit/1"* URL we will see the following page:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

<span data-ttu-id="f4e79-162">ビューで生成される HTML マークアップは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-162">The HTML markup generated by our view looks like below.</span></span> <span data-ttu-id="f4e79-163">標準の HTML- "&lt;保存&gt;"&lt;入力タイプ ="submit"/&gt;ボタンが押されたときに *、/Dinners/Edit/1* URL に HTTP POST を実行するフォーム要素を使用します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-163">It is standard HTML – with a &lt;form&gt; element that performs an HTTP POST to the */Dinners/Edit/1* URL when the "Save" &lt;input type="submit"/&gt; button is pushed.</span></span> <span data-ttu-id="f4e79-164">HTML&lt;入力タイプ="text"/&gt;要素は、編集可能な各プロパティに対して出力されています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-164">A HTML &lt;input type="text"/&gt; element has been output for each editable property:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a><span data-ttu-id="f4e79-165">Html.BeginForm() および Html.TextBox() Html ヘルパー メソッド</span><span class="sxs-lookup"><span data-stu-id="f4e79-165">Html.BeginForm() and Html.TextBox() Html Helper Methods</span></span>

<span data-ttu-id="f4e79-166">"Edit.aspx" ビュー テンプレートは、いくつかの "Html ヘルパー" メソッドを使用しています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-166">Our "Edit.aspx" view template is using several "Html Helper" methods: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), and Html.ValidationMessage().</span></span> <span data-ttu-id="f4e79-167">これらのヘルパー メソッドは、HTML マークアップを生成するだけでなく、組み込みのエラー処理と検証のサポートも提供します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-167">In addition to generating HTML markup for us, these helper methods provide built-in error handling and validation support.</span></span>

##### <a name="htmlbeginform-helper-method"></a><span data-ttu-id="f4e79-168">ヘルパー メソッド</span><span class="sxs-lookup"><span data-stu-id="f4e79-168">Html.BeginForm() helper method</span></span>

<span data-ttu-id="f4e79-169">Html.BeginForm() ヘルパー メソッドは、マークアップで&lt;&gt; HTML フォーム要素を出力するものです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-169">The Html.BeginForm() helper method is what output the HTML &lt;form&gt; element in our markup.</span></span> <span data-ttu-id="f4e79-170">Edit.aspx ビュー テンプレートでは、このメソッドを使用するときに C# の using ステートメントを適用していることに気付くでしょう。</span><span class="sxs-lookup"><span data-stu-id="f4e79-170">In our Edit.aspx view template you'll notice that we are applying a C# "using" statement when using this method.</span></span> <span data-ttu-id="f4e79-171">&lt;左中かっこはフォーム&gt;のコンテンツの先頭を示し、右中かっこは&lt;/form&gt;要素の終わりを示します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-171">The open curly brace indicates the beginning of the &lt;form&gt; content, and the closing curly brace is what indicates the end of the &lt;/form&gt; element:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

<span data-ttu-id="f4e79-172">または、このようなシナリオで「using」ステートメントのアプローチが不自然である場合は、Html.BeginForm() と Html.EndForm() の組み合わせを使用できます (これは同じことを行います)。</span><span class="sxs-lookup"><span data-stu-id="f4e79-172">Alternatively, if you find the "using" statement approach unnatural for a scenario like this, you can use a Html.BeginForm() and Html.EndForm() combination (which does the same thing):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

<span data-ttu-id="f4e79-173">パラメータを指定せずに Html.BeginForm() を呼び出すと、現在の要求の URL に HTTP-POST を実行するフォーム要素が出力されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-173">Calling Html.BeginForm() without any parameters will cause it to output a form element that does an HTTP-POST to the current request's URL.</span></span> <span data-ttu-id="f4e79-174">そのため、編集ビューでは*&lt;フォーム アクション=""ディナー/編集/1" メソッド ="post" 要素&gt;が*生成されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-174">That is why our Edit view generates a *&lt;form action="/Dinners/Edit/1" method="post"&gt;* element.</span></span> <span data-ttu-id="f4e79-175">別の URL に投稿する場合は、Html.BeginForm() に明示的なパラメータを渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-175">We could have alternatively passed explicit parameters to Html.BeginForm() if we wanted to post to a different URL.</span></span>

##### <a name="htmltextbox-helper-method"></a><span data-ttu-id="f4e79-176">ヘルパー メソッド</span><span class="sxs-lookup"><span data-stu-id="f4e79-176">Html.TextBox() helper method</span></span>

<span data-ttu-id="f4e79-177">Edit.aspx ビューでは、Html.TextBox() ヘルパー メソッド&lt;を使用して入力タイプ="text"/&gt;要素を出力します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-177">Our Edit.aspx view uses the Html.TextBox() helper method to output &lt;input type="text"/&gt; elements:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

<span data-ttu-id="f4e79-178">上記の Html.TextBox() メソッドは&lt;、1 つのパラメータを受け取り、出力する入力タイプ="text"/&gt;要素の id/name 属性と、テキストボックス値を設定するモデル プロパティの両方を指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-178">The Html.TextBox() method above takes a single parameter – which is being used to specify both the id/name attributes of the &lt;input type="text"/&gt; element to output, as well as the model property to populate the textbox value from.</span></span> <span data-ttu-id="f4e79-179">たとえば、編集ビューに渡した Dinner オブジェクトには ".NET Futures" という "Title" プロパティ値が含まれるため、Html.TextBox("title") メソッド呼び出し出力:*&lt;入力 id="title" name="title" タイプ&gt;="text" 値 ="NET Futures" /*.</span><span class="sxs-lookup"><span data-stu-id="f4e79-179">For example, the Dinner object we passed to the Edit view had a "Title" property value of ".NET Futures", and so our Html.TextBox("Title") method call output: *&lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.</span></span>

<span data-ttu-id="f4e79-180">または、最初の Html.TextBox() パラメータを使用して要素の id/name を指定し、2 番目のパラメータとして使用する値を明示的に渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-180">Alternatively, we can use the first Html.TextBox() parameter to specify the id/name of the element, and then explicitly pass in the value to use as a second parameter:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

<span data-ttu-id="f4e79-181">出力される値に対してカスタム書式を実行する場合も多くあります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-181">Often we'll want to perform custom formatting on the value that is output.</span></span> <span data-ttu-id="f4e79-182">Net に組み込まれた String.Format() 静的メソッドは、これらのシナリオに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-182">The String.Format() static method built-into .NET is useful for these scenarios.</span></span> <span data-ttu-id="f4e79-183">Edit.aspx ビュー テンプレートは、この値を使用して、日時の秒数が表示されないように EventDate 値 (DateTime 型) を書式設定しています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-183">Our Edit.aspx view template is using this to format the EventDate value (which is of type DateTime) so that it doesn't show seconds for the time:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

<span data-ttu-id="f4e79-184">Html.TextBox() の 3 番目のパラメータは、オプションで追加の HTML 属性を出力するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-184">A third parameter to Html.TextBox() can optionally be used to output additional HTML attributes.</span></span> <span data-ttu-id="f4e79-185">以下のコード スニペットは、追加の size="30" 属性と、入力型="text"/&lt;&gt;要素に対する class="mycssclass" 属性をレンダリングする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-185">The code-snippet below demonstrates how to render an additional size="30" attribute and a class="mycssclass" attribute on the &lt;input type="text"/&gt; element.</span></span> <span data-ttu-id="f4e79-186">クラス属性の名前をエスケープする方法に注意してください" クラス@" character because "" は C# の予約キーワードです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-186">Note how we are escaping the name of the class attribute using a "@" character because "class" is a reserved keyword in C#:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a><span data-ttu-id="f4e79-187">HTTP-POST 編集アクション メソッドの実装</span><span class="sxs-lookup"><span data-stu-id="f4e79-187">Implementing the HTTP-POST Edit Action Method</span></span>

<span data-ttu-id="f4e79-188">これで、EDIT アクション メソッドの HTTP-GET バージョンが実装されました。</span><span class="sxs-lookup"><span data-stu-id="f4e79-188">We now have the HTTP-GET version of our Edit action method implemented.</span></span> <span data-ttu-id="f4e79-189">ユーザーが */Dinners/Edit/1* URL を要求すると、次のような HTML ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-189">When a user requests the */Dinners/Edit/1* URL they receive an HTML page like the following:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

<span data-ttu-id="f4e79-190">"Save" ボタンを押すと、フォームが */Dinners/Edit/1* URL にポストされ、HTTP POST 動詞を使用して HTML&lt;入力&gt;フォームの値が送信されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-190">Pressing the "Save" button causes a form post to the */Dinners/Edit/1* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span> <span data-ttu-id="f4e79-191">それでは、Dinnerの保存を処理する編集アクションメソッドのHTTP POST動作を実装しましょう。</span><span class="sxs-lookup"><span data-stu-id="f4e79-191">Let's now implement the HTTP POST behavior of our edit action method – which will handle saving the Dinner.</span></span>

<span data-ttu-id="f4e79-192">まず、HTTP POST シナリオを処理することを示す "AcceptVerbs" 属性を持つ DinnersController に、オーバーロードされた "Edit" アクション メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-192">We'll begin by adding an overloaded "Edit" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

<span data-ttu-id="f4e79-193">オーバーロードされたアクション メソッドに [AcceptVerbs] 属性が適用されると、ASP.NET MVC は、着信 HTTP 動詞に応じて、適切なアクション メソッドへのディスパッチ要求を自動的に処理します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-193">When the [AcceptVerbs] attribute is applied to overloaded action methods, ASP.NET MVC automatically handles dispatching requests to the appropriate action method depending on the incoming HTTP verb.</span></span> <span data-ttu-id="f4e79-194">*/Dinners/Edit/[id]* URL への HTTP POST 要求は上記の Edit メソッドに送信され *、/Dinners/Edit/[id]* URL への他のすべての HTTP 動詞要求は、実装した最初の`[AcceptVerbs]`Edit メソッド (属性を持たない) に移動します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-194">HTTP POST requests to */Dinners/Edit/[id]* URLs will go to the above Edit method, while all other HTTP verb requests to */Dinners/Edit/[id]* URLs will go to the first Edit method we implemented (which did not have an `[AcceptVerbs]` attribute).</span></span>

| <span data-ttu-id="f4e79-195">**サイドトピック: なぜ HTTP 動詞を介して差別化するのですか?**</span><span class="sxs-lookup"><span data-stu-id="f4e79-195">**Side Topic: Why differentiate via HTTP verbs?**</span></span> |
| --- |
| <span data-ttu-id="f4e79-196">あなたは尋ねるかもしれません - なぜ私たちは単一のURLを使用し、HTTP動詞を介してその動作を区別するのですか?</span><span class="sxs-lookup"><span data-stu-id="f4e79-196">You might ask – why are we using a single URL and differentiating its behavior via the HTTP verb?</span></span> <span data-ttu-id="f4e79-197">編集変更の読み込みと保存を処理する URL を 2 つ別に持つのはなぜですか?</span><span class="sxs-lookup"><span data-stu-id="f4e79-197">Why not just have two separate URLs to handle loading and saving edit changes?</span></span> <span data-ttu-id="f4e79-198">たとえば、/Dinners/Edit/[id]は最初のフォームを表示し、/Dinners/Save/[id]はフォームポストを処理して保存しますか?</span><span class="sxs-lookup"><span data-stu-id="f4e79-198">For example: /Dinners/Edit/[id] to display the initial form and /Dinners/Save/[id] to handle the form post to save it?</span></span> <span data-ttu-id="f4e79-199">2 つの別々の URL を公開する場合の欠点は、/Dinners/Save/2 に投稿し、入力エラーのために HTML フォームを再表示する必要がある場合、エンド ユーザーはブラウザーのアドレス バーに /Dinners/Save/2 URL を持つことになります (フォームが投稿された URL であるため)。</span><span class="sxs-lookup"><span data-stu-id="f4e79-199">The downside with publishing two separate URLs is that in cases where we post to /Dinners/Save/2, and then need to redisplay the HTML form because of an input error, the end-user will end up having the /Dinners/Save/2 URL in their browser's address bar (since that was the URL the form posted to).</span></span> <span data-ttu-id="f4e79-200">エンドユーザーがこの再表示されたページをブラウザのお気に入りリストにブックマークしたり、URL をコピー/ペーストして友人にメールした場合、今後は動作しない URL を保存することになります (その URL は投稿値に依存するため)。</span><span class="sxs-lookup"><span data-stu-id="f4e79-200">If the end-user bookmarks this redisplayed page to their browser favorites list, or copy/pastes the URL and emails it to a friend, they will end up saving a URL that won't work in the future (since that URL depends on post values).</span></span> <span data-ttu-id="f4e79-201">単一の URL (/Dinners/Edit/[id]など) を公開し、HTTP 動詞で処理を区別することで、エンドユーザーが編集ページをブックマークしたり、URL を他のユーザーに送信したりしても安全です。</span><span class="sxs-lookup"><span data-stu-id="f4e79-201">By exposing a single URL (like: /Dinners/Edit/[id]) and differentiating the processing of it by HTTP verb, it is safe for end-users to bookmark the edit page and/or send the URL to others.</span></span> |

#### <a name="retrieving-form-post-values"></a><span data-ttu-id="f4e79-202">フォームポスト値の取得</span><span class="sxs-lookup"><span data-stu-id="f4e79-202">Retrieving Form Post Values</span></span>

<span data-ttu-id="f4e79-203">HTTP POST "Edit" メソッド内で、投稿されたフォームパラメータにアクセスする方法はさまざまです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-203">There are a variety of ways we can access posted form parameters within our HTTP POST "Edit" method.</span></span> <span data-ttu-id="f4e79-204">簡単な方法の 1 つは、Controller 基本クラスの Request プロパティを使用してフォーム コレクションにアクセスし、ポストされた値を直接取得することです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-204">One simple approach is to just use the Request property on the Controller base class to access the form collection and retrieve the posted values directly:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

<span data-ttu-id="f4e79-205">ただし、上記のアプローチは、特にエラー処理ロジックを追加すると、少し冗長です。</span><span class="sxs-lookup"><span data-stu-id="f4e79-205">The above approach is a little verbose, though, especially once we add error handling logic.</span></span>

<span data-ttu-id="f4e79-206">このシナリオの優れたアプローチは、コント ローラーの基本クラスに組み込みの*UpdateModel()* ヘルパー メソッドを活用することです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-206">A better approach for this scenario is to leverage the built-in *UpdateModel()* helper method on the Controller base class.</span></span> <span data-ttu-id="f4e79-207">これは、受信フォームのパラメータを使用して渡すオブジェクトのプロパティの更新をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-207">It supports updating the properties of an object we pass it using the incoming form parameters.</span></span> <span data-ttu-id="f4e79-208">リフレクションを使用してオブジェクトのプロパティ名を決定し、クライアントから送信された入力値に基づいて値を自動的に変換して値を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-208">It uses reflection to determine the property names on the object, and then automatically converts and assigns values to them based on the input values submitted by the client.</span></span>

<span data-ttu-id="f4e79-209">このコードを使用して HTTP-POST 編集アクションを簡略化するために UpdateModel() メソッドを使用できます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-209">We could use the UpdateModel() method to simplify our HTTP-POST Edit Action using this code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

<span data-ttu-id="f4e79-210">今、私たちは *、/ディナー/編集/1* URLを訪問し、私たちの夕食のタイトルを変更することができます:</span><span class="sxs-lookup"><span data-stu-id="f4e79-210">We can now visit the */Dinners/Edit/1* URL, and change the title of our Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

<span data-ttu-id="f4e79-211">[保存] ボタンをクリックすると、編集アクションにフォームポストが実行され、更新された値がデータベースに保存されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-211">When we click the "Save" button, we'll perform a form post to our Edit action, and the updated values will be persisted in the database.</span></span> <span data-ttu-id="f4e79-212">その後、夕食の詳細 URL にリダイレクトされます (新しく保存された値が表示されます)。</span><span class="sxs-lookup"><span data-stu-id="f4e79-212">We will then be redirected to the Details URL for the Dinner (which will display the newly saved values):</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a><span data-ttu-id="f4e79-213">編集エラーの処理</span><span class="sxs-lookup"><span data-stu-id="f4e79-213">Handling Edit Errors</span></span>

<span data-ttu-id="f4e79-214">現在の HTTP-POST 実装は、エラーがある場合を除いて正常に動作します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-214">Our current HTTP-POST implementation works fine – except when there are errors.</span></span>

<span data-ttu-id="f4e79-215">ユーザーがフォームの編集を間違えた場合は、フォームを修正するための情報を示すエラー メッセージがフォームに再表示されることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-215">When a user makes a mistake editing a form, we need to make sure that the form is redisplayed with an informative error message that guides them to fix it.</span></span> <span data-ttu-id="f4e79-216">これには、エンドユーザーが不正な入力 (例: 不正な形式の日付文字列) を投稿するケースや、入力形式が有効であるがビジネス ルール違反がある場合が含まれます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-216">This includes cases where an end-user posts incorrect input (for example: a malformed date string), as well as cases where the input format is valid but there is a business rule violation.</span></span> <span data-ttu-id="f4e79-217">エラーが発生した場合、ユーザーが最初に入力した入力データをフォームに保存して、変更を手動で再入力する必要がないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-217">When errors occur the form should preserve the input data the user originally entered so that they don't have to refill their changes manually.</span></span> <span data-ttu-id="f4e79-218">このプロセスは、フォームが正常に完了するまで、必要に応じて何度も繰り返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-218">This process should repeat as many times as necessary until the form successfully completes.</span></span>

<span data-ttu-id="f4e79-219">ASP.NETMVCには、エラー処理とフォームの再表示を容易にする優れた組み込み機能がいくつか含まれています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-219">ASP.NET MVC includes some nice built-in features that make error handling and form redisplay easy.</span></span> <span data-ttu-id="f4e79-220">これらの機能を実際に表示するには、次のコードを使用して Edit アクション メソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-220">To see these features in action let's update our Edit action method with the following code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

<span data-ttu-id="f4e79-221">上記のコードは、以前の実装と似ていますが、現在は try/catch エラー処理ブロックをラップしています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-221">The above code is similar to our previous implementation – except that we are now wrapping a try/catch error handling block around our work.</span></span> <span data-ttu-id="f4e79-222">UpdateModel() を呼び出すときに例外が発生した場合、または DinnerRepository を保存しようとすると (この場合、保存しようとしている Dinner オブジェクトがモデル内のルール違反により無効な場合は例外が発生します)、キャッチ エラー処理ブロックが実行されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-222">If an exception occurs either when calling UpdateModel(), or when we try and save the DinnerRepository (which will raise an exception if the Dinner object we are trying to save is invalid because of a rule violation within our model), our catch error handling block will execute.</span></span> <span data-ttu-id="f4e79-223">その中で、Dinner オブジェクトに存在するルール違反をループし、ModelState オブジェクトに追加します (これについては後で説明します)。</span><span class="sxs-lookup"><span data-stu-id="f4e79-223">Within it we loop over any rule violations that exist in the Dinner object and add them to a ModelState object (which we'll discuss shortly).</span></span> <span data-ttu-id="f4e79-224">その後、ビューを再表示します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-224">We then redisplay the view.</span></span>

<span data-ttu-id="f4e79-225">この作業を見て、アプリケーションを再実行し、Dinnerを編集し、空のタイトル、"BOGUS"のEventDateを持つ、米国の国の値を持つ英国の電話番号を使用するように変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="f4e79-225">To see this working let's re-run the application, edit a Dinner, and change it to have an empty Title, an EventDate of "BOGUS", and use a UK phone number with a country value of USA.</span></span> <span data-ttu-id="f4e79-226">"Save" ボタンを押すと、HTTP POST Edit メソッドは(エラーがあるため)Dinner を保存できないため、フォームを再表示します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-226">When we press the "Save" button our HTTP POST Edit method will not be able to save the Dinner (because there are errors) and will redisplay the form:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

<span data-ttu-id="f4e79-227">私たちのアプリケーションは、まともなエラー経験を持っています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-227">Our application has a decent error experience.</span></span> <span data-ttu-id="f4e79-228">無効な入力を含むテキスト要素は赤色で強調表示され、検証エラー メッセージがエンド ユーザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-228">The text elements with the invalid input are highlighted in red, and validation error messages are displayed to the end user about them.</span></span> <span data-ttu-id="f4e79-229">フォームは、ユーザーが最初に入力した入力データを保持しているため、何も補充する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f4e79-229">The form is also preserving the input data the user originally entered – so that they don't have to refill anything.</span></span>

<span data-ttu-id="f4e79-230">どのように、あなたは尋ねるかもしれない、これは起こったのですか?</span><span class="sxs-lookup"><span data-stu-id="f4e79-230">How, you might ask, did this occur?</span></span> <span data-ttu-id="f4e79-231">タイトル、EventDate、および ContactPhone のテキストボックスは、どのようにして赤でハイライトされ、最初に入力されたユーザー値を出力する方法を知っていますか?</span><span class="sxs-lookup"><span data-stu-id="f4e79-231">How did the Title, EventDate, and ContactPhone textboxes highlight themselves in red and know to output the originally entered user values?</span></span> <span data-ttu-id="f4e79-232">そして、エラーメッセージは、一番上のリストにどのように表示されますか?</span><span class="sxs-lookup"><span data-stu-id="f4e79-232">And how did error messages get displayed in the list at the top?</span></span> <span data-ttu-id="f4e79-233">良いニュースは、これは魔法によって起こらなかったということです - むしろ、入力検証とエラー処理シナリオを容易にする組み込みのASP.NETMVC機能のいくつかを使用したためです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-233">The good news is that this didn't occur by magic - rather it was because we used some of the built-in ASP.NET MVC features that make input validation and error handling scenarios easy.</span></span>

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a><span data-ttu-id="f4e79-234">モデル状態と検証 HTML ヘルパー メソッドについて</span><span class="sxs-lookup"><span data-stu-id="f4e79-234">Understanding ModelState and the Validation HTML Helper Methods</span></span>

<span data-ttu-id="f4e79-235">コント ローラー クラスには、ビューに渡されるモデル オブジェクトにエラーが存在することを示す方法を提供する"ModelState" プロパティ コレクションがあります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-235">Controller classes have a "ModelState" property collection which provides a way to indicate that errors exist with a model object being passed to a View.</span></span> <span data-ttu-id="f4e79-236">ModelState コレクション内のエラー エントリは、問題があるモデル プロパティの名前 ("Title"、"EventDate"、"ContactPhone"など) を識別し、人間にわかりやすいエラー メッセージを指定できるようにします (たとえば、「タイトルが必要です」)。</span><span class="sxs-lookup"><span data-stu-id="f4e79-236">Error entries within the ModelState collection identify the name of the model property with the issue (for example: "Title", "EventDate", or "ContactPhone"), and allow a human-friendly error message to be specified (for example: "Title is required").</span></span>

<span data-ttu-id="f4e79-237">モデル オブジェクトのプロパティにフォーム値を割り当てようとしたときに、エラーが発生すると *、UpdateModel()* ヘルパー メソッドによって ModelState コレクションが自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-237">The *UpdateModel()* helper method automatically populates the ModelState collection when it encounters errors while trying to assign form values to properties on the model object.</span></span> <span data-ttu-id="f4e79-238">たとえば、Dinner オブジェクトの EventDate プロパティの型は、DateTime です。</span><span class="sxs-lookup"><span data-stu-id="f4e79-238">For example, our Dinner object's EventDate property is of type DateTime.</span></span> <span data-ttu-id="f4e79-239">上記のシナリオで UpdateModel() メソッドが文字列値 "BOGUS" を割り当てることができなかった場合、UpdateModel() メソッドは、そのプロパティで割り当てエラーが発生したことを示すエントリを ModelState コレクションに追加しました。</span><span class="sxs-lookup"><span data-stu-id="f4e79-239">When the UpdateModel() method was unable to assign the string value "BOGUS" to it in the scenario above, the UpdateModel() method added an entry to the ModelState collection indicating an assignment error had occurred with that property.</span></span>

<span data-ttu-id="f4e79-240">開発者は、Dinner オブジェクトのアクティブなルール違反に基づくエントリを ModelState コレクションに設定する"catch" エラー処理ブロック内で以下のように、ModelState コレクションに明示的にエラー エントリを追加するコードを記述することもできます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-240">Developers can also write code to explicitly add error entries into the ModelState collection like we are doing below within our "catch" error handling block, which is populating the ModelState collection with entries based on the active Rule Violations in the Dinner object:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a><span data-ttu-id="f4e79-241">モデル状態との Html ヘルパー統合</span><span class="sxs-lookup"><span data-stu-id="f4e79-241">Html Helper Integration with ModelState</span></span>

<span data-ttu-id="f4e79-242">HTML ヘルパー メソッド ( Html.TextBox() など ) は、出力をレンダリングするときに ModelState コレクションをチェックします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-242">HTML helper methods - like Html.TextBox() - check the ModelState collection when rendering output.</span></span> <span data-ttu-id="f4e79-243">アイテムにエラーが存在する場合、ユーザーが入力した値と CSS エラー クラスがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-243">If an error for the item exists, they render the user-entered value and a CSS error class.</span></span>

<span data-ttu-id="f4e79-244">たとえば、"編集" ビューでは、Html.TextBox() ヘルパー メソッドを使用して、Dinner オブジェクトの EventDate をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-244">For example, in our "Edit" view we are using the Html.TextBox() helper method to render the EventDate of our Dinner object:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

<span data-ttu-id="f4e79-245">ビューがエラー シナリオでレンダリングされると、Html.TextBox() メソッドは、Dinner オブジェクトの "EventDate" プロパティに関連付けられたエラーがあるかどうかを確認するために ModelState コレクションをチェックしました。</span><span class="sxs-lookup"><span data-stu-id="f4e79-245">When the view was rendered in the error scenario, the Html.TextBox() method checked the ModelState collection to see if there were any errors associated with the "EventDate" property of our Dinner object.</span></span> <span data-ttu-id="f4e79-246">エラーがあると判断すると、送信されたユーザー入力(「BOGUS」)が値としてレンダリングされ&lt;、cssエラークラスが入力タイプ="textbox"/&gt;マークアップに追加されました。</span><span class="sxs-lookup"><span data-stu-id="f4e79-246">When it determined that there was an error it rendered the submitted user input ("BOGUS") as the value, and added a css error class to the &lt;input type="textbox"/&gt; markup it generated:</span></span>

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

<span data-ttu-id="f4e79-247">css エラークラスの外観をカスタマイズして、希望する外観にすることができます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-247">You can customize the appearance of the css error class to look however you want.</span></span> <span data-ttu-id="f4e79-248">既定の CSS エラー クラスである "入力検証エラー" は *、\content\site.css*スタイルシートで定義されており、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-248">The default CSS error class – "input-validation-error" – is defined in the *\content\site.css* stylesheet and looks like below:</span></span>

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

<span data-ttu-id="f4e79-249">この CSS ルールは、無効な入力要素が次のように強調表示される原因となります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-249">This CSS rule is what caused our invalid input elements to be highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a><span data-ttu-id="f4e79-250">ヘルパー メソッド</span><span class="sxs-lookup"><span data-stu-id="f4e79-250">Html.ValidationMessage() Helper Method</span></span>

<span data-ttu-id="f4e79-251">ヘルパー メソッド Html.ValidationMessage() を使用して、特定のモデル プロパティに関連付けられた ModelState エラー メッセージを出力できます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-251">The Html.ValidationMessage() helper method can be used to output the ModelState error message associated with a particular model property:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

<span data-ttu-id="f4e79-252">上記のコード出力: \* &lt;span クラス ="フィールド検証エラー"&gt;値 'BOGUS'&lt;は無効です /span&gt;\*</span><span class="sxs-lookup"><span data-stu-id="f4e79-252">The above code outputs: *&lt;span class="field-validation-error"&gt; The value ‘BOGUS' is invalid&lt;/span&gt;*</span></span>

<span data-ttu-id="f4e79-253">Html.ValidationMessage() ヘルパー メソッドは、開発者が表示されるエラー テキスト メッセージをオーバーライドできるようにする 2 番目のパラメーターもサポートしています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-253">The Html.ValidationMessage() helper method also supports a second parameter that allows developers to override the error text message that is displayed:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

<span data-ttu-id="f4e79-254">上記のコード出力: EventDate プロパティにエラーが存在する場合、既定のエラー テキストの代わりに*&lt;span class="フィールド検証エラー"&gt;\*&lt;/span&gt;* です。</span><span class="sxs-lookup"><span data-stu-id="f4e79-254">The above code outputs: *&lt;span class="field-validation-error"&gt;\*&lt;/span&gt;* instead of the default error text when an error is present for the EventDate property.</span></span>

##### <a name="htmlvalidationsummary-helper-method"></a><span data-ttu-id="f4e79-255">ヘルパー メソッド</span><span class="sxs-lookup"><span data-stu-id="f4e79-255">Html.ValidationSummary() Helper Method</span></span>

<span data-ttu-id="f4e79-256">Html.ValidationSummary() ヘルパー メソッドを使用すると、概要エラー メッセージを表示し、ModelState&gt;&lt;コレクション内&gt;のすべての詳細なエラー メッセージの一覧を&lt;ul&gt;&lt;li//ul に表示できます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-256">The Html.ValidationSummary() helper method can be used to render a summary error message, accompanied by a &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; list of all detailed error messages in the ModelState collection:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

<span data-ttu-id="f4e79-257">Html.ValidationSummary() ヘルパー メソッドは、詳細なエラーの一覧の上に表示する概要エラー メッセージを定義する、省略可能な文字列パラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-257">The Html.ValidationSummary() helper method takes an optional string parameter – which defines a summary error message to display above the list of detailed errors:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

<span data-ttu-id="f4e79-258">オプションで CSS を使用して、エラーリストの表示をオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-258">You can optionally use CSS to override what the error list looks like.</span></span>

#### <a name="using-a-addruleviolations-helper-method"></a><span data-ttu-id="f4e79-259">ヘルパー メソッドの使用</span><span class="sxs-lookup"><span data-stu-id="f4e79-259">Using a AddRuleViolations Helper Method</span></span>

<span data-ttu-id="f4e79-260">最初の HTTP-POST Edit 実装では、catch ブロック内で foreach ステートメントを使用して、Dinner オブジェクトのルール違反をループし、コントローラの ModelState コレクションに追加しました。</span><span class="sxs-lookup"><span data-stu-id="f4e79-260">Our initial HTTP-POST Edit implementation used a foreach statement within its catch block to loop over the Dinner object's Rule Violations and add them to the controller's ModelState collection:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

<span data-ttu-id="f4e79-261">このコードを少し簡潔にするため、NerdDinner プロジェクトに "ControllerHelpers" クラスを追加し、mvc ModelStateDictionary クラス ASP.NETにヘルパー メソッドを追加する "AddRule違反" 拡張メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-261">We can make this code a little cleaner by adding a "ControllerHelpers" class to the NerdDinner project, and implement an "AddRuleViolations" extension method within it that adds a helper method to the ASP.NET MVC ModelStateDictionary class.</span></span> <span data-ttu-id="f4e79-262">この拡張メソッドは、ルール違反エラーの一覧を使用して ModelState ディクショナリを設定するために必要なロジックをカプセル化できます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-262">This extension method can encapsulate the logic necessary to populate the ModelStateDictionary with a list of RuleViolation errors:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

<span data-ttu-id="f4e79-263">その後、HTTP-POST Edit アクション メソッドを更新して、この拡張メソッドを使用して、ModelState コレクションにディナー ルール違反を設定できます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-263">We can then update our HTTP-POST Edit action method to use this extension method to populate the ModelState collection with our Dinner Rule Violations.</span></span>

#### <a name="complete-edit-action-method-implementations"></a><span data-ttu-id="f4e79-264">編集アクションメソッドの実装の完了</span><span class="sxs-lookup"><span data-stu-id="f4e79-264">Complete Edit Action Method Implementations</span></span>

<span data-ttu-id="f4e79-265">以下のコードは、編集シナリオに必要なすべてのコントローラー ロジックを実装します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-265">The code below implements all of the controller logic necessary for our Edit scenario:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

<span data-ttu-id="f4e79-266">Edit の実装の良いところは、Controller クラスも View テンプレートも、Dinner モデルによって適用される特定の検証やビジネス ルールについて何も知っている必要がないことです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-266">The nice thing about our Edit implementation is that neither our Controller class nor our View template has to know anything about the specific validation or business rules being enforced by our Dinner model.</span></span> <span data-ttu-id="f4e79-267">将来的にはモデルにルールを追加することができ、それらをサポートするためにコントローラやビューにコード変更を加える必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f4e79-267">We can add additional rules to our model in the future and do not have to make any code changes to our controller or view in order for them to be supported.</span></span> <span data-ttu-id="f4e79-268">これにより、将来のアプリケーション要件を最小限のコード変更で容易に進化させる柔軟性が得られます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-268">This provides us with the flexibility to easily evolve our application requirements in the future with a minimum of code changes.</span></span>

### <a name="create-support"></a><span data-ttu-id="f4e79-269">サポートの作成</span><span class="sxs-lookup"><span data-stu-id="f4e79-269">Create Support</span></span>

<span data-ttu-id="f4e79-270">DinnersController クラスの "編集" 動作の実装が完了しました。</span><span class="sxs-lookup"><span data-stu-id="f4e79-270">We've finished implementing the "Edit" behavior of our DinnersController class.</span></span> <span data-ttu-id="f4e79-271">次に、ユーザーが新しい Dinners を追加できるようにする"Create"サポートを実装します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-271">Let's now move on to implement the "Create" support on it – which will enable users to add new Dinners.</span></span>

#### <a name="the-http-get-create-action-method"></a><span data-ttu-id="f4e79-272">HTTP-GET 作成アクション メソッド</span><span class="sxs-lookup"><span data-stu-id="f4e79-272">The HTTP-GET Create Action Method</span></span>

<span data-ttu-id="f4e79-273">まず、作成アクション メソッドの HTTP "GET" 動作を実装します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-273">We'll begin by implementing the HTTP "GET" behavior of our create action method.</span></span> <span data-ttu-id="f4e79-274">このメソッドは、他のユーザーが */Dinners/CREATE* URL にアクセスしたときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-274">This method will be called when someone visits the */Dinners/Create* URL.</span></span> <span data-ttu-id="f4e79-275">実装は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-275">Our implementation looks like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

<span data-ttu-id="f4e79-276">上記のコードは、新しい Dinner オブジェクトを作成し、その EventDate プロパティを 1 週間後に割り当てます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-276">The code above creates a new Dinner object, and assigns its EventDate property to be one week in the future.</span></span> <span data-ttu-id="f4e79-277">次に、新しい Dinner オブジェクトに基づくビューをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-277">It then renders a View that is based on the new Dinner object.</span></span> <span data-ttu-id="f4e79-278">*View()* ヘルパー メソッドに名前を明示的に渡していないので、ビュー テンプレートを解決するために、規則ベースの既定のパスを使用します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-278">Because we haven't explicitly passed a name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Create.aspx.</span></span>

<span data-ttu-id="f4e79-279">次に、このビュー テンプレートを作成します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-279">Let's now create this view template.</span></span> <span data-ttu-id="f4e79-280">これは、Create アクションメソッド内で右クリックし、「ビューの追加」コンテキストメニューコマンドを選択することで行うことができます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-280">We can do this by right-clicking within the Create action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="f4e79-281">[ビューの追加] ダイアログでは、Dinner オブジェクトをビュー テンプレートに渡すことを示し、"Create" テンプレートを自動スキャフォールディングすることを選択します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-281">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to the view template, and choose to auto-scaffold a "Create" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

<span data-ttu-id="f4e79-282">[追加] ボタンをクリックすると、新しいスキャフォールド ベースの "Create.aspx" ビューが "\Views\Dinners" ディレクトリに保存され、IDE 内で開きます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-282">When we click the "Add" button, Visual Studio will save a new scaffold-based "Create.aspx" view to the "\Views\Dinners" directory, and open it up within the IDE:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

<span data-ttu-id="f4e79-283">生成されたデフォルトの"create"スキャフォールディングファイルに変更を加え、次のように変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="f4e79-283">Let's make a few changes to the default "create" scaffold file that was generated for us, and modify it up to look like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

<span data-ttu-id="f4e79-284">そして今、私たちのアプリケーションを実行し、ブラウザ内で *「/Dinners /Create」URL*にアクセスすると、Createアクションの実装から以下のようなUIがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-284">And now when we run our application and access the *"/Dinners/Create"* URL within the browser it will render UI like below from our Create action implementation:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a><span data-ttu-id="f4e79-285">HTTP-POST 作成アクション メソッドの実装</span><span class="sxs-lookup"><span data-stu-id="f4e79-285">Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="f4e79-286">CREATE アクション メソッドの HTTP-GET バージョンが実装されています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-286">We have the HTTP-GET version of our Create action method implemented.</span></span> <span data-ttu-id="f4e79-287">ユーザーが [保存] ボタンをクリックすると、フォームのポストを実行して *、/Dinners/CREATE* URL を&lt;作成&gt;し、HTTP POST 動詞を使用して HTML 入力フォームの値を送信します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-287">When a user clicks the "Save" button it performs a form post to the */Dinners/Create* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span>

<span data-ttu-id="f4e79-288">次に、アクション作成メソッドの HTTP POST 動作を実装しましょう。</span><span class="sxs-lookup"><span data-stu-id="f4e79-288">Let's now implement the HTTP POST behavior of our create action method.</span></span> <span data-ttu-id="f4e79-289">まず、HTTP POST シナリオを処理することを示す "AcceptVerbs" 属性を持つ DinnersController に、オーバーロードされた "Create" アクション メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-289">We'll begin by adding an overloaded "Create" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

<span data-ttu-id="f4e79-290">HTTP-POST が有効な "Create" メソッド内のポストされたフォーム パラメーターにアクセスするには、さまざまな方法があります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-290">There are a variety of ways we can access the posted form parameters within our HTTP-POST enabled "Create" method.</span></span>

<span data-ttu-id="f4e79-291">1 つの方法は、新しい Dinner オブジェクトを作成し *、UpdateModel()* ヘルパー メソッドを使用することです (Edit アクションで行ったように) ポストされたフォーム値を設定します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-291">One approach is to create a new Dinner object and then use the *UpdateModel()* helper method (like we did with the Edit action) to populate it with the posted form values.</span></span> <span data-ttu-id="f4e79-292">その後、DinnerRepository に追加し、データベースに永続化し、以下のコードを使用して新しく作成された Dinner を表示するために、ユーザーを詳細アクションにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-292">We can then add it to our DinnerRepository, persist it to the database, and redirect the user to our Details action to show the newly created Dinner using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

<span data-ttu-id="f4e79-293">代わりに、Create() アクションメソッドがメソッドパラメータとして Dinner オブジェクトを受け取るアプローチを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-293">Alternatively, we can use an approach where we have our Create() action method take a Dinner object as a method parameter.</span></span> <span data-ttu-id="f4e79-294">ASP.NETMVC は自動的に新しい Dinner オブジェクトをインスタンス化し、フォーム入力を使用してそのプロパティを設定し、アクション メソッドに渡します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-294">ASP.NET MVC will then automatically instantiate a new Dinner object for us, populate its properties using the form inputs, and pass it to our action method:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

<span data-ttu-id="f4e79-295">上記のアクション メソッドは、ModelState.IsValid プロパティをチェックして、Dinner オブジェクトにフォームポスト値が正常に設定されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-295">Our action method above verifies that the Dinner object has been successfully populated with the form post values by checking the ModelState.IsValid property.</span></span> <span data-ttu-id="f4e79-296">入力変換の問題 (EventDate プロパティの "BOGUS" の文字列など) がある場合、この値は false を返し、何らかの問題がある場合はアクション メソッドがフォームを再表示します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-296">This will return false if there are input conversion issues (for example: a string of "BOGUS" for the EventDate property), and if there are any issues our action method redisplays the form.</span></span>

<span data-ttu-id="f4e79-297">入力値が有効な場合、アクション メソッドは新しい Dinner を追加して DinnerRepository に保存しようとします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-297">If the input values are valid, then the action method attempts to add and save the new Dinner to the DinnerRepository.</span></span> <span data-ttu-id="f4e79-298">この処理は try/catch ブロック内でラップされ、ビジネス ルール違反が発生した場合にフォームを再表示します (これにより、dinnerRepository.Save() メソッドが例外を発生させます)。</span><span class="sxs-lookup"><span data-stu-id="f4e79-298">It wraps this work within a try/catch block and redisplays the form if there are any business rule violations (which would cause the dinnerRepository.Save() method to raise an exception).</span></span>

<span data-ttu-id="f4e79-299">このエラー処理の動作を確認するには *、/Dinners/CREATE* URL をリクエストし、新しい Dinner の詳細を入力します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-299">To see this error handling behavior in action, we can request the */Dinners/Create* URL and fill out details about a new Dinner.</span></span> <span data-ttu-id="f4e79-300">入力または値が正しくないと、次のように強調表示されたエラーで作成フォームが再表示されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-300">Incorrect input or values will cause the create form to be redisplayed with the errors highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

<span data-ttu-id="f4e79-301">作成フォームが編集フォームとまったく同じ検証とビジネス ルールを遵守していることに注目してください。</span><span class="sxs-lookup"><span data-stu-id="f4e79-301">Notice how our Create form is honoring the exact same validation and business rules as our Edit form.</span></span> <span data-ttu-id="f4e79-302">これは、検証ルールとビジネス ルールがモデルで定義され、アプリケーションの UI またはコントローラに埋め込まれなかったためです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-302">This is because our validation and business rules were defined in the model, and were not embedded within the UI or controller of the application.</span></span> <span data-ttu-id="f4e79-303">つまり、検証やビジネス ルールを 1 か所で変更/進化させ、アプリケーション全体に適用できることを意味します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-303">This means we can later change/evolve our validation or business rules in a single place and have them apply throughout our application.</span></span> <span data-ttu-id="f4e79-304">新しいルールや既存のルールの変更を自動的に反映するために、Edit または Create アクションメソッド内のコードを変更する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f4e79-304">We will not have to change any code within either our Edit or Create action methods to automatically honor any new rules or modifications to existing ones.</span></span>

<span data-ttu-id="f4e79-305">入力値を修正し、再度 [保存] ボタンをクリックすると、DinnerRepository への追加が成功し、新しい Dinner がデータベースに追加されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-305">When we fix the input values and click the "Save" button again, our addition to the DinnerRepository will succeed, and a new Dinner will be added to the database.</span></span> <span data-ttu-id="f4e79-306">その後、新しく作成されたディナーの詳細が表示されます *。./Dinners/Details/[id]URL*にリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-306">We will then be redirected to the */Dinners/Details/[id]* URL – where we will be presented with details about the newly created Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a><span data-ttu-id="f4e79-307">サポートの削除</span><span class="sxs-lookup"><span data-stu-id="f4e79-307">Delete Support</span></span>

<span data-ttu-id="f4e79-308">それでは、DinnersController に "削除" サポートを追加しましょう。</span><span class="sxs-lookup"><span data-stu-id="f4e79-308">Let's now add "Delete" support to our DinnersController.</span></span>

#### <a name="the-http-get-delete-action-method"></a><span data-ttu-id="f4e79-309">HTTP-GET 削除アクション メソッド</span><span class="sxs-lookup"><span data-stu-id="f4e79-309">The HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="f4e79-310">まず、削除アクション メソッドの HTTP GET 動作を実装します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-310">We'll begin by implementing the HTTP GET behavior of our delete action method.</span></span> <span data-ttu-id="f4e79-311">このメソッドは、誰かが */Dinners/Delete/[id]* URL にアクセスしたときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-311">This method will get called when someone visits the */Dinners/Delete/[id]* URL.</span></span> <span data-ttu-id="f4e79-312">実装は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-312">Below is the implementation:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

<span data-ttu-id="f4e79-313">アクション メソッドは、削除する Dinner の取得を試みます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-313">The action method attempts to retrieve the Dinner to be deleted.</span></span> <span data-ttu-id="f4e79-314">Dinner が存在する場合は、Dinner オブジェクトに基づいてビューがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-314">If the Dinner exists it renders a View based on the Dinner object.</span></span> <span data-ttu-id="f4e79-315">オブジェクトが存在しない場合 (または既に削除されている場合)、"Details" アクション メソッド用に作成した "NotFound" ビュー テンプレートをレンダリングするビューが返されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-315">If the object doesn't exist (or has already been deleted) it returns a View that renders the "NotFound" view template we created earlier for our "Details" action method.</span></span>

<span data-ttu-id="f4e79-316">Delete アクションメソッド内で右クリックし、「ビューの追加」コンテキストメニューコマンドを選択することで、「削除」ビューテンプレートを作成できます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-316">We can create the "Delete" view template by right-clicking within the Delete action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="f4e79-317">[ビューの追加] ダイアログでは、Dinner オブジェクトをモデルとしてビュー テンプレートに渡すことを示し、空のテンプレートを作成することを選択します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-317">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to create an empty template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

<span data-ttu-id="f4e79-318">[追加] ボタンをクリックすると、Visual Studio は "\Views\Dinners" ディレクトリ内に新しい "Delete.aspx" ビュー テンプレート ファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-318">When we click the "Add" button, Visual Studio will add a new "Delete.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="f4e79-319">テンプレートに HTML とコードを追加して、次のような削除確認画面を実装します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-319">We'll add some HTML and code to the template to implement a delete confirmation screen like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

<span data-ttu-id="f4e79-320">上記のコードは、削除する Dinner のタイトルを表示し、エンド&lt;ユーザー&gt;がその中の [削除] ボタンをクリックした場合に POST を実行するフォーム要素を /Dinners/Delete/[id] URL に出力します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-320">The code above displays the title of the Dinner to be deleted, and outputs a &lt;form&gt; element that does a POST to the /Dinners/Delete/[id] URL if the end-user clicks the "Delete" button within it.</span></span>

<span data-ttu-id="f4e79-321">アプリケーションを実行し、有効な Dinner オブジェクトの *"/Dinners/Delete/[id]"* URL にアクセスすると、次のように UI がレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-321">When we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it renders UI like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| <span data-ttu-id="f4e79-322">**サイドトピック:なぜ私たちはPOSTを行っているのですか?**</span><span class="sxs-lookup"><span data-stu-id="f4e79-322">**Side Topic: Why are we doing a POST?**</span></span> |
| --- |
| <span data-ttu-id="f4e79-323">あなたは尋ねるかもしれません - なぜ私たちは削除確認画面で&lt;フォーム&gt;を作成する努力をしましたか?</span><span class="sxs-lookup"><span data-stu-id="f4e79-323">You might ask – why did we go through the effort of creating a &lt;form&gt; within our Delete confirmation screen?</span></span> <span data-ttu-id="f4e79-324">実際の削除操作を実行するアクション メソッドにリンクするには、標準のハイパーリンクを使用してみませんか。</span><span class="sxs-lookup"><span data-stu-id="f4e79-324">Why not just use a standard hyperlink to link to an action method that does the actual delete operation?</span></span> <span data-ttu-id="f4e79-325">その理由は、Web クローラや検索エンジンが URL を検出し、リンクをたどったときにデータが誤って削除されるのを防ぐように注意する必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-325">The reason is because we want to be careful to guard against web-crawlers and search engines discovering our URLs and inadvertently causing data to be deleted when they follow the links.</span></span> <span data-ttu-id="f4e79-326">HTTP-GET ベースの URL は、アクセス/クロールが安全であると見なされ、HTTP-POST の URL に従わないことを想定しています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-326">HTTP-GET based URLs are considered "safe" for them to access/crawl, and they are supposed to not follow HTTP-POST ones.</span></span> <span data-ttu-id="f4e79-327">適切なルールは、常に、HTTP-POST 要求の背後に破壊的な操作やデータ変更操作を配置することです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-327">A good rule is to make sure you always put destructive or data modifying operations behind HTTP-POST requests.</span></span> |

#### <a name="implementing-the-http-post-delete-action-method"></a><span data-ttu-id="f4e79-328">HTTP-POST 削除アクション メソッドの実装</span><span class="sxs-lookup"><span data-stu-id="f4e79-328">Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="f4e79-329">削除確認画面を表示する削除アクションメソッドの HTTP-GET バージョンが実装されました。</span><span class="sxs-lookup"><span data-stu-id="f4e79-329">We now have the HTTP-GET version of our Delete action method implemented which displays a delete confirmation screen.</span></span> <span data-ttu-id="f4e79-330">エンドユーザーが「削除」ボタンをクリックすると *、/Dinners/Dinner/[id]URL*にフォームポストが実行されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-330">When an end user clicks the "Delete" button it will perform a form post to the */Dinners/Dinner/[id]* URL.</span></span>

<span data-ttu-id="f4e79-331">次のコードを使用して、削除アクション メソッドの HTTP "POST" 動作を実装してみましょう。</span><span class="sxs-lookup"><span data-stu-id="f4e79-331">Let's now implement the HTTP "POST" behavior of the delete action method using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

<span data-ttu-id="f4e79-332">削除アクション メソッドの HTTP-POST バージョンは、削除するディナー オブジェクトを取得しようとします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-332">The HTTP-POST version of our Delete action method attempts to retrieve the dinner object to delete.</span></span> <span data-ttu-id="f4e79-333">(既に削除されているため) 見つからない場合は、"NotFound" テンプレートがレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-333">If it can't find it (because it has already been deleted) it renders our "NotFound" template.</span></span> <span data-ttu-id="f4e79-334">Dinner が見つかった場合は、Dinner リポジトリから削除されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-334">If it finds the Dinner, it deletes it from the DinnerRepository.</span></span> <span data-ttu-id="f4e79-335">その後、「削除済み」テンプレートをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-335">It then renders a "Deleted" template.</span></span>

<span data-ttu-id="f4e79-336">"削除済み" テンプレートを実装するには、アクション メソッドを右クリックし、[ビューの追加] コンテキスト メニューを選択します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-336">To implement the "Deleted" template we'll right-click in the action method and choose the "Add View" context menu.</span></span> <span data-ttu-id="f4e79-337">ビューに "Deleted" という名前を付け、空のテンプレートにします (厳密に型指定されたモデル オブジェクトは受け取りません)。</span><span class="sxs-lookup"><span data-stu-id="f4e79-337">We'll name our view "Deleted" and have it be an empty template (and not take a strongly-typed model object).</span></span> <span data-ttu-id="f4e79-338">その後、HTML コンテンツを追加します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-338">We'll then add some HTML content to it:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

<span data-ttu-id="f4e79-339">そして今、私たちは、アプリケーションを実行し、有効なDinnerオブジェクトの *「/ディナー/削除/[id]」URL*にアクセスすると、次のような私たちの夕食の削除確認画面が表示されます:</span><span class="sxs-lookup"><span data-stu-id="f4e79-339">And now when we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it will render our Dinner delete confirmation screen like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

<span data-ttu-id="f4e79-340">「削除」ボタンをクリックすると *、/Dinners/Delete/[id]URL*に対してHTTP-POSTが実行され、データベースからディナーが削除され、「削除済み」ビューテンプレートが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-340">When we click the "Delete" button it will perform an HTTP-POST to the */Dinners/Delete/[id]* URL, which will delete the Dinner from our database, and display our "Deleted" view template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a><span data-ttu-id="f4e79-341">モデル バインド セキュリティ</span><span class="sxs-lookup"><span data-stu-id="f4e79-341">Model Binding Security</span></span>

<span data-ttu-id="f4e79-342">ASP.NET MVC の組み込みのモデル バインド機能を使用する 2 つの異なる方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="f4e79-342">We've discussed two different ways to use the built-in model-binding features of ASP.NET MVC.</span></span> <span data-ttu-id="f4e79-343">最初に UpdateModel() メソッドを使用して既存のモデル オブジェクトのプロパティを更新し、2 つ目は mvc のサポート ASP.NETを使用してアクション メソッド パラメーターとしてモデル オブジェクトを渡します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-343">The first using the UpdateModel() method to update properties on an existing model object, and the second using ASP.NET MVC's support for passing model objects in as action method parameters.</span></span> <span data-ttu-id="f4e79-344">これらの技術の両方が非常に強力で非常に便利です。</span><span class="sxs-lookup"><span data-stu-id="f4e79-344">Both of these techniques are very powerful and extremely useful.</span></span>

<span data-ttu-id="f4e79-345">この力はまた、それに責任をもたらします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-345">This power also brings with it responsibility.</span></span> <span data-ttu-id="f4e79-346">ユーザー入力を受け入れる際には常にセキュリティについて妄想することが重要であり、オブジェクトをバインドして入力を行う場合も同様です。</span><span class="sxs-lookup"><span data-stu-id="f4e79-346">It is important to always be paranoid about security when accepting any user input, and this is also true when binding objects to form input.</span></span> <span data-ttu-id="f4e79-347">HTML や JavaScript のインジェクション攻撃を避けるために、ユーザーが入力した値を常に HTML エンコードし、SQL インジェクション攻撃に注意する必要があります (注: LINQ to SQL を使用して、これらの種類の攻撃を防ぐためにパラメーターを自動的にエンコードします)。</span><span class="sxs-lookup"><span data-stu-id="f4e79-347">You should be careful to always HTML encode any user-entered values to avoid HTML and JavaScript injection attacks, and be careful of SQL injection attacks (note: we are using LINQ to SQL for our application, which automatically encodes parameters to prevent these types of attacks).</span></span> <span data-ttu-id="f4e79-348">クライアント側の検証だけに頼ることはなく、サーバー側の検証を常に使用して、偽の値を送信しようとするハッカーを防ぐ必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-348">You should never rely on client-side validation alone, and always employ server-side validation to guard against hackers attempting to send you bogus values.</span></span>

<span data-ttu-id="f4e79-349">ASP.NET MVC のバインディング機能を使用する際に考える追加のセキュリティ項目の 1 つは、バインドするオブジェクトのスコープです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-349">One additional security item to make sure you think about when using the binding features of ASP.NET MVC is the scope of the objects you are binding.</span></span> <span data-ttu-id="f4e79-350">具体的には、バインドを許可するプロパティのセキュリティへの影響を理解し、エンド ユーザーが実際に更新できるプロパティのみを更新できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-350">Specifically, you want to make sure you understand the security implications of the properties you are allowing to be bound, and make sure you only allow those properties that really should be updatable by an end-user to be updated.</span></span>

<span data-ttu-id="f4e79-351">デフォルトでは、UpdateModel() メソッドは、入力フォームのパラメーター値に一致するモデル オブジェクトのすべてのプロパティを更新しようとします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-351">By default, the UpdateModel() method will attempt to update all properties on the model object that match incoming form parameter values.</span></span> <span data-ttu-id="f4e79-352">同様に、アクションメソッドのパラメータとして渡されるオブジェクトは、デフォルトで、フォームパラメータを介してすべてのプロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-352">Likewise, objects passed as action method parameters also by default can have all of their properties set via form parameters.</span></span>

#### <a name="locking-down-binding-on-a-per-usage-basis"></a><span data-ttu-id="f4e79-353">使用ごとにバインドをロックダウンする</span><span class="sxs-lookup"><span data-stu-id="f4e79-353">Locking down binding on a per-usage basis</span></span>

<span data-ttu-id="f4e79-354">バインディング ポリシーは、更新可能なプロパティの明示的な "include list" を提供することで、使用ごとにロックダウンできます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-354">You can lock down the binding policy on a per-usage basis by providing an explicit "include list" of properties that can be updated.</span></span> <span data-ttu-id="f4e79-355">これは、次のような UpdateModel() メソッドに追加の文字列配列パラメータを渡すことによって行うことができます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-355">This can be done by passing an extra string array parameter to the UpdateModel() method like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

<span data-ttu-id="f4e79-356">アクション メソッドのパラメーターとして渡されるオブジェクトは、次のように指定できるプロパティの "include list" を有効にする [Bind] 属性もサポートします。</span><span class="sxs-lookup"><span data-stu-id="f4e79-356">Objects passed as action method parameters also support a [Bind] attribute that enables an "include list" of allowed properties to be specified like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a><span data-ttu-id="f4e79-357">型ベースでのバインドのロック</span><span class="sxs-lookup"><span data-stu-id="f4e79-357">Locking down binding on a type basis</span></span>

<span data-ttu-id="f4e79-358">また、バインディング規則をタイプごとにロックダウンすることもできます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-358">You can also lock down the binding rules on a per-type basis.</span></span> <span data-ttu-id="f4e79-359">これにより、バインド規則を一度指定し、すべてのコントローラーとアクション メソッドのすべてのシナリオ (UpdateModel とアクション メソッドのパラメーター の両方のシナリオを含む) で適用できます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-359">This allows you to specify the binding rules once, and then have them apply in all scenarios (including both UpdateModel and action method parameter scenarios) across all controllers and action methods.</span></span>

<span data-ttu-id="f4e79-360">型ごとのバインド規則は、型に [Bind] 属性を追加するか、またはアプリケーションの Global.asax ファイル内に登録することでカスタマイズできます (型を所有していないシナリオに便利です)。</span><span class="sxs-lookup"><span data-stu-id="f4e79-360">You can customize the per-type binding rules by adding a [Bind] attribute onto a type, or by registering it within the Global.asax file of the application (useful for scenarios where you don't own the type).</span></span> <span data-ttu-id="f4e79-361">その後、Bind 属性の Include プロパティと Exclude プロパティを使用して、特定のクラスまたはインターフェイスにバインドできるプロパティを制御できます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-361">You can then use the Bind attribute's Include and Exclude properties to control which properties are bindable for the particular class or interface.</span></span>

<span data-ttu-id="f4e79-362">NerdDinner アプリケーションの Dinner クラスにこのテクニックを使用し、バインド可能なプロパティのリストを次に制限する [Bind] 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="f4e79-362">We'll use this technique for the Dinner class in our NerdDinner application, and add a [Bind] attribute to it that restricts the list of bindable properties to the following:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

<span data-ttu-id="f4e79-363">RSVPs コレクションをバインディングを介して操作することは許可されておらず、また、DinnerID または HostedBy プロパティをバインディングによって設定することも許可していないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="f4e79-363">Notice we are not allowing the RSVPs collection to be manipulated via binding, nor are we allowing the DinnerID or HostedBy properties to be set via binding.</span></span> <span data-ttu-id="f4e79-364">セキュリティ上の理由から、アクションメソッド内の明示的なコードを使用してこれらの特定のプロパティを操作するだけです。</span><span class="sxs-lookup"><span data-stu-id="f4e79-364">For security reasons we'll instead only manipulate these particular properties using explicit code within our action methods.</span></span>

### <a name="crud-wrap-up"></a><span data-ttu-id="f4e79-365">CRUDラップアップ</span><span class="sxs-lookup"><span data-stu-id="f4e79-365">CRUD Wrap-Up</span></span>

<span data-ttu-id="f4e79-366">ASP.NET MVC には、フォームの投稿シナリオの実装に役立つ多くの組み込み機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-366">ASP.NET MVC includes a number of built-in features that help with implementing form posting scenarios.</span></span> <span data-ttu-id="f4e79-367">これらの機能を使用して、DinnerRepository の上に CRUD UI サポートを提供しました。</span><span class="sxs-lookup"><span data-stu-id="f4e79-367">We used a variety of these features to provide CRUD UI support on top of our DinnerRepository.</span></span>

<span data-ttu-id="f4e79-368">アプリケーションを実装するために、モデルに焦点を当てたアプローチを使用しています。</span><span class="sxs-lookup"><span data-stu-id="f4e79-368">We are using a model-focused approach to implement our application.</span></span> <span data-ttu-id="f4e79-369">つまり、すべての検証とビジネス ルールロジックは、コントローラやビューではなく、モデルレイヤー内で定義されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-369">This means that all our validation and business rule logic is defined within our model layer – and not within our controllers or views.</span></span> <span data-ttu-id="f4e79-370">当社のコントローラクラスもビューテンプレートも、Dinnerモデルクラスによって施行されている特定のビジネスルールについて何も知りません。</span><span class="sxs-lookup"><span data-stu-id="f4e79-370">Neither our Controller class nor our View templates know anything about the specific business rules being enforced by our Dinner model class.</span></span>

<span data-ttu-id="f4e79-371">これにより、アプリケーション アーキテクチャがクリーンな状態に保ち、テストが容易になります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-371">This will keep our application architecture clean and make it easier to test.</span></span> <span data-ttu-id="f4e79-372">将来的には、モデルレイヤーにビジネスルールを追加することができ、それらをサポートするためにコントローラまたはビューに*コード変更を加える必要はありません*。</span><span class="sxs-lookup"><span data-stu-id="f4e79-372">We can add additional business rules to our model layer in the future and *not have to make any code changes* to our Controller or View in order for them to be supported.</span></span> <span data-ttu-id="f4e79-373">これにより、将来的にアプリケーションを進化させ、変更するための多くの俊敏性が提供されます。</span><span class="sxs-lookup"><span data-stu-id="f4e79-373">This is going to provide us with a great deal of agility to evolve and change our application in the future.</span></span>

<span data-ttu-id="f4e79-374">DinnersController は、ディナーリスト/詳細を有効にし、サポートの作成、編集、削除を行うようになりました。</span><span class="sxs-lookup"><span data-stu-id="f4e79-374">Our DinnersController now enables Dinner listings/details, as well as create, edit and delete support.</span></span> <span data-ttu-id="f4e79-375">クラスの完全なコードは以下にあります。</span><span class="sxs-lookup"><span data-stu-id="f4e79-375">The complete code for the class can be found below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a><span data-ttu-id="f4e79-376">次の手順</span><span class="sxs-lookup"><span data-stu-id="f4e79-376">Next Step</span></span>

<span data-ttu-id="f4e79-377">DinnersController クラス内に基本的な CRUD (作成、読み取り、更新、および削除) のサポート実装が用意されました。</span><span class="sxs-lookup"><span data-stu-id="f4e79-377">We now have basic CRUD (Create, Read, Update and Delete) support implement within our DinnersController class.</span></span>

<span data-ttu-id="f4e79-378">次に、ViewData クラスと ViewModel クラスを使用して、フォーム上の UI をさらに豊かにする方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="f4e79-378">Let's now look at how we can use ViewData and ViewModel classes to enable even richer UI on our forms.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f4e79-379">[前へ](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [次へ](use-viewdata-and-implement-viewmodel-classes.md)</span><span class="sxs-lookup"><span data-stu-id="f4e79-379">[Previous](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
[Next](use-viewdata-and-implement-viewmodel-classes.md)</span></span>
