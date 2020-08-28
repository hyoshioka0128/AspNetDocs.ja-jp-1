---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
title: Edit メソッドと Edit ビューを調べるMicrosoft Docs
author: Rick-Anderson
description: '注: このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用するこちらで入手できます。 より安全で、より簡単にフォローとデモができます...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 41eb99ca-e88f-4720-ae6d-49a958da8116
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 16ce02ba00e13b4cff2d6e86b2d9e0684aab096e
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044520"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>Edit メソッドと Edit ビューの確認

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する [こちらで](../../getting-started/introduction/getting-started.md) 入手できます。 より安全で、より簡単にフォローし、より多くの機能を紹介します。

このセクションでは、ムービーコントローラーに対して生成されたアクションメソッドとビューを確認します。 次に、カスタム検索ページを追加します。

アプリケーションを実行し、 `Movies` ブラウザーのアドレスバーの URL に */ムービー* を追加して、コントローラーを参照します。 **編集**リンクの上にマウスポインターを置くと、リンク先の URL が表示されます。

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

**Edit**リンクは、 `Html.ActionLink` *Views\Movies\Index.cshtml*ビューのメソッドによって生成されました。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

![Html.actionlink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`オブジェクトは、 [System.web. Mvc. WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx)基本クラスのプロパティを使用して公開されるヘルパーです。 `ActionLink`ヘルパーのメソッドを使用すると、コントローラーのアクションメソッドにリンクする HTML ハイパーリンクを簡単に動的に生成できます。 メソッドの最初の引数 `ActionLink` は、表示するリンクテキスト (など `<a>Edit Me</a>` ) です。 2番目の引数は、呼び出すアクションメソッドの名前です。 最後の引数は、ルートデータ (この場合は4の ID) を生成する [匿名オブジェクト](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) です。

前の図に示すように、生成されたリンクは `http://localhost:xxxxx/Movies/Edit/4` です。 既定のルート ( *App \_ Start\RouteConfig.cs*で確立されます) は、URL パターンを受け取り `{controller}/{action}/{id}` ます。 したがって、ASP.NET は、 `http://localhost:xxxxx/Movies/Edit/4` `Edit` `Movies` パラメーターが4に等しいコントローラーのアクションメソッドへの要求に変換し `ID` ます。 *App \_ Start\RouteConfig.cs*ファイルから次のコードを確認します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

クエリ文字列を使用して、アクションメソッドのパラメーターを渡すこともできます。 たとえば、URL は、 `http://localhost:xxxxx/Movies/Edit?ID=4` `ID` コントローラーのアクションメソッドに4のパラメーターも渡し `Edit` `Movies` ます。

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

コントローラーを開き `Movies` ます。 2つの `Edit` アクションメソッドを次に示します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cs)]

2 番目の `Edit` アクション メソッドの前に `HttpPost` 属性が付いていることに注意してください。 この属性は、メソッドのオーバーロードを `Edit` POST 要求に対してのみ呼び出すことができるように指定します。 `HttpGet`最初の編集メソッドに属性を適用することもできますが、これは既定値なので必要ありません。 (メソッドとして暗黙的に属性を割り当てられるアクションメソッドを参照し `HttpGet` `HttpGet` ます)。

`HttpGet` `Edit` メソッドはムービー ID パラメーターを受け取り、Entity Framework メソッドを使用してムービーを検索 `Find` し、選択したムービーを編集ビューに返します。 パラメーターを指定せずにメソッドが呼び出された場合、ID パラメーターは [既定値](https://msdn.microsoft.com/library/dd264739.aspx) のゼロを指定し `Edit` ます。 ムービーが見つからない場合は、 [HttpNotFound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) が返されます。 スキャフォールディング システムが編集ビューを作成したときは、そのシステムが `Movie` クラスを調べて、クラスの各プロパティの `<label>` および `<input>` 要素をレンダリングするコードを作成しました。 次の例は、生成された編集ビューを示しています。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cshtml)]

ビューテンプレートにファイルの先頭にステートメントが含まれていることに注意して `@model MvcMovie.Models.Movie` ください。これは、ビューがビューテンプレートのモデルを型と想定していることを示し `Movie` ます。

スキャフォールディングコードでは、HTML マークアップを効率化するためにいくつかの *ヘルパーメソッド* を使用しています。 ヘルパーには、 [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx) フィールドの名前 ( &quot; Title &quot; 、 &quot; releasedate &quot; 、 &quot; Genre &quot; 、または &quot; Price &quot; ) が表示されます。 ヘルパーは、 [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) HTML 要素をレンダリングし `<input>` ます。 ヘルパーには、 [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) そのプロパティに関連付けられている検証メッセージが表示されます。

アプリケーションを実行し、 */ムービー* の URL に移動します。 **[編集]** リンクをクリックします。 ブラウザーで、ページのソースを表示します。 Form 要素の HTML を次に示します。

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html?highlight=7,10-11)]

要素は、 `<input>` `<form>` `action` 属性が */Movies/Edit* URL にポストされるように設定されている HTML 要素に含まれています。 [ **編集** ] ボタンがクリックされると、フォームデータはサーバーにポストされます。

## <a name="processing-the-post-request"></a>POST 要求の処理

次のリストでは、`Edit` アクション メソッドの `HttpPost` バージョンを示します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

[ASP.NET MVC モデルバインダー](https://msdn.microsoft.com/magazine/hh781022.aspx)は、ポストされたフォーム値を取得し、 `Movie` パラメーターとして渡されるオブジェクトを作成し `movie` ます。 `ModelState.IsValid` メソッドは、フォームで送信されたデータを使って `Movie` オブジェクトを変更 (編集または更新) できることを検証します。 データが有効な場合、ムービーデータは `Movies` インスタンスのコレクションに保存され `db(MovieDBContext` ます)。 新しいムービーデータは、のメソッドを呼び出すことによってデータベースに保存され `SaveChanges` `MovieDBContext` ます。 データを保存すると、コードはクラスのアクションメソッドにユーザーをリダイレクトし `Index` ます。これには、直前に加えられた `MoviesController` 変更も含めて、ムービーコレクションのが表示されます。

ポストされた値が有効でない場合は、フォームに再登録されます。 `Html.ValidationMessageFor` *Edit. cshtml* view テンプレートのヘルパーは、適切なエラーメッセージを表示します。

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

> [!NOTE]
> 小数点にコンマ (,) を使用する英語以外のロケールの jQuery 検証をサポートするには、 &quot; &quot; *globalize.js* および特定の *カルチャ/globalize.cultures.js* ファイル (from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) と JavaScript を使用する必要があり `Globalize.parseFloat` ます。 次のコードは、fr-fr カルチャを操作するための Views\Movies\Edit.cshtml ファイルの変更を示してい &quot; &quot; ます。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

小数点のフィールドには、小数点ではなくコンマが必要になる場合があります。 一時的な解決策として、グローバリゼーション要素をプロジェクトのルート web.config ファイルに追加することができます。 次のコードは、カルチャが米国英語に設定されたグローバリゼーション要素を示しています。

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.xml)]

すべての `HttpGet` メソッドは同様のパターンに従います。 これらは、ムービーオブジェクト (またはの場合はオブジェクトの一覧) を取得 `Index` し、モデルをビューに渡します。 メソッドは、 `Create` 空のムービーオブジェクトを Create ビューに渡します。 データの作成、編集、削除、またはそれ以外の変更を行うすべてのメソッドは、メソッドの `HttpPost` のオーバーロードでそれを行います。 HTTP GET メソッドでのデータの変更は、セキュリティ上のリスクがあります。ブログ投稿「 [ASP.NET MVC Tip #46 –セキュリティホールを作成](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)するので、Delete リンクは使用しない」を参照してください。 GET メソッドでデータを変更することは、HTTP のベストプラクティスおよびアーキテクチャの [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) パターンにも違反します。これは、get 要求でアプリケーションの状態を変更しないことを指定します。 つまり、GET 操作の実行は、副作用がなく、永続化されたデータを変更しない、安全な操作である必要があります。

## <a name="adding-a-search-method-and-search-view"></a>検索メソッドと検索ビューの追加

このセクションで `SearchIndex` は、ジャンルまたは名前で映画を検索できるようにするアクションメソッドを追加します。 これは、 */Movies/SearchIndex* URL を使用して利用できます。 要求では、ムービーを検索するためにユーザーが入力できる入力要素を含む HTML フォームが表示されます。 ユーザーがフォームを送信すると、アクションメソッドはユーザーによって投稿された検索値を取得し、その値を使用してデータベースを検索します。

## <a name="displaying-the-searchindex-form"></a>SearchIndex フォームの表示

まず `SearchIndex` 、既存のクラスにアクションメソッドを追加し `MoviesController` ます。 メソッドは、HTML フォームを含むビューを返します。 コードは次のとおりです。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

メソッドの1行目では、 `SearchIndex` 次の [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) クエリを作成してムービーを選択します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cs)]

この時点でクエリが定義されていますが、データストアに対してまだ実行されていません。

パラメーターに `searchString` 文字列が含まれている場合は、次のコードを使用して、検索文字列の値をフィルター処理するようにムービークエリが変更されます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample11.cs)]

上の `s => s.Title` コードは[ラムダ式](https://msdn.microsoft.com/library/bb397687.aspx)です。 ラムダは、メソッドベースの [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) クエリで、上記のコードで使用される [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) メソッドなどの標準クエリ演算子メソッドの引数として使用されます。 LINQ クエリは、定義されている場合や、やなどのメソッドを呼び出すことによって変更された場合は実行されません `Where` `OrderBy` 。 代わりに、クエリの実行が遅延されます。つまり、式の評価は、その結果が実際に反復処理されるか、メソッドが呼び出されるまで遅延され [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) ます。 このサンプルでは、 `SearchIndex` クエリは SearchIndex ビューで実行されます。 クエリの遅延実行の詳細については、「[クエリの実行](https://msdn.microsoft.com/library/bb738633.aspx)」を参照してください。

これで、フォームを `SearchIndex` ユーザーに表示するビューを実装できるようになりました。 メソッド内を右クリックし、 `SearchIndex` [ **ビューの追加**] をクリックします。 [ **ビューの追加** ] ダイアログボックスで、 `Movie` モデルクラスとしてビューテンプレートにオブジェクトを渡すように指定します。 [ **スキャフォールディング template** ] の一覧で [ **list**] を選択し、[ **Add**] をクリックします。

![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image5.png)

[ **追加** ] ボタンをクリックすると、 *Views\Movies\SearchIndex.cshtml* view テンプレートが作成されます。 [**スキャフォールディング template** ] の一覧で [ **list** ] を選択したので、Visual Studio では、既定のマークアップがビューに自動的に生成されます (スキャフォールディング)。 スキャフォールディングによって HTML フォームが作成されました。 クラスを調べ、 `Movie` `<label>` クラスの各プロパティの要素をレンダリングするコードを作成しました。 次の一覧は、生成された Create ビューを示しています。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cshtml)]

アプリケーションを実行し、 */Movies/SearchIndex*に移動します。 `?searchString=ghost` などのクエリ文字列を URL に追加します。 フィルターされたムービーが表示されます。

![Searchqrキルギスタン r](examining-the-edit-methods-and-edit-view/_static/image6.png)

メソッドのシグネチャを `SearchIndex` 、という名前のパラメーターを持つように変更すると `id` 、 `id` パラメーターは `{id}` *global.asax* ファイルに設定されている既定のルートのプレースホルダーと一致します。

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample13.txt)]

元のメソッドは次のようになります。 `SearchIndex`

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cs)]

変更後のメソッドは次のように `SearchIndex` なります。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cs?highlight=1,3)]

これで、クエリ文字列の値ではなく、ルート データ (URL セグメント) として検索タイトルを渡すことができます。

![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image7.png)

ただし、ユーザーがムービーを検索するたびに URL の変更を求めることはできません。 ここで、ムービーをフィルター処理するための UI を追加します。 メソッドのシグネチャを変更して、 `SearchIndex` ルートバインド ID パラメーターを渡す方法をテストした場合は、 `SearchIndex` メソッドがという名前の文字列パラメーターを受け取るように、メソッドのシグネチャを変更し `searchString` ます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

*Views\Movies\SearchIndex.cshtml*ファイルを開き、の直後 `@Html.ActionLink("Create New", "Create")` に次のように追加します。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml?highlight=2)]

次の例では、フィルターマークアップが追加された *Views\Movies\SearchIndex.cshtml* ファイルの一部を示します。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cshtml?highlight=12-15)]

ヘルパーは、 `Html.BeginForm` 開始タグを作成し `<form>` ます。 ヘルパーを使うと、 `Html.BeginForm` ユーザーが [ **フィルター** ] ボタンをクリックしてフォームを送信したときに、フォームがポストされます。

アプリケーションを実行し、ムービーを検索します。

![](examining-the-edit-methods-and-edit-view/_static/image8.png)

`HttpPost`メソッドのオーバーロードはありません `SearchIndex` 。 メソッドはアプリケーションの状態を変更せず、データをフィルター処理するだけなので、必要ありません。

以下の `HttpPost SearchIndex` メソッドを追加できます。 この場合、アクション呼び出し元はメソッドと一致 `HttpPost SearchIndex` し、メソッドは次の図のように実行され `HttpPost SearchIndex` ます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image9.png)

ただし、この `HttpPost` バージョンの `SearchIndex` メソッドを追加しても、実装方法は制限されます。 たとえば、特定の検索をブックマークするか、友だちにリンクを送信し、友だちがそれをクリックしてムービーのフィルターされた同じリストを表示できるようにするとします。 HTTP POST 要求の URL は、GET 要求の URL (localhost: xxxxx/映画/SearchIndex) と同じであることに注意してください。 URL 自体には検索情報がありません。 現在、検索文字列の情報は、フォームフィールド値としてサーバーに送信されます。 つまり、URL でブックマークや友人に送信するために、その検索情報をキャプチャすることはできません。

この問題を解決するには、 `BeginForm` POST 要求で URL に検索情報を追加する必要があり、HttpGet バージョンのメソッドにルーティングする必要があることを指定するのオーバーロードを使用し `SearchIndex` ます。 既存のパラメーターなしの `BeginForm` メソッドを次のように置き換えます。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cshtml)]

![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

これで、検索を送信するときに、URL に検索クエリ文字列が含まれています。 `HttpPost SearchIndex` メソッドがある場合でも、検索時には `HttpGet SearchIndex` アクション メソッドにも移動します。

![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image11.png)

## <a name="adding-search-by-genre"></a>ジャンルによる検索の追加

メソッドのバージョンを追加した場合は `HttpPost` `SearchIndex` 、ここで削除します。

次に、ユーザーがジャンルで映画を検索できるようにする機能を追加します。 `SearchIndex` メソッドを次のコードに置き換えます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cs)]

このバージョンの `SearchIndex` メソッドは、追加のパラメーターを受け取り `movieGenre` ます。 最初の数行のコードでは、 `List` データベースからムービーのジャンルを保持するオブジェクトを作成します。

次のコードは、データベースからすべてのジャンルを取得する LINQ クエリです。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample22.cs)]

このコードでは、ジェネリックコレクションのメソッドを使用して、 `AddRange` `List` リストにすべての個別のジャンルを追加します。 (修飾子を指定しないと `Distinct` 、重複するジャンルが追加されます。たとえば、サンプルではコメディが2回追加されます)。 次に、このコードでは、オブジェクトにジャンルの一覧を格納し `ViewBag` ます。

次のコードは、パラメーターを確認する方法を示して `movieGenre` います。 空でない場合は、選択したムービーが指定したジャンルに限定されるように、ムービークエリがさらに制限されます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample23.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>ジャンルによる検索をサポートするために、SearchIndex ビューにマークアップを追加する

ヘルパーを `Html.DropDownList` ヘルパーの直前に *Views\Movies\SearchIndex.cshtml* ファイルに追加し `TextBox` ます。 完成したマークアップは次のようになります。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample24.cshtml?highlight=4)]

アプリケーションを実行し、 */Movies/SearchIndex*に移動します。 ジャンル、映画名、両方の条件で検索を試してみてください。

![](examining-the-edit-methods-and-edit-view/_static/image12.png)

このセクションでは、フレームワークによって生成される CRUD アクションメソッドとビューについて説明しました。 ユーザーがムービーのタイトルとジャンルで検索できるようにする検索アクションメソッドとビューを作成しました。 次のセクションでは、モデルにプロパティを追加する方法 `Movie` と、テストデータベースを自動的に作成する初期化子を追加する方法について説明します。

> [!div class="step-by-step"]
> [前へ](accessing-your-models-data-from-a-controller.md)
> [次へ](adding-a-new-field-to-the-movie-model-and-table.md)
