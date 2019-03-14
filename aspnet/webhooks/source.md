---
uid: webhooks/source
title: ASP.NET Webhook のソース コードと NuGet パッケージ |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook のソース コードと NuGet パッケージへのリンク
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: ff716b476f7dc69b6071d3febd5b5871e4f02689
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57027189"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="90f79-103">ASP.NET Webhook のソース コードと NuGet パッケージ</span><span class="sxs-lookup"><span data-stu-id="90f79-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="90f79-104">Microsoft ASP.NET Webhook はモジュールの Microsoft ASP.NET ファミリの一部でありとしてホストされる、 [GitHub でオープン ソース プロジェクト](https://github.com/aspnet/WebHooks)します。</span><span class="sxs-lookup"><span data-stu-id="90f79-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="90f79-105">つまり、投稿をそのまま使用しましたを参照してください、[投稿に関するガイドライン](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)プル要求を送信する前にします。</span><span class="sxs-lookup"><span data-stu-id="90f79-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="90f79-106">このオンライン ドキュメントの読み取りを行うようになりましたがもとしてホストされる[GitHub でオープン ソース](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide)も投稿を受け入れるとします。</span><span class="sxs-lookup"><span data-stu-id="90f79-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="90f79-107">NuGet パッケージ</span><span class="sxs-lookup"><span data-stu-id="90f79-107">NuGet packages</span></span>

<span data-ttu-id="90f79-108">[NuGet パッケージの](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)は 3 つの部分に分けられます。</span><span class="sxs-lookup"><span data-stu-id="90f79-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="90f79-109">[一般的な](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common):送信者と受信者の間で共有される一般的なパッケージです。</span><span class="sxs-lookup"><span data-stu-id="90f79-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="90f79-110">[送信者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom):他のユーザーに、独自の Webhook の送信をサポートしているパッケージのセット。</span><span class="sxs-lookup"><span data-stu-id="90f79-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="90f79-111">Webhook に送信するための機能がで詳しく説明されている[送信 Webhook](sending/index.md)します。</span><span class="sxs-lookup"><span data-stu-id="90f79-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/index.md).</span></span>

* <span data-ttu-id="90f79-112">[受信側](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers):他のユーザーからの Webhook の受信をサポートしているパッケージのセット。</span><span class="sxs-lookup"><span data-stu-id="90f79-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="90f79-113">Webhook を受信するための機能がで詳しく説明されている[受信 Webhook](receiving/index.md)します。</span><span class="sxs-lookup"><span data-stu-id="90f79-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>