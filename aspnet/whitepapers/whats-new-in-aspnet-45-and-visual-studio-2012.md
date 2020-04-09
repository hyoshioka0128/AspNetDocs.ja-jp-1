---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 および Visual Studio 2012 の新機能 |マイクロソフトドキュメント
author: rick-anderson
description: このドキュメントでは、ASP.NET 4.5 で導入されている新機能と拡張機能について説明します。 また、Web 開発の改善についても説明しています。
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675887"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>ASP.NET 4.5 と Visual Studio 2012 の新機能

> このドキュメントでは、ASP.NET 4.5 で導入されている新機能と拡張機能について説明します。 また、Visual Studio 2012 での Web 開発の改善についても説明します。 この文書は2012年2月29日に公開されました。

- [ASP.NETコア ランタイムとフレームワーク](#_Toc318097372)

    - [HTTP 要求と応答の非同期読み取りと書き込み](#_Toc318097373)
    - [HttpRequest 処理の機能強化](#_Toc318097374)
    - [非同期的に応答をフラッシュする](#_Toc318097375)
    - [*await*および*タスク*ベースの非同期モジュールおよびハンドラーのサポート](#_Toc318097376)
    - [非同期 HTTP モジュール](#_Toc318097377)
    - [非同期 HTTP ハンドラー](#_Toc318097378)
    - [新しいASP.NET要求検証機能](#_Toc318097379)
    - [遅延 (「遅延」) 要求の検証](#_Toc318097380)
    - [未検証要求のサポート](#_Toc318097381)
    - [アンチXSSライブラリ](#_Toc318097382)
    - [Web ソケット プロトコルのサポート](#_Toc318097383)
    - [バンドルとミンフィケーション](#_Toc318097384)
    - [Web ホスティングのパフォーマンス向上](#_Toc_perf)

        - [主要なパフォーマンス要因](#_Toc_perf_1)
        - [新しいパフォーマンス機能の要件](#_Toc_perf_2)
        - [共通アセンブリの共有](#_Toc_perf_3)
        - [マルチコア JIT コンパイルを使用して、高速なスタートアップを実現](#_Toc_perf_4)
        - [メモリ用に最適化するためのガベージ コレクションのチューニング](#_Toc_perf_5)
        - [Web アプリケーションのプリフェッチ](#_Toc_perf_6)
- [ASP.NET Web Forms](#_Toc318097385)

    - [厳密に型指定されたデータ コントロール](#_Toc318097386)
    - [モデル バインド](#_Toc318097387)

        - [データの選択](#_Toc318097388)
        - [値プロバイダー](#_Toc318097389)
        - [コントロールの値によるフィルター処理](#_Toc318097390)
    - [HTML エンコードされたデータ バインディング式](#_Toc318097391)
    - [控えめな検証](#_Toc318097392)
    - [HTML5 の更新プログラム](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET Web ページ 2](#_Toc318097395)
- [ビジュアル スタジオ 2012 リリース候補](#_Toc318097396)

    - [Visual Studio 2010 と Visual Studio 2012 リリース候補との間のプロジェクト共有 (プロジェクトの互換性)](#project-compatibility)
    - [ASP.NET 4.5 Web サイト テンプレートの設定変更](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [IIS 7 でのASP.NET ルーティングのネイティブ サポート](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML エディター](#_Toc318097397)

        - [スマートタスク](#_Toc318097398)
        - [ワイアリアサポート](#_Toc318097399)
        - [新しい HTML5 スニペット](#_Toc318097400)
        - [ユーザー コントロールに抽出する](#_Toc318097401)
        - [属性内のコード ナゲットの IntelliSense](#_Toc318097402)
        - [開始タグまたは終了タグの名前を変更すると、一致するタグの名前が自動的に変更される](#_Toc318097403)
        - [イベント ハンドラの生成](#_Toc318097404)
        - [スマートインデント](#_Toc318097405)
        - [ステートメントの自動削減入力](#_Toc318097406)
    - [スクリプトエディタ](#_Toc318097407)

        - [コードのアウトライン](#_Toc318097408)
        - [ブレースのマッチング](#_Toc318097409)
        - [定義へ移動](#_Toc318097410)
        - [ECMAスクリプト5サポート](#_Toc318097411)
        - [ドム インテライセンス](#_Toc318097412)
        - [VSDOC シグネチャのオーバーロード](#_Toc318097413)
        - [暗黙的な参照](#_Toc318097414)
    - [CSS エディター](#_Toc318097415)

        - [ステートメントの自動削減入力](#_Toc318097416)
        - [階層インデント。](#_Toc318097417)
        - [CSS ハックのサポート](#_Toc318097418)
        - [ベンダー固有のスキーマ (-moz -,-Webkit)](#_Toc318097419)
        - [コメントとコメント解除のサポート](#_Toc318097420)
        - [Color picker](#_Toc318097421)
        - [スニペット](#_Toc318097422)
        - [カスタム領域](#_Toc318097423)
    - [Page Inspector](#_Toc318097424)
    - [置換](#_Toc318097425)

        - [発行プロファイル](#_Toc318097426)
        - [プリコンパイルとマージのASP.NET](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [免責 事項](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NETコア ランタイムとフレームワーク

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>HTTP 要求と応答の非同期読み取りと書き込み

ASP.NET 4 では、HTTP 要求エンティティをストリームとして読み取る*機能が導入*されました。 このメソッドは、要求エンティティへのストリーミング アクセスを提供します。 しかし、同期的に実行され、要求の間スレッドが縛られます。

ASP.NET 4.5 では、HTTP 要求エンティティでストリームを非同期に読み取る機能と、非同期的にフラッシュする機能がサポートされています。 ASP.NET 4.5 では、HTTP 要求エンティティをダブル バッファーする機能も提供し、.aspx ページ ハンドラーや ASP.NET MVC コントローラーなどのダウンストリーム HTTP ハンドラーとの統合が容易になります。

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>HttpRequest 処理の機能強化

*httpRequest.GetBufferlessInputStream*から ASP.NET 4.5 から返されるストリーム参照は、同期および非同期の読み取りメソッドの両方をサポートしています。 *GetBufferlessInputStream*から返される*ストリーム*オブジェクトは、BeginRead メソッドと EndRead メソッドの両方を実装するようになりました。 非同期*Stream*メソッドを使用すると、要求エンティティをチャンク単位で非同期に読み取り、ASP.NETは非同期読み取りループの各反復の間に現在のスレッドを解放できます。

ASP.NET 4.5 は、バッファリングされた方法で要求エンティティを読み取るためのコンパニオン メソッドも追加*しました。* この新しいオーバーロードは、同期読み取りと非同期読み取りの両方をサポートする*GetBufferlessInputStream*のように機能します。 ただし、読み取り中に *、GetBufferedInputStream*は、ダウンストリームのモジュールとハンドラーが要求エンティティにアクセスできるように、エンティティのバイトをASP.NET内部バッファーにコピーします。 たとえば、パイプライン内の一部の上流コードが*GetBufferedInputStream*を使用して既に要求エンティティを読み取っている場合は *、HttpRequest.Form または HttpRequest.Files*を使用できます。 *HttpRequest.Files* これにより、要求に対して非同期処理を実行できます (たとえば、データベースへの大きなファイルアップロードのストリーミングなど) が、後で .aspx ページと MVC ASP.NET コントローラーを実行します。

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>非同期的に応答をフラッシュする

HTTP クライアントへの応答の送信は、クライアントが遠く離れているか、または帯域幅の低い接続を持つ場合にかなりの時間を要する場合があります。 通常、ASP.NETは、アプリケーションによって作成された応答バイトをバッファします。 ASP.NET、要求処理の最後の最後に、発生したバッファーの単一の送信操作を実行します。

バッファリングされた応答が大きい場合 (たとえば、大きなファイルをクライアントにストリーミングする場合)、定期的に*HttpResponse.Flush*を呼び出してバッファ出力をクライアントに送信し、メモリ使用量を制御する必要があります。 ただし *、Flush*は同期呼び出しであるため *、Flush*を繰り回し、実行時間が長い可能性がある要求の間はスレッドを消費します。

ASP.NET 4.5 では *、HttpResponse*クラスの*BeginFlush*メソッドと*EndFlush*メソッドを使用して、非同期的にフラッシュを実行するためのサポートが追加されています。 これらのメソッドを使用すると、オペレーティング システムスレッドを縛らずにクライアントにデータを増分的に送信する非同期モジュールと非同期ハンドラを作成できます。 *BeginFlush*と*EndFlush*呼び出しの間で、ASP.NETは現在のスレッドを解放します。 これにより、実行時間の長い HTTP ダウンロードをサポートするために必要なアクティブスレッドの総数が大幅に削減されます。

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>*await*および*Task*ベースの非同期モジュールとハンドラーのサポート

.NET Framework 4 では、タスクと呼ばれる非同期プログラミングの概念が導入*されました*。 タスクは、*タスク*の種類と関連する型によって表*System.Threading.Tasks*されます。 .NET Framework 4.5 は、この機能をベースに、*タスク*オブジェクトの操作を簡単にするコンパイラの機能強化を備えています。 .NET Framework 4.5 では、コンパイラは 2 つの新*await*しいキーワード*を*サポートしています。 *await*キーワードは、コードの一部が他のコードを非同期に待機する必要があることを示す構文の省略形です。 *async*キーワードは、メソッドをタスクベースの非同期メソッドとしてマークするために使用できるヒントを表します。

*await* *、async、* および*Task*オブジェクトを組み合わせると、.NET 4.5 で非同期コードを記述する方がはるかに簡単になります。 ASP.NET 4.5 では、新しいコンパイラ拡張機能を使用して非同期 HTTP モジュールと非同期 HTTP ハンドラーを記述できる新しい API でこれらの簡略化がサポートされています。

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>非同期 HTTP モジュール

*Task*オブジェクトを返すメソッド内で非同期処理を実行するとします。 Microsoft ホーム ページをダウンロードするための非同期呼び出しを行う非同期メソッドを定義するコード例を次に示します。 メソッド シグネチャと、メソッド シグネチャへの*async*キーワードの使用と *、呼*び出し*の待機*に注意してください。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

この方法は、ダウンロード完了の待機中に呼び出し履歴のアンワインドを自動的に処理し、ダウンロードが完了した後に呼び出し履歴を自動的に復元します。

ここで、この非同期メソッドを非同期 ASP.NET HTTP モジュールで使用するとします。 ASP.NET 4.5 には、ヘルパー メソッド (*EventHandlerTaskAsyncHelper*) と新しいデリゲート型 (*TaskEventHandler*) が含まれており、これを使用して、ASP.NET HTTP パイプラインによって公開された古い非同期プログラミング モデルとタスク ベースの非同期メソッドを統合できます。 この例は、次の方法を示しています。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>非同期 HTTP ハンドラー

ASP.NETで非同期ハンドラを記述する従来のアプローチは *、IHttpAsyncHandler*インターフェイスを実装することです。 ASP.NET 4.5 では、派生元の非同期基本型*HttpTaskAsyncHandler*が導入されており、非同期ハンドラーの記述が簡単になります。

型*は*抽象型であり、*メソッド*をオーバーライドする必要があります。 内部的にはASP.NETは *、ProcessRequestAsync*の戻り署名 *(Task*オブジェクト) と、ASP.NETパイプラインで使用される古い非同期プログラミング モデルを統合します。

次の例は、非同期 HTTP ハンドラーの実装の一部として*Task*および*await*を使用する方法を示しています。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>新しいASP.NET要求検証機能

既定では、ASP.NETは要求の検証を実行し、フィールド、ヘッダー、Cookie などのマークアップまたはスクリプトを検索する要求を調べます。 検出された場合、ASP.NETは例外をスローします。 これは、クロスサイト スクリプティング攻撃の可能性に対する防御の第 1 線として機能します。

ASP.NET 4.5 を使用すると、検証されていない要求データを選択して読み取りが容易になります。 ASP.NET4.5はまた、以前は外部ライブラリであった人気のAntiXSSライブラリを統合しています。

開発者は、アプリケーションの要求検証を選択的にオフにする機能を頻繁に求めています。 たとえば、アプリケーションがフォーラム ソフトウェアの場合、HTML 形式のフォーラムの投稿やコメントをユーザーに送信できるようにする一方で、要求の検証が他のすべてをチェックしていることを確認できます。

ASP.NET 4.5 では、検証されていない入力を簡単に処理できる 2 つの機能が導入されています。

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>遅延 (「遅延」) 要求の検証

ASP.NET 4.5 では、デフォルトですべての要求データは要求の検証の対象となります。 ただし、要求データに実際にアクセスするまで要求の検証を延期するようにアプリケーションを構成できます。 (これは、特定のデータ シナリオでの遅延読み込みなどの用語に基づいて、遅延要求の検証と呼ばれることもあります)。次の例のように *、httpRUntime*要素で*requestValidationMode*属性を 4.5 に設定することで、Web.config ファイルで遅延検証を使用するようにアプリケーションを構成できます。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

要求検証モードが 4.5 に設定されている場合、要求の検証は、特定の要求値に対してのみトリガーされ、コードがその値にアクセスした場合にのみトリガーされます。 たとえば、コードが Request.Form[フォーラム\_ポスト]の値を取得した場合、要求の検証はフォーム コレクション内のその要素に対してのみ呼び出されます。 *Form*コレクション内の他の要素は検証されません。 以前のバージョンのASP.NETでは、コレクション内のいずれかの要素にアクセスしたときに、要求コレクション全体に対して要求の検証がトリガーされていました。 新しい動作により、異なるアプリケーション コンポーネントが、他の部分で要求の検証をトリガーしなくても、異なる要求データを簡単に確認できます。

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>未検証要求のサポート

遅延要求検証だけでは、要求検証を選択的にバイパスするという問題は解決しません。 Request.Form[フォーラム\_ポスト]への呼び出しは、その特定の要求値に対する要求検証を引き起こします。 ただし、そのフィールドでマークアップを許可する必要があるため、検証をトリガーせずにこのフィールドにアクセスする場合があります。

これを可能にするために、ASP.NET 4.5 は、データを要求する未検証アクセスをサポートするようになりました。 ASP.NET 4.5 には *、HttpRequest*クラスに*新しい未検証*コレクション プロパティが含まれています。 このコレクションは、*フォーム*、*クエリ文字列*、*クッキー*、*および Url*などの要求データの一般的な値すべてにアクセスできます。

フォーラムの例を使用して、未検証の要求データを読み取ることができるように、まず、新しい要求検証モードを使用するようにアプリケーションを構成する必要があります。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

その後 *、HttpRequest.Unvalidated*プロパティを使用して、検証されていないフォームの値を読み取ることができます。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> セキュリティ -*検証されていない要求データを注意して使用してください!* ASP.NET 4.5 では、検証されていない要求のプロパティとコレクションが追加され、非常に特定の未検証の要求データに簡単にアクセスできるようになりました。 ただし、危険なテキストがユーザーにレンダリングされないように、未加工の要求データに対してカスタム検証を実行する必要があります。

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>アンチXSSライブラリ

Microsoft AntiXSS ライブラリの人気により、ASP.NET 4.5 には、そのライブラリのバージョン 4.0 のコア エンコーディング ルーチンが組み込まれています。

エンコーディング ルーチンは、新しい*名前空間*の*AntiXssEncoder*型によって実装されます。 型に実装されている任意の静的エンコーディング メソッドを呼び出すことによって *、AntiXssEncoder*型を直接使用できます。 ただし、新しい反 XSS ルーチンを使用する最も簡単な方法は、既定で*AntiXssEncoder*クラスを使用するようにASP.NET アプリケーションを構成することです。 これを行うには、Web.config ファイルに次の属性を追加します。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

*AntiXssEncoder*型を使用するように*encoderType*属性が設定されている場合、ASP.NETのすべての出力エンコーディングは自動的に新しいエンコーディング ルーチンを使用します。

これらは、ASP.NET 4.5 に組み込まれた外部 AntiXSS ライブラリの部分です。

- *をエンコード*する 、*フォームUrl エンコード*、および*属性エンコード*
- *エンコードと**エンコード*
- *Url エンコード*と*Url パスエンコード*(新しい)
- *エンコード*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>Web ソケット プロトコルのサポート

WebSockets プロトコルは、HTTP 経由でクライアントとサーバー間の安全なリアルタイム双方向通信を確立する方法を定義する標準ベースのネットワーク プロトコルです。 マイクロソフトは、IETF と W3C の両方の標準機関と協力して、プロトコルの定義に役立っています。 WebSockets プロトコルは、ブラウザーだけでなく、あらゆるクライアントでサポートされており、Microsoft はクライアントとモバイルオペレーティング システムの両方で WebSockets プロトコルをサポートする相当なリソースを投資しています。

WebSockets プロトコルを使用すると、クライアントとサーバー間で長時間実行されるデータ転送を作成することがはるかに容易になります。 たとえば、クライアントとサーバー間で実際の長時間接続を確立できるため、チャット アプリケーションの作成が非常に簡単になります。 ソケットの動作をシミュレートするために、定期ポーリングや HTTP ロングポーリングなどの回避策に頼る必要はありません。

ASP.NET 4.5 および IIS 8 には低レベルの WebSocket が含まれ、ASP.NET開発者は WebSockets オブジェクトで文字列データとバイナリ データの両方を非同期に読み書きするためにマネージ API を使用できます。 ASP.NET 4.5 の場合、WebSockets プロトコルを操作するための型を含む新しい*System.Web.WebSockets*名前空間があります。

ブラウザー クライアントは、次の例のように、ASP.NET アプリケーションの URL を指す DOM WebSocket オブジェクトを作成することによって *、WebSockets*接続を確立します。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

任意の種類のモジュールまたはハンドラーを使用して、ASP.NETで WebSockets エンドポイントを作成できます。 前の例では、.ashx ファイルはハンドラーを作成する簡単な方法であるため、.ashx ファイルが使用されました。

WebSockets プロトコルによると、ASP.NETアプリケーションは、要求を HTTP GET 要求から WebSockets 要求にアップグレードする必要があることを示すことによって、クライアントの WebSocket 要求を受け入れます。 次に例を示します。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

*AcceptWebSocketRequest*メソッドは、現在の HTTP 要求をアンウィンASP.NETし、関数デリゲートに制御を転送するため、関数デリゲートを受け入れます。 概念的には、このアプローチは、バックグラウンド作業を実行するスレッド開始デリゲートを定義する*System.Threading.Thread*の使用方法に似ています。

ASP.NETし、クライアントが WebSockets ハンドシェイクを正常に完了した後、ASP.NETはデリゲートを呼び出し、WebSockets アプリケーションの実行を開始します。 次のコード例は、ASP.NETでの組み込みの WebSocket サポートを使用する単純なエコー アプリケーションを示しています。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

*await*キーワードと非同期タスク ベースの操作に対する .NET 4.5 のサポートは、WebSockets アプリケーションを記述するのに自然に適しています。 このコード例は、WebSockets 要求がASP.NET内部で完全に非同期的に実行されることを示しています。 アプリケーションは、await ソケットを呼び出すことによって、クライアントからメッセージが送信されるのを非同期に待機*します。受信非同期*. 同様に、await ソケットを呼び出すことによって、非同期メッセージをクライアントに送信できます *。送信非同期*.

ブラウザーでは、アプリケーションは*onmessage*関数を介して WebSockets メッセージを受信します。 ブラウザーからメッセージを送信するには、次の例に示すように *、WebSocket* DOM 型の*送信*メソッドを呼び出します。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

今後、この機能の更新プログラムをリリースして、このリリースで必要な低レベルのコーディングの一部を WebSockets アプリケーション用に抽象化する可能性があります。

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>バンドルと縮小

バンドルを使用すると、個々の JavaScript ファイルと CSS ファイルを 1 つのファイルのように扱うことができるバンドルに結合できます。 縮小は、必要のない空白文字やその他の文字を削除することで、JavaScript ファイルと CSS ファイルを縮めます。 これらの機能は、Web フォーム、ASP.NET MVC、および Web ページで機能します。

バンドルは、バンドルクラスまたはその子クラスの 1 つである ScriptBundle とスタイルバンドルを使用して作成されます。 バンドルのインスタンスを設定した後、そのバンドルはグローバル BundleCollection インスタンスに追加するだけで、受信リクエストに対して使用できるようになります。 デフォルトテンプレートでは、バンドル構成は BundleConfig ファイルで実行されます。 このデフォルト設定では、テンプレートで使用されるすべてのコアスクリプトと CSS ファイルのバンドルが作成されます。

バンドルは、可能ないくつかのヘルパー メソッドのいずれかを使用してビュー内から参照されます。 デバッグモードとリリースモードの場合にバンドルに対して異なるマークアップをレンダリングするために、ScriptBundle クラスと StyleBundle クラスには、ヘルパー メソッド Render があります。 デバッグ モードの場合、Render はバンドル内の各リソースのマークアップを生成します。 リリース モードの場合、Render はバンドル全体に対して 1 つのマークアップ要素を生成します。 デバッグ モードとリリース モードの切り替えは、以下に示すように、web.config のコンパイル要素のデバッグ属性を変更することで実現できます。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

さらに、最適化の有効化または無効化は、バンドルテーブルを使用して直接設定できます。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

ファイルがバンドルされると、最初にアルファベット順に並べ替えられます (**ソリューション エクスプローラー**で表示される方法)。 次に、既知のライブラリとカスタム拡張 (jQuery、MooTools、Dojo など) が最初に読み込まれるように編成されます。 たとえば、上記のように Scripts フォルダのバンドルの最終順序は次のようになります。

1. jquery-1.6.2.js
2. jクエリ-ui.js
3. を使用します。
4. a.js

CSS ファイルもアルファベット順に並べ替えられ、その後、reset.css と normalize.css が他のファイルより先に来るように再編成されます。 上記のスタイルフォルダのバンドルの最終的なソートは次のようになります。

1. リセット.css
2. コンテンツ.css
3. の
4. グローバル.css
5. メニュー.css
6. スタイル.css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>Web ホスティングのパフォーマンス向上

.NET Framework 4.5 および Windows 8 では、Web サーバーのワークロードのパフォーマンスを大幅に向上させる機能が導入されています。 これには、削減(最大35%)が含まれます。起動時間と、ASP.NETを使用する Web ホスティング サイトのメモリフットプリントの両方で使用します。

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>主要なパフォーマンス要因

理想的には、すべてのウェブサイトは、それが来るたびに、次の要求に迅速な応答を保証するためにアクティブで、メモリ内にあるべきです。 サイトの応答性に影響する要因には、次のようなものがあります。

- アプリ プールのリサイクル後にサイトが再起動するまでの時間。 これは、サイト アセンブリがメモリに存在しなくなったときに、サイトの Web サーバー プロセスを起動するのにかかる時間です。 (プラットフォーム アセンブリは、他のサイトで使用されているため、メモリ内に残っています)。この状況は、"コールド サイト、ウォーム フレームワークスタートアップ" または単に "コールド サイトスタートアップ" と呼ばれます。
- サイトが占有するメモリの量。 この用語は、「サイトごとのメモリ消費量」または「共有されていないワーキング セット」です。

新しいパフォーマンスの向上は、これらの両方の要因に焦点を当てています。

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>新しいパフォーマンス機能の要件

新機能の要件は、次のカテゴリに分類できます。

- .NET Framework 4 で実行される機能強化。
- .NET Framework 4.5 が必要ですが、どのバージョンの Windows でも実行できる機能強化。
- Windows 8 で実行されている .NET Framework 4.5 でのみ使用できる機能強化。

パフォーマンスは、有効にできる改善のレベルごとに向上します。

.NET Framework 4.5 の一部の機能強化では、他のシナリオにも適用される、より広範なパフォーマンス機能を利用しています。

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>共通アセンブリの共有

**要件**: .NET フレームワーク 4 および Visual Studio 11 開発者プレビュー SDK

サーバー上の異なるサイトでは、多くの場合、同じヘルパー アセンブリ (たとえば、スタート キットやサンプル アプリケーションのアセンブリ) を使用します。 各サイトは、Bin ディレクトリにこれらのアセンブリの独自のコピーを持っています。 アセンブリのオブジェクト コードは同一ですが、アセンブリは物理的に分離されているため、コールド サイトの起動時に各アセンブリを個別に読み取り、メモリに個別に保持する必要があります。

新しいインターン機能により、この非効率性が解消され、RAM 要件と負荷時間の両方が削減されます。 インターン化により、Windows はファイル システム内の各アセンブリの 1 つのコピーを保持し、サイトの Bin フォルダ内の個々のアセンブリは、単一のコピーへのシンボリック リンクに置き換えられます。 個々のサイトに個別のバージョンのアセンブリが必要な場合、シンボリック リンクは新しいバージョンのアセンブリに置き換えられ、そのサイトだけが影響を受けます。

シンボリック リンクを使用してアセンブリを共有するには、aspnet\_intern.exe という名前の新しいツールが必要です。 これは、Visual Studio 11 開発者向けプレビュー SDK の一部として提供されています。 (ただし、最新の[更新プログラム](https://support.microsoft.com/kb/2468871)をインストールしている場合は、.NET Framework 4 のみがインストールされているシステムで動作します)。

対象となるすべてのアセンブリが確実にインターン化されるようにするには、aspnet\_intern.exe を定期的に実行します (たとえば、週に 1 回はスケジュールされたタスクとして実行します)。 一般的な用途は次のとおりです。

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

すべてのオプションを表示するには、引数を指定しないツールを実行します。

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>マルチコア JIT コンパイルを使用して、高速なスタートアップを実現

**要件**: .NET フレームワーク 4.5

コールド サイトのスタートアップの場合、アセンブリをディスクから読み取る必要があるだけでなく、サイトを JIT コンパイルする必要があります。 複雑なサイトでは、大幅な遅延が発生する可能性があります。 .NET Framework 4.5 の新しい汎用技術により、JIT コンパイルを利用可能なプロセッサ コアに分散させることで、これらの遅延を軽減できます。 これは、サイトの以前の起動時に収集された情報を使用して、できるだけ早くこれを行います。 [メソッドによって](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx)実装されるこの機能。

ASP.NETでは、複数のコアを使用した JIT コンパイルがデフォルトで有効になっているため、この機能を利用するために何もする必要はありません。 この機能を無効にする場合は、Web.config ファイルで次の設定を行います。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>メモリ用に最適化するためのガベージ コレクションのチューニング

**要件**: .NET フレームワーク 4.5

サイトが実行されると、ガベージ コレクター (GC) ヒープの使用は、そのメモリ消費の重要な要因になる可能性があります。 他のガベージ コレクタと同様に、.NET Framework GC は CPU 時間 (コレクションの頻度と重要度) とメモリ消費 (新しいオブジェクト、解放されたオブジェクト、または自由に使用できるオブジェクトに使用される領域の追加) との間のトレードオフを行います。 以前のリリースでは、適切なバランスを実現するために GC を構成する方法についてのガイダンスを提供してきました (たとえば[、2.0/3.5 共有ホスティング構成ASP.NET参照](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration))。

NET Framework 4.5 では、複数のスタンドアロン設定ではなく、ワークロードで定義された構成設定を使用して、以前に推奨されていたすべての GC 設定と、サイトごとの作業セットに対して追加のパフォーマンスを提供する新しいチューニングを有効にできます。

GC メモリチューニングを有効にするには、次の設定を Windows\Net\Framework\v4.0.30319\aspnet.config ファイルに追加します。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

(aspnet.config の変更に関する以前のガイダンスに慣れている場合は、この設定によって古い設定が置き換えられます。古い設定を削除する必要はありません。

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>Web アプリケーションのプリフェッチ

**要件**: Windows 8 で実行されている .NET フレームワーク 4.5

いくつかのリリースでは、Windows には[プリフェッチャー](http://en.wikipedia.org/wiki/Prefetcher)と呼ばれるテクノロジが組み込まれており、アプリケーションの起動にかかるディスク読み取りコストを削減できます。 コールド スタートアップは主にクライアント アプリケーションの問題であるため、このテクノロジはサーバーに不可欠なコンポーネントのみを含む Windows Server には含まれていません。 プリフェッチは、Windows Server の最新バージョンで利用可能になり、個々の Web サイトの起動を最適化できます。

Windows サーバーの場合、プリフェッチャーはデフォルトでは有効になっていません。 高密度 Web ホスティング用のプリフェッチャーを有効にして構成するには、コマンド・ラインで以下のコマンド・セットを実行します。

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

次に、プリフェッチャーをASP.NETアプリケーションと統合するには、次のコードを Web.config ファイルに追加します。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>厳密に型指定されたデータ コントロール

ASP.NET 4.5 では、Web フォームにはデータを操作するためのいくつかの機能強化が含まれています。 最初の改善点は、厳密に型指定されたデータ コントロールです。 以前のバージョンのASP.NETの Web フォーム コントロールの場合は *、Eval*とデータ 連結式を使用して、データ バインド値を表示します。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

双方向のデータ バインディングの場合は *、Bind*を使用します。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

実行時に、これらの呼び出しは、リフレクションを使用して、指定されたメンバーの値を読み取り、その結果をマークアップに表示します。 この方法により、任意の未定データに対するデータバインドが容易になります。

ただし、このようなデータバインディング式は、メンバー名の IntelliSense、ナビゲーション (定義へ移動など)、コンパイル時のこれらの名前のチェックなどの機能をサポートしていません。

この問題に対処するために、ASP.NET 4.5 では、コントロールがバインドされているデータのデータ型を宣言する機能が追加されています。 これは、新しい*ItemType*プロパティを使用して行います。 このプロパティを設定すると、データ バインディング式のスコープで 2 つの新しい型指定された変数を使用できます: *Item*と*BindItem*。 変数は厳密に型指定されているため、Visual Studio の開発エクスペリエンスの利点を最大限に活用できます。

双方向のデータ 連結式の場合は *、BindItem*変数を使用します。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

データ バインディングをサポートする ASP.NET Web フォーム フレームワークのほとんどのコントロールは *、ItemType*プロパティをサポートするように更新されました。

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>モデル バインド

モデル バインドは、Web フォーム コントロールASP.NETのデータ バインディングを拡張して、コードに焦点を当てたデータ アクセスを操作します。 このメソッドには *、ObjectDataSource*コントロールとモデル バインドの概念ASP.NET MVC に組み込まれています。

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>データの選択

モデル バインドを使用してデータを選択するようにデータ コントロールを構成するには、コントロールの*SelectMethod*プロパティをページのコード内のメソッドの名前に設定します。 データ コントロールは、ページのライフ サイクルで適切なタイミングでメソッドを呼び出し、返されたデータを自動的にバインドします。 明示的に呼び出す必要はありません、 *DataBind*メソッドです。

次の例では *、GetCategories*という名前のメソッドを使用するように*GridView*コントロールが構成されています。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

GetCategories*GetCategories*メソッドは、ページのコードで作成します。 単純な選択操作の場合、メソッドはパラメーターを必要としないし *、IEnumerable*または*IQueryable*オブジェクトを返す必要があります。 新しい*ItemType*プロパティが設定されている場合[(厳密に](#_Toc318097386)型指定されたデータ 連結式を有効にする)、これらのインターフェイスのジェネリック バージョン ( *IEnumerable&lt;&gt; T*または*IQueryable&lt;T&gt;*) が返され *、ItemType*プロパティの型に一致する*T*パラメーター (たとえば *、IQueryable&lt;Category)&gt;* が返されます。

次の例は *、GetCategories*メソッドのコードを示しています。 この例では、Northwind サンプル データベースでエンティティ フレームワーク コードファースト モデルを使用します。 このコードは、クエリが*Include*メソッドを使用して各カテゴリの関連製品の詳細を返すようになります。 (これにより、マークアップの*TemplateField*要素は[、n+1 を選択](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)しなくても、各カテゴリの製品の数を表示します。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

ページが実行されると *、GridView*コントロールは*GetCategories*メソッドを自動的に呼び出し、構成されたフィールドを使用して返されたデータを表示します。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

select メソッドは*IQueryable*オブジェクトを返すため *、GridView*コントロールはクエリを実行する前に、さらに操作できます。 たとえば *、GridView*コントロールは、並べ替えとページングのクエリ式を実行する前に返された*IQueryable*オブジェクトに追加できるため、これらの操作は基になる LINQ プロバイダーによって実行されます。 この場合、Entity Framework は、これらの操作がデータベースで実行されることを確認します。

並べ替えとページングを許可するように変更された*GridView*コントロールの例を次に示します。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

これで、ページが実行されると、コントロールは、データの現在のページのみが表示され、選択した列の順序が設定されていることを確認できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

返されたデータをフィルター処理するには、select メソッドにパラメーターを追加する必要があります。 これらのパラメーターは、実行時にモデル バインドによって設定され、データを返す前にクエリを変更するために使用できます。

たとえば、クエリ文字列にキーワードを入力して、ユーザーが商品をフィルター処理できるようにするとします。 メソッドにパラメーターを追加し、パラメーター値を使用するようにコードを更新できます。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

このコードには、*キーワード*に値が指定されている場合に*Where*式が含まれ、クエリ結果が返されます。

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>値プロバイダー

前の例は *、キーワード*パラメーターの値がどこから来ているかについては具体的ではありませんでした。 この情報を示すために、パラメーター属性を使用できます。 この例では *、名前空間**にあるクラスを*使用できます。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

これは、実行時にクエリ文字列から*キーワード*パラメーターに値をバインドしようとするモデル バインドを指示します。 (この場合は型変換を実行する必要がありますが、この場合は行いません)。値を指定できず、型が null 非許容型の場合は、例外がスローされます。

これらのメソッドの値のソースは値プロバイダーと呼ばれ、使用する値プロバイダーを示すパラメーター属性は値プロバイダー属性と呼ばれます。 Web フォームには、クエリ文字列、Cookie、フォーム値、コントロール、ビューステート、セッション状態、プロファイル プロパティなど、Web フォーム アプリケーションにおける一般的なユーザー入力ソースの値プロバイダと対応する属性が含まれます。 カスタム値プロバイダーを作成することもできます。

既定では、パラメーター名は値プロバイダー コレクション内の値を検索するキーとして使用されます。 この例では、コードはキーワードという名前のクエリ文字列値を検索します (例: ~/default.aspx?キーワード=chef)。 カスタム キーを引数としてパラメーター属性に渡すことによって、カスタム キーを指定できます。 たとえば、q という名前のクエリ文字列変数の値を使用するには、次のようにします。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

このメソッドがページのコード内にある場合、ユーザーはクエリ文字列を使用してキーワードを渡すことによって結果をフィルター処理できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

モデル バインドでは、値の読み取り、null 値のチェック、適切な型への変換、変換が成功したかどうかの確認、およびクエリ内の値の使用など、手作業でコーディングする必要がある多くのタスクが実行されます。 モデル バインドの結果、コードが非常に少なくなり、アプリケーション全体で機能を再利用できます。

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>コントロールの値によるフィルター処理

例を拡張して、ユーザーがドロップダウン リストからフィルター値を選択できるようにするとします。 次のドロップダウン リストをマークアップに追加し *、SelectMethod*プロパティを使用して別のメソッドからデータを取得するように構成します。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

通常は、一致する製品が見つからない場合にコントロールにメッセージを表示するように *、GridView*コントロールに*空のデータ テンプレート*要素も追加します。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

ページ コードで、ドロップダウン リストの新しい select メソッドを追加します。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

最後に *、GetProducts*の選択メソッドを更新して、ドロップダウン リストから選択したカテゴリの ID を含む新しいパラメーターを取得します。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

ページが実行されると、ユーザーはドロップダウン リストからカテゴリを選択でき *、GridView*コントロールは自動的に再バインドされ、フィルター処理されたデータが表示されます。 モデル バインドは、選択メソッドのパラメーターの値を追跡し、ポストバック後にパラメーター値が変更されたかどうかを検出するためです。 その場合、モデル バインドは、関連付けられたデータ コントロールを強制的にデータにバインドします。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML エンコードされたデータ バインディング式

データ 連結式の結果を HTML エンコードできるようになりました。 コロンを追加する (:)データ バインディング式を&lt;マークする %# プレフィックスの末尾に次の値を指定します。

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>控えめな検証

クライアント側の検証ロジックに控えめな JavaScript を使用するように、組み込みの検証コントロールを構成できるようになりました。 これにより、ページ マークアップでインライン表示される JavaScript の量が大幅に減少し、ページ全体のサイズが小さくなります。 バリデータ コントロールの控えめな JavaScript を構成するには、次のいずれかの方法があります。

- Web.config ファイルの*&lt;appSettings&gt;* 要素に次の設定を追加してグローバルに実行します。 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- 静的な*System.Web.UI.ValidationSettings.UnobsiveValidationMode*プロパティを*控えめな検証モードに*設定することでグローバルに (通常、Global.asax ファイルの*アプリケーション\_開始*メソッドで)。
- *ページ*クラスの新しい*UnobtrusiveValidationMode*プロパティを *[控えめな検証モード]* に設定してページを個別に指定します。

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5 の更新プログラム

HTML5 の新機能を利用するために、Web フォーム サーバー コントロールに対していくつかの改良が加えられた。

- *TextBox*コントロールの*TextMode*プロパティは、*電子メール*、*日時*などの新しい HTML5 入力タイプをサポートするように更新されました。
- *FileUpload*コントロールは、この HTML5 機能をサポートするブラウザーからの複数のファイルアップロードをサポートするようになりました。
- 検証コントロールで HTML5 入力要素の検証がサポートされるようになりました。
- URL を表す属性を持つ新しい HTML5 要素は、runat="サーバー" をサポートするようになりました。 その結果、アプリケーションルートを表す ~ 演算子のように、URL パスでASP.NET規約を使用できます (たとえば、&lt;ビデオ runat="サーバー" src="~/myVideo.wmv" /&gt;)。
- *UPDATEPanel*コントロールは、HTML5 入力フィールドの投稿をサポートするように修正されました。

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 ベータ版は、Visual Studio 11 ベータ版に含まれるようになりました。 ASP.NETMVCは、モデル ビュー コントローラー (MVC) パターンを活用して、高度にテスト可能で保守が容易な Web アプリケーションを開発するためのフレームワークです。 ASP.NET MVC 4 では、モバイル Web 用のアプリケーションを簡単に構築でき、任意のデバイスにアクセスできる HTTP サービスを構築するのに役立つ ASP.NET Web API が含まれています。 詳細については、「 mvc [4 リリース ノートASP.NET](mvc4-release-notes.md)」を参照してください。

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET Web ページ 2

新機能には、次のようなものがあります。

- 新しいサイト テンプレートと更新されたサイト テンプレート。
- 検証ヘルパーを使用してサーバー側およびクライアント側の*検証*を追加します。
- アセットマネージャーを使用してスクリプトを登録する機能。
- OAuth と OpenID を使用して、Facebook やその他のサイトからのログインを有効にします。
- マップ ヘルパーを使用して*マップ*を追加します。
- Web ページ アプリケーションを並べて実行する。
- モバイル デバイス用のページのレンダリング。

これらの機能と全ページのコード例の詳細については、「 [Web ページ 2 のトップ機能 」](https://go.microsoft.com/fwlink/?LinkID=227824)を参照してください。

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>ビジュアルウェブ開発者 11 ベータ版

このセクションでは、Web 開発の改善について説明します 11 ベータ版と Visual Studio 2012 リリース候補の Web 開発します。

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Visual Studio 2010 と Visual Studio 2012 リリース候補との間のプロジェクト共有 (プロジェクトの互換性)

Visual Studio 2012 リリース候補まで、Visual Studio の新しいバージョンで既存のプロジェクトを開くと、変換ウィザードが起動しました。 これにより、プロジェクトのコンテンツ (資産) とソリューションを、下位互換性のない新しい形式にアップグレードする必要がありました。 したがって、変換後は、Visual Studio の古いバージョンでプロジェクトを開くことができなかった。

多くのお客様は、これが正しいアプローチではないと私たちに言いました。 Visual Studio 11 ベータ版では、Visual Studio 2010 SP1 を使用したプロジェクトとソリューションの共有をサポートするようになりました。 つまり、Visual Studio 2012 リリース候補で 2010 プロジェクトを開く場合でも、Visual Studio 2010 SP1 でプロジェクトを開くことができることを意味します。

> [!NOTE]
> いくつかの種類のプロジェクトは、Visual Studio 2010 SP1 と Visual Studio 2012 リリース候補の間で共有することはできません。 これには、古いプロジェクト (MVC 2 ASP.NET プロジェクトなど) や特別な目的 (セットアップ プロジェクトなど) 用のプロジェクトが含まれます。

Visual Studio 11 ベータ版で初めて Visual Studio 2010 SP1 Web プロジェクトを開くと、次のプロパティがプロジェクト ファイルに追加されます。

- ファイルアップグレードフラグ
- アップグレードバックアップロケーション
- オールドツールバージョン
- VisualStudioVersion
- ツールパス

プロジェクト ファイルをアップグレードするプロセスでは、アップグレードフラグ、アップグレードバックアップロケーション、およびオールドツールバージョンが使用されます。 Visual Studio 2010 でのプロジェクトの操作に影響はありません。

現在のプロジェクトの Visual Studio のバージョンを示す MSBuild 4.5 で使用される新しいプロパティです。 このプロパティは MSBuild 4.0 (Visual Studio 2010 SP1 で使用される MSBuild のバージョン) には存在しないため、プロジェクト ファイルに既定値を挿入します。

プロパティは、MSBuildExtensionsPath32 設定で表されるパスからインポートする正しい .targets ファイルを決定するために使用されます。

また、インポート要素に関連するいくつかの変更もあります。 これらの変更は、Visual Studio の両方のバージョン間の互換性をサポートするために必要です。

> [!NOTE]
> プロジェクトが 2 つの異なるコンピューターで Visual Studio 2010 SP1 と Visual Studio 11 Beta の間で\_共有されている場合、およびプロジェクトにアプリケーション データ フォルダーにローカル データベースが含まれている場合は、データベースで使用される SQL Server のバージョンが両方のコンピューターにインストールされていることを確認する必要があります。

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>ASP.NET 4.5 Web サイト テンプレートの設定変更

Visual Studio 2012 リリース候補の Web サイト テンプレートを使用して作成されたサイトの既定の*Web.config*ファイルに対して、次の変更が行われました。

- `<httpRuntime>`要素では、`encoderType`属性が既定で設定され、ASP.NETに追加された AntiXSS 型が使用されるようになりました。 詳細については[、AntiXSS ライブラリを](#_Toc318097382)参照してください。
- また、`<httpRuntime>`要素では、`requestValidationMode`属性は「4.5」に設定されています。 これは、既定では、要求の検証は遅延 ("遅延") 検証を使用するように構成されていることを意味します。 詳細については、「[新しいASP.NET要求検証機能](#_Toc318097379)」を参照してください。
- セクション`<modules>`の要素に`<system.webServer>`属性が`runAllManagedModulesForAllRequests`含まれていません。 (既定値は false です)。つまり、SP1 に更新されていないバージョンの IIS 7 を使用している場合、新しいサイトでのルーティングに問題がある可能性があります。 詳細については、「 [IIS 7 でのASP.NET ルーティングのネイティブ サポート](#Native_Support_In_IIS7_For_ASPNET_Routine)」を参照してください。

これらの変更は、既存のアプリケーションには影響しません。 ただし、既存の Web サイトと、新しいテンプレートを使用して ASP.NET 4.5 用に作成した新しい Web サイトとの動作の違いを表している可能性があります。

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>IIS 7 でのASP.NET ルーティングのネイティブ サポート

これは、ASP.NETに対する変更ではなく、SP1 更新プログラムが適用されていない IIS 7 のバージョンを使用している場合に影響を与える可能性のある、新しい Web サイト プロジェクトのテンプレートの変更です。

ASP.NETでは、ルーティングをサポートするために、アプリケーションに次の構成設定を追加できます。

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

**runAllManagedModulesForAllRequests**が true の場合`http://mysite/myapp/home`、URL に *.aspx* *、.mvc、* または同様の拡張子がない場合でも、URL のような URL はASP.NETに行きます。

IIS 7 に対して行われた更新により **、runAllManagedModulesForAllRequests**設定は不要になり、ネイティブでASP.NET ルーティングをサポートします。 (更新プログラムの詳細については、「Microsoft サポート技術情報」を参照してください特定[の IIS 7.0 または IIS 7.5 ハンドラーが、URL がピリオドで終わる要求を処理できる更新プログラム](https://support.microsoft.com/kb/980368)です。

Web サイトが IIS 7 で実行されており、IIS が更新されている場合は **、runAllManagedModulesForAllRequests**を true に設定する必要はありません。 実際には、要求に不要な処理オーバーヘッドが追加されるため、true に設定することはお勧めしません。 この設定が true の場合 *、.htm* *、.jpg、* およびその他の静的ファイルを含むすべての要求も、ASP.NET要求パイプラインを通過します。

Visual Studio 2012 RC で提供されるテンプレートを使用して新しい ASP.NET 4.5 Web サイトを作成する場合、Web サイトの構成には**runAllManagedModulesForAllRequests**設定は含まれません。 これは、デフォルトでは設定が false であることを意味します。

SP1 がインストールされていない Windows 7 で Web サイトを実行すると、IIS 7 には必要な更新プログラムは含まれません。 その結果、ルーティングは機能せず、エラーが表示されます。 ルーティングが機能しない問題が発生した場合は、次のいずれかの操作を行うことができます。

- Windows 7 を SP1 に更新し、IIS 7 に更新プログラムを追加します。
- 上記のマイクロソフト サポート資料に記載されている更新プログラムをインストールします。
- その Web サイトの Web.config ファイルで **、runAllManagedModulesForAllRequests**を true に設定します。 これは、要求に多少のオーバーヘッドを追加することに注意してください。

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML エディター

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>スマートタスク

デザイン ビューでは、サーバー コントロールの複雑なプロパティには、ダイアログ ボックスやウィザードが関連付けられていることが多く、設定が容易になります。 たとえば、特別なダイアログ ボックスを使用して、データ ソースを*Repeater*コントロールに追加したり *、GridView*コントロールに列を追加したりできます。

ただし、複雑なプロパティのこの種類の UI ヘルプは、ソース ビューでは使用できません。 したがって、Visual Studio 11 では、ソース ビューのスマート タスクが導入されています。 スマート タスクは、C# および Visual Basic エディターで一般的に使用される機能のコンテキスト対応のショートカットです。

Web フォーム コントロールASP.NETの場合、スマート タスクは、要素内にカーソルがあるときに、サーバー タグに小さなグリフとして表示されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

スマート タスクは、グリフをクリックするか、Ctrl キーを押しながら押すと展開されます。 (ドット)、コード エディターと同じように。 デザイン ビューのスマート タスクに似たショートカットが表示されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

たとえば、前の図のスマート タスクは、GridView タスク オプションを示しています。 [列を編集]を選択すると、次のダイアログ ボックスが表示されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

ダイアログ ボックスに入力すると、デザイン ビューで設定できるプロパティと同じプロパティが設定されます。 [OK] をクリックすると、コントロールのマークアップが新しい設定で更新されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>ワイアリアサポート

アクセス可能なウェブサイトを書くことはますます重要になっています。 [WAI-ARIA アクセシビリティ標準](http://www.w3.org/WAI/intro/aria)は、開発者がアクセシビリティ対応のウェブサイトを作成する方法を定義します。 この標準は、Visual Studio で完全にサポートされるようになりました。

たとえば、*ロール*属性に完全な IntelliSense が追加されました。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

WAI-ARIA 標準では、HTML5 ドキュメントにセマンティクスを追加できる*aria という*プレフィックスが付いた属性も導入されています。 Visual Studio では、次の*アリア*属性も完全にサポートされています。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>新しい HTML5 スニペット

一般的に使用される HTML5 マークアップを簡単に作成できるように、Visual Studio には多数のスニペットが用意されています。 例として、ビデオ スニペットがあります。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

スニペットを呼び出すには、IntelliSense で要素が選択されたときに Tab キーを 2 回押します。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

これにより、カスタマイズできるスニペットが生成されます。

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>ユーザー コントロールに抽出する

大規模な Web ページでは、個々の部分をユーザー コントロールに移動することをお勧めします。 この形式のリファクタリングは、ページの読みやすさを向上させ、ページ構造を簡略化するのに役立ちます。

このことを簡単にするため、ソース ビューで Web フォーム ページを編集するときに、ページ内のテキストを選択して右クリックし、[ユーザーコントロールに抽出] を選択します。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>属性内のコード ナゲットの IntelliSense

Visual Studio は、すべてのページまたはコントロールでサーバー側コード ナゲット用の IntelliSense を常に提供してきました。 現在、Visual Studio には、HTML 属性のコード ナゲット用 IntelliSense も含まれています。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

これにより、データ 連結式を簡単に作成できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>開始タグまたは終了タグの名前を変更すると、一致するタグの名前が自動的に変更される

HTML 要素の名前を変更すると (*たとえば、div*タグを*ヘッダー*タグに変更した場合)、対応する開始タグまたは終了タグもリアルタイムで変更されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

これは、終了タグを変更したり、間違ったタグを変更するのを忘れた場合のエラーを回避するのに役立ちます。

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>イベント ハンドラの生成

Visual Studio には、ソース ビューにイベント ハンドラーを記述して手動でバインドするための機能が含まれるようになりました。 ソース ビューでイベント名を編集している場合、IntelliSense&lt;は 、&gt;正しいシグネチャを持つページのコードにイベント ハンドラーを作成する新しいイベントの作成を表示します。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

既定では、イベント ハンドラーは、イベント処理メソッドの名前にコントロールの ID を使用します。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

結果のイベント ハンドラーは次のようになります (この場合は C# で)。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>スマートインデント

空の HTML 要素の中で Enter キーを押すと、エディターは挿入ポイントを適切な場所に置きます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

この位置で Enter キーを押すと、終了タグが下に移動され、開始タグと一致するようにインデントされます。 挿入ポイントもインデントされます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>ステートメントの自動削減入力

Visual Studio の IntelliSense リストは、入力内容に基づいてフィルター処理されるようになったので、関連するオプションのみが表示されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

また、IntelliSense リスト内の個々の単語のタイトルの大文字と小文字に基づいてフィルター処理を行います。 たとえば、"dl" と入力すると、dl と asp:DataList の両方が表示されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

この機能を使用すると、既知の要素のステートメント補完を取得する時間が短縮されます。

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript エディター

Visual Studio 2012 リリース候補の JavaScript エディターは完全に新しいものであり、Visual Studio での JavaScript の操作のエクスペリエンスを大幅に向上させます。

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>コードのアウトライン表示

すべての関数に対してアウトライン領域が自動的に作成されるようになり、現在のフォーカスに関連しないファイルの一部を折りたたむようになりました。

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>かっこの一致

左または右中かっこにカーソルを置くと、対応するカーソルが強調表示されます。

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>定義へ移動

[定義へ移動] コマンドを使用すると、関数または変数のソースにジャンプできます。

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAスクリプト5サポート

エディターは、JavaScript 言語を記述する標準の最新バージョンである ECMAScript5 の新しい構文と API をサポートしています。

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>ドム インテライセンス

DOM API 用 IntelliSense は、*クエリセレクタ*、DOM ストレージ、クロスドキュメント メッセージング、*キャンバス*など、多くの新しい HTML5 API をサポートし、改善されました。 DOM IntelliSense は、ネイティブ タイプ ライブラリ定義ではなく、単一の単純な JavaScript ファイルによって駆動されるようになりました。 これにより、拡張または置換が容易になります。

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC シグネチャのオーバーロード

次の例に示すように、新しい*&lt;シグネチャ&gt;* 要素を使用して、JavaScript 関数の個別のオーバーロードに対して詳細な IntelliSense コメントを宣言できるようになりました。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>暗黙的な参照

JavaScript ファイルを中央のリストに追加し、そのファイルのリストに暗黙的に含めることができるので、その内容は IntelliSense で取得できます。 たとえば、jQuery ファイルをファイルの中央のリストに追加すると、明示的に参照したかどうかにかかわらず(///&lt;参照/&gt;を使用して)、ファイルの任意の JavaScript ブロック内の jQuery 関数の IntelliSense を取得できます。

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS エディター

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>ステートメントの自動削減入力

CSS の IntelliSense リストは、選択したスキーマでサポートされている CSS プロパティと値に基づいてフィルター処理されるようになりました。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense では、タイトルケース検索もサポートしています。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>階層インデント

CSS エディタではインデントを使用して階層的なルールを表示し、カスケードルールの論理的な編成方法の概要を示します。 次の例では、セレクター#listはリストのカスケード子であり、インデントされます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

次の例は、より複雑な継承を示しています。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

規則のインデントは、その親規則によって決まります。 階層インデントは既定で有効になっていますが、[オプション] ダイアログ ボックス (メニュー バーの [ツール]、[ オプション] ) を無効にできます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS ハックのサポート

何百もの実世界の CSS ファイルを分析すると、CSS のハッキングは非常に一般的であり、現在 Visual Studio は最も広く使用されているファイルをサポートしています。 このサポートには、IntelliSense と星形の\*検証 (\_) とアンダースコア ( ) プロパティ のハックが含まれます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

一般的なセレクターハックもサポートされているため、適用しても階層インデントが維持されます。 Internet Explorer 7 をターゲットにするための一般的なセレクタ ハックは、セレクタの先頭に*\*:first-child + html*を付ける方法です。 このルールを使用すると、階層インデントが維持されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>ベンダー固有のスキーマ (-moz-, -webkit)

CSS3 では、さまざまな時間に異なるブラウザーによって実装された多くのプロパティが導入されています。 以前は、開発者はベンダ固有の構文を使用して、特定のブラウザー用のコードを作成する必要が出ていた。 これらのブラウザー固有のプロパティは、IntelliSense に含まれるようになりました。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>コメントとコメント解除のサポート

コード エディターで使用するのと同じショートカット (Ctrl+ K、C をコメントに、Ctrl + K キーを押してコメントを解除する) を使用して CSS ルールをコメント化したり、コメントを解除したりできるようになりました。

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>Color picker

以前のバージョンの Visual Studio では、色に関連する属性の IntelliSense は、名前付きの色の値のドロップダウン リストで構成されていました。 このリストは、フル機能のカラー ピッカーに置き換えられました。

カラー値を入力すると、カラー ピッカーが自動的に表示され、以前に使用した色のリストと、その後に既定のカラー パレットが表示されます。 マウスまたはキーボードを使用して色を選択できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

リストは、完全なカラーピッカーに拡張できます。 ピッカーでは、不透明度スライダを移動すると、色を RGBA に自動的に変換してアルファ チャンネルを制御できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>スニペット

CSS エディタのスニペットを使用すると、クロスブラウザ スタイルを簡単かつ迅速に作成できます。 ブラウザー固有の設定を必要とする多くの CSS3 プロパティは、スニペットにロールされています。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS スニペットは、IntelliSense リストを示すアットマーク (@)を入力することで、高度なシナリオ (CSS3 メディア クエリなど) をサポートします。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

値を選択@mediaして Tab キーを押すと、CSS エディターによって次のスニペットが挿入されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

コードのスニペットと同様に、独自の CSS スニペットを作成できます。

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>カスタム領域

コード エディターで既に使用できる名前付きコード領域が、CSS 編集で使用できるようになりました。 これにより、関連するスタイル ブロックを簡単にグループ化できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

領域が折りたたまれている場合、領域の名前が表示されます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Page Inspector

ページ インスペクターは、Visual Studio IDE で Web ページ (HTML、Web フォーム、ASP.NET MVC、または Web ページ) をレンダリングし、ソース コードと結果の出力の両方を確認できるツールです。 ページインスペクタでは、ASP.NETページのページインスペクターを使用して、ブラウザにレンダリングされる HTML マークアップを生成したサーバー側コードを特定できます。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

ページインスペクターの詳細については、次のチュートリアルを参照してください。

- [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)でのページ インスペクターの使用
- Web フォームでのページインスペクタ[ASP.NET使用](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)

<a id="_Toc318097425"></a>
### <a name="publishing"></a>置換

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>発行プロファイル

Visual Studio 2010 では、Web アプリケーション プロジェクトの発行情報はバージョン管理に格納されず、他のユーザーと共有するためのものではありません。 Visual Studio 2012 リリース候補では、発行プロファイルの形式が変更されました。 チームアーティファクトが作成され、MSBuild に基づくビルドから簡単に活用できるようになりました。 ビルド構成情報は[発行]ダイアログ ボックスにあり、発行前にビルド構成を簡単に切り替えることができます。

発行プロファイルは、発行プロファイル フォルダーに格納されます。 フォルダの場所は、使用しているプログラミング言語によって異なります。

- C#: プロパティ\発行プロファイル
- ビジュアル ベーシック: マイ プロジェクト\発行プロファイル

各プロファイルは MSBuild ファイルです。 発行中に、このファイルはプロジェクトの MSBuild ファイルにインポートされます。 Visual Studio 2010 では、発行プロセスまたはパッケージ プロセスに変更を加える場合は **、ProjectName**.wpp.targets という名前のファイルにカスタマイズを配置する必要があります。 これは引き続きサポートされていますが、カスタマイズを発行プロファイル自体に配置できるようになりました。 これにより、カスタマイズはそのプロファイルにのみ使用されます。

MSBuild の発行プロファイルを利用できるようになりました。 これを行うには、プロジェクトをビルドするときに次のコマンドを使用します。

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

project.csproj 値はプロジェクトのパスであり、プロファイル名はパブリッシュするプロファイルの名前です。 または *、PublishProfile*プロパティのプロファイル名を渡す代わりに、発行プロファイルへの完全パスを渡すことができます。

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>プリコンパイルとマージのASP.NET

Web アプリケーション プロジェクトの場合、Visual Studio 2012 リリース候補は、プロジェクトを発行またはパッケージ化するときにサイトのコンテンツをプリコンパイルし、マージできる [パッケージ/発行 Web プロパティ] ページにオプションを追加します。 これらのオプションを表示するには、ソリューション エクスプローラーでプロジェクトを右クリックし、[プロパティ] を選択して、[パッケージ化/発行 Web] プロパティ ページを選択します。 次の図は、[このアプリケーションを公開前にプリコンパイルする] オプションを示しています。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

このオプションを選択すると、Web アプリケーションを発行またはパッケージ化するたびに、Visual Studio によってアプリケーションがプリコンパイルされます。 サイトのプリコンパイル方法やアセンブリのマージ方法を制御する場合は、[詳細設定] ボタンをクリックしてこれらのオプションを構成します。

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

Visual Studio で Web プロジェクトをテストするための既定の Web サーバーが IIS エクスプレスになりました。 開発中のローカル Web サーバーの場合は、Visual Studio 開発サーバーが依然としてオプションですが、IIS Express が推奨されるサーバーになりました。 Visual Studio 11 ベータ版で IIS エクスプレスを使用するエクスペリエンスは、Visual Studio 2010 SP1 での使用と非常によく似ています。

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>免責事項

このドキュメントは暫定版であり、ここで説明するソフトウェアの最終的な商業リリースより前に大幅に変更される可能性があります。

このドキュメントに含まれる情報は、取り上げている問題についての、公開時点における Microsoft Corporation の見解を表します。 Microsoft は変化する市場状況に対応する必要があるため、これを Microsoft による確約と解釈しないでください。Microsoft は、記載されている情報の公開後の正確さを保証できません。

このホワイト ペーパーは、情報提供のみを目的としています。 マイクロソフトは、このドキュメント内の情報に関して、明示的、暗黙的、または法的ないかなる保証も行いません。

お客様ご自身の責任において、適用されるすべての著作権関連法規に従ったご使用を願います。 このソフトウェアおよびマニュアルのいかなる部分も、米国 Microsoft Corporation の書面による許諾を受けることなく、その目的を問わず、どのような形態であっても、複製または譲渡することは禁じられています。ここでいう形態とは、複写や記録など、電子的な、または物理的なすべての手段を含みます。

Microsoft は、このマニュアルに記載されている内容に関し、特許、特許申請、商標、著作権、またはその他の無体財産権を有する場合があります。 別途マイクロソフトのライセンス契約上に明示の規定がない限り、このドキュメントはこれらの特許、商標、著作権、またはその他の無体財産権に関する権利をお客様に許諾するものではありません。

特に記載されていない限り、ここに記載されている会社、組織、製品、ドメイン名、電子メールアドレス、ロゴ、人物、場所、イベントは架空のものであり、実際の会社、組織、製品、ドメイン名、電子メールアドレス、ロゴ、人物、人物、場所、またはイベントとの関連付けは意図されていないか、または推測されるべきである。

(C) 2012 Microsoft Corporation. All rights reserved.

Microsoft および Windows は、米国および他の国における Microsoft Corporation の登録商標または商標です。

本ドキュメントで説明する実際の製造元および製品名は、それぞれの所有者の商標である場合があります。
