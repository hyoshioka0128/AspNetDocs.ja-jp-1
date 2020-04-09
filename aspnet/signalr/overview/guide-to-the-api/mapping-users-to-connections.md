---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: SignalR ユーザーの接続へのマッピング |マイクロソフトドキュメント
author: bradygaster
description: このトピックでは、ユーザーとその接続に関する情報を保持する方法について説明します。 パトリック・フレッチャーはこのトピックを書くのを手伝いました。 このトピックで使用されているソフトウェア バージョン.
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675779"
---
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="d69cf-105">SignalR ユーザーを接続にマッピングする</span><span class="sxs-lookup"><span data-stu-id="d69cf-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="d69cf-106">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d69cf-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="d69cf-107">このトピックでは、ユーザーとその接続に関する情報を保持する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d69cf-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="d69cf-108">パトリック・フレッチャーはこのトピックを書くのを手伝いました。</span><span class="sxs-lookup"><span data-stu-id="d69cf-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="d69cf-109">このトピックで使用するソフトウェアバージョン</span><span class="sxs-lookup"><span data-stu-id="d69cf-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="d69cf-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d69cf-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="d69cf-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="d69cf-111">.NET 4.5</span></span>
> - <span data-ttu-id="d69cf-112">シグナル・バージョン 2</span><span class="sxs-lookup"><span data-stu-id="d69cf-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="d69cf-113">このトピックの以前のバージョン</span><span class="sxs-lookup"><span data-stu-id="d69cf-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="d69cf-114">SignalR の以前のバージョンについては[、SignalR の古いバージョン](../older-versions/index.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d69cf-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="d69cf-115">質問とコメント</span><span class="sxs-lookup"><span data-stu-id="d69cf-115">Questions and comments</span></span>
>
> <span data-ttu-id="d69cf-116">このチュートリアルを気に入った方法と、ページの下部にあるコメントで改善できる内容についてのフィードバックを残してください。</span><span class="sxs-lookup"><span data-stu-id="d69cf-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="d69cf-117">チュートリアルに直接関連しない質問がある場合は[、ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="d69cf-118">はじめに</span><span class="sxs-lookup"><span data-stu-id="d69cf-118">Introduction</span></span>

<span data-ttu-id="d69cf-119">ハブに接続する各クライアントは、一意の接続 ID を渡します。この値は、ハブ コンテキスト`Context.ConnectionId`のプロパティで取得できます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="d69cf-120">アプリケーションでユーザーを接続 ID にマップし、そのマッピングを保持する必要がある場合は、次のいずれかを使用できます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="d69cf-121">ユーザー ID プロバイダー (SignalR 2)</span><span class="sxs-lookup"><span data-stu-id="d69cf-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="d69cf-122">辞書などの[メモリ内ストレージ](#inmemory)</span><span class="sxs-lookup"><span data-stu-id="d69cf-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="d69cf-123">各ユーザーの SignalR グループ</span><span class="sxs-lookup"><span data-stu-id="d69cf-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="d69cf-124">データベース テーブルや Azure テーブル[ストレージなどの永続的な外部](#database)ストレージ</span><span class="sxs-lookup"><span data-stu-id="d69cf-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="d69cf-125">これらの実装は、このトピックで示します。</span><span class="sxs-lookup"><span data-stu-id="d69cf-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="d69cf-126">クラスの`OnConnected`メソッド`OnDisconnected`、、および`OnReconnected``Hub`メソッドを使用して、ユーザー接続の状態を追跡します。</span><span class="sxs-lookup"><span data-stu-id="d69cf-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="d69cf-127">アプリケーションに最適な方法は、次の条件に依存します。</span><span class="sxs-lookup"><span data-stu-id="d69cf-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="d69cf-128">アプリケーションをホストしている Web サーバーの数。</span><span class="sxs-lookup"><span data-stu-id="d69cf-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="d69cf-129">現在接続しているユーザーの一覧を取得する必要があるかどうか。</span><span class="sxs-lookup"><span data-stu-id="d69cf-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="d69cf-130">アプリケーションまたはサーバーの再起動時にグループおよびユーザー情報を保持する必要があるかどうか。</span><span class="sxs-lookup"><span data-stu-id="d69cf-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="d69cf-131">外部サーバーを呼び出す待ち時間が問題かどうか。</span><span class="sxs-lookup"><span data-stu-id="d69cf-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="d69cf-132">次の表は、これらの考慮事項に対してどのアプローチが機能するかを示しています。</span><span class="sxs-lookup"><span data-stu-id="d69cf-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="d69cf-133">複数のサーバー</span><span class="sxs-lookup"><span data-stu-id="d69cf-133">More than one server</span></span> | <span data-ttu-id="d69cf-134">現在接続しているユーザーの一覧を取得する</span><span class="sxs-lookup"><span data-stu-id="d69cf-134">Get list of currently connected users</span></span> | <span data-ttu-id="d69cf-135">再起動後に情報を保持する</span><span class="sxs-lookup"><span data-stu-id="d69cf-135">Persist information after restarts</span></span> | <span data-ttu-id="d69cf-136">最適なパフォーマンス</span><span class="sxs-lookup"><span data-stu-id="d69cf-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d69cf-137">ユーザー ID プロバイダー</span><span class="sxs-lookup"><span data-stu-id="d69cf-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="d69cf-138">メモリ内</span><span class="sxs-lookup"><span data-stu-id="d69cf-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="d69cf-139">シングルユーザー グループ</span><span class="sxs-lookup"><span data-stu-id="d69cf-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="d69cf-140">常設、外部</span><span class="sxs-lookup"><span data-stu-id="d69cf-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="d69cf-141">IUserID プロバイダ</span><span class="sxs-lookup"><span data-stu-id="d69cf-141">IUserID provider</span></span>

<span data-ttu-id="d69cf-142">この機能により、ユーザーは新しいインターフェイス IUserIdProvider を介して IRequest に基づいてユーザー ID が何であるかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="d69cf-143">**を提供します。**</span><span class="sxs-lookup"><span data-stu-id="d69cf-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="d69cf-144">既定では、ユーザー名`IPrincipal.Identity.Name`としてユーザーを使用する実装があります。</span><span class="sxs-lookup"><span data-stu-id="d69cf-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="d69cf-145">これを変更するには、アプリケーションの`IUserIdProvider`起動時に実装をグローバル ホストに登録します。</span><span class="sxs-lookup"><span data-stu-id="d69cf-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="d69cf-146">ハブ内から、次の API を使用してこれらのユーザーにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="d69cf-147">**特定のユーザーへのメッセージの送信**</span><span class="sxs-lookup"><span data-stu-id="d69cf-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="d69cf-148">メモリ内ストレージ</span><span class="sxs-lookup"><span data-stu-id="d69cf-148">In-memory storage</span></span>

<span data-ttu-id="d69cf-149">次の例は、メモリに格納されているディクショナリに接続情報とユーザー情報を保持する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d69cf-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="d69cf-150">ディクショナリは、`HashSet`を使用して接続 ID を格納します。ユーザーはいつでも SignalR アプリケーションに複数の接続を持つことができます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="d69cf-151">たとえば、複数のデバイスまたは複数のブラウザー タブを介して接続されているユーザーには、複数の接続 ID があります。</span><span class="sxs-lookup"><span data-stu-id="d69cf-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="d69cf-152">アプリケーションがシャットダウンすると、すべての情報は失われますが、ユーザーが接続を再確立すると、情報が再び入力されます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="d69cf-153">環境に複数の Web サーバーが含まれている場合、各サーバーが個別の接続のコレクションを持つため、メモリー内ストレージは機能しません。</span><span class="sxs-lookup"><span data-stu-id="d69cf-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="d69cf-154">最初の例は、ユーザーと接続のマッピングを管理するクラスを示しています。</span><span class="sxs-lookup"><span data-stu-id="d69cf-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="d69cf-155">ハッシュセットのキーは、ユーザーの名前になります。</span><span class="sxs-lookup"><span data-stu-id="d69cf-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="d69cf-156">次の例は、ハブからの接続マッピング クラスの使用方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d69cf-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="d69cf-157">クラスのインスタンスは変数名`_connections`に格納されます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="d69cf-158">シングルユーザー グループ</span><span class="sxs-lookup"><span data-stu-id="d69cf-158">Single-user groups</span></span>

<span data-ttu-id="d69cf-159">各ユーザーのグループを作成し、そのユーザーのみに到達する場合は、そのグループにメッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="d69cf-160">各グループの名前は、ユーザーの名前です。</span><span class="sxs-lookup"><span data-stu-id="d69cf-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="d69cf-161">ユーザーが複数の接続を持つ場合、各接続 ID がユーザーのグループに追加されます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="d69cf-162">ユーザーが切断されたときに、グループから手動でユーザーを削除しないでください。</span><span class="sxs-lookup"><span data-stu-id="d69cf-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="d69cf-163">このアクションは、SignalR フレームワークによって自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="d69cf-164">次の例は、シングル ユーザー グループを実装する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d69cf-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="d69cf-165">永続的な外部ストレージ</span><span class="sxs-lookup"><span data-stu-id="d69cf-165">Permanent, external storage</span></span>

<span data-ttu-id="d69cf-166">このトピックでは、接続情報を格納するためにデータベースまたは Azure テーブル ストレージを使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="d69cf-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="d69cf-167">この方法は、各 Web サーバーが同じデータ リポジトリと対話できるため、複数の Web サーバーがある場合に機能します。</span><span class="sxs-lookup"><span data-stu-id="d69cf-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="d69cf-168">Web サーバーが動作しなくなったり、アプリケーションが再起動した場合`OnDisconnected`、メソッドは呼び出されません。</span><span class="sxs-lookup"><span data-stu-id="d69cf-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="d69cf-169">したがって、データ リポジトリに、有効でなくなった接続 ID のレコードが含まれる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d69cf-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="d69cf-170">これらの孤立したレコードをクリーンアップするには、アプリケーションに関連する期間外に作成された接続を無効にします。</span><span class="sxs-lookup"><span data-stu-id="d69cf-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="d69cf-171">このセクションの例には、接続が作成された時点の追跡の値が含まれていますが、バックグラウンド プロセスとして行う場合があるため、古いレコードをクリーンアップする方法は示しません。</span><span class="sxs-lookup"><span data-stu-id="d69cf-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="d69cf-172">データベース</span><span class="sxs-lookup"><span data-stu-id="d69cf-172">Database</span></span>

<span data-ttu-id="d69cf-173">次の例は、データベース内の接続およびユーザー情報を保持する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="d69cf-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="d69cf-174">データ アクセス テクノロジは、どのような方法でも使用できます。ただし、次の例では、Entity Framework を使用してモデルを定義する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="d69cf-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="d69cf-175">これらのエンティティ モデルは、データベース テーブルとフィールドに対応します。</span><span class="sxs-lookup"><span data-stu-id="d69cf-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="d69cf-176">データ構造は、アプリケーションの要件によってかなり異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="d69cf-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="d69cf-177">最初の例では、多数の接続エンティティに関連付けることができるユーザー エンティティを定義する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="d69cf-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="d69cf-178">次に、ハブから、次に示すコードを使用して各接続の状態を追跡できます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="d69cf-179">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="d69cf-179">Azure table storage</span></span>

<span data-ttu-id="d69cf-180">次の Azure テーブル ストレージの例は、データベースの例に似ています。</span><span class="sxs-lookup"><span data-stu-id="d69cf-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="d69cf-181">Azure テーブル ストレージ サービスを使用する際に必要な情報がすべて含まれているわけではありません。</span><span class="sxs-lookup"><span data-stu-id="d69cf-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="d69cf-182">詳細については、「 [.NET のテーブル ストレージの使用方法](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d69cf-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="d69cf-183">接続情報を格納するテーブル エンティティの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d69cf-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="d69cf-184">ユーザーは、ユーザー名でデータをパーティション分割し、各エンティティを接続 ID で識別するため、ユーザーはいつでも複数の接続を確立できます。</span><span class="sxs-lookup"><span data-stu-id="d69cf-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="d69cf-185">ハブでは、各ユーザーの接続の状態を追跡します。</span><span class="sxs-lookup"><span data-stu-id="d69cf-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
