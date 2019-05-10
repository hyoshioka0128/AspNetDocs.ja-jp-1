---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
title: (C#) Repeater コントロールで ModalPopup を使用する |Microsoft Docs
author: wenz
description: AJAX Control Toolkit の ModalPopup コントロールには、クライアント側の手段を使用してモーダル ポップアップを作成する簡単な方法が用意されています。 この contr. を使用することも.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d686d84a-1c58-492e-8a77-3eb5a0cfe918
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: f6d17fb9c09a9b0a7dda7335491c10e136a91170
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115383"
---
# <a name="using-modalpopup-with-a-repeater-control-c"></a><span data-ttu-id="fb8d3-104">Repeater コントロールで ModalPopup を使用する (C#)</span><span class="sxs-lookup"><span data-stu-id="fb8d3-104">Using ModalPopup with a Repeater Control (C#)</span></span>

<span data-ttu-id="fb8d3-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="fb8d3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fb8d3-106">[コードのダウンロード](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip)または[PDF のダウンロード](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="fb8d3-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)</span></span>

> <span data-ttu-id="fb8d3-107">AJAX Control Toolkit の ModalPopup コントロールには、クライアント側の手段を使用してモーダル ポップアップを作成する簡単な方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="fb8d3-108">Repeater 内でこのコントロールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-108">It is also possible to use this control within a repeater.</span></span>

## <a name="overview"></a><span data-ttu-id="fb8d3-109">概要</span><span class="sxs-lookup"><span data-stu-id="fb8d3-109">Overview</span></span>

<span data-ttu-id="fb8d3-110">AJAX Control Toolkit の ModalPopup コントロールには、クライアント側の手段を使用してモーダル ポップアップを作成する簡単な方法が用意されています。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="fb8d3-111">Repeater 内でこのコントロールを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-111">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="fb8d3-112">手順</span><span class="sxs-lookup"><span data-stu-id="fb8d3-112">Steps</span></span>

<span data-ttu-id="fb8d3-113">まず、データ ソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-113">First of all, a data source is required.</span></span> <span data-ttu-id="fb8d3-114">このサンプルでは、AdventureWorks データベースと Microsoft SQL Server 2005 Express Edition を使用します。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="fb8d3-115">データベース (express edition を含む)、Visual Studio のインストールのオプションの一部であるし、下の個別のダウンロードとしても利用[ https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)します。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="fb8d3-116">AdventureWorks データベースが SQL Server 2005 サンプルとサンプル データベースの一部 (ダウンロード[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="fb8d3-117">データベースをセットアップする最も簡単な方法は、Microsoft SQL Server Management Studio Express を使用する、([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) とアタッチ、`AdventureWorks.mdf`データベース ファイル。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span> <span data-ttu-id="fb8d3-118">このサンプルでは、SQL Server 2005 Express Edition のインスタンスが呼び出されること前提としています`SQLEXPRESS`は web サーバーと同じコンピューター上に存在して、既定の設定にもなります。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="fb8d3-119">場合は、セットアップが異なる場合は、データベースの接続情報を調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-119">If your setup differs, you have to adapt the connection information for the database.</span></span> <span data-ttu-id="fb8d3-120">ASP.NET AJAX Control Toolkit の機能をアクティブ化するために、`ScriptManager`コントロールは、ページのどこでも配置する必要があります (ただし内、`<form>`要素)。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="fb8d3-121">次に、ページにデータ ソースを追加します。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-121">Then, add a data source to the page.</span></span> <span data-ttu-id="fb8d3-122">少量のデータを使用するためにはのみ、AdventureWorks データベースの Vendor テーブルの最初の 5 つのエントリを選択します。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="fb8d3-123">データ ソースを作成するには、Visual Studio アシスタントを使用する場合は、現在のバージョンのバグは、テーブル名のプレフィックスにしないことに注意してください。 (`Vendor`) と`Purchasing`します。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="fb8d3-124">次のマークアップは、正しい構文を示しています。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="fb8d3-125">次に、モーダル ポップアップとして機能するパネルを追加します。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-125">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="fb8d3-126">含まれている、`Button`コントロールをもう一度、ポップアップを閉じます。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-126">It contains a `Button` control to close the popup again:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="fb8d3-127">リピータ内でポップアップを作成するには、`ModalPopupExtender`内でコントロールを配置する必要があります、 `<ItemTemplate>` repeater のセクション。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-127">In order to make the popup work within the repeater, the `ModalPopupExtender` control must be put within the `<ItemTemplate>` section of the repeater.</span></span> <span data-ttu-id="fb8d3-128">ように、パネルが、repeater 外ですが、エクステンダーが内部です。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-128">So the panel is outside the repeater, but the extender is inside.</span></span> <span data-ttu-id="fb8d3-129">リピータのマークアップを次に示します。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-129">Here is the markup for the repeater:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="fb8d3-130">次に、モーダル ポップアップをトリガーするように、その横にあるボタンで、データ ソース内のすべての項目が表示されます。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-130">Then, every item in the data source is displayed with a button next to it that triggers the modal popup.</span></span>

<span data-ttu-id="fb8d3-131">[![データ ソースのエントリごとに、モーダル ポップアップをトリガーできます。](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fb8d3-131">[![The modal popup can be triggered for every data source entry](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="fb8d3-132">データ ソースのエントリごとに、モーダル ポップアップをトリガーできます ([フルサイズの画像を表示する をクリックします](using-modalpopup-with-a-repeater-control-cs/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="fb8d3-132">The modal popup can be triggered for every data source entry ([Click to view full-size image](using-modalpopup-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fb8d3-133">[前へ](launching-a-modal-popup-window-from-server-code-cs.md)
> [次へ](handling-postbacks-from-a-modalpopup-cs.md)</span><span class="sxs-lookup"><span data-stu-id="fb8d3-133">[Previous](launching-a-modal-popup-window-from-server-code-cs.md)
[Next](handling-postbacks-from-a-modalpopup-cs.md)</span></span>
