---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: AJAX Control Toolkit コントロールとコントロールエクステンダーの使用 (VB) |Microsoft Docs
author: rick-anderson
description: AJAX Control Toolkit のコントロールとエクステンダーを ASP.NET ページに追加する方法について説明します。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 416ee0d4931a3850c1e9bb4ba28db43f5e1647bf
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044364"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a>AJAX Control Toolkit のコントロールとコントロール エクステンダーを使用する (VB)

[Microsoft](https://github.com/microsoft)

> AJAX Control Toolkit のコントロールとエクステンダーを ASP.NET ページに追加する方法について説明します。

AJAX Control Toolkit には、一連のコントロールとコントロールエクステンダーが含まれています。 この簡単なチュートリアルでは、ASP.NET ページにコントロールとコントロールエクステンダーの両方を追加する方法について説明します。

> [!NOTE] 
> 
> Ajax コントロールツールキットをインストールし、Visual Studio/Visual Web Developer ツールボックスに AJAX Control Toolkit を追加する方法については、「チュートリアル- [Ajax Control toolkit の概要](get-started-with-the-ajax-control-toolkit-vb.md)」を参照してください。

## <a name="using-ajax-control-toolkit-controls"></a>AJAX コントロールツールキットコントロールの使用

AJAX コントロールツールキットコントロールは、通常の ASP.NET コントロールと同様に動作します。 ツールボックスから ASP.NET ページにコントロールをドラッグできます。 コントロールは、デザインビューまたはソースビューのいずれかのページに追加できます。

AJAX Control Toolkit のコントロールを使用する場合は、特別な要件が1つあります。 ページに ScriptManager コントロールが含まれている必要があります。 ScriptManager コントロールは、AJAX コントロールツールキットコントロールに必要なすべての JavaScript を含めることを担当します。

たとえば、AJAX コントロールツールキットタブには、エディターコントロールという名前のコントロールが含まれています。 このコントロールは、リッチ HTML エディターを表示します。 次の手順に従って、エディターコントロールをページに追加します。

1. ShowEditor という名前の新しい ASP.NET ページを作成します。
2. [ツールボックス] の [AJAX 拡張] タブの下にある ScriptManager コントロールを選択し、コントロールをページにドラッグします。
3. ツールボックスの [AJAX Control Toolkit] タブの下にあるエディターコントロールを選択し、コントロールをページにドラッグします (図1を参照)。 デザイナーは図2のようになります。
4. メニューオプション [デバッグ]、[デバッグの **開始** ] の順に選択するか、F5 キーを押して、web サイトを実行します。
5. 図3のページが表示されます。

[![HTML エディターコントロールの選択](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)

**図 01**: HTML エディターコントロールを選択[する (クリックすると、フルサイズのイメージが表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png)されます)

[![ScriptManager コントロールとエディットコントロールを使用した Visual Studio デザイナー](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)

**図 02**: ScriptManager コントロールとエディットコントロールを使用した Visual Studio デザイナー ([クリックすると、フルサイズのイメージが表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png)されます)

[![DisplayEditor .aspx ページ](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)

**図 03**: displayeditor .aspx ページ ([クリックしてフルサイズのイメージを表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))

## <a name="using-ajax-control-toolkit-control-extenders"></a>AJAX Control Toolkit コントロールエクステンダーの使用

AJAX コントロールツールキットには、コントロールエクステンダーも含まれています。 名前が示すように、コントロールエクステンダーは既存のコントロールの機能を拡張します。 たとえば、ConfirmButton コントロールエクステンダーは、標準の ASP.NET Button コントロールを拡張します。 エクステンダーは、ボタンコントロールの動作を変更して、ボタンをクリックしたときに確認ダイアログが表示されるようにします。

コントロールエクステンダーは、AJAX コントロールツールキットコントロールと同様に、ScriptManager コントロールを必要とします。 ページでコントロールエクステンダーの使用を開始する前に、ScriptManager コントロールをページに追加する必要があります。

ConfirmButton コントロールエクステンダーを使用するには、次の手順に従います。

1. ShowConfirmButton .aspx という名前の新しい ASP.NET ページを作成します。
2. [AJAX 拡張] タブの下にあるページにコントロールをドラッグして、ScriptManager コントロールをページに追加します。
3. ツールボックスの [標準] タブの下にあるボタンをデザイナー画面にドラッグして、標準のボタンコントロールをページに追加します。
4. [拡張タスクの **追加** ] オプションをクリックします (図4を参照)。
5. [拡張の選択] ダイアログで、[ConfirmButtonExtender] を選択し (図5を参照)、[OK] ボタンをクリックします。
6. デザイナーで [Button] コントロールを選択し、プロパティウィンドウの Extender、Button1 confirmbuttonextender ノードの順に展開し \_ ます (図6を参照)。 値 *' 本当? '* を割り当てる を ConfirmText プロパティにします。
7. メニューオプション [ **デバッグ]、[デバッグの開始** ] の順に選択するか、F5 キーを押して、ページを実行します。

[![[拡張タスクの追加] オプション](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)

**図 04**: [拡張タスクの追加] オプション ([クリックすると、フルサイズの画像が表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png)されます)

[![ConfirmButton コントロールエクステンダーの選択](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)

**図 05**: confirmbutton コントロールエクステンダーを選択[する (クリックすると、フルサイズのイメージが表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png)されます)

[![ConfirmButton プロパティの設定](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)

**図 06**: confirmbutton プロパティの設定 ([クリックすると、フルサイズの画像が表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png)される)

ページが開くと、ボタンが表示されます。 このボタンをクリックすると、図7の確認ダイアログが表示されます。

[![確認ダイアログを表示しています](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)

**図 07**: 確認ダイアログ[を表示する (クリックすると、フルサイズの画像が表示](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png)されます)

通常は、コントロールエクステンダーをページにドラッグしないことに注意してください。 代わりに、[拡張タスクの **追加** ] オプションを使用して、既にページに追加したコントロールに extender を追加します。 さらに、拡張されるコントロールのプロパティシートを開いて、コントロールエクステンダーのプロパティを設定することにも注意してください。

1つの ASP.NET コントロールは、複数のコントロールエクステンダーで拡張できます。 拡張されるコントロールのプロパティシートには、コントロールに関連付けられているすべてのコントロールエクステンダーが一覧表示されます。

> [!div class="step-by-step"]
> [前へ](get-started-with-the-ajax-control-toolkit-vb.md)
> [次へ](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)
