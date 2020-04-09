---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: 監視とテレメトリ (Azure を使用した実際のクラウド アプリの構築) |マイクロソフトドキュメント
author: MikeWasson
description: Azure 電子書籍を使用したリアル ワールド クラウド アプリの構築は、スコット ガスリーが開発したプレゼンテーションに基づいています。 それは彼ができる13のパターンと実践を説明します.
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f61810ea7b486b2fa0bbb234edea7541eedde835
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675671"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>監視とテレメトリ (Azure を使用した実際のクラウド アプリの構築)

[マイク・ワッソン](https://github.com/MikeWasson),[リック・アンダーソン](https://twitter.com/RickAndMSFT),[トム・ダイクストラ](https://github.com/tdykstra)

[修正イットプロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure 電子書籍**を使用したリアル ワールド クラウド アプリの構築**は、スコット ガスリーが開発したプレゼンテーションに基づいています。 クラウド向けの Web アプリの開発を成功させるために役立つ 13 のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章を](introduction.md)参照してください。

多くの人々は、アプリケーションがダウンしたときに顧客に知らせるために顧客に依存しています。 これは実際にはどこでもベストプラクティスではなく、特にクラウドでのベストプラクティスではありません。 迅速な通知の保証はなく、通知を受け取ると、何が起こったのかについて最小限または誤解を招くデータを得ることがよくあります。 優れたテレメトリとログ記録システムを使用すると、アプリの動作を把握でき、問題が発生した場合は、すぐに確認し、トラブルシューティングに役立つ情報を入手できます。

## <a name="buy-or-rent-a-telemetry-solution"></a>テレメトリ ソリューションを購入またはレンタルする

> [!NOTE]
> この記事は[、アプリケーションインサイトが](/azure/application-insights/app-insights-overview)リリースされる前に書かれました。 アプリケーション インサイトは、Azure のテレメトリ ソリューションの推奨アプローチです。 詳細については[、ASP.NET Web サイトのアプリケーションインサイトの設定を](/azure/application-insights/app-insights-asp-net)参照してください。

クラウド環境の素晴らしい点の1つは、勝利への道を購入したりレンタルしたりするのは本当に簡単だということです。 テレメトリは一例です。 多くの努力を必要とせず、非常にコスト効率の高い、本当に優れたテレメトリシステムを稼働させることができます。 Azure と統合する優れたパートナーが多数あり、一部には無料のレベルがあるため、基本的なテレメトリを無償で利用できます。 Azure で現在利用できるもののほんの一部を次に示します。

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[マイクロソフト システム センター](http://www.petri.co.il/microsoft-system-center-introduction.htm#)には、監視機能も含まれています。

テレメトリ システムを使用する簡単さを示すために、新しい遺物の設定を簡単に説明します。

Azure 管理ポータルで、サービスにサインアップします。 [**新規作成**] をクリックし、[**ストア**] をクリックします。 [**アドオンの選択**] ダイアログ ボックスが表示されます。 下にスクロールして[**新しい遺物 ]** をクリックします。

![アドオンの選択](monitoring-and-telemetry/_static/image1.png)

右矢印をクリックし、目的のサービスレベルを選択します。 このデモでは無料の利用枠を使用します。

![アドオンの個人用設定](monitoring-and-telemetry/_static/image2.png)

右矢印をクリックして「購入」を確認すると、New Relic がポータルにアドオンとして表示されるようになりました。

![購入の確認](monitoring-and-telemetry/_static/image3.png)

![管理ポータルの新しい遺物アドオン](monitoring-and-telemetry/_static/image4.png)

[**接続情報**] をクリックし、ライセンス キーをコピーします。

![接続情報](monitoring-and-telemetry/_static/image5.png)

ポータルで Web アプリの **[構成**] タブに移動し、[**パフォーマンスの監視]** を **[アドオン**] に設定し、[**アドオンの選択**] ドロップダウン リストを **[新しい遺物]** に設定します。 次に、[**保存**] をクリックします。

![[構成] タブの新しい遺物](monitoring-and-telemetry/_static/image6.png)

Visual Studio で、アプリに新しい遺物 NuGet パッケージをインストールします。

![[構成] タブでの開発者分析](monitoring-and-telemetry/_static/image7.png)

アプリを Azure にデプロイし、使用を開始します。 いくつかの修正 It タスクを作成して、新しい Relic が監視するアクティビティを提供します。

次に、ポータルの [**アドオン**] タブの **[新しい遺物**] ページに戻り、[**管理**] をクリックします。 認証用のシングル サインオンを使用して、ポータルから New Relic 管理ポータルに送信されるので、資格情報を再入力する必要はありません。 [概要] ページには、さまざまなパフォーマンス統計情報が表示されます。 (画像をクリックすると、概要ページのフルサイズが表示されます。

[![[新しい遺物の監視] タブ](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

以下は、ご覧の統計のほんの一部です。

- 異なる時間帯の平均応答時間。

    ![応答時間](monitoring-and-telemetry/_static/image10.png)
- 1 日の異なる時間におけるスループット率 (1 分あたりの要求数)。

    ![スループット](monitoring-and-telemetry/_static/image11.png)
- サーバーの CPU 時間が異なる HTTP 要求の処理に費やされました。

    ![Web トランザクション時間](monitoring-and-telemetry/_static/image12.png)
- アプリケーション コードのさまざまな部分で CPU 時間を消費する:

    ![トレースの詳細](monitoring-and-telemetry/_static/image13.png)
- パフォーマンスの履歴統計。

    ![歴史的業績](monitoring-and-telemetry/_static/image14.png)
- Blob サービスなどの外部サービスへの呼び出しと、サービスの信頼性と応答性に関する統計情報。

    ![外部サービス](monitoring-and-telemetry/_static/image15.png)

    ![外部サービス](monitoring-and-telemetry/_static/image16.png)

    ![外部サービス](monitoring-and-telemetry/_static/image17.png)
- 世界のどこで、または米国の Web アプリのトラフィックがどこから来たかについての情報。

    ![[地理的な場所]](monitoring-and-telemetry/_static/image18.png)

レポートやイベントを設定することもできます。 たとえば、エラーが表示され始めたら、いつでも問題をサポートスタッフに通知する電子メールを送信できます。

![Reports](monitoring-and-telemetry/_static/image19.png)

新しい遺物はテレメトリシステムの一例に過ぎません。他のサービスからもこのすべてを取得できます。 クラウドの美しさは、コードを記述することなく、最小限または費用をかけずに、アプリケーションがどのように使用されているか、顧客が実際に経験している内容に関するより多くの情報を突然得ることができるということです。

<a id="log"></a>
## <a name="log-for-insight"></a>インサイトのログ

テレメトリ パッケージは最初の手順としては良いですが、独自のコードをインストルメント化する必要があります。 テレメトリ サービスは、問題が発生した場合に通知し、顧客が経験していることを示しますが、コードで何が起こっているのかについて多くの洞察を得ることができなくなる場合があります。

アプリの動作を確認するために、運用サーバーにリモートでアクセスする必要はありません。 1 台のサーバーがある場合は実用的かもしれませんが、何百ものサーバーにスケールし、どのサーバーにリモートで接続する必要があるかわからない場合はどうでしょうか。 ログには、問題を分析してデバッグするために運用サーバーにリモートで接続する必要のない十分な情報が必要です。 ログだけで問題を特定できるように、十分な情報を記録する必要があります。

### <a name="log-in-production"></a>本番環境でログイン

多くのユーザーが、問題が発生し、デバッグする場合にのみ、運用環境でトレースをオンにします。 これにより、問題を認識してから、問題に関するトラブルシューティング情報を取得するまでの間にかなりの時間がかかることがあります。 また、取得する情報は、断続的なエラーには役立たない場合があります。

ストレージが安価なクラウド環境で推奨されているのは、常に本番環境でログオンし続けましょう。 このようにして、エラーが発生した場合は既にログに記録されており、時間の経過とともに発生する問題や、異なる時間に定期的に発生する問題の分析に役立つ履歴データを取得できます。 古いログを削除するパージ プロセスを自動化できますが、ログを保持するよりも、このようなプロセスを設定する方がコストがかかる場合があります。

ログ記録の追加費用は、何か問題が発生したときに必要なすべての情報を利用できるようにすることで、トラブルシューティングに要する時間とコストを節約できるのと比べると、簡単です。 その後、誰かが昨夜8時頃にランダムエラーを起こしたと言ったが、彼らはエラーを覚えていないとき、あなたは簡単に問題が何であったかを見つけることができます。

月に 4 ドル未満の場合は、50 GB のログを手元に保持でき、パフォーマンスのボトルネックを避けるために、ログ ライブラリが非同期であることを確認する 1 つの点を念頭に置く限り、ログ記録のパフォーマンスへの影響は簡単です。

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>アクションが必要なログから情報を提供するログを区別する

ログは、情報を提供するためのものです (私はあなたに何かを知ってほしい) または ACT (私はあなたに何かをしてほしい)。 真に人や自動化されたプロセスにアクションを実行する必要がある問題に対してのみACTログを書くように注意してください。 あまりにも多くのACTログはノイズを発生させるので、本物の問題を見つけるためにすべてをふるいにかけるためにあまりにも多くの作業が必要です。 また、ACT ログがサポート スタッフに電子メールを送信するなどのアクションを自動的にトリガーする場合は、1 つの問題によって何千ものアクションがトリガーされないようにします。

NET System.Diagnostics トレースでは、ログにエラー、警告、情報、およびデバッグ/詳細レベルを割り当てることができます。 ACT ログのエラー レベルを予約し、INFORM ログに低いレベルを使用することで、ACT と INFORM ログを区別できます。

![ログ記録のレベル](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>実行時のログ レベルの構成

運用環境で常にログを記録する価値がありますが、もう 1 つのベスト プラクティスは、アプリケーションを再展開または再起動することなく、ログ記録する詳細レベルを実行時に調整できるログ記録フレームワークを実装することです。 たとえば、トレース機能を使用`System.Diagnostics`する場合は、エラー、警告、情報、およびデバッグ/詳細ログを作成できます。 エラー、警告、情報ログを常に運用環境でログに記録することをお勧めします。

Azure App Service の Web アプリには、`System.Diagnostics`ファイル システム、テーブル ストレージ、または BLOB ストレージにログを書き込む機能が組み込まれています。 ストレージの宛先ごとに異なるログレベルを選択したり、アプリケーションを再起動せずにログレベルをリアルタイムで変更したりできます。 BLOB ストレージのサポートにより[、HDInsight](https://docs.microsoft.com/azure/hdinsight/)は BLOB ストレージを直接操作する方法を認識しているため、アプリケーション ログで HDInsight 分析ジョブを実行しやすくなります。

### <a name="log-exceptions"></a>例外をログに記録する

例外を置くだけではありません *。* ログコード内の ToString() 。 それは文脈情報を残します。 SQL エラーの場合は、SQL エラー番号を除外します。 すべての例外に対して、コンテキスト情報、例外自体、および内部例外を含めて、トラブルシューティングに必要なすべてを提供していることを確認します。 たとえば、コンテキスト情報には、サーバー名、トランザクション ID、およびユーザー名 (パスワードやシークレットは含まれません) が含まれます。

例外ログで正しいことを行うために各開発者に頼っている場合、それらのいくつかはそうしません。 毎回正しい方法で実行されるようにするには、ロガー インターフェイスに例外処理をビルドします。

### <a name="log-calls-to-services"></a>サービスへの通話をログに記録する

データベース、REST API、外部サービスなど、アプリからサービスを呼び出すたびにログを書き込むのを強くお勧めします。 成功または失敗の兆候だけでなく、各要求にかかった時間をログに含めます。 クラウド環境では、完全な停止ではなく、スローダウンに関連する問題がしばしば発生します。 通常10ミリ秒かかるものは、突然1秒かかるかもしれません。 アプリが遅いと言われると、New Relic や持っているテレメトリ サービスを確認してエクスペリエンスを検証できるようにし、自分のログを見て、遅い理由の詳細を確認できます。

### <a name="use-an-ilogger-interface"></a>ILogger インターフェイスを使用する

プロダクション アプリケーションを作成するときに推奨される操作は、単純な*ILogger*インターフェイスを作成し、その中にいくつかのメソッドを貼り付ける方法です。 これにより、ログの実装を後で簡単に変更でき、すべてのコードを使用する必要がなくて済みます。 Fix It アプリ`System.Diagnostics.Trace`全体でクラスを使用することもできますが、代わりに*ILogger*を実装するログ クラスでカバーの下で使用し、アプリ全体で*ILogger*メソッドを呼び出します。

このようにして、ロギングをより豊かにしたい場合は、必要なロギングメカニズムに[`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs)置き換えることができます。 たとえば、アプリが大きくなるにつれて[、NLog](http://nlog-project.org/)や[エンタープライズ ライブラリ のログ記録アプリケーション ブロック](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)などのより包括的なログ パッケージを使用するように決定する場合があります。 [(Log4Net](http://logging.apache.org/log4net/)は、もう 1 つの一般的なログ フレームワークですが、非同期ログは実行されません)。

NLog などのフレームワークを使用する理由の 1 つとして、ログ出力を別々の大容量データ ストアと高価値データ ストアに分割することが考えられます。 これにより、ACT データへの迅速なアクセスを維持しながら、高速なクエリを実行する必要がない大量の INFORM データを効率的に格納できます。

### <a name="semantic-logging"></a>セマンティック ログ

より有用な診断情報を生成できる比較的新しいログ記録方法については、「[エンタープライズ ライブラリ セマンティック ログ アプリケーション ブロック (SLAB)」](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)を参照してください。 SLAB では、.NET 4.5 で[Windows イベント トレース](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx)(ETW) およびイベント[ソース](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx)のサポートを使用して、構造化されたクエリ可能なログを作成できます。 ログに記録するイベントの種類ごとに異なるメソッドを定義し、書き込む情報をカスタマイズできるようにします。 たとえば、SQL データベース エラーをログに記録するには、`LogSQLDatabaseError`メソッドを呼び出します。 このような例外の場合、重要な情報がエラー番号であることを知っているので、メソッドシグネチャにエラー番号パラメータを含め、書き込むログレコードにエラー番号を別のフィールドとして記録することができます。 数値は別のフィールドに含まれているため、エラー番号をメッセージ文字列に連結した場合よりも、SQL エラー番号に基づいてレポートを簡単かつ確実に取得できます。

## <a name="logging-in-the-fix-it-app"></a>修正アプリでのログイン

### <a name="the-ilogger-interface"></a>ILogger インターフェイス

ここでは、修正イットアプリの*ILogger*インターフェイスです。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

これらのメソッドを使用すると *、System.Diagnostics*でサポートされている同じ 4 つのレベルでログを書き込めます。 TraceApi メソッドは、待機時間に関する情報を含む外部サービス呼び出しをログに記録するためのものです。 デバッグ/詳細レベルのメソッドのセットを追加することもできます。

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger インターフェイスのロガー実装

インターフェイスの実装は本当に簡単です。 基本的には、標準の*System.Diagnostics*メソッドを呼び出すだけです。 次のスニペットは、3 つの情報メソッドと、それぞれ 1 つずつを示しています。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>ILogger メソッドを呼び出す

Fix It アプリのコードが例外をキャッチするたびに *、ILogger*メソッドを呼び出して例外の詳細をログに記録します。 また、データベース、Blob サービス、または REST API を呼び出すたびに、呼び出しの前にストップウォッチが開始され、サービスが戻ったときにストップウォッチが停止し、成功または失敗に関する情報と共に経過時間が記録されます。

ログ メッセージには、クラス名とメソッド名が含まれていることに注意してください。 ログ メッセージがアプリケーション コードの書き込み部分を識別するようにすることをお勧めします。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

したがって、Fix It アプリが SQL Database を呼び出すたびに、呼び出し、呼び出し元のメソッド、および正確にかかった時間を確認できます。

![ログ内の SQL データベースクエリ](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

ログを参照すると、データベース呼び出しの時間が可変であることがわかります。 この情報は役に立つ可能性があります: アプリは、このすべてをログに記録するため、データベース サービスが時間の経過ととおりにどのように実行されているかの履歴傾向を分析できます。 たとえば、サービスはほとんどの場合は高速ですが、要求が失敗したり、応答が遅くなったりする場合があります。

Blob サービスでも同じ操作を実行できます - アプリが新しいファイルをアップロードするたびにログが記録され、各ファイルのアップロードにかかった時間を正確に確認できます。

![BLOB アップロード ログ](monitoring-and-telemetry/_static/image23.png)

サービスを呼び出すたびにコードを記述するコードは数行にすぎず、誰かが問題に遭遇したと言うたびに、問題が何であったのか、エラーだったのか、それとも遅く実行されていたのかを正確に知っています。 サーバーにリモートで接続したり、エラーが発生した後にログを有効にしたりすることなく、問題の原因を特定して、問題の再現を希望できます。

## <a name="dependency-injection-in-the-fix-it-app"></a>Fix It アプリでの依存関係の挿入

上記の例のリポジトリ コンストラクタがロガー インターフェイスの実装をどのように取得するのか疑問に思うかもしれません。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

実装にインターフェイスを接続するには、アプリは[AutoFac](http://autofac.org/)で[依存関係の挿入](http://en.wikipedia.org/wiki/Dependency_injection)(DI) を使用します。 DI を使用すると、コード全体でインターフェイスに基づくオブジェクトを使用でき、インターフェイスのインスタンス化時に使用される実装を 1 か所で指定するだけで済みます。 これにより、実装を簡単に変更できます。 または、自動テストの場合は、ロガーのモックバージョンを置き換える必要があります。

Fix It アプリケーションは、すべてのリポジトリとすべてのコントローラで DI を使用します。 コントローラクラスのコンストラクタは、リポジトリがロガーインターフェイスを取得するのと同じ方法で*ITaskRepository*インターフェイスを取得します。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

アプリは、自動的にこれらのコンス トラクターの*タスクリポジトリ*と*ロガー*インスタンスを提供する AutoFac DI ライブラリを使用します。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

このコードは基本的に、コンストラクタが*ILogger*インターフェイスを必要とし *、Logger*クラスのインスタンスを渡し、IFixItTaskRepositoryインターフェイスが必要なときはいつでも*FixItTaskRepository*クラスのインスタンスを渡すことを示しています。 *IFixItTaskRepository*

[AutoFac](http://autofac.org/)は、使用できる多くの依存関係の挿入フレームワークの 1 つです。 もう 1 つの人気のあるのは、マイクロソフトのパターンとプラクティスで推奨されサポートされている[Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx)です。

## <a name="built-in-logging-support-in-azure"></a>Azure での組み込みのログのサポート

Azure では、Azure[アプリ サービスでの Web アプリの次の種類のログ記録がサポートされています](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)。

- System.Diagnostics トレース (サイトを再起動せずにオンとオフを切り、オンにして、その場でレベルを設定できます)。
- ウィンドウズイベント。
- IIS ログ (HTTP/FREB)

Azure では、クラウド[サービスで次の種類のログ記録がサポートされています](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)。

- 診断トレース。
- パフォーマンス カウンター。
- ウィンドウズイベント。
- IIS ログ (HTTP/FREB)
- カスタム ディレクトリの監視。

修正アプリは、System.Diagnostics トレースを使用します。 Web アプリで System.Diagnostics ログを有効にするために必要なのは、ポータル内のスイッチを反転するか、REST API を呼び出すことだけです。 ポータルで、サイトの **[構成**] タブをクリックし、下にスクロールして **[アプリケーション診断**] セクションを表示します。 ログ記録のオンとオフを切り、必要なログレベルを選択できます。 Azure で、ログをファイル システムまたはストレージ アカウントに書き込むことができます。

![[構成] タブでのアプリ診断とサイト診断](monitoring-and-telemetry/_static/image24.png)

Azure でのログ記録を有効にすると、作成中に [Visual Studio の出力] ウィンドウにログが表示されます。

![ストリーミング ログ メニュー](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![ストリーミング ログ メニュー](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

また、ストレージ アカウントに書き込まれたログを持ち、Visual Studio の**サーバー エクスプローラー**や Azure ストレージ[エクスプローラー](https://azure.microsoft.com/features/storage-explorer/)などの Azure ストレージ テーブル サービスにアクセスできるツールを使用してログを表示することもできます。

![サーバー エクスプローラのログ](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>まとめ

簡単に、使用でき、独自のコードでログを記録し、Azure でログを構成する、使用できやすいテレメトリ システムを実装できます。 また、運用上の問題が発生した場合、テレメトリ システムとカスタム ログを組み合わせて、問題が顧客にとって大きな問題になる前に、問題を迅速に解決するのに役立ちます。

次の[章](transient-fault-handling.md)では、一時的なエラーを処理する方法を見て、調査する必要がある実稼働の問題にならないようにします。

## <a name="resources"></a>リソース

詳細については、次のリソースを参照してください。

主にテレメトリに関するドキュメント:

- [マイクロソフトのパターンとプラクティス - Azure ガイダンス](https://msdn.microsoft.com/library/dn568099.aspx). 「インストルメンテーションとテレメトリのガイダンス、サービス のメータリング ガイダンス、正常性エンドポイントの監視パターン、およびランタイム再構成パターン」を参照してください。
- [クラウドでのペニー ピンチ: Azure Web サイトでの新しい遺物パフォーマンス監視の有効化](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)
- [Azure クラウド サービスでの大規模サービスの設計に関するベスト プラクティス](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx) マーク・シムズとマイケル・トマシーによるホワイトペーパー。 「テレメトリと診断」セクションを参照してください。
- [アプリケーションインサイトを用いて次世代開発を行う](https://msdn.microsoft.com/magazine/dn683794.aspx) MSDN マガジンの記事。

主にロギングに関するドキュメント:

- [セマンティック ログ アプリケーション ブロック (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/) ニール・マッケンジーは、SLABでセマンティックロギングのケースを提示します。
- [セマンティック ログを使用した構造化された意味のあるログの作成](https://channel9.msdn.com/Events/Build/2013/3-336): (ビデオ)ジュリアン・ドミンゲスは、SLABでセマンティックロギングのケースを提示します。
- [EF6 SQL ロギング – パート 1: 単純なログ記録](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/). アーサー ビッカース EF 6 でエンティティ フレームワークによって実行されるクエリをログに記録する方法を示します。
- [ASP.NET MVC アプリケーションでのエンティティ フレームワークでの接続の回復性とコマンドの傍受](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 9 部構成のチュートリアル シリーズの 4 番目は、エンティティ フレームワークによってデータベースに送信される SQL コマンドをログに記録する EF 6 コマンドの傍受機能を使用する方法を示します。
- [C# 5.0 発信者情報属性を使用してログ記録を改善](http://www.dotnetcurry.com/showarticle.aspx?ID=972)する 。 呼び出し元のメソッドの名前をリテラルにハードコーディングしたり、リフレクションを使用して手動で取得したりせずに、呼び出し元のメソッドの名前を簡単にログに記録する方法。

トラブルシューティングに関するドキュメント:

- [Azure&amp;のトラブルシューティング のデバッグブログ](https://blogs.msdn.com/b/kwill/).
- [AzureTools – Azure 開発者サポート チームが使用する診断ユーティリティ](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true)。 Azure VM でさまざまな診断および監視ツールをダウンロードして実行できるツールのダウンロード リンクを紹介し、提供します。 特定の VM で問題を診断する必要がある場合に役立ちます。
- [Visual Studio を使用して Azure アプリ サービスの Web アプリのトラブルシューティングを行います](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)。 System.Diagnostics トレースとリモート デバッグの概要を説明する手順を示します。

ビデオ:

- [フェイルセーフ: スケーラブルで回復力のあるクラウド サービスの構築](https://channel9.msdn.com/Series/FailSafe) ウルリッヒ・ホーマン、マルク・メルクリ、マーク・シムズによる9部構成のシリーズ。 マイクロソフト カスタマー アドバイザリー チーム (CAT) の実際の顧客との経験から得たストーリーで、高レベルの概念とアーキテクチャの原則を非常にアクセスしやすく興味深い方法で紹介します。 エピソード 4 と 9 は、監視とテレメトリに関するものです。 エピソード 9 には、サービスメトリックスハブ、AppDynamics、新しい遺物、および PagerDuty の監視サービスの概要が含まれています。
- [大きな建物: Azure のお客様から学んだ教訓 - パート II](https://channel9.msdn.com/Events/Build/2012/3-030). マーク・シムズは、失敗に対する設計とすべてをインストルメント化することについて話します。 フェイルセーフシリーズと同様ですが、より多くの方法の詳細に入ります。

コード サンプル:

- [Azure のクラウド サービスの基礎](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Microsoft Azure カスタマー アドバイザリ チームによって作成されたサンプル アプリケーション。 次の記事で説明されているように、テレメトリとログ記録の両方のプラクティスを示します。 このサンプルでは[、NLog](http://nlog-project.org/)を使用してアプリケーション ログを実装しています。 関連ドキュメントについては、[テレメトリとログ記録に関する TechNet Wiki の 4 つの記事のシリーズを](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)参照してください。

> [!div class="step-by-step"]
> [前へ](design-to-survive-failures.md)
> [次へ](transient-fault-handling.md)
