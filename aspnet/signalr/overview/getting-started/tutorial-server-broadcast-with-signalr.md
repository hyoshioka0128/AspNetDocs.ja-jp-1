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
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="54411-103">チュートリアル: SignalR 2 を使用したサーバー ブロードキャスト</span><span class="sxs-lookup"><span data-stu-id="54411-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="54411-104">このチュートリアルでは、SignalR 2 を使用してサーバー ブロードキャスト機能を提供する web アプリケーションASP.NET作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="54411-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="54411-105">サーバー ブロードキャストとは、サーバーがクライアントに送信された通信を開始することを意味します。</span><span class="sxs-lookup"><span data-stu-id="54411-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="54411-106">このチュートリアルで作成するアプリケーションは、サーバー ブロードキャスト機能の一般的なシナリオである株式のティッカーをシミュレートします。</span><span class="sxs-lookup"><span data-stu-id="54411-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="54411-107">定期的に、サーバーはランダムに株価を更新し、接続されているすべてのクライアントに更新をブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="54411-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="54411-108">ブラウザでは、**変更**列と列の番号と**%** 記号が、サーバーからの通知に応じて動的に変化します。</span><span class="sxs-lookup"><span data-stu-id="54411-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="54411-109">同じ URL に対して他のブラウザーを開くと、同じデータと同じ変更が同時に表示されます。</span><span class="sxs-lookup"><span data-stu-id="54411-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![ウェブを作成する](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="54411-111">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="54411-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="54411-112">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="54411-112">Create the project</span></span>
> * <span data-ttu-id="54411-113">サーバー コードを設定する</span><span class="sxs-lookup"><span data-stu-id="54411-113">Set up the server code</span></span>
> * <span data-ttu-id="54411-114">サーバー コードを確認する</span><span class="sxs-lookup"><span data-stu-id="54411-114">Examine the server code</span></span>
> * <span data-ttu-id="54411-115">クライアント コードを設定する</span><span class="sxs-lookup"><span data-stu-id="54411-115">Set up the client code</span></span>
> * <span data-ttu-id="54411-116">クライアント コードを確認する</span><span class="sxs-lookup"><span data-stu-id="54411-116">Examine the client code</span></span>
> * <span data-ttu-id="54411-117">アプリケーションをテストする</span><span class="sxs-lookup"><span data-stu-id="54411-117">Test the application</span></span>
> * <span data-ttu-id="54411-118">ログの有効化</span><span class="sxs-lookup"><span data-stu-id="54411-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54411-119">アプリケーションのビルド手順を実行しない場合は、新しい空のASP.NET Web アプリケーション プロジェクトに SignalR.Sample パッケージをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="54411-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="54411-120">このチュートリアルの手順を実行せずに NuGet パッケージをインストールする場合は *、readme.txt*ファイルの指示に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="54411-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="54411-121">パッケージを実行するには、インストールされたパッケージ内のメソッドを呼び出す`ConfigureSignalR`OWIN スタートアップ クラスを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="54411-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="54411-122">OWIN スタートアップ クラスを追加しないと、エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="54411-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="54411-123">この記事の[「StockTicker サンプルのインストール](#install-the-stockticker-sample)」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="54411-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54411-124">前提条件</span><span class="sxs-lookup"><span data-stu-id="54411-124">Prerequisites</span></span>

* <span data-ttu-id="54411-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) と **ASP.NET および開発**ワークロード。</span><span class="sxs-lookup"><span data-stu-id="54411-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="54411-126">プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="54411-126">Create the project</span></span>

<span data-ttu-id="54411-127">このセクションでは、Visual Studio 2017 を使用して空のASP.NET Web アプリケーションを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="54411-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="54411-128">Visual Studio で、ASP.NET Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="54411-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![ウェブを作成する](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="54411-130">[**新しいASP.NET Web アプリケーション - SignalR.StockTicker]** ウィンドウで、[**空]** を選択したままにして **、[OK] を選択します**。</span><span class="sxs-lookup"><span data-stu-id="54411-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="54411-131">サーバー コードを設定する</span><span class="sxs-lookup"><span data-stu-id="54411-131">Set up the server code</span></span>

<span data-ttu-id="54411-132">このセクションでは、サーバー上で実行されるコードを設定します。</span><span class="sxs-lookup"><span data-stu-id="54411-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="54411-133">ストック クラスの作成</span><span class="sxs-lookup"><span data-stu-id="54411-133">Create the Stock class</span></span>

<span data-ttu-id="54411-134">まず、ストックに関する情報を保存および送信するために使用する*Stock*モデル クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="54411-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="54411-135">**ソリューション エクスプローラ**で、プロジェクトを右クリックし、[**Add** > **クラス**の追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="54411-136">クラスに*Stock*という名前を付け、プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="54411-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="54411-137">*Stock.cs*ファイル内のコードを次のコードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="54411-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="54411-138">株式の作成時に設定する 2 つのプロパティは`Symbol`、たとえば、マイクロソフトの MSFT と`Price`です。</span><span class="sxs-lookup"><span data-stu-id="54411-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="54411-139">その他のプロパティは`Price`、設定する方法とタイミングによって異なります。</span><span class="sxs-lookup"><span data-stu-id="54411-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="54411-140">初めて 設定`Price`すると、値が`DayOpen`に反映されます。</span><span class="sxs-lookup"><span data-stu-id="54411-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="54411-141">その後、 を設定`Price`すると、 と の`Change`差`PercentChange``Price`に基づいて プロパティ値と`DayOpen`プロパティ値が計算されます。</span><span class="sxs-lookup"><span data-stu-id="54411-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="54411-142">ストックティッカーハブクラスとストックティッカークラスを作成する</span><span class="sxs-lookup"><span data-stu-id="54411-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="54411-143">SignalR ハブ API を使用して、サーバーとクライアント間の対話を処理します。</span><span class="sxs-lookup"><span data-stu-id="54411-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="54411-144">SignalR`StockTickerHub``Hub`クラスから派生したクラスは、クライアントからの受信接続とメソッド呼び出しを処理します。</span><span class="sxs-lookup"><span data-stu-id="54411-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="54411-145">また、在庫データを更新してオブジェクトを実行`Timer`する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="54411-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="54411-146">オブジェクト`Timer`は、クライアント接続に関係なく、価格の更新を定期的にトリガーします。</span><span class="sxs-lookup"><span data-stu-id="54411-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="54411-147">ハブは一時的であるため`Hub`、これらの関数をクラスに入れることはできません。</span><span class="sxs-lookup"><span data-stu-id="54411-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="54411-148">このアプリは、`Hub`クライアントからサーバーへの接続や呼び出しなど、ハブ上の各タスクのクラス インスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="54411-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="54411-149">したがって、在庫データを保持し、価格を更新し、価格の更新をブロードキャストするメカニズムは、別のクラスで実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="54411-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="54411-150">クラス`StockTicker`に名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="54411-150">You'll name the class `StockTicker`.</span></span>

![ストックティッカーからの放送](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="54411-152">`StockTicker`クラスのインスタンスをサーバー上で実行する必要があるのは 1 つのみなので、各`StockTickerHub`インスタンスからシングルトン`StockTicker`インスタンスへの参照を設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="54411-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="54411-153">この`StockTicker`クラスは、ストック データを持ち、更新をトリガーしますが`StockTicker`、クラスではないため、クライアント`Hub`にブロードキャストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="54411-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="54411-154">クラス`StockTicker`は SignalR ハブ接続コンテキスト オブジェクトへの参照を取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="54411-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="54411-155">その後、SignalR 接続コンテキスト オブジェクトを使用してクライアントにブロードキャストできます。</span><span class="sxs-lookup"><span data-stu-id="54411-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="54411-156">StockTickerHub.csの作成</span><span class="sxs-lookup"><span data-stu-id="54411-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="54411-157">**ソリューション エクスプローラ**で、プロジェクトを右クリックし、[**Add** > **新しい項目**の追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="54411-158">[**新しい項目の追加 - SignalR.StockTicker]** で、[**インストール済みの** > **Visual C#** > **Web** > **SignalR]** を選択し **、[SignalR ハブ クラス (v2)]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="54411-159">クラスに*名前を付け*、プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="54411-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="54411-160">この手順では *、StockTickerHub.cs*クラス ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="54411-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="54411-161">同時に、SignalR をサポートするスクリプト ファイルとアセンブリ参照のセットをプロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="54411-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="54411-162">*StockTickerHub.cs*ファイル内のコードを次のコードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="54411-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="54411-163">ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="54411-163">Save the file.</span></span>

<span data-ttu-id="54411-164">アプリは[、ハブ](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)クラスを使用して、クライアントがサーバーで呼び出すことができるメソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="54411-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="54411-165">1 つのメソッドを定義しています: `GetAllStocks()`。</span><span class="sxs-lookup"><span data-stu-id="54411-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="54411-166">クライアントが最初にサーバーに接続すると、このメソッドを呼び出して、現在の価格ですべての株式のリストを取得します。</span><span class="sxs-lookup"><span data-stu-id="54411-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="54411-167">このメソッドは、メモリからデータを`IEnumerable<Stock>`返すため、同期的に実行して戻ることができます。</span><span class="sxs-lookup"><span data-stu-id="54411-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="54411-168">データベース検索や Web サービス呼び出しなど、待機を伴う何かを行ってメソッドがデータを取得する必要がある`Task<IEnumerable<Stock>>`場合は、非同期処理を有効にする戻り値として指定します。</span><span class="sxs-lookup"><span data-stu-id="54411-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="54411-169">詳細については[、「signalR Hubs API ガイドASP.NET - サーバー - 非同期で実行する場合」を](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)参照してください。</span><span class="sxs-lookup"><span data-stu-id="54411-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="54411-170">この`HubName`属性は、アプリがクライアント上の JavaScript コードでハブを参照する方法を指定します。</span><span class="sxs-lookup"><span data-stu-id="54411-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="54411-171">この属性を使用しない場合、クライアントのデフォルト名は、クラス名の camelCase バージョンです`stockTickerHub`。</span><span class="sxs-lookup"><span data-stu-id="54411-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="54411-172">`StockTicker`クラスを作成するときに後で説明したように、アプリは静的`Instance`プロパティにそのクラスのシングルトン インスタンスを作成します。</span><span class="sxs-lookup"><span data-stu-id="54411-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="54411-173">そのシングルトン インスタンス`StockTicker`は、接続または切断するクライアントの数に関係なくメモリ内にあります。</span><span class="sxs-lookup"><span data-stu-id="54411-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="54411-174">このインスタンスは、メソッド`GetAllStocks()`が現在のストック情報を返すために使用するものです。</span><span class="sxs-lookup"><span data-stu-id="54411-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="54411-175">StockTicker.csの作成</span><span class="sxs-lookup"><span data-stu-id="54411-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="54411-176">**ソリューション エクスプローラ**で、プロジェクトを右クリックし、[**Add** > **クラス**の追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="54411-177">クラスに*名前を付け、* プロジェクトに追加します。</span><span class="sxs-lookup"><span data-stu-id="54411-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="54411-178">*StockTicker.cs*ファイル内のコードを次のコードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="54411-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="54411-179">すべてのスレッドが StockTicker コードの同じインスタンスを実行するため、StockTicker クラスはスレッドセーフでなければなりません。</span><span class="sxs-lookup"><span data-stu-id="54411-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="54411-180">サーバー コードを確認する</span><span class="sxs-lookup"><span data-stu-id="54411-180">Examine the server code</span></span>

<span data-ttu-id="54411-181">サーバー コードを調べると、アプリの動作を理解しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="54411-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="54411-182">シングルトン インスタンスを静的フィールドに格納する</span><span class="sxs-lookup"><span data-stu-id="54411-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="54411-183">このコードは、クラスの`_instance`インスタンスを使用してプロパティ`Instance`をバックする静的フィールドを初期化します。</span><span class="sxs-lookup"><span data-stu-id="54411-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="54411-184">コンストラクターはプライベートであるため、アプリケーションで作成できるクラスの唯一のインスタンスです。</span><span class="sxs-lookup"><span data-stu-id="54411-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="54411-185">アプリは、フィールドに[遅延初期化](/dotnet/framework/performance/lazy-initialization)を`_instance`使用します。</span><span class="sxs-lookup"><span data-stu-id="54411-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="54411-186">パフォーマンス上の理由ではありません。</span><span class="sxs-lookup"><span data-stu-id="54411-186">It's not for performance reasons.</span></span> <span data-ttu-id="54411-187">インスタンスの作成がスレッド セーフであることを確認します。</span><span class="sxs-lookup"><span data-stu-id="54411-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="54411-188">クライアントがサーバーに接続するたびに、別のスレッドで実行されている StockTickerHub クラスの新しいインスタンスは、クラスで先に説明したように、`StockTicker.Instance`静的プロパティから StockTicker シングルトン`StockTickerHub`インスタンスを取得します。</span><span class="sxs-lookup"><span data-stu-id="54411-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="54411-189">コンカレントディクショナリへのストックデータの保存</span><span class="sxs-lookup"><span data-stu-id="54411-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="54411-190">コンストラクターは、いくつかのサンプル`_stocks`ストックデータを使用してコレクションを初期化`GetAllStocks`し、ストックを返します。</span><span class="sxs-lookup"><span data-stu-id="54411-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="54411-191">前に説明したように、この株式のコレクションは、クライアント`StockTickerHub.GetAllStocks`が呼び出すことができるクラスの`Hub`サーバー メソッドである によって返されます。</span><span class="sxs-lookup"><span data-stu-id="54411-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="54411-192">ストック コレクションは、スレッド セーフの[同時ディクショナリ](https://msdn.microsoft.com/library/dd287191.aspx)型として定義されます。</span><span class="sxs-lookup"><span data-stu-id="54411-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="54411-193">代わりに[、Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx)オブジェクトを使用して、ディクショナリを変更するときに明示的にロックすることもできます。</span><span class="sxs-lookup"><span data-stu-id="54411-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="54411-194">このサンプル アプリケーションでは、アプリケーション データをメモリに格納し、アプリケーションがインスタンスを破棄するときにデータを失うことは問題です`StockTicker`。</span><span class="sxs-lookup"><span data-stu-id="54411-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="54411-195">実際のアプリケーションでは、データベースのようなバックエンド データ ストアを操作します。</span><span class="sxs-lookup"><span data-stu-id="54411-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="54411-196">株価の定期的な更新</span><span class="sxs-lookup"><span data-stu-id="54411-196">Periodically updating stock prices</span></span>

<span data-ttu-id="54411-197">コンストラクタは、株価を`Timer`ランダムに更新するメソッドを定期的に呼び出すオブジェクトを起動します。</span><span class="sxs-lookup"><span data-stu-id="54411-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="54411-198">`Timer`を`UpdateStockPrices`呼び出し、state パラメーターで null を渡します。</span><span class="sxs-lookup"><span data-stu-id="54411-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="54411-199">価格を更新する前に、アプリはオブジェクトにロック`_updateStockPricesLock`を取ります。</span><span class="sxs-lookup"><span data-stu-id="54411-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="54411-200">コードは、別のスレッドが既に価格を更新しているかどうかをチェックし、`TryUpdateStockPrice`リスト内の各株式を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="54411-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="54411-201">この`TryUpdateStockPrice`メソッドは、株価を変更するかどうか、および変更する金額を決定します。</span><span class="sxs-lookup"><span data-stu-id="54411-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="54411-202">株価が変わると、アプリは、すべての`BroadcastStockPrice`接続されたクライアントに株価の変更をブロードキャストするために呼び出します。</span><span class="sxs-lookup"><span data-stu-id="54411-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="54411-203">スレッド`_updatingStockPrices`セーフであることを確認するために[volatile](https://msdn.microsoft.com/library/x13ttww7.aspx)として指定されたフラグ。</span><span class="sxs-lookup"><span data-stu-id="54411-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="54411-204">実際のアプリケーションでは、`TryUpdateStockPrice`メソッドは、価格を検索する Web サービスを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="54411-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="54411-205">このコードでは、アプリはランダムな変更を行うために乱数ジェネレーターを使用します。</span><span class="sxs-lookup"><span data-stu-id="54411-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="54411-206">StockTicker クラスがクライアントにブロードキャストできるように SignalR コンテキストを取得する</span><span class="sxs-lookup"><span data-stu-id="54411-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="54411-207">価格の変更は`StockTicker`オブジェクトで発生するため、接続されているすべてのクライアントでメソッドを`updateStockPrice`呼び出す必要があるオブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="54411-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="54411-208">`Hub`クラスでは、クライアント メソッドを呼び出すための API`StockTicker`がありますが、`Hub`クラスから派生したものではなく、オブジェクトへの参照もありません`Hub`。</span><span class="sxs-lookup"><span data-stu-id="54411-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="54411-209">接続されたクライアントにブロードキャストするには、`StockTicker`クラスは`StockTickerHub`クラスの SignalR コンテキスト インスタンスを取得し、それを使用してクライアントのメソッドを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="54411-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="54411-210">コードは、シングルトン クラス インスタンスを作成し、その参照をコンストラクターに渡し、コンストラクターがプロパティに配置するときに SignalR コンテキストへの参照`Clients`を取得します。</span><span class="sxs-lookup"><span data-stu-id="54411-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="54411-211">コンテキストを一度だけ取得する理由は 2 つありますが、コンテキストの取得はコストのかかる作業であり、一度取得すると、アプリがクライアントに送信されるメッセージの意図した順序を確実に維持します。</span><span class="sxs-lookup"><span data-stu-id="54411-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="54411-212">コンテキストの`Clients`プロパティを取得し、`StockTickerClient`プロパティに配置すると、クラスと同じように見えるクライアント メソッドを呼び出すコードを`Hub`記述できます。</span><span class="sxs-lookup"><span data-stu-id="54411-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="54411-213">たとえば、すべてのクライアントにブロードキャストするには、 を書`Clients.All.updateStockPrice(stock)`くことができます。</span><span class="sxs-lookup"><span data-stu-id="54411-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="54411-214">呼`updateStockPrice`び出しているメソッドはまだ存在`BroadcastStockPrice`しません。</span><span class="sxs-lookup"><span data-stu-id="54411-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="54411-215">後でクライアントで実行するコードを記述するときに追加します。</span><span class="sxs-lookup"><span data-stu-id="54411-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="54411-216">`updateStockPrice`ここで`Clients.All`参照できるのは、動的であるため、アプリが実行時に式を評価することを意味します。</span><span class="sxs-lookup"><span data-stu-id="54411-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="54411-217">このメソッド呼び出しが実行されると、SignalR はメソッド名とパラメーター値をクライアントに送信し、クライアントに という`updateStockPrice`名前のメソッドがある場合、アプリはそのメソッドを呼び出してパラメーター値を渡します。</span><span class="sxs-lookup"><span data-stu-id="54411-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="54411-218">`Clients.All`は、すべてのクライアントに送信することを意味します。</span><span class="sxs-lookup"><span data-stu-id="54411-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="54411-219">SignalR には、送信先のクライアントまたはクライアント グループを指定するその他のオプションが用意されています。</span><span class="sxs-lookup"><span data-stu-id="54411-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="54411-220">詳細については、「[ハブ接続コンテキスト](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="54411-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="54411-221">シグナル R ルートを登録する</span><span class="sxs-lookup"><span data-stu-id="54411-221">Register the SignalR route</span></span>

<span data-ttu-id="54411-222">サーバーは、どの URL をインターセプトして SignalR に送信するかを知る必要があります。</span><span class="sxs-lookup"><span data-stu-id="54411-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="54411-223">これを行うには、OWIN スタートアップ クラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="54411-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="54411-224">**ソリューション エクスプローラ**で、プロジェクトを右クリックし、[**Add** > **新しい項目**の追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="54411-225">[**新しい項目の追加 - SignalR.StockTicker]** **で 、[インストール済みの** > **Visual C#** > **Web]** を選択し **、[OWIN スタートアップ クラス**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="54411-226">クラスに*Startup*という名前を付け **、[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="54411-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="54411-227">*Startup.cs*ファイルの既定のコードを次のコードで置き換えます。</span><span class="sxs-lookup"><span data-stu-id="54411-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="54411-228">これで、サーバー コードの設定が完了しました。</span><span class="sxs-lookup"><span data-stu-id="54411-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="54411-229">次のセクションでは、クライアントを設定します。</span><span class="sxs-lookup"><span data-stu-id="54411-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="54411-230">クライアント コードを設定する</span><span class="sxs-lookup"><span data-stu-id="54411-230">Set up the client code</span></span>

<span data-ttu-id="54411-231">このセクションでは、クライアントで実行されるコードを設定します。</span><span class="sxs-lookup"><span data-stu-id="54411-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="54411-232">HTML ページと Java スクリプト ファイルを作成する</span><span class="sxs-lookup"><span data-stu-id="54411-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="54411-233">HTML ページにデータが表示され、JavaScript ファイルがデータを整理します。</span><span class="sxs-lookup"><span data-stu-id="54411-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="54411-234">ストックティッカーを作成します。</span><span class="sxs-lookup"><span data-stu-id="54411-234">Create StockTicker.html</span></span>

<span data-ttu-id="54411-235">最初に、HTML クライアントを追加します。</span><span class="sxs-lookup"><span data-stu-id="54411-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="54411-236">**ソリューション エクスプローラ**で、プロジェクトを右クリックし **、[HTML ページ**の**追加** > ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="54411-237">ファイルに*StockTicker という名前を付け\*\*\*、[OK]*\* を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="54411-238">*StockTicker.html*ファイルの既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="54411-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="54411-239">HTML では、5 つの列、ヘッダー行、および 5 つの列すべてにまたがる単一のセルを持つデータ行を持つテーブルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="54411-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="54411-240">データ行は"読み込み中."を示しています。アプリが起動すると、一時的に。</span><span class="sxs-lookup"><span data-stu-id="54411-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="54411-241">JavaScript コードは、その行を削除し、サーバーから取得したストック データを含むその行を追加します。</span><span class="sxs-lookup"><span data-stu-id="54411-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="54411-242">スクリプト タグは次の項目を指定します。</span><span class="sxs-lookup"><span data-stu-id="54411-242">The script tags specify:</span></span>

    * <span data-ttu-id="54411-243">jQuery スクリプト ファイル。</span><span class="sxs-lookup"><span data-stu-id="54411-243">The jQuery script file.</span></span>

    * <span data-ttu-id="54411-244">SignalR コア スクリプト ファイル。</span><span class="sxs-lookup"><span data-stu-id="54411-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="54411-245">SignalR プロキシ スクリプト ファイル。</span><span class="sxs-lookup"><span data-stu-id="54411-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="54411-246">後で作成する StockTicker スクリプト ファイル。</span><span class="sxs-lookup"><span data-stu-id="54411-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="54411-247">アプリは、SignalR プロキシ スクリプト ファイルを動的に生成します。</span><span class="sxs-lookup"><span data-stu-id="54411-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="54411-248">"/signalr/hubs" URL を指定し、ハブ クラスのメソッド (この場合は) のメソッド`StockTickerHub.GetAllStocks`のプロキシ メソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="54411-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="54411-249">必要に応じて[、SignalR ユーティリティ](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)を使用してこの JavaScript ファイルを手動で生成できます。</span><span class="sxs-lookup"><span data-stu-id="54411-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="54411-250">メソッド呼び出しで動的ファイルの作成を`MapHubs`無効にすることを忘れないでください。</span><span class="sxs-lookup"><span data-stu-id="54411-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="54411-251">**ソリューション エクスプローラ**で、[**スクリプト]** を展開します。</span><span class="sxs-lookup"><span data-stu-id="54411-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="54411-252">jQuery と SignalR のスクリプト ライブラリは、プロジェクトで表示されます。</span><span class="sxs-lookup"><span data-stu-id="54411-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="54411-253">パッケージ マネージャーは、SignalR スクリプトの新しいバージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="54411-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="54411-254">コード ブロック内のスクリプト参照を、プロジェクト内のスクリプト ファイルのバージョンに対応するように更新します。</span><span class="sxs-lookup"><span data-stu-id="54411-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="54411-255">**ソリューション エクスプローラー**で、 *[ StockTicker.html*] を右クリックし、[**スタート ページとして設定**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="54411-256">ストックティッカー.jsを作成します。</span><span class="sxs-lookup"><span data-stu-id="54411-256">Create StockTicker.js</span></span>

<span data-ttu-id="54411-257">次に、JavaScript ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="54411-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="54411-258">**ソリューション エクスプローラー**で、プロジェクトを右クリックし **、[JavaScript ファイル**の**追加** > ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="54411-259">ファイルに*StockTicker という名前を付け\*\*\*、[OK]*\* を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="54411-260">次のコードを*StockTicker.js*ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="54411-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="54411-261">クライアント コードを確認する</span><span class="sxs-lookup"><span data-stu-id="54411-261">Examine the client code</span></span>

<span data-ttu-id="54411-262">クライアント コードを調べると、クライアント コードがサーバー コードと対話してアプリを動作させる方法を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="54411-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="54411-263">接続の開始</span><span class="sxs-lookup"><span data-stu-id="54411-263">Starting the connection</span></span>

<span data-ttu-id="54411-264">`$.connection`は SignalR プロキシを指します。</span><span class="sxs-lookup"><span data-stu-id="54411-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="54411-265">コードは、クラスのプロキシへの参照を`StockTickerHub`取得し、変数に`ticker`入れます。</span><span class="sxs-lookup"><span data-stu-id="54411-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="54411-266">プロキシ名は、`HubName`属性によって設定された名前です。</span><span class="sxs-lookup"><span data-stu-id="54411-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="54411-267">すべての変数と関数を定義した後、ファイル内のコードの最後の行は SignalR 関数を呼び出すことによって`start`SignalR 接続を初期化します。</span><span class="sxs-lookup"><span data-stu-id="54411-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="54411-268">この`start`関数は非同期的に実行され、 [jQuery Deferred オブジェクト](http://api.jquery.com/category/deferred-object/)を返します。</span><span class="sxs-lookup"><span data-stu-id="54411-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="54411-269">done 関数を呼び出して、アプリが非同期アクションを完了したときに呼び出す関数を指定できます。</span><span class="sxs-lookup"><span data-stu-id="54411-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="54411-270">すべての株式を取得する</span><span class="sxs-lookup"><span data-stu-id="54411-270">Getting all the stocks</span></span>

<span data-ttu-id="54411-271">この`init`関数は、`getAllStocks`サーバー上の関数を呼び出し、サーバーが返す情報を使用してストック テーブルを更新します。</span><span class="sxs-lookup"><span data-stu-id="54411-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="54411-272">デフォルトでは、メソッド名がサーバー上で pascal で大文字と小文字を区別されていても、クライアントで camelCasing を使用する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="54411-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="54411-273">CamelCasing 規則はメソッドにのみ適用され、オブジェクトには適用されません。</span><span class="sxs-lookup"><span data-stu-id="54411-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="54411-274">たとえば`stock.Symbol`、 および`stock.Price`を参照し、 `stock.symbol` `stock.price`または を参照します。</span><span class="sxs-lookup"><span data-stu-id="54411-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="54411-275">このメソッド`init`では`formatStock`、アプリケーションは、`stock`サーバーから受信した各ストック オブジェクトのテーブル行の HTML を作成します`supplant``rowTemplate``stock`。</span><span class="sxs-lookup"><span data-stu-id="54411-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="54411-276">結果の HTML は、ストック テーブルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="54411-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="54411-277">非同期`start`関数`init`の終了後に実行される`callback`関数として渡すことによって呼び出します。</span><span class="sxs-lookup"><span data-stu-id="54411-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="54411-278">呼び出`init`し後に別の JavaScript`start`ステートメントとして呼び出した場合、開始関数が接続の確立を完了するのを待たずにすぐに実行されるため、関数は失敗します。</span><span class="sxs-lookup"><span data-stu-id="54411-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="54411-279">その場合、`init`関数は、アプリがサーバー接続を`getAllStocks`確立する前に関数を呼び出そうとします。</span><span class="sxs-lookup"><span data-stu-id="54411-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="54411-280">更新された株価の取得</span><span class="sxs-lookup"><span data-stu-id="54411-280">Getting updated stock prices</span></span>

<span data-ttu-id="54411-281">サーバーは、株価を変更すると、接続されたクライアント`updateStockPrice`を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="54411-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="54411-282">アプリは、サーバーからの呼び出しで使用`stockTicker`できるように、プロキシのクライアント プロパティに関数を追加します。</span><span class="sxs-lookup"><span data-stu-id="54411-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="54411-283">この`updateStockPrice`関数は、サーバーから受信したストックオブジェクトを、関数と同じ方法でテーブル行`init`にフォーマットします。</span><span class="sxs-lookup"><span data-stu-id="54411-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="54411-284">テーブルに行を追加する代わりに、テーブル内のストックの現在の行を検索し、その行を新しい行に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="54411-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="54411-285">アプリケーションをテストする</span><span class="sxs-lookup"><span data-stu-id="54411-285">Test the application</span></span>

<span data-ttu-id="54411-286">アプリをテストして、動作していることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="54411-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="54411-287">すべてのブラウザウィンドウに株価が変動するライブストックテーブルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="54411-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="54411-288">ツールバーで[**スクリプトのデバッグ]** をオンにし、再生ボタンを選択して、デバッグモードでアプリを実行します。</span><span class="sxs-lookup"><span data-stu-id="54411-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![ユーザーがデバッグ モードをオンにし、再生を選択するスクリーンショット。](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="54411-290">ブラウザウィンドウが開き、**ライブストックテーブル**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="54411-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="54411-291">ストックテーブルには、最初は「読み込み.」が表示されます。ライン、その後、短い時間後に、アプリは、最初の株式データを表示し、株価が変化し始めます。</span><span class="sxs-lookup"><span data-stu-id="54411-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="54411-292">ブラウザから URL をコピーし、他の 2 つのブラウザを開いて、URL をアドレス バーに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="54411-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="54411-293">最初のストック表示は最初のブラウザと同じで、変更は同時に行われます。</span><span class="sxs-lookup"><span data-stu-id="54411-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="54411-294">すべてのブラウザーを閉じ、新しいブラウザーを開き、同じ URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="54411-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="54411-295">StockTicker シングルトン オブジェクトは、サーバーで実行し続けました。</span><span class="sxs-lookup"><span data-stu-id="54411-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="54411-296">**ライブストックテーブル**は、株式が変化し続けたことを示しています。</span><span class="sxs-lookup"><span data-stu-id="54411-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="54411-297">変更の数値がゼロの初期テーブルは表示されません。</span><span class="sxs-lookup"><span data-stu-id="54411-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="54411-298">ブラウザーを閉じます。</span><span class="sxs-lookup"><span data-stu-id="54411-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="54411-299">ログの有効化</span><span class="sxs-lookup"><span data-stu-id="54411-299">Enable logging</span></span>

<span data-ttu-id="54411-300">SignalR には、トラブルシューティングを支援するためにクライアントで有効にできるログ機能が組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="54411-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="54411-301">このセクションでは、ログ記録を有効にし、SignalR が使用している次のトランスポート方法のどれをログが示す例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="54411-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="54411-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket)、IIS 8 および現在のブラウザーでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="54411-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="54411-303">[サーバー送信イベント](http://en.wikipedia.org/wiki/Server-sent_events)、 Internet Explorer 以外のブラウザでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="54411-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="54411-304">[永遠にフレーム](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)、インターネットエクスプローラでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="54411-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="54411-305">[Ajax ロングポーリング](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)、すべてのブラウザでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="54411-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="54411-306">SignalR は、特定の接続に対して、サーバーとクライアントの両方がサポートする最適なトランスポート方法を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="54411-307">*ストックティッカー.js*を開きます。</span><span class="sxs-lookup"><span data-stu-id="54411-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="54411-308">ファイルの末尾で接続を初期化するコードの直前にログ記録を有効にするには、次の強調表示されたコード行を追加します。</span><span class="sxs-lookup"><span data-stu-id="54411-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="54411-309">**F5 キー**を押してプロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="54411-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="54411-310">ブラウザの開発者ツールウィンドウを開き、コンソールを選択してログを表示します。</span><span class="sxs-lookup"><span data-stu-id="54411-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="54411-311">新しい接続のトランスポート メソッドをネゴシエートする SignalR のログを表示するには、ページを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="54411-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="54411-312">Windows 8 (IIS 8) でインターネット エクスプローラ 10 を実行している場合、トランスポート方法は**WebSockets**です。</span><span class="sxs-lookup"><span data-stu-id="54411-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="54411-313">Windows 7 (IIS 7.5) でインターネット エクスプローラ 10 を実行している場合、トランスポート方法は**iframe**です。</span><span class="sxs-lookup"><span data-stu-id="54411-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="54411-314">Windows 8 (IIS 8) で Firefox 19 を実行している場合、転送方法は**WebSockets**です。</span><span class="sxs-lookup"><span data-stu-id="54411-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="54411-315">Firefox で Firebug アドインをインストールしてコンソール ウィンドウを表示します。</span><span class="sxs-lookup"><span data-stu-id="54411-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="54411-316">Windows 7 (IIS 7.5) で Firefox 19 を実行している場合、トランスポート方法は**サーバー送信**イベントです。</span><span class="sxs-lookup"><span data-stu-id="54411-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="54411-317">ストックティッカーサンプルのインストール</span><span class="sxs-lookup"><span data-stu-id="54411-317">Install the StockTicker sample</span></span>

<span data-ttu-id="54411-318">[サンプル](http://nuget.org/packages/microsoft.aspnet.signalr.sample)はストックティッカーアプリケーションをインストールします。</span><span class="sxs-lookup"><span data-stu-id="54411-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="54411-319">NuGet パッケージには、最初から作成した簡略化されたバージョンよりも多くの機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="54411-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="54411-320">チュートリアルのこのセクションでは、NuGet パッケージをインストールし、新機能と、それらを実装するコードを確認します。</span><span class="sxs-lookup"><span data-stu-id="54411-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54411-321">このチュートリアルの前の手順を実行せずにパッケージをインストールする場合は、プロジェクトに OWIN スタートアップ クラスを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="54411-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="54411-322">NuGet パッケージのこの readme.txt ファイルでは、この手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="54411-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="54411-323">サンプルの NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="54411-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="54411-324">**ソリューション エクスプローラー**でプロジェクトを右クリックし、**[NuGet パッケージの管理]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="54411-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="54411-325">**NuGet パッケージ マネージャー: SignalR.StockTicker**で **、[ 参照 ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="54411-326">[**パッケージ ソース**] で、[ **nuget.org**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="54411-327">検索ボックスに*SignalR.Sample*と入力**Microsoft.AspNet.SignalR.Sample** > し、[**インストール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="54411-328">**ソリューション エクスプローラー**で*SignalR.Sample*フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="54411-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="54411-329">SignalR.Sample パッケージをインストールすると、フォルダーとその内容が作成されました。</span><span class="sxs-lookup"><span data-stu-id="54411-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="54411-330">*SignalR.Sample*フォルダで *、StockTicker.html*を右クリックし、[**スタート ページとして設定]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="54411-331">SignalR.Sample NuGet パッケージをインストールすると、*スクリプト*フォルダーにある jQuery のバージョンが変更される場合があります。</span><span class="sxs-lookup"><span data-stu-id="54411-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="54411-332">パッケージが*SignalR.Sample*フォルダーにインストールする新しい*StockTicker.html*ファイルは、パッケージがインストールする jQuery バージョンと同期しますが、元の*StockTicker.html*ファイルを再度実行する場合は、最初にスクリプト タグの jQuery 参照を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="54411-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="54411-333">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="54411-333">Run the application</span></span>

 <span data-ttu-id="54411-334">最初のアプリで見たテーブルには便利な機能がありました。</span><span class="sxs-lookup"><span data-stu-id="54411-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="54411-335">完全な株式ティッカーアプリケーションは、新しい機能を示しています:株式データと、彼らが上昇し、下落するにつれて色を変更する株式を示す水平スクロールウィンドウ。</span><span class="sxs-lookup"><span data-stu-id="54411-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="54411-336">**F5** キーを押して、アプリを実行します。</span><span class="sxs-lookup"><span data-stu-id="54411-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="54411-337">初めてアプリを実行すると、「マーケット」は「閉じている」と、静的なテーブルとスクロールされていないティッカーウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="54411-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="54411-338">**[オープン マーケット**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-338">Select **Open Market**.</span></span>

    ![ライブティッカーのスクリーンショット。](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="54411-340">**[ライブストックティッカー** ]ボックスが水平にスクロールし始め、サーバーは定期的に株価の変化をランダムに放送し始めます。</span><span class="sxs-lookup"><span data-stu-id="54411-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="54411-341">株価が変化するたびに、アプリは**ライブストックテーブル**と**ライブストックティッカー**の両方を更新します。</span><span class="sxs-lookup"><span data-stu-id="54411-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="54411-342">株式の価格変動がプラスの場合、アプリは、背景が緑色の株式を示しています。</span><span class="sxs-lookup"><span data-stu-id="54411-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="54411-343">変更が負の場合、アプリは赤い背景でストックを表示します。</span><span class="sxs-lookup"><span data-stu-id="54411-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="54411-344">[**市場を閉じる**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="54411-345">テーブルの更新が停止します。</span><span class="sxs-lookup"><span data-stu-id="54411-345">The table updates stop.</span></span>

    * <span data-ttu-id="54411-346">ティッカーがスクロールを停止します。</span><span class="sxs-lookup"><span data-stu-id="54411-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="54411-347">**[リセット]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="54411-347">Select **Reset**.</span></span>

    * <span data-ttu-id="54411-348">すべてのストックデータがリセットされます。</span><span class="sxs-lookup"><span data-stu-id="54411-348">All stock data is reset.</span></span>

    * <span data-ttu-id="54411-349">アプリは、価格変更が開始される前に、初期状態を復元します。</span><span class="sxs-lookup"><span data-stu-id="54411-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="54411-350">ブラウザから URL をコピーし、他の 2 つのブラウザを開いて、URL をアドレス バーに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="54411-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="54411-351">各ブラウザーで、同じデータが同時に動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="54411-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="54411-352">コントロールのいずれかを選択すると、すべてのブラウザーが同時に同じ方法で応答します。</span><span class="sxs-lookup"><span data-stu-id="54411-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="54411-353">ライブストックティッカーディスプレイ</span><span class="sxs-lookup"><span data-stu-id="54411-353">Live Stock Ticker display</span></span>

<span data-ttu-id="54411-354">**ライブストックティッカー**表示は、CSSスタイルによって単一行`<div>`にフォーマットされた要素の順序なしリストです。</span><span class="sxs-lookup"><span data-stu-id="54411-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="54411-355">`<li>`アプリは、テンプレート文字列のプレースホルダーを置き換え、要素を要素に動的に追加することで、テーブルと同じ方法でティ`<li>`ッカーを初期化`<ul>`して更新します。</span><span class="sxs-lookup"><span data-stu-id="54411-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="54411-356">このアプリでは、jQuery`animate`関数を使用してスクロールして、 内の順序付けされていないリストの左`<div>`余白を変更します。</span><span class="sxs-lookup"><span data-stu-id="54411-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="54411-357">シグナルラー.サンプルストックティッカー.html</span><span class="sxs-lookup"><span data-stu-id="54411-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="54411-358">株式銘柄のHTMLコード:</span><span class="sxs-lookup"><span data-stu-id="54411-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="54411-359">シグナルラー.サンプルストックティッカー.css</span><span class="sxs-lookup"><span data-stu-id="54411-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="54411-360">株式証券のCSSコード:</span><span class="sxs-lookup"><span data-stu-id="54411-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="54411-361">信号機サンプルシグナル</span><span class="sxs-lookup"><span data-stu-id="54411-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="54411-362">スクロールさせる jQuery コード:</span><span class="sxs-lookup"><span data-stu-id="54411-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="54411-363">クライアントが呼び出すことができるサーバー上の追加メソッド</span><span class="sxs-lookup"><span data-stu-id="54411-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="54411-364">アプリに柔軟性を追加するために、アプリが呼び出すことができる追加のメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="54411-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="54411-365">シグナル・サンプル・StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="54411-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="54411-366">この`StockTickerHub`クラスは、クライアントが呼び出すことができる 4 つの追加メソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="54411-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="54411-367">アプリは、`OpenMarket`ページ`CloseMarket``Reset`上部のボタンに応答して 、 を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="54411-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="54411-368">1 つのクライアントが、すべてのクライアントに即時に伝達される状態の変化をトリガーするパターンを示します。</span><span class="sxs-lookup"><span data-stu-id="54411-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="54411-369">これらの各メソッドは、市場の状態を`StockTicker`変更する原因となるクラス内のメソッドを呼び出し、新しい状態をブロードキャストします。</span><span class="sxs-lookup"><span data-stu-id="54411-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="54411-370">シグナル・サンプル・StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="54411-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="54411-371">`StockTicker`クラスでは、アプリは、列挙値を返すプロパティを使用`MarketState`して市場の状態`MarketState`を維持します。</span><span class="sxs-lookup"><span data-stu-id="54411-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="54411-372">市場の状態を変更するメソッドのそれぞれは、クラスがスレッドセーフでなければならないの`StockTicker`で、ロックブロック内でそうします。</span><span class="sxs-lookup"><span data-stu-id="54411-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="54411-373">このコードがスレッド セーフであることを確認するには、指定`_marketState`された`MarketState``volatile`プロパティをバックするフィールド。</span><span class="sxs-lookup"><span data-stu-id="54411-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="54411-374">`BroadcastMarketStateChange`メソッドと`BroadcastMarketReset`メソッドは、クライアントで定義された異なるメソッドを呼び出す点を除いて、既に見た BroadcastStockPrice メソッドに似ています。</span><span class="sxs-lookup"><span data-stu-id="54411-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="54411-375">サーバーが呼び出すことができるクライアント上の追加機能</span><span class="sxs-lookup"><span data-stu-id="54411-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="54411-376">これで`updateStockPrice`、この関数はテーブルとティッカー表示の両方を処理し、`jQuery.Color`赤と緑の色を点滅させるために使用します。</span><span class="sxs-lookup"><span data-stu-id="54411-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="54411-377">*SignalR.StockTicker.js*の新機能は、市場の状態に基づいてボタンを有効または無効にします。</span><span class="sxs-lookup"><span data-stu-id="54411-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="54411-378">また、**ライブストックティッカー**水平スクロールを停止または開始します。</span><span class="sxs-lookup"><span data-stu-id="54411-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="54411-379">多くの関数がに`ticker.client`追加されているため、アプリは[jQuery 拡張関数](http://api.jquery.com/jQuery.extend/)を使用して追加します。</span><span class="sxs-lookup"><span data-stu-id="54411-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="54411-380">接続の確立後の追加クライアントセットアップ</span><span class="sxs-lookup"><span data-stu-id="54411-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="54411-381">クライアントが接続を確立した後、追加の作業を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="54411-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="54411-382">市場が開いているか閉じているかどうかを調べるので、`marketOpened`適切`marketClosed`なまたは機能を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="54411-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="54411-383">ボタンにサーバー メソッド呼び出しをアタッチします。</span><span class="sxs-lookup"><span data-stu-id="54411-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="54411-384">サーバー メソッドは、アプリが接続を確立するまでボタンに接続されません。</span><span class="sxs-lookup"><span data-stu-id="54411-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="54411-385">そのため、コードはサーバーメソッドを呼び出してから利用できません。</span><span class="sxs-lookup"><span data-stu-id="54411-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54411-386">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="54411-386">Additional resources</span></span>

<span data-ttu-id="54411-387">このチュートリアルでは、サーバーからすべての接続されたクライアントにメッセージをブロードキャストする SignalR アプリケーションをプログラムする方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="54411-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="54411-388">現在、メッセージを定期的にブロードキャストし、任意のクライアントからの通知に応答することができます。</span><span class="sxs-lookup"><span data-stu-id="54411-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="54411-389">マルチスレッド シングルトン インスタンスの概念を使用して、マルチプレイヤー オンライン ゲームシナリオでサーバーの状態を維持できます。</span><span class="sxs-lookup"><span data-stu-id="54411-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="54411-390">例については[、SignalR に基づく ShootR ゲームを](https://github.com/NTaylorMullen/ShootR)参照してください。</span><span class="sxs-lookup"><span data-stu-id="54411-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="54411-391">ピアツーピア通信シナリオを示すチュートリアルについては[、「SignalR の概要」および「SignalR](introduction-to-signalr.md)による[リアルタイム更新](tutorial-high-frequency-realtime-with-signalr.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="54411-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="54411-392">SignalR の詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="54411-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="54411-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="54411-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="54411-394">シグナル・プロジェクト</span><span class="sxs-lookup"><span data-stu-id="54411-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="54411-395">シグナル R の GitHub とサンプル</span><span class="sxs-lookup"><span data-stu-id="54411-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="54411-396">シグナルRウィキ</span><span class="sxs-lookup"><span data-stu-id="54411-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="54411-397">次のステップ</span><span class="sxs-lookup"><span data-stu-id="54411-397">Next steps</span></span>

<span data-ttu-id="54411-398">このチュートリアルでは、次のことを行いました。</span><span class="sxs-lookup"><span data-stu-id="54411-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="54411-399">プロジェクトを作成しました</span><span class="sxs-lookup"><span data-stu-id="54411-399">Created the project</span></span>
> * <span data-ttu-id="54411-400">サーバー コードを設定する</span><span class="sxs-lookup"><span data-stu-id="54411-400">Set up the server code</span></span>
> * <span data-ttu-id="54411-401">サーバー コードを調べた</span><span class="sxs-lookup"><span data-stu-id="54411-401">Examined the server code</span></span>
> * <span data-ttu-id="54411-402">クライアント コードを設定する</span><span class="sxs-lookup"><span data-stu-id="54411-402">Set up the client code</span></span>
> * <span data-ttu-id="54411-403">クライアント コードを調べた</span><span class="sxs-lookup"><span data-stu-id="54411-403">Examined the client code</span></span>
> * <span data-ttu-id="54411-404">アプリケーションをテストする</span><span class="sxs-lookup"><span data-stu-id="54411-404">Tested the application</span></span>
> * <span data-ttu-id="54411-405">有効なログ記録</span><span class="sxs-lookup"><span data-stu-id="54411-405">Enabled logging</span></span>

<span data-ttu-id="54411-406">次の記事に進み、SignalR 2 を使用するリアルタイム Web アプリケーションの作成方法ASP.NET学んでください。</span><span class="sxs-lookup"><span data-stu-id="54411-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="54411-407">SignalR を使用してリアルタイムの Web アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="54411-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
