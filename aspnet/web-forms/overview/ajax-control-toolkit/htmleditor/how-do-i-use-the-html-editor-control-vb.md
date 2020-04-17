---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: HTML エディタ コントロールを使用する方法 (VB) |マイクロソフトドキュメント
author: rick-anderson
description: HTMLEditor は、ツールバーのボタンを使用して HTML コンテンツを簡単に作成および編集できる AJAX コントロールASP.NETです。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: bba42b4b6ff130b209b92c1608bc37f2f574c19c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542834"
---
# <a name="how-do-i-use-the-html-editor-control-vb"></a>HTML エディタ コントロールを使用する方法 (VB)

[マイクロソフト](https://github.com/microsoft)

> HTMLEditor は、ツールバーのボタンを使用して HTML コンテンツを簡単に作成および編集できる AJAX コントロールASP.NETです。

このチュートリアルの目的は、AJAX コントロール ツールキットに含まれている HTML エディター コントロールの概要を提供することです。 HTML エディタには、フォント サイズの変更、フォントの選択、背景色の変更、前景色の変更、リンクの追加、画像の追加、テキストの配置の変更、切り取り、コピー、および貼り付け操作を行うためのオプションがあります (図 1 参照)。

[![HTML エディタ](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)

**図 01**: HTML エディタ ([フルサイズの画像を表示する をクリック](how-do-i-use-the-html-editor-control-vb/_static/image2.png))

HTML エディタを使用すると、デザイン モードを使用してコンテンツを入力したり、HTML を直接入力したりできます。 HTML コンテンツをプレビューするオプションも提供されています (図 2 参照)。

[![デザイン、HTML、プレビューボタン](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)

**図 02**: デザイン、HTML、およびプレビュー ボタン ([フルサイズの画像を表示する をクリック](how-do-i-use-the-html-editor-control-vb/_static/image4.png))

このチュートリアルでは、HTML エディターを表示する方法、HTML エディターに表示されるツール バー ボタンをカスタマイズする方法、およびクロスサイト スクリプティング攻撃を回避する方法について説明します。

## <a name="displaying-the-html-editor"></a>HTML エディタの表示

ASP.NETページで HTML エディタを使用する前に、まず ScriptManager コントロールをページに追加する必要があります。 コントロールは、Visual Studio/Visual Web 開発者エクスプレス ツールボックスの [AJAX 拡張機能] タブの下にあります。

ページ上の他のコントロールの前に、ページの上部に ScriptManager コントロールを配置する必要があります。 たとえば、開いているサーバー側&lt;フォーム&gt;タグのすぐ下に配置できます。

HTML エディター コントロールは、ツールボックスに AJAX コントロール ツールキット コントロールの残りの部分があります。 Editor コントロールと呼ばれます (図 3 参照)。

[![HTML エディター コントロール](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)

**図 03**: HTML エディタ コントロール ([フルサイズの画像を表示する をクリック](how-do-i-use-the-html-editor-control-vb/_static/image6.png)します )

HTML エディタをページにドラッグした後、プロパティ シートでプロパティを設定できます。 たとえば、通常は幅と高さのプロパティを設定します。 リスト 1 には、HTML エディターを含む ASP.NET ページのソースが含まれています。

**リスト 1 - シンプルエディター.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

リスト 1 のページには、HTML エディター コントロール、ボタン コントロール、およびリテラル コントロールが含まれています。 ボタンをクリックすると、HTML エディターの内容が Literal コントロールに表示されます (図 4 を参照)。

[![HTML エディタを使用したフォームの送信](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)

**図 04**: HTML エディタを使用してフォームを送信する ([フルサイズの画像を表示するには、](how-do-i-use-the-html-editor-control-vb/_static/image8.png)

HTML エディタのコンテンツ プロパティは、HTML エディタに入力された HTML コンテンツを取得するために使用されます。 この HTML コンテンツには JavaScript が含まれている可能性があることに注意してください。 次のセクションでは、JavaScript インジェクション攻撃を防ぐ方法について説明します。

## <a name="customizing-the-html-editor-toolbar"></a>HTML エディタ ツールバーのカスタマイズ

エディターに表示するボタンを正確にカスタマイズできます。 たとえば、HTML タブを削除して、HTML エディターを HTML モードに切り替えないようにすることができます。 または、フォント サイズのドロップダウン リストを削除して、ユーザーがフォーラム メッセージの投稿に過度に大きなテキストを作成できないようにすることができます (図 5 参照)。

[![カスタマイズされた HTML エディタ](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)

**図 05**: カスタマイズされた HTML エディタ ([フルサイズの画像を表示する をクリック](how-do-i-use-the-html-editor-control-vb/_static/image10.png))

ツール バーのボタンをカスタマイズするには、基本エディタ クラスから新しい HTML エディタを派生します。 たとえば、リスト 2 のカスタム エディターには、太字と斜体のツールバー ボタンのみが含まれています。 その他のツールバー ボタンはすべて削除されました。 さらに、エディタの下部から HTML タブが削除されました (ただし、[デザイン] タブと [プレビュー] タブは表示されません)。

**リスト 2\_- アプリ コード\カスタム エディター.vb**

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

クラスが自動的にコンパイルされるように、リスト 2\_のクラスを App Code フォルダーに追加する必要があります。 アプリ\_コードフォルダがウェブサイトに存在しない場合は、フォルダを追加するだけです。

カスタム エディターを作成した後、通常の HTML エディターを追加するのと同じ方法で、ASP.NETページに追加できます (リスト 3 を参照)。

**リスト 3 - カスタムエディター.aspx を表示します。**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>クロスサイト スクリプティング (XSS) 攻撃を回避する

ユーザーからの入力を受け入れ、その入力を Web サイトに再表示すると、Web サイトをクロスサイト スクリプティング (XSS) 攻撃に対して開く可能性があります。 理論的には、悪意のあるハッカーは、入力が再表示されたときに実行されるJavaScriptコードを送信する可能性があります。 JavaScriptは、ユーザーのパスワードやその他の機密情報を盗むために使用することができます。

通常、Web ページに表示する前に、ユーザーから取得した入力を HTML エンコードすることで XSS 攻撃を打ち破ることができます。 しかし、HTML エディタの出力を HTML エンコードすると、&lt;スクリプト&gt;タグをエンコードするだけでなく、すべての HTML タグもエンコードされます。 つまり、フォントの種類、フォント サイズ、背景色などの書式設定がすべて失われます。

パスワード、クレジット カード番号、社会保障番号などの機密情報をユーザーから収集する場合は、HTML エディタを使用してユーザーから取得したエンコードされていないコンテンツを表示しないでください。 HTML エディタは、HTML コンテンツを再表示しない場合や、信頼できるユーザーが WEB サイトに HTML コンテンツを送信している場合にのみ使用してください。

たとえば、ブログ アプリケーションを作成しているとします。 このような場合は、ブログの投稿を作成するときに HTML エディターを使用する意味があります。 ブログ投稿を投稿するのはあなただけであり、おそらく、悪意のあるJavaScriptを提出しないように自分を信頼することができます。 ただし、匿名ユーザーがコメントを投稿できるようにする場合は、HTML エディタを使用しても意味がありません。 ユーザーがパスワードなどの機密情報を送信する場合は、特に注意が必要です。 悪意のあるユーザーが、パスワードを盗むのに適した JavaScript を含むコメントを投稿する可能性があります。

## <a name="summary"></a>まとめ

このチュートリアルでは、AJAX コントロール ツールキットに含まれている HTML エディター コントロールの簡単な概要を提供しました。 HTML エディタを使用して、ユーザーからのリッチ コンテンツを受け入れ、コンテンツをサーバーに送信する方法を学習しました。 HTML エディタで表示されるツール バー ボタンをカスタマイズする方法についても説明しました。 最後に、HTML エディタを使用して悪意のある入力を受け入れるときにクロスサイト スクリプティング攻撃を回避する方法を学習しました。

> [!div class="step-by-step"]
> [前へ](how-do-i-use-the-html-editor-control-cs.md)
