---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
title: カラーピッカー コントロール エクステンダ (C#) の使用 |マイクロソフトドキュメント
author: rick-anderson
description: ColorPicker は、ポップアップ コントロールの UI を使用してクライアント側の色を選択する機能を提供する AJAX エクステンダASP.NETです。 それは任意のASP.NETに取り付けることができます。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0d86a1e7-a910-4ab2-b85c-7a9ea6906c39
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 63b6bc58d36fdfcb5ee0a1c97988091e8d35505b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543133"
---
# <a name="using-the-colorpicker-control-extender-c"></a>カラーピッカー コントロール エクステンダーの使用 (C#)

[マイクロソフト](https://github.com/microsoft)

> ColorPicker は、ポップアップ コントロールの UI を使用してクライアント側の色を選択する機能を提供する AJAX エクステンダASP.NETです。 任意のASP.NET TextBox コントロールにアタッチできます。 それ。

このチュートリアルの目的は、AJAX コントロール ツールキット ColorPicker コントロール エクステンダーを使用する方法を説明することです。 ColorPicker コントロール エクステンダは、色を選択できるポップアップ ダイアログを表示します。 ColorPicker は、ユーザーが色を選択するための直感的なユーザー インターフェイスを提供する場合に便利です。

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>カラー ピッカー コントロール エクステンダを使用したテキスト ボックス コントロールの拡張

たとえば、訪問者がカスタマイズされた名刺を作成できる Web サイトを作成するとします。 来場者は名刺のテキストを入力し、色を選択することができます。 リスト 1 のASP.NET ページには、txtCardText と txtCardColor という名前の 2 つのテキスト ボックス コントロールがあります。 フォームを送信すると、選択した値が表示されます (図 1 参照)。

[![名刺を作成するための簡単なフォーム](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)

**図 01**: 名刺を作成するための簡易フォーム ([フルサイズの画像を表示する をクリック](using-the-colorpicker-control-extender-cs/_static/image2.png))

**リスト 1 - カードの作成.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample1.aspx)]

リスト 1 のフォームは機能しますが、優れたユーザー エクスペリエンスを提供しません。 ユーザーはテキストボックスに色を入力する必要があります。 ユーザーが特殊な色(例えば、エンドウ豆の緑のちょうど右の色合い)を望む場合、ユーザーは何の助けもなくHTMLカラーコードを把握する必要があります。

ColorPicker コントロール エクステンダーを使用すると、より優れたユーザー エクスペリエンスを作成できます。 ColorPicker は、テキスト ボックス コントロールにフォーカスを移動するときに色のダイアログボックスを表示します (図 2 を参照してください)。

[![カラーピッカー コントロール エクステンダ](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)

**図 02**: ColorPicker コントロール エクステンダ ([フルサイズの画像を表示する をクリック](using-the-colorpicker-control-extender-cs/_static/image4.png)します )

ColorPicker コントロール エクステンダをリスト 1 のフォームで使用するには、次の 2 つの手順を実行する必要があります。

1. ページにスクリプト マネージャー コントロールを追加する
2. ページに ColorPicker コントロール エクステンダーを追加します。

カラー ピッカーを使用する前に、ページにスクリプト マネージャーを追加する必要があります。 ScriptManager を追加する適切な場所は、サーバー側&lt;フォーム&gt;タグの開始のすぐ下にあります。 ツールボックスからページに ScriptManager をドラッグできます (ScriptManager は AJAX 拡張機能タブの下にあります)。 または、サーバー側フォームの開始タグの下にあるソースビューに次のタグを入力することもできます。

&lt;asp:スクリプトマネージャー ID="スクリプトマネージャー1" ランサット="サーバー" /&gt;

ColorPicker コントロール エクステンダーをページに追加する最も簡単な方法は、デザイン ビューです。 txtCardColor テキスト ボックスの上にマウス ポインタを置くと、スマート タスク オプションが表示され、エクステンダを追加できます (図 3 参照)。 このオプションを選択すると、エクステンダー ウィザードが表示されます (図 4 参照)。

[![エクステンダーの追加](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)

**図 03**: エクステンダの追加 ([フルサイズの画像を表示する をクリック](using-the-colorpicker-control-extender-cs/_static/image6.png))

[![エクステンダー ウィザードを使用したコントロール エクステンダの選択](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)

**図 04**: エクステンダ ウィザードでコントロール エクステンダを選択する ([フルサイズのイメージを表示する をクリック](using-the-colorpicker-control-extender-cs/_static/image8.png)して )

カラー ピッカー エクステンダーを選択して、カラー ピッカー エクステンダーを使用して txtCardColor テキスト ボックスを拡張できます。 [OK] をクリックしてダイアログ ボックスを閉じます。

これらの変更を行うと、ページのソースはリスト 2 のようになります。

リスト 2 - CreateCard.aspx (カラーピッカーを使用)

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample2.aspx)]

ページには、テキスト ボックスのテキスト ボックスコントロールの真下に表示される ColorPickerExtender コントロールが含まれています。 コントロールは、カラー ピッカー ダイアログを表示するように、txtCardColor コントロールを拡張します。

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>ボタンを使用してカラー ピッカー ダイアログを起動する

カラー ピッカー エクステンダーは、次のプロパティをサポートします。

- PopupButtonId - カラー ピッカー ダイアログを表示するページのボタンの ID。
- ポップアップ位置 - カラー ピッカー ダイアログのターゲット コントロールを基準とした位置。 指定できる値は、絶対値、中心、左下、左下、左、右上、右、左(デフォルトは下左)です。
- サンプル コントロール Id - 選択した色を表示するコントロールの ID。
- 選択された色 - カラー ピッカーによって選択された初期色。

これらのプロパティを使用して、カラー ピッカー ダイアログの表示方法と選択した色の表示方法をカスタマイズできます。 リスト 3 のページでは、これらのプロパティの使用方法を示します。

**リスト 3 - カードボタンを作成します。**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample3.aspx)]

リスト 3 のページには、[色の選択] ボタンが含まれています (図 5 を参照)。 このボタンをクリックすると、テキスト ボックスの上にカラー ピッカー ダイアログが表示されます。 ダイアログボックスから色を選択すると、選択した色が lblSample Label コントロールの背景色として表示されます。

プロパティは、色の選択ボタンを ColorPicker エクステンダーに関連付けるために使用されます。 PopupButtonID プロパティの値を指定すると、ターゲット コントロールにフォーカスがあるときに、カラー ピッカー ダイアログが表示されなくなります。 ダイアログを表示するには、ボタンをクリックする必要があります。

プロパティは、選択した色を表示するコントロールを ColorPicker に関連付けるために使用されます。 ColorPicker は、このコントロールの背景色を現在選択されている色に変更します。

[![ボタンを使用したカラー ピッカー ダイアログの表示](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)

**図 05**: ボタンを使用してカラー ピッカー ダイアログを表示する ([フルサイズの画像を表示する をクリック](using-the-colorpicker-control-extender-cs/_static/image10.png)して)

## <a name="summary"></a>まとめ

このチュートリアルでは、ColorPicker コントロール エクステンダーを使用してポップアップカラー ピッカー ダイアログを表示する方法について説明しました。 まず、フォーカスが TextBox コントロールに移動したときにダイアログを表示する方法を調べました。 次に、ボタンがクリックされたときにカラー ピッカー ダイアログを表示するボタンを作成する方法を学習しました。

> [!div class="step-by-step"]
> [次へ](using-the-colorpicker-control-extender-vb.md)
