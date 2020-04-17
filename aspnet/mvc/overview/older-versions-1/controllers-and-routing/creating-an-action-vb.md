---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: アクション (VB) を作成する |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NET MVC コントローラーに新しいアクションを追加する方法について説明します。 メソッドをアクションにするための要件について説明します。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: dd651155bdb931cb8358d369b3c0c2c98abb86b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542249"
---
# <a name="creating-an-action-vb"></a><span data-ttu-id="d618d-104">アクションを作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="d618d-104">Creating an Action (VB)</span></span>

<span data-ttu-id="d618d-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d618d-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d618d-106">ASP.NET MVC コントローラーに新しいアクションを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d618d-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="d618d-107">メソッドをアクションにするための要件について説明します。</span><span class="sxs-lookup"><span data-stu-id="d618d-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="d618d-108">このチュートリアルの目的は、新しいコントローラー アクションを作成する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="d618d-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="d618d-109">アクション メソッドの要件について学習します。</span><span class="sxs-lookup"><span data-stu-id="d618d-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="d618d-110">また、メソッドがアクションとして公開されないようにする方法についても学習します。</span><span class="sxs-lookup"><span data-stu-id="d618d-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="d618d-111">コントローラへのアクションの追加</span><span class="sxs-lookup"><span data-stu-id="d618d-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="d618d-112">新しいアクションをコントローラーに追加するには、新しいメソッドをコントローラーに追加します。</span><span class="sxs-lookup"><span data-stu-id="d618d-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="d618d-113">たとえば、リスト 1 のコントローラには、Index() という名前のアクションと、SayHello() という名前のアクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d618d-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="d618d-114">どちらのメソッドもアクションとして公開されます。</span><span class="sxs-lookup"><span data-stu-id="d618d-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="d618d-115">**リスト 1 - コントローラー\ホームコントローラー.vb**</span><span class="sxs-lookup"><span data-stu-id="d618d-115">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

<span data-ttu-id="d618d-116">アクションとして宇宙に公開されるためには、メソッドは特定の要件を満たす必要があります。</span><span class="sxs-lookup"><span data-stu-id="d618d-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="d618d-117">メソッドはパブリックである必要があります。</span><span class="sxs-lookup"><span data-stu-id="d618d-117">The method must be public.</span></span>
- <span data-ttu-id="d618d-118">メソッドを静的メソッドにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="d618d-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="d618d-119">メソッドを拡張メソッドにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="d618d-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="d618d-120">メソッドをコンストラクター、取得、またはセッターにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="d618d-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="d618d-121">メソッドにオープン ジェネリック型を指定することはできません。</span><span class="sxs-lookup"><span data-stu-id="d618d-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="d618d-122">メソッドは、コントローラーの基本クラスのメソッドではありません。</span><span class="sxs-lookup"><span data-stu-id="d618d-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="d618d-123">メソッドに**ref**パラメーターまたは out パラメーター**を**含めることはできません。</span><span class="sxs-lookup"><span data-stu-id="d618d-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="d618d-124">コントローラ アクションの戻り値の型に制限はありません。</span><span class="sxs-lookup"><span data-stu-id="d618d-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="d618d-125">コントローラーアクションは、文字列、DateTime、Random クラスのインスタンス、または void を返すことができます。</span><span class="sxs-lookup"><span data-stu-id="d618d-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="d618d-126">ASP.NET MVC フレームワークは、アクションの結果ではない戻り値の型を文字列に変換し、ブラウザーに文字列をレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="d618d-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="d618d-127">これらの要件に違反しないメソッドをコントローラに追加すると、そのメソッドはコントローラ アクションとして公開されます。</span><span class="sxs-lookup"><span data-stu-id="d618d-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="d618d-128">ここで注意してください。</span><span class="sxs-lookup"><span data-stu-id="d618d-128">Be careful here.</span></span> <span data-ttu-id="d618d-129">コントローラアクションは、インターネットに接続しているすべてのユーザーが呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="d618d-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="d618d-130">たとえば、DeleteMyWebsite() コントローラ アクションを作成しないでください。</span><span class="sxs-lookup"><span data-stu-id="d618d-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="d618d-131">パブリック メソッドが呼び出されないようにする</span><span class="sxs-lookup"><span data-stu-id="d618d-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="d618d-132">コントローラ クラスでパブリック メソッドを作成する必要があり、そのメソッドをコントローラ アクションとして公開しない場合は&lt;、NonAction&gt;属性を使用してメソッドが呼び出されないようにできます。</span><span class="sxs-lookup"><span data-stu-id="d618d-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the &lt;NonAction&gt; attribute.</span></span> <span data-ttu-id="d618d-133">たとえば、リスト 2 のコントローラには、NonAction&lt;&gt;属性で修飾された CompanySecrets() という名前のパブリック メソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d618d-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the &lt;NonAction&gt; attribute.</span></span>

<span data-ttu-id="d618d-134">**リスト 2 - コントローラー\ワークコントローラー.vb**</span><span class="sxs-lookup"><span data-stu-id="d618d-134">**Listing 2 - Controllers\WorkController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

<span data-ttu-id="d618d-135">ブラウザーのアドレス バーに /Work/CompanySecrets と入力して CompanySecrets() コントローラー アクションを呼び出そうとすると、図 1 のエラー メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d618d-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="d618d-136">[![非アクション メソッドの呼び出し](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d618d-136">[![Invoking a NonAction method](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span></span>

<span data-ttu-id="d618d-137">**図 01**: NonAction メソッドの呼び出し ([フルサイズの画像を表示する をクリック](creating-an-action-vb/_static/image2.png)して)</span><span class="sxs-lookup"><span data-stu-id="d618d-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-vb/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d618d-138">[前へ](creating-a-controller-vb.md)
> [次へ](aspnet-mvc-controllers-overview-cs.md)</span><span class="sxs-lookup"><span data-stu-id="d618d-138">[Previous](creating-a-controller-vb.md)
[Next](aspnet-mvc-controllers-overview-cs.md)</span></span>
