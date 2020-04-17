---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: マスター ページと部分を使用して UI を再利用する |マイクロソフトドキュメント
author: rick-anderson
description: ステップ7では、部分的なビューテンプレートとマスターページを使用して、コードの重複を排除するために、ビューテンプレート内に「DRY原則」を適用する方法を見てみましょう。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f381c4424a9fa0718cd234beeb01ce41bc4ca61e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542600"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>マスター ページと部分を利用して UI を再使用する

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、MVC 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)の手順 7 ASP.NET。
> 
> ステップ7では、部分的なビューテンプレートとマスターページを使用して、コードの重複を排除するために、ビューテンプレート内の「DRY原則」を適用する方法を見てみましょう。
> 
> mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。

## <a name="nerddinner-step-7-partials-and-master-pages"></a>NerdDinner ステップ 7: パーシャルとマスター ページ

MVCが受け入れるデザイン哲学ASP.NET一つは、「自分自身を繰り返さない」原則(一般的に「DRY」と呼ばれる)です。 DRY 設計はコードとロジックの重複を排除し、最終的にアプリケーションの構築を高速化し、保守が容易になります。

私たちはすでにいくつかのNerdDinnerシナリオで適用されるDRY原則を見てきました。 いくつかの例: 検証ロジックはモデルレイヤー内に実装されており、コントローラーの編集シナリオと作成シナリオの両方に適用できます。編集、詳細、および削除アクション メソッド全体で "NotFound" ビュー テンプレートを再利用しています。ビューテンプレートで規約命名パターンを使用しています。また、編集と作成の両方のアクション シナリオに対して、DinnerFormViewModel クラスを再利用しています。

ここで、ビューテンプレート内の「DRY原則」を適用してコードの重複を排除する方法を見てみましょう。

### <a name="re-visiting-our-edit-and-create-view-templates"></a>編集と作成のビュー テンプレートに再アクセスします。

現在、"Edit.aspx" と "Create.aspx" という 2 つの異なるビュー テンプレートを使用して、ディナー フォームの UI を表示しています。 それらの簡単な視覚的な比較は、それらがどれほど似ているかを強調します。 作成フォームは次のようになります。

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

そして、私たちの"編集"フォームは次のようになります。

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

大きな違いはありませんか? タイトルとヘッダーテキスト以外のフォームレイアウトと入力コントロールは同じです。

"Edit.aspx" ビュー テンプレートと "Create.aspx" ビュー テンプレートを開くと、同じフォーム レイアウトと入力コントロール コードが含まれていることがわかります。 この重複は、新しいDinnerプロパティを導入または変更するたびに2回変更する必要があることを意味します。

### <a name="using-partial-view-templates"></a>部分ビュー テンプレートの使用

ASP.NET MVC では、ページの部分部分のビュー レンダリング ロジックをカプセル化するために使用できる "部分ビュー" テンプレートを定義する機能がサポートされています。 "Partials" は、ビュー レンダリング ロジックを一度定義し、アプリケーション全体の複数の場所で再利用する便利な方法を提供します。

Edit.aspx と Create.aspx ビュー テンプレートの重複を "DRY-up" にするため、フォーム レイアウトと両方に共通する入力要素をカプセル化する"DinnerForm.ascx" という名前の部分ビュー テンプレートを作成します。 これを行うには、/Views/Dinnersディレクトリを右クリックし、[&gt;ビューの追加]メニューコマンドを選択します。

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

これにより、[ビューの追加] ダイアログが表示されます。 "DinnerForm" を作成する新しいビューに名前を付け、ダイアログ内の [部分ビューを作成する] チェック ボックスをオンにして、それを DinnerFormViewModel クラスに渡すことを示します。

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

[追加] ボタンをクリックすると、Visual Studio は "\Views\Dinners" ディレクトリ内に新しい "DinnerForm.ascx" ビュー テンプレートを作成します。

その後、Edit.aspx/Create.aspx ビュー テンプレートから重複したフォーム レイアウト/入力コントロール コードをコピー/貼り付け、新しい "DinnerForm.ascx" 部分ビュー テンプレートに貼り付けることができます。

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

その後、編集ビューテンプレートと作成ビューテンプレートを更新して、DinnerForm 部分テンプレートを呼び出してフォームの重複を排除できます。 これを行うには、ビューテンプレート内でHtml.RenderPartial(「ディナーフォーム」)を呼び出します。

##### <a name="createaspx"></a>aspx を作成します。

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>編集.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

Html.RenderPartial を呼び出すときに、目的の部分テンプレートのパスを明示的に修飾できます (たとえば、~ビュー/ディナー/DinnerForm.ascx")。 ただし、上記のコードでは、ASP.NET MVC 内の規約ベースの名前付けパターンを利用し、レンダリングする部分の名前として "DinnerForm" を指定しています。 これを行うときASP.NETMVCは、コンベンションベースのビューディレクトリで最初に見ます (DinnersControllerの場合、これは /Views/ディナーになります)。 そこに部分テンプレートが見つからない場合は、/Views/Shared ディレクトリで探します。

部分ビューの名前だけを使用して Html.RenderPartial() が呼び出されると、ASP.NET MVC は、呼び出し元のビュー テンプレートで使用される同じモデルと ViewData ディクショナリ オブジェクトを部分ビューに渡します。 または、Html.RenderPartial() のオーバーロードされたバージョンがあり、これを使用して、部分ビューに使用する代替モデル オブジェクトや ViewData ディクショナリを渡すことができます。 これは、完全なモデル/ビューモデルのサブセットのみを渡すシナリオに役立ちます。

| **サイドトピック: &lt;%=&gt; &gt;%&lt;ではなく % % が %** |
| --- |
| 上記のコードで気づいたことの 1 つは、Html.RenderPartial()&lt;を呼&gt;び出すときに&lt;%=&gt; % ブロックではなく % ブロックを使用していることです。 &lt;ASP.NETの&gt;%= % ブロックは、開発者が指定した値をレンダリングすることを示&lt;します (たとえば、%= "Hello" % が&gt;"Hello" をレンダリングします)。 &lt;%&gt;ブロックは、代わりに、開発者がコードを実行する必要があり、その中のレンダリングされた出力を明示的に実行する必要&lt;があることを示します ( たとえば、 %&gt;Response.Write("Hello") % 。 上記の Html.RenderPartial&gt;コードで % ブロックを&lt;使用している理由は、Html.RenderPartial() メソッドが文字列を返さないため、代わりにコンテンツを呼び出し元のビュー テンプレートの出力ストリームに直接出力するためです。 これは、パフォーマンス効率の理由から行われ、そうすることで(潜在的に非常に大きな)一時的な文字列オブジェクトを作成する必要がなくなります。 これにより、メモリ使用量が削減され、アプリケーション全体のスループットが向上します。 Html.RenderPartial() を使用する場合の一般的な誤りの 1 つは、呼び出しの末尾にセミ&lt;コロンを&gt;追加するのを忘れて % ブロック内に入るということです。 たとえば、このコードはコンパイラ エラーを引き&lt;起こします: % Html.RenderPartial("DinnerForm")&gt; %&lt;代わりに書く必要があります。%&gt; %&gt; &lt;ブロックは自己完結型のコード ステートメントであり、C# コード ステートメントを使用する場合はセミコロンで終了する必要があるためです。 |

### <a name="using-partial-view-templates-to-clarify-code"></a>部分ビュー テンプレートを使用したコードの明確化

複数の場所でビューレンダリングロジックを複製することを避けるために、「DinnerForm」部分ビューテンプレートを作成しました。 これは、部分ビュー テンプレートを作成する最も一般的な理由です。

単一の場所で呼び出されている場合でも、部分的なビューを作成することは意味があります。 ビュー レンダリング ロジックを抽出して、1 つ以上の適切な名前の部分テンプレートに分割すると、非常に複雑なビュー テンプレートが読みやすくなります。

たとえば、プロジェクトの Site.master ファイルの次のコード スニペットを考えてみましょう (このコードはまもなく見ています)。 このコードは、画面の右上にログイン/ログアウトリンクを表示するロジックが"LogOnUserControl"部分にカプセル化されているため、読み取りが比較的簡単です。

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

ビュー テンプレート内の html/code マークアップを理解しようとして混乱を見つけるたびに、その一部が抽出され、適切な名前の部分ビューにリファクタリングされた場合、そのマークアップが明確にならないかどうかを検討してください。

### <a name="master-pages"></a>マスター ページ

部分的なビューをサポートするだけでなく、ASP.NET MVC は、サイトの共通のレイアウトとトップレベルの html を定義するために使用できる「マスター ページ」テンプレートを作成する機能もサポートします。 コンテンツ プレースホルダ コントロールをマスター ページに追加して、ビューで上書きまたは "塗りつぶし" できる置き換え可能領域を識別できます。 これにより、アプリケーション全体に共通のレイアウトを適用する非常に効果的な (および DRY) 方法が提供されます。

既定では、新しいASP.NET MVC プロジェクトには、マスター ページ テンプレートが自動的に追加されます。 このマスター ページは "Site.master" と名付けられ、\Views\Shared\ フォルダ内にあります。

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

既定の Site.master ファイルは次のようになります。 これは、サイトの外側のHTMLと上部のナビゲーション用のメニューを定義します。 このコントロールには、タイトル用と、ページのプライマリ コンテンツを置き換える場所の 2 つの置き換え可能なコンテンツ プレースホルダ コントロールが含まれています。

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

NerdDinner アプリケーション用に作成したすべてのビュー テンプレート (「リスト」、「詳細」、「編集」、「作成」、「NotFound」など) は、この Site.master テンプレートに基づいています。 これは、[ビューの追加] ダイアログを使用してビューを作成したときに、既定でトップ&lt;% @&gt; Page % ディレクティブに追加された "MasterPageFile" 属性によって示されます。

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

つまり、Site.master コンテンツを変更し、ビュー テンプレートをレンダリングするときに変更を自動的に適用して使用することができます。

Site.master のヘッダー セクションを更新して、アプリケーションのヘッダーが "My MVC アプリケーション" ではなく "NerdDinner" になるようにします。 また、最初のタブが "夕食を検索" (HomeController の Index() アクションメソッドによって処理される) になるようにナビゲーションメニューを更新し、"夕食のホスト" という新しいタブを追加しましょう (DinnersController の Create() アクションメソッドによって処理されます)。

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

Site.master ファイルを保存してブラウザを更新すると、ヘッダーの変更がアプリケーション内のすべてのビューに表示されます。 次に例を示します。

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

そして *、/ディナー/編集/[id]URL*で:

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>次の手順

パーシャルページとマスターページには、ビューを整理するための非常に柔軟なオプションが用意されています。 ビューコンテンツやコードの重複を避け、ビューテンプレートを読みやすく管理しやすくすることができます。

ここで、先ほど作成したリストのシナリオを再検討し、スケーラブルなページングサポートを有効にしましょう。

> [!div class="step-by-step"]
> [前へ](use-viewdata-and-implement-viewmodel-classes.md)
> [次へ](implement-efficient-data-paging.md)
