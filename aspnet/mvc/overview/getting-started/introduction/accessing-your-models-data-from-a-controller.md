---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: コントローラーからモデルのデータにアクセスする |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 26d1a66cbc022664af14e4dfe4c4b4892d409b95
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045170"
---
# <a name="accessing-your-models-data-from-a-controller"></a>コントローラーからモデルのデータにアクセスする

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

このセクションでは、新しいクラスを作成 `MoviesController` し、ムービーデータを取得して、ビューテンプレートを使用してブラウザーに表示するコードを記述します。

次の手順に進む前に **、アプリケーションをビルドし**ます。 アプリケーションをビルドしないと、コントローラーを追加するときにエラーが表示されます。

ソリューションエクスプローラーで、 *Controllers* フォルダーを右クリックし、[ **追加**]、[ **コントローラー**] の順にクリックします。

![](accessing-your-models-data-from-a-controller/_static/image1.png)

[ **スキャフォールディングの追加** ] ダイアログボックスで、[ **MVC 5 Controller with views**] をクリックし、[Entity Framework] をクリックして、[ **追加**] をクリックします。

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- モデルクラスの [ **ムービー (MvcMovie)** ] を選択します。
- データコンテキストクラスの **Mo? Dbcontext (MvcMovie. model)** を選択します。
- コントローラー名として「 **moviescontroller.cs**」と入力します。

  次の図は、完成したダイアログを示しています。  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

**[追加]** をクリックします。 (エラーが発生した場合は、コントローラーの追加を開始する前にアプリケーションをビルドしていないことがあります)。Visual Studio では、次のファイルとフォルダーが作成されます。

- *Controllers*フォルダー内の*MoviesController.cs*ファイル。
- *Views\Movies*フォルダー。
- 新しい*Views\Movies*フォルダーに、cshtml、Cshtml、 *Details、Edit.* cshtml、および*Index*を作成します。

Visual Studio では、 [crud](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (作成、読み取り、更新、および削除) アクションメソッドとビューが自動的に作成されます (crud アクションメソッドとビューの自動作成はスキャフォールディングと呼ばれます)。 これで、ムービーエントリの作成、一覧表示、編集、削除を行うことができる、完全に機能する web アプリケーションが完成しました。

アプリケーションを実行し、[ **MVC ムービー** ] リンクをクリックします (または、 `Movies` ブラウザーのアドレスバーの URL に */ムービー* を追加して、コントローラーを参照します)。 アプリケーションは既定のルーティング ( *App \_ Start\RouteConfig.cs* ファイルで定義されています) に依存しているため、ブラウザー `http://localhost:xxxxx/Movies` の要求はコントローラーの既定のアクションメソッドにルーティングされ `Index` `Movies` ます。 つまり、ブラウザーの要求は、 `http://localhost:xxxxx/Movies` ブラウザーの要求と実質的に同じです `http://localhost:xxxxx/Movies/Index` 。 まだ追加していないため、結果はムービーの空の一覧になります。

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>ムービーの作成

**[Create New]\(新規作成\)** リンクを選択します。 ムービーに関する詳細を入力し、[ **作成** ] ボタンをクリックします。

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> 価格フィールドに小数点またはコンマを入力することはできません。 小数点にコンマ (,) を使用し、英語 (米国) 以外の日付形式を使用する英語以外のロケールの jQuery 検証をサポートするには、 &quot; &quot; *globalize.js* および特定の *カルチャ/globalize.cultures.js* ファイル (from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) と JavaScript を使用する必要があり `Globalize.parseFloat` ます。 これを行う方法については、次のチュートリアルで説明します。 ここでは、単に 10 のような整数を入力します。

[ **作成** ] ボタンをクリックすると、フォームがサーバーにポストされます。このとき、ムービー情報はデータベースに保存されます。 次に *、ムービーの URL に* リダイレクトされます。ここで、新しく作成したムービーを一覧に表示できます。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

いくつかのムービー エントリを作成します。 [**編集**]、[**詳細**]、および [**削除**] リンクを試してください。すべて機能します。

## <a name="examining-the-generated-code"></a>生成されたコードの調査

*Controllers\MoviesController.cs*ファイルを開き、生成されたメソッドを確認し `Index` ます。 次に、メソッドを使用したムービーコントローラーの一部を `Index` 示します。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

コントローラーに対する要求では、 `Movies` テーブル内のすべてのエントリが返され、 `Movies` その結果がビューに渡され `Index` ます。 前に説明したように、クラスの次の行は、 `MoviesController` ムービーデータベースコンテキストをインスタンス化します。 ムービーデータベースコンテキストを使用して、映画のクエリ、編集、および削除を行うことができます。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>厳密に型指定されたモデルと @model キーワード

このチュートリアルの前半では、オブジェクトを使用して、コントローラーがビューテンプレートにデータまたはオブジェクトを渡す方法について説明しました `ViewBag` 。 `ViewBag`は、ビューに情報を渡すための便利な遅延バインディング方法を提供する動的オブジェクトです。

MVC では、 *厳密* に型指定されたオブジェクトをビューテンプレートに渡すこともできます。 この厳密に型指定されたアプローチによって、Visual Studio エディターでのコードのコンパイル時のチェックと、より高度な [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) が有効になります。 Visual Studio のスキャフォールディング機構では、メソッドとビューを作成するときに、この方法 ( *厳密* に型指定されたモデルを渡す) をクラスおよびビューテンプレートと共に使用し `MoviesController` ました。

*Controllers\MoviesController.cs*ファイルで、生成されたメソッドを確認し `Details` ます。 `Details`メソッドは次のようになります。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

`id`通常、パラメーターはルートデータとして渡されます。たとえば、 `http://localhost:1234/movies/details/1` コントローラーをムービーコントローラーに設定し、アクションをに、を `details` 1 に設定し `id` ます。 次のように、クエリ文字列を使用して id を渡すこともできます。

`http://localhost:1234/movies/details?id=1`

`Movie`が見つかった場合、モデルのインスタンス `Movie` はビューに渡され `Details` ます。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

*Views\Movies\Details.cshtml*ファイルの内容を確認します。

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

`@model`ビューテンプレートファイルの先頭にステートメントを含めることで、ビューが想定するオブジェクトの型を指定できます。 ムービー コントローラーを作成したとき、Visual Studio によって *Details.cshtml* ファイルの先頭に `@model` ステートメントが自動的に追加されています。

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

この `@model` ディレクティブにより、厳密に型指定された `Model` オブジェクトを使って、コントローラーがビューに渡したムービーにアクセスできます。 たとえば、 *Details. cshtml* テンプレートでは、コードは各ムービーフィールドをに渡し、 `DisplayNameFor` 厳密 [に](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) 型指定されたオブジェクトを使用して HTML ヘルパーを表示し `Model` ます。 `Create` `Edit` メソッドとビューテンプレートも、ムービーモデルオブジェクトを渡します。

MoviesController.cs ファイルで、*インデックスの cshtml*ビューテンプレートとメソッドを確認します。 `Index` *MoviesController.cs* [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) `View` アクションメソッドでヘルパーメソッドを呼び出すときに、コードによってオブジェクトが作成されることに注意して `Index` ください。 次に、コードはこの `Movies` リスト `Index` をアクションメソッドからビューに渡します。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

ムービーコントローラーを作成すると、Visual Studio によって、次の `@model` ステートメントが *Index. cshtml* ファイルの先頭に自動的に追加されます。

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

この `@model` ディレクティブを使用すると、 `Model` 厳密に型指定されたオブジェクトを使用して、コントローラーがビューに渡すムービーの一覧にアクセスできます。 たとえば、 *Index. cshtml* テンプレートでは、コードは、 `foreach` 厳密に型指定されたオブジェクトに対してステートメントを実行して、ムービーをループし `Model` ます。

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

`Model`オブジェクトはオブジェクトとして厳密に型指定されるため `IEnumerable<Movie>` 、 `item` ループ内の各オブジェクトはとして型指定され `Movie` ます。 その他の利点としては、コードエディターでのコードのコンパイル時チェックと IntelliSense の完全なサポートがあります。

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>SQL Server LocalDB の使用

Entity Framework Code First は、指定されたデータベース接続文字列がまだ存在していないデータベースを指していることを検出した `Movies` ため、データベースを自動的に作成 Code First ます。 これが作成されたことを確認するには、[ *アプリ \_ データ* ] フォルダーを調べます。 *ムービーの .mdf*ファイルが表示されない場合は、**ソリューションエクスプローラー**ツールバーの [**すべてのファイルを表示**] ボタンをクリックし、[**更新**] ボタンをクリックして、[*アプリ \_ データ*] フォルダーを展開します。

![](accessing-your-models-data-from-a-controller/_static/image9.png)

[ *.Mdf* ] をダブルクリックして **サーバーエクスプローラー**を開き、[ **テーブル** ] フォルダーを展開して、ムービーテーブルを表示します。 [ID] の横にあるキーアイコンに注意してください。 既定では、EF は、ID という名前のプロパティを主キーとして作成します。 EF と MVC の詳細については、「Tom Dykstra's [mvc と ef](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)の優れたチュートリアル」を参照してください。

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

テーブルを右クリック `Movies` し、[ **テーブルデータの表示** ] をクリックして、作成したデータを表示します。

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

テーブルを右クリック `Movies` し、[ **テーブル定義を開く** ] をクリックして、Entity Framework Code First 作成されたテーブル構造を確認します。

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

前の手順で作成したクラスにテーブルのスキーマがどのよう `Movies` にマップされるかに注目 `Movie` してください。 このスキーマは、クラスに基づいて自動的に作成さ Code First Entity Framework `Movie` ます。

操作が完了したら、 *Mo? Dbcontext* を右クリックし、[ **接続を閉じる**] を選択して接続を閉じます。 (接続を閉じないと、次にプロジェクトを実行したときにエラーが表示される場合があります)。

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

これで、データを表示、編集、更新および削除できるデータベースができました。 次のチュートリアルでは、スキャフォールディングコードの残りの部分を確認し、 `SearchIndex` `SearchIndex` このデータベースで映画を検索できるようにするメソッドとビューを追加します。 MVC での Entity Framework の使用の詳細については、「 [ASP.NET MVC アプリケーションの Entity Framework データモデルの作成](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)」を参照してください。

> [!div class="step-by-step"]
> [前へ](creating-a-connection-string.md)
> [次へ](examining-the-edit-methods-and-edit-view.md)
