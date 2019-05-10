---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: TagBuilder クラスを使用して、HTML ヘルパー (VB) をビルドする |Microsoft Docs
author: StephenWalther
description: Stephen Walther TagBuilder クラスという名前の ASP.NET MVC フレームワークで便利なユーティリティ クラスを紹介します。 TagBuilder クラスを簡単に使用できます.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b0aa9816209cc326d3dea4b8dfb1b13cf697fcd
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130360"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a><span data-ttu-id="a52da-104">TagBuilder クラスを使用して、HTML ヘルパー (VB) をビルドするには</span><span class="sxs-lookup"><span data-stu-id="a52da-104">Using the TagBuilder Class to Build HTML Helpers (VB)</span></span>

<span data-ttu-id="a52da-105">によって[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="a52da-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="a52da-106">Stephen Walther TagBuilder クラスという名前の ASP.NET MVC フレームワークで便利なユーティリティ クラスを紹介します。</span><span class="sxs-lookup"><span data-stu-id="a52da-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="a52da-107">TagBuilder クラスを使用すると、HTML タグを簡単に構築します。</span><span class="sxs-lookup"><span data-stu-id="a52da-107">You can use the TagBuilder class to easily build HTML tags.</span></span>

<span data-ttu-id="a52da-108">ASP.NET MVC フレームワークには、TagBuilder クラスで HTML ヘルパーを作成するときに使用できるという便利なユーティリティ クラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a52da-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="a52da-109">TagBuilder クラスでは、クラスの名前からわかるように、使用する HTML タグを簡単に構築できます。</span><span class="sxs-lookup"><span data-stu-id="a52da-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="a52da-110">この簡単なチュートリアルでは、TagBuilder クラスの概要が提供され、HTML を表示する単純な HTML ヘルパーをビルドするときに、このクラスを使用する方法を学習します&lt;img&gt;タグ。</span><span class="sxs-lookup"><span data-stu-id="a52da-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="a52da-111">TagBuilder クラスの概要</span><span class="sxs-lookup"><span data-stu-id="a52da-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="a52da-112">TagBuilder クラスは、System.Web.Mvc 名前空間に含まれます。</span><span class="sxs-lookup"><span data-stu-id="a52da-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="a52da-113">5 つのメソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="a52da-113">It has five methods:</span></span>

- <span data-ttu-id="a52da-114">AddCssClass() – を使用すると、新しい追加*クラス =""* タグに属性します。</span><span class="sxs-lookup"><span data-stu-id="a52da-114">AddCssClass() – Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="a52da-115">GenerateId() – では、id 属性、タグを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="a52da-115">GenerateId() – Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="a52da-116">このメソッドは id の期間を自動的に置き換えられます (既定では、ピリオド、アンダー スコアに置換)</span><span class="sxs-lookup"><span data-stu-id="a52da-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="a52da-117">MergeAttribute() – では、タグに属性を追加することができます。</span><span class="sxs-lookup"><span data-stu-id="a52da-117">MergeAttribute() – Enables you to add attributes to a tag.</span></span> <span data-ttu-id="a52da-118">このメソッドの複数のオーバー ロードがあります。</span><span class="sxs-lookup"><span data-stu-id="a52da-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="a52da-119">SetInnerText() – では、タグの内部テキ ストを設定することができます。</span><span class="sxs-lookup"><span data-stu-id="a52da-119">SetInnerText() – Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="a52da-120">内部テキ ストは、HTML が自動的にエンコードします。</span><span class="sxs-lookup"><span data-stu-id="a52da-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="a52da-121">ToString() – では、タグをレンダリングすることができます。</span><span class="sxs-lookup"><span data-stu-id="a52da-121">ToString() – Enables you to render the tag.</span></span> <span data-ttu-id="a52da-122">通常のタグ、開始タグ、終了タグ、または自己終了タグを作成するかどうかを指定することができます。</span><span class="sxs-lookup"><span data-stu-id="a52da-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>

<span data-ttu-id="a52da-123">TagBuilder クラスでは、次の 4 つの重要なプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="a52da-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="a52da-124">属性: すべてのタグの属性を表します。</span><span class="sxs-lookup"><span data-stu-id="a52da-124">Attributes – Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="a52da-125">IdAttributeDotReplacement – は、期間 (既定ではアンダー スコア) を置換する GenerateId() メソッドによって使用される文字を表します。</span><span class="sxs-lookup"><span data-stu-id="a52da-125">IdAttributeDotReplacement – Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="a52da-126">InnerHTML – は、タグの内部の内容を表します。</span><span class="sxs-lookup"><span data-stu-id="a52da-126">InnerHTML – Represents the inner contents of the tag.</span></span> <span data-ttu-id="a52da-127">このプロパティに文字列を割り当てる*しない*HTML 文字列をエンコードします。</span><span class="sxs-lookup"><span data-stu-id="a52da-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="a52da-128">TagName – は、タグの名前を表します。</span><span class="sxs-lookup"><span data-stu-id="a52da-128">TagName – Represents the name of the tag.</span></span>

<span data-ttu-id="a52da-129">これらのメソッドとプロパティをすべて提供基本メソッドとプロパティを HTML タグを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a52da-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="a52da-130">本当に TagBuilder クラスを使用する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="a52da-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="a52da-131">StringBuilder クラスは、代わりに使用する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a52da-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="a52da-132">ただし、TagBuilder クラスで、容易に少し。</span><span class="sxs-lookup"><span data-stu-id="a52da-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="a52da-133">イメージの HTML ヘルパーの作成</span><span class="sxs-lookup"><span data-stu-id="a52da-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="a52da-134">TagBuilder クラスのインスタンスを作成するときは、TagBuilder コンス トラクターにビルドするタグの名前を渡します。</span><span class="sxs-lookup"><span data-stu-id="a52da-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="a52da-135">次に、タグの属性を変更する AddCssClass と MergeAttribute() メソッドと同様のメソッドを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="a52da-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="a52da-136">最後に、タグを表示するために、ToString() メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="a52da-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="a52da-137">たとえば、リスト 1 には、イメージの HTML ヘルパーが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a52da-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="a52da-138">イメージ ヘルパーは HTML を表す TagBuilder で内部的に実装&lt;img&gt;タグ。</span><span class="sxs-lookup"><span data-stu-id="a52da-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="a52da-139">**1 – Helpers\ImageHelper.vb を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="a52da-139">**Listing 1 – Helpers\ImageHelper.vb**</span></span>

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

<span data-ttu-id="a52da-140">リスト 1 でモジュールには、Image() という名前の 2 つのオーバー ロードされたメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="a52da-140">The module in Listing 1 contains two overloaded methods named Image().</span></span> <span data-ttu-id="a52da-141">Image() メソッドを呼び出すときにをかどうかは、一連の HTML 属性を表すオブジェクトを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="a52da-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="a52da-142">TagBuilder.MergeAttribute() メソッドを使用して、TagBuilder に src 属性などの個々 の属性を追加する方法に注意してください。</span><span class="sxs-lookup"><span data-stu-id="a52da-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="a52da-143">確認、さらに、TagBuilder.MergeAttributes() メソッドを使用して、TagBuilder に属性のコレクションを追加する方法。</span><span class="sxs-lookup"><span data-stu-id="a52da-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="a52da-144">MergeAttributes() メソッドは、辞書を受け取ります&lt;object&gt;パラメーター。</span><span class="sxs-lookup"><span data-stu-id="a52da-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="a52da-145">ディクショナリに属性のコレクションを表すオブジェクトを変換する RouteValueDictionary クラスが使用される&lt;object&gt;します。</span><span class="sxs-lookup"><span data-stu-id="a52da-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="a52da-146">イメージ ヘルパーを作成した後は、その他の標準の HTML ヘルパーのいずれかのように、ASP.NET MVC ビューで、ヘルパーを使用できます。</span><span class="sxs-lookup"><span data-stu-id="a52da-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="a52da-147">リスト 2 での表示では、イメージ ヘルパーを使用して、2 回、Xbox の同じイメージを表示 (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="a52da-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="a52da-148">HTML 属性のコレクションの有無にかかわらず、Image() ヘルパーが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="a52da-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="a52da-149">**Listing 2 – Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="a52da-149">**Listing 2 – Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]

<span data-ttu-id="a52da-150">[![[新しいプロジェクト] ダイアログ ボックス](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a52da-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="a52da-151">**図 01**:イメージ ヘルパーを使用して ([フルサイズの画像を表示する をクリックします](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))。</span><span class="sxs-lookup"><span data-stu-id="a52da-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span></span>

<span data-ttu-id="a52da-152">Index.aspx ビューの上部にあるイメージ ヘルパーに関連付けられている名前空間をインポートする必要がありますに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a52da-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="a52da-153">次のディレクティブを使用して、ヘルパーがインポートされます。</span><span class="sxs-lookup"><span data-stu-id="a52da-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

<span data-ttu-id="a52da-154">Visual Basic アプリケーションで、既定の名前空間は、アプリケーションの名前の場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="a52da-154">In a Visual Basic application, the default namespace is the same as the name of the application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a52da-155">[前へ](creating-custom-html-helpers-vb.md)
> [次へ](creating-page-layouts-with-view-master-pages-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a52da-155">[Previous](creating-custom-html-helpers-vb.md)
[Next](creating-page-layouts-with-view-master-pages-vb.md)</span></span>
