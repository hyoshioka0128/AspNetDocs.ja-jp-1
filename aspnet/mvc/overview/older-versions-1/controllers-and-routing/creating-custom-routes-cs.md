---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: カスタム ルートの作成 (C#) |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NET MVC アプリケーションにカスタム ルートを追加する方法について説明します。 このチュートリアルでは、Global.asax ファイルの既定のルート テーブルを変更する方法について説明します。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: b66ccc5e0cd4f6d7e5884394c2b7555b76382d3d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542756"
---
# <a name="creating-custom-routes-c"></a>カスタム ルートを作成する (C#)

[マイクロソフト](https://github.com/microsoft)

> ASP.NET MVC アプリケーションにカスタム ルートを追加する方法について説明します。 このチュートリアルでは、Global.asax ファイルの既定のルート テーブルを変更する方法について説明します。

このチュートリアルでは、ASP.NET MVC アプリケーションにカスタム ルートを追加する方法について説明します。 Global.asax ファイルの既定のルート テーブルをカスタム ルートで変更する方法を学習します。

多くの単純なASP.NET MVC アプリケーションでは、既定のルート テーブルは正常に動作します。 ただし、特殊なルーティングニーズがある場合もあります。 その場合は、カスタム ルートを作成できます。

たとえば、ブログ アプリケーションを作成しているとします。 次のような着信要求を処理する必要があります。

/アーカイブ/12-25-2009

ユーザーがこの要求を入力すると、2009/12/25 に対応するブログエントリを返します。 このタイプの要求を処理するには、カスタム ルートを作成する必要があります。

リスト 1 の Global.asax ファイルには、/Archive/*エントリ日付*のような要求を処理する Blog という名前の新しいカスタム ルートが含まれています。

**リスト 1 - グローバル.asax (カスタム ルートを使用)**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

ルート テーブルに追加するルートの順序は重要です。 新しいカスタムのブログルートは、既存のデフォルトルートの前に追加されます。 順序を逆にした場合、既定のルートは、カスタム ルートの代わりに常に呼び出されます。

カスタムのブログルートは、/Archive/ で始まるすべてのリクエストと一致します。 したがって、次のすべての URL と一致します。

- /アーカイブ/12-25-2009

- /アーカイブ/10-6-2004

- /アーカイブ/リンゴ

カスタム ルートは、受信した要求を Archive という名前のコントローラにマップし、Entry() アクションを呼び出します。 Entry() メソッドが呼び出されると、エントリの日付は entryDate という名前のパラメーターとして渡されます。

リスト 2 のコントローラーでブログカスタム ルートを使用できます。

**リスト 2 - ArchiveController.cs**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

リスト 2 の Entry() メソッドは、DateTime 型のパラメーターを受け取ります。 MVC フレームワークは、入力日付を URL から DateTime 値に自動的に変換するのに十分なスマートさです。 URL からの入力日付パラメータを DateTime に変換できない場合は、エラーが発生します (図 1 参照)。

**図1 - パラメータ変換によるエラー**

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

**図 01**: 変換パラメータからのエラー ([フルサイズの画像を表示する をクリックします](creating-custom-routes-cs/_static/image2.png))

## <a name="summary"></a>まとめ

このチュートリアルの目的は、カスタム ルートを作成する方法を示すものでした。 ブログエントリを表す Global.asax ファイルのルート テーブルにカスタム ルートを追加する方法を学習しました。 ブログ エントリの要求を ArchiveController という名前のコントローラと Entry() という名前のコントローラ アクションにマップする方法について説明しました。

> [!div class="step-by-step"]
> [前へ](aspnet-mvc-controllers-overview-cs.md)
> [次へ](creating-a-route-constraint-cs.md)
