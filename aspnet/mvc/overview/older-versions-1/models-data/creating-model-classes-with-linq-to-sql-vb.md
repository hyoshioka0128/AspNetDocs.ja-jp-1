---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
title: LINQ to SQL (VB) を使用したモデル クラスの作成 |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルの目的は、ASP.NET MVC アプリケーションのモデル クラスを作成する 1 つの方法について説明することです。 このチュートリアルでは、モデル c..を構築する方法を学習します。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: a4a25a75-d71f-4509-98b4-df72e748985a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
msc.type: authoredcontent
ms.openlocfilehash: 1a6133227eedc8934af7bf872532ca667b97d0f8
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542704"
---
# <a name="creating-model-classes-with-linq-to-sql-vb"></a>LINQ to SQL でモデル クラスを作成する (VB)

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_VB.pdf)

> このチュートリアルの目的は、ASP.NET MVC アプリケーションのモデル クラスを作成する 1 つの方法について説明することです。 このチュートリアルでは、Microsoft LINQ to SQL を利用して、モデル クラスを構築し、データベース にアクセスする方法を学習します。

このチュートリアルの目的は、ASP.NET MVC アプリケーションのモデル クラスを作成する 1 つの方法について説明することです。 このチュートリアルでは、Microsoft LINQ to SQL を利用して、モデル クラスを構築し、データベース にアクセスする方法を学習します。

このチュートリアルでは、基本的なムービー データベース アプリケーションを構築します。 まず、ムービー データベース アプリケーションを、できるだけ簡単かつ最速の方法で作成します。 私たちは、コントローラのアクションから直接すべてのデータアクセスを実行します。

次に、リポジトリ パターンの使用方法について説明します。 リポジトリ パターンを使用するには、もう少し作業が必要です。 ただし、このパターンを採用する利点は、変更に適応可能で簡単にテストできるアプリケーションを構築できることです。

## <a name="what-is-a-model-class"></a>モデルクラスとは

MVC モデルには、MVC ビューまたは MVC コントローラーに含まれていないアプリケーション ロジックがすべて含まれています。 特に、MVC モデルには、アプリケーション ビジネスとデータ アクセス ロジックがすべて含まれます。

さまざまなテクノロジを使用して、データ アクセス ロジックを実装できます。 たとえば、Microsoft エンティティ フレームワーク、NHibernate、亜音速、またはADO.NET クラスを使用してデータ アクセス クラスを構築できます。

このチュートリアルでは、LINQ to SQL を使用してデータベースのクエリと更新を行います。 LINQ to SQL では、非常に簡単にデータベースを操作できます。 ただし、mvc フレームワークASP.NETは LINQ to SQL に関連付けられてはなりません。 ASP.NET MVC は、あらゆるデータ アクセス テクノロジと互換性があります。

## <a name="create-a-movie-database"></a>ムービー データベースを作成する

このチュートリアルでは、モデルクラスを構築する方法を説明するために、単純なムービーデータベースアプリケーションを構築します。 最初の手順は、新しいデータベースを作成することです。 ソリューション エクスプローラ ウィンドウ\_で [App Data] フォルダを右クリックし、メニュー オプションの **[追加]、[新しい項目]** の順に選択します。 SQL Server データベース テンプレートを選択し、その名前を MoviesDB.mdf に指定し、[**追加**] ボタンをクリックします (図 1 を参照)。

[![新しい SQL Server データベースの追加](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)

**図 01**: 新しい SQL Server データベースの追加 ([フルサイズの画像を表示するには [ ] をクリック](creating-model-classes-with-linq-to-sql-vb/_static/image3.png)します )

新しいデータベースを作成した後、アプリケーション\_データ フォルダーにある MoviesDB.mdf ファイルをダブルクリックして、データベースを開くことができます。 MoviesDB.mdf ファイルをダブルクリックすると、サーバー エクスプローラ ウィンドウが開きます (図 2 参照)。

|   | サーバー エクスプローラ ウィンドウは、Visual Web 開発者を使用する場合はデータベース エクスプローラ ウィンドウと呼ばれます。 |
|---|----------------------------------------------------------------------------------------------------|
|   |                                                                                                    |

[![サーバー エクスプローラー ウィンドウの使用](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)

**図 02**: [サーバー エクスプローラ] ウィンドウを使用して ([フルサイズの画像を表示するには、ここをクリック](creating-model-classes-with-linq-to-sql-vb/_static/image6.png)します)

ムービーを表すテーブルをデータベースに 1 つ追加する必要があります。 [テーブル] フォルダを右クリックし、メニュー オプションの **[新しいテーブルの追加]** を選択します。 このメニュー オプションを選択すると、テーブル デザイナーが開きます (図 3 参照)。

[![サーバー エクスプローラー ウィンドウの使用](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)

**図 03**: テーブル デザイナ ([フルサイズの画像を表示する をクリック](creating-model-classes-with-linq-to-sql-vb/_static/image9.png)します )

データベース テーブルに次の列を追加する必要があります。

| **列名** | **[データ型]** | **NULL を許可する** |
| --- | --- | --- |
| Id | int | False |
| タイトル | ンヴァルチャル(200) | False |
| ディレクター | ンヴァルチャル(50) | False |

Id 列に対して 2 つの特別な操作を行う必要があります。 まず、テーブル デザイナーで列を選択し、キーのアイコンをクリックして、Id 列を主キー列としてマークする必要があります。 LINQ to SQL では、データベースに対して挿入または更新を実行するときに、主キー列を指定する必要があります。

次に **、Is** Identity プロパティに値 Yes を割り当てることによって、Id 列を ID 列としてマークする必要があります (図 3 参照)。 ID 列は、テーブルに新しいデータ行を追加するたびに自動的に新しい番号が割り当てられる列です。

これらの変更を行った後、テーブルを tblMovie という名前で保存します。 [保存] ボタンをクリックすると、テーブルを保存できます。

## <a name="create-linq-to-sql-classes"></a>LINQ to SQL クラスを作成する

この MVC モデルには、tblMovie データベース テーブルを表す LINQ to SQL クラスが含まれます。 これらの LINQ to SQL クラスを作成する最も簡単な方法は、モデル フォルダーを右クリックし **、[追加]、[新しい項目**] を選択し、LINQ to SQL クラス テンプレートを選択し、クラスに Movie.dbml という名前を付け、[**追加**] ボタンをクリックします (図 4 参照)。

[![LINQ to SQL クラスの作成](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)

**図 04**: LINQ to SQL クラスの作成 ([フルサイズの画像を表示する をクリック](creating-model-classes-with-linq-to-sql-vb/_static/image12.png)して )

ムービー LINQ to SQL クラスを作成するとすぐに、オブジェクト リレーショナル デザイナーが表示されます。 データベース テーブルを [サーバー エクスプローラー] ウィンドウからオブジェクト リレーショナル デザイナーにドラッグして、特定のデータベース テーブルを表す LINQ to SQL クラスを作成できます。 オブジェクト リレーショナル デザイナーに tblMovie データベース テーブルを追加する必要があります (図 4 参照)。

[![オブジェクト リレーショナル デザイナーの使用](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)

**図 05**: オブジェクト リレーショナル デザイナを使用する ([フルサイズの画像を表示する をクリック](creating-model-classes-with-linq-to-sql-vb/_static/image15.png)します )

既定では、オブジェクト リレーショナル デザイナーは、デザイナーにドラッグしたデータベース テーブルとまったく同じ名前のクラスを作成します。 しかし、クラスtblMovieを呼び出したくありません。 したがって、デザイナーでクラスの名前をクリックし、クラスの名前をムービーに変更します。

最後に、忘れずに [**保存**] ボタン (フロッピーの画像) をクリックして、LINQ to SQL クラスを保存します。 それ以外の場合、LINQ to SQL クラスはオブジェクト リレーショナル デザイナーによって生成されません。

## <a name="using-linq-to-sql-in-a-controller-action"></a>コントローラ アクションで LINQ を使用した SQL の使用

LINQ to SQL クラスができたので、これらのクラスを使用してデータベースからデータを取得できます。 このセクションでは、コントローラー アクション内で直接 LINQ to SQL クラスを使用する方法について説明します。 MVC ビューで tblMovies データベース テーブルからムービーの一覧を表示します。

まず、ホームコントローラクラスを変更する必要があります。 このクラスは、アプリケーションの [コントローラー] フォルダーにあります。 クラスを変更して、リスト 1 のクラスのように見えます。

**リスト1 –`Controllers\HomeController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample1.vb)]

リスト 1 の Index() アクションは、LINQ to SQL データコンテキスト クラス (MovieDataContext) を使用して MoviesDB データベースを表します。 クラスは、Visual Studio オブジェクト リレーショナル デザイナーによって生成されました。

LINQ クエリは、tblMovies データベース テーブルからすべてのムービーを取得するために、DataContext に対して実行されます。 ムービーのリストは、movies という名前のローカル変数に割り当てられます。 最後に、ムービーのリストはビュー データを通じてビューに渡されます。

ムービーを表示するには、次にインデックスビューを変更する必要があります。 インデックス ビューは、ビュー\ホーム\ フォルダーにあります。 インデックス ビューを更新して、リスト 2 のビューのように見えます。

**リスト2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample2.aspx)]

変更されたインデックス ビューには、ビュー&lt;の上部に %@ インポート名前空間 %&gt;ディレクティブが含まれていることに注意してください。 このディレクティブは、MvcApplication1 名前空間をインポートします。 この名前空間は、モデル クラス (特に Movie クラス) をビューで操作するために必要です。

リスト 2 のビューには、ViewData.Model プロパティで表されるすべてのアイテムを反復処理する For Each ループが含まれています。 タイトルプロパティの値は、各ムービーに対して表示されます。

プロパティの値が IEnumerable にキャストされていることに注意してください。 これは、ViewData.Model の内容をループするために必要です。 ここでのもう 1 つのオプションは、厳密に型指定されたビューを作成することです。 厳密に型指定されたビューを作成するときは、ビューの分離コード クラス内の特定の型に ViewData.Model プロパティをキャストします。

HomeController クラスとインデックス ビューを変更した後でアプリケーションを実行すると、空白のページが表示されます。 tblMovies データベース テーブルにムービー レコードがないため、空白のページが表示されます。

tblMovies データベース テーブルにレコードを追加するには、サーバー エクスプローラ ウィンドウ (Visual Web Developer の [データベース エクスプローラ] ウィンドウ) で tblMovies データベース テーブルを右クリックし、メニュー オプションの **[テーブル データの表示**] を選択します。 表示されるグリッドを使用して、ムービー レコードを挿入できます (図 5 参照)。

[![ムービーを挿入する](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)

**図 06**: 動画の挿入 ([フルサイズの画像を表示する をクリック](creating-model-classes-with-linq-to-sql-vb/_static/image18.png))

データベース レコードを tblMovies テーブルに追加し、アプリケーションを実行すると、図 7 のページが表示されます。 ムービー データベースのレコードはすべて箇条書きリストに表示されます。

[![インデックス ビューでムービーを表示する](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)

**図 07**: インデックス ビューでムービーを表示する ([フルサイズの画像を表示する をクリック](creating-model-classes-with-linq-to-sql-vb/_static/image21.png)して)

## <a name="using-the-repository-pattern"></a>リポジトリ パターンの使用

前のセクションでは、コント ローラー アクション内で直接 SQL クラスに LINQ を使用します。 Index() コントローラ アクションから直接 MovieDataContext クラスを使用しました。 単純なアプリケーションの場合にこれを行うことに何の問題もありません。 ただし、コント ローラー クラスで LINQ to SQL を直接操作すると、より複雑なアプリケーションを構築する必要がある場合に問題が発生します。

コントローラ クラス内で LINQ to SQL を使用すると、将来データ アクセス テクノロジを切り替えるのが困難になります。 たとえば、Microsoft LINQ から SQL への切り替えから、データ アクセス テクノロジとして Microsoft エンティティ フレームワークの使用に切り替えることができます。 その場合は、アプリケーション内のデータベースにアクセスするすべてのコントローラを書き換える必要があります。

また、コントローラ クラス内で LINQ to SQL を使用すると、アプリケーションの単体テストを作成することが困難になります。 通常は、単体テストを実行するときにデータベースと対話しません。 単体テストを使用して、データベース サーバーではなくアプリケーション ロジックをテストする場合。

将来の変更に適応しやすく、より簡単にテストできる MVC アプリケーションを構築するには、リポジトリ パターンの使用を検討する必要があります。 リポジトリ パターンを使用する場合は、データベース アクセス ロジックをすべて含む個別のリポジトリ クラスを作成します。

リポジトリ クラスを作成するときは、リポジトリ クラスで使用されるすべてのメソッドを表すインターフェイスを作成します。 コントローラー内では、リポジトリではなくインターフェイスに対してコードを記述します。 この方法で、将来、さまざまなデータ アクセス テクノロジを使用してリポジトリを実装できます。

リスト 3 のインターフェイスは IMovieRepository という名前で、ListAll() という名前の単一のメソッドを表します。

**リスト3 –`Models\IMovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample3.vb)]

リスト 4 のリポジトリ クラスは、IMovieRepository インターフェイスを実装しています。 このメソッドには、IMovieRepository インターフェイスで必要なメソッドに対応する ListAll() という名前のメソッドが含まれていることに注意してください。

**リスト4 –`Models\MovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample4.vb)]

最後に、リスト 5 の MoviesController クラスはリポジトリ パターンを使用します。 LINQ to SQL クラスを直接使用しなくなりました。

**リスト5 –`Controllers\MoviesController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample5.vb)]

リスト 5 の MoviesController クラスには 2 つのコンストラクターがあることに注意してください。 最初のコンストラクターであるパラメーターなしのコンストラクターは、アプリケーションの実行中に呼び出されます。 このコンストラクターは、MovieRepository クラスのインスタンスを作成し、2 番目のコンストラクターに渡します。

2 番目のコンストラクターには、IMovieRepository パラメーターという 1 つのパラメーターがあります。 このコンストラクターは、パラメーターの値をリポジトリというクラス\_レベルのフィールドに割り当てるだけです。

MoviesController クラスは、依存性注入パターンと呼ばれるソフトウェア設計パターンを利用しています。 特に、コンストラクタ依存注入という名前のプラグインを使用しています。 このパターンの詳細については、マーティン・ファウラーの次の記事を読んでください。

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

MoviesController クラスのすべてのコード (最初のコンストラクターを除く) は、実際のムービーリポジトリ クラスではなく IMovieRepository インターフェイスとやり取りします。 コードは、インターフェイスの具体的な実装ではなく、抽象インターフェイスと対話します。

アプリケーションで使用されるデータ アクセス テクノロジを変更する場合は、代替データベース アクセス テクノロジを使用するクラスを使用して IMovieRepository インターフェイスを実装するだけです。 たとえば、エンティティ フレームワークムービーリポジトリクラスまたはサブソニックムービーリポジトリクラスを作成できます。 コントローラ クラスはインターフェイスに対してプログラムされているため、IMovieRepository の新しい実装をコントローラ クラスに渡すことができます。

さらに、MoviesController クラスをテストする場合は、ムービーのリポジトリ クラスを MoviesController に渡すことができます。 実際にはデータベースにアクセスせず、IMovieRepository インターフェイスの必要なメソッドをすべて含むクラスを使用して、IMovieRepository クラスを実装できます。 そうすれば、実際のデータベースにアクセスせずに MoviesController クラスを単体テストできます。

## <a name="summary"></a>まとめ

このチュートリアルの目的は、MICROSOFT LINQ to SQL を利用して MVC モデル クラスを作成する方法を示すことでした。 ASP.NETのMVCアプリケーションでデータベースデータを表示するための2つの戦略を検討しました。 まず、LINQ to SQL クラスを作成し、コントローラー アクション内で直接クラスを使用しました。 コントローラー内で LINQ to SQL クラスを使用すると、MVC アプリケーションでデータベース データをすばやく簡単に表示できます。

次に、データベース データを表示するための、もう少し難しいが、間違いなく高潔なパスを探しました。 リポジトリ パターンを利用し、すべてのデータベース アクセス ロジックを別のリポジトリ クラスに配置しました。 コントローラでは、具体的なクラスではなく、インターフェイスに対してすべてのコードを記述しました。 リポジトリ パターンの利点は、将来的にデータベース アクセス テクノロジを簡単に変更でき、コントローラ クラスを簡単にテストできる点です。

> [!div class="step-by-step"]
> [前へ](creating-model-classes-with-the-entity-framework-vb.md)
> [次へ](displaying-a-table-of-database-data-vb.md)
