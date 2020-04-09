---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: Web API における認証と承認ASP.NET |マイクロソフトドキュメント
author: MikeWasson
description: Web API での認証と承認の概要ASP.NET提供します。
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675863"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a><span data-ttu-id="a9195-103">ASP.NET Web API での認証と承認</span><span class="sxs-lookup"><span data-stu-id="a9195-103">Authentication and Authorization in ASP.NET Web API</span></span>

<span data-ttu-id="a9195-104">[マイク・ワッソン](https://github.com/MikeWasson)著</span><span class="sxs-lookup"><span data-stu-id="a9195-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a9195-105">Web API を作成しましたが、次は Web API へのアクセスを制御する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a9195-105">You've created a web API, but now you want to control access to it.</span></span> <span data-ttu-id="a9195-106">この一連の記事では、承認されていないユーザーから Web API を保護するためのいくつかのオプションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="a9195-106">In this series of articles, we'll look at some options for securing a web API from unauthorized users.</span></span> <span data-ttu-id="a9195-107">このシリーズでは、認証と承認の両方について説明します。</span><span class="sxs-lookup"><span data-stu-id="a9195-107">This series will cover both authentication and authorization.</span></span>

- <span data-ttu-id="a9195-108">*認証*は、ユーザーの ID を知っています。</span><span class="sxs-lookup"><span data-stu-id="a9195-108">*Authentication* is knowing the identity of the user.</span></span> <span data-ttu-id="a9195-109">たとえば、Alice はユーザー名とパスワードでログインし、サーバーはパスワードを使用して Alice を認証します。</span><span class="sxs-lookup"><span data-stu-id="a9195-109">For example, Alice logs in with her username and password, and the server uses the password to authenticate Alice.</span></span>
- <span data-ttu-id="a9195-110">*承認*は、ユーザーがアクションを実行できるかどうかを決定します。</span><span class="sxs-lookup"><span data-stu-id="a9195-110">*Authorization* is deciding whether a user is allowed to perform an action.</span></span> <span data-ttu-id="a9195-111">たとえば、Alice にはリソースを取得する権限がありますが、リソースを作成することはできません。</span><span class="sxs-lookup"><span data-stu-id="a9195-111">For example, Alice has permission to get a resource but not create a resource.</span></span>

<span data-ttu-id="a9195-112">シリーズの最初の記事では、Web API における認証と承認の概要ASP.NET説明します。</span><span class="sxs-lookup"><span data-stu-id="a9195-112">The first article in the series gives a general overview of authentication and authorization in ASP.NET Web API.</span></span> <span data-ttu-id="a9195-113">その他のトピックでは、Web API の一般的な認証シナリオについて説明します。</span><span class="sxs-lookup"><span data-stu-id="a9195-113">Other topics describe common authentication scenarios for Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="a9195-114">このシリーズをレビューし、貴重なフィードバックを提供してくれた人々に感謝します:リック・アンダーソン、リーバイ・ブロデリック、バリー・ドランス、トム・ダイクストラ、ホンメイ・ゲ、デビッド・マットソン、ダニエル・ロス、ティム・ティーケン。</span><span class="sxs-lookup"><span data-stu-id="a9195-114">Thanks to the people who reviewed this series and provided valuable feedback: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.</span></span>

## <a name="authentication"></a><span data-ttu-id="a9195-115">認証</span><span class="sxs-lookup"><span data-stu-id="a9195-115">Authentication</span></span>

<span data-ttu-id="a9195-116">Web API は、認証がホストで行われると想定しています。</span><span class="sxs-lookup"><span data-stu-id="a9195-116">Web API assumes that authentication happens in the host.</span></span> <span data-ttu-id="a9195-117">Web ホスティングの場合、ホストは IIS で、認証に HTTP モジュールを使用します。</span><span class="sxs-lookup"><span data-stu-id="a9195-117">For web-hosting, the host is IIS, which uses HTTP modules for authentication.</span></span> <span data-ttu-id="a9195-118">IIS または ASP.NET に組み込まれている認証モジュールを使用するようにプロジェクトを構成したり、独自の HTTP モジュールを記述してカスタム認証を実行したりできます。</span><span class="sxs-lookup"><span data-stu-id="a9195-118">You can configure your project to use any of the authentication modules built in to IIS or ASP.NET, or write your own HTTP module to perform custom authentication.</span></span>

<span data-ttu-id="a9195-119">ホストは、ユーザーを認証するときに、コードが実行されているセキュリティ コンテキストを表す[IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx)オブジェクトである*プリンシパル*を作成します。</span><span class="sxs-lookup"><span data-stu-id="a9195-119">When the host authenticates the user, it creates a *principal*, which is an [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) object that represents the security context under which code is running.</span></span> <span data-ttu-id="a9195-120">ホストは **、Thread.CurrentPrincipal**を設定することで、プリンシパルを現在のスレッドにアタッチします。</span><span class="sxs-lookup"><span data-stu-id="a9195-120">The host attaches the principal to the current thread by setting **Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="a9195-121">プリンシパルには、ユーザーに関する情報を含む関連付けられた**Identity**オブジェクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a9195-121">The principal contains an associated **Identity** object that contains information about the user.</span></span> <span data-ttu-id="a9195-122">ユーザーが認証されている場合 **、Identity.IsAuthenticated**プロパティは**true**を返します。</span><span class="sxs-lookup"><span data-stu-id="a9195-122">If the user is authenticated, the **Identity.IsAuthenticated** property returns **true**.</span></span> <span data-ttu-id="a9195-123">匿名要求の場合 **、IsAuthenticated は** **false**を返します。</span><span class="sxs-lookup"><span data-stu-id="a9195-123">For anonymous requests, **IsAuthenticated** returns **false**.</span></span> <span data-ttu-id="a9195-124">プリンシパルの詳細については、「[ロールベースのセキュリティ](https://msdn.microsoft.com/library/shz8h065.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a9195-124">For more information about principals, see [Role-Based Security](https://msdn.microsoft.com/library/shz8h065.aspx).</span></span>

### <a name="http-message-handlers-for-authentication"></a><span data-ttu-id="a9195-125">認証用の HTTP メッセージ ハンドラ</span><span class="sxs-lookup"><span data-stu-id="a9195-125">HTTP Message Handlers for Authentication</span></span>

<span data-ttu-id="a9195-126">認証にホストを使用する代わりに、認証ロジックを HTTP[メッセージ ハンドラ](../advanced/http-message-handlers.md)に入れることができます。</span><span class="sxs-lookup"><span data-stu-id="a9195-126">Instead of using the host for authentication, you can put authentication logic into an [HTTP message handler](../advanced/http-message-handlers.md).</span></span> <span data-ttu-id="a9195-127">その場合、メッセージ ハンドラーは HTTP 要求を調べてプリンシパルを設定します。</span><span class="sxs-lookup"><span data-stu-id="a9195-127">In that case, the message handler examines the HTTP request and sets the principal.</span></span>

<span data-ttu-id="a9195-128">認証にメッセージ ハンドラを使用する必要がある場合</span><span class="sxs-lookup"><span data-stu-id="a9195-128">When should you use message handlers for authentication?</span></span> <span data-ttu-id="a9195-129">いくつかのトレードオフを次に示します。</span><span class="sxs-lookup"><span data-stu-id="a9195-129">Here are some tradeoffs:</span></span>

- <span data-ttu-id="a9195-130">HTTP モジュールは、ASP.NET パイプラインを通過するすべての要求を参照します。</span><span class="sxs-lookup"><span data-stu-id="a9195-130">An HTTP module sees all requests that go through the ASP.NET pipeline.</span></span> <span data-ttu-id="a9195-131">メッセージ ハンドラーは、Web API にルーティングされた要求のみを参照します。</span><span class="sxs-lookup"><span data-stu-id="a9195-131">A message handler only sees requests that are routed to Web API.</span></span>
- <span data-ttu-id="a9195-132">ルートごとのメッセージ ハンドラを設定して、特定のルートに認証スキームを適用できます。</span><span class="sxs-lookup"><span data-stu-id="a9195-132">You can set per-route message handlers, which lets you apply an authentication scheme to a specific route.</span></span>
- <span data-ttu-id="a9195-133">HTTP モジュールは IIS に固有のものです。</span><span class="sxs-lookup"><span data-stu-id="a9195-133">HTTP modules are specific to IIS.</span></span> <span data-ttu-id="a9195-134">メッセージ ハンドラーはホストに依存しないため、Web ホスティングとセルフ ホスティングの両方で使用できます。</span><span class="sxs-lookup"><span data-stu-id="a9195-134">Message handlers are host-agnostic, so they can be used with both web-hosting and self-hosting.</span></span>
- <span data-ttu-id="a9195-135">HTTP モジュールは、IIS ログ、監査などに参加します。</span><span class="sxs-lookup"><span data-stu-id="a9195-135">HTTP modules participate in IIS logging, auditing, and so on.</span></span>
- <span data-ttu-id="a9195-136">HTTP モジュールは、パイプラインで以前に実行されます。</span><span class="sxs-lookup"><span data-stu-id="a9195-136">HTTP modules run earlier in the pipeline.</span></span> <span data-ttu-id="a9195-137">メッセージ ハンドラーで認証を処理する場合、プリンシパルはハンドラーが実行されるまで設定されません。</span><span class="sxs-lookup"><span data-stu-id="a9195-137">If you handle authentication in a message handler, the principal does not get set until the handler runs.</span></span> <span data-ttu-id="a9195-138">さらに、応答がメッセージ ハンドラーから離れると、プリンシパルは前のプリンシパルに戻ります。</span><span class="sxs-lookup"><span data-stu-id="a9195-138">Moreover, the principal reverts back to the previous principal when the response leaves the message handler.</span></span>

<span data-ttu-id="a9195-139">一般的に、自己ホストをサポートする必要がない場合は、HTTPモジュールが適しています。</span><span class="sxs-lookup"><span data-stu-id="a9195-139">Generally, if you don't need to support self-hosting, an HTTP module is a better option.</span></span> <span data-ttu-id="a9195-140">自己ホストをサポートする必要がある場合は、メッセージ ハンドラーを検討してください。</span><span class="sxs-lookup"><span data-stu-id="a9195-140">If you need to support self-hosting, consider a message handler.</span></span>

### <a name="setting-the-principal"></a><span data-ttu-id="a9195-141">プリンシパルの設定</span><span class="sxs-lookup"><span data-stu-id="a9195-141">Setting the Principal</span></span>

<span data-ttu-id="a9195-142">アプリケーションでカスタム認証ロジックを実行する場合は、次の 2 つの場所でプリンシパルを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a9195-142">If your application performs any custom authentication logic, you must set the principal on two places:</span></span>

- <span data-ttu-id="a9195-143">**スレッド.現在のプリンシパル**。</span><span class="sxs-lookup"><span data-stu-id="a9195-143">**Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="a9195-144">このプロパティは、.NET でスレッドのプリンシパルを設定する標準的な方法です。</span><span class="sxs-lookup"><span data-stu-id="a9195-144">This property is the standard way to set the thread's principal in .NET.</span></span>
- <span data-ttu-id="a9195-145">**ユーザー**.</span><span class="sxs-lookup"><span data-stu-id="a9195-145">**HttpContext.Current.User**.</span></span> <span data-ttu-id="a9195-146">このプロパティは、ASP.NETに固有です。</span><span class="sxs-lookup"><span data-stu-id="a9195-146">This property is specific to ASP.NET.</span></span>

<span data-ttu-id="a9195-147">次のコードは、プリンシパルを設定する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="a9195-147">The following code shows how to set the principal:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="a9195-148">Web ホスティングの場合は、両方の場所でプリンシパルを設定する必要があります。そうしないと、セキュリティ コンテキストが矛盾する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a9195-148">For web-hosting, you must set the principal in both places; otherwise the security context may become inconsistent.</span></span> <span data-ttu-id="a9195-149">ただし、自己ホストの場合は **、HttpContext.Current**は null です。</span><span class="sxs-lookup"><span data-stu-id="a9195-149">For self-hosting, however, **HttpContext.Current** is null.</span></span> <span data-ttu-id="a9195-150">コードがホストに依存しないようにするには、次に示すように**HttpContext.Current**に割り当てる前に null を確認します。</span><span class="sxs-lookup"><span data-stu-id="a9195-150">To ensure your code is host-agnostic, therefore, check for null before assigning to **HttpContext.Current**, as shown.</span></span>

## <a name="authorization"></a><span data-ttu-id="a9195-151">承認</span><span class="sxs-lookup"><span data-stu-id="a9195-151">Authorization</span></span>

<span data-ttu-id="a9195-152">承認は、後でパイプラインで、コントローラーに近い状態で行われます。</span><span class="sxs-lookup"><span data-stu-id="a9195-152">Authorization happens later in the pipeline, closer to the controller.</span></span> <span data-ttu-id="a9195-153">これにより、リソースへのアクセスを許可するときに、より細かい選択を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="a9195-153">That lets you make more granular choices when you grant access to resources.</span></span>

- <span data-ttu-id="a9195-154">*承認フィルター*は、コントローラーアクションの前に実行されます。</span><span class="sxs-lookup"><span data-stu-id="a9195-154">*Authorization filters* run before the controller action.</span></span> <span data-ttu-id="a9195-155">要求が承認されていない場合、フィルターはエラー応答を返し、アクションは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="a9195-155">If the request is not authorized, the filter returns an error response, and the action is not invoked.</span></span>
- <span data-ttu-id="a9195-156">コントローラー アクション内で **、ApiController.User**プロパティから現在のプリンシパルを取得できます。</span><span class="sxs-lookup"><span data-stu-id="a9195-156">Within a controller action, you can get the current principal from the **ApiController.User** property.</span></span> <span data-ttu-id="a9195-157">たとえば、ユーザー名に基づいてリソースの一覧をフィルタし、そのユーザーに属するリソースのみを返す場合があります。</span><span class="sxs-lookup"><span data-stu-id="a9195-157">For example, you might filter a list of resources based on the user name, returning only those resources that belong to that user.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a><span data-ttu-id="a9195-158">[承認] 属性の使用</span><span class="sxs-lookup"><span data-stu-id="a9195-158">Using the [Authorize] Attribute</span></span>

<span data-ttu-id="a9195-159">Web API には、組み込みの承認フィルター[が用意されています](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a9195-159">Web API provides a built-in authorization filter, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx).</span></span> <span data-ttu-id="a9195-160">このフィルタは、ユーザーが認証されているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="a9195-160">This filter checks whether the user is authenticated.</span></span> <span data-ttu-id="a9195-161">それでない場合は、アクションを呼び出さずに HTTP ステータス コード 401 (許可されていません) を返します。</span><span class="sxs-lookup"><span data-stu-id="a9195-161">If not, it returns HTTP status code 401 (Unauthorized), without invoking the action.</span></span>

<span data-ttu-id="a9195-162">フィルタは、グローバル、コントローラ レベル、または個々のアクションのレベルで適用できます。</span><span class="sxs-lookup"><span data-stu-id="a9195-162">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>

<span data-ttu-id="a9195-163">**グローバル**: すべての Web API コントローラーのアクセスを制限するには、グローバル フィルター リストに**AuthorizeAttribute**フィルターを追加します。</span><span class="sxs-lookup"><span data-stu-id="a9195-163">**Globally**: To restrict access for every Web API controller, add the **AuthorizeAttribute** filter to the global filter list:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="a9195-164">**コントローラ**: 特定のコントローラへのアクセスを制限するには、コントローラに属性としてフィルタを追加します。</span><span class="sxs-lookup"><span data-stu-id="a9195-164">**Controller**: To restrict access for a specific controller, add the filter as an attribute to the controller:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="a9195-165">**アクション**: 特定のアクションへのアクセスを制限するには、アクション メソッドに属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="a9195-165">**Action**: To restrict access for specific actions, add the attribute to the action method:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="a9195-166">または、コントローラを制限し、属性を使用して特定のアクションへの匿名アクセスを`[AllowAnonymous]`許可することもできます。</span><span class="sxs-lookup"><span data-stu-id="a9195-166">Alternatively, you can restrict the controller and then allow anonymous access to specific actions, by using the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="a9195-167">次の例では、`Post`メソッドは制限されていますが、メソッドは`Get`匿名アクセスを許可しています。</span><span class="sxs-lookup"><span data-stu-id="a9195-167">In the following example, the `Post` method is restricted, but the `Get` method allows anonymous access.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="a9195-168">前の例では、フィルタにより、認証されたユーザーが制限されたメソッドにアクセスできるようになります。匿名ユーザーのみが除外されます。アクセスを特定のユーザーまたは特定のロールのユーザーに制限することもできます。</span><span class="sxs-lookup"><span data-stu-id="a9195-168">In the previous examples, the filter allows any authenticated user to access the restricted methods; only anonymous users are kept out. You can also limit access to specific users or to users in specific roles:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="a9195-169">Web API コントローラーの**承認属性**フィルターは、**名前空間**内にあります。</span><span class="sxs-lookup"><span data-stu-id="a9195-169">The **AuthorizeAttribute** filter for Web API controllers is located in the **System.Web.Http** namespace.</span></span> <span data-ttu-id="a9195-170">Web API コントローラーと互換性のない **、System.Web.Mvc**名前空間内の MVC コント ローラーの同様のフィルターがあります。</span><span class="sxs-lookup"><span data-stu-id="a9195-170">There is a similar filter for MVC controllers in the **System.Web.Mvc** namespace, which is not compatible with Web API controllers.</span></span>

### <a name="custom-authorization-filters"></a><span data-ttu-id="a9195-171">カスタム承認フィルタ</span><span class="sxs-lookup"><span data-stu-id="a9195-171">Custom Authorization Filters</span></span>

<span data-ttu-id="a9195-172">カスタム承認フィルターを作成するには、次のいずれかの型から派生します。</span><span class="sxs-lookup"><span data-stu-id="a9195-172">To write a custom authorization filter, derive from one of these types:</span></span>

- <span data-ttu-id="a9195-173">**属性を承認**します。</span><span class="sxs-lookup"><span data-stu-id="a9195-173">**AuthorizeAttribute**.</span></span> <span data-ttu-id="a9195-174">現在のユーザーとユーザーのロールに基づいて承認ロジックを実行するには、このクラスを拡張します。</span><span class="sxs-lookup"><span data-stu-id="a9195-174">Extend this class to perform authorization logic based on the current user and the user's roles.</span></span>
- <span data-ttu-id="a9195-175">**フィルター属性を指定**します。</span><span class="sxs-lookup"><span data-stu-id="a9195-175">**AuthorizationFilterAttribute**.</span></span> <span data-ttu-id="a9195-176">このクラスを拡張して、現在のユーザーまたはロールに基づくとは限らない同期承認ロジックを実行します。</span><span class="sxs-lookup"><span data-stu-id="a9195-176">Extend this class to perform synchronous authorization logic that is not necessarily based on the current user or role.</span></span>
- <span data-ttu-id="a9195-177">**I 認証フィルター .**</span><span class="sxs-lookup"><span data-stu-id="a9195-177">**IAuthorizationFilter**.</span></span> <span data-ttu-id="a9195-178">非同期承認ロジックを実行するには、このインターフェイスを実装します。たとえば、承認ロジックが非同期 I/O またはネットワーク呼び出しを行う場合などです。</span><span class="sxs-lookup"><span data-stu-id="a9195-178">Implement this interface to perform asynchronous authorization logic; for example, if your authorization logic makes asynchronous I/O or network calls.</span></span> <span data-ttu-id="a9195-179">(承認ロジックが CPU にバインドされている場合は、非同期メソッドを記述する必要がないため **、AuthorizationFilterAttribute**から派生する方が簡単です。</span><span class="sxs-lookup"><span data-stu-id="a9195-179">(If your authorization logic is CPU-bound, it is simpler to derive from **AuthorizationFilterAttribute**, because then you don't need to write an asynchronous method.)</span></span>

<span data-ttu-id="a9195-180">次の図は、**クラスのクラス**階層を示しています。</span><span class="sxs-lookup"><span data-stu-id="a9195-180">The following diagram shows the class hierarchy for the **AuthorizeAttribute** class.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a><span data-ttu-id="a9195-181">コントローラ アクション内の承認</span><span class="sxs-lookup"><span data-stu-id="a9195-181">Authorization Inside a Controller Action</span></span>

<span data-ttu-id="a9195-182">場合によっては、要求の続行を許可し、プリンシパルに基づいて動作を変更する場合があります。</span><span class="sxs-lookup"><span data-stu-id="a9195-182">In some cases, you might allow a request to proceed, but change the behavior based on the principal.</span></span> <span data-ttu-id="a9195-183">たとえば、ユーザーのロールによって、返される情報が変わる場合があります。</span><span class="sxs-lookup"><span data-stu-id="a9195-183">For example, the information that you return might change depending on the user's role.</span></span> <span data-ttu-id="a9195-184">コントローラー メソッド内で、現在のプリンシパルを**取得できます。**</span><span class="sxs-lookup"><span data-stu-id="a9195-184">Within a controller method, you can get the current principal from the **ApiController.User** property.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
