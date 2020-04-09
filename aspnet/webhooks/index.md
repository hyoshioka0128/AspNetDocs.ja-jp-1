---
uid: webhooks/index
title: ウェブフックの概要をASP.NET |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NETウェブフックの概要。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa5fa190386ec803a6801de2d815c948677fe1f5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675442"
---
# <a name="aspnet-webhooks-overview"></a>ASP.NETウェブフックの概要

WebHooks は、Web API と SaaS サービスを結び付けるための単純なパブリッシュ/サブ モデルを提供する軽量 HTTP パターンです。 サービスでイベントが発生すると、登録されたサブスクライバに HTTP POST 要求の形式で通知が送信されます。 POST 要求には、イベントに関する情報が含まれており、それに応じて受信側が動作することを可能にします。

そのシンプルさのために、WebHookはすでに[Dropbox、GitHub、](http://dropbox.com/)[ビットバケット](https://bitbucket.org/)[、MailChimp、](http://www.mailchimp.com/)[ペイパル](http://www.paypal.com/)、[スラック](http://www.slack.com)、[ストライプ](http://www.stripe.com)、[トレロ](http://www.trello.com/)、および多くを含む多数のサービスによって公開されています。 [GitHub](https://www.github.com/) たとえば[、Dropbox](http://dropbox.com/)でファイルが変更されたか、GitHub でコード変更が行われたか[、PayPal](http://www.paypal.com/)で支払いが開始されたか[、Trello](http://www.trello.com/)でカードが作成されたことを示す WebHook が考えます。 可能性は無限大です!

マイクロソフト ASP.NET WebHooks では、ASP.NET アプリケーションの一部として WebHook の送受信を容易に行うことができます。

* 受信側では、任意の数の WebHook プロバイダーから WebHook を受信および処理するための共通モデルを提供します。 それは[、ドロップボックス](http://dropbox.com/)[、GitHub、](https://www.github.com/)[ビットバケット](https://bitbucket.org/)、[メールチンパンジー](http://www.mailchimp.com/)、[ペイパル](http://www.paypal.com/)、[プッシャー](http://www.pusher.com)、[セールスフォース](http://www.salesforce.com)、[スラック](http://www.slack.com)、[ストライプ](http://www.stripe.com)、[トレロ](http://www.trello.com/)、[ワードプレス](http://www.wordpress.com)、[ゼンデスク](https://www.zendesk.com/)のサポートを備えたボックスから出てきますが、より多くのサポートを追加するのは簡単です。

* 送信側では、サブスクリプションの管理と格納、および適切なサブスクライバーセットへのイベント通知の送信をサポートします。 これにより、購読者がサブスクライブできる独自のイベントセットを定義し、発生時に通知することができます。

シナリオに応じて、2 つの部分を一緒に使用することも、離れたりすることもできます。 他のサービスから WebHook を受信するだけで済む場合は、受信側の部分だけを使用できます。他のユーザーが使用できるように WebHook を公開するだけの場合は、それを行うことができます。

コードは Web API 2 と ASP.NET MVC 5 ASP.NET対象とし[、GitHub で OSS](https://github.com/aspnet/WebHooks)として利用できます。

## <a name="webhooks-overview"></a>ウェブフックの概要

WebHooks は、サービス間での使用方法が異なるパターンですが、基本的な考え方は同じです。 WebHook は、ユーザーが他の場所で発生したイベントをサブスクライブできる単純な pub/sub モデルと考えることができます。 イベント通知は、イベント自体に関する情報を含む HTTP POST 要求として伝達されます。

通常、HTTP POST 要求には、WebHook がトリガーされるイベントに関する情報を含む、WebHook の送信者によって決定される JSON オブジェクトまたは HTML フォーム データが含まれます。 たとえば[、GitHub](https://www.github.com/)からの WebHook POST 要求本文は、特定のリポジトリで開かれる新しい問題の結果として次のようになります。

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

WebHook が実際に意図した送信者から送信されるようにするため、POST 要求は何らかの方法でセキュリティで保護され、受信側によって検証されます。 たとえば[、GitHub WebHooks](https://developer.github.com/webhooks/)には、要求本文のハッシュを含む*X ハブ署名*HTTP ヘッダーが含まれており、これは受信側の実装によってチェックされるため、心配する必要はありません。

WebHook フローは、一般的に次のようになります。

* WebHook 送信者は、クライアントがサブスクライブできるイベントを公開します。 イベントは、システムに対する監視可能な変更 (たとえば、新しいデータ項目が挿入された、プロセスが完了した、または他の何かを示します) を記述します。

* WebHook レシーバは、次の 4 つの項目から成る WebHook を登録してサブスクライブします。

     1. HTTP POST 要求の形式でイベント通知をポストする URI。

     2. WebHook を起動する特定のイベントを記述するフィルターのセット。

     3. HTTP POST 要求の署名に使用されるシークレット キー。

     4. HTTP POST 要求に含まれる追加データ。 これは、たとえば、追加の HTTP ヘッダー フィールドや HTTP POST 要求本文に含まれるプロパティです。

* イベントが発生すると、一致する WebHook 登録が見つかり、HTTP POST 要求が送信されます。 通常、何らかの理由で受信者が応答しない場合、または HTTP POST 要求がエラー応答を返した場合、HTTP POST 要求の生成が複数回再試行されます。

## <a name="webhooks-processing-pipeline"></a>Webフック処理パイプライン

受信 WebHook の処理パイプラインをASP.NETマイクロソフトは次のようになります。

![ASP.NET Webhook 処理パイプライン](_static/WebHookReceivers.png)

ここでの 2 つの主要な概念は *、レシーバー*と*ハンドラーです*。

* *受信側は、* 特定の送信者からの WebHook の特定のフレーバーを処理し、WebHook 要求が実際に意図された送信者から送信されていることを確認するためのセキュリティ チェックを実施する責任があります。

* *ハンドラー*は通常、ユーザー コードが特定の WebHook を処理する場所です。

以下のノードでは、これらの概念の詳細について説明します。
