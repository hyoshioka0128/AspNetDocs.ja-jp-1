---
uid: signalr/overview/getting-started/introduction-to-signalr
title: シグナルR の概要 |マイクロソフトドキュメント
author: bradygaster
description: この記事では、SignalR とは何か、および作成するために設計されたソリューションの一部について説明します。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675941"
---
# <a name="introduction-to-signalr"></a>SignalR 入門

[パトリック・フレッチャー](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> この記事では、SignalR とは何か、および作成するために設計されたソリューションの一部について説明します。 
> 
> ## <a name="questions-and-comments"></a>質問とコメント
> 
> このチュートリアルを気に入った方法と、ページの下部にあるコメントで改善できる内容についてのフィードバックを残してください。 チュートリアルに直接関連しない質問がある場合は[、ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)に投稿できます。

## <a name="what-is-signalr"></a>シグナルとは何ですか?

ASP.NET SignalR は、アプリケーションにリアルタイム Web 機能を追加するプロセスを簡略化するASP.NET開発者向けのライブラリです。 リアルタイム Web 機能とは、サーバーコードが新しいデータを要求するのを待つ代わりに、接続されたクライアントにコンテンツを即座にプッシュする機能です。

SignalR を使用すると、ASP.NETアプリケーションにあらゆる種類の "リアルタイム" Web 機能を追加できます。 チャットは例としてよく使われますが、もっと多くのことを行うことができます。 ユーザーが Web ページを更新して新しいデータを表示したり、ページが新しいデータを取得するために[長いポーリング](http://en.wikipedia.org/wiki/Push_technology#Long_polling)を実装したりするときはいつでも、SignalR を使用する候補になります。 例としては、ダッシュボードと監視アプリケーション、共同アプリケーション (ドキュメントの同時編集など)、ジョブの進捗状況の更新、リアルタイムフォームなどがあります。

SignalR は、リアルタイム ゲームなど、サーバーからの高周波更新を必要とするまったく新しい種類の Web アプリケーションも有効にします。

SignalR は、クライアント ブラウザー (およびその他のクライアント プラットフォーム) で JavaScript 関数を呼び出すサーバーからクライアントへのリモート プロシージャ コール (RPC) を作成するための簡単な API をサーバー側の .NET コードから提供します。 SignalR には、接続管理用の API (接続イベントや接続解除イベントなど) や、接続のグループ化も含まれています。

![SignalR を使用したメソッドの呼び出し](introduction-to-signalr/_static/image1.png)

SignalR では、自動的に接続管理が処理され、ユーザーは、チャットルームのように、同時に接続されているすべてのクライアントにメッセージをブロードキャストすることができます。 また、特定のクライアントにメッセージを送信することもできます。 クライアントとサーバー間の接続は、通信ごとに再確立される従来の HTTP 接続とは異なり、永続的なものです。

SignalR は、サーバー コードがリモート プロシージャ コール (RPC) を使用してブラウザーのクライアント コードを呼び出すことができる 、Web 上で一般的な要求と応答モデルではなく、"サーバー プッシュ" 機能をサポートします。

SignalR アプリケーションは、組み込みプロバイダーとサード パーティ製のスケールアウト プロバイダーを使用して、数千のクライアントにスケール アウトできます。

組み込みプロバイダーには、次のものがあります。
* [Service Bus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

サードパーティのプロバイダには次のものがあります。
* [Nキャッシュ](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).

SignalR はオープンソースで[、GitHub](https://github.com/signalr)を通じてアクセスできます。

## <a name="signalr-and-websocket"></a>シグナルとウェブソケット

SignalR は、新しい WebSocket トランスポートを使用して、必要に応じて古いトランスポートにフォールバックします。 WebSocket を直接使ってアプリを記述することは確かに可能ですが、SignalR を使用すると、実装する必要のある多くの機能が既に実行されていることを意味します。 最も重要なことは、これは、古いクライアント用に別のコード パスを作成する必要なく、WebSocket を利用するようにアプリをコーディングできることを意味します。 SignalR は、基になるトランスポートの変更をサポートするように更新されるため、WebSocket のバージョン間で一貫性のあるインターフェイスをアプリケーションに提供するため、WebSocket の更新を心配する必要がなくなります。

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>トランスポートとフォールバック

SignalR は、クライアントとサーバー間でリアルタイムの作業を行うために必要なトランスポートの一部を抽象化します。 SignalR 接続は HTTP として開始され、使用可能な場合は WebSocket 接続に昇格されます。 WebSocket は、サーバー メモリを最も効率的に使用し、遅延が最も低く、最も基になる機能 (クライアントとサーバー間の全二重通信など) を備えていますが、最も厳しい要件もあります。 これらの要件が満たされない場合、SignalR は他のトランスポートを使用して接続を試みます。

### <a name="html-5-transports"></a>HTML 5 トランスポート

これらのトランスポートは、 HTML [5](http://en.wikipedia.org/wiki/HTML5)のサポートに依存します。 クライアントブラウザがHTML 5標準をサポートしていない場合は、古いトランスポートが使用されます。

- **WebSocket** (サーバーとブラウザーの両方が Websocket をサポートできることを示している場合)。 WebSocket は、クライアントとサーバー間の真の永続的な双方向接続を確立する唯一のトランスポートです。 ただし、WebSocket には最も厳しい要件もあります。それは完全にマイクロソフトのインターネットエクスプローラ、グーグルクローム、およびMozilla Firefoxの最新バージョンでのみ完全にサポートされており、オペラやサファリなどの他のブラウザで部分的な実装のみを持っています。
- **サーバー送信イベント**、 イベント ソースとも呼ばれます (ブラウザーがサーバー送信イベントをサポートしている場合は、基本的には Internet Explorer 以外のすべてのブラウザーです)。

### <a name="comet-transports"></a>彗星輸送

次のトランスポートは、クライアントが特に要求せずにクライアントにデータをプッシュするためにサーバーが使用できる、ブラウザーまたは他のクライアントが長い HTTP 要求を保持する[Comet](http://en.wikipedia.org/wiki/Comet_(programming)) Web アプリケーション モデルに基づいています。

- **フォーエバーフレーム**(インターネットエクスプローラのみ)。 Forever Frame は、完了していないサーバー上のエンドポイントに要求を行う非表示の IFrame を作成します。 その後、サーバーは、直ちに実行されるスクリプトをクライアントに送信し続け、サーバー間の一方向のリアルタイム接続を提供します。 クライアントからサーバーへの接続は、サーバーからクライアントへの接続から別々の接続を使用し、標準の HTTP 要求と同様に、送信する必要があるデータごとに新しい接続が作成されます。
- **Ajax ロングポーリング**. ロングポーリングでは、永続的な接続は作成されませんが、代わりに、サーバーが応答するまで開いたままの要求でサーバーをポーリングし、その時点で接続が閉じ、新しい接続が直ちに要求されます。 これにより、接続がリセットされる間に、ある程度の待機時間が発生する可能性があります。

どの構成でどのトランスポートがサポートされるのかの詳細については、「[サポートされるプラットフォーム](supported-platforms.md)」を参照してください。

### <a name="transport-selection-process"></a>輸送選択プロセス

次の一覧は、SignalR が使用するトランスポートを決定するために使用する手順を示しています。

1. ブラウザが Internet Explorer 8 以前の場合は、ロングポーリングが使用されます。
2. JSONP が構成されている場合 (つまり`jsonp`、接続の開始時`true`にパラメーターが設定されている場合)、ロングポーリングが使用されます。
3. クロスドメイン接続が行われている場合 (つまり、SignalR エンドポイントがホスティング ページと同じドメインにない場合)、次の条件が満たされている場合は WebSocket が使用されます。

   - クライアントは CORS (クロスオリジンリソース共有) をサポートしています。 CORS をサポートするクライアントの詳細については[、caniuse.comの CORS](http://www.caniuse.com/CORS)を参照してください。
   - クライアントは Web ソケットをサポートしています
   - サーバーは Web ソケットをサポートしています

     これらの条件のいずれかが満たされない場合は、ロングポーリングが使用されます。 クロスドメイン接続の詳細については、クロス[ドメイン接続を確立する方法を](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)参照してください。
4. JSONP が構成されておらず、接続がクロスドメインでない場合、クライアントとサーバーの両方がサポートしている場合は WebSocket が使用されます。
5. クライアントまたはサーバーのいずれかが WebSocket をサポートしていない場合、サーバー送信イベントが使用可能な場合は使用されます。
6. サーバー送信イベントが使用できない場合は、フォーエバーフレームが試行されます。
7. フォーエバーフレームに障害が発生した場合は、ロングポーリングが使用されます。

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>トランスポートの監視

ハブでログを有効にし、ブラウザーでコンソール ウィンドウを開くと、アプリケーションが使用しているトランスポートを確認できます。

ブラウザーでハブのイベントのログ記録を有効にするには、クライアント アプリケーションに次のコマンドを追加します。

`$.connection.hub.logging = true;`

- Internet Explorer で、F12 キーを押して開発者ツールを開き、[コンソール] タブをクリックします。

    ![インターネット エクスプローラのコンソール](introduction-to-signalr/_static/image2.png)
- Chrome で、Ctrl キーを押しながら Shift キーを押しながら J キーを押してコンソールを開きます。

    ![グーグルクロームのコンソール](introduction-to-signalr/_static/image3.png)

コンソールを開いてログを記録すると、SignalR によって使用されているトランスポートを確認できます。

![WebSocket トランスポートを示すインターネット エクスプローラのコンソール](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>トランスポートの指定

トランスポートのネゴシエーションには、一定の時間とクライアント/サーバーリソースが必要です。 クライアント機能がわかっている場合は、クライアント接続の開始時にトランスポートを指定できます。 次のコード スニペットは、クライアントが他のプロトコルをサポートしていない場合に使用される Ajax ロング ポーリング トランスポートを使用して接続を開始する方法を示しています。

`connection.start({ transport: 'longPolling' });`

クライアントが特定のトランスポートを順番に試す場合は、フォールバック順序を指定できます。 次のコード スニペットは、WebSocket を試してみて、それを失敗して、ロング ポーリングに直接行くことを示しています。

`connection.start({ transport: ['webSockets','longPolling'] });`

トランスポートを指定するための文字列定数は、次のように定義されます。

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>接続とハブ

SignalR API には、クライアントとサーバー間の通信用の 2 つのモデルが含まれています: 永続的な接続とハブ。

接続は、単一受信者、グループ化、またはブロードキャスト メッセージを送信するための単純なエンドポイントを表します。 永続接続 API (PersistentConnection クラスによって .NET コードで表される) は、SignalR が公開する低レベルの通信プロトコルに開発者が直接アクセスすることを許可します。 接続通信モデルを使用すると、Windows コミュニケーション 基盤などの接続ベースの API を使用した開発者にはなじみ深いものです。

ハブは、クライアントとサーバーが互いに直接メソッドを呼び出すことができる、接続 API に基づいて構築されたより高レベルのパイプラインです。 SignalR は、マシン境界を越えてのディスパッチを魔法のように処理し、クライアントがローカル メソッドと同じくらい簡単にサーバー上のメソッドを呼び出すことを可能にします。 Hubs 通信モデルを使用することは、.NET リモート処理などのリモート呼び出し API を使用した開発者にとってなじみ深いものです。 ハブを使用すると、厳密に型指定されたパラメーターをメソッドに渡して、モデル バインドを有効にすることもできます。

### <a name="architecture-diagram"></a>アーキテクチャの図

次の図は、ハブ、永続的接続、およびトランスポートに使用される基盤となるテクノロジの関係を示しています。

![API、トランスポート、およびクライアントを示す SignalR アーキテクチャ図](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>ハブの仕組み

サーバー側コードがクライアント上のメソッドを呼び出すと、呼び出されるメソッドの名前とパラメーターを含むアクティブなトランスポートを介してパケットが送信されます (オブジェクトがメソッド パラメーターとして送信されると、JSON を使用してシリアル化されます)。 クライアントは、クライアント側のコードで定義されたメソッドにメソッド名を一致します。 一致する場合、クライアント メソッドは逆シリアル化されたパラメーター データを使用して実行されます。

メソッド呼び出しは[、Fiddler](http://fiddler2.com/)などのツールを使用して監視できます。 次の図は、Fiddler のログ ペインで SignalR サーバーから Web ブラウザー クライアントに送信されるメソッド呼び出しを示しています。 メソッド呼び出しは、 という`MoveShapeHub`ハブから送信され、呼び出されるメソッド`updateShape`が呼び出されます。

![SignalR トラフィックを示すフィドラー ログのビュー](introduction-to-signalr/_static/image6.png)

この例では、ハブ名は`H`パラメーターで識別されます。メソッド名は`M`パラメーターで識別され、メソッドに送信されるデータは`A`パラメーターで識別されます。 このメッセージを生成したアプリケーションは、[高周波リアルタイム](tutorial-high-frequency-realtime-with-signalr.md)チュートリアルで作成されます。

### <a name="choosing-a-communication-model"></a>通信モデルの選択

ほとんどのアプリケーションでは、Hubs API を使用する必要があります。 接続 API は、次の状況で使用できます。

- 実際に送信されるメッセージの形式を指定する必要があります。
- 開発者は、リモート呼び出しモデルではなく、メッセージングとディスパッチ モデルを使用することを好みます。
- SignalR を使用するために、メッセージング モデルを使用する既存のアプリケーションが移植されています。
