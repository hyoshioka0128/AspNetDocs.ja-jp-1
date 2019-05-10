---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: シングル サインオン (Azure で現実世界のクラウド アプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子書籍で構築実世界クラウド アプリは、Scott Guthrie が開発したプレゼンテーションに基づいています。 13 のパターンとプラクティスを彼がについて説明しています.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 8f6c23eb71ea323b6ab06943097f927f717a8099
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65118743"
---
# <a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="95f4d-104">シングル サインオン (Azure で現実世界のクラウド アプリの構築)</span><span class="sxs-lookup"><span data-stu-id="95f4d-104">Single Sign-On (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="95f4d-105">によって[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson]((https://twitter.com/RickAndMSFT))、 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="95f4d-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="95f4d-106">[ダウンロードその修正プロジェクト](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)または[電子書籍をダウンロード](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="95f4d-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="95f4d-107">**構築現実世界の Cloud Apps with Azure**電子書籍は Scott Guthrie が開発したプレゼンテーションに基づきます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="95f4d-108">13 のパターンについて説明しするのに役立つプラクティスは、クラウドの web アプリの開発が成功します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="95f4d-109">電子書籍の詳細については、次を参照してください。[第 1 章](introduction.md)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="95f4d-110">クラウド アプリを開発しているときに考慮する多くのセキュリティの問題がありますが、このシリーズの 1 つだけに注目します。 シングル サインオンします。</span><span class="sxs-lookup"><span data-stu-id="95f4d-110">There are many security issues to think about when you're developing a cloud app, but for this series we'll focus on just one: single sign-on.</span></span> <span data-ttu-id="95f4d-111">次の質問の質問は"主にビルド アプリ自分の会社の従業員クラウドでのこれらのアプリをホストしてはどうすれば引き続き従業員がいるし、アプリを実行しているときに、オンプレミス環境で使用するのと同じセキュリティ モデルを使用するように有効にするホスト ファイアウォールの内側にでしょうか。"</span><span class="sxs-lookup"><span data-stu-id="95f4d-111">A question people often ask is this: "I'm primarily building apps for the employees of my company; how do I host these apps in the cloud and still enable them to use the same security model that my employees know and use in the on-premises environment when they're running apps that are hosted inside the firewall?"</span></span> <span data-ttu-id="95f4d-112">このシナリオを有効にする方法の 1 つには、Azure Active Directory (Azure AD) が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-112">One of the ways we enable this scenario is called Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="95f4d-113">Azure AD では、エンタープライズ基幹業務 (LOB) アプリ使用できるように、インターネットを経由でき、ビジネス パートナーもこれらのアプリを使用できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-113">Azure AD enables you to make enterprise line-of-business (LOB) apps available over the Internet, and it enables you to make these apps available to business partners as well.</span></span>

## <a name="introduction-to-azure-ad"></a><span data-ttu-id="95f4d-114">Azure AD の概要</span><span class="sxs-lookup"><span data-stu-id="95f4d-114">Introduction to Azure AD</span></span>

<span data-ttu-id="95f4d-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/)提供[Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx)クラウドで。</span><span class="sxs-lookup"><span data-stu-id="95f4d-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) provides [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) in the cloud.</span></span> <span data-ttu-id="95f4d-116">主な機能を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-116">Key features include the following:</span></span>

- <span data-ttu-id="95f4d-117">オンプレミスの Active Directory と統合します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-117">It integrates with on-premises Active Directory.</span></span>
- <span data-ttu-id="95f4d-118">アプリでのシングル サインオンが有効にします。</span><span class="sxs-lookup"><span data-stu-id="95f4d-118">It enables single sign-on with your apps.</span></span>
- <span data-ttu-id="95f4d-119">などのオープン標準をサポートしています[SAML](http://en.wikipedia.org/wiki/SAML_2.0)、 [Ws-fed](http://en.wikipedia.org/wiki/WS-Federation)、および[OAuth 2.0](http://oauth.net/2/)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-119">It supports open standards such as [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-Fed](http://en.wikipedia.org/wiki/WS-Federation), and [OAuth 2.0](http://oauth.net/2/).</span></span>
- <span data-ttu-id="95f4d-120">エンタープライズがサポートしている[Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-120">It supports Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx).</span></span>

<span data-ttu-id="95f4d-121">イントラネット アプリケーションにサインオンする従業員を有効化に使用するオンプレミス Windows Server Active Directory 環境があるとします。</span><span class="sxs-lookup"><span data-stu-id="95f4d-121">Suppose you have an on-premises Windows Server Active Directory environment that you use to enable employees to sign on to Intranet apps:</span></span>

![](single-sign-on/_static/image1.png)

<span data-ttu-id="95f4d-122">クラウドにディレクトリを作成は、どのような Azure AD を使用する操作を行います。</span><span class="sxs-lookup"><span data-stu-id="95f4d-122">What Azure AD enables you to do is create a directory in the cloud.</span></span> <span data-ttu-id="95f4d-123">これは無料の機能と簡単にセットアップできます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-123">It's a free feature and easy to set up.</span></span>

<span data-ttu-id="95f4d-124">オンプレミスの Active Directory; から完全に独立したできます。すべてのユーザーが選択して、インターネットからアプリに認証を配置することができます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-124">It can be entirely independent from your on-premises Active Directory; you can put anyone you want in it and authenticate them in Internet apps.</span></span>

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

<span data-ttu-id="95f4d-126">オンプレミスと統合することができます AD。</span><span class="sxs-lookup"><span data-stu-id="95f4d-126">Or you can integrate it with your on-premises AD.</span></span>

![AD と WAAD の統合](single-sign-on/_static/image3.png)

<span data-ttu-id="95f4d-128">これで、オンプレミスで認証できるすべての従業員は、ファイアウォールを開くか、データ センター内の新しいサーバーをデプロイする必要がありません – インターネット経由で認証もできます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-128">Now all the employees who can authenticate on-premises can also authenticate over the Internet – without you having to open up a firewall or deploy any new servers in your data center.</span></span> <span data-ttu-id="95f4d-129">すべての既存 Active Directory 環境を把握し、現在使用して、内部アプリのシングル サインオンを機能に与えるを活用する続行することができます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-129">You can continue to leverage all the existing Active Directory environment that you know and use today to give your internal apps single-sign on capability.</span></span>

<span data-ttu-id="95f4d-130">AD と Azure AD の間には、この接続を確立した後に、web アプリと、従業員、クラウドでの認証にモバイル デバイスを有効することも受け入れるように、Office 365、SalesForce.com、または Google apps などのサードパーティ製アプリを有効にすることができます、従業員の資格情報。</span><span class="sxs-lookup"><span data-stu-id="95f4d-130">Once you've made this connection between AD and Azure AD, you can also enable your web apps and your mobile devices to authenticate your employees in the cloud, and you can enable third-party apps, such as Office 365, SalesForce.com, or Google apps, to accept your employees' credentials.</span></span> <span data-ttu-id="95f4d-131">Office 365 を使用している場合既にセットアップが Azure AD と Office 365 では、Azure AD を使用して、認証と承認するためです。</span><span class="sxs-lookup"><span data-stu-id="95f4d-131">If you're using Office 365, you're already set up with Azure AD because Office 365 uses Azure AD for authentication and authorization.</span></span>

![サード パーティ製アプリ](single-sign-on/_static/image4.png)

<span data-ttu-id="95f4d-133">このアプローチの美しさはいつでも、組織を追加またはユーザーを削除またはユーザーがパスワードを変更する、オンプレミス環境で現在使用されている同じプロセスを使用します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-133">The beauty of this approach is that any time your organization adds or deletes a user, or a user changes a password, you use the same process that you use today in your on-premises environment.</span></span> <span data-ttu-id="95f4d-134">すべてで、オンプレミスの AD 変更を自動的に、クラウド環境を反映します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-134">All of your on-premises AD changes are automatically propagated to the cloud environment.</span></span>

<span data-ttu-id="95f4d-135">会社を使用して良い知らせは、Office 365 に移行する場合は、Azure AD の Office 365 では、Azure AD を使用して、認証するために自動的にセットアップを必要があります。</span><span class="sxs-lookup"><span data-stu-id="95f4d-135">If your company is using or moving to Office 365, the good news is that you'll have Azure AD set up automatically because Office 365 uses Azure AD for authentication.</span></span> <span data-ttu-id="95f4d-136">このため、簡単に独自のアプリでは、Office 365 を使用する同じ認証を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-136">So you can easily use in your own apps the same authentication that Office 365 uses.</span></span>

## <a name="set-up-an-azure-ad-tenant"></a><span data-ttu-id="95f4d-137">Azure AD テナントをセットアップします。</span><span class="sxs-lookup"><span data-stu-id="95f4d-137">Set up an Azure AD tenant</span></span>

<span data-ttu-id="95f4d-138">Azure AD ディレクトリが、Azure AD と呼ばれる[テナント](https://technet.microsoft.com/library/jj573650.aspx)、し、テナントを設定することは非常に簡単です。</span><span class="sxs-lookup"><span data-stu-id="95f4d-138">an Azure AD directory is called an Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx), and setting up a tenant is pretty easy.</span></span> <span data-ttu-id="95f4d-139">紹介する方法の概念を説明するために、Azure 管理ポータルで行われますが、もちろん他のポータルの関数と同様に行うこともできますが、スクリプトまたは管理 API を使用しています。</span><span class="sxs-lookup"><span data-stu-id="95f4d-139">We'll show you how it's done in the Azure Management Portal in order to illustrate the concepts, but of course like the other portal functions you can also do it by using a script or management API.</span></span>

<span data-ttu-id="95f4d-140">管理ポータルでは、Active Directory タブをクリックします。</span><span class="sxs-lookup"><span data-stu-id="95f4d-140">In the management portal click the Active Directory tab.</span></span>

![ポータルで WAAD](single-sign-on/_static/image5.png)

<span data-ttu-id="95f4d-142">自動的に、Azure のアカウントの 1 つの Azure AD テナントがあるし、クリックすることができます、**追加**追加のディレクトリを作成するページの下部にあるボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="95f4d-142">You automatically have one Azure AD tenant for your Azure account, and you can click the **Add** button at the bottom of the page to create additional directories.</span></span> <span data-ttu-id="95f4d-143">テスト環境用と運用環境で 1 つは、たとえばする可能性があります。</span><span class="sxs-lookup"><span data-stu-id="95f4d-143">You might want one for a test environment and one for production, for example.</span></span> <span data-ttu-id="95f4d-144">新しいディレクトリの名前について慎重に検討します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-144">Think carefully about what you name a new directory.</span></span> <span data-ttu-id="95f4d-145">いずれかの混乱を招くことができると、ユーザー用にもう一度、名前を使用し、ディレクトリの名前を使用する場合。</span><span class="sxs-lookup"><span data-stu-id="95f4d-145">If you use your name for the directory and then you use your name again for one of the users, that can be confusing.</span></span>

![ディレクトリを追加します。](single-sign-on/_static/image6.png)

<span data-ttu-id="95f4d-147">ポータルでは、作成、削除、およびこの環境内でユーザーを管理する完全にサポートがあります。</span><span class="sxs-lookup"><span data-stu-id="95f4d-147">The portal has full support for creating, deleting, and managing users within this environment.</span></span> <span data-ttu-id="95f4d-148">たとえば、追加ユーザーに移動、**ユーザー**  タブでをクリックし、**ユーザーの追加**ボタン。</span><span class="sxs-lookup"><span data-stu-id="95f4d-148">For example, to add a user go to the **Users** tab and click the **Add User** button.</span></span>

![ユーザー ボタンを追加します。](single-sign-on/_static/image7.png)

![追加ユーザー ダイアログ ボックス](single-sign-on/_static/image8.png)

<span data-ttu-id="95f4d-151">存在する新しいユーザーを作成するには、このディレクトリにのみ、またはこのディレクトリ内のユーザーとして、このディレクトリのユーザー登録または別の Azure AD ディレクトリのユーザーとして Microsoft アカウントを登録することができます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-151">You can create a new user who exists only in this directory, or you can register a Microsoft Account as a user in this directory, or register or a user from another Azure AD directory as a user in this directory.</span></span> <span data-ttu-id="95f4d-152">(実際のディレクトリに既定のドメインになります ContosoTest.onmicrosoft.com します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-152">(In a real directory, the default domain would be ContosoTest.onmicrosoft.com.</span></span> <span data-ttu-id="95f4d-153">使用することできますも、ドメインの contoso.com のような独自に選択します。)</span><span class="sxs-lookup"><span data-stu-id="95f4d-153">You can also use a domain of your own choosing, like contoso.com.)</span></span>

![ユーザーの種類](single-sign-on/_static/image9.png)

![追加ユーザー ダイアログ ボックス](single-sign-on/_static/image10.png)

<span data-ttu-id="95f4d-156">ロールにユーザーを割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-156">You can assign the user to a role.</span></span>

![ユーザー プロファイル](single-sign-on/_static/image11.png)

<span data-ttu-id="95f4d-158">一時パスワードを使用して、アカウントが作成されます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-158">And the account is created with a temporary password.</span></span>

![一時パスワード](single-sign-on/_static/image12.png)

<span data-ttu-id="95f4d-160">この方法で作成したユーザーは、このクラウド ディレクトリを使用して、web アプリにすぐにログインできます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-160">The users you create this way can immediately log in to your web apps using this cloud directory.</span></span>

<span data-ttu-id="95f4d-161">エンタープライズ シングル サインオン、優れた新、**ディレクトリ統合** タブ。</span><span class="sxs-lookup"><span data-stu-id="95f4d-161">What's great for enterprise single sign-on, though, is the **Directory Integration** tab:</span></span>

![ディレクトリ統合 タブ](single-sign-on/_static/image13.png)

<span data-ttu-id="95f4d-163">ディレクトリの統合を有効にした場合と[ツールをダウンロード](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)組織内で既に使用している既存のオンプレミス Active Directory とは、このクラウド ディレクトリを同期することができます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-163">If you enable directory integration, and [download a tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), you can sync this cloud directory with your existing on-premises Active Directory that you're already using inside your organization.</span></span> <span data-ttu-id="95f4d-164">このクラウド ディレクトリ ディレクトリに格納されているユーザーをすべて表示されます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-164">Then all of the users stored in your directory will show up in this cloud directory.</span></span> <span data-ttu-id="95f4d-165">クラウド アプリでは、すべての既存の Active Directory の資格情報を使用して、従業員の認証できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="95f4d-165">Your cloud apps can now authenticate all of your employees using their existing Active Directory credentials.</span></span> <span data-ttu-id="95f4d-166">同期ツールと Azure AD 自体 – これはすべて無料です。</span><span class="sxs-lookup"><span data-stu-id="95f4d-166">And all this is free – both the sync tool and Azure AD itself.</span></span>

<span data-ttu-id="95f4d-167">このツールは、これらのスクリーン ショットからわかるように、簡単に使用するウィザードです。</span><span class="sxs-lookup"><span data-stu-id="95f4d-167">The tool is a wizard that is easy to use, as you can see from these screen shots.</span></span> <span data-ttu-id="95f4d-168">これらは完全な手順については、基本的なプロセスを示すほんの一例ではありません。</span><span class="sxs-lookup"><span data-stu-id="95f4d-168">These are not complete instructions, just an example showing you the basic process.</span></span> <span data-ttu-id="95f4d-169">詳細な方法を操作を行います it に関する情報は、内のリンクを参照してください、[リソース](#resources)章の最後のセクション。</span><span class="sxs-lookup"><span data-stu-id="95f4d-169">For more detailed how-to-do-it information, see the links in the [Resources](#resources) section at the end of the chapter.</span></span>

![WAAD 同期ツール構成ウィザード](single-sign-on/_static/image14.png)

<span data-ttu-id="95f4d-171">クリックして**次**、Azure Active Directory の資格情報を入力します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-171">Click **Next**, and then enter your Azure Active Directory credentials.</span></span>

![WAAD 同期ツール構成ウィザード](single-sign-on/_static/image15.png)

<span data-ttu-id="95f4d-173">をクリックして **[次へ]**、して enter、オンプレミス AD の資格情報。</span><span class="sxs-lookup"><span data-stu-id="95f4d-173">Click **Next**, and then enter your on-premises AD credentials.</span></span>

![WAAD 同期ツール構成ウィザード](single-sign-on/_static/image16.png)

<span data-ttu-id="95f4d-175">クリックして**次**、され、クラウドでの AD パスワードのハッシュを格納することを示します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-175">Click **Next**, and then indicate if you want to store a hash of your AD passwords in the cloud.</span></span>

![WAAD 同期ツール構成ウィザード](single-sign-on/_static/image17.png)

<span data-ttu-id="95f4d-177">クラウドに格納できるパスワード ハッシュは、一方向のハッシュです。実際のパスワードは、Azure AD では格納されません。</span><span class="sxs-lookup"><span data-stu-id="95f4d-177">The password hash that you can store in the cloud is a one-way hash; actual passwords are never stored in Azure AD.</span></span> <span data-ttu-id="95f4d-178">使用する必要がありますに対して、クラウドにハッシュを格納する場合は、 [Active Directory フェデレーション サービス](https://technet.microsoft.com/library/hh831502.aspx)(ADFS)。</span><span class="sxs-lookup"><span data-stu-id="95f4d-178">If you decide against storing hashes in the cloud, you'll have to use [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span></span> <span data-ttu-id="95f4d-179">[ときに考慮するその他の要因 ADFS を使用するかどうかを選択する](https://technet.microsoft.com/library/jj573653.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-179">There are also [other factors to consider when choosing whether or not to use ADFS](https://technet.microsoft.com/library/jj573653.aspx).</span></span> <span data-ttu-id="95f4d-180">ADFS オプションには、いくつかの追加の構成手順が必要です。</span><span class="sxs-lookup"><span data-stu-id="95f4d-180">The ADFS option requires a few additional configuration steps.</span></span>

<span data-ttu-id="95f4d-181">クラウドでハッシュを格納するか、完了したら、およびツールをクリックするとディレクトリの同期を開始する場合**次**します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-181">If you choose to store hashes in the cloud, you're done, and the tool starts synchronizing directories when you click **Next**.</span></span>

![WAAD 同期ツール構成ウィザード](single-sign-on/_static/image18.png)

<span data-ttu-id="95f4d-183">数分で完了します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-183">And in a few minutes you're done.</span></span>

![WAAD 同期ツール構成ウィザード](single-sign-on/_static/image19.png)

<span data-ttu-id="95f4d-185">のみ、これ以上 Windows 2003 では、組織内の 1 つのドメイン コント ローラー上で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="95f4d-185">You only have to run this on one domain controller in the organization, on Windows 2003 or higher.</span></span> <span data-ttu-id="95f4d-186">再起動する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="95f4d-186">And no need to reboot.</span></span> <span data-ttu-id="95f4d-187">完了すると、すべてのユーザーは、クラウド、行うことができますから任意の web またはモバイル アプリケーション、SAML、OAuth、Ws-fed を使用してシングル サインオンします。</span><span class="sxs-lookup"><span data-stu-id="95f4d-187">When you're done, all of your users are in the cloud and you can do single sign-on from any web or mobile application, using SAML, OAuth, or WS-Fed.</span></span>

<span data-ttu-id="95f4d-188">これは、セキュリティで保護する方法について尋ね場合があります: は Microsoft を使用して、機密性の高いビジネス データのでしょうか。</span><span class="sxs-lookup"><span data-stu-id="95f4d-188">Sometimes we get asked about how secure this is – does Microsoft use it for their own sensitive business data?</span></span> <span data-ttu-id="95f4d-189">答えはイエスでしょう。</span><span class="sxs-lookup"><span data-stu-id="95f4d-189">And the answer is yes we do.</span></span> <span data-ttu-id="95f4d-190">内部の Microsoft SharePoint サイトにアクセスする場合など、 [ https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/)にログインするように求めを取得します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-190">For example, if you go to the internal Microsoft SharePoint site at [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), you get prompted to log in.</span></span>

![Office 365 のサインイン](single-sign-on/_static/image20.png)

<span data-ttu-id="95f4d-192">Microsoft では、ADFS が有効になって Microsoft ID を入力すると、ADFS ログイン ページにリダイレクトを取得するようにします。</span><span class="sxs-lookup"><span data-stu-id="95f4d-192">Microsoft has enabled ADFS, so when you enter a Microsoft ID, you get redirected to an ADFS log-in page.</span></span>

![Ad FS のサインイン](single-sign-on/_static/image21.png)

<span data-ttu-id="95f4d-194">内部の Microsoft の AD アカウントに格納されている資格情報を入力すると、この内部アプリケーションへのアクセスがあります。</span><span class="sxs-lookup"><span data-stu-id="95f4d-194">And once you enter credentials stored in an internal Microsoft AD account, you have access to this internal application.</span></span>

![MS の SharePoint サイト](single-sign-on/_static/image22.png)

<span data-ttu-id="95f4d-196">私たちは既に ADFS が Azure AD が、使用できるようになりましたが、ログイン プロセスは、クラウドで Azure AD ディレクトリを通過する前に設定するために主に AD のサインインにサーバーを使います。</span><span class="sxs-lookup"><span data-stu-id="95f4d-196">We're using an AD sign-in server mainly because we already had ADFS set up before Azure AD became available, but the log-in process is going through an Azure AD directory in the cloud.</span></span> <span data-ttu-id="95f4d-197">当社の重要なドキュメント、ソース管理、パフォーマンス管理ファイル、売上レポート、および詳細は、クラウドでの配置し、それらをセキュリティで保護する正確なこれと同じソリューションを使用しています。</span><span class="sxs-lookup"><span data-stu-id="95f4d-197">We put our important documents, source control, performance management files, sales reports, and more, in the cloud and are using this exact same solution to secure them.</span></span>

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a><span data-ttu-id="95f4d-198">Azure AD シングル サインオンを使用する ASP.NET アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-198">Create an ASP.NET app that uses Azure AD for single sign-on</span></span>

<span data-ttu-id="95f4d-199">Visual Studio では、実に容易にいくつかのスクリーン ショットからわかるように、Azure AD シングル サインオンを使用するアプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-199">Visual Studio makes it really easy to create an app that uses Azure AD for single sign-on, as you can see from a few screen shots.</span></span>

<span data-ttu-id="95f4d-200">MVC または Web フォームでは、新しい ASP.NET アプリケーションを作成するときに既定の認証方法は、ASP.NET の Id です。</span><span class="sxs-lookup"><span data-stu-id="95f4d-200">When you create a new ASP.NET application, either MVC or Web Forms, the default authentication method is ASP.NET Identity.</span></span> <span data-ttu-id="95f4d-201">Azure AD に変更をクリックする、**認証の変更**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="95f4d-201">To change that to Azure AD, you click a **Change Authentication** button.</span></span>

![認証の変更](single-sign-on/_static/image23.png)

<span data-ttu-id="95f4d-203">組織アカウントを選択、ドメイン名を入力し、シングル サインオンの します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-203">Select Organizational Accounts, enter your domain name, and then select Single Sign On.</span></span>

![認証ダイアログ ボックスを構成します。](single-sign-on/_static/image24.png)

<span data-ttu-id="95f4d-205">こともアプリの読み取りまたは読み取り/書き込みディレクトリ データに対するアクセス許可。</span><span class="sxs-lookup"><span data-stu-id="95f4d-205">You can also give the app read or read/write permission for directory data.</span></span> <span data-ttu-id="95f4d-206">使用できるようにする場合、 [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx)をユーザーの電話番号を調べる調べる on などの前回のログインするときに、オフィスにいるかどうか。</span><span class="sxs-lookup"><span data-stu-id="95f4d-206">If you do that, it can use the [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) to look up users' phone number, find out if they're in the office, when they last logged on, etc.</span></span>

<span data-ttu-id="95f4d-207">実行する必要がある Visual Studio を要求する資格情報、Azure AD テナントの管理者と、プロジェクトと新しいアプリケーションに Azure AD テナントの両方を構成します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-207">That's all you have to do - Visual Studio asks for the credentials for an administrator for your Azure AD tenant, and then it configures both your project and your Azure AD tenant for the new application.</span></span>

<span data-ttu-id="95f4d-208">プロジェクトを実行して、サインイン ページが表示されます、Azure AD ディレクトリでユーザーの資格情報でサインインすることができます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-208">When you run the project, you'll see a sign-in page, and you can sign in with credentials of a user in your Azure AD directory.</span></span>

![組織アカウントのサインイン](single-sign-on/_static/image25.png)

![ログに記録](single-sign-on/_static/image26.png)

<span data-ttu-id="95f4d-211">アプリを Azure にデプロイするときに行う必要があるすべてが選択されて、**組織認証を有効にする**チェック ボックスをオンし、もう一度 Visual Studio のすべての構成を行います。 します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-211">When you deploy the app to Azure, all you have to do is select an **Enable Organizational Authentication** check box, and once again Visual Studio takes care of all the configuration for you.</span></span>

![Web を発行します。](single-sign-on/_static/image27.png)

<span data-ttu-id="95f4d-213">これらのスクリーン ショットは、Azure AD 認証を使用するアプリをビルドする方法を示す完全なステップ バイ ステップ チュートリアルから取得されます。[Azure Active Directory と ASP.NET アプリの開発](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-213">These screen shots come from a complete step-by-step tutorial that shows how to build an app that uses Azure AD authentication: [Developing ASP.NET Apps with Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span></span>

## <a name="summary"></a><span data-ttu-id="95f4d-214">まとめ</span><span class="sxs-lookup"><span data-stu-id="95f4d-214">Summary</span></span>

<span data-ttu-id="95f4d-215">この章では、Azure Active Directory、Visual Studio および ASP.NET をしやすく、組織のユーザーのインターネット アプリケーションでシングル サインオンを設定する説明しました。</span><span class="sxs-lookup"><span data-stu-id="95f4d-215">In this chapter you saw that Azure Active Directory, Visual Studio, and ASP.NET, make it easy to set up single sign-on in Internet applications for your organization's users.</span></span> <span data-ttu-id="95f4d-216">ユーザーは、Active Directory を使用して、内部ネットワークでのサインオンに使用するのと同じ資格情報を使用してアプリをインターネットでサインオンできます。</span><span class="sxs-lookup"><span data-stu-id="95f4d-216">Your users can sign on in Internet apps using the same credentials they use to sign on using Active Directory in your internal network.</span></span>

<span data-ttu-id="95f4d-217">[[次へ] の章](data-storage-options.md)クラウド アプリの使用可能なデータ ストレージ オプションになります。</span><span class="sxs-lookup"><span data-stu-id="95f4d-217">The [next chapter](data-storage-options.md) looks at the data storage options available for a cloud app.</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="95f4d-218">リソース</span><span class="sxs-lookup"><span data-stu-id="95f4d-218">Resources</span></span>

<span data-ttu-id="95f4d-219">詳細については、次のリソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="95f4d-219">For more information, see the following resources:</span></span>

- <span data-ttu-id="95f4d-220">[Azure Active Directory のドキュメント](https://docs.microsoft.com/azure/active-directory/)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-220">[Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="95f4d-221">Windowsazure.com サイトのドキュメントについては Azure AD ポータルのページです。</span><span class="sxs-lookup"><span data-stu-id="95f4d-221">Portal page for Azure AD documentation on the windowsazure.com site.</span></span> <span data-ttu-id="95f4d-222">ステップ バイ ステップ チュートリアルについては、次を参照してください。、**開発**セクション。</span><span class="sxs-lookup"><span data-stu-id="95f4d-222">For step by step tutorials, see the **Develop** section.</span></span>
- <span data-ttu-id="95f4d-223">[Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-223">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/).</span></span> <span data-ttu-id="95f4d-224">Azure で多要素認証に関するドキュメントについてはポータル ページです。</span><span class="sxs-lookup"><span data-stu-id="95f4d-224">Portal page for documentation about multi-factor authentication in Azure.</span></span>
- <span data-ttu-id="95f4d-225">[組織アカウントの認証オプション](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-225">[Organizational account authentication options](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions).</span></span> <span data-ttu-id="95f4d-226">Visual Studio 2013 の [新しいプロジェクト] ダイアログ ボックスで、Azure AD の認証オプションの説明です。</span><span class="sxs-lookup"><span data-stu-id="95f4d-226">Explanation of the Azure AD authentication options in the Visual Studio 2013 new-project dialog.</span></span>
- <span data-ttu-id="95f4d-227">[Microsoft Patterns and Practices - フェデレーション Id パターン](https://msdn.microsoft.com/library/dn589790.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-227">[Microsoft Patterns and Practices - Federated Identity Pattern](https://msdn.microsoft.com/library/dn589790.aspx).</span></span>
- <span data-ttu-id="95f4d-228">[方法:Azure Active Directory Sync ツールのインストール](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-228">[HowTo: Install the Azure Active Directory Sync Tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span></span>
- <span data-ttu-id="95f4d-229">[Active Directory フェデレーション サービス 2.0 コンテンツ マップ](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-229">[Active Directory Federation Services 2.0 Content Map](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span></span> <span data-ttu-id="95f4d-230">ADFS 2.0 に関するドキュメントへのリンク。</span><span class="sxs-lookup"><span data-stu-id="95f4d-230">Links to documentation about ADFS 2.0.</span></span>
- <span data-ttu-id="95f4d-231">[Windows Azure AD アプリケーションでのロールベースおよび ACL ベース承認](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-231">[Role-Based and ACL-Based Authorization in a Windows Azure AD Application](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span></span> <span data-ttu-id="95f4d-232">サンプル アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="95f4d-232">Sample application.</span></span>
- <span data-ttu-id="95f4d-233">[Azure Active Directory Graph API ブログ](https://blogs.msdn.com/b/aadgraphteam/)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-233">[Azure Active Directory Graph API blog](https://blogs.msdn.com/b/aadgraphteam/).</span></span>
- <span data-ttu-id="95f4d-234">[アクセス制御では、BYOD と Directory ハイブリッド Id インフラストラクチャを統合](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)します。</span><span class="sxs-lookup"><span data-stu-id="95f4d-234">[Access Control in BYOD and Directory Integration in a Hybrid Identity Infrastructure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span></span> <span data-ttu-id="95f4d-235">Tech Ed 2014 セッション ビデオ Gayana Bagdasaryan によってです。</span><span class="sxs-lookup"><span data-stu-id="95f4d-235">Tech Ed 2014 session video by Gayana Bagdasaryan.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="95f4d-236">[前へ](web-development-best-practices.md)
> [次へ](data-storage-options.md)</span><span class="sxs-lookup"><span data-stu-id="95f4d-236">[Previous](web-development-best-practices.md)
[Next](data-storage-options.md)</span></span>
