---
uid: webhooks/receiving/handlers
title: ASP.NETウェブフックハンドラ |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NET WebHook で要求を処理する方法。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: ff12dd8df167eca17ecbd9f03a71807d44af2b30
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675213"
---
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="94a09-103">ASP.NETの Web フック ハンドラー</span><span class="sxs-lookup"><span data-stu-id="94a09-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="94a09-104">WebHook 要求が WebHook 受信側によって検証されると、ユーザー コードで処理できるようになります。</span><span class="sxs-lookup"><span data-stu-id="94a09-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="94a09-105">これが*ハンドラ*の入ってくる場所です。</span><span class="sxs-lookup"><span data-stu-id="94a09-105">This is where *handlers* come in.</span></span> <span data-ttu-id="94a09-106">ハンドラーは[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)インターフェイスから派生しますが、通常はインターフェイスから直接派生するのではなく[、WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)クラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="94a09-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="94a09-107">WebHook 要求は、1 つ以上のハンドラーで処理できます。</span><span class="sxs-lookup"><span data-stu-id="94a09-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="94a09-108">ハンドラは、Order が単純な整数である場合、それぞれの*Order*プロパティが、それぞれ最下位から最高の順に呼び出されます (1 ~ 100 の間に推奨されます)。</span><span class="sxs-lookup"><span data-stu-id="94a09-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![WebHook ハンドラー順序プロパティ図](_static/Handlers.png)

<span data-ttu-id="94a09-110">ハンドラーは、必要に応じて、処理を停止し、応答を WebHook に HTTP 応答として返送する WebHookHandlerContext に*応答プロパティを*設定できます。</span><span class="sxs-lookup"><span data-stu-id="94a09-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="94a09-111">上記の場合、ハンドラ C は B より高い順序を持ち、B が応答を設定するため、呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="94a09-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="94a09-112">通常、応答の設定は、応答が元の API に情報を返すことができる WebHook にのみ関連します。</span><span class="sxs-lookup"><span data-stu-id="94a09-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="94a09-113">これは、たとえば、応答が WebHook の元のチャネルにポストバックされる Slack WebHook の場合です。</span><span class="sxs-lookup"><span data-stu-id="94a09-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="94a09-114">ハンドラは、その特定の受信側からの WebHook のみを受信する場合に、Receiver プロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="94a09-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="94a09-115">彼らは受信機を設定しない場合、彼らはそれらのすべてのために呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="94a09-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="94a09-116">応答のもう 1 つの一般的な使用は *、WebHook*がアクティブでなくなり、それ以上要求を送信する必要がないことを示すために 410 Gone 応答を使用することです。</span><span class="sxs-lookup"><span data-stu-id="94a09-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="94a09-117">デフォルトでは、ハンドラはすべての WebHook 受信機によって呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="94a09-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="94a09-118">ただし *、Receiver*プロパティがハンドラの名前に設定されている場合、そのハンドラはその受信側からの WebHook リクエストのみを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="94a09-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="94a09-119">ウェブフックの処理</span><span class="sxs-lookup"><span data-stu-id="94a09-119">Processing a WebHook</span></span>

<span data-ttu-id="94a09-120">ハンドラーが呼び出されると、WebHook 要求に関する情報を含む[WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs)を取得します。</span><span class="sxs-lookup"><span data-stu-id="94a09-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="94a09-121">データ (通常は HTTP 要求本文) は *、Data*プロパティから使用できます。</span><span class="sxs-lookup"><span data-stu-id="94a09-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="94a09-122">データの型は通常 JSON または HTML フォーム データですが、必要に応じてより具体的な型にキャストできます。</span><span class="sxs-lookup"><span data-stu-id="94a09-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="94a09-123">たとえば、ASP.NET WebHook によって生成されたカスタム WebHook は、次のように[カスタム通知](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs)の型にキャストできます。</span><span class="sxs-lookup"><span data-stu-id="94a09-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a><span data-ttu-id="94a09-124">キュー処理</span><span class="sxs-lookup"><span data-stu-id="94a09-124">Queued Processing</span></span>

<span data-ttu-id="94a09-125">ほとんどの WebHook 送信者は、数秒以内に応答が生成されない場合、WebHook を再送信します。</span><span class="sxs-lookup"><span data-stu-id="94a09-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="94a09-126">つまり、ハンドラーは、再度呼び出されるのではないために、その時間内に処理を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="94a09-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="94a09-127">処理に時間がかかる場合、または別々に処理する方が良い場合は[、WebHook 要求](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)をキュー [(Azure Storage キュー](https://msdn.microsoft.com/library/azure/dd179353.aspx)など) に送信するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="94a09-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="94a09-128">[実装](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)の概要は、ここで提供されています。</span><span class="sxs-lookup"><span data-stu-id="94a09-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
