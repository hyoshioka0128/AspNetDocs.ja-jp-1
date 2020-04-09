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
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>付録: 修正イットサンプルアプリケーション (Azure を使用した実世界のクラウドアプリの構築)

[マイク・ワッソン](https://github.com/MikeWasson),[リック・アンダーソン](https://twitter.com/RickAndMSFT),[トム・ダイクストラ](https://github.com/tdykstra)

[修正イットプロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> Azure 電子書籍**を使用したリアル ワールド クラウド アプリの構築**は、スコット ガスリーが開発したプレゼンテーションに基づいています。 クラウド向けの Web アプリの開発を成功させるために役立つ 13 のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章を](introduction.md)参照してください。

Azure を使用した実世界のクラウド アプリの構築に関するこの付録には、ダウンロードできる Fix It サンプル アプリケーションに関する追加情報を提供する次のセクションが含まれています。

- [既知の問題](#knownissues)
- [ベスト プラクティス](#bestpractices)
- [ローカル コンピューターで Visual Studio からアプリを実行する方法](#run-in-vs)
- [Windows PowerShell スクリプトを使用して基本アプリを Azure アプリ サービス Web アプリにデプロイする方法](#deploybase)
- [スクリプトのトラブルシューティング](#troubleshooting)
- [キュー処理を含むアプリを Azure アプリ サービス Web アプリと Azure クラウド サービスにデプロイする方法](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>既知の問題

Fix It アプリは、この電子書籍に記載されているパターンの一部をできるだけ簡単に説明するために開発されました。 しかし、電子書籍は現実世界のアプリの構築に関するものであるため、Fix It コードはリリースされたソフトウェアと同様のレビューとテストプロセスに従いました。 私たちは多くの問題を発見し、実際のアプリケーションと同様に、そのうちのいくつかは修正され、そのうちのいくつかは後のリリースに延期しました。

次の一覧には、運用アプリケーションで対処する必要がある問題が含まれていますが、何らかの理由で、Fix It サンプル アプリケーションの初期リリースでは対処しないことにしました。

### <a name="security"></a>Security

- 存在しない所有者にタスクを割り当てることができないようにしてください。
- 自分が作成したタスクまたは自分に割り当てられているタスクのみを表示および変更できることを確認します。
- サインイン ページと認証 Cookie には HTTPS を使用します。
- 認証クッキーの期限を指定します。

### <a name="input-validation"></a>入力の検証

一般に、運用アプリでは、Fix It アプリよりも多くの入力検証が行われます。 たとえば、アップロード可能な画像サイズ/画像ファイルサイズは制限されるべきです。

### <a name="administrator-functionality"></a>管理者機能

管理者は、既存のタスクの所有権を変更できる必要があります。 たとえば、タスクの作成者が退社し、管理アクセスが有効になっていない限り、タスクを保守する権限を持つユーザーが残さない場合があります。

### <a name="queue-message-processing"></a>キュー メッセージ処理

Fix It アプリでのキュー メッセージ処理は、最小限のコードでキュー中心の作業パターンを示すために簡単に設計されました。 この単純なコードは、実際の実稼働アプリケーションには適していません。

- このコードでは、各キュー メッセージが 1 回だけ処理されることを保証するものではありません。 キューからメッセージを取得すると、タイムアウト期間があり、その間にメッセージは他のキュー リスナーからは見えません。 メッセージが削除される前にタイムアウトが切れた場合、メッセージは再び表示されます。 したがって、ワーカー ロール インスタンスがメッセージの処理に長時間を費やす場合、理論的には同じメッセージが 2 回処理され、データベース内の重複したタスクが発生する可能性があります。 この問題の詳細については[、「Azure ストレージ キューの使用](https://msdn.microsoft.com/library/ff803365.aspx#sec7)」を参照してください。
- キューポーリング ロジックは、メッセージの取得をバッチ処理することで、よりコスト効率が高くなる可能性があります。 呼び出すたびに[、](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)トランザクションコストが発生します。 代わりに、単一のトランザクションで複数のメッセージを取得する[CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (複数形の's') を呼び出すことができます。 Azure Storage Queue のトランザクション コストは非常に低いため、ほとんどのシナリオではコストへの影響は大きくはありません。
- キュー メッセージ処理コードの緊密なループにより、CPU アフィニティが発生し、マルチコア VM を効率的に使用しません。 より優れた設計では、タスクの並列処理を使用して、複数の非同期タスクを並列に実行します。
- キューメッセージ処理には、基本的な例外処理しかありません。 たとえば、有害な[メッセージ](https://msdn.microsoft.com/library/ms789028.aspx)を処理しないコードです。 (メッセージの処理によって例外が発生した場合は、エラーをログに記録してメッセージを削除する必要があります。

### <a name="sql-queries-are-unbounded"></a>SQL クエリは無制限です

現在の Fix It コードでは、インデックス ページのクエリが返す行数に制限はありません。 大量のタスクがデータベースに入力されると、受信したリストのサイズがパフォーマンスの問題を引き起こす可能性があります。 解決策は、ページングを実装することです。 例については、「 [MVC アプリケーションのASP.NETでのエンティティ フレームワークを使用した並べ替え、フィルター処理、およびページング」](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)を参照してください。

### <a name="view-models-recommended"></a>推奨モデルの表示

Fix It アプリは、FixItTask エンティティ クラスを使用して、コントローラーとビューの間で情報を渡します。 ベスト プラクティスは、ビュー モデルを使用することです。 ドメイン モデル (FixItTask エンティティ クラスなど) はデータの永続化に必要な要素を中心に設計されていますが、ビュー モデルはデータの表示用に設計できます。 詳細については、「 [12 ASP.NET MVC のベスト プラクティス](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)」を参照してください。

### <a name="secure-image-blob-recommended"></a>セキュアイメージブロブ推奨

Fix It アプリはアップロードした画像をパブリックとして保存するため、URL を見つけた人は誰でも画像にアクセスできます。 画像は公開ではなく保護できます。

### <a name="no-powershell-automation-scripts-for-queues"></a>キューに PowerShell オートメーション スクリプトはありません

PowerShell のオートメーション スクリプトのサンプルは、Azure アプリ サービス Web アプリで完全に実行される Fix It の基本バージョンに対してのみ作成されました。 Web アプリと、キュー処理に必要なクラウド サービス環境を設定してデプロイするためのスクリプトは提供されていません。

### <a name="special-handling-for-html-codes-in-user-input"></a>ユーザー入力における HTML コードの特別な処理

ASP.NET、悪意のあるユーザーがユーザー入力テキスト ボックスにスクリプトを入力してクロスサイト スクリプティング攻撃を試みるさまざまな方法を自動的に防ぎます。 また、タスク`DisplayFor`のタイトルとメモを表示するために使用される MVC ヘルパーは、ブラウザーに送信する値を HTML エンコードします。 しかし、本番アプリでは、追加の対策を講じる必要があるかもしれません。 詳細については、「 [ASP.NET の要求検証](https://msdn.microsoft.com/library/hh882339.aspx)」を参照してください。

<a id="bestpractices"></a>
## <a name="best-practices"></a>ベスト プラクティス

以下は、コード レビューと Fix It アプリの元のバージョンのテストで発見された後に修正されたいくつかの問題です。 元のコーダが特定のベストプラクティスを認識していなかったために引き起こされたものもあれば、コードが迅速に書かれてリリースされたソフトウェアを意図していなかったためのものもありました。 このレビューとテストから学んだことが Web アプリを開発している他のユーザーにとって役立つ可能性がある場合に備えて、ここで問題をリストアップしています。

### <a name="dispose-the-database-repository"></a>データベース リポジトリを破棄する

クラス`FixItTaskRepository`は、エンティティ フレームワーク`DbContext`インスタンスを破棄する必要があります。 これを`IDisposable``FixItTaskRepository`クラスで実装して行いました。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

AutoFac はインスタンスを`FixItTaskRepository`自動的に破棄するので、明示的に破棄する必要はありません。

もう 1 つの方法`DbContext`は、`FixItTaskRepository`からメンバー変数を削除し`DbContext`、代わりに各リポジトリ メソッド内に`using`ステートメント内にローカル変数を作成することです。 次に例を示します。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>DI でシングルトンをそのように登録する

`PhotoService`クラスと`Logger`クラスのインスタンスは 1 つだけ必要なので、これらのクラスは *、DependenciesConfig.cs*で[依存関係を注入するために単一のインスタンスとして登録](https://code.google.com/p/autofac/wiki/InstanceScope)する必要があります。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>セキュリティ: エラーの詳細をユーザーに表示しない

元の Fix It アプリには一般的なエラー ページが含まれていなかったため、すべての例外が UI にバブルアップするため、データベース接続エラーなどの一部の例外では、完全なスタック トレースがブラウザーに表示される可能性があります。 詳細なエラー情報により、悪意のあるユーザーによる攻撃が容易になることがあります。 解決策は、例外の詳細をログに記録し、エラーの詳細を含まないエラー ページをユーザーに表示することです。 Fix It アプリは既にログに記録されており、エラー ページを表示するために`<customErrors mode=On>`、Web.config ファイルに追加されました。

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

既定では、*ビュー\共有\エラー.cshtml*がエラーに対して表示されます。 *Error.cshtml*をカスタマイズするか、独自のエラー ページ ビューを`defaultRedirect`作成して属性を追加できます。 特定のエラーに対して異なるエラーページを指定することもできます。

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>セキュリティ: タスクの作成者のみが編集できるようにする

ダッシュボードインデックスページには、ログオンしたユーザーによって作成されたタスクのみが表示されますが、悪意のあるユーザーが別のユーザーのタスクの ID を持つ URL を作成する可能性があります。 その*場合は*、DashboardController.csに 404 を返すコードを追加しました。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>例外を飲み込まない

元の Fix It アプリは、SQL クエリから生じる例外をログに記録した後、単に null を返しました。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

これにより、クエリは成功したが、行が返されないかのようにユーザーに見える。 解決策は、キャッチしてログに記録した後に例外を再スローすることです。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>作業者ロールのすべての例外をキャッチ

ワーカー ロール内の未処理の例外は VM をリサイクルするため、try-catch ブロックで行う処理をすべてラップし、すべての例外を処理します。

### <a name="specify-length-for-string-properties-in-entity-classes"></a>エンティティ クラスの文字列プロパティの長さを指定する

単純なコードを表示するために、Fix It アプリの元のバージョンでは、FixItTask エンティティのフィールドの長さが指定されず、その結果、データベース内で varchar(max) として定義されました。 その結果、UI はほぼすべての量の入力を受け入れます。 長さを指定すると、Web ページのユーザー入力とデータベース内の列サイズの両方に適用される制限が設定されます。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>変更が予想されない場合に、プライベート メンバーを読み取り専用としてマークする

たとえば、`DashboardController`クラス内での`FixItTaskRepository`インスタンスが作成され、変更される予定はないので、それを[readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)として定義しました。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>リストを使用します。リストの代わりに Any() 。カウント()0 &gt;

リスト内の 1 つまたは複数の項目が指定した条件に適合するかどうかが気にする場合は、条件に適合する項目が見つかるとすぐに返されるため[、Any](https://msdn.microsoft.com/library/bb534972.aspx) `Count`メソッドを使用します。 ダッシュボード*Index.cshtml*ファイルには、元々次のコードが含まれています。

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

これを次に変更しました。

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>MVC ヘルパーを使用して MVC ビューで URL を生成する

ホーム ページ**の [修正を作成**] ボタンの場合、Fix It アプリはアンカー要素をハードコーディングしました。

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

このような表示/アクションリンクの場合は[、Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML ヘルパーを使用することをお望みします。

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>ワーカー ロールで Thread.Sleep の代わりに Task.Delay を使用する

新しいプロジェクト テンプレートでは`Thread.Sleep`、ワーカー ロールのサンプル コードを記述しますが、スレッドをスリープ状態にする原因として、スレッド プールが不要なスレッドを追加で生成する可能性があります。 代わりに[Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx)を使用することで、これを回避できます。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>非同期の無効を回避する

非同期メソッドが値を返す必要がない場合は、 ではなく`Task``void`型を返します。

この例はクラスから`FixItQueueManager`取得されます。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

トップレベルのイベント`async void`ハンドラーにのみ使用してください。 としてメソッド`async void`を定義すると、呼び出し元**はメソッドを待機**したり、メソッドがスローする例外をキャッチしたりできません。 詳細については、「[非同期プログラミングのベスト プラクティス](https://msdn.microsoft.com/magazine/jj991977.aspx)」を参照してください。

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>キャンセル トークンを使用して作業者ロール ループから切り離す

通常、ワーカー ロールの**Run**メソッドには、無限ループが含まれています。 ワーカー ロールが停止しているときは、[メソッド](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)が呼び出されます。 Run メソッド内で実行されている作業をキャンセルし、正常に終了するには、**このメソッドを**使用する必要があります。 それ以外の場合、プロセスは操作の途中で終了する可能性があります。

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>自動 MIME スニッフィング手順をオプトアウトする

場合によっては、Web サーバーで指定された種類とは異なる MIME タイプが報告される場合があります。 たとえば、INTERNET Explorer が HTTP 応答ヘッダーのコンテンツ タイプ: text/plain で配信されたファイル内の HTML コンテンツを検出した場合、コンテンツを HTML として表示する必要があると判断されます。 残念ながら、この "MIME スニッフィング" は、信頼されていないコンテンツをホストしているサーバーのセキュリティ問題を引き起こす可能性があります。 この問題に対処するために、Internet Explorer 8 は MIME タイプの判別コードに多くの変更を加え、アプリケーション開発者が[MIME スニッフィングを無効にできるようにします](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。 次のコードが*Web.config*ファイルに追加されました。

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>バンドルと縮小を有効にする

Visual Studio が新しい Web プロジェクトを作成する場合、JavaScript ファイルのバンドルと縮小は既定では有効になりません。 BundleConfig.csでコード行を追加しました。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>認証クッキーの有効期限を設定する

既定では、認証 Cookie は 2 週間で期限切れになります。 時間を短くすると、より安全です。 この設定は *、次のStartupAuth.cs*で変更できます。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>ローカル コンピューターで Visual Studio からアプリを実行する方法

Fix It アプリを実行するには、次の 2 つの方法があります。

- 新しいタスクを直接 SQL データベースに書き込む基本アプリケーションを実行します。
- キューとバックエンド サービスを使用してアプリケーションを実行し、タスクを作成します。 キュー パターンについては、「[キュー中心の作業パターン](queue-centric-work-pattern.md)」の章で説明します。

<a id="runbase"></a>
### <a name="run-the-base-application"></a>基本アプリケーションを実行する

1. [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) のインストール。
2. [.NET 用 Azure SDK をインストールします](https://azure.microsoft.com/downloads/)。
3. [.zip](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)ファイルは MSDN コード ギャラリーからダウンロードします。
4. ファイル エクスプローラーで、.zip ファイルを右クリックして [プロパティ] をクリックし、[プロパティ] ウィンドウで [ブロック解除] をクリックします。
5. ファイルを解凍します。
6. .sln ファイルをダブルクリックして、Visual Studio を起動します。
7. [**ツール**] メニューの **[NuGet パッケージ マネージャー**] をクリックし、[パッケージ マネージャー**コンソール**] をクリックします。
8. パッケージ マネージャー コンソール (PMC) で[復元]をクリックします。
9. Visual Studio を終了します。
10. Azure[ストレージ エミュレーター](/azure/storage/common/storage-use-emulator)を起動します。
11. Visual Studio を再起動し、前の手順で閉じたソリューション ファイルを開きます。
12. FixIt プロジェクトがスタートアップ プロジェクトとして設定されていることを確認し、Ctrl キーを押しながら F5 キーを押してプロジェクトを実行します。

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>キュー処理を使用してアプリケーションを実行する

1. 「[基本アプリケーションを実行する](#runbase)」の指示に従ってブラウザーを閉じ、Visual Studio を閉じます。
2. 管理者特権で Visual Studio を起動します。 (Azure コンピューティング エミュレーターを使用しますが、これには管理者権限が必要です)。
3. *MyFixIt*プロジェクト (Web プロジェクト) のアプリケーション*Web.config*ファイルで、`appSettings/UseQueues`値を "true" に変更します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. Azure[ストレージ エミュレーター](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)がまだ実行されていない場合は、もう一度起動します。
5. 修正 Web プロジェクトとマイフィックスイットクラウドサービスプロジェクトを同時に実行します。

    Visual Studio を使用:

   1. **F5 キー**を押して、FixIt プロジェクトを実行します。
   2. **ソリューション エクスプローラー**で、MyFixItCloudService プロジェクトを右クリックし、[**新しいインスタンスの****デバッグ** > 開始] をクリックします。

    Web 用の Visual Studio 2013 エクスプレスの使用:

   3. ソリューション エクスプローラーで、FixIt ソリューションを右クリックし、[**プロパティ]** を選択します。
   4. [**複数のスタートアップ プロジェクト]** を選択します。
   5. [**アクション**] ドロップダウン リストの [マイフィックスイット] と [マイフィックスイットクラウドサービス] で、[開始] を**選択**します。
   6. **[OK]** をクリックします。
   7. **F5** キーを押して両方のプロジェクトを実行します。

      プロジェクトを実行すると、Azure コンピューティング エミュレーターが起動します。 ファイアウォールの構成によっては、ファイアウォールを通過するエミュレーターを許可する必要がある場合があります。

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>Windows PowerShell スクリプトを使用して基本アプリを Azure アプリ サービス Web アプリにデプロイする方法

[[すべての自動]](automate-everything.md)パターンを説明するために、Fix It アプリには、Azure で環境を設定し、プロジェクトを新しい環境にデプロイするスクリプトが付属しています。 次の手順では、スクリプトの使用方法について説明します。

キューを使用せずに Azure で実行する場合、キューを使用してローカルで実行するように変更を行った場合は、次の手順に進む前に UseQueues appSetting 値を false に設定し直してください。

この手順では、Fix It ソリューションをローカルでダウンロードして実行し、Azure アカウントを持っているか、管理が承認されている Azure サブスクリプションを持っていることを前提としています。

1. **コンソール**をインストールします。 手順については、「 [Azure PowerShell のインストールおよび構成方法](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)」を参照してください。

    このカスタマイズされたコンソールは、Azure サブスクリプションで動作するように構成されています。 Azure モジュールは*プログラム ファイル*ディレクトリにインストールされ、Azure PowerShell コンソールを使用するたびに自動的にインポートされます。

    Windows PowerShell ISE などの別のホスト プログラムで作業する場合は[、Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553)コマンドレットを使用して Azure モジュールをインポートするか、Azure モジュールのコマンドを使用してモジュールの自動インポートをトリガーしてください。
2. **[管理者として実行**] オプションを使用して Azure PowerShell を起動します。
3. [コマンドレット](https://go.microsoft.com/fwlink/p/?linkid=293941)を実行して、Azure PowerShell 実行ポリシーを に`RemoteSigned`設定します。 **Y** (はい) と入力して、ポリシーの変更を完了します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    この設定では、デジタル署名されていないローカル スクリプトを実行できます。 (実行ポリシーを に`Unrestricted`設定して、後でブロック解除の手順を行う必要がなくなりますが、セキュリティ上の理由から推奨されません)。
4. このコマンド`Add-AzureAccount`レットを実行して、アカウントの資格情報を使用して PowerShell を設定します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    これらの資格情報は一定期間が経過すると期限切れになり、コマンドレットを`Add-AzureAccount`再実行する必要があります。 この電子書籍を作成中は、資格情報の有効期限が切れる前の時間制限は 12 時間です。
5. 複数のサブスクリプションがある場合は、Select-AzureSubscription コマンドレットを使用して、テスト環境を作成するサブスクリプションを指定します。
6. コマンドレットを使用して、同じ Azure サブスクリプション`Get-AzurePublishSettingsFile`の`Import-AzurePublishSettingsFile`管理証明書をインポートします。 これらのコマンドレットの最初のコマンドレットは証明書ファイルをダウンロードし、2 番目のコマンドレットでは、インポートするためにそのファイルの場所を指定します。 > [!IMPORTANT]
   > ダウンロードしたファイルには Azure サービスの管理に使用できる証明書が含まれているため、ダウンロードしたファイルを安全な場所に保管するか、ファイルを削除します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    証明書は、SQL Database サーバーでファイアウォール規則を設定するために開発マシンの IP アドレスを検出する REST API 呼び出しに使用されます。
7. [Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912)コマンドレット ( エイリアス`cd`は`chdir`、 `sl`、および ) を実行して、スクリプトが格納されているディレクトリに移動します。 (これらは Fix It ソリューション フォルダーの*オートメーション*フォルダーにあります。ディレクトリ名のいずれかにスペースが含まれている場合は、パスを引用符で囲みます。 たとえば、`c:\Sample Apps\FixIt\Automation`ディレクトリに移動するには、次のコマンドを入力します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. Windows PowerShell でこれらのスクリプトを実行できるようにするには、[ファイルのブロック解除](https://go.microsoft.com/fwlink/p/?linkid=294021)コマンドレットを使用します。 (スクリプトはインターネットからダウンロードされたためブロックされます)。

    > [!WARNING]
    > セキュリティ -`Unblock-File`スクリプトまたは実行可能ファイルで実行する前に、メモ帳でファイルを開き、コマンドを確認して、悪意のあるコードが含まれていないことを確認します。

    たとえば、次のコマンドは、現在`Unblock-File`のディレクトリ内のすべてのスクリプトでコマンドレットを実行します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. ベース (キュー処理なし) の Web アプリを作成するには、環境作成スクリプトを実行します。

    required`Name`パラメーターは、データベースの名前を指定し、スクリプトが作成するストレージ アカウントにも使用されます。 名前は、azurewebsites.net ドメイン内でグローバルに一意である必要があります。 Fixit や Test のように一意ではない名前を指定した場合 (または例の fixitdemo のように)、`New-AzureWebsite`競合を報告する内部エラーでコマンドレットが失敗します。 このスクリプトは、Web アプリ、ストレージ アカウント、およびデータベースの名前要件に準拠するために、名前を小文字に変換します。

    必須`SqlDatabasePassword`パラメーターは、SQL データベース用に作成される管理者アカウントのパスワードを指定します。 &amp;&lt;パスワード&gt;に特殊な XML 文字を含;)。 これは、スクリプトの記述方法の制限であり、Azure の制限ではありません。

    たとえば、"fixitdemo" という名前の Web アプリを作成し、"Passw0rd1" という SQL Server 管理者パスワードを使用する場合は、次のコマンドを入力します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    名前はazurewebsites.net ドメイン内で一意である必要があり、パスワードはパスワードの複雑さに関する SQL Database の要件を満たしている必要があります。 (Passw0rd1 の例は要件を満たしています)。

    コマンドは ".\". スクリプトの悪意のある実行を防ぐために、Windows PowerShell では、スクリプトを実行するときにスクリプト ファイルへの完全修飾パスを指定する必要があります。 ドットを使用して、現在のディレクトリ (".\"または、次のような完全修飾パスを指定します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    スクリプトの詳細については、コマンドレットを使用`Get-Help`します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    Get-Help`Detailed`コマンド`Full`レット`Parameters`の`Examples`パラメーター 、、および パラメーターを使用して、返されるヘルプをフィルター処理できます。

    スクリプトが失敗した場合、または "新しい AzureWeb サイト : 呼び出しセット AzureSubscription と選択 AzureSubscription" などのエラーが生成された場合は、Azure PowerShell の構成が完了していない可能性があります。

    スクリプトが完了したら、Azure 管理ポータルを使用して、作成されたリソースを確認できます[。.「すべての自動化](automate-everything.md)」の章に示すようにします。
10. 新しい Azure 環境に FixIt プロジェクトをデプロイするには *、AzureWebsite.ps1*スクリプトを使用します。 次に例を示します。

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    デプロイが完了すると、ブラウザーが開き、Azure で [Fix It] が実行されます。

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>スクリプトのトラブルシューティング

これらのスクリプトを実行するときに発生する最も一般的なエラーは、アクセス許可に関連しています。 成功し`Add-AzureAccount``Import-AzurePublishSettingsFile`、同じ Azure サブスクリプションに使用したことを確認します。 たとえ`Add-AzureAccount`成功したとしても、もう一度実行する必要があるかもしれません。 追加された`Add-AzureAccount`アクセス許可は 12 時間で期限切れになります。

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>オブジェクト参照がオブジェクト インスタンスに設定されていません。

スクリプトがエラーを返す場合 ("オブジェクト参照がオブジェクトのインスタンスに設定されていません" など) は、Windows PowerShell が処理するオブジェクトを見つけることができない (null 参照例外`Add-AzureAccount`) ことを意味します。

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>内部エラー: サーバーで内部エラーが発生しました。

azurewebsites.net`New-AzureWebsite`ドメイン内で名前が一意でない場合、コマンドレットは内部エラーを返します。 エラーを解決するには、*名前*に別の値を使用します。

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>スクリプトの再起動

"スクリプトが完了しました" というメッセージを出力する前にスクリプトが失敗したために*新しい AzureWebsiteEnv.ps1*スクリプトを再起動する必要がある場合は、停止する前にスクリプトが作成したリソースを削除する必要があります。 たとえば、スクリプトで既に ContosoFixItDemo Web アプリが作成されている場合、同じ名前でスクリプトを再度実行すると、スクリプトは失敗します。

停止する前にスクリプトが作成したリソースを確認するには、次のコマンドレットを使用します。

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`: このコマンドレットを実行するには、データベース サーバー`Get-AzureSqlDatabase`名を次のコマンドにパイプします。`Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

これらのリソースを削除するには、次のコマンドを使用します。 データベース サーバーを削除すると、そのサーバーに関連付けられているデータベースが自動的に削除されます。

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>キュー処理を含むアプリを Azure アプリ サービス Web アプリと Azure クラウド サービスにデプロイする方法

キューを有効にするには、MyFixIt\Web.config ファイルで次の変更を行います。 で`appSettings`、値を "true"`UseQueues`に変更します。

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

次に、[前述](#deploybase)のように、Azure App Service の Web アプリに MVC アプリケーションをデプロイします。

次に、新しい Azure クラウド サービスを作成します。 Fix It アプリに含まれるスクリプトは、クラウド サービスを作成またはデプロイしません。 ポータルで、[**新しい** -- **コンピューティング**-**クラウド サービス** -- **クイック作成**] をクリックし、URL とデータセンターの場所を入力します。 Web アプリをデプロイしたのと同じデータセンターを使用します。

![](the-fix-it-sample-application/_static/image1.png)

クラウド サービスを展開する前に、構成ファイルの一部を更新する必要があります。

MyFixIt.WorkerRole\app.config の`connectionStrings`で、接続文字列の値を`appdb`SQL データベースの実際の接続文字列に置き換えます。 ポータルから接続文字列を取得できます。 ポータルで、[ **SQL データベース** - **appdb** - Sql**データベースの表示**] をクリックします。 ADO.NET接続文字列をコピーし、値を app.config ファイルに貼り付けます。 "{ここにあなたの\_パスワード\_}" をデータベースパスワードに置き換えます。 (MVC アプリを配置するためにスクリプトを使用した場合、スクリプト パラメーターでデータベース`SqlDatabasePassword`パスワードを指定します)。

結果は次のようになります。

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

同じ MyFixIt.WorkerRole\app.config ファイルの`appSettings`で、Azure ストレージ アカウントの 2 つのプレースホルダー値を置き換えます。

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

ポータルからアクセス キーを取得できます。 [ストレージ アカウントを管理する方法を](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)参照してください。

MyFixItCloudService\サービス構成.Cloud.cscfg で、Azure ストレージ アカウントの同じ 2 つのプレースホルダー値を置き換えます。

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

これで、クラウド サービスを展開する準備が整いました。 ソリューションの詳細で、MyFixItCloudService プロジェクトを右クリックし、[**発行**] を選択します。 詳細については、[このチュートリアル](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)の第 2 部にある「[アプリケーションを Azure にデプロイ](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)する」を参照してください。

> [!div class="step-by-step"]
> [前へ](more-patterns-and-guidance.md)
