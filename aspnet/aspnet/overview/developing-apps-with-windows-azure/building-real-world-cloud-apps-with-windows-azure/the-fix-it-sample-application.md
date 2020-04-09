---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: '付録: 修正イットサンプルアプリケーション (Azure を使用した実世界のクラウドアプリの構築) |マイクロソフトドキュメント'
author: MikeWasson
description: Azure 電子書籍を使用したリアル ワールド クラウド アプリの構築は、スコット ガスリーが開発したプレゼンテーションに基づいています。 それは彼ができる13のパターンと実践を説明します.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675635"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="8c56c-104">付録: 修正イットサンプルアプリケーション (Azure を使用した実世界のクラウドアプリの構築)</span><span class="sxs-lookup"><span data-stu-id="8c56c-104">Appendix: The Fix It Sample Application (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="8c56c-105">[マイク・ワッソン](https://github.com/MikeWasson),[リック・アンダーソン](https://twitter.com/RickAndMSFT),[トム・ダイクストラ](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8c56c-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="8c56c-106">修正イットプロジェクトをダウンロード</span><span class="sxs-lookup"><span data-stu-id="8c56c-106">Download The Fix It Project</span></span>](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> <span data-ttu-id="8c56c-107">Azure 電子書籍**を使用したリアル ワールド クラウド アプリの構築**は、スコット ガスリーが開発したプレゼンテーションに基づいています。</span><span class="sxs-lookup"><span data-stu-id="8c56c-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="8c56c-108">クラウド向けの Web アプリの開発を成功させるために役立つ 13 のパターンとプラクティスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="8c56c-109">電子書籍の詳細については、[最初の章を](introduction.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="8c56c-110">Azure を使用した実世界のクラウド アプリの構築に関するこの付録には、ダウンロードできる Fix It サンプル アプリケーションに関する追加情報を提供する次のセクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8c56c-110">This appendix to the Building Real World Cloud Apps with Azure e-book contains the following sections that provide additional information about the Fix It sample application that you can download:</span></span>

- [<span data-ttu-id="8c56c-111">既知の問題</span><span class="sxs-lookup"><span data-stu-id="8c56c-111">Known issues</span></span>](#knownissues)
- [<span data-ttu-id="8c56c-112">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="8c56c-112">Best practices</span></span>](#bestpractices)
- [<span data-ttu-id="8c56c-113">ローカル コンピューターで Visual Studio からアプリを実行する方法</span><span class="sxs-lookup"><span data-stu-id="8c56c-113">How to run the app from Visual Studio on your local computer</span></span>](#run-in-vs)
- [<span data-ttu-id="8c56c-114">Windows PowerShell スクリプトを使用して基本アプリを Azure アプリ サービス Web アプリにデプロイする方法</span><span class="sxs-lookup"><span data-stu-id="8c56c-114">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>](#deploybase)
- [<span data-ttu-id="8c56c-115">スクリプトのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="8c56c-115">Troubleshooting the Windows PowerShell scripts</span></span>](#troubleshooting)
- [<span data-ttu-id="8c56c-116">キュー処理を含むアプリを Azure アプリ サービス Web アプリと Azure クラウド サービスにデプロイする方法</span><span class="sxs-lookup"><span data-stu-id="8c56c-116">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a><span data-ttu-id="8c56c-117">既知の問題</span><span class="sxs-lookup"><span data-stu-id="8c56c-117">Known issues</span></span>

<span data-ttu-id="8c56c-118">Fix It アプリは、この電子書籍に記載されているパターンの一部をできるだけ簡単に説明するために開発されました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-118">The Fix It app was originally developed in order to illustrate as simply as possible some of the patterns presented in this e-book.</span></span> <span data-ttu-id="8c56c-119">しかし、電子書籍は現実世界のアプリの構築に関するものであるため、Fix It コードはリリースされたソフトウェアと同様のレビューとテストプロセスに従いました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-119">However, since the e-book is about building real-world apps, we subjected the Fix It code to a review and testing process similar to what we'd do for released software.</span></span> <span data-ttu-id="8c56c-120">私たちは多くの問題を発見し、実際のアプリケーションと同様に、そのうちのいくつかは修正され、そのうちのいくつかは後のリリースに延期しました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-120">We found a number of issues, and as with any real-world application, some of them we fixed and some of them we deferred to a later release.</span></span>

<span data-ttu-id="8c56c-121">次の一覧には、運用アプリケーションで対処する必要がある問題が含まれていますが、何らかの理由で、Fix It サンプル アプリケーションの初期リリースでは対処しないことにしました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-121">The following list includes issues that should be addressed in a production application, but for one reason or another we decided not to address in the initial release of the Fix It sample application.</span></span>

### <a name="security"></a><span data-ttu-id="8c56c-122">Security</span><span class="sxs-lookup"><span data-stu-id="8c56c-122">Security</span></span>

- <span data-ttu-id="8c56c-123">存在しない所有者にタスクを割り当てることができないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-123">Ensure that you can't assign a task to a non-existent owner.</span></span>
- <span data-ttu-id="8c56c-124">自分が作成したタスクまたは自分に割り当てられているタスクのみを表示および変更できることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-124">Ensure that you can only view and modify tasks that you created or are assigned to you.</span></span>
- <span data-ttu-id="8c56c-125">サインイン ページと認証 Cookie には HTTPS を使用します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-125">Use HTTPS for sign-in pages and authentication cookies.</span></span>
- <span data-ttu-id="8c56c-126">認証クッキーの期限を指定します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-126">Specify a time limit for authentication cookies.</span></span>

### <a name="input-validation"></a><span data-ttu-id="8c56c-127">入力の検証</span><span class="sxs-lookup"><span data-stu-id="8c56c-127">Input validation</span></span>

<span data-ttu-id="8c56c-128">一般に、運用アプリでは、Fix It アプリよりも多くの入力検証が行われます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-128">In general, a production app would do more input validation than the Fix It app.</span></span> <span data-ttu-id="8c56c-129">たとえば、アップロード可能な画像サイズ/画像ファイルサイズは制限されるべきです。</span><span class="sxs-lookup"><span data-stu-id="8c56c-129">For example, the image size / image file size allowed for upload should be limited.</span></span>

### <a name="administrator-functionality"></a><span data-ttu-id="8c56c-130">管理者機能</span><span class="sxs-lookup"><span data-stu-id="8c56c-130">Administrator functionality</span></span>

<span data-ttu-id="8c56c-131">管理者は、既存のタスクの所有権を変更できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-131">An administrator should be able to change ownership on existing tasks.</span></span> <span data-ttu-id="8c56c-132">たとえば、タスクの作成者が退社し、管理アクセスが有効になっていない限り、タスクを保守する権限を持つユーザーが残さない場合があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-132">For example, the creator of a task might leave the company, leaving no one with authority to maintain the task unless administrative access is enabled.</span></span>

### <a name="queue-message-processing"></a><span data-ttu-id="8c56c-133">キュー メッセージ処理</span><span class="sxs-lookup"><span data-stu-id="8c56c-133">Queue message processing</span></span>

<span data-ttu-id="8c56c-134">Fix It アプリでのキュー メッセージ処理は、最小限のコードでキュー中心の作業パターンを示すために簡単に設計されました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-134">Queue message processing in the Fix It app was designed to be simple in order to illustrate the queue-centric work pattern with a minimum amount of code.</span></span> <span data-ttu-id="8c56c-135">この単純なコードは、実際の実稼働アプリケーションには適していません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-135">This simple code would not be adequate for an actual production application.</span></span>

- <span data-ttu-id="8c56c-136">このコードでは、各キュー メッセージが 1 回だけ処理されることを保証するものではありません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-136">The code does not guarantee that each queue message will be processed at most once.</span></span> <span data-ttu-id="8c56c-137">キューからメッセージを取得すると、タイムアウト期間があり、その間にメッセージは他のキュー リスナーからは見えません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-137">When you get a message from the queue, there is a timeout period, during which the message is invisible to other queue listeners.</span></span> <span data-ttu-id="8c56c-138">メッセージが削除される前にタイムアウトが切れた場合、メッセージは再び表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-138">If the timeout expires before the message is deleted, the message becomes visible again.</span></span> <span data-ttu-id="8c56c-139">したがって、ワーカー ロール インスタンスがメッセージの処理に長時間を費やす場合、理論的には同じメッセージが 2 回処理され、データベース内の重複したタスクが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-139">Therefore, if a worker role instance spends a long time processing a message, it is theoretically possible for the same message to get processed twice, resulting in a duplicate task in the database.</span></span> <span data-ttu-id="8c56c-140">この問題の詳細については[、「Azure ストレージ キューの使用](https://msdn.microsoft.com/library/ff803365.aspx#sec7)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-140">For more information about this issue, see [Using Azure Storage Queues](https://msdn.microsoft.com/library/ff803365.aspx#sec7).</span></span>
- <span data-ttu-id="8c56c-141">キューポーリング ロジックは、メッセージの取得をバッチ処理することで、よりコスト効率が高くなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-141">The queue polling logic could be more cost-effective, by batching message retrieval.</span></span> <span data-ttu-id="8c56c-142">呼び出すたびに[、](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)トランザクションコストが発生します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-142">Every time you call [CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx), there is a transaction cost.</span></span> <span data-ttu-id="8c56c-143">代わりに、単一のトランザクションで複数のメッセージを取得する[CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (複数形の's') を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-143">Instead, you can call [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (note the plural 's'), which gets multiple messages in a single transaction.</span></span> <span data-ttu-id="8c56c-144">Azure Storage Queue のトランザクション コストは非常に低いため、ほとんどのシナリオではコストへの影響は大きくはありません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-144">The transaction costs for Azure Storage Queues are very low, so the impact on costs is not substantial in most scenarios.</span></span>
- <span data-ttu-id="8c56c-145">キュー メッセージ処理コードの緊密なループにより、CPU アフィニティが発生し、マルチコア VM を効率的に使用しません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-145">The tight loop in the queue message-processing code causes CPU affinity, which does not utilize multi-core VMs efficiently.</span></span> <span data-ttu-id="8c56c-146">より優れた設計では、タスクの並列処理を使用して、複数の非同期タスクを並列に実行します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-146">A better design would use task parallelism to run several async tasks in parallel.</span></span>
- <span data-ttu-id="8c56c-147">キューメッセージ処理には、基本的な例外処理しかありません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-147">Queue message-processing has only rudimentary exception handling.</span></span> <span data-ttu-id="8c56c-148">たとえば、有害な[メッセージ](https://msdn.microsoft.com/library/ms789028.aspx)を処理しないコードです。</span><span class="sxs-lookup"><span data-stu-id="8c56c-148">For example, the code doesn't handle [poison messages](https://msdn.microsoft.com/library/ms789028.aspx).</span></span> <span data-ttu-id="8c56c-149">(メッセージの処理によって例外が発生した場合は、エラーをログに記録してメッセージを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-149">(When message processing causes an exception, you have to log the error and delete the message, or the worker role will try to process it again, and the loop will continue indefinitely.)</span></span>

### <a name="sql-queries-are-unbounded"></a><span data-ttu-id="8c56c-150">SQL クエリは無制限です</span><span class="sxs-lookup"><span data-stu-id="8c56c-150">SQL queries are unbounded</span></span>

<span data-ttu-id="8c56c-151">現在の Fix It コードでは、インデックス ページのクエリが返す行数に制限はありません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-151">Current Fix It code places no limit on how many rows the queries for Index pages might return.</span></span> <span data-ttu-id="8c56c-152">大量のタスクがデータベースに入力されると、受信したリストのサイズがパフォーマンスの問題を引き起こす可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-152">If a large volume of tasks is entered into the database, the size of the resulting lists received could cause performance issues.</span></span> <span data-ttu-id="8c56c-153">解決策は、ページングを実装することです。</span><span class="sxs-lookup"><span data-stu-id="8c56c-153">The solution is to implement paging.</span></span> <span data-ttu-id="8c56c-154">例については、「 [MVC アプリケーションのASP.NETでのエンティティ フレームワークを使用した並べ替え、フィルター処理、およびページング」](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-154">For an example, see [Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).</span></span>

### <a name="view-models-recommended"></a><span data-ttu-id="8c56c-155">推奨モデルの表示</span><span class="sxs-lookup"><span data-stu-id="8c56c-155">View models recommended</span></span>

<span data-ttu-id="8c56c-156">Fix It アプリは、FixItTask エンティティ クラスを使用して、コントローラーとビューの間で情報を渡します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-156">The Fix It app uses the FixItTask entity class to pass information between the controller and the view.</span></span> <span data-ttu-id="8c56c-157">ベスト プラクティスは、ビュー モデルを使用することです。</span><span class="sxs-lookup"><span data-stu-id="8c56c-157">A best practice is to use view models.</span></span> <span data-ttu-id="8c56c-158">ドメイン モデル (FixItTask エンティティ クラスなど) はデータの永続化に必要な要素を中心に設計されていますが、ビュー モデルはデータの表示用に設計できます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-158">The domain model (e.g., the FixItTask entity class) is designed around what is needed for data persistence, while a view model can be designed for data presentation.</span></span> <span data-ttu-id="8c56c-159">詳細については、「 [12 ASP.NET MVC のベスト プラクティス](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-159">For more information, see [12 ASP.NET MVC Best Practices](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).</span></span>

### <a name="secure-image-blob-recommended"></a><span data-ttu-id="8c56c-160">セキュアイメージブロブ推奨</span><span class="sxs-lookup"><span data-stu-id="8c56c-160">Secure image blob recommended</span></span>

<span data-ttu-id="8c56c-161">Fix It アプリはアップロードした画像をパブリックとして保存するため、URL を見つけた人は誰でも画像にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-161">The Fix It app stores uploaded images as public, meaning that anyone who finds the URL can access the images.</span></span> <span data-ttu-id="8c56c-162">画像は公開ではなく保護できます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-162">The images could be secured instead of public.</span></span>

### <a name="no-powershell-automation-scripts-for-queues"></a><span data-ttu-id="8c56c-163">キューに PowerShell オートメーション スクリプトはありません</span><span class="sxs-lookup"><span data-stu-id="8c56c-163">No PowerShell automation scripts for queues</span></span>

<span data-ttu-id="8c56c-164">PowerShell のオートメーション スクリプトのサンプルは、Azure アプリ サービス Web アプリで完全に実行される Fix It の基本バージョンに対してのみ作成されました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-164">Sample PowerShell automation scripts were written only for the base version of Fix It that runs entirely in Azure App Service Web Apps.</span></span> <span data-ttu-id="8c56c-165">Web アプリと、キュー処理に必要なクラウド サービス環境を設定してデプロイするためのスクリプトは提供されていません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-165">We haven't provided scripts for setting up and deploying to the web app plus Cloud Service environment required for queue processing.</span></span>

### <a name="special-handling-for-html-codes-in-user-input"></a><span data-ttu-id="8c56c-166">ユーザー入力における HTML コードの特別な処理</span><span class="sxs-lookup"><span data-stu-id="8c56c-166">Special handling for HTML codes in user input</span></span>

<span data-ttu-id="8c56c-167">ASP.NET、悪意のあるユーザーがユーザー入力テキスト ボックスにスクリプトを入力してクロスサイト スクリプティング攻撃を試みるさまざまな方法を自動的に防ぎます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-167">ASP.NET automatically prevents many ways in which malicious users might attempt cross-site scripting attacks by entering script in user input text boxes.</span></span> <span data-ttu-id="8c56c-168">また、タスク`DisplayFor`のタイトルとメモを表示するために使用される MVC ヘルパーは、ブラウザーに送信する値を HTML エンコードします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-168">And the MVC `DisplayFor` helper used to display task titles and notes automatically HTML-encodes values that it sends to the browser.</span></span> <span data-ttu-id="8c56c-169">しかし、本番アプリでは、追加の対策を講じる必要があるかもしれません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-169">But in a production app you might want to take additional measures.</span></span> <span data-ttu-id="8c56c-170">詳細については、「 [ASP.NET の要求検証](https://msdn.microsoft.com/library/hh882339.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-170">For more information, see [Request Validation in ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).</span></span>

<a id="bestpractices"></a>
## <a name="best-practices"></a><span data-ttu-id="8c56c-171">ベスト プラクティス</span><span class="sxs-lookup"><span data-stu-id="8c56c-171">Best practices</span></span>

<span data-ttu-id="8c56c-172">以下は、コード レビューと Fix It アプリの元のバージョンのテストで発見された後に修正されたいくつかの問題です。</span><span class="sxs-lookup"><span data-stu-id="8c56c-172">Following are some issues that were fixed after being discovered in code review and testing of the original version of the Fix It app.</span></span> <span data-ttu-id="8c56c-173">元のコーダが特定のベストプラクティスを認識していなかったために引き起こされたものもあれば、コードが迅速に書かれてリリースされたソフトウェアを意図していなかったためのものもありました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-173">Some were caused by the original coder not being aware of a particular best practice, some simply because the code was written quickly and wasn't intended for released software.</span></span> <span data-ttu-id="8c56c-174">このレビューとテストから学んだことが Web アプリを開発している他のユーザーにとって役立つ可能性がある場合に備えて、ここで問題をリストアップしています。</span><span class="sxs-lookup"><span data-stu-id="8c56c-174">We're listing the issues here in case there's something we learned from this review and testing that might be helpful to others who are also developing web apps.</span></span>

### <a name="dispose-the-database-repository"></a><span data-ttu-id="8c56c-175">データベース リポジトリを破棄する</span><span class="sxs-lookup"><span data-stu-id="8c56c-175">Dispose the database repository</span></span>

<span data-ttu-id="8c56c-176">クラス`FixItTaskRepository`は、エンティティ フレームワーク`DbContext`インスタンスを破棄する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-176">The `FixItTaskRepository` class must dispose the Entity Framework `DbContext` instance.</span></span> <span data-ttu-id="8c56c-177">これを`IDisposable``FixItTaskRepository`クラスで実装して行いました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-177">We did this by implementing `IDisposable` in the `FixItTaskRepository` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

<span data-ttu-id="8c56c-178">AutoFac はインスタンスを`FixItTaskRepository`自動的に破棄するので、明示的に破棄する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-178">Note that AutoFac will automatically dispose the `FixItTaskRepository` instance, so we don't need to explicitly dispose it.</span></span>

<span data-ttu-id="8c56c-179">もう 1 つの方法`DbContext`は、`FixItTaskRepository`からメンバー変数を削除し`DbContext`、代わりに各リポジトリ メソッド内に`using`ステートメント内にローカル変数を作成することです。</span><span class="sxs-lookup"><span data-stu-id="8c56c-179">Another option is to remove the `DbContext` member variable from `FixItTaskRepository`, and instead create a local `DbContext` variable within each repository method, inside a `using` statement.</span></span> <span data-ttu-id="8c56c-180">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-180">For example:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a><span data-ttu-id="8c56c-181">DI でシングルトンをそのように登録する</span><span class="sxs-lookup"><span data-stu-id="8c56c-181">Register singletons as such with DI</span></span>

<span data-ttu-id="8c56c-182">`PhotoService`クラスと`Logger`クラスのインスタンスは 1 つだけ必要なので、これらのクラスは *、DependenciesConfig.cs*で[依存関係を注入するために単一のインスタンスとして登録](https://code.google.com/p/autofac/wiki/InstanceScope)する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-182">Since only one instance of the `PhotoService` class and `Logger` class is needed, these classes should be [registered as single instances for dependency injection](https://code.google.com/p/autofac/wiki/InstanceScope) in *DependenciesConfig.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a><span data-ttu-id="8c56c-183">セキュリティ: エラーの詳細をユーザーに表示しない</span><span class="sxs-lookup"><span data-stu-id="8c56c-183">Security: Don't show error details to users</span></span>

<span data-ttu-id="8c56c-184">元の Fix It アプリには一般的なエラー ページが含まれていなかったため、すべての例外が UI にバブルアップするため、データベース接続エラーなどの一部の例外では、完全なスタック トレースがブラウザーに表示される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-184">The original Fix It app didn't have a generic error page and just let all exceptions bubble up to the UI, so some exceptions such as database connection errors could result in a full stack trace being displayed to the browser.</span></span> <span data-ttu-id="8c56c-185">詳細なエラー情報により、悪意のあるユーザーによる攻撃が容易になることがあります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-185">Detailed error information can sometimes facilitate attacks by malicious users.</span></span> <span data-ttu-id="8c56c-186">解決策は、例外の詳細をログに記録し、エラーの詳細を含まないエラー ページをユーザーに表示することです。</span><span class="sxs-lookup"><span data-stu-id="8c56c-186">The solution is to log the exception details and display an error page to the user that doesn't include error details.</span></span> <span data-ttu-id="8c56c-187">Fix It アプリは既にログに記録されており、エラー ページを表示するために`<customErrors mode=On>`、Web.config ファイルに追加されました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-187">The Fix It app was already logging, and in order to display an error page, we added `<customErrors mode=On>` in the Web.config file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

<span data-ttu-id="8c56c-188">既定では、*ビュー\共有\エラー.cshtml*がエラーに対して表示されます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-188">By default this causes *Views\Shared\Error.cshtml* to be displayed for errors.</span></span> <span data-ttu-id="8c56c-189">*Error.cshtml*をカスタマイズするか、独自のエラー ページ ビューを`defaultRedirect`作成して属性を追加できます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-189">You can customize *Error.cshtml* or create your own error page view and add a `defaultRedirect` attribute.</span></span> <span data-ttu-id="8c56c-190">特定のエラーに対して異なるエラーページを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-190">You can also specify different error pages for specific errors.</span></span>

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a><span data-ttu-id="8c56c-191">セキュリティ: タスクの作成者のみが編集できるようにする</span><span class="sxs-lookup"><span data-stu-id="8c56c-191">Security: only allow a task to be edited by its creator</span></span>

<span data-ttu-id="8c56c-192">ダッシュボードインデックスページには、ログオンしたユーザーによって作成されたタスクのみが表示されますが、悪意のあるユーザーが別のユーザーのタスクの ID を持つ URL を作成する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-192">The Dashboard Index page only shows tasks created by the logged-on user, but a malicious user could create a URL with an ID to another user's task.</span></span> <span data-ttu-id="8c56c-193">その*場合は*、DashboardController.csに 404 を返すコードを追加しました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-193">We added code in *DashboardController.cs* to return a 404 in that case:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a><span data-ttu-id="8c56c-194">例外を飲み込まない</span><span class="sxs-lookup"><span data-stu-id="8c56c-194">Don't swallow exceptions</span></span>

<span data-ttu-id="8c56c-195">元の Fix It アプリは、SQL クエリから生じる例外をログに記録した後、単に null を返しました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-195">The original Fix It app just returned null after logging an exception that resulted from a SQL query:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

<span data-ttu-id="8c56c-196">これにより、クエリは成功したが、行が返されないかのようにユーザーに見える。</span><span class="sxs-lookup"><span data-stu-id="8c56c-196">This would make it look to the user as if the query succeeded but just didn't return any rows.</span></span> <span data-ttu-id="8c56c-197">解決策は、キャッチしてログに記録した後に例外を再スローすることです。</span><span class="sxs-lookup"><span data-stu-id="8c56c-197">Solution is to re-throw the exception after catching and logging:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a><span data-ttu-id="8c56c-198">作業者ロールのすべての例外をキャッチ</span><span class="sxs-lookup"><span data-stu-id="8c56c-198">Catch all exceptions in worker roles</span></span>

<span data-ttu-id="8c56c-199">ワーカー ロール内の未処理の例外は VM をリサイクルするため、try-catch ブロックで行う処理をすべてラップし、すべての例外を処理します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-199">Any unhandled exceptions in a worker role will cause the VM to be recycled, so you want to wrap everything you do in a try-catch block and handle all exceptions.</span></span>

### <a name="specify-length-for-string-properties-in-entity-classes"></a><span data-ttu-id="8c56c-200">エンティティ クラスの文字列プロパティの長さを指定する</span><span class="sxs-lookup"><span data-stu-id="8c56c-200">Specify length for string properties in entity classes</span></span>

<span data-ttu-id="8c56c-201">単純なコードを表示するために、Fix It アプリの元のバージョンでは、FixItTask エンティティのフィールドの長さが指定されず、その結果、データベース内で varchar(max) として定義されました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-201">In order to display simple code, the original version of the Fix It app didn't specify lengths for the fields of the FixItTask entity, and as a result they were defined as varchar(max) in the database.</span></span> <span data-ttu-id="8c56c-202">その結果、UI はほぼすべての量の入力を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-202">As a result, the UI would accept almost any amount of input.</span></span> <span data-ttu-id="8c56c-203">長さを指定すると、Web ページのユーザー入力とデータベース内の列サイズの両方に適用される制限が設定されます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-203">Specifying lengths sets limits that apply both to user input in the web page and column size in the database:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a><span data-ttu-id="8c56c-204">変更が予想されない場合に、プライベート メンバーを読み取り専用としてマークする</span><span class="sxs-lookup"><span data-stu-id="8c56c-204">Mark private members as readonly when they aren't expected to change</span></span>

<span data-ttu-id="8c56c-205">たとえば、`DashboardController`クラス内での`FixItTaskRepository`インスタンスが作成され、変更される予定はないので、それを[readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)として定義しました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-205">For example, in the `DashboardController` class an instance of `FixItTaskRepository` is created and isn't expected to change, so we defined it as [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx).</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a><span data-ttu-id="8c56c-206">リストを使用します。リストの代わりに Any() 。カウント()0 &gt;</span><span class="sxs-lookup"><span data-stu-id="8c56c-206">Use list.Any() instead of list.Count() &gt; 0</span></span>

<span data-ttu-id="8c56c-207">リスト内の 1 つまたは複数の項目が指定した条件に適合するかどうかが気にする場合は、条件に適合する項目が見つかるとすぐに返されるため[、Any](https://msdn.microsoft.com/library/bb534972.aspx) `Count`メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-207">If you all you care about is whether one or more items in a list fit the specified criteria, use the [Any](https://msdn.microsoft.com/library/bb534972.aspx) method, because it returns as soon as an item fitting the criteria is found, whereas the `Count` method always has to iterate through every item.</span></span> <span data-ttu-id="8c56c-208">ダッシュボード*Index.cshtml*ファイルには、元々次のコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8c56c-208">The Dashboard *Index.cshtml* file originally had this code:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

<span data-ttu-id="8c56c-209">これを次に変更しました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-209">We changed it to this:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a><span data-ttu-id="8c56c-210">MVC ヘルパーを使用して MVC ビューで URL を生成する</span><span class="sxs-lookup"><span data-stu-id="8c56c-210">Generate URLs in MVC views using MVC helpers</span></span>

<span data-ttu-id="8c56c-211">ホーム ページ**の [修正を作成**] ボタンの場合、Fix It アプリはアンカー要素をハードコーディングしました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-211">For the **Create a Fix It** button on the home page, the Fix It app hard coded an anchor element:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

<span data-ttu-id="8c56c-212">このような表示/アクションリンクの場合は[、Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML ヘルパーを使用することをお望みします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-212">For View/Action links like this it's better to use the [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML helper, for example:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a><span data-ttu-id="8c56c-213">ワーカー ロールで Thread.Sleep の代わりに Task.Delay を使用する</span><span class="sxs-lookup"><span data-stu-id="8c56c-213">Use Task.Delay instead of Thread.Sleep in worker role</span></span>

<span data-ttu-id="8c56c-214">新しいプロジェクト テンプレートでは`Thread.Sleep`、ワーカー ロールのサンプル コードを記述しますが、スレッドをスリープ状態にする原因として、スレッド プールが不要なスレッドを追加で生成する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-214">The new-project template puts `Thread.Sleep` in the sample code for a worker role, but causing the thread to sleep can cause the thread pool to spawn additional unnecessary threads.</span></span> <span data-ttu-id="8c56c-215">代わりに[Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx)を使用することで、これを回避できます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-215">You can avoid that by using [Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx) instead.</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a><span data-ttu-id="8c56c-216">非同期の無効を回避する</span><span class="sxs-lookup"><span data-stu-id="8c56c-216">Avoid async void</span></span>

<span data-ttu-id="8c56c-217">非同期メソッドが値を返す必要がない場合は、 ではなく`Task``void`型を返します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-217">If an async method doesn't need to return a value, return a `Task` type rather than `void`.</span></span>

<span data-ttu-id="8c56c-218">この例はクラスから`FixItQueueManager`取得されます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-218">This example is from the `FixItQueueManager` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

<span data-ttu-id="8c56c-219">トップレベルのイベント`async void`ハンドラーにのみ使用してください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-219">You should use `async void` only for top-level event handlers.</span></span> <span data-ttu-id="8c56c-220">としてメソッド`async void`を定義すると、呼び出し元**はメソッドを待機**したり、メソッドがスローする例外をキャッチしたりできません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-220">If you define a method as `async void`, the caller cannot **await** the method or catch any exceptions the method throws.</span></span> <span data-ttu-id="8c56c-221">詳細については、「[非同期プログラミングのベスト プラクティス](https://msdn.microsoft.com/magazine/jj991977.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-221">For more information, see [Best Practices in Asynchronous Programming](https://msdn.microsoft.com/magazine/jj991977.aspx).</span></span>

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a><span data-ttu-id="8c56c-222">キャンセル トークンを使用して作業者ロール ループから切り離す</span><span class="sxs-lookup"><span data-stu-id="8c56c-222">Use a cancellation token to break from worker role loop</span></span>

<span data-ttu-id="8c56c-223">通常、ワーカー ロールの**Run**メソッドには、無限ループが含まれています。</span><span class="sxs-lookup"><span data-stu-id="8c56c-223">Typically, the **Run** method on a worker role contains an infinite loop.</span></span> <span data-ttu-id="8c56c-224">ワーカー ロールが停止しているときは、[メソッド](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-224">When the worker role is stopping, the [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) method is called.</span></span> <span data-ttu-id="8c56c-225">Run メソッド内で実行されている作業をキャンセルし、正常に終了するには、**このメソッドを**使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-225">You should use this method to cancel the work that is being done inside the **Run** method and exit gracefully.</span></span> <span data-ttu-id="8c56c-226">それ以外の場合、プロセスは操作の途中で終了する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-226">Otherwise, the process might be terminated in the middle of an operation.</span></span>

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a><span data-ttu-id="8c56c-227">自動 MIME スニッフィング手順をオプトアウトする</span><span class="sxs-lookup"><span data-stu-id="8c56c-227">Opt out of Automatic MIME Sniffing Procedure</span></span>

<span data-ttu-id="8c56c-228">場合によっては、Web サーバーで指定された種類とは異なる MIME タイプが報告される場合があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-228">In some cases, Internet Explorer reports a MIME type different than the type specified by the web server.</span></span> <span data-ttu-id="8c56c-229">たとえば、INTERNET Explorer が HTTP 応答ヘッダーのコンテンツ タイプ: text/plain で配信されたファイル内の HTML コンテンツを検出した場合、コンテンツを HTML として表示する必要があると判断されます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-229">For instance, if Internet Explorer finds HTML content in a file delivered with the HTTP response header Content-Type: text/plain, Internet Explorer determines that the content should be rendered as HTML.</span></span> <span data-ttu-id="8c56c-230">残念ながら、この "MIME スニッフィング" は、信頼されていないコンテンツをホストしているサーバーのセキュリティ問題を引き起こす可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-230">Unfortunately, this "MIME-sniffing" can also lead to security problems for servers hosting untrusted content.</span></span> <span data-ttu-id="8c56c-231">この問題に対処するために、Internet Explorer 8 は MIME タイプの判別コードに多くの変更を加え、アプリケーション開発者が[MIME スニッフィングを無効にできるようにします](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8c56c-231">To combat this problem, Internet Explorer 8 has made a number of changes to MIME-type determination code and allows application developers to [opt out of MIME-sniffing](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx).</span></span> <span data-ttu-id="8c56c-232">次のコードが*Web.config*ファイルに追加されました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-232">The following code was added to the *Web.config* file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a><span data-ttu-id="8c56c-233">バンドルと縮小を有効にする</span><span class="sxs-lookup"><span data-stu-id="8c56c-233">Enable bundling and minification</span></span>

<span data-ttu-id="8c56c-234">Visual Studio が新しい Web プロジェクトを作成する場合、JavaScript ファイルのバンドルと縮小は既定では有効になりません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-234">When Visual Studio creates a new web project, bundling and minification of JavaScript files is not enabled by default.</span></span> <span data-ttu-id="8c56c-235">BundleConfig.csでコード行を追加しました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-235">We added a line of code in BundleConfig.cs:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a><span data-ttu-id="8c56c-236">認証クッキーの有効期限を設定する</span><span class="sxs-lookup"><span data-stu-id="8c56c-236">Set an expiration time-out for authentication cookies</span></span>

<span data-ttu-id="8c56c-237">既定では、認証 Cookie は 2 週間で期限切れになります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-237">By default, authentication cookies expire in two weeks.</span></span> <span data-ttu-id="8c56c-238">時間を短くすると、より安全です。</span><span class="sxs-lookup"><span data-stu-id="8c56c-238">A shorter time is more secure.</span></span> <span data-ttu-id="8c56c-239">この設定は *、次のStartupAuth.cs*で変更できます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-239">You can change this setting in *StartupAuth.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a><span data-ttu-id="8c56c-240">ローカル コンピューターで Visual Studio からアプリを実行する方法</span><span class="sxs-lookup"><span data-stu-id="8c56c-240">How to run the app from Visual Studio on your local computer</span></span>

<span data-ttu-id="8c56c-241">Fix It アプリを実行するには、次の 2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-241">There are two ways to run the Fix It app:</span></span>

- <span data-ttu-id="8c56c-242">新しいタスクを直接 SQL データベースに書き込む基本アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-242">Run the base application that writes new tasks directly to the SQL database.</span></span>
- <span data-ttu-id="8c56c-243">キューとバックエンド サービスを使用してアプリケーションを実行し、タスクを作成します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-243">Run the application using a queue plus a backend service to create tasks.</span></span> <span data-ttu-id="8c56c-244">キュー パターンについては、「[キュー中心の作業パターン](queue-centric-work-pattern.md)」の章で説明します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-244">The queue pattern is described in the chapter [Queue-Centric Work Pattern](queue-centric-work-pattern.md).</span></span>

<a id="runbase"></a>
### <a name="run-the-base-application"></a><span data-ttu-id="8c56c-245">基本アプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="8c56c-245">Run the base application</span></span>

1. <span data-ttu-id="8c56c-246">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) のインストール。</span><span class="sxs-lookup"><span data-stu-id="8c56c-246">Install [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>
2. <span data-ttu-id="8c56c-247">[.NET 用 Azure SDK をインストールします](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="8c56c-247">Install the [Azure SDK for .NET for Visual Studio](https://azure.microsoft.com/downloads/).</span></span>
3. <span data-ttu-id="8c56c-248">[.zip](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)ファイルは MSDN コード ギャラリーからダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-248">Download the .zip file from the [MSDN Code Gallery](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).</span></span>
4. <span data-ttu-id="8c56c-249">ファイル エクスプローラーで、.zip ファイルを右クリックして [プロパティ] をクリックし、[プロパティ] ウィンドウで [ブロック解除] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-249">In File Explorer, right-click the .zip file and click Properties, then in the Properties window click Unblock.</span></span>
5. <span data-ttu-id="8c56c-250">ファイルを解凍します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-250">Unzip the file.</span></span>
6. <span data-ttu-id="8c56c-251">.sln ファイルをダブルクリックして、Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-251">Double-click the .sln file to launch Visual Studio.</span></span>
7. <span data-ttu-id="8c56c-252">[**ツール**] メニューの **[NuGet パッケージ マネージャー**] をクリックし、[パッケージ マネージャー**コンソール**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-252">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>
8. <span data-ttu-id="8c56c-253">パッケージ マネージャー コンソール (PMC) で[復元]をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-253">In the Package Manager Console (PMC), click Restore.</span></span>
9. <span data-ttu-id="8c56c-254">Visual Studio を終了します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-254">Exit Visual Studio.</span></span>
10. <span data-ttu-id="8c56c-255">Azure[ストレージ エミュレーター](/azure/storage/common/storage-use-emulator)を起動します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-255">Start the [Azure storage emulator](/azure/storage/common/storage-use-emulator).</span></span>
11. <span data-ttu-id="8c56c-256">Visual Studio を再起動し、前の手順で閉じたソリューション ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-256">Restart Visual Studio, opening the solution file you closed in the previous step.</span></span>
12. <span data-ttu-id="8c56c-257">FixIt プロジェクトがスタートアップ プロジェクトとして設定されていることを確認し、Ctrl キーを押しながら F5 キーを押してプロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-257">Make sure the FixIt project is set as the startup project, and then press CTRL+F5 to run the project.</span></span>

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a><span data-ttu-id="8c56c-258">キュー処理を使用してアプリケーションを実行する</span><span class="sxs-lookup"><span data-stu-id="8c56c-258">Run the application with queue processing</span></span>

1. <span data-ttu-id="8c56c-259">「[基本アプリケーションを実行する](#runbase)」の指示に従ってブラウザーを閉じ、Visual Studio を閉じます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-259">Follow the directions for [Run the base application](#runbase), and then close the browser and close Visual Studio.</span></span>
2. <span data-ttu-id="8c56c-260">管理者特権で Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-260">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="8c56c-261">(Azure コンピューティング エミュレーターを使用しますが、これには管理者権限が必要です)。</span><span class="sxs-lookup"><span data-stu-id="8c56c-261">(You'll be using the Azure compute emulator, and that requires administrator privileges.)</span></span>
3. <span data-ttu-id="8c56c-262">*MyFixIt*プロジェクト (Web プロジェクト) のアプリケーション*Web.config*ファイルで、`appSettings/UseQueues`値を "true" に変更します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-262">In the application *Web.config* file in the *MyFixIt* project (the web project), change the value of `appSettings/UseQueues` to "true":</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. <span data-ttu-id="8c56c-263">Azure[ストレージ エミュレーター](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)がまだ実行されていない場合は、もう一度起動します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-263">If the [Azure storage emulator](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) isn't still running, start it again.</span></span>
5. <span data-ttu-id="8c56c-264">修正 Web プロジェクトとマイフィックスイットクラウドサービスプロジェクトを同時に実行します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-264">Run the FixIt web project and the MyFixItCloudService project simultaneously.</span></span>

    <span data-ttu-id="8c56c-265">Visual Studio を使用:</span><span class="sxs-lookup"><span data-stu-id="8c56c-265">Using Visual Studio:</span></span>

   1. <span data-ttu-id="8c56c-266">**F5 キー**を押して、FixIt プロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-266">Press **F5** to run the FixIt project.</span></span>
   2. <span data-ttu-id="8c56c-267">**ソリューション エクスプローラー**で、MyFixItCloudService プロジェクトを右クリックし、[**新しいインスタンスの\*\*\*\*デバッグ** > 開始] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-267">In **Solution Explorer**, right-click the MyFixItCloudService project, and then click **Debug** > **Start New Instance**.</span></span>

    <span data-ttu-id="8c56c-268">Web 用の Visual Studio 2013 エクスプレスの使用:</span><span class="sxs-lookup"><span data-stu-id="8c56c-268">Using Visual Studio 2013 Express for Web:</span></span>

   3. <span data-ttu-id="8c56c-269">ソリューション エクスプローラーで、FixIt ソリューションを右クリックし、[**プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-269">In Solution Explorer, right-click the FixIt solution and select **Properties**.</span></span>
   4. <span data-ttu-id="8c56c-270">[**複数のスタートアップ プロジェクト]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-270">Select **Multiple Startup Projects**.</span></span>
   5. <span data-ttu-id="8c56c-271">[**アクション**] ドロップダウン リストの [マイフィックスイット] と [マイフィックスイットクラウドサービス] で、[開始] を**選択**します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-271">In the **Action** dropdown list under MyFixIt and MyFixItCloudService, select **Start**.</span></span>
   6. <span data-ttu-id="8c56c-272">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-272">Click **OK**.</span></span>
   7. <span data-ttu-id="8c56c-273">**F5** キーを押して両方のプロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-273">Press **F5** to run both projects.</span></span>

      <span data-ttu-id="8c56c-274">プロジェクトを実行すると、Azure コンピューティング エミュレーターが起動します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-274">When you run the MyFixItCloudService project, Visual Studio starts the Azure compute emulator.</span></span> <span data-ttu-id="8c56c-275">ファイアウォールの構成によっては、ファイアウォールを通過するエミュレーターを許可する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-275">Depending on your firewall configuration, you might need to allow the emulator through the firewall.</span></span>

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a><span data-ttu-id="8c56c-276">Windows PowerShell スクリプトを使用して基本アプリを Azure アプリ サービス Web アプリにデプロイする方法</span><span class="sxs-lookup"><span data-stu-id="8c56c-276">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>

<span data-ttu-id="8c56c-277">[[すべての自動]](automate-everything.md)パターンを説明するために、Fix It アプリには、Azure で環境を設定し、プロジェクトを新しい環境にデプロイするスクリプトが付属しています。</span><span class="sxs-lookup"><span data-stu-id="8c56c-277">To illustrate the [Automate Everything](automate-everything.md) pattern, the Fix It app is supplied with scripts that set up an environment in Azure and deploy the project to the new environment.</span></span> <span data-ttu-id="8c56c-278">次の手順では、スクリプトの使用方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-278">The following instructions explain how to use the scripts.</span></span>

<span data-ttu-id="8c56c-279">キューを使用せずに Azure で実行する場合、キューを使用してローカルで実行するように変更を行った場合は、次の手順に進む前に UseQueues appSetting 値を false に設定し直してください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-279">If you want to run in Azure without using queues, and you made the changes to run locally with queues, make sure you set the UseQueues appSetting value back to false before proceeding with the following instructions.</span></span>

<span data-ttu-id="8c56c-280">この手順では、Fix It ソリューションをローカルでダウンロードして実行し、Azure アカウントを持っているか、管理が承認されている Azure サブスクリプションを持っていることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="8c56c-280">These instructions assume you have already downloaded and run the Fix It solution locally, and that you have an Azure account or have an Azure subscription that you are authorized to manage.</span></span>

1. <span data-ttu-id="8c56c-281">**コンソール**をインストールします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-281">Install the **Azure PowerShell** console.</span></span> <span data-ttu-id="8c56c-282">手順については、「 [Azure PowerShell のインストールおよび構成方法](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-282">For instructions, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span>

    <span data-ttu-id="8c56c-283">このカスタマイズされたコンソールは、Azure サブスクリプションで動作するように構成されています。</span><span class="sxs-lookup"><span data-stu-id="8c56c-283">This customized console is configured to work with your Azure subscription.</span></span> <span data-ttu-id="8c56c-284">Azure モジュールは*プログラム ファイル*ディレクトリにインストールされ、Azure PowerShell コンソールを使用するたびに自動的にインポートされます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-284">The Azure module is installed in the *Program Files* directory and is automatically imported on every use of the Azure PowerShell console.</span></span>

    <span data-ttu-id="8c56c-285">Windows PowerShell ISE などの別のホスト プログラムで作業する場合は[、Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553)コマンドレットを使用して Azure モジュールをインポートするか、Azure モジュールのコマンドを使用してモジュールの自動インポートをトリガーしてください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-285">If you prefer to work in a different host program, such as Windows PowerShell ISE, be sure to use the [Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet to import the Azure module or use a command in the Azure module to trigger automatic importing of the module.</span></span>
2. <span data-ttu-id="8c56c-286">**[管理者として実行**] オプションを使用して Azure PowerShell を起動します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-286">Start Azure PowerShell with the **Run as administrator** option.</span></span>
3. <span data-ttu-id="8c56c-287">[コマンドレット](https://go.microsoft.com/fwlink/p/?linkid=293941)を実行して、Azure PowerShell 実行ポリシーを に`RemoteSigned`設定します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-287">Run the [Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet to set the Azure PowerShell execution policy to `RemoteSigned`.</span></span> <span data-ttu-id="8c56c-288">**Y** (はい) と入力して、ポリシーの変更を完了します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-288">Enter **Y** (for Yes) to complete the policy change.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    <span data-ttu-id="8c56c-289">この設定では、デジタル署名されていないローカル スクリプトを実行できます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-289">This setting enables you to run local scripts that aren't digitally signed.</span></span> <span data-ttu-id="8c56c-290">(実行ポリシーを に`Unrestricted`設定して、後でブロック解除の手順を行う必要がなくなりますが、セキュリティ上の理由から推奨されません)。</span><span class="sxs-lookup"><span data-stu-id="8c56c-290">(You can also set the execution policy to `Unrestricted`, which would eliminate the need for the unblock step later, but this is not recommended for security reasons.)</span></span>
4. <span data-ttu-id="8c56c-291">このコマンド`Add-AzureAccount`レットを実行して、アカウントの資格情報を使用して PowerShell を設定します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-291">Run the `Add-AzureAccount` cmdlet to set up PowerShell with credentials for your account.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    <span data-ttu-id="8c56c-292">これらの資格情報は一定期間が経過すると期限切れになり、コマンドレットを`Add-AzureAccount`再実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-292">These credentials expire after a period of time and you have to re-run the `Add-AzureAccount` cmdlet.</span></span> <span data-ttu-id="8c56c-293">この電子書籍を作成中は、資格情報の有効期限が切れる前の時間制限は 12 時間です。</span><span class="sxs-lookup"><span data-stu-id="8c56c-293">As this e-book is being written, the time limit before credentials expire is 12 hours.</span></span>
5. <span data-ttu-id="8c56c-294">複数のサブスクリプションがある場合は、Select-AzureSubscription コマンドレットを使用して、テスト環境を作成するサブスクリプションを指定します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-294">If you have multiple subscriptions, use the Select-AzureSubscription cmdlet to specify the subscription you want to create the test environment in.</span></span>
6. <span data-ttu-id="8c56c-295">コマンドレットを使用して、同じ Azure サブスクリプション`Get-AzurePublishSettingsFile`の`Import-AzurePublishSettingsFile`管理証明書をインポートします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-295">Import a management certificate for the same Azure subscription by using the `Get-AzurePublishSettingsFile` and `Import-AzurePublishSettingsFile` cmdlets.</span></span> <span data-ttu-id="8c56c-296">これらのコマンドレットの最初のコマンドレットは証明書ファイルをダウンロードし、2 番目のコマンドレットでは、インポートするためにそのファイルの場所を指定します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-296">The first of these cmdlets downloads a certificate file, and in the second one you specify the location of that file in order to import it.</span></span> > [!IMPORTANT]
   > <span data-ttu-id="8c56c-297">ダウンロードしたファイルには Azure サービスの管理に使用できる証明書が含まれているため、ダウンロードしたファイルを安全な場所に保管するか、ファイルを削除します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-297">Keep the downloaded file in a safe location or delete it when you're done with it, because it contains a certificate that can be used to manage your Azure services.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    <span data-ttu-id="8c56c-298">証明書は、SQL Database サーバーでファイアウォール規則を設定するために開発マシンの IP アドレスを検出する REST API 呼び出しに使用されます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-298">The certificate is used for a REST API call that detects the development machine's IP address in order to set a firewall rule on the SQL Database server.</span></span>
7. <span data-ttu-id="8c56c-299">[Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912)コマンドレット ( エイリアス`cd`は`chdir`、 `sl`、および ) を実行して、スクリプトが格納されているディレクトリに移動します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-299">Run the [Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (aliases are `cd`, `chdir`, and `sl`) to navigate to the directory that contains the scripts.</span></span> <span data-ttu-id="8c56c-300">(これらは Fix It ソリューション フォルダーの*オートメーション*フォルダーにあります。ディレクトリ名のいずれかにスペースが含まれている場合は、パスを引用符で囲みます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-300">(They're located in the *Automation* folder in the Fix It solution folder.) Put the path in quotes if any of the directory names contain spaces.</span></span> <span data-ttu-id="8c56c-301">たとえば、`c:\Sample Apps\FixIt\Automation`ディレクトリに移動するには、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-301">For example, to navigate to the `c:\Sample Apps\FixIt\Automation` directory you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. <span data-ttu-id="8c56c-302">Windows PowerShell でこれらのスクリプトを実行できるようにするには、[ファイルのブロック解除](https://go.microsoft.com/fwlink/p/?linkid=294021)コマンドレットを使用します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-302">To allow Windows PowerShell to run these scripts, use the [Unblock-File](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet.</span></span> <span data-ttu-id="8c56c-303">(スクリプトはインターネットからダウンロードされたためブロックされます)。</span><span class="sxs-lookup"><span data-stu-id="8c56c-303">(The scripts are blocked because they were downloaded from the Internet.)</span></span>

    > [!WARNING]
    > <span data-ttu-id="8c56c-304">セキュリティ -`Unblock-File`スクリプトまたは実行可能ファイルで実行する前に、メモ帳でファイルを開き、コマンドを確認して、悪意のあるコードが含まれていないことを確認します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-304">Security - Before running `Unblock-File` on any script or executable file, open the file in Notepad, examine the commands, and verify that they do not contain any malicious code.</span></span>

    <span data-ttu-id="8c56c-305">たとえば、次のコマンドは、現在`Unblock-File`のディレクトリ内のすべてのスクリプトでコマンドレットを実行します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-305">For example, the following command runs the `Unblock-File` cmdlet on all scripts in the current directory.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. <span data-ttu-id="8c56c-306">ベース (キュー処理なし) の Web アプリを作成するには、環境作成スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-306">To create the web app for the base (no queues processing) Fix It app, run the environment creation script.</span></span>

    <span data-ttu-id="8c56c-307">required`Name`パラメーターは、データベースの名前を指定し、スクリプトが作成するストレージ アカウントにも使用されます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-307">The required `Name` parameter specifies the name of the database and is also used for the storage account that the script creates.</span></span> <span data-ttu-id="8c56c-308">名前は、azurewebsites.net ドメイン内でグローバルに一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-308">The name must be globally unique within the azurewebsites.net domain.</span></span> <span data-ttu-id="8c56c-309">Fixit や Test のように一意ではない名前を指定した場合 (または例の fixitdemo のように)、`New-AzureWebsite`競合を報告する内部エラーでコマンドレットが失敗します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-309">If you specify a name that is not unique, like Fixit or Test (or even as in the example, fixitdemo), the `New-AzureWebsite` cmdlet fails with an Internal Error that reports a conflict.</span></span> <span data-ttu-id="8c56c-310">このスクリプトは、Web アプリ、ストレージ アカウント、およびデータベースの名前要件に準拠するために、名前を小文字に変換します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-310">The script converts the name to all lower-case to comply with name requirements for web apps, storage accounts, and databases.</span></span>

    <span data-ttu-id="8c56c-311">必須`SqlDatabasePassword`パラメーターは、SQL データベース用に作成される管理者アカウントのパスワードを指定します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-311">The required `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="8c56c-312">&amp;&lt;パスワード&gt;に特殊な XML 文字を含;)。</span><span class="sxs-lookup"><span data-stu-id="8c56c-312">Don't include special XML characters in the password (&amp; &lt; &gt; ;).</span></span> <span data-ttu-id="8c56c-313">これは、スクリプトの記述方法の制限であり、Azure の制限ではありません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-313">This is a limitation of the way the scripts were written, not a limitation of Azure.</span></span>

    <span data-ttu-id="8c56c-314">たとえば、"fixitdemo" という名前の Web アプリを作成し、"Passw0rd1" という SQL Server 管理者パスワードを使用する場合は、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-314">For example, if you want to create a web app named "fixitdemo" and use a SQL Server administrator password of "Passw0rd1", you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    <span data-ttu-id="8c56c-315">名前はazurewebsites.net ドメイン内で一意である必要があり、パスワードはパスワードの複雑さに関する SQL Database の要件を満たしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-315">The name must be unique in the azurewebsites.net domain, and the password must meet SQL Database requirements for password complexity.</span></span> <span data-ttu-id="8c56c-316">(Passw0rd1 の例は要件を満たしています)。</span><span class="sxs-lookup"><span data-stu-id="8c56c-316">(The example Passw0rd1 does meet the requirements.)</span></span>

    <span data-ttu-id="8c56c-317">コマンドは ".\".</span><span class="sxs-lookup"><span data-stu-id="8c56c-317">Note that the command begins with ".\".</span></span> <span data-ttu-id="8c56c-318">スクリプトの悪意のある実行を防ぐために、Windows PowerShell では、スクリプトを実行するときにスクリプト ファイルへの完全修飾パスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-318">To help prevent malicious execution of scripts, Windows PowerShell requires that you provide the fully qualified path to the script file when you run a script.</span></span> <span data-ttu-id="8c56c-319">ドットを使用して、現在のディレクトリ (".\"または、次のような完全修飾パスを指定します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-319">You can use a dot to indicate the current directory (".\") or provide the fully qualified path, such as:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    <span data-ttu-id="8c56c-320">スクリプトの詳細については、コマンドレットを使用`Get-Help`します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-320">For more information about the script, use the `Get-Help` cmdlet.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    <span data-ttu-id="8c56c-321">Get-Help`Detailed`コマンド`Full`レット`Parameters`の`Examples`パラメーター 、、および パラメーターを使用して、返されるヘルプをフィルター処理できます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-321">You can use the `Detailed`, `Full`, `Parameters`, and `Examples` parameters of the Get-Help cmdlet to filter the help that is returned.</span></span>

    <span data-ttu-id="8c56c-322">スクリプトが失敗した場合、または "新しい AzureWeb サイト : 呼び出しセット AzureSubscription と選択 AzureSubscription" などのエラーが生成された場合は、Azure PowerShell の構成が完了していない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-322">If the script fails or generates errors, such as "New-AzureWebsite : Call Set-AzureSubscription and Select-AzureSubscription first," you might not have completed the configuration of Azure PowerShell.</span></span>

    <span data-ttu-id="8c56c-323">スクリプトが完了したら、Azure 管理ポータルを使用して、作成されたリソースを確認できます[。.「すべての自動化](automate-everything.md)」の章に示すようにします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-323">After the script finishes, you can use the Azure Management Portal to see the resources that were created, as shown in the [Automate Everything](automate-everything.md) chapter.</span></span>
10. <span data-ttu-id="8c56c-324">新しい Azure 環境に FixIt プロジェクトをデプロイするには *、AzureWebsite.ps1*スクリプトを使用します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-324">To deploy the FixIt project to the new Azure environment, use the *AzureWebsite.ps1* script.</span></span> <span data-ttu-id="8c56c-325">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-325">For example:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    <span data-ttu-id="8c56c-326">デプロイが完了すると、ブラウザーが開き、Azure で [Fix It] が実行されます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-326">When deployment is done, the browser opens with Fix It running in Azure.</span></span>

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a><span data-ttu-id="8c56c-327">スクリプトのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="8c56c-327">Troubleshooting the Windows PowerShell scripts</span></span>

<span data-ttu-id="8c56c-328">これらのスクリプトを実行するときに発生する最も一般的なエラーは、アクセス許可に関連しています。</span><span class="sxs-lookup"><span data-stu-id="8c56c-328">The most common errors encountered when running these scripts are related to permissions.</span></span> <span data-ttu-id="8c56c-329">成功し`Add-AzureAccount``Import-AzurePublishSettingsFile`、同じ Azure サブスクリプションに使用したことを確認します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-329">Make sure that `Add-AzureAccount` and `Import-AzurePublishSettingsFile` were successful and that you used them for the same Azure subscription.</span></span> <span data-ttu-id="8c56c-330">たとえ`Add-AzureAccount`成功したとしても、もう一度実行する必要があるかもしれません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-330">Even if `Add-AzureAccount` was successful you might have to run it again.</span></span> <span data-ttu-id="8c56c-331">追加された`Add-AzureAccount`アクセス許可は 12 時間で期限切れになります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-331">The permissions added by `Add-AzureAccount` expire in 12 hours.</span></span>

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a><span data-ttu-id="8c56c-332">オブジェクト参照がオブジェクト インスタンスに設定されていません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-332">Object reference not set to an instance of an object.</span></span>

<span data-ttu-id="8c56c-333">スクリプトがエラーを返す場合 ("オブジェクト参照がオブジェクトのインスタンスに設定されていません" など) は、Windows PowerShell が処理するオブジェクトを見つけることができない (null 参照例外`Add-AzureAccount`) ことを意味します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-333">If the script returns errors, such as "Object reference not set to an instance of an object," which means that Windows PowerShell can't find an object to process (this is a null reference exception), run the `Add-AzureAccount` cmdlet and try the script again.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a><span data-ttu-id="8c56c-334">内部エラー: サーバーで内部エラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-334">InternalError: The server encountered an internal error.</span></span>

<span data-ttu-id="8c56c-335">azurewebsites.net`New-AzureWebsite`ドメイン内で名前が一意でない場合、コマンドレットは内部エラーを返します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-335">The `New-AzureWebsite` cmdlet returns an internal error when the name is not unique in the azurewebsites.net domain.</span></span> <span data-ttu-id="8c56c-336">エラーを解決するには、*名前*に別の値を使用します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-336">To resolve the error, use a different value for the name, which is in the Name parameter of *New-AzureWebsiteEnv.ps1*.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a><span data-ttu-id="8c56c-337">スクリプトの再起動</span><span class="sxs-lookup"><span data-stu-id="8c56c-337">Restarting the script</span></span>

<span data-ttu-id="8c56c-338">"スクリプトが完了しました" というメッセージを出力する前にスクリプトが失敗したために*新しい AzureWebsiteEnv.ps1*スクリプトを再起動する必要がある場合は、停止する前にスクリプトが作成したリソースを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-338">If you need to restart the *New-AzureWebsiteEnv.ps1* script because it failed before it printed the "Script is complete" message, you might want to delete resources that the script created before it stopped.</span></span> <span data-ttu-id="8c56c-339">たとえば、スクリプトで既に ContosoFixItDemo Web アプリが作成されている場合、同じ名前でスクリプトを再度実行すると、スクリプトは失敗します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-339">For example, if the script already created the ContosoFixItDemo web app and you run the script again with the same name, the script will fail because the name is in use.</span></span>

<span data-ttu-id="8c56c-340">停止する前にスクリプトが作成したリソースを確認するには、次のコマンドレットを使用します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-340">To determine which resources the script created before it stopped, use the following cmdlets:</span></span>

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- <span data-ttu-id="8c56c-341">`Get-AzureSqlDatabase`: このコマンドレットを実行するには、データベース サーバー`Get-AzureSqlDatabase`名を次のコマンドにパイプします。`Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span><span class="sxs-lookup"><span data-stu-id="8c56c-341">`Get-AzureSqlDatabase`: To run this cmdlet, pipe the database server name to `Get-AzureSqlDatabase`:   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span></span>

<span data-ttu-id="8c56c-342">これらのリソースを削除するには、次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-342">To delete these resources, use the following commands.</span></span> <span data-ttu-id="8c56c-343">データベース サーバーを削除すると、そのサーバーに関連付けられているデータベースが自動的に削除されます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-343">Note that if you delete the database server, you automatically delete the databases associated with the server.</span></span>

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a><span data-ttu-id="8c56c-344">キュー処理を含むアプリを Azure アプリ サービス Web アプリと Azure クラウド サービスにデプロイする方法</span><span class="sxs-lookup"><span data-stu-id="8c56c-344">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>

<span data-ttu-id="8c56c-345">キューを有効にするには、MyFixIt\Web.config ファイルで次の変更を行います。</span><span class="sxs-lookup"><span data-stu-id="8c56c-345">To enable queues, make the following change in the MyFixIt\Web.config file.</span></span> <span data-ttu-id="8c56c-346">で`appSettings`、値を "true"`UseQueues`に変更します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-346">Under `appSettings`, change the value of `UseQueues` to "true":</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

<span data-ttu-id="8c56c-347">次に、[前述](#deploybase)のように、Azure App Service の Web アプリに MVC アプリケーションをデプロイします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-347">Then deploy the MVC application to an web app in Azure App Service, as described [earlier](#deploybase).</span></span>

<span data-ttu-id="8c56c-348">次に、新しい Azure クラウド サービスを作成します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-348">Next, create a new Azure cloud service.</span></span> <span data-ttu-id="8c56c-349">Fix It アプリに含まれるスクリプトは、クラウド サービスを作成またはデプロイしません。</span><span class="sxs-lookup"><span data-stu-id="8c56c-349">The scripts included with the Fix It app do not create or deploy the cloud service, so you must use Azure portal for this.</span></span> <span data-ttu-id="8c56c-350">ポータルで、[**新しい** -- **コンピューティング**-**クラウド サービス** -- **クイック作成**] をクリックし、URL とデータセンターの場所を入力します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-350">In the portal, click **New** -- **Compute** – **Cloud Service** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="8c56c-351">Web アプリをデプロイしたのと同じデータセンターを使用します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-351">Use the same data center where you deployed the web app.</span></span>

![](the-fix-it-sample-application/_static/image1.png)

<span data-ttu-id="8c56c-352">クラウド サービスを展開する前に、構成ファイルの一部を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-352">Before you can deploy the cloud service, you need to update some of the configuration files.</span></span>

<span data-ttu-id="8c56c-353">MyFixIt.WorkerRole\app.config の`connectionStrings`で、接続文字列の値を`appdb`SQL データベースの実際の接続文字列に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-353">In MyFixIt.WorkerRole\app.config, under `connectionStrings`, replace the value of the `appdb` connection string with the actual connection string for the SQL Database.</span></span> <span data-ttu-id="8c56c-354">ポータルから接続文字列を取得できます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-354">You can get the connection string from the portal.</span></span> <span data-ttu-id="8c56c-355">ポータルで、[ **SQL データベース** - **appdb** - Sql**データベースの表示**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8c56c-355">In the portal, click **SQL Databases** - **appdb** - **View SQL Database connection strings for ADO .Net, ODBC, PHP, and JDBC**.</span></span> <span data-ttu-id="8c56c-356">ADO.NET接続文字列をコピーし、値を app.config ファイルに貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-356">Copy the ADO.NET connection string and paste the value into the app.config file.</span></span> <span data-ttu-id="8c56c-357">"{ここにあなたの\_パスワード\_}" をデータベースパスワードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-357">Replace "{your\_password\_here}" with your database password.</span></span> <span data-ttu-id="8c56c-358">(MVC アプリを配置するためにスクリプトを使用した場合、スクリプト パラメーターでデータベース`SqlDatabasePassword`パスワードを指定します)。</span><span class="sxs-lookup"><span data-stu-id="8c56c-358">(Assuming you used the scripts to deploy the MVC app, you specified the database password in the `SqlDatabasePassword` script parameter.)</span></span>

<span data-ttu-id="8c56c-359">結果は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="8c56c-359">The result should look like the following:</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

<span data-ttu-id="8c56c-360">同じ MyFixIt.WorkerRole\app.config ファイルの`appSettings`で、Azure ストレージ アカウントの 2 つのプレースホルダー値を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-360">In the same MyFixIt.WorkerRole\app.config file, under `appSettings`, replace the two placeholder values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

<span data-ttu-id="8c56c-361">ポータルからアクセス キーを取得できます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-361">You can get the access key from the portal.</span></span> <span data-ttu-id="8c56c-362">[ストレージ アカウントを管理する方法を](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-362">See [How To Manage Storage Accounts](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span></span>

<span data-ttu-id="8c56c-363">MyFixItCloudService\サービス構成.Cloud.cscfg で、Azure ストレージ アカウントの同じ 2 つのプレースホルダー値を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="8c56c-363">In MyFixItCloudService\ServiceConfiguration.Cloud.cscfg, replace the same two placeholders values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

<span data-ttu-id="8c56c-364">これで、クラウド サービスを展開する準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="8c56c-364">Now you are ready to deploy the cloud service.</span></span> <span data-ttu-id="8c56c-365">ソリューションの詳細で、MyFixItCloudService プロジェクトを右クリックし、[**発行**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="8c56c-365">In Solution Explore, right-click the MyFixItCloudService project and select **Publish**.</span></span> <span data-ttu-id="8c56c-366">詳細については、[このチュートリアル](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)の第 2 部にある「[アプリケーションを Azure にデプロイ](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c56c-366">For more information, see "[Deploy the Application to Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)", which is in part 2 of [this tutorial](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8c56c-367">前へ</span><span class="sxs-lookup"><span data-stu-id="8c56c-367">Previous</span></span>](more-patterns-and-guidance.md)
