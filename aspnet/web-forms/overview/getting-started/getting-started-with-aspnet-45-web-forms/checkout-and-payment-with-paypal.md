---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: ペイパルでのチェックアウトと支払い |マイクロソフトドキュメント
author: Erikre
description: このチュートリアル シリーズ ASP.NETでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 for.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675689"
---
# <a name="checkout-and-payment-with-paypal"></a><span data-ttu-id="c3642-103">精算と PayPal による支払い</span><span class="sxs-lookup"><span data-stu-id="c3642-103">Checkout and Payment with PayPal</span></span>

<span data-ttu-id="c3642-104">[エリック・レイタン](https://github.com/Erikre)著</span><span class="sxs-lookup"><span data-stu-id="c3642-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="c3642-105">[Wingtip Toys サンプル プロジェクト (C#) をダウンロードするか、](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)[電子書籍をダウンロード (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="c3642-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="c3642-106">このチュートリアル シリーズでは、ASP.NET 4.5 および Web 用の Visual Studio Express 2013 を使用して、ASP.NET Web フォーム アプリケーションを構築する基本について説明します。</span><span class="sxs-lookup"><span data-stu-id="c3642-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="c3642-107">[C# ソース コードを含む](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)Visual Studio 2013 プロジェクトは、このチュートリアル シリーズに付属しています。</span><span class="sxs-lookup"><span data-stu-id="c3642-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="c3642-108">このチュートリアルでは、PayPal を使用してユーザーの承認、登録、および支払いを含むように Wingtip Toys サンプル アプリケーションを変更する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c3642-108">This tutorial describes how to modify the Wingtip Toys sample application to include user authorization, registration, and payment using PayPal.</span></span> <span data-ttu-id="c3642-109">ログインしているユーザーのみが製品を購入する権限を持ちます。</span><span class="sxs-lookup"><span data-stu-id="c3642-109">Only users who are logged in will have authorization to purchase products.</span></span> <span data-ttu-id="c3642-110">ASP.NET 4.5 Web フォーム プロジェクト テンプレートの組み込みのユーザー登録機能には、必要なものの多くが既に含まれています。</span><span class="sxs-lookup"><span data-stu-id="c3642-110">The ASP.NET 4.5 Web Forms project template's built-in user registration functionality already includes much of what you need.</span></span> <span data-ttu-id="c3642-111">PayPal エクスプレス チェックアウト機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-111">You will add PayPal Express Checkout functionality.</span></span> <span data-ttu-id="c3642-112">このチュートリアルでは、PayPal開発者のテスト環境を使用しているので、実際の資金は転送されません。</span><span class="sxs-lookup"><span data-stu-id="c3642-112">In this tutorial you be using the PayPal developer testing environment, so no actual funds will be transferred.</span></span> <span data-ttu-id="c3642-113">チュートリアルの最後に、ショッピング カートに追加する製品を選択し、チェックアウト ボタンをクリックして、PayPal テスト Web サイトにデータを転送することで、アプリケーションをテストします。</span><span class="sxs-lookup"><span data-stu-id="c3642-113">At the end of the tutorial, you will test the application by selecting products to add to the shopping cart, clicking the checkout button, and transferring data to the PayPal testing web site.</span></span> <span data-ttu-id="c3642-114">PayPal テスト Web サイトで、出荷と支払い情報を確認し、購入を確認して完了するために、ローカルの Wingtip Toys サンプル アプリケーションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="c3642-114">On the PayPal testing web site, you will confirm your shipping and payment information and then return to the local Wingtip Toys sample application to confirm and complete the purchase.</span></span>

<span data-ttu-id="c3642-115">スケーラビリティとセキュリティに対応したオンライン ショッピングを専門とする経験豊富なサードパーティの支払いプロセッサがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="c3642-115">There are several experienced third-party payment processors that specialize in online shopping that address scalability and security.</span></span> <span data-ttu-id="c3642-116">ASP.NET開発者は、ショッピングと購入ソリューションを実装する前に、サードパーティの支払いソリューションを利用することの利点を考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-116">ASP.NET developers should consider the advantages of utilizing a third party payment solution before implementing a shopping and purchasing solution.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c3642-117">Wingtip Toys サンプル アプリケーションは、ASP.NET Web 開発者が利用できる特定のASP.NETの概念と機能を示すように設計されています。</span><span class="sxs-lookup"><span data-stu-id="c3642-117">The Wingtip Toys sample application was designed to shown specific ASP.NET concepts and features available to ASP.NET web developers.</span></span> <span data-ttu-id="c3642-118">このサンプル アプリケーションは、スケーラビリティとセキュリティに関して考えられるすべての状況に合わせて最適化されたものではありません。</span><span class="sxs-lookup"><span data-stu-id="c3642-118">This sample application was not optimized for all possible circumstances in regard to scalability and security.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="c3642-119">ここでは、次の内容について学習します。</span><span class="sxs-lookup"><span data-stu-id="c3642-119">What you'll learn:</span></span>

- <span data-ttu-id="c3642-120">フォルダ内の特定のページへのアクセスを制限する方法。</span><span class="sxs-lookup"><span data-stu-id="c3642-120">How to restrict access to specific pages in a folder.</span></span>
- <span data-ttu-id="c3642-121">匿名ショッピング カートから既知のショッピング カートを作成する方法。</span><span class="sxs-lookup"><span data-stu-id="c3642-121">How to create a known shopping cart from an anonymous shopping cart.</span></span>
- <span data-ttu-id="c3642-122">プロジェクトの SSL を有効にする方法。</span><span class="sxs-lookup"><span data-stu-id="c3642-122">How to enable SSL for the project.</span></span>
- <span data-ttu-id="c3642-123">OAuth プロバイダーをプロジェクトに追加する方法。</span><span class="sxs-lookup"><span data-stu-id="c3642-123">How to add an OAuth provider to the project.</span></span>
- <span data-ttu-id="c3642-124">PayPal テスト環境を使用して製品を購入する PayPal を使用する方法。</span><span class="sxs-lookup"><span data-stu-id="c3642-124">How to use PayPal to purchase products using the PayPal testing environment.</span></span>
- <span data-ttu-id="c3642-125">**詳細ビュー**コントロールでの PayPal から詳細を表示する方法。</span><span class="sxs-lookup"><span data-stu-id="c3642-125">How to display details from PayPal in a **DetailsView** control.</span></span>
- <span data-ttu-id="c3642-126">PayPalから取得した詳細でWingtipのおもちゃのアプリケーションのデータベースを更新する方法。</span><span class="sxs-lookup"><span data-stu-id="c3642-126">How to update the database of the Wingtip Toys application with details obtained from PayPal.</span></span>

## <a name="adding-order-tracking"></a><span data-ttu-id="c3642-127">注文追跡の追加</span><span class="sxs-lookup"><span data-stu-id="c3642-127">Adding Order Tracking</span></span>

<span data-ttu-id="c3642-128">このチュートリアルでは、ユーザーが作成した順序からデータを追跡する 2 つの新しいクラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3642-128">In this tutorial, you'll create two new classes to track data from the order a user has created.</span></span> <span data-ttu-id="c3642-129">クラスは、出荷情報、購入合計、および支払確認に関するデータを追跡します。</span><span class="sxs-lookup"><span data-stu-id="c3642-129">The classes will track data regarding shipping information, purchase total, and payment confirmation.</span></span>

### <a name="add-the-order-and-orderdetail-model-classes"></a><span data-ttu-id="c3642-130">順序および注文詳細モデル クラスの追加</span><span class="sxs-lookup"><span data-stu-id="c3642-130">Add the Order and OrderDetail Model Classes</span></span>

<span data-ttu-id="c3642-131">このチュートリアル シリーズの前半`Category`では *、Models*フォルダーに 、、`Product`および クラスを作成して、カテゴリ、製品`CartItem`、およびショッピング カートのアイテムのスキーマを定義しました。</span><span class="sxs-lookup"><span data-stu-id="c3642-131">Earlier in this tutorial series, you defined the schema for categories, products, and shopping cart items by creating the `Category`, `Product`, and `CartItem` classes in the *Models* folder.</span></span> <span data-ttu-id="c3642-132">次に、2 つの新しいクラスを追加して、製品の注文のスキーマと注文の詳細を定義します。</span><span class="sxs-lookup"><span data-stu-id="c3642-132">Now you will add two new classes to define the schema for the product order and the details of the order.</span></span>

1. <span data-ttu-id="c3642-133">**Models**フォルダに、 という名前の新しいクラス*Order.cs*追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-133">In the **Models** folder, add a new class named *Order.cs*.</span></span>   
   <span data-ttu-id="c3642-134">新しいクラス ファイルがエディターに表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-134">The new class file is displayed in the editor.</span></span>
2. <span data-ttu-id="c3642-135">既定のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-135">Replace the default code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. <span data-ttu-id="c3642-136">*OrderDetail.cs*クラスを*Models*フォルダーに追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-136">Add an *OrderDetail.cs* class to the *Models* folder.</span></span>
4. <span data-ttu-id="c3642-137">既定のコードを以下のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-137">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

<span data-ttu-id="c3642-138">`Order`および`OrderDetail`クラスには、購買および出荷に使用する注文情報を定義するスキーマが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c3642-138">The `Order` and `OrderDetail` classes contain the schema to define the order information used for purchasing and shipping.</span></span>

<span data-ttu-id="c3642-139">さらに、エンティティ クラスを管理し、データベースへのデータ アクセスを提供するデータベース コンテキスト クラスを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-139">In addition, you will need to update the database context class that manages the entity classes and that provides data access to the database.</span></span> <span data-ttu-id="c3642-140">これを行うには、新しく作成された Order クラス`OrderDetail`とモデル`ProductContext`クラスをクラスに追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-140">To do this, you will add the newly created Order and `OrderDetail` model classes to `ProductContext` class.</span></span>

1. <span data-ttu-id="c3642-141">**ソリューション エクスプローラー**で *、ProductContext.cs*ファイルを検索して開きます。</span><span class="sxs-lookup"><span data-stu-id="c3642-141">In **Solution Explorer**, find and open the *ProductContext.cs* file.</span></span>
2. <span data-ttu-id="c3642-142">次に示すように、強調表示されたコードを*ProductContext.cs*ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-142">Add the highlighted code to the *ProductContext.cs* file as shown below:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

<span data-ttu-id="c3642-143">このチュートリアル シリーズで既に説明したように *、ProductContext.cs*ファイルのコードは`System.Data.Entity`、Entity Framework のすべてのコア機能にアクセスできるように名前空間を追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-143">As mentioned previously in this tutorial series, the code in the *ProductContext.cs* file adds the `System.Data.Entity` namespace so that you have access to all the core functionality of the Entity Framework.</span></span> <span data-ttu-id="c3642-144">この機能には、厳密に型指定されたオブジェクトを操作してデータを照会、挿入、更新、および削除する機能が含まれます。</span><span class="sxs-lookup"><span data-stu-id="c3642-144">This functionality includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span> <span data-ttu-id="c3642-145">クラス内の上記の`ProductContext`コードは、新しく追加`Order`されたクラスと`OrderDetail`クラスへの Entity Framework アクセスを追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-145">The above code in the `ProductContext` class adds Entity Framework access to the newly added `Order` and `OrderDetail` classes.</span></span>

## <a name="adding-checkout-access"></a><span data-ttu-id="c3642-146">チェックアウト アクセスの追加</span><span class="sxs-lookup"><span data-stu-id="c3642-146">Adding Checkout Access</span></span>

<span data-ttu-id="c3642-147">Wingtip Toys サンプル アプリケーションを使用すると、匿名ユーザーはショッピング カートに製品を確認および追加できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-147">The Wingtip Toys sample application allows anonymous users to review and add products to a shopping cart.</span></span> <span data-ttu-id="c3642-148">ただし、匿名ユーザーがショッピング カートに追加した商品を購入する場合は、サイトにログオンする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-148">However, when anonymous users choose to purchase the products they added to the shopping cart, they must log on to the site.</span></span> <span data-ttu-id="c3642-149">ログオンすると、チェックアウトと購入プロセスを処理する Web アプリケーションの制限されたページにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="c3642-149">Once they have logged on, they can access the restricted pages of the Web application that handle the checkout and purchase process.</span></span> <span data-ttu-id="c3642-150">これらの制限されたページは、アプリケーションの*チェックアウト*フォルダーに含まれています。</span><span class="sxs-lookup"><span data-stu-id="c3642-150">These restricted pages are contained in the *Checkout* folder of the application.</span></span>

### <a name="add-a-checkout-folder-and-pages"></a><span data-ttu-id="c3642-151">チェックアウト フォルダとページを追加する</span><span class="sxs-lookup"><span data-stu-id="c3642-151">Add a Checkout Folder and Pages</span></span>

<span data-ttu-id="c3642-152">チェックアウト フォルダーと、*その*中に、チェックアウトプロセス中に表示されるページを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3642-152">You will now create the *Checkout* folder and the pages in it that the customer will see during the checkout process.</span></span> <span data-ttu-id="c3642-153">これらのページは、このチュートリアルの後半で更新します。</span><span class="sxs-lookup"><span data-stu-id="c3642-153">You will update these pages later in this tutorial.</span></span>

1. <span data-ttu-id="c3642-154">**ソリューション エクスプローラ**でプロジェクト名 (**Wingtip Toys**) を右クリックし、[**新しいフォルダの追加 ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-154">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add a New Folder**.</span></span> 

    ![PayPal でのチェックアウトと支払い - 新しいフォルダー](checkout-and-payment-with-paypal/_static/image1.png)
2. <span data-ttu-id="c3642-156">新しいフォルダに 「チェックアウト」 という名前*を付けます*。</span><span class="sxs-lookup"><span data-stu-id="c3642-156">Name the new folder *Checkout*.</span></span>
3. <span data-ttu-id="c3642-157">*[チェックアウト*] フォルダを右クリックし、[**Add**-&gt;**新しい項目**の追加] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-157">Right-click the *Checkout* folder and then select **Add**-&gt;**New Item**.</span></span> 

    ![PayPal でのチェックアウトと支払い - 新しいアイテム](checkout-and-payment-with-paypal/_static/image2.png)
4. <span data-ttu-id="c3642-159">**[新しい項目の追加]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-159">The **Add New Item** dialog box is displayed.</span></span>
5. <span data-ttu-id="c3642-160">左側の **[Visual C#**  - &gt; **Web**テンプレート] グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-160">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="c3642-161">次に、中央のウィンドウで [**マスター ページを含む Web フォーム**] を選択し、"CheckoutStart.aspx" という名前を*付けます*。</span><span class="sxs-lookup"><span data-stu-id="c3642-161">Then, from the middle pane, select **Web Form with Master Page**and name it *CheckoutStart.aspx*.</span></span> 

    ![PayPal でのチェックアウトと支払い - 新しい項目の追加ダイアログ](checkout-and-payment-with-paypal/_static/image3.png)
6. <span data-ttu-id="c3642-163">前と同様に、マスター ページとして*Site.Master*ファイルを選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-163">As before, select the *Site.Master* file as the master page.</span></span>
7. <span data-ttu-id="c3642-164">上記と同じ手順を使用して、次のページを *[チェックアウト*] フォルダに追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-164">Add the following additional pages to the *Checkout* folder using the same steps above:</span></span>   

    - <span data-ttu-id="c3642-165">レビューをチェックアウト.aspx</span><span class="sxs-lookup"><span data-stu-id="c3642-165">CheckoutReview.aspx</span></span>
    - <span data-ttu-id="c3642-166">チェックアウトコンプリート.aspx</span><span class="sxs-lookup"><span data-stu-id="c3642-166">CheckoutComplete.aspx</span></span>
    - <span data-ttu-id="c3642-167">チェックアウトキャンセル.aspx</span><span class="sxs-lookup"><span data-stu-id="c3642-167">CheckoutCancel.aspx</span></span>
    - <span data-ttu-id="c3642-168">エラーをチェックアウト.aspx</span><span class="sxs-lookup"><span data-stu-id="c3642-168">CheckoutError.aspx</span></span>

### <a name="add-a-webconfig-file"></a><span data-ttu-id="c3642-169">Web.config ファイルを追加する</span><span class="sxs-lookup"><span data-stu-id="c3642-169">Add a Web.config File</span></span>

<span data-ttu-id="c3642-170">新しい*Web.config*ファイルを *[チェックアウト*] フォルダに追加すると、フォルダに含まれるすべてのページへのアクセスを制限できるようになります。</span><span class="sxs-lookup"><span data-stu-id="c3642-170">By adding a new *Web.config* file to the *Checkout* folder, you will be able to restrict access to all the pages contained in the folder.</span></span>

1. <span data-ttu-id="c3642-171">*[チェックアウト*] フォルダを右クリックし、[**新しい項目**の**追加]** -&gt;を選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-171">Right-click the *Checkout* folder and select **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="c3642-172">**[新しい項目の追加]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-172">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="c3642-173">左側の **[Visual C#**  - &gt; **Web**テンプレート] グループを選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-173">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="c3642-174">次に、中央のウィンドウで **[Web 構成ファイル**] を選択し、既定の名前の*Web.config*をそのまま使用**します。**</span><span class="sxs-lookup"><span data-stu-id="c3642-174">Then, from the middle pane, select **Web Configuration File**, accept the default name of *Web.config*, and then select **Add**.</span></span>
3. <span data-ttu-id="c3642-175">*Web.config* ファイルの XML の内容を次の内容で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-175">Replace the existing XML content in the *Web.config* file with the following:</span></span>  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. <span data-ttu-id="c3642-176">*Web.config* ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="c3642-176">Save the *Web.config* file.</span></span>

<span data-ttu-id="c3642-177">*Web.config*ファイルは、Web アプリケーションのすべての不明なユーザーが*チェックアウト*フォルダーに含まれるページへのアクセスを拒否する必要があることを指定します。</span><span class="sxs-lookup"><span data-stu-id="c3642-177">The *Web.config* file specifies that all unknown users of the Web application must be denied access to the pages contained in the *Checkout* folder.</span></span> <span data-ttu-id="c3642-178">ただし、ユーザーがアカウントを登録し、ログオンしている場合は、既知のユーザーになり、*チェックアウト*フォルダー内のページにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="c3642-178">However, if the user has registered an account and is logged on, they will be a known user and will have access to the pages in the *Checkout* folder.</span></span>

<span data-ttu-id="c3642-179">ASP.NET構成は階層に従い、各*Web.config*ファイルは、そのフォルダーとその下にあるすべての子ディレクトリに構成設定を適用することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="c3642-179">It's important to note that ASP.NET configuration follows a hierarchy, where each *Web.config* file applies configuration settings to the folder that it is in and to all of the child directories below it.</span></span>

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a><span data-ttu-id="c3642-180">プロジェクトに対して SSL を有効にする</span><span class="sxs-lookup"><span data-stu-id="c3642-180">Enable SSL for the Project</span></span>

 <span data-ttu-id="c3642-181">Secure Sockets Layer (SSL) は、Web サーバーと Web クライアント間の通信に定義されたプロトコルで、暗号化によって通信の安全性を強化することができます。</span><span class="sxs-lookup"><span data-stu-id="c3642-181">Secure Sockets Layer (SSL) is a protocol defined to allow Web servers and Web clients to communicate more securely through the use of encryption.</span></span> <span data-ttu-id="c3642-182">SSL を使わないと、クライアントとサーバー間で送信されるデータが、ネットワークに物理的にアクセスできる第三者によるパケット スニッフィングの標的になります。</span><span class="sxs-lookup"><span data-stu-id="c3642-182">When SSL is not used, data sent between the client and server is open to packet sniffing by anyone with physical access to the network.</span></span> <span data-ttu-id="c3642-183">また、プレーンな HTTP を使用すると、いくつかの一般的な認証方式の安全性も低下します。</span><span class="sxs-lookup"><span data-stu-id="c3642-183">Additionally, several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="c3642-184">具体的には、基本認証とフォーム認証で送信する資格情報が暗号化されません。</span><span class="sxs-lookup"><span data-stu-id="c3642-184">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="c3642-185">安全性を確保するには、これらの認証方式で SSL を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-185">To be secure, these authentication schemes must use SSL.</span></span> 

1. <span data-ttu-id="c3642-186">**ソリューション エクスプローラー**で**WingtipToys**プロジェクトをクリックし **、F4**キーを押して **[プロパティ]** ウィンドウを表示します。</span><span class="sxs-lookup"><span data-stu-id="c3642-186">In **Solution Explorer**, click the **WingtipToys** project, then press **F4** to display the **Properties** window.</span></span>
2. <span data-ttu-id="c3642-187">**SSL の有効化**を に変更します`true`。</span><span class="sxs-lookup"><span data-stu-id="c3642-187">Change **SSL Enabled** to `true`.</span></span>
3. <span data-ttu-id="c3642-188">後で使用するための **SSL URL** をコピーします。</span><span class="sxs-lookup"><span data-stu-id="c3642-188">Copy the **SSL URL** so you can use it later.</span></span>   
 <span data-ttu-id="c3642-189">SSL URL は`https://localhost:44300/`、SSL Web サイトを以前に作成していなければ (以下に示す) 場合を除き、表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-189">The SSL URL will be `https://localhost:44300/` unless you've previously created SSL Web Sites (as shown below).</span></span>   
    <span data-ttu-id="c3642-190">![プロジェクト プロパティ](checkout-and-payment-with-paypal/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c3642-190">![Project Properties](checkout-and-payment-with-paypal/_static/image4.png)</span></span>
4. <span data-ttu-id="c3642-191">**ソリューション エクスプローラ**で **、WingtipToys**プロジェクトを右クリックし、[**プロパティ**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-191">In **Solution Explorer**, right click the **WingtipToys** project and click **Properties**.</span></span>
5. <span data-ttu-id="c3642-192">左側のタブで **[Web]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-192">In the left tab, click **Web**.</span></span>
6. <span data-ttu-id="c3642-193">先ほど保存した SSL **URL を**使用するようにプロジェクト**URL**を変更します。</span><span class="sxs-lookup"><span data-stu-id="c3642-193">Change the **Project Url** to use the **SSL URL** that you saved earlier.</span></span>   
    <span data-ttu-id="c3642-194">![プロジェクトの Web プロパティ](checkout-and-payment-with-paypal/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c3642-194">![Project Web Properties](checkout-and-payment-with-paypal/_static/image5.png)</span></span>
7. <span data-ttu-id="c3642-195">**CTRL + S キーを押して**ページを保存します。</span><span class="sxs-lookup"><span data-stu-id="c3642-195">Save the page by pressing **CTRL+S**.</span></span>
8. <span data-ttu-id="c3642-196">**Ctrl キーを押しながら F5 キー**を押して、アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="c3642-196">Press **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="c3642-197">Visual Studio により、SSL の警告を回避するためのオプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-197">Visual Studio will display an option to allow you to avoid SSL warnings.</span></span>
9. <span data-ttu-id="c3642-198">IIS Express SSL 証明書を信頼する場合は **[はい]** をクリックして続行します。</span><span class="sxs-lookup"><span data-stu-id="c3642-198">Click **Yes** to trust the IIS Express SSL certificate and continue.</span></span>   
    <span data-ttu-id="c3642-199">![IIS Express SSL 証明書の詳細](checkout-and-payment-with-paypal/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="c3642-199">![IIS Express SSL certificate details](checkout-and-payment-with-paypal/_static/image6.png)</span></span>  
 <span data-ttu-id="c3642-200"> セキュリティ警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-200">A Security Warning is displayed.</span></span>
10. <span data-ttu-id="c3642-201">**[はい]** をクリックしてローカルホストに証明書をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c3642-201">Click **Yes** to install the certificate to your localhost.</span></span>   
    <span data-ttu-id="c3642-202">![セキュリティ警告ダイアログ ボックス](checkout-and-payment-with-paypal/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c3642-202">![Security Warning dialog box](checkout-and-payment-with-paypal/_static/image7.png)</span></span>  
 <span data-ttu-id="c3642-203"> ブラウザー ウィンドウが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-203">The browser window will be displayed.</span></span>

<span data-ttu-id="c3642-204">SSL を使用して、Web アプリケーションをローカルで簡単にテストできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="c3642-204">You can now easily test your Web application locally using SSL.</span></span>

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a><span data-ttu-id="c3642-205">OAuth 2.0 プロバイダーを追加する</span><span class="sxs-lookup"><span data-stu-id="c3642-205">Add an OAuth 2.0 Provider</span></span>

<span data-ttu-id="c3642-206">ASP.NET Web フォームは、メンバーシップと認証のオプションが強化されています。</span><span class="sxs-lookup"><span data-stu-id="c3642-206">ASP.NET Web Forms provides enhanced options for membership and authentication.</span></span> <span data-ttu-id="c3642-207">OAuth もこうした強化点の 1 つです。</span><span class="sxs-lookup"><span data-stu-id="c3642-207">These enhancements include OAuth.</span></span> <span data-ttu-id="c3642-208">OAuth は、Web、モバイル、およびデスクトップのアプリケーションからシンプルで標準的な方法で安全に認証するためのオープン プロトコルです。</span><span class="sxs-lookup"><span data-stu-id="c3642-208">OAuth is an open protocol that allows secure authorization in a simple and standard method from web, mobile, and desktop applications.</span></span> <span data-ttu-id="c3642-209">ASP.NET Web フォーム テンプレートは OAuth を使用して、Facebook、Twitter、Google、および Microsoft を認証プロバイダーとして公開します。</span><span class="sxs-lookup"><span data-stu-id="c3642-209">The ASP.NET Web Forms template uses OAuth to expose Facebook, Twitter, Google and Microsoft as authentication providers.</span></span> <span data-ttu-id="c3642-210">このチュートリアルでは Google のみを認証プロバイダーとして使用しますが、コードを少し変更すれば他のプロバイダーも使用できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-210">Although this tutorial uses only Google as the authentication provider, you can easily modify the code to use any of the providers.</span></span> <span data-ttu-id="c3642-211">他のプロバイダーを実装する手順は、このチュートリアルで説明する手順とほとんど同じです。</span><span class="sxs-lookup"><span data-stu-id="c3642-211">The steps to implement other providers are very similar to the steps you will see in this tutorial.</span></span>

<span data-ttu-id="c3642-212">このチュートリアルでは、認証の他にロールを使用して権限を付与します。</span><span class="sxs-lookup"><span data-stu-id="c3642-212">In addition to authentication, the tutorial will also use roles to implement authorization.</span></span> <span data-ttu-id="c3642-213">`canEdit` ロールに追加したユーザーだけが連絡先を変更 (作成、編集、削除) できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-213">Only those users you add to the `canEdit` role will be able to change data (create, edit, or delete contacts).</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c3642-214">Windows Live アプリケーションは、作業中の Web サイトのライブ URL のみを受け入れるため、ログインのテストにローカル Web サイトの URL を使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="c3642-214">Windows Live applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>

<span data-ttu-id="c3642-215">次の手順を実行することで、Google 認証プロバイダーを追加できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-215">The following steps will allow you to add a Google authentication provider.</span></span>

1. <span data-ttu-id="c3642-216">*アプリケーション\_の開始\スタートアップ.Auth.csファイルを*開きます。</span><span class="sxs-lookup"><span data-stu-id="c3642-216">Open the *App\_Start\Startup.Auth.cs* file.</span></span>
2. <span data-ttu-id="c3642-217">`app.UseGoogleAuthentication()` メソッドのコメント文字を削除して、メソッドを次のような記述にします。</span><span class="sxs-lookup"><span data-stu-id="c3642-217">Remove the comment characters from the `app.UseGoogleAuthentication()` method so that the method appears as follows:</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. <span data-ttu-id="c3642-218">[Google Developers Console](https://console.developers.google.com/)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="c3642-218">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span> <span data-ttu-id="c3642-219">Google デベロッパーの電子メール アカウント (gmail.com) でサインインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-219">You will also need to sign-in with your Google developer email account (gmail.com).</span></span> <span data-ttu-id="c3642-220">Google アカウントを持っていない場合は、 **[Create an account]** リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-220">If you do not have a Google account, select the **Create an account** link.</span></span>   
   <span data-ttu-id="c3642-221">**Google Developers Console**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-221">Next, you'll see the **Google Developers Console**.</span></span>   
    <span data-ttu-id="c3642-222">![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="c3642-222">![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)</span></span>
4. <span data-ttu-id="c3642-223">[**プロジェクトの作成**] ボタンをクリックし、プロジェクト名と ID を入力します (既定値を使用できます)。</span><span class="sxs-lookup"><span data-stu-id="c3642-223">Click the **Create Project** button and enter a project name and ID (you can use the default values).</span></span> <span data-ttu-id="c3642-224">次に、**契約のチェックボックス**と[**作成**]ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-224">Then, click the **agreement checkbox** and the **Create** button.</span></span>  

    ![グーグル - 新しいプロジェクト](checkout-and-payment-with-paypal/_static/image9.png)

   <span data-ttu-id="c3642-226"> 新しいプロジェクトが数秒で作成され、新しいプロジェクトのページがブラウザーに表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-226">In a few seconds the new project will be created and your browser will display the new projects page.</span></span>
5. <span data-ttu-id="c3642-227">左側のタブで**&amp;[API 認証**] をクリックし、[**資格情報**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-227">In the left tab, click **APIs &amp; auth**, and then click **Credentials**.</span></span>
6. <span data-ttu-id="c3642-228">**[OAuth]** の下の **[新しいクライアント ID**の作成] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-228">Click the **Create New Client ID** under **OAuth**.</span></span>   
   <span data-ttu-id="c3642-229">**[Create Client ID]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-229">The **Create Client ID** dialog will be displayed.</span></span>   
    <span data-ttu-id="c3642-230">![Google - クライアント ID の作成](checkout-and-payment-with-paypal/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="c3642-230">![Google - Create Client ID](checkout-and-payment-with-paypal/_static/image10.png)</span></span>
7. <span data-ttu-id="c3642-231">[**クライアント ID**の作成] ダイアログで、アプリケーションの種類に応える既定の Web**アプリケーション**をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="c3642-231">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
8. <span data-ttu-id="c3642-232">このチュートリアルで前に使用した SSL URL に **[許可された JavaScript の配信元**] を設定します (`https://localhost:44300/`他の SSL プロジェクトを作成していない場合)。</span><span class="sxs-lookup"><span data-stu-id="c3642-232">Set the **Authorized JavaScript Origins** to the SSL URL you used earlier in this tutorial (`https://localhost:44300/` unless you've created other SSL projects).</span></span>   
   <span data-ttu-id="c3642-233">この URL は、アプリケーションの発信元です。</span><span class="sxs-lookup"><span data-stu-id="c3642-233">This URL is the origin for your application.</span></span> <span data-ttu-id="c3642-234">このサンプルでは、ローカルホストテスト URL のみを入力します。</span><span class="sxs-lookup"><span data-stu-id="c3642-234">For this sample, you will only enter the localhost test URL.</span></span> <span data-ttu-id="c3642-235">ただし、ローカルホストと本番環境を考慮して複数の URL を入力できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-235">However, you can enter multiple URLs to account for localhost and production.</span></span>
9. <span data-ttu-id="c3642-236">**[Authorized Redirect URI]** には次の値を設定します。</span><span class="sxs-lookup"><span data-stu-id="c3642-236">Set the **Authorized Redirect URI** to the following:</span></span> 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   <span data-ttu-id="c3642-237">この値は、ASP.NET OAuth ユーザーが Google の OAuth サーバーとの通信に使用する URI です。</span><span class="sxs-lookup"><span data-stu-id="c3642-237">This value is the URI that ASP.NET OAuth users to communicate with the google OAuth server.</span></span> <span data-ttu-id="c3642-238">上記で使用した SSL URL`https://localhost:44300/`を覚えておいてください (他の SSL プロジェクトを作成していない場合)。</span><span class="sxs-lookup"><span data-stu-id="c3642-238">Remember the SSL URL you used above (    `https://localhost:44300/` unless you've created other SSL projects).</span></span>
10. <span data-ttu-id="c3642-239">[クライアント ID の**作成]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-239">Click the **Create Client ID** button.</span></span>
11. <span data-ttu-id="c3642-240">Google デベロッパー コンソールの左側のメニューで、[**同意] 画面**のメニュー項目をクリックし、メールアドレスと製品名を設定します。</span><span class="sxs-lookup"><span data-stu-id="c3642-240">On the left menu of the Google Developers Console, click the **Consent screen** menu item, then set your email address and product name.</span></span> <span data-ttu-id="c3642-241">フォームに入力したら、[**保存**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-241">When you have completed the form, click **Save**.</span></span>
12. <span data-ttu-id="c3642-242">**API**メニュー項目をクリックし、下にスクロールして **、Google+ API**の横にある**オフ**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-242">Click the **APIs** menu item, scroll down and click the **off** button next to **Google+ API**.</span></span>   
    <span data-ttu-id="c3642-243">このオプションを受け入れると、Google+ API が有効になります。</span><span class="sxs-lookup"><span data-stu-id="c3642-243">Accepting this option will enable the Google+ API.</span></span>
13. <span data-ttu-id="c3642-244">また、**バージョン 3.0.0 に Microsoft.Owin** NuGet パッケージを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-244">You must also update the **Microsoft.Owin** NuGet package to version 3.0.0.</span></span>   
    <span data-ttu-id="c3642-245">[**ツール**] メニューの **[NuGet パッケージ マネージャー** ] を選択し、[**ソリューションの NuGet パッケージの管理**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-245">From the **Tools** menu, select **NuGet Package Manager** and then select **Manage NuGet Packages for Solution**.</span></span>  
    <span data-ttu-id="c3642-246">**[NuGet パッケージの管理**] ウィンドウで **、Microsoft.Owin**パッケージを見つけてバージョン 3.0.0 に更新します。</span><span class="sxs-lookup"><span data-stu-id="c3642-246">From the **Manage NuGet Packages** window, find and update the **Microsoft.Owin** package to version 3.0.0.</span></span>
14. <span data-ttu-id="c3642-247">Visual Studio で、`UseGoogleAuthentication`**クライアント ID**と**クライアント シークレット**をコピーして、メソッドに貼り付け *、Startup.Auth.cs*ページのメソッドを更新します。</span><span class="sxs-lookup"><span data-stu-id="c3642-247">In Visual Studio, update the `UseGoogleAuthentication` method of the *Startup.Auth.cs* page by copying and pasting the **Client ID** and **Client Secret** into the method.</span></span> <span data-ttu-id="c3642-248">以下に示す**クライアント ID**と**クライアント シークレット**の値はサンプルで、機能しません。</span><span class="sxs-lookup"><span data-stu-id="c3642-248">The **Client ID** and **Client Secret** values shown below are samples and will not work.</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. <span data-ttu-id="c3642-249">**Ctrl キーを押しながら F5 キー**を押して、アプリケーションをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="c3642-249">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="c3642-250">**[Log in]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-250">Click the **Log in** link.</span></span>
16. <span data-ttu-id="c3642-251">[**別のサービスを使用してログイン**] の下にある **[Google]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-251">Under **Use another service to log in**, click **Google**.</span></span>  
    <span data-ttu-id="c3642-252">![ログイン](checkout-and-payment-with-paypal/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="c3642-252">![Log in](checkout-and-payment-with-paypal/_static/image11.png)</span></span>
17. <span data-ttu-id="c3642-253">資格情報の入力が必要な場合、Google のサイトにリダイレクトされるので、リダイレクト先のサイトで資格情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="c3642-253">If you need to enter your credentials, you will be redirected to the google site where you will enter your credentials.</span></span>  
    ![Google - サインイン](checkout-and-payment-with-paypal/_static/image12.png)
18. <span data-ttu-id="c3642-255">資格情報を入力すると、作成した Web アプリケーションにアクセス許可を与えるプロンプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-255">After you enter your credentials, you will be prompted to give permissions to the web application you just created.</span></span>  
    ![プロジェクトのデフォルト サービス アカウント](checkout-and-payment-with-paypal/_static/image13.png)
19. <span data-ttu-id="c3642-257">**[Accept]\(受け入れる\)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-257">Click **Accept**.</span></span> <span data-ttu-id="c3642-258">これで、Google アカウントを登録できる**WingtipToys**アプリケーションの **[登録**] ページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="c3642-258">You will now be redirected back to the **Register** page of the **WingtipToys** application where you can register your Google account.</span></span>  
    <span data-ttu-id="c3642-259">![Google アカウントへの登録](checkout-and-payment-with-paypal/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="c3642-259">![Register with your Google Account](checkout-and-payment-with-paypal/_static/image14.png)</span></span>
20. <span data-ttu-id="c3642-260">Google アカウントに使用するローカルの電子メール登録名を変更できますが、通常は既定の電子メール エイリアス (認証に使用したエイリアス) を変更しません。</span><span class="sxs-lookup"><span data-stu-id="c3642-260">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="c3642-261">上記**のように[ログイン]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-261">Click **Log in** as shown above.</span></span>

### <a name="modifying-login-functionality"></a><span data-ttu-id="c3642-262">ログイン機能の変更</span><span class="sxs-lookup"><span data-stu-id="c3642-262">Modifying Login Functionality</span></span>

<span data-ttu-id="c3642-263">このチュートリアル シリーズで既に説明したように、ユーザー登録機能の多くは、既定では ASP.NET Web フォーム テンプレートに含まれています。</span><span class="sxs-lookup"><span data-stu-id="c3642-263">As previously mentioned in this tutorial series, much of the user registration functionality has been included in the ASP.NET Web Forms template by default.</span></span> <span data-ttu-id="c3642-264">次に、メソッドを呼び出すために既定の*Login.aspx*ページ`MigrateCart`と*Register.aspx*ページを変更します。</span><span class="sxs-lookup"><span data-stu-id="c3642-264">Now you will modify the default *Login.aspx* and *Register.aspx* pages to call the `MigrateCart` method.</span></span> <span data-ttu-id="c3642-265">この`MigrateCart`メソッドは、新しくログインしたユーザーを匿名ショッピング カートに関連付けます。</span><span class="sxs-lookup"><span data-stu-id="c3642-265">The `MigrateCart` method associates a newly logged in user with an anonymous shopping cart.</span></span> <span data-ttu-id="c3642-266">ユーザーとショッピング カートを関連付けることで、Wingtip Toys サンプル アプリケーションは、ユーザーのショッピング カートを訪問の間に維持することができます。</span><span class="sxs-lookup"><span data-stu-id="c3642-266">By associating the user and shopping cart, the Wingtip Toys sample application will be able to maintain the shopping cart of the user between visits.</span></span>

1. <span data-ttu-id="c3642-267">**ソリューション エクスプローラ**で *、[Account]* フォルダを探して開きます。</span><span class="sxs-lookup"><span data-stu-id="c3642-267">In **Solution Explorer**, find and open the *Account* folder.</span></span>
2. <span data-ttu-id="c3642-268">Login.aspx.cs*というコード*ビハインド ページを変更して、次のように表示されるように、黄色で強調表示されたコードを含めます。</span><span class="sxs-lookup"><span data-stu-id="c3642-268">Modify the code-behind page named *Login.aspx.cs* to include the code highlighted in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. <span data-ttu-id="c3642-269">*Login.aspx.cs*ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="c3642-269">Save the *Login.aspx.cs* file.</span></span>

<span data-ttu-id="c3642-270">ここでは、メソッドの定義が存在しないという警告を`MigrateCart`無視できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-270">For now, you can ignore the warning that there is no definition for the `MigrateCart` method.</span></span> <span data-ttu-id="c3642-271">このチュートリアルでは、後で追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-271">You will be adding it a bit later in this tutorial.</span></span>

<span data-ttu-id="c3642-272">*Login.aspx.cs*分離コード ファイルは、LogIn メソッドをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="c3642-272">The *Login.aspx.cs* code-behind file supports a LogIn method.</span></span> <span data-ttu-id="c3642-273">Login.aspx ページを調べることで、このページには、クリックするとコードビハインドのハンドラーを`LogIn`トリガーする 「ログイン」ボタンが含まれていることがわかります。</span><span class="sxs-lookup"><span data-stu-id="c3642-273">By inspecting the Login.aspx page, you'll see that this page includes a "Log in" button that when click triggers the `LogIn` handler on the code-behind.</span></span>

<span data-ttu-id="c3642-274">Login.aspx.csの`Login`メソッドが呼*Login.aspx.cs*び出されると、名前の付いた`usersShoppingCart`ショッピング カートの新しいインスタンスが作成されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-274">When the `Login` method on the *Login.aspx.cs* is called, a new instance of the shopping cart named `usersShoppingCart` is created.</span></span> <span data-ttu-id="c3642-275">ショッピング カートの ID (GUID) が取得され、変数に`cartId`設定されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-275">The ID of the shopping cart (a GUID) is retrieved and set to the `cartId` variable.</span></span> <span data-ttu-id="c3642-276">次に、`MigrateCart`このメソッドが呼び出`cartId`され、ログインしているユーザーの名前との両方がこのメソッドに渡されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-276">Then, the `MigrateCart` method is called, passing both the `cartId` and the name of the logged-in user to this method.</span></span> <span data-ttu-id="c3642-277">ショッピング カートを移行すると、匿名ショッピング カートの識別に使用される GUID がユーザー名に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="c3642-277">When the shopping cart is migrated, the GUID used to identify the anonymous shopping cart is replaced with the user name.</span></span>

<span data-ttu-id="c3642-278">ユーザーがログインしたときにショッピング カートを移行するように*Login.aspx.cs*分離コード ファイルを変更する以外に、ユーザーが新しいアカウントを作成してログインしたときにショッピング カートを移行するように*Register.aspx.cs分離ファイル*を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-278">In addition to modifying the *Login.aspx.cs* code-behind file to migrate the shopping cart when the user logs in, you must also modify the *Register.aspx.cs code-behind file* to migrate the shopping cart when the user creates a new account and logs in.</span></span>

1. <span data-ttu-id="c3642-279">*[アカウント*] フォルダで、 という名前のコード ビハインド ファイル*Register.aspx.cs*開きます。</span><span class="sxs-lookup"><span data-stu-id="c3642-279">In the *Account* folder, open the code-behind file named *Register.aspx.cs*.</span></span>
2. <span data-ttu-id="c3642-280">コードを黄色で含めて、コードビハインド ファイルを次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="c3642-280">Modify the code-behind file by including the code in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. <span data-ttu-id="c3642-281">*Register.aspx.cs*ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="c3642-281">Save the *Register.aspx.cs* file.</span></span> <span data-ttu-id="c3642-282">もう一度、メソッドに関する`MigrateCart`警告を無視します。</span><span class="sxs-lookup"><span data-stu-id="c3642-282">Once again, ignore the warning about the `MigrateCart` method.</span></span>

<span data-ttu-id="c3642-283">`CreateUser_Click`イベント ハンドラーで使用したコードは、`LogIn`メソッドで使用したコードと非常によく似ています。</span><span class="sxs-lookup"><span data-stu-id="c3642-283">Notice that the code you used in the `CreateUser_Click` event handler is very similar to the code you used in the `LogIn` method.</span></span> <span data-ttu-id="c3642-284">ユーザーがサイトに登録またはログインすると、`MigrateCart`メソッドの呼び出しが行われます。</span><span class="sxs-lookup"><span data-stu-id="c3642-284">When the user registers or logs in to the site, a call to the `MigrateCart` method will be made.</span></span>

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="c3642-285">ショッピング カートの移行</span><span class="sxs-lookup"><span data-stu-id="c3642-285">Migrating the Shopping Cart</span></span>

<span data-ttu-id="c3642-286">ログインと登録のプロセスが更新されましたので、このメソッドを使用してショッピング カートを移行するコードを`MigrateCart`追加できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-286">Now that you have the log-in and registration process updated, you can add the code to migrate the shopping cart using the `MigrateCart` method.</span></span>

1. <span data-ttu-id="c3642-287">**ソリューション エクスプローラー**で*Logic*フォルダーを見つけて *、ShoppingCartActions.cs*クラス ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="c3642-287">In **Solution Explorer**, find the *Logic* folder and open the *ShoppingCartActions.cs* class file.</span></span>
2. <span data-ttu-id="c3642-288">ShoppingCartActions.cs*ファイル内*の既存のコードに黄色で強調表示されたコードを追加して *、ShoppingCartActions.cs*ファイル内のコードが次のように表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="c3642-288">Add the code highlighted in yellow to the existing code in the *ShoppingCartActions.cs* file, so that the code in the *ShoppingCartActions.cs* file appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

<span data-ttu-id="c3642-289">この`MigrateCart`メソッドは、既存の cartId を使用して、ユーザーのショッピング カートを検索します。</span><span class="sxs-lookup"><span data-stu-id="c3642-289">The `MigrateCart` method uses the existing cartId to find the shopping cart of the user.</span></span> <span data-ttu-id="c3642-290">次に、コードはすべてのショッピング カートのアイテムをループ処理し、`CartId``CartItem`プロパティ (スキーマで指定された) をログイン ユーザー名に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-290">Next, the code loops through all the shopping cart items and replaces the `CartId` property (as specified by the `CartItem` schema) with the logged-in user name.</span></span>

### <a name="updating-the-database-connection"></a><span data-ttu-id="c3642-291">データベース接続の更新</span><span class="sxs-lookup"><span data-stu-id="c3642-291">Updating the Database Connection</span></span>

<span data-ttu-id="c3642-292">このチュートリアルを**使用して、事前構築された**Wingtip Toys サンプル アプリケーションを使用する場合は、既定のメンバーシップ データベースを再作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-292">If you are following this tutorial using the **prebuilt** Wingtip Toys sample application, you must recreate the default membership database.</span></span> <span data-ttu-id="c3642-293">既定の接続文字列を変更すると、次回アプリケーションを実行する際にメンバーシップ データベースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-293">By modifying the default connection string, the membership database will be created the next time the application runs.</span></span>

1. <span data-ttu-id="c3642-294">プロジェクトのルートにある*Web.config*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="c3642-294">Open the *Web.config* file at the root of the project.</span></span>
2. <span data-ttu-id="c3642-295">次のように表示されるように、既定の接続文字列を更新します。</span><span class="sxs-lookup"><span data-stu-id="c3642-295">Update the default connection string so that it appears as follows:</span></span>   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a><span data-ttu-id="c3642-296">ペイパルの統合</span><span class="sxs-lookup"><span data-stu-id="c3642-296">Integrating PayPal</span></span>

<span data-ttu-id="c3642-297">PayPalは、オンライン加盟店による支払いを受け付けるウェブベースの課金プラットフォームです。</span><span class="sxs-lookup"><span data-stu-id="c3642-297">PayPal is a web-based billing platform that accepts payments by online merchants.</span></span> <span data-ttu-id="c3642-298">このチュートリアルでは、次にPayPalのエクスプレスチェックアウト機能をアプリケーションに統合する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c3642-298">This tutorial next explains how to integrate PayPal's Express Checkout functionality into your application.</span></span> <span data-ttu-id="c3642-299">エクスプレスチェックアウトを使用すると、顧客はPayPalを使用してショッピングカートに追加したアイテムの支払いを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="c3642-299">Express Checkout allows your customers to use PayPal to pay for the items they have added to their shopping cart.</span></span>

### <a name="create-paypal-test-accounts"></a><span data-ttu-id="c3642-300">PayPal テスト アカウントの作成</span><span class="sxs-lookup"><span data-stu-id="c3642-300">Create PayPal Test Accounts</span></span>

<span data-ttu-id="c3642-301">PayPal テスト環境を使用するには、開発者テスト アカウントを作成して確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-301">To use the PayPal testing environment, you must create and verify a developer test account.</span></span> <span data-ttu-id="c3642-302">開発者テスト アカウントを使用して、購入者テスト アカウントと販売者テスト アカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3642-302">You will use the developer test account to create a buyer test account and a seller test account.</span></span> <span data-ttu-id="c3642-303">開発者テスト アカウントの資格情報では、Wingtip Toys サンプル アプリケーションが PayPal テスト環境にアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="c3642-303">The developer test account credentials also will allow the Wingtip Toys sample application to access the PayPal testing environment.</span></span>

1. <span data-ttu-id="c3642-304">ブラウザで、PayPal 開発者テストサイトに移動します。</span><span class="sxs-lookup"><span data-stu-id="c3642-304">In a browser, navigate to the PayPal developer testing site:</span></span>   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. <span data-ttu-id="c3642-305">PayPal デベロッパー アカウントをお持ちの場合は、[**サインアップ**] をクリックし、サインアップ手順に従って新しいアカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="c3642-305">If you don't have a PayPal developer account, create a new account by clicking **Sign Up**and following the sign up steps.</span></span> <span data-ttu-id="c3642-306">既存の PayPal 開発者アカウントをお持ちの場合は、[ログイン] をクリックして**ログイン**します。</span><span class="sxs-lookup"><span data-stu-id="c3642-306">If you have an existing PayPal developer account, sign in by clicking **Log In**.</span></span> <span data-ttu-id="c3642-307">このチュートリアルの後で Wingtip Toys サンプル アプリケーションをテストするには、PayPal 開発者アカウントが必要になります。</span><span class="sxs-lookup"><span data-stu-id="c3642-307">You will need your PayPal developer account to test the Wingtip Toys sample application later in this tutorial.</span></span>
3. <span data-ttu-id="c3642-308">PayPal デベロッパーアカウントにサインアップしたばかりの場合は、PayPal で PayPal 開発者アカウントを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-308">If you have just signed up for your PayPal developer account, you may need to verify your PayPal developer account with PayPal.</span></span> <span data-ttu-id="c3642-309">PayPal がメールアカウントに送信した手順に従って、アカウントを確認できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-309">You can verify your account by following the steps that PayPal sent to your email account.</span></span> <span data-ttu-id="c3642-310">PayPal 開発者アカウントを確認したら、PayPal 開発者テストサイトにログインし直してください。</span><span class="sxs-lookup"><span data-stu-id="c3642-310">Once you have verified your PayPal developer account, log back into the PayPal developer testing site.</span></span>
4. <span data-ttu-id="c3642-311">PayPal デベロッパーアカウントでPayPal開発者サイトにログインした後、PayPalの購入者テストアカウントをまだお持ちでない場合は、アカウントを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-311">After you are logged in to the PayPal developer site with your PayPal developer account you need to create a PayPal buyer test account if you don't already have one.</span></span> <span data-ttu-id="c3642-312">購入者のテスト アカウントを作成するには、PayPal サイトで [**アプリケーション**] タブをクリックし、[**サンドボックス アカウント**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-312">To create a buyer test account, on the PayPal site click the **Applications** tab and then click **Sandbox accounts**.</span></span>   
 <span data-ttu-id="c3642-313">**[サンドボックス テスト アカウント**] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-313">The **Sandbox test accounts** page is shown.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="c3642-314">PayPal デベロッパー サイトでは、既にマーチャント テスト アカウントが提供されています。</span><span class="sxs-lookup"><span data-stu-id="c3642-314">The PayPal Developer site already provides a merchant test account.</span></span>

    ![PayPal でのチェックアウトと支払い - サンドボックス テスト アカウント](checkout-and-payment-with-paypal/_static/image15.png)
5. <span data-ttu-id="c3642-316">[サンドボックス テスト アカウント] ページで、[**アカウントの作成**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-316">On the Sandbox test accounts page, click **Create Account**.</span></span>
6. <span data-ttu-id="c3642-317">[**テスト アカウントの作成**] ページで、任意の購入者テスト アカウントの電子メールとパスワードを選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-317">On the **Create test account** page choose a buyer test account email and password of your choice.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="c3642-318">このチュートリアルの最後で Wingtip Toys サンプル アプリケーションをテストするには、購入者の電子メール アドレスとパスワードが必要です。</span><span class="sxs-lookup"><span data-stu-id="c3642-318">You will need the buyer email addresses and password to test the Wingtip Toys sample application at the end of this tutorial.</span></span>

    ![PayPal でのチェックアウトと支払い - サンドボックス テスト アカウント](checkout-and-payment-with-paypal/_static/image16.png)
7. <span data-ttu-id="c3642-320">[アカウントの作成] ボタンをクリックして、購入者テスト**アカウントを作成**します。</span><span class="sxs-lookup"><span data-stu-id="c3642-320">Create the buyer test account by clicking the **Create Account** button.</span></span>  
 <span data-ttu-id="c3642-321">[**サンドボックス テスト アカウント**] ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-321">The **Sandbox Test accounts** page is displayed.</span></span> 

    ![PayPal でのチェックアウトと支払い - ペイパル アカウント](checkout-and-payment-with-paypal/_static/image17.png)
8. <span data-ttu-id="c3642-323">[**サンドボックス テスト アカウント**] ページで、**ファシリテーター**の電子メール アカウントをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-323">On the **Sandbox test accounts** page, click the **facilitator** email account.</span></span>  
    <span data-ttu-id="c3642-324">**プロファイル**と**通知**のオプションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-324">**Profile** and **Notification** options appear.</span></span>
9. <span data-ttu-id="c3642-325">[**プロファイル**] オプションを選択し **、[API 資格情報**] をクリックして、マーチャント テスト アカウントの API 資格情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="c3642-325">Select the **Profile** option, then click **API credentials** to view your API credentials for the merchant test account.</span></span>
10. <span data-ttu-id="c3642-326">TEST API の資格情報をメモ帳にコピーします。</span><span class="sxs-lookup"><span data-stu-id="c3642-326">Copy the TEST API credentials to notepad.</span></span>

<span data-ttu-id="c3642-327">Wingtip Toys サンプル アプリケーションから PayPal テスト環境への API 呼び出しを行うには、表示されているクラシック TEST API の認証情報 (ユーザー名、パスワード、および署名) が必要です。</span><span class="sxs-lookup"><span data-stu-id="c3642-327">You will need your displayed Classic TEST API credentials (Username, Password, and Signature) to make API calls from the Wingtip Toys sample application to the PayPal testing environment.</span></span> <span data-ttu-id="c3642-328">次の手順で資格情報を追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-328">You will add the credentials in the next step.</span></span>

### <a name="add-paypal-class-and-api-credentials"></a><span data-ttu-id="c3642-329">PayPal クラスと API 資格情報の追加</span><span class="sxs-lookup"><span data-stu-id="c3642-329">Add PayPal Class and API Credentials</span></span>

<span data-ttu-id="c3642-330">PayPal コードの大半を 1 つのクラスに配置します。</span><span class="sxs-lookup"><span data-stu-id="c3642-330">You will place the majority of the PayPal code into a single class.</span></span> <span data-ttu-id="c3642-331">このクラスには、PayPal との通信に使用されるメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c3642-331">This class contains the methods used to communicate with PayPal.</span></span> <span data-ttu-id="c3642-332">また、このクラスに PayPal 資格情報を追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-332">Also, you will add your PayPal credentials to this class.</span></span>

1. <span data-ttu-id="c3642-333">Visual Studio 内の Wingtip Toys サンプル アプリケーション**で、Logic**フォルダーを右クリックし、[**新しい項目**の**追加** -&gt;] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-333">In the Wingtip Toys sample application within Visual Studio, right-click the **Logic** folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="c3642-334">**[新しい項目の追加]** ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-334">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="c3642-335">左側の [**インストール済み**] ウィンドウの **[Visual C#** ] で、[**コード**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-335">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span>
3. <span data-ttu-id="c3642-336">中央のペインで 、[**クラス**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-336">From the middle pane, select **Class**.</span></span> <span data-ttu-id="c3642-337">この新しいクラス**に名前を付PayPalFunctions.cs。**</span><span class="sxs-lookup"><span data-stu-id="c3642-337">Name this new class **PayPalFunctions.cs**.</span></span>
4. <span data-ttu-id="c3642-338">**[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-338">Click **Add**.</span></span>  
   <span data-ttu-id="c3642-339">新しいクラス ファイルがエディターに表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-339">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="c3642-340">既定のコードを以下のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-340">Replace the default code with the following code:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. <span data-ttu-id="c3642-341">このチュートリアルで前に表示した Merchant API の認証情報 (ユーザー名、パスワード、および署名) を追加して、PayPal テスト環境に関数呼び出しを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="c3642-341">Add the Merchant API credentials (Username, Password, and Signature) that you displayed earlier in this tutorial so that you can make function calls to the PayPal testing environment.</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="c3642-342">このサンプル アプリケーションでは、資格情報を C# ファイル (.cs) に追加するだけです。</span><span class="sxs-lookup"><span data-stu-id="c3642-342">In this sample application you are simply adding credentials to a C# file (.cs).</span></span> <span data-ttu-id="c3642-343">ただし、実装されたソリューションでは、構成ファイルで資格情報を暗号化することを検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-343">However, in a implemented solution, you should consider encrypting your credentials in a configuration file.</span></span>

<span data-ttu-id="c3642-344">クラスには、ほとんどの機能が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c3642-344">The NVPAPICaller class contains the majority of the PayPal functionality.</span></span> <span data-ttu-id="c3642-345">クラスのコードは、PayPal テスト環境からテスト購入を行うために必要なメソッドを提供します。</span><span class="sxs-lookup"><span data-stu-id="c3642-345">The code in the class provides the methods needed to make a test purchase from the PayPal testing environment.</span></span> <span data-ttu-id="c3642-346">購入には、次の 3 つの PayPal 関数が使用されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-346">The following three PayPal functions are used to make purchases:</span></span>

- <span data-ttu-id="c3642-347">`SetExpressCheckout` 関数</span><span class="sxs-lookup"><span data-stu-id="c3642-347">`SetExpressCheckout` function</span></span>
- <span data-ttu-id="c3642-348">`GetExpressCheckoutDetails` 関数</span><span class="sxs-lookup"><span data-stu-id="c3642-348">`GetExpressCheckoutDetails` function</span></span>
- <span data-ttu-id="c3642-349">`DoExpressCheckoutPayment` 関数</span><span class="sxs-lookup"><span data-stu-id="c3642-349">`DoExpressCheckoutPayment` function</span></span>

<span data-ttu-id="c3642-350">この`ShortcutExpressCheckout`メソッドは、ショッピング カートからテスト購入情報と製品の詳細を収集し`SetExpressCheckout`、PayPal 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c3642-350">The `ShortcutExpressCheckout` method collects the test purchase information and product details from the shopping cart and calls the `SetExpressCheckout` PayPal function.</span></span> <span data-ttu-id="c3642-351">この`GetCheckoutDetails`メソッドは、購入の詳細を確認`GetExpressCheckoutDetails`し、テスト購入を行う前にPayPal関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c3642-351">The `GetCheckoutDetails` method confirms purchase details and calls the `GetExpressCheckoutDetails` PayPal function before making the test purchase.</span></span> <span data-ttu-id="c3642-352">この`DoCheckoutPayment`メソッドは、PayPal 関数を呼び出してテスト`DoExpressCheckoutPayment`環境からテスト購入を完了します。</span><span class="sxs-lookup"><span data-stu-id="c3642-352">The `DoCheckoutPayment` method completes the test purchase from the testing environment by calling the `DoExpressCheckoutPayment` PayPal function.</span></span> <span data-ttu-id="c3642-353">残りのコードは、文字列のエンコード、文字列のデコード、配列の処理、資格情報の決定など、PayPal のメソッドとプロセスをサポートします。</span><span class="sxs-lookup"><span data-stu-id="c3642-353">The remaining code supports the PayPal methods and process, such as encoding strings, decoding strings, processing arrays, and determining credentials.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c3642-354">PayPalでは[、PayPalのAPI仕様](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)に基づいてオプションの購入詳細を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="c3642-354">PayPal allows you to include optional purchase details based on [PayPal's API specification](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout).</span></span> <span data-ttu-id="c3642-355">Wingtip Toys サンプル アプリケーションでコードを拡張することで、ローカライズの詳細、製品の説明、税、顧客サービス番号、その他の多くのオプション フィールドを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="c3642-355">By extending the code in the Wingtip Toys sample application, you can include localization details, product descriptions, tax, a customer service number, as well as many other optional fields.</span></span>

<span data-ttu-id="c3642-356">**戻**りと取り消しメソッドで指定されている URL をキャンセルするポート番号を使用します。</span><span class="sxs-lookup"><span data-stu-id="c3642-356">Notice that the return and cancel URLs that are specified in the **ShortcutExpressCheckout** method use a port number.</span></span>

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

<span data-ttu-id="c3642-357">ビジュアル Web 開発者が SSL を使用して Web プロジェクトを実行する場合、通常はポート 44300 が Web サーバーに使用されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-357">When Visual Web Developer runs a web project using SSL, commonly the port 44300 is used for the web server.</span></span> <span data-ttu-id="c3642-358">上に示したように、ポート番号は 44300 です。</span><span class="sxs-lookup"><span data-stu-id="c3642-358">As shown above, the port number is 44300.</span></span> <span data-ttu-id="c3642-359">アプリケーションを実行すると、別のポート番号が表示される場合があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-359">When you run the application, you could see a different port number.</span></span> <span data-ttu-id="c3642-360">このチュートリアルの最後で Wingtip Toys サンプル アプリケーションを正常に実行できるように、ポート番号をコードで正しく設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-360">Your port number needs to be correctly set in the code so that you can successful run the Wingtip Toys sample application at the end of this tutorial.</span></span> <span data-ttu-id="c3642-361">このチュートリアルの次のセクションでは、ローカル ホストポート番号を取得し、PayPal クラスを更新する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="c3642-361">The next section of this tutorial explains how to retrieve the local host port number and update the PayPal class.</span></span>

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a><span data-ttu-id="c3642-362">PayPal クラスのローカルホスト ポート番号を更新します。</span><span class="sxs-lookup"><span data-stu-id="c3642-362">Update the LocalHost Port Number in the PayPal Class</span></span>

<span data-ttu-id="c3642-363">Wingtip Toys サンプル アプリケーションは、PayPal テスト サイトに移動し、Wingtip Toys サンプル アプリケーションのローカル インスタンスに戻って製品を購入します。</span><span class="sxs-lookup"><span data-stu-id="c3642-363">The Wingtip Toys sample application purchases products by navigating to the PayPal testing site and returning to your local instance of the Wingtip Toys sample application.</span></span> <span data-ttu-id="c3642-364">PayPal が正しい URL に戻るには、上記の PayPal コードでローカルで実行されているサンプル アプリケーションのポート番号を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-364">In order to have PayPal return to the correct URL, you need to specify the port number of the locally running sample application in the PayPal code mentioned above.</span></span>

1. <span data-ttu-id="c3642-365">**ソリューション エクスプローラ**でプロジェクト名 (**WingtipToys**) を右クリックし、[**プロパティ ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-365">Right-click the project name (**WingtipToys**) in **Solution Explorer** and select **Properties**.</span></span>
2. <span data-ttu-id="c3642-366">左側の列で **、[Web]** タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-366">In the left column, select the **Web** tab.</span></span>
3. <span data-ttu-id="c3642-367">**[プロジェクト URL]** ボックスからポート番号を取得します。</span><span class="sxs-lookup"><span data-stu-id="c3642-367">Retrieve the port number from the **Project Url** box.</span></span>
4. <span data-ttu-id="c3642-368">必要に応じて *、PayPalFunctions.cs*ファイルの PayPal`NVPAPICaller`クラス ( ) で、 web アプリケーションのポート番号を使用するように、`returnURL`を`cancelURL`更新します。</span><span class="sxs-lookup"><span data-stu-id="c3642-368">If needed, update the `returnURL` and `cancelURL` in the PayPal class (`NVPAPICaller`) in the *PayPalFunctions.cs* file to use the port number of your web application:</span></span>   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

<span data-ttu-id="c3642-369">これで、追加したコードが、ローカル Web アプリケーションの想定されるポートと一致します。</span><span class="sxs-lookup"><span data-stu-id="c3642-369">Now the code that you added will match the expected port for your local Web application.</span></span> <span data-ttu-id="c3642-370">PayPal は、ローカル コンピューター上の正しい URL に戻ることができるでしょう。</span><span class="sxs-lookup"><span data-stu-id="c3642-370">PayPal will be able to return to the correct URL on your local machine.</span></span>

### <a name="add-the-paypal-checkout-button"></a><span data-ttu-id="c3642-371">PayPal チェックアウト ボタンを追加する</span><span class="sxs-lookup"><span data-stu-id="c3642-371">Add the PayPal Checkout Button</span></span>

<span data-ttu-id="c3642-372">サンプル アプリケーションにプライマリ PayPal 関数が追加されましたので、これらの関数を呼び出すために必要なマークアップとコードの追加を開始できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-372">Now that the primary PayPal functions have been added to the sample application, you can begin adding the markup and code needed to call these functions.</span></span> <span data-ttu-id="c3642-373">まず、ショッピング カート ページにユーザーに表示されるチェックアウト ボタンを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-373">First, you must add the checkout button that the user will see on the shopping cart page.</span></span>

1. <span data-ttu-id="c3642-374">*ショッピングカート.aspx*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="c3642-374">Open the *ShoppingCart.aspx* file.</span></span>
2. <span data-ttu-id="c3642-375">ファイルの一番下までスクロールして、コメントを`<!--Checkout Placeholder -->`見つけます。</span><span class="sxs-lookup"><span data-stu-id="c3642-375">Scroll to the bottom of the file and find the `<!--Checkout Placeholder -->` comment.</span></span>
3. <span data-ttu-id="c3642-376">マークアップが次のように置`ImageButton`き換えられるように、コメントをコントロールに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-376">Replace the comment with an `ImageButton` control so that the mark up is replaced as follows:</span></span>  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. <span data-ttu-id="c3642-377">*ShoppingCart.aspx.cs*ファイルで、イベント`UpdateBtn_Click`ハンドラーがファイルの末尾に近づくと、イベント`CheckOutBtn_Click`ハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-377">In the *ShoppingCart.aspx.cs* file, after the `UpdateBtn_Click` event handler near the end of the file, add the `CheckOutBtn_Click` event handler:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. <span data-ttu-id="c3642-378">また *、ShoppingCart.aspx.cs*ファイルで、新しいイメージ`CheckoutBtn`ボタンが次のように参照されるように、 への参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-378">Also in the *ShoppingCart.aspx.cs* file, add a reference to the `CheckoutBtn`, so that the new image button is referenced as follows:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. <span data-ttu-id="c3642-379">変更を*ShoppingCart.aspx*ファイルと*ShoppingCart.aspx.cs*ファイルの両方に保存します。</span><span class="sxs-lookup"><span data-stu-id="c3642-379">Save your changes to both the *ShoppingCart.aspx* file and the *ShoppingCart.aspx.cs* file.</span></span>
7. <span data-ttu-id="c3642-380">メニューから[ビルド**Debug**-&gt;**ウィングヒントのデバッグ] を**選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-380">From the menu, select **Debug**-&gt;**Build WingtipToys**.</span></span>  
   <span data-ttu-id="c3642-381">プロジェクトは、新しく追加された**ImageButton**コントロールで再構築されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-381">The project will be rebuilt with the newly added **ImageButton** control.</span></span>

### <a name="send-purchase-details-to-paypal"></a><span data-ttu-id="c3642-382">購入の詳細を PayPal に送信する</span><span class="sxs-lookup"><span data-stu-id="c3642-382">Send Purchase Details to PayPal</span></span>

<span data-ttu-id="c3642-383">ユーザーがショッピング カート ページ (*ShoppingCart.aspx*) の **[チェックアウト**] ボタンをクリックすると、購入プロセスが開始されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-383">When the user clicks the **Checkout** button on the shopping cart page (*ShoppingCart.aspx*), they'll begin the purchase process.</span></span> <span data-ttu-id="c3642-384">次のコードは、製品の購入に必要な最初のPayPal関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="c3642-384">The following code calls the first PayPal function needed to purchase products.</span></span>

1. <span data-ttu-id="c3642-385">*チェックアウト*フォルダから *、CheckoutStart.aspx.cs*というコードビハインド ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="c3642-385">From the *Checkout* folder, open the code-behind file named *CheckoutStart.aspx.cs*.</span></span>   
   <span data-ttu-id="c3642-386">コードビハインド ファイルを開いてください。</span><span class="sxs-lookup"><span data-stu-id="c3642-386">Be sure to open the code-behind file.</span></span>
2. <span data-ttu-id="c3642-387">既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-387">Replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

<span data-ttu-id="c3642-388">アプリケーションのユーザーがショッピング カート ページの **[チェックアウト**] ボタンをクリックすると、ブラウザーは*CheckoutStart.aspx*ページに移動します。</span><span class="sxs-lookup"><span data-stu-id="c3642-388">When the user of the application clicks the **Checkout** button on the shopping cart page, the browser will navigate to the *CheckoutStart.aspx* page.</span></span> <span data-ttu-id="c3642-389">*ページ*が読み込まれると、メソッドが`ShortcutExpressCheckout`呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-389">When the *CheckoutStart.aspx* page loads, the `ShortcutExpressCheckout` method is called.</span></span> <span data-ttu-id="c3642-390">この時点で、ユーザーは PayPal テスト Web サイトに転送されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-390">At this point, the user is transferred to the PayPal testing web site.</span></span> <span data-ttu-id="c3642-391">PayPalサイトでは、ユーザーがPayPalの資格情報を入力し、購入の詳細を確認し、PayPal契約を受け入れ、メソッドが完了したWingtip Toys`ShortcutExpressCheckout`サンプルアプリケーションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="c3642-391">On the PayPal site, the user enters their PayPal credentials, reviews the purchase details, accepts the PayPal agreement and returns to the Wingtip Toys sample application where the `ShortcutExpressCheckout` method completes.</span></span> <span data-ttu-id="c3642-392">メソッドが`ShortcutExpressCheckout`完了すると、メソッドで指定された*CheckoutReview.aspx*ページにユーザーがリダイレクトされます`ShortcutExpressCheckout`。</span><span class="sxs-lookup"><span data-stu-id="c3642-392">When the `ShortcutExpressCheckout` method is complete, it will redirect the user to the *CheckoutReview.aspx* page specified in the `ShortcutExpressCheckout` method.</span></span> <span data-ttu-id="c3642-393">これにより、Wingtip Toys サンプル アプリケーション内から注文の詳細を確認できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-393">This allows the user to review the order details from within the Wingtip Toys sample application.</span></span>

### <a name="review-order-details"></a><span data-ttu-id="c3642-394">注文の詳細の確認</span><span class="sxs-lookup"><span data-stu-id="c3642-394">Review Order Details</span></span>

<span data-ttu-id="c3642-395">PayPal から戻った後、Wingtip Toys サンプル アプリケーションの*CheckoutReview.aspx*ページに注文の詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-395">After returning from PayPal, the *CheckoutReview.aspx* page of the Wingtip Toys sample application displays the order details.</span></span> <span data-ttu-id="c3642-396">このページでは、製品を購入する前に注文の詳細を確認できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-396">This page allows the user to review the order details before purchasing the products.</span></span> <span data-ttu-id="c3642-397">次のようにして *、CheckoutReview.aspx*ページを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-397">The *CheckoutReview.aspx* page must be created as follows:</span></span>

1. <span data-ttu-id="c3642-398">*チェックアウト*フォルダで *、"CheckoutReview.aspx"* という名前のページを開きます。</span><span class="sxs-lookup"><span data-stu-id="c3642-398">In the *Checkout* folder, open the page named *CheckoutReview.aspx*.</span></span>
2. <span data-ttu-id="c3642-399">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-399">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. <span data-ttu-id="c3642-400">CheckoutReview.aspx.csというコードビハインド ページ*を*開き、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-400">Open the code-behind page named *CheckoutReview.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

<span data-ttu-id="c3642-401">**DetailsView**コントロールは、PayPal から返された注文の詳細を表示するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-401">The **DetailsView** control is used to display the order details that have been returned from PayPal.</span></span> <span data-ttu-id="c3642-402">また、上記のコードでは、Wingtip Toys データベースに注文の詳細`OrderDetail`をオブジェクトとして保存します。</span><span class="sxs-lookup"><span data-stu-id="c3642-402">Also, the above code saves the order details to the Wingtip Toys database as an `OrderDetail` object.</span></span> <span data-ttu-id="c3642-403">ユーザーが [**完全な注文**] ボタンをクリックすると、ユーザーは *[チェックアウト完了.aspx]* ページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="c3642-403">When the user clicks on the **Complete Order** button, they are redirected to the *CheckoutComplete.aspx* page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c3642-404">**ヒント**</span><span class="sxs-lookup"><span data-stu-id="c3642-404">**Tip**</span></span>
> 
> <span data-ttu-id="c3642-405">*CheckoutReview.aspx*ページのマークアップでは、`<ItemStyle>`タグがページの下部にある**DetailsView**コントロール内の項目のスタイルを変更するために使用されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="c3642-405">In the markup of the *CheckoutReview.aspx* page, notice that the `<ItemStyle>` tag is used to change the style of the items within the **DetailsView** control near the bottom of the page.</span></span> <span data-ttu-id="c3642-406">**デザイン ビュー**でページを表示し (Visual Studio の左下隅にある **[デザイン**] を選択して) **DetailsView**コントロールを選択し、**スマート タグ**(コントロールの右上にある矢印アイコン) を選択すると **、DetailsView タスク**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-406">By viewing the page in **Design View** (by selecting **Design** at the lower left corner of Visual Studio), then selecting the **DetailsView** control, and selecting the **Smart Tag** (the arrow icon at the top right of the control), you will be able to see the **DetailsView Tasks**.</span></span>
> 
> ![PayPal でのチェックアウトと支払い - フィールドの編集](checkout-and-payment-with-paypal/_static/image18.png)
> 
> <span data-ttu-id="c3642-408">[**フィールドの編集**] を選択すると、[**フィールド**] ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-408">By selecting **Edit Fields**, the **Fields** dialog box will appear.</span></span> <span data-ttu-id="c3642-409">このダイアログ ボックスでは **、DetailsView**コントロールの表示プロパティ **(ItemStyle**など) を簡単に制御できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-409">In this dialog box you can easily control the visual properties, such as **ItemStyle**, of the **DetailsView** control.</span></span>
> 
> ![PayPal でのチェックアウトと支払い - フィールド ダイアログ](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a><span data-ttu-id="c3642-411">完全購入</span><span class="sxs-lookup"><span data-stu-id="c3642-411">Complete Purchase</span></span>

<span data-ttu-id="c3642-412">*チェックアウトコンプリート.aspx*ページは、ペイパルから購入を行います。</span><span class="sxs-lookup"><span data-stu-id="c3642-412">*CheckoutComplete.aspx* page makes the purchase from PayPal.</span></span> <span data-ttu-id="c3642-413">前述のように、アプリケーションが*CheckoutComplete.aspx*ページに移動する前に、ユーザーが **[完全な注文**] ボタンをクリックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-413">As mentioned above, the user must click on the **Complete Order** button before the application will navigate to the *CheckoutComplete.aspx* page.</span></span>

1. <span data-ttu-id="c3642-414">*[チェックアウト*] フォルダで、[*チェックアウト完了.aspx]* という名前のページを開きます。</span><span class="sxs-lookup"><span data-stu-id="c3642-414">In the *Checkout* folder, open the page named *CheckoutComplete.aspx*.</span></span>
2. <span data-ttu-id="c3642-415">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-415">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. <span data-ttu-id="c3642-416">*CheckoutComplete.aspx.cs*というコードビハインド ページを開き、既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-416">Open the code-behind page named *CheckoutComplete.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

<span data-ttu-id="c3642-417">*[チェックアウト完了.aspx]* ページが読み込`DoCheckoutPayment`まれると、メソッドが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-417">When the *CheckoutComplete.aspx* page is loaded, the `DoCheckoutPayment` method is called.</span></span> <span data-ttu-id="c3642-418">前述のとおり、この`DoCheckoutPayment`メソッドは PayPal テスト環境からの購入を完了します。</span><span class="sxs-lookup"><span data-stu-id="c3642-418">As mentioned earlier, the `DoCheckoutPayment` method completes the purchase from the PayPal testing environment.</span></span> <span data-ttu-id="c3642-419">PayPal が注文の購入を完了すると *、CheckoutComplete.aspx*ページには、購入者`ID`への支払いトランザクションが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-419">Once PayPal has completed the purchase of the order, the *CheckoutComplete.aspx* page displays a payment transaction `ID` to the purchaser.</span></span>

### <a name="handle-cancel-purchase"></a><span data-ttu-id="c3642-420">購入のキャンセルを処理する</span><span class="sxs-lookup"><span data-stu-id="c3642-420">Handle Cancel Purchase</span></span>

<span data-ttu-id="c3642-421">ユーザーが購入をキャンセルすると決定した場合、ユーザーは*CheckoutCancel.aspx*ページに移動し、注文がキャンセルされたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="c3642-421">If the user decides to cancel the purchase, they will be directed to the *CheckoutCancel.aspx* page where they will see that their order has been cancelled.</span></span>

1. <span data-ttu-id="c3642-422">チェックアウト*フォルダーで* *CheckoutCancel.aspx*という名前のページを開きます。</span><span class="sxs-lookup"><span data-stu-id="c3642-422">Open the page named *CheckoutCancel.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="c3642-423">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-423">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a><span data-ttu-id="c3642-424">購買エラーの処理</span><span class="sxs-lookup"><span data-stu-id="c3642-424">Handle Purchase Errors</span></span>

<span data-ttu-id="c3642-425">購入プロセス中のエラーは *、CheckoutError.aspx*ページによって処理されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-425">Errors during the purchase process will be handled by the *CheckoutError.aspx* page.</span></span> <span data-ttu-id="c3642-426">エラーが発生した場合は *、CheckoutStart.aspx*ページ *、CheckoutReview.aspx*ページ、および*チェックアウトコンプリート.aspx*ページの分離コードがそれぞれ*CheckoutError.aspx*ページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="c3642-426">The code-behind of the *CheckoutStart.aspx* page, the *CheckoutReview.aspx* page, and the *CheckoutComplete.aspx* page will each redirect to the *CheckoutError.aspx* page if an error occurs.</span></span>

1. <span data-ttu-id="c3642-427">チェックアウト*フォルダーで* *CheckoutError.aspx*という名前のページを開きます。</span><span class="sxs-lookup"><span data-stu-id="c3642-427">Open the page named *CheckoutError.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="c3642-428">既存のマークアップを次のように置き換えます。</span><span class="sxs-lookup"><span data-stu-id="c3642-428">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

<span data-ttu-id="c3642-429">*チェックアウト処理中に*エラーが発生すると、エラーの詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-429">The *CheckoutError.aspx* page is displayed with the error details when an error occurs during the checkout process.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="c3642-430">アプリケーションの実行</span><span class="sxs-lookup"><span data-stu-id="c3642-430">Running the Application</span></span>

<span data-ttu-id="c3642-431">アプリケーションを実行して、製品の購入方法を確認します。</span><span class="sxs-lookup"><span data-stu-id="c3642-431">Run the application to see how to purchase products.</span></span> <span data-ttu-id="c3642-432">PayPal テスト環境で実行されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="c3642-432">Note that you will be running in the PayPal testing environment.</span></span> <span data-ttu-id="c3642-433">実際のお金は交換されません。</span><span class="sxs-lookup"><span data-stu-id="c3642-433">No actual money is being exchanged.</span></span>

1. <span data-ttu-id="c3642-434">すべてのファイルが Visual Studio に保存されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c3642-434">Make sure all your files are saved in Visual Studio.</span></span>
2. <span data-ttu-id="c3642-435">Web ブラウザを開き、[https://developer.paypal.com](https://developer.paypal.com/)に移動します。</span><span class="sxs-lookup"><span data-stu-id="c3642-435">Open a Web browser and navigate to [https://developer.paypal.com](https://developer.paypal.com/).</span></span>
3. <span data-ttu-id="c3642-436">このチュートリアルで前に作成した PayPal 開発者アカウントでログインします。</span><span class="sxs-lookup"><span data-stu-id="c3642-436">Login with your PayPal developer account that you created earlier in this tutorial.</span></span>  
   <span data-ttu-id="c3642-437">PayPal の開発者サンドボックスでは、エクスプレスチェックアウトをテストするためにログイン[https://developer.paypal.com](https://developer.paypal.com/)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-437">For PayPal's developer sandbox, you need to be logged in at [https://developer.paypal.com](https://developer.paypal.com/) to test express checkout.</span></span> <span data-ttu-id="c3642-438">これは、PayPalのサンドボックステストにのみ適用され、PayPalのライブ環境には適用されません。</span><span class="sxs-lookup"><span data-stu-id="c3642-438">This only applies to PayPal's sandbox testing, not to PayPal's live environment.</span></span>
4. <span data-ttu-id="c3642-439">Visual Studio で**F5**キーを押して、Wingtip Toys サンプル アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="c3642-439">In Visual Studio, press **F5** to run the Wingtip Toys sample application.</span></span>  
   <span data-ttu-id="c3642-440">データベースの再構築後、ブラウザーが開き *、Default.aspx*ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-440">After the database rebuilds, the browser will open and show the *Default.aspx* page.</span></span>
5. <span data-ttu-id="c3642-441">"Cars" などの商品カテゴリを選択し、各商品の横にある [**カートに追加**] をクリックして、ショッピング カートに 3 つの異なる製品を追加します。</span><span class="sxs-lookup"><span data-stu-id="c3642-441">Add three different products to the shopping cart by selecting the product category, such as "Cars" and then clicking **Add to Cart** next to each product.</span></span>  
   <span data-ttu-id="c3642-442">ショッピング カートには、選択した商品が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-442">The shopping cart will display the product you have selected.</span></span>
6. <span data-ttu-id="c3642-443">PayPal**PayPal**ボタンをクリックしてチェックアウトします。</span><span class="sxs-lookup"><span data-stu-id="c3642-443">Click the **PayPal** button to checkout.</span></span> 

    ![PayPalでのチェックアウトと支払い - カート](checkout-and-payment-with-paypal/_static/image20.png)

   <span data-ttu-id="c3642-445">チェックアウトするには、Wingtip Toys サンプル アプリケーションのユーザー アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="c3642-445">Checking out will require that you have a user account for the Wingtip Toys sample application.</span></span>
7. <span data-ttu-id="c3642-446">ページの右側にある**Google**リンクをクリックして、既存のgmail.comメールアカウントでログインします。</span><span class="sxs-lookup"><span data-stu-id="c3642-446">Click the **Google** link on the right of the page to log in with an existing gmail.com email account.</span></span>  
   <span data-ttu-id="c3642-447">gmail.com アカウントがない場合は、[テスト](https://www.gmail.com/)目的で作成www.gmail.com。</span><span class="sxs-lookup"><span data-stu-id="c3642-447">If you do not have a gmail.com account, you can create one for testing purposes at [www.gmail.com](https://www.gmail.com/).</span></span> <span data-ttu-id="c3642-448">[登録] をクリックして、標準のローカル アカウントを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="c3642-448">You can also use a standard local account by clicking "Register".</span></span> 

    ![PayPalでのチェックアウトと支払い - ログイン](checkout-and-payment-with-paypal/_static/image21.png)
8. <span data-ttu-id="c3642-450">Gmail アカウントとパスワードでログインします。</span><span class="sxs-lookup"><span data-stu-id="c3642-450">Sign in with your gmail account and password.</span></span> 

    ![PayPal でのチェックアウトと支払い - Gmail サインイン](checkout-and-payment-with-paypal/_static/image22.png)
9. <span data-ttu-id="c3642-452">[**ログイン**] ボタンをクリックして、Gmail アカウントを Wingtip Toys サンプル アプリケーションのユーザー名で登録します。</span><span class="sxs-lookup"><span data-stu-id="c3642-452">Click the **Log in** button to register your gmail account with your Wingtip Toys sample application user name.</span></span> 

    ![PayPalでのチェックアウトと支払い - アカウント登録](checkout-and-payment-with-paypal/_static/image23.png)
10. <span data-ttu-id="c3642-454">PayPal テスト サイトで、このチュートリアルで前に作成した**購入者**の電子メール アドレスとパスワードを追加し、[**ログイン**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-454">On the PayPal test site, add your **buyer** email address and password that you created earlier in this tutorial, then click the **Log In** button.</span></span> 

    ![PayPal でのチェックアウトと支払い - ペイパル サインイン](checkout-and-payment-with-paypal/_static/image24.png)
11. <span data-ttu-id="c3642-456">PayPal ポリシーに同意し、[**同意して続行**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-456">Agree to the PayPal policy and click the **Agree and Continue** button.</span></span>  
    <span data-ttu-id="c3642-457">このページは、このPayPalアカウントを初めて使用する場合にのみ表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-457">Note that this page is only displayed the first time you use this PayPal account.</span></span> <span data-ttu-id="c3642-458">再び、これはテストアカウントであり、実際のお金は交換されません。</span><span class="sxs-lookup"><span data-stu-id="c3642-458">Again note that this is a test account, no real money is exchanged.</span></span> 

    ![ペイパルでのチェックアウトと支払い - ペイパルポリシー](checkout-and-payment-with-paypal/_static/image25.png)
12. <span data-ttu-id="c3642-460">PayPal テスト環境レビュー ページで注文情報を確認し、[**続行**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-460">Review the order information on the PayPal testing environment review page and click **Continue**.</span></span> 

    ![PayPal によるチェックアウトと支払い - レビュー情報](checkout-and-payment-with-paypal/_static/image26.png)
13. <span data-ttu-id="c3642-462">*[CheckoutReview.aspx]* ページで、注文金額を確認し、生成された送付先住所を表示します。</span><span class="sxs-lookup"><span data-stu-id="c3642-462">On the *CheckoutReview.aspx* page, verify the order amount and view the generated shipping address.</span></span> <span data-ttu-id="c3642-463">次に、[**注文の完了**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="c3642-463">Then, click the **Complete Order** button.</span></span> 

    ![PayPal によるチェックアウトと支払い - オーダーレビュー](checkout-and-payment-with-paypal/_static/image27.png)
14. <span data-ttu-id="c3642-465">**[チェックアウト完了.aspx]** ページが、支払トランザクション ID と共に表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-465">The **CheckoutComplete.aspx** page is displayed with a payment transaction ID.</span></span> 

    ![PayPal でのチェックアウトと支払い - チェックアウト完了](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a><span data-ttu-id="c3642-467">データベースの確認</span><span class="sxs-lookup"><span data-stu-id="c3642-467">Reviewing the Database</span></span>

<span data-ttu-id="c3642-468">アプリケーションの実行後に Wingtip Toys サンプル アプリケーション データベースで更新されたデータを確認すると、アプリケーションが製品の購入を正常に記録したことがわかります。</span><span class="sxs-lookup"><span data-stu-id="c3642-468">By reviewing the updated data in the Wingtip Toys sample application database after running the application, you can see that the application successfully recorded the purchase of the products.</span></span>

<span data-ttu-id="c3642-469">*Wingtiptoys.mdf*データベース ファイルに含まれるデータは、このチュートリアル シリーズで前述したように、**データベース エクスプローラー**ウィンドウ (Visual Studio の**サーバー エクスプローラー**ウィンドウ) を使用して検査できます。</span><span class="sxs-lookup"><span data-stu-id="c3642-469">You can inspect the data contained in the *Wingtiptoys.mdf* database file by using the **Database Explorer** window (**Server Explorer** window in Visual Studio) as you did earlier in this tutorial series.</span></span>

1. <span data-ttu-id="c3642-470">ブラウザ ウィンドウが開いている場合は、閉じます。</span><span class="sxs-lookup"><span data-stu-id="c3642-470">Close the browser window if it is still open.</span></span>
2. <span data-ttu-id="c3642-471">Visual Studio で、**ソリューション エクスプローラー**の上部にある **[すべてのファイルを表示**] アイコンを選択して、[アプリ**\_データ**] フォルダーを展開できるようにします。</span><span class="sxs-lookup"><span data-stu-id="c3642-471">In Visual Studio, select the **Show All Files** icon at the top of **Solution Explorer** to allow you to expand the **App\_Data** folder.</span></span>
3. <span data-ttu-id="c3642-472">**[アプリ\_データ**] フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="c3642-472">Expand the **App\_Data** folder.</span></span>  
 <span data-ttu-id="c3642-473">フォルダの **[すべてのファイルを表示]** アイコンを選択する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="c3642-473">You may need to select the **Show All Files** icon for the folder.</span></span>
4. <span data-ttu-id="c3642-474">*Wingtiptoys.mdf*データベース ファイルを右クリックし、[**開く**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-474">Right-click the *Wingtiptoys.mdf* database file and select **Open**.</span></span>  
    <span data-ttu-id="c3642-475">**サーバー エクスプローラ**が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-475">**Server Explorer** is displayed.</span></span>
5. <span data-ttu-id="c3642-476">**[テーブル]** フォルダーを展開します。</span><span class="sxs-lookup"><span data-stu-id="c3642-476">Expand the **Tables** folder.</span></span>
6. <span data-ttu-id="c3642-477">**[受注]** テーブルを右クリックし、[**テーブル データの表示**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-477">Right-click the **Orders**table and select **Show Table Data**.</span></span>  
 <span data-ttu-id="c3642-478">**[受注]** テーブルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-478">The **Orders** table is displayed.</span></span>
7. <span data-ttu-id="c3642-479">[**支払トランザクション ID]** 列を確認して、トランザクションが正常に終了したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="c3642-479">Review the **PaymentTransactionID** column to confirm successful transactions.</span></span> 

    ![PayPal でのチェックアウトと支払い - データベースの確認](checkout-and-payment-with-paypal/_static/image29.png)
8. <span data-ttu-id="c3642-481">**[受注]** テーブル ウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="c3642-481">Close the **Orders** table window.</span></span>
9. <span data-ttu-id="c3642-482">サーバー エクスプローラで **、OrderDetails**テーブルを右クリックし、[**テーブル データの表示**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-482">In the Server Explorer, right-click the **OrderDetails** table and select **Show Table Data**.</span></span>
10. <span data-ttu-id="c3642-483">`OrderId` **[受注明細]** テーブルの値と`Username`値を確認します。</span><span class="sxs-lookup"><span data-stu-id="c3642-483">Review the `OrderId` and `Username` values in the **OrderDetails** table.</span></span> <span data-ttu-id="c3642-484">これらの値は **、Orders** `OrderId`テーブル`Username`に含まれる値と 値と一致します。</span><span class="sxs-lookup"><span data-stu-id="c3642-484">Note that these values match the `OrderId` and `Username` values included in the **Orders** table.</span></span>
11. <span data-ttu-id="c3642-485">**[受注明細]** テーブル ウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="c3642-485">Close the **OrderDetails** table window.</span></span>
12. <span data-ttu-id="c3642-486">Wingtip Toys データベース ファイル (*Wingtiptoys.mdf*) を右クリックし、[**接続を閉じる**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c3642-486">Right-click the Wingtip Toys database file (*Wingtiptoys.mdf*) and select **Close Connection**.</span></span>
13. <span data-ttu-id="c3642-487">**[ソリューション エクスプローラー** ] ウィンドウが表示されない場合は、[**サーバー エクスプローラー** ] ウィンドウの下部にある [ソリューション**エクスプローラー** ] をクリックして、**ソリューション エクスプローラー**を再度表示します。</span><span class="sxs-lookup"><span data-stu-id="c3642-487">If you do not see the **Solution Explorer** window, click **Solution Explorer** at the bottom of the **Server Explorer** window to show the **Solution Explorer** again.</span></span>

## <a name="summary"></a><span data-ttu-id="c3642-488">まとめ</span><span class="sxs-lookup"><span data-stu-id="c3642-488">Summary</span></span>

<span data-ttu-id="c3642-489">このチュートリアルでは、注文と注文の詳細スキーマを追加して、製品の購入を追跡しました。</span><span class="sxs-lookup"><span data-stu-id="c3642-489">In this tutorial you added order and order detail schemas to track the purchase of products.</span></span> <span data-ttu-id="c3642-490">また、Wingtip Toys サンプル アプリケーションに PayPal 機能を統合しました。</span><span class="sxs-lookup"><span data-stu-id="c3642-490">You also integrated PayPal functionality into the Wingtip Toys sample application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c3642-491">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="c3642-491">Additional Resources</span></span>

<span data-ttu-id="c3642-492">[ASP.NET構成の概要](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="c3642-492">[ASP.NET Configuration Overview](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span></span>  
[<span data-ttu-id="c3642-493">Azure アプリ サービスにメンバーシップ、OAuth、および SQL データベースを使用してセキュリティで保護されたASP.NET Web フォーム アプリを展開する</span><span class="sxs-lookup"><span data-stu-id="c3642-493">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="c3642-494">マイクロソフト Azure - 無料試用版</span><span class="sxs-lookup"><span data-stu-id="c3642-494">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a><span data-ttu-id="c3642-495">免責事項</span><span class="sxs-lookup"><span data-stu-id="c3642-495">Disclaimer</span></span>

<span data-ttu-id="c3642-496">このチュートリアルには、サンプル コードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c3642-496">This tutorial contains sample code.</span></span> <span data-ttu-id="c3642-497">このようなサンプルコードは、いかなる種類の保証もなく「ありがち」に提供されます。</span><span class="sxs-lookup"><span data-stu-id="c3642-497">Such sample code is provided "as is" without warranty of any kind.</span></span> <span data-ttu-id="c3642-498">したがって、マイクロソフトは、サンプル コードの正確性、完全性、または品質を保証しません。</span><span class="sxs-lookup"><span data-stu-id="c3642-498">Accordingly, Microsoft does not guarantee the accuracy, integrity, or quality of the sample code.</span></span> <span data-ttu-id="c3642-499">お客様は、ご自身の責任でサンプルコードを使用することに同意します。</span><span class="sxs-lookup"><span data-stu-id="c3642-499">You agree to use the sample code at your own risk.</span></span> <span data-ttu-id="c3642-500">いかなる場合でも、サンプル コード、コンテンツ、サンプル コード、コンテンツ、またはサンプル コードの使用によって生じたあらゆる種類の損失または損害に関するエラーや欠落を含むが、これらに限定されないいかなる方法でも、Microsoft はユーザーに対して責任を負いません。</span><span class="sxs-lookup"><span data-stu-id="c3642-500">Under no circumstances will Microsoft be liable to you in any way for any sample code, content, including but not limited to, any errors or omissions in any sample code, content, or any loss or damage of any kind incurred as a result of the use of any sample code.</span></span> <span data-ttu-id="c3642-501">お客様は、ここに通知され、マイクロソフトがいかなる損失、損失の主張、傷害または損害の請求、その中に表明された見解を含むがこれらに限定されない、またはそれらに限定されないあらゆる種類の損害に対して無害にマイクロソフトを補償、保存、保持することに同意します。</span><span class="sxs-lookup"><span data-stu-id="c3642-501">You are hereby notified and do hereby agree to indemnify, save and hold Microsoft harmless from and against any and all loss, claims of loss, injury or damage of any kind including, without limitation, those occasioned by or arising from material that you post, transmit, use or rely on including, but not limited to, the views expressed therein.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c3642-502">[前へ](shopping-cart.md)
> [次へ](membership-and-administration.md)</span><span class="sxs-lookup"><span data-stu-id="c3642-502">[Previous](shopping-cart.md)
[Next](membership-and-administration.md)</span></span>
