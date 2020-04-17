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
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a>AJAX Control Toolkit の概要 (VB)

[マイクロソフト](https://github.com/microsoft)

> AJAX コントロール ツールキットの使用を開始するために知っておくべきことをすべて説明します。

AJAX コントロール ツールキットには、ASP.NET アプリケーションで使用できる 30 を超える無料コントロールが含まれています。 このチュートリアルでは、AJAX コントロール ツールキットをダウンロードし、Visual Studio/Visual Web 開発者エクスプレス ツールボックスにツールキット コントロールを追加する方法を学習します。

## <a name="downloading-the-ajax-control-toolkit"></a>AJAX コントロール ツールキットのダウンロード

[AJAX コントロール ツールキット](http://devexpress.com/act)は、ASP.NET コミュニティのメンバーとASP.NET チームによって開発されたオープン ソース プロジェクトです。

[![AJAX コントロール ツールキットのダウンロード](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)

**図 01**: AJAX コントロール ツールキットのダウンロード ([フルサイズの画像を表示する をクリック](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))

ファイルをダウンロードした後、ファイルのブロックを解除する必要があります。 ファイルを右クリックし、[プロパティ] を選択して、[**ブロック**解除] ボタンをクリックします (図 2 参照)。

[![AJAX コントロール ツールキット ZIP ファイルのブロック解除](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)

**図 02**: AJAX コントロール ツールキット ZIP ファイルのブロックを解除する ([フルサイズの画像を表示する をクリック](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))

ファイルのブロックを解除した後、ファイルを解凍できます。 **Extract All** これで、このツールキットを Visual Studio/Visual Web 開発者ツールボックスに追加する準備ができました。

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>AJAX コントロール ツールキットをツールボックスに追加する

AJAX コントロール ツールキットを使用する最も簡単な方法は、Visual Studio/Visual Web 開発者ツールボックスにツールキットを追加することです (図 3 参照)。 この方法では、ツールキット コントロールを使用する場合に、ページ上にドラッグするだけで、そのコントロールをページにドラッグできます。

[![AJAX コントロール ツールキットがツールボックスに表示されます。](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)

**図 03**: AJAX コントロール ツールキットがツールボックスに表示されます ([フルサイズの画像を表示する をクリック](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png)します)

まず、ツールボックスに AJAX コントロール ツールキット タブを追加する必要があります。 次の手順に従います。

1. メニューオプション「ファイル」「新規ウェブサイト」を選択して、新しいASP.NETWebサイトを作成します。 [ソリューション エクスプローラー] ウィンドウで Default.aspx をダブルクリックして、エディターでファイルを開きます。
2. [全般] タブの下にある [ツールボックス] を右クリックし、メニュー オプションの **[タブの追加]** を選択します (図 4 参照)。
3. AJAX コントロール ツールキットという名前の新しいタブを入力します。

[![新しいタブを追加する](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)

**図 04**: 新しいタブを追加する ([フルサイズの画像を表示する をクリック](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png)します)

次に、AJAX コントロール ツールキット コントロールを新しいタブに追加する必要があります。

- [AJAX コントロール ツールキット] タブの下を右クリックし、メニュー オプションの **[項目の選択] を選択します (図 5 を参照**)。
- AJAX コントロール ツールキットを解凍した場所を参照し、AjaxControlToolkit.dll アセンブリを選択します。

[![ツールボックスに追加する項目の選択](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)

**図 05**: ツールボックスに追加する項目を選択します ([フルサイズの画像を表示する をクリック](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png)します)

これらの手順を完了すると、ツールキット コントロールがすべてツールボックスに表示されます。

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>新しいバージョンのツールキットへのアップグレード

古いリリースのツールキットを使用していて、新しいバージョンに移行する必要がある場合は、以下の手順を実行することをお勧めします。

- バイナリ - ウェブサイトの Bin フォルダーから AjaxControlToolkit.dll アセンブリの古いバージョンを削除します。
- ツールボックス項目 - AJAX コントロール ツールキット タブを削除し、上記の手順に従って、AjaxControlToolkit.dll アセンブリの新しいバージョンでタブを再作成します。

> [!div class="step-by-step"]
> [前へ](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [次へ](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
