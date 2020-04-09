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
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="207a2-103">ASP.NET Webhooks ソース コードと NuGet パッケージ</span><span class="sxs-lookup"><span data-stu-id="207a2-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="207a2-104">マイクロソフト ASP.NET WebHooks は、マイクロソフト ASP.NET モジュール ファミリの一部であり[、GitHub のオープン ソース プロジェクト](https://github.com/aspnet/WebHooks)としてホストされています。</span><span class="sxs-lookup"><span data-stu-id="207a2-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="207a2-105">これは、投稿を受け入れることを意味しますが、プルリクエストを提出する前に[、投稿ガイドライン](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="207a2-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="207a2-106">このオンライン ドキュメントは[、GitHub のオープン ソース](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide)としてもホストされ、投稿も受け付けています。</span><span class="sxs-lookup"><span data-stu-id="207a2-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="207a2-107">NuGet パッケージ</span><span class="sxs-lookup"><span data-stu-id="207a2-107">NuGet packages</span></span>

<span data-ttu-id="207a2-108">[NuGet パッケージ](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)は、次の 3 つの部分に分かれています。</span><span class="sxs-lookup"><span data-stu-id="207a2-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="207a2-109">[共通](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): 送信者と受信者の間で共有される共通パッケージ。</span><span class="sxs-lookup"><span data-stu-id="207a2-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="207a2-110">[送信者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): 自分の WebHook を他のユーザーに送信するためのパッケージのセット。</span><span class="sxs-lookup"><span data-stu-id="207a2-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="207a2-111">WebHook を送信するための機能については[、WebHook の送信](sending/senders.md)で詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="207a2-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="207a2-112">[受信機](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): 他の人から WebHook を受信するパッケージのセット。</span><span class="sxs-lookup"><span data-stu-id="207a2-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="207a2-113">WebHook を受信するための機能については[、WebHook の受信](receiving/index.md)で詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="207a2-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
