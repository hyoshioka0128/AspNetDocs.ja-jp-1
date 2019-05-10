---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: ASP.NET Web API で HTML フォーム データを送信します。Url エンコード フォーム データ - ASP.NET 4.x
author: MikeWasson
description: この記事では、asp.net Web API コント ローラーに url エンコード フォーム データをポストする方法を示しています 4.x。
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115464"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="e994d-103">ASP.NET Web API で HTML フォーム データを送信します。URL エンコード フォーム データ</span><span class="sxs-lookup"><span data-stu-id="e994d-103">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>

<span data-ttu-id="e994d-104">作成者[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e994d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="e994d-105">第 1 部:URL エンコード フォーム データ</span><span class="sxs-lookup"><span data-stu-id="e994d-105">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="e994d-106">この記事では、Web API コント ローラーに url エンコード フォーム データをポストする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="e994d-106">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="e994d-107">HTML フォームの概要</span><span class="sxs-lookup"><span data-stu-id="e994d-107">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="e994d-108">複合型を送信します。</span><span class="sxs-lookup"><span data-stu-id="e994d-108">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="e994d-109">AJAX を使用してフォーム データを送信します。</span><span class="sxs-lookup"><span data-stu-id="e994d-109">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="e994d-110">単純型を送信します。</span><span class="sxs-lookup"><span data-stu-id="e994d-110">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="e994d-111">[完成したプロジェクトをダウンロード](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)します。</span><span class="sxs-lookup"><span data-stu-id="e994d-111">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="e994d-112">HTML フォームの概要</span><span class="sxs-lookup"><span data-stu-id="e994d-112">Overview of HTML Forms</span></span>

<span data-ttu-id="e994d-113">HTML フォームの使用か、取得、または、サーバーにデータを送信する投稿します。</span><span class="sxs-lookup"><span data-stu-id="e994d-113">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="e994d-114">**メソッド**の属性、**フォーム**要素は、HTTP メソッド。</span><span class="sxs-lookup"><span data-stu-id="e994d-114">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="e994d-115">既定のメソッドには GET です。</span><span class="sxs-lookup"><span data-stu-id="e994d-115">The default method is GET.</span></span> <span data-ttu-id="e994d-116">フォームで使用する場合の取得、データがクエリ文字列としての URI でエンコードされたフォーム。</span><span class="sxs-lookup"><span data-stu-id="e994d-116">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="e994d-117">フォーム POST を使用する場合は、フォーム データが要求本文に配置されます。</span><span class="sxs-lookup"><span data-stu-id="e994d-117">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="e994d-118">データの送信、 **enctype**属性が要求本文の形式を指定します。</span><span class="sxs-lookup"><span data-stu-id="e994d-118">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="e994d-119">enctype</span><span class="sxs-lookup"><span data-stu-id="e994d-119">enctype</span></span> | <span data-ttu-id="e994d-120">説明</span><span class="sxs-lookup"><span data-stu-id="e994d-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e994d-121">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="e994d-121">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="e994d-122">フォーム データは、URI クエリ文字列のような名前と値のペアとしてエンコードされます。</span><span class="sxs-lookup"><span data-stu-id="e994d-122">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="e994d-123">これは、投稿の既定の形式です。</span><span class="sxs-lookup"><span data-stu-id="e994d-123">This is the default format for POST.</span></span> |
| <span data-ttu-id="e994d-124">マルチパート/フォーム データ</span><span class="sxs-lookup"><span data-stu-id="e994d-124">multipart/form-data</span></span> | <span data-ttu-id="e994d-125">フォーム データは、マルチパート MIME メッセージとしてエンコードされます。</span><span class="sxs-lookup"><span data-stu-id="e994d-125">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="e994d-126">サーバーにファイルをアップロードする場合は、この形式を使用します。</span><span class="sxs-lookup"><span data-stu-id="e994d-126">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="e994d-127">この記事の第 1 部では、x-www-form-urlencoded 形式で検索します。</span><span class="sxs-lookup"><span data-stu-id="e994d-127">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="e994d-128">[第 2 部](sending-html-form-data-part-2.md)マルチパート MIME について説明します。</span><span class="sxs-lookup"><span data-stu-id="e994d-128">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="e994d-129">複合型を送信します。</span><span class="sxs-lookup"><span data-stu-id="e994d-129">Sending Complex Types</span></span>

<span data-ttu-id="e994d-130">通常は、複数のフォーム コントロールから取得した値から成る複合型を送信します。</span><span class="sxs-lookup"><span data-stu-id="e994d-130">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="e994d-131">ステータスの更新を表す次のモデルを検討してください。</span><span class="sxs-lookup"><span data-stu-id="e994d-131">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="e994d-132">受け取る Web API コント ローラーを次に示します、 `Update` POST 経由でのオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="e994d-132">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="e994d-133">このコント ローラーを使用して[アクション ベースのルーティング](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)でルート テンプレートがあるため、 &quot;api/{controller}/{action}/{id}&quot;します。</span><span class="sxs-lookup"><span data-stu-id="e994d-133">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="e994d-134">クライアントは、データをポスト&quot;/api/updates/complex&quot;します。</span><span class="sxs-lookup"><span data-stu-id="e994d-134">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>

<span data-ttu-id="e994d-135">これでユーザー状態の更新を送信するための HTML フォームを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="e994d-135">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="e994d-136">注意、**アクション**フォーム上の属性は、コント ローラー アクションの URI。</span><span class="sxs-lookup"><span data-stu-id="e994d-136">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="e994d-137">フォームに入力されたいくつかの値を次に示します。</span><span class="sxs-lookup"><span data-stu-id="e994d-137">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="e994d-138">ユーザーは、送信をクリックすると、ブラウザーが送信 HTTP 要求を次のような。</span><span class="sxs-lookup"><span data-stu-id="e994d-138">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="e994d-139">要求本文がフォーム データには、名前/値ペアとして書式設定が含まれていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e994d-139">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="e994d-140">Web API がのインスタンスに自動的に名前/値ペアを変換、`Update`クラス。</span><span class="sxs-lookup"><span data-stu-id="e994d-140">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="e994d-141">AJAX を使用してフォーム データを送信します。</span><span class="sxs-lookup"><span data-stu-id="e994d-141">Sending Form Data via AJAX</span></span>

<span data-ttu-id="e994d-142">ユーザーは、フォームを送信して、ブラウザーが現在のページから離れた応答メッセージの本文を表示します。</span><span class="sxs-lookup"><span data-stu-id="e994d-142">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="e994d-143">応答が HTML ページは、[ok] です。</span><span class="sxs-lookup"><span data-stu-id="e994d-143">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="e994d-144">Web API、ただし、応答本文は通常、いずれかを空や JSON などの構造化データが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e994d-144">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="e994d-145">その場合は、ページは、応答を処理できるように、AJAX を使用してフォーム データが要求を送信する際になります。</span><span class="sxs-lookup"><span data-stu-id="e994d-145">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="e994d-146">次のコードでは、jQuery を使用してフォーム データを投稿する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="e994d-146">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="e994d-147">JQuery**送信**関数は、新しい関数にフォームのアクションを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e994d-147">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="e994d-148">これには、[送信] ボタンの既定の動作がオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="e994d-148">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="e994d-149">**シリアル化**関数は、名前/値ペアにフォーム データをシリアル化します。</span><span class="sxs-lookup"><span data-stu-id="e994d-149">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="e994d-150">サーバーにフォーム データを送信する呼び出し`$.post()`します。</span><span class="sxs-lookup"><span data-stu-id="e994d-150">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="e994d-151">要求が完了したら、`.success()`または`.error()`ハンドラーでは、ユーザーに適切なメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e994d-151">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="e994d-152">単純型を送信します。</span><span class="sxs-lookup"><span data-stu-id="e994d-152">Sending Simple Types</span></span>

<span data-ttu-id="e994d-153">前のセクションでは、複合型は、Web API は、モデル クラスのインスタンスに逆シリアル化を送信しました。</span><span class="sxs-lookup"><span data-stu-id="e994d-153">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="e994d-154">文字列などの単純型を送信することもできます。</span><span class="sxs-lookup"><span data-stu-id="e994d-154">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="e994d-155">単純型を送信する前に、代わりに、複合型で値をラッピング検討してください。</span><span class="sxs-lookup"><span data-stu-id="e994d-155">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="e994d-156">これはサーバー側では、モデルの検証のメリットを提供し、必要な場合に、モデルを拡張しやすきます。</span><span class="sxs-lookup"><span data-stu-id="e994d-156">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>

<span data-ttu-id="e994d-157">単純型を送信する基本的な手順は同じですが 2 つの微妙な違いがあります。</span><span class="sxs-lookup"><span data-stu-id="e994d-157">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="e994d-158">最初に、コント ローラーにする必要がありますを装飾するパラメーター名の**FromBody**属性。</span><span class="sxs-lookup"><span data-stu-id="e994d-158">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="e994d-159">既定では、Web API は、要求 URI からの単純型の取得を試みます。</span><span class="sxs-lookup"><span data-stu-id="e994d-159">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="e994d-160">**FromBody**属性値の読み取り、要求本文から Web API に指示します。</span><span class="sxs-lookup"><span data-stu-id="e994d-160">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="e994d-161">Web API を読み取り、応答本文、多くても 1 回のみ、アクションの 1 つのパラメーターは、要求本文から取得できます。</span><span class="sxs-lookup"><span data-stu-id="e994d-161">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="e994d-162">要求本文から複数の値を取得する必要がある場合は、複合型を定義します。</span><span class="sxs-lookup"><span data-stu-id="e994d-162">If you need to get multiple values from the request body, define a complex type.</span></span>

<span data-ttu-id="e994d-163">次に、クライアントは、次の形式で値を送信する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e994d-163">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="e994d-164">具体的には、名前/値ペアの名前の部分は単純型の空にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e994d-164">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="e994d-165">すべてのブラウザーが HTML フォームは、これをサポートしますが、次のようにスクリプトでこの形式を作成します。</span><span class="sxs-lookup"><span data-stu-id="e994d-165">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="e994d-166">フォームの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="e994d-166">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="e994d-167">フォームの値を送信するスクリプトを次に示します。</span><span class="sxs-lookup"><span data-stu-id="e994d-167">And here is the script to submit the form value.</span></span> <span data-ttu-id="e994d-168">前のスクリプトからの唯一の違いに渡される引数、**投稿**関数。</span><span class="sxs-lookup"><span data-stu-id="e994d-168">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="e994d-169">同じアプローチを使用して、単純型の配列を送信できます。</span><span class="sxs-lookup"><span data-stu-id="e994d-169">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="e994d-170">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="e994d-170">Additional Resources</span></span>

[<span data-ttu-id="e994d-171">第 2 部: ファイルのアップロードとマルチパート MIME</span><span class="sxs-lookup"><span data-stu-id="e994d-171">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
