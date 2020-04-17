---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Web API を使用した OData v4 の複合型継承ASP.NET |マイクロソフトドキュメント
author: rick-anderson
description: OData v4 仕様によると、複合型は別の複合型から継承できます。 (複合型は、キーのない構造化タイプです。ウェブ API.
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: f433cf625c7d6ff4922d8c4a9954682fc0f1cc33
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543601"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="c0b9c-104">Web API を使用した OData v4 の複合型継承ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c0b9c-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="c0b9c-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c0b9c-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c0b9c-106">OData v4[仕様](http://www.odata.org/documentation/odata-version-4-0/)によると、複合型は別の複合型から継承できます。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="c0b9c-107">*(複合*型は、キーのない構造化タイプです。Web API OData 5.3 は、複合型の継承をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="c0b9c-108">このトピックでは、複雑な継承型を使用してエンティティ データ モデル (EDM) を構築する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="c0b9c-109">完全なソース コードについては[、「OData 複合型の継承のサンプル](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c0b9c-110">チュートリアルで使用するソフトウェアバージョン</span><span class="sxs-lookup"><span data-stu-id="c0b9c-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c0b9c-111">ウェブ API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="c0b9c-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="c0b9c-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="c0b9c-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="c0b9c-113">モデル階層</span><span class="sxs-lookup"><span data-stu-id="c0b9c-113">Model Hierarchy</span></span>

<span data-ttu-id="c0b9c-114">複合型の継承を説明するために、次のクラス階層を使用します。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="c0b9c-115">`Shape`は抽象複合型です。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="c0b9c-116">`Rectangle`、 `Triangle`、`Circle`および は から`Shape`派生した`RoundRectangle`複合型であり`Rectangle`、 から派生します。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="c0b9c-117">`Window`はエンティティ型であり、インスタンスを`Shape`含みます。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="c0b9c-118">これらの型を定義する CLR クラスを次に示します。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="c0b9c-119">EDM モデルの構築</span><span class="sxs-lookup"><span data-stu-id="c0b9c-119">Build the EDM Model</span></span>

<span data-ttu-id="c0b9c-120">EDM を作成するには、CLR 型から継承関係を推測する**ODataConventionModelBuilder**を使用します。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="c0b9c-121">また **、ODataModelBuilder**を使用して、EDM を明示的にビルドすることもできます。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="c0b9c-122">この処理にはコードが必要ですが、EDM をより詳細に制御できます。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="c0b9c-123">これらの 2 つの例では、同じ EDM スキーマを作成します。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="c0b9c-124">メタデータ ドキュメント</span><span class="sxs-lookup"><span data-stu-id="c0b9c-124">Metadata Document</span></span>

<span data-ttu-id="c0b9c-125">OData メタデータ ドキュメントは、複合型の継承を示しています。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="c0b9c-126">メタデータ ドキュメントからは、次のことがわかります。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="c0b9c-127">`Shape`複合型は抽象型です。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="c0b9c-128">`Rectangle`複合型`Triangle`、 `Circle` 、 、 の`Shape`基本型は、 が基本型です。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="c0b9c-129">型`RoundRectangle`の基本型`Rectangle`は、 です。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="c0b9c-130">複合型のキャスト</span><span class="sxs-lookup"><span data-stu-id="c0b9c-130">Casting Complex Types</span></span>

<span data-ttu-id="c0b9c-131">複合型のキャストがサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="c0b9c-132">たとえば、次のクエリは`Shape`にキャストします。 `Rectangle`</span><span class="sxs-lookup"><span data-stu-id="c0b9c-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="c0b9c-133">応答ペイロードは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="c0b9c-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
