---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/index
title: Visual Studio 2008 以前のバージョンでの Web サイトプロジェクトの配置 |Microsoft Docs
author: rick-anderson
description: ASP.NET web アプリケーションは、通常、ローカルの開発環境で設計、作成、およびテストされ、運用環境に配置する必要があります。
ms.author: riande
ms.date: 05/16/2012
ms.assetid: 6f72bde8-f2f1-4e4a-94e5-494c3c153c14
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects
msc.type: chapter
ms.openlocfilehash: 43c2397ef4ccc5eacb2ff4c5d04f62b9c8c481b7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78420490"
---
# <a name="deploying-web-site-projects-in-visual-studio-2008-and-earlier"></a><span data-ttu-id="27a5d-103">Visual Studio 2008 以前で Web サイト プロジェクトを配置する</span><span class="sxs-lookup"><span data-stu-id="27a5d-103">Deploying Web Site Projects in Visual Studio 2008 and earlier</span></span>

> <span data-ttu-id="27a5d-104">ASP.NET web アプリケーションは、通常、ローカル開発環境で設計、作成、およびテストされます。リリースの準備ができたら、運用環境に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="27a5d-104">ASP.NET web applications are typically designed, created, and tested in a local development environment and need to be deployed to a production environment once it is ready for release.</span></span> <span data-ttu-id="27a5d-105">このチュートリアルシリーズでは、デプロイプロセスについて詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="27a5d-105">This tutorial series details the deployment process.</span></span>

- [<span data-ttu-id="27a5d-106">ASP.NET ホスティングのオプション (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-106">ASP.NET Hosting Options (C#)</span></span>](asp-net-hosting-options-cs.md)
- [<span data-ttu-id="27a5d-107">展開が必要なファイルを決定する (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-107">Determining What Files Need to Be Deployed (C#)</span></span>](determining-what-files-need-to-be-deployed-cs.md)
- [<span data-ttu-id="27a5d-108">FTP クライアントを使用してサイトを展開する (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-108">Deploying Your Site Using an FTP Client (C#)</span></span>](deploying-your-site-using-an-ftp-client-cs.md)
- [<span data-ttu-id="27a5d-109">Visual Studio を使用してサイトを展開する (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-109">Deploying Your Site Using Visual Studio (C#)</span></span>](deploying-your-site-using-visual-studio-cs.md)
- [<span data-ttu-id="27a5d-110">開発と運用の間の一般的な構成の違い (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-110">Common Configuration Differences Between Development and Production (C#)</span></span>](common-configuration-differences-between-development-and-production-cs.md)
- [<span data-ttu-id="27a5d-111">IIS と ASP.NET 開発サーバーの間の中心的違い (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-111">Core Differences Between IIS and the ASP.NET Development Server (C#)</span></span>](core-differences-between-iis-and-the-asp-net-development-server-cs.md)
- [<span data-ttu-id="27a5d-112">データベースを展開する (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-112">Deploying a Database (C#)</span></span>](deploying-a-database-cs.md)
- [<span data-ttu-id="27a5d-113">実稼働データベースを使用するように Web アプリケーションを構成する (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-113">Configuring the Production Web Application to Use the Production Database (C#)</span></span>](configuring-the-production-web-application-to-use-the-production-database-cs.md)
- [<span data-ttu-id="27a5d-114">アプリケーション サービスを使用する Web サイトを構成する (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-114">Configuring a Website that Uses Application Services (C#)</span></span>](configuring-a-website-that-uses-application-services-cs.md)
- [<span data-ttu-id="27a5d-115">データベースの開発と展開のための戦略 (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-115">Strategies for Database Development and Deployment (C#)</span></span>](strategies-for-database-development-and-deployment-cs.md)
- [<span data-ttu-id="27a5d-116">カスタム エラー ページを表示する (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-116">Displaying a Custom Error Page (C#)</span></span>](displaying-a-custom-error-page-cs.md)
- [<span data-ttu-id="27a5d-117">未処理の例外を処理する (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-117">Processing Unhandled Exceptions (C#)</span></span>](processing-unhandled-exceptions-cs.md)
- [<span data-ttu-id="27a5d-118">ASP.NET の状態監視でエラーの詳細をログに記録する (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-118">Logging Error Details with ASP.NET Health Monitoring (C#)</span></span>](logging-error-details-with-asp-net-health-monitoring-cs.md)
- [<span data-ttu-id="27a5d-119">ELMAH でエラーの詳細をログに記録する (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-119">Logging Error Details with ELMAH (C#)</span></span>](logging-error-details-with-elmah-cs.md)
- [<span data-ttu-id="27a5d-120">Web サイトを事前コンパイルする (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-120">Precompiling Your Website (C#)</span></span>](precompiling-your-website-cs.md)
- [<span data-ttu-id="27a5d-121">運用 Web サイトのユーザーとロール (C#)</span><span class="sxs-lookup"><span data-stu-id="27a5d-121">Users and Roles On Production Website (C#)</span></span>](users-and-roles-on-the-production-website-cs.md)
- [<span data-ttu-id="27a5d-122">ASP.NET ホスティングのオプション (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-122">ASP.NET Hosting Options (VB)</span></span>](asp-net-hosting-options-vb.md)
- [<span data-ttu-id="27a5d-123">展開が必要なファイルを決定する (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-123">Determining What Files Need to Be Deployed (VB)</span></span>](determining-what-files-need-to-be-deployed-vb.md)
- [<span data-ttu-id="27a5d-124">FTP クライアントを使用してサイトを展開する (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-124">Deploying Your Site Using an FTP Client (VB)</span></span>](deploying-your-site-using-an-ftp-client-vb.md)
- [<span data-ttu-id="27a5d-125">Visual Studio を使用してサイトを展開する (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-125">Deploying Your Site Using Visual Studio (VB)</span></span>](deploying-your-site-using-visual-studio-vb.md)
- [<span data-ttu-id="27a5d-126">開発と運用の間の一般的な構成の違い (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-126">Common Configuration Differences Between Development and Production (VB)</span></span>](common-configuration-differences-between-development-and-production-vb.md)
- [<span data-ttu-id="27a5d-127">IIS と ASP.NET 開発サーバーの間の中心的違い (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-127">Core Differences Between IIS and the ASP.NET Development Server (VB)</span></span>](core-differences-between-iis-and-the-asp-net-development-server-vb.md)
- [<span data-ttu-id="27a5d-128">データベースを展開する (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-128">Deploying a Database (VB)</span></span>](deploying-a-database-vb.md)
- [<span data-ttu-id="27a5d-129">実稼働データベースを使用するように Web アプリケーションを構成する (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-129">Configuring the Production Web Application to Use the Production Database (VB)</span></span>](configuring-the-production-web-application-to-use-the-production-database-vb.md)
- [<span data-ttu-id="27a5d-130">アプリケーション サービスを使用する Web サイトを構成する (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-130">Configuring a Website that Uses Application Services (VB)</span></span>](configuring-a-website-that-uses-application-services-vb.md)
- [<span data-ttu-id="27a5d-131">データベースの開発と展開のための戦略 (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-131">Strategies for Database Development and Deployment (VB)</span></span>](strategies-for-database-development-and-deployment-vb.md)
- [<span data-ttu-id="27a5d-132">カスタム エラー ページを表示する (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-132">Displaying a Custom Error Page (VB)</span></span>](displaying-a-custom-error-page-vb.md)
- [<span data-ttu-id="27a5d-133">未処理の例外を処理する (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-133">Processing Unhandled Exceptions (VB)</span></span>](processing-unhandled-exceptions-vb.md)
- [<span data-ttu-id="27a5d-134">ASP.NET の状態監視でエラーの詳細をログに記録する (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-134">Logging Error Details with ASP.NET Health Monitoring (VB)</span></span>](logging-error-details-with-asp-net-health-monitoring-vb.md)
- [<span data-ttu-id="27a5d-135">ELMAH でエラーの詳細をログに記録する (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-135">Logging Error Details with ELMAH (VB)</span></span>](logging-error-details-with-elmah-vb.md)
- [<span data-ttu-id="27a5d-136">Web サイトを事前コンパイルする (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-136">Precompiling Your Website (VB)</span></span>](precompiling-your-website-vb.md)
- [<span data-ttu-id="27a5d-137">運用 Web サイトのユーザーとロール (VB)</span><span class="sxs-lookup"><span data-stu-id="27a5d-137">Users and Roles On Production Website (VB)</span></span>](users-and-roles-on-the-production-website-vb.md)
