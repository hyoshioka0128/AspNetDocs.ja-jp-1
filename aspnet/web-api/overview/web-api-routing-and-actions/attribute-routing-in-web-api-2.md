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
# <a name="attribute-routing-in-aspnet-web-api-2"></a>Web API 2 でASP.NET属性ルーティング

[マイク・ワッソン](https://github.com/MikeWasson)著

*ルーティング*とは、Web API がアクションに対して URI と一致する方法です。 Web API 2 は、属性ルーティング と呼ばれる新しいタイプの*ルーティングを*サポートします。 名前が示すように、属性ルーティングでは属性を使用してルートを定義します。 属性ルーティングを使用すると、Web API の URI をより詳細に制御できます。 たとえば、リソースの階層を記述する URI を簡単に作成できます。

以前の形式のルーティングは、規則ベースのルーティングと呼ばれ、引き続き完全にサポートされています。 実際には、同じプロジェクトで両方のテクニックを組み合わせることができます。

このトピックでは、属性ルーティングを有効にする方法を示し、属性ルーティングのさまざまなオプションについて説明します。 属性ルーティングを使用するエンド ツー エンド チュートリアルについては[、「Web API 2 での属性ルーティングを使用した REST API](create-a-rest-api-with-attribute-routing.md)の作成」を参照してください。

## <a name="prerequisites"></a>前提条件

[ビジュアルスタジオ2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)コミュニティ、プロフェッショナル、またはエンタープライズエディション

または、NuGet パッケージ マネージャーを使用して、必要なパッケージをインストールします。 Visual Studio の [**ツール]** メニューから **[NuGet パッケージ マネージャー**] を選択し、[**パッケージ マネージャー コンソール**] を選択します。 パッケージ マネージャー コンソール ウィンドウで次のコマンドを入力します。

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>属性ルーティングの理由

Web API の最初のリリースでは *、規則ベースの*ルーティングが使用されました。 このタイプのルーティングでは、基本的にパラメータ化された文字列である 1 つまたは複数のルート テンプレートを定義します。 フレームワークは、要求を受信すると、URI とルート テンプレートを照合します。 規則ベースのルーティングの詳細については、「 [Web API でのルーティングASP.NET](routing-in-aspnet-web-api.md)参照してください。

規則ベースのルーティングの利点の 1 つは、テンプレートが 1 か所で定義され、ルーティング規則がすべてのコントローラに一貫して適用される点です。 残念ながら、規則ベースのルーティングでは、RESTful API で一般的な特定の URI パターンをサポートすることが困難になります。 たとえば、多くの場合、リソースには子リソースが含まれます。 これらの関係を反映する URI を作成するのは当然です。

`/customers/1/orders`

この種類の URI は、規則ベースのルーティングを使用して作成するのが困難です。 これは可能ですが、コントローラーやリソースの種類が多い場合は、結果が適切に拡張されません。

属性ルーティングでは、この URI のルートを定義するのは簡単です。 コントローラーアクションに属性を追加するだけです。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

ここでは、属性ルーティングを容易にする他のパターンをいくつか示します。

**API のバージョン管理**

この例では、"/api/v1/products" は "/api/v2/products" とは異なるコントローラにルーティングされます。

`/api/v1/products`
`/api/v2/products`

**オーバーロードされた URI セグメント**

この例では、"1" は注文番号ですが、"保留" はコレクションにマップされます。

`/orders/1`
`/orders/pending`

**複数のパラメーター型**

この例では、"1" は注文番号ですが、"2013/06/16" は日付を指定します。

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>属性ルーティングの有効化

属性ルーティングを有効にするには、構成中に**MapHttpAttributeRoutes を**呼び出します。 この拡張メソッドは、**クラス**で定義されています。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

属性ルーティングは、[規則ベースの](routing-in-aspnet-web-api.md)ルーティングと組み合わせることができます。 規則に基づくルートを定義するには **、MapHttpRoute**メソッドを呼び出します。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

Web API の構成の詳細については、「Web API [2 の構成ASP.NET」](../advanced/configuring-aspnet-web-api.md)を参照してください。

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>注意: Web API 1 からの移行

Web API 2 より前の Web API プロジェクト テンプレートでは、次のようなコードが生成されます。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

属性ルーティングが有効になっている場合、このコードは例外をスローします。 属性ルーティングを使用するように既存の Web API プロジェクトをアップグレードする場合は、この構成コードを必ず次のように更新してください。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> 詳細については、「 [ASP.NET ホストを使用した Web API の構成](../advanced/configuring-aspnet-web-api.md#webhost)」を参照してください。

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>ルート属性の追加

属性を使用して定義されたルートの例を次に示します。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

文字列&quot;顧客/{顧客Id}/注文&quot;は、ルートの URI テンプレートです。 Web API は、要求 URI をテンプレートと照合しようとします。 この例では、「顧客」と「注文」はリテラル・セグメントであり、「{customerId}」は変数パラメーターです。 次の URI はこのテンプレートと一致します。

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

このトピックで後述する[制約](#constraints)を使用して、照合を制限できます。

ルート テンプレート&quot;の {customerId}&quot;パラメーターが、メソッドの*customerId*パラメーターの名前と一致していることに注意してください。 Web API は、コントローラー アクションを呼び出すときに、ルート パラメーターのバインドを試みます。 たとえば、URI が の`http://example.com/customers/1/orders`場合、Web API はアクションの*customerId*パラメーターに値 "1" をバインドしようとします。

URI テンプレートには、次のような複数のパラメーターを指定できます。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

ルート属性を持たないコントローラ メソッドは、規則ベースのルーティングを使用します。 このようにして、同じプロジェクトで両方の種類のルーティングを組み合わせることができます。

## <a name="http-methods"></a>HTTP メソッド

Web API は、リクエストの HTTP メソッド (GET、POST など) に基づいてアクションを選択します。 既定では、Web API は、コントローラー メソッド名の先頭に一致する大文字と小文字を区別しないものを検索します。 たとえば、HTTP PUT 要求`PutCustomers`と一致する名前のコントローラー メソッドが一致します。

この規則は、次の属性を使用してメソッドを修飾することでオーバーライドできます。

- **[HttpDelete]**
- **[HttpGet]**
- **[HttpHead]**
- **[オプション]**
- **[Httpパッチ]**
- **[HttpPost]**
- **[HttpPut]**

次の例では、CreateBook メソッドを HTTP POST 要求にマップします。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

非標準メソッドを含むその他のすべての HTTP メソッドでは、HTTP メソッドのリストを受け取る**AcceptVerbs**属性を使用します。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>ルート プレフィックス

多くの場合、コントローラ内のルートはすべて同じプレフィックスで始まります。 次に例を示します。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

**[RoutePrefix]** 属性を使用して、コントローラ全体に共通のプレフィックスを設定できます。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

メソッド属性でチルダ (~) を使用して、ルート プレフィックスをオーバーライドします。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

ルート プレフィックスには、次のパラメータを含めることができます。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>ルート制約

ルート制約を使用すると、ルート テンプレート内のパラメータの照合方法を制限できます。 一般的な構文&quot;は {パラメーター:&quot;制約} です。 次に例を示します。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

ここでは、最初のルートは、URI の&quot;id&quot;セグメントが整数の場合にのみ選択されます。 それ以外の場合は、2 番目のルートが選択されます。

次の表は、サポートされる制約の一覧です。

| 制約 | 説明 | 例 |
| --- | --- | --- |
| alpha | 大文字または小文字の英字 (a-z、A から Z) に一致する | {x:アルファ} |
| bool | ブール値に一致します。 | {x:ブール} |
| DATETIME | **日付時刻**の値に一致します。 | {x:日時} |
| decimal | 10 進値と一致します。 | {x:10 進数} |
| double | 64 ビット浮動小数点値に一致します。 | {x:double} |
| float | 32 ビット浮動小数点値に一致します。 | {x:フロート} |
| guid | GUID 値に一致します。 | {x:guid} |
| INT | 32 ビット整数値に一致します。 | {x:int} |
| length | 指定した長さまたは指定した長さの範囲内の文字列に一致します。 | {x:長さ(6)}{x:長さ(1,20)} |
| long | 64 ビット整数値に一致します。 | {x:長} |
| max | 最大値を持つ整数と一致します。 | {x:最大(10)} |
| Maxlength | 長さが最大の文字列と一致します。 | {x:最大長(10)} |
| min | 最小値を持つ整数と一致します。 | {x:分(10)} |
| 最小長さ | 長さが最小の文字列に一致します。 | {x:分の長さ(10)} |
| range | 値の範囲内の整数と一致します。 | {x:範囲(10,50)} |
| regex | 正規表現に一致します。 | {x:regex(^\d{3}-\d -\d{3}{4}$)} |

min&quot;&quot;などの制約の一部は、かっこで囲まれた引数を取ります。 コロンで区切って、パラメーターに複数の制約を適用できます。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>カスタム ルート制約

カスタム ルート制約を作成するには **、IHttpRouteConstraint**インターフェイスを実装します。 たとえば、次の制約は、パラメーターを 0 以外の整数値に制限します。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

次のコードは、制約を登録する方法を示しています。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

これで、ルートに制約を適用できます。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

インターフェイスを実装することで **、Default InlineConstraintResolver**クラス全体を**IInlineConstraintResolver**置き換えることもできます。 これを行うと **、IInlineConstraintResolver**の実装で明示的に追加されない限り、組み込み制約がすべて置き換えられます。

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>オプションの URI パラメーターとデフォルト値

ルート パラメータに疑問符を追加することで、URI パラメータをオプションにすることができます。 ルート パラメータがオプションの場合は、メソッド パラメータの既定値を定義する必要があります。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

この例では、`/api/books/locale/1033``/api/books/locale`同じリソースを返します。

または、次のように、ルート テンプレート内の既定値を指定できます。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

これは前の例とほぼ同じですが、デフォルト値を適用すると動作が若干異なります。

- 最初の例 ("{lcid:int?}") では、既定値の 1033 がメソッド パラメーターに直接割り当てられるため、パラメーターはこの正確な値を持ちます。
- 2 番目の例 ("{lcid:int=1033}" )では、既定値の "1033" はモデル バインド プロセスを通過します。 デフォルトのモデルバインダーは、"1033" を数値 1033 に変換します。 ただし、カスタム モデル バインダーをプラグインすると、何か違う可能性があります。

(ほとんどの場合、パイプラインにカスタム モデル バインダーがない限り、2 つのフォームは同等になります。

<a id="route-names"></a>
## <a name="route-names"></a>ルート名

Web API では、すべてのルートに名前が付けられます。 ルート名は、HTTP 応答にリンクを含めることができるように、リンクを生成するのに便利です。

ルート名を指定するには、属性の**Name**プロパティを設定します。 次の例は、ルート名を設定する方法と、リンクを生成するときにルート名を使用する方法を示しています。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>ルートオーダー

フレームワークは、URI とルートを照合しようとする際に、特定の順序でルートを評価します。 順序を指定するには、ルート属性の**Order**プロパティを設定します。 小さい値が最初に評価されます。 デフォルトの注文値はゼロです。

合計順序付けがどのように決定されるかは次のとおりです。

1. ルート属性の**Order**プロパティを比較します。
2. ルート テンプレートの各 URI セグメントを確認します。 各セグメントについて、次のように順序を付け、

    1. リテラル セグメント。
    2. 制約を使用してパラメータをルーティングします。
    3. 制約のないルート パラメータ。
    4. 制約付きのワイルドカード パラメータ セグメント。
    5. 制約のないワイルドカード パラメータ セグメント。
3. タイの場合、ルートはルート テンプレートの大文字と小文字を区別しない序数文字列比較 ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) によって順序付けられます。

次に例を示します。 次のコントローラを定義するとします。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

これらのルートは次のように並べられます。

1. 注文/詳細
2. 注文/{id}
3. 注文/{顧客名}
4. 注文/{\*日付}
5. 注文/保留中

"details" はリテラル セグメントであり、"{id}" の前に表示されますが **、Order**プロパティが 1 であるため、"pending" が最後に表示されます。 (この例では、"details" または "pending" という名前の顧客が存在しないものとします。 一般に、あいまいなルートを避けるようにしてください。 この例では、より優れたルート`GetByCustomer`テンプレートは "顧客/{顧客名}" です)。
