---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: コントローラとビューを使用してリスト/詳細 UI を実装する |マイクロソフトドキュメント
author: rick-anderson
description: 手順 4 では、モデルを利用してユーザーにデータの一覧/詳細ナビゲーション エクスペリエンスを提供するコントローラーをアプリケーションに追加する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 49c7dc977477a4edbfcfc68b166ae7ea3fa22f2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541313"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>コントローラーとビューを使用し、リスティング/詳細 UI を実装する

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、mvc 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NETの手順 4 です。
> 
> 手順 4 では、NerdDinner サイトでディナーのデータ一覧/詳細ナビゲーション エクスペリエンスをユーザーに提供するために、モデルを利用するアプリケーションに Controller を追加する方法を示します。
> 
> mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。

## <a name="nerddinner-step-4-controllers-and-views"></a>NerdDinner ステップ 4: コントローラーとビュー

従来の Web フレームワーク (従来の ASP、PHP、ASP.NET Web フォームなど) では、通常、受信 URL はディスク上のファイルにマップされます。 たとえば、"/Products.aspx" や "/Products.php" などの URL の要求は、"Products.aspx" または "Products.php" ファイルで処理される場合があります。

Web ベースの MVC フレームワークは、URL をサーバー コードに対して少し異なる方法でマップします。 受信 URL をファイルにマップする代わりに、URL をクラスのメソッドにマップします。 これらのクラスは「コントローラ」と呼ばれ、着信 HTTP 要求の処理、ユーザー入力の処理、データの取得と保存、クライアントに返送する応答の決定 (HTML の表示、ファイルのダウンロード、別の URL へのリダイレクトなど) を担当します。

NerdDinnerアプリケーションの基本モデルを構築したので、次のステップは、それを利用して、私たちのサイト上のDinnersのデータリスト/詳細ナビゲーション体験をユーザーに提供するアプリケーションにコントローラを追加することです。

### <a name="adding-a-dinnerscontroller-controller"></a>ディナーコントローラコントローラの追加

まず、Web プロジェクト内の "コントローラー" フォルダーを右クリックし、**コント&gt;ローラー**メニューコマンドを選択します (Ctrl-M、Ctrl-C を入力してこのコマンドを実行することもできます)。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

これにより、「コントローラの追加」ダイアログが表示されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

新しいコントローラに「DinnersController」という名前を付け、[追加]ボタンをクリックします。 次に、\Controllers ディレクトリの下にDinnersController.csファイルを追加します。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

また、コード エディター内で新しい DinnersController クラスを開きます。

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>DinnersController クラスへの Index() および Details() アクションメソッドの追加

私たちは、今後のディナーのリストを閲覧するために私たちのアプリケーションを使用して訪問者を有効にし、彼らはそれについての具体的な詳細を見るためにリスト内の任意のディナーをクリックできるようにしたいと考えています。 これを行うには、アプリケーションから次の URL を公開します。

| **URL** | **目的** |
| --- | --- |
| */ディナー/* | 今後のディナーの HTML リストを表示する |
| */ディナー/詳細/[id]* | URL に埋め込まれた "id" パラメータで示される特定のディナーに関する詳細を表示します。 たとえば、/Dinners/Details/2 には、DinnerID 値が 2 のディナーに関する詳細を HTML ページに表示します。 |

以下のような DinnersController クラスに 2 つのパブリックな "アクション メソッド" を追加することで、これらの URL の初期実装を公開します。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

次に NerdDinner アプリケーションを実行し、ブラウザーを使用して呼び出します。 *"/Dinners/"* URL を入力すると *、Index()* メソッドが実行され、次の応答が返されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

*"/ディナー/詳細/2"* URL を入力すると*Details()* メソッドが実行され、次の応答が返されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

あなたは疑問に思うかもしれません - mvcASP.NET DinnersControllerクラスを作成し、それらのメソッドを呼び出すためにどのように知っていましたか? それを理解するために、ルーティングのしくみを簡単に見てみましょう。

### <a name="understanding-aspnet-mvc-routing"></a>MVC ルーティングASP.NETについて

ASP.NET MVC には強力な URL ルーティング エンジンが含まれており、URL をコントローラ クラスにマップする方法を柔軟に制御できます。 これにより、MVC ASP.NET がどのコントローラクラスを作成するか、どのメソッドを呼び出すのかを選択する方法を完全にカスタマイズできるだけでなく、変数を URL/Querystring から自動的に解析し、パラメータ引数としてメソッドに渡すさまざまな方法を構成できます。 SEO (検索エンジン最適化) のサイトを完全に最適化し、アプリケーションから必要な URL 構造を公開する柔軟性を提供します。

既定では、新しいASP.NET MVC プロジェクトには、既に登録されている URL ルーティング 規則の事前構成されたセットが付属しています。 これにより、明示的に何も設定しなくても、アプリケーションを簡単に開始できます。 既定のルーティング ルールの登録は、プロジェクトの "アプリケーション" クラス内にあります。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

MVC ルーティング 規則ASP.NET既定の規則は、このクラスの "RegisterRoutes" メソッド内に登録されます。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

「ルート。上記の MapRoute()"メソッド呼び出しは、URL 形式を使用して着信 URL をコントローラー クラスにマップする既定のルーティング ルールを登録します。 "MapRoute()" メソッド呼び出しに渡される 3 番目のパラメーターは、URL に存在しない場合にコントローラー/アクション/id 値に使用する一連の既定値です (コントローラー = "ホーム"、アクション="インデックス"、Id=" )。

次の表は、既定の "<em>/{コントローラー}/{action}/{id}"</em>ルート規則を使用してさまざまな URL がマップされる方法を示しています。

| **URL** | **コントローラクラス** | **アクション メソッド** | **渡されたパラメータ** |
| --- | --- | --- | --- |
| */ディナー/詳細/2* | ディナーズコントローラー | 詳細(id) | id=2 |
| */ディナー/編集/5* | ディナーズコントローラー | 編集(id) | id=5 |
| */ディナー/作成* | ディナーズコントローラー | Create() | 該当なし |
| */ディナー* | ディナーズコントローラー | インデックス() | 該当なし |
| */home* | ホームコントローラー | インデックス() | 該当なし |
| */* | ホームコントローラー | インデックス() | 該当なし |

最後の 3 行は、使用されている既定値 (コントローラー = ホーム、アクション = インデックス、ID = "") を示します。 "Index" メソッドが指定されていない場合はデフォルトのアクション名として登録されるため、"/Dinners" および "/Home" URL によって、コントローラ クラスで Index() アクション メソッドが呼び出されます。 "Home" コントローラが指定されていない場合は既定のコントローラとして登録されるため、"/" URL によって HomeController が作成され、そのコントローラに対する Index() アクション メソッドが呼び出されます。

これらのデフォルトのURLルーティングルールが気に入らない場合は、変更が簡単です - 上記のRegisterRoutesメソッド内で編集するだけです。 しかし、NerdDinnerアプリケーションでは、デフォルトのURLルーティングルールを変更するのではなく、そのまま使用します。

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>私たちのディナーコントローラからディナーリポジトリを使用する

DinnersController の Index() アクションメソッドと Details() アクションメソッドの現在の実装を、モデルを使用する実装に置き換えてみましょう。

この動作を実装するために、先ほど構築した DinnerRepository クラスを使用します。 まず、"NerdDinner.Models" 名前空間を参照する "using" ステートメントを追加し、DinnerController クラスのフィールドとして DinnerRepository のインスタンスを宣言します。

この章の後半では、「依存関係の注入」という概念を紹介し、より良い単体テストを可能にする DinnerRepository への参照をコントローラが取得する別の方法を示します。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

これで、取得したデータ モデル オブジェクトを使用して HTML 応答を生成する準備ができました。

### <a name="using-views-with-our-controller"></a>コントローラでビューを使用する

アクションメソッド内でコードを記述して HTML をアセンブルし *、Response.Write()* ヘルパーメソッドを使用してクライアントに送り返す方法は可能ですが、このアプローチは非常に簡単に扱いにくくなります。 より優れたアプローチは、DinnersController アクション メソッド内でアプリケーションロジックとデータロジックを実行し、HTML 応答をレンダリングするために必要なデータを、HTML 表現を出力する独立した "ビュー" テンプレートに渡す方法です。 ここですぐにわかるように、「ビュー」テンプレートは、HTML マークアップと埋め込みレンダリング コードの組み合わせを含むテキスト ファイルです。

コント ローラー ロジックをビュー レンダリングから分離すると、いくつかの大きな利点があります。 特に、アプリケーション コードと UI の書式設定/レンダリング コードの間に明確な "懸念事項の分離" を強制するのに役立ちます。 これにより、UI レンダリング ロジックから切り離してアプリケーション ロジックを単体テストする方がはるかに簡単になります。 アプリケーション コードを変更しなくても、UI レンダリング テンプレートを後で簡単に変更できます。 また、開発者とデザイナーが共同でプロジェクトに対して共同作業を行いやすくなります。

DinnersController クラスを更新して、2 つのアクション メソッドのメソッド シグネチャを "void" の戻り値の型から "ActionResult" の戻り値の型に変更することで、ビュー テンプレートを使用して HTML UI 応答を返すことを示すことができます。 次に、コント ローラーの基本クラスで*View()* ヘルパー メソッドを呼び出して、次のような "ViewResult" オブジェクトを返すことができます。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

上記で使用している*View()* ヘルパー メソッドのシグネチャは、次のようになります。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

*View()* ヘルパー メソッドの最初のパラメーターは、HTML 応答のレンダリングに使用するビュー テンプレート ファイルの名前です。 2 番目のパラメーターは、HTML 応答をレンダリングするためにビュー テンプレートが必要とするデータを含むモデル オブジェクトです。

Index() アクションメソッド内で*View()* ヘルパーメソッドを呼び出し、「インデックス」ビューテンプレートを使用してディナーの HTML リストをレンダリングすることを示しています。 ここでは、ビュー テンプレートに Dinner オブジェクトのシーケンスを渡して、リストを生成します。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

Details() アクションメソッド内では、URL 内で指定された ID を使用して Dinner オブジェクトを取得しようとします。 有効な Dinner が見つかった場合は *、View()* ヘルパー メソッドを呼び出し、取得した Dinner オブジェクトをレンダリングするために "Details" ビュー テンプレートを使用することを示します。 無効なディナーが要求された場合、"NotFound" ビュー テンプレート (およびテンプレート名を受け取るオーバーロードされたバージョンの*View()* ヘルパー メソッド) を使用して、Dinner が存在しないことを示す、役立つエラー メッセージが表示されます。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

次に、"NotFound"、"詳細"、および "インデックス" ビュー テンプレートを実装してみましょう。

### <a name="implementing-the-notfound-view-template"></a>"NotFound" ビュー テンプレートの実装

まず、要求されたディナーが見つからないことを示すわかりやすいエラー メッセージを表示する "NotFound" ビュー テンプレートを実装します。

コント ローラー アクション メソッド内でテキスト カーソルを配置して新しいビュー テンプレートを作成し、右クリックして [ビューの追加] メニュー コマンドを選択します (Ctrl-M、Ctrl-V を入力してこのコマンドを実行することもできます)。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

これにより、以下のような「ビューの追加」ダイアログが表示されます。 既定では、ダイアログが起動されたときのカーソルが含まれるアクション メソッドの名前 (この場合は "Details" ) に合わせて作成するビューの名前があらかじめ入力されます。 最初に "NotFound" テンプレートを実装する必要があるため、このビュー名をオーバーライドし、"NotFound" に設定します。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

[追加] ボタンをクリックすると、Visual Studio は "\Views\Dinners" ディレクトリ内に新しい "NotFound.aspx" ビュー テンプレートを作成します (ディレクトリがまだ存在しない場合にも作成されます)。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

また、コード エディター内で新しい "NotFound.aspx" ビュー テンプレートを開きます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

ビュー テンプレートには、既定でコンテンツとコードを追加できる 2 つの "コンテンツ領域" があります。 最初の方法では、返送される HTML ページの "タイトル" をカスタマイズできます。 2つ目は、返送されるHTMLページの「メインコンテンツ」をカスタマイズすることができます。

"NotFound" ビュー テンプレートを実装するには、基本的なコンテンツをいくつか追加します。

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

その後、ブラウザ内で試すことができます。 これを行うには *、「ディナー/詳細/9999」URLを*リクエストしましょう。 これは、現在データベースに存在しないディナーを参照し、DinnersController.Details() アクションメソッドが "NotFound" ビューテンプレートをレンダリングする原因となります。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

上記のスクリーン ショットで気づくことの 1 つは、基本的なビュー テンプレートが、画面上のメイン コンテンツを囲む HTML の束を継承していることです。 これは、ビュー テンプレートがサイト上のすべてのビューに一貫したレイアウトを適用できる "マスター ページ" テンプレートを使用しているためです。 マスター ページの動作については、このチュートリアルの後半で説明します。

### <a name="implementing-the-details-view-template"></a>"詳細" ビュー テンプレートの実装

ここでは、単一の Dinner モデル用に HTML を生成する"詳細" ビュー テンプレートを実装しましょう。

これを行うには、テキストカーソルを Details アクションメソッド内に配置し、右クリックして [ビューの追加] メニュー コマンド (または Ctrl+M、Ctrl-V キーを押します) を選択します。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

これにより、[ビューの追加] ダイアログが表示されます。 既定のビュー名 (「詳細」) をそのまま使用します。 ダイアログで[厳密に型指定されたビューを作成]チェックボックスを選択し、コントローラからビューに渡すモデルタイプの名前を選択します(コンボボックスのドロップダウンを使用)。 このビューでは、Dinner オブジェクトを渡しています (この型の完全修飾名は "NerdDinner.Models.Dinner"です)。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

「空のビュー」を作成することを選択した前のテンプレートとは異なり、今回は「詳細」テンプレートを使用してビューを自動的に「スキャフォールディング」することを選択します。 このことを示すには、上記のダイアログで「コンテンツの表示」ドロップダウンを変更します。

「スキャフォールディング」は、私たちが渡すDinnerオブジェクトに基づいて、詳細ビューテンプレートの初期実装を生成します。 これにより、ビュー テンプレートの実装を簡単に開始できます。

[追加] ボタンをクリックすると、Visual Studio は "\Views\Dinners" ディレクトリ内に新しい "Details.aspx" ビュー テンプレート ファイルを作成します。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

また、コード エディター内で新しい "Details.aspx" ビュー テンプレートを開きます。 このファイルには、Dinner モデルに基づく詳細ビューの初期スキャフォールディング実装が含まれます。 スキャフォールディング エンジンは、.NET リフレクションを使用して、渡されたクラスで公開されているパブリック プロパティを調べ、見つかった各型に基づいて適切なコンテンツを追加します。

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

*"/Dinners/Details/1"* URL をリクエストすると、この "詳細" スキャフォールディングの実装がブラウザでどのようなものであるかを確認できます。 この URL を使用すると、最初に作成したときに手動でデータベースに追加したディナーのいずれかが表示されます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

これにより、すぐに起動して実行し、Details.aspx ビューの初期実装を提供します。 その後、UIをカスタマイズして満足するように調整することができます。

詳細を見ると、 Details.aspx テンプレートは、静的 HTML だけでなく、埋め込まれたレンダリング コードが含まれていることがわかります。 &lt;%&gt;コード ナゲットはビュー テンプレートのレンダリング時にコードを&lt;実行し、%= %&gt;コード ナゲットは、その中に含まれるコードを実行し、その結果をテンプレートの出力ストリームにレンダリングします。

厳密に型指定された "Model" プロパティを使用して、コントローラーから渡された "Dinner" モデル オブジェクトにアクセスするコードを View 内に記述できます。 Visual Studio では、エディター内でこの "モデル" プロパティにアクセスする際に、完全なコードインテッラーセンスを提供します。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

最終的な詳細ビュー テンプレートのソースが次のようになるように、いくつかの調整を行いましょう。

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

*「/ディナー/詳細/1」URL*に再びアクセスすると、次のようにレンダリングされます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>"インデックス" ビュー テンプレートの実装

今度は、今後のディナーのリストを生成する「インデックス」ビューテンプレートを実装しましょう。 これを行うには、テキストカーソルをインデックスアクションメソッド内に配置し、右クリックして[ビューの追加]メニューコマンド(またはCtrl-M、Ctrl-Vを押す)を選択します。

[ビューの追加] ダイアログでは、"Index" という名前のビュー テンプレートを保持し、[厳密に型指定されたビューを作成する] チェック ボックスをオンにします。 今回は、"List" ビュー テンプレートを自動的に生成し、ビューに渡されるモデルタイプとして "NerdDinner.Models.Dinner" を選択します (これは、"List" スキャフォールドを作成すると、コントローラからビューに Dinner オブジェクトのシーケンスを渡すことを前提にビューの追加ダイアログが表示されます)。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

[追加] ボタンをクリックすると、Visual Studio は "\Views\Dinners" ディレクトリ内に新しい "Index.aspx" ビュー テンプレート ファイルを作成します。 ビューに渡す Dinners の HTML テーブル リストを提供する初期実装を "スキャフォールディング" します。

アプリケーションを実行し *、"/Dinners/"* URL にアクセスすると、次のようにディナーのリストがレンダリングされます。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

上記のテーブルソリューションは、私たちのDinnerデータのグリッドのようなレイアウトを提供します - それは私たちが私たちの消費者がDinnerリストに直面している場合に望むものではありません。 Index.aspx ビュー テンプレートを更新し、データの列数を少なくするように変更し&lt;、ul&gt;要素を使用して次のコードを使用してテーブルの代わりにレンダリングできます。

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

モデルの各ディナーをループ処理するときに、上記の foreach ステートメント内で "var" キーワードを使用しています。 C# 3.0 に慣れていない人は、"var" を使用すると、dinner オブジェクトが遅延バインディングされていることを意味すると考えるかもしれません。 これは、コンパイラが厳密に型指定された "Model" プロパティ ("IEnumerable&lt;Dinner " という型) に&gt;対して型推論を使用し、ローカルの "dinner" 変数を Dinner 型としてコンパイルしていることを意味します。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

ブラウザの */Dinners* URL で更新を行うと、更新されたビューは次のようになります。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

これは見栄えが良いですが、まだ完全にそこにはありません。 最後の手順は、エンドユーザーがリスト内の個々の Dinner をクリックして、その詳細を確認できるようにすることです。 これを実装するには、DinnersController の詳細アクション メソッドにリンクする HTML ハイパーリンク要素をレンダリングします。

これらのハイパーリンクは、2 つの方法のいずれかでインデックス ビュー内に生成できます。 1 つ目は、以下&lt;のような&gt;要素を手動で作成し、HTML&gt;要素内に&lt;&gt; % % ブロックを埋め込みます。 &lt;

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

別の方法として、コントローラ上の別のアクション メソッドにリンクする&lt;&gt;要素をプログラムで HTML の作成をサポートする、ASP.NET MVC 内の組み込みの "Html.ActionLink() " ヘルパー メソッドを利用する方法もあります。

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

Html.ActionLink() ヘルパー メソッドの最初のパラメーターは、表示するリンク テキスト (この場合は、dinner のタイトル) で、2 番目のパラメーターはリンクを生成する Controller アクション名 (この場合は Details メソッド) であり、3 番目のパラメーターはアクションに送信する一連のパラメーターです (プロパティ名/値を持つ匿名型として実装されます)。 この場合、リンクするディナーの "id" パラメーターを指定し、ASP.NET MVC の既定の URL ルーティング ルールは "{Controller}/{アクション}/{id}" であるため、Html.ActionLink() ヘルパー メソッドは次の出力を生成します。

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

Index.aspx ビューでは、Html.ActionLink() ヘルパー メソッドのアプローチを使用し、リスト内の各ディナーを適切な詳細 URL にリンクします。

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

そして今、私たちは */Dinners* URLをヒットすると、私たちのディナーリストは以下のようになります:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

リスト内のディナーのいずれかをクリックすると、その詳細を表示するために移動します。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>規約ベースの名前付けと \Views ディレクトリ構造

ASP.NET MVC アプリケーションでは、既定で、ビュー テンプレートを解決するときに、規則に基づいたディレクトリの名前付け構造を使用します。 これにより、開発者は Controller クラス内からビューを参照するときに、場所のパスを完全に修飾する必要がなくなります。 既定では、ASP.NET MVC は、アプリケーションの下にある *\Views\[ControllerName]\*ディレクトリ内のビュー テンプレート ファイルを探します。

たとえば、DinnersController クラスに取り組んできましたが、このクラスは、"インデックス"、"詳細"、"NotFound" の 3 つのビュー テンプレートを明示的に参照します。 ASP.NET MVC は、既定では、アプリケーションのルート ディレクトリの下にある*\Views\Dinners*ディレクトリ内でこれらのビューを探します。

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

プロジェクト内に現在3つのコントローラクラスがある方法に注意してください (DinnersController、 HomeControllerとAccountController - 最後の2つは、プロジェクトを作成したときにデフォルトで追加されました)、\Viewsディレクトリ内に3つのサブディレクトリ(コントローラごとに1つ)があります。

ホーム および アカウント コントローラから参照されるビューは、それぞれの*\Views\Home*ディレクトリおよび*\Views\Account*ディレクトリからビュー テンプレートを自動的に解決します。 *\Views\Shared*サブディレクトリには、アプリケーション内の複数のコントローラで再利用されるビュー テンプレートを格納する方法が用意されています。 ASP.NETMVC がビュー テンプレートを解決しようとすると、最初に*\Views\[Controller]* の特定のディレクトリ内でチェックされ、ビュー テンプレートが見つからない場合は*\Views\Shared*ディレクトリ内に表示されます。

個々のビュー テンプレートに名前を付ける場合は、ビュー テンプレートがレンダリングの原因となったアクション メソッドと同じ名前を共有することをお勧めします。 たとえば、上記の "Index" アクション メソッドは、"Index" ビューを使用してビューの結果を表示し、"Details" アクション メソッドは "Details" ビューを使用して結果を表示しています。 これにより、各アクションに関連付けられているテンプレートをすばやく確認できます。

ビュー テンプレートがコントローラで呼び出されるアクション メソッドと同じ名前を持っている場合、開発者はビュー テンプレート名を明示的に指定する必要はありません。 代わりに、モデル オブジェクトを "View()" ヘルパー メソッドに渡すだけで (ビュー名を指定せずに)ASP.NET、MVC は自動的にディスク上の*ビュー\[テンプレートを\[* 使用してレンダリングすることを推測します。

これにより、コントローラコードを少しクリーンアップし、コード内で名前を二度複製することを避けられます。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

上記のコードは、サイトの素敵なディナーリスト/詳細エクスペリエンスを実装するために必要なすべてです。

#### <a name="next-step"></a>次の手順

私たちは今、構築された素敵なディナーブラウジング体験を持っています。

今すぐ CRUD (作成、読み取り、更新、削除) データフォーム編集のサポートを有効にしましょう。

> [!div class="step-by-step"]
> [前へ](build-a-model-with-business-rule-validations.md)
> [次へ](provide-crud-create-read-update-delete-data-form-entry-support.md)
