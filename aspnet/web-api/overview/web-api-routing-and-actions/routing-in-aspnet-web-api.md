---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: web API でASP.NETルーティング |マイクロソフトドキュメント
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675755"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="c599a-102">ASP.NET Web API でのルーティング</span><span class="sxs-lookup"><span data-stu-id="c599a-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="c599a-103">[マイク・ワッソン](https://github.com/MikeWasson)著</span><span class="sxs-lookup"><span data-stu-id="c599a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c599a-104">この記事では、web API ASP.NETが HTTP 要求をコントローラーにルーティングする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c599a-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="c599a-105">ASP.NET MVC に精通している場合、Web API ルーティングは MVC ルーティングとよく似ています。</span><span class="sxs-lookup"><span data-stu-id="c599a-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="c599a-106">主な違いは、Web API がアクションを選択するために URI パスではなく HTTP 動詞を使用することです。</span><span class="sxs-lookup"><span data-stu-id="c599a-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="c599a-107">Web API では MVC 形式のルーティングを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="c599a-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="c599a-108">この記事では、ASP.NET MVC の知識を前提としていません。</span><span class="sxs-lookup"><span data-stu-id="c599a-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="c599a-109">ルーティング テーブル</span><span class="sxs-lookup"><span data-stu-id="c599a-109">Routing Tables</span></span>

<span data-ttu-id="c599a-110">ASP.NET Web API では、*コントローラ*は HTTP 要求を処理するクラスです。</span><span class="sxs-lookup"><span data-stu-id="c599a-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="c599a-111">コントローラのパブリック メソッドは、*アクション メソッド*または単にアクション と呼*ばれます*。</span><span class="sxs-lookup"><span data-stu-id="c599a-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="c599a-112">Web API フレームワークは、要求を受信すると、要求をアクションにルーティングします。</span><span class="sxs-lookup"><span data-stu-id="c599a-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="c599a-113">呼び出すアクションを決定するために、フレームワークは*ルーティング テーブル*を使用します。</span><span class="sxs-lookup"><span data-stu-id="c599a-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="c599a-114">Web API 用の Visual Studio プロジェクト テンプレートは、既定のルートを作成します。</span><span class="sxs-lookup"><span data-stu-id="c599a-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="c599a-115">このルートは *、WebApiConfig.cs*ファイルで定義され、*\_アプリケーションの開始*ディレクトリに配置されます。</span><span class="sxs-lookup"><span data-stu-id="c599a-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="c599a-116">クラスの詳細については、「Web API の`WebApiConfig`[構成ASP.NET」](../advanced/configuring-aspnet-web-api.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c599a-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="c599a-117">Web API を自己ホストする場合は、オブジェクトにルーティング テーブルを`HttpSelfHostConfiguration`直接設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c599a-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="c599a-118">詳細については、「 [Web API のセルフ ホスト](../older-versions/self-host-a-web-api.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c599a-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="c599a-119">ルーティング テーブルの各エントリには、*ルート テンプレート*が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c599a-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="c599a-120">Web API の既定のルート&quot;テンプレートは、API/{コントローラ}/{id} です&quot;。</span><span class="sxs-lookup"><span data-stu-id="c599a-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="c599a-121">このテンプレートでは&quot;、api&quot;はリテラル パス セグメントであり、{controller} と {id} はプレースホルダー変数です。</span><span class="sxs-lookup"><span data-stu-id="c599a-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="c599a-122">Web API フレームワークは、HTTP 要求を受信すると、ルーティング テーブル内のいずれかのルート テンプレートに対して URI を照合しようとします。</span><span class="sxs-lookup"><span data-stu-id="c599a-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="c599a-123">一致するルートがない場合、クライアントは 404 エラーを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="c599a-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="c599a-124">たとえば、次の URI は既定のルートと一致します。</span><span class="sxs-lookup"><span data-stu-id="c599a-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="c599a-125">/api/連絡先</span><span class="sxs-lookup"><span data-stu-id="c599a-125">/api/contacts</span></span>
- <span data-ttu-id="c599a-126">/api/連絡先/1</span><span class="sxs-lookup"><span data-stu-id="c599a-126">/api/contacts/1</span></span>
- <span data-ttu-id="c599a-127">/api/製品/ギズモ1</span><span class="sxs-lookup"><span data-stu-id="c599a-127">/api/products/gizmo1</span></span>

<span data-ttu-id="c599a-128">ただし、次の URI は&quot;API&quot;セグメントがないため一致しません。</span><span class="sxs-lookup"><span data-stu-id="c599a-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="c599a-129">/連絡先/1</span><span class="sxs-lookup"><span data-stu-id="c599a-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="c599a-130">ルートで "api" を使用する理由は、MVC ルーティングとの衝突ASP.NET回避するためです。</span><span class="sxs-lookup"><span data-stu-id="c599a-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="c599a-131">このようにすると、/contacts&quot;&quot;を MVC コントローラーに移動し&quot;、/api/contact&quot;を Web API コントローラーに移動させることができます。</span><span class="sxs-lookup"><span data-stu-id="c599a-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="c599a-132">もちろん、この規則が気に入らない場合は、デフォルトのルートテーブルを変更できます。</span><span class="sxs-lookup"><span data-stu-id="c599a-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="c599a-133">一致するルートが見つかると、Web API はコントローラーとアクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="c599a-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="c599a-134">コントローラーを見つけるために、Web API &quot;&quot;は *{controller}* 変数の値にコントローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="c599a-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="c599a-135">アクションを見つけるには、Web API は HTTP 動詞を検索し、その HTTP 動詞名で始まる名前のアクションを探します。</span><span class="sxs-lookup"><span data-stu-id="c599a-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="c599a-136">たとえば、GET 要求を使用すると、Web API は GetContact &quot;&quot;や&quot;GetAllContacts&quot;&quot;&quot;などの "Get" というプレフィックスが付いたアクションを検索します。</span><span class="sxs-lookup"><span data-stu-id="c599a-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="c599a-137">この規約は、GET、ポスト、プット、削除、ヘッド、オプション、およびパッチの動詞にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="c599a-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="c599a-138">コントローラーの属性を使用して、他の HTTP 動詞を有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="c599a-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="c599a-139">その例については後で説明します。</span><span class="sxs-lookup"><span data-stu-id="c599a-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="c599a-140">ルート テンプレート内の他のプレースホルダー変数 *({id}* など) は、アクション パラメーターにマップされます。</span><span class="sxs-lookup"><span data-stu-id="c599a-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="c599a-141">1 つ例を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="c599a-141">Let's look at an example.</span></span> <span data-ttu-id="c599a-142">次のコントローラを定義するとします。</span><span class="sxs-lookup"><span data-stu-id="c599a-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="c599a-143">以下に、考えられる HTTP 要求と、それぞれに対して呼び出されるアクションを示します。</span><span class="sxs-lookup"><span data-stu-id="c599a-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="c599a-144">HTTP 動詞</span><span class="sxs-lookup"><span data-stu-id="c599a-144">HTTP Verb</span></span> | <span data-ttu-id="c599a-145">URI パス</span><span class="sxs-lookup"><span data-stu-id="c599a-145">URI Path</span></span> | <span data-ttu-id="c599a-146">アクション</span><span class="sxs-lookup"><span data-stu-id="c599a-146">Action</span></span> | <span data-ttu-id="c599a-147">パラメーター</span><span class="sxs-lookup"><span data-stu-id="c599a-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c599a-148">GET</span><span class="sxs-lookup"><span data-stu-id="c599a-148">GET</span></span> | <span data-ttu-id="c599a-149">api/製品</span><span class="sxs-lookup"><span data-stu-id="c599a-149">api/products</span></span> | <span data-ttu-id="c599a-150">すべての製品を取得します。</span><span class="sxs-lookup"><span data-stu-id="c599a-150">GetAllProducts</span></span> | <span data-ttu-id="c599a-151">*(なし)*</span><span class="sxs-lookup"><span data-stu-id="c599a-151">*(none)*</span></span> |
| <span data-ttu-id="c599a-152">GET</span><span class="sxs-lookup"><span data-stu-id="c599a-152">GET</span></span> | <span data-ttu-id="c599a-153">api/製品/4</span><span class="sxs-lookup"><span data-stu-id="c599a-153">api/products/4</span></span> | <span data-ttu-id="c599a-154">製品バイId</span><span class="sxs-lookup"><span data-stu-id="c599a-154">GetProductById</span></span> | <span data-ttu-id="c599a-155">4</span><span class="sxs-lookup"><span data-stu-id="c599a-155">4</span></span> |
| <span data-ttu-id="c599a-156">DELETE</span><span class="sxs-lookup"><span data-stu-id="c599a-156">DELETE</span></span> | <span data-ttu-id="c599a-157">api/製品/4</span><span class="sxs-lookup"><span data-stu-id="c599a-157">api/products/4</span></span> | <span data-ttu-id="c599a-158">製品の削除</span><span class="sxs-lookup"><span data-stu-id="c599a-158">DeleteProduct</span></span> | <span data-ttu-id="c599a-159">4</span><span class="sxs-lookup"><span data-stu-id="c599a-159">4</span></span> |
| <span data-ttu-id="c599a-160">POST</span><span class="sxs-lookup"><span data-stu-id="c599a-160">POST</span></span> | <span data-ttu-id="c599a-161">api/製品</span><span class="sxs-lookup"><span data-stu-id="c599a-161">api/products</span></span> | <span data-ttu-id="c599a-162">*(一致しない)*</span><span class="sxs-lookup"><span data-stu-id="c599a-162">*(no match)*</span></span> |  |

<span data-ttu-id="c599a-163">URI の *{id}* セグメントが存在する場合は、アクションの*id*パラメーターにマップされることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="c599a-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="c599a-164">この例では、コントローラは*2*つの GET メソッドを定義します。</span><span class="sxs-lookup"><span data-stu-id="c599a-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="c599a-165">また、コントローラは Post.. を定義していないため、POST 要求は&quot;失敗します。&quot;メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="c599a-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="c599a-166">ルーティングバリエーション</span><span class="sxs-lookup"><span data-stu-id="c599a-166">Routing Variations</span></span>

<span data-ttu-id="c599a-167">前のセクションでは、Web API の基本的なルーティングメカニズムASP.NET説明しました。</span><span class="sxs-lookup"><span data-stu-id="c599a-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="c599a-168">このセクションでは、いくつかのバリエーションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="c599a-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="c599a-169">HTTP 動詞</span><span class="sxs-lookup"><span data-stu-id="c599a-169">HTTP verbs</span></span>

<span data-ttu-id="c599a-170">HTTP 動詞の名前付け規則を使用する代わりに、アクション メソッドを次のいずれかの属性で修飾することで、アクションの HTTP 動詞を明示的に指定できます。</span><span class="sxs-lookup"><span data-stu-id="c599a-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="c599a-171">次の例では、`FindProduct`メソッドが GET 要求にマップされています。</span><span class="sxs-lookup"><span data-stu-id="c599a-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="c599a-172">アクションに複数の HTTP 動詞を許可したり、GET、PUT、POST、削除、ヘッド、オプション、および PATCH 以外の HTTP 動詞を`[AcceptVerbs]`許可したりするには、HTTP 動詞のリストを取る属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="c599a-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="c599a-173">アクション名によるルーティング</span><span class="sxs-lookup"><span data-stu-id="c599a-173">Routing by Action Name</span></span>

<span data-ttu-id="c599a-174">既定のルーティング テンプレートでは、Web API は HTTP 動詞を使用してアクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="c599a-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="c599a-175">ただし、アクション名が URI に含まれるルートを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="c599a-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="c599a-176">このルート テンプレートでは *、{action}* パラメーターはコントローラーのアクション メソッドに名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="c599a-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="c599a-177">この形式のルーティングでは、属性を使用して、許可される HTTP 動詞を指定します。</span><span class="sxs-lookup"><span data-stu-id="c599a-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="c599a-178">たとえば、コントローラーに次のメソッドがあるとします。</span><span class="sxs-lookup"><span data-stu-id="c599a-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="c599a-179">この場合、GET リクエストの "api/製品/詳細/1" はメソッドに`Details`マップされます。</span><span class="sxs-lookup"><span data-stu-id="c599a-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="c599a-180">このルーティングスタイルは、ASP.NET MVC に似ており、RPC スタイルの API に適している場合があります。</span><span class="sxs-lookup"><span data-stu-id="c599a-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="c599a-181">属性を使用して、アクション名を`[ActionName]`オーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="c599a-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="c599a-182">次の例では、api/製品/サムネイル/ &quot;*id*にマップする 2 つのアクションがあります。1 つは GET をサポートし、もう 1 つは POST をサポートします。</span><span class="sxs-lookup"><span data-stu-id="c599a-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="c599a-183">非アクション</span><span class="sxs-lookup"><span data-stu-id="c599a-183">Non-Actions</span></span>

<span data-ttu-id="c599a-184">メソッドがアクションとして呼び出されないようにするには、 属性を使用`[NonAction]`します。</span><span class="sxs-lookup"><span data-stu-id="c599a-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="c599a-185">これは、メソッドがルーティングルールに一致する場合でも、メソッドがアクションではないことをフレームワークに通知します。</span><span class="sxs-lookup"><span data-stu-id="c599a-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="c599a-186">参考資料</span><span class="sxs-lookup"><span data-stu-id="c599a-186">Further Reading</span></span>

<span data-ttu-id="c599a-187">このトピックでは、ルーティングの概要を説明しました。</span><span class="sxs-lookup"><span data-stu-id="c599a-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="c599a-188">詳細については、「[ルーティングとアクションの選択](routing-and-action-selection.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c599a-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
