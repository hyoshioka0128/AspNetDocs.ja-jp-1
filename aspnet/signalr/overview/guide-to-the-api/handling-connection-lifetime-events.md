---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: SignalR での接続の有効期間イベントの理解と処理 |マイクロソフトドキュメント
author: bradygaster
description: この記事では、Hubs API によって公開されるイベントの使用方法について説明します。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675827"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>SignalR の接続有効期間イベントについて理解し、処理する

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> この記事では、処理できる SignalR 接続、再接続、および切断イベントの概要、および構成可能なタイムアウトとキープアライブ設定について説明します。
>
> この記事では、SignalR と接続の有効期間イベントに関する知識が既にあるものとします。 SignalR の概要については[、「SignalR の概要](../getting-started/introduction-to-signalr.md)」を参照してください。 接続の有効期間イベントの一覧については、次のリソースを参照してください。
>
> - [ハブ クラスで接続の有効期間イベントを処理する方法](hubs-api-guide-server.md#connectionlifetime)
> - [JavaScript クライアントで接続の有効期間イベントを処理する方法](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [NET クライアントで接続の有効期間イベントを処理する方法](hubs-api-guide-net-client.md#connectionlifetime)
>
> ## <a name="software-versions-used-in-this-topic"></a>このトピックで使用するソフトウェアバージョン
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
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

## <a name="overview"></a>概要

このトピックの内容は次のとおりです。

- [接続の有効期間の用語とシナリオ](#terminology)

    - [SignalR 接続、トランスポート接続、および物理接続](#signalrvstransport)
    - [トランスポート切断シナリオ](#transportdisconnect)
    - [クライアント切断のシナリオ](#clientdisconnect)
    - [サーバー切断のシナリオ](#serverdisconnect)
- [タイムアウトとキープアライブの設定](#timeoutkeepalive)

    - [接続タイムアウト](#connectiontimeout)
    - [切断タイムアウト](#disconnecttimeout)
    - [KeepAlive](#keepalive)
    - [タイムアウトとキープアライブの設定を変更する方法](#changetimeout)
- [切断についてユーザーに通知する方法](#notifydisconnect)
- [連続的に再接続する方法](#continuousreconnect)
- [サーバー コードでクライアントを切断する方法](#disconnectclientfromserver)
- [切断の理由の検出](#detectingreasonfordisconnection)

API リファレンストピックへのリンクは、API の .NET 4.5 バージョンに関するトピックです。 .NET 4 を使用している場合は[、API のトピックの .NET 4 バージョンを](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)参照してください。

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>接続の有効期間の用語とシナリオ

SignalR Hub のイベント ハンドラは`OnReconnected`、特定`OnConnected`のクライアント`OnDisconnected`に対しては実行後ではなく、直接実行できます。 切断せずに再接続できる理由は、SignalR で 「接続」という単語が使用される方法が複数あるからである。

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SignalR 接続、トランスポート接続、および物理接続

この記事では *、SignalR 接続*、*トランスポート接続*、および*物理接続*を区別します。

- **SignalR 接続**は、クライアントとサーバー URL の間の論理的な関係を指し、SignalR API によって維持され、接続 ID によって一意に識別されます。 この関係に関するデータは SignalR によって維持され、トランスポート接続を確立するために使用されます。 クライアントが`Stop`メソッドを呼び出したとき、または SignalR が失われたトランスポート接続を再確立しようとしているときにタイムアウト制限に達すると、関係が終了し、SignalR がデータを破棄します。
- **トランスポート接続**とは、クライアントとサーバーの間の論理的な関係を指し、4 つのトランスポート API のいずれかによって維持されます。 SignalR はトランスポート API を使用してトランスポート接続を作成し、トランスポート API は物理ネットワーク接続の存在に依存してトランスポート接続を作成します。 トランスポート接続は、SignalR が終了するか、トランスポート API が物理接続が切断されていることを検出したときに終了します。
- **物理的な接続**とは、クライアント コンピュータとサーバー コンピュータ間の通信を容易にする、物理的なネットワーク リンク (ワイヤー、ワイヤレス信号、ルーターなど) を指します。 トランスポート接続を確立するには物理接続が存在し、SignalR 接続を確立するためにはトランスポート接続を確立する必要があります。 ただし、物理接続を切断しても、このトピックで後述するとおり、トランスポート接続または SignalR 接続がすぐに終了するとは限りません。

次の図では、SignalR 接続はハブ API と PersistentConnection API SignalR レイヤーで表され、トランスポート接続はトランスポート層で表され、物理的な接続はサーバーとクライアント間の線で表されます。

![SignalR アーキテクチャ図](handling-connection-lifetime-events/_static/image1.png)

SignalR クライアント`Start`でメソッドを呼び出すときに、サーバーへの物理的な接続を確立するために必要なすべての情報を SignalR クライアント コードを提供します。 SignalR クライアント コードは、この情報を使用して HTTP 要求を行い、4 つのトランスポート方法のいずれかを使用する物理接続を確立します。 トランスポート接続が失敗した場合やサーバーに障害が発生した場合、クライアントには、同じ SignalR URL への新しいトランスポート接続を自動的に再確立するために必要な情報が残っているため、SignalR 接続はすぐには消えません。 このシナリオでは、ユーザー アプリケーションからの介入は関係なく、SignalR クライアント コードが新しいトランスポート接続を確立するとき、新しい SignalR 接続を開始しません。 SignalR 接続の連続性は、メソッドを呼び出したときに作成される接続 ID が変更されないという`Start`事実に反映されます。

ハブ`OnReconnected`のイベント ハンドラは、トランスポート接続が失われた後に自動的に再確立されたときに実行されます。 イベント`OnDisconnected`ハンドラーは、SignalR 接続の終了時に実行されます。 SignalR 接続は、次のいずれかの方法で終了できます。

- クライアントがメソッドを呼`Stop`び出した場合、停止メッセージがサーバーに送信され、クライアントとサーバーの両方がただちに SignalR 接続を終了します。
- クライアントとサーバー間の接続が失われると、クライアントは再接続を試み、サーバーはクライアントの再接続を待機します。 再接続が失敗し、切断タイムアウト期間が終了した場合、クライアントとサーバーの両方が SignalR 接続を終了します。 クライアントは再接続を停止し、サーバーは SignalR 接続の表現を破棄します。
- `Stop`クライアントがメソッドを呼び出す機会を持たずに実行を停止した場合、サーバーはクライアントが再接続するのを待ち、切断タイムアウト期間が経過した後に SignalR 接続を終了します。
- サーバーが停止すると、クライアントは再接続 (トランスポート接続の再作成) を試み、切断タイムアウト期間が経過した後に SignalR 接続を終了します。

接続に問題がなく、ユーザー アプリケーションがメソッドを呼び出して SignalR`Stop`接続を終了すると、SignalR 接続とトランスポート接続が同じ時間に開始および終了します。 以降のセクションでは、その他のシナリオについて詳しく説明します。

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>トランスポート切断シナリオ

物理接続が遅い場合や、接続が中断される可能性があります。 中断の長さなどの要因によっては、トランスポート接続がドロップされる場合があります。 SignalR は、トランスポート接続の再確立を試みます。 トランスポート接続 API が中断を検出してトランスポート接続をドロップし、SignalR が接続が失われたことをすぐに検出することがあります。 他のシナリオでは、トランスポート接続 API も SignalR も、接続が失われたことをすぐに認識しなくなります。 長いポーリングを除くすべてのトランスポートで、SignalR クライアントは*キープアライブ*という関数を使用して、トランスポート API が検出できない接続の損失をチェックします。 長時間ポーリング接続については、このトピックの後半の[「タイムアウトとキープアライブの設定](#timeoutkeepalive)」を参照してください。

接続が非アクティブの場合、サーバーは定期的にキープアライブ パケットをクライアントに送信します。 この記事が作成された時点で、デフォルトの頻度は 10 秒ごとに設定されます。 これらのパケットをリッスンすることで、クライアントは接続に問題があるかどうかを知ることができます。 キープアライブ パケットが予期したタイミングで受信されない場合、しばらくするとクライアントは、低速や中断などの接続の問題があると見なします。 キープアライブが長時間経過してもまだ受信されない場合、クライアントは接続が切断されたと見なし、再接続を試みます。

次の図は、トランスポート API ですぐに認識されない物理接続に問題がある場合に、一般的なシナリオで発生するクライアント イベントとサーバー イベントを示しています。 この図は、次の状況に適用されます。

- トランスポートは、WebSocket、永遠のフレーム、またはサーバーから送信されるイベントです。
- 物理ネットワーク接続の中断の期間はさまざまです。
- トランスポート API は中断を認識しないため、SignalR はキープアライブ機能に依存してそれらを検出します。

![トランスポート切断](handling-connection-lifetime-events/_static/image2.png)

クライアントが再接続モードに入っても、切断タイムアウトの制限内でトランスポート接続を確立できない場合、サーバーは SignalR 接続を終了します。 その場合、サーバーはハブの`OnDisconnected`メソッドを実行し、クライアントが後で接続する場合に備えて、クライアントに送信する切断メッセージをキューに入れます。 その後、クライアントが再接続すると、disconnect コマンドを受け取り`Stop`、メソッドを呼び出します。 このシナリオでは、`OnReconnected`クライアントが再接続したときに実行されず、クライアント`OnDisconnected`が呼び出`Stop`されたときには実行されません。 次の図は、このシナリオを示しています。

![トランスポートの中断 - サーバー タイムアウト](handling-connection-lifetime-events/_static/image3.png)

クライアントで発生する SignalR 接続の有効期間イベントは次のとおりです。

- `ConnectionSlow`クライアント イベント。

    最後のメッセージまたはキープアライブ ping を受信してから、キープアライブ タイムアウト期間の事前設定された割合が経過したときに発生します。 既定のキープアライブ タイムアウト警告期間は、キープアライブ タイムアウトの 2/3 です。 キープアライブ タイムアウトは 20 秒なので、警告は約 13 秒で発生します。

    デフォルトでは、サーバーはキープアライブ ping を 10 秒ごとに送信し、クライアントは約 2 秒ごとにキープアライブ ping をチェックします (キープアライブ タイムアウト値とキープアライブ タイムアウト警告値の差の 1/3)。

    トランスポート API が切断を認識した場合、キープアライブ タイムアウト警告期間が経過する前に、SignalR に切断が通知される場合があります。 その場合、`ConnectionSlow`イベントは発生せず、SignalR はイベントに直接移動します`Reconnecting`。
- `Reconnecting`クライアント イベント。

    (a) トランスポート API が接続が失われたことを検出した場合、または (b) 最後のメッセージまたはキープアライブ ping が受信されてからキープアライブ・タイムアウト期間が経過した場合に発生します。 SignalR クライアント コードが再接続を試み始めます。 トランスポート接続が失われたときにアプリケーションで何らかのアクションを実行する場合は、このイベントを処理できます。 既定のキープアライブ タイムアウト期間は現在 20 秒です。

    SignalR が再接続モードのときにクライアント コードがハブ メソッドを呼び出そうとすると、SignalR はコマンドの送信を試みます。 ほとんどの場合、そのような試みは失敗しますが、状況によっては成功する可能性があります。 サーバー送信イベント、永遠にフレーム、および長時間ポーリング トランスポートの SignalR は、2 つの通信チャネルを使用します。 受信に使用されるチャネルは、永続的に開かれたチャネルであり、物理的な接続が中断されたときに閉じられるチャネルです。 送信に使用されるチャネルは使用可能なままであるため、物理接続が復元された場合、受信チャネルが再確立される前に、クライアントからサーバーへのメソッド呼び出しが成功する可能性があります。 SignalR が受信に使用されるチャネルを再度開くまで、戻り値は受信されません。
- `Reconnected`クライアント イベント。

    トランスポート接続が再確立されたときに発生します。 ハブ`OnReconnected`内のイベント ハンドラーが実行されます。
- `Closed`クライアント イベント`disconnected`( JavaScript のイベント ) 。

    トランスポート接続が切断された後に SignalR クライアント コードが再接続しようとしている間に切断タイムアウト期間が経過したときに発生します。 デフォルトの切断タイムアウトは 30 秒です。 (このイベントは、メソッドが呼び出されたために`Stop`接続が終了したときにも発生します)。

トランスポート API によって検出されず、キープアライブ のタイムアウト警告期間よりも長い間、サーバーからのキープアライブ ping の受信を遅延しないトランスポート接続の中断は、接続の有効期間イベントが発生しない可能性があります。

一部のネットワーク環境では、意図的にアイドル状態の接続を閉じる、キープアライブ パケットの別の機能は、SignalR 接続が使用中であることをこれらのネットワークに知らせることによって、これを防ぐために役立ちます。 極端な場合、キープアライブ ping のデフォルトの頻度では、接続が閉じられるのを防ぐには十分でない場合があります。 その場合、より頻繁に送信されるようにキープアライブ ping を設定できます。 詳細については、このトピックの後半の「[タイムアウトとキープアライブの設定](#timeoutkeepalive)」を参照してください。

> [!NOTE]
>
> **重要**: ここで説明する一連のイベントは保証されません。 SignalR は、このスキームに従って予測可能な方法で接続の有効期間イベントを発生させようとしますが、ネットワーク イベントの多くのバリエーションと、トランスポート API などの基になる通信フレームワークがそれらを処理するさまざまな方法があります。 たとえば、クライアントが`Reconnected`再接続した場合にイベントが発生しない場合や、接続の`OnConnected`確立が失敗したときにサーバー上のハンドラーが実行される場合があります。 このトピックでは、通常は特定の典型的な状況によって生じる効果のみを説明します。

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>クライアント切断のシナリオ

ブラウザー クライアントでは、SignalR 接続を維持する SignalR クライアント コードは、Web ページの JavaScript コンテキストで実行されます。 そのため、SignalR 接続は、1 つのページから別のページに移動するときに終了する必要があり、複数のブラウザー ウィンドウまたはタブから接続する場合は、複数の接続 ID を持つ複数の接続を持っている理由です。 ユーザーがブラウザー ウィンドウまたはタブを閉じたり、新しいページに移動したり、ページを更新したりすると、SignalR クライアント コードがブラウザ イベントを処理してメソッドを呼び出す`Stop`ため、SignalR 接続は直ちに終了します。 このようなシナリオ、またはアプリケーションがメソッドを呼び出すときに任意の`Stop`クライアント プラットフォーム`OnDisconnected`では、イベント ハンドラーがサーバーで直ちに実行され、`Closed`クライアントがイベントを発生させます`disconnected`(イベントは JavaScript で指定されています)。

クライアント アプリケーションまたは、そのアプリケーションを実行しているコンピューターがクラッシュしたり、スリープ状態になった場合 (ユーザーがラップトップを閉じた場合など)、サーバーは何が起こったかを通知されません。 サーバーが知る限り、クライアントの損失は接続の中断によるもので、クライアントが再接続しようとしている可能性があります。 したがって、このようなシナリオでは、サーバーはクライアントに再接続の機会を与えるために待機し`OnDisconnected`、切断タイムアウト期間が満了するまで (デフォルトでは約 30 秒) 実行されません。 次の図は、このシナリオを示しています。

![クライアント コンピュータの障害](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>サーバー切断のシナリオ

サーバーがオフラインになると、再起動、失敗、アプリ ドメインのリサイクルなどが発生し、接続が失われた場合や、トランスポート API と SignalR がサーバーのデータを削除したことをすぐに認識し`ConnectionSlow`、SignalR がイベントを発生させずに再接続を試みる可能性があります。 クライアントが再接続モードに入り、切断タイムアウト期間が終了する前にサーバーが回復または再起動するか、新しいサーバーがオンラインになった場合、クライアントは復元されたサーバーまたは新しいサーバーに再接続します。 その場合、SignalR 接続はクライアントで続行され、イベント`Reconnected`が発生します。 最初のサーバーでは、`OnDisconnected`実行されることはなく、新しいサーバー上では`OnReconnected`、そのサーバー`OnConnected`上のクライアントに対して実行されたことはありませんが、実行されます。 (再起動後またはアプリケーション ドメインのリサイクル後にクライアントが同じサーバーに再接続した場合も、サーバーが再起動すると、以前の接続アクティビティのメモリが存在しないため、この影響は同じです)。次の図では、トランスポート API が失われた接続をすぐに認識し、`ConnectionSlow`イベントが発生しないことを前提としています。

![サーバー障害と再接続](handling-connection-lifetime-events/_static/image5.png)

切断タイムアウト時間内にサーバーが使用可能にならない場合、SignalR 接続は終了します。 このシナリオでは`Closed`、(JavaScript`disconnected`クライアントの) イベントはクライアントで発生します`OnDisconnected`が、サーバー上で呼び出されることはありません。 次の図では、トランスポート API が接続が失われたことを認識しないため、SignalR キープアライブ機能によって検出され`ConnectionSlow`、イベントが発生することを前提としています。

![サーバー障害とタイムアウト](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>タイムアウトとキープアライブの設定

既定`ConnectionTimeout`の`DisconnectTimeout`、 `KeepAlive` 、および 値はほとんどのシナリオに適していますが、環境に特別なニーズがある場合は変更できます。 たとえば、ネットワーク環境でアイドル状態の接続が 5 秒間閉じた場合、キープアライブ値を減らす必要がある場合があります。

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

この設定は、トランスポート接続を開いたままにして応答を待機してから、その接続を閉じて新しい接続を開く時間を表します。 デフォルト値は 110 秒です。

この設定は、キープアライブ機能が無効になっている場合にのみ適用され、通常は長時間ポーリング トランスポートにのみ適用されます。 次の図は、この設定が長時間ポーリング トランスポート接続に及ぼす影響を示しています。

![ロングポーリングトランスポート接続](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>切断タイムアウト

この設定は、イベントを発生させる前にトランスポート接続が失われた後に待機`Disconnected`する時間を表します。 既定値は 30 秒です。 を設定`DisconnectTimeout`すると`KeepAlive`、自動的に値の 1/3`DisconnectTimeout`に設定されます。

<a id="keepalive"></a>

### <a name="keepalive"></a>KeepAlive

この設定は、アイドル接続を介してキープアライブ パケットを送信するまでの待機時間を表します。 既定値は 10 秒です。 この値は、値の`DisconnectTimeout`1/3 を超える値であってはなりません。

`DisconnectTimeout`と の両方を設定する`KeepAlive`場合は`KeepAlive`、`DisconnectTimeout`の後に設定します。 それ以外`KeepAlive`の場合は、タイムアウト値`DisconnectTimeout`の`KeepAlive`1/3 に自動的に設定すると、設定が上書きされます。

キープアライブ機能を無効にする場合`KeepAlive`は、null に設定します。 長期ポーリング トランスポートでは、キープアライブ機能は自動的に無効になります。

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>タイムアウトとキープアライブの設定を変更する方法

これらの設定の既定値を変更するには、次の例に`Application_Start`示すように *、Global.asax*ファイルで設定します。 サンプル コードに示されている値は、既定値と同じです。

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>切断についてユーザーに通知する方法

アプリケーションによっては、接続に問題がある場合にユーザーにメッセージを表示する必要がある場合があります。 これを行う方法とタイミングには、いくつかのオプションがあります。 次のコード サンプルは、生成されたプロキシを使用する JavaScript クライアント用です。

- イベントを`connectionSlow`処理して、SignalR が接続の問題を認識すると、再接続モードに入る前に、メッセージを表示します。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- SignalR`reconnecting`が切断を認識し、再接続モードに入るとき、イベントを処理してメッセージを表示します。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- 再接続の`disconnected`試行がタイムアウトしたときにメッセージを表示するイベントを処理します。このシナリオでは、サーバーとの接続を再確立する唯一の方法は、新しい接続 ID を作成する`Start`メソッドを呼び出すことによって SignalR 接続を再起動することです。 次のコード サンプルでは、メソッドの呼び出しによって発生した SignalR 接続の通常の終了後ではなく、再接続タイムアウト後にのみ通知を発行することを`Stop`確認するフラグを使用します。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>連続的に再接続する方法

アプリケーションによっては、接続が失われ、再接続の試行がタイムアウトになった後に、接続を自動的に再確立する必要がある場合があります。これを行うには、`Start``Closed`イベント ハンドラー (JavaScript クライアントの`disconnected`イベント ハンドラー) からメソッドを呼び出すことができます。 サーバーまたは物理接続が使用できない場合に、頻`Start`繁に行わないように、呼び出しの前に一定期間待つ必要があります。 次のコード サンプルは、生成されたプロキシを使用する JavaScript クライアント用です。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

モバイル クライアントで注意する必要がある潜在的な問題は、サーバーまたは物理接続が使用できないときに連続的な再接続を試行すると、不要なバッテリが消耗する可能性があるという点です。

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>サーバー コードでクライアントを切断する方法

SignalR バージョン 2 には、クライアントを切断するための組み込みのサーバー API がありません。 [今後、この機能を追加する予定](https://github.com/SignalR/SignalR/issues/2101)があります。 現在の SignalR リリースでは、クライアントをサーバーから切断する最も簡単な方法は、クライアントに切断メソッドを実装し、そのメソッドをサーバーから呼び出す方法です。 次のコード サンプルは、生成されたプロキシを使用する JavaScript クライアントの切断メソッドを示しています。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> セキュリティ - クライアントが再接続されたり、ハッキングされたコードがメソッドを削除したり、その動作を変更したりする可能性があるため、クライアントの切断方法も、提案された組み込み API も`stopClient`、悪意のあるコードを実行しているハッキングされたクライアントのシナリオに対処しません。 ステートフルサービス拒否 (DOS) 保護を実装する適切な場所は、フレームワークやサーバー層ではなくフロントエンド インフラストラクチャにあります。

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>切断の理由の検出

SignalR 2.1 は、`OnDisconnect`タイムアウトではなく、クライアントが意図的に切断されているかどうかを示すサーバー イベントにオーバーロードを追加します。クライアント`StopCalled`が明示的に接続を閉じた場合、パラメーターは true です。 JavaScript では、サーバー エラーによってクライアントが切断された場合、エラー情報は クライアントに`$.connection.hub.lastError`.

**C# サーバー`stopCalled`コード: パラメーター**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**JavaScript クライアント コード:`lastError`イベント`disconnect`内でアクセスします。**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]
