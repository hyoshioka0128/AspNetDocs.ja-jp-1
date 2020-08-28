---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: Edit メソッドと Edit ビューを調べるMicrosoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 1894971430c4febee19f095373411ed319edc015
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045209"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>Edit メソッドと Edit ビューの確認

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

このセクションでは、ムービーコントローラーに対して生成された `Edit` アクションメソッドとビューを確認します。 しかし、最初に、リリース日の見栄えを良くするために、短い diversion を行います。 *Modelthe modelfile*を開き、次に示す強調表示された行を追加します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

次のように、日付カルチャを指定することもできます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) については、次のチュートリアルで説明します。 [Display](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayattribute.aspx) 属性は、フィールドの名前として表示する内容 (ここでは、"ReleaseDate" ではなく、"Release Date") を指定します。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性はデータの型 (この場合は日付) を指定するため、フィールドに格納される時刻情報は表示されません。 [Displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性は、日付形式が正しく表示されない、Chrome ブラウザーのバグに必要です。

アプリケーションを実行し、コントローラーを参照し `Movies` ます。 **編集**リンクの上にマウスポインターを置くと、リンク先の URL が表示されます。

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

**Edit**リンクは、 `Html.ActionLink` *Views\Movies\Index.cshtml*ビューのメソッドによって生成されました。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![Html.actionlink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`オブジェクトは、 [System.web. Mvc. WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx)基本クラスのプロパティを使用して公開されるヘルパーです。 `ActionLink`ヘルパーのメソッドを使用すると、コントローラーのアクションメソッドにリンクする HTML ハイパーリンクを簡単に動的に生成できます。 メソッドの最初の引数 `ActionLink` は、表示するリンクテキスト (など `<a>Edit Me</a>` ) です。 2番目の引数は、呼び出すアクションメソッドの名前 (この場合は `Edit` アクション) です。 最後の引数は、ルートデータ (この場合は4の ID) を生成する [匿名オブジェクト](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) です。

前の図に示すように、生成されたリンクは `http://localhost:1234/Movies/Edit/4` です。 既定のルート ( *App \_ Start\RouteConfig.cs*で確立されます) は、URL パターンを受け取り `{controller}/{action}/{id}` ます。 したがって、ASP.NET は、 `http://localhost:1234/Movies/Edit/4` `Edit` `Movies` パラメーターが4に等しいコントローラーのアクションメソッドへの要求に変換し `ID` ます。 *App \_ Start\RouteConfig.cs*ファイルから次のコードを確認します。 [Maproute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md)メソッドは、HTTP 要求を適切なコントローラーとアクションメソッドにルーティングし、オプションの ID パラメーターを指定するために使用されます。 [Maproute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md)メソッドは、 [HtmlHelpers](https://msdn.microsoft.com/library/system.web.mvc.htmlhelper(v=vs.108).aspx) `ActionLink` コントローラー、アクションメソッド、およびルートデータに指定された url を生成するために、などの htmlhelpers によっても使用されます。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

クエリ文字列を使用して、アクションメソッドのパラメーターを渡すこともできます。 たとえば、URL は、 `http://localhost:1234/Movies/Edit?ID=3` `ID` コントローラーのアクションメソッドに3のパラメーターも渡し `Edit` `Movies` ます。

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

コントローラーを開き `Movies` ます。 2つの `Edit` アクションメソッドを次に示します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

2 番目の `Edit` アクション メソッドの前に `HttpPost` 属性が付いていることに注意してください。 この属性は、メソッドのオーバーロードを `Edit` POST 要求に対してのみ呼び出すことができるように指定します。 `HttpGet`最初の編集メソッドに属性を適用することもできますが、これは既定値なので必要ありません。 (メソッドとして暗黙的に属性を割り当てられるアクションメソッドを参照し `HttpGet` `HttpGet` ます)。 [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) 属性は、ハッカーがモデルにデータを過剰に送信することを防ぐ、もう1つの重要なセキュリティメカニズムです。 プロパティは、変更するバインド属性にのみ含める必要があります。 過剰投稿とバインドの属性については、「 [過剰投稿のセキュリティ](https://go.microsoft.com/fwlink/?LinkId=317598)に関するメモ」を参照してください。 このチュートリアルで使用する単純なモデルでは、モデル内のすべてのデータをバインドします。 [Validateアンチ Forgerytoken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx)属性は、要求の偽造を防止するために使用され、 `@Html.AntiForgeryToken()` 編集ビューファイル (*Views\Movies\Edit.cshtml*) でとペアになっています。部分を以下に示します。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

`@Html.AntiForgeryToken()` コントローラーのメソッドで一致する必要がある非表示の偽造防止トークンを生成し `Edit` `Movies` ます。 クロスサイト要求の偽造 (XSRF または CSRF とも呼ばれます) の詳細については、「チュートリアル [XSRF/Csrf 防止 (MVC](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md))」を参照してください。

`HttpGet` `Edit` メソッドはムービー ID パラメーターを受け取り、Entity Framework メソッドを使用してムービーを検索 `Find` し、選択したムービーを編集ビューに返します。 ムービーが見つからない場合は、 [HttpNotFound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) が返されます。 スキャフォールディング システムが編集ビューを作成したときは、そのシステムが `Movie` クラスを調べて、クラスの各プロパティの `<label>` および `<input>` 要素をレンダリングするコードを作成しました。 次の例は、visual studio のスキャフォールディングシステムによって生成された編集ビューを示しています。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

ビューテンプレートにファイルの先頭にステートメントが含まれていることに注意して `@model MvcMovie.Models.Movie` ください。これは、ビューがビューテンプレートのモデルを型と想定していることを示し `Movie` ます。

スキャフォールディングコードでは、HTML マークアップを効率化するためにいくつかの *ヘルパーメソッド* を使用しています。 ヘルパーには、 [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx) フィールドの名前 ( &quot; Title &quot; 、 &quot; releasedate &quot; 、 &quot; Genre &quot; 、または &quot; Price &quot; ) が表示されます。 ヘルパーは、 [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) HTML 要素をレンダリングし `<input>` ます。 ヘルパーには、 [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) そのプロパティに関連付けられている検証メッセージが表示されます。

アプリケーションを実行し、 */ムービー* の URL に移動します。 **[編集]** リンクをクリックします。 ブラウザーで、ページのソースを表示します。 Form 要素の HTML を次に示します。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

要素は、 `<input>` `<form>` `action` 属性が */Movies/Edit* URL にポストされるように設定されている HTML 要素に含まれています。 フォームデータは、[ **保存** ] ボタンをクリックするとサーバーにポストされます。 2行目は、呼び出しによって生成された非表示の [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) トークンを示して `@Html.AntiForgeryToken()` います。

## <a name="processing-the-post-request"></a>POST 要求の処理

次のリストでは、`Edit` アクション メソッドの `HttpPost` バージョンを示します。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

[Validateアンチ Forgerytoken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx)属性は、ビューでの呼び出しによって生成された[XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)トークンを検証し `@Html.AntiForgeryToken()` ます。

[ASP.NET MVC モデルバインダー](https://msdn.microsoft.com/library/dd410405.aspx)は、ポストされたフォーム値を取得し、 `Movie` パラメーターとして渡されるオブジェクトを作成し `movie` ます。 は、フォームで送信されたデータを使用して `ModelState.IsValid` オブジェクトの変更 (編集または更新) を行うことができるかどうかを確認し `Movie` ます。 データが有効な場合、ムービーデータは `Movies` (インスタンス) のコレクションに保存され `db` `MovieDBContext` ます。 新しいムービーデータは、のメソッドを呼び出すことによってデータベースに保存され `SaveChanges` `MovieDBContext` ます。 データを保存した後、コードはユーザーを `MoviesController` クラスの `Index` アクション メソッドにリダイレクトします。そこでは、行われたばかりの変更を含むムービー コレクションが表示されます。

クライアント側の検証によってフィールドの値が無効であると判断されるとすぐに、エラーメッセージが表示されます。 JavaScript が無効になっている場合、クライアント側の検証は無効になります。 ただし、ポストされた値が無効であることがサーバーによって検出され、フォームの値がエラーメッセージと共に再登録されます。

検証の詳細については、チュートリアルの後半で詳しく説明します。

`Html.ValidationMessageFor` *Edit. cshtml* view テンプレートのヘルパーは、適切なエラーメッセージを表示します。

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

すべての `HttpGet` メソッドは同様のパターンに従います。 これらは、ムービーオブジェクト (またはの場合はオブジェクトの一覧) を取得 `Index` し、モデルをビューに渡します。 メソッドは、 `Create` 空のムービーオブジェクトを Create ビューに渡します。 データの作成、編集、削除、またはそれ以外の変更を行うすべてのメソッドは、メソッドの `HttpPost` のオーバーロードでそれを行います。 HTTP GET メソッドでのデータの変更は、セキュリティ上のリスクがあります。ブログ投稿「 [ASP.NET MVC Tip #46 –セキュリティホールを作成](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)するので、Delete リンクは使用しない」を参照してください。 GET メソッドでデータを変更することは、HTTP のベストプラクティスおよびアーキテクチャの [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) パターンにも違反します。これは、get 要求でアプリケーションの状態を変更しないことを指定します。 つまり、GET 操作の実行は、副作用がなく、永続化されたデータを変更しない、安全な操作である必要があります。

## <a name="jquery-validation-for-non-english-locales"></a>英語以外のロケールの jQuery 検証

米国英語版のコンピューターを使用している場合は、このセクションを省略して次のチュートリアルに進むことができます。 このチュートリアルのグローバライズバージョンは、 [こちら](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475)からダウンロードできます。 国際化に関する優れた2部構成のチュートリアルについては、「 [Nadeem's ASP.NET MVC 5 国際化](http://afana.me/post/aspnet-mvc-internationalization.aspx)」を参照してください。

> [!NOTE]
> 小数点にコンマ (,) を使用し、英語 (米国) 以外の日付形式を使用する英語以外のロケールの jQuery 検証をサポートするには、 &quot; &quot; *globalize.js* および特定の *カルチャ/globalize.cultures.js* ファイル (from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) と JavaScript を使用する必要があり `Globalize.parseFloat` ます。 JQuery の英語以外の検証は NuGet から取得できます。 (英語ロケールを使用している場合は、グローバライズをインストールしないでください)。

1. [ **ツール** ] メニューの [ **nuget パッケージマネージャー**] をクリックし、[ **ソリューションの nuget パッケージの管理**] をクリックします。

    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. 左側のウィンドウで、[参照] を選択し<strong>*ます。</strong> *(下の画像を参照してください)。
3. 入力ボックスに「* グローバライズ * *」と入力します。

    ![](examining-the-edit-methods-and-edit-view/_static/image6.png) を選択し `jQuery.Validation.Globalize` 、 `MvcMovie` [ **インストール**] をクリックします。 *Scripts\jquery.globalize\globalize.js*ファイルがプロジェクトに追加されます。 * スクリプト \ Jquery. Globalize\ \* culture フォルダーには、多くのカルチャ JavaScript ファイルが含まれます。 このパッケージのインストールには5分かかる場合があります。

   次のコードは、Views\Movies\Edit.cshtml ファイルに対する変更を示しています。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

すべての編集ビューでこのコードが繰り返されないようにするには、レイアウトファイルに移動します。 スクリプトのダウンロードを最適化するには、「my チュートリアルの [バンドルと縮小](../../performance/bundling-and-minification.md)」を参照してください。

詳細については、「 [ASP.NET mvc 3 国際化](http://afana.me/post/aspnet-mvc-internationalization.aspx) AND [ASP.NET mvc 3 国際化-パート 2 ()](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx)」を参照してください。

一時的な解決策として、ロケールでの検証作業ができない場合は、コンピューターで英語 (米国) を使用するように強制するか、ブラウザーで JavaScript を無効にすることができます。 コンピューターで英語 (米国) を使用するようにするには、グローバリゼーション要素をプロジェクトのルート *web.config* ファイルに追加します。 次のコードは、カルチャが米国英語に設定されたグローバリゼーション要素を示しています。

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><a id="jQueryAjaxJSON"></a> 次のチュートリアルでは、検索機能を実装します。

> [!div class="step-by-step"]
> [前へ](accessing-your-models-data-from-a-controller.md)
> [次へ](adding-search.md)
