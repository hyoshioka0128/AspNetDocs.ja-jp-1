---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: カスタム HTML ヘルパーの作成 (C#) |マイクロソフトドキュメント
author: microsoft
description: このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示します。 HTMLヘルパーを利用して.
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a2e5a5b42aa5bf267a42fef2fcad7022001ce6f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675338"
---
# <a name="creating-custom-html-helpers-c"></a>カスタム HTML ヘルパーの作成 (C#)

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示します。 HTML ヘルパーを利用することで、標準 HTML ページを作成するために実行する必要がある HTML タグの手間のかかる入力を減らすことができます。

このチュートリアルの目的は、MVC ビュー内で使用できるカスタム HTML ヘルパーを作成する方法を示します。 HTML ヘルパーを利用することで、標準 HTML ページを作成するために実行する必要がある HTML タグの手間のかかる入力を減らすことができます。

このチュートリアルの最初の部分では、ASP.NET MVC フレームワークに含まれている既存の HTML ヘルパーのいくつかを説明します。 次に、カスタム HTML ヘルパーを作成する 2 つのメソッドについて説明します: 静的メソッドを作成し、拡張メソッドを作成することによってカスタム HTML ヘルパーを作成する方法について説明します。

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

たとえば、リスト 1 のフォームを考えてみましょう。 このフォームは、2 つの標準 HTML ヘルパーの助けを借りてレンダリングされます (図 1 を参照)。 このフォームでは、 `Html.BeginForm()` `Html.TextBox()`および Helper メソッドを使用して、単純な HTML フォームをレンダリングします。

[![HTML ヘルパーで表示されるページ](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**図 01**: HTML ヘルパーで表示されるページ ([フルサイズの画像を表示する をクリック](creating-custom-html-helpers-cs/_static/image3.png)して )

**リスト1 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

Html.BeginForm() ヘルパー メソッドは、HTML`<form>`タグの開始タグと終了タグを作成するために使用されます。 `Html.BeginForm()`メソッドが using ステートメント内で呼び出されることに注意してください。 using ステートメントは、タグ`<form>`が using ブロックの最後で閉じられることを保証します。

必要に応じて、使用ブロックを作成する代わりに、Html.EndForm() ヘルパー メソッドを呼び`<form>`出してタグを閉じることもできます。 最も直感的に見える開始タグと終了`<form>`タグを作成するには、どちらの方法を使用しても問題ありません。

ヘルパー`Html.TextBox()`メソッドは、リスト 1 で`<input>`HTML タグをレンダリングするために使用されます。 ブラウザで [ソースの表示] を選択すると、リスト 2 に HTML ソースが表示されます。 ソースに標準の HTML タグが含まれていることに注意してください。

> [!IMPORTANT]
> HTML ヘルパー`Html.TextBox()`は`<%= %>``<% %>`タグではなくタグでレンダリングされます。 等号を含めなければ、ブラウザには何も表示されません。

mvc フレームワークASP.NETには、少数のヘルパーセットが含まれています。 ほとんどの場合、カスタム HTML ヘルパーを使用して MVC フレームワークを拡張する必要があります。 このチュートリアルの残りの部分では、カスタム HTML ヘルパーを作成する 2 つの方法について説明します。

**リスト2 –`Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>静的メソッドを使用した HTML ヘルパーの作成

新しい HTML ヘルパーを作成する最も簡単な方法は、文字列を返す静的メソッドを作成することです。 たとえば、HTML`<label>`タグを表示する新しい HTML ヘルパーを作成するとします。 リスト 2 のクラスを使用して`<label>`、 をレンダリングできます。

**リスト2 –`Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

リスト 2 のクラスについて特別なことは何もありません。 この`Label()`メソッドは、単に文字列を返します。

リスト 3 の変更されたインデックス`LabelHelper`ビューでは、`<label>`を使用して HTML タグをレンダリングします。 ビューには、名前空間を`<%@ imports %>`インポートするディレクティブが含まれていること`Application1.Helpers`に注意してください。

**リスト2 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>拡張メソッドを使用した HTML ヘルパーの作成

ASP.NET MVC フレームワークに含まれる標準の HTML ヘルパーと同じように動作する HTML ヘルパーを作成する場合は、拡張メソッドを作成する必要があります。 拡張メソッドを使用すると、既存のクラスに新しいメソッドを追加できます。 HTML ヘルパー メソッドを作成するときは、ビューの Html プロパティで表される HtmlHelper クラスに新しいメソッドを追加します。

リスト 3 のクラスは、 という名前`HtmlHelper``Label()`のクラスに拡張メソッドを追加します。 このクラスについて注意すべき点がいくつかあります。 まず、クラスが静的クラスであることに注意してください。 静的クラスを使用して拡張メソッドを定義する必要があります。

次に、`Label()`メソッドの最初のパラメータの前にキーワード`this`が付いていることに注目してください。 拡張メソッドの最初のパラメーターは、拡張メソッドが拡張するクラスを示します。

**リスト3 –`Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

拡張メソッドを作成し、アプリケーションを正常にビルドすると、クラスの他のすべてのメソッドと同様に、拡張メソッドが Visual Studio Intellisense に表示されます (図 2 参照)。 唯一の違いは、拡張メソッドが、その横に特別な記号 (下向き矢印のアイコン) が付いた表示です。

[![拡張メソッドを使用する](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**図 02**: Html.Label() 拡張メソッドを使用して ([フルサイズの画像を表示する をクリック](creating-custom-html-helpers-cs/_static/image6.png)します)

リスト 4 の変更されたインデックス ビューでは、Html.Label() 拡張メソッドを`<label>`使用して、すべてのタグを表示します。

**リスト4 –`Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>まとめ

このチュートリアルでは、カスタム HTML ヘルパーを作成する 2 つの方法を学習しました。 まず、文字列を返す静的メソッドを`Label()`作成してカスタム HTML ヘルパーを作成する方法を学習しました。 次に、クラスに拡張メソッドを作成`Label()`してカスタム HTML ヘルパー メソッドを作成`HtmlHelper`する方法を学習しました。

このチュートリアルでは、非常に単純な HTML ヘルパー メソッドの構築に重点を置きました。 HTML ヘルパーは、必要に応じて複雑になる可能性があることを認識します。 ツリー ビュー、メニュー、データベース データのテーブルなどのリッチ コンテンツを表示する HTML ヘルパーを作成できます。

> [!div class="step-by-step"]
> [前へ](asp-net-mvc-views-overview-cs.md)
> [次へ](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
