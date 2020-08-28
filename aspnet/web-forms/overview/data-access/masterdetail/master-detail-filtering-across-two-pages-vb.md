---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
title: 2つのページでマスター/詳細をフィルター処理する (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、GridView を使用してデータベース内のサプライヤーを一覧表示することで、このパターンを実装します。 GridView の各 supplier 行には、ビューが含まれています...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 361d6a44-3f1f-4daf-85df-d4c2b8bf065d
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 0e30d47a565c3b6cb9f647d54d47c10a418762f4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044975"
---
# <a name="masterdetail-filtering-across-two-pages-vb"></a>2 つのページでマスター/詳細をフィルター処理する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[サンプルアプリのダウンロード](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_9_VB.exe) または [PDF のダウンロード](master-detail-filtering-across-two-pages-vb/_static/datatutorial09vb1.pdf)

> このチュートリアルでは、GridView を使用してデータベース内のサプライヤーを一覧表示することで、このパターンを実装します。 GridView の各仕入先の行には、[製品の表示] リンクが含まれています。このリンクをクリックすると、選択した業者の製品が一覧表示された別のページに移動します。

## <a name="introduction"></a>概要

前の2つのチュートリアルでは、DropDownLists を使用して "マスター" レコードを表示する1つの web ページでマスター/詳細レポートを表示する方法、および "詳細" を表示するための [GridView](master-detail-filtering-with-a-dropdownlist-vb.md) または [DetailsView](master-detail-filtering-with-two-dropdownlists-vb.md) コントロールについて説明しました。 マスター/詳細レポートに使用されるもう1つの一般的なパターンは、1つの web ページにマスターレコードを作成し、その詳細を別の web ページに表示することです。 フォーラムの web サイト ( [ASP.NET フォーラム](https://forums.asp.net/)など) は、このパターンを実践するための好例です。 ASP.NET フォーラムは、さまざまなフォーラムはじめに、Web フォーム、データ表示コントロールなどで構成されています。 各フォーラムは多くのスレッドで構成されており、各スレッドは多数の投稿で構成されています。 ASP.NET フォーラムのホームページに、フォーラムが表示されます。 フォーラムをクリックすると、 `ShowForum.aspx` そのフォーラムのスレッドが一覧表示されるページに whisks ます。 同様に、スレッドをクリックすると `ShowPost.aspx` 、クリックされたスレッドの投稿が表示されます。

このチュートリアルでは、GridView を使用してデータベース内のサプライヤーを一覧表示することで、このパターンを実装します。 GridView の各仕入先の行には、[製品の表示] リンクが含まれています。このリンクをクリックすると、選択した業者の製品が一覧表示された別のページに移動します。

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>手順 1: `SupplierListMaster.aspx` `ProductsForSupplierDetails.aspx` フォルダーへのページとページの追加 `Filtering`

3番目のチュートリアルでページレイアウトを定義すると `BasicReporting` 、、、およびの各フォルダーに "starter" ページがいくつか追加されました `Filtering` `CustomFormatting` 。 ただし、その時点でこのチュートリアルのスタートページを追加していません。そのため、との2つの新しいページをフォルダーに追加してみましょう `Filtering` 。 `SupplierListMaster.aspx` `ProductsForSupplierDetails.aspx` `SupplierListMaster.aspx` によって "マスター" レコードが一覧表示され、 `ProductsForSupplierDetails.aspx` 選択した仕入先の製品が表示されます。

これら2つの新しいページを作成する場合は、マスターページに関連付ける必要があり `Site.master` ます。

![SupplierListMaster および ProductsForSupplierDetails ページをフィルター処理フォルダーに追加します。](master-detail-filtering-across-two-pages-vb/_static/image1.png)

**図 1**: `SupplierListMaster.aspx` `ProductsForSupplierDetails.aspx` ページとページをフォルダーに追加する `Filtering`

また、新しいページをプロジェクトに追加する場合は、必ずサイトマップファイルを更新してください `Web.sitemap` 。 このチュートリアルでは、 `SupplierListMaster.aspx` フィルター処理のレポート要素の子として次の XML コンテンツを使用して、単にページをサイトマップに追加し `<siteMapNode>` ます。

[!code-xml[Main](master-detail-filtering-across-two-pages-vb/samples/sample1.xml)]

> [!NOTE]
> K を使用して新しい ASP.NET ページを追加するときに、サイトマップファイルの更新プロセスを自動化でき [ます。 Scott Allen](http://odetocode.com/Blogs/scott/)の無料の Visual Studio [サイトマップマクロ](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)です。

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>手順 2: での業者の一覧の表示`SupplierListMaster.aspx`

ページとページを作成したので `SupplierListMaster.aspx` `ProductsForSupplierDetails.aspx` 、次の手順では、でサプライヤーの GridView を作成し `SupplierListMaster.aspx` ます。 GridView をページに追加し、新しい ObjectDataSource にバインドします。 この ObjectDataSource では、クラスのメソッドを使用して、 `SuppliersBLL` `GetSuppliers()` すべての業者を返す必要があります。

[![SuppliersBLL クラスを選択します。](master-detail-filtering-across-two-pages-vb/_static/image3.png)](master-detail-filtering-across-two-pages-vb/_static/image2.png)

**図 2**: クラスを選択 `SuppliersBLL` [する (クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-vb/_static/image4.png)されます)

[![GetSuppliers () メソッドを使用するように ObjectDataSource を構成する](master-detail-filtering-across-two-pages-vb/_static/image6.png)](master-detail-filtering-across-two-pages-vb/_static/image5.png)

**図 3**: メソッドを使用するように ObjectDataSource を構成する `GetSuppliers()` ([クリックすると、フルサイズのイメージが表示](master-detail-filtering-across-two-pages-vb/_static/image7.png)されます)

クリックすると、ユーザーが選択した `ProductsForSupplierDetails.aspx` 行の値をクエリ文字列を使用して渡すように、各 GridView 行に「Products」というタイトルのリンクを含める必要があり `SupplierID` ます。 たとえば、ユーザーが東京 Traders 業者の [製品の表示] リンクをクリックした場合 ( `SupplierID` 値が4の場合) は、に送信される必要があり `ProductsForSupplierDetails.aspx?SupplierID=4` ます。

これを行うには、GridView に hyperlink [フィールド](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx) を追加します。これにより、各 gridview 行にハイパーリンクが追加されます。 まず、GridView のスマートタグから [列の編集] リンクをクリックします。 次に、左上の一覧から [ハイパーリンク] フィールドを選択し、[追加] をクリックして、GridView のフィールドリストにハイパーリンクフィールドを含めます。

[![ハイパーリンクフィールドを GridView に追加する](master-detail-filtering-across-two-pages-vb/_static/image9.png)](master-detail-filtering-across-two-pages-vb/_static/image8.png)

**図 4**: GridView にハイパーリンクフィールドを追加する ([クリックすると、フルサイズのイメージが表示](master-detail-filtering-across-two-pages-vb/_static/image10.png)されます)

ハイパーリンクフィールドは、各 GridView 行のリンクに同じテキストまたは URL 値を使用するように構成できます。また、各行にバインドされたデータ値に基づいてこれらの値を指定することもできます。 すべての行に対して静的な値を指定するには、ハイパーリンクフィールドの `Text` プロパティまたはプロパティを使用し `NavigateUrl` ます。 すべての行でリンクテキストを同じにするため、ハイパーリンクフィールドのプロパティを設定して `Text` 製品を表示します。

[![ハイパーリンクフィールドの Text プロパティを設定して製品を表示する](master-detail-filtering-across-two-pages-vb/_static/image12.png)](master-detail-filtering-across-two-pages-vb/_static/image11.png)

**図 5**: ハイパーリンクフィールドのプロパティを設定して `Text` 製品を表示する ([クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-vb/_static/image13.png)されます)

GridView 行にバインドされている基になるデータに基づいてテキストまたは URL の値を設定するには、プロパティまたはプロパティで、テキストまたは URL の値をプルするデータフィールドを指定し `DataTextField` `DataNavigateUrlFields` ます。 `DataTextField` 1つのデータフィールドにのみ設定できます。ただし、では、 `DataNavigateUrlFields` データフィールドのコンマ区切りの一覧を設定できます。 多くの場合、現在の行のデータフィールド値といくつかの静的マークアップの組み合わせに基づいて、テキストまたは URL を指定する必要があります。 このチュートリアルでは、たとえば、ハイパーリンクフィールドのリンクの URL をにする必要があり `ProductsForSupplierDetails.aspx?SupplierID=supplierID` ます。ここで、 *`supplierID`* は各 GridView の行の `SupplierID` 値です。 ここでは、静的な値とデータドリブン値の両方が必要であることに注意してください。 `ProductsForSupplierDetails.aspx?SupplierID=` リンクの URL の部分は静的であるのに対し、部分はデータドリブンであり、 *`supplierID`* その値は各行独自の `SupplierID` 値です。

静的値とデータドリブン値の組み合わせを示すには、 `DataTextFormatString` プロパティとプロパティを使用し `DataNavigateUrlFormatString` ます。 これらのプロパティで、必要に応じて静的マークアップを入力し、 `{0}` プロパティまたはプロパティで指定したフィールドの値を表示するマーカーを使用し `DataTextField` `DataNavigateUrlFields` ます。 プロパティに `DataNavigateUrlFields` 複数のフィールドが指定されている場合、 `{0}` 最初のフィールド値を挿入する場所、2番目のフィールド値、およびなどを使用し `{1}` ます。

このチュートリアルにこれを適用するには、プロパティをに設定する必要があります。これは、 `DataNavigateUrlFields` `SupplierID` 行ごとにカスタマイズする必要がある値を持つデータフィールドであり、 `DataNavigateUrlFormatString` プロパティをに設定するため `ProductsForSupplierDetails.aspx?SupplierID={0}` です。

[![[ハイパーリンク] フィールドに、仕入先に基づく適切なリンク URL を含めるように構成します。](master-detail-filtering-across-two-pages-vb/_static/image15.png)](master-detail-filtering-across-two-pages-vb/_static/image14.png)

**図 6**: ハイパーリンクフィールドで、に基づく適切なリンク URL を含めるように構成します `SupplierID` ([クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-vb/_static/image16.png)されます)。

ハイパーリンクフィールドを追加した後は、GridView のフィールドのカスタマイズと順序変更を自由に行うことができます。 次のマークアップは、いくつかの細かいフィールドレベルのカスタマイズを行った後の GridView を示しています。

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample2.aspx)]

ブラウザーでページを表示し `SupplierListMaster.aspx` てみましょう。 図7に示すように、現在のページには、[製品の表示] リンクを含むすべての仕入先が表示されています。 [Products の表示] リンクをクリックすると、に移動して `ProductsForSupplierDetails.aspx` 、クエリ文字列内の業者のを渡し `SupplierID` ます。

[![各仕入先の行には、製品の表示のリンクが含まれています](master-detail-filtering-across-two-pages-vb/_static/image18.png)](master-detail-filtering-across-two-pages-vb/_static/image17.png)

**図 7**: 各仕入先の行に [製品の表示] リンクが含まれている ([クリックしてフルサイズの画像を表示する](master-detail-filtering-across-two-pages-vb/_static/image19.png))

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>手順 3: で仕入先の製品を一覧表示する`ProductsForSupplierDetails.aspx`

この時点で、 `SupplierListMaster.aspx` ページは、 `ProductsForSupplierDetails.aspx` クエリ文字列で選択された業者を渡して、ユーザーをに送信してい `SupplierID` ます。 チュートリアルの最後の手順は、 `ProductsForSupplierDetails.aspx` `SupplierID` クエリ文字列を使用して渡されたと等しいを持つ GridView で製品を表示することです `SupplierID` 。 これを行うには、GridView をページに追加します。そのためには、 `ProductsForSupplierDetails.aspx` クラスからメソッドを呼び出すという名前の新しい ObjectDataSource コントロールを使用し `ProductsBySupplierDataSource` `GetProductsBySupplierID(supplierID)` `ProductsBLL` ます。

[![ProductsBySupplierDataSource という名前の新しい ObjectDataSource を追加します。](master-detail-filtering-across-two-pages-vb/_static/image21.png)](master-detail-filtering-across-two-pages-vb/_static/image20.png)

**図 8**: 新しい ObjectDataSource を追加 `ProductsBySupplierDataSource` する ([クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-vb/_static/image22.png)される)

[![製品の Bll クラスを選択します](master-detail-filtering-across-two-pages-vb/_static/image24.png)](master-detail-filtering-across-two-pages-vb/_static/image23.png)

**図 9**: クラスを選択 `ProductsBLL` [する (クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-vb/_static/image25.png)されます)

[![ObjectDataSource に Get$ By仕入先 (仕入先) メソッドを呼び出します。](master-detail-filtering-across-two-pages-vb/_static/image27.png)](master-detail-filtering-across-two-pages-vb/_static/image26.png)

**図 10**: ObjectDataSource によってメソッドが呼び出されるよう `GetProductsBySupplierID(supplierID)` [にする (クリックすると、フルサイズのイメージが表示](master-detail-filtering-across-two-pages-vb/_static/image28.png)されます)

データソースの構成ウィザードの最後の手順では、メソッドのパラメーターのソースを指定するように求められ `GetProductsBySupplierID(supplierID)` *`supplierID`* ます。 Querystring 値を使用するには、パラメーターソースを QueryString に設定し、QueryStringField テキストボックス () で使用する querystring 値の名前を入力し `SupplierID` ます。

[![仕入先のパラメーター値に、仕入先の Querystring の値を設定します。](master-detail-filtering-across-two-pages-vb/_static/image30.png)](master-detail-filtering-across-two-pages-vb/_static/image29.png)

**図 11**: *`supplierID`* Querystring 値からパラメーター値を設定 `SupplierID` する ([クリックすると、フルサイズのイメージが表示](master-detail-filtering-across-two-pages-vb/_static/image31.png)されます)

必要な作業は以上です。 図12に、 `ProductsForSupplierDetails.aspx` から [東京 Traders] リンクをクリックすると表示されるページを示し `SupplierListMaster.aspx` ます。

[![東京 Traders 社が提供する製品が表示されます。](master-detail-filtering-across-two-pages-vb/_static/image33.png)](master-detail-filtering-across-two-pages-vb/_static/image32.png)

**図 12**: 東京 Traders が提供する製品が表示されます ([クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-vb/_static/image34.png)されます)

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>仕入先情報の表示`ProductsForSupplierDetails.aspx`

図12に示すように、 `ProductsForSupplierDetails.aspx` `SupplierID` クエリ文字列に指定されたによって提供される製品の一覧が表示されます。 ただし、このページに直接送信されたユーザーは、図12に東京 Traders 社の製品が表示されていることはわかりません。 この問題を解決するには、このページでサプライヤー情報を表示することもできます。

まず、products GridView の上に FormView を追加します。 クラスのメソッドを呼び出すという名前の新しい ObjectDataSource コントロールを作成 `SuppliersDataSource` `SuppliersBLL` `GetSupplierBySupplierID(supplierID)` します。

[![SuppliersBLL クラスを選択します。](master-detail-filtering-across-two-pages-vb/_static/image36.png)](master-detail-filtering-across-two-pages-vb/_static/image35.png)

**図 13**: クラスを選択 `SuppliersBLL` [する (クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-vb/_static/image37.png)されます)

[![ObjectDataSource で GetSupplierBySupplierID (仕入先) メソッドを呼び出します。](master-detail-filtering-across-two-pages-vb/_static/image39.png)](master-detail-filtering-across-two-pages-vb/_static/image38.png)

**図 14**: ObjectDataSource によってメソッドが呼び出されるよう `GetSupplierBySupplierID(supplierID)` [にする (クリックすると、フルサイズのイメージが表示](master-detail-filtering-across-two-pages-vb/_static/image40.png)されます)

と同様に、 `ProductsBySupplierDataSource` パラメーターに *`supplierID`* querystring 値の値が割り当てられている必要があり `SupplierID` ます。

[![仕入先のパラメーター値に、仕入先の Querystring の値を設定します。](master-detail-filtering-across-two-pages-vb/_static/image42.png)](master-detail-filtering-across-two-pages-vb/_static/image41.png)

**図 15**: *`supplierID`* Querystring 値からパラメーター値を設定 `SupplierID` する ([クリックすると、フルサイズのイメージが表示](master-detail-filtering-across-two-pages-vb/_static/image43.png)されます)

デザインビューで FormView を ObjectDataSource にバインドすると、Visual Studio は、 `ItemTemplate` `InsertItemTemplate` `EditItemTemplate` objectdatasource によって返される各データフィールドに対して、ラベルと TextBox Web コントロールを含む formview の、、およびを自動的に作成します。 仕入先情報を表示するだけなので、とを削除してもかまい `InsertItemTemplate` `EditItemTemplate` ません。 次に、ItemTemplate を編集して、仕入先の会社名を要素に、 `<h3>` 住所、市区町村、国、電話番号を会社名の下に表示するようにします。 または、「ObjectDataSource を使用した `DataSourceID` `ItemTemplate` データの[表示](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)」のチュートリアルで説明したように、手動で FormView を設定し、マークアップを作成することもできます。

これらの編集の後、FormView の宣言型マークアップは次のようになります。

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample3.aspx)]

図16は、上記の業者情報が含まれていた後のページのスクリーンショットを示し `ProductsForSupplierDetails.aspx` ています。

[![製品の一覧には、業者に関する概要が含まれています。](master-detail-filtering-across-two-pages-vb/_static/image45.png)](master-detail-filtering-across-two-pages-vb/_static/image44.png)

**図 16**: 製品の一覧には、業者に関する概要が含まれています ([クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-vb/_static/image46.png)されます)

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>UI の最後のタッチを適用する `ProductsForSupplierDetails.aspx`

このレポートのユーザーエクスペリエンスを向上させるために、このページにはいくつかの追加機能が用意されてい `ProductsForSupplierDetails.aspx` ます。 現在、ユーザーがページからサプライヤーの一覧に戻ることができる唯一の方法 `ProductsForSupplierDetails.aspx` は、ブラウザーの [戻る] ボタンをクリックすることです。 リンク先のページにハイパーリンクコントロールを追加して `ProductsForSupplierDetails.aspx` `SupplierListMaster.aspx` 、ユーザーがマスターリストに戻るための別の方法を提供してみましょう。

[![ハイパーリンクコントロールを追加して、ユーザーを SupplierListMaster に戻します。](master-detail-filtering-across-two-pages-vb/_static/image48.png)](master-detail-filtering-across-two-pages-vb/_static/image47.png)

**図 17**: ハイパーリンクコントロールを追加して、ユーザーに戻るようにします `SupplierListMaster.aspx` ([クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-vb/_static/image49.png)されます)

製品が存在しない仕入先の [製品の表示] リンクをクリックした場合、 `ProductsBySupplierDataSource` の ObjectDataSource は `ProductsForSupplierDetails.aspx` 結果を返しません。 ObjectDataSource にバインドされている GridView では、ユーザーのブラウザーのページに空白の領域が生じるマークアップはレンダリングされません。 選択した業者に関連付けられている製品がないことをユーザーにより明確に伝えるために、 `EmptyDataText` このような状況が発生したときに表示するメッセージに GridView のプロパティを設定できます。 このプロパティを "この供給業者によって提供される製品はありません" に設定しました。

既定では、Northwinds データベースのすべての仕入先は、少なくとも1つの製品を提供します。 ただし、このチュートリアルでは、 `Products` Supplier Escargots Nouveaux が製品に関連付けられなくなるように、テーブルを手動で変更しました。 図18は、この変更が行われた後の Escargots Nouveaux の詳細ページを示しています。

[![仕入先が製品を提供していないことがユーザーに通知されます。](master-detail-filtering-across-two-pages-vb/_static/image51.png)](master-detail-filtering-across-two-pages-vb/_static/image50.png)

**図 18**: 業者が製品を提供していないことがユーザーに通知される ([クリックすると、フルサイズの画像が表示](master-detail-filtering-across-two-pages-vb/_static/image52.png)されます)

## <a name="summary"></a>まとめ

マスター/詳細レポートでは、マスターレコードと詳細レコードの両方を1ページに表示できますが、多くの web サイトでは、2つの web ページに分割されています。 このチュートリアルでは、このようなマスター/詳細レポートを実装する方法について説明しました。これには、"マスター" web ページの GridView にサプライヤーを一覧表示し、[詳細] ページに一覧表示されている関連製品を表示します。 マスター web ページの各 supplier 行には、行の値に沿って渡された詳細ページへのリンクが含まれていま `SupplierID` した。 このような行固有のリンクは、GridView の [ハイパーリンク] フィールドを使用して簡単に追加できます。

詳細ページでは、クラスのメソッドを呼び出すことによって、指定された業者のこれらの製品を取得しました `ProductsBLL` `GetProductsBySupplierID(supplierID)` 。 パラメーター *`supplierID`* の値は、querystring をパラメーターソースとして使用して宣言的に指定されました。 また、FormView を使用して詳細ページでサプライヤーの詳細を表示する方法についても説明しました。

[次のチュートリアル](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)では、マスター/詳細レポートについて説明します。 GridView で製品の一覧を表示する方法について説明します。各行には [選択] ボタンがあります。 [選択] ボタンをクリックすると、同じページの DetailsView コントロールにその製品の詳細が表示されます。

プログラミングを楽しんでください。

## <a name="about-the-author"></a>著者について

1998以来、 [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)は 7 asp/創設者 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)の執筆者であり、Microsoft Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は [*、ASP.NET 2.0 を24時間以内に教え*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ています。 彼は、にアクセスでき[ mitchell@4GuysFromRolla.com ます。](mailto:mitchell@4GuysFromRolla.com) または彼のブログを参照してください。これは、「」にあり [http://ScottOnWriting.NET](http://ScottOnWriting.NET) ます。

## <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビュー担当者は、Hilton Giesenow でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、に行をドロップ[ mitchell@4GuysFromRolla.com します。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [前へ](master-detail-filtering-with-two-dropdownlists-vb.md)
> [次へ](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)
