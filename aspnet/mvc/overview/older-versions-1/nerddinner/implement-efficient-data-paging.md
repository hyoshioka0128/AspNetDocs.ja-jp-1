---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 効率的なデータ ページングを実装する |マイクロソフトドキュメント
author: rick-anderson
description: ステップ 8 では、1000 のディナーを一度に表示するのではなく、今後 10 回のディナーのみを表示するように、/Dinners URL にページング サポートを追加する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: a833553fe44b62b136f7eb55c7e00eca0b0462c6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541326"
---
# <a name="implement-efficient-data-paging"></a><span data-ttu-id="5a5a4-103">効率的なデータ ページングを実装する</span><span class="sxs-lookup"><span data-stu-id="5a5a4-103">Implement Efficient Data Paging</span></span>

<span data-ttu-id="5a5a4-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5a5a4-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="5a5a4-105">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="5a5a4-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="5a5a4-106">これは、MVC 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)の手順 8 ASP.NET示します。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-106">This is step 8 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="5a5a4-107">手順 8 では、/Dinners URL にページング サポートを追加して、1000 のディナーを一度に表示する代わりに、一度に 10 回の今後のディナーのみを表示し、エンド ユーザーが SEO に優しい方法でリスト全体を前後にページ移動できるようにする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-107">Step 8 shows how to add paging support to our /Dinners URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>
> 
> <span data-ttu-id="5a5a4-108">mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-8-paging-support"></a><span data-ttu-id="5a5a4-109">NerdDinner ステップ 8: ページングのサポート</span><span class="sxs-lookup"><span data-stu-id="5a5a4-109">NerdDinner Step 8: Paging Support</span></span>

<span data-ttu-id="5a5a4-110">私たちのサイトが成功した場合、それは今後の夕食の数千人を持つことになります。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-110">If our site is successful, it will have thousands of upcoming dinners.</span></span> <span data-ttu-id="5a5a4-111">私たちは、これらのディナーのすべてを処理するために私たちのUIがスケールし、ユーザーがそれらを閲覧できるように確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-111">We need to make sure that our UI scales to handle all of these dinners, and allows users to browse them.</span></span> <span data-ttu-id="5a5a4-112">これを有効にするために *、/Dinners* URLにページングサポートを追加して、1000のディナーを一度に表示するのではなく、一度に10回のディナーのみを表示し、エンドユーザーがSEOフレンドリーな方法でリスト全体を前後にページできるようにします。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-112">To enable this, we'll add paging support to our */Dinners* URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>

### <a name="index-action-method-recap"></a><span data-ttu-id="5a5a4-113">インデックス() アクション メソッドの要約</span><span class="sxs-lookup"><span data-stu-id="5a5a4-113">Index() Action Method Recap</span></span>

<span data-ttu-id="5a5a4-114">DinnersController クラス内の Index() アクション メソッドは、現在次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-114">The Index() action method within our DinnersController class currently looks like below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

<span data-ttu-id="5a5a4-115">*/Dinners* URL に対してリクエストが行われると、今後のすべてのディナーのリストが取得され、そのすべての一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-115">When a request is made to the */Dinners* URL, it retrieves a list of all upcoming dinners and then renders a listing of all of them out:</span></span>

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a><span data-ttu-id="5a5a4-116">クエリ可能 T&lt;について&gt;</span><span class="sxs-lookup"><span data-stu-id="5a5a4-116">Understanding IQueryable&lt;T&gt;</span></span>

<span data-ttu-id="5a5a4-117">*IQueryable&lt;&gt; T*は、.NET 3.5 の一部として LINQ で導入されたインターフェイスです。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-117">*IQueryable&lt;T&gt;* is an interface that was introduced with LINQ as part of .NET 3.5.</span></span> <span data-ttu-id="5a5a4-118">ページング サポートを実装するために利用できる強力な "遅延実行" シナリオを有効にします。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-118">It enables powerful "deferred execution" scenarios that we can take advantage of to implement paging support.</span></span>

<span data-ttu-id="5a5a4-119">私たちの夕食リポジトリでは、FindUpcomingDinners()&lt;メソッド&gt;からIQueryableディナーシーケンスを返しています。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-119">In our DinnerRepository we are returning an IQueryable&lt;Dinner&gt; sequence from our FindUpcomingDinners() method:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

<span data-ttu-id="5a5a4-120">FindUpcomingDinners() メソッドによって返される IQueryable&lt;Dinner&gt;オブジェクトは、LINQ to SQL を使用してデータベースから Dinner オブジェクトを取得するクエリをカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-120">The IQueryable&lt;Dinner&gt; object returned by our FindUpcomingDinners() method encapsulates a query to retrieve Dinner objects from our database using LINQ to SQL.</span></span> <span data-ttu-id="5a5a4-121">重要なのは、クエリ内のデータにアクセスして反復処理を行うか、そのデータに対して ToList() メソッドを呼び出すまで、データベースに対してクエリを実行しません。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-121">Importantly, it won't execute the query against the database until we attempt to access/iterate over the data in the query, or until we call the ToList() method on it.</span></span> <span data-ttu-id="5a5a4-122">FindUpcomingDinners() メソッドを呼び出すコードは、クエリを実行する前に、IQueryable&lt;Dinner&gt;オブジェクトに "連鎖" 操作/フィルターを追加することをオプションで選択できます。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-122">The code calling our FindUpcomingDinners() method can optionally choose to add additional "chained" operations/filters to the IQueryable&lt;Dinner&gt; object before executing the query.</span></span> <span data-ttu-id="5a5a4-123">LINQ to SQL は、データが要求されたときにデータベースに対して結合されたクエリを実行するのに十分なスマートです。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-123">LINQ to SQL is then smart enough to execute the combined query against the database when the data is requested.</span></span>

<span data-ttu-id="5a5a4-124">ページング ロジックを実装するには、DinnersController の Index() アクション メソッドを更新して、返された IQueryable&lt;Dinner&gt;シーケンスに追加の "スキップ" 演算子と "Take" 演算子を適用してから、ToList() を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-124">To implement paging logic we can update our DinnersController's Index() action method so that it applies additional "Skip" and "Take" operators to the returned IQueryable&lt;Dinner&gt; sequence before calling ToList() on it:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

<span data-ttu-id="5a5a4-125">上記のコードは、データベース内の最初の 10 個の今後のディナーをスキップし、20 個のディナーを返します。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-125">The above code skips over the first 10 upcoming dinners in the database, and then returns back 20 dinners.</span></span> <span data-ttu-id="5a5a4-126">LINQ to SQL は、Web サーバーではなく、SQL データベースでスキップロジックを実行する最適化された SQL クエリを構築するのに十分なほどスマートです。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-126">LINQ to SQL is smart enough to construct an optimized SQL query that performs this skipping logic in the SQL database – and not in the web-server.</span></span> <span data-ttu-id="5a5a4-127">これは、データベースに何百万もの Dinners が含まれている場合でも、この要求の一部として取得される 10 個のみの情報を取得することを意味します (効率的でスケーラブル)。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-127">This means that even if we have millions of upcoming Dinners in the database, only the 10 we want will be retrieved as part of this request (making it efficient and scalable).</span></span>

### <a name="adding-a-page-value-to-the-url"></a><span data-ttu-id="5a5a4-128">URL に "ページ" 値を追加する</span><span class="sxs-lookup"><span data-stu-id="5a5a4-128">Adding a "page" value to the URL</span></span>

<span data-ttu-id="5a5a4-129">特定のページ範囲をハードコーディングするのではなく、URL に、ユーザーが要求している Dinner 範囲を示す "ページ" パラメーターを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-129">Instead of hard-coding a specific page range, we'll want our URLs to include a "page" parameter that indicates which Dinner range a user is requesting.</span></span>

#### <a name="using-a-querystring-value"></a><span data-ttu-id="5a5a4-130">クエリ文字列値の使用</span><span class="sxs-lookup"><span data-stu-id="5a5a4-130">Using a Querystring value</span></span>

<span data-ttu-id="5a5a4-131">次のコードは、クエリ文字列パラメーターをサポートし *、/Dinners?page=2*のような URL を有効にするために、Index() アクション メソッドを更新する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-131">The code below demonstrates how we can update our Index() action method to support a querystring parameter and enable URLs like */Dinners?page=2*:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

<span data-ttu-id="5a5a4-132">上記の Index() アクションメソッドには、"page" という名前のパラメータがあります。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-132">The Index() action method above has a parameter named "page".</span></span> <span data-ttu-id="5a5a4-133">パラメーターは、null 許容整数として宣言されています (これは int? が示すものです)。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-133">The parameter is declared as a nullable integer (that is what int? indicates).</span></span> <span data-ttu-id="5a5a4-134">これは *、/Dinners?page=2* URL の値がパラメータ値として渡されることを意味します。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-134">This means that the */Dinners?page=2* URL will cause a value of "2" to be passed as the parameter value.</span></span> <span data-ttu-id="5a5a4-135">*/Dinners* URL (クエリ文字列値なし) は、NULL 値が渡されます。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-135">The */Dinners* URL (without a querystring value) will cause a null value to be passed.</span></span>

<span data-ttu-id="5a5a4-136">ページ値にページサイズ (この場合は 10 行) を掛けて、スキップするディナーの数を決定します。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-136">We are multiplying the page value by the page size (in this case 10 rows) to determine how many dinners to skip over.</span></span> <span data-ttu-id="5a5a4-137">Null 許容型を扱う場合に便利な[C# null "合体" 演算子 (?) を](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx)使用しています。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-137">We are using the [C# null "coalescing" operator (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) which is useful when dealing with nullable types.</span></span> <span data-ttu-id="5a5a4-138">上記のコードでは、ページ パラメータが null の場合、ページの値 0 が割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-138">The code above assigns page the value of 0 if the page parameter is null.</span></span>

#### <a name="using-embedded-url-values"></a><span data-ttu-id="5a5a4-139">埋め込み URL 値の使用</span><span class="sxs-lookup"><span data-stu-id="5a5a4-139">Using Embedded URL values</span></span>

<span data-ttu-id="5a5a4-140">クエリ文字列値を使用する代わりに、実際の URL 自体にページ パラメーターを埋め込むことがあります。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-140">An alternative to using a querystring value would be to embed the page parameter within the actual URL itself.</span></span> <span data-ttu-id="5a5a4-141">たとえば *、/ディナー/ページ/2*または */ディナー/2。*</span><span class="sxs-lookup"><span data-stu-id="5a5a4-141">For example: */Dinners/Page/2* or */Dinners/2*.</span></span> <span data-ttu-id="5a5a4-142">ASP.NET MVC には、このようなシナリオを簡単にサポートできる強力な URL ルーティング エンジンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-142">ASP.NET MVC includes a powerful URL routing engine that makes it easy to support scenarios like this.</span></span>

<span data-ttu-id="5a5a4-143">任意の受信 URL または URL 形式を、必要なコントローラークラスまたはアクション メソッドにマップするカスタム ルーティング ルールを登録できます。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-143">We can register custom routing rules that map any incoming URL or URL format to any controller class or action method we want.</span></span> <span data-ttu-id="5a5a4-144">必要なのは、プロジェクト内で Global.asax ファイルを開くことだけです。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-144">All we need to-do is to open the Global.asax file within our project:</span></span>

![](implement-efficient-data-paging/_static/image2.png)

<span data-ttu-id="5a5a4-145">次に、ルートへの最初の呼び出しのような MapRoute() ヘルパー メソッドを使用して、新しいマッピング ルールを登録します。以下のマップルート()</span><span class="sxs-lookup"><span data-stu-id="5a5a4-145">And then register a new mapping rule using the MapRoute() helper method like the first call to routes.MapRoute() below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

<span data-ttu-id="5a5a4-146">上記では、"今後のディナー"という名前の新しいルーティングルールを登録しています。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-146">Above we are registering a new routing rule named "UpcomingDinners".</span></span> <span data-ttu-id="5a5a4-147">URL 形式 "Dinners/Page/{page}" を示しています 。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-147">We are indicating it has the URL format "Dinners/Page/{page}" – where {page} is a parameter value embedded within the URL.</span></span> <span data-ttu-id="5a5a4-148">MapRoute() メソッドの 3 番目のパラメーターは、この形式に一致する URL を DinnersController クラスの Index() アクション メソッドにマップする必要があることを示します。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-148">The third parameter to the MapRoute() method indicates that we should map URLs that match this format to the Index() action method on the DinnersController class.</span></span>

<span data-ttu-id="5a5a4-149">クエリ文字列のシナリオで以前とまったく同じ Index() コードを使用できます。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-149">We can use the exact same Index() code we had before with our Querystring scenario – except now our "page" parameter will come from the URL and not the querystring:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

<span data-ttu-id="5a5a4-150">そして今、私たちはアプリケーションを実行し *、/Dinners*を入力すると、最初の10の今後のディナーが表示されます:</span><span class="sxs-lookup"><span data-stu-id="5a5a4-150">And now when we run the application and type in */Dinners* we'll see the first 10 upcoming dinners:</span></span>

![](implement-efficient-data-paging/_static/image3.png)

<span data-ttu-id="5a5a4-151">*そして、私たちが/ディナー/ページ/1*を入力すると、夕食の次のページが表示されます:</span><span class="sxs-lookup"><span data-stu-id="5a5a4-151">And when we type in */Dinners/Page/1* we'll see the next page of dinners:</span></span>

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a><span data-ttu-id="5a5a4-152">ページ ナビゲーション UI の追加</span><span class="sxs-lookup"><span data-stu-id="5a5a4-152">Adding page navigation UI</span></span>

<span data-ttu-id="5a5a4-153">ページング シナリオを完了するための最後の手順は、ユーザーが Dinner データを簡単にスキップできるように、ビュー テンプレート内に "次" と "前" ナビゲーション UI を実装することです。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-153">The last step to complete our paging scenario will be to implement "next" and "previous" navigation UI within our view template to enable users to easily skip over the Dinner data.</span></span>

<span data-ttu-id="5a5a4-154">これを正しく実装するには、データベース内のディナーの合計数と、そのデータの変換対象となるデータのページ数を知る必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-154">To implement this correctly, we'll need to know the total number of Dinners in the database, as well as how many pages of data this translates to.</span></span> <span data-ttu-id="5a5a4-155">次に、現在要求されている "ページ" 値がデータの先頭または末尾にあるかどうかを計算し、それに応じて "前の" UI と "次へ" UI を表示または非表示にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-155">We'll then need to calculate whether the currently requested "page" value is at the beginning or end of the data, and show or hide the "previous" and "next" UI accordingly.</span></span> <span data-ttu-id="5a5a4-156">このロジックを Index() アクションメソッド内に実装できます。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-156">We could implement this logic within our Index() action method.</span></span> <span data-ttu-id="5a5a4-157">または、このロジックをより再利用しやすい方法でカプセル化するヘルパークラスをプロジェクトに追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-157">Alternatively we can add a helper class to our project that encapsulates this logic in a more re-usable way.</span></span>

<span data-ttu-id="5a5a4-158">以下は、.NET Framework に組み込まれているリスト&lt;T&gt;コレクション クラスから派生した単純な "PaginatedList" ヘルパー クラスです。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-158">Below is a simple "PaginatedList" helper class that derives from the List&lt;T&gt; collection class built-into the .NET Framework.</span></span> <span data-ttu-id="5a5a4-159">IQueryable データの任意のシーケンスを改ページ調整するために使用できる再使用できるコレクション クラスを実装します。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-159">It implements a re-usable collection class that can be used to paginate any sequence of IQueryable data.</span></span> <span data-ttu-id="5a5a4-160">NerdDinner&lt;アプリケーションでは、IQueryable Dinner&gt;の結果を使用して動作しますが、他のアプリケーション シナリオで IQueryable&gt;&lt;&gt;&lt;製品または IQueryable 顧客の結果に対しても簡単に使用できます。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-160">In our NerdDinner application we'll have it work over IQueryable&lt;Dinner&gt; results, but it could just as easily be used against IQueryable&lt;Product&gt; or IQueryable&lt;Customer&gt; results in other application scenarios:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

<span data-ttu-id="5a5a4-161">"PageIndex"、"PageSize"、"TotalCount"、および "合計ページ" などのプロパティを計算して公開する方法の上に注意してください。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-161">Notice above how it calculates and then exposes properties like "PageIndex", "PageSize", "TotalCount", and "TotalPages".</span></span> <span data-ttu-id="5a5a4-162">また、コレクション内のデータページが元のシーケンスの先頭または末尾にあるかどうかを示す 2 つのヘルパー プロパティ "HasPreviousPage" と "HasNextPage" を公開します。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-162">It also then exposes two helper properties "HasPreviousPage" and "HasNextPage" that indicate whether the page of data in the collection is at the beginning or end of the original sequence.</span></span> <span data-ttu-id="5a5a4-163">上記のコードでは、Dinnerオブジェクトの総数のカウントを取得する2つのSQLクエリが実行され(これはオブジェクトを返すのではなく、整数を返す「SELECT COUNT」文を実行します)、もう1つは現在のデータページに必要なデータ行だけをデータベースから取得します。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-163">The above code will cause two SQL queries to be run - the first to retrieve the count of the total number of Dinner objects (this doesn't return the objects – rather it performs a "SELECT COUNT" statement that returns an integer), and the second to retrieve just the rows of data we need from our database for the current page of data.</span></span>

<span data-ttu-id="5a5a4-164">その後、DinnersController.Index() ヘルパー メソッドを更新して、DinnerRepository.FindUpcomingDinners() の結果から PaginatedList&lt;ディナー&gt;を作成し、ビュー テンプレートに渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-164">We can then update our DinnersController.Index() helper method to create a PaginatedList&lt;Dinner&gt; from our DinnerRepository.FindUpcomingDinners() result, and pass it to our view template:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

<span data-ttu-id="5a5a4-165">次に、ビューページ&lt;&lt;&gt;&gt;&lt;IEnumerable&lt;&gt;&gt;Dinner の代わりに ViewPage NerdDinner.Helpers.PaginatedList ディナーから継承するように 、ビュー テンプレートの下に次のコードを追加して、次のナビゲーション UI と前のナビゲーション UI を表示または非表示にするように、ビュー テンプレートの一番下に次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-165">We can then update the \Views\Dinners\Index.aspx view template to inherit from ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt;&gt; instead of ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;, and then add the following code to the bottom of our view-template to show or hide next and previous navigation UI:</span></span>

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

<span data-ttu-id="5a5a4-166">ハイパーリンクを生成するために Html.RouteLink() ヘルパー メソッドを使用する方法の上に注意してください。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-166">Notice above how we are using the Html.RouteLink() helper method to generate our hyperlinks.</span></span> <span data-ttu-id="5a5a4-167">このメソッドは、前に使用した Html.ActionLink() ヘルパー メソッドに似ています。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-167">This method is similar to the Html.ActionLink() helper method we've used previously.</span></span> <span data-ttu-id="5a5a4-168">違いは、Global.asax ファイル内で設定する "今後のディナー" ルーティング ルールを使用して URL を生成することです。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-168">The difference is that we are generating the URL using the "UpcomingDinners" routing rule we setup within our Global.asax file.</span></span> <span data-ttu-id="5a5a4-169">これにより *、"/Dinners/Page/{page}* という形式の Index() アクション メソッドへの URL が生成されます。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-169">This ensures that we'll generate URLs to our Index() action method that have the format: */Dinners/Page/{page}* – where the {page} value is a variable we are providing above based on the current PageIndex.</span></span>

<span data-ttu-id="5a5a4-170">そして今、我々は再び私たちのアプリケーションを実行すると、我々は我々のブラウザで一度に10ディナーが表示されます:</span><span class="sxs-lookup"><span data-stu-id="5a5a4-170">And now when we run our application again we'll see 10 dinners at a time in our browser:</span></span>

![](implement-efficient-data-paging/_static/image5.png)

<span data-ttu-id="5a5a4-171">&lt;&lt;&gt;また&lt;、&gt;ページの下部にナビゲーション UI があり、検索エンジンでアクセス可能な URL を使用してデータを前方および逆方向にスキップ&gt;できます。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-171">We also have &lt;&lt;&lt; and &gt;&gt;&gt; navigation UI at the bottom of the page that allows us to skip forwards and backwards over our data using search engine accessible URLs:</span></span>

![](implement-efficient-data-paging/_static/image6.png)

| <span data-ttu-id="5a5a4-172">**サイドトピック: IQueryable T の&lt;意味を理解する&gt;**</span><span class="sxs-lookup"><span data-stu-id="5a5a4-172">**Side Topic: Understanding the implications of IQueryable&lt;T&gt;**</span></span> |
| --- |
| <span data-ttu-id="5a5a4-173">IQueryable&lt;&gt; T は、さまざまな興味深い遅延実行シナリオ (ページングやコンポジション ベースのクエリなど) を可能にする非常に強力な機能です。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-173">IQueryable&lt;T&gt; is a very powerful feature that enables a variety of interesting deferred execution scenarios (like paging and composition based queries).</span></span> <span data-ttu-id="5a5a4-174">すべての強力な機能と同様に、あなたはそれを使用する方法に注意し、それが悪用されていないかどうかを確認したいと思います。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-174">As with all powerful features, you want to be careful with how you use it and make sure it is not abused.</span></span> <span data-ttu-id="5a5a4-175">リポジトリから IQueryable&lt;T&gt;の結果を返すと、呼び出し元のコードがチェーン化された演算子メソッドに追加され、最終的なクエリ実行に参加できることを認識することが重要です。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-175">It is important to recognize that returning an IQueryable&lt;T&gt; result from your repository enables calling code to append on chained operator methods to it, and so participate in the ultimate query execution.</span></span> <span data-ttu-id="5a5a4-176">この機能を呼び出しコードを提供しない場合は、既に実行されているクエリ&lt;の&gt;結果を含む&lt;IList T または IEnumerable T&gt;の結果を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-176">If you do not want to provide calling code this ability, then you should return back IList&lt;T&gt; or IEnumerable&lt;T&gt; results - which contain the results of a query that has already executed.</span></span> <span data-ttu-id="5a5a4-177">ページネーションのシナリオでは、実際のデータページネーション ロジックを呼び出されるリポジトリ メソッドにプッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-177">For pagination scenarios this would require you to push the actual data pagination logic into the repository method being called.</span></span> <span data-ttu-id="5a5a4-178">このシナリオでは、FindUpcomingDinners() ファインダー&lt;メソッドを更新して、PaginatedList ディナー&gt;検索予定ディナー (int pageIndex, int pageSize) を返す署名を持っているか 、または IList&lt;ディナー&gt;の合計カウントを返すために "totalCount" アウトパラムを使用します。&lt;&gt;</span><span class="sxs-lookup"><span data-stu-id="5a5a4-178">In this scenario we might update our FindUpcomingDinners() finder method to have a signature that either returned a PaginatedList: PaginatedList&lt; Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize) { } Or return back an IList&lt;Dinner&gt;, and use a "totalCount" out param to return the total count of Dinners: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out int totalCount) { }</span></span> |

### <a name="next-step"></a><span data-ttu-id="5a5a4-179">次の手順</span><span class="sxs-lookup"><span data-stu-id="5a5a4-179">Next Step</span></span>

<span data-ttu-id="5a5a4-180">それでは、アプリケーションに認証と承認のサポートを追加する方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="5a5a4-180">Let's now look at how we can add authentication and authorization support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5a5a4-181">[前へ](re-use-ui-using-master-pages-and-partials.md)
> [次へ](secure-applications-using-authentication-and-authorization.md)</span><span class="sxs-lookup"><span data-stu-id="5a5a4-181">[Previous](re-use-ui-using-master-pages-and-partials.md)
[Next](secure-applications-using-authentication-and-authorization.md)</span></span>
