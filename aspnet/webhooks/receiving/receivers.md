---
uid: webhooks/receiving/receivers
title: ASP.NETウェブフック受信機 |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NETウェブフック受信機
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: 60f46141b59fc3888a6480d8201160420469d1a7
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675163"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="504d3-103">ASP.NETウェブフック受信機</span><span class="sxs-lookup"><span data-stu-id="504d3-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="504d3-104">WebHook を受信する送信者は、送信者が誰であるかによって異なります。</span><span class="sxs-lookup"><span data-stu-id="504d3-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="504d3-105">場合によっては、WebHook を登録する追加の手順があり、購読者が本当にリッスンしていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="504d3-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="504d3-106">一部の WebHook は、HTTP POST 要求にイベント情報への参照のみを含むプッシュツープル モデルを提供し、その後独立して取得します。</span><span class="sxs-lookup"><span data-stu-id="504d3-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="504d3-107">多くの場合、セキュリティ モデルは多少異なります。</span><span class="sxs-lookup"><span data-stu-id="504d3-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="504d3-108">マイクロソフト ASP.NET WebHooks の目的は、特定のバリアントの WebHook を処理する方法を理解するのに多くの時間を費やすことなく、API を結び付けやすく、一貫性を高める方法を提供することです。</span><span class="sxs-lookup"><span data-stu-id="504d3-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="504d3-109">WebHook 受信側は、特定の送信側からの WebHook の受け入れと検証を行います。</span><span class="sxs-lookup"><span data-stu-id="504d3-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="504d3-110">WebHook レシーバーは、それぞれ独自の構成を持つ任意の数の WebHook をサポートできます。</span><span class="sxs-lookup"><span data-stu-id="504d3-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="504d3-111">たとえば、GitHub WebHook レシーバーは、任意の数の GitHub リポジトリから WebHook を受け入れることができます。</span><span class="sxs-lookup"><span data-stu-id="504d3-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="504d3-112">ウェブフック受信機のURI</span><span class="sxs-lookup"><span data-stu-id="504d3-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="504d3-113">マイクロソフトASP.NETWebHookをインストールすると、オープンエンドのサービスからのWebHook要求を受け入れる一般的なWebHookコントローラが得られます。</span><span class="sxs-lookup"><span data-stu-id="504d3-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="504d3-114">要求が到着すると、特定の WebHook 送信側を処理するためにインストールした適切な受信者が選択されます。</span><span class="sxs-lookup"><span data-stu-id="504d3-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="504d3-115">このコントローラーの URI は、サービスに登録する WebHook URI であり、次の形式です。</span><span class="sxs-lookup"><span data-stu-id="504d3-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="504d3-116">セキュリティ上の理由から、多くの WebHook 受信機は URI が*https* URI であることを要求し、場合によっては、意図されたパーティだけが上記の URI に WebHook を送信できることを強制するために使用される追加のクエリ パラメーターを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="504d3-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="504d3-117">コンポーネント`<receiver>`は、受信者の名前`github`です。 `slack`</span><span class="sxs-lookup"><span data-stu-id="504d3-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="504d3-118">*{id}* は、特定の WebHook 受信側の構成を識別するために使用できるオプションの識別子です。</span><span class="sxs-lookup"><span data-stu-id="504d3-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="504d3-119">これは、特定の受信機にN WebHookを登録するために使用することができます。</span><span class="sxs-lookup"><span data-stu-id="504d3-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="504d3-120">たとえば、次の 3 つの URI を使用して、3 つの独立した WebHook に登録できます。</span><span class="sxs-lookup"><span data-stu-id="504d3-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="504d3-121">WebHook レシーバーのインストール</span><span class="sxs-lookup"><span data-stu-id="504d3-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="504d3-122">マイクロソフト ASP.NET WebHook を使用して WebHook を受信するには、まず、WebHook を受信するプロバイダーの Nuget パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="504d3-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="504d3-123">Nuget パッケージは、最後の部分がサポートされているサービスを示す[Microsoft.AspNet.WebHooks.Receivers.\* という](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)名前です。</span><span class="sxs-lookup"><span data-stu-id="504d3-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="504d3-124">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="504d3-124">For example</span></span>

<span data-ttu-id="504d3-125">[ASP.NET WebHook によって](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)生成された WebHook を受信するためのサポートを提供[します](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)。</span><span class="sxs-lookup"><span data-stu-id="504d3-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="504d3-126">ボックスの一部からは、Dropbox、GitHub、MailChimp、PayPal、プッシャー、セールスフォース、スラック、ストライプ、トレロ、ワードプレスのサポートを見つけることができますが、他のプロバイダの任意の数をサポートすることは可能です。</span><span class="sxs-lookup"><span data-stu-id="504d3-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="504d3-127">WebHook レシーバーの構成</span><span class="sxs-lookup"><span data-stu-id="504d3-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="504d3-128">WebHook レシーバーは[IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)を介して構成され、そのインターフェイスの特定の実装は、任意の依存関係の注入モデルを使用して登録できます。</span><span class="sxs-lookup"><span data-stu-id="504d3-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="504d3-129">既定の実装では、Web.config ファイルで設定できるアプリケーション設定を使用するか、Azure Web Apps を使用する場合は[Azure ポータル](https://portal.azure.com/)を使用して設定できます。</span><span class="sxs-lookup"><span data-stu-id="504d3-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Azure App Settings](_static/AzureAppSettings.png)

<span data-ttu-id="504d3-131">アプリケーション設定キーの形式は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="504d3-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="504d3-132">値は、WebHook が登録されている *{id}* 値に一致する値のコンマ区切りのリストです。</span><span class="sxs-lookup"><span data-stu-id="504d3-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="504d3-133">WebHook レシーバーの初期化</span><span class="sxs-lookup"><span data-stu-id="504d3-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="504d3-134">WebHook レシーバーは、通常 *、WebApiConfig*静的クラスで、それらを登録することによって初期化されます。</span><span class="sxs-lookup"><span data-stu-id="504d3-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
