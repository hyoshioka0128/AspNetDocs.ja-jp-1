---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Web API を使用した OData v4 でのオープン ASP.NET型 |マイクロソフトドキュメント
author: rick-anderson
description: OData v4 では、オープン タイプは、型定義で宣言されたプロパティに加えて、動的プロパティを含む構造化型です。 開く...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d63c96df6614896b3b67eef94a8907e528572567
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543731"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="cab71-104">Web API を使用した OData v4 でのオープンASP.NET型</span><span class="sxs-lookup"><span data-stu-id="cab71-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="cab71-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="cab71-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="cab71-106">OData v4 では、*オープン タイプ*は、型定義で宣言されたプロパティに加えて、動的プロパティを含む構造化型です。</span><span class="sxs-lookup"><span data-stu-id="cab71-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="cab71-107">オープンタイプを使用すると、データモデルに柔軟性を追加できます。</span><span class="sxs-lookup"><span data-stu-id="cab71-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="cab71-108">このチュートリアルでは、Web API OData でオープン型ASP.NET使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="cab71-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="cab71-109">このチュートリアルでは、Web API で OData エンドポイントを作成する方法ASP.NET既に理解していることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="cab71-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="cab71-110">ない場合は、まず[OData v4 エンドポイントの作成を](create-an-odata-v4-endpoint.md)読み取ります。</span><span class="sxs-lookup"><span data-stu-id="cab71-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="cab71-111">チュートリアルで使用するソフトウェアバージョン</span><span class="sxs-lookup"><span data-stu-id="cab71-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="cab71-112">ウェブ API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="cab71-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="cab71-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="cab71-113">OData v4</span></span>

<span data-ttu-id="cab71-114">まず、いくつかの OData 用語:</span><span class="sxs-lookup"><span data-stu-id="cab71-114">First, some OData terminology:</span></span>

- <span data-ttu-id="cab71-115">エンティティタイプ: キーを持つ構造化タイプ。</span><span class="sxs-lookup"><span data-stu-id="cab71-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="cab71-116">複合型: キーのない構造化タイプ。</span><span class="sxs-lookup"><span data-stu-id="cab71-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="cab71-117">オープンタイプ: 動的プロパティを持つタイプ。</span><span class="sxs-lookup"><span data-stu-id="cab71-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="cab71-118">エンティティ型と複合型の両方を開くことができます。</span><span class="sxs-lookup"><span data-stu-id="cab71-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="cab71-119">動的プロパティの値は、プリミティブ型、複合型、または列挙型のいずれかです。または、これらの型のコレクション。</span><span class="sxs-lookup"><span data-stu-id="cab71-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="cab71-120">オープン型の詳細については[、OData v4 仕様](http://www.odata.org/documentation/odata-version-4-0/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cab71-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="cab71-121">Web OData ライブラリのインストール</span><span class="sxs-lookup"><span data-stu-id="cab71-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="cab71-122">NuGet パッケージ マネージャーを使用して、最新の Web API OData ライブラリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="cab71-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="cab71-123">[パッケージ マネージャー コンソール] ウィンドウから:</span><span class="sxs-lookup"><span data-stu-id="cab71-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="cab71-124">CLR 型の定義</span><span class="sxs-lookup"><span data-stu-id="cab71-124">Define the CLR Types</span></span>

<span data-ttu-id="cab71-125">まず、EDM モデルを CLR 型として定義します。</span><span class="sxs-lookup"><span data-stu-id="cab71-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="cab71-126">エンティティ データ モデル (EDM) が作成されると、</span><span class="sxs-lookup"><span data-stu-id="cab71-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="cab71-127">`Category`は列挙型です。</span><span class="sxs-lookup"><span data-stu-id="cab71-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="cab71-128">`Address`は複合型です。</span><span class="sxs-lookup"><span data-stu-id="cab71-128">`Address` is a complex type.</span></span> <span data-ttu-id="cab71-129">(キーを持たないため、エンティティ型ではありません)。</span><span class="sxs-lookup"><span data-stu-id="cab71-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="cab71-130">`Customer`はエンティティ型です。</span><span class="sxs-lookup"><span data-stu-id="cab71-130">`Customer` is an entity type.</span></span> <span data-ttu-id="cab71-131">(キーがあります。</span><span class="sxs-lookup"><span data-stu-id="cab71-131">(It has a key.)</span></span>
- <span data-ttu-id="cab71-132">`Press`はオープンな複合型です。</span><span class="sxs-lookup"><span data-stu-id="cab71-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="cab71-133">`Book`は開いているエンティティ型です。</span><span class="sxs-lookup"><span data-stu-id="cab71-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="cab71-134">オープン型を作成するには、CLR 型に動的プロパティを保持する`IDictionary<string, object>`type のプロパティが必要です。</span><span class="sxs-lookup"><span data-stu-id="cab71-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="cab71-135">EDM モデルの構築</span><span class="sxs-lookup"><span data-stu-id="cab71-135">Build the EDM Model</span></span>

<span data-ttu-id="cab71-136">**ODataConventionModelBuilder**を使用して EDM を`Press`作成`Book`し、`IDictionary<string, object>`プロパティの存在に基づいてオープン型として自動的に追加する場合。</span><span class="sxs-lookup"><span data-stu-id="cab71-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="cab71-137">また **、ODataModelBuilder**を使用して、EDM を明示的にビルドすることもできます。</span><span class="sxs-lookup"><span data-stu-id="cab71-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="cab71-138">OData コントローラーの追加</span><span class="sxs-lookup"><span data-stu-id="cab71-138">Add an OData Controller</span></span>

<span data-ttu-id="cab71-139">次に、OData コント ローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="cab71-139">Next, add an OData controller.</span></span> <span data-ttu-id="cab71-140">このチュートリアルでは、GET と POST 要求をサポートし、インメモリ リストを使用してエンティティを格納する単純なコントローラーを使用します。</span><span class="sxs-lookup"><span data-stu-id="cab71-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="cab71-141">最初`Book`のインスタンスには動的プロパティが存在しません。</span><span class="sxs-lookup"><span data-stu-id="cab71-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="cab71-142">2`Book`番目のインスタンスには、次の動的プロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="cab71-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="cab71-143">"公開済み": プリミティブ型</span><span class="sxs-lookup"><span data-stu-id="cab71-143">"Published": Primitive type</span></span>
- <span data-ttu-id="cab71-144">「著者」:プリミティブ型のコレクション</span><span class="sxs-lookup"><span data-stu-id="cab71-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="cab71-145">"その他のカテゴリ": 列挙型のコレクション。</span><span class="sxs-lookup"><span data-stu-id="cab71-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="cab71-146">また、その`Press``Book`インスタンスのプロパティには、次の動的プロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="cab71-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="cab71-147">「ブログ」:プリミティブ型</span><span class="sxs-lookup"><span data-stu-id="cab71-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="cab71-148">"アドレス": 複合型</span><span class="sxs-lookup"><span data-stu-id="cab71-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="cab71-149">メタデータのクエリ</span><span class="sxs-lookup"><span data-stu-id="cab71-149">Query the Metadata</span></span>

<span data-ttu-id="cab71-150">OData メタデータ ドキュメントを取得するには、GET 要求を`~/$metadata`に送信します。</span><span class="sxs-lookup"><span data-stu-id="cab71-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="cab71-151">応答本文は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="cab71-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="cab71-152">メタデータ ドキュメントからは、次のことがわかります。</span><span class="sxs-lookup"><span data-stu-id="cab71-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="cab71-153">および の型の場合、属性の`OpenType`値は true です。 `Press` `Book`</span><span class="sxs-lookup"><span data-stu-id="cab71-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="cab71-154">`Customer`と`Address`の型には、この属性はありません。</span><span class="sxs-lookup"><span data-stu-id="cab71-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="cab71-155">エンティティ`Book`型には、ISBN、タイトル、およびプレスという 3 つの宣言済みプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="cab71-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="cab71-156">OData メタデータには、CLR クラス`Book.Properties`のプロパティは含まれません。</span><span class="sxs-lookup"><span data-stu-id="cab71-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="cab71-157">同様に`Press`、複合型には、宣言されたプロパティが 2 つだけ( Name と Category) があります。</span><span class="sxs-lookup"><span data-stu-id="cab71-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="cab71-158">メタデータには、CLR クラスの`Press.DynamicProperties`プロパティは含まれません。</span><span class="sxs-lookup"><span data-stu-id="cab71-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="cab71-159">エンティティのクエリ</span><span class="sxs-lookup"><span data-stu-id="cab71-159">Query an Entity</span></span>

<span data-ttu-id="cab71-160">ISBN が "978-0-7356-7942-9" の書籍を入手するには、 GET`~/Books('978-0-7356-7942-9')`要求を 送信します。</span><span class="sxs-lookup"><span data-stu-id="cab71-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="cab71-161">応答本文は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="cab71-161">The response body should look similar to the following.</span></span> <span data-ttu-id="cab71-162">(読みやすくするためにインデントされます。</span><span class="sxs-lookup"><span data-stu-id="cab71-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="cab71-163">動的プロパティは、宣言されたプロパティとインラインで含まれることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="cab71-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="cab71-164">エンティティの投稿</span><span class="sxs-lookup"><span data-stu-id="cab71-164">POST an Entity</span></span>

<span data-ttu-id="cab71-165">Book エンティティを追加するには、POST 要求を`~/Books`に送信します。</span><span class="sxs-lookup"><span data-stu-id="cab71-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="cab71-166">クライアントは、要求ペイロードに動的プロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="cab71-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="cab71-167">リクエストの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="cab71-167">Here is an example request.</span></span> <span data-ttu-id="cab71-168">"価格" と "公開済み" プロパティに注意してください。</span><span class="sxs-lookup"><span data-stu-id="cab71-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="cab71-169">コントローラー メソッドにブレークポイントを設定すると、Web API によってこれらのプロパティがディクショナリに追加されている`Properties`ことがわかります。</span><span class="sxs-lookup"><span data-stu-id="cab71-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="cab71-170">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="cab71-170">Additional Resources</span></span>

[<span data-ttu-id="cab71-171">OData オープンタイプのサンプル</span><span class="sxs-lookup"><span data-stu-id="cab71-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
