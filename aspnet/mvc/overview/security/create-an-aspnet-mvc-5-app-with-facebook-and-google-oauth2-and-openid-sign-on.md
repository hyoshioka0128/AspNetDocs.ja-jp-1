---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: フェイスブック、ツイッター、リンクトイン、グーグルOAuth2サインオン(C#)でMVC 5アプリを作成する |マイクロソフトドキュメント
author: Rick-Anderson
description: このチュートリアルでは、ユーザーが外部認証からの資格情報を使用して OAuth 2.0 を使用してログインできるようにする ASP.NET MVC 5 Web アプリケーションを構築する方法を示します。
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675917"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="7e12f-103">Facebook、Twitter、LinkedIn、Google の OAuth2 サインオンを使用して ASP.NET MVC 5 アプリを作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="7e12f-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="7e12f-104">[リック・アンダーソン](https://twitter.com/RickAndMSFT)著</span><span class="sxs-lookup"><span data-stu-id="7e12f-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="7e12f-105">このチュートリアルでは、ユーザーがFacebook、Twitter、LinkedIn、マイクロソフト、Google などの外部認証プロバイダーからの資格情報を使用して[OAuth 2.0](http://oauth.net/2/)を使用してログインできるようにする、ASP.NET MVC 5 Web アプリケーションを構築する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="7e12f-106">簡単にするために、このチュートリアルでは、FacebookとGoogleからの資格情報を使用して作業することに焦点を当てています。</span><span class="sxs-lookup"><span data-stu-id="7e12f-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="7e12f-107">Web サイトでこれらの資格情報を有効にすると、何百万ものユーザーが既にこれらの外部プロバイダーにアカウントを持っているため、大きな利点があります。</span><span class="sxs-lookup"><span data-stu-id="7e12f-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="7e12f-108">これらのユーザーは、新しい資格情報のセットを作成して覚えておく必要がない場合は、サイトにサインアップする傾向が高くなります。</span><span class="sxs-lookup"><span data-stu-id="7e12f-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="7e12f-109">SMS[と電子メール 2 要素認証を使用して MVC 5 アプリをASP.NET](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)も参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="7e12f-110">このチュートリアルでは、ユーザーのプロファイル データを追加する方法、およびメンバーシップ API を使用してロールを追加する方法も示します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="7e12f-111">このチュートリアルは[リック・アンダーソン](https://blogs.msdn.com/rickAndy)によって書かれた (Twitterで私[@RickAndMSFT](https://twitter.com/RickAndMSFT)に従ってください: ).</span><span class="sxs-lookup"><span data-stu-id="7e12f-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="7e12f-112">作業の開始</span><span class="sxs-lookup"><span data-stu-id="7e12f-112">Getting Started</span></span>

<span data-ttu-id="7e12f-113">まず、Web 用または[Visual Studio 2013 用の Visual Studio Express](https://go.microsoft.com/fwlink/?LinkId=299058) [2013](https://go.microsoft.com/fwlink/?LinkId=306566)をインストールして実行します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="7e12f-114">Visual Studio [2013 更新プログラム 3](https://go.microsoft.com/fwlink/?LinkId=390521)以降をインストールします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="7e12f-115">Dropbox、GitHub、リンクティン、インスタグラム、バッファ、セールスフォース、スチーム、スタックエクスチェンジ、トリジット、トゥイッチ、ツイッター、Yahoo!、その他のヘルプについては、この[サンプルプロジェクト](https://github.com/matthewdunsdon/oauthforaspnet)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="7e12f-116">Google OAuth 2 を使用して、SSL 警告なしでローカルでデバッグするには、Visual Studio [2013 更新プログラム 3](https://go.microsoft.com/fwlink/?LinkId=390521)以降をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e12f-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="7e12f-117">**[スタート**] ページで [**新しいプロジェクト**] をクリックするか、メニューを使用して **[ファイル**] をクリックし、[**新しいプロジェクト**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="7e12f-118">最初のアプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="7e12f-118">Creating Your First Application</span></span>

<span data-ttu-id="7e12f-119">[**新しいプロジェクト**] をクリックし、左側の **[Visual C#]** を選択してから **、[Web]** を選択して **、[Web アプリケーションASP.NET]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="7e12f-120">プロジェクトに "MvcAuth" という名前を付け **、[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="7e12f-121">[**新しいASP.NET プロジェクト**] ダイアログボックスで **、[MVC]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="7e12f-122">[認証] が **[個別のユーザー アカウント**] でない場合は、[**認証の変更**] ボタンをクリックし、[**個別のユーザー アカウント**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="7e12f-123">**クラウドでホスト を**チェックすることで、アプリは Azure でホストすることが非常に簡単になります。</span><span class="sxs-lookup"><span data-stu-id="7e12f-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="7e12f-124">**[クラウドでホスト**] を選択した場合は、[構成] ダイアログボックスに入力します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="7e12f-125">NuGet を使用して最新の OWIN ミドルウェアを更新する</span><span class="sxs-lookup"><span data-stu-id="7e12f-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="7e12f-126">NuGet パッケージ マネージャーを使用して[OWIN ミドルウェア](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)を更新する 。</span><span class="sxs-lookup"><span data-stu-id="7e12f-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="7e12f-127">左側のメニューで[**更新]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="7e12f-128">**[すべて更新**] ボタンをクリックするか、次の画像に示すように OWIN パッケージのみを検索できます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="7e12f-129">下の図では、OWIN パッケージのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="7e12f-130">パッケージ マネージャ コンソール (PMC) からコマンド`Update-Package`を入力すると、すべてのパッケージが更新されます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="7e12f-131">**F5**キーまたは**Ctrl キーを押しながら F5 キー**を押して、アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="7e12f-132">下の図では、ポート番号は 1234 です。</span><span class="sxs-lookup"><span data-stu-id="7e12f-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="7e12f-133">アプリケーションを実行すると、別のポート番号が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="7e12f-134">ブラウザウィンドウのサイズによっては、ナビゲーションアイコンをクリックして **、ホーム**、**情報**、**連絡先**、**登録**、ログインの各リンク**を**表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e12f-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="7e12f-135">プロジェクトでの SSL の設定</span><span class="sxs-lookup"><span data-stu-id="7e12f-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="7e12f-136">グーグルやフェイスブックなどの認証プロバイダに接続するには、SSLを使用するようにIIS-Expressを設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e12f-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="7e12f-137">ログイン後もSSLを使用し続け、HTTPに戻らないようにすることが重要であり、ログインクッキーはあなたのユーザー名とパスワードと同じくらい秘密であり、SSLを使用せずにワイヤーを介してクリアテキストで送信します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="7e12f-138">また、MVC パイプラインが実行される前にハンドシェイクを実行し、チャネル (HTTPS が HTTP よりも遅くなる部分の大部分) をセキュリティで保護する時間が既に取られているため、ログイン後に HTTP にリダイレクトしても、現在の要求や今後の要求が大幅に速くなりません。</span><span class="sxs-lookup"><span data-stu-id="7e12f-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="7e12f-139">**ソリューション エクスプローラー**で **、MvcAuth**プロジェクトをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="7e12f-140">F4 キーを押してプロジェクトのプロパティを表示します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="7e12f-141">または、[**表示**] メニューの [**プロパティ ウィンドウ]** を選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="7e12f-142">**[SSL の有効化**] を [True] に変更します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="7e12f-143">SSL URL をコピーします`https://localhost:44300/`(他の SSL プロジェクトを作成していない場合)。</span><span class="sxs-lookup"><span data-stu-id="7e12f-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="7e12f-144">**ソリューション エクスプローラー**で **、 MvcAuth**プロジェクトを右クリックし、[**プロパティ ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="7e12f-145">**[Web]** タブを選択し、[**プロジェクト URL]** ボックスに SSL URL を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="7e12f-146">ファイルを保存します (Ctl+S)。</span><span class="sxs-lookup"><span data-stu-id="7e12f-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="7e12f-147">FacebookとGoogleの認証アプリを設定するには、このURLが必要です。</span><span class="sxs-lookup"><span data-stu-id="7e12f-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="7e12f-148">すべての要求で HTTPS を`Home`使用する必要がある場合は[、RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)属性をコントローラーに追加します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="7e12f-149">より安全な方法は、アプリケーションに[RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)フィルターを追加することです。</span><span class="sxs-lookup"><span data-stu-id="7e12f-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="7e12f-150">「SSL&quot;によるアプリケーションの保護」セクションと「認証&quot;と SQL DB を[使用してASP.NET MVC アプリを作成し、Azure App Service にデプロイする](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)」の「属性を認証する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="7e12f-151">ホームコントローラの一部を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="7e12f-152">Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="7e12f-153">過去に証明書をインストールした場合は、このセクションの残りの部分をスキップして[、OAuth 2 用の Google アプリを作成し、プロジェクトに接続するに](#goog)移動し、指示に従って IIS Express が生成した自己署名証明書を信頼します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="7e12f-154">localhost を表す証明書をインストールする場合は、**セキュリティの警告**ダイアログを読み、[**はい**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="7e12f-155">IE は *ホーム* ページを表示し、SSL の警告はありません。</span><span class="sxs-lookup"><span data-stu-id="7e12f-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="7e12f-156">Google Chrome も証明書を受け入れ、警告なしに HTTPS コンテンツを表示します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="7e12f-157">Firefox は独自の証明書ストアを使用するため、警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="7e12f-158">このアプリケーションでは、[**リスクを理解しています**] をクリックしても安全に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="7e12f-159">OAuth 2 用の Google アプリを作成し、アプリをプロジェクトに接続する</span><span class="sxs-lookup"><span data-stu-id="7e12f-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="7e12f-160">現在の Google OAuth の手順については[、「ASP.NETコアでの Google 認証の設定](/aspnet/core/security/authentication/social/google-logins)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="7e12f-161">[Google Developers Console](https://console.developers.google.com/)にアクセスします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="7e12f-162">プロジェクトをまだ作成していない場合は、左側のタブで **[認証情報**] を選択し、[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="7e12f-163">左側のタブで 、[**資格情報**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="7e12f-164">[**資格情報の作成\*\*\*\*]、[OAuth クライアント ID]** の順にクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="7e12f-165">[**クライアント ID**の作成] ダイアログで、アプリケーションの種類に応える既定の Web**アプリケーション**をそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="7e12f-166">**認証された JavaScript**オリジンを上記で使用した SSL`https://localhost:44300/` URL に設定します (他の SSL プロジェクトを作成していない場合)。</span><span class="sxs-lookup"><span data-stu-id="7e12f-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="7e12f-167">**許可されたリダイレクト URI**を次の値に設定します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="7e12f-168">OAuth 同意画面のメニュー項目をクリックし、電子メール アドレスと製品名を設定します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="7e12f-169">フォームに入力したら、[**保存**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="7e12f-170">[ライブラリ] メニュー項目をクリックし **、Google+ API**を検索し、それをクリックして [有効] を押します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="7e12f-171">次の図は、有効な API を示しています。</span><span class="sxs-lookup"><span data-stu-id="7e12f-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="7e12f-172">Google API マネージャで[**認証情報**]タブにアクセスし、**クライアント ID**を取得します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="7e12f-173">ダウンロードして、アプリケーションシークレットと共に JSON ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="7e12f-174">**ClientId**と**ClientSecret**をコピーして`UseGoogleAuthentication`*、App_Start*フォルダーの*Startup.Auth.cs*ファイルにあるメソッドに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="7e12f-175">以下に示す**クライアント ID**値と**クライアント シークレット**値はサンプルであり、動作しません。</span><span class="sxs-lookup"><span data-stu-id="7e12f-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="7e12f-176">セキュリティ - ソース コードに機密データを格納しないでください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="7e12f-177">アカウントと資格情報は、サンプルをシンプルに保つために上記のコードに追加されます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="7e12f-178">[ASP.NETと Azure アプリ サービスにパスワードやその他の機密データをデプロイするためのベスト プラクティスを](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="7e12f-179">**Ctrl キーを押しながら F5 キー**を押して、アプリケーションをビルドして実行します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="7e12f-180">**[Log in]** リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="7e12f-181">[**別のサービスを使用してログイン**] の下にある **[Google]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="7e12f-182">上記の手順のいずれかを見逃すと、HTTP 401エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="7e12f-183">上記の手順を再確認してください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-183">Recheck your steps above.</span></span> <span data-ttu-id="7e12f-184">必要な設定 (**製品名**など) を見逃した場合は、不足しているアイテムを追加して保存します。認証が機能するまでに数分かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="7e12f-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="7e12f-185">認証情報を入力する Google サイトにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="7e12f-186">資格情報を入力すると、作成した Web アプリケーションにアクセス許可を与えるプロンプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="7e12f-187">**[Accept]\(受け入れる\)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-187">Click **Accept**.</span></span> <span data-ttu-id="7e12f-188">これで、Google アカウントを登録できる MvcAuth アプリケーションの **[登録**] ページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="7e12f-189">Google アカウントに使用するローカルの電子メール登録名を変更できますが、通常は既定の電子メール エイリアス (認証に使用したエイリアス) を変更しません。</span><span class="sxs-lookup"><span data-stu-id="7e12f-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="7e12f-190">**[登録]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="7e12f-191">Facebookでアプリを作成し、プロジェクトにアプリを接続する</span><span class="sxs-lookup"><span data-stu-id="7e12f-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="7e12f-192">現在の Facebook OAuth2 認証手順については[、Facebook 認証の設定を](/aspnet/core/security/authentication/social/facebook-logins)参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="7e12f-193">メンバーシップ データを確認する</span><span class="sxs-lookup"><span data-stu-id="7e12f-193">Examine the Membership Data</span></span>

<span data-ttu-id="7e12f-194">[**表示**] メニューの [**サーバー エクスプローラ**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="7e12f-195">**[既定の接続 (MvcAuth)]** を展開し **、[テーブル**] を展開し **、[AspNetUsers]** を右クリックして 、[**テーブル データの表示**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers テーブル データ](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="7e12f-197">ユーザー クラスへのプロファイル データの追加</span><span class="sxs-lookup"><span data-stu-id="7e12f-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="7e12f-198">このセクションでは、次の図に示すように、登録時にユーザー データに生年月日と出身地を追加します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![故郷とBdayとのreg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="7e12f-200">*モデル\IdentityModels.cs*ファイルを開き、生年月日とホームタウンのプロパティを追加します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="7e12f-201">*モデル\AccountViewModels.cs*ファイルと設定された生年月日とホームタウンの`ExternalLoginConfirmationViewModel`プロパティを開きます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="7e12f-202">*コントローラ\AccountController.cs*ファイルを開き、次のようにアクションメソッドで生年月日と`ExternalLoginConfirmation`故郷のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="7e12f-203">生年月日と故郷を*ビュー\アカウント\外部ログイン確認.cshtml*ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="7e12f-204">メンバーシップデータベースを削除して、Facebookアカウントをアプリケーションに再登録し、新しい生年月日とホームタウンのプロフィール情報を追加できることを確認します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="7e12f-205">**ソリューション エクスプローラー**で 、[**すべてのファイルの表示**] アイコンをクリックし、[*データの\_追加]、[aspnet-MvcAuth-&lt;dateStamp&gt;.mdf]* の順にクリックして 、[**削除**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="7e12f-206">[**ツール**] メニューの **[NuGet パッケージ マネージャ**] をクリックし、[パッケージ マネージャー**コンソール**(PMC)] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="7e12f-207">PMCに次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="7e12f-208">移行を有効にする</span><span class="sxs-lookup"><span data-stu-id="7e12f-208">Enable-Migrations</span></span>
2. <span data-ttu-id="7e12f-209">アドイン移行のイニト</span><span class="sxs-lookup"><span data-stu-id="7e12f-209">Add-Migration Init</span></span>
3. <span data-ttu-id="7e12f-210">データベースの更新</span><span class="sxs-lookup"><span data-stu-id="7e12f-210">Update-Database</span></span>

<span data-ttu-id="7e12f-211">アプリケーションを実行し、ログインし、一部のユーザーを登録するには、FaceBookとGoogleを使用しています。</span><span class="sxs-lookup"><span data-stu-id="7e12f-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="7e12f-212">メンバーシップ データを確認する</span><span class="sxs-lookup"><span data-stu-id="7e12f-212">Examine the Membership Data</span></span>

<span data-ttu-id="7e12f-213">[**表示**] メニューの [**サーバー エクスプローラ**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="7e12f-214">**AspNetUsers**を右クリックし、[**テーブル データの表示**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="7e12f-215">および`HomeTown``BirthDate`フィールドは以下に示します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="7e12f-216">アプリをログオフして別のアカウントでログインする</span><span class="sxs-lookup"><span data-stu-id="7e12f-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="7e12f-217">Facebookでアプリにログインし、ログアウトして(同じブラウザを使用して)別のFacebookアカウントでログインしようとすると、すぐに以前に使用していたFacebookアカウントにログインします。</span><span class="sxs-lookup"><span data-stu-id="7e12f-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="7e12f-218">別のアカウントを使用するには、Facebookに移動してFacebookでログアウトする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7e12f-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="7e12f-219">同じ規則が他のサード パーティ認証プロバイダにも適用されます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="7e12f-220">別のブラウザを使用して、別のアカウントでログインすることもできます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e12f-221">次の手順</span><span class="sxs-lookup"><span data-stu-id="7e12f-221">Next Steps</span></span>

<span data-ttu-id="7e12f-222">YahooとLinkedInの指示のためのジェリー・ペルサーによる[OWINのためのヤフーとLinkedIn OAuthセキュリティプロバイダの紹介](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="7e12f-223">ソーシャルログインボタンを有効にするには、MVC 5ASP.NETJerrieのかなりソーシャルログインボタンを参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="7e12f-224">このチュートリアルを続けて、次の手順を示す、[認証と SQL DB を使用して ASP.NET MVC アプリを作成し、Azure アプリ サービス にデプロイ](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)するチュートリアルに従ってください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="7e12f-225">アプリを Azure にデプロイする方法。</span><span class="sxs-lookup"><span data-stu-id="7e12f-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="7e12f-226">ロールを使用してアプリを保護する方法。</span><span class="sxs-lookup"><span data-stu-id="7e12f-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="7e12f-227">[RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx)フィルターと[承認](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)フィルターを使用してアプリを保護する方法。</span><span class="sxs-lookup"><span data-stu-id="7e12f-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="7e12f-228">メンバーシップ API を使用してユーザーとロールを追加する方法。</span><span class="sxs-lookup"><span data-stu-id="7e12f-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="7e12f-229">このチュートリアルを気に入った方法と改善できる内容についてのフィードバックを残してください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="7e12f-230">新しいトピックは、「[コードを使用して表示する方法」でも](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)リクエストできます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="7e12f-231">ASP.NETに追加する新機能を要求して投票することもできます。</span><span class="sxs-lookup"><span data-stu-id="7e12f-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="7e12f-232">たとえば、ツールに投票して[、ユーザーとロールを作成および管理できます。](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="7e12f-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="7e12f-233">外部認証サービスの仕組ASP.NET詳細については、 Robert McMurray の[外部認証サービス](https://asp.net/web-api/overview/security/external-authentication-services)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7e12f-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="7e12f-234">ロバートの記事では、マイクロソフトとTwitterの認証を有効にする方法についても詳しく説明しています。</span><span class="sxs-lookup"><span data-stu-id="7e12f-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="7e12f-235">Tom Dykstra の優れた[EF/MVC チュートリアル](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)では、エンティティ フレームワークを操作する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="7e12f-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
