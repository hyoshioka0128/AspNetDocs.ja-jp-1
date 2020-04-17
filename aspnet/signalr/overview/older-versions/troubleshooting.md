---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR トラブルシューティング (SignalR 1.x) |マイクロソフトドキュメント
author: bradygaster
description: この資料では、SignalR アプリケーションの開発に関する一般的な問題について説明します。
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543094"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="5716f-103">SignalR トラブルシューティング (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="5716f-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="5716f-104">[パトリック・フレッチャー](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="5716f-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5716f-105">このドキュメントでは、SignalR に関する一般的なトラブルシューティングの問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="5716f-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="5716f-106">このドキュメントには、次のセクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5716f-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="5716f-107">クライアントとサーバー間のメソッドの呼び出しがサイレント で失敗する</span><span class="sxs-lookup"><span data-stu-id="5716f-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="5716f-108">その他の接続の問題</span><span class="sxs-lookup"><span data-stu-id="5716f-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="5716f-109">コンパイルおよびサーバー側エラー</span><span class="sxs-lookup"><span data-stu-id="5716f-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="5716f-110">ビジュアルスタジオの問題</span><span class="sxs-lookup"><span data-stu-id="5716f-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="5716f-111">インターネット インフォメーション サービスの問題</span><span class="sxs-lookup"><span data-stu-id="5716f-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="5716f-112">Azure の問題</span><span class="sxs-lookup"><span data-stu-id="5716f-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="5716f-113">クライアントとサーバー間のメソッドの呼び出しがサイレント で失敗する</span><span class="sxs-lookup"><span data-stu-id="5716f-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="5716f-114">このセクションでは、クライアントとサーバー間のメソッド呼び出しが、意味のあるエラー メッセージなしで失敗する原因について説明します。</span><span class="sxs-lookup"><span data-stu-id="5716f-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="5716f-115">SignalR アプリケーションでは、サーバーはクライアントが実装するメソッドに関する情報を持っていません。サーバーがクライアント メソッドを呼び出すと、メソッド名とパラメーター データがクライアントに送信され、サーバーが指定した形式で存在する場合にのみメソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="5716f-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="5716f-116">クライアントで一致するメソッドが見つからない場合は、何も起こらず、サーバー上でエラー メッセージは発生しません。</span><span class="sxs-lookup"><span data-stu-id="5716f-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="5716f-117">呼び出されないクライアント メソッドをさらに調査するには、ハブで start メソッドを呼び出す前にログ記録を有効にして、サーバーからどのような呼び出しが発生しているかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="5716f-117">To further investigate client methods not getting called, you can turn on logging before calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="5716f-118">JavaScript アプリケーションでのログ記録を有効にするには、「[クライアント側のログを有効にする方法 (JavaScript クライアント バージョン)」](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="5716f-119">.NET クライアント アプリケーションでログを有効にするには、「[クライアント側のログ記録を有効にする方法 (.NET クライアント バージョン)」](../guide-to-the-api/hubs-api-guide-net-client.md#logging)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="5716f-120">メソッドのスペルが間違っている、メソッドシグネチャが正しくない、またはハブ名が正しくない</span><span class="sxs-lookup"><span data-stu-id="5716f-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="5716f-121">呼び出されたメソッドの名前またはシグネチャがクライアントの適切なメソッドと完全に一致しない場合、呼び出しは失敗します。</span><span class="sxs-lookup"><span data-stu-id="5716f-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="5716f-122">サーバーによって呼び出されたメソッド名が、クライアント上のメソッドの名前と一致することを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="5716f-123">また、SignalR は、JavaScript で適切にキャメルケース メソッドを使用してハブ プロキシを作成するため`SendMessage`、サーバーで呼び出`sendMessage`されるメソッドはクライアント プロキシで呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="5716f-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="5716f-124">サーバー側コードで`HubName`属性を使用する場合は、使用される名前がクライアント上のハブの作成に使用された名前と一致することを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="5716f-125">属性を`HubName`使用しない場合は、JavaScript クライアントのハブの名前が、ChatHub ではなく chatHub などのキャメルケースであることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="5716f-126">クライアント上のメソッド名が重複しています</span><span class="sxs-lookup"><span data-stu-id="5716f-126">Duplicate method name on client</span></span>

<span data-ttu-id="5716f-127">大文字と小文字の違いだけが異なるメソッドがクライアントに重複していないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="5716f-128">クライアント アプリケーションに という`sendMessage`メソッドがある場合は、 メソッドも呼び出`SendMessage`されていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="5716f-129">クライアントで JSON パーサーが見つからない</span><span class="sxs-lookup"><span data-stu-id="5716f-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="5716f-130">SignalR は、サーバーとクライアント間の呼び出しをシリアル化するために、JSON パーサーが存在する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5716f-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="5716f-131">クライアントに組み込みの JSON パーサー (Internet Explorer 7 など) がない場合は、アプリケーションに JSON パーサーを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="5716f-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="5716f-132">JSON パーサーは[ここから](http://nuget.org/packages/json2)ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="5716f-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="5716f-133">ハブと永続接続の構文を混在させる</span><span class="sxs-lookup"><span data-stu-id="5716f-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="5716f-134">SignalR は、ハブと永続接続の 2 つの通信モデルを使用します。</span><span class="sxs-lookup"><span data-stu-id="5716f-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="5716f-135">クライアント コードでは、これら 2 つの通信モデルを呼び出す構文が異なります。</span><span class="sxs-lookup"><span data-stu-id="5716f-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="5716f-136">サーバー コードにハブを追加した場合は、すべてのクライアント コードで適切なハブ構文が使用されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="5716f-137">**クライアントで永続的な接続を作成する JavaScript クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="5716f-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="5716f-138">**JavaScript クライアントでハブ プロキシを作成する JavaScript クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="5716f-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="5716f-139">**ルートを永続的な接続にマップする C# サーバー コード**</span><span class="sxs-lookup"><span data-stu-id="5716f-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="5716f-140">**ハブへのルートをマップする C# サーバー コード、または複数のアプリケーションがある場合は複数のハブにルーティングする**</span><span class="sxs-lookup"><span data-stu-id="5716f-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="5716f-141">サブスクリプションが追加される前に接続が開始されました</span><span class="sxs-lookup"><span data-stu-id="5716f-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="5716f-142">サーバーから呼び出すことができるメソッドがプロキシに追加される前にハブの接続が開始された場合、メッセージは受信されません。</span><span class="sxs-lookup"><span data-stu-id="5716f-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="5716f-143">次の JavaScript コードは、ハブを正しく起動しません。</span><span class="sxs-lookup"><span data-stu-id="5716f-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="5716f-144">**ハブ メッセージの受信を許可しない不正な JavaScript クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="5716f-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="5716f-145">代わりに、Start を呼び出す前にメソッド サブスクリプションを追加します。</span><span class="sxs-lookup"><span data-stu-id="5716f-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="5716f-146">**ハブにサブスクリプションを正しく追加する JavaScript クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="5716f-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="5716f-147">ハブ プロキシにメソッド名がありません</span><span class="sxs-lookup"><span data-stu-id="5716f-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="5716f-148">サーバーで定義されているメソッドがクライアントでサブスクライブされていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="5716f-149">サーバーがメソッドを定義しても、クライアント プロキシに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5716f-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="5716f-150">メソッドは、次の方法でクライアント プロキシに追加できます (メソッドはハブの`client`メンバーに直接追加されません)。</span><span class="sxs-lookup"><span data-stu-id="5716f-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="5716f-151">**ハブ プロキシにメソッドを追加する JavaScript クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="5716f-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="5716f-152">パブリックとして宣言されていないハブまたはハブ メソッド</span><span class="sxs-lookup"><span data-stu-id="5716f-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="5716f-153">クライアントで表示するには、ハブの実装とメソッドを`public`として宣言する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5716f-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="5716f-154">別のアプリケーションからハブにアクセスする</span><span class="sxs-lookup"><span data-stu-id="5716f-154">Accessing hub from a different application</span></span>

<span data-ttu-id="5716f-155">SignalR ハブは、SignalR クライアントを実装するアプリケーションを介してのみアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="5716f-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="5716f-156">SignalR は、他の通信ライブラリ (SOAP や WCF Web サービスなど) と相互運用できません。ターゲット プラットフォームで使用できる SignalR クライアントがない場合は、サーバーのエンドポイントに直接アクセスできません。</span><span class="sxs-lookup"><span data-stu-id="5716f-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="5716f-157">データの手動シリアル化</span><span class="sxs-lookup"><span data-stu-id="5716f-157">Manually serializing data</span></span>

<span data-ttu-id="5716f-158">SignalR は自動的に JSON を使用してメソッドのパラメーターをシリアル化します。</span><span class="sxs-lookup"><span data-stu-id="5716f-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="5716f-159">リモート ハブ メソッドが OnDisconnected 関数のクライアントで実行されない</span><span class="sxs-lookup"><span data-stu-id="5716f-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="5716f-160">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="5716f-160">This behavior is by design.</span></span> <span data-ttu-id="5716f-161">呼`OnDisconnected`び出されると、ハブは既に状態`Disconnected`に入っており、それ以上のハブ メソッドを呼び出す必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5716f-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="5716f-162">**OnDisconnected イベントでコードを正しく実行する C# サーバー コード**</span><span class="sxs-lookup"><span data-stu-id="5716f-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="5716f-163">接続の制限に達しました</span><span class="sxs-lookup"><span data-stu-id="5716f-163">Connection limit reached</span></span>

<span data-ttu-id="5716f-164">Windows 7 のようなクライアント オペレーティング システムで IIS のフル バージョンを使用する場合、10 接続の制限が課されます。</span><span class="sxs-lookup"><span data-stu-id="5716f-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="5716f-165">クライアント OS を使用する場合は、代わりに IIS Express を使用してこの制限を回避します。</span><span class="sxs-lookup"><span data-stu-id="5716f-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="5716f-166">クロスドメイン接続が正しく設定されていません</span><span class="sxs-lookup"><span data-stu-id="5716f-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="5716f-167">クロスドメイン接続 (SignalR URL がホスト ページと同じドメインにない接続) が正しく設定されていない場合、エラー メッセージが表示されずに接続が失敗する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5716f-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="5716f-168">クロスドメイン通信を有効にする方法については、クロス[ドメイン接続を確立する方法を](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="5716f-169">NET クライアントで NTLM (アクティブ ディレクトリ) を使用した接続が機能しない</span><span class="sxs-lookup"><span data-stu-id="5716f-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="5716f-170">ドメイン セキュリティを使用する .NET クライアント アプリケーションの接続は、接続が正しく構成されていないと失敗することがあります。</span><span class="sxs-lookup"><span data-stu-id="5716f-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="5716f-171">ドメイン環境で SignalR を使用するには、次のように必要な接続プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="5716f-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="5716f-172">**接続資格情報を実装する C# クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="5716f-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="5716f-173">その他の接続の問題</span><span class="sxs-lookup"><span data-stu-id="5716f-173">Other connection issues</span></span>

<span data-ttu-id="5716f-174">ここでは、接続中に発生する特定の現象やエラー メッセージの原因と解決策について説明します。</span><span class="sxs-lookup"><span data-stu-id="5716f-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="5716f-175">「データを送信する前に Start を呼び出す必要があります」エラー</span><span class="sxs-lookup"><span data-stu-id="5716f-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="5716f-176">このエラーは、接続が開始される前にコードが SignalR オブジェクトを参照している場合に一般的に発生します。</span><span class="sxs-lookup"><span data-stu-id="5716f-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="5716f-177">サーバーで定義されたメソッドを呼び出すハンドラなどのワイヤアップは、接続の完了後に追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5716f-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="5716f-178">呼`Start`び出しは非同期であるため、呼び出しの完了前に呼び出し後のコードが実行される可能性があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="5716f-179">接続が完全に開始された後にハンドラーを追加する最善の方法は、start メソッドにパラメーターとして渡されるコールバック関数にハンドラーを追加することです。</span><span class="sxs-lookup"><span data-stu-id="5716f-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="5716f-180">**SignalR オブジェクトを参照するイベント ハンドラーを正しく追加する JavaScript クライアント コード**</span><span class="sxs-lookup"><span data-stu-id="5716f-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="5716f-181">このエラーは、SignalR オブジェクトが参照されている間に接続が停止した場合にも表示されます。</span><span class="sxs-lookup"><span data-stu-id="5716f-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="5716f-182">「301 永久に移動」または「302 一時的に移動」エラー</span><span class="sxs-lookup"><span data-stu-id="5716f-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="5716f-183">このエラーは、プロジェクトに SignalR という名前のフォルダーが含まれている場合に表示され、自動的に作成されたプロキシに干渉します。</span><span class="sxs-lookup"><span data-stu-id="5716f-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="5716f-184">このエラーを回避するには、アプリケーションで呼び出`SignalR`されるフォルダーを使用したり、自動プロキシ生成をオフにしたりしないでください。</span><span class="sxs-lookup"><span data-stu-id="5716f-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="5716f-185">詳細については[、「生成されたプロキシと、そのプロキシがあなたのために何をするのか](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="5716f-186">NET または Silverlight クライアントで "403 禁止" エラーが発生しました</span><span class="sxs-lookup"><span data-stu-id="5716f-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="5716f-187">このエラーは、ドメイン間通信が適切に有効になっていないドメイン間の環境で発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5716f-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="5716f-188">クロスドメイン通信を有効にする方法については、クロス[ドメイン接続を確立する方法を](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="5716f-189">Silverlight クライアントでドメイン間接続を確立するには[、「Silverlight クライアントからのドメイン間接続](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="5716f-190">"404 見つかりません" エラー</span><span class="sxs-lookup"><span data-stu-id="5716f-190">"404 Not Found" error</span></span>

<span data-ttu-id="5716f-191">この問題には、いくつかの原因があります。</span><span class="sxs-lookup"><span data-stu-id="5716f-191">There are several causes for this issue.</span></span> <span data-ttu-id="5716f-192">次のすべてを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-192">Verify all of the following:</span></span>

- <span data-ttu-id="5716f-193">**ハブ プロキシ アドレス参照が正しくフォーマットされていません:** このエラーは、生成されたハブ プロキシ アドレスへの参照が正しくフォーマットされていない場合に一般的に発生します。</span><span class="sxs-lookup"><span data-stu-id="5716f-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="5716f-194">ハブ アドレスへの参照が正しく行われたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="5716f-195">詳細については、[動的に生成されたプロキシを参照する方法](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="5716f-196">**ハブ ルートを追加する前に、アプリケーションにルートを追加します。** アプリケーションで他のルートを使用する場合は、最初に追加されたルートが`MapHubs`への呼び出しであることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="5716f-197">"500 内部サーバー エラー"</span><span class="sxs-lookup"><span data-stu-id="5716f-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="5716f-198">これは、さまざまな原因を持つ可能性のある非常に一般的なエラーです。</span><span class="sxs-lookup"><span data-stu-id="5716f-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="5716f-199">エラーの詳細は、サーバーのイベント ログに記録されるか、サーバーのデバッグを通じて見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="5716f-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="5716f-200">サーバーの詳細なエラーをオンにすることで、より詳細なエラー情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="5716f-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="5716f-201">詳細については、「 [Hub クラスのエラーを処理する方法](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="5716f-202">"型エラー:&lt;ハブ&gt;の型が定義されていません" エラー</span><span class="sxs-lookup"><span data-stu-id="5716f-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="5716f-203">このエラーは、呼び出し`MapHubs`が正しく行われなかった場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="5716f-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="5716f-204">詳細については[、SignalR ルートを登録し、SignalR オプションを構成する方法](../guide-to-the-api/hubs-api-guide-server.md#route)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="5716f-205">ユーザー コードによって処理されませんでした。</span><span class="sxs-lookup"><span data-stu-id="5716f-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="5716f-206">メソッドに送信するパラメーターにシリアル化できない型 (ファイル ハンドルやデータベース接続など) が含まれていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="5716f-207">クライアントに送信したくないサーバー側オブジェクトのメンバーを使用する必要がある場合 (セキュリティまたはシリアル化の理由から) 属性を使用します`JSONIgnore`。</span><span class="sxs-lookup"><span data-stu-id="5716f-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="5716f-208">「プロトコル エラー: 不明なトランスポート」エラー</span><span class="sxs-lookup"><span data-stu-id="5716f-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="5716f-209">このエラーは、クライアントが SignalR が使用するトランスポートをサポートしていない場合に発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="5716f-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="5716f-210">SignalR で使用できるブラウザーの詳細については、[トランスポートとフォールバック](../getting-started/introduction-to-signalr.md#transports)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="5716f-211">"JavaScript ハブ プロキシの生成が無効になっています。</span><span class="sxs-lookup"><span data-stu-id="5716f-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="5716f-212">このエラーは、`DisableJavaScriptProxies`で動的に生成されたプロキシへの参照を含む間に設定`signalr/hubs`されている場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="5716f-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="5716f-213">プロキシを手動で作成する方法の詳細については、「[生成されたプロキシと、そのプロキシが何を行うか」を](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="5716f-214">「接続 ID の形式が正しくありません」または「アクティブな SignalR 接続中にユーザー ID を変更することはできません」エラー</span><span class="sxs-lookup"><span data-stu-id="5716f-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="5716f-215">このエラーは、認証が使用されている場合に表示され、クライアントは接続が停止する前にログアウトされます。</span><span class="sxs-lookup"><span data-stu-id="5716f-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="5716f-216">解決策は、クライアントをログアウトする前に SignalR 接続を停止することです。</span><span class="sxs-lookup"><span data-stu-id="5716f-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="5716f-217">"キャッチされないエラー: シグナル: jQuery が見つかりません。</span><span class="sxs-lookup"><span data-stu-id="5716f-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="5716f-218">「SignalR.js ファイル」エラーの前に jQuery が参照されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="5716f-219">シグナル・クライアントを実行するには jQuery が必要です。</span><span class="sxs-lookup"><span data-stu-id="5716f-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="5716f-220">jQuery への参照が正しいこと、使用されるパスが有効であること、および jQuery への参照が SignalR への参照より前にあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="5716f-221">"キャッチされていない型エラー: 未定義の&lt;プロパティ&gt;' プロパティ ' を読み取ることができません" エラー</span><span class="sxs-lookup"><span data-stu-id="5716f-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="5716f-222">このエラーは、jQuery またはハブ プロキシが正しく参照されなかった場合に発生します。</span><span class="sxs-lookup"><span data-stu-id="5716f-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="5716f-223">jQuery とハブ プロキシへの参照が正しいこと、使用されるパスが有効であること、および jQuery への参照がハブ プロキシへの参照より前であることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="5716f-224">ハブ プロキシへの既定の参照は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5716f-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="5716f-225">**ハブ プロキシを正しく参照する HTML クライアント側コード**</span><span class="sxs-lookup"><span data-stu-id="5716f-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="5716f-226">"ユーザー コードによって処理されませんでした" エラー</span><span class="sxs-lookup"><span data-stu-id="5716f-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="5716f-227">このエラーは、誤ったオーバーロードが使用`Hub.On`されている場合に発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="5716f-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="5716f-228">メソッドに戻り値がある場合、戻り値の型はジェネリック型パラメーターとして指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5716f-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="5716f-229">**クライアントで定義されたメソッド (生成されたプロキシなし)**</span><span class="sxs-lookup"><span data-stu-id="5716f-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="5716f-230">接続 ID が一致しないか、ページ読み込み間の接続が中断される</span><span class="sxs-lookup"><span data-stu-id="5716f-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="5716f-231">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="5716f-231">This behavior is by design.</span></span> <span data-ttu-id="5716f-232">ハブ オブジェクトはページ オブジェクトでホストされるため、ページが更新されるとハブは破棄されます。</span><span class="sxs-lookup"><span data-stu-id="5716f-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="5716f-233">複数ページのアプリケーションでは、ページ読み込み間で一貫性を持たることができるように、ユーザーと接続 ID の間の関連付けを維持する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5716f-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="5716f-234">接続 ID は、`ConcurrentDictionary`オブジェクトまたはデータベースのサーバーに格納できます。</span><span class="sxs-lookup"><span data-stu-id="5716f-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="5716f-235">"値を null にすることはできません" エラー</span><span class="sxs-lookup"><span data-stu-id="5716f-235">"Value cannot be null" error</span></span>

<span data-ttu-id="5716f-236">オプション パラメータを持つサーバー側メソッドは現在サポートされていません。省略可能なパラメーターを省略すると、メソッドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="5716f-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="5716f-237">詳細については、「オプション[パラメータ](https://github.com/SignalR/SignalR/issues/324)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="5716f-238">「Firefox はアドレス&lt;&gt;でサーバーへの接続を確立できません」 Firebug のエラー</span><span class="sxs-lookup"><span data-stu-id="5716f-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="5716f-239">このエラー メッセージは、WebSocket トランスポートのネゴシエーションが失敗し、代わりに別のトランスポートが使用された場合に Firebug で表示されます。</span><span class="sxs-lookup"><span data-stu-id="5716f-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="5716f-240">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="5716f-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="5716f-241">NET クライアント アプリケーションでエラー「検証手順に従ってリモート証明書が無効です」</span><span class="sxs-lookup"><span data-stu-id="5716f-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="5716f-242">サーバーにカスタム クライアント証明書が必要な場合は、要求を行う前に接続に x509certificate を追加できます。</span><span class="sxs-lookup"><span data-stu-id="5716f-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="5716f-243">を使用して`Connection.AddClientCertificate`接続に証明書を追加します。</span><span class="sxs-lookup"><span data-stu-id="5716f-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="5716f-244">認証がタイムアウトした後に接続が切断される</span><span class="sxs-lookup"><span data-stu-id="5716f-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="5716f-245">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="5716f-245">This behavior is by design.</span></span> <span data-ttu-id="5716f-246">接続がアクティブな間は認証資格情報を変更できません。資格情報を更新するには、接続を停止して再起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5716f-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="5716f-247">オンコネクテッドは、jQueryモバイルを使用しているときに2回呼び出されます</span><span class="sxs-lookup"><span data-stu-id="5716f-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="5716f-248">jQuery Mobileの`initializePage`関数は、各ページのスクリプトを強制的に再実行し、2つ目の接続を作成します。</span><span class="sxs-lookup"><span data-stu-id="5716f-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="5716f-249">この問題の解決策は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="5716f-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="5716f-250">JavaScript ファイルの前に jQuery モバイルへの参照を含めます。</span><span class="sxs-lookup"><span data-stu-id="5716f-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="5716f-251">を設定`initializePage``$.mobile.autoInitializePage = false`して機能を無効にします。</span><span class="sxs-lookup"><span data-stu-id="5716f-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="5716f-252">接続を開始する前に、ページの初期化が完了するまで待ちます。</span><span class="sxs-lookup"><span data-stu-id="5716f-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="5716f-253">サーバー送信イベントを使用して Silverlight アプリケーションでメッセージが遅延する</span><span class="sxs-lookup"><span data-stu-id="5716f-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="5716f-254">サーバーが Silverlight でイベントを送信した場合、メッセージが遅延します。</span><span class="sxs-lookup"><span data-stu-id="5716f-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="5716f-255">代わりに長いポーリングを使用するには、接続を開始するときに次の方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="5716f-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="5716f-256">フォーエバー フレーム プロトコルを使用して "アクセス許可が拒否されました"</span><span class="sxs-lookup"><span data-stu-id="5716f-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="5716f-257">これは、ここで説明する既知の問題[です](https://github.com/SignalR/SignalR/issues/1963)。</span><span class="sxs-lookup"><span data-stu-id="5716f-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="5716f-258">この現象は最新の JQuery ライブラリを使用して発生することがあります。回避策は、アプリケーションを JQuery 1.8.2 にダウングレードすることです。</span><span class="sxs-lookup"><span data-stu-id="5716f-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="5716f-259">コンパイルおよびサーバー側エラー</span><span class="sxs-lookup"><span data-stu-id="5716f-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="5716f-260">次のセクションでは、コンパイラとサーバー側のランタイム エラーに対する可能な解決策について説明します。</span><span class="sxs-lookup"><span data-stu-id="5716f-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="5716f-261">ハブ インスタンスへの参照が null です</span><span class="sxs-lookup"><span data-stu-id="5716f-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="5716f-262">ハブ インスタンスは接続ごとに作成されるため、コード内にハブのインスタンスを自分で作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="5716f-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="5716f-263">ハブ自体の外部からハブのメソッドを呼び出す場合は、「ハブ コンテキストへの参照を取得する方法について、[ハブ クラス外からクライアント メソッドを呼び出し、グループを管理する方法](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5716f-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="5716f-264">セッションが null です。</span><span class="sxs-lookup"><span data-stu-id="5716f-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="5716f-265">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="5716f-265">This behavior is by design.</span></span> <span data-ttu-id="5716f-266">セッション状態を有効にすると双方向メッセージングが中断されるため、SignalR はASP.NETセッション状態をサポートしません。</span><span class="sxs-lookup"><span data-stu-id="5716f-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="5716f-267">オーバーライドする適切なメソッドがありません</span><span class="sxs-lookup"><span data-stu-id="5716f-267">No suitable method to override</span></span>

<span data-ttu-id="5716f-268">古いドキュメントやブログのコードを使用している場合、このエラーが表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="5716f-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="5716f-269">変更または非推奨のメソッドの名前を参照していないことを確認します (など`OnConnectedAsync`)。</span><span class="sxs-lookup"><span data-stu-id="5716f-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="5716f-270">をクリックします。</span><span class="sxs-lookup"><span data-stu-id="5716f-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="5716f-271">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="5716f-271">This behavior is by design.</span></span> <span data-ttu-id="5716f-272">このメンバーは非推奨であるため、使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="5716f-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="5716f-273">"signalr.hubs' という名前のルートは既にルート コレクションにあります」エラー</span><span class="sxs-lookup"><span data-stu-id="5716f-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="5716f-274">このエラーは、アプリケーションによって`MapHubs`2 回呼び出された場合に表示されます。</span><span class="sxs-lookup"><span data-stu-id="5716f-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="5716f-275">一部のアプリケーション`MapHubs`例では、グローバル アプリケーション ファイル内で直接呼び出します。他のクラスはラッパークラスで呼び出しを行います。</span><span class="sxs-lookup"><span data-stu-id="5716f-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="5716f-276">アプリケーションが両方とも実行しないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="5716f-277">ビジュアルスタジオの問題</span><span class="sxs-lookup"><span data-stu-id="5716f-277">Visual Studio issues</span></span>

<span data-ttu-id="5716f-278">このセクションでは、Visual Studio で発生する問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="5716f-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="5716f-279">ソリューション エクスプローラーに [スクリプト ドキュメント] ノードが表示されない</span><span class="sxs-lookup"><span data-stu-id="5716f-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="5716f-280">いくつかのチュートリアルでは、デバッグ中にソリューション エクスプローラーの "スクリプト ドキュメント" ノードに移動します。</span><span class="sxs-lookup"><span data-stu-id="5716f-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="5716f-281">このノードは JavaScript デバッガーによって生成され、Internet Explorer でブラウザー クライアントをデバッグしている間のみ表示されます。クロムまたは Firefox を使用している場合、ノードは表示されません。</span><span class="sxs-lookup"><span data-stu-id="5716f-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="5716f-282">また、別のクライアント デバッガー (Silverlight デバッガーなど) が実行されている場合、JavaScript デバッガーも実行されません。</span><span class="sxs-lookup"><span data-stu-id="5716f-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="5716f-283">信号は、Visual Studio 2008 以前では動作しません。</span><span class="sxs-lookup"><span data-stu-id="5716f-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="5716f-284">この動作は仕様です。</span><span class="sxs-lookup"><span data-stu-id="5716f-284">This behavior is by design.</span></span> <span data-ttu-id="5716f-285">SignalR は .NET Framework 4 以降を必要とします。このためには、Visual Studio 2010 以降で SignalR アプリケーションを開発する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5716f-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="5716f-286">IIS の問題</span><span class="sxs-lookup"><span data-stu-id="5716f-286">IIS issues</span></span>

<span data-ttu-id="5716f-287">ここでは、インターネット インフォメーション サービスに関する問題について説明します。</span><span class="sxs-lookup"><span data-stu-id="5716f-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="5716f-288">MapHubs 呼び出し後に Web サイトがクラッシュする</span><span class="sxs-lookup"><span data-stu-id="5716f-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="5716f-289">この問題は、SignalR の最新バージョンで修正されました。</span><span class="sxs-lookup"><span data-stu-id="5716f-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="5716f-290">NuGet を使用してインストールを更新して、最新のリリース バージョンの SignalR を使用していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5716f-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="5716f-291">Azure の問題</span><span class="sxs-lookup"><span data-stu-id="5716f-291">Azure issues</span></span>

<span data-ttu-id="5716f-292">このセクションには、Azure に関する問題が含まれています。</span><span class="sxs-lookup"><span data-stu-id="5716f-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="5716f-293">トピック名を変更した後、Azure バックプレーンを通じてメッセージが受信されない</span><span class="sxs-lookup"><span data-stu-id="5716f-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="5716f-294">Azure バックプレーンで使用されるトピックは、ユーザーが構成できるように意図されていません。</span><span class="sxs-lookup"><span data-stu-id="5716f-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
