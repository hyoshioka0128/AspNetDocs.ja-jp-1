---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: ドラッグ アンド ドロップで ReorderList (c#) |Microsoft Docs
author: wenz
description: ReorderList コントロール、AJAX Control Toolkit では、ユーザーがドラッグ アンド ドロップを使用して並べ替えることができる一覧を提供します。 現在の注文リストのものとしています.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 8adeceba0d43d6baf1af944a910750ca0682b097
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124932"
---
# <a name="drag-and-drop-via-reorderlist-c"></a><span data-ttu-id="4895f-104">ReorderList 経由でドラッグ アンド ドロップする (C#)</span><span class="sxs-lookup"><span data-stu-id="4895f-104">Drag and Drop via ReorderList (C#)</span></span>

<span data-ttu-id="4895f-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4895f-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4895f-106">[コードのダウンロード](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip)または[PDF のダウンロード](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="4895f-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span></span>

> <span data-ttu-id="4895f-107">ReorderList コントロール、AJAX Control Toolkit では、ユーザーがドラッグ アンド ドロップを使用して並べ替えることができる一覧を提供します。</span><span class="sxs-lookup"><span data-stu-id="4895f-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="4895f-108">リストの現在の順序は、サーバーに保存されます。</span><span class="sxs-lookup"><span data-stu-id="4895f-108">The current order of the list shall be persisted on the server.</span></span>

## <a name="overview"></a><span data-ttu-id="4895f-109">概要</span><span class="sxs-lookup"><span data-stu-id="4895f-109">Overview</span></span>

<span data-ttu-id="4895f-110">`ReorderList` AJAX Control Toolkit でコントロールには、ユーザーがドラッグ アンド ドロップを使用して並べ替えることができる一覧が用意されています。</span><span class="sxs-lookup"><span data-stu-id="4895f-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="4895f-111">リストの現在の順序は、サーバーに保存されます。</span><span class="sxs-lookup"><span data-stu-id="4895f-111">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="4895f-112">手順</span><span class="sxs-lookup"><span data-stu-id="4895f-112">Steps</span></span>

<span data-ttu-id="4895f-113">`ReorderList`コントロールが一覧に、データベースからデータをバインディングをサポートします。</span><span class="sxs-lookup"><span data-stu-id="4895f-113">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="4895f-114">何よりすばらしいは、データ ストアにリストの要素の順序の変更の書き込みもサポートしています。</span><span class="sxs-lookup"><span data-stu-id="4895f-114">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="4895f-115">このサンプルでは、データ ストアとして Microsoft SQL Server 2005 Express Edition を使用します。</span><span class="sxs-lookup"><span data-stu-id="4895f-115">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="4895f-116">データベースは、express edition を含め、Visual Studio のインストールのオプション (および無料) 部分です。</span><span class="sxs-lookup"><span data-stu-id="4895f-116">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="4895f-117">個別のダウンロードとして入手[ https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)します。</span><span class="sxs-lookup"><span data-stu-id="4895f-117">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="4895f-118">このサンプルでは、SQL Server 2005 Express Edition のインスタンスが呼び出されること前提としています`SQLEXPRESS`は web サーバーと同じコンピューター上に存在して、既定の設定にもなります。</span><span class="sxs-lookup"><span data-stu-id="4895f-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="4895f-119">場合は、セットアップが異なる場合は、データベースの接続情報を調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4895f-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="4895f-120">データベースを設定する最も簡単な方法は、Microsoft SQL Server Management Studio Express を使用する、([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) )。</span><span class="sxs-lookup"><span data-stu-id="4895f-120">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="4895f-121">サーバーへの接続をダブルクリックして`Databases`新しいデータベースを作成し、(右クリックし、 `New Database`) と呼ばれる`Tutorials`します。</span><span class="sxs-lookup"><span data-stu-id="4895f-121">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="4895f-122">という新しいテーブルを作成すると、このデータベースに`AJAX`次の 4 つの列を含む。</span><span class="sxs-lookup"><span data-stu-id="4895f-122">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="4895f-123">`id` (プライマリ キー、整数、identity、いない NULL)</span><span class="sxs-lookup"><span data-stu-id="4895f-123">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="4895f-124">`char` (char (1)、NULL)</span><span class="sxs-lookup"><span data-stu-id="4895f-124">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="4895f-125">`description` (varchar (50)、NULL)</span><span class="sxs-lookup"><span data-stu-id="4895f-125">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="4895f-126">`position` (int, NULL)</span><span class="sxs-lookup"><span data-stu-id="4895f-126">`position` (int, NULL)</span></span>

<span data-ttu-id="4895f-127">[![AJAX のテーブルのレイアウト](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4895f-127">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="4895f-128">AJAX のテーブルのレイアウト ([フルサイズの画像を表示する をクリックします](drag-and-drop-via-reorderlist-cs/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="4895f-128">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span></span>

<span data-ttu-id="4895f-129">次に、表に、いくつかの値を設定します。</span><span class="sxs-lookup"><span data-stu-id="4895f-129">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="4895f-130">なお、`position`列は、要素の並べ替え順序を保持します。</span><span class="sxs-lookup"><span data-stu-id="4895f-130">Note that the `position` column holds the sort order of the elements.</span></span>

<span data-ttu-id="4895f-131">[![AJAX の表に、初期データ](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="4895f-131">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span></span>

<span data-ttu-id="4895f-132">AJAX の表に、初期データ ([フルサイズの画像を表示する をクリックします](drag-and-drop-via-reorderlist-cs/_static/image6.png))。</span><span class="sxs-lookup"><span data-stu-id="4895f-132">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span></span>

<span data-ttu-id="4895f-133">次の手順を生成する必要があります、`SqlDataSource`新しいデータベースとそのテーブルでの通信を制御します。</span><span class="sxs-lookup"><span data-stu-id="4895f-133">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="4895f-134">データ ソースをサポートする必要があります、`SELECT`と`UPDATE`SQL コマンド。</span><span class="sxs-lookup"><span data-stu-id="4895f-134">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="4895f-135">リストの要素の順序が変更された後で、ときに、`ReorderList`コントロールは、データ ソースの 2 つの値を自動的に送信する`Update`コマンド: 新しい位置と、要素の ID。</span><span class="sxs-lookup"><span data-stu-id="4895f-135">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="4895f-136">そのため、データ ソースのニーズ、`<UpdateParameters>`これら 2 つの値のセクション。</span><span class="sxs-lookup"><span data-stu-id="4895f-136">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="4895f-137">`ReorderList`コントロールは、次の属性を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4895f-137">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="4895f-138">`AllowReorder`:かどうか、リスト項目を並べ替えることができます。</span><span class="sxs-lookup"><span data-stu-id="4895f-138">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="4895f-139">`DataSourceID`:データ ソースの ID</span><span class="sxs-lookup"><span data-stu-id="4895f-139">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="4895f-140">`DataKeyField`:データ ソースに主キー列の名前</span><span class="sxs-lookup"><span data-stu-id="4895f-140">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="4895f-141">`SortOrderField`:リスト項目の並べ替え順序を提供するデータ ソース列</span><span class="sxs-lookup"><span data-stu-id="4895f-141">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="4895f-142">`<DragHandleTemplate>`と`<ItemTemplate>`セクションでは、リストのレイアウトを微調整することができます。</span><span class="sxs-lookup"><span data-stu-id="4895f-142">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="4895f-143">また、データ バインドが可能なを使用して、`Eval()`メソッド、ご覧のとおり。</span><span class="sxs-lookup"><span data-stu-id="4895f-143">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="4895f-144">次の CSS スタイル情報 (で参照されている、`<DragHandleTemplate>`のセクション、`ReorderList`コントロール) により、マウス ポインターをドラッグ ハンドルに置いたときに適切に変更します。</span><span class="sxs-lookup"><span data-stu-id="4895f-144">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

<span data-ttu-id="4895f-145">最後に、`ScriptManager`コントロールがページの ASP.NET AJAX を初期化します。</span><span class="sxs-lookup"><span data-stu-id="4895f-145">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="4895f-146">ブラウザーでこの例を実行し、リスト項目を少し変更します。</span><span class="sxs-lookup"><span data-stu-id="4895f-146">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="4895f-147">次に、ページを再度読み込んでか、データベースを見てください。</span><span class="sxs-lookup"><span data-stu-id="4895f-147">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="4895f-148">変更後の位置が保持されているし、は、値でも反映されます、`position`データベース内の列のマークアップを使用して、任意のコードは一切だけです。</span><span class="sxs-lookup"><span data-stu-id="4895f-148">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>

<span data-ttu-id="4895f-149">[![新しい一覧項目の順序に従って、データベースで変更データ](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="4895f-149">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span></span>

<span data-ttu-id="4895f-150">新しい一覧に従って、データベースで変更データ項目の順序 ([フルサイズの画像を表示する をクリックします](drag-and-drop-via-reorderlist-cs/_static/image9.png))。</span><span class="sxs-lookup"><span data-stu-id="4895f-150">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4895f-151">[前へ](using-postbacks-with-reorderlist-cs.md)
> [次へ](using-postbacks-with-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="4895f-151">[Previous](using-postbacks-with-reorderlist-cs.md)
[Next](using-postbacks-with-reorderlist-vb.md)</span></span>
