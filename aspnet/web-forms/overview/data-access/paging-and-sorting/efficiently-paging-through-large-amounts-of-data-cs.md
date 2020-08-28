---
uid: web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs
title: 大量のデータを効率的にページングする (C#) |Microsoft Docs
author: rick-anderson
description: データ表示コントロールの既定のページングオプションは、大量のデータを操作する場合は、基になるデータソースコントロール retriev...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 59c01998-9326-4ecb-9392-cb9615962140
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 154bcfeed8e64869b7c32d35b4fb05b6e611dadc
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045274"
---
# <a name="efficiently-paging-through-large-amounts-of-data-c"></a>大量のデータを効率的にページングする (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_25_CS.exe) または [PDF のダウンロード](efficiently-paging-through-large-amounts-of-data-cs/_static/datatutorial25cs1.pdf)

> データ表示コントロールの既定のページングオプションは、データのサブセットのみが表示されている場合でも、基になるデータソースコントロールによってすべてのレコードが取得されるため、大量のデータを処理する場合には適していません。 このような状況では、カスタムページングを有効にする必要があります。

## <a name="introduction"></a>概要

前のチュートリアルで説明したように、ページングは次の2つの方法のいずれかで実装できます。

- **既定のページング** は、データ Web コントロール s スマートタグの [ページングの有効化] オプションをオンにするだけで実装できます。ただし、データページを表示するたびに、ObjectDataSource によって *すべて* のレコードが取得されますが、それらのサブセットのみがページに表示されます。
- **カスタムページング** を使用すると、ユーザーによって要求されたデータの特定のページに表示する必要があるレコードだけをデータベースから取得することで、既定のページングのパフォーマンスが向上します。ただし、カスタムページングでは、既定のページングよりも実装に多少の労力が必要になります。

実装が簡単であるため、チェックボックスをオンにするだけで完了です。 既定のページングは魅力的なオプションです。 ただし、すべてのレコードを取得するための単純なアプローチでは、大量のデータをページングする場合や、多数の同時ユーザーがいるサイトの場合は、信じを選択できます。 このような状況では、応答性の高いシステムを提供するために、カスタムページングを有効にする必要があります。

カスタムページングの課題は、データの特定のページに必要なレコードの正確なセットを返すクエリを記述できることです。 幸い Microsoft SQL Server 2005 では、結果の順位付けに新しいキーワードが提供されているため、レコードの適切なサブセットを効率的に取得するためのクエリを作成できます。 このチュートリアルでは、この新しい SQL Server 2005 キーワードを使用して、GridView コントロールにカスタムページングを実装する方法について説明します。 カスタムページング用のユーザーインターフェイスは、既定のページングの場合と同じですが、カスタムページングを使用して1つのページから次のページにステップインすると、既定のページングよりもはるかに高速に処理されることがあります。

> [!NOTE]
> カスタムページングによって発生する実際のパフォーマンスの向上は、ページングされているレコードの総数と、データベースサーバーへの負荷の発生回数によって異なります。 このチュートリアルの最後では、カスタムページングを通じて得られるパフォーマンスの利点を示す、いくつかの大まかなメトリックについて説明します。

## <a name="step-1-understanding-the-custom-paging-process"></a>手順 1: カスタムページングプロセスを理解する

データをページングする場合、ページに表示される正確なレコードは、要求されているデータのページと、ページごとに表示されるレコードの数によって異なります。 たとえば、ページごとに10個の製品を表示して81製品を使用するとします。 最初のページを表示するときは、製品 1 ~ 10 が必要です。2番目のページを表示する場合は、製品 11 ~ 20 を対象としています。

取得する必要があるレコードと、ページングインターフェイスをどのようにレンダリングするかを決定する変数が3つあります。

- **開始行インデックス** 表示するデータページの最初の行のインデックス。このインデックスを計算するには、ページインデックスに、ページごとに表示するレコードを乗算して追加します。 たとえば、(ページインデックスが0である) 最初のページに対して一度に10個のレコードを使用する場合、開始行インデックスは 0 \* 10 + 1 または1になります。2ページ目 (ページインデックスが 1) の場合、開始行インデックスは 1 \* 10 + 1 または11になります。
- [**最大行数**] ページごとに表示するレコードの最大数。 最後のページでは、ページサイズよりも多くのレコードが返される可能性があるため、この変数は最大行数と呼ばれます。 たとえば、ページごとに81製品10件のレコードをページングする場合、9番目と最後のページには1つのレコードのみが表示されます。 ただし、ページがない場合は、[最大行数] の値よりも多くのレコードが表示されます。
- **合計レコード数** ページングされているレコードの合計数。 この変数は、特定のページに対して取得するレコードを決定するために必要ではありませんが、ページングインターフェイスを決定します。 たとえば、81製品がページングされている場合、ページングインターフェイスはページング UI に9ページの番号を表示することを認識します。

既定のページングでは、開始行インデックスは、ページインデックスとページサイズの積として計算されます。一方、最大行数は単にページサイズになります。 既定のページングでは、データのページを表示するときに、データベースからすべてのレコードが取得されるため、各行のインデックスが認識されるため、開始行のインデックス行を簡単なタスクに移動できます。 さらに、レコード数の合計はすぐに使用できます。これは、DataTable 内のレコードの数 (または、データベースの結果を保持するために使用されている任意のオブジェクト) にすぎません。

開始行インデックスと最大行数変数を指定した場合、カスタムページングの実装では、先頭行のインデックスから始まるレコードの正確なサブセットと、その後の最大行数までのレコードのみを返す必要があります。 カスタムページングには2つの課題があります。

- 行インデックスは、ページングされているデータ全体の各行に効率的に関連付ける必要があります。これにより、指定された開始行インデックスでレコードを返すことができます。
- ページングされているレコードの合計数を指定する必要があります

次の2つの手順では、これら2つの課題に対応するために必要な SQL スクリプトを確認します。 SQL スクリプトに加えて、DAL および BLL でメソッドを実装する必要もあります。

## <a name="step-2-returning-the-total-number-of-records-being-paged-through"></a>手順 2: ページングされているレコードの合計数を取得する

表示されるページのレコードの正確なサブセットを取得する方法を確認する前に、まず、ページングされているレコードの合計数を取得する方法を見てみましょう。 この情報は、ページングユーザーインターフェイスを適切に構成するために必要です。 特定の SQL クエリによって返されるレコードの合計数は、 [ `COUNT` 集計関数](https://msdn.microsoft.com/library/ms175997.aspx)を使用して取得できます。 たとえば、テーブル内のレコードの合計数を確認するに `Products` は、次のクエリを使用します。

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample1.sql)]

この情報を返すメソッドを DAL に追加してみましょう。 特に、前に示したステートメントを実行するという DAL メソッドを作成 `TotalNumberOfProducts()` `SELECT` します。

まず、型指定された `Northwind.xsd` データセットファイルをフォルダーで開き `App_Code/DAL` ます。 次に、デザイナーでを右クリックし、[ `ProductsTableAdapter` クエリの追加] を選択します。 前のチュートリアルで説明したように、これにより、新しいメソッドを DAL に追加することができます。このメソッドを呼び出すと、特定の SQL ステートメントまたはストアドプロシージャが実行されます。 この記事では、前のチュートリアルの TableAdapter メソッドと同様に、アドホック SQL ステートメントを使用することを選択します。

![アドホック SQL ステートメントを使用する](efficiently-paging-through-large-amounts-of-data-cs/_static/image1.png)

**図 1**: アドホック SQL ステートメントを使用する

次の画面で、作成するクエリの種類を指定できます。 このクエリは単一のスカラー値を返すため、テーブル内のレコードの合計数は、1つの `Products` 値を返すオプションを選択し `SELECT` ます。

![1つの値を返す SELECT ステートメントを使用するようにクエリを構成する](efficiently-paging-through-large-amounts-of-data-cs/_static/image2.png)

**図 2**: 単一の値を返す SELECT ステートメントを使用するようにクエリを構成する

使用するクエリの種類を指定したら、次にクエリを指定する必要があります。

![SELECT COUNT (*) FROM Products クエリ](efficiently-paging-through-large-amounts-of-data-cs/_static/image3.png)

**図 3**: Products クエリから SELECT COUNT () を使用する \*

最後に、メソッドの名前を指定します。 前述のように、を使用 `TotalNumberOfProducts` します。

![DAL メソッドに TotalNumberOfProducts という名前を指定する](efficiently-paging-through-large-amounts-of-data-cs/_static/image4.png)

**図 4**: DAL メソッド TotalNumberOfProducts に名前を指定する

[完了] をクリックすると、ウィザードによって DAL にメソッドが追加され `TotalNumberOfProducts` ます。 SQL クエリの結果がの場合、DAL 内のスカラーを返すメソッドは、null 許容型を返し `NULL` ます。 `COUNT`ただし、クエリでは常に値以外が返されます `NULL` 。 DAL メソッドは null 許容の整数を返します。

DAL メソッドに加えて、BLL にもメソッドが必要です。 クラスファイルを開き、 `ProductsBLL` `TotalNumberOfProducts` 単に DAL のメソッドを呼び出すメソッドを追加し `TotalNumberOfProducts` ます。

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample2.cs)]

DAL のメソッドは、 `TotalNumberOfProducts` null 許容の整数を返します。ただし、クラス s メソッドを作成して、 `ProductsBLL` 標準の整数を `TotalNumberOfProducts` 返すようにしました。 そのため、クラスのメソッドから、 `ProductsBLL` `TotalNumberOfProducts` DAL のメソッドによって返される null 許容の整数値の部分を返す必要があり `TotalNumberOfProducts` ます。 を呼び出すと、 `GetValueOrDefault()` null 許容の整数が存在する場合はその値が返されます。 null 許容の整数がの場合は、 `null` 既定の整数値0が返されます。

## <a name="step-3-returning-the-precise-subset-of-records"></a>手順 3: レコードの正確なサブセットを取得する

次のタスクでは、DAL でメソッドを作成します。このメソッドは、前に説明した行の開始インデックスと最大行数変数を受け取り、適切なレコードを返します。 これを行う前に、まず必要な SQL スクリプトを見てみましょう。 私たちが直面する課題は、開始行のインデックス (およびレコードの最大数) で開始されたレコードだけを返すことができるように、結果全体の行にインデックスを効率的に割り当てることができることです。

これは、データベーステーブルに行インデックスとして機能する列が既に存在する場合は問題になりません。 一見すると、 `Products` `ProductID` 最初の製品が `ProductID` 1、2番目の製品が2であるため、テーブルのフィールドは十分であると思うかもしれません。 ただし、製品を削除すると、シーケンスのギャップが残りますので、この方法は無効化です。

行インデックスをデータに効率的に関連付けるために使用される一般的な手法には、次の2つがあります。これにより、レコードの正確なサブセットを取得できるようになります。

- **SQL Server 2005 s `ROW_NUMBER()` の使用キーワード** new SQL Server 2005 の場合、 `ROW_NUMBER()` キーワードは、順序付けに基づいて、返された各レコードに順位を関連付けます。 この順位付けは、各行の行インデックスとして使用できます。
- **テーブル変数と `SET ROWCOUNT` を使用する**SQL Server s [ `SET ROWCOUNT` ステートメント](https://msdn.microsoft.com/library/ms188774.aspx)を使用して、クエリが終了する前に処理する必要があるレコードの合計数を指定できます。[テーブル変数](http://www.sqlteam.com/item.asp?ItemID=9454)は、[一時テーブル](http://www.sqlteam.com/item.asp?ItemID=2029)に似た表形式データを保持できるローカル t-sql 変数です。 このアプローチは、Microsoft SQL Server 2005 と SQL Server 2000 の両方で同様に機能します (一方、 `ROW_NUMBER()` アプローチは SQL Server 2005 でのみ機能します)。  
  
  ここでの考え方は、 `IDENTITY` データがページングされているテーブルの主キーの列と列を持つテーブル変数を作成することです。 次に、データがページングされているテーブルの内容がテーブル変数にダンプされます。これにより、テーブル内の `IDENTITY` 各レコードに対して (列を介して) 連続する行インデックスが関連付けられます。 テーブル変数に値が設定されると、 `SELECT` 基になるテーブルと結合されたテーブル変数のステートメントを実行して、特定のレコードを取り出すことができます。 ステートメントを使用して、 `SET ROWCOUNT` テーブル変数にダンプする必要があるレコードの数をインテリジェントに制限します。  
  
  この方法の効率は、要求されているページ番号に基づいてい `SET ROWCOUNT` ます。値には、開始行インデックスと最大行数の値が割り当てられているためです。 データの最初のいくつかのページなど、番号の小さいページを使用してページングを行う場合、この方法は非常に効率的です。 ただし、最後の近くにページを取得すると、既定のページングのようなパフォーマンスが示されます。

このチュートリアルでは、キーワードを使用してカスタムページングを実装し `ROW_NUMBER()` ます。 テーブル変数と手法の使用方法の詳細については `SET ROWCOUNT` 、 [大きな結果セットを使用したページングのより効率的な方法](http://www.4guysfromrolla.com/webtech/042606-1.shtml)に関するページを参照してください。

キーワードは、 `ROW_NUMBER()` 次の構文を使用して、特定の順序で返される各レコードの順位付けに関連付けられています。

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample3.sql)]

`ROW_NUMBER()` 指定された順序に関して、各レコードのランクを指定する数値を返します。 たとえば、各製品の順位を最も高価なものから順に確認するには、次のクエリを使用します。

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample4.sql)]

図5に、Visual Studio のクエリウィンドウで実行した場合のクエリの結果を示します。 製品は、各行の価格と共に価格で並べ替えられていることに注意してください。

![返されたレコードごとに価格順位が含まれます。](efficiently-paging-through-large-amounts-of-data-cs/_static/image5.png)

**図 5**: 返されたレコードごとに価格順位が含まれる

> [!NOTE]
> `ROW_NUMBER()` は、SQL Server 2005 で使用できる多くの新しい順位付け関数の1つにすぎません。 の詳細については、 `ROW_NUMBER()` 他の順位付け関数と共に、 [Microsoft SQL Server 2005 を使用して順位](http://www.4guysfromrolla.com/webtech/010406-1.shtml)付けされた結果を返すことをお読みください。

句で指定された列 (上の例では) によって結果に順位を付けた場合 `ORDER BY` `OVER` `UnitPrice` 、SQL Server は結果を並べ替える必要があります。 これは、結果が並べ替えられている列にクラスター化インデックスがある場合、またはカバリングインデックスがある場合は、簡単な操作ですが、それ以外の場合はコストが高くなる可能性があります。 十分に大きなクエリのパフォーマンスを向上させるには、結果の並べ替えに使用する列に非クラスター化インデックスを追加することを検討してください。 パフォーマンスに関する考慮事項の詳細については、「 [SQL Server 2005 の順位付け関数とパフォーマンス](http://www.sql-server-performance.com/ak_ranking_functions.asp) 」を参照してください。

によって返される順位付け情報は、 `ROW_NUMBER()` 句で直接使用することはできません `WHERE` 。 ただし、派生テーブルを使用して結果を返すことができます `ROW_NUMBER()` 。これは、句に表示でき `WHERE` ます。 たとえば、次のクエリでは、派生テーブルを使用して、ProductName 列と UnitPrice 列を結果と共に返し、 `ROW_NUMBER()` 句を使用して、 `WHERE` 価格順位が 11 ~ 20 の製品のみを返します。

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample5.sql)]

この概念をさらに拡張すると、この方法を使用して、目的の開始行インデックスと最大行数値を指定して、特定のデータページを取得できます。

[!code-html[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample6.html)]

> [!NOTE]
> このチュートリアルで後ほど説明するように、 *`StartRowIndex`* ObjectDataSource によって指定されたは0から始まるインデックスが作成されますが、 `ROW_NUMBER()` SQL Server 2005 によって返される値は1からインデックスが作成されます。 したがって、 `WHERE` 句は、 `PriceRank` が厳密により大きく、以下であるレコードを返し *`StartRowIndex`* *`StartRowIndex`*  +  *`MaximumRows`* ます。

ここでは、を使用してデータの特定のページを取得する方法について説明しました。 `ROW_NUMBER()` 開始行のインデックスと最大行数の値を指定して、このロジックを DAL および BLL のメソッドとして実装する必要があります。

このクエリを作成するときは、結果の順位付け順序を決める必要があります。製品の名前をアルファベット順に並べ替えてみましょう。 これは、このチュートリアルのカスタムページング実装では、並べ替えを行うこともできないカスタムページングレポートを作成できないことを意味します。 次のチュートリアルでは、このような機能を提供する方法について説明します。

前のセクションでは、DAL メソッドをアドホック SQL ステートメントとして作成しました。 残念ながら、TableAdapter ウィザードで使用される Visual Studio の T-sql パーサーは、 `OVER` 関数で使用される構文とはまったく同じでは `ROW_NUMBER()` ありません。 このため、この DAL メソッドはストアドプロシージャとして作成する必要があります。 [表示] メニューからサーバーエクスプローラーを選択します (または、Ctrl + Alt + S キーを押して)、ノードを展開し `NORTHWND.MDF` ます。 新しいストアドプロシージャを追加するには、[ストアドプロシージャ] ノードを右クリックし、[新しいストアドプロシージャの追加] を選択します (図6を参照)。

![製品のページング用に新しいストアドプロシージャを追加する](efficiently-paging-through-large-amounts-of-data-cs/_static/image6.png)

**図 6**: 製品を使用したページング用の新しいストアドプロシージャの追加

このストアドプロシージャは、2つの整数入力パラメーター (と) を受け入れ、 `@startRowIndex` `@maximumRows` `ROW_NUMBER()` フィールドによって並べ替えられた関数を使用して、 `ProductName` 指定したより大きい行と s 以下の行だけを返す必要があり `@startRowIndex` `@startRowIndex`  +  `@maximumRow` ます。 新しいストアドプロシージャに次のスクリプトを入力し、[保存] アイコンをクリックして、ストアドプロシージャをデータベースに追加します。

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample7.sql)]

ストアドプロシージャを作成した後、すぐにテストしてみてください。 `GetProductsPaged` サーバーエクスプローラーでストアドプロシージャ名を右クリックし、[実行] オプションを選択します。 Visual Studio では、入力パラメーターと s を入力するように求められ `@startRowIndex` `@maximumRow` ます (図7を参照)。 異なる値を試し、結果を確認します。

![@startRowIndexパラメーターとパラメーターの値を入力してください @maximumRows](efficiently-paging-through-large-amounts-of-data-cs/_static/image7.png)

<strong>図 7</strong>: @startRowIndex パラメーターとパラメーターの値を入力する @maximumRows

これらの入力パラメーター値を選択すると、出力ウィンドウに結果が表示されます。 図8は、パラメーターとパラメーターの両方に対して10を渡した場合の結果を示して `@startRowIndex` `@maximumRows` います。

[![データの2番目のページに表示されるレコードが返されます。](efficiently-paging-through-large-amounts-of-data-cs/_static/image9.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image8.png)

**図 8**: データの2番目のページに表示されるレコードが返されます ([クリックすると、フルサイズの画像が表示](efficiently-paging-through-large-amounts-of-data-cs/_static/image10.png)されます)

このストアドプロシージャを作成したので、メソッドを作成する準備ができました `ProductsTableAdapter` 。 型指定されたデータセットを開き、 `Northwind.xsd` を右クリックして、[ `ProductsTableAdapter` クエリの追加] オプションを選択します。 アドホック SQL ステートメントを使用してクエリを作成する代わりに、既存のストアドプロシージャを使用してクエリを作成します。

![既存のストアドプロシージャを使用した DAL メソッドの作成](efficiently-paging-through-large-amounts-of-data-cs/_static/image11.png)

**図 9**: 既存のストアドプロシージャを使用して DAL メソッドを作成する

次に、呼び出すストアドプロシージャを選択するように求められます。 `GetProductsPaged`ドロップダウンリストからストアドプロシージャを選択します。

![ドロップダウンリストから [GetProductsPaged 切れ] ストアドプロシージャを選択します。](efficiently-paging-through-large-amounts-of-data-cs/_static/image12.png)

**図 10**: ドロップダウンリストから GetProductsPaged 切れストアドプロシージャを選択する

次の画面では、ストアドプロシージャによって返されるデータの種類 (表形式データ、単一値、値なし) を求められます。 `GetProductsPaged`ストアドプロシージャは複数のレコードを返すことができるため、表形式のデータを返すことを示します。

![ストアドプロシージャが表形式データを返すことを示します。](efficiently-paging-through-large-amounts-of-data-cs/_static/image13.png)

**図 11**: ストアドプロシージャが表形式データを返すことを示す

最後に、作成するメソッドの名前を指定します。 前のチュートリアルと同様に、DataTable への Fill と DataTable の両方を使用してメソッドを作成します。 最初のメソッドと2番目のメソッドに名前を指定し `FillPaged` `GetProductsPaged` ます。

![メソッドに FillPaged と GetProductsPaged 切れの名前を指定します。](efficiently-paging-through-large-amounts-of-data-cs/_static/image14.png)

**図 12**: メソッドに fillpaged と GetProductsPaged 切れの名前を指定する

DAL メソッドを作成して製品の特定のページを返すだけでなく、BLL にもそのような機能を提供する必要があります。 DAL メソッドと同様に、BLL s GetProductsPaged 切れのメソッドは、開始行インデックスと最大行数を指定するために2つの整数入力を受け取る必要があり、指定された範囲内に収まるレコードだけを返す必要があります。 このような BLL メソッドを Productbll クラスに作成します。このクラスは、次のように、DAL s GetProductsPaged 切れのメソッドに単にを呼び出します。

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample8.cs)]

BLL メソッドの入力パラメーターには任意の名前を使用できますが、後で説明するように、 `startRowIndex` `maximumRows` このメソッドを使用するように ObjectDataSource を構成する場合は、追加の作業を使用して保存することを選択します。

## <a name="step-4-configuring-the-objectdatasource-to-use-custom-paging"></a>手順 4: カスタムページングを使用するように ObjectDataSource を構成する

特定のレコードのサブセットにアクセスするための BLL メソッドと DAL メソッドを使用すると、カスタムページングを使用して基になるレコードをページ化する GridView コントロールを作成できます。 まず、フォルダー内のページを開き、 `EfficientPaging.aspx` `PagingAndSorting` GridView をページに追加して、新しい ObjectDataSource コントロールを使用するように構成します。 このチュートリアルでは、多くの場合、クラス s メソッドを使用するように ObjectDataSource が構成されていました `ProductsBLL` `GetProducts` 。 ここでは、メソッドを使用します。これは、 `GetProductsPaged` メソッドが `GetProducts` データベース内の *すべて* の製品を返すのに対し、は `GetProductsPaged` 特定のレコードのサブセットのみを返すためです。

![Productbll クラス s GetProductsPaged 切れメソッドを使用するように ObjectDataSource を構成する](efficiently-paging-through-large-amounts-of-data-cs/_static/image15.png)

**図 13**: Productbll クラス s GetProductsPaged 切れメソッドを使用するように ObjectDataSource を構成する

読み取り専用の GridView を作成しているため、[挿入]、[更新]、および [削除] タブの [メソッド] ドロップダウンリストを [(なし)] に設定します。

次に、ObjectDataSource ウィザードで、メソッドのソースと入力パラメーターの値を入力するように求められ `GetProductsPaged` `startRowIndex` `maximumRows` ます。 これらの入力パラメーターは、実際に GridView によって自動的に設定されるので、[ソース] を [なし] のままにし、[完了] をクリックします。

![入力パラメーターソースは None のままにします。](efficiently-paging-through-large-amounts-of-data-cs/_static/image16.png)

**図 14**: 入力パラメーターソースを [なし] のままにする

ObjectDataSource ウィザードを完了すると、GridView には各製品データフィールドの BoundField または CheckBoxField が含まれます。 必要に応じて、GridView の外観を自由に調整してください。 `ProductName`、、 `CategoryName` `SupplierName` 、 `QuantityPerUnit` 、および `UnitPrice` boundfields のみを表示するように選択しました。 また、そのスマートタグの [ページングを有効にする] チェックボックスをオンにして、ページングをサポートするように GridView を構成します。 これらの変更が完了すると、GridView および ObjectDataSource の宣言マークアップは次のようになります。

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample9.aspx)]

ただし、ブラウザーを使用してページにアクセスした場合、GridView は見つかりません。

![GridView が表示されない](efficiently-paging-through-large-amounts-of-data-cs/_static/image17.png)

**図 15**: GridView が表示されない

ObjectDataSource が、 `GetProductsPaged` `startRowIndex` 入力パラメーターと入力パラメーターの両方の値として現在0を使用しているため、GridView が見つかりません `maximumRows` 。 そのため、結果として得られる SQL クエリはレコードを返さないため、GridView は表示されません。

これを解決するには、カスタムページングを使用するように ObjectDataSource を構成する必要があります。 これは、次の手順で実現できます。

1. **Objectdatasource s `EnablePaging` `true` プロパティ**を次の2つの追加パラメーターに渡す必要があることを指定します `SelectMethod` 。1つは開始行インデックスを指定する ( [`StartRowIndexParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx) )、もう1つは最大行数を指定する ( [`MaximumRowsParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx) ) です。
2. **ObjectDataSource `StartRowIndexParameterName` と `MaximumRowsParameterName` プロパティを設定** します `StartRowIndexParameterName` `MaximumRowsParameterName` 。プロパティとプロパティは、カスタムページングのためにに渡される入力パラメーターの名前を示し `SelectMethod` ます。 既定では、これらのパラメーター名はおよびです。そのため、 `startIndexRow` `maximumRows` BLL でメソッドを作成するときに、これらの値を入力パラメーターとして `GetProductsPaged` 使用しました。 やなど、BLL のメソッドに異なるパラメーター名を使用することを選択した場合は `GetProductsPaged` `startIndex` `maxRows` 、ObjectDataSource のとプロパティを適宜設定する必要があり `StartRowIndexParameterName` `MaximumRowsParameterName` ます (たとえば、の場合は startIndex、 `StartRowIndexParameterName` maxRows の場合は `MaximumRowsParameterName` )。
3. **ObjectDataSource s [ `SelectCountMethod` プロパティ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod(VS.80).aspx)を、ページングされるレコードの合計数を返すメソッドの名前に設定します ( `TotalNumberOfProducts` )** `ProductsBLL` 。クラスのメソッドが、 `TotalNumberOfProducts` クエリを実行する DAL メソッドを使用して、ページングされているレコードの合計数を返すことを思い出して `SELECT COUNT(*) FROM Products` ください。 この情報は、ページングインターフェイスを正しく表示するために ObjectDataSource によって必要になります。
4. ウィザードを使用して ObjectDataSource を構成するときに** `startRowIndex` `maximumRows` `<asp:Parameter>` Objectdatasource s 宣言マークアップから要素と要素を削除すると**、Visual Studio によって、 `<asp:Parameter>` メソッドの入力パラメーターに2つの要素が自動的に追加され `GetProductsPaged` ます。 `EnablePaging`をに設定する `true` と、これらのパラメーターは自動的に渡されます。宣言構文にも含まれている場合、ObjectDataSource は、メソッドに*4 つ*のパラメーターを渡し、 `GetProductsPaged` 2 つのパラメーターをメソッドに渡し `TotalNumberOfProducts` ます。 これらの要素を削除し忘れた場合 `<asp:Parameter>` 、ブラウザーを使用してページを閲覧すると、次のようなエラーメッセージが表示されます。 *ObjectDataSource ' ObjectDataSource1 ' は、パラメーター: startrowindex, maximumrows を持つ非ジェネリックメソッド ' TotalNumberOfProducts ' を見つける*ことができませんでした。

これらの変更を行った後、ObjectDataSource s 宣言構文は次のようになります。

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample10.aspx)]

`EnablePaging`プロパティとプロパティが `SelectCountMethod` 設定され、 `<asp:Parameter>` 要素が削除されていることに注意してください。 図16は、これらの変更が加えられた後のプロパティウィンドウのスクリーンショットを示しています。

![カスタムページングを使用するには、ObjectDataSource コントロールを構成します。](efficiently-paging-through-large-amounts-of-data-cs/_static/image18.png)

**図 16**: カスタムページングを使用するには、ObjectDataSource コントロールを構成する

これらの変更を行った後、ブラウザーを使用してこのページにアクセスします。 10個の製品がアルファベット順に並べられて表示されます。 一度に1ページずつデータをステップ実行します。 既定のページングとカスタムページングの間のエンドユーザーの視点とは視覚的な違いはありませんが、カスタムページングでは、特定のページに表示する必要があるレコードのみを取得するため、大量のデータをより効率的にページングできます。

[![製品名によって並べ替えられたデータは、カスタムページングを使用してページングされます。](efficiently-paging-through-large-amounts-of-data-cs/_static/image20.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image19.png)

**図 17**: 製品名の順に並べられたデータは、カスタムページングを使用してページングされます ([クリックすると、フルサイズの画像が表示](efficiently-paging-through-large-amounts-of-data-cs/_static/image21.png)されます)

> [!NOTE]
> カスタムページングでは、ObjectDataSource のによって返されるページカウント値 `SelectCountMethod` は、GridView のビューステートに格納されます。 その他の gridview 変数 `PageIndex` 、、 `EditIndex` `SelectedIndex` 、コレクションなどは、 `DataKeys` gridview のプロパティの値に関係なく保持される *コントロールの状態*に格納され `EnableViewState` ます。 値は `PageCount` ビューステートを使用してポストバック間で永続化されるため、最後のページに移動するためのリンクを含むページングインターフェイスを使用する場合は、GridView のビューステートが有効になっている必要があります。 (ページングインターフェイスに最後のページへの直接リンクが含まれていない場合は、ビューステートを無効にすることができます)。

最後のページのリンクをクリックすると、ポストバックが発生し、そのプロパティを更新するように GridView に指示し `PageIndex` ます。 最後のページのリンクがクリックされた場合、GridView によってプロパティが `PageIndex` そのプロパティより1小さい値に割り当てられ `PageCount` ます。 ビューステートが無効になっている場合は、 `PageCount` ポストバック間で値が失われ、に `PageIndex` は、代わりに最大の整数値が割り当てられます。 次に、GridView は、プロパティとプロパティを乗算することによって、開始行インデックスを決定しようとし `PageSize` `PageCount` ます。 この結果、 `OverflowException` 製品が許容される最大整数サイズを超えているため、が発生します。

## <a name="implement-custom-paging-and-sorting"></a>カスタムページングと並べ替えの実装

現在のカスタムページング実装では、ストアドプロシージャの作成時に、データをページングする順序を静的に指定する必要があり `GetProductsPaged` ます。 ただし、[ページングを有効にする] オプションに加えて、GridView のスマートタグに [並べ替えを有効にする] チェックボックスが含まれていることに注意してください。 残念ながら、現在のカスタムページング実装を使用して GridView に並べ替えサポートを追加すると、現在表示されているデータページのレコードのみが並べ替えられます。 たとえば、ページングもサポートするように GridView を構成した場合、データの最初のページを表示するときに、製品名で降順に並べ替えて、ページ1で製品の順序を逆にします。 図18に示すように、この例では、アルファベットの逆順で並べ替えを行う場合の最初の製品として Carnarvon 虎を示しています。 Carnarvon 虎の後に続く71の他の製品はアルファベット順に表示されます。並べ替えでは、最初のページのレコードだけが考慮されます。

[![現在のページに表示されているデータのみが並べ替えられます](efficiently-paging-through-large-amounts-of-data-cs/_static/image23.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image22.png)

**図 18**: 現在のページに表示されているデータのみが並べ替えられている ([クリックすると、フルサイズの画像が表示](efficiently-paging-through-large-amounts-of-data-cs/_static/image24.png)されます)

並べ替えは、データの現在のページにのみ適用されます。これは、データが BLL のメソッドから取得された後に並べ替えが行われているためです `GetProductsPaged` 。このメソッドは、特定のページのレコードのみを返します。 並べ替えを正しく実装するには、データ `GetProductsPaged` の特定のページを返す前にデータが適切に順位付けされるように、並べ替え式をメソッドに渡す必要があります。 これを実現する方法については、次のチュートリアルで説明します。

## <a name="implementing-custom-paging-and-deleting"></a>カスタムページングの実装と削除

カスタムページング手法を使用してデータがページングされている GridView で機能の削除を有効にすると、最後のページから最後のレコードを削除しても、gridview が適切にデクリメントされるのではなく、gridview が消え `PageIndex` ます。 このバグを再現するには、先ほど作成したチュートリアルの削除を有効にします。 最後のページ (ページ 9) に移動します。ここでは、81製品、一度に10個の製品を使用してページングを行っているため、1つの製品が表示されます。 この製品を削除します。

最後の製品を *削除すると、GridView が* 自動的に8番目のページに移り、そのような機能が既定のページングで表示されます。 ただし、カスタムページングを使用すると、最後のページでその最後の製品を削除した後、GridView が画面から完全に消えるだけです。 これが発生する正確 *な理由は、このチュートリアル* の範囲を超えています。この問題の原因については、詳細については、「 [カスタムページングを使用して GridView から最後のページの最後のレコードを削除](http://scottonwriting.net/sowblog/posts/7326.aspx) する」を参照してください。 概要では、[削除] ボタンがクリックされたときに GridView によって実行される次の一連の手順が原因です。

1. レコードを削除する
2. 指定したとに表示する適切なレコードを取得します。 `PageIndex``PageSize`
3. が `PageIndex` データソース内のデータのページ数を超えていないことを確認します。存在する場合は、自動的に GridView s プロパティをデクリメントします。 `PageIndex`
4. 手順2で取得したレコードを使用して、データの適切なページを GridView にバインドします。

問題の原因は、手順 2. で表示するレコードを取得するときに使用されていたのが、その `PageIndex` `PageIndex` レコードだけが削除された最後のページのままであることです。 したがって、手順 2. では、データの最後のページにレコードが含まれていないため、レコードは返され *ません* 。 次に、ステップ3では、GridView は、その `PageIndex` プロパティがデータソース内のページの総数 (最後のページの最後のレコードを削除したため) を超えていることを認識し、そのプロパティをデクリメントし `PageIndex` ます。 手順4では、GridView は、手順 2. で取得したデータにそれ自体をバインドしようとします。ただし、手順2ではレコードが返されませんでした。その結果、GridView が空になります。 既定のページングでは、手順 2. で *すべて* のレコードがデータソースから取得されるため、この問題は表面化しません。

この問題を解決するには、2つのオプションがあります。 1つ目は、削除された `RowDeleted` ばかりのページに表示されるレコードの数を決定する GridView s イベントハンドラーのイベントハンドラーを作成することです。 レコードが1つしか存在しない場合は、削除したばかりのレコードが最後のレコードである必要があり、GridView をデクリメントする必要があり `PageIndex` ます。 もちろん、削除操作が実際に成功した場合にのみを更新することをお勧めし `PageIndex` ます。これは、プロパティがであることを確認することによって決定でき `e.Exception` `null` ます。

この方法は、 `PageIndex` 手順1の後、手順 2. の前にを更新するため、機能します。 したがって、手順 2. では、適切なレコードセットが返されます。 これを実現するには、次のようなコードを使用します。

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample11.cs)]

別の回避策として、ObjectDataSource s イベントのイベントハンドラーを作成 `RowDeleted` し、 `AffectedRows` プロパティの値を1に設定します。 手順 1. でレコードを削除した後 (ただし、手順2でデータを再取得する前)、その `PageIndex` 操作によって1つ以上の行が影響を受けた場合、GridView によってプロパティが更新されます。 ただし、 `AffectedRows` プロパティは ObjectDataSource によって設定されないため、この手順は省略されます。 このステップを実行する1つの方法は `AffectedRows` 、削除操作が正常に完了した場合にプロパティを手動で設定することです。 これは、次のようなコードを使用して実現できます。

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample12.cs)]

これらのイベントハンドラーのコードは、この例の分離コードクラスに記載されて `EfficientPaging.aspx` います。

## <a name="comparing-the-performance-of-default-and-custom-paging"></a>既定のページングとカスタムページングのパフォーマンスの比較

カスタムページングは必要なレコードのみを取得するため、既定のページングでは、表示される各ページの *すべて* のレコードが返されるので、カスタムページングは既定のページングよりも効率的であることがわかります。 しかし、カスタムページングはどの程度効率的ですか。 既定のページングからカスタムページングに移行すると、どのようなパフォーマンスの向上が見られますか。

残念ながら、ここでは1つのサイズがすべての回答に適合しているわけではありません。 パフォーマンスの向上は、多くの要因に依存しています。最も目立つのは、ページングされているレコードの数と、web サーバーとデータベースサーバー間の通信チャネルに対して行われた負荷です。 少数のレコードを含む小さいテーブルの場合、パフォーマンスの差はごくわずかです。 ただし、大規模なテーブルでは、数千から数百の行がありますが、パフォーマンスの違いは鋭角です。

[SQL Server 2005 を使用した ASP.NET 2.0 でのカスタムページングに関する](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)記事では、5万レコードを含むデータベーステーブルを使用してページングするときに、これら2つのページング手法のパフォーマンスの違いを示すために実行したいくつかのパフォーマンステストが含まれています。 これらのテストでは、( [SQL Profiler](https://msdn.microsoft.com/library/ms173757.aspx)を使用して) SQL Server レベルでクエリを実行する時間と、 [ASP.NET s トレース機能](https://msdn.microsoft.com/library/y13fw6we.aspx)を使用して ASP.NET ページでクエリを実行する時間の両方を確認しました。 これらのテストは、1つのアクティブなユーザーを使用して開発用ボックスで実行されているため、科学的なものではなく、一般的な web サイトのロードパターンを模倣していないことに注意してください。 とは異なり、結果は、十分な量のデータを処理するときの既定のページングとカスタムページングの実行時間の相対的な違いを示しています。

|  | **平均実行時間 (秒)** | **Reads** |
| --- | --- | --- |
| **既定のページング SQL Profiler** | 1.411 | 383 |
| **カスタムページング SQL Profiler** | 0.002 | 29 |
| **既定のページング ASP.NET トレース** | 2.379 | *N/A* |
| **カスタムページング ASP.NET トレース** | 0.029 | *N/A* |

ご覧のように、データの特定のページを取得するには、平均で354回の読み取りを必要とし、時間の経過と共に完了する必要があります。 ASP.NET ページでは、ページを既定のページングを使用したときに要した時間<sup>を1/100 に</sup> 近づけることができました。 これらの結果の詳細については、「 [マイ記事](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx) 」を参照してください。コードとデータベースをダウンロードして、独自の環境でこれらのテストを再現することができます。

## <a name="summary"></a>まとめ

既定のページングは、データ Web コントロールのスマートタグの [ページングを有効にする] チェックボックスをオンにするだけで実装するたいしたですが、このような単純さにはパフォーマンスのコストが伴います。 既定のページングでは、ユーザーがデータの任意のページを要求したときに、すべてのレコードが表示される場合がありますが、 *すべて* のレコードが返されます。 このパフォーマンスのオーバーヘッドを回避するために、ObjectDataSource では、別のページングオプションのカスタムページングが提供されています。

カスタムページングでは、表示する必要があるレコードのみを取得することによって、既定のページングパフォーマンスの問題が改善されますが、カスタムページングの実装にも関係があります。 最初に、要求されたレコードの特定のサブセットに適切にアクセスする (そして効率的に) クエリを記述する必要があります。 これはさまざまな方法で実現できます。このチュートリアルでは、SQL Server 2005 s new 関数を使用し `ROW_NUMBER()` て結果に順位を付け、順位が指定された範囲内にある結果だけを返すようにする方法を説明しました。 さらに、ページングされるレコードの合計数を決定する手段を追加する必要があります。 これらの DAL メソッドと BLL メソッドを作成した後、ObjectDataSource を構成して、ページ全体の合計レコード数を確認し、開始行インデックスと最大行数の値を適切に BLL に渡すことができるようにする必要もあります。

カスタムページングの実装には多くの手順が必要であり、既定のページングほど単純ではありませんが、十分な量のデータをページングする場合はカスタムページングが不可欠です。 確認した結果が表示されると、カスタムページングによって ASP.NET ページのレンダリング時間が短縮され、データベースサーバーの負荷が1つ以上の大きな順序で軽減される可能性があります。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は [*、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 彼は、にアクセスでき[ mitchell@4GuysFromRolla.com ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは、「」にあり [http://ScottOnWriting.NET](http://ScottOnWriting.NET) ます。

> [!div class="step-by-step"]
> [前へ](paging-and-sorting-report-data-cs.md)
> [次へ](sorting-custom-paged-data-cs.md)
