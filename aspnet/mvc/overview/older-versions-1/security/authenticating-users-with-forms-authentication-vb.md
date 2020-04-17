---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: フォーム認証 (VB) を使用したユーザーの認証 |マイクロソフトドキュメント
author: rick-anderson
description: '[Authorize] 属性を使用して、MVC アプリケーションの特定のページをパスワードで保護する方法について説明します。 Web サイト管理の使用方法も学習します。'
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 9e3117af55db2effed20b6421c2322f1c265f1c7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540819"
---
# <a name="authenticating-users-with-forms-authentication-vb"></a><span data-ttu-id="b1390-104">フォーム認証でユーザーを認証する (VB)</span><span class="sxs-lookup"><span data-stu-id="b1390-104">Authenticating Users with Forms Authentication (VB)</span></span>

<span data-ttu-id="b1390-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b1390-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b1390-106">[Authorize] 属性を使用して、MVC アプリケーションの特定のページをパスワードで保護する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b1390-106">Learn how to use the [Authorize] attribute to password protect particular pages in your MVC application.</span></span> <span data-ttu-id="b1390-107">Web サイト管理ツールを使用してユーザーとロールを作成および管理する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b1390-107">You learn how to use the Web Site Administration Tool to create and manage users and roles.</span></span> <span data-ttu-id="b1390-108">また、ユーザー アカウントとロール情報の格納場所を構成する方法についても説明します。</span><span class="sxs-lookup"><span data-stu-id="b1390-108">You also learn how to configure where user account and role information is stored.</span></span>

<span data-ttu-id="b1390-109">このチュートリアルの目的は、フォーム認証を使用して、ASP.NET MVC アプリケーションのビューをパスワード保護する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="b1390-109">The goal of this tutorial is to explain how you can use Forms authentication to password protect the views in your ASP.NET MVC applications.</span></span> <span data-ttu-id="b1390-110">Web サイト管理ツールを使用してユーザーとロールを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="b1390-110">You learn how to use the Web Site Administration Tool to create users and roles.</span></span> <span data-ttu-id="b1390-111">また、権限のないユーザーがコントローラのアクションを呼び出すことを防ぐ方法についても学習します。</span><span class="sxs-lookup"><span data-stu-id="b1390-111">You also learn how to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="b1390-112">最後に、ユーザー名とパスワードの保存場所を構成する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="b1390-112">Finally, you learn how to configure where user names and passwords are stored.</span></span>

#### <a name="using-the-web-site-administration-tool"></a><span data-ttu-id="b1390-113">Web サイト管理ツールの使用</span><span class="sxs-lookup"><span data-stu-id="b1390-113">Using the Web Site Administration Tool</span></span>

<span data-ttu-id="b1390-114">他の作業を行う前に、ユーザーとロールを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b1390-114">Before we do anything else, we should start by creating some users and roles.</span></span> <span data-ttu-id="b1390-115">新しいユーザーとロールを作成する最も簡単な方法は、Visual Studio 2008 Web サイト管理ツールを利用することです。</span><span class="sxs-lookup"><span data-stu-id="b1390-115">The easiest way to create new users and roles is to take advantage of the Visual Studio 2008 Web Site Administration Tool.</span></span> <span data-ttu-id="b1390-116">このツールを起動するには、メニュー オプションの **[プロジェクト]、ASP.NET構成を選択**します。</span><span class="sxs-lookup"><span data-stu-id="b1390-116">You can launch this tool by selecting the menu option **Project, ASP.NET Configuration**.</span></span> <span data-ttu-id="b1390-117">または、ソリューション エクスプローラ ウィンドウの上部に表示される世界に当たるハンマーの (やや怖い) アイコンをクリックして Web サイト管理ツールを起動することもできます (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="b1390-117">Alternatively, you can launch the Web Site Administration Tool by clicking the (somewhat scary) icon of the hammer hitting the world that appears at the top of the Solution Explorer window (see Figure 1).</span></span>

<span data-ttu-id="b1390-118">**図 1 – Web サイト管理ツールの起動**</span><span class="sxs-lookup"><span data-stu-id="b1390-118">**Figure 1 – Launching the Web Site Administration Tool**</span></span>

![clip_image002[4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

<span data-ttu-id="b1390-120">Web サイト管理ツールで、新しいユーザーとロールを作成するには、[セキュリティ] タブを**Create user**クリックします。</span><span class="sxs-lookup"><span data-stu-id="b1390-120">Within the Web Site Administration Tool, you create new users and roles by selecting the Security tab. Click the **Create user** link to create a new user named Stephen (see Figure 2).</span></span> <span data-ttu-id="b1390-121">Stephen ユーザーに必要なパスワード (*たとえば、シークレット*) を指定します。</span><span class="sxs-lookup"><span data-stu-id="b1390-121">Provide the Stephen user with any password that you want (for example, *secret*).</span></span>

<span data-ttu-id="b1390-122">**図 2 – 新しいユーザーの作成**</span><span class="sxs-lookup"><span data-stu-id="b1390-122">**Figure 2 – Creating a new user**</span></span>

![clip_image004[4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

<span data-ttu-id="b1390-124">新しいロールを作成するには、まずロールを有効にし、1 つ以上のロールを定義します。</span><span class="sxs-lookup"><span data-stu-id="b1390-124">You create new roles by first enabling roles and defining one or more roles.</span></span> <span data-ttu-id="b1390-125">[ロールを有効にする] リンクをクリックして **、ロールを有効に**します。</span><span class="sxs-lookup"><span data-stu-id="b1390-125">Enable roles by clicking the **Enable roles** link.</span></span> <span data-ttu-id="b1390-126">次に、[役割の作成] または [**役割の管理**] リンクをクリックして *、管理者*という名前の役割を作成します (図 3 参照)。</span><span class="sxs-lookup"><span data-stu-id="b1390-126">Next, create a role named *Administrators* by clicking the **Create or Manage roles** link (see Figure 3).</span></span>

<span data-ttu-id="b1390-127">**図 3 – 新しいロールの作成**</span><span class="sxs-lookup"><span data-stu-id="b1390-127">**Figure 3 – Creating a new role**</span></span>

![clip_image006[4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

<span data-ttu-id="b1390-129">最後に、Sally という名前の新しいユーザーを作成し、[ユーザーの作成] リンクをクリックし、Sally の作成時に [管理者] を選択して、Sally を管理者ロールに関連付けます (図 4 参照)。</span><span class="sxs-lookup"><span data-stu-id="b1390-129">Finally, create a new user named Sally and associate Sally with the Administrators role by clicking the Create User link and selecting Administrators when creating Sally (see Figure 4).</span></span>

<span data-ttu-id="b1390-130">**図 4 – ロールへのユーザーの追加**</span><span class="sxs-lookup"><span data-stu-id="b1390-130">**Figure 4 – Adding a user to a role**</span></span>

![clip_image008[4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

<span data-ttu-id="b1390-132">すべてが言われ、完了したら、Stephen と Sally という名前の 2 人の新しいユーザーを持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="b1390-132">When all is said and done, you should have two new users named Stephen and Sally.</span></span> <span data-ttu-id="b1390-133">また、管理者という名前の新しい役割も必要です。</span><span class="sxs-lookup"><span data-stu-id="b1390-133">You should also have a new role named Administrators.</span></span> <span data-ttu-id="b1390-134">サリーは管理者ロールのメンバーであり、スティーブンは属していません。</span><span class="sxs-lookup"><span data-stu-id="b1390-134">Sally is a member of the Administrators role and Stephen is not.</span></span>

#### <a name="requiring-authorization"></a><span data-ttu-id="b1390-135">認証の要求</span><span class="sxs-lookup"><span data-stu-id="b1390-135">Requiring Authorization</span></span>

<span data-ttu-id="b1390-136">ユーザーがコントローラー アクションを呼び出す前に、アクションに [Authorize] 属性を追加して、ユーザーを認証するように要求できます。</span><span class="sxs-lookup"><span data-stu-id="b1390-136">You can require a user to be authenticated before the user invokes a controller action by adding the [Authorize] attribute to the action.</span></span> <span data-ttu-id="b1390-137">[Authorize] 属性を個々のコントローラー アクションに適用するか、この属性をコントローラ クラス全体に適用できます。</span><span class="sxs-lookup"><span data-stu-id="b1390-137">You can apply the [Authorize] attribute to an individual controller action or you can apply this attribute to an entire controller class.</span></span>

<span data-ttu-id="b1390-138">たとえば、リスト 1 のコントローラは、CompanySecrets() という名前のアクションを公開します。</span><span class="sxs-lookup"><span data-stu-id="b1390-138">For example, the controller in Listing 1 exposes an action named CompanySecrets().</span></span> <span data-ttu-id="b1390-139">このアクションは [Authorize] 属性で修飾されているため、ユーザーが認証されない限り、このアクションを呼び出すことはできません。</span><span class="sxs-lookup"><span data-stu-id="b1390-139">Because this action is decorated with the [Authorize] attribute, this action cannot be invoked unless a user is authenticated.</span></span>

<span data-ttu-id="b1390-140">**リスト 1 - コントローラ\ホームコントローラー.vb**</span><span class="sxs-lookup"><span data-stu-id="b1390-140">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

<span data-ttu-id="b1390-141">ブラウザーのアドレス バーに URL /Home/CompanySecrets を入力して CompanySecrets() アクションを呼び出し、認証されたユーザーでない場合は、自動的にログイン ビューにリダイレクトされます (図 5 参照)。</span><span class="sxs-lookup"><span data-stu-id="b1390-141">If you invoke the CompanySecrets() action by entering the URL /Home/CompanySecrets in the address bar of your browser, and you are not an authenticated user, then you will be redirected to the Login view automatically (see Figure 5).</span></span>

<span data-ttu-id="b1390-142">**図5 – ログインビュー**</span><span class="sxs-lookup"><span data-stu-id="b1390-142">**Figure 5 – The Login view**</span></span>

![clip_image010[4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

<span data-ttu-id="b1390-144">ログインビューを使用して、ユーザー名とパスワードを入力できます。</span><span class="sxs-lookup"><span data-stu-id="b1390-144">You can use the Login view to enter your user name and password.</span></span> <span data-ttu-id="b1390-145">登録ユーザーでない場合は、登録リンクをクリックして**登録**ビューに移動できます (図 6 参照)。</span><span class="sxs-lookup"><span data-stu-id="b1390-145">If you are not a registered user then you can click the **register** link to navigate to the Register view (see Figure 6).</span></span> <span data-ttu-id="b1390-146">登録ビューを使用して、新しいユーザー アカウントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="b1390-146">You can use the Register view to create a new user account.</span></span>

<span data-ttu-id="b1390-147">**図6 – レジスタビュー**</span><span class="sxs-lookup"><span data-stu-id="b1390-147">**Figure 6 – The Register view**</span></span>

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

<span data-ttu-id="b1390-149">正常にログインすると、会社の秘密のビューが表示されます (図 7 参照)。</span><span class="sxs-lookup"><span data-stu-id="b1390-149">After you successfully log in, you can see the CompanySecrets view (see Figure 7).</span></span> <span data-ttu-id="b1390-150">デフォルトでは、ブラウザウィンドウを閉じるまでログインし続けます。</span><span class="sxs-lookup"><span data-stu-id="b1390-150">By default, you will continue to be logged in until you close your browser window.</span></span>

<span data-ttu-id="b1390-151">**図 7 – 会社秘密ビュー**</span><span class="sxs-lookup"><span data-stu-id="b1390-151">**Figure 7 – The CompanySecrets view**</span></span>

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a><span data-ttu-id="b1390-153">ユーザー名またはユーザー ロールによる承認</span><span class="sxs-lookup"><span data-stu-id="b1390-153">Authorizing by User Name or User Role</span></span>

<span data-ttu-id="b1390-154">[Authorize] 属性を使用すると、特定のユーザーセットまたは特定のユーザー ロール セットに対するコントローラ アクションへのアクセスを制限できます。</span><span class="sxs-lookup"><span data-stu-id="b1390-154">You can use the [Authorize] attribute to restrict access to a controller action to a particular set of users or a particular set of user roles.</span></span> <span data-ttu-id="b1390-155">たとえば、リスト 2 で変更されたホーム コント ローラーには、StephenSecrets() と管理者の秘密() という名前の 2 つの新しいアクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b1390-155">For example, the modified Home controller in Listing 2 contains two new actions named StephenSecrets() and AdministratorSecrets().</span></span>

<span data-ttu-id="b1390-156">**リスト 2 - コントローラ\ホームコントローラー.vb**</span><span class="sxs-lookup"><span data-stu-id="b1390-156">**Listing 2 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

<span data-ttu-id="b1390-157">スティーブンというユーザー名を持つユーザーのみが、StephenSecrets() アクションを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="b1390-157">Only a user with the user name Stephen can invoke the StephenSecrets() action.</span></span> <span data-ttu-id="b1390-158">他のすべてのユーザーはログインビューにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="b1390-158">All other users get redirected to the Login view.</span></span> <span data-ttu-id="b1390-159">Users プロパティは、ユーザー アカウント名のコンマ区切りのリストを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="b1390-159">The Users property accepts a comma separated list of user account names.</span></span>

<span data-ttu-id="b1390-160">管理者ロールのユーザーのみが管理者秘密() アクションを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="b1390-160">Only users in the Administrators role can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="b1390-161">たとえば、サリーは管理者グループのメンバーであるため、管理者の秘密() アクションを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="b1390-161">For example, because Sally is a member of the Administrators group, she can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="b1390-162">他のすべてのユーザーはログインビューにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="b1390-162">All other users get redirected to the Login view.</span></span> <span data-ttu-id="b1390-163">ロール プロパティは、ロール名のコンマ区切りのリストを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="b1390-163">The Roles property accepts a comma separated list of role names.</span></span>

#### <a name="configuring-authentication"></a><span data-ttu-id="b1390-164">認証の構成</span><span class="sxs-lookup"><span data-stu-id="b1390-164">Configuring Authentication</span></span>

<span data-ttu-id="b1390-165">この時点で、ユーザー アカウントとロール情報がどこに格納されているか疑問に思うかもしれません。</span><span class="sxs-lookup"><span data-stu-id="b1390-165">At this point, you might be wondering where the user account and role information is being stored.</span></span> <span data-ttu-id="b1390-166">既定では、情報は、MVC アプリケーションのアプリ\_データ フォルダーにある ASPNETDB.mdf という名前の (RANU) SQL Express データベースに格納されます。</span><span class="sxs-lookup"><span data-stu-id="b1390-166">By default, the information is stored in a (RANU) SQL Express database named ASPNETDB.mdf located in your MVC application's App\_Data folder.</span></span> <span data-ttu-id="b1390-167">このデータベースは、メンバーシップの使用を開始すると、ASP.NET フレームワークによって自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="b1390-167">This database is generated by the ASP.NET framework automatically when you start using membership.</span></span>

<span data-ttu-id="b1390-168">ソリューション エクスプ ローラー ウィンドウで ASPNETDB.mdf データベースを表示するには、最初にメニュー オプションプロジェクト、すべてのファイルを表示を選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b1390-168">In order to see the ASPNETDB.mdf database in the Solution Explorer window, you first need to select the menu option Project, Show All Files.</span></span>

<span data-ttu-id="b1390-169">アプリケーションを開発する場合は、既定の SQL Express データベースを使用しても問題ありません。</span><span class="sxs-lookup"><span data-stu-id="b1390-169">Using the default SQL Express database is fine when developing an application.</span></span> <span data-ttu-id="b1390-170">ただし、ほとんどの場合、運用アプリケーションでは既定の ASPNETDB.mdf データベースを使用する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="b1390-170">Most likely, however, you won't want to use the default ASPNETDB.mdf database for a production application.</span></span> <span data-ttu-id="b1390-171">この場合、次の 2 つの手順を実行して、ユーザー アカウント情報の格納場所を変更できます。</span><span class="sxs-lookup"><span data-stu-id="b1390-171">In that case, you can change where user account information is stored by completing the following two steps:</span></span>

1. <span data-ttu-id="b1390-172">アプリケーション サービス データベース オブジェクトを運用データベースに追加する - 実稼働データベースを指すアプリケーション接続文字列を変更する</span><span class="sxs-lookup"><span data-stu-id="b1390-172">Add the Application Services database objects to your production database - Change your application connection string to point to your production database</span></span>

<span data-ttu-id="b1390-173">最初の手順では、必要なデータベース オブジェクト (テーブルとストアド プロシージャ) をすべて運用データベースに追加します。</span><span class="sxs-lookup"><span data-stu-id="b1390-173">The first step is to add all of the necessary database objects (tables and stored procedures) to your production database.</span></span> <span data-ttu-id="b1390-174">これらのオブジェクトを新しいデータベースに追加する最も簡単な方法は、sql Server セットアップ ウィザードASP.NETを利用することです (図 8 参照)。</span><span class="sxs-lookup"><span data-stu-id="b1390-174">The easiest way to add these objects to a new database is to take advantage of the ASP.NET SQL Server Setup Wizard (see Figure 8).</span></span> <span data-ttu-id="b1390-175">このツールを起動する場合は、Visual Studio 2008 プログラム グループから Visual Studio 2008 コマンド プロンプトを開き、コマンド プロンプトから次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="b1390-175">You can launch this tool by opening the Visual Studio 2008 Command Prompt from the Microsoft Visual Studio 2008 program group and executing the following command from the command prompt:</span></span>

<span data-ttu-id="b1390-176">aspnet\_のレジストリー</span><span class="sxs-lookup"><span data-stu-id="b1390-176">aspnet\_regsql</span></span>

<span data-ttu-id="b1390-177">**図 8 – sql Server セットアップ ウィザードASP.NET**</span><span class="sxs-lookup"><span data-stu-id="b1390-177">**Figure 8 – The ASP.NET SQL Server Setup Wizard**</span></span>

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

<span data-ttu-id="b1390-179">SQL Serversql Server セットアップ ウィザードASP.NETを使用すると、ネットワーク上の SQL Server データベースを選択し、ASP.NET アプリケーション サービスに必要なすべてのデータベース オブジェクトをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="b1390-179">The ASP.NET SQL Server Setup Wizard enables you to select a SQL Server database on your network and install all of the database objects required by the ASP.NET application services.</span></span> <span data-ttu-id="b1390-180">データベース サーバーはローカル マシン上に配置する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="b1390-180">The database server is not required to be located on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="b1390-181">SQL Server SQL Server セットアップ ウィザードASP.NETを使用しない場合は、次のフォルダにアプリケーション サービス データベース オブジェクトを追加するための SQL スクリプトを検索できます。</span><span class="sxs-lookup"><span data-stu-id="b1390-181">If you don't want to use the ASP.NET SQL Server Setup Wizard, then you can find SQL scripts for adding the application services database objects in the following folder:</span></span>
> 
> 
> <span data-ttu-id="b1390-182">C:\Windows\マイクロソフト.NET\フレームワーク\v2.0.50727</span><span class="sxs-lookup"><span data-stu-id="b1390-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span></span>

<span data-ttu-id="b1390-183">必要なデータベース オブジェクトを作成した後、MVC アプリケーションで使用されるデータベース接続を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b1390-183">After you create the necessary database objects, you need to modify the database connection used by your MVC application.</span></span> <span data-ttu-id="b1390-184">Web 構成 (web.config) ファイル内の ApplicationServices 接続文字列を変更して、運用データベースを指します。</span><span class="sxs-lookup"><span data-stu-id="b1390-184">Modify the ApplicationServices connection string in your web configuration (web.config) file so that it points to the production database.</span></span> <span data-ttu-id="b1390-185">たとえば、リスト 3 の変更された接続は、MyProductionDB という名前のデータベースを指しています (元の ApplicationServices 接続文字列はコメント アウトされています)。</span><span class="sxs-lookup"><span data-stu-id="b1390-185">For example, the modified connection in Listing 3 points to a database named MyProductionDB (the original ApplicationServices connection string has been commented out).</span></span>

<span data-ttu-id="b1390-186">**リスト 3 - Web.config**</span><span class="sxs-lookup"><span data-stu-id="b1390-186">**Listing 3 – Web.config**</span></span>

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a><span data-ttu-id="b1390-187">データベース権限の設定</span><span class="sxs-lookup"><span data-stu-id="b1390-187">Configuring Database Permissions</span></span>

<span data-ttu-id="b1390-188">統合セキュリティを使用してデータベースに接続する場合は、データベースへのログインとして正しい Windows ユーザー アカウントを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b1390-188">If you use Integrated Security to connect to your database then you will need to add the correct Windows user account as a login to your database.</span></span> <span data-ttu-id="b1390-189">正しいアカウントは、web サーバーとして開発サーバーまたはインターネット インフォメーション サービスASP.NETを使用しているかどうかによって異なります。</span><span class="sxs-lookup"><span data-stu-id="b1390-189">The correct account depends on whether you are using the ASP.NET Development Server or Internet Information Services as your web server.</span></span> <span data-ttu-id="b1390-190">正しいユーザー アカウントは、オペレーティング システムによっても異なります。</span><span class="sxs-lookup"><span data-stu-id="b1390-190">The correct user account also depends on your operating system.</span></span>

<span data-ttu-id="b1390-191">ASP.NET開発サーバー (Visual Studio で使用される既定の Web サーバー) を使用している場合、アプリケーションは Windows ユーザー アカウントのコンテキスト内で実行されます。</span><span class="sxs-lookup"><span data-stu-id="b1390-191">If you are using the ASP.NET Development Server (the default web server used by Visual Studio) then your application executes within the context of your Windows user account.</span></span> <span data-ttu-id="b1390-192">その場合は、Windows ユーザー アカウントをデータベース サーバー ログインとして追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b1390-192">In that case, you need to add your Windows user account as a database server login.</span></span>

<span data-ttu-id="b1390-193">または、インターネット インフォメーション サービスを使用している場合は、データベース サーバー ログインとして ASPNET アカウントまたは NT AUTHORITY/NETWORK SERVICE アカウントを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b1390-193">Alternatively, if you are using Internet Information Services then you need to add either the ASPNET account or the NT AUTHORITY/NETWORK SERVICE account as a database server login.</span></span> <span data-ttu-id="b1390-194">Windows XP を使用している場合は、データベースへのログインとして ASPNET アカウントを追加します。</span><span class="sxs-lookup"><span data-stu-id="b1390-194">If you are using Windows XP then add the ASPNET account as a login to your database.</span></span> <span data-ttu-id="b1390-195">Windows Vista や Windows Server 2008 など、より新しいオペレーティング システムを使用している場合は、NT オーソリティ/ネットワーク サービス アカウントをデータベース ログインとして追加します。</span><span class="sxs-lookup"><span data-stu-id="b1390-195">If you are using a more recent operating system, such as Windows Vista or Windows Server 2008, then add the NT AUTHORITY/NETWORK SERVICE account as the database login.</span></span>

<span data-ttu-id="b1390-196">新しいユーザー アカウントをデータベースに追加するには、Microsoft SQL Server 管理スタジオを使用します (図 9 参照)。</span><span class="sxs-lookup"><span data-stu-id="b1390-196">You can add a new user account to your database by using Microsoft SQL Server Management Studio (see Figure 9).</span></span>

<span data-ttu-id="b1390-197">**図 9 – 新しい SQL Server ログインの作成**</span><span class="sxs-lookup"><span data-stu-id="b1390-197">**Figure 9 – Creating a new Microsoft SQL Server login**</span></span>

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

<span data-ttu-id="b1390-199">必要なログインを作成したら、適切なデータベース ロールを持つデータベース ユーザーにログインをマップする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b1390-199">After you create the required login, you need to map the login to a database user with the right database roles.</span></span> <span data-ttu-id="b1390-200">ログインをダブルクリックし、[ユーザー マッピング] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="b1390-200">Double-click the login and select the User Mapping tab. Select one or more application services database roles.</span></span> <span data-ttu-id="b1390-201">たとえば、ユーザーを認証するには、aspnet\_メンバーシップ\_の BasicAccess データベース ロールを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b1390-201">For example, in order to authenticate users, you need to enable the aspnet\_Membership\_BasicAccess database role.</span></span> <span data-ttu-id="b1390-202">新しいユーザーを作成するには、aspnet\_メンバーシップ\_FullAccess データベース ロールを有効にする必要があります (図 10 を参照)。</span><span class="sxs-lookup"><span data-stu-id="b1390-202">In order to create new users, you need to enable the aspnet\_Membership\_FullAccess database role (see Figure 10).</span></span>

<span data-ttu-id="b1390-203">**図 10 – アプリケーション サービス データベース ロールの追加**</span><span class="sxs-lookup"><span data-stu-id="b1390-203">**Figure 10 – Adding Application Services database roles**</span></span>

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a><span data-ttu-id="b1390-205">まとめ</span><span class="sxs-lookup"><span data-stu-id="b1390-205">Summary</span></span>

<span data-ttu-id="b1390-206">このチュートリアルでは、ASP.NETの MVC アプリケーションを構築するときにフォーム認証を使用する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="b1390-206">In this tutorial, you learned how to use Forms authentication when building an ASP.NET MVC application.</span></span> <span data-ttu-id="b1390-207">最初に、Web サイト管理ツールを利用して新しいユーザーとロールを作成する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="b1390-207">First, you learned how to create new users and roles by taking advantage of the Web Site Administration Tool.</span></span> <span data-ttu-id="b1390-208">次に、[Authorize] 属性を使用して、承認されていないユーザーがコントローラアクションを呼び出すことを防ぐ方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="b1390-208">Next, you learned how to use the [Authorize] attribute to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="b1390-209">最後に、ユーザーとロールの情報を運用データベースに格納するように MVC アプリケーションを構成する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="b1390-209">Finally, you learned how to configure your MVC application to store user and role information in a production database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b1390-210">[前へ](preventing-javascript-injection-attacks-cs.md)
> [次へ](authenticating-users-with-windows-authentication-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b1390-210">[Previous](preventing-javascript-injection-attacks-cs.md)
[Next](authenticating-users-with-windows-authentication-vb.md)</span></span>
