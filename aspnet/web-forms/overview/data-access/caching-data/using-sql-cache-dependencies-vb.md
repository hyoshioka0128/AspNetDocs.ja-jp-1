---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-vb
title: SQL キャッシュの依存関係を使用する (VB) |Microsoft Docs
author: rick-anderson
description: 最も簡単なキャッシュ方法は、キャッシュされたデータの有効期限が指定した期間後に切れるようにすることです。 ただし、この簡単な方法では、キャッシュされたデータが
ms.author: riande
ms.date: 05/30/2007
ms.assetid: bd347d93-4251-4532-801c-a36f2dfa7f96
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-vb
msc.type: authoredcontent
ms.openlocfilehash: 175169772ba04376e1bd1cb143b13a200652a9bf
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044793"
---
# <a name="using-sql-cache-dependencies-vb"></a>SQL キャッシュ依存関係を使用する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_VB.zip) または [PDF のダウンロード](using-sql-cache-dependencies-vb/_static/datatutorial61vb1.pdf)

> 最も簡単なキャッシュ方法は、キャッシュされたデータの有効期限が指定した期間後に切れるようにすることです。 ただし、この簡単な方法では、キャッシュされたデータが基になるデータソースと関連付けられていないことを意味します。その結果、古いデータが長すぎるか、現在のデータが短時間で期限切れになります。 より優れたアプローチは、SqlCacheDependency クラスを使用して、SQL データベースで基になるデータが変更されるまでデータがキャッシュされたままになるようにすることです。 このチュートリアルでは、その方法を説明します。

## <a name="introduction"></a>概要

アーキテクチャチュートリアルの ObjectDataSource および[キャッシュデータ](caching-data-in-the-architecture-vb.md)[を使用](caching-data-with-the-objectdatasource-vb.md)してデータをキャッシュするキャッシュ技法では、時間ベースの有効期限を使用して、指定した期間の経過後にキャッシュからデータを削除しました。 この方法は、データ staleness に対するキャッシュのパフォーマンス向上のバランスを取るための最も簡単な方法です。 時間の有効期限を *x* 秒に設定すると、ページ開発者は、キャッシュのパフォーマンス上のメリットを *x* 秒だけで concedes ことができます。ただし、データが最大で *x* 秒を超えないようにすることは簡単です。 もちろん、静的なデータの場合、 *x* は web アプリケーションの有効期間に拡張できます。これは、「 [アプリケーションの起動時にデータをキャッシュ](caching-data-at-application-startup-vb.md) する」チュートリアルで確認したものです。

データベースデータをキャッシュする場合、時間ベースの有効期限は使いやすいものとして選択されることがよくありますが、多くの場合、不適切な解決策になります。 データベース内の基になるデータが変更されるまで、データベースのデータはキャッシュされたままになることが理想的です。その後、キャッシュは削除されます。 この方法では、キャッシュのパフォーマンス上の利点が最大限に向上し、古いデータの存続期間を最小限に抑えることができます。 ただし、これらの利点を活用するためには、基になるデータベースデータが変更されたことを認識し、対応する項目をキャッシュから見つけするシステムがいくつか存在している必要があります。 ASP.NET 2.0 より前のページ開発者は、このシステムの実装を担当していました。

ASP.NET 2.0 は、対応するキャッシュされた項目を削除できるように、データベース内で変更が発生したことを判断するために[ `SqlCacheDependency` クラス](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx)と必要なインフラストラクチャを提供します。 基になるデータがどのように変更されたかを判断するには、通知とポーリングの2つの方法があります。 通知とポーリングの違いについて説明した後、ポーリングをサポートするために必要なインフラストラクチャを作成し、 `SqlCacheDependency` 宣言型のシナリオやプログラムによるシナリオでクラスを使用する方法について確認します。

## <a name="understanding-notification-and-polling"></a>通知とポーリングについて

データベース内のデータが変更された日時を判断するには、通知とポーリングの2つの手法を使用できます。 通知を使用すると、クエリが最後に実行されてから特定のクエリの結果が変更されたときに、そのクエリに関連付けられているキャッシュされた項目が削除された時点で、データベースは ASP.NET ランタイムに自動的に警告します。 データベースサーバーは、ポーリングを使用して、特定のテーブルが最後に更新された日時に関する情報を保持します。 ASP.NET ランタイムは、データベースを定期的にポーリングして、キャッシュに入ってから変更されたテーブルを確認します。 データが変更されているテーブルには、関連付けられているキャッシュ項目が削除されます。

通知オプションは、ポーリングよりも設定が少なくて済むため、テーブルレベルではなくクエリレベルで変更が追跡されるため、より詳細な設定が必要になります。 残念ながら、通知は Microsoft SQL Server 2005 (つまり、Express 以外のエディション) の全エディションでのみ利用できます。 ただし、ポーリングオプションは、7.0 から2005のすべてのバージョンの Microsoft SQL Server に使用できます。 これらのチュートリアルでは SQL Server 2005 の Express edition を使用しているため、ポーリングオプションの設定と使用について重点的に説明します。 SQL Server 2005 s の通知機能に関するその他のリソースについては、このチュートリアルの最後にある「参考資料」セクションを参照してください。

ポーリングを使用する場合、データベースは、、 `AspNet_SqlCacheTablesForChangeNotification` 、およびという3つの列を持つという名前のテーブルを含むように構成する必要があり `tableName` `notificationCreated` `changeId` ます。 このテーブルには、web アプリケーションの SQL キャッシュ依存関係で使用する必要があるデータを含むテーブルごとに1行のデータが格納されます。 列には、テーブル `tableName` の名前を指定し `notificationCreated` ます。は、テーブルに行が追加された日時を示します。 `changeId`列の型は `int` で、初期値は0です。 この値は、テーブルへの変更ごとにインクリメントされます。

データベースでは、テーブルに加えて、 `AspNet_SqlCacheTablesForChangeNotification` SQL キャッシュ依存関係に表示される可能性のある各テーブルにトリガーを含める必要もあります。 これらのトリガーは、行が挿入、更新、または削除されるたびに実行され、でテーブルの値をインクリメントし `changeId` `AspNet_SqlCacheTablesForChangeNotification` ます。

ASP.NET ランタイムは、オブジェクトを `changeId` 使用してデータをキャッシュするときに、テーブルの現在のを追跡し `SqlCacheDependency` ます。 データベースは定期的にチェックされ、 `SqlCacheDependency` `changeId` データベース内の値とは異なる値を持つオブジェクトは削除されます。これは、 `changeId` データがキャッシュされてからテーブルに変更があったことを示す値が異なるためです。

## <a name="step-1-exploring-theaspnet_regsqlexecommand-line-program"></a>手順 1: `aspnet_regsql.exe` コマンドラインプログラムの調査

ポーリング方法を使用する場合、データベースは、前に説明したインフラストラクチャを格納するようにセットアップする必要があります。定義済みテーブル ( `AspNet_SqlCacheTablesForChangeNotification` )、いくつかのストアドプロシージャ、および web アプリケーションの SQL キャッシュ依存関係で使用できる各テーブルのトリガーです。 これらのテーブル、ストアドプロシージャ、およびトリガーは、フォルダーにあるコマンドラインプログラムを使用して作成でき `aspnet_regsql.exe` `$WINDOWS$\Microsoft.NET\Framework\version` ます。 `AspNet_SqlCacheTablesForChangeNotification`テーブルおよび関連するストアドプロシージャを作成するには、コマンドラインから次のコマンドを実行します。

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample1.cmd)]

> [!NOTE]
> これらのコマンドを実行するには、指定されたデータベースログインがロールおよびロールに存在する必要があり [`db_securityadmin`](https://msdn.microsoft.com/library/ms188685.aspx) [`db_ddladmin`](https://msdn.microsoft.com/library/ms190667.aspx) ます。 コマンドラインプログラムによってデータベースに送信された T-sql を確認するには、こちらの `aspnet_regsql.exe` [ブログエントリ](http://scottonwriting.net/sowblog/posts/10709.aspx)を参照してください。

たとえば、Windows 認証を使用してという名前のデータベースサーバー上のという名前の Microsoft SQL Server データベースにポーリングするためのインフラストラクチャを追加するには、 `pubs` `ScottsServer` 適切なディレクトリに移動し、コマンドラインで次のように入力します。

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample2.cmd)]

データベースレベルのインフラストラクチャを追加した後、SQL キャッシュの依存関係で使用されるこれらのテーブルにトリガーを追加する必要があります。 コマンドラインプログラムをもう一度使用しますが、スイッチを使用するのではなく、スイッチを使用し `aspnet_regsql.exe` てテーブル名を指定し、 `-t` 次のようにスイッチを使用し `-ed` `-et` ます。

[!code-html[Main](using-sql-cache-dependencies-vb/samples/sample3.html)]

上のデータベースのテーブルおよびテーブルにトリガーを追加するには `authors` `titles` `pubs` `ScottsServer` 、次のように使用します。

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample4.cmd)]

このチュートリアルでは、、、およびの各テーブルにトリガーを追加し `Products` `Categories` `Suppliers` ます。 ここでは、手順 3. の特定のコマンドライン構文について説明します。

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inapp_data"></a>手順 2: で Microsoft SQL Server 2005 Express Edition データベースを参照する`App_Data`

`aspnet_regsql.exe`コマンドラインプログラムでは、必要なポーリングインフラストラクチャを追加するために、データベースとサーバー名が必要です。 しかし、このフォルダーに格納されている Microsoft SQL Server 2005 Express データベースのデータベースとサーバー名はどのようなものです `App_Data` か。 データベースとサーバーの名前を検出するのではなく、データベースを `localhost\SQLExpress` データベースインスタンスにアタッチし、 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)を使用してデータの名前を変更するのが最も簡単な方法です。 SQL Server 2005 の全バージョンがコンピューターにインストールされている場合は、既にコンピューターに SQL Server Management Studio がインストールされている可能性があります。 Express edition のみを使用している場合は、無料の [Microsoft SQL Server Management Studio Express edition](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)をダウンロードできます。

まず、Visual Studio を終了します。 次に、SQL Server Management Studio を開き、 `localhost\SQLExpress` Windows 認証を使用してサーバーへの接続を選択します。

![Localhost\SQLExpress サーバーにアタッチする](using-sql-cache-dependencies-vb/_static/image1.gif)

**図 1**: サーバーに接続する `localhost\SQLExpress`

サーバーに接続すると、Management Studio にサーバーが表示され、データベース、セキュリティなどのサブフォルダーが表示されます。 Databases フォルダーを右クリックし、[アタッチ] オプションを選択します。 [データベースのアタッチ] ダイアログボックスが表示されます (図2を参照)。 [追加] ボタンをクリックし、 `NORTHWND.MDF` web アプリケーション s フォルダー内のデータベースフォルダーを選択し `App_Data` ます。

[![NORTHWND.MDF をアタッチします。App_Data フォルダーからの MDF データベース](using-sql-cache-dependencies-vb/_static/image2.gif)](using-sql-cache-dependencies-vb/_static/image1.png)

**図 2**: `NORTHWND.MDF` フォルダーからデータベースをアタッチ `App_Data` する ([クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-vb/_static/image2.png)されます)

これにより、データベースが [データベース] フォルダーに追加されます。 データベース名には、データベースファイルへの完全なパス、または [GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)を付加した完全パスを指定できます。 Aspnetregsql.exe コマンドラインツールを使用するときに、この長いデータベース名を入力する必要がないようにするには \_ 、アタッチしたデータベースを右クリックし、[名前の変更] をクリックして、データベースの名前をよりわかりやすい名前に変更します。 データベースの名前を DataTutorials に変更しました。

![アタッチされたデータベースの名前を、よりわかりやすい名前に変更します。](using-sql-cache-dependencies-vb/_static/image3.gif)

**図 3**: アタッチされたデータベースの名前を人にわかりやすい名前に変更する

## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>手順 3: ポーリングインフラストラクチャを Northwind データベースに追加する

これで、フォルダーからデータベースがアタッチされたので `NORTHWND.MDF` `App_Data` 、ポーリングインフラストラクチャを追加する準備ができました。 データベースの名前を DataTutorials に変更した場合は、次の4つのコマンドを実行します。

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample5.cmd)]

これらの4つのコマンドを実行した後、Management Studio でデータベース名を右クリックし、[タスク] サブメニューにアクセスして、[デタッチ] を選択します。 次に、Management Studio を閉じて、Visual Studio を再度開きます。

Visual Studio を再び開いたら、サーバーエクスプローラーを使用してデータベースをドリルダウンします。 新しいテーブル ( `AspNet_SqlCacheTablesForChangeNotification` )、新しいストアドプロシージャ、およびテーブルのトリガーに注意して `Products` `Categories` `Suppliers` ください。

![データベースに必要なポーリングインフラストラクチャが含まれるようになりました](using-sql-cache-dependencies-vb/_static/image4.gif)

**図 4**: データベースに必要なポーリングインフラストラクチャが含まれるようになった

## <a name="step-4-configuring-the-polling-service"></a>手順 4: ポーリングサービスを構成する

データベースに必要なテーブル、トリガー、およびストアドプロシージャを作成したら、最後の手順として、 `Web.config` 使用するデータベースとポーリング頻度をミリ秒単位で指定することによって、ポーリングサービスを構成します。 次のマークアップは、1秒ごとに Northwind データベースをポーリングします。

[!code-xml[Main](using-sql-cache-dependencies-vb/samples/sample6.xml)]

`name`要素の値 `<add>` (NorthwindDB) により、人間が判読できる名前が特定のデータベースに関連付けられます。 SQL キャッシュの依存関係を使用する場合は、ここで定義されているデータベース名と、キャッシュされたデータの基になっているテーブルを参照する必要があります。 クラスを使用して、 `SqlCacheDependency` 手順 6. で SQL キャッシュの依存関係とキャッシュされたデータをプログラムで関連付ける方法について説明します。

SQL キャッシュの依存関係が確立されると、ポーリングシステムは、要素で定義されているデータベースに 1 `<databases>` ミリ秒ごとに接続 `pollTime` し、ストアドプロシージャを実行し `AspNet_SqlCachePollingStoredProcedure` ます。 コマンドラインツールを使用して手順 3. で追加したこのストアドプロシージャは、 `aspnet_regsql.exe` `tableName` `changeId` の各レコードの値と値を返し `AspNet_SqlCacheTablesForChangeNotification` ます。 古くなった SQL キャッシュ依存関係はキャッシュから削除されます。

この設定により、 `pollTime` パフォーマンスとデータ staleness のトレードオフが生じます。 小さい値を指定すると、 `pollTime` データベースへの要求数が増加しますが、キャッシュから古いデータをより迅速に見つけます。 大きな値を指定すると、 `pollTime` データベース要求の数が減少しますが、バックエンドデータが変更されてから関連するキャッシュ項目が削除されるまでの間の遅延が増加します。 幸いなことに、データベース要求では、単純な簡易テーブルから少数の行を返す単純なストアドプロシージャを実行しています。 ただし、 `pollTime` アプリケーションのデータベースアクセスとデータ staleness の間で最適なバランスを見つけるために、さまざまな値を試してみることをお勧めします。 `pollTime`許容される最小値は500です。

> [!NOTE]
> 上の例では、 `pollTime` 要素に1つの値を `<sqlCacheDependency>` 指定しますが、必要に応じて要素の値を指定することもでき `pollTime` `<add>` ます。 これは、複数のデータベースを指定し、データベースごとにポーリング頻度をカスタマイズする場合に便利です。

## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>手順 5: SQL キャッシュの依存関係を宣言的に操作する

手順 1. ~ 4. で、必要なデータベースインフラストラクチャを設定し、ポーリングシステムを構成する方法を説明しました。 このインフラストラクチャが整ったら、プログラムまたは宣言的手法を使用して、関連付けられた SQL キャッシュ依存関係を持つ項目をデータキャッシュに追加できるようになりました。 この手順では、SQL キャッシュの依存関係を宣言によって操作する方法を確認します。 手順 6. では、プログラムによるアプローチについて説明します。

[Objectdatasource チュートリアルを使用したキャッシュデータ](caching-data-with-the-objectdatasource-vb.md)では、objectdatasource の宣言型キャッシュ機能について説明しています。 プロパティをに、 `EnableCaching` プロパティを `True` 一定の `CacheDuration` 時間間隔に設定するだけで、ObjectDataSource は、基になるオブジェクトから返されたデータを指定された間隔で自動的にキャッシュします。 ObjectDataSource では、1つまたは複数の SQL キャッシュの依存関係を使用することもできます。

SQL キャッシュの依存関係を宣言によって使用する方法を示すには、フォルダー内のページを開き、 `SqlCacheDependencies.aspx` `Caching` GridView をツールボックスからデザイナーにドラッグします。 GridView をに設定 `ID` し `ProductsDeclarative` 、そのスマートタグから、という名前の新しい ObjectDataSource にバインドするように選択し `ProductsDataSourceDeclarative` ます。

[![新しい ObjectDataSource 名前付き製品 Datasource宣言を作成します。](using-sql-cache-dependencies-vb/_static/image5.gif)](using-sql-cache-dependencies-vb/_static/image3.png)

**図 5**: 新しい ObjectDataSource という名前のを作成 `ProductsDataSourceDeclarative` [する (クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-vb/_static/image4.png)される)

クラスを使用するように ObjectDataSource を構成 `ProductsBLL` し、[選択] タブのドロップダウンリストをに設定し `GetProducts()` ます。 [更新] タブで、 `UpdateProduct` 3 つの入力パラメーター (、、) を持つオーバーロードを選択し `productName` `unitPrice` `productID` ます。 [挿入] タブと [削除] タブで、ドロップダウンリストを [(なし)] に設定します。

[![3つの入力パラメーターで UpdateProduct オーバーロードを使用する](using-sql-cache-dependencies-vb/_static/image6.gif)](using-sql-cache-dependencies-vb/_static/image5.png)

**図 6**: 3 つの入力パラメーターを使用して Updateproduct オーバーロードを使用する ([クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-vb/_static/image6.png)されます)

[![[挿入] タブと [削除] タブで、ドロップダウンリストを [(なし)] に設定します。](using-sql-cache-dependencies-vb/_static/image7.gif)](using-sql-cache-dependencies-vb/_static/image7.png)

**図 7**: 挿入と削除のタブでドロップダウンリストを (なし) に設定する ([クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-vb/_static/image8.png)されます)

データソースの構成ウィザードを完了すると、Visual Studio によって、各データフィールドの GridView に BoundFields と CheckBoxFields が作成されます。 、、およびのすべてのフィールドを削除 `ProductName` `CategoryName` し、必要に `UnitPrice` 応じてこれらのフィールドの書式を設定します。 GridView s スマートタグから、[ページングを有効にする]、[並べ替えを有効にする]、および [編集を有効にする] チェックボックスをオンにします。 Visual Studio によって、ObjectDataSource s プロパティがに設定され `OldValuesParameterFormatString` `original_{0}` ます。 GridView s edit 機能が正常に機能するためには、このプロパティを宣言構文から完全に削除するか、既定値であるに設定し直 `{0}` します。

最後に、GridView の上にラベル Web コントロールを追加し、その `ID` プロパティをに `ODSEvents` 、プロパティをに設定し `EnableViewState` `False` ます。 これらの変更を行った後、ページの宣言型マークアップは次のようになります。 SQL キャッシュの依存関係機能を示すために必要ではない GridView フィールドに対して、いくつかのカスタマイズされたカスタマイズを行ったことに注意してください。

[!code-aspx[Main](using-sql-cache-dependencies-vb/samples/sample7.aspx)]

次に、ObjectDataSource s イベントのイベントハンドラーを作成 `Selecting` し、その中に次のコードを追加します。

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample8.vb)]

ObjectDataSource s イベントは、 `Selecting` 基になるオブジェクトからデータを取得するときにのみ発生することを思い出してください。 ObjectDataSource が独自のキャッシュからデータにアクセスする場合、このイベントは発生しません。

ここでは、ブラウザーを使用してこのページにアクセスします。 まだキャッシュを実装していないので、グリッドをページ表示、並べ替え、または編集するたびに、ページに "選択したイベントが発生しました" というテキストが表示されます。図8に示します。

[![ObjectDataSource s 選択イベントは、GridView がページング、編集、または並べ替えのたびに発生します。](using-sql-cache-dependencies-vb/_static/image8.gif)](using-sql-cache-dependencies-vb/_static/image9.png)

**図 8**: ObjectDataSource s イベントは、 `Selecting` GridView がページング、編集、または並べ替えられるたびに発生します ([クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-vb/_static/image10.png)されます)

「 [Objectdatasource チュートリアルを使用](caching-data-with-the-objectdatasource-vb.md) したデータのキャッシュ」で説明したように、プロパティをに設定すると、 `EnableCaching` `True` objectdatasource によって、プロパティで指定された期間のデータがキャッシュされ `CacheDuration` ます。 ObjectDataSource には、次のパターンを使用して、キャッシュされたデータに1つ以上の SQL キャッシュの依存関係を追加する[ `SqlCacheDependency` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx)もあります。

[!code-css[Main](using-sql-cache-dependencies-vb/samples/sample9.css)]

ここで、 *databaseName* は、の要素の属性で指定されているデータベースの名前です `name` `<add>` `Web.config` 。 *tableName* はデータベーステーブルの名前です。 たとえば、Northwind s テーブルに対する SQL キャッシュの依存関係に基づいてデータを無期限にキャッシュする ObjectDataSource を作成するには、 `Products` objectdatasource s `EnableCaching` プロパティをに設定し、 `True` その `SqlCacheDependency` プロパティを NorthwindDB: Products に設定します。

> [!NOTE]
> SQL キャッシュの依存関係 *と* 時間ベースの有効期限を使用するに `EnableCaching` は `True` 、をに、を `CacheDuration` 時間間隔に、 `SqlCacheDependency` データベースとテーブル名をに設定します。 時間ベースの有効期限に達した場合、または、基になるデータベースデータが変更されたことがポーリングシステムによって記録された場合、ObjectDataSource はデータを削除します。

の GridView には、 `SqlCacheDependencies.aspx` 2 つのテーブルのデータが表示され `Products` `Categories` ます (製品 s `CategoryName` フィールドは、を使用して取得され `JOIN` `Categories` ます)。 そのため、SQL キャッシュの依存関係を2つ指定します。 NorthwindDB: Products;NorthwindDB: カテゴリ。

[![製品とカテゴリの SQL キャッシュ依存関係を使用してキャッシュをサポートするように ObjectDataSource を構成する](using-sql-cache-dependencies-vb/_static/image9.gif)](using-sql-cache-dependencies-vb/_static/image11.png)

**図 9**: とで SQL キャッシュの依存関係を使用してキャッシュをサポートするように ObjectDataSource を構成する `Products` `Categories` ([クリックしてフルサイズのイメージを表示する](using-sql-cache-dependencies-vb/_static/image12.png))

キャッシュをサポートするように ObjectDataSource を構成したら、ブラウザーを使用してページに戻ります。 ここでも、"選択したイベントが発生しました" というテキストは最初のページに移動したときに表示されますが、ページング、並べ替え、または [編集] ボタンまたは [キャンセル] ボタンをクリックすると消えます。 これは、データが ObjectDataSource のキャッシュに読み込まれた後、 `Products` テーブルまたは `Categories` テーブルが変更されるか、GridView によってデータが更新されるまで、データはそのまま保持されるためです。

グリッドをページングし、[イベントが発生したイベントの選択] がないことを示すために、新しいブラウザーウィンドウを開き、[編集]、[挿入]、および [削除] セクション () の基本チュートリアルに移動し `~/EditInsertDelete/Basics.aspx` ます。 製品の名前または価格を更新します。 次に、最初のブラウザーウィンドウに対して、別のデータページを表示するか、グリッドを並べ替えるか、または行 s の [編集] ボタンをクリックします。 ここでは、基になるデータベースデータが変更されたため、"選択したイベントが再表示されました。" と表示されます (図10を参照)。 テキストが表示されない場合は、しばらく待ってからもう一度やり直してください。 ポーリングサービスは、ミリ秒ごとにテーブルへの変更を確認しているので、基になるデータが更新されてからキャッシュされ `Products` `pollTime` たデータが削除されるまでの間に遅延が発生します。

[![Products テーブルを変更して、キャッシュされた製品データを見つけ](using-sql-cache-dependencies-vb/_static/image10.gif)](using-sql-cache-dependencies-vb/_static/image13.png)

**図 10**: Products テーブルを変更してキャッシュされた製品データを見つけ[する (クリックしてフルサイズの画像を表示する](using-sql-cache-dependencies-vb/_static/image14.png))

## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>手順 6: プログラムでクラスを操作する `SqlCacheDependency`

アーキテクチャチュートリアルの [キャッシュデータ](caching-data-in-the-architecture-vb.md) は、キャッシュと ObjectDataSource を密に結合するのではなく、アーキテクチャで個別のキャッシュレイヤーを使用する利点を確認しました。 このチュートリアルでは、 `ProductsCL` データキャッシュをプログラムで操作する方法を示すクラスを作成しました。 キャッシュレイヤーで SQL キャッシュの依存関係を利用するには、クラスを使用し `SqlCacheDependency` ます。

ポーリングシステムでは、 `SqlCacheDependency` オブジェクトは特定のデータベースとテーブルのペアに関連付けられている必要があります。 たとえば、次のコードでは、 `SqlCacheDependency` Northwind データベースのテーブルに基づいてオブジェクトを作成し `Products` ます。

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample10.vb)]

S コンストラクターに対する2つの入力パラメーター `SqlCacheDependency` は、それぞれデータベース名とテーブル名です。 ObjectDataSource s プロパティと同様に `SqlCacheDependency` 、使用されるデータベース名は、の `name` 要素の属性で指定された値と同じです `<add>` `Web.config` 。 テーブル名は、データベーステーブルの実際の名前です。

`SqlCacheDependency`データキャッシュに追加された項目にを関連付けるには、 `Insert` 依存関係を受け入れるメソッドオーバーロードのいずれかを使用します。 次のコードでは、永続的な期間のデータキャッシュに *値* が追加されますが、テーブルのに関連付けられ `SqlCacheDependency` `Products` ます。 つまり、メモリの制約によって削除されるまで、またはポーリングシステムによってテーブルがキャッシュされてから変更されたことが検出されるまで、 *値* はキャッシュに保持され `Products` ます。

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample11.vb)]

キャッシュレイヤー s クラスは、 `ProductsCL` 現在、 `Products` 時間ベースの有効期限60秒を使用してテーブルのデータをキャッシュします。 代わりに、SQL キャッシュの依存関係を使用するように、このクラスを更新してみましょう。 `ProductsCL`データをキャッシュに追加するクラスのメソッドには、現在、 `AddCacheItem` 次のコードが含まれています。

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample12.vb)]

`SqlCacheDependency`キャッシュ依存関係の代わりにオブジェクトを使用するように、このコードを更新し `MasterCacheKeyArray` ます。

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample13.vb)]

この機能をテストするには、既存の gridview の下にあるページに GridView を追加し `ProductsDeclarative` ます。 この新しい GridView をに設定し、 `ID` `ProductsProgrammatic` そのスマートタグを使用して、という名前の新しい ObjectDataSource にバインドし `ProductsDataSourceProgrammatic` ます。 クラスを使用するように ObjectDataSource を構成し `ProductsCL` 、[選択] タブと [更新] タブのドロップダウンリストをそれぞれとに設定し `GetProducts` `UpdateProduct` ます。

[![ProductsCL クラスを使用するように ObjectDataSource を構成する](using-sql-cache-dependencies-vb/_static/image11.gif)](using-sql-cache-dependencies-vb/_static/image15.png)

**図 11**: クラスを使用するように ObjectDataSource を構成する `ProductsCL` ([クリックすると、フルサイズのイメージが表示](using-sql-cache-dependencies-vb/_static/image16.png)されます)

[![[SELECT Tab s] ドロップダウンリストから GetProducts メソッドを選択します。](using-sql-cache-dependencies-vb/_static/image12.gif)](using-sql-cache-dependencies-vb/_static/image17.png)

**図 12**: [ `GetProducts` Select Tab s] ドロップダウンリストからメソッドを選択[する (クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-vb/_static/image18.png)されます)

[![[更新] タブのドロップダウンリストから、UpdateProduct メソッドを選択します。](using-sql-cache-dependencies-vb/_static/image13.gif)](using-sql-cache-dependencies-vb/_static/image19.png)

**図 13**: [更新] タブのドロップダウンリストから Updateproduct メソッドを選択[する (クリックすると、フルサイズの画像が表示](using-sql-cache-dependencies-vb/_static/image20.png)されます)

データソースの構成ウィザードを完了すると、Visual Studio によって、各データフィールドの GridView に BoundFields と CheckBoxFields が作成されます。 このページに最初に追加された GridView と同様に、 `ProductName` 、、およびのすべてのフィールドを削除 `CategoryName` し、必要に `UnitPrice` 応じてこれらのフィールドの書式を設定します。 GridView s スマートタグから、[ページングを有効にする]、[並べ替えを有効にする]、および [編集を有効にする] チェックボックスをオンにします。 Objectdatasource と同様に `ProductsDataSourceDeclarative` 、Visual Studio は `ProductsDataSourceProgrammatic` objectdatasource s `OldValuesParameterFormatString` プロパティをに設定し `original_{0}` ます。 GridView s edit 機能が正常に機能するためには、このプロパティをに戻し `{0}` ます (または、プロパティの割り当てを宣言構文から完全に削除します)。

これらのタスクを完了すると、結果として得られる GridView および ObjectDataSource の宣言マークアップは次のようになります。

[!code-aspx[Main](using-sql-cache-dependencies-vb/samples/sample14.aspx)]

キャッシュ層で SQL キャッシュの依存関係をテストするには、クラス s メソッドにブレークポイントを設定 `ProductCL` `AddCacheItem` し、デバッグを開始します。 初めてアクセスするときは `SqlCacheDependencies.aspx` 、データが最初に要求され、キャッシュに格納されるため、ブレークポイントにヒットします。 次に、GridView 内の別のページに移動するか、いずれかの列を並べ替えます。 これにより、GridView はデータを再クエリしますが、 `Products` データベーステーブルが変更されていないため、データがキャッシュに格納されます。 データがキャッシュに繰り返し見つからない場合は、コンピューターに十分なメモリがあることを確認してから、もう一度やり直してください。

GridView のいくつかのページを使用してページングを行った後、2番目のブラウザーウィンドウを開き、[編集]、[挿入]、および [削除] セクション () の基本チュートリアルに移動し `~/EditInsertDelete/Basics.aspx` ます。 Products テーブルからレコードを更新してから、最初のブラウザーウィンドウから新しいページを表示するか、並べ替えヘッダーのいずれかをクリックします。

このシナリオでは、次の2つのいずれかが表示されます。ブレークポイントがヒットすると、データベースの変更によってキャッシュデータが削除されたことを示します。または、ブレークポイントにヒットしません。つまり、によって古いデータが表示されるようになり `SqlCacheDependencies.aspx` ます。 ブレークポイントにヒットしない場合は、データが変更されてからポーリングサービスがまだ起動していない可能性があります。 ポーリングサービスは、ミリ秒ごとにテーブルへの変更を確認しているので、基になるデータが更新されてからキャッシュされ `Products` `pollTime` たデータが削除されるまでの間に遅延が発生します。

> [!NOTE]
> この遅延は、の GridView を通じて製品の1つを編集するときに表示される可能性が高く `SqlCacheDependencies.aspx` なります。 アーキテクチャチュートリアルの [キャッシュデータ](caching-data-in-the-architecture-vb.md) では、キャッシュ依存関係を追加して、 `MasterCacheKeyArray` クラス s メソッドによって編集されるデータが `ProductsCL` キャッシュから削除されたことを確認しまし `UpdateProduct` た。 ただし、この手順の前半でメソッドを変更するときには、このキャッシュの依存関係を置き換えました `AddCacheItem` 。したがって、クラスは、ポーリングシステムによって `ProductsCL` テーブルの変更が確認されるまで、キャッシュされたデータを引き続き表示し `Products` ます。 手順 7. でキャッシュの依存関係を導入する方法について説明し `MasterCacheKeyArray` ます。

## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>手順 7: キャッシュされた項目に複数の依存関係を関連付ける

`MasterCacheKeyArray`キャッシュ依存関係を使用して、*すべて*の製品関連データが、関連付けられている1つの項目が更新されたときにキャッシュから確実に削除されることを思い出してください。 たとえば、メソッドは、 `GetProductsByCategoryID(categoryID)` `ProductsDataTables` 一意の *categoryID* 値ごとにインスタンスをキャッシュします。 これらのオブジェクトのいずれかが削除さ `MasterCacheKeyArray` れると、キャッシュの依存関係によって、他のオブジェクトも削除されます。 このキャッシュ依存関係がない場合、キャッシュされたデータが変更されると、他のキャッシュされた製品データが古くなっている可能性があります。 そのため、 `MasterCacheKeyArray` SQL キャッシュの依存関係を使用する場合は、キャッシュの依存関係を維持することが重要です。 ただし、data cache s メソッドでは、 `Insert` 単一の依存関係オブジェクトのみが許可されます。

さらに、SQL キャッシュの依存関係を使用する場合は、複数のデータベーステーブルを依存関係として関連付けることが必要になる場合があります。 たとえば、 `ProductsDataTable` クラスにキャッシュされたには、 `ProductsCL` 各製品のカテゴリ名と仕入先名が含まれていますが、 `AddCacheItem` メソッドはの依存関係のみを使用し `Products` ます。 この場合、ユーザーがカテゴリまたは供給業者の名前を更新すると、キャッシュされた製品データはキャッシュに残り、期限切れになります。 そのため、キャッシュされた製品データをテーブルだけでなく、テーブル `Products` とテーブルにも依存させる必要が `Categories` `Suppliers` あります。

[ `AggregateCacheDependency` クラス](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx)は、複数の依存関係をキャッシュ項目に関連付けるための手段を提供します。 まず、インスタンスを作成し `AggregateCacheDependency` ます。 次に、s メソッドを使用して依存関係のセットを追加し `AggregateCacheDependency` `Add` ます。 その後、データキャッシュに項目を挿入するときに、 `AggregateCacheDependency` インスタンスを渡します。 インスタンスの *いずれか* の依存関係が変更されると、キャッシュされ `AggregateCacheDependency` た項目は削除されます。

クラス s メソッドの更新されたコードを次に示し `ProductsCL` `AddCacheItem` ます。 メソッドは `MasterCacheKeyArray` `SqlCacheDependency` 、、、およびの各テーブルのオブジェクトと共に、キャッシュの依存関係を作成し `Products` `Categories` `Suppliers` ます。 これらはすべて `AggregateCacheDependency` 、という名前の1つのオブジェクトに結合さ `aggregateDependencies` れ、その後、メソッドに渡され `Insert` ます。

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample15.vb)]

この新しいコードをテストします。これで、、、またはの各テーブルに変更を加える `Products` `Categories` と、 `Suppliers` キャッシュされたデータが削除されます。 さらに、 `ProductsCL` クラス s `UpdateProduct` メソッドは、GridView を通じて製品を編集するときに呼び出され、 `MasterCacheKeyArray` キャッシュの依存関係を見つけします。これにより、キャッシュされたが `ProductsDataTable` 削除され、次の要求でデータが再取得されます。

> [!NOTE]
> SQL キャッシュの依存関係は、 [出力キャッシュ](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx)と共に使用することもできます。 この機能のデモンストレーションについては、「 [SQL Server での ASP.NET 出力キャッシュの使用](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx)」を参照してください。

## <a name="summary"></a>まとめ

データベースデータをキャッシュする場合、データはデータベースで変更されるまでキャッシュに保持されるのが理想的です。 ASP.NET 2.0 を使用すると、SQL キャッシュの依存関係を作成し、宣言型とプログラムによる両方のシナリオで使用できます。 この方法の課題の1つは、データが変更されたときの検出です。 Microsoft SQL Server 2005 の完全バージョンでは、クエリの結果が変更されたときにアプリケーションを警告できる通知機能を提供します。 SQL Server 2005 とそれ以前のバージョンの SQL Server の Express Edition では、代わりにポーリングシステムを使用する必要があります。 幸いにも、必要なポーリングインフラストラクチャの設定は非常に簡単です。

プログラミングを楽しんでください。

## <a name="further-reading"></a>もっと読む

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [Microsoft SQL Server 2005 でのクエリ通知の使用](https://msdn.microsoft.com/library/ms175110.aspx)
- [クエリ通知の作成](https://msdn.microsoft.com/library/ms188669.aspx)
- [クラスを使用した ASP.NET でのキャッシュ `SqlCacheDependency`](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [ASP.NET SQL Server 登録ツール ( `aspnet_regsql.exe` )](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [概要 `SqlCacheDependency`](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は [*、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 彼は、にアクセスでき[ mitchell@4GuysFromRolla.com ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは、「」にあり [http://ScottOnWriting.NET](http://ScottOnWriting.NET) ます。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Marko Rangel、Teresa Murphy、および Hilton Giesenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、に行をドロップ[ mitchell@4GuysFromRolla.com します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [[戻る]](caching-data-at-application-startup-vb.md)
