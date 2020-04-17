---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 認証と承認を使用したアプリケーションのセキュリティ保護 |マイクロソフトドキュメント
author: rick-anderson
description: ステップ 9 では、NerdDinner アプリケーションをセキュリティで保護するための認証と承認を追加する方法を示しています。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d96f2763f6e62f9dd599fdb7977a97993d218305
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542574"
---
# <a name="secure-applications-using-authentication-and-authorization"></a><span data-ttu-id="2cb9a-103">認証と承認を利用した安全なアプリケーション</span><span class="sxs-lookup"><span data-stu-id="2cb9a-103">Secure Applications Using Authentication and Authorization</span></span>

<span data-ttu-id="2cb9a-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2cb9a-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="2cb9a-105">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="2cb9a-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="2cb9a-106">これは、mvc 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NET手順 9 です。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-106">This is step 9 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="2cb9a-107">手順 9 では、NerdDinner アプリケーションをセキュリティで保護するための認証と承認を追加する方法を示し、ユーザーが登録してサイトにログインして新しいディナーを作成する必要があり、ディナーをホストしているユーザーだけが後で編集できるようにします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-107">Step 9 shows how to add authentication and authorization to secure our NerdDinner application, so that users need to register and login to the site to create new dinners, and only the user who is hosting a dinner can edit it later.</span></span>
> 
> <span data-ttu-id="2cb9a-108">mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-9-authentication-and-authorization"></a><span data-ttu-id="2cb9a-109">NerdDinner ステップ 9: 認証と承認</span><span class="sxs-lookup"><span data-stu-id="2cb9a-109">NerdDinner Step 9: Authentication and Authorization</span></span>

<span data-ttu-id="2cb9a-110">今私たちのNerdDinnerアプリケーションは、任意の夕食の詳細を作成し、編集するサイトを訪問する人を付与します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-110">Right now our NerdDinner application grants anyone visiting the site the ability to create and edit the details of any dinner.</span></span> <span data-ttu-id="2cb9a-111">ユーザーが登録してサイトにログインして新しいディナーを作成し、ディナーをホストしているユーザーだけが後で編集できるように制限を追加するように、これを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-111">Let's change this so that users need to register and login to the site to create new dinners, and add a restriction so that only the user who is hosting a dinner can edit it later.</span></span>

<span data-ttu-id="2cb9a-112">これを有効にするには、認証と承認を使用してアプリケーションを保護します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-112">To enable this we'll use authentication and authorization to secure our application.</span></span>

### <a name="understanding-authentication-and-authorization"></a><span data-ttu-id="2cb9a-113">認証と承認について</span><span class="sxs-lookup"><span data-stu-id="2cb9a-113">Understanding Authentication and Authorization</span></span>

<span data-ttu-id="2cb9a-114">*認証*とは、アプリケーションにアクセスするクライアントの ID を識別して検証するプロセスです。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-114">*Authentication* is the process of identifying and validating the identity of a client accessing an application.</span></span> <span data-ttu-id="2cb9a-115">より簡単に言えば、エンドユーザーがウェブサイトを訪れたときに「誰」であるかを特定することです。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-115">Put more simply, it is about identifying "who" the end-user is when they visit a website.</span></span> <span data-ttu-id="2cb9a-116">ASP.NETは、ブラウザーユーザーを認証する複数の方法をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-116">ASP.NET supports multiple ways to authenticate browser users.</span></span> <span data-ttu-id="2cb9a-117">インターネット Web アプリケーションの場合、最も一般的な認証方法は"フォーム認証" と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-117">For Internet web applications, the most common authentication approach used is called "Forms Authentication".</span></span> <span data-ttu-id="2cb9a-118">フォーム認証を使用すると、開発者はアプリケーション内で HTML ログイン フォームを作成し、エンド ユーザーが送信するユーザー名とパスワードをデータベースやその他のパスワード資格情報ストアに照らして検証できます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-118">Forms Authentication enables a developer to author an HTML login form within their application, and then validate the username/password an end-user submits against a database or other password credential store.</span></span> <span data-ttu-id="2cb9a-119">ユーザー名とパスワードの組み合わせが正しい場合、開発者はASP.NETに、暗号化された HTTP Cookie を発行して、将来の要求を超えてユーザーを識別するように依頼できます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-119">If the username/password combination is correct, the developer can then ask ASP.NET to issue an encrypted HTTP cookie to identify the user across future requests.</span></span> <span data-ttu-id="2cb9a-120">NerdDinner アプリケーションでは、フォーム認証を使用します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-120">We'll by using forms authentication with our NerdDinner application.</span></span>

<span data-ttu-id="2cb9a-121">*承認*とは、認証されたユーザーが特定の URL/リソースにアクセスする権限を持っているかどうか、または何らかのアクションを実行する権限を持っているかどうかを判断するプロセスです。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-121">*Authorization* is the process of determining whether an authenticated user has permission to access a particular URL/resource or to perform some action.</span></span> <span data-ttu-id="2cb9a-122">たとえば、NerdDinner アプリケーションでは、ログインしているユーザーのみが */Dinners/CREATE* URL にアクセスし、新しいディナーを作成することを承認します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-122">For example, within our NerdDinner application we'll want to authorize that only users who are logged in can access the */Dinners/Create* URL and create new Dinners.</span></span> <span data-ttu-id="2cb9a-123">また、ディナーをホストしているユーザーだけが編集できるように承認ロジックを追加し、他のすべてのユーザーに対する編集アクセスを拒否することもできます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-123">We'll also want to add authorization logic so that only the user who is hosting a dinner can edit it – and deny edit access to all other users.</span></span>

### <a name="forms-authentication-and-the-accountcontroller"></a><span data-ttu-id="2cb9a-124">フォーム認証とアカウント コントローラー</span><span class="sxs-lookup"><span data-stu-id="2cb9a-124">Forms Authentication and the AccountController</span></span>

<span data-ttu-id="2cb9a-125">ASP.NET MVC の既定の Visual Studio プロジェクト テンプレートは、新しいASP.NET MVC アプリケーションが作成されたときに自動的にフォーム認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-125">The default Visual Studio project template for ASP.NET MVC automatically enables forms authentication when new ASP.NET MVC applications are created.</span></span> <span data-ttu-id="2cb9a-126">また、事前に作成されたアカウントログインページの実装がプロジェクトに自動的に追加され、サイト内のセキュリティを簡単に統合できます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-126">It also automatically adds a pre-built account login page implementation to the project – which makes it really easy to integrate security within a site.</span></span>

<span data-ttu-id="2cb9a-127">既定の Site.master マスター ページには、アクセスするユーザーが認証されていない場合、サイトの右上に "ログオン" リンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-127">The default Site.master master page displays a "Log On" link at the top-right of the site when the user accessing it is not authenticated:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

<span data-ttu-id="2cb9a-128">[ログオン] リンクをクリックすると、ユーザーは */アカウント/ログオン*URL に移動します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-128">Clicking the "Log On" link takes a user to the */Account/LogOn* URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

<span data-ttu-id="2cb9a-129">登録していない訪問者は *、"* 登録" リンクをクリックして登録できます 。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-129">Visitors who haven't registered can do so by clicking the "Register" link – which will take them to the */Account/Register* URL and allow them to enter account details:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

<span data-ttu-id="2cb9a-130">[登録] ボタンをクリックすると、ASP.NET メンバーシップ システム内に新しいユーザーが作成され、フォーム認証を使用してサイトにユーザーを認証します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-130">Clicking the "Register" button will create a new user within the ASP.NET Membership system, and authenticate the user onto the site using forms authentication.</span></span>

<span data-ttu-id="2cb9a-131">ユーザーがログインすると、Site.master はページの右上を変更して"ようこそ [ユーザー名]" を出力します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-131">When a user is logged-in, the Site.master changes the top-right of the page to output a "Welcome [username]!"</span></span> <span data-ttu-id="2cb9a-132">メッセージを表示し、"ログオン" リンクではなく "ログオフ" リンクをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-132">message and renders a "Log Off" link instead of a "Log On" one.</span></span> <span data-ttu-id="2cb9a-133">[ログオフ] リンクをクリックすると、ユーザーがログアウトします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-133">Clicking the "Log Off" link logs out the user:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

<span data-ttu-id="2cb9a-134">上記のログイン、ログアウト、および登録の機能は、プロジェクトの作成時に Visual Studio によってプロジェクトに追加された AccountController クラス内に実装されています。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-134">The above login, logout, and registration functionality is implemented within the AccountController class that was added to our project by Visual Studio when it created the project.</span></span> <span data-ttu-id="2cb9a-135">アカウント コント ローラーの UI は、\ビュー\アカウント ディレクトリ内のビュー テンプレートを使用して実装されます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-135">The UI for the AccountController is implemented using view templates within the \Views\Account directory:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

<span data-ttu-id="2cb9a-136">クラスは、ASP.NETフォーム認証システムを使用して暗号化認証クッキーを発行し、ASP.NETメンバーシップAPIを使用してユーザー名/パスワードを保存および検証します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-136">The AccountController class uses the ASP.NET Forms Authentication system to issue encrypted authentication cookies, and the ASP.NET Membership API to store and validate usernames/passwords.</span></span> <span data-ttu-id="2cb9a-137">ASP.NET メンバーシップ API は拡張可能で、任意のパスワード資格情報ストアを使用できます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-137">The ASP.NET Membership API is extensible and enables any password credential store to be used.</span></span> <span data-ttu-id="2cb9a-138">ASP.NETには、SQL データベース内または Active Directory 内にユーザー名とパスワードを格納する組み込みのメンバーシップ プロバイダー実装が付属しています。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-138">ASP.NET ships with built-in membership provider implementations that store username/passwords within a SQL database, or within Active Directory.</span></span>

<span data-ttu-id="2cb9a-139">NerdDinner アプリケーションが使用するメンバーシップ プロバイダを構成するには、プロジェクトのルートにある "web.config" ファイルを開き、その&lt;中&gt;のメンバーシップ セクションを探します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-139">We can configure which membership provider our NerdDinner application should use by opening the "web.config" file at the root of the project and looking for the &lt;membership&gt; section within it.</span></span> <span data-ttu-id="2cb9a-140">プロジェクトの作成時に追加された既定の web.config SQL メンバーシップ プロバイダーを登録し、データベースの場所を指定するのには "ApplicationServices" という名前の接続文字列を使用するように構成します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-140">The default web.config added when the project was created registers the SQL membership provider, and configures it to use a connection-string named "ApplicationServices" to specify the database location.</span></span>

<span data-ttu-id="2cb9a-141">既定の "アプリケーション サービス" 接続文字列 (web.config ファイルの&lt;接続文字列&gt;セクションで指定) は、SQL Express を使用するように構成されています。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-141">The default "ApplicationServices" connection string (which is specified within the &lt;connectionStrings&gt; section of the web.config file) is configured to use SQL Express.</span></span> <span data-ttu-id="2cb9a-142">これは、"ASPNETDB" という名前の SQL Express データベースを指しています。MDF" アプリケーションの 「アプリ\_データ」 ディレクトリの下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-142">It points to a SQL Express database named "ASPNETDB.MDF" under the application's "App\_Data" directory.</span></span> <span data-ttu-id="2cb9a-143">アプリケーション内で初めて Membership API を使用するときにこのデータベースが存在しない場合、ASP.NETは自動的にデータベースを作成し、適切なメンバーシップ データベース スキーマをその中にプロビジョニングします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-143">If this database doesn't exist the first time the Membership API is used within the application, ASP.NET will automatically create the database and provision the appropriate membership database schema within it:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

<span data-ttu-id="2cb9a-144">SQL Express を使用する代わりに、完全な SQL Server インスタンスを使用する (またはリモート データベースに接続する) 場合は、web.config ファイル内の "ApplicationServices" 接続文字列を更新し、適切なメンバーシップ スキーマがデータベースに追加されていることを確認するだけです。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-144">If instead of using SQL Express we wanted to use a full SQL Server instance (or connect to a remote database), all we'd need to-do is to update the "ApplicationServices" connection string within the web.config file and make sure that the appropriate membership schema has been added to the database it points at.</span></span> <span data-ttu-id="2cb9a-145">\Windows\Microsoft.NET\Framework\v2.0.50727\ ディレクトリ内で "aspnet\_regsql.exe" ユーティリティを実行すると、メンバーシップやその他のASP.NETアプリケーション サービスに対する適切なスキーマをデータベースに追加できます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-145">You can run the "aspnet\_regsql.exe" utility within the \Windows\Microsoft.NET\Framework\v2.0.50727\ directory to add the appropriate schema for membership and the other ASP.NET application services to a database.</span></span>

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a><span data-ttu-id="2cb9a-146">[承認] フィルターを使用して 、/ディナー/URL の作成を承認します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-146">Authorizing the /Dinners/Create URL using the [Authorize] filter</span></span>

<span data-ttu-id="2cb9a-147">NerdDinner アプリケーションの安全な認証とアカウント管理の実装を有効にするコードを記述する必要はありませんでした。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-147">We didn't have to write any code to enable a secure authentication and account management implementation for the NerdDinner application.</span></span> <span data-ttu-id="2cb9a-148">ユーザーは、当社のアプリケーションに新しいアカウントを登録し、サイトのログイン/ログアウトを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-148">Users can register new accounts with our application, and login/logout of the site.</span></span>

<span data-ttu-id="2cb9a-149">これで、承認ロジックをアプリケーションに追加し、訪問者の認証ステータスとユーザー名を使用して、サイト内で何ができるか、またはできないかを制御できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-149">Now we can add authorization logic to the application, and use the authentication status and username of visitors to control what they can and can't do within the site.</span></span> <span data-ttu-id="2cb9a-150">まず、DinnersController クラスの "作成" アクション メソッドに承認ロジックを追加します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-150">Let's begin by adding authorization logic to the "Create" action methods of our DinnersController class.</span></span> <span data-ttu-id="2cb9a-151">具体的には *、/Dinners/CREATE* URL にアクセスするユーザーがログインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-151">Specifically, we will require that users accessing the */Dinners/Create* URL must be logged in.</span></span> <span data-ttu-id="2cb9a-152">ログインしていない場合は、ログインページにリダイレクトしてログインできるようにします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-152">If they aren't logged in we'll redirect them to the login page so that they can sign-in.</span></span>

<span data-ttu-id="2cb9a-153">このロジックを実装するのは非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-153">Implementing this logic is pretty easy.</span></span> <span data-ttu-id="2cb9a-154">必要なのは、次のように Create アクション メソッドに [Authorize] フィルター属性を追加することだけです。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-154">All we need to-do is to add an [Authorize] filter attribute to our Create action methods like so:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

<span data-ttu-id="2cb9a-155">ASP.NET MVC では、アクション メソッドに宣言的に適用できる再使用できるロジックを実装するために使用できる "アクション フィルター" を作成する機能がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-155">ASP.NET MVC supports the ability to create "action filters" that can be used to implement re-usable logic that can be declaratively applied to action methods.</span></span> <span data-ttu-id="2cb9a-156">[Authorize] フィルターは、ASP.NET MVC によって提供される組み込みのアクション フィルターの 1 つであり、開発者がアクション メソッドとコント ローラー クラスに承認規則を宣言的に適用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-156">The [Authorize] filter is one of the built-in action filters provided by ASP.NET MVC, and it enables a developer to declaratively apply authorization rules to action methods and controller classes.</span></span>

<span data-ttu-id="2cb9a-157">上記のようなパラメータを指定せずに適用すると、[Authorize] フィルタはアクションメソッドリクエストを行うユーザーがログインする必要があることを強制し、ログインURLが存在しない場合は自動的にブラウザをリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-157">When applied without any parameters (like above) the [Authorize] filter enforces that the user making the action method request must be logged in – and it will automatically redirect the browser to the login URL if they aren't.</span></span> <span data-ttu-id="2cb9a-158">このリダイレクトを行うとき、最初に要求された URL はクエリ文字列引数として渡されます (たとえば、/Account/LogOn?を返します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-158">When doing this redirect the originally requested URL is passed as a querystring argument (for example: /Account/LogOn?ReturnUrl=%2fDinners%2fCreate).</span></span> <span data-ttu-id="2cb9a-159">アカウント コント ローラーは、ユーザーがログインすると、最初に要求された URL にリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-159">The AccountController will then redirect the user back to the originally requested URL once they login.</span></span>

<span data-ttu-id="2cb9a-160">[Authorize] フィルターは、ユーザーがログインし、許可されたユーザーの一覧または許可されたセキュリティ ロールのメンバーの両方に含まれるようにするために使用できる "ユーザー" または "ロール" プロパティを指定する機能をオプションでサポートします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-160">The [Authorize] filter optionally supports the ability to specify a "Users" or "Roles" property that can be used to require that the user is both logged in and within a list of allowed users or a member of an allowed security role.</span></span> <span data-ttu-id="2cb9a-161">たとえば、次のコードでは、"scottgu" と "billg" の 2 人の特定のユーザーのみが /Dinners/CREATE URL にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-161">For example, the code below only allows two specific users, "scottgu" and "billg", to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

<span data-ttu-id="2cb9a-162">特定のユーザー名をコードに埋め込むと、保守が容易にできない傾向があります。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-162">Embedding specific user names within code tends to be pretty un-maintainable though.</span></span> <span data-ttu-id="2cb9a-163">より良い方法は、コードがチェックする上位レベルの "ロール" を定義し、データベースまたはアクティブディレクトリ システムを使用してユーザーをロールにマップすることです (実際のユーザー マッピング リストをコードから外部に格納できるようにします)。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-163">A better approach is to define higher-level "roles" that the code checks against, and then to map users into the role using either a database or active directory system (enabling the actual user mapping list to be stored externally from the code).</span></span> <span data-ttu-id="2cb9a-164">ASP.NETには、組み込みのロール管理 API と、このユーザー/ロール マッピングの実行に役立つロール プロバイダー (SQL および Active Directory 用のロール プロバイダーを含む) の組み込みセットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-164">ASP.NET includes a built-in role management API as well as a built-in set of role providers (including ones for SQL and Active Directory) that can help perform this user/role mapping.</span></span> <span data-ttu-id="2cb9a-165">次に、特定の 「管理者」ロール内のユーザーのみが /Dinners/CREATE URL にアクセスできるようにコードを更新できます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-165">We could then update the code to only allow users within a specific "admin" role to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a><span data-ttu-id="2cb9a-166">ディナー作成時にUser.Identity.Nameプロパティを使用する</span><span class="sxs-lookup"><span data-stu-id="2cb9a-166">Using the User.Identity.Name property when Creating Dinners</span></span>

<span data-ttu-id="2cb9a-167">Controller 基本クラスで公開されるUser.Identity.Nameプロパティを使用して、現在ログインしている要求のユーザーのユーザー名を取得できます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-167">We can retrieve the username of the currently logged-in user of a request using the User.Identity.Name property exposed on the Controller base class.</span></span>

<span data-ttu-id="2cb9a-168">以前は、Create() アクションメソッドの HTTP-POST バージョンを実装したときに、Dinner の "HostedBy" プロパティを静的な文字列にハードコーディングしていました。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-168">Earlier when we implemented the HTTP-POST version of our Create() action method we had hardcoded the "HostedBy" property of the Dinner to a static string.</span></span> <span data-ttu-id="2cb9a-169">このコードを更新して、User.Identity.Nameプロパティを使用したり、Dinner を作成するホスト用に RSVP を自動的に追加したりできます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-169">We can now update this code to instead use the User.Identity.Name property, as well as automatically add an RSVP for the host creating the Dinner:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

<span data-ttu-id="2cb9a-170">Create() メソッドに [Authorize] 属性を追加したので、ASP.NET MVC は、/Dinners/Create URL にアクセスするユーザーがサイトにログインしている場合にのみアクション メソッドが実行されるようにします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-170">Because we have added an [Authorize] attribute to the Create() method, ASP.NET MVC ensures that the action method only executes if the user visiting the /Dinners/Create URL is logged in on the site.</span></span> <span data-ttu-id="2cb9a-171">したがって、User.Identity.Nameプロパティ値には常に有効なユーザー名が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-171">As such, the User.Identity.Name property value will always contain a valid username.</span></span>

### <a name="using-the-useridentityname-property-when-editing-dinners"></a><span data-ttu-id="2cb9a-172">ディナーの編集時にUser.Identity.Nameプロパティを使用する</span><span class="sxs-lookup"><span data-stu-id="2cb9a-172">Using the User.Identity.Name property when Editing Dinners</span></span>

<span data-ttu-id="2cb9a-173">ここで、ユーザー自身がホストしているディナーのプロパティのみを編集できるように制限する承認ロジックを追加してみましょう。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-173">Let's now add some authorization logic that restricts users so that they can only edit the properties of dinners they themselves are hosting.</span></span>

<span data-ttu-id="2cb9a-174">これを支援するために、まず、Dinner オブジェクトに "IsHostedBy(ユーザー名)" ヘルパー メソッドを追加します (Dinner.cs部分クラス内で以前に構築しました)。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-174">To help with this, we'll first add an "IsHostedBy(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="2cb9a-175">このヘルパー メソッドは、指定されたユーザー名が Dinner HostedBy プロパティと一致するかどうかに応じて true または false を返し、大文字と小文字を区別しない文字列比較を実行するために必要なロジックをカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-175">This helper method returns true or false depending on whether a supplied username matches the Dinner HostedBy property, and encapsulates the logic necessary to perform a case-insensitive string comparison of them:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

<span data-ttu-id="2cb9a-176">次に、DinnersController クラス内の Edit() アクション メソッドに [Authorize] 属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-176">We'll then add an [Authorize] attribute to the Edit() action methods within our DinnersController class.</span></span> <span data-ttu-id="2cb9a-177">これにより、ユーザーが */Dinners/Edit/[id]* URL を要求するためにログインする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-177">This will ensure that users must be logged in to request a */Dinners/Edit/[id]* URL.</span></span>

<span data-ttu-id="2cb9a-178">その後、Dinner.IsHostedBy(ユーザー名) ヘルパー メソッドを使用して、ログインしているユーザーが Dinner ホストと一致することを確認するコードを Edit メソッドに追加できます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-178">We can then add code to our Edit methods that uses the Dinner.IsHostedBy(username) helper method to verify that the logged-in user matches the Dinner host.</span></span> <span data-ttu-id="2cb9a-179">ユーザーがホストでない場合は、"無効な所有者" ビューを表示し、要求を終了します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-179">If the user is not the host, we'll display an "InvalidOwner" view and terminate the request.</span></span> <span data-ttu-id="2cb9a-180">これを行うコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-180">The code to do this looks like below:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

<span data-ttu-id="2cb9a-181">次に、\Views\Dinners ディレクトリを右クリックし、[追加-&gt;表示] メニュー コマンドを選択して、新しい "無効な所有者" ビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-181">We can then right-click on the \Views\Dinners directory and choose the Add-&gt;View menu command to create a new "InvalidOwner" view.</span></span> <span data-ttu-id="2cb9a-182">次のエラー メッセージを設定します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-182">We'll populate it with the below error message:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

<span data-ttu-id="2cb9a-183">そして今、ユーザーが自分が所有していないディナーを編集しようとすると、エラーメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-183">And now when a user attempts to edit a dinner they don't own, they'll get an error message:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

<span data-ttu-id="2cb9a-184">私たちのコントローラ内のDelete()アクションメソッドについても同じ手順を繰り返して、Dinnersを削除する権限をロックダウンし、Dinnerのホストだけがそれを削除できるようにします。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-184">We can repeat the same steps for the Delete() action methods within our controller to lock down permission to delete Dinners as well, and ensure that only the host of a Dinner can delete it.</span></span>

### <a name="showinghiding-edit-and-delete-links"></a><span data-ttu-id="2cb9a-185">編集リンクと削除リンクの表示/非表示</span><span class="sxs-lookup"><span data-stu-id="2cb9a-185">Showing/Hiding Edit and Delete Links</span></span>

<span data-ttu-id="2cb9a-186">詳細 URL から DinnersController クラスの編集と削除のアクション メソッドにリンクしています。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-186">We are linking to the Edit and Delete action method of our DinnersController class from our Details URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

<span data-ttu-id="2cb9a-187">現在、詳細 URL への訪問者がディナーのホストであるかどうかに関係なく、編集と削除のアクション リンクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-187">Currently we are showing the Edit and Delete action links regardless of whether the visitor to the details URL is the host of the dinner.</span></span> <span data-ttu-id="2cb9a-188">訪問先のユーザーがディナーの所有者である場合にのみリンクが表示されるように、これを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-188">Let's change this so that the links are only displayed if the visiting user is the owner of the dinner.</span></span>

<span data-ttu-id="2cb9a-189">DinnersController 内の Details() アクション メソッドは、Dinner オブジェクトを取得し、モデル オブジェクトとしてビュー テンプレートに渡します。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-189">The Details() action method within our DinnersController retrieves a Dinner object and then passes it as the model object to our view template:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

<span data-ttu-id="2cb9a-190">次のような Dinner.IsHostedBy() ヘルパー メソッドを使用して、ビュー テンプレートを更新して、編集リンクと削除リンクを条件付きで表示/非表示にすることができます。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-190">We can update our view template to conditionally show/hide the Edit and Delete links by using the Dinner.IsHostedBy() helper method like below:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a><span data-ttu-id="2cb9a-191">次の手順</span><span class="sxs-lookup"><span data-stu-id="2cb9a-191">Next Steps</span></span>

<span data-ttu-id="2cb9a-192">それでは、AJAX を使用して、RSVP に対して認証されたユーザーを有効にする方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="2cb9a-192">Let's now look at how we can enable authenticated users to RSVP for dinners using AJAX.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2cb9a-193">[前へ](implement-efficient-data-paging.md)
> [次へ](use-ajax-to-deliver-dynamic-updates.md)</span><span class="sxs-lookup"><span data-stu-id="2cb9a-193">[Previous](implement-efficient-data-paging.md)
[Next](use-ajax-to-deliver-dynamic-updates.md)</span></span>
