---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: .NET クライアントから Web API を呼び出す (C#)-ASP.NET 4.x
author: MikeWasson
description: このチュートリアルでは、.NET 4.x アプリケーションから web API を呼び出す方法について説明します。
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 484d927eeb0ba49f5f00d476f4658ebc081d0a4a
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172940"
---
# <a name="call-a-web-api-from-a-net-client-c"></a>.NET クライアントから Web API を呼び出す (C#)

by [Mike Wasson](https://github.com/MikeWasson)および[Rick Anderson](https://twitter.com/RickAndMSFT)

[完成したプロジェクトをダウンロード](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)します。 [ダウンロードの方法はこちらをご覧ください。](/aspnet/core/tutorials/#how-to-download-a-sample) 

このチュートリアルでは、.NET アプリケーションから web API を呼び出す方法につい[て説明します](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)。

このチュートリアルでは、次の web API を使用するクライアントアプリを作成します。

| アクション | HTTP メソッド | 相対 URI |
| --- | --- | --- |
| ID で製品を取得する | GET | /api/*id* |
| 新しい製品の作成 | POST | /api/製品 |
| 製品を更新する | PUT | /api/*id* |
| 製品を削除する | DELETE | /api/*id* |

ASP.NET Web API でこの API を実装する方法については、「 [CRUD 操作をサポートする WEB api の作成](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)」を参照してください。

わかりやすくするために、このチュートリアルのクライアントアプリケーションは Windows コンソールアプリケーションです。 **Httpclient**は、Windows Phone および Windows ストアアプリでもサポートされています。 詳細については、「[ポータブルライブラリを使用して複数のプラットフォームの WEB API クライアントコードを作成](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)する」を参照してください。

**注:** ベース Url と相対 Uri をハードコーディングされた値として渡す場合は、API を利用するための規則に注意して `HttpClient` ください。 プロパティは、 `HttpClient.BaseAddress` 末尾のスラッシュ () を含むアドレスに設定する必要があり `/` ます。 たとえば、ハードコーディングされたリソース Uri をメソッドに渡す場合は、 `HttpClient.GetAsync` 先頭にスラッシュを入れないでください。 ID でを取得するには `Product` :

1. 一連`client.BaseAddress = new Uri("https://localhost:5001/");`
1. を要求 `Product` します。 たとえば、`client.GetAsync<Product>("api/products/4");` のようにします。

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a>コンソール アプリケーションを作成する

Visual Studio で、 **HttpClientSample**という名前の新しい Windows コンソールアプリを作成し、次のコードを貼り付けます。

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

上記のコードは、完全なクライアントアプリです。

`RunAsync`が実行され、完了するまでブロックされます。 ほとんどの**Httpclient**メソッドは、ネットワーク i/o を実行するため、非同期です。 すべての非同期タスクは、内部で実行され `RunAsync` ます。 通常、アプリはメインスレッドをブロックしませんが、このアプリは相互作用を許可しません。

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a>Web API クライアントライブラリをインストールする

NuGet パッケージマネージャーを使用して、Web API クライアントライブラリパッケージをインストールします。

**[ツール]** メニューで、**[NuGet パッケージ マネージャー]** > **[パッケージ マネージャー コンソール]** の順に選択します。 パッケージマネージャーコンソール (PMC) で、次のコマンドを入力します。

`Install-Package Microsoft.AspNet.WebApi.Client`

上記のコマンドは、プロジェクトに次の NuGet パッケージを追加します。

* WebApi (Microsoft AspNet. クライアント)
* Newtonsoft.Json

Netwonsoft (Json.NET とも呼ばれます) は、.NET 用の一般的な高パフォーマンスの JSON フレームワークです。

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a>モデルクラスの追加

次の `Product` クラスを調べます。

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

このクラスは、web API によって使用されるデータモデルと一致します。 アプリは**Httpclient**を使用して、 `Product` HTTP 応答からインスタンスを読み取ることができます。 アプリでは、逆シリアル化コードを記述する必要はありません。

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a>HttpClient を作成して初期化する

静的**Httpclient**プロパティを確認します。

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

**Httpclient**は、1回だけインスタンス化し、アプリケーションの有効期間全体に再利用することを目的としています。 次の状況では、 **Socketexception**エラーが発生する可能性があります。

* 要求ごとに新しい**Httpclient**インスタンスを作成しています。
* サーバーの負荷が高くなっています。

要求ごとに新しい**Httpclient**インスタンスを作成すると、使用可能なソケットが枯渇する可能性があります。

次のコードでは、 **Httpclient**インスタンスを初期化します。

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

上記のコードでは次の操作が行われます。

* HTTP 要求のベース URI を設定します。 ポート番号を、サーバーアプリで使用するポートに変更します。 サーバーアプリのポートが使用されていない場合、アプリは機能しません。
* Accept ヘッダーを "application/json" に設定します。 このヘッダーを設定すると、JSON 形式でデータを送信するようにサーバーに指示されます。

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a>GET 要求を送信してリソースを取得する

次のコードは、製品の GET 要求を送信します。

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

**GetAsync**メソッドは、HTTP GET 要求を送信します。 メソッドが完了すると、HTTP 応答を含む**HttpResponseMessage**が返されます。 応答の状態コードが成功コードである場合、応答本文には製品の JSON 表現が含まれます。 **Readasasync**を呼び出して、JSON ペイロードをインスタンスに逆シリアル化し `Product` ます。 応答本文は任意に大きくなる可能性があるため、 **Readasasync**メソッドは非同期です。

**Httpclient**は、HTTP 応答にエラーコードが含まれている場合に例外をスローしません。 状態がエラーコードの場合 **、"プロパティ**の報告" プロパティは**false**になります。 HTTP エラーコードを例外として扱う場合は、応答オブジェクトで[EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx)を呼び出します。 `EnsureSuccessStatusCode`ステータスコードが 200 299 の範囲外になると、例外がスローさ &ndash; れます。 **Httpclient**は、要求がタイムアウトした場合など、他の理由で例外をスローする場合があることに注意 &mdash; してください。

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a>逆シリアル化するメディアの種類のフォーマッタ

パラメーターを使用せずに**Readasasync**を呼び出すと、既定の*メディアフォーマッタ*セットを使用して応答本文が読み取られます。 既定のフォーマッタは、JSON、XML、およびフォーム url でエンコードされたデータをサポートします。

既定のフォーマッタを使用する代わりに、フォーマッタのリストを**Readasasync**メソッドに渡すことができます。  カスタムのメディアタイプフォーマッタがある場合は、フォーマッタの一覧を使用すると便利です。

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

詳細については、「 [ASP.NET Web API 2 のメディアフォーマッタ](../formats-and-model-binding/media-formatters.md)」を参照してください。

## <a name="sending-a-post-request-to-create-a-resource"></a>POST 要求を送信してリソースを作成する

次のコードは、インスタンスを含む POST 要求を `Product` JSON 形式で送信します。

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

**Postasjsonasync**メソッド:

* オブジェクトを JSON にシリアル化します。
* POST 要求で JSON ペイロードを送信します。

要求が成功した場合は、次のようになります。

* このメソッドは、201 (Created) 応答を返します。
* 応答には、作成されたリソースの URL を Location ヘッダーに含める必要があります。

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a>PUT 要求を送信してリソースを更新する

次のコードは、製品を更新する PUT 要求を送信します。

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

**PutAsJsonAsync**メソッドは**Postasjsonasync**と同様に機能しますが、POST ではなく PUT 要求を送信する点が異なります。

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a>削除要求を送信してリソースを削除する

次のコードは、削除要求を送信して製品を削除します。

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

GET と同様、DELETE 要求には要求本文がありません。 DELETE を使用して JSON または XML 形式を指定する必要はありません。

## <a name="test-the-sample"></a>サンプルをテストする

クライアントアプリをテストするには:

1. サーバーアプリを[ダウンロード](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server)して実行します。 [ダウンロードの方法はこちらをご覧ください。](/aspnet/core/#how-to-download-a-sample) サーバーアプリが動作していることを確認します。 たとえば、は `http://localhost:64195/api/products` 製品の一覧を返す必要があります。
2. HTTP 要求のベース URI を設定します。 ポート番号を、サーバーアプリで使用するポートに変更します。
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. クライアント アプリを実行します。 次の出力が生成されます。

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
