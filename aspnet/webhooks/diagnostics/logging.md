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
# <a name="aspnet-webhooks-logging"></a>ウェブフックのログをASP.NETする

マイクロソフトASP.NET WebHooks は、問題や問題を報告する方法としてログ記録を使用しています。 デフォルトでは、ログは[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)を使用して書き込まれ、他のログ ストリームと同様に[トレース リスナーを](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)使用して追跡できます。

Web アプリケーションを Azure Web アプリとしてデプロイすると、ログは自動的に取得され、他の[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)ログと共に管理できます。 詳細については[、Azure アプリ サービスで Web アプリの診断ログを有効にするをご覧ください](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)。

また、「Visual Studio を[使用した Azure アプリ サービスでの Web アプリのトラブルシューティング](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)」で説明されているように、ログは Visual Studio 内から直接取得できます。

## <a name="redirecting-logs"></a>ログのリダイレクト

[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)にログを書き込む代わりに[、Log4Net](http://logging.apache.org/log4net/)や[NLog](http://nlog-project.org/)などのログ マネージャに直接ログを記録できる代替ログ実装を提供できます。 単に[ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)の実装を提供し、お好みの依存性注入エンジンでそれを登録し、それはマイクロソフトASP.NETWebHooksによって拾われます。 詳細については[、Web API 2 の依存関係ASP.NETインジェクション](https://www.asp.net/web-api/overview/advanced/dependency-injection)を参照してください。
