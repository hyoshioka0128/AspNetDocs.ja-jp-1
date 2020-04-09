---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: Web API 2 でASP.NET属性ルーティング |マイクロソフトドキュメント
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675382"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="8841f-102">Web API 2 でASP.NET属性ルーティング</span><span class="sxs-lookup"><span data-stu-id="8841f-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="8841f-103">[マイク・ワッソン](https://github.com/MikeWasson)著</span><span class="sxs-lookup"><span data-stu-id="8841f-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="8841f-104">*ルーティング*とは、Web API がアクションに対して URI と一致する方法です。</span><span class="sxs-lookup"><span data-stu-id="8841f-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="8841f-105">Web API 2 は、属性ルーティング と呼ばれる新しいタイプの*ルーティングを*サポートします。</span><span class="sxs-lookup"><span data-stu-id="8841f-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="8841f-106">名前が示すように、属性ルーティングでは属性を使用してルートを定義します。</span><span class="sxs-lookup"><span data-stu-id="8841f-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="8841f-107">属性ルーティングを使用すると、Web API の URI をより詳細に制御できます。</span><span class="sxs-lookup"><span data-stu-id="8841f-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="8841f-108">たとえば、リソースの階層を記述する URI を簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="8841f-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="8841f-109">以前の形式のルーティングは、規則ベースのルーティングと呼ばれ、引き続き完全にサポートされています。</span><span class="sxs-lookup"><span data-stu-id="8841f-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="8841f-110">実際には、同じプロジェクトで両方のテクニックを組み合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="8841f-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="8841f-111">このトピックでは、属性ルーティングを有効にする方法を示し、属性ルーティングのさまざまなオプションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="8841f-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="8841f-112">属性ルーティングを使用するエンド ツー エンド チュートリアルについては[、「Web API 2 での属性ルーティングを使用した REST API](create-a-rest-api-with-attribute-routing.md)の作成」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8841f-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8841f-113">前提条件</span><span class="sxs-lookup"><span data-stu-id="8841f-113">Prerequisites</span></span>

<span data-ttu-id="8841f-114">[ビジュアルスタジオ2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)コミュニティ、プロフェッショナル、またはエンタープライズエディション</span><span class="sxs-lookup"><span data-stu-id="8841f-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="8841f-115">または、NuGet パッケージ マネージャーを使用して、必要なパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="8841f-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="8841f-116">Visual Studio の [**ツール]** メニューから **[NuGet パッケージ マネージャー**] を選択し、[**パッケージ マネージャー コンソール**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8841f-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="8841f-117">パッケージ マネージャー コンソール ウィンドウで次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="8841f-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="8841f-118">属性ルーティングの理由</span><span class="sxs-lookup"><span data-stu-id="8841f-118">Why Attribute Routing?</span></span>

<span data-ttu-id="8841f-119">Web API の最初のリリースでは *、規則ベースの*ルーティングが使用されました。</span><span class="sxs-lookup"><span data-stu-id="8841f-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="8841f-120">このタイプのルーティングでは、基本的にパラメータ化された文字列である 1 つまたは複数のルート テンプレートを定義します。</span><span class="sxs-lookup"><span data-stu-id="8841f-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="8841f-121">フレームワークは、要求を受信すると、URI とルート テンプレートを照合します。</span><span class="sxs-lookup"><span data-stu-id="8841f-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="8841f-122">規則ベースのルーティングの詳細については、「 [Web API でのルーティングASP.NET](routing-in-aspnet-web-api.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="8841f-122">For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="8841f-123">規則ベースのルーティングの利点の 1 つは、テンプレートが 1 か所で定義され、ルーティング規則がすべてのコントローラに一貫して適用される点です。</span><span class="sxs-lookup"><span data-stu-id="8841f-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="8841f-124">残念ながら、規則ベースのルーティングでは、RESTful API で一般的な特定の URI パターンをサポートすることが困難になります。</span><span class="sxs-lookup"><span data-stu-id="8841f-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="8841f-125">たとえば、多くの場合、リソースには子リソースが含まれます。</span><span class="sxs-lookup"><span data-stu-id="8841f-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="8841f-126">これらの関係を反映する URI を作成するのは当然です。</span><span class="sxs-lookup"><span data-stu-id="8841f-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="8841f-127">この種類の URI は、規則ベースのルーティングを使用して作成するのが困難です。</span><span class="sxs-lookup"><span data-stu-id="8841f-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="8841f-128">これは可能ですが、コントローラーやリソースの種類が多い場合は、結果が適切に拡張されません。</span><span class="sxs-lookup"><span data-stu-id="8841f-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="8841f-129">属性ルーティングでは、この URI のルートを定義するのは簡単です。</span><span class="sxs-lookup"><span data-stu-id="8841f-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="8841f-130">コントローラーアクションに属性を追加するだけです。</span><span class="sxs-lookup"><span data-stu-id="8841f-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="8841f-131">ここでは、属性ルーティングを容易にする他のパターンをいくつか示します。</span><span class="sxs-lookup"><span data-stu-id="8841f-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="8841f-132">**API のバージョン管理**</span><span class="sxs-lookup"><span data-stu-id="8841f-132">**API versioning**</span></span>

<span data-ttu-id="8841f-133">この例では、"/api/v1/products" は "/api/v2/products" とは異なるコントローラにルーティングされます。</span><span class="sxs-lookup"><span data-stu-id="8841f-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="8841f-134">**オーバーロードされた URI セグメント**</span><span class="sxs-lookup"><span data-stu-id="8841f-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="8841f-135">この例では、"1" は注文番号ですが、"保留" はコレクションにマップされます。</span><span class="sxs-lookup"><span data-stu-id="8841f-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="8841f-136">**複数のパラメーター型**</span><span class="sxs-lookup"><span data-stu-id="8841f-136">**Multiple parameter types**</span></span>

<span data-ttu-id="8841f-137">この例では、"1" は注文番号ですが、"2013/06/16" は日付を指定します。</span><span class="sxs-lookup"><span data-stu-id="8841f-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="8841f-138">属性ルーティングの有効化</span><span class="sxs-lookup"><span data-stu-id="8841f-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="8841f-139">属性ルーティングを有効にするには、構成中に**MapHttpAttributeRoutes を**呼び出します。</span><span class="sxs-lookup"><span data-stu-id="8841f-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="8841f-140">この拡張メソッドは、**クラス**で定義されています。</span><span class="sxs-lookup"><span data-stu-id="8841f-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="8841f-141">属性ルーティングは、[規則ベースの](routing-in-aspnet-web-api.md)ルーティングと組み合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="8841f-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="8841f-142">規則に基づくルートを定義するには **、MapHttpRoute**メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="8841f-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="8841f-143">Web API の構成の詳細については、「Web API [2 の構成ASP.NET」](../advanced/configuring-aspnet-web-api.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8841f-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="8841f-144">注意: Web API 1 からの移行</span><span class="sxs-lookup"><span data-stu-id="8841f-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="8841f-145">Web API 2 より前の Web API プロジェクト テンプレートでは、次のようなコードが生成されます。</span><span class="sxs-lookup"><span data-stu-id="8841f-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="8841f-146">属性ルーティングが有効になっている場合、このコードは例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="8841f-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="8841f-147">属性ルーティングを使用するように既存の Web API プロジェクトをアップグレードする場合は、この構成コードを必ず次のように更新してください。</span><span class="sxs-lookup"><span data-stu-id="8841f-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="8841f-148">詳細については、「 [ASP.NET ホストを使用した Web API の構成](../advanced/configuring-aspnet-web-api.md#webhost)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8841f-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="8841f-149">ルート属性の追加</span><span class="sxs-lookup"><span data-stu-id="8841f-149">Adding Route Attributes</span></span>

<span data-ttu-id="8841f-150">属性を使用して定義されたルートの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="8841f-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="8841f-151">文字列&quot;顧客/{顧客Id}/注文&quot;は、ルートの URI テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="8841f-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="8841f-152">Web API は、要求 URI をテンプレートと照合しようとします。</span><span class="sxs-lookup"><span data-stu-id="8841f-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="8841f-153">この例では、「顧客」と「注文」はリテラル・セグメントであり、「{customerId}」は変数パラメーターです。</span><span class="sxs-lookup"><span data-stu-id="8841f-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="8841f-154">次の URI はこのテンプレートと一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="8841f-155">このトピックで後述する[制約](#constraints)を使用して、照合を制限できます。</span><span class="sxs-lookup"><span data-stu-id="8841f-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="8841f-156">ルート テンプレート&quot;の {customerId}&quot;パラメーターが、メソッドの*customerId*パラメーターの名前と一致していることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8841f-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="8841f-157">Web API は、コントローラー アクションを呼び出すときに、ルート パラメーターのバインドを試みます。</span><span class="sxs-lookup"><span data-stu-id="8841f-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="8841f-158">たとえば、URI が の`http://example.com/customers/1/orders`場合、Web API はアクションの*customerId*パラメーターに値 "1" をバインドしようとします。</span><span class="sxs-lookup"><span data-stu-id="8841f-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="8841f-159">URI テンプレートには、次のような複数のパラメーターを指定できます。</span><span class="sxs-lookup"><span data-stu-id="8841f-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="8841f-160">ルート属性を持たないコントローラ メソッドは、規則ベースのルーティングを使用します。</span><span class="sxs-lookup"><span data-stu-id="8841f-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="8841f-161">このようにして、同じプロジェクトで両方の種類のルーティングを組み合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="8841f-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8841f-162">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="8841f-162">HTTP Methods</span></span>

<span data-ttu-id="8841f-163">Web API は、リクエストの HTTP メソッド (GET、POST など) に基づいてアクションを選択します。</span><span class="sxs-lookup"><span data-stu-id="8841f-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="8841f-164">既定では、Web API は、コントローラー メソッド名の先頭に一致する大文字と小文字を区別しないものを検索します。</span><span class="sxs-lookup"><span data-stu-id="8841f-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="8841f-165">たとえば、HTTP PUT 要求`PutCustomers`と一致する名前のコントローラー メソッドが一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="8841f-166">この規則は、次の属性を使用してメソッドを修飾することでオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="8841f-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="8841f-167">**[HttpDelete]**</span><span class="sxs-lookup"><span data-stu-id="8841f-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="8841f-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="8841f-168">**[HttpGet]**</span></span>
- <span data-ttu-id="8841f-169">**[HttpHead]**</span><span class="sxs-lookup"><span data-stu-id="8841f-169">**[HttpHead]**</span></span>
- <span data-ttu-id="8841f-170">**[オプション]**</span><span class="sxs-lookup"><span data-stu-id="8841f-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="8841f-171">**[Httpパッチ]**</span><span class="sxs-lookup"><span data-stu-id="8841f-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="8841f-172">**[HttpPost]**</span><span class="sxs-lookup"><span data-stu-id="8841f-172">**[HttpPost]**</span></span>
- <span data-ttu-id="8841f-173">**[HttpPut]**</span><span class="sxs-lookup"><span data-stu-id="8841f-173">**[HttpPut]**</span></span>

<span data-ttu-id="8841f-174">次の例では、CreateBook メソッドを HTTP POST 要求にマップします。</span><span class="sxs-lookup"><span data-stu-id="8841f-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="8841f-175">非標準メソッドを含むその他のすべての HTTP メソッドでは、HTTP メソッドのリストを受け取る**AcceptVerbs**属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="8841f-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="8841f-176">ルート プレフィックス</span><span class="sxs-lookup"><span data-stu-id="8841f-176">Route Prefixes</span></span>

<span data-ttu-id="8841f-177">多くの場合、コントローラ内のルートはすべて同じプレフィックスで始まります。</span><span class="sxs-lookup"><span data-stu-id="8841f-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="8841f-178">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="8841f-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="8841f-179">**[RoutePrefix]** 属性を使用して、コントローラ全体に共通のプレフィックスを設定できます。</span><span class="sxs-lookup"><span data-stu-id="8841f-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="8841f-180">メソッド属性でチルダ (~) を使用して、ルート プレフィックスをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="8841f-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="8841f-181">ルート プレフィックスには、次のパラメータを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="8841f-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="8841f-182">ルート制約</span><span class="sxs-lookup"><span data-stu-id="8841f-182">Route Constraints</span></span>

<span data-ttu-id="8841f-183">ルート制約を使用すると、ルート テンプレート内のパラメータの照合方法を制限できます。</span><span class="sxs-lookup"><span data-stu-id="8841f-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="8841f-184">一般的な構文&quot;は {パラメーター:&quot;制約} です。</span><span class="sxs-lookup"><span data-stu-id="8841f-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="8841f-185">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="8841f-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="8841f-186">ここでは、最初のルートは、URI の&quot;id&quot;セグメントが整数の場合にのみ選択されます。</span><span class="sxs-lookup"><span data-stu-id="8841f-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="8841f-187">それ以外の場合は、2 番目のルートが選択されます。</span><span class="sxs-lookup"><span data-stu-id="8841f-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="8841f-188">次の表は、サポートされる制約の一覧です。</span><span class="sxs-lookup"><span data-stu-id="8841f-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="8841f-189">制約</span><span class="sxs-lookup"><span data-stu-id="8841f-189">Constraint</span></span> | <span data-ttu-id="8841f-190">説明</span><span class="sxs-lookup"><span data-stu-id="8841f-190">Description</span></span> | <span data-ttu-id="8841f-191">例</span><span class="sxs-lookup"><span data-stu-id="8841f-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8841f-192">alpha</span><span class="sxs-lookup"><span data-stu-id="8841f-192">alpha</span></span> | <span data-ttu-id="8841f-193">大文字または小文字の英字 (a-z、A から Z) に一致する</span><span class="sxs-lookup"><span data-stu-id="8841f-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="8841f-194">{x:アルファ}</span><span class="sxs-lookup"><span data-stu-id="8841f-194">{x:alpha}</span></span> |
| <span data-ttu-id="8841f-195">bool</span><span class="sxs-lookup"><span data-stu-id="8841f-195">bool</span></span> | <span data-ttu-id="8841f-196">ブール値に一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-196">Matches a Boolean value.</span></span> | <span data-ttu-id="8841f-197">{x:ブール}</span><span class="sxs-lookup"><span data-stu-id="8841f-197">{x:bool}</span></span> |
| <span data-ttu-id="8841f-198">DATETIME</span><span class="sxs-lookup"><span data-stu-id="8841f-198">datetime</span></span> | <span data-ttu-id="8841f-199">**日付時刻**の値に一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="8841f-200">{x:日時}</span><span class="sxs-lookup"><span data-stu-id="8841f-200">{x:datetime}</span></span> |
| <span data-ttu-id="8841f-201">decimal</span><span class="sxs-lookup"><span data-stu-id="8841f-201">decimal</span></span> | <span data-ttu-id="8841f-202">10 進値と一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-202">Matches a decimal value.</span></span> | <span data-ttu-id="8841f-203">{x:10 進数}</span><span class="sxs-lookup"><span data-stu-id="8841f-203">{x:decimal}</span></span> |
| <span data-ttu-id="8841f-204">double</span><span class="sxs-lookup"><span data-stu-id="8841f-204">double</span></span> | <span data-ttu-id="8841f-205">64 ビット浮動小数点値に一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="8841f-206">{x:double}</span><span class="sxs-lookup"><span data-stu-id="8841f-206">{x:double}</span></span> |
| <span data-ttu-id="8841f-207">float</span><span class="sxs-lookup"><span data-stu-id="8841f-207">float</span></span> | <span data-ttu-id="8841f-208">32 ビット浮動小数点値に一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="8841f-209">{x:フロート}</span><span class="sxs-lookup"><span data-stu-id="8841f-209">{x:float}</span></span> |
| <span data-ttu-id="8841f-210">guid</span><span class="sxs-lookup"><span data-stu-id="8841f-210">guid</span></span> | <span data-ttu-id="8841f-211">GUID 値に一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-211">Matches a GUID value.</span></span> | <span data-ttu-id="8841f-212">{x:guid}</span><span class="sxs-lookup"><span data-stu-id="8841f-212">{x:guid}</span></span> |
| <span data-ttu-id="8841f-213">INT</span><span class="sxs-lookup"><span data-stu-id="8841f-213">int</span></span> | <span data-ttu-id="8841f-214">32 ビット整数値に一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="8841f-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="8841f-215">{x:int}</span></span> |
| <span data-ttu-id="8841f-216">length</span><span class="sxs-lookup"><span data-stu-id="8841f-216">length</span></span> | <span data-ttu-id="8841f-217">指定した長さまたは指定した長さの範囲内の文字列に一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="8841f-218">{x:長さ(6)}{x:長さ(1,20)}</span><span class="sxs-lookup"><span data-stu-id="8841f-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="8841f-219">long</span><span class="sxs-lookup"><span data-stu-id="8841f-219">long</span></span> | <span data-ttu-id="8841f-220">64 ビット整数値に一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="8841f-221">{x:長}</span><span class="sxs-lookup"><span data-stu-id="8841f-221">{x:long}</span></span> |
| <span data-ttu-id="8841f-222">max</span><span class="sxs-lookup"><span data-stu-id="8841f-222">max</span></span> | <span data-ttu-id="8841f-223">最大値を持つ整数と一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="8841f-224">{x:最大(10)}</span><span class="sxs-lookup"><span data-stu-id="8841f-224">{x:max(10)}</span></span> |
| <span data-ttu-id="8841f-225">Maxlength</span><span class="sxs-lookup"><span data-stu-id="8841f-225">maxlength</span></span> | <span data-ttu-id="8841f-226">長さが最大の文字列と一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="8841f-227">{x:最大長(10)}</span><span class="sxs-lookup"><span data-stu-id="8841f-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="8841f-228">min</span><span class="sxs-lookup"><span data-stu-id="8841f-228">min</span></span> | <span data-ttu-id="8841f-229">最小値を持つ整数と一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="8841f-230">{x:分(10)}</span><span class="sxs-lookup"><span data-stu-id="8841f-230">{x:min(10)}</span></span> |
| <span data-ttu-id="8841f-231">最小長さ</span><span class="sxs-lookup"><span data-stu-id="8841f-231">minlength</span></span> | <span data-ttu-id="8841f-232">長さが最小の文字列に一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="8841f-233">{x:分の長さ(10)}</span><span class="sxs-lookup"><span data-stu-id="8841f-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="8841f-234">range</span><span class="sxs-lookup"><span data-stu-id="8841f-234">range</span></span> | <span data-ttu-id="8841f-235">値の範囲内の整数と一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="8841f-236">{x:範囲(10,50)}</span><span class="sxs-lookup"><span data-stu-id="8841f-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="8841f-237">regex</span><span class="sxs-lookup"><span data-stu-id="8841f-237">regex</span></span> | <span data-ttu-id="8841f-238">正規表現に一致します。</span><span class="sxs-lookup"><span data-stu-id="8841f-238">Matches a regular expression.</span></span> | <span data-ttu-id="8841f-239">{x:regex(^\d{3}-\d -\d{3}{4}$)}</span><span class="sxs-lookup"><span data-stu-id="8841f-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="8841f-240">min&quot;&quot;などの制約の一部は、かっこで囲まれた引数を取ります。</span><span class="sxs-lookup"><span data-stu-id="8841f-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="8841f-241">コロンで区切って、パラメーターに複数の制約を適用できます。</span><span class="sxs-lookup"><span data-stu-id="8841f-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="8841f-242">カスタム ルート制約</span><span class="sxs-lookup"><span data-stu-id="8841f-242">Custom Route Constraints</span></span>

<span data-ttu-id="8841f-243">カスタム ルート制約を作成するには **、IHttpRouteConstraint**インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="8841f-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="8841f-244">たとえば、次の制約は、パラメーターを 0 以外の整数値に制限します。</span><span class="sxs-lookup"><span data-stu-id="8841f-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="8841f-245">次のコードは、制約を登録する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="8841f-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="8841f-246">これで、ルートに制約を適用できます。</span><span class="sxs-lookup"><span data-stu-id="8841f-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="8841f-247">インターフェイスを実装することで **、Default InlineConstraintResolver**クラス全体を**IInlineConstraintResolver**置き換えることもできます。</span><span class="sxs-lookup"><span data-stu-id="8841f-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="8841f-248">これを行うと **、IInlineConstraintResolver**の実装で明示的に追加されない限り、組み込み制約がすべて置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="8841f-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="8841f-249">オプションの URI パラメーターとデフォルト値</span><span class="sxs-lookup"><span data-stu-id="8841f-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="8841f-250">ルート パラメータに疑問符を追加することで、URI パラメータをオプションにすることができます。</span><span class="sxs-lookup"><span data-stu-id="8841f-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="8841f-251">ルート パラメータがオプションの場合は、メソッド パラメータの既定値を定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8841f-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="8841f-252">この例では、`/api/books/locale/1033``/api/books/locale`同じリソースを返します。</span><span class="sxs-lookup"><span data-stu-id="8841f-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="8841f-253">または、次のように、ルート テンプレート内の既定値を指定できます。</span><span class="sxs-lookup"><span data-stu-id="8841f-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="8841f-254">これは前の例とほぼ同じですが、デフォルト値を適用すると動作が若干異なります。</span><span class="sxs-lookup"><span data-stu-id="8841f-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="8841f-255">最初の例 ("{lcid:int?}") では、既定値の 1033 がメソッド パラメーターに直接割り当てられるため、パラメーターはこの正確な値を持ちます。</span><span class="sxs-lookup"><span data-stu-id="8841f-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="8841f-256">2 番目の例 ("{lcid:int=1033}" )では、既定値の "1033" はモデル バインド プロセスを通過します。</span><span class="sxs-lookup"><span data-stu-id="8841f-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="8841f-257">デフォルトのモデルバインダーは、"1033" を数値 1033 に変換します。</span><span class="sxs-lookup"><span data-stu-id="8841f-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="8841f-258">ただし、カスタム モデル バインダーをプラグインすると、何か違う可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8841f-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="8841f-259">(ほとんどの場合、パイプラインにカスタム モデル バインダーがない限り、2 つのフォームは同等になります。</span><span class="sxs-lookup"><span data-stu-id="8841f-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="8841f-260">ルート名</span><span class="sxs-lookup"><span data-stu-id="8841f-260">Route Names</span></span>

<span data-ttu-id="8841f-261">Web API では、すべてのルートに名前が付けられます。</span><span class="sxs-lookup"><span data-stu-id="8841f-261">In Web API, every route has a name.</span></span> <span data-ttu-id="8841f-262">ルート名は、HTTP 応答にリンクを含めることができるように、リンクを生成するのに便利です。</span><span class="sxs-lookup"><span data-stu-id="8841f-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="8841f-263">ルート名を指定するには、属性の**Name**プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="8841f-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="8841f-264">次の例は、ルート名を設定する方法と、リンクを生成するときにルート名を使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="8841f-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="8841f-265">ルートオーダー</span><span class="sxs-lookup"><span data-stu-id="8841f-265">Route Order</span></span>

<span data-ttu-id="8841f-266">フレームワークは、URI とルートを照合しようとする際に、特定の順序でルートを評価します。</span><span class="sxs-lookup"><span data-stu-id="8841f-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="8841f-267">順序を指定するには、ルート属性の**Order**プロパティを設定します。</span><span class="sxs-lookup"><span data-stu-id="8841f-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="8841f-268">小さい値が最初に評価されます。</span><span class="sxs-lookup"><span data-stu-id="8841f-268">Lower values are evaluated first.</span></span> <span data-ttu-id="8841f-269">デフォルトの注文値はゼロです。</span><span class="sxs-lookup"><span data-stu-id="8841f-269">The default order value is zero.</span></span>

<span data-ttu-id="8841f-270">合計順序付けがどのように決定されるかは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="8841f-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="8841f-271">ルート属性の**Order**プロパティを比較します。</span><span class="sxs-lookup"><span data-stu-id="8841f-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="8841f-272">ルート テンプレートの各 URI セグメントを確認します。</span><span class="sxs-lookup"><span data-stu-id="8841f-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="8841f-273">各セグメントについて、次のように順序を付け、</span><span class="sxs-lookup"><span data-stu-id="8841f-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="8841f-274">リテラル セグメント。</span><span class="sxs-lookup"><span data-stu-id="8841f-274">Literal segments.</span></span>
    2. <span data-ttu-id="8841f-275">制約を使用してパラメータをルーティングします。</span><span class="sxs-lookup"><span data-stu-id="8841f-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="8841f-276">制約のないルート パラメータ。</span><span class="sxs-lookup"><span data-stu-id="8841f-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="8841f-277">制約付きのワイルドカード パラメータ セグメント。</span><span class="sxs-lookup"><span data-stu-id="8841f-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="8841f-278">制約のないワイルドカード パラメータ セグメント。</span><span class="sxs-lookup"><span data-stu-id="8841f-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="8841f-279">タイの場合、ルートはルート テンプレートの大文字と小文字を区別しない序数文字列比較 ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) によって順序付けられます。</span><span class="sxs-lookup"><span data-stu-id="8841f-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="8841f-280">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="8841f-280">Here is an example.</span></span> <span data-ttu-id="8841f-281">次のコントローラを定義するとします。</span><span class="sxs-lookup"><span data-stu-id="8841f-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="8841f-282">これらのルートは次のように並べられます。</span><span class="sxs-lookup"><span data-stu-id="8841f-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="8841f-283">注文/詳細</span><span class="sxs-lookup"><span data-stu-id="8841f-283">orders/details</span></span>
2. <span data-ttu-id="8841f-284">注文/{id}</span><span class="sxs-lookup"><span data-stu-id="8841f-284">orders/{id}</span></span>
3. <span data-ttu-id="8841f-285">注文/{顧客名}</span><span class="sxs-lookup"><span data-stu-id="8841f-285">orders/{customerName}</span></span>
4. <span data-ttu-id="8841f-286">注文/{\*日付}</span><span class="sxs-lookup"><span data-stu-id="8841f-286">orders/{\*date}</span></span>
5. <span data-ttu-id="8841f-287">注文/保留中</span><span class="sxs-lookup"><span data-stu-id="8841f-287">orders/pending</span></span>

<span data-ttu-id="8841f-288">"details" はリテラル セグメントであり、"{id}" の前に表示されますが **、Order**プロパティが 1 であるため、"pending" が最後に表示されます。</span><span class="sxs-lookup"><span data-stu-id="8841f-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="8841f-289">(この例では、"details" または "pending" という名前の顧客が存在しないものとします。</span><span class="sxs-lookup"><span data-stu-id="8841f-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="8841f-290">一般に、あいまいなルートを避けるようにしてください。</span><span class="sxs-lookup"><span data-stu-id="8841f-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="8841f-291">この例では、より優れたルート`GetByCustomer`テンプレートは "顧客/{顧客名}" です)。</span><span class="sxs-lookup"><span data-stu-id="8841f-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
