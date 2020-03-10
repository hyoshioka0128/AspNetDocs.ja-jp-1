---
uid: signalr/overview/security/persistent-connection-authorization
title: SignalR 永続的接続の認証と承認 |Microsoft Docs
author: bradygaster
description: このトピックでは、永続的な接続で承認を強制する方法について説明します。 SignalR アプリケーションへのセキュリティの統合に関する一般的な情報については,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467476"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="3a032-104">SignalR 永続的接続の認証と承認</span><span class="sxs-lookup"><span data-stu-id="3a032-104">Authentication and Authorization for SignalR Persistent Connections</span></span>

<span data-ttu-id="3a032-105">[Fletcher (パトリック](https://github.com/pfletcher))、 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3a032-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="3a032-106">このトピックでは、永続的な接続で承認を強制する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="3a032-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="3a032-107">SignalR アプリケーションへのセキュリティの統合に関する一般的な情報については、「[セキュリティの概要](introduction-to-security.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3a032-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="3a032-108">このトピックで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="3a032-108">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="3a032-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3a032-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="3a032-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="3a032-110">.NET 4.5</span></span>
> - <span data-ttu-id="3a032-111">SignalR バージョン2</span><span class="sxs-lookup"><span data-stu-id="3a032-111">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="3a032-112">このトピックの前のバージョン</span><span class="sxs-lookup"><span data-stu-id="3a032-112">Previous versions of this topic</span></span>
>
> <span data-ttu-id="3a032-113">以前のバージョンの SignalR の詳細については、「[古いバージョンの SignalR](../older-versions/index.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3a032-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="3a032-114">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="3a032-114">Questions and comments</span></span>
>
> <span data-ttu-id="3a032-115">このチュートリアルの良い点に関するフィードバックや、ページ下部にあるコメントで改善できる点をお知らせください。</span><span class="sxs-lookup"><span data-stu-id="3a032-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="3a032-116">チュートリアルに直接関係のない質問がある場合は、 [ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="3a032-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="3a032-117">承認を強制する</span><span class="sxs-lookup"><span data-stu-id="3a032-117">Enforce authorization</span></span>

<span data-ttu-id="3a032-118">[PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx)を使用するときに承認規則を適用するには、`AuthorizeRequest` メソッドをオーバーライドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="3a032-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="3a032-119">永続的な接続では、`Authorize` 属性を使用できません。</span><span class="sxs-lookup"><span data-stu-id="3a032-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="3a032-120">`AuthorizeRequest` メソッドは、要求されたアクションを実行する権限がユーザーに与えられていることを確認するために、すべての要求の前に SignalR フレームワークによって呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="3a032-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="3a032-121">`AuthorizeRequest` メソッドがクライアントから呼び出されていません。代わりに、アプリケーションの標準の認証メカニズムを使用してユーザーを認証します。</span><span class="sxs-lookup"><span data-stu-id="3a032-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="3a032-122">次の例は、認証されたユーザーに要求を制限する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="3a032-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="3a032-123">AuthorizeRequest メソッドには、カスタマイズされた承認ロジックを追加することができます。たとえば、ユーザーが特定のロールに属しているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="3a032-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
