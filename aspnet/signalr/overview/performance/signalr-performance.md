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
# <a name="signalr-performance"></a><span data-ttu-id="50f7f-103">SignalR パフォーマンス</span><span class="sxs-lookup"><span data-stu-id="50f7f-103">SignalR Performance</span></span>

<span data-ttu-id="50f7f-104">[パトリック・フレッチャー](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="50f7f-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="50f7f-105">このトピックでは、SignalR アプリケーションのパフォーマンスを設計、測定、および改善する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="50f7f-106">このトピックで使用するソフトウェアバージョン</span><span class="sxs-lookup"><span data-stu-id="50f7f-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="50f7f-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="50f7f-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="50f7f-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="50f7f-108">.NET 4.5</span></span>
> - <span data-ttu-id="50f7f-109">シグナル・バージョン 2</span><span class="sxs-lookup"><span data-stu-id="50f7f-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="50f7f-110">このトピックの以前のバージョン</span><span class="sxs-lookup"><span data-stu-id="50f7f-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="50f7f-111">SignalR の以前のバージョンについては[、SignalR の古いバージョン](../older-versions/index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="50f7f-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="50f7f-112">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="50f7f-112">Questions and comments</span></span>
>
> <span data-ttu-id="50f7f-113">このチュートリアルを気に入った方法と、ページの下部にあるコメントで改善できる内容についてのフィードバックを残してください。</span><span class="sxs-lookup"><span data-stu-id="50f7f-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="50f7f-114">チュートリアルに直接関連しない質問がある場合は[、ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="50f7f-115">SignalR のパフォーマンスとスケーリングに関する最近のプレゼンテーションについては[、「ASP.NET SignalR を使用したリアルタイム Web](https://channel9.msdn.com/Events/Build/2013/3-502)のスケーリング」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="50f7f-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="50f7f-116">このトピックには、次のセクションが含まれます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="50f7f-117">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="50f7f-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="50f7f-118">パフォーマンスに関する SignalR サーバーのチューニング</span><span class="sxs-lookup"><span data-stu-id="50f7f-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="50f7f-119">パフォーマンスに関する問題のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="50f7f-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="50f7f-120">SignalR パフォーマンス カウンタの使用</span><span class="sxs-lookup"><span data-stu-id="50f7f-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="50f7f-121">他のパフォーマンス カウンタの使用</span><span class="sxs-lookup"><span data-stu-id="50f7f-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="50f7f-122">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="50f7f-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="50f7f-123">設計上の考慮事項</span><span class="sxs-lookup"><span data-stu-id="50f7f-123">Design considerations</span></span>

<span data-ttu-id="50f7f-124">このセクションでは、SignalR アプリケーションの設計中に実装できるパターンについて説明し、不要なネットワーク トラフィックを生成することによってパフォーマンスが低下しないようにします。</span><span class="sxs-lookup"><span data-stu-id="50f7f-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="50f7f-125">メッセージの頻度の調整</span><span class="sxs-lookup"><span data-stu-id="50f7f-125">Throttling message frequency</span></span>

<span data-ttu-id="50f7f-126">リアルタイム ゲーム アプリケーションなど、高頻度でメッセージを送信するアプリケーションでも、ほとんどのアプリケーションは 1 秒間に数個以上のメッセージを送信する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="50f7f-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="50f7f-127">各クライアントが生成するトラフィックの量を減らすために、メッセージ ループを実装して、メッセージを固定レートより頻繁にキューに入れ、送信することができます (つまり、送信される時間間隔内にメッセージがある場合は、1 秒ごとに一定の数のメッセージが送信されます)。</span><span class="sxs-lookup"><span data-stu-id="50f7f-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="50f7f-128">(クライアントとサーバーの両方から) 一定のレートにメッセージをスロットリングするサンプル アプリケーションについては[、SignalR を使用した高周波リアルタイムを](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="50f7f-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="50f7f-129">メッセージ サイズの縮小</span><span class="sxs-lookup"><span data-stu-id="50f7f-129">Reducing message size</span></span>

<span data-ttu-id="50f7f-130">シリアル化されたオブジェクトのサイズを小さくすることで、SignalR メッセージのサイズを小さくすることができます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="50f7f-131">サーバー コードで、送信する必要のないプロパティを含むオブジェクトを送信する場合は、 属性を使用してそれらのプロパティがシリアル化されないようにします`JsonIgnore`。</span><span class="sxs-lookup"><span data-stu-id="50f7f-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="50f7f-132">プロパティの名前もメッセージに格納されます。プロパティの名前は、`JsonProperty`属性を使用して短縮できます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="50f7f-133">次のコード サンプルでは、クライアントに送信されるプロパティを除外する方法と、プロパティ名を短くする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="50f7f-134">**クライアントに送信されるデータを除外する JsonIgnore 属性を示す .NET サーバー コードと、メッセージ サイズを小さくする JsonProperty 属性**</span><span class="sxs-lookup"><span data-stu-id="50f7f-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="50f7f-135">クライアント コードの読みやすさや保守性を維持するために、省略されたプロパティ名は、メッセージを受信した後で人間のわかりやすい名前に再マップできます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="50f7f-136">次のコード サンプルでは、短縮名を長い名前に再マップする方法の 1 つを示します`reMap`。</span><span class="sxs-lookup"><span data-stu-id="50f7f-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="50f7f-137">**短縮されたプロパティ名を人間が読み取り可能な名前に再マップするクライアント側の JavaScript コード**</span><span class="sxs-lookup"><span data-stu-id="50f7f-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="50f7f-138">同じ方法を使用して、クライアントからサーバーへのメッセージの名前を短くすることもできます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="50f7f-139">メッセージ オブジェクトのメモリ使用量 (つまり、メッセージに使用されるメモリの量) を減らすことで、パフォーマンスを向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="50f7f-140">たとえば、a の全範囲`int`が必要ない場合は、`short`または`byte`を代わりに使用できます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="50f7f-141">メッセージはサーバー メモリのメッセージ バスに格納されるため、メッセージのサイズを小さくすると、サーバーのメモリの問題にも対処できます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="50f7f-142">パフォーマンスに関する SignalR サーバーのチューニング</span><span class="sxs-lookup"><span data-stu-id="50f7f-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="50f7f-143">次の構成設定を使用して、SignalR アプリケーションのパフォーマンスを向上させるためにサーバーを調整できます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="50f7f-144">ASP.NETアプリケーションのパフォーマンスを向上させる方法の一般情報については[、ASP.NETパフォーマンスの向上を](https://msdn.microsoft.com/library/ff647787.aspx)参照してください。</span><span class="sxs-lookup"><span data-stu-id="50f7f-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="50f7f-145">**SignalR 構成設定**</span><span class="sxs-lookup"><span data-stu-id="50f7f-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="50f7f-146">**既定**の設定では、SignalR は接続ごとに 1,000 個のメッセージを 1 つの接続のハブあたりのメモリに保持します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="50f7f-147">大きなメッセージを使用している場合は、メモリの問題が発生し、この値を小さくすることで軽減できます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="50f7f-148">この設定は、ASP.NET アプリケーション`Application_Start`のイベント ハンドラー、または自己ホスト型アプリケーション`Configuration`の OWIN スタートアップ クラスのメソッドで設定できます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="50f7f-149">次のサンプルでは、使用するサーバー メモリの量を減らすために、アプリケーションのメモリ使用量を削減するために、この値を減らす方法を示します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="50f7f-150">**既定のメッセージ バッファ サイズを減らすStartup.csの .NET サーバー コード**</span><span class="sxs-lookup"><span data-stu-id="50f7f-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="50f7f-151">**IIS 構成設定**</span><span class="sxs-lookup"><span data-stu-id="50f7f-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="50f7f-152">**アプリケーションあたりの最大同時要求**数 : 同時 IIS 要求の数を増やすと、要求の処理に使用できるサーバー リソースが増えます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="50f7f-153">デフォルト値は 5000 です。この設定を増やすには、管理者特権でのコマンド プロンプトで次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="50f7f-154">**アプリケーション プール キュー長**: これは、Http.sys がアプリケーション プールに対してキューに入る要求の最大数です。</span><span class="sxs-lookup"><span data-stu-id="50f7f-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="50f7f-155">キューがいっぱいになると、新しい要求は 503 の 「サービスを利用できません」応答を受信します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="50f7f-156">既定値は 1000 です。</span><span class="sxs-lookup"><span data-stu-id="50f7f-156">The default value is 1000.</span></span>

    <span data-ttu-id="50f7f-157">アプリケーションをホストしているアプリケーション プール内のワーカー プロセスのキューの長さを短くすると、メモリ リソースが節約されます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="50f7f-158">詳細については、「[アプリケーション プールの管理、チューニング、および構成](https://technet.microsoft.com/library/cc745955.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="50f7f-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="50f7f-159">**ASP.NET構成設定**</span><span class="sxs-lookup"><span data-stu-id="50f7f-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="50f7f-160">このセクションには、ファイルで設定できる構成設定が`aspnet.config`含まれています。</span><span class="sxs-lookup"><span data-stu-id="50f7f-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="50f7f-161">このファイルは、プラットフォームに応じて、次の 2 つの場所のいずれかに見られます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="50f7f-162">SignalR のパフォーマンスを向上させるASP.NET設定には、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="50f7f-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="50f7f-163">**CPU あたりの最大同時要求**数 : この設定を増やすと、パフォーマンスのボトルネックが軽減される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="50f7f-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="50f7f-164">この設定を増やすには、次の構成設定を`aspnet.config`ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="50f7f-165">**要求キューの制限**: 接続の合計数がこの設定を`maxConcurrentRequestsPerCPU`超えると、ASP.NETキューを使用して要求の調整が開始されます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="50f7f-166">キューのサイズを大きくするには、設定を`requestQueueLimit`増やします。</span><span class="sxs-lookup"><span data-stu-id="50f7f-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="50f7f-167">これを行うには、次の構成設定を (`processModel`ではなく`aspnet.config`)`config/machine.config`ノードに追加します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="50f7f-168">パフォーマンスに関する問題のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="50f7f-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="50f7f-169">このセクションでは、アプリケーションのパフォーマンスのボトルネックを見つける方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="50f7f-170">WebSocket が使用されていることを確認する</span><span class="sxs-lookup"><span data-stu-id="50f7f-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="50f7f-171">SignalR はクライアントとサーバー間の通信にさまざまなトランスポートを使用できますが、WebSocket はパフォーマンス上の大きな利点を提供するため、クライアントとサーバーがサポートする場合は使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50f7f-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="50f7f-172">クライアントとサーバーが WebSocket の要件を満たしているかどうかを確認するには、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="50f7f-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="50f7f-173">アプリケーションで使用されているトランスポートを確認するには、ブラウザー開発者ツールを使用し、ログを調べて、接続に使用されているトランスポートを確認します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="50f7f-174">Internet Explorer および Chrome でのブラウザ開発ツールの使用については、「[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="50f7f-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="50f7f-175">SignalR パフォーマンス カウンタの使用</span><span class="sxs-lookup"><span data-stu-id="50f7f-175">Using SignalR performance counters</span></span>

<span data-ttu-id="50f7f-176">このセクションでは、パッケージ内にある SignalR パフォーマンス カウンターを有効に`Microsoft.AspNet.SignalR.Utils`して使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="50f7f-177">signalr.exe をインストールしています</span><span class="sxs-lookup"><span data-stu-id="50f7f-177">Installing signalr.exe</span></span>

<span data-ttu-id="50f7f-178">パフォーマンス カウンタは、SignalR.exe というユーティリティを使用してサーバーに追加できます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="50f7f-179">このユーティリティをインストールするには、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="50f7f-180">Visual Studio で、[**ツール]** > **を選択する ツール NuGet パッケージ マネージャー** > **ソリューションの NuGet パッケージを管理します。**</span><span class="sxs-lookup"><span data-stu-id="50f7f-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="50f7f-181">**signalr.utils**を検索し、[インストール] を選択します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="50f7f-182">パッケージをインストールするための使用許諾契約書に同意します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="50f7f-183">に SignalR.exe が`<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`インストールされます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="50f7f-184">SignalR.exe を使用したパフォーマンス カウンタのインストール</span><span class="sxs-lookup"><span data-stu-id="50f7f-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="50f7f-185">SignalR パフォーマンス カウンターをインストールするには、次のパラメーターを使用して、管理者特権のコマンド プロンプトで SignalR.exe を実行します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="50f7f-186">SignalR パフォーマンス カウンタを削除するには、管理者特権のコマンド プロンプトで SignalR.exe を次のパラメータを使用して実行します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="50f7f-187">シグナルパフォーマンスカウンタ</span><span class="sxs-lookup"><span data-stu-id="50f7f-187">SignalR Performance counters</span></span>

<span data-ttu-id="50f7f-188">ユーティリティ パッケージは、次のパフォーマンス カウンターをインストールします。</span><span class="sxs-lookup"><span data-stu-id="50f7f-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="50f7f-189">"Total" カウンタは、前回のアプリケーション プールまたはサーバーの再起動以降のイベント数を測定します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="50f7f-190">**接続のメトリック**</span><span class="sxs-lookup"><span data-stu-id="50f7f-190">**Connection metrics**</span></span>

<span data-ttu-id="50f7f-191">次のメトリックは、発生した接続の有効期間イベントを測定します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="50f7f-192">詳細については、「[接続の有効期間イベントの概要と処理](../guide-to-the-api/handling-connection-lifetime-events.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="50f7f-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="50f7f-193">**接続接続**</span><span class="sxs-lookup"><span data-stu-id="50f7f-193">**Connections Connected**</span></span>
- <span data-ttu-id="50f7f-194">**再接続された接続**</span><span class="sxs-lookup"><span data-stu-id="50f7f-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="50f7f-195">**接続が切断されました**</span><span class="sxs-lookup"><span data-stu-id="50f7f-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="50f7f-196">**接続現在**</span><span class="sxs-lookup"><span data-stu-id="50f7f-196">**Connections Current**</span></span>

<span data-ttu-id="50f7f-197">**メッセージのメトリック**</span><span class="sxs-lookup"><span data-stu-id="50f7f-197">**Message metrics**</span></span>

<span data-ttu-id="50f7f-198">次のメトリックは、SignalR によって生成されるメッセージ トラフィックを測定します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="50f7f-199">**受信した接続メッセージの合計**</span><span class="sxs-lookup"><span data-stu-id="50f7f-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="50f7f-200">**送信された接続メッセージの総数**</span><span class="sxs-lookup"><span data-stu-id="50f7f-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="50f7f-201">**受信した接続メッセージ/秒**</span><span class="sxs-lookup"><span data-stu-id="50f7f-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="50f7f-202">**送信された接続メッセージ/秒**</span><span class="sxs-lookup"><span data-stu-id="50f7f-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="50f7f-203">**メッセージ バスメトリック**</span><span class="sxs-lookup"><span data-stu-id="50f7f-203">**Message bus metrics**</span></span>

<span data-ttu-id="50f7f-204">次のメトリックは、内部 SignalR メッセージ バス(すべての受信および送信 SignalR メッセージが配置されるキュー)を介してトラフィックを測定します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="50f7f-205">メッセージは送信またはブロードキャスト時に**公開されます**。</span><span class="sxs-lookup"><span data-stu-id="50f7f-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="50f7f-206">このコンテキストの**サブスクライバー**は、メッセージ バスのサブスクリプションです。これは、クライアント数とサーバー自体の数に等しいはずです。</span><span class="sxs-lookup"><span data-stu-id="50f7f-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="50f7f-207">**割り当てワーカー**は、アクティブな接続にデータを送信するコンポーネントです。**ビジー状態のワーカー**は、メッセージを積極的に送信しているワーカーです。</span><span class="sxs-lookup"><span data-stu-id="50f7f-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="50f7f-208">**受信したメッセージ バス メッセージの総数**</span><span class="sxs-lookup"><span data-stu-id="50f7f-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="50f7f-209">**受信したメッセージ バス メッセージ/秒**</span><span class="sxs-lookup"><span data-stu-id="50f7f-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="50f7f-210">**メッセージ バス メッセージの公開総数**</span><span class="sxs-lookup"><span data-stu-id="50f7f-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="50f7f-211">**メッセージ バス メッセージの公開/秒**</span><span class="sxs-lookup"><span data-stu-id="50f7f-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="50f7f-212">**メッセージ バス サブスクライバ現在**</span><span class="sxs-lookup"><span data-stu-id="50f7f-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="50f7f-213">**メッセージ バス のサブスクライバーの合計**</span><span class="sxs-lookup"><span data-stu-id="50f7f-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="50f7f-214">**メッセージ バス のサブスクライバー/秒**</span><span class="sxs-lookup"><span data-stu-id="50f7f-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="50f7f-215">**メッセージ バス割り当てワーカー**</span><span class="sxs-lookup"><span data-stu-id="50f7f-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="50f7f-216">**メッセージ バスの使用中のワーカー**</span><span class="sxs-lookup"><span data-stu-id="50f7f-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="50f7f-217">**メッセージ バス トピックの現在**</span><span class="sxs-lookup"><span data-stu-id="50f7f-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="50f7f-218">**エラーメトリック**</span><span class="sxs-lookup"><span data-stu-id="50f7f-218">**Error metrics**</span></span>

<span data-ttu-id="50f7f-219">次のメトリックは、SignalR メッセージ トラフィックによって生成されたエラーを測定します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="50f7f-220">**ハブまたはハブ**のメソッドを解決できない場合、ハブ解決エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="50f7f-221">**ハブ呼び出し**エラーは、ハブ メソッドの呼び出し中にスローされる例外です。</span><span class="sxs-lookup"><span data-stu-id="50f7f-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="50f7f-222">**トランスポート**エラーは、HTTP 要求または応答中に発生する接続エラーです。</span><span class="sxs-lookup"><span data-stu-id="50f7f-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="50f7f-223">**エラー: すべての合計**</span><span class="sxs-lookup"><span data-stu-id="50f7f-223">**Errors: All Total**</span></span>
- <span data-ttu-id="50f7f-224">**エラー: すべて/秒**</span><span class="sxs-lookup"><span data-stu-id="50f7f-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="50f7f-225">**エラー: ハブの解決の合計**</span><span class="sxs-lookup"><span data-stu-id="50f7f-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="50f7f-226">**エラー: ハブの解像度/秒**</span><span class="sxs-lookup"><span data-stu-id="50f7f-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="50f7f-227">**エラー: ハブ呼び出しの合計**</span><span class="sxs-lookup"><span data-stu-id="50f7f-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="50f7f-228">**エラー: ハブ呼び出し/秒**</span><span class="sxs-lookup"><span data-stu-id="50f7f-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="50f7f-229">**エラー: トランスポート合計**</span><span class="sxs-lookup"><span data-stu-id="50f7f-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="50f7f-230">**エラー: トランスポート/秒**</span><span class="sxs-lookup"><span data-stu-id="50f7f-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="50f7f-231">**スケールアウトメトリック**</span><span class="sxs-lookup"><span data-stu-id="50f7f-231">**Scaleout metrics**</span></span>

<span data-ttu-id="50f7f-232">次のメトリックは、スケールアウト プロバイダーによって生成されたトラフィックとエラーを測定します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="50f7f-233">このコンテキストの**ストリーム**は、スケールアウト プロバイダーによって使用されるスケール単位です。これは、SQL Server が使用されている場合はテーブル、サービス バスを使用する場合はトピック、Redis が使用されている場合はサブスクリプションです。</span><span class="sxs-lookup"><span data-stu-id="50f7f-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="50f7f-234">各ストリームは、順序付けられた読み取りおよび書き込み操作を保証します。単一ストリームは潜在的なスケールのボトルネックであるため、ストリームの数を増やしてそのボトルネックを減らすことができます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="50f7f-235">複数のストリームを使用する場合、SignalR は、特定の接続から送信されたメッセージが順番に送信されるように、これらのストリームにメッセージを自動的に配布 (シャード) します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="50f7f-236">[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)設定は、SignalR によって維持されるスケールアウト送信キューの長さを制御します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="50f7f-237">この値を 0 より大きい値に設定すると、送信キュー内のすべてのメッセージが、構成済みのメッセージング・バックプレーンに一度に 1 つずつ送信されます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="50f7f-238">キューのサイズが構成された長さを超えた場合、キュー内のメッセージ数が設定値より少なくなるまで、送信の後続の呼び出しは[InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx)ですぐに失敗します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="50f7f-239">実装されたバックプレーンは一般的に独自のキューイングまたはフロー制御を持つため、キューイングはデフォルトで無効になっています。</span><span class="sxs-lookup"><span data-stu-id="50f7f-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="50f7f-240">SQL Server の場合、接続プールは、一度に送信される回数を効果的に制限します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="50f7f-241">既定では、SQL Server と Redis に 1 つのストリームのみが使用され、サービス バスには 5 つのストリームが使用され、キューイングは無効になっていますが、SQL Server とサービス バスの構成を使用してこれらの設定を変更できます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="50f7f-242">**SQL Server バックプレーンのテーブル数とキューの長さを構成するための .NET サーバー コード**</span><span class="sxs-lookup"><span data-stu-id="50f7f-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="50f7f-243">**Service Bus バックプレーンのトピック数とキュー長を構成するための .NET サーバー コード**</span><span class="sxs-lookup"><span data-stu-id="50f7f-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="50f7f-244">**バッファリング**ストリームは、障害が発生した状態に入ったストリームです。ストリームが障害状態になると、ストリームが障害を発生しなくなるまで、バックプレーンに送信されるすべてのメッセージは直ちに失敗します。</span><span class="sxs-lookup"><span data-stu-id="50f7f-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="50f7f-245">**送信キューの長さは**、投稿済みでまだ送信されていないメッセージの数です。</span><span class="sxs-lookup"><span data-stu-id="50f7f-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="50f7f-246">**スケールアウト メッセージ バス メッセージの受信/秒**</span><span class="sxs-lookup"><span data-stu-id="50f7f-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="50f7f-247">**スケールアウト ストリームの合計**</span><span class="sxs-lookup"><span data-stu-id="50f7f-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="50f7f-248">**スケールアウト ストリームが開いている**</span><span class="sxs-lookup"><span data-stu-id="50f7f-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="50f7f-249">**スケールアウト ストリームのバッファリング**</span><span class="sxs-lookup"><span data-stu-id="50f7f-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="50f7f-250">**スケールアウト エラーの合計**</span><span class="sxs-lookup"><span data-stu-id="50f7f-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="50f7f-251">**スケールアウト エラー/秒**</span><span class="sxs-lookup"><span data-stu-id="50f7f-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="50f7f-252">**スケールアウト送信キューの長さ**</span><span class="sxs-lookup"><span data-stu-id="50f7f-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="50f7f-253">これらのカウンタの測定方法の詳細については、「 [Azure Service Bus を使用した SignalR スケールアウト](scaleout-with-windows-azure-service-bus.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="50f7f-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="50f7f-254">他のパフォーマンス カウンタの使用</span><span class="sxs-lookup"><span data-stu-id="50f7f-254">Using other performance counters</span></span>

<span data-ttu-id="50f7f-255">次のパフォーマンス カウンタは、アプリケーションのパフォーマンスを監視する場合にも役立ちます。</span><span class="sxs-lookup"><span data-stu-id="50f7f-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="50f7f-256">**メモリ**</span><span class="sxs-lookup"><span data-stu-id="50f7f-256">**Memory**</span></span>

- <span data-ttu-id="50f7f-257">.NET CLR\\メモリ # すべてのヒープのバイト数 (w3wp の場合)</span><span class="sxs-lookup"><span data-stu-id="50f7f-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="50f7f-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="50f7f-258">**ASP.NET**</span></span>

- <span data-ttu-id="50f7f-259">ASP.NET\要求現在</span><span class="sxs-lookup"><span data-stu-id="50f7f-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="50f7f-260">ASP.NET\キューに入れられます</span><span class="sxs-lookup"><span data-stu-id="50f7f-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="50f7f-261">ASP.NET\拒否されました</span><span class="sxs-lookup"><span data-stu-id="50f7f-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="50f7f-262">**Cpu**</span><span class="sxs-lookup"><span data-stu-id="50f7f-262">**CPU**</span></span>

- <span data-ttu-id="50f7f-263">プロセッサ情報\プロセッサ時間</span><span class="sxs-lookup"><span data-stu-id="50f7f-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="50f7f-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="50f7f-264">**TCP/IP**</span></span>

- <span data-ttu-id="50f7f-265">TCPv6/接続が確立されました</span><span class="sxs-lookup"><span data-stu-id="50f7f-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="50f7f-266">TCPv4/接続が確立されました</span><span class="sxs-lookup"><span data-stu-id="50f7f-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="50f7f-267">**ウェブサービス**</span><span class="sxs-lookup"><span data-stu-id="50f7f-267">**Web Service**</span></span>

- <span data-ttu-id="50f7f-268">Web サービス\現在の接続</span><span class="sxs-lookup"><span data-stu-id="50f7f-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="50f7f-269">Web サービス\最大接続数</span><span class="sxs-lookup"><span data-stu-id="50f7f-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="50f7f-270">**スレッド**</span><span class="sxs-lookup"><span data-stu-id="50f7f-270">**Threading**</span></span>

- <span data-ttu-id="50f7f-271">現在の論理スレッドの\\.NET CLR ロックおよびスレッド数</span><span class="sxs-lookup"><span data-stu-id="50f7f-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="50f7f-272">現在の物理スレッドの\\.NET CLR ロックとスレッド数</span><span class="sxs-lookup"><span data-stu-id="50f7f-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="50f7f-273">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="50f7f-273">Other Resources</span></span>

<span data-ttu-id="50f7f-274">パフォーマンスの監視とチューニングASP.NETの詳細については、以下のトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="50f7f-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="50f7f-275">[ASP.NET のパフォーマンスの概要](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="50f7f-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="50f7f-276">IIS 7.5、IIS 7.0、および IIS 6.0 でのASP.NETスレッドの使用</span><span class="sxs-lookup"><span data-stu-id="50f7f-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="50f7f-277">&lt;アプリケーションプール&gt;要素 (Web 設定)</span><span class="sxs-lookup"><span data-stu-id="50f7f-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
