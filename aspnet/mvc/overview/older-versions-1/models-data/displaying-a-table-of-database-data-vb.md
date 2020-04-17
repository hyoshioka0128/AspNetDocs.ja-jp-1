---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: データベース データ (VB) のテーブルを表示する |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルでは、データベース レコードのセットを表示する 2 つの方法を示します。 HTML ta.. でデータベースレコードのセットをフォーマットする 2 つの方法を示します。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 9b03e6a0d2bf7d2bf59ba4dca3076fa306d3fed4
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541898"
---
# <a name="displaying-a-table-of-database-data-vb"></a>データベース データの表を表示する (VB)

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> このチュートリアルでは、データベース レコードのセットを表示する 2 つの方法を示します。 HTML テーブルのデータベース レコードのセットを書式設定する 2 つの方法を示します。 まず、ビュー内で直接データベース レコードを書式設定する方法を説明します。 次に、データベース レコードの書式設定時に部分を利用する方法を示します。

このチュートリアルの目的は、ASP.NET MVC アプリケーションでデータベース データの HTML テーブルを表示する方法を説明することです。 まず、Visual Studio に含まれるスキャフォールディング ツールを使用して、レコードのセットを自動的に表示するビューを生成する方法を学習します。 次に、データベース レコードの書式設定時に部分をテンプレートとして使用する方法について説明します。

## <a name="create-the-model-classes"></a>モデル クラスの作成

映画データベーステーブルからレコードのセットを表示します。 Movies データベース テーブルには、次の列が含まれています。

<a id="0.4_table01"></a>

| **列名** | **[データ型]** | **NULL を許可する** |
| --- | --- | --- |
| Id | int | False |
| タイトル | ンヴァルチャル(200) | False |
| ディレクター | NVarchar(50) | False |
| 日付リリース済 | DateTime | False |

ASP.NET MVC アプリケーションで Movies テーブルを表すために、モデル クラスを作成する必要があります。 このチュートリアルでは、Microsoft エンティティ フレームワークを使用して、モデル クラスを作成します。

> [!NOTE] 
> 
> このチュートリアルでは、マイクロソフト エンティティ フレームワークを使用します。 ただし、LINQ to SQL、NHibernate、またはADO.NETを含む ASP.NET MVC アプリケーションからデータベースを操作するには、さまざまなテクノロジを使用できることを理解することが重要です。

エンティティ データ モデル ウィザードを起動するには、次の手順に従います。

1. ソリューション エクスプローラ ウィンドウで Models フォルダを右クリックし、メニュー オプションの **[追加]、[新しい項目]** の順に選択します。
2. **[データ**] カテゴリを選択し **、[ADO.NET エンティティ データ モデル]** テンプレートを選択します。
3. データ モデルに*MoviesDBModel.edmx*という名前を付け、[**追加**] ボタンをクリックします。

[追加] ボタンをクリックすると、エンティティ データ モデル ウィザードが表示されます (図 1 参照)。 ウィザードを完了するには、次の手順を実行します。

1. [**モデル コンテンツの選択]** ステップで、[**データベースから生成**] オプションを選択します。
2. [**データ接続の選択]** ステップで *、MoviesDB.mdf*データ接続と、接続設定の*名前を*使用します。 **[次へ]** をクリックします。
3. [**データベース オブジェクトの選択]** ステップで、[テーブル] ノードを展開し、[Movies] テーブルを選択します。 *名前空間のモデル*を入力し、[**完了**] ボタンをクリックします。

[![LINQ to SQL クラスの作成](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)

**図 01**: LINQ to SQL クラスの作成 ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image2.png)して )

エンティティ データ モデル ウィザードを完了すると、エンティティ データ モデル デザイナーが開きます。 デザイナーは、Movies エンティティを表示する必要があります (図 2 を参照してください)。

[![エンティティ データ モデル デザイナー](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)

**図 02**: エンティティ データ モデル デザイナ ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image4.png)します )

続行する前に、1 つの変更を加える必要があります。 エンティティ データ ウィザードは *、Movies*データベース テーブルを表す Movies という名前のモデル クラスを生成します。 映画クラスを使用して特定のムービーを表現するため、クラスの名前を*映画*ではなく*ムービー* (複数形ではなく単数形) に変更する必要があります。

デザイナー画面でクラスの名前をダブルクリックし、クラスの名前を映画からムービーに変更します。 この変更を行った後、**保存**ボタン (フロッピー ディスクのアイコン) をクリックしてムービー クラスを生成します。

## <a name="create-the-movies-controller"></a>映画コントローラを作成する

データベースレコードを表現する方法ができたので、ムービーのコレクションを返すコントローラを作成できます。 Visual Studio ソリューション エクスプローラー ウィンドウで、[コントローラー] フォルダーを右クリックし、メニュー オプション**の [追加]、[コント ローラー** ] を選択します (図 3 参照)。

[![[コントローラーの追加] メニュー](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)

**図 03**: コントローラの追加メニュー ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image6.png))

[**コントローラの追加**] ダイアログが表示されたら、コントローラ名を MovieController に入力します (図 4 を参照)。 [**追加**]ボタンをクリックして、新しいコントローラを追加します。

[![[コントローラの追加] ダイアログ](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)

**図 04**: [コントローラの追加] ダイアログボックス ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image8.png))

ムービーコントローラが公開する Index() アクションを変更して、データベースレコードのセットを返す必要があります。 リスト 1 のコントローラーのように見えるコントローラーを変更します。

**リスト 1 - コントローラ\ムービーコントローラー.vb**

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

リスト 1 では、MoviesDBEntities クラスを使用して、MoviesDB データベースを表します。 式*エンティティ。ムービーセット.ToList()は*、映画データベーステーブルからすべてのムービーのセットを返します。

## <a name="create-the-view"></a>ビューの作成

HTML テーブルに一連のデータベース レコードを表示する最も簡単な方法は、Visual Studio によって提供されるスキャフォールディングを利用することです。

メニュー オプションの [**ビルド]、[ ソリューションのビルド**] の順に選択してアプリケーションをビルドします。 **[ビューの追加]** ダイアログを開く前にアプリケーションをビルドする必要があります。

Index() アクションを右クリックし、メニュー オプションの**ビューの追加**を選択します (図 5 を参照)。

[![ビューの追加](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)

**図 05**: ビューの追加 ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image10.png))

[**ビューの追加]** ダイアログで、[厳密に**型指定されたビューを作成**する] チェック ボックスをオンにします。 **ビュー データ**クラスとして Movie クラスを選択します。 **ビューの内容**として *[リスト]* を選択します (図 6 を参照)。 これらのオプションを選択すると、ムービーの一覧を表示する厳密に型指定されたビューが生成されます。

[![[ビューの追加] ダイアログ](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)

**図 06**: [ビューの追加] ダイアログボックス ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image12.png))

**[追加**] ボタンをクリックすると、リスト 2 のビューが自動的に生成されます。 このビューには、ムービーのコレクションを反復処理し、ムービーの各プロパティを表示するために必要なコードが含まれています。

**リスト 2 - ビュー\ムービー\インデックス.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

アプリケーションを実行するには、メニュー オプションの **[デバッグ]、[デバッグの開始**] を選択します (または F5 キーを押します)。 アプリケーションを実行すると、インターネット エクスプローラが起動します。 /Movie URL に移動すると、図 7 のページが表示されます。

[![映画のテーブル](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)

**図07**: 動画の表 ([フルサイズの画像を表示する をクリック](displaying-a-table-of-database-data-vb/_static/image14.png))

図 7 のデータベース レコードのグリッドの外観について何も気に入らない場合は、インデックス ビューを変更するだけです。 たとえば、インデックス ビューを変更して *、DateReleased*ヘッダーを *[リリース日]* に変更できます。

## <a name="create-a-template-with-a-partial"></a>部分を含むテンプレートを作成する

ビューが複雑になりすぎる場合は、ビューをパーシャルに分割することをお勧めします。 パーシャルを使用すると、ビューの理解と維持が容易になります。 ムービー データベースの各レコードを書式設定するテンプレートとして使用できる部分を作成します。

部分を作成するには、次の手順に従います。

1. [ビュー]\Movie フォルダを右クリックし、メニュー オプションの [**ビューの追加]** を選択します。
2. *[部分ビューの作成 (.ascx)]* というラベルの付いたチェック ボックスをオンにします。
3. 部分的な*ムービーテンプレートに名前を付けます*。
4. [**厳密に型指定されたビューを作成する**] チェック ボックスをオンにします。
5. ビュー データ*クラス*として [ムービー] を選択します。
6. *ビューのコンテンツ*として [空] を選択します。
7. [**追加**] ボタンをクリックして、部分をプロジェクトに追加します。

これらの手順を完了したら、ムービー テンプレートの一部をリスト 3 のように変更します。

**リスト 3 – ビュー\ムービー\ムービーテンプレート.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

リスト 3 の部分には、1 行のレコードのテンプレートが含まれています。

リスト 4 の変更されたインデックス ビューでは、ムービー テンプレートの部分を使用します。

**リスト 4 - ビュー\ムービー\インデックス.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

リスト 4 のビューには、すべてのムービーを反復処理する For Each ループが含まれています。 ムービーごとに、ムービーテンプレートの部分を使用してムービーのフォーマットを設定します。 レンダリングテンプレートは、ヘルパー メソッドを呼び出すことによってレンダリングされます。

変更されたインデックス ビューでは、データベース レコードの HTML テーブルとまったく同じものがレンダリングされます。 しかし、ビューは大幅に簡略化されました。

RenderPartial() メソッドは文字列を返さないため、他のほとんどのヘルパー メソッドとは異なります。 したがって、%= Html.RenderPartial() &lt;% の&gt;&lt;代わりに % Html.RenderPartial() % を&gt;使用して RenderPartial() メソッドを呼び出す必要があります。

## <a name="summary"></a>まとめ

このチュートリアルの目的は、HTML テーブルにデータベース レコードのセットを表示する方法を説明することです。 最初に、Microsoft エンティティ フレームワークを利用して、コントローラー アクションからデータベース レコードのセットを返す方法を学習しました。 次に、Visual Studio スキャフォールディングを使用して、項目のコレクションを自動的に表示するビューを生成する方法について説明しました。 最後に、部分を利用してビューを簡略化する方法を学習しました。 各データベース レコードを書式設定できるように、部分をテンプレートとして使用する方法を学習しました。

> [!div class="step-by-step"]
> [前へ](creating-model-classes-with-linq-to-sql-vb.md)
> [次へ](performing-simple-validation-vb.md)
