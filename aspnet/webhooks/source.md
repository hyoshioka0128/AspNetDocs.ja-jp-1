---
uid: webhooks/source
title: ASP.NET WebHooks ソース コードと NuGet パッケージ |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NET WebHooks ソース コードと NuGet パッケージへのリンク
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: ad368125878871c0e38f35152c86fe4eea143924
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675320"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET Webhooks ソース コードと NuGet パッケージ

マイクロソフト ASP.NET WebHooks は、マイクロソフト ASP.NET モジュール ファミリの一部であり[、GitHub のオープン ソース プロジェクト](https://github.com/aspnet/WebHooks)としてホストされています。 これは、投稿を受け入れることを意味しますが、プルリクエストを提出する前に[、投稿ガイドライン](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)を参照してください。

このオンライン ドキュメントは[、GitHub のオープン ソース](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide)としてもホストされ、投稿も受け付けています。

## <a name="nuget-packages"></a>NuGet パッケージ

[NuGet パッケージ](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)は、次の 3 つの部分に分かれています。

* [共通](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): 送信者と受信者の間で共有される共通パッケージ。

* [送信者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): 自分の WebHook を他のユーザーに送信するためのパッケージのセット。 WebHook を送信するための機能については[、WebHook の送信](sending/senders.md)で詳しく説明します。

* [受信機](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): 他の人から WebHook を受信するパッケージのセット。 WebHook を受信するための機能については[、WebHook の受信](receiving/index.md)で詳しく説明します。
