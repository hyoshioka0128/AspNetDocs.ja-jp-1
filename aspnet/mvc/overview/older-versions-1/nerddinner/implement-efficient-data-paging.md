---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 効率的なデータ ページングを実装する |マイクロソフトドキュメント
author: rick-anderson
description: ステップ 8 では、1000 のディナーを一度に表示するのではなく、今後 10 回のディナーのみを表示するように、/Dinners URL にページング サポートを追加する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: a833553fe44b62b136f7eb55c7e00eca0b0462c6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541326"
---
# <a name="implement-efficient-data-paging"></a>効率的なデータ ページングを実装する

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、MVC 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)の手順 8 ASP.NET示します。
> 
> 手順 8 では、/Dinners URL にページング サポートを追加して、1000 のディナーを一度に表示する代わりに、一度に 10 回の今後のディナーのみを表示し、エンド ユーザーが SEO に優しい方法でリスト全体を前後にページ移動できるようにする方法を示します。
> 
> mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。

## <a name="nerddinner-step-8-paging-support"></a>NerdDinner ステップ 8: ページングのサポート

私たちのサイトが成功した場合、それは今後の夕食の数千人を持つことになります。 私たちは、これらのディナーのすべてを処理するために私たちのUIがスケールし、ユーザーがそれらを閲覧できるように確認する必要があります。 これを有効にするために *、/Dinners* URLにページングサポートを追加して、1000のディナーを一度に表示するのではなく、一度に10回のディナーのみを表示し、エンドユーザーがSEOフレンドリーな方法でリスト全体を前後にページできるようにします。

### <a name="index-action-method-recap"></a>インデックス() アクション メソッドの要約

DinnersController クラス内の Index() アクション メソッドは、現在次のようになります。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

*/Dinners* URL に対してリクエストが行われると、今後のすべてのディナーのリストが取得され、そのすべての一覧が表示されます。

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>クエリ可能 T&lt;について&gt;

*IQueryable&lt;&gt; T*は、.NET 3.5 の一部として LINQ で導入されたインターフェイスです。 ページング サポートを実装するために利用できる強力な "遅延実行" シナリオを有効にします。

私たちの夕食リポジトリでは、FindUpcomingDinners()&lt;メソッド&gt;からIQueryableディナーシーケンスを返しています。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

FindUpcomingDinners() メソッドによって返される IQueryable&lt;Dinner&gt;オブジェクトは、LINQ to SQL を使用してデータベースから Dinner オブジェクトを取得するクエリをカプセル化します。 重要なのは、クエリ内のデータにアクセスして反復処理を行うか、そのデータに対して ToList() メソッドを呼び出すまで、データベースに対してクエリを実行しません。 FindUpcomingDinners() メソッドを呼び出すコードは、クエリを実行する前に、IQueryable&lt;Dinner&gt;オブジェクトに "連鎖" 操作/フィルターを追加することをオプションで選択できます。 LINQ to SQL は、データが要求されたときにデータベースに対して結合されたクエリを実行するのに十分なスマートです。

ページング ロジックを実装するには、DinnersController の Index() アクション メソッドを更新して、返された IQueryable&lt;Dinner&gt;シーケンスに追加の "スキップ" 演算子と "Take" 演算子を適用してから、ToList() を呼び出します。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

上記のコードは、データベース内の最初の 10 個の今後のディナーをスキップし、20 個のディナーを返します。 LINQ to SQL は、Web サーバーではなく、SQL データベースでスキップロジックを実行する最適化された SQL クエリを構築するのに十分なほどスマートです。 これは、データベースに何百万もの Dinners が含まれている場合でも、この要求の一部として取得される 10 個のみの情報を取得することを意味します (効率的でスケーラブル)。

### <a name="adding-a-page-value-to-the-url"></a>URL に "ページ" 値を追加する

特定のページ範囲をハードコーディングするのではなく、URL に、ユーザーが要求している Dinner 範囲を示す "ページ" パラメーターを含める必要があります。

#### <a name="using-a-querystring-value"></a>クエリ文字列値の使用

次のコードは、クエリ文字列パラメーターをサポートし *、/Dinners?page=2*のような URL を有効にするために、Index() アクション メソッドを更新する方法を示しています。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

上記の Index() アクションメソッドには、"page" という名前のパラメータがあります。 パラメーターは、null 許容整数として宣言されています (これは int? が示すものです)。 これは *、/Dinners?page=2* URL の値がパラメータ値として渡されることを意味します。 */Dinners* URL (クエリ文字列値なし) は、NULL 値が渡されます。

ページ値にページサイズ (この場合は 10 行) を掛けて、スキップするディナーの数を決定します。 Null 許容型を扱う場合に便利な[C# null "合体" 演算子 (?) を](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx)使用しています。 上記のコードでは、ページ パラメータが null の場合、ページの値 0 が割り当てられます。

#### <a name="using-embedded-url-values"></a>埋め込み URL 値の使用

クエリ文字列値を使用する代わりに、実際の URL 自体にページ パラメーターを埋め込むことがあります。 たとえば *、/ディナー/ページ/2*または */ディナー/2。* ASP.NET MVC には、このようなシナリオを簡単にサポートできる強力な URL ルーティング エンジンが含まれています。

任意の受信 URL または URL 形式を、必要なコントローラークラスまたはアクション メソッドにマップするカスタム ルーティング ルールを登録できます。 必要なのは、プロジェクト内で Global.asax ファイルを開くことだけです。

![](implement-efficient-data-paging/_static/image2.png)

次に、ルートへの最初の呼び出しのような MapRoute() ヘルパー メソッドを使用して、新しいマッピング ルールを登録します。以下のマップルート()

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

上記では、"今後のディナー"という名前の新しいルーティングルールを登録しています。 URL 形式 "Dinners/Page/{page}" を示しています 。 MapRoute() メソッドの 3 番目のパラメーターは、この形式に一致する URL を DinnersController クラスの Index() アクション メソッドにマップする必要があることを示します。

クエリ文字列のシナリオで以前とまったく同じ Index() コードを使用できます。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

そして今、私たちはアプリケーションを実行し *、/Dinners*を入力すると、最初の10の今後のディナーが表示されます:

![](implement-efficient-data-paging/_static/image3.png)

*そして、私たちが/ディナー/ページ/1*を入力すると、夕食の次のページが表示されます:

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>ページ ナビゲーション UI の追加

ページング シナリオを完了するための最後の手順は、ユーザーが Dinner データを簡単にスキップできるように、ビュー テンプレート内に "次" と "前" ナビゲーション UI を実装することです。

これを正しく実装するには、データベース内のディナーの合計数と、そのデータの変換対象となるデータのページ数を知る必要があります。 次に、現在要求されている "ページ" 値がデータの先頭または末尾にあるかどうかを計算し、それに応じて "前の" UI と "次へ" UI を表示または非表示にする必要があります。 このロジックを Index() アクションメソッド内に実装できます。 または、このロジックをより再利用しやすい方法でカプセル化するヘルパークラスをプロジェクトに追加することもできます。

以下は、.NET Framework に組み込まれているリスト&lt;T&gt;コレクション クラスから派生した単純な "PaginatedList" ヘルパー クラスです。 IQueryable データの任意のシーケンスを改ページ調整するために使用できる再使用できるコレクション クラスを実装します。 NerdDinner&lt;アプリケーションでは、IQueryable Dinner&gt;の結果を使用して動作しますが、他のアプリケーション シナリオで IQueryable&gt;&lt;&gt;&lt;製品または IQueryable 顧客の結果に対しても簡単に使用できます。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

"PageIndex"、"PageSize"、"TotalCount"、および "合計ページ" などのプロパティを計算して公開する方法の上に注意してください。 また、コレクション内のデータページが元のシーケンスの先頭または末尾にあるかどうかを示す 2 つのヘルパー プロパティ "HasPreviousPage" と "HasNextPage" を公開します。 上記のコードでは、Dinnerオブジェクトの総数のカウントを取得する2つのSQLクエリが実行され(これはオブジェクトを返すのではなく、整数を返す「SELECT COUNT」文を実行します)、もう1つは現在のデータページに必要なデータ行だけをデータベースから取得します。

その後、DinnersController.Index() ヘルパー メソッドを更新して、DinnerRepository.FindUpcomingDinners() の結果から PaginatedList&lt;ディナー&gt;を作成し、ビュー テンプレートに渡すことができます。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

次に、ビューページ&lt;&lt;&gt;&gt;&lt;IEnumerable&lt;&gt;&gt;Dinner の代わりに ViewPage NerdDinner.Helpers.PaginatedList ディナーから継承するように 、ビュー テンプレートの下に次のコードを追加して、次のナビゲーション UI と前のナビゲーション UI を表示または非表示にするように、ビュー テンプレートの一番下に次のコードを追加します。

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

ハイパーリンクを生成するために Html.RouteLink() ヘルパー メソッドを使用する方法の上に注意してください。 このメソッドは、前に使用した Html.ActionLink() ヘルパー メソッドに似ています。 違いは、Global.asax ファイル内で設定する "今後のディナー" ルーティング ルールを使用して URL を生成することです。 これにより *、"/Dinners/Page/{page}* という形式の Index() アクション メソッドへの URL が生成されます。

そして今、我々は再び私たちのアプリケーションを実行すると、我々は我々のブラウザで一度に10ディナーが表示されます:

![](implement-efficient-data-paging/_static/image5.png)

&lt;&lt;&gt;また&lt;、&gt;ページの下部にナビゲーション UI があり、検索エンジンでアクセス可能な URL を使用してデータを前方および逆方向にスキップ&gt;できます。

![](implement-efficient-data-paging/_static/image6.png)

| **サイドトピック: IQueryable T の&lt;意味を理解する&gt;** |
| --- |
| IQueryable&lt;&gt; T は、さまざまな興味深い遅延実行シナリオ (ページングやコンポジション ベースのクエリなど) を可能にする非常に強力な機能です。 すべての強力な機能と同様に、あなたはそれを使用する方法に注意し、それが悪用されていないかどうかを確認したいと思います。 リポジトリから IQueryable&lt;T&gt;の結果を返すと、呼び出し元のコードがチェーン化された演算子メソッドに追加され、最終的なクエリ実行に参加できることを認識することが重要です。 この機能を呼び出しコードを提供しない場合は、既に実行されているクエリ&lt;の&gt;結果を含む&lt;IList T または IEnumerable T&gt;の結果を返す必要があります。 ページネーションのシナリオでは、実際のデータページネーション ロジックを呼び出されるリポジトリ メソッドにプッシュする必要があります。 このシナリオでは、FindUpcomingDinners() ファインダー&lt;メソッドを更新して、PaginatedList ディナー&gt;検索予定ディナー (int pageIndex, int pageSize) を返す署名を持っているか 、または IList&lt;ディナー&gt;の合計カウントを返すために "totalCount" アウトパラムを使用します。&lt;&gt; |

### <a name="next-step"></a>次の手順

それでは、アプリケーションに認証と承認のサポートを追加する方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](re-use-ui-using-master-pages-and-partials.md)
> [次へ](secure-applications-using-authentication-and-authorization.md)
