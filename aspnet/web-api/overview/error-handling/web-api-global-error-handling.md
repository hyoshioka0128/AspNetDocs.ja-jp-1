---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: Web API 2 ASP.NETグローバルエラー処理 - ASP.NET 4.x
author: davidmatson
description: ASP.NET 4.x の Web API 2 でのグローバル エラー処理ASP.NET概要。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 5ff54d2e4ed881ce927d0a401fb79d9b8bc5b8a1
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675426"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>Web API 2 におけるグローバルエラー処理ASP.NET

[デビッド・マットソン](https://github.com/davidmatson),[リック・アンダーソン](https://twitter.com/RickAndMSFT)

このトピックでは、ASP.NET 4.x の Web API 2 でのグローバルASP.NETエラー処理の概要を示します。 今日、Web API では、エラーをグローバルにログに記録または処理する簡単な方法はありません。 一部の未処理の例外は[例外フィルター](exception-handling.md)を使用して処理できますが、例外フィルターでは処理できない場合が多くあります。 次に例を示します。

1. コントローラー コンストラクターからスローされる例外。
2. メッセージ ハンドラーからスローされる例外。
3. ルーティング中にスローされる例外。
4. 応答コンテンツのシリアル化中にスローされる例外。

これらの例外を(可能な場合は)ログに記録し、処理するための簡単で一貫した方法を提供したいと考えています。 

例外を処理する場合は、エラー応答を送信できるケースと、例外をログに記録するケースが 2 つあります。 後者のケースの例は、応答のストリーミング コンテンツの途中で例外がスローされる場合です。その場合、ステータスコード、ヘッダー、および部分コンテンツがすでにネットワークを越えて行っているので、新しい応答メッセージを送信するには遅すぎるので、接続を中止するだけです。 例外を処理して新しい応答メッセージを生成することはできませんが、例外のログ記録はサポートされています。 エラーを検出できる場合は、次に示すように適切なエラー応答を返すことができます。

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>既存のオプション

[例外フィルター](exception-handling.md)に加えて、[メッセージ ハンドラー](../advanced/http-message-handlers.md)を使用して、500 レベルの応答をすべて監視できますが、元のエラーに関するコンテキストがないため、これらの応答に対する動作は困難です。 メッセージ ハンドラーには、処理できるケースに関する例外フィルターと同じ制限がいくつかあります。 Web API にはエラー状態をキャプチャするトレース インフラストラクチャがありますが、トレース インフラストラクチャは診断用であり、運用環境での実行には適していません。 グローバル例外処理とロギングは、本番稼働中に実行でき、既存の監視ソリューション[(ELMAH](https://code.google.com/p/elmah/)など) に接続できるサービスである必要があります。

### <a name="solution-overview"></a>ソリューションの概要

 処理されない例外をログに記録して処理する 2 つの新しいユーザー置換可能サービス[、IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md)と IExceptionHandler を提供します。 サービスは非常に似ていますが、2 つの大きな違いがあります。

1. 複数の例外ロガーの登録はサポートしていますが、1 つの例外ハンドラのみを使用できます。
2. 接続を中止しようとしている場合でも、例外ロガーは常に呼び出されます。 例外ハンドラは、送信する応答メッセージを選択できる場合にのみ呼び出されます。

どちらのサービスも、例外が検出されたポイントからの関連情報を含む例外コンテキストへのアクセスを提供します[HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx)。 [HttpRequestContext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx)

### <a name="design-principles"></a>設計原則

1. **壊れた変更はありません**この機能はマイナー リリースで追加されるため、ソリューションに影響を与える重要な制約の 1 つは、型コントラクトまたは動作に対する変更が発生しないということです。 この制約は、既存の catch ブロックが例外を 500 応答に変えるという点で、実行したいクリーンアップを除外しました。 この追加のクリーンアップは、今後のメジャー リリースで考慮する必要があります。 これが重要な場合は[、Web API ユーザーの声ASP.NET](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)で投票してください。
2. **Web API コンストラクトとの整合性の維持**Web API のフィルター パイプラインは、アクション固有、コントローラー固有、またはグローバル スコープでロジックを柔軟に適用することで、横断的な問題に対処する優れた方法です。 例外フィルターを含むフィルターは、グローバル スコープで登録されている場合でも、常にアクションとコントローラーコンテキストを持ちます。 このコントラクトはフィルターに適していますが、例外フィルターは、グローバルスコープのフィルターであっても、アクションやコントローラー コンテキストが存在しないメッセージ ハンドラーからの例外など、一部の例外処理のケースに適していないことを意味します。 例外処理にフィルターによって提供される柔軟なスコープを使用する場合は、例外フィルターが必要です。 しかし、コントローラコンテキストの外部で例外を処理する必要がある場合は、完全なグローバルエラー処理(コントローラコンテキストとアクションコンテキスト制約のないもの)のための別の構造も必要です。

### <a name="when-to-use"></a>使用する場合

- 例外ロガーは、Web API によってキャッチされたすべての未処理の例外を見るためのソリューションです。
- 例外ハンドラーは、Web API によってキャッチされた未処理の例外に対するすべての可能な応答をカスタマイズするためのソリューションです。
- 例外フィルターは、特定のアクションまたはコントローラーに関連するサブセットの未処理の例外を処理するための最も簡単なソリューションです。

### <a name="service-details"></a>サービスの詳細

 例外ロガーおよびハンドラー サービス インターフェイスは、それぞれのコンテキストを取る単純な非同期メソッドです。 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 また、これらのインターフェイスの両方に基本クラスを提供します。 コア (同期または非同期) メソッドをオーバーライドするのは、推奨時間にログまたは処理するために必要なすべてです。 ロギングの場合、`ExceptionLogger`基本クラスは、コア ロギング メソッドが各例外に対して 1 回だけ呼び出されるようにします (後で呼び出し履歴をさらに上に伝播し、再びキャッチされた場合でも)。 基本`ExceptionHandler`クラスは、呼び出し履歴の先頭にある例外に対してのみコア処理メソッドを呼び出し、入れ子になった従来の catch ブロックを無視します。 (これらの基本クラスの簡略化されたバージョンは、以下の付録に記載されています)。の`IExceptionLogger`両方`IExceptionHandler`とを使用して例外に関`ExceptionContext`する情報を受信します。

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

フレームワークが例外ロガーまたは例外ハンドラを呼び出すとき、それは常に`Exception`と`Request`を提供します。 単体テストを除き、常に`RequestContext`. これはめったに提供`ControllerContext`されません`ActionContext`(例外フィルターの catch ブロックから呼び出す場合のみ)。 (応答を`Response`書こうとしている場合に特定の IIS の場合にのみ) を提供することはほとんどありません。 これらのプロパティの一部は、例外クラス`null`のメンバーにアクセスする`null`前にチェックする必要があります。`CatchBlock` は、どの catch ブロックが例外を検出したかを示す文字列です。 catch ブロック文字列は次のとおりです。

- を使用します。
- メソッドを送信します。
- をクリックします。
- IException フィルター (ApiController の ExecuteAsync の例外フィルター パイプラインの処理)
- OWIN ホスト:

    - 出力をバッファリングするための非同期
    - 出力をストリーミングするための同期
- Web ホスト:

    - 出力をバッファリングするための非同期
    - 出力をストリーミングするための非同期
    - エラー回復のエラーがバッファー出力モードで発生した場合の非同期

catch ブロック文字列のリストは、静的読み取り専用プロパティを使用して使用することもできます。 (コア キャッチ ブロック文字列は静的 ExceptionCatchBlocks にあり、残りは OWIN と Web ホストのそれぞれに 1 つの静的クラスに表示されます)。`IsTopLevelCatchBlock` は、呼び出し履歴の先頭でのみ例外を処理する推奨パターンに従う場合に役立ちます。 入れ子になった catch ブロックが発生した場合に例外を 500 個の応答に変換するのではなく、例外ハンドラーを使用すると、ホストに見えるまで例外を伝達できます。

に加えて`ExceptionContext`、ロガーは完全`ExceptionLoggerContext`なを介して情報の一部を取得します。

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

2 番目の`CanBeHandled`プロパティは、logger が処理できない例外を識別できるようにします。 接続が中断され、新しい応答メッセージを送信できない場合、ロガーは呼び出されますが、ハンドラーは呼び出***されず***、ロガーはこのプロパティからこのシナリオを識別できます。

に追加して`ExceptionContext`、ハンドラーは、例外を処理するために完全`ExceptionHandlerContext`に設定できる 1 つのプロパティを取得します。

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

例外ハンドラーは、`Result`プロパティをアクションの結果 (たとえば、例外結果[、InternalServerErrorResult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx)、[ステータスコード結果](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)、またはカスタム結果) に設定することによって例外を処理したことを示します。 [ExceptionResult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx) プロパティが`Result`null の場合、例外は処理されず、元の例外が再スローされます。

呼び出し履歴の先頭にある例外については、API 呼び出し元に対して応答が適切であることを確認するための追加の手順を実行しました。 例外がホストに伝達される場合、呼び出し元は、通常は HTML であり、通常は適切な API エラー応答ではない、死の黄色の画面または他のホスト提供応答を参照してください。 このような場合、Result は null 以外から開始され、カスタム例外ハンドラーが明示的に (ハンドルされない)`null`に戻す場合にのみ、例外がホストに伝播されます。 このような`Result`場合`null`ににに設定すると、2 つのシナリオで役立ちます。

1. OWIN は、Web API の前または外部に登録されたミドルウェアを処理するカスタム例外を使用して、Web API をホストしました。
2. ブラウザーを介したローカル デバッグでは、実際には、未処理の例外に対する有用な応答である、死の黄色の画面です。

例外ロガーと例外ハンドラーの両方について、ロガーまたはハンドラー自体が例外をスローした場合に回復する処理は何もしません。 (例外を伝播させる以外に、より良い方法を使用する場合は、このページの下部にフィードバックを残します。例外ロガーとハンドラーのコントラクトは、例外を呼び出し元に伝達させないようにする必要があります。それ以外の場合、例外は単に伝播し、多くの場合、ホストに対して HTML エラー (ASP など) が発生します。NET の黄色い画面) はクライアントに送り返されます (通常、JSON または XML を想定する API 呼び出し元の推奨オプションではありません)。

## <a name="examples"></a>例

### <a name="tracing-exception-logger"></a>トレース例外ロガー

以下の例外ロガーは、構成済みのトレース ソース (Visual Studio のデバッグ出力ウィンドウを含む) に例外データを送信します。

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>カスタム エラー メッセージ例外ハンドラ

以下の例外ハンドラは、サポートに問い合わせるための電子メールアドレスを含む、クライアントにカスタムエラー応答を生成します。

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>例外フィルターの登録

プロジェクトを作成するために「mvc 4 Web アプリケーションASP.NET」プロジェクト テンプレートを使用する場合は、`WebApiConfig`クラス内の web API 構成コードを*App_Start*フォルダーに配置します。

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>付録: 基本クラスの詳細

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
