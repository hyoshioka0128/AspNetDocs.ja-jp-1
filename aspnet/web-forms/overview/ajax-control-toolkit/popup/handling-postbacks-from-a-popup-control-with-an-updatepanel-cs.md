---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: ポップアップコントロールからのポストバックを UpdatePanel (C#) で処理するMicrosoft Docs
author: wenz
description: AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 特別な注意が必要です...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 8b9e58d68b3d6c5d01ceaba6c01653e9574b541b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496666"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a>ポップアップ コントロールからポストバックを処理する (UpdatePanel あり) (C#)

[Christian Wenz](https://github.com/wenz)別

[コードのダウンロード](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip)または[PDF のダウンロード](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)

> AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 このようなポップアップ内でポストバックが発生した場合は、特別な注意が必要です。

## <a name="overview"></a>概要

AJAX Control Toolkit の PopupControl extender は、他のコントロールがアクティブになったときにポップアップをトリガーする簡単な方法を提供します。 このようなポップアップ内でポストバックが発生した場合は、特別な注意が必要です。

## <a name="steps"></a>手順

ポストバックで `PopupControl` を使用すると、ポストバックによるページの更新が `UpdatePanel` によって妨げられる可能性があります。 次のマークアップは、いくつかの重要な要素を定義します。

- ASP.NET AJAX Control Toolkit が動作するように `ScriptManager` コントロール
- ポップアップをトリガーする2つの `TextBox` コントロール
- ポップアップとして機能する `Panel` コントロール
- パネル内では、`Calendar` コントロールが `UpdatePanel` コントロール内に埋め込まれます。
- パネルをテキストボックスに割り当てる2つの `PopupControlExtender` コントロール

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

`Calendar` コントロールの `OnSelectionChanged` 属性が設定されていることに注意してください。 そのため、ユーザーがカレンダー内の日付を選択すると、ポストバックが発生し、サーバー側のメソッド `c1_SelectionChanged()` が実行されます。 そのメソッド内で、現在の日付を取得し、テキストボックスに書き戻す必要があります。

の構文は次のとおりです。最初に、ページの `PopupControlExtender` のプロキシオブジェクトを生成する必要があります。 ASP.NET AJAX Control Toolkit には、`GetProxyForCurrentPopup()` メソッドが用意されています。 このメソッドが返すオブジェクトは、`Commit()` メソッドをサポートしています。このメソッドは、ポップアップをトリガーしたコントロール (メソッド呼び出しをトリガーしたコントロールではない) に値を返します。 次のコードでは、`Commit()` メソッドの引数として選択された日付を提供しています。これにより、コードは、選択した日付をテキストボックスに書き戻します。

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

これで、カレンダーの日付をクリックするたびに、選択した日付が関連するテキストボックスに表示され、多くの web サイトで現在検出できる日付の選択コントロールが作成されます。

[ユーザーがテキストボックスをクリックしたときにカレンダーが表示される ![](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)

ユーザーがテキストボックスをクリックするとカレンダーが表示されます ([クリックすると、フルサイズの画像が表示](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png)されます)

[日付をクリック ![と、テキストボックスに挿入されます。](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)

日付をクリックするとテキストボックスに挿入されます ([クリックすると、フルサイズの画像が表示](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png)されます)

> [!div class="step-by-step"]
> [前へ](using-multiple-popup-controls-cs.md)
> [次へ](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
