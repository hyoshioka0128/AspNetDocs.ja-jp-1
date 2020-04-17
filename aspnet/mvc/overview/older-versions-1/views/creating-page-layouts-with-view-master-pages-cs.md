---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: ビュー マスター ページを使用したページ レイアウトの作成 (C#) |マイクロソフトドキュメント
author: rick-anderson
description: このチュートリアルでは、ビュー マスター ページを利用して、アプリケーション内の複数のページの共通ページ レイアウトを作成する方法を学習します。 あなたは..を使用することができます。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: d313e017d7061ae03e8dea79e611d0cf3838297d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542522"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a>ビュー マスター ページでページ レイアウトを作成する (C#)

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> このチュートリアルでは、ビュー マスター ページを利用して、アプリケーション内の複数のページの共通ページ レイアウトを作成する方法を学習します。 ビュー マスター ページを使用して、2 列のページ レイアウトを定義し、Web アプリケーションのすべてのページに 2 列のレイアウトを使用できます。

## <a name="creating-page-layouts-with-view-master-pages"></a>ビュー マスター ページを使用したページ レイアウトの作成

このチュートリアルでは、ビュー マスター ページを利用して、アプリケーション内の複数のページの共通ページ レイアウトを作成する方法を学習します。 ビュー マスター ページを使用して、2 列のページ レイアウトを定義し、Web アプリケーションのすべてのページに 2 列のレイアウトを使用できます。

また、ビュー マスター ページを利用して、アプリケーション内の複数のページで共通のコンテンツを共有することもできます。 たとえば、Web サイトのロゴ、ナビゲーション リンク、バナー広告をビュー マスター ページに配置できます。 これにより、アプリケーションのすべてのページでこのコンテンツが自動的に表示されます。

このチュートリアルでは、新しいビュー マスター ページを作成し、マスター ページに基づいて新しいビュー コンテンツ ページを作成する方法について説明します。

### <a name="creating-a-view-master-page"></a>ビュー マスター ページの作成

2 列のレイアウトを定義するビュー マスター ページを作成してみましょう。 MVC プロジェクトに新しいビュー マスター ページを追加するには、ビュー\共有フォルダーを右クリックし、メニュー オプション**の追加、新しい項目**を選択し **、MVC ビュー マスター ページ**テンプレート (図 1 参照) を選択します。

[![ビュー マスター ページの追加](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)

**図 01**: ビュー マスター ページの追加 ([フルサイズの画像を表示する をクリック](creating-page-layouts-with-view-master-pages-cs/_static/image3.png)します )

アプリケーションでは、複数のビュー マスター ページを作成できます。 各ビューマスターページは、異なるページレイアウトを定義できます。 たとえば、特定のページに 2 列のレイアウトを設定し、その他のページに 3 列のレイアウトを設定する場合があります。

ビュー マスター ページは、MVC ビューの標準ASP.NET外観が非常に大きく似ています。 ただし、標準ビューとは異なり、ビュー マスター ページには`<asp:ContentPlaceHolder>`1 つ以上のタグが含まれます。 タグ`<contentplaceholder>`は、個々のコンテンツ ページで上書きできるマスター ページの領域をマークするために使用されます。

たとえば、リスト 1 のビュー マスター ページは、2 列のレイアウトを定義します。 これには 2`<contentplaceholder>`つのタグが含まれています。 各`<ContentPlaceHolder>`列に 1 つずつ。

**リスト1 –`Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

リスト 1 のビュー マスター ページの本文`<div>`には、2 つの列に対応する 2 つのタグが含まれています。 カスケード スタイル シート列クラスは、両方`<div>`のタグに適用されます。 このクラスは、マスター ページの先頭で宣言されているスタイル シートで定義されます。 デザイン ビューに切り替えると、ビュー マスター ページのレンダリング方法をプレビューできます。 ソース コード エディターの左下にある [デザイン] タブをクリックします (図 2 参照)。

[![デザイナーでのマスター ページのプレビュー](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)

**図 02**: デザイナーでマスター ページをプレビューする ([フルサイズのイメージを表示する をクリック](creating-page-layouts-with-view-master-pages-cs/_static/image6.png)して )

### <a name="creating-a-view-content-page"></a>ビュー コンテンツ ページの作成

ビュー マスター ページを作成した後、ビュー マスター ページに基づいて 1 つ以上のビュー コンテンツ ページを作成できます。 たとえば、ホーム コントローラーのインデックス ビュー コンテンツ ページを作成するには、ビュー\ホーム フォルダを右クリックし **、[追加]、[新しい項目**] の順に選択し **、MVC ビュー コンテンツ ページ**テンプレートを選択して Index.aspx という名前を入力し、[**追加**] ボタンをクリックします (図 3 参照)。

[![ビュー コンテンツ ページの追加](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)

**図 03**: ビュー コンテンツ ページを追加する ([フルサイズの画像を表示するには [ ] をクリック](creating-page-layouts-with-view-master-pages-cs/_static/image9.png)します )

[追加] ボタンをクリックすると、新しいダイアログが表示され、ビュー のマスター ページを選択してビュー コンテンツ ページに関連付けることができます (図 4 参照)。 前のセクションで作成した Site.master ビュー マスター ページに移動できます。

[![マスター ページの選択](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)

**図 04**: マスタ ページの選択 ([フルサイズの画像を表示する をクリック](creating-page-layouts-with-view-master-pages-cs/_static/image12.png)します )

Site.master マスター ページに基づいて新しいビュー コンテンツ ページを作成すると、リスト 2 でファイルが取得されます。

**リスト2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

このビューには、`<asp:Content>`ビュー マスター ページの各`<asp:ContentPlaceHolder>`タグに対応するタグが含まれています。 各`<asp:Content>`タグには、オーバーライドする特定`<asp:ContentPlaceHolder>`のタグを指す ContentPlaceHolderID 属性が含まれています。

さらに、リスト 2 のコンテンツ ビュー ページには、通常の開始 HTML タグと終了 HTML タグが含まれていないことに注意してください。 たとえば、開始タグと終了`<html>``<head>`タグは含まれません。 通常の開始タグと終了タグはすべて、ビュー マスター ページに含まれます。

ビューコンテンツページに表示するコンテンツは、タグ内に`<asp:Content>`配置する必要があります。 これらのタグの外部に HTML やその他のコンテンツを配置すると、ページを表示しようとするとエラーが発生します。

コンテンツ ビュー ページのマスター`<asp:ContentPlaceHolder>`ページのすべてのタグを上書きする必要はありません。 タグを特定のコンテンツで`<asp:ContentPlaceHolder>`置き換える場合にのみ、タグをオーバーライドする必要があります。

たとえば、リスト 3 で変更したインデックス ビューには`<asp:Content>`、2 つのタグしか含めなされません。 各タグには`<asp:Content>`、いくつかのテキストが含まれています。

**リスト3 –`Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

リスト 3 のビューが要求されると、図 5 のページが表示されます。 ビューは、2 つの列を持つページをレンダリングします。 さらに、ビュー コンテンツ ページのコンテンツがビュー マスター ページのコンテンツとマージされることにも注意してください。

[![インデックス ビューのコンテンツ ページ](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)

**図 05**: インデックス ビューのコンテンツ ページ ([フルサイズの画像を表示する をクリック](creating-page-layouts-with-view-master-pages-cs/_static/image15.png)します )

### <a name="modifying-view-master-page-content"></a>マスター ページの表示コンテンツの変更

ビュー マスター ページを操作するときに直ちに発生する問題の 1 つは、異なるビュー コンテンツ ページが要求されたときにビュー マスター ページのコンテンツを変更する問題です。 たとえば、Web アプリケーションの各ページに固有のタイトルを設定します。 ただし、タイトルはビュー のマスター ページで宣言され、ビュー コンテンツ ページでは宣言されません。 では、各ビュー コンテンツ ページのページ タイトルをどのようにカスタマイズすればよいでしょうか。

ビュー コンテンツ ページで表示されるタイトルを変更するには、2 つの方法があります。 まず、ビュー コンテンツ ページの上部で宣言された`<%@ page %>`ディレクティブの title 属性にページ タイトルを割り当てます。 たとえば、ページタイトル「スーパーグレートWebサイト」をインデックスビューに割り当てる場合、インデックスビューの上部に次のディレクティブを含めることができます。

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

インデックス ビューがブラウザにレンダリングされると、ブラウザのタイトル バーに目的のタイトルが表示されます。

[![ブラウザーのタイトル バー](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)

title 属性が機能するためにマスター ビュー ページが満たす必要がある重要な要件が 1 つあります。 ビュー マスター ページには、`<head runat="server">`ヘッダーの通常`<head>`のタグではなく、タグが含まれている必要があります。 タグに`<head>`runat="server" 属性が含まれていない場合、タイトルは表示されません。 既定のビュー マスター ページには`<head runat="server">`、必要なタグが含まれています。

個々のビュー コンテンツ ページからマスター ページのコンテンツを変更する別の方法として、`<asp:ContentPlaceHolder>`タグで変更する領域をラップします。 たとえば、マスター ビュー ページによってレンダリングされるタイトルだけでなく、メタ タグも変更するとします。 リスト 4 のマスター ビュー`<asp:ContentPlaceHolder>`ページには、`<head>`そのタグ内にタグが含まれています。

**リスト4 –`Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

リスト 4`<asp:ContentPlaceHolder>`のタグには、デフォルトのタイトルとデフォルトのメタタグのデフォルトコンテンツが含まれていることに注意してください。 個々のビューコンテンツページでこの`<asp:ContentPlaceHolder>`タグを上書きしない場合は、デフォルトのコンテンツが表示されます。

リスト 5 のコンテンツ ビュー ページ`<asp:ContentPlaceHolder>`は、カスタム タイトルとカスタム メタ タグを表示するためにタグを上書きします。

**リスト5 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a>まとめ

このチュートリアルでは、マスター ページの表示とコンテンツ ページの表示に関する基本的な概要を説明しました。 新しいビュー マスター ページを作成し、そのマスター ページに基づいてコンテンツ ページを作成する方法について説明しました。 また、特定のビュー コンテンツ ページからビュー マスター ページのコンテンツを変更する方法についても説明しました。

> [!div class="step-by-step"]
> [前へ](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [次へ](passing-data-to-view-master-pages-cs.md)
