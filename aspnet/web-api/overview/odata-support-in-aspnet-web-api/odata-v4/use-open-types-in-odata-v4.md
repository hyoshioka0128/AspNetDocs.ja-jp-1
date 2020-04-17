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
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>Web API を使用した OData v4 でのオープンASP.NET型

[マイクロソフト](https://github.com/microsoft)

> OData v4 では、*オープン タイプ*は、型定義で宣言されたプロパティに加えて、動的プロパティを含む構造化型です。 オープンタイプを使用すると、データモデルに柔軟性を追加できます。 このチュートリアルでは、Web API OData でオープン型ASP.NET使用する方法を示します。
> 
> このチュートリアルでは、Web API で OData エンドポイントを作成する方法ASP.NET既に理解していることを前提としています。 ない場合は、まず[OData v4 エンドポイントの作成を](create-an-odata-v4-endpoint.md)読み取ります。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>チュートリアルで使用するソフトウェアバージョン
> 
> 
> - ウェブ API OData 5.3
> - OData v4

まず、いくつかの OData 用語:

- エンティティタイプ: キーを持つ構造化タイプ。
- 複合型: キーのない構造化タイプ。
- オープンタイプ: 動的プロパティを持つタイプ。 エンティティ型と複合型の両方を開くことができます。

動的プロパティの値は、プリミティブ型、複合型、または列挙型のいずれかです。または、これらの型のコレクション。 オープン型の詳細については[、OData v4 仕様](http://www.odata.org/documentation/odata-version-4-0/)を参照してください。

## <a name="install-the-web-odata-libraries"></a>Web OData ライブラリのインストール

NuGet パッケージ マネージャーを使用して、最新の Web API OData ライブラリをインストールします。 [パッケージ マネージャー コンソール] ウィンドウから:

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>CLR 型の定義

まず、EDM モデルを CLR 型として定義します。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

エンティティ データ モデル (EDM) が作成されると、

- `Category`は列挙型です。
- `Address`は複合型です。 (キーを持たないため、エンティティ型ではありません)。
- `Customer`はエンティティ型です。 (キーがあります。
- `Press`はオープンな複合型です。
- `Book`は開いているエンティティ型です。

オープン型を作成するには、CLR 型に動的プロパティを保持する`IDictionary<string, object>`type のプロパティが必要です。

## <a name="build-the-edm-model"></a>EDM モデルの構築

**ODataConventionModelBuilder**を使用して EDM を`Press`作成`Book`し、`IDictionary<string, object>`プロパティの存在に基づいてオープン型として自動的に追加する場合。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

また **、ODataModelBuilder**を使用して、EDM を明示的にビルドすることもできます。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>OData コントローラーの追加

次に、OData コント ローラーを追加します。 このチュートリアルでは、GET と POST 要求をサポートし、インメモリ リストを使用してエンティティを格納する単純なコントローラーを使用します。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

最初`Book`のインスタンスには動的プロパティが存在しません。 2`Book`番目のインスタンスには、次の動的プロパティがあります。

- "公開済み": プリミティブ型
- 「著者」:プリミティブ型のコレクション
- "その他のカテゴリ": 列挙型のコレクション。

また、その`Press``Book`インスタンスのプロパティには、次の動的プロパティがあります。

- 「ブログ」:プリミティブ型
- "アドレス": 複合型

## <a name="query-the-metadata"></a>メタデータのクエリ

OData メタデータ ドキュメントを取得するには、GET 要求を`~/$metadata`に送信します。 応答本文は次のようになります。

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

メタデータ ドキュメントからは、次のことがわかります。

- および の型の場合、属性の`OpenType`値は true です。 `Press` `Book` `Customer`と`Address`の型には、この属性はありません。
- エンティティ`Book`型には、ISBN、タイトル、およびプレスという 3 つの宣言済みプロパティがあります。 OData メタデータには、CLR クラス`Book.Properties`のプロパティは含まれません。
- 同様に`Press`、複合型には、宣言されたプロパティが 2 つだけ( Name と Category) があります。 メタデータには、CLR クラスの`Press.DynamicProperties`プロパティは含まれません。

## <a name="query-an-entity"></a>エンティティのクエリ

ISBN が "978-0-7356-7942-9" の書籍を入手するには、 GET`~/Books('978-0-7356-7942-9')`要求を 送信します。 応答本文は、次のようになります。 (読みやすくするためにインデントされます。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

動的プロパティは、宣言されたプロパティとインラインで含まれることに注意してください。

## <a name="post-an-entity"></a>エンティティの投稿

Book エンティティを追加するには、POST 要求を`~/Books`に送信します。 クライアントは、要求ペイロードに動的プロパティを設定できます。

リクエストの例を次に示します。 "価格" と "公開済み" プロパティに注意してください。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

コントローラー メソッドにブレークポイントを設定すると、Web API によってこれらのプロパティがディクショナリに追加されている`Properties`ことがわかります。

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>その他のリソース

[OData オープンタイプのサンプル](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
