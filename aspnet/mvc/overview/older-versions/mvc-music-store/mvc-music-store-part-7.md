---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: 第 7 部:メンバーシップと承認 |Microsoft Docs
author: jongalloway
description: このチュートリアル シリーズでは、すべての ASP.NET MVC のミュージック ストア サンプル アプリケーションをビルドする手順について説明します。 第 7 部では、メンバーシップと承認について説明します。
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65112469"
---
# <a name="part-7-membership-and-authorization"></a><span data-ttu-id="20db1-104">第 7 部:メンバーシップと承認</span><span class="sxs-lookup"><span data-stu-id="20db1-104">Part 7: Membership and Authorization</span></span>

<span data-ttu-id="20db1-105">[Jon Galloway](https://github.com/jongalloway) による</span><span class="sxs-lookup"><span data-stu-id="20db1-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="20db1-106">MVC のミュージック ストアは、チュートリアル アプリケーションを紹介し、web 開発用の ASP.NET MVC と Visual Studio を使用する方法をステップ バイ ステップについて説明します。</span><span class="sxs-lookup"><span data-stu-id="20db1-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="20db1-107">MVC のミュージック ストアは、オンラインで音楽のアルバムを販売し、基本的なサイトの管理、ユーザー サインインし、買い物カゴの機能を実装する軽量サンプル ストア実装です。</span><span class="sxs-lookup"><span data-stu-id="20db1-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="20db1-108">このチュートリアル シリーズでは、すべての ASP.NET MVC のミュージック ストア サンプル アプリケーションをビルドする手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="20db1-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="20db1-109">第 7 部では、メンバーシップと承認について説明します。</span><span class="sxs-lookup"><span data-stu-id="20db1-109">Part 7 covers Membership and Authorization.</span></span>

<span data-ttu-id="20db1-110">ストア マネージャー コント ローラーは、サイトにアクセスしてすべてのユーザーに現在アクセスできません。</span><span class="sxs-lookup"><span data-stu-id="20db1-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="20db1-111">サイト管理者に権限を制限するこれを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="20db1-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="20db1-112">AccountController とビューの追加</span><span class="sxs-lookup"><span data-stu-id="20db1-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="20db1-113">完全な ASP.NET MVC 3 Web アプリケーション テンプレートと、ASP.NET MVC 3 空 Web アプリケーション テンプレートの 1 つの違いは、空のテンプレートには、アカウントのコント ローラーは含まれません。</span><span class="sxs-lookup"><span data-stu-id="20db1-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="20db1-114">完全な ASP.NET MVC 3 Web アプリケーション テンプレートから作成された新しい ASP.NET MVC アプリケーションからいくつかのファイルをコピーして、アカウント コント ローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="20db1-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="20db1-115">完全な ASP.NET MVC 3 Web アプリケーション テンプレートを使用して、新しい ASP.NET MVC アプリケーションを作成し、次のファイルをプロジェクト内の同じディレクトリにコピーします。</span><span class="sxs-lookup"><span data-stu-id="20db1-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="20db1-116">コント ローラーのディレクトリにコピー AccountController.cs</span><span class="sxs-lookup"><span data-stu-id="20db1-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="20db1-117">モデルのディレクトリにコピー AccountModels</span><span class="sxs-lookup"><span data-stu-id="20db1-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="20db1-118">Views ディレクトリ内のアカウント ディレクトリを作成し、4 つすべてのビューをコピー</span><span class="sxs-lookup"><span data-stu-id="20db1-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="20db1-119">MvcMusicStore で開始するために、コント ローラーとモデルのクラスの名前空間を変更します。</span><span class="sxs-lookup"><span data-stu-id="20db1-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="20db1-120">AccountController クラスは MvcMusicStore.Controllers 名前空間を使用する必要があり、AccountModels クラス MvcMusicStore.Models 名前空間を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="20db1-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

<span data-ttu-id="20db1-121">*注:これらのファイルでは、チュートリアルの先頭に、サイト設計のファイルをコピーした MvcMusicStore Assets.zip ダウンロードで入手できます。メンバーシップのファイルは、Code ディレクトリにあります。*</span><span class="sxs-lookup"><span data-stu-id="20db1-121">*Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial. The Membership files are located in the Code directory.*</span></span>

<span data-ttu-id="20db1-122">更新されたソリューションは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="20db1-122">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="20db1-123">ASP.NET の構成サイトを持つ管理ユーザーを追加します。</span><span class="sxs-lookup"><span data-stu-id="20db1-123">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="20db1-124">Web サイトで承認を要求する、前にアクセス権を持つユーザーを作成する必要になります。</span><span class="sxs-lookup"><span data-stu-id="20db1-124">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="20db1-125">ユーザーを作成する最も簡単な方法では、組み込みの ASP.NET の構成 web サイトを使用します。</span><span class="sxs-lookup"><span data-stu-id="20db1-125">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="20db1-126">次のソリューション エクスプ ローラーで、アイコンをクリックして、ASP.NET の構成 web サイトを起動します。</span><span class="sxs-lookup"><span data-stu-id="20db1-126">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="20db1-127">これは、構成の web サイトを起動します。</span><span class="sxs-lookup"><span data-stu-id="20db1-127">This launches a configuration website.</span></span> <span data-ttu-id="20db1-128">[ホーム画面で、[セキュリティ] タブをクリックし、画面の中央に"ロールを有効にする] リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="20db1-128">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="20db1-129">「ロールの作成または管理」リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="20db1-129">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="20db1-130">ロール名として"Administrator"を入力し、[役割の追加] ボタンを押します。</span><span class="sxs-lookup"><span data-stu-id="20db1-130">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="20db1-131">戻る ボタンをクリックし、左側にあるユーザーの作成リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="20db1-131">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="20db1-132">左側の次の情報を使用してユーザー情報フィールドに入力します。</span><span class="sxs-lookup"><span data-stu-id="20db1-132">Fill in the user information fields on the left using the following information:</span></span>

| <span data-ttu-id="20db1-133">**フィールド**</span><span class="sxs-lookup"><span data-stu-id="20db1-133">**Field**</span></span> | <span data-ttu-id="20db1-134">**[値]**</span><span class="sxs-lookup"><span data-stu-id="20db1-134">**Value**</span></span> |
| --- | --- |
| <span data-ttu-id="20db1-135">**ユーザー名**</span><span class="sxs-lookup"><span data-stu-id="20db1-135">**User Name**</span></span> | <span data-ttu-id="20db1-136">管理者</span><span class="sxs-lookup"><span data-stu-id="20db1-136">Administrator</span></span> |
| <span data-ttu-id="20db1-137">**パスワード**</span><span class="sxs-lookup"><span data-stu-id="20db1-137">**Password**</span></span> | <span data-ttu-id="20db1-138">password123!</span><span class="sxs-lookup"><span data-stu-id="20db1-138">password123!</span></span> |
| <span data-ttu-id="20db1-139">**パスワードの確認入力**</span><span class="sxs-lookup"><span data-stu-id="20db1-139">**Confirm Password**</span></span> | <span data-ttu-id="20db1-140">password123!</span><span class="sxs-lookup"><span data-stu-id="20db1-140">password123!</span></span> |
| <span data-ttu-id="20db1-141">**電子メール**</span><span class="sxs-lookup"><span data-stu-id="20db1-141">**E-mail**</span></span> | <span data-ttu-id="20db1-142">(任意の電子メール アドレスは機能)</span><span class="sxs-lookup"><span data-stu-id="20db1-142">(any email address will work)</span></span> |
| <span data-ttu-id="20db1-143">**セキュリティの質問**</span><span class="sxs-lookup"><span data-stu-id="20db1-143">**Security Question**</span></span> | <span data-ttu-id="20db1-144">(好き)</span><span class="sxs-lookup"><span data-stu-id="20db1-144">(whatever you like)</span></span> |
| <span data-ttu-id="20db1-145">**セキュリティ返答**</span><span class="sxs-lookup"><span data-stu-id="20db1-145">**Security Answer**</span></span> | <span data-ttu-id="20db1-146">(好き)</span><span class="sxs-lookup"><span data-stu-id="20db1-146">(whatever you like)</span></span> |

<span data-ttu-id="20db1-147">*注:もちろん、たい任意のパスワードを使用できます。既定のパスワード セキュリティ設定が必要なパスワードは 7 文字の長さを 1 つの英数字以外の文字が含まれています。*</span><span class="sxs-lookup"><span data-stu-id="20db1-147">*Note: You can of course use any password you'd like. The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.*</span></span>

<span data-ttu-id="20db1-148">このユーザーの管理者ロールを選択し、ユーザーの作成 ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="20db1-148">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="20db1-149">この時点では、ユーザーが正常に作成されたことを示すメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="20db1-149">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="20db1-150">ブラウザー ウィンドウを閉じることができますようになりました。</span><span class="sxs-lookup"><span data-stu-id="20db1-150">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="20db1-151">ロール ベースの承認</span><span class="sxs-lookup"><span data-stu-id="20db1-151">Role-based Authorization</span></span>

<span data-ttu-id="20db1-152">ユーザーが、クラス内のコント ローラー アクションにアクセスする管理者ロールである必要がありますを指定する [Authorize] 属性を使用して StoreManagerController にアクセスを制限できることです。</span><span class="sxs-lookup"><span data-stu-id="20db1-152">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

<span data-ttu-id="20db1-153">*注:[Authorize] 属性は、特定のアクション メソッドをおよびコント ローラーのクラス レベルで配置できます。*</span><span class="sxs-lookup"><span data-stu-id="20db1-153">*Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.*</span></span>

<span data-ttu-id="20db1-154">ログオン ダイアログ/StoreManager を今すぐ参照が表示されます。</span><span class="sxs-lookup"><span data-stu-id="20db1-154">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="20db1-155">後、新しい管理者アカウントでログオンする前に、とアルバムの編集画面に移動することができました。</span><span class="sxs-lookup"><span data-stu-id="20db1-155">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="20db1-156">[前へ](mvc-music-store-part-6.md)
> [次へ](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="20db1-156">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>
