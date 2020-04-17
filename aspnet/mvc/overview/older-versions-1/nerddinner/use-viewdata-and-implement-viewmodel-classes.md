---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: ビューデータを使用してビューモデル クラスを実装する |マイクロソフトドキュメント
author: rick-anderson
description: 手順 6 では、よりリッチなフォーム編集シナリオのサポートを有効にする方法を示し、コントローラーからビューにデータを渡すために使用できる 2 つのアプローチについても説明します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 7fa2af2a55d12bbe11b29dff594823a1e5ea0152
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541105"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>ViewData を使用し、ViewModel クラスを実装する

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、MVC 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NETの手順 6 です。
> 
> 手順 6 では、よりリッチなフォーム編集シナリオのサポートを有効にする方法を示し、コントローラーからビューにデータを渡すために使用できる 2 つの方法についても説明します: ViewData と ViewModel。
> 
> mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>オタクディナーステップ6:ビューデータとビューモデル

フォームポストのシナリオの数を取り上げ、作成、更新、削除 (CRUD) サポートを実装する方法について説明しました。 DinnersController の実装をさらに進め、より充実したフォーム編集シナリオのサポートを可能にします。 これを行う間、コント ローラーからビューにデータを渡すために使用できる 2 つのアプローチを説明します: ViewData と ViewModel.

### <a name="passing-data-from-controllers-to-view-templates"></a>コントローラからビューテンプレートへのデータの受け渡し

MVC パターンの特徴の 1 つは、アプリケーションのさまざまなコンポーネント間で実施するのに役立つ厳密な "懸念事項の分離" です。 モデル、コントローラ、ビューはそれぞれ、明確に定義された役割と責任を持ち、互いの間で明確に定義された方法で通信します。 これにより、テストの容易性とコードの再利用が促進されます。

コント ローラー クラスは、クライアントに HTML 応答を返すことを決定する場合、明示的に応答をレンダリングするために必要なすべてのデータをビュー テンプレートに渡します。 ビュー テンプレートは、データ取得やアプリケーション ロジックを実行せず、代わりに、コントローラーによって渡されるモデル/データから追い出されるレンダリング コードのみを持つことを制限する必要があります。

今、DinnersControllerクラスによってビューテンプレートに渡されるモデルデータは、Index() の場合はディナーオブジェクトのリスト、および詳細()、Edit()、Create()、Delete()の場合は単一のディナーオブジェクトです。 アプリケーションに UI 機能を追加する場合、ビュー テンプレート内で HTML 応答をレンダリングするために、このデータ以外のデータを渡す必要がよくあります。 たとえば、編集ビューと作成ビューの "国" フィールドを HTML テキストボックスからドロップダウンリストに変更する場合があります。 ビュー テンプレートの国名のドロップダウン リストをハードコーディングするのではなく、動的に設定するサポート対象国のリストから生成することもできます。 Dinner オブジェクト*と*サポートされている国のリストを、コントローラからビュー テンプレートに渡す方法が必要です。

これを達成する2つの方法を見てみましょう。

### <a name="using-the-viewdata-dictionary"></a>ビューデータ ディクショナリの使用

コント ローラーの基本クラスは、コント ローラーからビューに追加のデータ項目を渡すために使用できる"ViewData"ディクショナリ プロパティを公開します。

たとえば、編集ビュー内の "Country" テキスト ボックスを HTML テキストボックスからドロップダウンリストに変更するシナリオをサポートするために、国のドロップダウンリストのモデルとして使用できる SelectList オブジェクトを (Dinner オブジェクトに加えて) 渡すように Edit() アクション メソッドを更新します。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

上記の SelectList のコンストラクターは、ドロップダウン リストに入力する郡のリストと、現在選択されている値を受け入れます。

その後、前に使用した Html.TextBox() ヘルパー メソッドの代わりに Html.DropDownList() ヘルパー メソッドを使用するように Edit.aspx ビュー テンプレートを更新できます。

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

上記の Html.DropDownList() ヘルパー メソッドは、2 つのパラメーターを受け取ります。 最初の要素は、出力する HTML フォーム要素の名前です。 2 つ目は、ViewData ディクショナリを使用して渡した "SelectList" モデルです。 C# "as" キーワードを使用して、辞書内の型を SelectList としてキャストしています。

そして今、私たちのアプリケーションを実行し、ブラウザ内の */Dinners /Edit/1* URLにアクセスすると、編集UIが更新され、テキストボックスではなく国のドロップダウンリストが表示されます。

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

HTTP-POST Edit メソッドからビュー テンプレートの編集もレンダリングするため (エラーが発生した場合)、エラー シナリオでビュー テンプレートがレンダリングされるときに、このメソッドも更新して SelectList を ViewData に追加するようにします。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

そして今、私たちのディナーコントローラの編集シナリオは、ドロップダウンリストをサポートしています。

### <a name="using-a-viewmodel-pattern"></a>ビューモデル パターンの使用

ViewData ディクショナリ アプローチには、高速で実装が簡単であるという利点があります。 ただし、入力ミスはコンパイル時にキャッチされないエラーにつながる可能性があるため、一部の開発者は文字列ベースの辞書を使用することを好まない。 型指定されていない ViewData ディクショナリでは、ビュー テンプレートで C# のような厳密に型指定された言語を使用する場合は、"as" 演算子を使用するか、キャストする必要があります。

別の方法として、"ビューモデル" パターンと呼ばれる方法があります。 このパターンを使用する場合、特定のビュー シナリオに最適化され、ビュー テンプレートで必要な動的な値/コンテンツのプロパティを公開する厳密に型指定されたクラスを作成します。 コントローラクラスは、これらのビュー最適化クラスを設定し、使用するビューテンプレートに渡すことができます。 これにより、ビュー テンプレート内でのタイプ セーフ、コンパイル時チェック、およびエディターのインテリセンスが可能になります。

たとえば、Dinner フォームの編集シナリオを有効にするには、次のような "DinnerFormViewModel" クラスを作成して、厳密に型指定された 2 つのプロパティ (Dinner オブジェクトと、国のドロップダウンリストに設定するために必要な SelectList モデル) を公開します。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

その後、リポジトリから取得した Dinner オブジェクトを使用して DinnerFormViewModel を作成し、ビュー テンプレートに渡すために Edit() アクション メソッドを更新できます。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

次に、edit.aspx ページの上部にある "inherits" 属性を次のように変更して、"Dinner" オブジェクトの代わりに "DinnerFormViewModel" を期待するようにビュー テンプレートを更新します。

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

これを行うと、ビュー テンプレート内の "モデル" プロパティのインテリセンスが更新され、それを渡す DinnerFormViewModel 型のオブジェクト モデルが反映されます。

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

その後、ビューコードを更新して動作を回避できます。 作成している入力要素の名前を変更しない方法に注目してください (フォーム要素は"Title","Country"という名前になります) - しかし、私たちは、DinnerFormViewModelクラスを使用して値を取得するためにHTMLヘルパーメソッドを更新しています。

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

また、エラーをレンダリングするときに DinnerFormViewModel クラスを使用するように、編集ポスト メソッドを更新します。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

また、Create() アクションメソッドを更新して、まったく同じ*DinnerFormViewModel*クラスを再利用して、それらの中の国々のドロップダウンリストを有効にすることもできます。 以下は HTTP-GET の実装です。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

以下は HTTP-POST Create メソッドの実装です。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

そして今、私たちの編集画面と作成画面の両方が国を選ぶためのドロップダウンリストをサポートしています。

### <a name="custom-shaped-viewmodel-classes"></a>カスタムシェイプのビューモデル クラス

上のシナリオでは、クラスは、サポートする SelectList モデル プロパティと共に、Dinner モデル オブジェクトをプロパティとして直接公開します。 この方法は、ビュー テンプレート内に作成する HTML UI がドメイン モデル オブジェクトに比較的近い場合に適しています。

この場合に該当しないシナリオでは、オブジェクト モデルがビューで使用できるように最適化され、基になるドメイン モデル オブジェクトとはまったく異なる可能性があるカスタムシェイプの ViewModel クラスを作成できます。 たとえば、複数のモデル オブジェクトから収集されたプロパティ名や集計プロパティを公開する可能性があります。

カスタムシェイプの ViewModel クラスは、コントローラーからビューにデータを渡してレンダリングするために使用できるほか、コントローラーのアクション メソッドにポストバックされたフォーム データを処理するのにも役立ちます。 この後のシナリオでは、アクション メソッドで、フォームポストデータを使用して ViewModel オブジェクトを更新し、ViewModel インスタンスを使用して、実際のドメイン モデル オブジェクトをマップまたは取得する可能性があります。

カスタムシェイプの ViewModel クラスは、柔軟性を高めることができ、ビュー テンプレート内のレンダリング コードやアクション メソッド内のフォームポスト コードが複雑になりすぎる場合に、いつでも調べることができます。 これは、多くの場合、ドメイン モデルが生成する UI に明確に対応していない、および中間のカスタム型の ViewModel クラスが役立つという兆候です。

### <a name="next-step"></a>次の手順

ここでは、パーシャルページとマスターページを使用して、アプリケーション全体で UI を再利用して共有する方法について説明します。

> [!div class="step-by-step"]
> [前へ](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [次へ](re-use-ui-using-master-pages-and-partials.md)
