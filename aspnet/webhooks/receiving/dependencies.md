---
uid: webhooks/receiving/dependencies
title: ASP.NET Webhooks レシーバの依存関係 |マイクロソフトドキュメント
author: rick-anderson
description: 受信側の依存関係と、ASP.NET WebHook での依存関係の注入。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: b50442b3d95512bc0db7583b93de3bbef2d4bb4a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675208"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET Webhook のレシーバーの依存関係

マイクロソフトASP.NET WebHooks は、依存関係の注入を念頭に置いて設計されています。 システム内のほとんどの依存関係は、依存関係注入エンジンを使用して代替実装に置き換えることができます。

レシーバー[の依存関係](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs)の一覧については、次を参照してください。 依存関係が登録されていない場合は、既定の実装が使用されます。 既定の実装の一覧については[、「ReceiverServices」](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs)を参照してください。
