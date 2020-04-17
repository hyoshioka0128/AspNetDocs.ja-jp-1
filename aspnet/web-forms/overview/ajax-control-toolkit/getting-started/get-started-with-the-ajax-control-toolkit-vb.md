---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: AJAX コントロール ツールキット (VB) を使用して開始 |マイクロソフトドキュメント
author: rick-anderson
description: AJAX コントロール ツールキットの使用を開始するために知っておくべきことをすべて説明します。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: 6af5e293a35ce3e3ba35a0f7abfd2d92d538c84c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543562"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a><span data-ttu-id="9f469-103">AJAX Control Toolkit の概要 (VB)</span><span class="sxs-lookup"><span data-stu-id="9f469-103">Get Started with the AJAX Control Toolkit (VB)</span></span>

<span data-ttu-id="9f469-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9f469-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="9f469-105">AJAX コントロール ツールキットの使用を開始するために知っておくべきことをすべて説明します。</span><span class="sxs-lookup"><span data-stu-id="9f469-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="9f469-106">AJAX コントロール ツールキットには、ASP.NET アプリケーションで使用できる 30 を超える無料コントロールが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9f469-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="9f469-107">このチュートリアルでは、AJAX コントロール ツールキットをダウンロードし、Visual Studio/Visual Web 開発者エクスプレス ツールボックスにツールキット コントロールを追加する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="9f469-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="9f469-108">AJAX コントロール ツールキットのダウンロード</span><span class="sxs-lookup"><span data-stu-id="9f469-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="9f469-109">[AJAX コントロール ツールキット](http://devexpress.com/act)は、ASP.NET コミュニティのメンバーとASP.NET チームによって開発されたオープン ソース プロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="9f469-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span>

<span data-ttu-id="9f469-110">[![AJAX コントロール ツールキットのダウンロード](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9f469-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span></span>

<span data-ttu-id="9f469-111">**図 01**: AJAX コントロール ツールキットのダウンロード ([フルサイズの画像を表示する をクリック](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="9f469-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span></span>

<span data-ttu-id="9f469-112">ファイルをダウンロードした後、ファイルのブロックを解除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9f469-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="9f469-113">ファイルを右クリックし、[プロパティ] を選択して、[**ブロック**解除] ボタンをクリックします (図 2 参照)。</span><span class="sxs-lookup"><span data-stu-id="9f469-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="9f469-114">[![AJAX コントロール ツールキット ZIP ファイルのブロック解除](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="9f469-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span></span>

<span data-ttu-id="9f469-115">**図 02**: AJAX コントロール ツールキット ZIP ファイルのブロックを解除する ([フルサイズの画像を表示する をクリック](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="9f469-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span></span>

<span data-ttu-id="9f469-116">ファイルのブロックを解除した後、ファイルを解凍できます。 **Extract All**</span><span class="sxs-lookup"><span data-stu-id="9f469-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="9f469-117">これで、このツールキットを Visual Studio/Visual Web 開発者ツールボックスに追加する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="9f469-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="9f469-118">AJAX コントロール ツールキットをツールボックスに追加する</span><span class="sxs-lookup"><span data-stu-id="9f469-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="9f469-119">AJAX コントロール ツールキットを使用する最も簡単な方法は、Visual Studio/Visual Web 開発者ツールボックスにツールキットを追加することです (図 3 参照)。</span><span class="sxs-lookup"><span data-stu-id="9f469-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="9f469-120">この方法では、ツールキット コントロールを使用する場合に、ページ上にドラッグするだけで、そのコントロールをページにドラッグできます。</span><span class="sxs-lookup"><span data-stu-id="9f469-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="9f469-121">[![AJAX コントロール ツールキットがツールボックスに表示されます。](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="9f469-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span></span>

<span data-ttu-id="9f469-122">**図 03**: AJAX コントロール ツールキットがツールボックスに表示されます ([フルサイズの画像を表示する をクリック](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png)します)</span><span class="sxs-lookup"><span data-stu-id="9f469-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span></span>

<span data-ttu-id="9f469-123">まず、ツールボックスに AJAX コントロール ツールキット タブを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9f469-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="9f469-124">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="9f469-124">Follow these steps.</span></span>

1. <span data-ttu-id="9f469-125">メニューオプション「ファイル」「新規ウェブサイト」を選択して、新しいASP.NETWebサイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="9f469-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="9f469-126">[ソリューション エクスプローラー] ウィンドウで Default.aspx をダブルクリックして、エディターでファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="9f469-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="9f469-127">[全般] タブの下にある [ツールボックス] を右クリックし、メニュー オプションの **[タブの追加]** を選択します (図 4 参照)。</span><span class="sxs-lookup"><span data-stu-id="9f469-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="9f469-128">AJAX コントロール ツールキットという名前の新しいタブを入力します。</span><span class="sxs-lookup"><span data-stu-id="9f469-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="9f469-129">[![新しいタブを追加する](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="9f469-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span></span>

<span data-ttu-id="9f469-130">**図 04**: 新しいタブを追加する ([フルサイズの画像を表示する をクリック](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png)します)</span><span class="sxs-lookup"><span data-stu-id="9f469-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span></span>

<span data-ttu-id="9f469-131">次に、AJAX コントロール ツールキット コントロールを新しいタブに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9f469-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="9f469-132">[AJAX コントロール ツールキット] タブの下を右クリックし、メニュー オプションの **[項目の選択] を選択します (図 5 を参照**)。</span><span class="sxs-lookup"><span data-stu-id="9f469-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="9f469-133">AJAX コントロール ツールキットを解凍した場所を参照し、AjaxControlToolkit.dll アセンブリを選択します。</span><span class="sxs-lookup"><span data-stu-id="9f469-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="9f469-134">[![ツールボックスに追加する項目の選択](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="9f469-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span></span>

<span data-ttu-id="9f469-135">**図 05**: ツールボックスに追加する項目を選択します ([フルサイズの画像を表示する をクリック](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png)します)</span><span class="sxs-lookup"><span data-stu-id="9f469-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span></span>

<span data-ttu-id="9f469-136">これらの手順を完了すると、ツールキット コントロールがすべてツールボックスに表示されます。</span><span class="sxs-lookup"><span data-stu-id="9f469-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="9f469-137">新しいバージョンのツールキットへのアップグレード</span><span class="sxs-lookup"><span data-stu-id="9f469-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="9f469-138">古いリリースのツールキットを使用していて、新しいバージョンに移行する必要がある場合は、以下の手順を実行することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="9f469-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="9f469-139">バイナリ - ウェブサイトの Bin フォルダーから AjaxControlToolkit.dll アセンブリの古いバージョンを削除します。</span><span class="sxs-lookup"><span data-stu-id="9f469-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="9f469-140">ツールボックス項目 - AJAX コントロール ツールキット タブを削除し、上記の手順に従って、AjaxControlToolkit.dll アセンブリの新しいバージョンでタブを再作成します。</span><span class="sxs-lookup"><span data-stu-id="9f469-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9f469-141">[前へ](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [次へ](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9f469-141">[Previous](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
[Next](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span></span>
