---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: カスタム HTML ヘルパー (VB) を作成する |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示します。 HTMLヘルパーを利用して.
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 52f16bf666edc9f1c95c01faf004e303fcb6a0b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542509"
---
# <a name="creating-custom-html-helpers-vb"></a>カスタム HTML ヘルパーの作成 (VB)

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示します。 HTML ヘルパーを利用することで、標準 HTML ページを作成するために実行する必要がある HTML タグの手間のかかる入力を減らすことができます。

このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示します。 HTML ヘルパーを利用することで、標準 HTML ページを作成するために実行する必要がある HTML タグの手間のかかる入力を減らすことができます。

このチュートリアルの最初の部分では、ASP.NET MVC フレームワークに含まれている既存の HTML ヘルパーのいくつかを説明します。 次に、カスタム HTML ヘルパーを作成する 2 つのメソッドについて説明します: 共有メソッドを作成し、拡張メソッドを作成することによってカスタム HTML ヘルパーを作成する方法について説明します。

## <a name="understanding-html-helpers"></a>HTML ヘルパーについて

HTML ヘルパーは、文字列を返すメソッドにすぎません。 文字列は、必要な任意の種類のコンテンツを表すことができます。 たとえば、HTML ヘルパーを使用して、HTML`<input>`やタグなどの標準 HTML`<img>`タグをレンダリングできます。 また、HTML ヘルパーを使用して、タブ ストリップやデータベース データの HTML テーブルなど、より複雑なコンテンツをレンダリングすることもできます。

ASP.NET MVC フレームワークには、次の標準 HTML ヘルパーのセットが含まれています (完全な一覧ではありません)。

- アクションリンク()
- を開始します。
- チェックボックス()
- をクリックします。
- をクリックします。
- 隠された()
- リストボックス()
- パスワード()
- ラジオボタン()
- テキストエリア()
- テキストボックス()

たとえば、リスト 1 のフォームを考えてみましょう。 このフォームは、2 つの標準 HTML ヘルパーの助けを借りてレンダリングされます (図 1 を参照)。 このフォームでは、 `Html.BeginForm()` `Html.TextBox()`および ヘルパー メソッドを使用します。

[![HTML ヘルパーで表示されるページ](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)

**図 01**: HTML ヘルパーで表示されるページ ([フルサイズの画像を表示する をクリック](creating-custom-html-helpers-vb/_static/image3.png)して )

**リスト1 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

ヘルパー`Html.BeginForm()`メソッドは、開始 HTML タグと終了`<form>`HTML タグを作成するために使用されます。 `Html.BeginForm()`メソッドが using ステートメント内で呼び出されることに注意してください。 using ステートメントは、タグ`<form>`が using ブロックの最後で閉じられることを保証します。

必要に応じて、使用ブロックを作成する代わりに、Html.EndForm() ヘルパー メソッドを呼び`<form>`出してタグを閉じることもできます。 最も直感的に見える開始タグと終了`<form>`タグを作成するには、どちらの方法を使用しても問題ありません。

ヘルパー`Html.TextBox()`メソッドは、リスト 1 で`<input>`HTML タグをレンダリングするために使用されます。 ブラウザで [ソースの表示] を選択すると、リスト 2 に HTML ソースが表示されます。 ソースに標準の HTML タグが含まれていることに注意してください。

> [!IMPORTANT]
> HTML ヘルパー`Html.TextBox()`は`<%= %>``<% %>`タグではなくタグでレンダリングされます。 等号を含めなければ、ブラウザには何も表示されません。

mvc フレームワークASP.NETには、少数のヘルパーセットが含まれています。 ほとんどの場合、カスタム HTML ヘルパーを使用して MVC フレームワークを拡張する必要があります。 このチュートリアルの残りの部分では、カスタム HTML ヘルパーを作成する 2 つの方法について説明します。

**リスト2 –`Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a>共有メソッドを使用した HTML ヘルパーの作成

新しい HTML ヘルパーを作成する最も簡単な方法は、文字列を返す共有メソッドを作成することです。 たとえば、HTML`<label>`タグを表示する新しい HTML ヘルパーを作成するとします。 リスト 2 のクラスを使用して`<label>`、 をレンダリングできます。

**リスト2 –`Helpers\LabelHelper.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

リスト 2 のクラスについて特別なことは何もありません。 この`Label()`メソッドは、単に文字列を返します。

リスト 3 の変更されたインデックス`LabelHelper`ビューでは、`<label>`を使用して HTML タグをレンダリングします。 ビューには、Application1.Helpers 名前空間をインポートする`<%@ imports %>`ディレクティブが含まれていることに注意してください。

**リスト2 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>拡張メソッドを使用した HTML ヘルパーの作成

ASP.NET MVC フレームワークに含まれる標準の HTML ヘルパーと同じように動作する HTML ヘルパーを作成する場合は、拡張メソッドを作成する必要があります。 拡張メソッドを使用すると、既存のクラスに新しいメソッドを追加できます。 HTML ヘルパー メソッドを作成するときは、ビューの`HtmlHelper`Html プロパティで表されるクラスに新しいメソッドを追加します。

リスト 3 の Visual Basic モジュールは`Label()`、クラス`HtmlHelper`に名前の拡張メソッドを追加します。 このモジュールについて注意すべき点がいくつかあります。 まず、モジュールが属性で装飾されていることに`<Extension()>`注目してください。 この属性を使用するには、名前空間をインポートする必要`System.Runtime.CompilerServices`があります。

次に、メソッドの最初のパラメーターが`Label()`クラスを表`HtmlHelper`していることに注目してください。 拡張メソッドの最初のパラメーターは、拡張メソッドが拡張するクラスを示します。

**リスト3 –`Helpers\LabelExtensions.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

拡張メソッドを作成し、アプリケーションを正常にビルドすると、クラスの他のすべてのメソッドと同様に、拡張メソッドが Visual Studio Intellisense に表示されます (図 2 参照)。 唯一の違いは、拡張メソッドが、その横に特別な記号 (下向き矢印のアイコン) が付いた表示です。

[![拡張メソッドを使用する](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)

**図 02**: Html.Label() 拡張メソッドを使用して ([フルサイズの画像を表示する をクリック](creating-custom-html-helpers-vb/_static/image6.png)します)

リスト 4 の変更されたインデックス ビューでは、Html.Label() 拡張メソッドを&lt;使用&gt;して、すべてのラベル タグを表示します。

**リスト4 –`Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a>まとめ

このチュートリアルでは、カスタム HTML ヘルパーを作成する 2 つの方法を学習しました。 まず、文字列を返す共有メソッドを`Label()`作成してカスタム HTML ヘルパーを作成する方法を学習しました。 次に、クラスに拡張メソッドを作成`Label()`してカスタム HTML ヘルパー メソッドを作成`HtmlHelper`する方法を学習しました。

このチュートリアルでは、非常に単純な HTML ヘルパー メソッドの構築に重点を置きました。 HTML ヘルパーは、必要に応じて複雑になる可能性があることを認識します。 ツリー ビュー、メニュー、データベース データのテーブルなどのリッチ コンテンツを表示する HTML ヘルパーを作成できます。

> [!div class="step-by-step"]
> [前へ](asp-net-mvc-views-overview-vb.md)
> [次へ](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
