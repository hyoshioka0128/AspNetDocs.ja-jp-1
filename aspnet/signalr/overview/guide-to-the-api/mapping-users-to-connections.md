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
# <a name="mapping-signalr-users-to-connections"></a>SignalR ユーザーを接続にマッピングする

[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> このトピックでは、ユーザーとその接続に関する情報を保持する方法について説明します。
>
> パトリック・フレッチャーはこのトピックを書くのを手伝いました。
>
> ## <a name="software-versions-used-in-this-topic"></a>このトピックで使用するソフトウェアバージョン
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - シグナル・バージョン 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>このトピックの以前のバージョン
>
> SignalR の以前のバージョンについては[、SignalR の古いバージョン](../older-versions/index.md)を参照してください。
>
> ## <a name="questions-and-comments"></a>質問とコメント
>
> このチュートリアルを気に入った方法と、ページの下部にあるコメントで改善できる内容についてのフィードバックを残してください。 チュートリアルに直接関連しない質問がある場合は[、ASP.NET SignalR フォーラム](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)または[StackOverflow.com](http://stackoverflow.com/)に投稿できます。

## <a name="introduction"></a>はじめに

ハブに接続する各クライアントは、一意の接続 ID を渡します。この値は、ハブ コンテキスト`Context.ConnectionId`のプロパティで取得できます。 アプリケーションでユーザーを接続 ID にマップし、そのマッピングを保持する必要がある場合は、次のいずれかを使用できます。

- [ユーザー ID プロバイダー (SignalR 2)](#IUserIdProvider)
- 辞書などの[メモリ内ストレージ](#inmemory)
- [各ユーザーの SignalR グループ](#groups)
- データベース テーブルや Azure テーブル[ストレージなどの永続的な外部](#database)ストレージ

これらの実装は、このトピックで示します。 クラスの`OnConnected`メソッド`OnDisconnected`、、および`OnReconnected``Hub`メソッドを使用して、ユーザー接続の状態を追跡します。

アプリケーションに最適な方法は、次の条件に依存します。

- アプリケーションをホストしている Web サーバーの数。
- 現在接続しているユーザーの一覧を取得する必要があるかどうか。
- アプリケーションまたはサーバーの再起動時にグループおよびユーザー情報を保持する必要があるかどうか。
- 外部サーバーを呼び出す待ち時間が問題かどうか。

次の表は、これらの考慮事項に対してどのアプローチが機能するかを示しています。

|  | 複数のサーバー | 現在接続しているユーザーの一覧を取得する | 再起動後に情報を保持する | 最適なパフォーマンス |
| --- | --- | --- | --- | --- |
| ユーザー ID プロバイダー | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| メモリ内 |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| シングルユーザー グループ | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| 常設、外部 | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>IUserID プロバイダ

この機能により、ユーザーは新しいインターフェイス IUserIdProvider を介して IRequest に基づいてユーザー ID が何であるかを指定できます。

**を提供します。**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

既定では、ユーザー名`IPrincipal.Identity.Name`としてユーザーを使用する実装があります。 これを変更するには、アプリケーションの`IUserIdProvider`起動時に実装をグローバル ホストに登録します。

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

ハブ内から、次の API を使用してこれらのユーザーにメッセージを送信できます。

**特定のユーザーへのメッセージの送信**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>メモリ内ストレージ

次の例は、メモリに格納されているディクショナリに接続情報とユーザー情報を保持する方法を示しています。 ディクショナリは、`HashSet`を使用して接続 ID を格納します。ユーザーはいつでも SignalR アプリケーションに複数の接続を持つことができます。 たとえば、複数のデバイスまたは複数のブラウザー タブを介して接続されているユーザーには、複数の接続 ID があります。

アプリケーションがシャットダウンすると、すべての情報は失われますが、ユーザーが接続を再確立すると、情報が再び入力されます。 環境に複数の Web サーバーが含まれている場合、各サーバーが個別の接続のコレクションを持つため、メモリー内ストレージは機能しません。

最初の例は、ユーザーと接続のマッピングを管理するクラスを示しています。 ハッシュセットのキーは、ユーザーの名前になります。

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

次の例は、ハブからの接続マッピング クラスの使用方法を示しています。 クラスのインスタンスは変数名`_connections`に格納されます。

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>シングルユーザー グループ

各ユーザーのグループを作成し、そのユーザーのみに到達する場合は、そのグループにメッセージを送信できます。 各グループの名前は、ユーザーの名前です。 ユーザーが複数の接続を持つ場合、各接続 ID がユーザーのグループに追加されます。

ユーザーが切断されたときに、グループから手動でユーザーを削除しないでください。 このアクションは、SignalR フレームワークによって自動的に実行されます。

次の例は、シングル ユーザー グループを実装する方法を示しています。

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>永続的な外部ストレージ

このトピックでは、接続情報を格納するためにデータベースまたは Azure テーブル ストレージを使用する方法について説明します。 この方法は、各 Web サーバーが同じデータ リポジトリと対話できるため、複数の Web サーバーがある場合に機能します。 Web サーバーが動作しなくなったり、アプリケーションが再起動した場合`OnDisconnected`、メソッドは呼び出されません。 したがって、データ リポジトリに、有効でなくなった接続 ID のレコードが含まれる可能性があります。 これらの孤立したレコードをクリーンアップするには、アプリケーションに関連する期間外に作成された接続を無効にします。 このセクションの例には、接続が作成された時点の追跡の値が含まれていますが、バックグラウンド プロセスとして行う場合があるため、古いレコードをクリーンアップする方法は示しません。

### <a name="database"></a>データベース

次の例は、データベース内の接続およびユーザー情報を保持する方法を示しています。 データ アクセス テクノロジは、どのような方法でも使用できます。ただし、次の例では、Entity Framework を使用してモデルを定義する方法を示します。 これらのエンティティ モデルは、データベース テーブルとフィールドに対応します。 データ構造は、アプリケーションの要件によってかなり異なる場合があります。

最初の例では、多数の接続エンティティに関連付けることができるユーザー エンティティを定義する方法を示します。

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

次に、ハブから、次に示すコードを使用して各接続の状態を追跡できます。

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure Table Storage

次の Azure テーブル ストレージの例は、データベースの例に似ています。 Azure テーブル ストレージ サービスを使用する際に必要な情報がすべて含まれているわけではありません。 詳細については、「 [.NET のテーブル ストレージの使用方法](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)」を参照してください。

接続情報を格納するテーブル エンティティの例を次に示します。 ユーザーは、ユーザー名でデータをパーティション分割し、各エンティティを接続 ID で識別するため、ユーザーはいつでも複数の接続を確立できます。

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

ハブでは、各ユーザーの接続の状態を追跡します。

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
