---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: ASP.NET Web API 2-ASP.NET 4.x での OData クエリオプションのサポート
author: MikeWasson
description: 概要 (コード例を含む) では、ASP.NET 4.x の ASP.NET Web API 2 での OData クエリオプションのサポートを示します。
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 96820fab7ac89885058962f44ded86cb0184ee97
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "86188629"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a>ASP.NET Web API 2 での OData クエリオプションのサポート

[Mike Wasson](https://github.com/MikeWasson)

この概要とコード例では、ASP.NET 4.x の ASP.NET Web API 2 での OData クエリオプションのサポートを示します。 

Odata は、OData クエリを変更するために使用できるパラメーターを定義します。 クライアントは、これらのパラメーターを要求 URI のクエリ文字列に送信します。 たとえば、結果を並べ替えるために、クライアントは $orderby パラメーターを使用します。

`http://localhost/Products?$orderby=Name`

OData 仕様では、これらのパラメーター*クエリオプション*が呼び出されます。 プロジェクト内の任意の Web API コントローラーの OData クエリオプションを有効にすることができ &#8212; コントローラーは OData エンドポイントである必要はありません。 これにより、フィルター処理や並べ替えなどの機能を任意の Web API アプリケーションに追加できます。

クエリオプションを有効にする前に、「 [OData セキュリティガイダンス](odata-security-guidance.md)」を参照してください。

- [OData クエリオプションの有効化](#enable)
- [クエリの例](#examples)
- [サーバー主導のページング](#server-paging)
- [クエリオプションの制限](#limiting_query_options)
- [クエリオプションの直接呼び出し](#ODataQueryOptions)
- [クエリの検証](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a>OData クエリオプションの有効化

Web API では、次の OData クエリオプションがサポートされています。

| オプション | 説明 |
| --- | --- |
| $expand | 関連エンティティをインラインで展開します。 |
| $filter | ブール条件に基づいて結果をフィルター処理します。 |
| $inlinecount | 応答内の一致するエンティティの合計数を含めるようにサーバーに指示します。 (サーバー側のページングに役立ちます)。 |
| $orderby | 結果を並べ替えます。 |
| $select | 応答に含めるプロパティを選択します。 |
| $skip | 最初の n 件の結果をスキップします。 |
| $top | 最初の n 件の結果のみを返します。 |

OData クエリオプションを使用するには、それらを明示的に有効にする必要があります。 アプリケーション全体でグローバルに有効にすることも、特定のコントローラーまたは特定のアクションに対して有効にすることもできます。

OData クエリオプションをグローバルに有効にするには、起動時に**Httpconfiguration**クラスで**enablequerysupport**を呼び出します。

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

**Enablequerysupport**メソッドは、 **IQueryable**型を返す任意のコントローラーアクションに対して、クエリオプションをグローバルに有効にします。 アプリケーション全体に対してクエリオプションを有効にしない場合は、[クエリ可能 **]** 属性をアクションメソッドに追加することで、特定のコントローラーアクションに対して有効にすることができます。

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a>クエリの例

ここでは、OData クエリオプションを使用して可能なクエリの種類について説明します。 クエリオプションの詳細については、 [www.odata.org](http://www.odata.org/)にある OData のドキュメントを参照してください。

$Expand と $select の詳細については、「 [$Value OData での $select、$expand、および ASP.NET Web API の使用](using-select-expand-and-value.md)」を参照してください。

**クライアント主導のページング**

大きなエンティティセットの場合、クライアントは結果の数を制限することがあります。 たとえば、クライアントが一度に10個のエントリを表示し、[次へ] リンクを使用して結果の次のページを取得する場合があります。 これを行うために、クライアントは $top オプションと $skip オプションを使用します。

`http://localhost/Products?$top=10&$skip=20`

$Top オプションは、返されるエントリの最大数を指定し、$skip オプションはスキップするエントリの数を指定します。 前の例では、21 ~ 30 のエントリをフェッチします。

**フィルター処理**

$Filter オプションを使用すると、クライアントはブール式を適用して結果をフィルター処理できます。 フィルター式は非常に強力です。これには、論理演算子、算術演算子、文字列関数、および日付関数が含まれます。

| カテゴリが "Toys" のすべての製品を返します。 | `http://localhost/Products?$filter=Category`eq ' Toys ' |
| --- | --- |
| 価格が10未満のすべての製品を返します。 | `http://localhost/Products?$filter=Price`lt 10 |
| 論理演算子: price >= 5、price <= 15 のすべての製品を返します。 | `http://localhost/Products?$filter=Price`ge 5 と価格 le 15 |
| 文字列関数: 名前に "zz" を含むすべての製品を返します。 | `http://localhost/Products?$filter=substringof('zz',Name)` |
| 日付関数: 2005 より後の ReleaseDate を含むすべての製品を返します。 | `http://localhost/Products?$filter=year(ReleaseDate)`gt 2005 |

**並べ替え**

結果を並べ替えるには、$orderby フィルターを使用します。

| 価格で並べ替えます。 | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| 価格で降順に並べ替えます (最高から最低)。 | `http://localhost/Products?$orderby=Price desc` |
| カテゴリで並べ替え、カテゴリ内で降順に並べ替えます。 | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a>サーバー主導のページング

データベースに何百万ものレコードが含まれている場合、それらすべてを1つのペイロードで送信することは望ましくありません。 これを回避するために、サーバーは単一の応答で送信するエントリの数を制限できます。 サーバーのページングを有効にするには、**クエリ**可能属性で**PageSize**プロパティを設定します。 値は、返されるエントリの最大数です。

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

コントローラーが OData 形式を返す場合、応答本文には次のデータページへのリンクが含まれます。

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

クライアントは、このリンクを使用して次のページを取得できます。 クライアントは、結果セット内のエントリの合計数を調べるために、値 "allpages" を使用して $inlinecount クエリオプションを設定できます。

`http://localhost/Products?$inlinecount=allpages`

値 "allpages" は、応答に合計数を含めるようにサーバーに指示します。

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> 次のページへのリンクとインラインカウントはどちらも OData 形式を必要とします。 その理由は、OData は、リンクとカウントを保持するために、応答本文に特別なフィールドを定義するためです。

非 OData 形式の場合でも、クエリの結果を**PageResult &lt; T &gt; **オブジェクトにラップすることで、次のページへのリンクとインラインカウントをサポートできます。 ただし、もう少しコードが必要です。 たとえば次のようになります。

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

JSON 応答の例を次に示します。

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a>クエリオプションの制限

クエリオプションを指定すると、クライアントはサーバーで実行されるクエリに対して多数の制御を行うことができます。 場合によっては、セキュリティやパフォーマンス上の理由で、使用可能なオプションを制限する必要があります。 **[クエリ可能]** 属性には、このの組み込みプロパティがいくつかあります。 次に例をいくつか示します。

ページングだけをサポートするために、$skip と $top のみを許可します。

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

特定のプロパティによってのみ順序付けを許可し、データベースでインデックスが作成されていないプロパティの並べ替えを防止します。

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

"Eq" 論理関数は許可しますが、その他の論理関数は使用できません。

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

算術演算子は使用できません。

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

**QueryableAttribute**インスタンスを構築し、それを**enablequerysupport**関数に渡すことで、オプションをグローバルに制限できます。

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a>クエリオプションの直接呼び出し

[クエリ可能 **]** 属性を使用する代わりに、コントローラーで直接クエリオプションを呼び出すことができます。 これを行うには、コントローラーメソッドに **、パラメーターを**追加します。 この場合、 **[クエリ可能]** 属性は必要ありません。

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

Web API は、URI クエリ文字列からの格納**オプションを設定**します。 クエリを適用するには、 **IQueryable** **を applyto**メソッドに渡します。 メソッドは、別の**IQueryable**を返します。

高度なシナリオでは、 **IQueryable**クエリプロバイダーを持っていない場合は、表示されている**オプション**を調べて、クエリオプションを別の形式に変換することができます。 (例については、「RaghuRam n Minti のブログ記事」を参照してください。これには、[サンプル](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)も含まれている[HQL に OData クエリを変換](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)します)。

<a id="query-validation"></a>
## <a name="query-validation"></a>クエリの検証

[クエリ可能 **]** 属性は、クエリを実行する前に検証します。 検証手順は、 **QueryableAttribute**メソッドで実行されます。 検証プロセスをカスタマイズすることもできます。

「 [OData セキュリティガイダンス](odata-security-guidance.md)」も参照してください。

最初に、 **web.config**名前空間で定義されているいずれかの検証クラスをオーバーライドします。 たとえば、次のバリデータークラスは、$orderby オプションの ' desc ' オプションを無効にします。

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

**[クエリ可能]** 属性をサブクラス化して、 **validatequery**メソッドをオーバーライドします。

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

次に、カスタム属性をグローバルまたはコントローラーごとに設定します。

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

使用する場合は、次のように、オプションの検証**コントロールを設定**します。

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
