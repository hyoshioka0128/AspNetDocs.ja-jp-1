---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: キャッシュされたページへの動的コンテンツの追加 (VB) |マイクロソフトドキュメント
author: rick-anderson
description: 同じページで動的コンテンツとキャッシュコンテンツを混在する方法について説明します。 ポストキャッシュ置換を使用すると、バナー広告などの動的コンテンツを表示できます。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 1ed022fc560becbd21722b94f2428cf7b32f2635
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542262"
---
# <a name="adding-dynamic-content-to-a-cached-page-vb"></a>キャッシュされたページに動的コンテンツを追加する (VB)

[マイクロソフト](https://github.com/microsoft)

> 同じページで動的コンテンツとキャッシュコンテンツを混在する方法について説明します。 ポストキャッシュ置換を使用すると、出力キャッシュされたページ内にバナー広告やニュースアイテムなどの動的コンテンツを表示できます。

出力キャッシュを利用することで、ASP.NET MVC アプリケーションのパフォーマンスを大幅に向上させることができます。 ページが要求されるたびにページを再生成する代わりに、ページを 1 回だけ生成して、複数のユーザーのメモリにキャッシュできます。

しかし、問題があります。 ページに動的コンテンツを表示する必要がある場合はどうでしょうか。 たとえば、ページにバナー広告を表示するとします。 すべてのユーザーがまったく同じ広告を表示するように、バナー広告をキャッシュしたくない。 あなたはそのようにお金を稼ぐことはありません!

幸いなことに、簡単な解決策があります。 *ポストキャッシュ置換*と呼ばれるASP.NETフレームワークの機能を利用できます。 キャッシュ後置換を使用すると、メモリにキャッシュされたページの動的コンテンツを置き換えることができます。

通常、OutputCache&lt;&gt;属性を使用してページを出力すると、ページはサーバーとクライアント (Web ブラウザー) の両方にキャッシュされます。 キャッシュ後置換を使用すると、ページはサーバー上でのみキャッシュされます。

#### <a name="using-post-cache-substitution"></a>キャッシュ後置換の使用

キャッシュ後置換を使用するには、2 つの手順が必要です。 まず、キャッシュされたページに表示する動的コンテンツを表す文字列を返すメソッドを定義する必要があります。 次に、ページに動的コンテンツを挿入するメソッドを呼び出します。

たとえば、キャッシュされたページに異なるニュース項目をランダムに表示するとします。 リスト 1 のクラスは、3 つのニュース項目のリストから 1 つのニュース項目をランダムに返す RenderNews() という名前の単一のメソッドを公開します。

**リスト 1 - モデル\ニュース.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

キャッシュ後の置換を利用するには、メソッドを呼び出します。 WriteSubstitution() メソッドは、キャッシュされたページの領域を動的コンテンツに置き換えるコードを設定します。 WriteSubstitution() メソッドは、リスト 2 のビューでランダムなニュース項目を表示するために使用されます。

**リスト 2 - ビュー\ホーム\インデックス.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

メソッドは、メソッドに渡されます。 メソッドが呼び出されないことに注意してください。 代わりに、メソッドへの参照が、AddressOf 演算子の助けを借りて WriteSubstitution() に渡されます。

インデックス ビューがキャッシュされます。 ビューはリスト 3 のコントローラーによって返されます。 Index() アクションは&lt;、60 秒間キャッシュされるインデックス&gt;ビューを発生させる OutputCache 属性で修飾されていることに注意してください。

**リスト 3 - コントローラ\ホームコントローラー.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

インデックス ビューがキャッシュされている場合でも、インデックス ページを要求すると異なるランダムなニュース項目が表示されます。 [インデックス] ページを要求すると、ページに表示される時間は 60 秒間変わりません (図 1 参照)。 時刻が変わらないということは、ページがキャッシュされていることを証明します。 しかし、WriteSubstitution() メソッドによって挿入されたコンテンツ ( ランダムなニュース項目 ) は、要求ごとに変更されます。

**図 1 – キャッシュされたページに動的なニュース項目を挿入する**

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>ヘルパー メソッドでのキャッシュ後置換の使用

キャッシュ後の置換を利用する簡単な方法は、カスタム ヘルパー メソッド内で WriteSubstitution() メソッドの呼び出しをカプセル化することです。 この方法は、リスト 4 のヘルパー メソッドによって示されています。

**リスト 4 – ヘルパー\AdHelper.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

リスト 4 には、2 つのメソッドを公開する Visual Basic モジュールが含まれています: レンダリングバナー() とレンダーバナー内部() 。 メソッドは、実際のヘルパー メソッドを表します。 このメソッドは、MVC htmlHelper クラスASP.NET標準を拡張して、他のヘルパー メソッドと同じようにビューで Html.RenderBanner() を呼び出すことができます。

メソッドは、メソッドにメソッドを渡してメソッドを呼び出します。

メソッドはプライベート メソッドです。 このメソッドはヘルパー メソッドとして公開されません。 RenderBannerInternal() メソッドは、3 つのバナー広告イメージのリストから 1 つのバナー広告イメージをランダムに返します。

リスト 5 の変更されたインデックス ビューは、RenderBanner() ヘルパー メソッドの使用方法を示しています。 MvcApplication1.Helpers 名前空間をインポートするビューの上部に追加&lt;の %@ インポート %&gt;ディレクティブが含まれていることに注意してください。 この名前空間をインポートしない場合、RenderBanner() メソッドは Html プロパティのメソッドとして表示されません。

**リスト 5 - ビュー\ホーム\インデックス.aspx (レンダーバナー()メソッドを使用)**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

リスト 5 のビューで表示されるページを要求すると、要求ごとに異なるバナー広告が表示されます (図 2 参照)。 ページはキャッシュされますが、RenderBanner() ヘルパー メソッドによってバナー広告が動的に挿入されます。

**図 2 – ランダムなバナー広告を表示するインデックス ビュー**

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a>まとめ

このチュートリアルでは、キャッシュされたページのコンテンツを動的に更新する方法について説明しました。 HttpResponse.WriteSubstitution() メソッドを使用して、キャッシュされたページに動的コンテンツを挿入できるようにする方法について説明しました。 また、HTML ヘルパー メソッド内で WriteSubstitution() メソッドの呼び出しをカプセル化する方法についても学習しました。

可能な限りキャッシュを利用して、Web アプリケーションのパフォーマンスに大きな影響を与える可能性があります。 このチュートリアルで説明したように、ページに動的コンテンツを表示する必要がある場合でも、キャッシュを利用できます。

> [!div class="step-by-step"]
> [前へ](improving-performance-with-output-caching-vb.md)
> [次へ](creating-a-controller-vb.md)
