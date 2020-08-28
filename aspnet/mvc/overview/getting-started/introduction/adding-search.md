---
uid: mvc/overview/getting-started/introduction/adding-search
title: Search |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: be4e4d13e574b0fcb77d2d0fb8c6f58041b1ece2
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044928"
---
# <a name="search"></a>検索

[!INCLUDE [consider RP](~/includes/razor.md)]

## <a name="adding-a-search-method-and-search-view"></a>検索メソッドと検索ビューの追加

このセクションで `Index` は、ジャンルまたは名前で映画を検索できるように、アクションメソッドに検索機能を追加します。

## <a name="prerequisites"></a>前提条件

このセクションのスクリーンショットを照合するには、アプリケーション (F5) を実行し、次のムービーをデータベースに追加する必要があります。

| タイトル | リリース日 | Genre | 価格 |
| ----- | ------------ | ----- | ----- |
| Ghostbusters | 6/8/1984 | コメディ | 6.99 |
| Ghostbusters II | 6/16/1989 | コメディ | 6.99 |
| Apes | 3/27/1986 | アクション | 5.99 |

## <a name="updating-the-index-form"></a>インデックスフォームの更新

まず、 `Index` 既存のクラスにアクションメソッドを更新し `MoviesController` ます。 コードは次のとおりです。

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

メソッドの1行目では、 `Index` 次の [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) クエリを作成してムービーを選択します。

[!code-csharp[Main](adding-search/samples/sample2.cs)]

この時点でクエリが定義されていますが、データベースに対してまだ実行されていません。

パラメーターに `searchString` 文字列が含まれている場合は、次のコードを使用して、検索文字列の値をフィルター処理するようにムービークエリが変更されます。

[!code-csharp[Main](adding-search/samples/sample3.cs)]

上の `s => s.Title` コードは[ラムダ式](https://msdn.microsoft.com/library/bb397687.aspx)です。 ラムダは、メソッドベースの [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) クエリで、上記のコードで使用される [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) メソッドなどの標準クエリ演算子メソッドの引数として使用されます。 LINQ クエリは、定義されている場合や、やなどのメソッドを呼び出すことによって変更された場合は実行されません `Where` `OrderBy` 。 代わりに、クエリの実行が遅延されます。つまり、式の評価は、その結果が実際に反復処理されるか、メソッドが呼び出されるまで遅延され [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) ます。 この `Search` サンプルでは、クエリは、 *cshtml* ビューで実行されます。 クエリの遅延実行の詳細については、「[クエリの実行](https://msdn.microsoft.com/library/bb738633.aspx)」を参照してください。

> [!NOTE]
> [Contains](https://msdn.microsoft.com/library/bb155125.aspx)メソッドは、上記の c# コードではなく、データベースで実行されます。 データベースでは、には、大文字と小文字を区別しない[SQL のような](https://msdn.microsoft.com/library/ms179859.aspx)マップ[が含まれてい](https://msdn.microsoft.com/library/bb155125.aspx)ます。

これで、フォームを `Index` 表示するビューをユーザーに更新できるようになりました。

アプリケーションを実行し、 */Movies/Index*に移動します。 `?searchString=ghost` などのクエリ文字列を URL に追加します。 フィルターされたムービーが表示されます。

![Searchqrキルギスタン r](adding-search/_static/image1.png)

メソッドのシグネチャを `Index` 、という名前のパラメーターを持つように変更すると、パラメーターは、 `id` `id` `{id}` *App \_ Start\RouteConfig.cs* ファイルに設定されている既定のルートのプレースホルダーと一致します。

[!code-json[Main](adding-search/samples/sample4.txt)]

元のメソッドは次のようになります。 `Index`

[!code-csharp[Main](adding-search/samples/sample5.cs)]

変更後のメソッドは次のように `Index` なります。

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

これで、クエリ文字列の値ではなく、ルート データ (URL セグメント) として検索タイトルを渡すことができます。

![](adding-search/_static/image2.png)

ただし、ユーザーがムービーを検索するたびに URL の変更を求めることはできません。 そのため、ここでは UI を追加して、ムービーをフィルターできるようにします。 メソッドのシグネチャを変更して、 `Index` ルートバインド ID パラメーターを渡す方法をテストした場合は、 `Index` メソッドがという名前の文字列パラメーターを受け取るように、メソッドのシグネチャを変更し `searchString` ます。

[!code-csharp[Main](adding-search/samples/sample7.cs)]

*Views\Movies\Index.cshtml*ファイルを開き、の直後 `@Html.ActionLink("Create New", "Create")` に、下に強調表示されているフォームマークアップを追加します。

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

ヘルパーは、 `Html.BeginForm` 開始タグを作成し `<form>` ます。 ヘルパーを使うと、 `Html.BeginForm` ユーザーが [ **フィルター** ] ボタンをクリックしてフォームを送信したときに、フォームがポストされます。

ビューファイルを表示したり編集したりすると、Visual Studio 2013 の機能が向上します。 ビューファイルを開いた状態でアプリケーションを実行すると、Visual Studio 2013 によって正しいコントローラーアクションメソッドが呼び出され、ビューが表示されます。

![](adding-search/_static/image3.png)

(上の図に示されているように) Visual Studio でインデックスビューを開いた状態で、Ctr F5 キーまたは F5 キーをタップしてアプリケーションを実行し、ムービーを検索します。

![](adding-search/_static/image4.png)

`HttpPost`メソッドのオーバーロードはありません `Index` 。 メソッドはアプリケーションの状態を変更せず、データをフィルター処理するだけなので、必要ありません。

以下の `HttpPost Index` メソッドを追加できます。 この場合、アクション呼び出し元はメソッドと一致 `HttpPost Index` し、メソッドは次の図のように実行され `HttpPost Index` ます。

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

ただし、この `HttpPost` バージョンの `Index` メソッドを追加しても、実装方法は制限されます。 たとえば、特定の検索をブックマークするか、友だちにリンクを送信し、友だちがそれをクリックしてムービーのフィルターされた同じリストを表示できるようにするとします。 HTTP POST 要求の URL は、GET 要求の URL (localhost: xxxxx/映画/インデックス) と同じであることに注意してください。 URL 自体には検索情報がありません。 現在、検索文字列の情報は、フォームフィールド値としてサーバーに送信されます。 つまり、URL でブックマークや友人に送信するために、その検索情報をキャプチャすることはできません。

このソリューションでは、 `BeginForm` POST 要求で URL に検索情報を追加し、メソッドのバージョンにルーティングする必要があることを指定するのオーバーロードを使用し `HttpGet` `Index` ます。 既存のパラメーターなしの `BeginForm` メソッドを次のマークアップに置き換えます。

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

これで、検索を送信するときに、URL に検索クエリ文字列が含まれています。 `HttpPost Index` メソッドがある場合でも、検索時には `HttpGet Index` アクション メソッドにも移動します。

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a>ジャンルによる検索の追加

メソッドのバージョンを追加した場合は `HttpPost` `Index` 、ここで削除します。

次に、ユーザーがジャンルで映画を検索できるようにする機能を追加します。 `Index` メソッドを次のコードに置き換えます。

[!code-csharp[Main](adding-search/samples/sample11.cs)]

このバージョンの `Index` メソッドは、追加のパラメーターを受け取り `movieGenre` ます。 最初の数行のコードでは、 `List` データベースからムービーのジャンルを保持するオブジェクトを作成します。

次のコードは、データベースからすべてのジャンルを取得する LINQ クエリです。

[!code-csharp[Main](adding-search/samples/sample12.cs)]

このコードでは、ジェネリックコレクションのメソッドを使用して、 `AddRange` `List` リストにすべての個別のジャンルを追加します。 (修飾子を指定しないと `Distinct` 、重複するジャンルが追加されます。たとえば、サンプルではコメディが2回追加されます)。 次に、このコードでは、オブジェクトにジャンルの一覧を格納し `ViewBag.MovieGenre` ます。 カテゴリデータ (ムービーのジャンルなど) を内の [Selectlist](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) オブジェクトとして格納した `ViewBag` 後、ドロップダウンリストボックスでカテゴリデータにアクセスすることは、MVC アプリケーションの一般的な方法です。

次のコードは、パラメーターを確認する方法を示して `movieGenre` います。 空でない場合は、選択したムービーが指定したジャンルに限定されるように、ムービークエリがさらに制限されます。

[!code-csharp[Main](adding-search/samples/sample13.cs)]

前述のように、クエリは、ムービーリストが反復処理されるまで、データベースでは実行されません (アクションメソッドが返された後、ビューで発生し `Index` ます)。

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a>ジャンルによる検索をサポートするためにマークアップをインデックスビューに追加する

ヘルパーを `Html.DropDownList` ヘルパーの直前に *Views\Movies\Index.cshtml* ファイルに追加し `TextBox` ます。 完成したマークアップは次のようになります。

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

次のコードの内容は以下のとおりです。

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

パラメーター "Mo参照 Genre" は、でを検索するためのヘルパーのキーを提供し `DropDownList` `IEnumerable<SelectListItem>` `ViewBag` ます。 は、 `ViewBag` アクションメソッドで設定されました。

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

パラメーター "All" は、オプションラベルを提供します。 ブラウザーでその選択肢を調べると、"value" 属性が空であることがわかります。 コントローラーによってフィルター処理されるのは、 `if` 文字列がで `null` も空でもないため、空の値を送信するとすべてのジャンルが表示され `movieGenre` ます。

オプションを既定で選択するように設定することもできます。 既定のオプションとして "コメディ" が必要な場合は、コントローラーのコードを次のように変更します。

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

アプリケーションを実行し、 */Movies/Index*に移動します。 ジャンル、映画名、両方の条件で検索を試してみてください。

![](adding-search/_static/image8.png)

このセクションでは、ユーザーがムービーのタイトルとジャンルで検索できるようにする検索アクションメソッドとビューを作成しました。 次のセクションでは、モデルにプロパティを追加する方法 `Movie` と、テストデータベースを自動的に作成する初期化子を追加する方法について説明します。

> [!div class="step-by-step"]
> [前へ](examining-the-edit-methods-and-edit-view.md)
> [次へ](adding-a-new-field.md)
