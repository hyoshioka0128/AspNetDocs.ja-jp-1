---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: AJAX を使用したマッピング シナリオの実装 |マイクロソフトドキュメント
author: rick-anderson
description: ステップ 11 は、AJAX マッピング サポートを NerdDinner アプリケーションに統合する方法を示し、ディナーを作成、編集、または表示しているユーザーが l..
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: f2e2640eb421d5ee8006915f46cbe1090b8d21ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542587"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>AJAX を使用し、マッピング シナリオを実装する

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、MVC 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)の手順 11 ASP.NETします。
> 
> ステップ 11 は、AJAX マッピング サポートを NerdDinner アプリケーションに統合する方法を示し、ディナーの作成、編集、または表示を行うユーザーがディナーの場所をグラフィカルに表示できるようにします。
> 
> mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>NerdDinner ステップ 11: AJAX マップの統合

AJAX マッピングのサポートを統合することで、アプリケーションをもう少し視覚的にわくわくします。 これにより、ディナーの作成、編集、または表示を行っているユーザーが、夕食の場所をグラフィカルに表示できるようになります。

### <a name="creating-a-map-partial-view"></a>マップ部分ビューの作成

アプリケーション内のいくつかの場所でマッピング機能を使用します。 コード DRY を維持するために、複数のコント ローラーアクションとビューで再利用できる単一の部分テンプレート内の共通のマップ機能をカプセル化します。 この部分ビューに "map.ascx" という名前を付け、\Views\Dinners ディレクトリ内に作成します。

map.ascx 部分を作成するには、\Views\Dinners ディレクトリを右クリックし、[追加-&gt;表示] メニュー コマンドを選択します。 ビューに "Map.ascx" という名前を付け、それを部分的なビューとして確認し、厳密に型指定された "Dinner" モデル クラスを渡すことを示します。

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

「追加」ボタンをクリックすると、部分テンプレートが作成されます。 次に、次の内容を含む Map.ascx ファイルを更新します。

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

最初&lt;のスクリプト&gt;参照は、Microsoft 仮想アース 6.2 マッピング ライブラリを指します。 2&lt;番目&gt;のスクリプト参照は、一般的な Javascript マッピング ロジックをカプセル化する map.js ファイルを指します。 &lt;div id="theMap"&gt;要素は、仮想地球がマップをホストするために使用するHTMLコンテナです。

その後、このビュー&lt;に&gt;固有の 2 つの JavaScript 関数を含む埋め込みスクリプト ブロックがあります。 最初の関数は、jQuery を使用して、ページがクライアント側スクリプトを実行する準備ができたときに実行される関数をワイヤアップします。 これは、仮想アース マップ コントロールを読み込むために Map.js スクリプト ファイル内で定義する LoadMap() ヘルパー関数を呼び出します。 2 番目の関数は、場所を識別するピンをマップに追加するコールバック イベント ハンドラーです。

クライアント側スクリプト ブロック内でサーバー側&lt;の %= %&gt;ブロックを使用して、JavaScript にマップする Dinner の緯度と経度を埋め込む方法に注目してください。 これは、クライアント側スクリプトで使用できる動的な値を出力する場合に便利な手法です (値を取得するためにサーバーに個別の AJAX コールバックを必要とせず、高速に実行できます)。 %= &lt;%&gt;ブロックは、ビューがサーバーでレンダリングしているときに実行されるため、HTML の出力は JavaScript 値が埋め込まれた状態になります (例: var latitude = 47.64312;)。

### <a name="creating-a-mapjs-utility-library"></a>Map.js ユーティリティ ライブラリの作成

ここで、マップの JavaScript 機能をカプセル化するために使用できる Map.js ファイルを作成しましょう (そして、上記の LoadMap メソッドと LoadPin メソッドを実装します)。 これを行うには、プロジェクト内の \Scripts ディレクトリを右クリックし、[新しい項目の&gt;追加] メニュー コマンドを選択し、JScript 項目を選択して "Map.js" という名前を付けます。

以下は、マップを表示し、夕食のために場所のピンを追加するために仮想地球と対話する Map.js ファイルに追加する JavaScript コードです。

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>マップを作成フォームと編集フォームと統合する

マップのサポートを既存の作成および編集のシナリオと統合します。 良いニュースは、これは非常に簡単で、コントローラコードを変更する必要がないということです。 作成ビューと編集ビューでは、ディナー フォーム UI を実装するための共通の "DinnerForm" 部分ビューが共有されるため、マップを 1 か所に追加して、作成シナリオと編集シナリオの両方で使用できます。

必要なのは、\Views\Dinners\DinnerForm.ascx 部分ビューを開き、新しいマップを部分的に含むように更新することだけです。 以下は、マップが追加されると、更新された DinnerForm の外観です (注: 簡潔にするために、以下のコード スニペットから HTML フォーム要素を省略します)。

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

上記の DinnerForm の一部は、モデル型として "DinnerFormViewModel" 型のオブジェクトを取ります (これは、Dinner オブジェクトと、国のドロップダウン リストを設定するための SelectList の両方が必要であるためです)。 私たちのマップの部分は、モデルタイプとしてタイプ"Dinner"のオブジェクトを必要とするので、マップの部分をレンダリングするときにDinnerFormViewModelのDinnerサブプロパティだけを渡しています。

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

部分に追加した JavaScript 関数は、jQuery を使用して"アドレス" HTML テキスト ボックスに "ぼかし" イベントを添付します。 ユーザーがテキスト ボックス内でクリックまたはタブを表示したときに発生する "フォーカス" イベントを聞いたことがあるでしょう。 反対は、ユーザーがテキスト ボックスを終了したときに発生する "ぼかし" イベントです。 上記のイベント ハンドラーは、この場合に緯度と経度のテキスト ボックスの値をクリアし、マップ上の新しい住所の場所をプロットします。 map.js ファイル内で定義したコールバック イベント ハンドラは、指定したアドレスに基づいて仮想アースから返された値を使用して、フォーム上の経度と緯度のテキストボックスを更新します。

そして今、我々は再びアプリケーションを実行し、「ホストディナー」タブをクリックすると、我々は私たちの標準的なDinnerフォーム要素と一緒に表示されるデフォルトのマップが表示されます:

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

住所を入力してタブを離すと、マップが動的に更新されて場所が表示され、イベント ハンドラーは緯度/経度のテキスト ボックスに位置値を設定します。

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

新しいディナーを保存し、編集のために再度開くと、ページが読み込まれるときにマップの場所が表示されます。

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

住所フィールドが変更されるたびに、地図と緯度/経度の座標が更新されます。

これで、マップに Dinner の場所が表示されるので、[緯度] フォームフィールドと [経度] フォームフィールドを非表示のテキスト ボックスから非表示の要素に変更することもできます (住所が入力されるたびにマップが自動的に更新されるため)。 これを行うには、HTML.TextBox() HTML ヘルパーの使用から Html.Hidden() ヘルパー メソッドの使用に切り替えます。

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

そして今、私たちのフォームはもう少しユーザーフレンドリーで、生の緯度/経度を表示しないようにします(それでも各 Dinnerをデータベースに保存しています)。

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>詳細ビューとのマップの統合

作成および編集のシナリオとマップが統合されたので、詳細シナリオと統合してみましょう。 必要なのは% Html.RenderPartial("マップ")を呼び出す&lt;ことだけです。詳細&gt;ビュー内の %

以下は、完全な詳細ビュー(マップ統合を使用)のソースコードがどのようなものかです。

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

そして今、ユーザーが/Dinners/Details/[id]URL に移動すると、夕食の詳細、地図上のディナーの場所(上にマウスを置くとディナーのタイトルとその住所が表示されるプッシュピンが付いています)が表示され、RSVPへのAJAXリンクがあります。

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>データベースとリポジトリでのロケーション検索の実装

AJAX の実装を終了するには、アプリケーションのホーム ページにマップを追加して、ユーザーが近くのディナーをグラフィカルに検索できるようにします。

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

まず、データベースとデータ リポジトリ層内でサポートを実装し、Dinners の場所ベースの半径検索を効率的に実行します。 [SQL 2008 の新しい地理空間機能](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx)を使用してこれを実装することも、代わりに、ここで記事で説明した SQL 関数アプローチを使用することもできます。 [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx)[http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

この手法を実装するには、Visual Studio 内で "サーバー エクスプ ローラー" を開き、 NerdDinner データベースを選択し、その下にある "関数" サブノードを右クリックし、新しい "スカラー値関数" を作成することを選択します。

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

次の DistanceBetween 関数を貼り付けます。

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

次に、"NearestDinners" と呼ぶ新しいテーブル値関数を SQL Server に作成します。

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

この「NearestDinners」テーブル関数は、DistanceBetween ヘルパー関数を使用して、私たちが提供する緯度と経度から100マイル以内のすべてのディナーを返します。

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

この関数を呼び出すには、まず 、\Models ディレクトリ内の NerdDinner.dbml ファイルをダブルクリックして、LINQ to SQL デザイナーを開きます。

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

次に、NearestDinners 関数と DistanceBetween 関数を LINQ to SQL デザイナーにドラッグします。

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

次に、NearestDinner 関数を使用して、指定した場所から 100 マイル以内にある今後のディナーを返す DinnerRepository クラスで"FindByLocation" クエリ メソッドを公開できます。

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>JSON ベースの AJAX 検索アクション メソッドの実装

新しい FindByLocation() リポジトリ メソッドを利用して、マップの設定に使用できる Dinner データのリストを返すコントローラー アクション メソッドを実装します。 このアクションメソッドは、クライアント上のJavaScriptを使用して簡単に操作できるように、JSON(JavaScriptオブジェクト表記法)形式でディナーデータを返すようにします。

これを実装するには、\Controllersディレクトリを右クリックし、&gt;コントローラメニューコマンドを選択して、新しい「SearchController」クラスを作成します。 次に、次のように新しい SearchController クラス内に "SearchByLocation" アクション メソッドを実装します。

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

検索コントローラーの SearchByLocation アクション メソッドは、内部的に近くのディナーのリストを取得するために DinnerRepository の FindByLocation メソッドを呼び出します。 ただし、Dinner オブジェクトをクライアントに直接返すのではなく、代わりに JsonDinner オブジェクトを返します。 JsonDinnerクラスは、ディナープロパティのサブセットを公開します(たとえば、セキュリティ上の理由から、夕食にRSVPを持っている人の名前は開示されません)。 また、ディナーに存在しない RSVPCount プロパティも含まれており、特定のディナーに関連付けられている RSVP オブジェクトの数をカウントして動的に計算されます。

次に、コントローラー基本クラスで Json() ヘルパーメソッドを使用して、JSON ベースのワイヤー形式を使用してディナーのシーケンスを返します。 JSON は、単純なデータ構造を表す標準のテキスト形式です。 次に、2 つの JsonDinner オブジェクトの JSON 形式のリストがアクション メソッドから返された場合の例を示します。

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>jQuery を使用して JSON ベースの AJAX メソッドを呼び出す

これで、NerdDinner アプリケーションのホーム ページを更新して、SearchController の SearchByLocation アクション メソッドを使用する準備ができました。 これを行うには、/Views/ホーム/Index.aspxビューテンプレートを開き、テキストボックス、検索ボタン、マップ、およびdinnerListというdiv&lt;&gt;要素を持つテンプレートを更新します。

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

次に、ページに 2 つの JavaScript 関数を追加できます。

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

最初の JavaScript 関数は、ページが最初に読み込まれたときにマップを読み込みます。 2 番目の JavaScript 関数は、検索ボタンで JavaScript のクリック イベント ハンドラーをワイヤリングします。 ボタンが押されると、Map.jsファイルに追加する FindDinnersGivenLocation() JavaScript 関数を呼び出します。

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

この関数はマップを呼び出します。入力した場所に中央に移動するには、仮想地球コントロール上のFind()を使用します。 仮想アース マップ サービスが戻ると、マップが返されます。Find() メソッドは、最後の引数として渡したコールバック メソッドを呼び出します。

メソッドは、実際の作業が行われる場所です。 jQuery の $.post() ヘルパー メソッドを使用して、SearchController の SearchByLocation() アクション メソッドに対する AJAX 呼び出しを実行します。 これは、$.post() ヘルパーメソッドが完了したときに呼び出されるインライン関数を定義し、SearchByLocation() アクションメソッドから返される JSON 形式のディナー結果は、"ディナー" という変数を使用して渡されます。 その後、返された各ディナーのforeachを行い、ディナーの緯度と経度やその他のプロパティを使用して、地図に新しいピンを追加します。 また、マップの右側にあるディナーの HTML リストにディナーエントリを追加します。 次に、プッシュピンと HTML リストの両方に対してホバー イベントをワイヤアップし、ユーザーがホバーしたときにディナーの詳細が表示されるようにします。

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

そして今、私たちは、アプリケーションを実行し、ホームページにアクセスすると、我々は地図が表示されます。 都市の名前を入力すると、マップは近くの今後のディナーを表示します。

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

夕食の上にマウスを置くと、それについての詳細が表示されます。

バブルまたは HTML リストの右側にある Dinner のタイトルをクリックすると、夕食に移動します。

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>次の手順

これで、NerdDinner アプリケーションのすべてのアプリケーション機能を実装しました。 それでは、自動単体テストを有効にする方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](use-ajax-to-deliver-dynamic-updates.md)
> [次へ](enable-automated-unit-testing.md)
