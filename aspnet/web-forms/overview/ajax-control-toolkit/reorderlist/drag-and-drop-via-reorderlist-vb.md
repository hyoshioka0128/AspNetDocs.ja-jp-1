---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
title: ReorderList を使用してドラッグアンドドロップ (VB) |Microsoft Docs
author: wenz
description: /data-access/tutorials/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 848e6bcf-4c3f-4d14-974d-e45b9444ab79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 3f7c5749053d8bf587467fb1939fca05ce2872a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446086"
---
# <a name="drag-and-drop-via-reorderlist-vb"></a><span data-ttu-id="20935-103">ReorderList 経由でドラッグ アンド ドロップする (VB)</span><span class="sxs-lookup"><span data-stu-id="20935-103">Drag and Drop via ReorderList (VB)</span></span>

<span data-ttu-id="20935-104">[Christian Wenz](https://github.com/wenz)別</span><span class="sxs-lookup"><span data-stu-id="20935-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="20935-105">[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="20935-105">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span></span>

> <span data-ttu-id="20935-106">AJAX コントロールツールキットの ReorderList コントロールは、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストを提供します。</span><span class="sxs-lookup"><span data-stu-id="20935-106">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="20935-107">リストの現在の順序は、サーバーで保持されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="20935-107">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="20935-108">概要</span><span class="sxs-lookup"><span data-stu-id="20935-108">Overview</span></span>

<span data-ttu-id="20935-109">AJAX コントロールツールキットの `ReorderList` コントロールには、ドラッグアンドドロップを使用してユーザーが並べ替えることのできるリストが用意されています。</span><span class="sxs-lookup"><span data-stu-id="20935-109">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="20935-110">リストの現在の順序は、サーバーで保持されている必要があります。</span><span class="sxs-lookup"><span data-stu-id="20935-110">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="20935-111">手順</span><span class="sxs-lookup"><span data-stu-id="20935-111">Steps</span></span>

<span data-ttu-id="20935-112">`ReorderList` コントロールでは、データベースからリストへのデータのバインドがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="20935-112">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="20935-113">また、リスト要素の順序に対する変更をデータストアに書き戻すこともできます。</span><span class="sxs-lookup"><span data-stu-id="20935-113">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="20935-114">このサンプルでは、データストアとして Microsoft SQL Server 2005 Express Edition を使用します。</span><span class="sxs-lookup"><span data-stu-id="20935-114">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="20935-115">データベースは、Visual Studio のインストールにおいて、express edition を含む省略可能な (無料の) 部分です。</span><span class="sxs-lookup"><span data-stu-id="20935-115">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="20935-116">また、 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)で個別にダウンロードすることもできます。</span><span class="sxs-lookup"><span data-stu-id="20935-116">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="20935-117">このサンプルでは、SQL Server 2005 Express Edition のインスタンスが `SQLEXPRESS` 呼び出され、web サーバーと同じコンピューター上に存在することを前提としています。これは、既定のセットアップでもあります。</span><span class="sxs-lookup"><span data-stu-id="20935-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="20935-118">セットアップが異なる場合は、データベースの接続情報を調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20935-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="20935-119">データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ) を使用することです。</span><span class="sxs-lookup"><span data-stu-id="20935-119">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="20935-120">サーバーに接続し、`Databases` をダブルクリックして、新しいデータベースを作成します (右クリックして [`New Database`] を選択し `Tutorials`)。</span><span class="sxs-lookup"><span data-stu-id="20935-120">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="20935-121">このデータベースで、次の4つの列を含む `AJAX` という名前の新しいテーブルを作成します。</span><span class="sxs-lookup"><span data-stu-id="20935-121">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="20935-122">`id` (主キー、整数、id、NULL 以外)</span><span class="sxs-lookup"><span data-stu-id="20935-122">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="20935-123">`char` (char (1)、NULL)</span><span class="sxs-lookup"><span data-stu-id="20935-123">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="20935-124">`description` (varchar (50)、NULL)</span><span class="sxs-lookup"><span data-stu-id="20935-124">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="20935-125">`position` (int, NULL)</span><span class="sxs-lookup"><span data-stu-id="20935-125">`position` (int, NULL)</span></span>

<span data-ttu-id="20935-126">[AJAX テーブルのレイアウトの ![](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="20935-126">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="20935-127">AJAX テーブルのレイアウト ([クリックすると、フルサイズの画像が表示](drag-and-drop-via-reorderlist-vb/_static/image3.png)されます)</span><span class="sxs-lookup"><span data-stu-id="20935-127">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span></span>

<span data-ttu-id="20935-128">次に、テーブルにいくつかの値を入力します。</span><span class="sxs-lookup"><span data-stu-id="20935-128">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="20935-129">`position` 列には、要素の並べ替え順序が保持されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="20935-129">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="20935-130">[AJAX テーブルの初期データの ![](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="20935-130">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span></span>

<span data-ttu-id="20935-131">AJAX テーブルの初期データ ([クリックすると、フルサイズの画像が表示](drag-and-drop-via-reorderlist-vb/_static/image6.png)されます)</span><span class="sxs-lookup"><span data-stu-id="20935-131">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span></span>

<span data-ttu-id="20935-132">次の手順では、新しいデータベースとそのテーブルと通信するために `SqlDataSource` コントロールを生成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20935-132">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="20935-133">データソースでは、`SELECT` および `UPDATE` SQL コマンドがサポートされている必要があります。</span><span class="sxs-lookup"><span data-stu-id="20935-133">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="20935-134">リスト要素の順序が変更されると、`ReorderList` コントロールは、新しい位置と要素の ID の2つの値を、データソースの `Update` コマンドに自動的に送信します。</span><span class="sxs-lookup"><span data-stu-id="20935-134">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="20935-135">そのため、データソースには、次の2つの値の `<UpdateParameters>` セクションが必要です。</span><span class="sxs-lookup"><span data-stu-id="20935-135">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="20935-136">`ReorderList` コントロールでは、次の属性を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20935-136">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="20935-137">`AllowReorder`: リスト項目を並べ替えることができるかどうか</span><span class="sxs-lookup"><span data-stu-id="20935-137">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="20935-138">`DataSourceID`: データソースの ID</span><span class="sxs-lookup"><span data-stu-id="20935-138">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="20935-139">`DataKeyField`: データソースの主キー列の名前</span><span class="sxs-lookup"><span data-stu-id="20935-139">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="20935-140">`SortOrderField`: リスト項目の並べ替え順序を提供するデータソース列</span><span class="sxs-lookup"><span data-stu-id="20935-140">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="20935-141">`<DragHandleTemplate>` セクションと `<ItemTemplate>` セクションでは、一覧のレイアウトを微調整できます。</span><span class="sxs-lookup"><span data-stu-id="20935-141">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="20935-142">また、次に示すように、`Eval()` メソッドを使用してデータバインディングを行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="20935-142">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="20935-143">次の CSS スタイル情報 (`ReorderList` コントロールの `<DragHandleTemplate>` セクションで参照) を使用すると、ドラッグハンドルの上にマウスポインターを置いたときに、マウスポインターが適切に変化します。</span><span class="sxs-lookup"><span data-stu-id="20935-143">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-vb/samples/sample3.css)]

<span data-ttu-id="20935-144">最後に、`ScriptManager` コントロールによって、ページの ASP.NET AJAX が初期化されます。</span><span class="sxs-lookup"><span data-stu-id="20935-144">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="20935-145">ブラウザーでこの例を実行し、リスト項目を1つのビットに再配置します。</span><span class="sxs-lookup"><span data-stu-id="20935-145">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="20935-146">次に、ページを再読み込みするか、データベースを確認します。</span><span class="sxs-lookup"><span data-stu-id="20935-146">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="20935-147">変更された位置が保持され、データベースの [`position`] 列の値と、マークアップを使用するだけで、すべてのコードが含まれていなくても反映されます。</span><span class="sxs-lookup"><span data-stu-id="20935-147">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="20935-148">[データベース内のデータが新しいリストアイテムの順序に従って変更 ![](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="20935-148">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span></span>

<span data-ttu-id="20935-149">データベース内のデータは、新しいリスト項目の順序に従って変更されます ([クリックすると、フルサイズの画像が表示](drag-and-drop-via-reorderlist-vb/_static/image9.png)されます)</span><span class="sxs-lookup"><span data-stu-id="20935-149">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="20935-150">[[戻る]](using-postbacks-with-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="20935-150">[Previous](using-postbacks-with-reorderlist-vb.md)</span></span>
