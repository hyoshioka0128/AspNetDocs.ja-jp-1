---
uid: webhooks/diagnostics/logging
title: ASP.NETウェブフックのロギング |マイクロソフトドキュメント
author: rick-anderson
description: WebHook にログインASP.NET方法。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: 350732acbd3a73bddb8f8b20dcd50c225d89be82
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675341"
---
# <a name="aspnet-webhooks-logging"></a><span data-ttu-id="44440-103">ウェブフックのログをASP.NETする</span><span class="sxs-lookup"><span data-stu-id="44440-103">ASP.NET WebHooks logging</span></span>

<span data-ttu-id="44440-104">マイクロソフトASP.NET WebHooks は、問題や問題を報告する方法としてログ記録を使用しています。</span><span class="sxs-lookup"><span data-stu-id="44440-104">Microsoft ASP.NET WebHooks uses logging as a way of reporting issues and problems.</span></span> <span data-ttu-id="44440-105">デフォルトでは、ログは[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)を使用して書き込まれ、他のログ ストリームと同様に[トレース リスナーを](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)使用して追跡できます。</span><span class="sxs-lookup"><span data-stu-id="44440-105">By default logs are written using [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) where they can be manged using [Trace Listeners](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) like any other log stream.</span></span>

<span data-ttu-id="44440-106">Web アプリケーションを Azure Web アプリとしてデプロイすると、ログは自動的に取得され、他の[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)ログと共に管理できます。</span><span class="sxs-lookup"><span data-stu-id="44440-106">When deploying your Web Application as an Azure Web App, the logs are automatically picked up and can be managed together with any other [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) logging.</span></span> <span data-ttu-id="44440-107">詳細については[、Azure アプリ サービスで Web アプリの診断ログを有効にするをご覧ください](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)。</span><span class="sxs-lookup"><span data-stu-id="44440-107">For details, please see [Enable diagnostics logging for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span></span>

<span data-ttu-id="44440-108">また、「Visual Studio を[使用した Azure アプリ サービスでの Web アプリのトラブルシューティング](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)」で説明されているように、ログは Visual Studio 内から直接取得できます。</span><span class="sxs-lookup"><span data-stu-id="44440-108">In addition, logs can be obtained straight from inside Visual Studio as described in [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="redirecting-logs"></a><span data-ttu-id="44440-109">ログのリダイレクト</span><span class="sxs-lookup"><span data-stu-id="44440-109">Redirecting Logs</span></span>

<span data-ttu-id="44440-110">[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)にログを書き込む代わりに[、Log4Net](http://logging.apache.org/log4net/)や[NLog](http://nlog-project.org/)などのログ マネージャに直接ログを記録できる代替ログ実装を提供できます。</span><span class="sxs-lookup"><span data-stu-id="44440-110">Instead of writing logs to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace), it is possible to provide an alternate logging implementation that can log directly to a log manager such as [Log4Net](http://logging.apache.org/log4net/) and [NLog](http://nlog-project.org/).</span></span> <span data-ttu-id="44440-111">単に[ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)の実装を提供し、お好みの依存性注入エンジンでそれを登録し、それはマイクロソフトASP.NETWebHooksによって拾われます。</span><span class="sxs-lookup"><span data-stu-id="44440-111">Simply provide an implementation of [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) and register it with a dependency injection engine of your choice and it will get picked up by Microsoft ASP.NET WebHooks.</span></span> <span data-ttu-id="44440-112">詳細については[、Web API 2 の依存関係ASP.NETインジェクション](https://www.asp.net/web-api/overview/advanced/dependency-injection)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="44440-112">Please see [Dependency Injection in ASP.NET Web API 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) for details.</span></span>
