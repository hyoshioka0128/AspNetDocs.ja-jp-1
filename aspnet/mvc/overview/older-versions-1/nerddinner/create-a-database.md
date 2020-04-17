---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: データベースの作成 | Microsoft Docs
author: rick-anderson
description: 手順 2 は、NerdDinner アプリケーションのすべてのディナーと RSVP データを保持するデータベースを作成する手順を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541612"
---
# <a name="create-a-database"></a>データベースの作成

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、mvc 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NETの手順 2 です。
> 
> 手順 2 は、NerdDinner アプリケーションのすべてのディナーと RSVP データを保持するデータベースを作成する手順を示します。
> 
> mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。

## <a name="nerddinner-step-2-creating-the-database"></a>NerdDinner ステップ 2: データベースの作成

私たちのNerdDinnerアプリケーションのすべてのディナーとRSVPデータを保存するためにデータベースを使用します。

以下の手順では、無料の SQL Server Express エディションを使用してデータベースを作成する方法を示します ([これは、マイクロソフト Web プラットフォーム インストーラ](https://www.microsoft.com/web/downloads/platform.aspx)の V2 を使用して簡単にインストールできます ) 。 このコードを記述する場合は、すべて SQL Server Express と完全な SQL Server の両方で動作します。

### <a name="creating-a-new-sql-server-express-database"></a>新しい SQL Server エクスプレス データベースの作成

まず、Web プロジェクトを右クリックし、[**&gt;新しい項目の追加**] メニュー コマンドを選択します。

![](create-a-database/_static/image1.png)

これにより、Visual Studio の [新しい項目の追加] ダイアログ が表示されます。 "データ" カテゴリでフィルター処理し、"SQL Server データベース" 項目テンプレートを選択します。

![](create-a-database/_static/image2.png)

"NerdDinner.mdf" を作成する SQL Server エクスプレス データベースに名前を付け、ヒット OK を付けます。 Visual Studio は、このファイルを \App\_Data ディレクトリ (既に読み取りと書き込みの両方のセキュリティ ACL を使用してセットアップされているディレクトリ) に追加するかどうか尋ねます。

![](create-a-database/_static/image3.png)

"はい" をクリックすると、新しいデータベースが作成され、ソリューション エクスプローラーに追加されます。

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>データベース内でのテーブルの作成

これで、新しい空のデータベースが作成されました。 それにいくつかのテーブルを追加してみましょう。

そのためには、Visual Studio 内の [サーバー エクスプローラ] タブ ウィンドウに移動します。 アプリケーションの \App\_データ フォルダーに格納されている SQL Server Express データベースは、サーバー エクスプ ローラー内に自動的に表示されます。 オプションで、[サーバー エクスプローラ] ウィンドウの上部にある [データベースに接続] アイコンを使用して、SQL Server データベース (ローカルとリモートの両方) をリストに追加することもできます。

![](create-a-database/_static/image5.png)

私たちは、私たちのNerdDinnerデータベースに2つのテーブルを追加します - 1つは私たちのディナーを保存し、もう1つはそれらにRSVPの受け入れを追跡します。 データベース内の 「Tables」 フォルダーを右クリックし、「新しいテーブルの追加」メニューコマンドを選択することで、新しいテーブルを作成できます。

![](create-a-database/_static/image6.png)

これにより、テーブルのスキーマを構成できるテーブル デザイナーが開きます。 "Dinners" テーブルでは、10 列のデータを追加します。

![](create-a-database/_static/image7.png)

"DinnerID" 列をテーブルの一意の主キーにします。 この設定は、[DinnerID] 列を右クリックし、[主キーの設定] メニュー項目を選択することで行うことができます。

![](create-a-database/_static/image8.png)

DinnerID を主キーにすることに加えて、新しいデータ行がテーブルに追加されると値が自動的にインクリメントされる「ID」列として設定します (つまり、最初に挿入された Dinner 行は DinnerID が 1、2 番目に挿入された行は DinnerID が 2 になります)。

"DinnerID" 列を選択し、"列のプロパティ" エディターを使用して、列の "(Is Identity)" プロパティを "はい" に設定することでこれを行うことができます。 標準 ID のデフォルトを使用します (1 から始まり、新しい Dinner 行ごとに 1 ずつ増やします)。

![](create-a-database/_static/image9.png)

次に、Ctrl-S を押すか、**ファイル-&gt;保存**メニューコマンドを使用して、テーブルを保存します。 これにより、テーブルに名前を付けるプロンプトが表示されます。 私たちはそれを「ディナー」と名前を付けます:

![](create-a-database/_static/image10.png)

新しい Dinners テーブルは、サーバー エクスプローラのデータベース内に表示されます。

次に、上記の手順を繰り返して"RSVP"テーブルを作成します。 このテーブルには 3 つの列があります。 RsvpID 列を主キーとして設定し、ID 列にします。

![](create-a-database/_static/image11.png)

私たちはそれを保存し、名前"RSVP"を与えます。

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>テーブル間の外部キーリレーションシップの設定

これで、データベース内に 2 つのテーブルが含まれています。 最後のスキーマ設計手順は、これら 2 つのテーブル間に "一対多" のリレーションシップを設定することです。 RSVP テーブルの "DinnerID" 列を構成して、"Dinners" テーブルの "DinnerID" 列と外部キーのリレーションシップを持つ場合に、これを行います。

これを行うには、サーバー エクスプローラで RSVP テーブルをダブルクリックして、テーブル デザイナ内で開きます。 その中の "DinnerID" 列を選択し、右クリックして [リレーションシップ]5S を選択します。コンテキスト メニュー コマンド:

![](create-a-database/_static/image12.png)

これにより、テーブル間のリレーションシップを設定するために使用できるダイアログが表示されます。

![](create-a-database/_static/image13.png)

[追加] ボタンをクリックして、ダイアログに新しいリレーションシップを追加します。 リレーションシップを追加したら、ダイアログボックスの右側にあるプロパティグリッド内のツリービューノード「テーブルと列の仕様」を展開し、"."ボタンは右に表示されます。

![](create-a-database/_static/image14.png)

「.」をクリックします。ボタンを押すと、リレーションシップに関係するテーブルと列を指定したり、リレーションシップに名前を付けることができるようにする別のダイアログが表示されます。

主キー テーブルを "ディナー" に変更し、ディナー テーブル内の "DinnerID" 列を主キーとして選択します。 RSVP テーブルは、外部キー テーブルと RSVP になります。DinnerID 列は、外部キーとして関連付けられます。

![](create-a-database/_static/image15.png)

これで、RSVP テーブルの各行が Dinner テーブルの行に関連付けられます。 SQL Server は参照整合性を維持し、有効な Dinner 行を指さない場合は新しい RSVP 行を追加できないようにします。 また、まだそれを参照している RSVP 行がある場合、Dinner 行を削除することもできなくなります。

### <a name="adding-data-to-our-tables"></a>テーブルへのデータの追加

Dinners テーブルにサンプル データを追加して、最後に終了します。 サーバー エクスプローラでテーブルを右クリックし、[テーブル データの表示] コマンドを選択して、テーブルにデータを追加できます。

![](create-a-database/_static/image16.png)

アプリケーションの実装を開始する際に、後で使用できる Dinner データの数行を追加します。

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>次の手順

データベースの作成が完了しました。 ここで、クエリと更新に使用できるモデル クラスを作成しましょう。

> [!div class="step-by-step"]
> [前へ](create-a-new-aspnet-mvc-project.md)
> [次へ](build-a-model-with-business-rule-validations.md)
