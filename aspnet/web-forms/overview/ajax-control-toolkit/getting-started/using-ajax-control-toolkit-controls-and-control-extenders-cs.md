---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: AJAX コントロール ツールキット コントロールとコントロール エクステンダの使用 (C#) |マイクロソフトドキュメント
author: rick-anderson
description: AJAX コントロール ツールキット コントロールとエクステンダーをASP.NET ページに追加する方法について説明します。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 5729db63f831b74ca37c573791c53c39265c1f39
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543718"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>AJAX Control Toolkit のコントロールとコントロール エクステンダーを使用する (C#)

[マイクロソフト](https://github.com/microsoft)

> AJAX コントロール ツールキット コントロールとエクステンダーをASP.NET ページに追加する方法について説明します。

AJAX コントロール ツールキットには、コントロールとコントロール エクステンダのセットが含まれています。 この簡単なチュートリアルでは、コントロールとコントロール エクステンダの両方をASP.NET ページに追加する方法について説明します。

> [!NOTE] 
> 
> AJAX コントロール ツールキットをインストールし、AJAX コントロール ツールキットを Visual Studio/Visual Web 開発者ツールボックスに追加する手順については[、「AJAX コントロール ツールキットの概要](get-started-with-the-ajax-control-toolkit-cs.md)」のチュートリアルを参照してください。

## <a name="using-ajax-control-toolkit-controls"></a>AJAX コントロール ツールキット コントロールの使用

AJAX コントロール ツールキット コントロールは、通常のASP.NET コントロールと同じように機能します。 ツールボックスからASP.NETページにコントロールをドラッグできます。 デザイン ビューまたはソース ビューで、ページにコントロールを追加できます。

AJAX コントロール ツールキットのコントロールを使用する場合、1 つの特別な要件があります。 ページには、スクリプト マネージャー コントロールが含まれている必要があります。 コントロールは、AJAX コントロール ツールキット コントロールに必要なすべての必要な JavaScript を含める役割を担います。

たとえば、AJAX コントロール ツールキット タブには、エディター コントロールという名前のコントロールが含まれています。 このコントロールは、リッチ HTML エディターを表示します。 エディター コントロールをページに追加するには、次の手順を実行します。

1. ShowEditor.aspx という名前の新しいASP.NET ページを作成します。
2. ツールボックスの [AJAX 拡張] タブの下にある ScriptManager コントロールを選択し、コントロールをページにドラッグします。
3. ツールボックスの [AJAX コントロール ツールキット] タブの下にある [エディター] コントロールを選択し、コントロールをページにドラッグします (図 1 参照)。 デザイナーは図 2 のようになります。
4. メニュー オプションの **[デバッグ]、[デバッグの開始] を**選択するか、または F5 キーを押して、Web サイトを実行します。
5. 図 3 にページが表示されます。

[![HTML エディター コントロールの選択](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**図 01**: HTML エディタ コントロールの選択 ([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))

[![スクリプト マネージャーと編集コントロールを使用したビジュアル スタジオ デザイナー](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**図 02**: スクリプト マネージャーと編集コントロールを持つ Visual Studio デザイナー ([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png)します )

[![表示エディター.aspx ページ](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**図 03**: DisplayEditor.aspx ページ ([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png)します )

## <a name="using-ajax-control-toolkit-control-extenders"></a>AJAX コントロール ツールキット コントロール エクステンダの使用

AJAX コントロール ツールキットには、コントロール エクステンダも含まれています。 名前が示すように、コントロール エクステンダは既存のコントロールの機能を拡張します。 たとえば、ConfirmButton コントロール エクステンダーは、標準のASP.NET ボタン コントロールを拡張します。 エクステンダは、ボタン コントロールの動作を変更して、ボタンをクリックすると確認ダイアログボックスが表示されるようにします。

コントロール エクステンダは、AJAX コントロール ツールキット コントロールと同様に、ScriptManager コントロールを必要とします。 ページでコントロール エクステンダーを使用する前に、ページに ScriptManager コントロールを追加する必要があります。

確認ボタン コントロール エクステンダーを使用するには、次の手順に従います。

1. という名前の新しいASP.NET ページを作成します。
2. コントロールをページにドラッグして、ページに ScriptManager コントロールを追加する、 AJAX 拡張機能タブ。
3. ツールボックスの [標準] タブの下にある [ボタン] をデザイナー画面にドラッグして、標準の Button コントロールをページに追加します。
4. エクス**テンダーの追加**タスク オプションをクリックします (図 4 を参照)。
5. [エクステンダの選択] ダイアログで、[ボタンエクステンダーの確認] (図 5 を参照) を選択し、[OK] ボタンをクリックします。
6. デザイナーでボタン コントロールを選択し、プロパティ ウィンドウでエクステン\_ダー、ボタン 1 確認ボタンエクステンダー ノードを展開します (図 6 を参照)。 値を *[本当に?* ] プロパティに代入します。
7. メニュー オプション[**デバッグ]、[デバッグの開始]、** または [F5 キー] をクリックして、ページを実行します。

[![エクステンダーの追加タスク オプション](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**図 04**: エクステンダーの追加タスク オプション ([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))

[![確認ボタン コントロール エクステンダーの選択](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**図 05**: ConfirmButton コントロール エクステンダの選択 ([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))

[![プロパティを設定する](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**図 06**: ConfirmButton プロパティの設定 ([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png)します)

ページが開くと、ボタンが表示されます。 ボタンをクリックすると、図 7 の確認ダイアログが表示されます。

[![確認ダイアログの表示](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**図07**: 確認ダイアログを表示する([フルサイズの画像を表示する をクリック](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))

通常は、コントロール エクステンダをページにドラッグしないことに注意してください。 代わりに、**エクステンダーの追加**タスク オプションを使用して、ページに既に追加したコントロールにエクステンダを追加します。 さらに、拡張するコントロールのプロパティ シートを開いて、コントロール エクステンダープロパティを設定します。

複数のコントロール エクステンダによって、1 つのASP.NET コントロールを拡張できます。 拡張されるコントロールのプロパティ シートには、コントロールに関連付けられているすべてのコントロール エクステンダが表示されます。

> [!div class="step-by-step"]
> [前へ](get-started-with-the-ajax-control-toolkit-cs.md)
> [次へ](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
