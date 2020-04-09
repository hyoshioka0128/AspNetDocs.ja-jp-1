---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: Web API における認証と承認ASP.NET |マイクロソフトドキュメント
author: MikeWasson
description: Web API での認証と承認の概要ASP.NET提供します。
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675863"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>ASP.NET Web API での認証と承認

[マイク・ワッソン](https://github.com/MikeWasson)著

Web API を作成しましたが、次は Web API へのアクセスを制御する必要があります。 この一連の記事では、承認されていないユーザーから Web API を保護するためのいくつかのオプションについて説明します。 このシリーズでは、認証と承認の両方について説明します。

- *認証*は、ユーザーの ID を知っています。 たとえば、Alice はユーザー名とパスワードでログインし、サーバーはパスワードを使用して Alice を認証します。
- *承認*は、ユーザーがアクションを実行できるかどうかを決定します。 たとえば、Alice にはリソースを取得する権限がありますが、リソースを作成することはできません。

シリーズの最初の記事では、Web API における認証と承認の概要ASP.NET説明します。 その他のトピックでは、Web API の一般的な認証シナリオについて説明します。

> [!NOTE]
> このシリーズをレビューし、貴重なフィードバックを提供してくれた人々に感謝します:リック・アンダーソン、リーバイ・ブロデリック、バリー・ドランス、トム・ダイクストラ、ホンメイ・ゲ、デビッド・マットソン、ダニエル・ロス、ティム・ティーケン。

## <a name="authentication"></a>認証

Web API は、認証がホストで行われると想定しています。 Web ホスティングの場合、ホストは IIS で、認証に HTTP モジュールを使用します。 IIS または ASP.NET に組み込まれている認証モジュールを使用するようにプロジェクトを構成したり、独自の HTTP モジュールを記述してカスタム認証を実行したりできます。

ホストは、ユーザーを認証するときに、コードが実行されているセキュリティ コンテキストを表す[IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx)オブジェクトである*プリンシパル*を作成します。 ホストは **、Thread.CurrentPrincipal**を設定することで、プリンシパルを現在のスレッドにアタッチします。 プリンシパルには、ユーザーに関する情報を含む関連付けられた**Identity**オブジェクトが含まれています。 ユーザーが認証されている場合 **、Identity.IsAuthenticated**プロパティは**true**を返します。 匿名要求の場合 **、IsAuthenticated は** **false**を返します。 プリンシパルの詳細については、「[ロールベースのセキュリティ](https://msdn.microsoft.com/library/shz8h065.aspx)」を参照してください。

### <a name="http-message-handlers-for-authentication"></a>認証用の HTTP メッセージ ハンドラ

認証にホストを使用する代わりに、認証ロジックを HTTP[メッセージ ハンドラ](../advanced/http-message-handlers.md)に入れることができます。 その場合、メッセージ ハンドラーは HTTP 要求を調べてプリンシパルを設定します。

認証にメッセージ ハンドラを使用する必要がある場合 いくつかのトレードオフを次に示します。

- HTTP モジュールは、ASP.NET パイプラインを通過するすべての要求を参照します。 メッセージ ハンドラーは、Web API にルーティングされた要求のみを参照します。
- ルートごとのメッセージ ハンドラを設定して、特定のルートに認証スキームを適用できます。
- HTTP モジュールは IIS に固有のものです。 メッセージ ハンドラーはホストに依存しないため、Web ホスティングとセルフ ホスティングの両方で使用できます。
- HTTP モジュールは、IIS ログ、監査などに参加します。
- HTTP モジュールは、パイプラインで以前に実行されます。 メッセージ ハンドラーで認証を処理する場合、プリンシパルはハンドラーが実行されるまで設定されません。 さらに、応答がメッセージ ハンドラーから離れると、プリンシパルは前のプリンシパルに戻ります。

一般的に、自己ホストをサポートする必要がない場合は、HTTPモジュールが適しています。 自己ホストをサポートする必要がある場合は、メッセージ ハンドラーを検討してください。

### <a name="setting-the-principal"></a>プリンシパルの設定

アプリケーションでカスタム認証ロジックを実行する場合は、次の 2 つの場所でプリンシパルを設定する必要があります。

- **スレッド.現在のプリンシパル**。 このプロパティは、.NET でスレッドのプリンシパルを設定する標準的な方法です。
- **ユーザー**. このプロパティは、ASP.NETに固有です。

次のコードは、プリンシパルを設定する方法を示しています。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

Web ホスティングの場合は、両方の場所でプリンシパルを設定する必要があります。そうしないと、セキュリティ コンテキストが矛盾する可能性があります。 ただし、自己ホストの場合は **、HttpContext.Current**は null です。 コードがホストに依存しないようにするには、次に示すように**HttpContext.Current**に割り当てる前に null を確認します。

## <a name="authorization"></a>承認

承認は、後でパイプラインで、コントローラーに近い状態で行われます。 これにより、リソースへのアクセスを許可するときに、より細かい選択を行うことができます。

- *承認フィルター*は、コントローラーアクションの前に実行されます。 要求が承認されていない場合、フィルターはエラー応答を返し、アクションは呼び出されません。
- コントローラー アクション内で **、ApiController.User**プロパティから現在のプリンシパルを取得できます。 たとえば、ユーザー名に基づいてリソースの一覧をフィルタし、そのユーザーに属するリソースのみを返す場合があります。

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>[承認] 属性の使用

Web API には、組み込みの承認フィルター[が用意されています](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。 このフィルタは、ユーザーが認証されているかどうかを確認します。 それでない場合は、アクションを呼び出さずに HTTP ステータス コード 401 (許可されていません) を返します。

フィルタは、グローバル、コントローラ レベル、または個々のアクションのレベルで適用できます。

**グローバル**: すべての Web API コントローラーのアクセスを制限するには、グローバル フィルター リストに**AuthorizeAttribute**フィルターを追加します。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**コントローラ**: 特定のコントローラへのアクセスを制限するには、コントローラに属性としてフィルタを追加します。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**アクション**: 特定のアクションへのアクセスを制限するには、アクション メソッドに属性を追加します。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

または、コントローラを制限し、属性を使用して特定のアクションへの匿名アクセスを`[AllowAnonymous]`許可することもできます。 次の例では、`Post`メソッドは制限されていますが、メソッドは`Get`匿名アクセスを許可しています。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

前の例では、フィルタにより、認証されたユーザーが制限されたメソッドにアクセスできるようになります。匿名ユーザーのみが除外されます。アクセスを特定のユーザーまたは特定のロールのユーザーに制限することもできます。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Web API コントローラーの**承認属性**フィルターは、**名前空間**内にあります。 Web API コントローラーと互換性のない **、System.Web.Mvc**名前空間内の MVC コント ローラーの同様のフィルターがあります。

### <a name="custom-authorization-filters"></a>カスタム承認フィルタ

カスタム承認フィルターを作成するには、次のいずれかの型から派生します。

- **属性を承認**します。 現在のユーザーとユーザーのロールに基づいて承認ロジックを実行するには、このクラスを拡張します。
- **フィルター属性を指定**します。 このクラスを拡張して、現在のユーザーまたはロールに基づくとは限らない同期承認ロジックを実行します。
- **I 認証フィルター .** 非同期承認ロジックを実行するには、このインターフェイスを実装します。たとえば、承認ロジックが非同期 I/O またはネットワーク呼び出しを行う場合などです。 (承認ロジックが CPU にバインドされている場合は、非同期メソッドを記述する必要がないため **、AuthorizationFilterAttribute**から派生する方が簡単です。

次の図は、**クラスのクラス**階層を示しています。

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>コントローラ アクション内の承認

場合によっては、要求の続行を許可し、プリンシパルに基づいて動作を変更する場合があります。 たとえば、ユーザーのロールによって、返される情報が変わる場合があります。 コントローラー メソッド内で、現在のプリンシパルを**取得できます。**

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
