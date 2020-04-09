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
# <a name="aspnet-webhooks-receivers"></a>ASP.NETウェブフック受信機

WebHook を受信する送信者は、送信者が誰であるかによって異なります。 場合によっては、WebHook を登録する追加の手順があり、購読者が本当にリッスンしていることを確認します。 一部の WebHook は、HTTP POST 要求にイベント情報への参照のみを含むプッシュツープル モデルを提供し、その後独立して取得します。 多くの場合、セキュリティ モデルは多少異なります。

マイクロソフト ASP.NET WebHooks の目的は、特定のバリアントの WebHook を処理する方法を理解するのに多くの時間を費やすことなく、API を結び付けやすく、一貫性を高める方法を提供することです。

WebHook 受信側は、特定の送信側からの WebHook の受け入れと検証を行います。 WebHook レシーバーは、それぞれ独自の構成を持つ任意の数の WebHook をサポートできます。 たとえば、GitHub WebHook レシーバーは、任意の数の GitHub リポジトリから WebHook を受け入れることができます。

## <a name="webhook-receiver-uris"></a>ウェブフック受信機のURI

マイクロソフトASP.NETWebHookをインストールすると、オープンエンドのサービスからのWebHook要求を受け入れる一般的なWebHookコントローラが得られます。 要求が到着すると、特定の WebHook 送信側を処理するためにインストールした適切な受信者が選択されます。

このコントローラーの URI は、サービスに登録する WebHook URI であり、次の形式です。

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

セキュリティ上の理由から、多くの WebHook 受信機は URI が*https* URI であることを要求し、場合によっては、意図されたパーティだけが上記の URI に WebHook を送信できることを強制するために使用される追加のクエリ パラメーターを含める必要があります。

コンポーネント`<receiver>`は、受信者の名前`github`です。 `slack`

*{id}* は、特定の WebHook 受信側の構成を識別するために使用できるオプションの識別子です。 これは、特定の受信機にN WebHookを登録するために使用することができます。 たとえば、次の 3 つの URI を使用して、3 つの独立した WebHook に登録できます。

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>WebHook レシーバーのインストール

マイクロソフト ASP.NET WebHook を使用して WebHook を受信するには、まず、WebHook を受信するプロバイダーの Nuget パッケージをインストールします。 Nuget パッケージは、最後の部分がサポートされているサービスを示す[Microsoft.AspNet.WebHooks.Receivers.* という](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)名前です。 次に例を示します。

[ASP.NET WebHook によって](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)生成された WebHook を受信するためのサポートを提供[します](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)。

ボックスの一部からは、Dropbox、GitHub、MailChimp、PayPal、プッシャー、セールスフォース、スラック、ストライプ、トレロ、ワードプレスのサポートを見つけることができますが、他のプロバイダの任意の数をサポートすることは可能です。

## <a name="configuring-a-webhook-receiver"></a>WebHook レシーバーの構成

WebHook レシーバーは[IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)を介して構成され、そのインターフェイスの特定の実装は、任意の依存関係の注入モデルを使用して登録できます。 既定の実装では、Web.config ファイルで設定できるアプリケーション設定を使用するか、Azure Web Apps を使用する場合は[Azure ポータル](https://portal.azure.com/)を使用して設定できます。

![Azure App Settings](_static/AzureAppSettings.png)

アプリケーション設定キーの形式は次のとおりです。

```
MS_WebHookReceiverSecret_<receiver>
```

値は、WebHook が登録されている *{id}* 値に一致する値のコンマ区切りのリストです。

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>WebHook レシーバーの初期化

WebHook レシーバーは、通常 *、WebApiConfig*静的クラスで、それらを登録することによって初期化されます。

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
