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
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>Web API を使用した OData v4 の複合型継承ASP.NET

[マイクロソフト](https://github.com/microsoft)

> OData v4[仕様](http://www.odata.org/documentation/odata-version-4-0/)によると、複合型は別の複合型から継承できます。 *(複合*型は、キーのない構造化タイプです。Web API OData 5.3 は、複合型の継承をサポートしています。
> 
> このトピックでは、複雑な継承型を使用してエンティティ データ モデル (EDM) を構築する方法について説明します。 完全なソース コードについては[、「OData 複合型の継承のサンプル](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)」を参照してください。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>チュートリアルで使用するソフトウェアバージョン
> 
> 
> - ウェブ API OData 5.3
> - OData v4

## <a name="model-hierarchy"></a>モデル階層

複合型の継承を説明するために、次のクラス階層を使用します。

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape`は抽象複合型です。 `Rectangle`、 `Triangle`、`Circle`および は から`Shape`派生した`RoundRectangle`複合型であり`Rectangle`、 から派生します。 `Window`はエンティティ型であり、インスタンスを`Shape`含みます。

これらの型を定義する CLR クラスを次に示します。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>EDM モデルの構築

EDM を作成するには、CLR 型から継承関係を推測する**ODataConventionModelBuilder**を使用します。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

また **、ODataModelBuilder**を使用して、EDM を明示的にビルドすることもできます。 この処理にはコードが必要ですが、EDM をより詳細に制御できます。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

これらの 2 つの例では、同じ EDM スキーマを作成します。

## <a name="metadata-document"></a>メタデータ ドキュメント

OData メタデータ ドキュメントは、複合型の継承を示しています。

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

メタデータ ドキュメントからは、次のことがわかります。

- `Shape`複合型は抽象型です。
- `Rectangle`複合型`Triangle`、 `Circle` 、 、 の`Shape`基本型は、 が基本型です。
- 型`RoundRectangle`の基本型`Rectangle`は、 です。

## <a name="casting-complex-types"></a>複合型のキャスト

複合型のキャストがサポートされるようになりました。 たとえば、次のクエリは`Shape`にキャストします。 `Rectangle`

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

応答ペイロードは次のとおりです。

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
