---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: ASP.NET Web API 2 | の単体テストコントローラーMicrosoft Docs
author: MikeWasson
description: このトピックでは、Web API 2 の単体テストコントローラーの特定の手法について説明します。 このトピックを読む前に、「チュートリアル単位...」を読むことをお勧めします。
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3b89009a375e766f1c5b439dfe3fffd43b4963b3
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172927"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a>ASP.NET Web API 2 の単体テスト コントローラー

[Mike Wasson](https://github.com/MikeWasson)

> このトピックでは、Web API 2 の単体テストコントローラーの特定の手法について説明します。 このトピックを読む前に、単体テストプロジェクトをソリューションに追加する方法を示すチュートリアル[単体テスト ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)を読むことをお勧めします。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>このチュートリアルで使用されているソフトウェアのバージョン
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2
> - [Moq](https://github.com/Moq) 4.5.30

> [!NOTE]
> Moq を使用しましたが、モックフレームワークにも同じアイデアが適用されます。 Moq 4.5.30 (以降) は、Visual Studio 2017、Roslyn、.NET 4.5 以降のバージョンをサポートしています。

単体テストの一般的なパターンは、 &quot; 次のとおりです &quot; 。

- 配置: テストを実行するための前提条件を設定します。
- Act: テストを実行します。
- Assert: テストが成功したことを確認します。

配置手順では、モックオブジェクトまたはスタブオブジェクトを使用することがよくあります。 これにより、依存関係の数が最小限に抑えられるため、テストは1つのテストに重点を置いています。

ここでは、Web API コントローラーで単体テストを行う必要がある点をいくつか示します。

- アクションは、正しい種類の応答を返します。
- 無効なパラメーターは、正しいエラー応答を返します。
- アクションは、リポジトリまたはサービスレイヤーで適切なメソッドを呼び出します。
- 応答にドメインモデルが含まれている場合は、モデルの種類を確認します。

これらは一般的なテストですが、詳細はコントローラーの実装によって異なります。 特に、コントローラーアクションが**HttpResponseMessage**または**Ihttpactionresult**を返すかどうかに大きな違いがあります。 これらの結果の種類の詳細については、「 [Web Api 2 でのアクションの結果](../getting-started-with-aspnet-web-api/action-results.md)」を参照してください。

## <a name="testing-actions-that-return-httpresponsemessage"></a>HttpResponseMessage を返すアクションのテスト

アクションが**HttpResponseMessage**を返すコントローラーの例を次に示します。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

コントローラーは、依存関係の挿入を使用してを挿入することに注意して `IProductRepository` ください。 これにより、モックリポジトリを挿入できるため、コントローラーのテストが容易になります。 次の単体テストでは、 `Get` メソッドがを応答本文に書き込むことを確認し `Product` ます。 がモックであると仮定 `repository` `IProductRepository` します。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

コントローラーで**要求**と**構成**を設定することが重要です。 それ以外の場合、テストは**system.argumentnullexception**または**InvalidOperationException**で失敗します。

## <a name="testing-link-generation"></a>リンク生成のテスト

`Post`メソッドは、 **urlhelper. リンク**を呼び出して、応答内にリンクを作成します。 そのためには、単体テストでもう少しセットアップする必要があります。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

**Urlhelper**クラスには要求 URL とルートデータが必要であるため、テストでこれらの値を設定する必要があります。 もう1つのオプションは、モックまたはスタブ**Urlhelper**です。 この方法では、ApiController の既定値を、固定値を返すモックまたはスタブバージョンに置き換え[ます](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx)。

[Moq](https://github.com/Moq)フレームワークを使用してテストを書き直してみましょう。 `Moq`テストプロジェクトに NuGet パッケージをインストールします。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

このバージョンでは、モック**Urlhelper**が定数文字列を返すため、ルートデータを設定する必要はありません。

## <a name="testing-actions-that-return-ihttpactionresult"></a>IHttpActionResult を返すテストアクション

Web API 2 では、コントローラーアクションは**Ihttpactionresult**を返すことができます。これは ASP.NET MVC の**actionresult**に似ています。 **Ihttpactionresult**インターフェイスは、HTTP 応答を作成するためのコマンドパターンを定義します。 コントローラーは、応答を直接作成するのではなく、 **Ihttpactionresult**を返します。 後で、パイプラインは**Ihttpactionresult**を呼び出して応答を作成します。 この方法では、 **HttpResponseMessage**に必要なセットアップの大部分をスキップできるため、単体テストの記述が容易になります。

アクションが**Ihttpactionresult**を返すコントローラーの例を次に示します。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

この例では、 **Ihttpactionresult**を使用する一般的なパターンをいくつか示します。 単体テストの方法を見てみましょう。

### <a name="action-returns-200-ok-with-a-response-body"></a>アクションは、応答本文で 200 (OK) を返します

`Get` `Ok(product)` 製品が見つかった場合、メソッドはを呼び出します。 単体テストで、戻り値の型が**OkNegotiatedContentResult**で、返された製品の ID が正しいことを確認します。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

単体テストでは、アクションの結果は実行されないことに注意してください。 アクションの結果によって HTTP 応答が正しく作成されると想定できます。 (そのため、Web API フレームワークには独自の単体テストがあります)。

### <a name="action-returns-404-not-found"></a>アクションは 404 (見つかりません) を返します

`Get` `NotFound()` 製品が見つからない場合、メソッドはを呼び出します。 この場合、単体テストでは、戻り値の型が**notfound の結果**であるかどうかのみをチェックします。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a>アクションは、応答本文なしで 200 (OK) を返します

`Delete`メソッドは、 `Ok()` 空の HTTP 200 応答を返すを呼び出します。 前の例と同様に、単体テストは戻り値の型をチェックします。この場合は**Okresult**です。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a>アクションは、Location ヘッダーを含む 201 (Created) を返します

メソッドは、 `Post` を呼び出して、 `CreatedAtRoute` Location ヘッダーに URI を含む HTTP 201 応答を返します。 単体テストで、アクションによって正しいルーティング値が設定されていることを確認します。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a>アクションは、応答本文を含む別の2xx を返します

`Put`メソッドはを呼び出して、 `Content` 応答本文と共に HTTP 202 (受理) 応答を返します。 この例は、200 (OK) を返すのと似ていますが、単体テストでも状態コードを確認する必要があります。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a>その他のリソース

- [単体テスト時のモック Entity Framework ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- [ASP.NET Web API サービスのテストの作成](https://docs.microsoft.com/en-gb/archive/blogs/youssefm/writing-tests-for-an-asp-net-web-api-service)(Youssef Moussaoui によるブログ投稿)
- [ルート デバッグを使用した ASP.NET Web API のデバッグ](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
