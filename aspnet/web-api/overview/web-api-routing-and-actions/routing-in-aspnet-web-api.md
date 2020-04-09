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
# <a name="routing-in-aspnet-web-api"></a>ASP.NET Web API でのルーティング

[マイク・ワッソン](https://github.com/MikeWasson)著

この記事では、web API ASP.NETが HTTP 要求をコントローラーにルーティングする方法について説明します。

> [!NOTE]
> ASP.NET MVC に精通している場合、Web API ルーティングは MVC ルーティングとよく似ています。 主な違いは、Web API がアクションを選択するために URI パスではなく HTTP 動詞を使用することです。 Web API では MVC 形式のルーティングを使用することもできます。 この記事では、ASP.NET MVC の知識を前提としていません。

## <a name="routing-tables"></a>ルーティング テーブル

ASP.NET Web API では、*コントローラ*は HTTP 要求を処理するクラスです。 コントローラのパブリック メソッドは、*アクション メソッド*または単にアクション と呼*ばれます*。 Web API フレームワークは、要求を受信すると、要求をアクションにルーティングします。

呼び出すアクションを決定するために、フレームワークは*ルーティング テーブル*を使用します。 Web API 用の Visual Studio プロジェクト テンプレートは、既定のルートを作成します。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

このルートは *、WebApiConfig.cs*ファイルで定義され、*\_アプリケーションの開始*ディレクトリに配置されます。

![](routing-in-aspnet-web-api/_static/image1.png)

クラスの詳細については、「Web API の`WebApiConfig`[構成ASP.NET」](../advanced/configuring-aspnet-web-api.md)を参照してください。

Web API を自己ホストする場合は、オブジェクトにルーティング テーブルを`HttpSelfHostConfiguration`直接設定する必要があります。 詳細については、「 [Web API のセルフ ホスト](../older-versions/self-host-a-web-api.md)」を参照してください。

ルーティング テーブルの各エントリには、*ルート テンプレート*が含まれています。 Web API の既定のルート&quot;テンプレートは、API/{コントローラ}/{id} です&quot;。 このテンプレートでは&quot;、api&quot;はリテラル パス セグメントであり、{controller} と {id} はプレースホルダー変数です。

Web API フレームワークは、HTTP 要求を受信すると、ルーティング テーブル内のいずれかのルート テンプレートに対して URI を照合しようとします。 一致するルートがない場合、クライアントは 404 エラーを受け取ります。 たとえば、次の URI は既定のルートと一致します。

- /api/連絡先
- /api/連絡先/1
- /api/製品/ギズモ1

ただし、次の URI は&quot;API&quot;セグメントがないため一致しません。

- /連絡先/1

> [!NOTE]
> ルートで "api" を使用する理由は、MVC ルーティングとの衝突ASP.NET回避するためです。 このようにすると、/contacts&quot;&quot;を MVC コントローラーに移動し&quot;、/api/contact&quot;を Web API コントローラーに移動させることができます。 もちろん、この規則が気に入らない場合は、デフォルトのルートテーブルを変更できます。

一致するルートが見つかると、Web API はコントローラーとアクションを選択します。

- コントローラーを見つけるために、Web API &quot;&quot;は *{controller}* 変数の値にコントローラーを追加します。
- アクションを見つけるには、Web API は HTTP 動詞を検索し、その HTTP 動詞名で始まる名前のアクションを探します。 たとえば、GET 要求を使用すると、Web API は GetContact &quot;&quot;や&quot;GetAllContacts&quot;&quot;&quot;などの "Get" というプレフィックスが付いたアクションを検索します。 この規約は、GET、ポスト、プット、削除、ヘッド、オプション、およびパッチの動詞にのみ適用されます。 コントローラーの属性を使用して、他の HTTP 動詞を有効にすることができます。 その例については後で説明します。
- ルート テンプレート内の他のプレースホルダー変数 *({id}* など) は、アクション パラメーターにマップされます。

1 つ例を見てみましょう。 次のコントローラを定義するとします。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

以下に、考えられる HTTP 要求と、それぞれに対して呼び出されるアクションを示します。

| HTTP 動詞 | URI パス | アクション | パラメーター |
| --- | --- | --- | --- |
| GET | api/製品 | すべての製品を取得します。 | *(なし)* |
| GET | api/製品/4 | 製品バイId | 4 |
| DELETE | api/製品/4 | 製品の削除 | 4 |
| POST | api/製品 | *(一致しない)* |  |

URI の *{id}* セグメントが存在する場合は、アクションの*id*パラメーターにマップされることに注意してください。 この例では、コントローラは*2*つの GET メソッドを定義します。

また、コントローラは Post.. を定義していないため、POST 要求は&quot;失敗します。&quot;メソッドを使用します。

## <a name="routing-variations"></a>ルーティングバリエーション

前のセクションでは、Web API の基本的なルーティングメカニズムASP.NET説明しました。 このセクションでは、いくつかのバリエーションについて説明します。

### <a name="http-verbs"></a>HTTP 動詞

HTTP 動詞の名前付け規則を使用する代わりに、アクション メソッドを次のいずれかの属性で修飾することで、アクションの HTTP 動詞を明示的に指定できます。

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

次の例では、`FindProduct`メソッドが GET 要求にマップされています。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

アクションに複数の HTTP 動詞を許可したり、GET、PUT、POST、削除、ヘッド、オプション、および PATCH 以外の HTTP 動詞を`[AcceptVerbs]`許可したりするには、HTTP 動詞のリストを取る属性を使用します。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>アクション名によるルーティング

既定のルーティング テンプレートでは、Web API は HTTP 動詞を使用してアクションを選択します。 ただし、アクション名が URI に含まれるルートを作成することもできます。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

このルート テンプレートでは *、{action}* パラメーターはコントローラーのアクション メソッドに名前を付けます。 この形式のルーティングでは、属性を使用して、許可される HTTP 動詞を指定します。 たとえば、コントローラーに次のメソッドがあるとします。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

この場合、GET リクエストの "api/製品/詳細/1" はメソッドに`Details`マップされます。 このルーティングスタイルは、ASP.NET MVC に似ており、RPC スタイルの API に適している場合があります。

属性を使用して、アクション名を`[ActionName]`オーバーライドできます。 次の例では、api/製品/サムネイル/ &quot;*id*にマップする 2 つのアクションがあります。1 つは GET をサポートし、もう 1 つは POST をサポートします。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>非アクション

メソッドがアクションとして呼び出されないようにするには、 属性を使用`[NonAction]`します。 これは、メソッドがルーティングルールに一致する場合でも、メソッドがアクションではないことをフレームワークに通知します。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>参考資料

このトピックでは、ルーティングの概要を説明しました。 詳細については、「[ルーティングとアクションの選択](routing-and-action-selection.md)」を参照してください。
