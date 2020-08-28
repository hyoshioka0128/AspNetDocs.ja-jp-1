---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: ASP.NET Web API 2 | で属性ルーティングを使用して REST API を作成します。Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: f6ff5fa18a44b3e6717ec0141ebe101bcdc0bee4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045183"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 で属性ルーティングを使用して REST API を作成する

[Mike Wasson](https://github.com/MikeWasson)

Web API 2 では、 *属性ルーティング*と呼ばれる新しい種類のルーティングがサポートされています。 属性ルーティングの一般的な概要については、「 [WEB API 2 での属性ルーティング](attribute-routing-in-web-api-2.md)」を参照してください。 このチュートリアルでは、属性ルーティングを使用して、書籍のコレクションの REST API を作成します。 API は、次のアクションをサポートします。

| アクション | URI の例 |
| --- | --- |
| すべての本の一覧を取得します。 | /api/books |
| ID でブックを取得します。 | /api/books/1 |
| ブックの詳細を取得します。 | 詳細情報 (& s) |
| ジャンル別の書籍の一覧を取得します。 | /api/books/fantasy |
| 出版日別の書籍の一覧を取得します。 | /api02-16/api/books/date/2013/02/16 (代替形式) (& 3) |
| 特定の作成者による書籍の一覧を取得します。 | ///ブック (& s) |

すべてのメソッドは読み取り専用 (HTTP GET 要求) です。

データ層については、Entity Framework を使用します。 書籍のレコードには、次のフィールドがあります。

- ID
- タイトル
- Genre
- 公開日
- 価格
- 説明
- AuthorID (Authors テーブルへの外部キー)

ただし、ほとんどの要求では、このデータのサブセット (タイトル、作成者、ジャンル) が返されます。 完全なレコードを取得するために、クライアントはを要求し `/api/books/{id}/details` ます。

## <a name="prerequisites"></a>前提条件

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community、Professional、または Enterprise edition。

## <a name="create-the-visual-studio-project"></a>Visual Studio プロジェクトを作成する

Visual Studio の実行から始めます。 **[ファイル]** メニューの **[新規作成]** を選択し、**[プロジェクト]** を選択します。

[**インストールされている**  >  **Visual C#** ] カテゴリを展開します。 [ **Visual C#**] で、[ **Web**] を選択します。 プロジェクトテンプレートの一覧で、[ **ASP.NET Web Application (.NET Framework)**] を選択します。 プロジェクトに「booksapi」という名前を指定 &quot; &quot; します。

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

[ **New ASP.NET Web Application** ] ダイアログボックスで、 **空** のテンプレートを選択します。 [フォルダーとコア参照の追加] で、[ **WEB API** ] チェックボックスをオンにします。 **[OK]** をクリックします。

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

これにより、Web API 機能用に構成されたスケルトンプロジェクトが作成されます。

### <a name="domain-models"></a>ドメインモデル

次に、ドメインモデルのクラスを追加します。 ソリューション エクスプローラーで、[モデル] フォルダーを右クリックします。 [ **追加**] を選択し、[ **クラス**] を選択します。 クラスに `Author` という名前を付けます。

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

Author.cs のコードを次のコードに置き換えます。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

次に、という名前の別のクラス `Book` を追加します。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a>Web API コントローラーを追加する

この手順では、データ層として Entity Framework を使用する Web API コントローラーを追加します。

Ctrl キーと Shift キーを押しながら B キーを押して、プロジェクトをビルドします。 Entity Framework は、リフレクションを使用してモデルのプロパティを検出します。そのため、データベーススキーマを作成するには、コンパイル済みのアセンブリが必要です。

ソリューション エクスプローラーで、[コントローラー] フォルダーを右クリックします。 [ **追加**] を選択し、[ **コントローラー**] を選択します。

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

[ **スキャフォールディングの追加** ] ダイアログボックスで、[ **アクションを含む Web API 2 コントローラー**] を選択し Entity Framework を使用します。

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

[ **コントローラーの追加** ] ダイアログボックスで、[ **コントローラー名**] に「bookscontroller」と入力し &quot; &quot; ます。 [ &quot; 非同期コントローラーアクションを使用する] チェックボックスをオンにし &quot; ます。 [ **モデルクラス**] で [Book] を選択し &quot; &quot; ます。 (ドロップダウンリストに表示されているクラスが表示されない場合は、プロジェクトをビルドしたことを `Book` 確認してください)。次に、[+] ボタンをクリックします。

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

[**新しいデータコンテキスト**] ダイアログボックスで [**追加**] をクリックします。

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

[**コントローラーの追加**] ダイアログボックスで [**追加**] をクリックします。 スキャフォールディングは、 `BooksController` API コントローラーを定義するという名前のクラスを追加します。 また、モデルフォルダーにという名前のクラスが追加され `BooksAPIContext` ます。これにより、Entity Framework のデータコンテキストが定義されます。

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a>データベースのシード

[ツール] メニューの [ **NuGet パッケージマネージャー**] を選択し、[ **パッケージマネージャーコンソール**] を選択します。

[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

このコマンドは、移行フォルダーを作成し、Configuration.cs という名前の新しいコードファイルを追加します。 このファイルを開き、メソッドに次のコードを追加し `Configuration.Seed` ます。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

[パッケージマネージャーコンソール] ウィンドウで、次のコマンドを入力します。

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

これらのコマンドは、ローカルデータベースを作成し、Seed メソッドを呼び出してデータベースにデータを読み込みます。

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a>DTO クラスの追加

ここでアプリケーションを実行し、GET 要求を/api/books/1 に送信すると、応答は次のようになります。 (読みやすくするためにインデントを追加しました)。

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

代わりに、この要求でフィールドのサブセットを返す必要があります。 また、作成者 ID ではなく、著者の名前を返すようにします。 これを実現するには、EF モデルではなく *データ転送オブジェクト* (DTO) を返すようにコントローラーメソッドを変更します。 DTO は、データを伝送するためだけに設計されたオブジェクトです。

ソリューションエクスプローラーで、プロジェクトを右クリックし、[ **Add**  |  **新しいフォルダー**の追加] を選択します。 フォルダーに「dto」という名前を指定 &quot; &quot; します。 次の定義を使用して、という名前のクラスを `BookDto` dto フォルダーに追加します。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

`BookDetailDto`という名前の別のクラスを追加します。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

次に、 `BooksController` インスタンスを返すようにクラスを更新し `BookDto` ます。 インスタンスをインスタンスに投影するには、クエリ可能な[Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx)メソッドを使用します。 `Book` `BookDto` コントローラークラスの更新されたコードを次に示します。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> `PutBook`、 `PostBook` 、およびの `DeleteBook` 各メソッドは、このチュートリアルでは必要ないため、削除しました。

ここで、アプリケーションを実行して/api/books/1 を要求すると、応答本文は次のようになります。

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a>ルート属性の追加

次に、属性ルーティングを使用するようにコントローラーを変換します。 まず、 **Routeprefix** 属性をコントローラーに追加します。 この属性は、このコントローラーのすべてのメソッドの初期 URI セグメントを定義します。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

次に、 **[Route]** 属性をコントローラーアクションに追加します。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

各コントローラーメソッドのルートテンプレートは、 **ルート** 属性に指定された文字列に加えて、プレフィックスとして使用されます。 メソッドでは、 `GetBook` ルートテンプレートにパラメーター化された文字列 &quot; {id: int} が含まれてい &quot; ます。これは、URI セグメントに整数値が含まれている場合に一致します。

| 方法 | ルート テンプレート | URI の例 |
| --- | --- | --- |
| `GetBooks` | "api/ブック" | `http://localhost/api/books` |
| `GetBook` | "api/books/{id: int}" | `http://localhost/api/books/5` |

## <a name="get-book-details"></a>ブックの詳細を取得する

ブックの詳細を取得するために、クライアントは GET 要求をに送信し `/api/books/{id}/details` ます。ここで、 *{id}* は本の id です。

`BooksController` クラスに次のメソッドを追加します。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

を要求すると、次の `/api/books/1/details` ような応答が表示されます。

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a>ジャンルで書籍を取得する

特定のジャンルに含まれる本の一覧を取得するために、クライアントは GET 要求をに送信し `/api/books/genre` ます。ここで、 *genre* はジャンルの名前です。 (例: `/api/books/fantasy`)。

に次のメソッドを追加し `BooksController` ます。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

ここでは、URI テンプレートに {genre} パラメーターを含むルートを定義しています。 Web API は、これらの2つの Uri を区別し、異なる方法でルーティングできることに注意してください。

`/api/books/1`

`/api/books/fantasy`

これは、 `GetBook` メソッドに "id" セグメントが整数値でなければならないという制約が含まれているためです。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

/Api/books/fantasy を要求すると、次のような応答が表示されます。

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a>作成者による書籍の取得

特定の作成者の書籍の一覧を取得するために、クライアントは GET 要求をに送信し `/api/authors/id/books` ます。ここで、 *id* は著者の id です。

に次のメソッドを追加し `BooksController` ます。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

この例は、 &quot; 書籍 &quot; が作成者の子リソースとして扱われるため、興味深いものです &quot; &quot; 。 このパターンは、RESTful Api では非常に一般的です。

ルートテンプレート内のチルダ (~) は、 **routeprefix** 属性のルートプレフィックスよりも優先されます。

## <a name="get-books-by-publication-date"></a>出版日による書籍の取得

発行日による書籍の一覧を取得するために、クライアントは GET 要求をに送信し `/api/books/date/yyyy-mm-dd` ます。ここで、 *yyyy-mm-dd* は日付です。

これを行う方法の1つを次に示します。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

`{pubdate:datetime}`パラメーターは**DateTime**値に一致するように制約されています。 これは機能しますが、実際には必要以上に制限されています。 たとえば、次の Uri はルートとも一致します。

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

これらの Uri を許可しても問題はありません。 ただし、ルートテンプレートに正規表現の制約を追加することで、ルートを特定の形式に制限することができます。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

これで、yyyy-mm-dd という形式の日付のみ &quot; が一致するようになりました &quot; 。 実際の日付があることを検証するために regex を使用しないことに注意してください。 これは、Web API が URI セグメントを **DateTime** インスタンスに変換しようとしたときに処理されます。 無効な日付 (' 2012-47-99 ' など) は変換されません。クライアントは404エラーを受け取ります。

別の `/api/books/date/yyyy/mm/dd` **[Route]** 属性を別の regex と共に追加することで、スラッシュ区切り記号 () をサポートすることもできます。

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

ここでは、微妙ですが重要な詳細があります。 2番目のルートテンプレートには、 \* {pubdate} パラメーターの先頭にワイルドカード文字 () があります。

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.txt)]

これにより、{pubdate} が URI の残りの部分と一致する必要があることがルーティングエンジンに通知されます。 既定では、テンプレートパラメーターは単一の URI セグメントと一致します。 この例では、{pubdate} を複数の URI セグメントにまたがって指定します。

`/api/books/date/2013/06/17`

## <a name="controller-code"></a>コントローラーコード

BooksController クラスの完全なコードを次に示します。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a>まとめ

属性ルーティングを使用すると、API の Uri を設計するときに、より柔軟に制御し、柔軟性を高めることができます。
