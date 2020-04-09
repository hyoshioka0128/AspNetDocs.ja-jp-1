---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'チュートリアル: SignalR 2 を使用したサーバー ブロードキャスト |マイクロソフトドキュメント'
author: tdykstra
description: このチュートリアルでは、SignalR 2 を使用してサーバー ブロードキャスト機能を提供する web アプリケーションASP.NET作成する方法を示します。
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675725"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>チュートリアル: SignalR 2 を使用したサーバー ブロードキャスト

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

このチュートリアルでは、SignalR 2 を使用してサーバー ブロードキャスト機能を提供する web アプリケーションASP.NET作成する方法を示します。 サーバー ブロードキャストとは、サーバーがクライアントに送信された通信を開始することを意味します。

このチュートリアルで作成するアプリケーションは、サーバー ブロードキャスト機能の一般的なシナリオである株式のティッカーをシミュレートします。 定期的に、サーバーはランダムに株価を更新し、接続されているすべてのクライアントに更新をブロードキャストします。 ブラウザでは、**変更**列と列の番号と**%** 記号が、サーバーからの通知に応じて動的に変化します。 同じ URL に対して他のブラウザーを開くと、同じデータと同じ変更が同時に表示されます。

![ウェブを作成する](tutorial-server-broadcast-with-signalr/_static/image1.png)

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * プロジェクトを作成する
> * サーバー コードを設定する
> * サーバー コードを確認する
> * クライアント コードを設定する
> * クライアント コードを確認する
> * アプリケーションをテストする
> * ログの有効化

> [!IMPORTANT]
> アプリケーションのビルド手順を実行しない場合は、新しい空のASP.NET Web アプリケーション プロジェクトに SignalR.Sample パッケージをインストールできます。 このチュートリアルの手順を実行せずに NuGet パッケージをインストールする場合は *、readme.txt*ファイルの指示に従う必要があります。 パッケージを実行するには、インストールされたパッケージ内のメソッドを呼び出す`ConfigureSignalR`OWIN スタートアップ クラスを追加する必要があります。 OWIN スタートアップ クラスを追加しないと、エラーが表示されます。 この記事の[「StockTicker サンプルのインストール](#install-the-stockticker-sample)」セクションを参照してください。

## <a name="prerequisites"></a>前提条件

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) と **ASP.NET および開発**ワークロード。

## <a name="create-the-project"></a>プロジェクトを作成する

このセクションでは、Visual Studio 2017 を使用して空のASP.NET Web アプリケーションを作成する方法を示します。

1. Visual Studio で、ASP.NET Web アプリケーションを作成します。

    ![ウェブを作成する](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. [**新しいASP.NET Web アプリケーション - SignalR.StockTicker]** ウィンドウで、[**空]** を選択したままにして **、[OK] を選択します**。

## <a name="set-up-the-server-code"></a>サーバー コードを設定する

このセクションでは、サーバー上で実行されるコードを設定します。

### <a name="create-the-stock-class"></a>ストック クラスの作成

まず、ストックに関する情報を保存および送信するために使用する*Stock*モデル クラスを作成します。

1. **ソリューション エクスプローラ**で、プロジェクトを右クリックし、[**Add** > **クラス**の追加] を選択します。

1. クラスに*Stock*という名前を付け、プロジェクトに追加します。

1. *Stock.cs*ファイル内のコードを次のコードで置き換えます。

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    株式の作成時に設定する 2 つのプロパティは`Symbol`、たとえば、マイクロソフトの MSFT と`Price`です。 その他のプロパティは`Price`、設定する方法とタイミングによって異なります。 初めて 設定`Price`すると、値が`DayOpen`に反映されます。 その後、 を設定`Price`すると、 と の`Change`差`PercentChange``Price`に基づいて プロパティ値と`DayOpen`プロパティ値が計算されます。

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>ストックティッカーハブクラスとストックティッカークラスを作成する

SignalR ハブ API を使用して、サーバーとクライアント間の対話を処理します。 SignalR`StockTickerHub``Hub`クラスから派生したクラスは、クライアントからの受信接続とメソッド呼び出しを処理します。 また、在庫データを更新してオブジェクトを実行`Timer`する必要もあります。 オブジェクト`Timer`は、クライアント接続に関係なく、価格の更新を定期的にトリガーします。 ハブは一時的であるため`Hub`、これらの関数をクラスに入れることはできません。 このアプリは、`Hub`クライアントからサーバーへの接続や呼び出しなど、ハブ上の各タスクのクラス インスタンスを作成します。 したがって、在庫データを保持し、価格を更新し、価格の更新をブロードキャストするメカニズムは、別のクラスで実行する必要があります。 クラス`StockTicker`に名前を付けます。

![ストックティッカーからの放送](tutorial-server-broadcast-with-signalr/_static/image3.png)

`StockTicker`クラスのインスタンスをサーバー上で実行する必要があるのは 1 つのみなので、各`StockTickerHub`インスタンスからシングルトン`StockTicker`インスタンスへの参照を設定する必要があります。 この`StockTicker`クラスは、ストック データを持ち、更新をトリガーしますが`StockTicker`、クラスではないため、クライアント`Hub`にブロードキャストする必要があります。 クラス`StockTicker`は SignalR ハブ接続コンテキスト オブジェクトへの参照を取得する必要があります。 その後、SignalR 接続コンテキスト オブジェクトを使用してクライアントにブロードキャストできます。

#### <a name="create-stocktickerhubcs"></a>StockTickerHub.csの作成

1. **ソリューション エクスプローラ**で、プロジェクトを右クリックし、[**Add** > **新しい項目**の追加] を選択します。

1. [**新しい項目の追加 - SignalR.StockTicker]** で、[**インストール済みの** > **Visual C#** > **Web** > **SignalR]** を選択し **、[SignalR ハブ クラス (v2)]** を選択します。

1. クラスに*名前を付け*、プロジェクトに追加します。

    この手順では *、StockTickerHub.cs*クラス ファイルを作成します。 同時に、SignalR をサポートするスクリプト ファイルとアセンブリ参照のセットをプロジェクトに追加します。

1. *StockTickerHub.cs*ファイル内のコードを次のコードで置き換えます。

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. ファイルを保存します。

アプリは[、ハブ](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)クラスを使用して、クライアントがサーバーで呼び出すことができるメソッドを定義します。 1 つのメソッドを定義しています: `GetAllStocks()`。 クライアントが最初にサーバーに接続すると、このメソッドを呼び出して、現在の価格ですべての株式のリストを取得します。 このメソッドは、メモリからデータを`IEnumerable<Stock>`返すため、同期的に実行して戻ることができます。

データベース検索や Web サービス呼び出しなど、待機を伴う何かを行ってメソッドがデータを取得する必要がある`Task<IEnumerable<Stock>>`場合は、非同期処理を有効にする戻り値として指定します。 詳細については[、「signalR Hubs API ガイドASP.NET - サーバー - 非同期で実行する場合」を](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)参照してください。

この`HubName`属性は、アプリがクライアント上の JavaScript コードでハブを参照する方法を指定します。 この属性を使用しない場合、クライアントのデフォルト名は、クラス名の camelCase バージョンです`stockTickerHub`。

`StockTicker`クラスを作成するときに後で説明したように、アプリは静的`Instance`プロパティにそのクラスのシングルトン インスタンスを作成します。 そのシングルトン インスタンス`StockTicker`は、接続または切断するクライアントの数に関係なくメモリ内にあります。 このインスタンスは、メソッド`GetAllStocks()`が現在のストック情報を返すために使用するものです。

#### <a name="create-stocktickercs"></a>StockTicker.csの作成

1. **ソリューション エクスプローラ**で、プロジェクトを右クリックし、[**Add** > **クラス**の追加] を選択します。

1. クラスに*名前を付け、* プロジェクトに追加します。

1. *StockTicker.cs*ファイル内のコードを次のコードで置き換えます。

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

すべてのスレッドが StockTicker コードの同じインスタンスを実行するため、StockTicker クラスはスレッドセーフでなければなりません。

### <a name="examine-the-server-code"></a>サーバー コードを確認する

サーバー コードを調べると、アプリの動作を理解しやすくなります。

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>シングルトン インスタンスを静的フィールドに格納する

このコードは、クラスの`_instance`インスタンスを使用してプロパティ`Instance`をバックする静的フィールドを初期化します。 コンストラクターはプライベートであるため、アプリケーションで作成できるクラスの唯一のインスタンスです。 アプリは、フィールドに[遅延初期化](/dotnet/framework/performance/lazy-initialization)を`_instance`使用します。 パフォーマンス上の理由ではありません。 インスタンスの作成がスレッド セーフであることを確認します。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

クライアントがサーバーに接続するたびに、別のスレッドで実行されている StockTickerHub クラスの新しいインスタンスは、クラスで先に説明したように、`StockTicker.Instance`静的プロパティから StockTicker シングルトン`StockTickerHub`インスタンスを取得します。

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>コンカレントディクショナリへのストックデータの保存

コンストラクターは、いくつかのサンプル`_stocks`ストックデータを使用してコレクションを初期化`GetAllStocks`し、ストックを返します。 前に説明したように、この株式のコレクションは、クライアント`StockTickerHub.GetAllStocks`が呼び出すことができるクラスの`Hub`サーバー メソッドである によって返されます。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

ストック コレクションは、スレッド セーフの[同時ディクショナリ](https://msdn.microsoft.com/library/dd287191.aspx)型として定義されます。 代わりに[、Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx)オブジェクトを使用して、ディクショナリを変更するときに明示的にロックすることもできます。

このサンプル アプリケーションでは、アプリケーション データをメモリに格納し、アプリケーションがインスタンスを破棄するときにデータを失うことは問題です`StockTicker`。 実際のアプリケーションでは、データベースのようなバックエンド データ ストアを操作します。

#### <a name="periodically-updating-stock-prices"></a>株価の定期的な更新

コンストラクタは、株価を`Timer`ランダムに更新するメソッドを定期的に呼び出すオブジェクトを起動します。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer`を`UpdateStockPrices`呼び出し、state パラメーターで null を渡します。 価格を更新する前に、アプリはオブジェクトにロック`_updateStockPricesLock`を取ります。 コードは、別のスレッドが既に価格を更新しているかどうかをチェックし、`TryUpdateStockPrice`リスト内の各株式を呼び出します。 この`TryUpdateStockPrice`メソッドは、株価を変更するかどうか、および変更する金額を決定します。 株価が変わると、アプリは、すべての`BroadcastStockPrice`接続されたクライアントに株価の変更をブロードキャストするために呼び出します。

スレッド`_updatingStockPrices`セーフであることを確認するために[volatile](https://msdn.microsoft.com/library/x13ttww7.aspx)として指定されたフラグ。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

実際のアプリケーションでは、`TryUpdateStockPrice`メソッドは、価格を検索する Web サービスを呼び出します。 このコードでは、アプリはランダムな変更を行うために乱数ジェネレーターを使用します。

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>StockTicker クラスがクライアントにブロードキャストできるように SignalR コンテキストを取得する

価格の変更は`StockTicker`オブジェクトで発生するため、接続されているすべてのクライアントでメソッドを`updateStockPrice`呼び出す必要があるオブジェクトです。 `Hub`クラスでは、クライアント メソッドを呼び出すための API`StockTicker`がありますが、`Hub`クラスから派生したものではなく、オブジェクトへの参照もありません`Hub`。 接続されたクライアントにブロードキャストするには、`StockTicker`クラスは`StockTickerHub`クラスの SignalR コンテキスト インスタンスを取得し、それを使用してクライアントのメソッドを呼び出す必要があります。

コードは、シングルトン クラス インスタンスを作成し、その参照をコンストラクターに渡し、コンストラクターがプロパティに配置するときに SignalR コンテキストへの参照`Clients`を取得します。

コンテキストを一度だけ取得する理由は 2 つありますが、コンテキストの取得はコストのかかる作業であり、一度取得すると、アプリがクライアントに送信されるメッセージの意図した順序を確実に維持します。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

コンテキストの`Clients`プロパティを取得し、`StockTickerClient`プロパティに配置すると、クラスと同じように見えるクライアント メソッドを呼び出すコードを`Hub`記述できます。 たとえば、すべてのクライアントにブロードキャストするには、 を書`Clients.All.updateStockPrice(stock)`くことができます。

呼`updateStockPrice`び出しているメソッドはまだ存在`BroadcastStockPrice`しません。 後でクライアントで実行するコードを記述するときに追加します。 `updateStockPrice`ここで`Clients.All`参照できるのは、動的であるため、アプリが実行時に式を評価することを意味します。 このメソッド呼び出しが実行されると、SignalR はメソッド名とパラメーター値をクライアントに送信し、クライアントに という`updateStockPrice`名前のメソッドがある場合、アプリはそのメソッドを呼び出してパラメーター値を渡します。

`Clients.All`は、すべてのクライアントに送信することを意味します。 SignalR には、送信先のクライアントまたはクライアント グループを指定するその他のオプションが用意されています。 詳細については、「[ハブ接続コンテキスト](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)」を参照してください。

### <a name="register-the-signalr-route"></a>シグナル R ルートを登録する

サーバーは、どの URL をインターセプトして SignalR に送信するかを知る必要があります。 これを行うには、OWIN スタートアップ クラスを追加します。

1. **ソリューション エクスプローラ**で、プロジェクトを右クリックし、[**Add** > **新しい項目**の追加] を選択します。

1. [**新しい項目の追加 - SignalR.StockTicker]** **で 、[インストール済みの** > **Visual C#** > **Web]** を選択し **、[OWIN スタートアップ クラス**] を選択します。

1. クラスに*Startup*という名前を付け **、[OK]** をクリックします。

1. *Startup.cs*ファイルの既定のコードを次のコードで置き換えます。

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

これで、サーバー コードの設定が完了しました。 次のセクションでは、クライアントを設定します。

## <a name="set-up-the-client-code"></a>クライアント コードを設定する

このセクションでは、クライアントで実行されるコードを設定します。

### <a name="create-the-html-page-and-javascript-file"></a>HTML ページと Java スクリプト ファイルを作成する

HTML ページにデータが表示され、JavaScript ファイルがデータを整理します。

#### <a name="create-stocktickerhtml"></a>ストックティッカーを作成します。

最初に、HTML クライアントを追加します。

1. **ソリューション エクスプローラ**で、プロジェクトを右クリックし **、[HTML ページ**の**追加** > ] を選択します。

1. ファイルに*StockTicker という名前を付け***、[OK]** を選択します。

1. *StockTicker.html*ファイルの既定のコードを次のコードに置き換えます。

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    HTML では、5 つの列、ヘッダー行、および 5 つの列すべてにまたがる単一のセルを持つデータ行を持つテーブルが作成されます。 データ行は"読み込み中."を示しています。アプリが起動すると、一時的に。 JavaScript コードは、その行を削除し、サーバーから取得したストック データを含むその行を追加します。

    スクリプト タグは次の項目を指定します。

    * jQuery スクリプト ファイル。

    * SignalR コア スクリプト ファイル。

    * SignalR プロキシ スクリプト ファイル。

    * 後で作成する StockTicker スクリプト ファイル。

    アプリは、SignalR プロキシ スクリプト ファイルを動的に生成します。 "/signalr/hubs" URL を指定し、ハブ クラスのメソッド (この場合は) のメソッド`StockTickerHub.GetAllStocks`のプロキシ メソッドを定義します。 必要に応じて[、SignalR ユーティリティ](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)を使用してこの JavaScript ファイルを手動で生成できます。 メソッド呼び出しで動的ファイルの作成を`MapHubs`無効にすることを忘れないでください。

1. **ソリューション エクスプローラ**で、[**スクリプト]** を展開します。

    jQuery と SignalR のスクリプト ライブラリは、プロジェクトで表示されます。

    > [!IMPORTANT]
    > パッケージ マネージャーは、SignalR スクリプトの新しいバージョンをインストールします。

1. コード ブロック内のスクリプト参照を、プロジェクト内のスクリプト ファイルのバージョンに対応するように更新します。

1. **ソリューション エクスプローラー**で、 *[ StockTicker.html*] を右クリックし、[**スタート ページとして設定**] を選択します。

#### <a name="create-stocktickerjs"></a>ストックティッカー.jsを作成します。

次に、JavaScript ファイルを作成します。

1. **ソリューション エクスプローラー**で、プロジェクトを右クリックし **、[JavaScript ファイル**の**追加** > ] を選択します。

1. ファイルに*StockTicker という名前を付け***、[OK]** を選択します。

1. 次のコードを*StockTicker.js*ファイルに追加します。

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>クライアント コードを確認する

クライアント コードを調べると、クライアント コードがサーバー コードと対話してアプリを動作させる方法を理解するのに役立ちます。

#### <a name="starting-the-connection"></a>接続の開始

`$.connection`は SignalR プロキシを指します。 コードは、クラスのプロキシへの参照を`StockTickerHub`取得し、変数に`ticker`入れます。 プロキシ名は、`HubName`属性によって設定された名前です。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

すべての変数と関数を定義した後、ファイル内のコードの最後の行は SignalR 関数を呼び出すことによって`start`SignalR 接続を初期化します。 この`start`関数は非同期的に実行され、 [jQuery Deferred オブジェクト](http://api.jquery.com/category/deferred-object/)を返します。 done 関数を呼び出して、アプリが非同期アクションを完了したときに呼び出す関数を指定できます。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>すべての株式を取得する

この`init`関数は、`getAllStocks`サーバー上の関数を呼び出し、サーバーが返す情報を使用してストック テーブルを更新します。 デフォルトでは、メソッド名がサーバー上で pascal で大文字と小文字を区別されていても、クライアントで camelCasing を使用する必要があることに注意してください。 CamelCasing 規則はメソッドにのみ適用され、オブジェクトには適用されません。 たとえば`stock.Symbol`、 および`stock.Price`を参照し、 `stock.symbol` `stock.price`または を参照します。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

このメソッド`init`では`formatStock`、アプリケーションは、`stock`サーバーから受信した各ストック オブジェクトのテーブル行の HTML を作成します`supplant``rowTemplate``stock`。 結果の HTML は、ストック テーブルに追加されます。

> [!NOTE]
> 非同期`start`関数`init`の終了後に実行される`callback`関数として渡すことによって呼び出します。 呼び出`init`し後に別の JavaScript`start`ステートメントとして呼び出した場合、開始関数が接続の確立を完了するのを待たずにすぐに実行されるため、関数は失敗します。 その場合、`init`関数は、アプリがサーバー接続を`getAllStocks`確立する前に関数を呼び出そうとします。

#### <a name="getting-updated-stock-prices"></a>更新された株価の取得

サーバーは、株価を変更すると、接続されたクライアント`updateStockPrice`を呼び出します。 アプリは、サーバーからの呼び出しで使用`stockTicker`できるように、プロキシのクライアント プロパティに関数を追加します。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

この`updateStockPrice`関数は、サーバーから受信したストックオブジェクトを、関数と同じ方法でテーブル行`init`にフォーマットします。 テーブルに行を追加する代わりに、テーブル内のストックの現在の行を検索し、その行を新しい行に置き換えます。

## <a name="test-the-application"></a>アプリケーションをテストする

アプリをテストして、動作していることを確認できます。 すべてのブラウザウィンドウに株価が変動するライブストックテーブルが表示されます。

1. ツールバーで[**スクリプトのデバッグ]** をオンにし、再生ボタンを選択して、デバッグモードでアプリを実行します。

    ![ユーザーがデバッグ モードをオンにし、再生を選択するスクリーンショット。](tutorial-server-broadcast-with-signalr/_static/image4.png)

    ブラウザウィンドウが開き、**ライブストックテーブル**が表示されます。 ストックテーブルには、最初は「読み込み.」が表示されます。ライン、その後、短い時間後に、アプリは、最初の株式データを表示し、株価が変化し始めます。

1. ブラウザから URL をコピーし、他の 2 つのブラウザを開いて、URL をアドレス バーに貼り付けます。

    最初のストック表示は最初のブラウザと同じで、変更は同時に行われます。

1. すべてのブラウザーを閉じ、新しいブラウザーを開き、同じ URL に移動します。

    StockTicker シングルトン オブジェクトは、サーバーで実行し続けました。 **ライブストックテーブル**は、株式が変化し続けたことを示しています。 変更の数値がゼロの初期テーブルは表示されません。

1. ブラウザーを閉じます。

## <a name="enable-logging"></a>ログの有効化

SignalR には、トラブルシューティングを支援するためにクライアントで有効にできるログ機能が組み込まれています。 このセクションでは、ログ記録を有効にし、SignalR が使用している次のトランスポート方法のどれをログが示す例を参照してください。

* [WebSockets](http://en.wikipedia.org/wiki/WebSocket)、IIS 8 および現在のブラウザーでサポートされています。

* [サーバー送信イベント](http://en.wikipedia.org/wiki/Server-sent_events)、 Internet Explorer 以外のブラウザでサポートされています。

* [永遠にフレーム](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)、インターネットエクスプローラでサポートされています。

* [Ajax ロングポーリング](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)、すべてのブラウザでサポートされています。

SignalR は、特定の接続に対して、サーバーとクライアントの両方がサポートする最適なトランスポート方法を選択します。

1. *ストックティッカー.js*を開きます。

1. ファイルの末尾で接続を初期化するコードの直前にログ記録を有効にするには、次の強調表示されたコード行を追加します。

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. **F5 キー**を押してプロジェクトを実行します。

1. ブラウザの開発者ツールウィンドウを開き、コンソールを選択してログを表示します。 新しい接続のトランスポート メソッドをネゴシエートする SignalR のログを表示するには、ページを更新する必要があります。

    * Windows 8 (IIS 8) でインターネット エクスプローラ 10 を実行している場合、トランスポート方法は**WebSockets**です。

    * Windows 7 (IIS 7.5) でインターネット エクスプローラ 10 を実行している場合、トランスポート方法は**iframe**です。

    * Windows 8 (IIS 8) で Firefox 19 を実行している場合、転送方法は**WebSockets**です。

        > [!TIP]
        > Firefox で Firebug アドインをインストールしてコンソール ウィンドウを表示します。

    * Windows 7 (IIS 7.5) で Firefox 19 を実行している場合、トランスポート方法は**サーバー送信**イベントです。

## <a name="install-the-stockticker-sample"></a>ストックティッカーサンプルのインストール

[サンプル](http://nuget.org/packages/microsoft.aspnet.signalr.sample)はストックティッカーアプリケーションをインストールします。 NuGet パッケージには、最初から作成した簡略化されたバージョンよりも多くの機能が含まれています。 チュートリアルのこのセクションでは、NuGet パッケージをインストールし、新機能と、それらを実装するコードを確認します。

> [!IMPORTANT]
> このチュートリアルの前の手順を実行せずにパッケージをインストールする場合は、プロジェクトに OWIN スタートアップ クラスを追加する必要があります。 NuGet パッケージのこの readme.txt ファイルでは、この手順について説明します。

### <a name="install-the-signalrsample-nuget-package"></a>サンプルの NuGet パッケージをインストールします。

1. **ソリューション エクスプローラー**でプロジェクトを右クリックし、**[NuGet パッケージの管理]** を選びます。

1. **NuGet パッケージ マネージャー: SignalR.StockTicker**で **、[ 参照 ]** を選択します。

1. [**パッケージ ソース**] で、[ **nuget.org**] を選択します。

1. 検索ボックスに*SignalR.Sample*と入力**Microsoft.AspNet.SignalR.Sample** > し、[**インストール**] を選択します。

1. **ソリューション エクスプローラー**で*SignalR.Sample*フォルダーを展開します。

    SignalR.Sample パッケージをインストールすると、フォルダーとその内容が作成されました。

1. *SignalR.Sample*フォルダで *、StockTicker.html*を右クリックし、[**スタート ページとして設定]** を選択します。

    > [!NOTE]
    > SignalR.Sample NuGet パッケージをインストールすると、*スクリプト*フォルダーにある jQuery のバージョンが変更される場合があります。 パッケージが*SignalR.Sample*フォルダーにインストールする新しい*StockTicker.html*ファイルは、パッケージがインストールする jQuery バージョンと同期しますが、元の*StockTicker.html*ファイルを再度実行する場合は、最初にスクリプト タグの jQuery 参照を更新する必要があります。

### <a name="run-the-application"></a>アプリケーションの実行

 最初のアプリで見たテーブルには便利な機能がありました。 完全な株式ティッカーアプリケーションは、新しい機能を示しています:株式データと、彼らが上昇し、下落するにつれて色を変更する株式を示す水平スクロールウィンドウ。

1. **F5** キーを押して、アプリを実行します。

     初めてアプリを実行すると、「マーケット」は「閉じている」と、静的なテーブルとスクロールされていないティッカーウィンドウが表示されます。

1. **[オープン マーケット**] を選択します。

    ![ライブティッカーのスクリーンショット。](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * **[ライブストックティッカー** ]ボックスが水平にスクロールし始め、サーバーは定期的に株価の変化をランダムに放送し始めます。

    * 株価が変化するたびに、アプリは**ライブストックテーブル**と**ライブストックティッカー**の両方を更新します。

    * 株式の価格変動がプラスの場合、アプリは、背景が緑色の株式を示しています。

    * 変更が負の場合、アプリは赤い背景でストックを表示します。

1. [**市場を閉じる**] を選択します。

    * テーブルの更新が停止します。

    * ティッカーがスクロールを停止します。

1. **[リセット]** を選択します。

    * すべてのストックデータがリセットされます。

    * アプリは、価格変更が開始される前に、初期状態を復元します。

1. ブラウザから URL をコピーし、他の 2 つのブラウザを開いて、URL をアドレス バーに貼り付けます。

1. 各ブラウザーで、同じデータが同時に動的に更新されます。

1. コントロールのいずれかを選択すると、すべてのブラウザーが同時に同じ方法で応答します。

### <a name="live-stock-ticker-display"></a>ライブストックティッカーディスプレイ

**ライブストックティッカー**表示は、CSSスタイルによって単一行`<div>`にフォーマットされた要素の順序なしリストです。 `<li>`アプリは、テンプレート文字列のプレースホルダーを置き換え、要素を要素に動的に追加することで、テーブルと同じ方法でティ`<li>`ッカーを初期化`<ul>`して更新します。 このアプリでは、jQuery`animate`関数を使用してスクロールして、 内の順序付けされていないリストの左`<div>`余白を変更します。

#### <a name="signalrsample-stocktickerhtml"></a>シグナルラー.サンプルストックティッカー.html

株式銘柄のHTMLコード:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>シグナルラー.サンプルストックティッカー.css

株式証券のCSSコード:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>信号機サンプルシグナル

スクロールさせる jQuery コード:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>クライアントが呼び出すことができるサーバー上の追加メソッド

アプリに柔軟性を追加するために、アプリが呼び出すことができる追加のメソッドがあります。

#### <a name="signalrsample-stocktickerhubcs"></a>シグナル・サンプル・StockTickerHub.cs

この`StockTickerHub`クラスは、クライアントが呼び出すことができる 4 つの追加メソッドを定義します。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

アプリは、`OpenMarket`ページ`CloseMarket``Reset`上部のボタンに応答して 、 を呼び出します。 1 つのクライアントが、すべてのクライアントに即時に伝達される状態の変化をトリガーするパターンを示します。 これらの各メソッドは、市場の状態を`StockTicker`変更する原因となるクラス内のメソッドを呼び出し、新しい状態をブロードキャストします。

#### <a name="signalrsample-stocktickercs"></a>シグナル・サンプル・StockTicker.cs

`StockTicker`クラスでは、アプリは、列挙値を返すプロパティを使用`MarketState`して市場の状態`MarketState`を維持します。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

市場の状態を変更するメソッドのそれぞれは、クラスがスレッドセーフでなければならないの`StockTicker`で、ロックブロック内でそうします。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

このコードがスレッド セーフであることを確認するには、指定`_marketState`された`MarketState``volatile`プロパティをバックするフィールド。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

`BroadcastMarketStateChange`メソッドと`BroadcastMarketReset`メソッドは、クライアントで定義された異なるメソッドを呼び出す点を除いて、既に見た BroadcastStockPrice メソッドに似ています。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>サーバーが呼び出すことができるクライアント上の追加機能

これで`updateStockPrice`、この関数はテーブルとティッカー表示の両方を処理し、`jQuery.Color`赤と緑の色を点滅させるために使用します。

*SignalR.StockTicker.js*の新機能は、市場の状態に基づいてボタンを有効または無効にします。 また、**ライブストックティッカー**水平スクロールを停止または開始します。 多くの関数がに`ticker.client`追加されているため、アプリは[jQuery 拡張関数](http://api.jquery.com/jQuery.extend/)を使用して追加します。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>接続の確立後の追加クライアントセットアップ

クライアントが接続を確立した後、追加の作業を行う必要があります。

* 市場が開いているか閉じているかどうかを調べるので、`marketOpened`適切`marketClosed`なまたは機能を呼び出します。

* ボタンにサーバー メソッド呼び出しをアタッチします。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

サーバー メソッドは、アプリが接続を確立するまでボタンに接続されません。 そのため、コードはサーバーメソッドを呼び出してから利用できません。

## <a name="additional-resources"></a>その他のリソース

このチュートリアルでは、サーバーからすべての接続されたクライアントにメッセージをブロードキャストする SignalR アプリケーションをプログラムする方法を学習しました。 現在、メッセージを定期的にブロードキャストし、任意のクライアントからの通知に応答することができます。 マルチスレッド シングルトン インスタンスの概念を使用して、マルチプレイヤー オンライン ゲームシナリオでサーバーの状態を維持できます。 例については[、SignalR に基づく ShootR ゲームを](https://github.com/NTaylorMullen/ShootR)参照してください。

ピアツーピア通信シナリオを示すチュートリアルについては[、「SignalR の概要」および「SignalR](introduction-to-signalr.md)による[リアルタイム更新](tutorial-high-frequency-realtime-with-signalr.md)」を参照してください。

SignalR の詳細については、次のリソースを参照してください。

* [ASP.NET SignalR](../../index.md)
* [シグナル・プロジェクト](http://signalr.net/)
* [シグナル R の GitHub とサンプル](https://github.com/SignalR/SignalR)
* [シグナルRウィキ](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、次のことを行いました。

> [!div class="checklist"]
> * プロジェクトを作成しました
> * サーバー コードを設定する
> * サーバー コードを調べた
> * クライアント コードを設定する
> * クライアント コードを調べた
> * アプリケーションをテストする
> * 有効なログ記録

次の記事に進み、SignalR 2 を使用するリアルタイム Web アプリケーションの作成方法ASP.NET学んでください。
> [!div class="nextstepaction"]
> [SignalR を使用してリアルタイムの Web アプリを作成する](real-time-web-applications-with-signalr.md)
