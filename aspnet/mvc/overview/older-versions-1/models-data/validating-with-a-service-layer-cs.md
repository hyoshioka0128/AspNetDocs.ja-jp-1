---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
title: サービス層 (c#) の検証 |Microsoft Docs
author: StephenWalther
description: コント ローラー アクションから、別のサービス層には、検証ロジックを移動する方法について説明します。 このチュートリアルでは、Stephen Walther がについて説明する方法をしています.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4eabc535-b8a1-43f5-bb99-cfeb86db0fca
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: da1a1c9cc79a452eb0d7597810e86f7bcf6cd179
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65122336"
---
# <a name="validating-with-a-service-layer-c"></a><span data-ttu-id="8d2a6-104">サービス層の検証 (C#)</span><span class="sxs-lookup"><span data-stu-id="8d2a6-104">Validating with a Service Layer (C#)</span></span>

<span data-ttu-id="8d2a6-105">によって[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="8d2a6-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="8d2a6-106">コント ローラー アクションから、別のサービス層には、検証ロジックを移動する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-106">Learn how to move your validation logic out of your controller actions and into a separate service layer.</span></span> <span data-ttu-id="8d2a6-107">このチュートリアルでは、Stephen Walther は、コント ローラー層から、サービス層を分離することで、懸念事項のシャープな分離を維持する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-107">In this tutorial, Stephen Walther explains how you can maintain a sharp separation of concerns by isolating your service layer from your controller layer.</span></span>

<span data-ttu-id="8d2a6-108">このチュートリアルの目的では、ASP.NET MVC アプリケーションで検証を実行する 1 つの方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-108">The goal of this tutorial is to describe one method of performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="8d2a6-109">このチュートリアルでは、コント ローラーから、別のサービス層には、検証ロジックを移動する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-109">In this tutorial, you learn how to move your validation logic out of your controllers and into a separate service layer.</span></span>

## <a name="separating-concerns"></a><span data-ttu-id="8d2a6-110">懸念事項の分離</span><span class="sxs-lookup"><span data-stu-id="8d2a6-110">Separating Concerns</span></span>

<span data-ttu-id="8d2a6-111">ASP.NET MVC アプリケーションをビルドすると、コント ローラー アクションの内部データベース ロジックを置かないでください。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-111">When you build an ASP.NET MVC application, you should not place your database logic inside your controller actions.</span></span> <span data-ttu-id="8d2a6-112">データベースとコント ローラー ロジックの混合によってアプリケーションの時間の経過と共に管理が困難です。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-112">Mixing your database and controller logic makes your application more difficult to maintain over time.</span></span> <span data-ttu-id="8d2a6-113">すべてのデータベース ロジックを別のリポジトリ層に配置することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-113">The recommendation is that you place all of your database logic in a separate repository layer.</span></span>

<span data-ttu-id="8d2a6-114">たとえば、リスト 1 には、ProductRepository をという名前の単純なリポジトリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-114">For example, Listing 1 contains a simple repository named the ProductRepository.</span></span> <span data-ttu-id="8d2a6-115">製品のリポジトリには、すべてのアプリケーションのデータ アクセス コードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-115">The product repository contains all of the data access code for the application.</span></span> <span data-ttu-id="8d2a6-116">一覧には、製品のリポジトリを実装する IProductRepository インターフェイスも含まれています。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-116">The listing also includes the IProductRepository interface that the product repository implements.</span></span>

<span data-ttu-id="8d2a6-117">**Listing 1 -- Models\ProductRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="8d2a6-117">**Listing 1 -- Models\ProductRepository.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample1.cs)]

<span data-ttu-id="8d2a6-118">リスト 2 でコント ローラーは、その Index() と Create() の両方のアクションのリポジトリ層を使用します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-118">The controller in Listing 2 uses the repository layer in both its Index() and Create() actions.</span></span> <span data-ttu-id="8d2a6-119">このコント ローラーに任意のデータベース ロジックが含まれていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-119">Notice that this controller does not contain any database logic.</span></span> <span data-ttu-id="8d2a6-120">リポジトリ層を作成するには、懸念事項の明確な分離を維持することができます。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-120">Creating a repository layer enables you to maintain a clean separation of concerns.</span></span> <span data-ttu-id="8d2a6-121">コント ローラーは、アプリケーションのフロー制御ロジックとリポジトリがデータ アクセス ロジックを担当します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-121">Controllers are responsible for application flow control logic and the repository is responsible for data access logic.</span></span>

<span data-ttu-id="8d2a6-122">**Listing 2 - Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="8d2a6-122">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample2.cs)]

## <a name="creating-a-service-layer"></a><span data-ttu-id="8d2a6-123">サービス層の作成</span><span class="sxs-lookup"><span data-stu-id="8d2a6-123">Creating a Service Layer</span></span>

<span data-ttu-id="8d2a6-124">そのため、アプリケーションのフロー制御ロジックはコント ローラーが属しているし、データ アクセス ロジックをリポジトリに属しています。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-124">So, application flow control logic belongs in a controller and data access logic belongs in a repository.</span></span> <span data-ttu-id="8d2a6-125">その場合は、コピー先の場所は、検証ロジックでしょうか。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-125">In that case, where do you put your validation logic?</span></span> <span data-ttu-id="8d2a6-126">1 つのオプションは、検証ロジックを配置する、*サービス層*します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-126">One option is to place your validation logic in a *service layer*.</span></span>

<span data-ttu-id="8d2a6-127">サービス層は、コント ローラーおよびリポジトリ層間の通信を仲介する ASP.NET MVC アプリケーションで追加のレイヤーです。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-127">A service layer is an additional layer in an ASP.NET MVC application that mediates communication between a controller and repository layer.</span></span> <span data-ttu-id="8d2a6-128">サービス層には、ビジネス ロジックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-128">The service layer contains business logic.</span></span> <span data-ttu-id="8d2a6-129">具体的には、検証ロジックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-129">In particular, it contains validation logic.</span></span>

<span data-ttu-id="8d2a6-130">たとえば、リスト 3 の製品のサービス層では、CreateProduct() メソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-130">For example, the product service layer in Listing 3 has a CreateProduct() method.</span></span> <span data-ttu-id="8d2a6-131">CreateProduct() メソッドは、製品を製品リポジトリに渡す前に、新しい製品を検証する ValidateProduct() メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-131">The CreateProduct() method calls the ValidateProduct() method to validate a new product before passing the product to the product repository.</span></span>

<span data-ttu-id="8d2a6-132">**3 - Models\ProductService.cs を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="8d2a6-132">**Listing 3 - Models\ProductService.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample3.cs)]

<span data-ttu-id="8d2a6-133">製品のコント ローラーはリポジトリ層ではなく、サービス層を使用するリスト 4 に更新されました。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-133">The Product controller has been updated in Listing 4 to use the service layer instead of the repository layer.</span></span> <span data-ttu-id="8d2a6-134">コント ローラーのレイヤーは、サービス層を説明します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-134">The controller layer talks to the service layer.</span></span> <span data-ttu-id="8d2a6-135">サービス層がリポジトリ層に説明します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-135">The service layer talks to the repository layer.</span></span> <span data-ttu-id="8d2a6-136">各レイヤーでは、個別の責任を持ちます。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-136">Each layer has a separate responsibility.</span></span>

<span data-ttu-id="8d2a6-137">**Listing 4 - Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="8d2a6-137">**Listing 4 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample4.cs)]

<span data-ttu-id="8d2a6-138">製品のコント ローラー コンス トラクターで、製品のサービスが作成されたことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-138">Notice that the product service is created in the product controller constructor.</span></span> <span data-ttu-id="8d2a6-139">製品サービスの作成時に、モデル状態ディクショナリがサービスに渡されます。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-139">When the product service is created, the model state dictionary is passed to the service.</span></span> <span data-ttu-id="8d2a6-140">製品のサービスでは、モデルの状態を使用して、コント ローラーに検証エラー メッセージを渡します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-140">The product service uses model state to pass validation error messages back to the controller.</span></span>

## <a name="decoupling-the-service-layer"></a><span data-ttu-id="8d2a6-141">サービス層を分離</span><span class="sxs-lookup"><span data-stu-id="8d2a6-141">Decoupling the Service Layer</span></span>

<span data-ttu-id="8d2a6-142">コント ローラーと 1 つの点では、サービス層を分離することができませんでした。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-142">We have failed to isolate the controller and service layers in one respect.</span></span> <span data-ttu-id="8d2a6-143">コント ローラーとサービス レイヤーは、モデルの状態を通信します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-143">The controller and service layers communicate through model state.</span></span> <span data-ttu-id="8d2a6-144">つまり、サービス層、ASP.NET MVC framework の特定の機能に依存しています。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-144">In other words, the service layer has a dependency on a particular feature of the ASP.NET MVC framework.</span></span>

<span data-ttu-id="8d2a6-145">可能な限り、コント ローラー レイヤーからサービス層を分離します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-145">We want to isolate the service layer from our controller layer as much as possible.</span></span> <span data-ttu-id="8d2a6-146">理論上は、任意の種類のアプリケーションと ASP.NET MVC アプリケーションだけでなく、サービス層を使用することができなければなりません。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-146">In theory, we should be able to use the service layer with any type of application and not only an ASP.NET MVC application.</span></span> <span data-ttu-id="8d2a6-147">たとえば、今後、する可能性が、WPF アプリケーションのフロント エンドを構築します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-147">For example, in the future, we might want to build a WPF front-end for our application.</span></span> <span data-ttu-id="8d2a6-148">ASP.NET MVC 依存関係を削除する方法モデルの状態は、サービス層から見つかったする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-148">We should find a way to remove the dependency on ASP.NET MVC model state from our service layer.</span></span>

<span data-ttu-id="8d2a6-149">リスト 5 では、サービス層を不要になったモデルの状態を使用するように更新されましたが。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-149">In Listing 5, the service layer has been updated so that it no longer uses model state.</span></span> <span data-ttu-id="8d2a6-150">代わりに、IValidationDictionary インターフェイスを実装する任意のクラスを使用します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-150">Instead, it uses any class that implements the IValidationDictionary interface.</span></span>

<span data-ttu-id="8d2a6-151">**5 - Models\ProductService.cs (分離) を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="8d2a6-151">**Listing 5 - Models\ProductService.cs (decoupled)**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample5.cs)]

<span data-ttu-id="8d2a6-152">IValidationDictionary インターフェイスは、リスト 6 で定義されます。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-152">The IValidationDictionary interface is defined in Listing 6.</span></span> <span data-ttu-id="8d2a6-153">このシンプルなインターフェイスは、1 つのメソッドと 1 つのプロパティを持ちます。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-153">This simple interface has a single method and a single property.</span></span>

<span data-ttu-id="8d2a6-154">**6 - Models\IValidationDictionary.cs を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="8d2a6-154">**Listing 6 - Models\IValidationDictionary.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample6.cs)]

<span data-ttu-id="8d2a6-155">リスト 7、ModelStateWrapper クラスという名前でクラスでは、IValidationDictionary インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-155">The class in Listing 7, named the ModelStateWrapper class, implements the IValidationDictionary interface.</span></span> <span data-ttu-id="8d2a6-156">モデル状態ディクショナリをコンス トラクターに渡すことによって、ModelStateWrapper クラスをインスタンス化できます。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-156">You can instantiate the ModelStateWrapper class by passing a model state dictionary to the constructor.</span></span>

<span data-ttu-id="8d2a6-157">**7 - Models\ModelStateWrapper.cs を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="8d2a6-157">**Listing 7 - Models\ModelStateWrapper.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample7.cs)]

<span data-ttu-id="8d2a6-158">最後に、一覧の 8 に更新されたコント ローラーは、そのコンス トラクターで、サービス層を作成するときに、ModelStateWrapper を使用します。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-158">Finally, the updated controller in Listing 8 uses the ModelStateWrapper when creating the service layer in its constructor.</span></span>

<span data-ttu-id="8d2a6-159">**Listing 8 - Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="8d2a6-159">**Listing 8 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample8.cs)]

<span data-ttu-id="8d2a6-160">IValidationDictionary を使用してインターフェイスと ModelStateWrapper クラスにより、コント ローラーの層から、サービス層を完全に分離できます。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-160">Using the IValidationDictionary interface and the ModelStateWrapper class enables us to completely isolate our service layer from our controller layer.</span></span> <span data-ttu-id="8d2a6-161">サービス層がモデル状態に依存するではなくなりました。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-161">The service layer is no longer dependent on model state.</span></span> <span data-ttu-id="8d2a6-162">サービス層に IValidationDictionary インターフェイスを実装する任意のクラスを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-162">You can pass any class that implements the IValidationDictionary interface to the service layer.</span></span> <span data-ttu-id="8d2a6-163">たとえば、WPF アプリケーションは、単純なコレクション クラスを使用して IValidationDictionary インターフェイスを実装する場合があります。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-163">For example, a WPF application might implement the IValidationDictionary interface with a simple collection class.</span></span>

## <a name="summary"></a><span data-ttu-id="8d2a6-164">まとめ</span><span class="sxs-lookup"><span data-stu-id="8d2a6-164">Summary</span></span>

<span data-ttu-id="8d2a6-165">このチュートリアルの目的は、ASP.NET MVC アプリケーションで検証を実行するための 1 つのアプローチについて説明することでした。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-165">The goal of this tutorial was to discuss one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="8d2a6-166">このチュートリアルでは、すべてのコント ローラーから、別のサービス層に、検証ロジックを移動する方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-166">In this tutorial, you learned how to move all of your validation logic out of your controllers and into a separate service layer.</span></span> <span data-ttu-id="8d2a6-167">ModelStateWrapper クラスを作成して、コント ローラーの層から、サービス層を分離する方法も学習しました。</span><span class="sxs-lookup"><span data-stu-id="8d2a6-167">You also learned how to isolate your service layer from your controller layer by creating a ModelStateWrapper class.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8d2a6-168">[前へ](validating-with-the-idataerrorinfo-interface-cs.md)
> [次へ](validation-with-the-data-annotation-validators-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8d2a6-168">[Previous](validating-with-the-idataerrorinfo-interface-cs.md)
[Next](validation-with-the-data-annotation-validators-cs.md)</span></span>
