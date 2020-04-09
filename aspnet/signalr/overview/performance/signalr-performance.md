---
uid: signalr/overview/performance/signalr-performance
title: シグナルパフォーマンス |マイクロソフトドキュメント
author: bradygaster
description: SignalR パフォーマンス
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675719"
---
# <a name="signalr-performance"></a>SignalR パフォーマンス

[パトリック・フレッチャー](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このトピックでは、SignalR アプリケーションのパフォーマンスを設計、測定、および改善する方法について説明します。
>
> ## <a name="software-versions-used-in-this-topic"></a>このトピックで使用するソフトウェアバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - シグナル・バージョン 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>このトピックの以前のバージョン
>
> SignalR の以前のバージョンについては[、SignalR の古いバージョン](../older-versions/index.md)を参照してください。
>
> ## <a name="questions-and-comments"></a>質問とコメント
>
> このチュートリアルを気に入った方法と、ページの下部にあるコメントで改善できる内容についてのフィードバックを残してください。 チュートリアルに直接関連しない質問がある場合は[、ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。

SignalR のパフォーマンスとスケーリングに関する最近のプレゼンテーションについては[、「ASP.NET SignalR を使用したリアルタイム Web](https://channel9.msdn.com/Events/Build/2013/3-502)のスケーリング」を参照してください。

このトピックには、次のセクションが含まれます。

- [設計上の考慮事項](#design)
- [パフォーマンスに関する SignalR サーバーのチューニング](#tuning)
- [パフォーマンスに関する問題のトラブルシューティング](#troubleshooting)
- [SignalR パフォーマンス カウンタの使用](#perfcounters)
- [他のパフォーマンス カウンタの使用](#othercounters)
- [その他のリソース](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>設計上の考慮事項

このセクションでは、SignalR アプリケーションの設計中に実装できるパターンについて説明し、不要なネットワーク トラフィックを生成することによってパフォーマンスが低下しないようにします。

### <a name="throttling-message-frequency"></a>メッセージの頻度の調整

リアルタイム ゲーム アプリケーションなど、高頻度でメッセージを送信するアプリケーションでも、ほとんどのアプリケーションは 1 秒間に数個以上のメッセージを送信する必要はありません。 各クライアントが生成するトラフィックの量を減らすために、メッセージ ループを実装して、メッセージを固定レートより頻繁にキューに入れ、送信することができます (つまり、送信される時間間隔内にメッセージがある場合は、1 秒ごとに一定の数のメッセージが送信されます)。 (クライアントとサーバーの両方から) 一定のレートにメッセージをスロットリングするサンプル アプリケーションについては[、SignalR を使用した高周波リアルタイムを](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)参照してください。

### <a name="reducing-message-size"></a>メッセージ サイズの縮小

シリアル化されたオブジェクトのサイズを小さくすることで、SignalR メッセージのサイズを小さくすることができます。 サーバー コードで、送信する必要のないプロパティを含むオブジェクトを送信する場合は、 属性を使用してそれらのプロパティがシリアル化されないようにします`JsonIgnore`。 プロパティの名前もメッセージに格納されます。プロパティの名前は、`JsonProperty`属性を使用して短縮できます。 次のコード サンプルでは、クライアントに送信されるプロパティを除外する方法と、プロパティ名を短くする方法を示します。

**クライアントに送信されるデータを除外する JsonIgnore 属性を示す .NET サーバー コードと、メッセージ サイズを小さくする JsonProperty 属性**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

クライアント コードの読みやすさや保守性を維持するために、省略されたプロパティ名は、メッセージを受信した後で人間のわかりやすい名前に再マップできます。 次のコード サンプルでは、短縮名を長い名前に再マップする方法の 1 つを示します`reMap`。

**短縮されたプロパティ名を人間が読み取り可能な名前に再マップするクライアント側の JavaScript コード**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

同じ方法を使用して、クライアントからサーバーへのメッセージの名前を短くすることもできます。

メッセージ オブジェクトのメモリ使用量 (つまり、メッセージに使用されるメモリの量) を減らすことで、パフォーマンスを向上させることができます。 たとえば、a の全範囲`int`が必要ない場合は、`short`または`byte`を代わりに使用できます。

メッセージはサーバー メモリのメッセージ バスに格納されるため、メッセージのサイズを小さくすると、サーバーのメモリの問題にも対処できます。

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>パフォーマンスに関する SignalR サーバーのチューニング

次の構成設定を使用して、SignalR アプリケーションのパフォーマンスを向上させるためにサーバーを調整できます。 ASP.NETアプリケーションのパフォーマンスを向上させる方法の一般情報については[、ASP.NETパフォーマンスの向上を](https://msdn.microsoft.com/library/ff647787.aspx)参照してください。

**SignalR 構成設定**

- **既定**の設定では、SignalR は接続ごとに 1,000 個のメッセージを 1 つの接続のハブあたりのメモリに保持します。 大きなメッセージを使用している場合は、メモリの問題が発生し、この値を小さくすることで軽減できます。 この設定は、ASP.NET アプリケーション`Application_Start`のイベント ハンドラー、または自己ホスト型アプリケーション`Configuration`の OWIN スタートアップ クラスのメソッドで設定できます。 次のサンプルでは、使用するサーバー メモリの量を減らすために、アプリケーションのメモリ使用量を削減するために、この値を減らす方法を示します。

    **既定のメッセージ バッファ サイズを減らすStartup.csの .NET サーバー コード**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS 構成設定**

- **アプリケーションあたりの最大同時要求**数 : 同時 IIS 要求の数を増やすと、要求の処理に使用できるサーバー リソースが増えます。 デフォルト値は 5000 です。この設定を増やすには、管理者特権でのコマンド プロンプトで次のコマンドを実行します。

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **アプリケーション プール キュー長**: これは、Http.sys がアプリケーション プールに対してキューに入る要求の最大数です。 キューがいっぱいになると、新しい要求は 503 の 「サービスを利用できません」応答を受信します。 既定値は 1000 です。

    アプリケーションをホストしているアプリケーション プール内のワーカー プロセスのキューの長さを短くすると、メモリ リソースが節約されます。 詳細については、「[アプリケーション プールの管理、チューニング、および構成](https://technet.microsoft.com/library/cc745955.aspx)」を参照してください。

**ASP.NET構成設定**

このセクションには、ファイルで設定できる構成設定が`aspnet.config`含まれています。 このファイルは、プラットフォームに応じて、次の 2 つの場所のいずれかに見られます。

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

SignalR のパフォーマンスを向上させるASP.NET設定には、次のようなものがあります。

- **CPU あたりの最大同時要求**数 : この設定を増やすと、パフォーマンスのボトルネックが軽減される可能性があります。 この設定を増やすには、次の構成設定を`aspnet.config`ファイルに追加します。

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **要求キューの制限**: 接続の合計数がこの設定を`maxConcurrentRequestsPerCPU`超えると、ASP.NETキューを使用して要求の調整が開始されます。 キューのサイズを大きくするには、設定を`requestQueueLimit`増やします。 これを行うには、次の構成設定を (`processModel`ではなく`aspnet.config`)`config/machine.config`ノードに追加します。

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>パフォーマンスに関する問題のトラブルシューティング

このセクションでは、アプリケーションのパフォーマンスのボトルネックを見つける方法について説明します。

### <a name="verifying-that-websocket-is-being-used"></a>WebSocket が使用されていることを確認する

SignalR はクライアントとサーバー間の通信にさまざまなトランスポートを使用できますが、WebSocket はパフォーマンス上の大きな利点を提供するため、クライアントとサーバーがサポートする場合は使用する必要があります。 クライアントとサーバーが WebSocket の要件を満たしているかどうかを確認するには、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。 アプリケーションで使用されているトランスポートを確認するには、ブラウザー開発者ツールを使用し、ログを調べて、接続に使用されているトランスポートを確認します。 Internet Explorer および Chrome でのブラウザ開発ツールの使用については、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>SignalR パフォーマンス カウンタの使用

このセクションでは、パッケージ内にある SignalR パフォーマンス カウンターを有効に`Microsoft.AspNet.SignalR.Utils`して使用する方法について説明します。

### <a name="installing-signalrexe"></a>signalr.exe をインストールしています

パフォーマンス カウンタは、SignalR.exe というユーティリティを使用してサーバーに追加できます。 このユーティリティをインストールするには、次の手順を実行します。

1. Visual Studio で、[**ツール]** > **を選択する ツール NuGet パッケージ マネージャー** > **ソリューションの NuGet パッケージを管理します。**
2. **signalr.utils**を検索し、[インストール] を選択します。

    ![](signalr-performance/_static/image1.png)
3. パッケージをインストールするための使用許諾契約書に同意します。
4. に SignalR.exe が`<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`インストールされます。

### <a name="installing-performance-counters-with-signalrexe"></a>SignalR.exe を使用したパフォーマンス カウンタのインストール

SignalR パフォーマンス カウンターをインストールするには、次のパラメーターを使用して、管理者特権のコマンド プロンプトで SignalR.exe を実行します。

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

SignalR パフォーマンス カウンタを削除するには、管理者特権のコマンド プロンプトで SignalR.exe を次のパラメータを使用して実行します。

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>シグナルパフォーマンスカウンタ

ユーティリティ パッケージは、次のパフォーマンス カウンターをインストールします。 "Total" カウンタは、前回のアプリケーション プールまたはサーバーの再起動以降のイベント数を測定します。

**接続のメトリック**

次のメトリックは、発生した接続の有効期間イベントを測定します。 詳細については、「[接続の有効期間イベントの概要と処理](../guide-to-the-api/handling-connection-lifetime-events.md)」を参照してください。

- **接続接続**
- **再接続された接続**
- **接続が切断されました**
- **接続現在**

**メッセージのメトリック**

次のメトリックは、SignalR によって生成されるメッセージ トラフィックを測定します。

- **受信した接続メッセージの合計**
- **送信された接続メッセージの総数**
- **受信した接続メッセージ/秒**
- **送信された接続メッセージ/秒**

**メッセージ バスメトリック**

次のメトリックは、内部 SignalR メッセージ バス(すべての受信および送信 SignalR メッセージが配置されるキュー)を介してトラフィックを測定します。 メッセージは送信またはブロードキャスト時に**公開されます**。 このコンテキストの**サブスクライバー**は、メッセージ バスのサブスクリプションです。これは、クライアント数とサーバー自体の数に等しいはずです。 **割り当てワーカー**は、アクティブな接続にデータを送信するコンポーネントです。**ビジー状態のワーカー**は、メッセージを積極的に送信しているワーカーです。

- **受信したメッセージ バス メッセージの総数**
- **受信したメッセージ バス メッセージ/秒**
- **メッセージ バス メッセージの公開総数**
- **メッセージ バス メッセージの公開/秒**
- **メッセージ バス サブスクライバ現在**
- **メッセージ バス のサブスクライバーの合計**
- **メッセージ バス のサブスクライバー/秒**
- **メッセージ バス割り当てワーカー**
- **メッセージ バスの使用中のワーカー**
- **メッセージ バス トピックの現在**

**エラーメトリック**

次のメトリックは、SignalR メッセージ トラフィックによって生成されたエラーを測定します。 **ハブまたはハブ**のメソッドを解決できない場合、ハブ解決エラーが発生します。 **ハブ呼び出し**エラーは、ハブ メソッドの呼び出し中にスローされる例外です。 **トランスポート**エラーは、HTTP 要求または応答中に発生する接続エラーです。

- **エラー: すべての合計**
- **エラー: すべて/秒**
- **エラー: ハブの解決の合計**
- **エラー: ハブの解像度/秒**
- **エラー: ハブ呼び出しの合計**
- **エラー: ハブ呼び出し/秒**
- **エラー: トランスポート合計**
- **エラー: トランスポート/秒**

<a id="scaleout_metrics"></a>

**スケールアウトメトリック**

次のメトリックは、スケールアウト プロバイダーによって生成されたトラフィックとエラーを測定します。 このコンテキストの**ストリーム**は、スケールアウト プロバイダーによって使用されるスケール単位です。これは、SQL Server が使用されている場合はテーブル、サービス バスを使用する場合はトピック、Redis が使用されている場合はサブスクリプションです。 各ストリームは、順序付けられた読み取りおよび書き込み操作を保証します。単一ストリームは潜在的なスケールのボトルネックであるため、ストリームの数を増やしてそのボトルネックを減らすことができます。 複数のストリームを使用する場合、SignalR は、特定の接続から送信されたメッセージが順番に送信されるように、これらのストリームにメッセージを自動的に配布 (シャード) します。

[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)設定は、SignalR によって維持されるスケールアウト送信キューの長さを制御します。 この値を 0 より大きい値に設定すると、送信キュー内のすべてのメッセージが、構成済みのメッセージング・バックプレーンに一度に 1 つずつ送信されます。 キューのサイズが構成された長さを超えた場合、キュー内のメッセージ数が設定値より少なくなるまで、送信の後続の呼び出しは[InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx)ですぐに失敗します。 実装されたバックプレーンは一般的に独自のキューイングまたはフロー制御を持つため、キューイングはデフォルトで無効になっています。 SQL Server の場合、接続プールは、一度に送信される回数を効果的に制限します。

既定では、SQL Server と Redis に 1 つのストリームのみが使用され、サービス バスには 5 つのストリームが使用され、キューイングは無効になっていますが、SQL Server とサービス バスの構成を使用してこれらの設定を変更できます。

**SQL Server バックプレーンのテーブル数とキューの長さを構成するための .NET サーバー コード**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**Service Bus バックプレーンのトピック数とキュー長を構成するための .NET サーバー コード**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

**バッファリング**ストリームは、障害が発生した状態に入ったストリームです。ストリームが障害状態になると、ストリームが障害を発生しなくなるまで、バックプレーンに送信されるすべてのメッセージは直ちに失敗します。 **送信キューの長さは**、投稿済みでまだ送信されていないメッセージの数です。

- **スケールアウト メッセージ バス メッセージの受信/秒**
- **スケールアウト ストリームの合計**
- **スケールアウト ストリームが開いている**
- **スケールアウト ストリームのバッファリング**
- **スケールアウト エラーの合計**
- **スケールアウト エラー/秒**
- **スケールアウト送信キューの長さ**

これらのカウンタの測定方法の詳細については、「 [Azure Service Bus を使用した SignalR スケールアウト](scaleout-with-windows-azure-service-bus.md)」を参照してください。

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>他のパフォーマンス カウンタの使用

次のパフォーマンス カウンタは、アプリケーションのパフォーマンスを監視する場合にも役立ちます。

**メモリ**

- .NET CLR\\メモリ # すべてのヒープのバイト数 (w3wp の場合)

**ASP.NET**

- ASP.NET\要求現在
- ASP.NET\キューに入れられます
- ASP.NET\拒否されました

**Cpu**

- プロセッサ情報\プロセッサ時間

**TCP/IP**

- TCPv6/接続が確立されました
- TCPv4/接続が確立されました

**ウェブサービス**

- Web サービス\現在の接続
- Web サービス\最大接続数

**スレッド**

- 現在の論理スレッドの\\.NET CLR ロックおよびスレッド数
- 現在の物理スレッドの\\.NET CLR ロックとスレッド数

<a id="otherresources"></a>

## <a name="other-resources"></a>その他のリソース

パフォーマンスの監視とチューニングASP.NETの詳細については、以下のトピックを参照してください。

- [ASP.NET のパフォーマンスの概要](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [IIS 7.5、IIS 7.0、および IIS 6.0 でのASP.NETスレッドの使用](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;アプリケーションプール&gt;要素 (Web 設定)](https://msdn.microsoft.com/library/dd560842.aspx)
