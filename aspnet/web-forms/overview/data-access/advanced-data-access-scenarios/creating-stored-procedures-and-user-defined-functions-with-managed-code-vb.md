---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
title: マネージコードを使用したストアドプロシージャとユーザー定義関数の作成 (VB) |Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 2005 は .NET 共通言語ランタイムと統合されているため、開発者はマネージコードを使用してデータベースオブジェクトを作成できます。 このチュートリアル...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 8be9a51b-ea6b-46c7-bfa2-476d9b14c24c
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 30c37750d89ff3503ead32c0b2a9708b99d785ff
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045287"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-vb"></a>マネージド コードでストアド プロシージャとユーザー定義関数を作成する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_VB.zip) または [PDF のダウンロード](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/datatutorial75vb1.pdf)

> Microsoft SQL Server 2005 は .NET 共通言語ランタイムと統合されているため、開発者はマネージコードを使用してデータベースオブジェクトを作成できます。 このチュートリアルでは、Visual Basic または C# コードを使用してマネージストアドプロシージャとマネージユーザー定義関数を作成する方法について説明します。 また、Visual Studio のこれらのエディションで、このようなマネージデータベースオブジェクトをデバッグする方法についても説明します。

## <a name="introduction"></a>概要

Microsoft s SQL Server 2005 などのデータベースでは、データの挿入、変更、および取得に [transact-sql (構造化照会言語 transact-sql)](http://en.wikipedia.org/wiki/Transact-SQL) が使用されます。 ほとんどのデータベースシステムには、1つの再利用可能な単位として実行できる一連の SQL ステートメントをグループ化するための構造が含まれています。 ストアドプロシージャの一例を次に示します。 もう1つは、 *ユーザー定義関数*(udf) です。これは、手順 9. で詳細を確認するコンストラクトです。

SQL は、データのセットを操作できるように設計されています。 `SELECT`、、およびの各ステートメントは、 `UPDATE` `DELETE` 対応するテーブル内のすべてのレコードに対して本質的に適用され、その句によってのみ制限され `WHERE` ます。 しかし、一度に1つのレコードを操作し、スカラーデータを操作するために設計された言語機能は多数あります。 では、レコードのセットを一度に1つずつループさ[せることが `CURSOR` ](http://www.sqlteam.com/item.asp?ItemID=553)できます。 、、などの文字列操作関数 `LEFT` は、 `CHARINDEX` `PATINDEX` スカラーデータを操作します。 SQL には、やなどの制御フローステートメントも含まれてい `IF` `WHILE` ます。

Microsoft SQL Server 2005 より前では、ストアドプロシージャと Udf は T-sql ステートメントのコレクションとしてのみ定義できました。 ただし、SQL Server 2005 は、 [共通言語ランタイム (CLR)](https://msdn.microsoft.com/netframework/aa497266.aspx)との統合を提供するように設計されています。これは、すべての .net アセンブリで使用されるランタイムです。 そのため、SQL Server 2005 データベースのストアドプロシージャと Udf は、マネージコードを使用して作成できます。 つまり、ストアドプロシージャまたは UDF を Visual Basic クラスのメソッドとして作成できます。 これにより、これらのストアドプロシージャおよび Udf は、.NET Framework と独自のカスタムクラスの機能を利用できるようになります。

このチュートリアルでは、マネージストアドプロシージャとユーザー定義関数を作成する方法と、それらを Northwind データベースに統合する方法について説明します。 始めましょう!

> [!NOTE]
> マネージデータベースオブジェクトには、対応する SQL server よりも利点があります。 言語の豊富さと知識があり、既存のコードとロジックを再利用できることが主な利点です。 ただし、管理されたデータベースオブジェクトは、処理ロジックがあまり必要としないデータのセットを操作する場合に効率が低下する可能性があります。 マネージコードと T-sql を使用する利点の詳細については、 [マネージコードを使用してデータベースオブジェクトを作成する利点](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx)を確認してください。

## <a name="step-1-moving-the-northwind-database-out-ofapp_data"></a>手順 1: Northwind データベースをから移動する`App_Data`

これまでのすべてのチュートリアルでは、web アプリケーション s フォルダー内の Microsoft SQL Server 2005 Express Edition データベースファイルが使用されてい `App_Data` ます。 `App_Data`すべてのファイルが1つのディレクトリ内に配置され、チュートリアルをテストするための追加の構成手順を必要としないため、データベースを簡単に配布して実行します。

ただし、このチュートリアルでは、で Northwind データベースをから移動 `App_Data` し、SQL Server 2005 Express Edition データベースインスタンスに明示的に登録します。 このチュートリアルの手順は、フォルダー内のデータベースを使用して実行できますが、 `App_Data` データベースを SQL Server 2005 Express Edition データベースインスタンスに明示的に登録すると、いくつかの手順がはるかに簡単になります。

このチュートリアルのダウンロードには、 `NORTHWND.MDF` と `NORTHWND_log.LDF` いう名前のフォルダーに配置された2つのデータベースファイルがあり `DataFiles` ます。 チュートリアルを独自に実装している場合は、Visual Studio を終了し、 `NORTHWND.MDF` `NORTHWND_log.LDF` ファイルとファイルを web サイト `App_Data` のフォルダーから web サイトの外部のフォルダーに移動します。 データベースファイルを別のフォルダーに移動したら、Northwind データベースを SQL Server 2005 Express Edition データベースインスタンスに登録する必要があります。 これは SQL Server Management Studio から行うことができます。 SQL Server 2005 の Express 以外のエディションがコンピューターにインストールされている場合は、Management Studio が既にインストールされている可能性があります。 コンピューターに SQL Server 2005 Express Edition しかない場合は、 [Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)をダウンロードしてインストールしてください。

SQL Server Management Studio を起動します。 図1に示すように、Management Studio は、どのサーバーに接続するかをたずねることで開始されます。 サーバー名として「localhost\SQLExpress」と入力し、[認証] ボックスの一覧で [Windows 認証] を選択し、[接続] をクリックします。

![適切なデータベースインスタンスに接続する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image1.png)

**図 1**: 適切なデータベースインスタンスに接続する

接続した後、[オブジェクトエクスプローラー] ウィンドウには、データベース、セキュリティ情報、管理オプションなど、SQL Server 2005 Express Edition データベースインスタンスに関する情報が一覧表示されます。

Northwind データベースは、 `DataFiles` SQL Server 2005 Express Edition データベースインスタンスに (または移動した場所にある) フォルダーにアタッチする必要があります。 [データベース] フォルダーを右クリックし、ショートカットメニューの [アタッチ] をクリックします。 [データベースのアタッチ] ダイアログボックスが表示されます。 [追加] ボタンをクリックし、該当するファイルにドリルダウンし `NORTHWND.MDF` て、[OK] をクリックします。 この時点で、画面は図2のようになります。

[![適切なデータベースインスタンスに接続する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image2.png)

**図 2**: 適切なデータベースインスタンスに接続する ([クリックすると、フルサイズのイメージが表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image4.png)されます)

> [!NOTE]
> [データベースのアタッチ] ダイアログボックスを使用し Management Studio て SQL Server 2005 Express Edition インスタンスに接続するときは、[マイドキュメント] などのユーザープロファイルディレクトリにドリルダウンすることはできません。 そのため、およびファイルは、 `NORTHWND.MDF` `NORTHWND_log.LDF` 非ユーザープロファイルディレクトリに配置してください。

[OK] ボタンをクリックして、データベースをアタッチします。 [データベースのアタッチ] ダイアログボックスが閉じ、オブジェクトエクスプローラーにアタッチされたデータベースが一覧表示されます。 Northwind データベースには、のような名前が付いている可能性があり `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF` ます。 データベースの名前を Northwind に変更するには、データベースを右クリックし、[名前の変更] を選択します。

![データベースの名前を Northwind に変更する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image5.png)

**図 3**: データベースの名前を Northwind に変更する

## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>手順 2: Visual Studio で新しいソリューションと SQL Server プロジェクトを作成する

SQL Server 2005 でマネージストアドプロシージャまたは Udf を作成するには、ストアドプロシージャと UDF ロジックをクラスの Visual Basic コードとして記述します。 コードを記述したら、このクラスをアセンブリ (ファイル) にコンパイルし、アセンブリを `.dll` SQL Server データベースに登録した後、アセンブリ内の対応するメソッドを参照するストアドプロシージャまたは UDF オブジェクトをデータベース内に作成する必要があります。 これらの手順はすべて手動で実行できます。 任意のテキストエディターでコードを作成し、コマンドラインから Visual Basic コンパイラ () を使用してコンパイルし `vbc.exe` 、コマンドまたは Management Studio を使用してデータベースに登録 [`CREATE ASSEMBLY`](https://msdn.microsoft.com/library/ms189524.aspx) し、同様の方法でストアドプロシージャまたは UDF オブジェクトを追加できます。 幸いなことに、Visual Studio の Professional および Team Systems バージョンには、これらのタスクを自動化する SQL Server プロジェクトの種類が含まれています。 このチュートリアルでは、SQL Server プロジェクトの種類を使用して、マネージストアドプロシージャと UDF を作成します。

> [!NOTE]
> Visual Web Developer または Standard edition の Visual Studio を使用している場合は、代わりに手動での方法を使用する必要があります。 手順13では、これらの手順を手動で実行するための詳細な手順について説明します。 手順13を読む前に手順 2 ~ 12 を読むことをお勧めします。これらの手順には、使用している Visual Studio のバージョンに関係なく適用する必要がある重要な SQL Server 構成手順が含まれているためです。

まず、Visual Studio を開きます。 [ファイル] メニューの [新しいプロジェクト] をクリックして、[新しいプロジェクト] ダイアログボックスを表示します (図4を参照)。 データベースプロジェクトの種類にドリルダウンし、右側に表示されているテンプレートから、新しい SQL Server プロジェクトの作成を選択します。 このプロジェクトに名前を `ManagedDatabaseConstructs` 付けて、という名前のソリューション内に配置することを選択しました `Tutorial75` 。

[![新しい SQL Server プロジェクトを作成する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image6.png)

**図 4**: 新しい SQL Server プロジェクトを作成[する (クリックしてフルサイズのイメージを表示する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image8.png))

[新しいプロジェクト] ダイアログボックスの [OK] ボタンをクリックして、ソリューションと SQL Server プロジェクトを作成します。

SQL Server プロジェクトは、特定のデータベースに関連付けられています。 その結果、新しい SQL Server プロジェクトを作成した後、すぐにこの情報を指定するように求められます。 図5に、手順1で SQL Server 2005 Express Edition データベースインスタンスに登録した Northwind データベースを指すように入力された [新しいデータベース参照] ダイアログボックスを示します。

![SQL Server プロジェクトを Northwind データベースに関連付ける](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image9.png)

**図 5**: SQL Server プロジェクトを Northwind データベースに関連付ける

このプロジェクト内で作成するマネージストアドプロシージャと Udf をデバッグするには、接続に対して SQL/CLR デバッグサポートを有効にする必要があります。 (図5のように) SQL Server プロジェクトを新しいデータベースに関連付けるたびに、Visual Studio は接続で SQL/CLR デバッグを有効にするかどうかを確認します (図6を参照)。 [はい] をクリックします。

![SQL/CLR デバッグを有効にする](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image10.png)

**図 6**: SQL/CLR デバッグを有効にする

この時点で、新しい SQL Server プロジェクトがソリューションに追加されました。 このファイルには、という名前のフォルダーが含まれてい `Test Scripts` `Test.sql` ます。このファイルは、プロジェクトで作成されたマネージデータベースオブジェクトのデバッグに使用されます。 ここでは、手順 12. でのデバッグについて説明します。

これで、新しいマネージストアドプロシージャと Udf をこのプロジェクトに追加できるようになりましたが、最初にソリューションに既存の web アプリケーションを含めます。 [ファイル] メニューの [追加] オプションを選択し、[既存の Web サイト] を選択します。 適切な web サイトフォルダーに移動し、[OK] をクリックします。 図7に示すように、これにより、web サイトと SQL Server プロジェクトの2つのプロジェクトが含まれるようにソリューションが更新され `ManagedDatabaseConstructs` ます。

![ソリューションエクスプローラーに2つのプロジェクトが含まれるようになりました](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image11.png)

**図 7**: ソリューションエクスプローラーに2つのプロジェクトが含まれるようになった

`NORTHWNDConnectionString`の値は、 `Web.config` 現在フォルダー内のファイルを参照して `NORTHWND.MDF` `App_Data` います。 このデータベースはから削除され、 `App_Data` SQL Server 2005 Express Edition データベースインスタンスに明示的に登録されているため、それに応じて値を更新する必要があり `NORTHWNDConnectionString` ます。 Web サイトのファイルを開き、 `Web.config` `NORTHWNDConnectionString` 接続文字列がを読み取るように値を変更します `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True` 。 この変更を行うと、 `<connectionStrings>` のセクションは `Web.config` 次のようになります。

[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample1.xml)]

> [!NOTE]
> [前のチュートリアル](debugging-stored-procedures-vb.md)で説明したように、ASP.NET web サイトなどのクライアントアプリケーションから SQL Server オブジェクトをデバッグする場合は、接続プールを無効にする必要があります。 上に示した接続文字列は、接続プール () を無効にし `Pooling=false` ます。 ASP.NET web サイトからマネージストアドプロシージャおよび Udf のデバッグを計画していない場合は、接続プールを有効にします。

## <a name="step-3-creating-a-managed-stored-procedure"></a>手順 3: マネージストアドプロシージャの作成

マネージストアドプロシージャを Northwind データベースに追加するには、まず、SQL Server プロジェクトのメソッドとしてストアドプロシージャを作成する必要があります。 ソリューションエクスプローラーから、プロジェクト名を右クリックし、[ `ManagedDatabaseConstructs` 新しい項目の追加] を選択します。 [新しい項目の追加] ダイアログボックスが表示され、プロジェクトに追加できるマネージデータベースオブジェクトの種類が一覧表示されます。 図8に示すように、これにはストアドプロシージャやユーザー定義関数などが含まれます。

まず、廃止されたすべての製品を単に返すストアドプロシージャを追加します。 新しいストアドプロシージャファイルにという名前を指定 `GetDiscontinuedProducts.vb` します。

[![GetDiscontinuedProducts という名前の新しいストアドプロシージャを追加します。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image12.png)

**図 8**: という名前の新しいストアドプロシージャを追加 `GetDiscontinuedProducts.vb` [する (クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image14.png)されます)

これにより、次の内容を含む新しい Visual Basic クラスファイルが作成されます。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample2.vb)]

ストアドプロシージャは、 `Shared` という名前のクラスファイル内のメソッドとして実装されることに注意して `Partial` `StoredProcedures` ください。 さらに、メソッドは、 `GetDiscontinuedProducts` メソッドをストアドプロシージャとしてマークする[ `SqlProcedure` 属性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlprocedureattribute.aspx)で修飾されます。

次のコードは、 `SqlCommand` オブジェクトを作成し、その `CommandText` フィールドが1と `SELECT` 等しい製品のテーブルからすべての列を返すクエリに設定し `Products` `Discontinued` ます。 次に、コマンドを実行し、結果をクライアントアプリケーションに送り返します。 このコードをメソッドに追加 `GetDiscontinuedProducts` します。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample3.vb)]

すべてのマネージデータベースオブジェクトには、呼び出し元のコンテキストを表す[ `SqlContext` オブジェクト](https://msdn.microsoft.com/library/ms131108.aspx)へのアクセス権があります。 は、 `SqlContext` [ `Pipe` プロパティ](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx)を使用して[ `SqlPipe` オブジェクト](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx)へのアクセスを提供します。 この `SqlPipe` オブジェクトは、SQL Server データベースと呼び出し元のアプリケーションの間で情報をフェリーするために使用されます。 その名前が示すように、 [ `ExecuteAndSend` メソッド](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx)は渡された `SqlCommand` オブジェクトを実行し、結果をクライアントアプリケーションに返します。

> [!NOTE]
> マネージデータベースオブジェクトは、セットベースのロジックではなく、手続き型ロジックを使用するストアドプロシージャおよび Udf に最適です。 手続き型のロジックでは、行ごとにデータセットを処理するか、スカラーデータを操作する必要があります。 ただし、先ほど作成したメソッドには、手続き型の `GetDiscontinuedProducts` ロジックは含まれません。 そのため、T-sql ストアドプロシージャとして実装するのが理想的です。 マネージストアドプロシージャを作成および配置するために必要な手順を示すために、マネージストアドプロシージャとして実装されています。

## <a name="step-4-deploying-the-managed-stored-procedure"></a>手順 4: マネージストアドプロシージャの配置

このコードが完成すると、Northwind データベースにデプロイできるようになります。 SQL Server プロジェクトを配置すると、コードがアセンブリにコンパイルされ、アセンブリがデータベースに登録され、データベースに対応するオブジェクトが作成されて、アセンブリ内の適切なメソッドにリンクされます。 配置オプションによって実行されるタスクの正確なセットは、手順13でより正確に記述されます。 `ManagedDatabaseConstructs`ソリューションエクスプローラーでプロジェクト名を右クリックし、[配置] オプションを選択します。 ただし、配置は次のエラーで失敗します: ' EXTERNAL ' 付近に正しくない構文があります。 現在のデータベースの互換性レベルを高い値に設定し、この機能を有効にする必要があります。 ストアドプロシージャのヘルプを参照してください `sp_dbcmptlevel` 。

このエラーメッセージは、アセンブリを Northwind データベースに登録しようとしたときに発生します。 SQL Server 2005 データベースにアセンブリを登録するには、データベースの互換性レベルを90に設定する必要があります。 既定では、新しい SQL Server 2005 データベースの互換性レベルは90です。 ただし、Microsoft SQL Server 2000 を使用して作成されたデータベースの既定の互換性レベルは80です。 Northwind データベースは最初 Microsoft SQL Server 2000 データベースであったため、その互換性レベルは現在は80に設定されているため、マネージデータベースオブジェクトを登録するには、90に上げる必要があります。

データベースの互換性レベルを更新するには、Management Studio で新しいクエリウィンドウを開き、次のように入力します。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample4.sql)]

ツールバーの [実行] アイコンをクリックして、上記のクエリを実行します。

[![Northwind データベースの互換性レベルを更新する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image15.png)

**図 9**: Northwind データベースの互換性レベルを更新[する (クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image17.png)されます)

互換性レベルを更新した後、SQL Server プロジェクトを再デプロイします。 今回は、配置がエラーなしで完了する必要があります。

SQL Server Management Studio に戻り、オブジェクトエクスプローラーで Northwind データベースを右クリックして、[最新の状態に更新] を選択します。 次に、[プログラミング] フォルダーをドリルダウンし、[アセンブリ] フォルダーを展開します。 図10に示すように、Northwind データベースには、プロジェクトによって生成されたアセンブリが含まれるようになりました `ManagedDatabaseConstructs` 。

![ManagedDatabaseConstructs アセンブリが Northwind データベースに登録されるようになりました。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image18.png)

**図 10**: `ManagedDatabaseConstructs` アセンブリが Northwind データベースに登録されるようになりました。

さらに、[ストアドプロシージャ] フォルダーを展開します。 ここには、という名前のストアドプロシージャが表示され `GetDiscontinuedProducts` ます。 このストアドプロシージャは、配置プロセスによって作成され、 `GetDiscontinuedProducts` アセンブリ内のメソッドを参照し `ManagedDatabaseConstructs` ます。 `GetDiscontinuedProducts`ストアドプロシージャが実行されると、メソッドが実行され `GetDiscontinuedProducts` ます。 これはマネージストアドプロシージャであるため、Management Studio (ストアドプロシージャ名の横にあるロックアイコン) を使用して編集することはできません。

![GetDiscontinuedProducts ストアドプロシージャは、[ストアドプロシージャ] フォルダーに一覧表示されます。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image19.png)

**図 11**: ストアド `GetDiscontinuedProducts` プロシージャが [ストアドプロシージャ] フォルダーに表示される

マネージストアドプロシージャを呼び出すことができるようになる前に、もう1つのハードルが必要です。データベースはマネージコードの実行を防止するように構成されています。 これを確認するには、新しいクエリウィンドウを開き、ストアドプロシージャを実行し `GetDiscontinuedProducts` ます。 次のエラーメッセージが表示されます。 .NET Framework でのユーザーコードの実行が無効になっています。 ' Clr enabled 構成オプションを有効にします。

Northwind データベースの構成情報を確認するには、クエリウィンドウでコマンドを入力して実行し `exec sp_configure` ます。 これは、clr enabled 設定が現在0に設定されていることを示しています。

[![Clr enabled 設定は現在0に設定されています](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image20.png)

**図 12**: Clr enabled 設定が現在0に設定されている ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image22.png)されます)

図12の各構成設定には4つの値が表示されています。最小値と最大値、および構成値と実行値です。 Clr enabled 設定の構成値を更新するには、次のコマンドを実行します。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample5.sql)]

を再実行すると、上記のステートメントによって `exec sp_configure` clr enabled 設定の config 値が1に更新されていますが、実行値がまだ0に設定されていることがわかります。 この構成の変更を反映するには、 [ `RECONFIGURE` コマンド](https://msdn.microsoft.com/library/ms176069.aspx)を実行する必要があります。これにより、実行値が現在の構成値に設定されます。 `RECONFIGURE`クエリウィンドウに「」と入力し、ツールバーの [実行] アイコンをクリックします。 ここで実行すると `exec sp_configure` 、clr が有効になっている設定の構成値と実行値の値1が表示されます。

Clr enabled 構成が完了すると、マネージストアドプロシージャを実行する準備が整い `GetDiscontinuedProducts` ます。 クエリウィンドウで、コマンドを入力して実行し `exec` `GetDiscontinuedProducts` ます。 ストアドプロシージャを呼び出すと、メソッド内の対応するマネージコードが実行され `GetDiscontinuedProducts` ます。 このコードは、 `SELECT` 廃止されたすべての製品を返すクエリを発行し、このデータを呼び出し元のアプリケーションに返します。これは、このインスタンスで SQL Server Management Studio します。 Management Studio は、これらの結果を受け取り、結果ウィンドウに表示します。

[![GetDiscontinuedProducts ストアドプロシージャは、廃止されたすべての製品を返します。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image23.png)

**図 13**: この `GetDiscontinuedProducts` ストアドプロシージャは、廃止されたすべての製品を返します ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image25.png)されます)

## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>手順 5: 入力パラメーターを受け取るマネージストアドプロシージャの作成

これらのチュートリアル全体で作成したクエリとストアドプロシージャの多くは、 *パラメーター*を使用しています。 たとえば、「 [型指定されたデータセットの tableadapter 用に新しいストアドプロシージャを作成する](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 」チュートリアルでは、 `GetProductsByCategoryID` という名前の入力パラメーターを受け取るという名前のストアドプロシージャを作成しました `@CategoryID` 。 その後、ストアドプロシージャは、指定された `CategoryID` パラメーターの値と一致するフィールドを持つすべての製品を返し `@CategoryID` ます。

入力パラメーターを受け取るマネージストアドプロシージャを作成するには、メソッドの定義でこれらのパラメーターを指定するだけです。 これを説明するために、次のように、という名前のプロジェクトに別のマネージストアドプロシージャを追加 `ManagedDatabaseConstructs` `GetProductsWithPriceLessThan` します。 このマネージストアドプロシージャは、価格を指定する入力パラメーターを受け取り、その `UnitPrice` フィールドがパラメーター s 値より小さいすべての製品を返します。

新しいストアドプロシージャをプロジェクトに追加するには、プロジェクト名を右クリックし、[ `ManagedDatabaseConstructs` 新しいストアドプロシージャの追加] を選択します。 そのファイルに `GetProductsWithPriceLessThan.vb` という名前を付けます。 手順 3. で見たように、これにより、クラス内に配置されたという名前のメソッドを含む新しい Visual Basic クラスファイルが作成され `GetProductsWithPriceLessThan` `Partial` `StoredProcedures` ます。

と `GetProductsWithPriceLessThan` いう名前の入力パラメーターを受け入れるようにメソッドの定義を更新 [`SqlMoney`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx) し、 `price` 実行するコードを記述してクエリ結果を返します。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample6.vb)]

`GetProductsWithPriceLessThan`メソッドの定義とコードは、 `GetDiscontinuedProducts` 手順 3. で作成したメソッドの定義とコードによく似ています。 唯一の違いは、 `GetProductsWithPriceLessThan` メソッドが入力パラメーターとしてを受け取る ( `price` )、 `SqlCommand` s クエリにパラメーター () が含まれ、 `@MaxPrice` s コレクションに追加されたパラメーターが、 `SqlCommand` `Parameters` 変数の値が割り当てら `price` れていることです。

このコードを追加した後、SQL Server プロジェクトを再デプロイします。 次に、SQL Server Management Studio に戻り、[ストアドプロシージャ] フォルダーを更新します。 新しいエントリが表示でき `GetProductsWithPriceLessThan` ます。 図14に示すように、クエリウィンドウから、コマンドを入力して実行します。これにより、 `exec GetProductsWithPriceLessThan 25` $25 未満のすべての製品が一覧表示されます。

[![$25 未満の製品が表示される](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image26.png)

**図 14**: $25 未満の製品が表示されます ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image28.png)されます)

## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>手順 6: データアクセス層からマネージストアドプロシージャを呼び出す

この時点で、 `GetDiscontinuedProducts` および `GetProductsWithPriceLessThan` マネージストアドプロシージャがプロジェクトに追加され、 `ManagedDatabaseConstructs` Northwind SQL Server データベースに登録されています。 また、これらのマネージストアドプロシージャを SQL Server Management Studio から呼び出しました (図13および14を参照してください)。 ただし、ASP.NET アプリケーションでこれらのマネージストアドプロシージャを使用するには、アーキテクチャのデータアクセス層とビジネスロジック層にそれらを追加する必要があります。 この手順では、型指定されたデータセットのに2つの新しいメソッドを追加します `ProductsTableAdapter` `NorthwindWithSprocs` 。最初に、型指定された [データセットの tableadapter チュートリアル用に新しいストアドプロシージャを作成](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) します。 手順 7. で、対応するメソッドを BLL に追加します。

`NorthwindWithSprocs`Visual Studio で型指定されたデータセットを開き、という名前のに新しいメソッドを追加し `ProductsTableAdapter` `GetDiscontinuedProducts` ます。 新しいメソッドを TableAdapter に追加するには、デザイナーで TableAdapter の名前を右クリックし、コンテキストメニューの [クエリの追加] オプションを選択します。

> [!NOTE]
> Northwind データベースを `App_Data` フォルダーから SQL Server 2005 Express Edition データベースインスタンスに移動したため、この変更を反映するために、の対応する接続文字列 Web.config 更新する必要があります。 手順2では、「」の値を更新する方法を説明しました `NORTHWNDConnectionString` `Web.config` 。 この更新を行ったことを忘れた場合は、[クエリの追加に失敗しました] というエラーメッセージが表示されます。 `NORTHWNDConnectionString` `Web.config` 新しいメソッドを TableAdapter に追加しようとしたときに、ダイアログボックスにオブジェクトの接続が見つかりません。 このエラーを解決するには、[OK] をクリックし、「」 `Web.config` `NORTHWNDConnectionString` の手順 2. で説明されているように、値を更新します。 その後、メソッドを TableAdapter にもう一度追加します。 今回は、エラーなしで動作します。

新しいメソッドを追加すると、TableAdapter クエリの構成ウィザードが起動されます。これは、過去のチュートリアルで何度も使用しています。 最初の手順では、TableAdapter がデータベースにアクセスする方法を指定するように求められます。これには、アドホック SQL ステートメントを使用する方法と、新規または既存のストアドプロシージャを使用する方法があります。 マネージストアドプロシージャを既に作成してデータベースに登録しているの `GetDiscontinuedProducts` で、[既存のストアドプロシージャを使用する] オプションを選択し、[次へ] をクリックします。

[![[既存のストアドプロシージャを使用する] オプションを選択します。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image29.png)

**図 15**: [既存のストアドプロシージャを使用する] オプションを選択[する (クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image31.png)されます)

次の画面では、メソッドが呼び出すストアドプロシージャを確認するメッセージが表示されます。 `GetDiscontinuedProducts`ドロップダウンリストからマネージストアドプロシージャを選択し、[次へ] をクリックします。

[![GetDiscontinuedProducts マネージストアドプロシージャを選択します。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image32.png)

**図 16**: `GetDiscontinuedProducts` マネージストアドプロシージャを選択[する (クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image34.png)されます)

次に、ストアドプロシージャから行を返すか、単一の値を返すか、または何も返さないかを指定するように求められます。 は `GetDiscontinuedProducts` 廃止された製品の行のセットを返すため、最初のオプション (表形式のデータ) を選択し、[次へ] をクリックします。

[![表形式のデータオプションを選択します。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image35.png)

**図 17**: 表形式のデータオプションを選択[する (クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image37.png)されます)

ウィザードの最後の画面では、使用するデータアクセスパターンと、結果として生成されるメソッドの名前を指定できます。 両方のチェックボックスをオンのままにして、メソッドにとという名前を指定し `FillByDiscontinued` `GetDiscontinuedProducts` ます。 [完了] をクリックしてウィザードを終了します。

[![メソッドに FillByDiscontinued と GetDiscontinuedProducts という名前を指定します。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image38.png)

**図 18**: メソッドに名前を指定 `FillByDiscontinued` し、 `GetDiscontinuedProducts` ([クリックしてフルサイズのイメージを表示する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image40.png))

`FillByPriceLessThan` `GetProductsWithPriceLessThan` `ProductsTableAdapter` マネージストアドプロシージャのとという名前のメソッドをに作成するには、この手順を繰り返し `GetProductsWithPriceLessThan` ます。

図19は、 `ProductsTableAdapter` およびマネージストアドプロシージャのメソッドをに追加した後のデータセットデザイナーのスクリーンショットを示して `GetDiscontinuedProducts` `GetProductsWithPriceLessThan` います。

[![ProductsTableAdapter には、この手順で追加された新しいメソッドが含まれています。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image41.png)

**図 19**: には、 `ProductsTableAdapter` この手順で追加した新しいメソッドが含まれています ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image43.png)されます)

## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>手順 7: ビジネスロジック層に対応するメソッドを追加する

手順 4. と 5. で追加したマネージストアドプロシージャを呼び出すメソッドを含むようにデータアクセス層を更新したので、次に、対応するメソッドをビジネスロジック層に追加する必要があります。 次の2つのメソッドをクラスに追加し `ProductsBLLWithSprocs` ます。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample7.vb)]

どちらのメソッドも、対応する DAL メソッドを呼び出して、インスタンスを返し `ProductsDataTable` ます。 `DataObjectMethodAttribute`各メソッドの上のマークアップにより、これらのメソッドは、ObjectDataSource s データソース構成ウィザードの [選択] タブのドロップダウンリストに表示されます。

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>手順 8: プレゼンテーション層からマネージストアドプロシージャを呼び出す

ビジネスロジックとデータアクセス層が拡張され、およびマネージストアドプロシージャの呼び出しがサポートされるようになったため `GetDiscontinuedProducts` `GetProductsWithPriceLessThan` 、ASP.NET ページを使用してこれらのストアドプロシージャの結果を表示できるようになりました。

フォルダー内のページを開き、 `ManagedFunctionsAndSprocs.aspx` `AdvancedDAL` ツールボックスから GridView をデザイナーにドラッグします。 GridView s プロパティを `ID` に設定 `DiscontinuedProducts` し、そのスマートタグから、という名前の新しい ObjectDataSource にバインドし `DiscontinuedProductsDataSource` ます。 クラス s メソッドからデータをプルするように ObjectDataSource を構成 `ProductsBLLWithSprocs` `GetDiscontinuedProducts` します。

[![製品 Bllwithsproc クラスを使用するように ObjectDataSource を構成する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image44.png)

**図 20**: クラスを使用するように ObjectDataSource を構成する `ProductsBLLWithSprocs` ([クリックすると、フルサイズのイメージが表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image46.png)されます)

[![[選択] タブのドロップダウンリストから GetDiscontinuedProducts メソッドを選択します。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image47.png)

**図 21**: [ `GetDiscontinuedProducts` 選択] タブのドロップダウンリストからメソッドを選択する ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image49.png)されます)

このグリッドを使用して製品情報が表示されるだけなので、[更新]、[挿入]、[削除] の各タブのドロップダウンリストを [(なし)] に設定し、[完了] をクリックします。

ウィザードを完了すると、Visual Studio によって、の各データフィールドに BoundField または CheckBoxField が自動的に追加され `ProductsDataTable` ます。 とを除くこれらのフィールドをすべて削除して `ProductName` `Discontinued` 、GridView および ObjectDataSource s の宣言型マークアップは次のようになります。

[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample8.aspx)]

ブラウザーを使用してこのページを表示します。 ページにアクセスすると、ObjectDataSource は `ProductsBLLWithSprocs` クラス s メソッドを呼び出し `GetDiscontinuedProducts` ます。 手順 7. で見たように、このメソッドは、ストアドプロシージャを呼び出す DAL s クラスのメソッドを呼び出し `ProductsDataTable` `GetDiscontinuedProducts` `GetDiscontinuedProducts` ます。 このストアドプロシージャはマネージストアドプロシージャであり、手順3で作成したコードを実行して、廃止された製品を返します。

マネージストアドプロシージャによって返される結果は、DAL によってにパッケージ化された `ProductsDataTable` 後、BLL に返されます。これにより、GridView にバインドされて表示されるプレゼンテーション層に返されます。 予想どおりに、廃止された製品がグリッドに表示されます。

[![廃止された製品が一覧表示されます](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image50.png)

**図 22**: 廃止された製品が一覧表示される ([クリックしてフルサイズの画像を表示する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image52.png))

さらに、テキストボックスと別の GridView をページに追加します。 この GridView で、クラス s メソッドを呼び出すことによって、テキストボックスに入力された量よりも少ない製品が表示されるようにし `ProductsBLLWithSprocs` `GetProductsWithPriceLessThan` ます。

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>手順 9: T-sql Udf の作成と呼び出し

ユーザー定義関数 (Udf) は、データベースオブジェクトで、プログラミング言語の関数のセマンティクスと密接に似ています。 Visual Basic の関数と同様に、Udf にはさまざまな数の入力パラメーターを含めることができ、特定の型の値を返すことができます。 UDF は、スカラーデータ (文字列、整数など) または表形式のデータのいずれかを返すことができます。 ここでは、スカラーデータ型を返す UDF で始まる両方の種類の Udf について簡単に見ていきます。

次の UDF は、特定の製品の在庫の推定値を計算します。 これは、3つの入力パラメーター (特定の製品の、、の各値) を使用して、型の値を返すことによって行わ `UnitPrice` `UnitsInStock` `Discontinued` `money` れます。 とを乗算することによって、在庫の推定値を計算し `UnitPrice` `UnitsInStock` ます。 廃止された項目の場合、この値は半分になります。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample9.sql)]

この UDF をデータベースに追加した後は、[プログラミング] フォルダー、[関数]、[スカラー値関数] の順に展開して、Management Studio で見つけることができます。 次のようなクエリで使用でき `SELECT` ます。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample10.sql)]

この `udf_ComputeInventoryValue` UDF を Northwind データベースに追加しました。図23は、Management Studio に表示された場合の上記のクエリの出力を示し `SELECT` ています。 UDF は、オブジェクトエクスプローラーの [スカラー値関数] フォルダーの下にも表示されます。

[![各製品のインベントリ値が一覧表示されます](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image53.png)

**図 23**: 各製品のインベントリ値が表示されます ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image55.png)されます)

Udf は表形式のデータも返すことができます。 たとえば、特定のカテゴリに属する製品を返す UDF を作成できます。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample11.sql)]

`udf_GetProductsByCategoryID`UDF は入力パラメーターを受け取り、 `@CategoryID` 指定されたクエリの結果を返し `SELECT` ます。 作成されたこの UDF は、 `FROM` クエリの (または) 句で参照でき `JOIN` `SELECT` ます。 次の例では、 `ProductID` `ProductName` 飲料ごとに、、およびの `CategoryID` 各値を返します。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample12.sql)]

この `udf_GetProductsByCategoryID` UDF を Northwind データベースに追加しました。図24に、Management Studio に表示された場合の上記のクエリの出力を示し `SELECT` ます。 表形式データを返す Udf は、[オブジェクトエクスプローラー s テーブル-値関数] フォルダーにあります。

[![各飲料の ProductID、ProductName、および CategoryID が一覧表示されます。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image56.png)

**図 24**: `ProductID` `ProductName` 飲料ごとに、、、およびが表示されます `CategoryID` (クリックすると、[フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image58.png)されます)

> [!NOTE]
> Udf の作成と使用の詳細については、「 [ユーザー定義関数の概要](http://www.sqlteam.com/item.asp?ItemID=1955)」を参照してください。 また [、ユーザー定義関数の長所と短所について](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)も確認してください。

## <a name="step-10-creating-a-managed-udf"></a>手順 10: マネージ UDF の作成

`udf_ComputeInventoryValue`上記の `udf_GetProductsByCategoryID` 例で作成したと udf は、t-sql データベースオブジェクトです。 SQL Server 2005 はマネージ Udf もサポートしています。これは、 `ManagedDatabaseConstructs` 手順 3. と 5. のマネージストアドプロシージャと同じようにプロジェクトに追加できます。 この手順では、を `udf_ComputeInventoryValue` マネージコードで UDF を実装します。

マネージ UDF をプロジェクトに追加するには `ManagedDatabaseConstructs` 、ソリューションエクスプローラーでプロジェクト名を右クリックし、[新しい項目の追加] を選択します。 [新しい項目の追加] ダイアログボックスでユーザー定義テンプレートを選択し、新しい UDF ファイルにという名前を指定し `udf_ComputeInventoryValue_Managed.vb` ます。

[![新しいマネージ UDF を ManagedDatabaseConstructs プロジェクトに追加する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image59.png)

**図 25**: 新しいマネージ UDF をプロジェクトに追加する `ManagedDatabaseConstructs` ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image61.png)されます)

ユーザー定義関数テンプレートは、という名前のクラスを作成し `Partial` `UserDefinedFunctions` ます。このメソッドの名前は、クラスファイルの名前 ( `udf_ComputeInventoryValue_Managed` このインスタンスでは) と同じになります。 このメソッドは、マネージ UDF としてメソッドにフラグを適用する[ `SqlFunction` 属性](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx)を使用して修飾されます。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample13.vb)]

`udf_ComputeInventoryValue`現在、メソッドは[ `SqlString` オブジェクト](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx)を返し、入力パラメーターを受け取りません。 メソッド定義を更新して、3つの入力パラメーター ( `UnitPrice` 、、および) を受け取るようにし、オブジェクトを返す必要があり `UnitsInStock` `Discontinued` `SqlMoney` ます。 在庫値を計算するためのロジックは、T-sql UDF のものと同じです `udf_ComputeInventoryValue` 。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample14.vb)]

UDF メソッドの入力パラメーターは、対応する SQL 型であることに注意してください。フィールドの場合は、の場合は、の場合は `SqlMoney` `UnitPrice` [`SqlInt16`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) `UnitsInStock` [`SqlBoolean`](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) `Discontinued` です。 これらのデータ型には、テーブルで定義されている型、列、型の列、 `Products` `UnitPrice` `money` `UnitsInStock` `smallint` および `Discontinued` 型の列 `bit` が反映されます。

このコードは、最初に、 `SqlMoney` 値0が割り当てられたという名前のインスタンスを作成し `inventoryValue` ます。 テーブルでは、 `Products` 列と列のデータベース値を使用でき `NULL` `UnitsInPrice` `UnitsInStock` ます。 したがって、最初に、これらの値にが含まれているかどうかを確認する必要があります。これは、 `NULL` `SqlMoney` オブジェクト s [ `IsNull` プロパティ](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx)を通じて行われます。 との両方に値以外の値が含まれている場合は、を計算して、 `UnitPrice` `UnitsInStock` `NULL` `inventoryValue` 2 つのの積になるようにします。 次に、 `Discontinued` が true の場合、値を半分にします。

> [!NOTE]
> オブジェクトでは、 `SqlMoney` 2 つの `SqlMoney` インスタンスを乗算することしかできません。 インスタンスにリテラル浮動小数点数を乗算することはできません `SqlMoney` 。 そのため、半分の場合は、 `inventoryValue` 値が0.5 の新しいインスタンスによって乗算さ `SqlMoney` れます。

## <a name="step-11-deploying-the-managed-udf"></a>手順 11: マネージ UDF を展開する

マネージ UDF が作成されたので、Northwind データベースにデプロイする準備ができました。 手順 4. で見たように、SQL Server プロジェクト内の管理オブジェクトは、ソリューションエクスプローラーでプロジェクト名を右クリックし、コンテキストメニューから [配置] オプションを選択することによって配置されます。

プロジェクトを配置したら、SQL Server Management Studio に戻り、[スカラー値関数] フォルダーを更新します。 2つのエントリが表示されるようになります。

- `dbo.udf_ComputeInventoryValue` -手順 9. で作成した T-sql UDF と
- `dbo.udf ComputeInventoryValue_Managed` -展開されたばかりの手順10で作成したマネージ UDF。

このマネージ UDF をテストするには、Management Studio 内から次のクエリを実行します。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample15.sql)]

このコマンドは、 `udf ComputeInventoryValue_Managed` T-sql udf ではなくマネージ udf を使用し `udf_ComputeInventoryValue` ますが、出力は同じです。 図23に戻って、UDF の出力のスクリーンショットを参照してください。

## <a name="step-12-debugging-the-managed-database-objects"></a>手順 12: マネージデータベースオブジェクトのデバッグ

「 [ストアドプロシージャのデバッグ](debugging-stored-procedures-vb.md) 」のチュートリアルでは、Visual Studio を使用して SQL Server をデバッグするための3つのオプション (直接データベースデバッグ、アプリケーションデバッグ、SQL Server プロジェクトからのデバッグ) について説明しました。 マネージデータベースオブジェクトは、直接データベースデバッグを使用してデバッグすることはできませんが、クライアントアプリケーションからデバッグしたり、SQL Server プロジェクトから直接デバッグしたりすることはできます。 ただし、デバッグを機能させるには、SQL Server 2005 データベースで SQL/CLR デバッグを許可する必要があります。 最初にプロジェクトを作成したときに、 `ManagedDatabaseConstructs` Visual Studio から SQL/CLR デバッグを有効にするかどうかをたずねるメッセージが表示されたことを思い出してください (手順2の図6を参照)。 この設定を変更するには、[サーバーエクスプローラー] ウィンドウでデータベースを右クリックします。

![データベースで SQL/CLR デバッグが許可されていることを確認する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image62.png)

**図 26**: データベースで SQL/CLR デバッグが許可されていることを確認する

マネージストアドプロシージャをデバッグする場合を考えてみましょう `GetProductsWithPriceLessThan` 。 まず、メソッドのコード内にブレークポイントを設定し `GetProductsWithPriceLessThan` ます。

[![GetProductsWithPriceLessThan メソッドにブレークポイントを設定する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image63.png)

**図 27**: メソッドにブレークポイントを設定 `GetProductsWithPriceLessThan` [する (クリックすると、フルサイズのイメージが表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image65.png)されます)

まず、SQL Server プロジェクトからマネージデータベースオブジェクトをデバッグする方法を見てみましょう。 このソリューションには、2つのプロジェクトが含まれています。 `ManagedDatabaseConstructs` SQL Server プロジェクトは、SQL Server プロジェクトからデバッグするために、デバッグの開始時に Visual Studio に SQL Server プロジェクトを起動するように指示する必要があり `ManagedDatabaseConstructs` ます。 `ManagedDatabaseConstructs`ソリューションエクスプローラーでプロジェクトを右クリックし、コンテキストメニューから [スタートアッププロジェクトに設定] オプションを選択します。

`ManagedDatabaseConstructs`デバッガーからプロジェクトを起動すると、ファイル内の SQL ステートメントが実行され `Test.sql` ます。このファイルは `Test Scripts` フォルダーにあります。 たとえば、マネージストアドプロシージャをテストするには、 `GetProductsWithPriceLessThan` 既存の `Test.sql` ファイルの内容を次のステートメントに置き換えます。これにより、 `GetProductsWithPriceLessThan` 14.95 の値を渡すマネージストアドプロシージャが呼び出され `@CategoryID` ます。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample16.sql)]

上記のスクリプトをに入力したら、[ `Test.sql` デバッグ] メニューに移動し、[デバッグの開始] または F5 キーを押すか、ツールバーの緑色の再生アイコンをクリックして、デバッグを開始します。 これにより、ソリューション内にプロジェクトがビルドされ、管理対象データベースオブジェクトが Northwind データベースに配置されて、スクリプトが実行され `Test.sql` ます。 この時点で、ブレークポイントにヒットし、メソッドをステップ実行したり、入力パラメーターの値を調べたりすることができ `GetProductsWithPriceLessThan` ます。

[![GetProductsWithPriceLessThan メソッド内のブレークポイントにヒットしました](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image66.png)

**図 28**: メソッド内のブレークポイントに `GetProductsWithPriceLessThan` ヒットしました ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image68.png)されます)

クライアントアプリケーションを使用して SQL database オブジェクトをデバッグするには、アプリケーションのデバッグをサポートするようにデータベースを構成する必要があります。 サーバーエクスプローラーでデータベースを右クリックし、[アプリケーションのデバッグ] オプションがオンになっていることを確認します。 さらに、ASP.NET アプリケーションを構成して、SQL デバッガーと統合し、接続プールを無効にする必要があります。 これらの手順については、「 [ストアドプロシージャのデバッグ](debugging-stored-procedures-vb.md) 」チュートリアルの手順 2. で詳しく説明しました。

ASP.NET アプリケーションとデータベースを構成したら、ASP.NET web サイトをスタートアッププロジェクトとして設定し、デバッグを開始します。 ブレークポイントが設定されている管理オブジェクトの1つを呼び出すページにアクセスすると、アプリケーションが停止し、制御がデバッガーに対して有効になります。このとき、図28に示すようにコードをステップ実行できます。

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>手順 13: マネージデータベースオブジェクトを手動でコンパイルして配置する

SQL Server プロジェクトを使用すると、管理されたデータベースオブジェクトの作成、コンパイル、および配置を簡単に行うことができます。 残念ながら、SQL Server プロジェクトは、Visual Studio の Professional および Team Systems エディションでのみ使用できます。 Visual Web Developer または Standard Edition の Visual Studio を使用していて、マネージデータベースオブジェクトを使用する場合は、手動で作成して配置する必要があります。 これには、次の4つのステップが含まれます。

1. マネージデータベースオブジェクトのソースコードを含むファイルを作成します。
2. オブジェクトをアセンブリにコンパイルします。
3. SQL Server 2005 データベースにアセンブリを登録します。
4. SQL Server に、アセンブリ内の適切なメソッドを指すデータベースオブジェクトを作成します。

これらのタスクについて説明するために、で `UnitPrice` 指定した値よりも大きい製品を返す新しいマネージストアドプロシージャを作成します。 コンピューター上にという名前の新しいファイルを作成 `GetProductsWithPriceGreaterThan.vb` し、ファイルに次のコードを入力します (Visual Studio、メモ帳、または任意のテキストエディターを使用してこれを行うことができます)。

[!code-vb[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample17.vb)]

このコードは、 `GetProductsWithPriceLessThan` 手順 5. で作成したメソッドとほぼ同じです。 唯一の違いは、メソッド名、 `WHERE` 句、およびクエリで使用されているパラメーター名です。 メソッドに戻り `GetProductsWithPriceLessThan` 、句を `WHERE` 読み取ります `WHERE UnitPrice < @MaxPrice` 。 ここでは `GetProductsWithPriceGreaterThan` 、を使用 `WHERE UnitPrice > @MinPrice` します。

ここで、このクラスをコンパイルしてアセンブリにする必要があります。 コマンドラインから、ファイルを保存したディレクトリに移動 `GetProductsWithPriceGreaterThan.vb` し、C# コンパイラ () を使用して、 `csc.exe` クラスファイルをアセンブリにコンパイルします。

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample18.cmd)]

V を含むフォルダーがシステムに存在しない場合、 `bc.exe` `PATH` そのパスを完全に参照する必要があり `%WINDOWS%\Microsoft.NET\Framework\version\` ます。次に例を示します。

[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample19.cmd)]

[![GetProductsWithPriceGreaterThan をアセンブリにコンパイルします。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image69.png)

**図 29**: `GetProductsWithPriceGreaterThan.vb` アセンブリにコンパイルする ([クリックすると、フルサイズのイメージが表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image71.png)されます)

フラグは、 `/t` Visual Basic クラスファイルを (実行可能ファイルではなく) DLL にコンパイルする必要があることを指定します。 フラグは、結果として `/out` 得られるアセンブリの名前を指定します。

> [!NOTE]
> `GetProductsWithPriceGreaterThan.vb`コマンドラインからクラスファイルをコンパイルする代わりに、 [Visual Basic Express edition](https://msdn.microsoft.com/vstudio/express/vb/)を使用するか、Visual Studio Standard edition で別のクラスライブラリプロジェクトを作成することもできます。 S ren Jacob Lauritsen には、ストアドプロシージャ用のコードと、 `GetProductsWithPriceGreaterThan` 手順3、5、および10で作成された2つのマネージストアドプロシージャと UDF を含む Visual Basic Express Edition プロジェクトが用意されています。 また、の ren プロジェクトには、対応するデータベースオブジェクトを追加するために必要な T-sql コマンドも含まれています。

アセンブリにコンパイルされたコードを使用して、SQL Server 2005 データベース内にアセンブリを登録する準備ができました。 これを行うには、T-sql を使用するか、コマンド `CREATE ASSEMBLY` または SQL Server Management Studio を使用します。 Management Studio の使用に重点を置いてみましょう。

Management Studio から、Northwind データベースの [プログラミング] フォルダーを展開します。 サブフォルダーの1つはアセンブリです。 新しいアセンブリをデータベースに手動で追加するには、[アセンブリ] フォルダーを右クリックし、コンテキストメニューの [新しいアセンブリ] をクリックします。 [新しいアセンブリ] ダイアログボックスが表示されます (図30を参照)。 [参照] ボタンをクリックして、コンパイルしたアセンブリを選択し、[ `ManuallyCreatedDBObjects.dll` OK] をクリックしてアセンブリをデータベースに追加します。 オブジェクトエクスプローラーにアセンブリが表示されないようにする必要があり `ManuallyCreatedDBObjects.dll` ます。

[![ManuallyCreatedDBObjects.dll アセンブリをデータベースに追加する](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image72.png)

**図 30**: `ManuallyCreatedDBObjects.dll` データベースにアセンブリを追加する ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image74.png)されます)

![ManuallyCreatedDBObjects.dll がオブジェクトエクスプローラーに表示されます。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image75.png)

**図 31**: `ManuallyCreatedDBObjects.dll` オブジェクトエクスプローラーに一覧表示されている

アセンブリは Northwind データベースに追加されていますが、ストアドプロシージャをアセンブリ内のメソッドに関連付けることは `GetProductsWithPriceGreaterThan` できません。 これを行うには、新しいクエリウィンドウを開き、次のスクリプトを実行します。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample20.sql)]

これにより、という名前の Northwind データベースに新しいストアドプロシージャが作成され、 `GetProductsWithPriceGreaterThan` マネージメソッド `GetProductsWithPriceGreaterThan` (アセンブリ内のクラス) に関連付けられ `StoredProcedures` `ManuallyCreatedDBObjects` ます。

上記のスクリプトを実行した後、オブジェクトエクスプローラーの [ストアドプロシージャ] フォルダーを最新の状態に更新します。 新しいストアドプロシージャのエントリが表示され `GetProductsWithPriceGreaterThan` ます。これには、その横にロックアイコンがあります。 このストアドプロシージャをテストするには、クエリウィンドウで次のスクリプトを入力して実行します。

[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/samples/sample21.sql)]

図32に示すように、上記のコマンドでは、$24.95 より大きい製品の情報が表示され `UnitPrice` ます。

[![ManuallyCreatedDBObjects.dll がオブジェクトエクスプローラーに表示されます。](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image76.png)

**図 32**: `ManuallyCreatedDBObjects.dll` がオブジェクトエクスプローラーに一覧表示されている ([クリックすると、フルサイズの画像が表示](creating-stored-procedures-and-user-defined-functions-with-managed-code-vb/_static/image78.png)されます)

## <a name="summary"></a>まとめ

Microsoft SQL Server 2005 は、共通言語ランタイム (CLR) との統合を提供します。これにより、マネージコードを使用してデータベースオブジェクトを作成できます。 以前は、これらのデータベースオブジェクトは T-sql を使用してのみ作成できましたが、Visual Basic などの .NET プログラミング言語を使用してこれらのオブジェクトを作成できるようになりました。 このチュートリアルでは、2つのマネージストアドプロシージャとマネージユーザー定義関数を作成しました。

Visual Studio s SQL Server プロジェクトの種類により、マネージデータベースオブジェクトの作成、コンパイル、配置が容易になります。 さらに、豊富なデバッグ機能が用意されています。 ただし、SQL Server プロジェクトの種類は、Visual Studio の Professional および Team Systems エディションでのみ使用できます。 Visual Web Developer または Standard Edition の Visual Studio を使用している場合は、手順 13. で説明したように、作成、コンパイル、および配置の手順を手動で実行する必要があります。

プログラミングを楽しんでください。

## <a name="further-reading"></a>もっと読む

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [ユーザー定義関数の長所と短所](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [マネージコードでの SQL Server 2005 オブジェクトの作成](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [SQL Server 2005 でマネージコードを使用してトリガーを作成する](http://www.15seconds.com/issue/041006.htm)
- [方法: CLR SQL Server ストアドプロシージャを作成および実行する](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [方法: CLR SQL Server ユーザー定義関数を作成および実行する](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [方法: スクリプトを編集して `Test.sql` SQL オブジェクトを実行する](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [ユーザー定義関数の概要](http://www.sqlteam.com/item.asp?ItemID=1955)
- [マネージコードと SQL Server 2005 (ビデオ)](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Transact-sql リファレンス](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [チュートリアル: マネージコードでのストアドプロシージャの作成](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は [*、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 彼は、にアクセスでき[ mitchell@4GuysFromRolla.com ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは、「」にあり [http://ScottOnWriting.NET](http://ScottOnWriting.NET) ます。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは、Jacob Lauritsen でした。 この記事の内容を確認するだけでなく、この記事のダウンロードに含まれている Visual C# Express Edition プロジェクトを作成して、マネージデータベースオブジェクトを手動でコンパイルすることもできます。 今後の MSDN 記事を確認することに興味がありますか? その場合は、に行をドロップ[ mitchell@4GuysFromRolla.com します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [[戻る]](debugging-stored-procedures-vb.md)
