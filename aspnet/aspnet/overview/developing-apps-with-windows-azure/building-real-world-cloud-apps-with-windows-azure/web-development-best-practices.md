---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: Web 開発のベスト プラクティス (Azure を使用した実際のクラウド アプリの構築) |マイクロソフトドキュメント
author: MikeWasson
description: Azure 電子書籍を使用したリアル ワールド クラウド アプリの構築は、スコット ガスリーが開発したプレゼンテーションに基づいています。 それは彼ができる13のパターンと実践を説明します.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: dfd8a3ac2328d3f17dfbe36e68b37d181177b0f4
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675641"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>Web 開発のベスト プラクティス (Azure を使用した実際のクラウド アプリの構築)

[マイク・ワッソン](https://github.com/MikeWasson),[リック・アンダーソン](https://twitter.com/RickAndMSFT),[トム・ダイクストラ](https://github.com/tdykstra)

[修正イットプロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure 電子書籍**を使用したリアル ワールド クラウド アプリの構築**は、スコット ガスリーが開発したプレゼンテーションに基づいています。 クラウド向けの Web アプリの開発を成功させるために役立つ 13 のパターンとプラクティスについて説明します。 電子書籍の詳細については、[最初の章を](introduction.md)参照してください。

最初の 3 つのパターンは、アジャイル開発プロセスの設定に関するものでした。残りはアーキテクチャとコードに関するものです。 これは、Web 開発のベスト プラクティスのコレクションです。

- スマート ロード バランサーの背後にある[ステートレス Web サーバー](#stateless) 。
- [セッション状態を回避](#sessionstate)する (または、これを回避できない場合は、データベースではなく分散キャッシュを使用します)。
- [CDN を使用して](#cdn)、静的ファイルアセット (イメージ、スクリプト) をエッジ・キャッシュします。
- [NET 4.5 の非同期サポートを使用](#async)して、呼び出しをブロックしないようにします。

これらのプラクティスは、クラウド アプリだけでなく、すべての Web 開発に有効ですが、クラウド アプリでは特に重要です。 クラウド環境で提供される柔軟性の高いスケーリングを最適に活用できるように、連携して作業を行います。 これらのプラクティスに従わない場合は、アプリケーションをスケーリングするときに制限が生じるでしょう。

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>スマート ロード バランサーの背後にあるステートレス Web 層

*ステートレス Web 層*は、アプリケーション データを Web サーバーのメモリまたはファイル システムに格納しないことを意味します。 Web 層をステートレスにしておくと、より優れたカスタマー エクスペリエンスを提供し、コストを節約できます。

- Web 層がステートレスで、ロード バランサーの背後にある場合は、サーバーを動的に追加または削除することで、アプリケーション トラフィックの変更にすばやく対応できます。 実際に使用している限り、サーバー リソースに対してのみ支払いを行うクラウド環境では、需要の変化に対応する能力が大幅に節約されます。
- ステートレス Web 層は、アプリケーションのスケールアウトが非常に簡単なアーキテクチャです。 また、スケーリングのニーズに迅速に対応し、プロセスの開発とテストに費やすお金を減らすことができます。
- オンプレミスのサーバーと同様に、クラウド サーバーは、パッチを適用して再起動する必要があります。Web 層がステートレスである場合、サーバーが一時的にダウンしたときにトラフィックを再ルーティングしても、エラーや予期しない動作は発生しません。

ほとんどの実際のアプリケーションでは、Web セッションの状態を格納する必要があります。ここでの主なポイントは、Webサーバーに保存しないことです。 キャッシュ プロバイダーを使用して、cookie 内のクライアントやプロセス外のサーバー側の場合など、他の方法ASP.NET状態を格納できます。 ローカル ファイル システムの代わりに[、Windows Azure Blob ストレージ](unstructured-blob-storage.md)にファイルを格納できます。

Web 層がステートレスである場合に、Windows Azure Web サイトでアプリケーションを簡単にスケーリングする方法の例として、管理ポータルで Windows Azure Web サイトの **[スケール**] タブを参照してください。

![[スケール] タブ](web-development-best-practices/_static/image1.png)

Web サーバーを追加する場合は、インスタンス数スライダーを右にドラッグするだけです。 5 に設定し、[**保存**] をクリックすると、数秒以内に Windows Azure に 5 台の Web サーバーが Web サイトのトラフィックを処理します。

![5 つのインスタンス](web-development-best-practices/_static/image2.png)

インスタンスのカウントを 3 に設定するか、1 に戻すのと同じように簡単に設定できます。 スケール バックすると、Windows Azure は時間単位ではなく分単位で課金されるため、すぐにお金の節約を開始します。

また、CPU 使用率に基づいて Web サーバーの数を自動的に増減するように Windows Azure に指示することもできます。 次の例では、CPU 使用率が 60% を下回ると、Web サーバーの数は最小 2 まで減少し、CPU 使用率が 80% を超えた場合、Web サーバーの数は最大 4 まで増加します。

![CPU 使用率によるスケール](web-development-best-practices/_static/image3.png)

また、勤務時間中にサイトがビジー状態になることがわかっている場合はどうでしょうか。 Windows Azure では、日中に複数のサーバーを実行し、1 つのサーバーの夜間、夜間、週末に減らすことができます。 次の一連のスクリーン ショットは、午前 8 時から午後 5 時までの勤務時間中に 1 台のサーバーを稼働時間外に実行し、4 台のサーバーを実行するように Web サイトを設定する方法を示しています。

![スケジュールによるスケール](web-development-best-practices/_static/image4.png)

![スケジュール時間の設定](web-development-best-practices/_static/image5.png)

![昼間のスケジュール](web-development-best-practices/_static/image6.png)

![平日のスケジュール](web-development-best-practices/_static/image7.png)

![週末のスケジュール](web-development-best-practices/_static/image8.png)

もちろん、このすべては、スクリプトだけでなく、ポータルで行うことができます。

アプリケーションのスケール アウト機能は、Web 層をステートレスに保つことによって、サーバー VM を動的に追加または削除する障害を避ける限り、Windows Azure ではほとんど無制限です。

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>セッション状態の回避

ユーザー セッションの状態をなんらかの形で格納しないのは、実際のクラウド アプリケーションでは実用的でない場合が多いですが、方法によっては、パフォーマンスとスケーラビリティに与える影響が大きくなります。 状態を格納する必要がある場合は、状態の量を少なくし、Cookie に格納することをお勧めします。 それが実現不可能な場合、次に最善の解決策は[、分散型のインメモリ キャッシュ](distributed-caching.md#sessionstate)用ASP.NETプロバイダとのセッション状態を使用することです。 パフォーマンスとスケーラビリティの観点から最もお勧めできないのが、データベースを利用したセッション状態プロバイダーを使用する方法です。

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>CDN を使用して静的ファイル資産をキャッシュする

CDN は、コンテンツ配信ネットワークの頭字語です。 CDN プロバイダーに画像やスクリプト ファイルなどの静的ファイル資産を提供し、プロバイダーは、ユーザーがアプリケーションにアクセスする場所で、キャッシュされた資産の比較的迅速な応答と低待機時間を得ることができるように、世界中のデータ センターにこれらのファイルをキャッシュします。 これにより、サイト全体のロード時間が短縮され、Web サーバーの負荷が軽減されます。 地理的に広く分散している対象ユーザーに到達する場合、CDN は特に重要です。

Windows Azure には CDN が含まれているので、Windows Azure または任意の Web ホスティング環境で実行されるアプリケーションで他の CDN を使用できます。

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>NET 4.5 の非同期サポートを使用して呼び出しをブロックしないようにする

.NET 4.5 では、タスクを非同期的に処理する作業を簡単にするために、C# および VB のプログラミング言語が拡張されました。 非同期プログラミングの利点は、複数の Web サービス呼び出しを同時に開始する場合など、並列処理の状況だけではありません。 また、高負荷条件下で Web サーバーのパフォーマンスを高め、信頼性の高い状態で実行することもできます。 Web サーバーでは使用可能なスレッドの数が限られており、すべてのスレッドが使用中の場合、高負荷条件の場合、着信要求はスレッドが解放されるまで待機する必要があります。 アプリケーション コードがデータベース クエリや Web サービス呼び出しなどのタスクを非同期的に処理しない場合、サーバーが I/O 応答を待機している間、多くのスレッドが不必要に縛られます。 これにより、負荷の高い状況下でサーバーが処理できるトラフィックの量が制限されます。 非同期プログラミングでは、Web サービスまたはデータベースがデータを返すのを待機しているスレッドは、 データが受信されるまで、新しい要求を処理するために解放されます。 ビジー状態の Web サーバーでは、数百または数千の要求を速やかに処理でき、それ以外の場合はスレッドが解放されるのを待ちます。

先ほど説明したように、Web サイトを処理する Web サーバーの数を増やすのと同じくらい簡単です。 したがって、サーバーがスループットを向上できる場合は、その数をそれほど多く必要としないため、特定のトラフィック量に対するサーバー数が他の方法よりも少なくて済むため、コストを削減できます。

NET 4.5 非同期プログラミング モデルのサポートは、web フォーム、MVC、および Web API の ASP.NET 4.5 に含まれています。エンティティ フレームワーク 6、および[Windows Azure ストレージ API](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx)で。

### <a name="async-support-in-aspnet-45"></a>ASP.NET 4.5 での非同期サポート

ASP.NET 4.5 では、言語だけでなく、MVC、Web フォーム、および Web API フレームワークにも非同期プログラミングのサポートが追加されました。 たとえば、ASP.NET MVC コントローラー アクション メソッドは、web 要求からデータを受け取り、ビューにデータを渡し、ブラウザーに送信される HTML を作成します。 多くの場合、アクション メソッドは、Web ページに表示したり、Web ページに入力されたデータを保存したりするために、データベースまたは Web サービスからデータを取得する必要があります。 このようなシナリオでは、アクション メソッドを非同期にするのは簡単です: *ActionResult*オブジェクトを返す代わりに、*タスク&lt;アクション&gt;の結果*を返し *、async*キーワードを使用してメソッドをマークします。 メソッド内で、コード行が待機時間を含む操作を開始するときに、await キーワードを使用してマークします。

データベース クエリのリポジトリ メソッドを呼び出す単純なアクション メソッドを次に示します。

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

次に、データベース呼び出しを非同期で処理するメソッドと同じです。

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

この点では、コンパイラは適切な非同期コードを生成します。 アプリケーションが 呼`FindTaskByIdAsync`び出しを行うと、ASP.NET要求を`FindTask`行い、ワーカー スレッドを巻き戻して、別の要求を処理できるようにします。 要求が`FindTask`完了すると、スレッドが再始動され、その呼び出しの後に来るコードの処理が続行されます。 `FindTask`要求が開始された時点からデータが返されるまでの間に、有用な処理を行うためのスレッドがあり、それ以外の場合は応答を待機します。

非同期コードにはオーバーヘッドがいくつか存在しますが、負荷の低い状況ではオーバーヘッドは無視できますが、負荷の高い条件では、使用可能なスレッドを待機する要求を処理できます。

ASP.NET 1.1 以降、このような非同期プログラミングを行うことは可能でしたが、書き込みが困難で、エラーが発生しやすく、デバッグが困難でした。 ASP.NET 4.5 でコーディングを簡略化したので、もうそれをしない理由はありません。

### <a name="async-support-in-entity-framework-6"></a>エンティティ フレームワーク 6 での非同期サポート

4.5 の非同期サポートの一環として、Web サービス呼び出し、ソケット、およびファイル システム I/O の非同期サポートが出荷されましたが、Web アプリケーションの最も一般的なパターンはデータベースをヒットするものであり、データ ライブラリは非同期をサポートしていませんでした。 現在、Entity Framework 6 は、データベース アクセスの非同期サポートを追加します。

Entity Framework 6 では、クエリまたはコマンドをデータベースに送信するすべてのメソッドは、非同期バージョンを持ちます。 この例は *、Find*メソッドの非同期バージョンを示しています。

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

また、この非同期サポートは、挿入、削除、更新、および単純な検索だけでなく、LINQ クエリでも機能します。

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

このコードでは、`Async`クエリを`ToList`データベースに送信するメソッドであるため、メソッドのバージョンがあります。 `Where`メソッドと`OrderByDescending`メソッドはクエリのみを構成し、`ToListAsync`メソッドはクエリを実行し、応答を変数`result`に格納します。

## <a name="summary"></a>まとめ

ここで説明する Web 開発のベスト プラクティスは、任意の Web プログラミング フレームワークとクラウド環境で実装できますが、ASP.NETと Windows Azure には簡単に使用できるツールがあります。 これらのパターンに従えば、Web 層を簡単にスケールアウトでき、各サーバーがより多くのトラフィックを処理できるため、経費を最小限に抑えることができます。

[次の章](single-sign-on.md)では、クラウドでシングル サインオンのシナリオがどのように有効にされるかを説明します。

## <a name="resources"></a>リソース

詳細については、以下のリソースを参照してください。

ステートレス Web サーバー:

- [マイクロソフトのパターンとプラクティス - 自動スケール ガイド](https://msdn.microsoft.com/library/dn589774.aspx):
- [Windows Azure Web サイトで ARR のインスタンス アフィニティを無効にする](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/)。 エレス・ベナリのブログ記事では、Windows Azure Web サイトのセッション アフィニティについて説明します。

Cdn：

- [フェイルセーフ: スケーラブルで回復力のあるクラウド サービスの構築](https://channel9.msdn.com/Series/FailSafe) ウルリッヒ・ホーマン、マルク・メルクリ、マーク・シムズによる9部構成のビデオシリーズ。 エピソード 3 の CDN ディスカッションを 1:34:00 から始めるをご覧ください。
- [Microsoft のパターンとプラクティス静的コンテンツ ホスティング パターン](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN レビュー](http://www.cdnreviews.com/). 多くの CDN の概要。

非同期プログラミング:

- [mvc 4 での非同期メソッドASP.NET使用](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)します。 リック・アンダーソンによるチュートリアル。
- [非同期と Await を使用した非同期プログラミング (C# および Visual Basic)。](https://msdn.microsoft.com/library/vstudio/hh191443.aspx) 非同期プログラミングの根拠、ASP.NET 4.5 での動作、および実装するコードの記述方法を説明する MSDN ホワイト ペーパー。
- [エンティティ フレームワークの非同期クエリと保存](https://msdn.microsoft.com/data/jj819165)
- [非同期を使用してASP.NET Web アプリケーションをビルドする方法](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7). ローワン・ミラーによるビデオプレゼンテーション。 高負荷条件下での Web サーバースループットの劇的な向上を非同期プログラミングによってどのように促進できるかを示すグラフィックデモを示します。
- [フェイルセーフ: スケーラブルで回復力のあるクラウド サービスの構築](https://channel9.msdn.com/Series/FailSafe) ウルリッヒ・ホーマン、マルク・メルクリ、マーク・シムズによる9部構成のビデオシリーズ。 非同期プログラミングがスケーラビリティに与える影響については、エピソード 4 とエピソード 8 を参照してください。
- [ASP.NET 4.5 で非同期メソッドを使用する魔法と重要なゴッチャ](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx). Scott Hanselman によるブログ投稿、 主に web フォーム アプリケーションでの非同期の使用に関ASP.NET。

Web 開発のその他のベスト プラクティスについては、次のリソースを参照してください。

- [Fix it サンプル アプリケーション - ベスト プラクティス](the-fix-it-sample-application.md#bestpractices). この電子書籍の付録には、Fix It アプリケーションで実装された多くのベスト プラクティスが記載されています。
- [ウェブ開発者チェックリスト](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [前へ](continuous-integration-and-continuous-delivery.md)
> [次へ](single-sign-on.md)
