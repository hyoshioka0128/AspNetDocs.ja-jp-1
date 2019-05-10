---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Azure Worker ロールで OWIN ホスト |Microsoft Docs
author: MikeWasson
description: このチュートリアルでは、Microsoft Azure worker ロールで OWIN を自己ホストする方法を示します。 Open Web Interface for .NET (OWIN) は、.NET の web サーバー間の抽象化を定義しています.
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 59d2e0d549427093f8a2424b17af81169b78ef30
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65118262"
---
# <a name="host-owin-in-an-azure-worker-role"></a><span data-ttu-id="dad92-104">Azure Worker ロールで OWIN をホストする</span><span class="sxs-lookup"><span data-stu-id="dad92-104">Host OWIN in an Azure Worker Role</span></span>

<span data-ttu-id="dad92-105">作成者[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="dad92-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="dad92-106">このチュートリアルでは、Microsoft Azure worker ロールで OWIN を自己ホストする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="dad92-106">This tutorial shows how to self-host OWIN in a Microsoft Azure worker role.</span></span>
>
> <span data-ttu-id="dad92-107">[.NET 用 Web インターフェイスを開き](http://owin.org/)(OWIN) .NET web サーバーおよび web アプリケーション間の抽象化を定義します。</span><span class="sxs-lookup"><span data-stu-id="dad92-107">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="dad92-108">OWIN により、OWIN の IIS の外部の独自のプロセスで web アプリケーションを自己ホストするために最適ですが、サーバーから web アプリケーションの分離 – Azure worker ロール内など。</span><span class="sxs-lookup"><span data-stu-id="dad92-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="dad92-109">このチュートリアルでは、Microsoft Azure worker ロール内での OWIN アプリケーションを自己ホストする方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="dad92-109">In this tutorial, you'll learn how to self-host an OWIN applications inside a Microsoft Azure worker role.</span></span> <span data-ttu-id="dad92-110">ワーカー ロールの詳細については、次を参照してください。 [Azure 実行モデル](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices)します。</span><span class="sxs-lookup"><span data-stu-id="dad92-110">To learn more about worker roles, see [Azure Execution Models](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="dad92-111">このチュートリアルで使用されるソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="dad92-111">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="dad92-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="dad92-112">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [<span data-ttu-id="dad92-113">Azure SDK for .NET 2.3</span><span class="sxs-lookup"><span data-stu-id="dad92-113">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)
> - [<span data-ttu-id="dad92-114">Microsoft.Owin.Selfhost 2.1.0</span><span class="sxs-lookup"><span data-stu-id="dad92-114">Microsoft.Owin.Selfhost 2.1.0</span></span>](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="dad92-115">Microsoft Azure プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="dad92-115">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="dad92-116">管理者特権で Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="dad92-116">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="dad92-117">Azure コンピューティング エミュレーターを使用してローカルでのアプリケーションをデバッグするには、管理者特権が必要です。</span><span class="sxs-lookup"><span data-stu-id="dad92-117">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="dad92-118">**ファイル** メニューのをクリックして**新規**、 をクリックし、**プロジェクト**します。</span><span class="sxs-lookup"><span data-stu-id="dad92-118">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="dad92-119">**インストールされたテンプレート**、Visual c# では、クリックして**クラウド** をクリックし、 **Windows Azure クラウド サービス**します。</span><span class="sxs-lookup"><span data-stu-id="dad92-119">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="dad92-120">プロジェクトとして「AzureApp」という名前にして**OK**します。</span><span class="sxs-lookup"><span data-stu-id="dad92-120">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="dad92-121">**新しい Windows Azure クラウド サービス**ダイアログ ボックスで、ダブルクリックして**ワーカー ロール**します。</span><span class="sxs-lookup"><span data-stu-id="dad92-121">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="dad92-122">既定の名前 ("WorkerRole1") のままにします。</span><span class="sxs-lookup"><span data-stu-id="dad92-122">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="dad92-123">この手順では、ソリューションにワーカー ロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="dad92-123">This step adds a worker role to the solution.</span></span> <span data-ttu-id="dad92-124">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="dad92-124">Click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="dad92-125">作成された Visual Studio ソリューションには、2 つのプロジェクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="dad92-125">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="dad92-126">&quot;AzureApp&quot;ロールと Azure のアプリケーションの構成を定義します。</span><span class="sxs-lookup"><span data-stu-id="dad92-126">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="dad92-127">&quot;WorkerRole1&quot;ワーカー ロールのコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="dad92-127">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="dad92-128">一般に、Azure のアプリケーションは、このチュートリアルは、1 つのロールを使用しますが、複数のロールを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="dad92-128">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a><span data-ttu-id="dad92-129">OWIN 自己ホスト パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="dad92-129">Add the OWIN Self-Host Packages</span></span>

<span data-ttu-id="dad92-130">**ツール** メニューのをクリックして**NuGet パッケージ マネージャー**、 をクリックし、**パッケージ マネージャー コンソール**します。</span><span class="sxs-lookup"><span data-stu-id="dad92-130">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="dad92-131">パッケージ マネージャー コンソール ウィンドウで、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="dad92-131">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="dad92-132">HTTP エンドポイントを追加します。</span><span class="sxs-lookup"><span data-stu-id="dad92-132">Add an HTTP Endpoint</span></span>

<span data-ttu-id="dad92-133">ソリューション エクスプ ローラーで、AzureApp プロジェクトを展開します。</span><span class="sxs-lookup"><span data-stu-id="dad92-133">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="dad92-134">ロール ノードを展開し、WorkerRole1 を右クリックし、**プロパティ**します。</span><span class="sxs-lookup"><span data-stu-id="dad92-134">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="dad92-135">クリックして**エンドポイント**、 をクリックし、**エンドポイントの追加**します。</span><span class="sxs-lookup"><span data-stu-id="dad92-135">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="dad92-136">**プロトコル**ドロップダウン リストで、"http"を選択します。</span><span class="sxs-lookup"><span data-stu-id="dad92-136">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="dad92-137">**パブリック ポート**と**プライベート ポート**80」と入力します。</span><span class="sxs-lookup"><span data-stu-id="dad92-137">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="dad92-138">これらのポート番号が異なることがあります。</span><span class="sxs-lookup"><span data-stu-id="dad92-138">These port numbers can be different.</span></span> <span data-ttu-id="dad92-139">パブリック ポートは、ロール要求を送信するときに使用するクライアントです。</span><span class="sxs-lookup"><span data-stu-id="dad92-139">The public port is what clients use when they send a request to the role.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a><span data-ttu-id="dad92-140">OWIN Startup クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="dad92-140">Create the OWIN Startup Class</span></span>

<span data-ttu-id="dad92-141">ソリューション エクスプ ローラーで WorkerRole1 プロジェクトを右クリックし、選択**追加** / **クラス**新しいクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="dad92-141">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="dad92-142">クラスに `Startup` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="dad92-142">Name the class `Startup`.</span></span>

<span data-ttu-id="dad92-143">次のようにすべての定型コードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="dad92-143">Replace all of the boilerplate code with the following:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

<span data-ttu-id="dad92-144">`UseWelcomePage`拡張メソッドは、アプリケーションには、サイトの動作を確認する単純な HTML ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="dad92-144">The `UseWelcomePage` extension method adds a simple HTML page to your application, to verify the site is working.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="dad92-145">OWIN ホストを開始します。</span><span class="sxs-lookup"><span data-stu-id="dad92-145">Start the OWIN Host</span></span>

<span data-ttu-id="dad92-146">WorkerRole.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="dad92-146">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="dad92-147">このクラスは、ワーカー ロールが開始および停止時に実行されるコードを定義します。</span><span class="sxs-lookup"><span data-stu-id="dad92-147">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="dad92-148">次の追加ステートメントを使用します。</span><span class="sxs-lookup"><span data-stu-id="dad92-148">Add the following using statement:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="dad92-149">追加、 **IDisposable**メンバーを`WorkerRole`クラス。</span><span class="sxs-lookup"><span data-stu-id="dad92-149">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="dad92-150">`OnStart`メソッドでは、ホストを起動する次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="dad92-150">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

<span data-ttu-id="dad92-151">**WebApp.Start**メソッドは、OWIN ホストを開始します。</span><span class="sxs-lookup"><span data-stu-id="dad92-151">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="dad92-152">名前、`Startup`クラスは、メソッドの型パラメーター。</span><span class="sxs-lookup"><span data-stu-id="dad92-152">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="dad92-153">慣例により、ホストが呼び出す、`Configure`このクラスのメソッド。</span><span class="sxs-lookup"><span data-stu-id="dad92-153">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="dad92-154">上書き、`OnStop`を破棄する、 *\_アプリ*インスタンス。</span><span class="sxs-lookup"><span data-stu-id="dad92-154">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

<span data-ttu-id="dad92-155">WorkerRole.cs の完全なコードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="dad92-155">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="dad92-156">ソリューションをビルドし、f5 キーを押して Azure コンピューティング エミュレーターでアプリケーションをローカルで実行します。</span><span class="sxs-lookup"><span data-stu-id="dad92-156">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="dad92-157">ファイアウォールの設定によっては、ファイアウォール経由のエミュレーターを許可する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dad92-157">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

<span data-ttu-id="dad92-158">コンピューティング エミュレーターでは、エンドポイントに、ローカル IP アドレスが割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="dad92-158">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="dad92-159">コンピューティング エミュレーター UI を表示することによって、IP アドレスを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="dad92-159">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="dad92-160">タスク バー通知領域のエミュレーター アイコンを右クリックして**コンピューティング エミュレーター UI**します。</span><span class="sxs-lookup"><span data-stu-id="dad92-160">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="dad92-161">サービスの展開で、サービスの詳細情報の展開 [id]、IP アドレスを検索します。</span><span class="sxs-lookup"><span data-stu-id="dad92-161">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="dad92-162">Web ブラウザーを開き、http に移動します:\/\/*アドレス*ここで、*アドレス*は、コンピューティング エミュレーターによって割り当てられた IP アドレスは、たとえば、`http://127.0.0.1:80`します。</span><span class="sxs-lookup"><span data-stu-id="dad92-162">Open a web browser and navigate to http:\/\/*address*, where *address* is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80`.</span></span> <span data-ttu-id="dad92-163">OWIN へようこそ ページを参照する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dad92-163">You should see the OWIN welcome page:</span></span>

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="dad92-164">Azure に配置する</span><span class="sxs-lookup"><span data-stu-id="dad92-164">Deploy to Azure</span></span>

<span data-ttu-id="dad92-165">この手順では、Azure アカウントが必要です。</span><span class="sxs-lookup"><span data-stu-id="dad92-165">For this step, you must have an Azure account.</span></span> <span data-ttu-id="dad92-166">1 つをいない場合は、ほんの数分で無料試用版アカウントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="dad92-166">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="dad92-167">詳細については、次を参照してください。 [Microsoft Azure の無料試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)します。</span><span class="sxs-lookup"><span data-stu-id="dad92-167">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="dad92-168">ソリューション エクスプ ローラーで、AzureApp プロジェクトを右クリックします。</span><span class="sxs-lookup"><span data-stu-id="dad92-168">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="dad92-169">**[発行]** を選びます。</span><span class="sxs-lookup"><span data-stu-id="dad92-169">Select **Publish**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image12.png)

<span data-ttu-id="dad92-170">Azure アカウントにサインインしていない場合はクリックして**サインイン**します。</span><span class="sxs-lookup"><span data-stu-id="dad92-170">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="dad92-171">サインインした後、サブスクリプションを選択およびクリックして**次**します。</span><span class="sxs-lookup"><span data-stu-id="dad92-171">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

<span data-ttu-id="dad92-172">クラウド サービスの名前を入力し、リージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="dad92-172">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="dad92-173">**[作成]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="dad92-173">Click **Create**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image17.png)

<span data-ttu-id="dad92-174">**[発行]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="dad92-174">Click **Publish**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="dad92-175">Azure アクティビティ ログ ウィンドウには、展開の進行状況が表示されます。</span><span class="sxs-lookup"><span data-stu-id="dad92-175">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="dad92-176">アプリが展開されると、参照`http://appname.cloudapp.net/`ここで、 *appname*クラウド サービスの名前を指定します。</span><span class="sxs-lookup"><span data-stu-id="dad92-176">When the app is deployed, browse to `http://appname.cloudapp.net/`, where *appname* is the name of your cloud service.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dad92-177">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="dad92-177">Additional Resources</span></span>

- [<span data-ttu-id="dad92-178">プロジェクト Katana の概要</span><span class="sxs-lookup"><span data-stu-id="dad92-178">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)
- [<span data-ttu-id="dad92-179">GitHub の Katana プロジェクト</span><span class="sxs-lookup"><span data-stu-id="dad92-179">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana/)
