---
uid: webhooks/index
title: ウェブフックの概要をASP.NET |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NETウェブフックの概要。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa5fa190386ec803a6801de2d815c948677fe1f5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675442"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="e0fe1-103">ASP.NETウェブフックの概要</span><span class="sxs-lookup"><span data-stu-id="e0fe1-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="e0fe1-104">WebHooks は、Web API と SaaS サービスを結び付けるための単純なパブリッシュ/サブ モデルを提供する軽量 HTTP パターンです。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="e0fe1-105">サービスでイベントが発生すると、登録されたサブスクライバに HTTP POST 要求の形式で通知が送信されます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="e0fe1-106">POST 要求には、イベントに関する情報が含まれており、それに応じて受信側が動作することを可能にします。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="e0fe1-107">そのシンプルさのために、WebHookはすでに[Dropbox、GitHub、](http://dropbox.com/)[ビットバケット](https://bitbucket.org/)[、MailChimp、](http://www.mailchimp.com/)[ペイパル](http://www.paypal.com/)、[スラック](http://www.slack.com)、[ストライプ](http://www.stripe.com)、[トレロ](http://www.trello.com/)、および多くを含む多数のサービスによって公開されています。 [GitHub](https://www.github.com/)</span><span class="sxs-lookup"><span data-stu-id="e0fe1-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="e0fe1-108">たとえば[、Dropbox](http://dropbox.com/)でファイルが変更されたか、GitHub でコード変更が行われたか[、PayPal](http://www.paypal.com/)で支払いが開始されたか[、Trello](http://www.trello.com/)でカードが作成されたことを示す WebHook が考えます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="e0fe1-109">可能性は無限大です!</span><span class="sxs-lookup"><span data-stu-id="e0fe1-109">The possibilities are endless!</span></span>

<span data-ttu-id="e0fe1-110">マイクロソフト ASP.NET WebHooks では、ASP.NET アプリケーションの一部として WebHook の送受信を容易に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="e0fe1-111">受信側では、任意の数の WebHook プロバイダーから WebHook を受信および処理するための共通モデルを提供します。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="e0fe1-112">それは[、ドロップボックス](http://dropbox.com/)[、GitHub、](https://www.github.com/)[ビットバケット](https://bitbucket.org/)、[メールチンパンジー](http://www.mailchimp.com/)、[ペイパル](http://www.paypal.com/)、[プッシャー](http://www.pusher.com)、[セールスフォース](http://www.salesforce.com)、[スラック](http://www.slack.com)、[ストライプ](http://www.stripe.com)、[トレロ](http://www.trello.com/)、[ワードプレス](http://www.wordpress.com)、[ゼンデスク](https://www.zendesk.com/)のサポートを備えたボックスから出てきますが、より多くのサポートを追加するのは簡単です。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="e0fe1-113">送信側では、サブスクリプションの管理と格納、および適切なサブスクライバーセットへのイベント通知の送信をサポートします。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="e0fe1-114">これにより、購読者がサブスクライブできる独自のイベントセットを定義し、発生時に通知することができます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="e0fe1-115">シナリオに応じて、2 つの部分を一緒に使用することも、離れたりすることもできます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="e0fe1-116">他のサービスから WebHook を受信するだけで済む場合は、受信側の部分だけを使用できます。他のユーザーが使用できるように WebHook を公開するだけの場合は、それを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="e0fe1-117">コードは Web API 2 と ASP.NET MVC 5 ASP.NET対象とし[、GitHub で OSS](https://github.com/aspnet/WebHooks)として利用できます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="e0fe1-118">ウェブフックの概要</span><span class="sxs-lookup"><span data-stu-id="e0fe1-118">WebHooks Overview</span></span>

<span data-ttu-id="e0fe1-119">WebHooks は、サービス間での使用方法が異なるパターンですが、基本的な考え方は同じです。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="e0fe1-120">WebHook は、ユーザーが他の場所で発生したイベントをサブスクライブできる単純な pub/sub モデルと考えることができます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="e0fe1-121">イベント通知は、イベント自体に関する情報を含む HTTP POST 要求として伝達されます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="e0fe1-122">通常、HTTP POST 要求には、WebHook がトリガーされるイベントに関する情報を含む、WebHook の送信者によって決定される JSON オブジェクトまたは HTML フォーム データが含まれます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="e0fe1-123">たとえば[、GitHub](https://www.github.com/)からの WebHook POST 要求本文は、特定のリポジトリで開かれる新しい問題の結果として次のようになります。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="e0fe1-124">WebHook が実際に意図した送信者から送信されるようにするため、POST 要求は何らかの方法でセキュリティで保護され、受信側によって検証されます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="e0fe1-125">たとえば[、GitHub WebHooks](https://developer.github.com/webhooks/)には、要求本文のハッシュを含む*X ハブ署名*HTTP ヘッダーが含まれており、これは受信側の実装によってチェックされるため、心配する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="e0fe1-126">WebHook フローは、一般的に次のようになります。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="e0fe1-127">WebHook 送信者は、クライアントがサブスクライブできるイベントを公開します。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="e0fe1-128">イベントは、システムに対する監視可能な変更 (たとえば、新しいデータ項目が挿入された、プロセスが完了した、または他の何かを示します) を記述します。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="e0fe1-129">WebHook レシーバは、次の 4 つの項目から成る WebHook を登録してサブスクライブします。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="e0fe1-130">HTTP POST 要求の形式でイベント通知をポストする URI。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="e0fe1-131">WebHook を起動する特定のイベントを記述するフィルターのセット。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="e0fe1-132">HTTP POST 要求の署名に使用されるシークレット キー。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="e0fe1-133">HTTP POST 要求に含まれる追加データ。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="e0fe1-134">これは、たとえば、追加の HTTP ヘッダー フィールドや HTTP POST 要求本文に含まれるプロパティです。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="e0fe1-135">イベントが発生すると、一致する WebHook 登録が見つかり、HTTP POST 要求が送信されます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="e0fe1-136">通常、何らかの理由で受信者が応答しない場合、または HTTP POST 要求がエラー応答を返した場合、HTTP POST 要求の生成が複数回再試行されます。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="e0fe1-137">Webフック処理パイプライン</span><span class="sxs-lookup"><span data-stu-id="e0fe1-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="e0fe1-138">受信 WebHook の処理パイプラインをASP.NETマイクロソフトは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET Webhook 処理パイプライン](_static/WebHookReceivers.png)

<span data-ttu-id="e0fe1-140">ここでの 2 つの主要な概念は *、レシーバー*と*ハンドラーです*。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="e0fe1-141">*受信側は、* 特定の送信者からの WebHook の特定のフレーバーを処理し、WebHook 要求が実際に意図された送信者から送信されていることを確認するためのセキュリティ チェックを実施する責任があります。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="e0fe1-142">*ハンドラー*は通常、ユーザー コードが特定の WebHook を処理する場所です。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="e0fe1-143">以下のノードでは、これらの概念の詳細について説明します。</span><span class="sxs-lookup"><span data-stu-id="e0fe1-143">In the following nodes these concepts are described in more details.</span></span>
