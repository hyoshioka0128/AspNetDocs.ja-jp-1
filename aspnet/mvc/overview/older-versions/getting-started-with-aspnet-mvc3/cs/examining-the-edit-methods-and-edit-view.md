---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
title: Edit メソッドと Edit ビューの確認 (C#) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 1d266bf0-a61e-423b-a3d2-13773d7dafe2
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: baa300c66bfae9fe602a8fe597e21b0abbaf3a63
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044988"
---
# <a name="examining-the-edit-methods-and-edit-view-c"></a>Edit メソッドと Edit ビューの確認 (C#)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する [こちらで](../../../getting-started/introduction/getting-started.md) 入手できます。 より安全で、より簡単にフォローし、より多くの機能を紹介します。
> 
> 
> このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。 または、次のリンクを使用して、前提条件を個別にインストールすることもできます。
> 
> - [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)
> 
> Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> このトピックでは、C# ソースコードを含む Visual Web Developer プロジェクトを使用できます。 [C# バージョンをダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。 Visual Basic を希望する場合は、このチュートリアルの [Visual Basic バージョン](../vb/intro-to-aspnet-mvc-3.md) に切り替えてください。

このセクションでは、ムービーコントローラーに対して生成されたアクションメソッドとビューを確認します。 次に、カスタム検索ページを追加します。

アプリケーションを実行し、 `Movies` ブラウザーのアドレスバーの URL に */ムービー* を追加して、コントローラーを参照します。 **編集**リンクの上にマウスポインターを置くと、リンク先の URL が表示されます。

[![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image2.png)](examining-the-edit-methods-and-edit-view/_static/image1.png)

**Edit**リンクは、 `Html.ActionLink` *Views\Movies\Index.cshtml*ビューのメソッドによって生成されました。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

[![Html.actionlink](examining-the-edit-methods-and-edit-view/_static/image4.png)](examining-the-edit-methods-and-edit-view/_static/image3.png)

`Html`オブジェクトは、基底クラスのプロパティを使用して公開されるヘルパーです `WebViewPage` 。 `ActionLink`ヘルパーのメソッドを使用すると、コントローラーのアクションメソッドにリンクする HTML ハイパーリンクを簡単に動的に生成できます。 メソッドの最初の引数 `ActionLink` は、表示するリンクテキスト (など `<a>Edit Me</a>` ) です。 2番目の引数は、呼び出すアクションメソッドの名前です。 最後の引数は、ルートデータ (この場合は4の ID) を生成する [匿名オブジェクト](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) です。

前の図に示すように、生成されたリンクは `http://localhost:xxxxx/Movies/Edit/4` です。 既定のルートは、URL パターンを受け取り `{controller}/{action}/{id}` ます。 したがって、ASP.NET は、 `http://localhost:xxxxx/Movies/Edit/4` `Edit` `Movies` パラメーターが4に等しいコントローラーのアクションメソッドへの要求に変換し `ID` ます。

クエリ文字列を使用して、アクションメソッドのパラメーターを渡すこともできます。 たとえば、URL は、 `http://localhost:xxxxx/Movies/Edit?ID=4` `ID` コントローラーのアクションメソッドに4のパラメーターも渡し `Edit` `Movies` ます。

[![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image6.png)](examining-the-edit-methods-and-edit-view/_static/image5.png)

コントローラーを開き `Movies` ます。 2つの `Edit` アクションメソッドを次に示します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

2 番目の `Edit` アクション メソッドの前に `HttpPost` 属性が付いていることに注意してください。 この属性は、メソッドのオーバーロードを `Edit` POST 要求に対してのみ呼び出すことができるように指定します。 `HttpGet`最初の編集メソッドに属性を適用することもできますが、これは既定値なので必要ありません。 (メソッドとして暗黙的に属性を割り当てられるアクションメソッドを参照し `HttpGet` `HttpGet` ます)。

`HttpGet` `Edit` メソッドはムービー ID パラメーターを受け取り、Entity Framework メソッドを使用してムービーを検索 `Find` し、選択したムービーを編集ビューに返します。 スキャフォールディング システムが編集ビューを作成したときは、そのシステムが `Movie` クラスを調べて、クラスの各プロパティの `<label>` および `<input>` 要素をレンダリングするコードを作成しました。 次の例は、生成された編集ビューを示しています。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

ビューテンプレートにファイルの先頭にステートメントが含まれていることに注意して `@model MvcMovie.Models.Movie` ください。これは、ビューがビューテンプレートのモデルを型と想定していることを示し `Movie` ます。

スキャフォールディングコードでは、HTML マークアップを効率化するためにいくつかの *ヘルパーメソッド* を使用しています。 ヘルパーには、 [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx) フィールドの名前 ("Title"、"ReleaseDate"、"Genre"、または "Price") が表示されます。 ヘルパーは、 [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) HTML 要素を表示し `<input>` ます。 ヘルパーには、 [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) そのプロパティに関連付けられている検証メッセージが表示されます。

アプリケーションを実行し、 */ムービー* の URL に移動します。 **[編集]** リンクをクリックします。 ブラウザーで、ページのソースを表示します。 ページの HTML は次の例のようになります。 (わかりやすくするためにメニューマークアップが除外されました)。

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample4.html)]

要素は、 `<input>` `<form>` `action` 属性が */Movies/Edit* URL にポストされるように設定されている HTML 要素に含まれています。 [ **編集** ] ボタンがクリックされると、フォームデータはサーバーにポストされます。

## <a name="processing-the-post-request"></a>POST 要求の処理

次のリストでは、`Edit` アクション メソッドの `HttpPost` バージョンを示します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs)]

ASP.NET framework モデルバインダーは、ポストされたフォーム値を取得し、 `Movie` パラメーターとして渡されるオブジェクトを作成し `movie` ます。 コードをチェックインすると、フォームで送信されたデータを使用して `ModelState.IsValid` オブジェクトを変更できるかどうかが確認され `Movie` ます。 データが有効な場合は、コードによって、ムービーデータがインスタンスのコレクションに保存され `Movies` `MovieDBContext` ます。 次に、のメソッドを呼び出して新しいムービーデータをデータベースに保存し `SaveChanges` `MovieDBContext` ます。これにより、データベースへの変更が保持されます。 データを保存した後、コードはクラスのアクションメソッドにユーザーをリダイレクトし `Index` `MoviesController` ます。これにより、更新されたムービーがムービーの一覧に表示されます。

ポストされた値が有効でない場合は、フォームに再登録されます。 `Html.ValidationMessageFor` *Edit. cshtml* view テンプレートのヘルパーは、適切なエラーメッセージを表示します。

[![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image8.png)](examining-the-edit-methods-and-edit-view/_static/image7.png)

> **ロケールに関する注意事項**通常、英語以外のロケールを使用する場合は、「[英語以外のロケールでの ASP.NET MVC 3 検証のサポート](https://msdn.microsoft.com/library/gg674880(VS.98).aspx)」を参照してください。

## <a name="making-the-edit-method-more-robust"></a>Edit メソッドの堅牢性を高める

`HttpGet` `Edit` スキャフォールディングシステムによって生成されたメソッドは、渡された ID が有効であるかどうかをチェックしません。 ユーザーが URL () から ID セグメントを削除すると、 `http://localhost:xxxxx/Movies/Edit` 次のエラーが表示されます。

[![Null_ID](examining-the-edit-methods-and-edit-view/_static/image10.png)](examining-the-edit-methods-and-edit-view/_static/image9.png)

ユーザーは、データベースに存在しない ID (など) を渡すこともでき `http://localhost:xxxxx/Movies/Edit/1234` ます。 `HttpGet` `Edit` この制限に対処するために、アクションメソッドに2つの変更を加えることができます。 最初に、 `ID` ID が明示的に渡されない場合は、パラメーターを既定値の0に変更します。 また、 `Find` ムービーオブジェクトをビューテンプレートに返す前に、メソッドが実際にムービーを見つけたかどうかを確認することもできます。 更新された `Edit` メソッドを次に示します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

ムービーが見つからない場合は、 `HttpNotFound` メソッドが呼び出されます。

すべての `HttpGet` メソッドは同様のパターンに従います。 これらは、ムービーオブジェクト (またはの場合はオブジェクトの一覧) を取得 `Index` し、モデルをビューに渡します。 メソッドは、 `Create` 空のムービーオブジェクトを Create ビューに渡します。 データの作成、編集、削除、またはそれ以外の変更を行うすべてのメソッドは、メソッドの `HttpPost` のオーバーロードでそれを行います。 HTTP GET メソッドでのデータの変更は、セキュリティ上のリスクがあります。ブログ投稿「 [ASP.NET MVC Tip #46 –セキュリティホールを作成](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)するので、Delete リンクは使用しない」を参照してください。 GET メソッドでデータを変更することは、HTTP のベストプラクティスおよびアーキテクチャの REST パターンにも違反します。これは、GET 要求でアプリケーションの状態を変更しないことを指定します。 言い換えると、GET 操作の実行は、副作用のない安全な操作である必要があります。

## <a name="adding-a-search-method-and-search-view"></a>検索メソッドと検索ビューの追加

このセクションで `SearchIndex` は、ジャンルまたは名前で映画を検索できるようにするアクションメソッドを追加します。 これは、 */Movies/SearchIndex* URL を使用して利用できます。 要求では、ムービーを検索するためにユーザーが入力できる入力要素を含む HTML フォームが表示されます。 ユーザーがフォームを送信すると、アクションメソッドはユーザーによって投稿された検索値を取得し、その値を使用してデータベースを検索します。

## <a name="displaying-the-searchindex-form"></a>SearchIndex フォームの表示

まず `SearchIndex` 、既存のクラスにアクションメソッドを追加し `MoviesController` ます。 メソッドは、HTML フォームを含むビューを返します。 コードは次のとおりです。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cs)]

メソッドの1行目では、 `SearchIndex` 次の [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) クエリを作成してムービーを選択します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cs)]

この時点でクエリが定義されていますが、データストアに対してまだ実行されていません。

パラメーターに `searchString` 文字列が含まれている場合は、次のコードを使用して、検索文字列の値をフィルター処理するようにムービークエリが変更されます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

LINQ クエリは、定義されている場合や、やなどのメソッドを呼び出すことによって変更された場合は実行されません `Where` `OrderBy` 。 代わりに、クエリの実行が遅延されます。つまり、式の評価は、その結果が実際に反復処理されるか、メソッドが呼び出されるまで遅延され [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) ます。 このサンプルでは、 `SearchIndex` クエリは SearchIndex ビューで実行されます。 クエリの遅延実行の詳細については、「[クエリの実行](https://msdn.microsoft.com/library/bb738633.aspx)」を参照してください。

これで、フォームを `SearchIndex` ユーザーに表示するビューを実装できるようになりました。 メソッド内を右クリックし、 `SearchIndex` [ **ビューの追加**] をクリックします。 [ **ビューの追加** ] ダイアログボックスで、 `Movie` モデルクラスとしてビューテンプレートにオブジェクトを渡すように指定します。 [ **スキャフォールディング template** ] の一覧で [ **list**] を選択し、[ **Add**] をクリックします。

[![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image12.png)](examining-the-edit-methods-and-edit-view/_static/image11.png)

[ **追加** ] ボタンをクリックすると、 *Views\Movies\SearchIndex.cshtml* view テンプレートが作成されます。 [**スキャフォールディング template** ] の一覧で [ **list** ] を選択したので、Visual Web Developer はビューの一部の既定のコンテンツを自動的に生成 (スキャフォールディング) します。 スキャフォールディングによって HTML フォームが作成されました。 クラスを調べ、 `Movie` `<label>` クラスの各プロパティの要素をレンダリングするコードを作成しました。 次の一覧は、生成された Create ビューを示しています。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

アプリケーションを実行し、 */Movies/SearchIndex*に移動します。 `?searchString=ghost` などのクエリ文字列を URL に追加します。 フィルターされたムービーが表示されます。

[![Searchqrキルギスタン r](examining-the-edit-methods-and-edit-view/_static/image14.png)](examining-the-edit-methods-and-edit-view/_static/image13.png)

メソッドのシグネチャを `SearchIndex` 、という名前のパラメーターを持つように変更すると `id` 、 `id` パラメーターは `{id}` *global.asax* ファイルに設定されている既定のルートのプレースホルダーと一致します。

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample11.txt)]

変更後のメソッドは次のように `SearchIndex` なります。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cs)]

これで、クエリ文字列の値ではなく、ルート データ (URL セグメント) として検索タイトルを渡すことができます。

[![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image16.png)](examining-the-edit-methods-and-edit-view/_static/image15.png)

ただし、ユーザーがムービーを検索するたびに URL の変更を求めることはできません。 ここで、ムービーをフィルター処理するための UI を追加します。 メソッドのシグネチャを変更して、 `SearchIndex` ルートバインド ID パラメーターを渡す方法をテストした場合は、 `SearchIndex` メソッドがという名前の文字列パラメーターを受け取るように、メソッドのシグネチャを変更し `searchString` ます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample13.cs)]

*Views\Movies\SearchIndex.cshtml*ファイルを開き、の直後 `@Html.ActionLink("Create New", "Create")` に次のように追加します。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cshtml)]

次の例では、フィルターマークアップが追加された *Views\Movies\SearchIndex.cshtml* ファイルの一部を示します。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cshtml)]

ヘルパーは、 `Html.BeginForm` 開始タグを作成し `<form>` ます。 ヘルパーを使うと、 `Html.BeginForm` ユーザーが [ **フィルター** ] ボタンをクリックしてフォームを送信したときに、フォームがポストされます。

アプリケーションを実行し、ムービーを検索します。

[![SearchIndxIE9_title](examining-the-edit-methods-and-edit-view/_static/image18.png)](examining-the-edit-methods-and-edit-view/_static/image17.png)

`HttpPost`メソッドのオーバーロードはありません `SearchIndex` 。 メソッドはアプリケーションの状態を変更せず、データをフィルター処理するだけなので、必要ありません。

以下の `HttpPost SearchIndex` メソッドを追加できます。 この場合、アクション呼び出し元はメソッドと一致 `HttpPost SearchIndex` し、メソッドは次の図のように実行され `HttpPost SearchIndex` ます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

[![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image20.png)](examining-the-edit-methods-and-edit-view/_static/image19.png)

ただし、この `HttpPost` バージョンの `SearchIndex` メソッドを追加しても、実装方法は制限されます。 たとえば、特定の検索をブックマークするか、友だちにリンクを送信し、友だちがそれをクリックしてムービーのフィルターされた同じリストを表示できるようにするとします。 HTTP POST 要求の URL は、GET 要求の URL (localhost: xxxxx/映画/SearchIndex) と同じであることに注意してください。 URL 自体には検索情報がありません。 現在、検索文字列の情報は、フォームフィールド値としてサーバーに送信されます。 つまり、URL でブックマークや友人に送信するために、その検索情報をキャプチャすることはできません。

この問題を解決するには、 `BeginForm` POST 要求で URL に検索情報を追加する必要があり、HttpGet バージョンのメソッドにルーティングする必要があることを指定するのオーバーロードを使用し `SearchIndex` ます。 既存のパラメーターなしの `BeginForm` メソッドを次のように置き換えます。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml)]

[![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image22.png)](examining-the-edit-methods-and-edit-view/_static/image21.png)

これで、検索を送信するときに、URL に検索クエリ文字列が含まれています。 `HttpPost SearchIndex` メソッドがある場合でも、検索時には `HttpGet SearchIndex` アクション メソッドにも移動します。

[![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image24.png)](examining-the-edit-methods-and-edit-view/_static/image23.png)

## <a name="adding-search-by-genre"></a>ジャンルによる検索の追加

メソッドのバージョンを追加した場合は `HttpPost` `SearchIndex` 、ここで削除します。

次に、ユーザーがジャンルで映画を検索できるようにする機能を追加します。 `SearchIndex` メソッドを次のコードに置き換えます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cs)]

このバージョンの `SearchIndex` メソッドは、追加のパラメーターを受け取り `movieGenre` ます。 最初の数行のコードでは、 `List` データベースからムービーのジャンルを保持するオブジェクトを作成します。

次のコードは、データベースからすべてのジャンルを取得する LINQ クエリです。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

このコードでは、ジェネリックコレクションのメソッドを使用して、 `AddRange` `List` リストにすべての個別のジャンルを追加します。 (修飾子を指定しないと `Distinct` 、重複するジャンルが追加されます。たとえば、サンプルではコメディが2回追加されます)。 次に、このコードでは、オブジェクトにジャンルの一覧を格納し `ViewBag` ます。

次のコードは、パラメーターを確認する方法を示して `movieGenre` います。 空でない場合は、選択したムービーを指定されたジャンルだけに制限するように、ムービークエリをさらに制約します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>ジャンルによる検索をサポートするために、SearchIndex ビューにマークアップを追加する

ヘルパーを `Html.DropDownList` ヘルパーの直前に *Views\Movies\SearchIndex.cshtml* ファイルに追加し `TextBox` ます。 完成したマークアップは次のようになります。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cshtml)]

アプリケーションを実行し、 */Movies/SearchIndex*に移動します。 ジャンル、映画名、両方の条件で検索を試してみてください。

このセクションでは、フレームワークによって生成される CRUD アクションメソッドとビューについて説明しました。 ユーザーがムービーのタイトルとジャンルで検索できるようにする検索アクションメソッドとビューを作成しました。 次のセクションでは、モデルにプロパティを追加する方法 `Movie` と、テストデータベースを自動的に作成する初期化子を追加する方法について説明します。

> [!div class="step-by-step"]
> [前へ](accessing-your-models-data-from-a-controller.md)
> [次へ](adding-a-new-field.md)
