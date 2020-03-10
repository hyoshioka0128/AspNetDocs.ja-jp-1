---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Katana で Windows 認証を有効にする |Microsoft Docs
author: MikeWasson
description: この記事では、Katana で Windows 認証を有効にする方法について説明します。 この例では、IIS を使用して Katana をホストし、HttpListener を使用して自己ホスト Kat...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500296"
---
# <a name="enabling-windows-authentication-in-katana"></a><span data-ttu-id="30f64-104">Katana で Windows 認証を有効にする</span><span class="sxs-lookup"><span data-stu-id="30f64-104">Enabling Windows Authentication in Katana</span></span>

<span data-ttu-id="30f64-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="30f64-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="30f64-106">この記事では、Katana で Windows 認証を有効にする方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="30f64-106">This article shows how to enable Windows Authentication in Katana.</span></span> <span data-ttu-id="30f64-107">この記事では、IIS を使用して Katana をホストし、HttpListener を使用してカスタムプロセスで自己ホスト Katana を使用する2つのシナリオについて説明します。</span><span class="sxs-lookup"><span data-stu-id="30f64-107">It covers two scenarios: Using IIS to host Katana, and using HttpListener to self-host Katana in a custom process.</span></span> <span data-ttu-id="30f64-108">この記事を確認するには、Dorrans、David Matson、Chris Ross に感謝します。</span><span class="sxs-lookup"><span data-stu-id="30f64-108">Thanks to Barry Dorrans, David Matson, and Chris Ross for reviewing this article.</span></span>

<span data-ttu-id="30f64-109">Katana は、.NET 用の Open Web Interface である[OWIN](http://owin.org/)の Microsoft の実装です。</span><span class="sxs-lookup"><span data-stu-id="30f64-109">Katana is Microsoft's implementation of [OWIN](http://owin.org/), the Open Web Interface for .NET.</span></span> <span data-ttu-id="30f64-110">OWIN と Katana の概要については、[こちら](an-overview-of-project-katana.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="30f64-110">You can read an introduction to OWIN and Katana [here](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="30f64-111">OWIN アーキテクチャには、いくつかのレイヤーがあります。</span><span class="sxs-lookup"><span data-stu-id="30f64-111">The OWIN architecture has several layers:</span></span>

- <span data-ttu-id="30f64-112">Host: OWIN パイプラインを実行するプロセスを管理します。</span><span class="sxs-lookup"><span data-stu-id="30f64-112">Host: Manages the process in which the OWIN pipeline runs.</span></span>
- <span data-ttu-id="30f64-113">サーバー: ネットワークソケットを開き、要求をリッスンします。</span><span class="sxs-lookup"><span data-stu-id="30f64-113">Server: Opens a network socket and listens for requests.</span></span>
- <span data-ttu-id="30f64-114">ミドルウェア: HTTP 要求と応答を処理します。</span><span class="sxs-lookup"><span data-stu-id="30f64-114">Middleware: Processes the HTTP request and response.</span></span>

<span data-ttu-id="30f64-115">現在、Katana には2つのサーバーがあり、どちらも Windows 統合認証をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="30f64-115">Katana currently provides two servers, both of which support Windows Integrated Authentication:</span></span>

- <span data-ttu-id="30f64-116">**Owin**のようになります。</span><span class="sxs-lookup"><span data-stu-id="30f64-116">**Microsoft.Owin.Host.SystemWeb**.</span></span> <span data-ttu-id="30f64-117">IIS を ASP.NET パイプラインと共に使用します。</span><span class="sxs-lookup"><span data-stu-id="30f64-117">Uses IIS with the ASP.NET pipeline.</span></span>
- <span data-ttu-id="30f64-118">**Owin. HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="30f64-118">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="30f64-119">[HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)を使用します。</span><span class="sxs-lookup"><span data-stu-id="30f64-119">Uses [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span></span> <span data-ttu-id="30f64-120">Katana を自己ホストする場合、このサーバーは現在既定のオプションです。</span><span class="sxs-lookup"><span data-stu-id="30f64-120">This server is currently the default option when self-hosting Katana.</span></span>

> [!NOTE]
> <span data-ttu-id="30f64-121">Katana では、現在、Windows 認証の OWIN ミドルウェアは提供されていません。この機能は既にサーバーで使用可能になっているためです。</span><span class="sxs-lookup"><span data-stu-id="30f64-121">Katana does not currently provide OWIN middleware for Windows Authentication, because this functionality is already available in the servers.</span></span>

## <a name="windows-authentication-in-iis"></a><span data-ttu-id="30f64-122">IIS での Windows 認証</span><span class="sxs-lookup"><span data-stu-id="30f64-122">Windows Authentication in IIS</span></span>

<span data-ttu-id="30f64-123">Owin を使用すると、IIS で Windows 認証を有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="30f64-123">Using Microsoft.Owin.Host.SystemWeb, you can simply enable Windows Authentication in IIS.</span></span>

<span data-ttu-id="30f64-124">まず、"ASP.NET Empty Web Application" プロジェクトテンプレートを使用して、新しい ASP.NET アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="30f64-124">Let's start by creating a new ASP.NET application, using the "ASP.NET Empty Web Application" project template.</span></span>

![](enabling-windows-authentication-in-katana/_static/image1.png)

<span data-ttu-id="30f64-125">次に、NuGet パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="30f64-125">Next, add NuGet packages.</span></span> <span data-ttu-id="30f64-126">**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="30f64-126">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="30f64-127">[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="30f64-127">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

<span data-ttu-id="30f64-128">ここで、次のコードを使用して、`Startup` という名前のクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="30f64-128">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

<span data-ttu-id="30f64-129">これで、IIS で実行される OWIN 用の "Hello world" アプリケーションを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="30f64-129">That's all you need to create a "Hello world" application for OWIN, running on IIS.</span></span> <span data-ttu-id="30f64-130">F5 キーを押してアプリケーションをデバッグします。</span><span class="sxs-lookup"><span data-stu-id="30f64-130">Press F5 to debug the application.</span></span> <span data-ttu-id="30f64-131">"Hello World!" が</span><span class="sxs-lookup"><span data-stu-id="30f64-131">You should see "Hello World!"</span></span> <span data-ttu-id="30f64-132">ブラウザーウィンドウに表示されます。</span><span class="sxs-lookup"><span data-stu-id="30f64-132">in the browser window.</span></span>

![](enabling-windows-authentication-in-katana/_static/image2.png)

<span data-ttu-id="30f64-133">次に、IIS Express で Windows 認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="30f64-133">Next, we'll enable Windows Authentication in IIS Express.</span></span> <span data-ttu-id="30f64-134">**[表示]** メニューの **[プロパティ]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="30f64-134">From the **View** menu, select **Properties**.</span></span> <span data-ttu-id="30f64-135">プロジェクトのプロパティを表示するには、ソリューションエクスプローラーでプロジェクト名をクリックします。</span><span class="sxs-lookup"><span data-stu-id="30f64-135">Click on the project name in Solution Explorer to view the project properties.</span></span>

<span data-ttu-id="30f64-136">**[プロパティ]** ウィンドウで、 **[匿名認証]** を **[無効]** に設定し、 **[Windows 認証]** を **[有効]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="30f64-136">In the **Properties** window, set **Anonymous Authentication** to **Disabled** and set **Windows Authentication** to **Enabled**.</span></span>

![](enabling-windows-authentication-in-katana/_static/image3.png)

<span data-ttu-id="30f64-137">Visual Studio からアプリケーションを実行する場合、IIS Express にはユーザーの Windows 資格情報が必要です。</span><span class="sxs-lookup"><span data-stu-id="30f64-137">When you run the application from Visual Studio, IIS Express will require the user's Windows credentials.</span></span> <span data-ttu-id="30f64-138">これは、 [Fiddler](http://fiddler2.com/home)または別の HTTP デバッグツールを使用して確認できます。</span><span class="sxs-lookup"><span data-stu-id="30f64-138">You can see this by using [Fiddler](http://fiddler2.com/home) or another HTTP debugging tool.</span></span> <span data-ttu-id="30f64-139">HTTP 応答の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="30f64-139">Here is an example HTTP response:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

<span data-ttu-id="30f64-140">この応答の WWW-認証ヘッダーは、サーバーが[Negotiate](http://www.ietf.org/rfc/rfc4559.txt)プロトコルをサポートしていることを示します。これは、Kerberos または NTLM のいずれかを使用します。</span><span class="sxs-lookup"><span data-stu-id="30f64-140">The WWW-Authenticate headers in this response indicate that the server supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protocol, which uses either Kerberos or NTLM.</span></span>

<span data-ttu-id="30f64-141">後で、アプリケーションをサーバーに展開するときに、[次の手順](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)に従って、そのサーバー上の IIS で Windows 認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="30f64-141">Later, when you deploy the application to a server, follow [these steps](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) to enable Windows Authentication in IIS on that server.</span></span>

## <a name="windows-authentication-in-httplistener"></a><span data-ttu-id="30f64-142">HttpListener での Windows 認証</span><span class="sxs-lookup"><span data-stu-id="30f64-142">Windows Authentication in HttpListener</span></span>

<span data-ttu-id="30f64-143">HttpListener を自己ホスト Katana に使用している場合は、 **HttpListener**インスタンスで Windows 認証を直接有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="30f64-143">If you are using Microsoft.Owin.Host.HttpListener to self-host Katana, you can enable Windows Authentication directly on the **HttpListener** instance.</span></span>

<span data-ttu-id="30f64-144">まず、新しいコンソールアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="30f64-144">First, create a new console application.</span></span> <span data-ttu-id="30f64-145">次に、NuGet パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="30f64-145">Next, add NuGet packages.</span></span> <span data-ttu-id="30f64-146">**[ツール]** メニューの **[NuGet パッケージマネージャー]** を選択し、 **[パッケージマネージャーコンソール]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="30f64-146">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="30f64-147">[パッケージ マネージャー コンソール] ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="30f64-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

<span data-ttu-id="30f64-148">ここで、次のコードを使用して、`Startup` という名前のクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="30f64-148">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

<span data-ttu-id="30f64-149">このクラスは、以前と同じ "Hello world" の例を実装しますが、認証スキームとして Windows 認証を設定します。</span><span class="sxs-lookup"><span data-stu-id="30f64-149">This class implements the same "Hello world" example from before, but it also sets Windows Authentication as the authentication scheme.</span></span>

<span data-ttu-id="30f64-150">`Main` 関数内で、OWIN パイプラインを開始します。</span><span class="sxs-lookup"><span data-stu-id="30f64-150">Inside the `Main` function, start the OWIN pipeline:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

<span data-ttu-id="30f64-151">Fiddler で要求を送信して、アプリケーションが Windows 認証を使用していることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="30f64-151">You can send a request in Fiddler to confirm that the application is using Windows Authentication:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a><span data-ttu-id="30f64-152">関連トピック</span><span class="sxs-lookup"><span data-stu-id="30f64-152">Related Topics</span></span>

[<span data-ttu-id="30f64-153">プロジェクト Katana の概要</span><span class="sxs-lookup"><span data-stu-id="30f64-153">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)

[<span data-ttu-id="30f64-154">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="30f64-154">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[<span data-ttu-id="30f64-155">MVC 5 での OWIN フォーム認証について</span><span class="sxs-lookup"><span data-stu-id="30f64-155">Understanding OWIN Forms Authentication in MVC 5</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
