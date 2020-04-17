---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: カスタム ルート (VB) を作成する |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NET MVC アプリケーションにカスタム ルートを追加する方法について説明します。 このチュートリアルでは、Global.asax ファイルの既定のルート テーブルを変更する方法について説明します。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: fd12307f685fa064832bb4198df06df2c3f2d3be
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542743"
---
# <a name="creating-custom-routes-vb"></a><span data-ttu-id="16bd2-104">カスタム ルートを作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="16bd2-104">Creating Custom Routes (VB)</span></span>

<span data-ttu-id="16bd2-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="16bd2-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="16bd2-106">ASP.NET MVC アプリケーションにカスタム ルートを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="16bd2-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="16bd2-107">このチュートリアルでは、Global.asax ファイルの既定のルート テーブルを変更する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="16bd2-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="16bd2-108">このチュートリアルでは、ASP.NET MVC アプリケーションにカスタム ルートを追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="16bd2-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="16bd2-109">Global.asax ファイルの既定のルート テーブルをカスタム ルートで変更する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="16bd2-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="16bd2-110">mvc アプリケーションASP.NET、既定のルート テーブルは正常に動作します。</span><span class="sxs-lookup"><span data-stu-id="16bd2-110">In ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="16bd2-111">ただし、特殊なルーティングニーズがある場合もあります。</span><span class="sxs-lookup"><span data-stu-id="16bd2-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="16bd2-112">その場合は、カスタム ルートを作成できます。</span><span class="sxs-lookup"><span data-stu-id="16bd2-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="16bd2-113">たとえば、ブログ アプリケーションを作成しているとします。</span><span class="sxs-lookup"><span data-stu-id="16bd2-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="16bd2-114">次のような着信要求を処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="16bd2-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="16bd2-115">/アーカイブ/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="16bd2-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="16bd2-116">ユーザーがこの要求を入力すると、2009/12/25 に対応するブログエントリを返します。</span><span class="sxs-lookup"><span data-stu-id="16bd2-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="16bd2-117">このタイプの要求を処理するには、カスタム ルートを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="16bd2-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="16bd2-118">リスト 1 の Global.asax ファイルには、/Archive/*エントリ日付*のような要求を処理する Blog という名前の新しいカスタム ルートが含まれています。</span><span class="sxs-lookup"><span data-stu-id="16bd2-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="16bd2-119">**リスト 1 - グローバル.asax (カスタム ルートを使用)**</span><span class="sxs-lookup"><span data-stu-id="16bd2-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

<span data-ttu-id="16bd2-120">ルート テーブルに追加するルートの順序は重要です。</span><span class="sxs-lookup"><span data-stu-id="16bd2-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="16bd2-121">新しいカスタムのブログルートは、既存のデフォルトルートの前に追加されます。</span><span class="sxs-lookup"><span data-stu-id="16bd2-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="16bd2-122">順序を逆にした場合、既定のルートは、カスタム ルートの代わりに常に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="16bd2-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="16bd2-123">カスタムのブログルートは、/Archive/ で始まるすべてのリクエストと一致します。</span><span class="sxs-lookup"><span data-stu-id="16bd2-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="16bd2-124">したがって、次のすべての URL と一致します。</span><span class="sxs-lookup"><span data-stu-id="16bd2-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="16bd2-125">/アーカイブ/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="16bd2-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="16bd2-126">/アーカイブ/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="16bd2-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="16bd2-127">/アーカイブ/リンゴ</span><span class="sxs-lookup"><span data-stu-id="16bd2-127">/Archive/apple</span></span>

<span data-ttu-id="16bd2-128">カスタム ルートは、受信した要求を Archive という名前のコントローラにマップし、Entry() アクションを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="16bd2-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="16bd2-129">Entry() メソッドが呼び出されると、エントリの日付は entryDate という名前のパラメーターとして渡されます。</span><span class="sxs-lookup"><span data-stu-id="16bd2-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="16bd2-130">リスト 2 のコントローラーでブログカスタム ルートを使用できます。</span><span class="sxs-lookup"><span data-stu-id="16bd2-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="16bd2-131">**リスト 2 - アーカイブコントローラー.vb**</span><span class="sxs-lookup"><span data-stu-id="16bd2-131">**Listing 2 - ArchiveController.vb**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

<span data-ttu-id="16bd2-132">リスト 2 の Entry() メソッドは、DateTime 型のパラメーターを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="16bd2-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="16bd2-133">MVC フレームワークは、入力日付を URL から DateTime 値に自動的に変換するのに十分なスマートさです。</span><span class="sxs-lookup"><span data-stu-id="16bd2-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="16bd2-134">URL からの入力日付パラメータを DateTime に変換できない場合は、エラーが発生します (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="16bd2-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="16bd2-135">**図1 - パラメータ変換によるエラー**</span><span class="sxs-lookup"><span data-stu-id="16bd2-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="16bd2-136">[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="16bd2-136">[![The New Project dialog box](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span></span>

<span data-ttu-id="16bd2-137">**図 01**: 変換パラメータからのエラー ([フルサイズの画像を表示する をクリックします](creating-custom-routes-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="16bd2-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-vb/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="16bd2-138">まとめ</span><span class="sxs-lookup"><span data-stu-id="16bd2-138">Summary</span></span>

<span data-ttu-id="16bd2-139">このチュートリアルの目的は、カスタム ルートを作成する方法を示すものでした。</span><span class="sxs-lookup"><span data-stu-id="16bd2-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="16bd2-140">ブログエントリを表す Global.asax ファイルのルート テーブルにカスタム ルートを追加する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="16bd2-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="16bd2-141">ブログ エントリの要求を ArchiveController という名前のコントローラと Entry() という名前のコントローラ アクションにマップする方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="16bd2-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="16bd2-142">[前へ](asp-net-mvc-controller-overview-vb.md)
> [次へ](creating-a-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="16bd2-142">[Previous](asp-net-mvc-controller-overview-vb.md)
[Next](creating-a-route-constraint-vb.md)</span></span>
