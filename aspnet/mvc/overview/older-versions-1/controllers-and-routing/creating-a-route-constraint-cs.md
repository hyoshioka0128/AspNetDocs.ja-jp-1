---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: ルート制約を作成 (c#) |Microsoft Docs
author: StephenWalther
description: このチュートリアルでは、Stephen Walther は、正規表現のルート制約を作成して、ブラウザーが一致するルートを要求する方法を制御する方法について説明します。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 51ef859287b3424faf85f4a3606a220ab48a9466
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123434"
---
# <a name="creating-a-route-constraint-c"></a><span data-ttu-id="95740-103">ルート制約を作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="95740-103">Creating a Route Constraint (C#)</span></span>

<span data-ttu-id="95740-104">によって[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="95740-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="95740-105">このチュートリアルでは、Stephen Walther は、正規表現のルート制約を作成して、ブラウザーが一致するルートを要求する方法を制御する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="95740-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>

<span data-ttu-id="95740-106">ルート制約を使用すると、特定のルートに一致するブラウザーの要求を制限できます。</span><span class="sxs-lookup"><span data-stu-id="95740-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="95740-107">正規表現を使用して、ルート制約を指定することができます。</span><span class="sxs-lookup"><span data-stu-id="95740-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="95740-108">たとえば、ルート、Global.asax ファイルでリスト 1 で定義したとします。</span><span class="sxs-lookup"><span data-stu-id="95740-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="95740-109">**1 - Global.asax.cs の一覧を表示します。**</span><span class="sxs-lookup"><span data-stu-id="95740-109">**Listing 1 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="95740-110">1 を一覧表示するには、製品をという名前のルートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="95740-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="95740-111">製品のルートを使用して、リスト 2 に含まれる「productcontroller」ブラウザー要求をマップすることができます。</span><span class="sxs-lookup"><span data-stu-id="95740-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="95740-112">**Listing 2 - Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="95740-112">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="95740-113">製品のコント ローラーによって公開される Details() アクションが productId という 1 つのパラメーターを受け入れることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="95740-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="95740-114">このパラメーターは、整数パラメーターです。</span><span class="sxs-lookup"><span data-stu-id="95740-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="95740-115">リスト 1 で定義されているルートは、次の Url のいずれかに一致します。</span><span class="sxs-lookup"><span data-stu-id="95740-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="95740-116">/製品/23</span><span class="sxs-lookup"><span data-stu-id="95740-116">/Product/23</span></span>
- <span data-ttu-id="95740-117">/製品/7</span><span class="sxs-lookup"><span data-stu-id="95740-117">/Product/7</span></span>

<span data-ttu-id="95740-118">残念ながら、ルートには、次の Url は一致も。</span><span class="sxs-lookup"><span data-stu-id="95740-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="95740-119">/製品/とおりです。</span><span class="sxs-lookup"><span data-stu-id="95740-119">/Product/blah</span></span>
- <span data-ttu-id="95740-120">/製品/apple</span><span class="sxs-lookup"><span data-stu-id="95740-120">/Product/apple</span></span>

<span data-ttu-id="95740-121">Details() アクションには、整数パラメーターが必要ですが、ため、整数値以外のものを含む要求を行うと、エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="95740-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="95740-122">たとえば、URL/Product/apple をお使いのブラウザーに入力した場合は、図 1 エラー ページを表示がされます。</span><span class="sxs-lookup"><span data-stu-id="95740-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>

<span data-ttu-id="95740-123">[![[新しいプロジェクト] ダイアログ ボックス](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="95740-123">[![The New Project dialog box](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span></span>

<span data-ttu-id="95740-124">**図 01**:展開のページが表示 ([フルサイズの画像を表示する をクリックします](creating-a-route-constraint-cs/_static/image2.png))。</span><span class="sxs-lookup"><span data-stu-id="95740-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-cs/_static/image2.png))</span></span>

<span data-ttu-id="95740-125">本当にする内容は、のみ一致する適切な整数 productId を含む Url です。</span><span class="sxs-lookup"><span data-stu-id="95740-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="95740-126">ルートに一致する Url を制限するのにルートを定義するときに制約を使用できます。</span><span class="sxs-lookup"><span data-stu-id="95740-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="95740-127">リスト 3 で修正された製品のルートには、整数にのみ一致する正規表現の制約が含まれています。</span><span class="sxs-lookup"><span data-stu-id="95740-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="95740-128">**3 - Global.asax.cs の一覧を表示します。**</span><span class="sxs-lookup"><span data-stu-id="95740-128">**Listing 3 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="95740-129">正規表現 \d+ では、1 つまたは複数の整数と一致します。</span><span class="sxs-lookup"><span data-stu-id="95740-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="95740-130">この制約により、次の Url と一致する製品ルート。</span><span class="sxs-lookup"><span data-stu-id="95740-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="95740-131">/製品/3</span><span class="sxs-lookup"><span data-stu-id="95740-131">/Product/3</span></span>
- <span data-ttu-id="95740-132">/製品/8999</span><span class="sxs-lookup"><span data-stu-id="95740-132">/Product/8999</span></span>

<span data-ttu-id="95740-133">次の Url ではないです。</span><span class="sxs-lookup"><span data-stu-id="95740-133">But not the following URLs:</span></span>

- <span data-ttu-id="95740-134">/製品/apple</span><span class="sxs-lookup"><span data-stu-id="95740-134">/Product/apple</span></span>
- <span data-ttu-id="95740-135">/製品</span><span class="sxs-lookup"><span data-stu-id="95740-135">/Product</span></span>

- <span data-ttu-id="95740-136">別のルートでこれらのブラウザー要求を処理します。 または、一致のルートがない場合、*リソースが見つかりませんでした*エラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="95740-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="95740-137">[前へ](creating-custom-routes-cs.md)
> [次へ](creating-a-custom-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="95740-137">[Previous](creating-custom-routes-cs.md)
[Next](creating-a-custom-route-constraint-cs.md)</span></span>
