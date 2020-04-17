---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: エンティティ フレームワーク (C#) を使用したモデル クラスの作成 |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルでは、マイクロソフト エンティティ フレームワークASP.NET MVC を使用する方法を学習します。 エンティティ ウィザードを使用して ADO.NET エンティティ Da.. を作成する方法を学習します。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 716d34167258b1005b25b1cd11bfaa6d80763320
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542665"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a>Entity Framework でモデル クラスを作成する (C#)

[マイクロソフト](https://github.com/microsoft)

> このチュートリアルでは、マイクロソフト エンティティ フレームワークASP.NET MVC を使用する方法を学習します。 エンティティ ウィザードを使用して、ADO.NET エンティティ データ モデルを作成する方法を学習します。 このチュートリアルでは、Entity Framework を使用してデータベース データを選択、挿入、更新、および削除する方法を示す Web アプリケーションを構築します。

このチュートリアルの目的は、mvc アプリケーションをビルドするときに Microsoft エンティティ フレームワークを使用してデータ アクセス クラスを作成する方法ASP.NET説明することです。 このチュートリアルでは、マイクロソフト エンティティ フレームワークの以前の知識がないことを前提としています。 このチュートリアルの最後に、Entity Framework を使用してデータベース レコードを選択、挿入、更新、および削除する方法を理解します。

Microsoft エンティティ フレームワークは、データベースからデータ アクセス層を自動的に生成できるオブジェクト リレーショナル マッピング (O/RM) ツールです。 Entity Framework を使用すると、データ アクセス クラスを手作業で構築する手間のかたえのある作業を回避できます。

ASP.NET MVC で Microsoft エンティティ フレームワークを使用する方法を説明するために、簡単なサンプル アプリケーションをビルドします。 ムービー データベース レコードを表示および編集できるムービー データベース アプリケーションを作成します。

このチュートリアルでは、サービス パック 1 を使用して Visual Studio 2008 またはビジュアル Web 開発者 2008 を使用していることを前提としています。 エンティティ フレームワークを使用するには、サービス パック 1 が必要です。 次のアドレスから、Visual Studio 2008 サービス パック 1 またはサービス パック 1 を使用したビジュアル Web 開発者をダウンロードできます。

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> ASP.NET MVC とマイクロソフト エンティティ フレームワークの間に不可欠な関係はありません。 mvc で使用できる Entity Framework にはいくつかの代替手段ASP.NET用意されています。 たとえば、MICROSOFT LINQ to SQL、NHibernate、または SubSonic などの他の O/RM ツールを使用して、MVC モデル クラスを構築できます。

## <a name="creating-the-movie-sample-database"></a>ムービー サンプル データベースの作成

ムービー データベース アプリケーションでは、次の列を含む Movies という名前のデータベース テーブルを使用します。

| 列名 | データ型 | Null を許可しますか? | 主キーですか? |
| --- | --- | --- | --- |
| Id | INT | False | True |
| タイトル | nvarchar(100) | False | False |
| ディレクター | nvarchar(100) | False | False |

次の手順に従って、このテーブルを ASP.NET MVC プロジェクトに追加できます。

1. ソリューション エクスプローラー ウィンドウ\_で [アプリ データ] フォルダーを右クリックし、メニュー オプション**の [追加]、[新しい項目]** を選択します。
2. [**新しい項目の追加]** ダイアログ ボックスで **、[SQL Server データベース**] を選択し、データベース名 MoviesDB.mdf を指定して、[**追加**] ボタンをクリックします。
3. MoviesDB.mdf ファイルをダブルクリックして、サーバー エクスプローラ/データベース エクスプローラ ウィンドウを開きます。
4. MoviesDB.mdf データベース接続を展開し、テーブル フォルダーを右クリックし、メニュー オプション**の新しいテーブルの追加**を選択します。
5. テーブル デザイナーで、ID、タイトル、およびディレクターの列を追加します。
6. [**保存**] ボタン (フロッピーのアイコンが表示されています) をクリックして、新しいテーブルを Movies という名前で保存します。

Movies データベース テーブルを作成した後、サンプル データをテーブルに追加する必要があります。 Movies テーブルを右クリックし、メニュー オプションの [**テーブル データを表示]** を選択します。 表示されるグリッドに偽のムービーデータを入力できます。

## <a name="creating-the-adonet-entity-data-model"></a>ADO.NET エンティティ データ モデルの作成

エンティティ フレームワークを使用するには、エンティティ データ モデルを作成する必要があります。 Visual Studio エンティティ データ*モデル ウィザード*を利用して、データベースからエンティティ データ モデルを自動的に生成できます。

次の手順に従います。

1. ソリューション エクスプローラ ウィンドウで Models フォルダを右クリックし、メニュー オプションの **[追加]、[新しい項目]** の順に選択します。
2. [**新しい項目の追加]** ダイアログで、[データ] カテゴリを選択します (図 1 参照)。
3. **[エンティティ データ モデルADO.NETテンプレートを**選択し、エンティティ データ モデルに MoviesDBModel.edmx という名前を付け、[**追加**] ボタンをクリックします。 **[追加**] ボタンをクリックすると、データ モデル ウィザードが起動します。
4. [**モデルコンテンツの選択]** ステップで、[**データベースから生成**] オプションを選択し、[**次へ**] ボタンをクリックします (図 2 を参照)。
5. [**データ接続の選択]** ステップで、MoviesDB.mdf データベース接続を選択し、エンティティ接続設定名を入力して、次**へ**ボタンをクリックします (図 3 を参照)。
6. [**データベース オブジェクトの選択]** ステップで、ムービー データベース テーブルを選択し、[**完了**] ボタンをクリックします (図 4 参照)。

これらの手順を完了すると、ADO.NET エンティティ データ モデル デザイナー (エンティティ デザイナー) が開きます。

**図 1 – 新しいエンティティ データ モデルの作成**

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

**図 2 – モデルコンテンツの選択ステップ**

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

**図 3 – データ接続の選択**

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

**図 4 – データベース オブジェクトの選択**

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a>ADO.NET エンティティ データ モデルの変更

エンティティ データ モデルを作成した後、エンティティ デザイナーを利用してモデルを変更できます (図 5 参照)。 エンティティ デザイナーは、ソリューション エクスプローラー ウィンドウ内のモデル フォルダーに含まれている MoviesDBModel.edmx ファイルをダブルクリックして、いつでも開くことができます。

**図 5 – エンティティ データ モデル デザイナーADO.NET**

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

たとえば、エンティティ デザイナーを使用して、エンティティ モデル データ ウィザードによって生成されるクラスの名前を変更できます。 ウィザードは、Movies という名前の新しいデータ アクセス クラスを作成しました。 つまり、ウィザードはクラスにデータベーステーブルとまったく同じ名前を付けたのです。 このクラスを使用して特定のムービーインスタンスを表すため、クラスの名前を「ムービー」から「ムービー」に変更する必要があります。

エンティティ クラスの名前を変更する場合は、エンティティ デザイナーでクラス名をダブルクリックし、新しい名前を入力します (図 6 参照)。 または、エンティティ デザイナーでエンティティを選択した後で、[プロパティ] ウィンドウでエンティティの名前を変更できます。

**図 6 – エンティティ名の変更**

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

変更を行った後、保存ボタン (フロッピー ディスクのアイコン) をクリックして、エンティティ データ モデルを保存することを忘れないでください。 この背後では、エンティティ デザイナーは C# クラスのセットを生成します。 これらのクラスを表示するには、[ソリューション エクスプローラー] ウィンドウからMoviesDBModel.Designer.cs ファイルを開きます。

次回エンティティ デザイナーを使用するときに、変更が上書きされるため、Designer.cs ファイル内のコードは変更しないでください。 Designer.cs ファイルで定義されているエンティティ クラスの機能を拡張する場合は、*部分クラス*を別々のファイルに作成できます。

#### <a name="selecting-database-records-with-the-entity-framework"></a>エンティティ フレームワークを使用したデータベース レコードの選択

ムービーレコードのリストを表示するページを作成して、ムービーデータベースアプリケーションの構築を開始しましょう。 リスト 1 のホーム コントローラは Index() という名前のアクションを公開します。 Index() アクションは、エンティティ フレームワークを利用して、ムービー データベース テーブルからすべてのムービー レコードを返します。

**リスト 1 - コントローラ\ホームコントローラー.cs**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

リスト 1 のコントローラーにはコンストラクターが含まれています。 コンストラクターは、db というクラス レベルの\_フィールドを初期化します。 db\_フィールドは、Microsoft エンティティ フレームワークによって生成されたデータベース エンティティを表します。 \_db フィールドは、エンティティ デザイナーによって生成された MoviesDBEntities クラスのインスタンスです。

ホーム コントローラーで MoviesDBEntities クラスを使用するには、名前空間 *(MVCProjectName.* モデル)。

db\_フィールドは、Movies データベーステーブルからレコードを取得するために、Index() アクション内で使用されます。 式\_db。ムービーセットは、ムービーデータベーステーブルからのすべてのレコードを表します。 ToList() メソッドは、ムービーのセットをムービーオブジェクトの汎用コレクション (リスト&lt;ムービー&gt;) に変換するために使用されます。

ムービー レコードは、エンティティへの LINQ の助けを借りて取得されます。 リスト 1 の Index() アクションでは、LINQ*メソッド構文*を使用してデータベース レコードのセットを取得します。 必要に応じて、代わりに LINQ*クエリ構文*を使用できます。 次の 2 つのステートメントは、まったく同じ処理を行います。

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

最も直感的にわかる LINQ 構文 (メソッド構文またはクエリ構文) を使用します。 2 つのアプローチの間にパフォーマンスに違いはありません– 唯一の違いはスタイルです。

リスト 2 のビューは、ムービーレコードを表示するために使用されます。

**リスト 2 - ビュー\ホーム\インデックス.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

リスト 2 のビューには、各ムービー レコードを反復処理し、ムービー レコードの Title プロパティと Director プロパティの値を表示する**foreach**ループが含まれています。 各レコードの横に [編集] と [削除] リンクが表示されます。 さらに、ビューの下部に [ムービーの追加] リンクが表示されます (図 7 参照)。

**図 7 – インデックス ビュー**

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

インデックス ビューは *、型付きビュー*です。 インデックス ビューには、&lt;モデル プロパティを&gt;厳密に型指定されたムービー オブジェクトの一覧コレクション (リスト&lt;ムービー) にキャストする*Inherits*属性を持つ %@ Page % ディレクティブが含まれています。

## <a name="inserting-database-records-with-the-entity-framework"></a>エンティティ フレームワークを使用したデータベース レコードの挿入

Entity Framework を使用すると、データベース テーブルに新しいレコードを簡単に挿入できます。 リスト 3 には、ムービー データベース テーブルに新しいレコードを挿入するために使用できるホーム コントローラー クラスに追加された 2 つの新しいアクションが含まれています。

**リスト 3 – コントローラ\ホームコントローラ.cs (メソッドの追加)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

最初の Add() アクションはビューを返すだけです。 ビューには、新しいムービー データベース レコードを追加するためのフォームが含まれています (図 8 参照)。 フォームを送信すると、2 番目の Add() アクションが呼び出されます。

2 番目の Add() アクションは AcceptVerbs 属性で修飾されていることに注意してください。 このアクションは、HTTP POST 操作を実行する場合にのみ呼び出すことができます。 つまり、このアクションは HTML フォームを投稿するときにのみ呼び出すことができます。

2 番目の Add() アクションは、ASP.NET MVC TryUpdateModel() メソッドの助けを借りて、エンティティ フレームワーク ムービー クラスの新しいインスタンスを作成します。 メソッドは、Add() メソッドに渡された FormCollection 内のフィールドを受け取り、これらの HTML フォームフィールドの値をムービークラスに割り当てます。

エンティティ フレームワークを使用する場合は、TryUpdateModel または UpdateModel メソッドを使用してエンティティ クラスのプロパティを更新するときに、プロパティの "ホワイト リスト" を指定する必要があります。

次に、Add() アクションは、いくつかの簡単なフォーム検証を実行します。 このアクションは、タイトルとディレクターの両方のプロパティに値があることを確認します。 検証エラーがある場合は、検証エラー メッセージが ModelState に追加されます。

検証エラーがない場合は、Entity Framework の助けを借りて、新しいムービー レコードが Movies データベース テーブルに追加されます。 新しいレコードは、次の 2 行のコードでデータベースに追加されます。

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

コードの最初の行は、エンティティ フレームワークによって追跡されているムービーのセットに新しいムービー エンティティを追加します。 2 行目のコードは、追跡対象の Movies に対して行われた変更を、基になるデータベースに保存します。

**図 8 – [追加] ビュー**

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a>エンティティ フレームワークを使用したデータベース レコードの更新

新しいデータベース レコードを挿入する方法として、Entity Framework でデータベース レコードを編集するのとほぼ同じアプローチに従うことができます。 リスト 4 には、Edit() という名前の 2 つの新しいコントローラ アクションが含まれています。 最初の Edit() アクションは、ムービーレコードを編集するための HTML フォームを返します。 2 番目の Edit() アクションは、データベースの更新を試みます。

**リスト 4 - コントローラ\ホームコントローラ.cs (メソッドの編集)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

2 番目の Edit() アクションは、編集中のムービーの ID に一致するデータベースからムービーレコードを取得することから始まります。 次の LINQ to Entities ステートメントは、特定の ID に一致する最初のデータベース レコードを取得します。

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

次に、TryUpdateModel() メソッドを使用して、HTML フォーム フィールドの値をムービー エンティティのプロパティに割り当てます。 更新する正確なプロパティを指定するホワイト リストが提供されていることに注意してください。

次に、ムービータイトルとディレクターの両方のプロパティに値が設定されていることを確認するために、いくつかの簡単な検証が実行されます。 いずれかのプロパティに値がない場合は、検証エラー メッセージが ModelState および ModelState.IsValid に追加され、値が false を返します。

検証エラーがない場合は、SaveChanges() メソッドを呼び出すことによって、基になる Movies データベース テーブルが変更によって更新されます。

データベース レコードを編集する場合は、編集中のレコードの ID を、データベースの更新を実行するコントローラー アクションに渡す必要があります。 それ以外の場合、コントローラー アクションは、基になるデータベースで更新するレコードを認識しません。 リスト 5 に含まれる編集ビューには、編集中のデータベース レコードの ID を表す非表示フォーム フィールドが含まれています。

**リスト 5 - ビュー\ホーム\編集.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>エンティティ フレームワークを使用したデータベース レコードの削除

このチュートリアルで取り組む必要がある最終的なデータベース操作は、データベースレコードを削除することです。 リスト 6 のコントローラー アクションを使用して、特定のデータベース レコードを削除できます。

**リスト 6 -- \コントローラー\ホームコントローラー.cs (削除アクション)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

Delete() アクションは、最初にアクションに渡された ID に一致するムービーエンティティを取得します。 次に、ムービーは DeleteObject() メソッドを呼び出した後に SaveChanges() メソッドを呼び出してデータベースから削除されます。 最後に、ユーザーはインデックス ビューにリダイレクトされます。

## <a name="summary"></a>まとめ

このチュートリアルの目的は、MVC と Microsoft エンティティ フレームワークASP.NETを利用して、データベース駆動型の web アプリケーションを構築する方法を示すことでした。 データベース レコードの選択、挿入、更新、および削除を可能にするアプリケーションの構築方法について説明しました。

最初に、エンティティ データ モデル ウィザードを使用して、Visual Studio 内からエンティティ データ モデルを生成する方法について説明しました。 次に、LINQ to Entities を使用してデータベース テーブルからデータベース レコードのセットを取得する方法について説明します。 最後に、Entity Framework を使用してデータベース レコードの挿入、更新、および削除を行いました。

> [!div class="step-by-step"]
> [次へ](creating-model-classes-with-linq-to-sql-cs.md)
