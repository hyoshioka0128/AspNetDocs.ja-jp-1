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
# <a name="aspnet-webhooks-handlers"></a>ASP.NETの Web フック ハンドラー

WebHook 要求が WebHook 受信側によって検証されると、ユーザー コードで処理できるようになります。 これが*ハンドラ*の入ってくる場所です。 ハンドラーは[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)インターフェイスから派生しますが、通常はインターフェイスから直接派生するのではなく[、WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)クラスを使用します。

WebHook 要求は、1 つ以上のハンドラーで処理できます。 ハンドラは、Order が単純な整数である場合、それぞれの*Order*プロパティが、それぞれ最下位から最高の順に呼び出されます (1 ~ 100 の間に推奨されます)。

![WebHook ハンドラー順序プロパティ図](_static/Handlers.png)

ハンドラーは、必要に応じて、処理を停止し、応答を WebHook に HTTP 応答として返送する WebHookHandlerContext に*応答プロパティを*設定できます。 上記の場合、ハンドラ C は B より高い順序を持ち、B が応答を設定するため、呼び出されません。

通常、応答の設定は、応答が元の API に情報を返すことができる WebHook にのみ関連します。 これは、たとえば、応答が WebHook の元のチャネルにポストバックされる Slack WebHook の場合です。 ハンドラは、その特定の受信側からの WebHook のみを受信する場合に、Receiver プロパティを設定できます。 彼らは受信機を設定しない場合、彼らはそれらのすべてのために呼び出されます。

応答のもう 1 つの一般的な使用は *、WebHook*がアクティブでなくなり、それ以上要求を送信する必要がないことを示すために 410 Gone 応答を使用することです。

デフォルトでは、ハンドラはすべての WebHook 受信機によって呼び出されます。 ただし *、Receiver*プロパティがハンドラの名前に設定されている場合、そのハンドラはその受信側からの WebHook リクエストのみを受け取ります。

## <a name="processing-a-webhook"></a>ウェブフックの処理

ハンドラーが呼び出されると、WebHook 要求に関する情報を含む[WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs)を取得します。 データ (通常は HTTP 要求本文) は *、Data*プロパティから使用できます。

データの型は通常 JSON または HTML フォーム データですが、必要に応じてより具体的な型にキャストできます。 たとえば、ASP.NET WebHook によって生成されたカスタム WebHook は、次のように[カスタム通知](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs)の型にキャストできます。

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

  ## <a name="queued-processing"></a>キュー処理

ほとんどの WebHook 送信者は、数秒以内に応答が生成されない場合、WebHook を再送信します。 つまり、ハンドラーは、再度呼び出されるのではないために、その時間内に処理を完了する必要があります。

処理に時間がかかる場合、または別々に処理する方が良い場合は[、WebHook 要求](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)をキュー [(Azure Storage キュー](https://msdn.microsoft.com/library/azure/dd179353.aspx)など) に送信するために使用できます。

[実装](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)の概要は、ここで提供されています。

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
