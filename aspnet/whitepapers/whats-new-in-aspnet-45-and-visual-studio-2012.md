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
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a><span data-ttu-id="5c614-104">ASP.NET 4.5 と Visual Studio 2012 の新機能</span><span class="sxs-lookup"><span data-stu-id="5c614-104">What's New in ASP.NET 4.5 and Visual Studio 2012</span></span>

> <span data-ttu-id="5c614-105">このドキュメントでは、ASP.NET 4.5 で導入されている新機能と拡張機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="5c614-105">This document describes new features and enhancements that are being introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="5c614-106">また、Visual Studio 2012 での Web 開発の改善についても説明します。</span><span class="sxs-lookup"><span data-stu-id="5c614-106">It also describes improvements being made for web development in Visual Studio 2012.</span></span> <span data-ttu-id="5c614-107">この文書は2012年2月29日に公開されました。</span><span class="sxs-lookup"><span data-stu-id="5c614-107">This document was originally published on February 29, 2012.</span></span>

- [<span data-ttu-id="5c614-108">ASP.NETコア ランタイムとフレームワーク</span><span class="sxs-lookup"><span data-stu-id="5c614-108">ASP.NET Core Runtime and Framework</span></span>](#_Toc318097372)

    - [<span data-ttu-id="5c614-109">HTTP 要求と応答の非同期読み取りと書き込み</span><span class="sxs-lookup"><span data-stu-id="5c614-109">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>](#_Toc318097373)
    - [<span data-ttu-id="5c614-110">HttpRequest 処理の機能強化</span><span class="sxs-lookup"><span data-stu-id="5c614-110">Improvements to HttpRequest handling</span></span>](#_Toc318097374)
    - [<span data-ttu-id="5c614-111">非同期的に応答をフラッシュする</span><span class="sxs-lookup"><span data-stu-id="5c614-111">Asynchronously flushing a response</span></span>](#_Toc318097375)
    - [<span data-ttu-id="5c614-112">*await*および*タスク*ベースの非同期モジュールおよびハンドラーのサポート</span><span class="sxs-lookup"><span data-stu-id="5c614-112">Support for *await* and *Task*-Based Asynchronous Modules and Handlers</span></span>](#_Toc318097376)
    - [<span data-ttu-id="5c614-113">非同期 HTTP モジュール</span><span class="sxs-lookup"><span data-stu-id="5c614-113">Asynchronous HTTP modules</span></span>](#_Toc318097377)
    - [<span data-ttu-id="5c614-114">非同期 HTTP ハンドラー</span><span class="sxs-lookup"><span data-stu-id="5c614-114">Asynchronous HTTP handlers</span></span>](#_Toc318097378)
    - [<span data-ttu-id="5c614-115">新しいASP.NET要求検証機能</span><span class="sxs-lookup"><span data-stu-id="5c614-115">New ASP.NET Request Validation Features</span></span>](#_Toc318097379)
    - [<span data-ttu-id="5c614-116">遅延 (「遅延」) 要求の検証</span><span class="sxs-lookup"><span data-stu-id="5c614-116">Deferred ("lazy") request validation</span></span>](#_Toc318097380)
    - [<span data-ttu-id="5c614-117">未検証要求のサポート</span><span class="sxs-lookup"><span data-stu-id="5c614-117">Support for unvalidated requests</span></span>](#_Toc318097381)
    - [<span data-ttu-id="5c614-118">アンチXSSライブラリ</span><span class="sxs-lookup"><span data-stu-id="5c614-118">AntiXSS Library</span></span>](#_Toc318097382)
    - [<span data-ttu-id="5c614-119">Web ソケット プロトコルのサポート</span><span class="sxs-lookup"><span data-stu-id="5c614-119">Support for WebSockets Protocol</span></span>](#_Toc318097383)
    - [<span data-ttu-id="5c614-120">バンドルとミンフィケーション</span><span class="sxs-lookup"><span data-stu-id="5c614-120">Bundling and Minification</span></span>](#_Toc318097384)
    - [<span data-ttu-id="5c614-121">Web ホスティングのパフォーマンス向上</span><span class="sxs-lookup"><span data-stu-id="5c614-121">Performance Improvements for Web Hosting</span></span>](#_Toc_perf)

        - [<span data-ttu-id="5c614-122">主要なパフォーマンス要因</span><span class="sxs-lookup"><span data-stu-id="5c614-122">Key Performance Factors</span></span>](#_Toc_perf_1)
        - [<span data-ttu-id="5c614-123">新しいパフォーマンス機能の要件</span><span class="sxs-lookup"><span data-stu-id="5c614-123">Requirements for New Performance Features</span></span>](#_Toc_perf_2)
        - [<span data-ttu-id="5c614-124">共通アセンブリの共有</span><span class="sxs-lookup"><span data-stu-id="5c614-124">Sharing Common Assemblies</span></span>](#_Toc_perf_3)
        - [<span data-ttu-id="5c614-125">マルチコア JIT コンパイルを使用して、高速なスタートアップを実現</span><span class="sxs-lookup"><span data-stu-id="5c614-125">Using multi-Core JIT compilation for faster startup</span></span>](#_Toc_perf_4)
        - [<span data-ttu-id="5c614-126">メモリ用に最適化するためのガベージ コレクションのチューニング</span><span class="sxs-lookup"><span data-stu-id="5c614-126">Tuning garbage collection to optimize for memory</span></span>](#_Toc_perf_5)
        - [<span data-ttu-id="5c614-127">Web アプリケーションのプリフェッチ</span><span class="sxs-lookup"><span data-stu-id="5c614-127">Prefetching for web applications</span></span>](#_Toc_perf_6)
- [<span data-ttu-id="5c614-128">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="5c614-128">ASP.NET Web Forms</span></span>](#_Toc318097385)

    - [<span data-ttu-id="5c614-129">厳密に型指定されたデータ コントロール</span><span class="sxs-lookup"><span data-stu-id="5c614-129">Strongly Typed Data Controls</span></span>](#_Toc318097386)
    - [<span data-ttu-id="5c614-130">モデル バインド</span><span class="sxs-lookup"><span data-stu-id="5c614-130">Model Binding</span></span>](#_Toc318097387)

        - [<span data-ttu-id="5c614-131">データの選択</span><span class="sxs-lookup"><span data-stu-id="5c614-131">Selecting data</span></span>](#_Toc318097388)
        - [<span data-ttu-id="5c614-132">値プロバイダー</span><span class="sxs-lookup"><span data-stu-id="5c614-132">Value providers</span></span>](#_Toc318097389)
        - [<span data-ttu-id="5c614-133">コントロールの値によるフィルター処理</span><span class="sxs-lookup"><span data-stu-id="5c614-133">Filtering by values from a control</span></span>](#_Toc318097390)
    - [<span data-ttu-id="5c614-134">HTML エンコードされたデータ バインディング式</span><span class="sxs-lookup"><span data-stu-id="5c614-134">HTML Encoded Data-Binding Expressions</span></span>](#_Toc318097391)
    - [<span data-ttu-id="5c614-135">控えめな検証</span><span class="sxs-lookup"><span data-stu-id="5c614-135">Unobtrusive Validation</span></span>](#_Toc318097392)
    - [<span data-ttu-id="5c614-136">HTML5 の更新プログラム</span><span class="sxs-lookup"><span data-stu-id="5c614-136">HTML5 Updates</span></span>](#_Toc318097393)
- [<span data-ttu-id="5c614-137">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="5c614-137">ASP.NET MVC 4</span></span>](#_Toc318097394)
- [<span data-ttu-id="5c614-138">ASP.NET Web ページ 2</span><span class="sxs-lookup"><span data-stu-id="5c614-138">ASP.NET Web Pages 2</span></span>](#_Toc318097395)
- [<span data-ttu-id="5c614-139">ビジュアル スタジオ 2012 リリース候補</span><span class="sxs-lookup"><span data-stu-id="5c614-139">Visual Studio 2012 Release Candidate</span></span>](#_Toc318097396)

    - [<span data-ttu-id="5c614-140">Visual Studio 2010 と Visual Studio 2012 リリース候補との間のプロジェクト共有 (プロジェクトの互換性)</span><span class="sxs-lookup"><span data-stu-id="5c614-140">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>](#project-compatibility)
    - [<span data-ttu-id="5c614-141">ASP.NET 4.5 Web サイト テンプレートの設定変更</span><span class="sxs-lookup"><span data-stu-id="5c614-141">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [<span data-ttu-id="5c614-142">IIS 7 でのASP.NET ルーティングのネイティブ サポート</span><span class="sxs-lookup"><span data-stu-id="5c614-142">Native Support in IIS 7 for ASP.NET Routing</span></span>](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [<span data-ttu-id="5c614-143">HTML エディター</span><span class="sxs-lookup"><span data-stu-id="5c614-143">HTML Editor</span></span>](#_Toc318097397)

        - [<span data-ttu-id="5c614-144">スマートタスク</span><span class="sxs-lookup"><span data-stu-id="5c614-144">Smart Tasks</span></span>](#_Toc318097398)
        - [<span data-ttu-id="5c614-145">ワイアリアサポート</span><span class="sxs-lookup"><span data-stu-id="5c614-145">WAI-ARIA support</span></span>](#_Toc318097399)
        - [<span data-ttu-id="5c614-146">新しい HTML5 スニペット</span><span class="sxs-lookup"><span data-stu-id="5c614-146">New HTML5 snippets</span></span>](#_Toc318097400)
        - [<span data-ttu-id="5c614-147">ユーザー コントロールに抽出する</span><span class="sxs-lookup"><span data-stu-id="5c614-147">Extract to user control</span></span>](#_Toc318097401)
        - [<span data-ttu-id="5c614-148">属性内のコード ナゲットの IntelliSense</span><span class="sxs-lookup"><span data-stu-id="5c614-148">IntelliSense for code nuggets in attributes</span></span>](#_Toc318097402)
        - [<span data-ttu-id="5c614-149">開始タグまたは終了タグの名前を変更すると、一致するタグの名前が自動的に変更される</span><span class="sxs-lookup"><span data-stu-id="5c614-149">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>](#_Toc318097403)
        - [<span data-ttu-id="5c614-150">イベント ハンドラの生成</span><span class="sxs-lookup"><span data-stu-id="5c614-150">Event handler generation</span></span>](#_Toc318097404)
        - [<span data-ttu-id="5c614-151">スマートインデント</span><span class="sxs-lookup"><span data-stu-id="5c614-151">Smart indent</span></span>](#_Toc318097405)
        - [<span data-ttu-id="5c614-152">ステートメントの自動削減入力</span><span class="sxs-lookup"><span data-stu-id="5c614-152">Auto-reduce statement completion</span></span>](#_Toc318097406)
    - [<span data-ttu-id="5c614-153">スクリプトエディタ</span><span class="sxs-lookup"><span data-stu-id="5c614-153">JavaScript Editor</span></span>](#_Toc318097407)

        - [<span data-ttu-id="5c614-154">コードのアウトライン</span><span class="sxs-lookup"><span data-stu-id="5c614-154">Code outlining</span></span>](#_Toc318097408)
        - [<span data-ttu-id="5c614-155">ブレースのマッチング</span><span class="sxs-lookup"><span data-stu-id="5c614-155">Brace matching</span></span>](#_Toc318097409)
        - [<span data-ttu-id="5c614-156">定義へ移動</span><span class="sxs-lookup"><span data-stu-id="5c614-156">Go to Definition</span></span>](#_Toc318097410)
        - [<span data-ttu-id="5c614-157">ECMAスクリプト5サポート</span><span class="sxs-lookup"><span data-stu-id="5c614-157">ECMAScript5 support</span></span>](#_Toc318097411)
        - [<span data-ttu-id="5c614-158">ドム インテライセンス</span><span class="sxs-lookup"><span data-stu-id="5c614-158">DOM IntelliSense</span></span>](#_Toc318097412)
        - [<span data-ttu-id="5c614-159">VSDOC シグネチャのオーバーロード</span><span class="sxs-lookup"><span data-stu-id="5c614-159">VSDOC signature overloads</span></span>](#_Toc318097413)
        - [<span data-ttu-id="5c614-160">暗黙的な参照</span><span class="sxs-lookup"><span data-stu-id="5c614-160">Implicit references</span></span>](#_Toc318097414)
    - [<span data-ttu-id="5c614-161">CSS エディター</span><span class="sxs-lookup"><span data-stu-id="5c614-161">CSS Editor</span></span>](#_Toc318097415)

        - [<span data-ttu-id="5c614-162">ステートメントの自動削減入力</span><span class="sxs-lookup"><span data-stu-id="5c614-162">Auto-reduce statement completion</span></span>](#_Toc318097416)
        - [<span data-ttu-id="5c614-163">階層インデント。</span><span class="sxs-lookup"><span data-stu-id="5c614-163">Hierarchical indentation.</span></span>](#_Toc318097417)
        - [<span data-ttu-id="5c614-164">CSS ハックのサポート</span><span class="sxs-lookup"><span data-stu-id="5c614-164">CSS hacks support</span></span>](#_Toc318097418)
        - [<span data-ttu-id="5c614-165">ベンダー固有のスキーマ (-moz -,-Webkit)</span><span class="sxs-lookup"><span data-stu-id="5c614-165">Vendor specific schemas (-moz-,-webkit)</span></span>](#_Toc318097419)
        - [<span data-ttu-id="5c614-166">コメントとコメント解除のサポート</span><span class="sxs-lookup"><span data-stu-id="5c614-166">Commenting and uncommenting support</span></span>](#_Toc318097420)
        - [<span data-ttu-id="5c614-167">Color picker</span><span class="sxs-lookup"><span data-stu-id="5c614-167">Color picker</span></span>](#_Toc318097421)
        - [<span data-ttu-id="5c614-168">スニペット</span><span class="sxs-lookup"><span data-stu-id="5c614-168">Snippets</span></span>](#_Toc318097422)
        - [<span data-ttu-id="5c614-169">カスタム領域</span><span class="sxs-lookup"><span data-stu-id="5c614-169">Custom regions</span></span>](#_Toc318097423)
    - [<span data-ttu-id="5c614-170">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="5c614-170">Page Inspector</span></span>](#_Toc318097424)
    - [<span data-ttu-id="5c614-171">置換</span><span class="sxs-lookup"><span data-stu-id="5c614-171">Publishing</span></span>](#_Toc318097425)

        - [<span data-ttu-id="5c614-172">発行プロファイル</span><span class="sxs-lookup"><span data-stu-id="5c614-172">Publish profiles</span></span>](#_Toc318097426)
        - [<span data-ttu-id="5c614-173">プリコンパイルとマージのASP.NET</span><span class="sxs-lookup"><span data-stu-id="5c614-173">ASP.NET precompilation and merge</span></span>](#_Toc318097427)
- [<span data-ttu-id="5c614-174">IIS Express</span><span class="sxs-lookup"><span data-stu-id="5c614-174">IIS Express</span></span>](#_Toc318097428)
- [<span data-ttu-id="5c614-175">免責 事項</span><span class="sxs-lookup"><span data-stu-id="5c614-175">Disclaimer</span></span>](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a><span data-ttu-id="5c614-176">ASP.NETコア ランタイムとフレームワーク</span><span class="sxs-lookup"><span data-stu-id="5c614-176">ASP.NET Core Runtime and Framework</span></span>

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a><span data-ttu-id="5c614-177">HTTP 要求と応答の非同期読み取りと書き込み</span><span class="sxs-lookup"><span data-stu-id="5c614-177">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>

<span data-ttu-id="5c614-178">ASP.NET 4 では、HTTP 要求エンティティをストリームとして読み取る*機能が導入*されました。</span><span class="sxs-lookup"><span data-stu-id="5c614-178">ASP.NET 4 introduced the ability to read an HTTP request entity as a stream using the *HttpRequest.GetBufferlessInputStream* method.</span></span> <span data-ttu-id="5c614-179">このメソッドは、要求エンティティへのストリーミング アクセスを提供します。</span><span class="sxs-lookup"><span data-stu-id="5c614-179">This method provided streaming access to the request entity.</span></span> <span data-ttu-id="5c614-180">しかし、同期的に実行され、要求の間スレッドが縛られます。</span><span class="sxs-lookup"><span data-stu-id="5c614-180">However, it executed synchronously, which tied up a thread for the duration of a request.</span></span>

<span data-ttu-id="5c614-181">ASP.NET 4.5 では、HTTP 要求エンティティでストリームを非同期に読み取る機能と、非同期的にフラッシュする機能がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="5c614-181">ASP.NET 4.5 supports the ability to read streams asynchronously on an HTTP request entity, and the ability to flush asynchronously.</span></span> <span data-ttu-id="5c614-182">ASP.NET 4.5 では、HTTP 要求エンティティをダブル バッファーする機能も提供し、.aspx ページ ハンドラーや ASP.NET MVC コントローラーなどのダウンストリーム HTTP ハンドラーとの統合が容易になります。</span><span class="sxs-lookup"><span data-stu-id="5c614-182">ASP.NET 4.5 also gives you the ability to double-buffer an HTTP request entity, which provides easier integration with downstream HTTP handlers such as .aspx page handlers and ASP.NET MVC controllers.</span></span>

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a><span data-ttu-id="5c614-183">HttpRequest 処理の機能強化</span><span class="sxs-lookup"><span data-stu-id="5c614-183">Improvements to HttpRequest handling</span></span>

<span data-ttu-id="5c614-184">*httpRequest.GetBufferlessInputStream*から ASP.NET 4.5 から返されるストリーム参照は、同期および非同期の読み取りメソッドの両方をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="5c614-184">The Stream reference returned by ASP.NET 4.5 from *HttpRequest.GetBufferlessInputStream* supports both synchronous and asynchronous read methods.</span></span> <span data-ttu-id="5c614-185">*GetBufferlessInputStream*から返される*ストリーム*オブジェクトは、BeginRead メソッドと EndRead メソッドの両方を実装するようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-185">The *Stream* object returned from *GetBufferlessInputStream* now implements both the BeginRead and EndRead methods.</span></span> <span data-ttu-id="5c614-186">非同期*Stream*メソッドを使用すると、要求エンティティをチャンク単位で非同期に読み取り、ASP.NETは非同期読み取りループの各反復の間に現在のスレッドを解放できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-186">The asynchronous *Stream* methods let you asynchronously read the request entity in chunks, while ASP.NET releases the current thread between each iteration of an asynchronous read loop.</span></span>

<span data-ttu-id="5c614-187">ASP.NET 4.5 は、バッファリングされた方法で要求エンティティを読み取るためのコンパニオン メソッドも追加*しました。*</span><span class="sxs-lookup"><span data-stu-id="5c614-187">ASP.NET 4.5 has also added a companion method for reading the request entity in a buffered way: *HttpRequest.GetBufferedInputStream*.</span></span> <span data-ttu-id="5c614-188">この新しいオーバーロードは、同期読み取りと非同期読み取りの両方をサポートする*GetBufferlessInputStream*のように機能します。</span><span class="sxs-lookup"><span data-stu-id="5c614-188">This new overload works like *GetBufferlessInputStream*, supporting both synchronous and asynchronous reads.</span></span> <span data-ttu-id="5c614-189">ただし、読み取り中に *、GetBufferedInputStream*は、ダウンストリームのモジュールとハンドラーが要求エンティティにアクセスできるように、エンティティのバイトをASP.NET内部バッファーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="5c614-189">However, as it reads, *GetBufferedInputStream* also copies the entity bytes into ASP.NET internal buffers so that downstream modules and handlers can still access the request entity.</span></span> <span data-ttu-id="5c614-190">たとえば、パイプライン内の一部の上流コードが*GetBufferedInputStream*を使用して既に要求エンティティを読み取っている場合は *、HttpRequest.Form または HttpRequest.Files*を使用できます。 *HttpRequest.Files*</span><span class="sxs-lookup"><span data-stu-id="5c614-190">For example, if some upstream code in the pipeline has already read the request entity using *GetBufferedInputStream*, you can still use *HttpRequest.Form* or *HttpRequest.Files*.</span></span> <span data-ttu-id="5c614-191">これにより、要求に対して非同期処理を実行できます (たとえば、データベースへの大きなファイルアップロードのストリーミングなど) が、後で .aspx ページと MVC ASP.NET コントローラーを実行します。</span><span class="sxs-lookup"><span data-stu-id="5c614-191">This lets you perform asynchronous processing on a request (for example, streaming a large file upload to a database), but still run .aspx pages and MVC ASP.NET controllers afterward.</span></span>

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a><span data-ttu-id="5c614-192">非同期的に応答をフラッシュする</span><span class="sxs-lookup"><span data-stu-id="5c614-192">Asynchronously flushing a response</span></span>

<span data-ttu-id="5c614-193">HTTP クライアントへの応答の送信は、クライアントが遠く離れているか、または帯域幅の低い接続を持つ場合にかなりの時間を要する場合があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-193">Sending responses to an HTTP client can take considerable time when the client is far away or has a low-bandwidth connection.</span></span> <span data-ttu-id="5c614-194">通常、ASP.NETは、アプリケーションによって作成された応答バイトをバッファします。</span><span class="sxs-lookup"><span data-stu-id="5c614-194">Normally ASP.NET buffers the response bytes as they are created by an application.</span></span> <span data-ttu-id="5c614-195">ASP.NET、要求処理の最後の最後に、発生したバッファーの単一の送信操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="5c614-195">ASP.NET then performs a single send operation of the accrued buffers at the very end of request processing.</span></span>

<span data-ttu-id="5c614-196">バッファリングされた応答が大きい場合 (たとえば、大きなファイルをクライアントにストリーミングする場合)、定期的に*HttpResponse.Flush*を呼び出してバッファ出力をクライアントに送信し、メモリ使用量を制御する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-196">If the buffered response is large (for example, streaming a large file to a client), you must periodically call *HttpResponse.Flush* to send buffered output to the client and keep memory usage under control.</span></span> <span data-ttu-id="5c614-197">ただし *、Flush*は同期呼び出しであるため *、Flush*を繰り回し、実行時間が長い可能性がある要求の間はスレッドを消費します。</span><span class="sxs-lookup"><span data-stu-id="5c614-197">However, because *Flush* is a synchronous call, iteratively calling *Flush* still consumes a thread for the duration of potentially long-running requests.</span></span>

<span data-ttu-id="5c614-198">ASP.NET 4.5 では *、HttpResponse*クラスの*BeginFlush*メソッドと*EndFlush*メソッドを使用して、非同期的にフラッシュを実行するためのサポートが追加されています。</span><span class="sxs-lookup"><span data-stu-id="5c614-198">ASP.NET 4.5 adds support for performing flushes asynchronously using the *BeginFlush* and *EndFlush* methods of the *HttpResponse* class.</span></span> <span data-ttu-id="5c614-199">これらのメソッドを使用すると、オペレーティング システムスレッドを縛らずにクライアントにデータを増分的に送信する非同期モジュールと非同期ハンドラを作成できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-199">Using these methods, you can create asynchronous modules and asynchronous handlers that incrementally send data to a client without tying up operating-system threads.</span></span> <span data-ttu-id="5c614-200">*BeginFlush*と*EndFlush*呼び出しの間で、ASP.NETは現在のスレッドを解放します。</span><span class="sxs-lookup"><span data-stu-id="5c614-200">In between *BeginFlush* and *EndFlush* calls, ASP.NET releases the current thread.</span></span> <span data-ttu-id="5c614-201">これにより、実行時間の長い HTTP ダウンロードをサポートするために必要なアクティブスレッドの総数が大幅に削減されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-201">This substantially reduces the total number of active threads that are needed in order to support long-running HTTP downloads.</span></span>

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a><span data-ttu-id="5c614-202">*await*および*Task*ベースの非同期モジュールとハンドラーのサポート</span><span class="sxs-lookup"><span data-stu-id="5c614-202">Support for *await* and *Task* - Based Asynchronous Modules and Handlers</span></span>

<span data-ttu-id="5c614-203">.NET Framework 4 では、タスクと呼ばれる非同期プログラミングの概念が導入*されました*。</span><span class="sxs-lookup"><span data-stu-id="5c614-203">The .NET Framework 4 introduced an asynchronous programming concept referred to as a *task*.</span></span> <span data-ttu-id="5c614-204">タスクは、*タスク*の種類と関連する型によって表*System.Threading.Tasks*されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-204">Tasks are represented by the *Task* type and related types in the *System.Threading.Tasks* namespace.</span></span> <span data-ttu-id="5c614-205">.NET Framework 4.5 は、この機能をベースに、*タスク*オブジェクトの操作を簡単にするコンパイラの機能強化を備えています。</span><span class="sxs-lookup"><span data-stu-id="5c614-205">The .NET Framework 4.5 builds on this with compiler enhancements that make working with *Task* objects simple.</span></span> <span data-ttu-id="5c614-206">.NET Framework 4.5 では、コンパイラは 2 つの新*await*しいキーワード*を*サポートしています。</span><span class="sxs-lookup"><span data-stu-id="5c614-206">In the .NET Framework 4.5, the compilers support two new keywords: *await* and *async*.</span></span> <span data-ttu-id="5c614-207">*await*キーワードは、コードの一部が他のコードを非同期に待機する必要があることを示す構文の省略形です。</span><span class="sxs-lookup"><span data-stu-id="5c614-207">The *await* keyword is syntactical shorthand for indicating that a piece of code should asynchronously wait on some other piece of code.</span></span> <span data-ttu-id="5c614-208">*async*キーワードは、メソッドをタスクベースの非同期メソッドとしてマークするために使用できるヒントを表します。</span><span class="sxs-lookup"><span data-stu-id="5c614-208">The *async* keyword represents a hint that you can use to mark methods as task-based asynchronous methods.</span></span>

<span data-ttu-id="5c614-209">*await* *、async、* および*Task*オブジェクトを組み合わせると、.NET 4.5 で非同期コードを記述する方がはるかに簡単になります。</span><span class="sxs-lookup"><span data-stu-id="5c614-209">The combination of *await*, *async*, and the *Task* object makes it much easier for you to write asynchronous code in .NET 4.5.</span></span> <span data-ttu-id="5c614-210">ASP.NET 4.5 では、新しいコンパイラ拡張機能を使用して非同期 HTTP モジュールと非同期 HTTP ハンドラーを記述できる新しい API でこれらの簡略化がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="5c614-210">ASP.NET 4.5 supports these simplifications with new APIs that let you write asynchronous HTTP modules and asynchronous HTTP handlers using the new compiler enhancements.</span></span>

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a><span data-ttu-id="5c614-211">非同期 HTTP モジュール</span><span class="sxs-lookup"><span data-stu-id="5c614-211">Asynchronous HTTP modules</span></span>

<span data-ttu-id="5c614-212">*Task*オブジェクトを返すメソッド内で非同期処理を実行するとします。</span><span class="sxs-lookup"><span data-stu-id="5c614-212">Suppose that you want to perform asynchronous work within a method that returns a *Task* object.</span></span> <span data-ttu-id="5c614-213">Microsoft ホーム ページをダウンロードするための非同期呼び出しを行う非同期メソッドを定義するコード例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="5c614-213">The following code example defines an asynchronous method that makes an asynchronous call to download the Microsoft home page.</span></span> <span data-ttu-id="5c614-214">メソッド シグネチャと、メソッド シグネチャへの*async*キーワードの使用と *、呼*び出し*の待機*に注意してください。</span><span class="sxs-lookup"><span data-stu-id="5c614-214">Notice the use of the *async* keyword in the method signature and the *await* call to *DownloadStringTaskAsync*.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

<span data-ttu-id="5c614-215">この方法は、ダウンロード完了の待機中に呼び出し履歴のアンワインドを自動的に処理し、ダウンロードが完了した後に呼び出し履歴を自動的に復元します。</span><span class="sxs-lookup"><span data-stu-id="5c614-215">That's all you have to write — the .NET Framework will automatically handle unwinding the call stack while waiting for the download to complete, as well as automatically restoring the call stack after the download is done.</span></span>

<span data-ttu-id="5c614-216">ここで、この非同期メソッドを非同期 ASP.NET HTTP モジュールで使用するとします。</span><span class="sxs-lookup"><span data-stu-id="5c614-216">Now suppose that you want to use this asynchronous method in an asynchronous ASP.NET HTTP module.</span></span> <span data-ttu-id="5c614-217">ASP.NET 4.5 には、ヘルパー メソッド (*EventHandlerTaskAsyncHelper*) と新しいデリゲート型 (*TaskEventHandler*) が含まれており、これを使用して、ASP.NET HTTP パイプラインによって公開された古い非同期プログラミング モデルとタスク ベースの非同期メソッドを統合できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-217">ASP.NET 4.5 includes a helper method (*EventHandlerTaskAsyncHelper*) and a new delegate type (*TaskEventHandler*) that you can use to integrate task-based asynchronous methods with the older asynchronous programming model exposed by the ASP.NET HTTP pipeline.</span></span> <span data-ttu-id="5c614-218">この例は、次の方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="5c614-218">This example shows how:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a><span data-ttu-id="5c614-219">非同期 HTTP ハンドラー</span><span class="sxs-lookup"><span data-stu-id="5c614-219">Asynchronous HTTP handlers</span></span>

<span data-ttu-id="5c614-220">ASP.NETで非同期ハンドラを記述する従来のアプローチは *、IHttpAsyncHandler*インターフェイスを実装することです。</span><span class="sxs-lookup"><span data-stu-id="5c614-220">The traditional approach to writing asynchronous handlers in ASP.NET is to implement the *IHttpAsyncHandler* interface.</span></span> <span data-ttu-id="5c614-221">ASP.NET 4.5 では、派生元の非同期基本型*HttpTaskAsyncHandler*が導入されており、非同期ハンドラーの記述が簡単になります。</span><span class="sxs-lookup"><span data-stu-id="5c614-221">ASP.NET 4.5 introduces the *HttpTaskAsyncHandler* asynchronous base type that you can derive from, which makes it much easier to write asynchronous handlers.</span></span>

<span data-ttu-id="5c614-222">型*は*抽象型であり、*メソッド*をオーバーライドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-222">The *HttpTaskAsyncHandler* type is abstract and requires you to override the *ProcessRequestAsync* method.</span></span> <span data-ttu-id="5c614-223">内部的にはASP.NETは *、ProcessRequestAsync*の戻り署名 *(Task*オブジェクト) と、ASP.NETパイプラインで使用される古い非同期プログラミング モデルを統合します。</span><span class="sxs-lookup"><span data-stu-id="5c614-223">Internally ASP.NET takes care of integrating the return signature (a *Task* object) of *ProcessRequestAsync* with the older asynchronous programming model used by the ASP.NET pipeline.</span></span>

<span data-ttu-id="5c614-224">次の例は、非同期 HTTP ハンドラーの実装の一部として*Task*および*await*を使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="5c614-224">The following example shows how you can use *Task* and *await* as part of the implementation of an asynchronous HTTP handler:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a><span data-ttu-id="5c614-225">新しいASP.NET要求検証機能</span><span class="sxs-lookup"><span data-stu-id="5c614-225">New ASP.NET Request Validation Features</span></span>

<span data-ttu-id="5c614-226">既定では、ASP.NETは要求の検証を実行し、フィールド、ヘッダー、Cookie などのマークアップまたはスクリプトを検索する要求を調べます。</span><span class="sxs-lookup"><span data-stu-id="5c614-226">By default, ASP.NET performs request validation — it examines requests to look for markup or script in fields, headers, cookies, and so on.</span></span> <span data-ttu-id="5c614-227">検出された場合、ASP.NETは例外をスローします。</span><span class="sxs-lookup"><span data-stu-id="5c614-227">If any is detected, ASP.NET throws an exception.</span></span> <span data-ttu-id="5c614-228">これは、クロスサイト スクリプティング攻撃の可能性に対する防御の第 1 線として機能します。</span><span class="sxs-lookup"><span data-stu-id="5c614-228">This acts as a first line of defense against potential cross-site scripting attacks.</span></span>

<span data-ttu-id="5c614-229">ASP.NET 4.5 を使用すると、検証されていない要求データを選択して読み取りが容易になります。</span><span class="sxs-lookup"><span data-stu-id="5c614-229">ASP.NET 4.5 makes it easy to selectively read unvalidated request data.</span></span> <span data-ttu-id="5c614-230">ASP.NET4.5はまた、以前は外部ライブラリであった人気のAntiXSSライブラリを統合しています。</span><span class="sxs-lookup"><span data-stu-id="5c614-230">ASP.NET 4.5 also integrates the popular AntiXSS library, which was formerly an external library.</span></span>

<span data-ttu-id="5c614-231">開発者は、アプリケーションの要求検証を選択的にオフにする機能を頻繁に求めています。</span><span class="sxs-lookup"><span data-stu-id="5c614-231">Developers have frequently asked for the ability to selectively turn off request validation for their applications.</span></span> <span data-ttu-id="5c614-232">たとえば、アプリケーションがフォーラム ソフトウェアの場合、HTML 形式のフォーラムの投稿やコメントをユーザーに送信できるようにする一方で、要求の検証が他のすべてをチェックしていることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-232">For example, if your application is forum software, you might want to allow users to submit HTML-formatted forum posts and comments, but still make sure that request validation is checking everything else.</span></span>

<span data-ttu-id="5c614-233">ASP.NET 4.5 では、検証されていない入力を簡単に処理できる 2 つの機能が導入されています。</span><span class="sxs-lookup"><span data-stu-id="5c614-233">ASP.NET 4.5 introduces two features that make it easy for you to selectively work with unvalidated input: deferred ("lazy") request validation and access to unvalidated request data.</span></span>

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a><span data-ttu-id="5c614-234">遅延 (「遅延」) 要求の検証</span><span class="sxs-lookup"><span data-stu-id="5c614-234">Deferred ("lazy") request validation</span></span>

<span data-ttu-id="5c614-235">ASP.NET 4.5 では、デフォルトですべての要求データは要求の検証の対象となります。</span><span class="sxs-lookup"><span data-stu-id="5c614-235">In ASP.NET 4.5, by default all request data is subject to request validation.</span></span> <span data-ttu-id="5c614-236">ただし、要求データに実際にアクセスするまで要求の検証を延期するようにアプリケーションを構成できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-236">However, you can configure the application to defer request validation until you actually access request data.</span></span> <span data-ttu-id="5c614-237">(これは、特定のデータ シナリオでの遅延読み込みなどの用語に基づいて、遅延要求の検証と呼ばれることもあります)。次の例のように *、httpRUntime*要素で*requestValidationMode*属性を 4.5 に設定することで、Web.config ファイルで遅延検証を使用するようにアプリケーションを構成できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-237">(This is sometimes referred to as lazy request validation, based on terms like lazy loading for certain data scenarios.) You can configure the application to use deferred validation in the Web.config file by setting the *requestValidationMode* attribute to 4.5 in the *httpRUntime* element, as in the following example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

<span data-ttu-id="5c614-238">要求検証モードが 4.5 に設定されている場合、要求の検証は、特定の要求値に対してのみトリガーされ、コードがその値にアクセスした場合にのみトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="5c614-238">When request validation mode is set to 4.5, request validation is triggered only for a specific request value and only when your code accesses that value.</span></span> <span data-ttu-id="5c614-239">たとえば、コードが Request.Form[フォーラム\_ポスト]の値を取得した場合、要求の検証はフォーム コレクション内のその要素に対してのみ呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-239">For example, if your code gets the value of Request.Form["forum\_post"], request validation is invoked only for that element in the form collection.</span></span> <span data-ttu-id="5c614-240">*Form*コレクション内の他の要素は検証されません。</span><span class="sxs-lookup"><span data-stu-id="5c614-240">None of the other elements in the *Form* collection are validated.</span></span> <span data-ttu-id="5c614-241">以前のバージョンのASP.NETでは、コレクション内のいずれかの要素にアクセスしたときに、要求コレクション全体に対して要求の検証がトリガーされていました。</span><span class="sxs-lookup"><span data-stu-id="5c614-241">In previous versions of ASP.NET, request validation was triggered for the entire request collection when any element in the collection was accessed.</span></span> <span data-ttu-id="5c614-242">新しい動作により、異なるアプリケーション コンポーネントが、他の部分で要求の検証をトリガーしなくても、異なる要求データを簡単に確認できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-242">The new behavior makes it easier for different application components to look at different pieces of request data without triggering request validation on other pieces.</span></span>

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a><span data-ttu-id="5c614-243">未検証要求のサポート</span><span class="sxs-lookup"><span data-stu-id="5c614-243">Support for unvalidated requests</span></span>

<span data-ttu-id="5c614-244">遅延要求検証だけでは、要求検証を選択的にバイパスするという問題は解決しません。</span><span class="sxs-lookup"><span data-stu-id="5c614-244">Deferred request validation alone doesn't solve the problem of selectively bypassing request validation.</span></span> <span data-ttu-id="5c614-245">Request.Form[フォーラム\_ポスト]への呼び出しは、その特定の要求値に対する要求検証を引き起こします。</span><span class="sxs-lookup"><span data-stu-id="5c614-245">The call to Request.Form["forum\_post"] still triggers request validation for that specific request value.</span></span> <span data-ttu-id="5c614-246">ただし、そのフィールドでマークアップを許可する必要があるため、検証をトリガーせずにこのフィールドにアクセスする場合があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-246">However, you might want to access this field without triggering validation because you want to allow markup in that field.</span></span>

<span data-ttu-id="5c614-247">これを可能にするために、ASP.NET 4.5 は、データを要求する未検証アクセスをサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-247">To allow this, ASP.NET 4.5 now supports unvalidated access to request data.</span></span> <span data-ttu-id="5c614-248">ASP.NET 4.5 には *、HttpRequest*クラスに*新しい未検証*コレクション プロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="5c614-248">ASP.NET 4.5 includes a new *Unvalidated* collection property in the *HttpRequest* class.</span></span> <span data-ttu-id="5c614-249">このコレクションは、*フォーム*、*クエリ文字列*、*クッキー*、*および Url*などの要求データの一般的な値すべてにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="5c614-249">This collection provides access to all of the common values of request data, like *Form*, *QueryString*, *Cookies*, and *Url*.</span></span>

<span data-ttu-id="5c614-250">フォーラムの例を使用して、未検証の要求データを読み取ることができるように、まず、新しい要求検証モードを使用するようにアプリケーションを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-250">Using the forum example, to be able to read unvalidated request data, you first need to configure the application to use the new request validation mode:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

<span data-ttu-id="5c614-251">その後 *、HttpRequest.Unvalidated*プロパティを使用して、検証されていないフォームの値を読み取ることができます。</span><span class="sxs-lookup"><span data-stu-id="5c614-251">You can then use the *HttpRequest.Unvalidated* property to read the unvalidated form value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> <span data-ttu-id="5c614-252">セキュリティ -*検証されていない要求データを注意して使用してください!*</span><span class="sxs-lookup"><span data-stu-id="5c614-252">Security - *Use unvalidated request data with care!*</span></span> <span data-ttu-id="5c614-253">ASP.NET 4.5 では、検証されていない要求のプロパティとコレクションが追加され、非常に特定の未検証の要求データに簡単にアクセスできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-253">ASP.NET 4.5 added the unvalidated request properties and collections to make it easier for you to access very specific unvalidated request data.</span></span> <span data-ttu-id="5c614-254">ただし、危険なテキストがユーザーにレンダリングされないように、未加工の要求データに対してカスタム検証を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-254">However, you must still perform custom validation on the raw request data to ensure that dangerous text is not rendered to users.</span></span>

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a><span data-ttu-id="5c614-255">アンチXSSライブラリ</span><span class="sxs-lookup"><span data-stu-id="5c614-255">AntiXSS Library</span></span>

<span data-ttu-id="5c614-256">Microsoft AntiXSS ライブラリの人気により、ASP.NET 4.5 には、そのライブラリのバージョン 4.0 のコア エンコーディング ルーチンが組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="5c614-256">Due to the popularity of the Microsoft AntiXSS Library, ASP.NET 4.5 now incorporates core encoding routines from version 4.0 of that library.</span></span>

<span data-ttu-id="5c614-257">エンコーディング ルーチンは、新しい*名前空間*の*AntiXssEncoder*型によって実装されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-257">The encoding routines are implemented by the *AntiXssEncoder* type in the new *System.Web.Security.AntiXss* namespace.</span></span> <span data-ttu-id="5c614-258">型に実装されている任意の静的エンコーディング メソッドを呼び出すことによって *、AntiXssEncoder*型を直接使用できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-258">You can use the *AntiXssEncoder* type directly by calling any of the static encoding methods that are implemented in the type.</span></span> <span data-ttu-id="5c614-259">ただし、新しい反 XSS ルーチンを使用する最も簡単な方法は、既定で*AntiXssEncoder*クラスを使用するようにASP.NET アプリケーションを構成することです。</span><span class="sxs-lookup"><span data-stu-id="5c614-259">However, the easiest approach for using the new anti-XSS routines is to configure an ASP.NET application to use the *AntiXssEncoder* class by default.</span></span> <span data-ttu-id="5c614-260">これを行うには、Web.config ファイルに次の属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="5c614-260">To do this, add the following attribute to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

<span data-ttu-id="5c614-261">*AntiXssEncoder*型を使用するように*encoderType*属性が設定されている場合、ASP.NETのすべての出力エンコーディングは自動的に新しいエンコーディング ルーチンを使用します。</span><span class="sxs-lookup"><span data-stu-id="5c614-261">When the *encoderType* attribute is set to use the *AntiXssEncoder* type, all output encoding in ASP.NET automatically uses the new encoding routines.</span></span>

<span data-ttu-id="5c614-262">これらは、ASP.NET 4.5 に組み込まれた外部 AntiXSS ライブラリの部分です。</span><span class="sxs-lookup"><span data-stu-id="5c614-262">These are the portions of the external AntiXSS library that have been incorporated into ASP.NET 4.5:</span></span>

- <span data-ttu-id="5c614-263">*をエンコード*する 、*フォームUrl エンコード*、および*属性エンコード*</span><span class="sxs-lookup"><span data-stu-id="5c614-263">*HtmlEncode*, *HtmlFormUrlEncode*, and *HtmlAttributeEncode*</span></span>
- <span data-ttu-id="5c614-264">*エンコードと\*\*エンコード*</span><span class="sxs-lookup"><span data-stu-id="5c614-264">*XmlAttributeEncode* and *XmlEncode*</span></span>
- <span data-ttu-id="5c614-265">*Url エンコード*と*Url パスエンコード*(新しい)</span><span class="sxs-lookup"><span data-stu-id="5c614-265">*UrlEncode* and *UrlPathEncode* (new)</span></span>
- <span data-ttu-id="5c614-266">*エンコード*</span><span class="sxs-lookup"><span data-stu-id="5c614-266">*CssEncode*</span></span>

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a><span data-ttu-id="5c614-267">Web ソケット プロトコルのサポート</span><span class="sxs-lookup"><span data-stu-id="5c614-267">Support for WebSockets Protocol</span></span>

<span data-ttu-id="5c614-268">WebSockets プロトコルは、HTTP 経由でクライアントとサーバー間の安全なリアルタイム双方向通信を確立する方法を定義する標準ベースのネットワーク プロトコルです。</span><span class="sxs-lookup"><span data-stu-id="5c614-268">WebSockets protocol is a standards-based network protocol that defines how to establish secure, real-time bidirectional communications between a client and a server over HTTP.</span></span> <span data-ttu-id="5c614-269">マイクロソフトは、IETF と W3C の両方の標準機関と協力して、プロトコルの定義に役立っています。</span><span class="sxs-lookup"><span data-stu-id="5c614-269">Microsoft has worked with both the IETF and W3C standards bodies to help define the protocol.</span></span> <span data-ttu-id="5c614-270">WebSockets プロトコルは、ブラウザーだけでなく、あらゆるクライアントでサポートされており、Microsoft はクライアントとモバイルオペレーティング システムの両方で WebSockets プロトコルをサポートする相当なリソースを投資しています。</span><span class="sxs-lookup"><span data-stu-id="5c614-270">The WebSockets protocol is supported by any client (not just browsers), with Microsoft investing substantial resources supporting WebSockets protocol on both client and mobile operating systems.</span></span>

<span data-ttu-id="5c614-271">WebSockets プロトコルを使用すると、クライアントとサーバー間で長時間実行されるデータ転送を作成することがはるかに容易になります。</span><span class="sxs-lookup"><span data-stu-id="5c614-271">WebSockets protocol makes it much easier to create long-running data transfers between a client and a server.</span></span> <span data-ttu-id="5c614-272">たとえば、クライアントとサーバー間で実際の長時間接続を確立できるため、チャット アプリケーションの作成が非常に簡単になります。</span><span class="sxs-lookup"><span data-stu-id="5c614-272">For example, writing a chat application is much easier because you can establish a true long-running connection between a client and a server.</span></span> <span data-ttu-id="5c614-273">ソケットの動作をシミュレートするために、定期ポーリングや HTTP ロングポーリングなどの回避策に頼る必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5c614-273">You do not have to resort to workarounds like periodic polling or HTTP long-polling to simulate the behavior of a socket.</span></span>

<span data-ttu-id="5c614-274">ASP.NET 4.5 および IIS 8 には低レベルの WebSocket が含まれ、ASP.NET開発者は WebSockets オブジェクトで文字列データとバイナリ データの両方を非同期に読み書きするためにマネージ API を使用できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-274">ASP.NET 4.5 and IIS 8 include low-level WebSockets support, enabling ASP.NET developers to use managed APIs for asynchronously reading and writing both string and binary data on a WebSockets object.</span></span> <span data-ttu-id="5c614-275">ASP.NET 4.5 の場合、WebSockets プロトコルを操作するための型を含む新しい*System.Web.WebSockets*名前空間があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-275">For ASP.NET 4.5, there is a new *System.Web.WebSockets* namespace that contains types for working with WebSockets protocol.</span></span>

<span data-ttu-id="5c614-276">ブラウザー クライアントは、次の例のように、ASP.NET アプリケーションの URL を指す DOM WebSocket オブジェクトを作成することによって *、WebSockets*接続を確立します。</span><span class="sxs-lookup"><span data-stu-id="5c614-276">A browser client establishes a WebSockets connection by creating a DOM *WebSocket* object that points to a URL in an ASP.NET application, as in the following example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

<span data-ttu-id="5c614-277">任意の種類のモジュールまたはハンドラーを使用して、ASP.NETで WebSockets エンドポイントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-277">You can create WebSockets endpoints in ASP.NET using any kind of module or handler.</span></span> <span data-ttu-id="5c614-278">前の例では、.ashx ファイルはハンドラーを作成する簡単な方法であるため、.ashx ファイルが使用されました。</span><span class="sxs-lookup"><span data-stu-id="5c614-278">In the previous example, an .ashx file was used, because .ashx files are a quick way to create a handler.</span></span>

<span data-ttu-id="5c614-279">WebSockets プロトコルによると、ASP.NETアプリケーションは、要求を HTTP GET 要求から WebSockets 要求にアップグレードする必要があることを示すことによって、クライアントの WebSocket 要求を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="5c614-279">According to the WebSockets protocol, an ASP.NET application accepts a client's WebSockets request by indicating that the request should be upgraded from an HTTP GET request to a WebSockets request.</span></span> <span data-ttu-id="5c614-280">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="5c614-280">Here's an example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

<span data-ttu-id="5c614-281">*AcceptWebSocketRequest*メソッドは、現在の HTTP 要求をアンウィンASP.NETし、関数デリゲートに制御を転送するため、関数デリゲートを受け入れます。</span><span class="sxs-lookup"><span data-stu-id="5c614-281">The *AcceptWebSocketRequest* method accepts a function delegate because ASP.NET unwinds the current HTTP request and then transfers control to the function delegate.</span></span> <span data-ttu-id="5c614-282">概念的には、このアプローチは、バックグラウンド作業を実行するスレッド開始デリゲートを定義する*System.Threading.Thread*の使用方法に似ています。</span><span class="sxs-lookup"><span data-stu-id="5c614-282">Conceptually this approach is similar to how you use *System.Threading.Thread*, where you define a thread-start delegate in which background work is performed.</span></span>

<span data-ttu-id="5c614-283">ASP.NETし、クライアントが WebSockets ハンドシェイクを正常に完了した後、ASP.NETはデリゲートを呼び出し、WebSockets アプリケーションの実行を開始します。</span><span class="sxs-lookup"><span data-stu-id="5c614-283">After ASP.NET and the client have successfully completed a WebSockets handshake, ASP.NET calls your delegate and the WebSockets application starts running.</span></span> <span data-ttu-id="5c614-284">次のコード例は、ASP.NETでの組み込みの WebSocket サポートを使用する単純なエコー アプリケーションを示しています。</span><span class="sxs-lookup"><span data-stu-id="5c614-284">The following code example shows a simple echo application that uses the built-in WebSockets support in ASP.NET:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

<span data-ttu-id="5c614-285">*await*キーワードと非同期タスク ベースの操作に対する .NET 4.5 のサポートは、WebSockets アプリケーションを記述するのに自然に適しています。</span><span class="sxs-lookup"><span data-stu-id="5c614-285">The support in .NET 4.5 for the *await* keyword and asynchronous task-based operations is a natural fit for writing WebSockets applications.</span></span> <span data-ttu-id="5c614-286">このコード例は、WebSockets 要求がASP.NET内部で完全に非同期的に実行されることを示しています。</span><span class="sxs-lookup"><span data-stu-id="5c614-286">The code example shows that a WebSockets request runs completely asynchronously inside ASP.NET.</span></span> <span data-ttu-id="5c614-287">アプリケーションは、await ソケットを呼び出すことによって、クライアントからメッセージが送信されるのを非同期に待機*します。受信非同期*.</span><span class="sxs-lookup"><span data-stu-id="5c614-287">The application waits asynchronously for a message to be sent from a client by calling *await socket.ReceiveAsync*.</span></span> <span data-ttu-id="5c614-288">同様に、await ソケットを呼び出すことによって、非同期メッセージをクライアントに送信できます *。送信非同期*.</span><span class="sxs-lookup"><span data-stu-id="5c614-288">Similarly, you can send an asynchronous message to a client by calling *await socket.SendAsync*.</span></span>

<span data-ttu-id="5c614-289">ブラウザーでは、アプリケーションは*onmessage*関数を介して WebSockets メッセージを受信します。</span><span class="sxs-lookup"><span data-stu-id="5c614-289">In the browser, an application receives WebSockets messages through an *onmessage* function.</span></span> <span data-ttu-id="5c614-290">ブラウザーからメッセージを送信するには、次の例に示すように *、WebSocket* DOM 型の*送信*メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="5c614-290">To send a message from a browser, you call the *send* method of the *WebSocket* DOM type, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

<span data-ttu-id="5c614-291">今後、この機能の更新プログラムをリリースして、このリリースで必要な低レベルのコーディングの一部を WebSockets アプリケーション用に抽象化する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-291">In the future, we might release updates to this functionality that abstract away some of the low-level coding that is required in this release for WebSockets applications.</span></span>

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a><span data-ttu-id="5c614-292">バンドルと縮小</span><span class="sxs-lookup"><span data-stu-id="5c614-292">Bundling and Minification</span></span>

<span data-ttu-id="5c614-293">バンドルを使用すると、個々の JavaScript ファイルと CSS ファイルを 1 つのファイルのように扱うことができるバンドルに結合できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-293">Bundling lets you combine individual JavaScript and CSS files into a bundle that can be treated like a single file.</span></span> <span data-ttu-id="5c614-294">縮小は、必要のない空白文字やその他の文字を削除することで、JavaScript ファイルと CSS ファイルを縮めます。</span><span class="sxs-lookup"><span data-stu-id="5c614-294">Minification condenses JavaScript and CSS files by removing whitespace and other characters that are not required.</span></span> <span data-ttu-id="5c614-295">これらの機能は、Web フォーム、ASP.NET MVC、および Web ページで機能します。</span><span class="sxs-lookup"><span data-stu-id="5c614-295">These features work with Web Forms, ASP.NET MVC, and Web Pages.</span></span>

<span data-ttu-id="5c614-296">バンドルは、バンドルクラスまたはその子クラスの 1 つである ScriptBundle とスタイルバンドルを使用して作成されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-296">Bundles are created using the Bundle class or one of its child classes, ScriptBundle and StyleBundle.</span></span> <span data-ttu-id="5c614-297">バンドルのインスタンスを設定した後、そのバンドルはグローバル BundleCollection インスタンスに追加するだけで、受信リクエストに対して使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="5c614-297">After configuring an instance of a bundle, the bundle is made available to incoming requests by simply adding it to a global BundleCollection instance.</span></span> <span data-ttu-id="5c614-298">デフォルトテンプレートでは、バンドル構成は BundleConfig ファイルで実行されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-298">In the default templates, bundle configuration is performed in a BundleConfig file.</span></span> <span data-ttu-id="5c614-299">このデフォルト設定では、テンプレートで使用されるすべてのコアスクリプトと CSS ファイルのバンドルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-299">This default configuration creates bundles for all of the core scripts and css files used by the templates.</span></span>

<span data-ttu-id="5c614-300">バンドルは、可能ないくつかのヘルパー メソッドのいずれかを使用してビュー内から参照されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-300">Bundles are referenced from within views by using one of a couple possible helper methods.</span></span> <span data-ttu-id="5c614-301">デバッグモードとリリースモードの場合にバンドルに対して異なるマークアップをレンダリングするために、ScriptBundle クラスと StyleBundle クラスには、ヘルパー メソッド Render があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-301">In order to support rendering different markup for a bundle when in debug vs. release mode, the ScriptBundle and StyleBundle classes have the helper method, Render.</span></span> <span data-ttu-id="5c614-302">デバッグ モードの場合、Render はバンドル内の各リソースのマークアップを生成します。</span><span class="sxs-lookup"><span data-stu-id="5c614-302">When in debug mode, Render will generate markup for each resource in the bundle.</span></span> <span data-ttu-id="5c614-303">リリース モードの場合、Render はバンドル全体に対して 1 つのマークアップ要素を生成します。</span><span class="sxs-lookup"><span data-stu-id="5c614-303">When in release mode, Render will generate a single markup element for the entire bundle.</span></span> <span data-ttu-id="5c614-304">デバッグ モードとリリース モードの切り替えは、以下に示すように、web.config のコンパイル要素のデバッグ属性を変更することで実現できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-304">Toggling between debug and release mode can be accomplished by modifying the debug attribute of the compilation element in web.config as shown below:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

<span data-ttu-id="5c614-305">さらに、最適化の有効化または無効化は、バンドルテーブルを使用して直接設定できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-305">Additionally, enabling or disabling optimization can be set directly via the BundleTable.EnableOptimizations property.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

<span data-ttu-id="5c614-306">ファイルがバンドルされると、最初にアルファベット順に並べ替えられます (**ソリューション エクスプローラー**で表示される方法)。</span><span class="sxs-lookup"><span data-stu-id="5c614-306">When files are bundled, they are first sorted alphabetically (the way they are displayed in **Solution Explorer**).</span></span> <span data-ttu-id="5c614-307">次に、既知のライブラリとカスタム拡張 (jQuery、MooTools、Dojo など) が最初に読み込まれるように編成されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-307">They are then organized so that known libraries and their custom extensions (such as jQuery, MooTools, and Dojo) are loaded first.</span></span> <span data-ttu-id="5c614-308">たとえば、上記のように Scripts フォルダのバンドルの最終順序は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5c614-308">For example, the final order for the bundling of the Scripts folder as shown above will be:</span></span>

1. <span data-ttu-id="5c614-309">jquery-1.6.2.js</span><span class="sxs-lookup"><span data-stu-id="5c614-309">jquery-1.6.2.js</span></span>
2. <span data-ttu-id="5c614-310">jクエリ-ui.js</span><span class="sxs-lookup"><span data-stu-id="5c614-310">jquery-ui.js</span></span>
3. <span data-ttu-id="5c614-311">を使用します。</span><span class="sxs-lookup"><span data-stu-id="5c614-311">jquery.tools.js</span></span>
4. <span data-ttu-id="5c614-312">a.js</span><span class="sxs-lookup"><span data-stu-id="5c614-312">a.js</span></span>

<span data-ttu-id="5c614-313">CSS ファイルもアルファベット順に並べ替えられ、その後、reset.css と normalize.css が他のファイルより先に来るように再編成されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-313">CSS files are also sorted alphabetically and then reorganized so that reset.css and normalize.css come before any other file.</span></span> <span data-ttu-id="5c614-314">上記のスタイルフォルダのバンドルの最終的なソートは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="5c614-314">The final sorting of the bundling of the Styles folder shown above will be this:</span></span>

1. <span data-ttu-id="5c614-315">リセット.css</span><span class="sxs-lookup"><span data-stu-id="5c614-315">reset.css</span></span>
2. <span data-ttu-id="5c614-316">コンテンツ.css</span><span class="sxs-lookup"><span data-stu-id="5c614-316">content.css</span></span>
3. <span data-ttu-id="5c614-317">の</span><span class="sxs-lookup"><span data-stu-id="5c614-317">forms.css</span></span>
4. <span data-ttu-id="5c614-318">グローバル.css</span><span class="sxs-lookup"><span data-stu-id="5c614-318">globals.css</span></span>
5. <span data-ttu-id="5c614-319">メニュー.css</span><span class="sxs-lookup"><span data-stu-id="5c614-319">menu.css</span></span>
6. <span data-ttu-id="5c614-320">スタイル.css</span><span class="sxs-lookup"><span data-stu-id="5c614-320">styles.css</span></span>

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a><span data-ttu-id="5c614-321">Web ホスティングのパフォーマンス向上</span><span class="sxs-lookup"><span data-stu-id="5c614-321">Performance Improvements for Web Hosting</span></span>

<span data-ttu-id="5c614-322">.NET Framework 4.5 および Windows 8 では、Web サーバーのワークロードのパフォーマンスを大幅に向上させる機能が導入されています。</span><span class="sxs-lookup"><span data-stu-id="5c614-322">The .NET Framework 4.5 and Windows 8 introduce features that can help you achieve a significant performance boost for web-server workloads.</span></span> <span data-ttu-id="5c614-323">これには、削減(最大35%)が含まれます。起動時間と、ASP.NETを使用する Web ホスティング サイトのメモリフットプリントの両方で使用します。</span><span class="sxs-lookup"><span data-stu-id="5c614-323">This includes a reduction (up to 35%) in both startup time and in the memory footprint of web hosting sites that use ASP.NET.</span></span>

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a><span data-ttu-id="5c614-324">主要なパフォーマンス要因</span><span class="sxs-lookup"><span data-stu-id="5c614-324">Key performance factors</span></span>

<span data-ttu-id="5c614-325">理想的には、すべてのウェブサイトは、それが来るたびに、次の要求に迅速な応答を保証するためにアクティブで、メモリ内にあるべきです。</span><span class="sxs-lookup"><span data-stu-id="5c614-325">Ideally, all websites should be active and in memory to assure quick response to the next request, whenever it comes.</span></span> <span data-ttu-id="5c614-326">サイトの応答性に影響する要因には、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="5c614-326">Factors that can affect site responsiveness include:</span></span>

- <span data-ttu-id="5c614-327">アプリ プールのリサイクル後にサイトが再起動するまでの時間。</span><span class="sxs-lookup"><span data-stu-id="5c614-327">The time it takes for a site to restart after an app pool recycles.</span></span> <span data-ttu-id="5c614-328">これは、サイト アセンブリがメモリに存在しなくなったときに、サイトの Web サーバー プロセスを起動するのにかかる時間です。</span><span class="sxs-lookup"><span data-stu-id="5c614-328">This is the time it takes to launch a web server process for the site when the site assemblies are no longer in memory.</span></span> <span data-ttu-id="5c614-329">(プラットフォーム アセンブリは、他のサイトで使用されているため、メモリ内に残っています)。この状況は、"コールド サイト、ウォーム フレームワークスタートアップ" または単に "コールド サイトスタートアップ" と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="5c614-329">(The platform assemblies are still in memory, since they are used by other sites.) This situation is referred to as "cold site, warm framework startup" or just "cold site startup."</span></span>
- <span data-ttu-id="5c614-330">サイトが占有するメモリの量。</span><span class="sxs-lookup"><span data-stu-id="5c614-330">How much memory the site occupies.</span></span> <span data-ttu-id="5c614-331">この用語は、「サイトごとのメモリ消費量」または「共有されていないワーキング セット」です。</span><span class="sxs-lookup"><span data-stu-id="5c614-331">Terms for this are "per-site memory consumption" or "unshared working set."</span></span>

<span data-ttu-id="5c614-332">新しいパフォーマンスの向上は、これらの両方の要因に焦点を当てています。</span><span class="sxs-lookup"><span data-stu-id="5c614-332">The new performance improvements focus on both of these factors.</span></span>

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a><span data-ttu-id="5c614-333">新しいパフォーマンス機能の要件</span><span class="sxs-lookup"><span data-stu-id="5c614-333">Requirements for New Performance Features</span></span>

<span data-ttu-id="5c614-334">新機能の要件は、次のカテゴリに分類できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-334">The requirements for the new features can be broken down into these categories:</span></span>

- <span data-ttu-id="5c614-335">.NET Framework 4 で実行される機能強化。</span><span class="sxs-lookup"><span data-stu-id="5c614-335">Improvements that run on the .NET Framework 4.</span></span>
- <span data-ttu-id="5c614-336">.NET Framework 4.5 が必要ですが、どのバージョンの Windows でも実行できる機能強化。</span><span class="sxs-lookup"><span data-stu-id="5c614-336">Improvements that require the .NET Framework 4.5 but can run on any version of Windows.</span></span>
- <span data-ttu-id="5c614-337">Windows 8 で実行されている .NET Framework 4.5 でのみ使用できる機能強化。</span><span class="sxs-lookup"><span data-stu-id="5c614-337">Improvements that are available only with .NET Framework 4.5 running on Windows 8.</span></span>

<span data-ttu-id="5c614-338">パフォーマンスは、有効にできる改善のレベルごとに向上します。</span><span class="sxs-lookup"><span data-stu-id="5c614-338">Performance increases with each level of improvement that you are able to enable.</span></span>

<span data-ttu-id="5c614-339">.NET Framework 4.5 の一部の機能強化では、他のシナリオにも適用される、より広範なパフォーマンス機能を利用しています。</span><span class="sxs-lookup"><span data-stu-id="5c614-339">Some of the .NET Framework 4.5 improvements take advantage of broader performance features that apply to other scenarios as well.</span></span>

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a><span data-ttu-id="5c614-340">共通アセンブリの共有</span><span class="sxs-lookup"><span data-stu-id="5c614-340">Sharing Common Assemblies</span></span>

<span data-ttu-id="5c614-341">**要件**: .NET フレームワーク 4 および Visual Studio 11 開発者プレビュー SDK</span><span class="sxs-lookup"><span data-stu-id="5c614-341">**Requirement**: .NET Framework 4 and Visual Studio 11 Developer Preview SDK</span></span>

<span data-ttu-id="5c614-342">サーバー上の異なるサイトでは、多くの場合、同じヘルパー アセンブリ (たとえば、スタート キットやサンプル アプリケーションのアセンブリ) を使用します。</span><span class="sxs-lookup"><span data-stu-id="5c614-342">Different sites on a server often use the same helper assemblies (for example, assemblies from a starter kit or sample application).</span></span> <span data-ttu-id="5c614-343">各サイトは、Bin ディレクトリにこれらのアセンブリの独自のコピーを持っています。</span><span class="sxs-lookup"><span data-stu-id="5c614-343">Each site has its own copy of these assemblies in its Bin directory.</span></span> <span data-ttu-id="5c614-344">アセンブリのオブジェクト コードは同一ですが、アセンブリは物理的に分離されているため、コールド サイトの起動時に各アセンブリを個別に読み取り、メモリに個別に保持する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-344">Even though the object code for the assemblies is identical, they're physically separate assemblies, so each assembly has to be read separately during cold site startup and kept separately in memory.</span></span>

<span data-ttu-id="5c614-345">新しいインターン機能により、この非効率性が解消され、RAM 要件と負荷時間の両方が削減されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-345">The new interning functionality solves this inefficiency and reduces both RAM requirements and load time.</span></span> <span data-ttu-id="5c614-346">インターン化により、Windows はファイル システム内の各アセンブリの 1 つのコピーを保持し、サイトの Bin フォルダ内の個々のアセンブリは、単一のコピーへのシンボリック リンクに置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="5c614-346">Interning lets Windows keep a single copy of each assembly in the file system, and individual assemblies in the site Bin folders are replaced with symbolic links to the single copy.</span></span> <span data-ttu-id="5c614-347">個々のサイトに個別のバージョンのアセンブリが必要な場合、シンボリック リンクは新しいバージョンのアセンブリに置き換えられ、そのサイトだけが影響を受けます。</span><span class="sxs-lookup"><span data-stu-id="5c614-347">If an individual site needs a distinct version of the assembly, the symbolic link is replaced by the new version of the assembly, and only that site is affected.</span></span>

<span data-ttu-id="5c614-348">シンボリック リンクを使用してアセンブリを共有するには、aspnet\_intern.exe という名前の新しいツールが必要です。</span><span class="sxs-lookup"><span data-stu-id="5c614-348">Sharing assemblies using symbolic links requires a new tool named aspnet\_intern.exe, which lets you create and manage the store of interned assemblies.</span></span> <span data-ttu-id="5c614-349">これは、Visual Studio 11 開発者向けプレビュー SDK の一部として提供されています。</span><span class="sxs-lookup"><span data-stu-id="5c614-349">It is provided as a part of the Visual Studio 11 Developer Preview SDK.</span></span> <span data-ttu-id="5c614-350">(ただし、最新の[更新プログラム](https://support.microsoft.com/kb/2468871)をインストールしている場合は、.NET Framework 4 のみがインストールされているシステムで動作します)。</span><span class="sxs-lookup"><span data-stu-id="5c614-350">(However, it will work on a system that has only the .NET Framework 4 installed, assuming you have installed the latest [update](https://support.microsoft.com/kb/2468871).)</span></span>

<span data-ttu-id="5c614-351">対象となるすべてのアセンブリが確実にインターン化されるようにするには、aspnet\_intern.exe を定期的に実行します (たとえば、週に 1 回はスケジュールされたタスクとして実行します)。</span><span class="sxs-lookup"><span data-stu-id="5c614-351">To make sure all eligible assemblies have been interned, you run aspnet\_intern.exe periodically (for example, once a week as a scheduled task).</span></span> <span data-ttu-id="5c614-352">一般的な用途は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="5c614-352">A typical use is as follows:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

<span data-ttu-id="5c614-353">すべてのオプションを表示するには、引数を指定しないツールを実行します。</span><span class="sxs-lookup"><span data-stu-id="5c614-353">To see all options, run the tool with no arguments.</span></span>

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a><span data-ttu-id="5c614-354">マルチコア JIT コンパイルを使用して、高速なスタートアップを実現</span><span class="sxs-lookup"><span data-stu-id="5c614-354">Using multi-Core JIT compilation for faster startup</span></span>

<span data-ttu-id="5c614-355">**要件**: .NET フレームワーク 4.5</span><span class="sxs-lookup"><span data-stu-id="5c614-355">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="5c614-356">コールド サイトのスタートアップの場合、アセンブリをディスクから読み取る必要があるだけでなく、サイトを JIT コンパイルする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-356">For a cold site startup, not only do assemblies have to be read from disk, but the site must be JIT-compiled.</span></span> <span data-ttu-id="5c614-357">複雑なサイトでは、大幅な遅延が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-357">For a complex site, this can add significant delays.</span></span> <span data-ttu-id="5c614-358">.NET Framework 4.5 の新しい汎用技術により、JIT コンパイルを利用可能なプロセッサ コアに分散させることで、これらの遅延を軽減できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-358">A new general-purpose technique in the .NET Framework 4.5 reduces these delays by spreading JIT-compilation across available processor cores.</span></span> <span data-ttu-id="5c614-359">これは、サイトの以前の起動時に収集された情報を使用して、できるだけ早くこれを行います。</span><span class="sxs-lookup"><span data-stu-id="5c614-359">It does this as much and as early as possible by using information gathered during previous launches of the site.</span></span> <span data-ttu-id="5c614-360">[メソッドによって](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx)実装されるこの機能。</span><span class="sxs-lookup"><span data-stu-id="5c614-360">This functionality implemented by the [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) method.</span></span>

<span data-ttu-id="5c614-361">ASP.NETでは、複数のコアを使用した JIT コンパイルがデフォルトで有効になっているため、この機能を利用するために何もする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5c614-361">JIT-compiling using multiple cores is enabled by default in ASP.NET, so you do not need to do anything to take advantage of this feature.</span></span> <span data-ttu-id="5c614-362">この機能を無効にする場合は、Web.config ファイルで次の設定を行います。</span><span class="sxs-lookup"><span data-stu-id="5c614-362">If you want to disable this feature, make the following setting in the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a><span data-ttu-id="5c614-363">メモリ用に最適化するためのガベージ コレクションのチューニング</span><span class="sxs-lookup"><span data-stu-id="5c614-363">Tuning garbage collection to optimize for memory</span></span>

<span data-ttu-id="5c614-364">**要件**: .NET フレームワーク 4.5</span><span class="sxs-lookup"><span data-stu-id="5c614-364">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="5c614-365">サイトが実行されると、ガベージ コレクター (GC) ヒープの使用は、そのメモリ消費の重要な要因になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-365">Once a site is running, its use of the garbage-collector (GC) heap can be a significant factor in its memory consumption.</span></span> <span data-ttu-id="5c614-366">他のガベージ コレクタと同様に、.NET Framework GC は CPU 時間 (コレクションの頻度と重要度) とメモリ消費 (新しいオブジェクト、解放されたオブジェクト、または自由に使用できるオブジェクトに使用される領域の追加) との間のトレードオフを行います。</span><span class="sxs-lookup"><span data-stu-id="5c614-366">Like any garbage collector, the .NET Framework GC makes tradeoffs between CPU time (frequency and significance of collections) and memory consumption (extra space that is used for new, freed, or free-able objects).</span></span> <span data-ttu-id="5c614-367">以前のリリースでは、適切なバランスを実現するために GC を構成する方法についてのガイダンスを提供してきました (たとえば[、2.0/3.5 共有ホスティング構成ASP.NET参照](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration))。</span><span class="sxs-lookup"><span data-stu-id="5c614-367">For previous releases, we have provided guidance on how to configure the GC to achieve the right balance (for example, see [ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span></span>

<span data-ttu-id="5c614-368">NET Framework 4.5 では、複数のスタンドアロン設定ではなく、ワークロードで定義された構成設定を使用して、以前に推奨されていたすべての GC 設定と、サイトごとの作業セットに対して追加のパフォーマンスを提供する新しいチューニングを有効にできます。</span><span class="sxs-lookup"><span data-stu-id="5c614-368">For the .NET Framework 4.5, instead of multiple standalone settings, a workload-defined configuration setting is available that enables all of the previously recommended GC settings as well as new tuning that delivers additional performance for the per-site working set.</span></span>

<span data-ttu-id="5c614-369">GC メモリチューニングを有効にするには、次の設定を Windows\Net\Framework\v4.0.30319\aspnet.config ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="5c614-369">To enable GC memory tuning, add the following setting to the Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

<span data-ttu-id="5c614-370">(aspnet.config の変更に関する以前のガイダンスに慣れている場合は、この設定によって古い設定が置き換えられます。古い設定を削除する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5c614-370">(If you're familiar with the previous guidance for changes to aspnet.config, note that this setting replaces the old settings — for example, there is no need to set gcServer, gcConcurrent, etc. You do not have to remove the old settings.)</span></span>

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a><span data-ttu-id="5c614-371">Web アプリケーションのプリフェッチ</span><span class="sxs-lookup"><span data-stu-id="5c614-371">Prefetching for web applications</span></span>

<span data-ttu-id="5c614-372">**要件**: Windows 8 で実行されている .NET フレームワーク 4.5</span><span class="sxs-lookup"><span data-stu-id="5c614-372">**Requirement**: .NET Framework 4.5 running on Windows 8</span></span>

<span data-ttu-id="5c614-373">いくつかのリリースでは、Windows には[プリフェッチャー](http://en.wikipedia.org/wiki/Prefetcher)と呼ばれるテクノロジが組み込まれており、アプリケーションの起動にかかるディスク読み取りコストを削減できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-373">For several releases, Windows has included a technology known as the [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) that reduces the disk-read cost of application startup.</span></span> <span data-ttu-id="5c614-374">コールド スタートアップは主にクライアント アプリケーションの問題であるため、このテクノロジはサーバーに不可欠なコンポーネントのみを含む Windows Server には含まれていません。</span><span class="sxs-lookup"><span data-stu-id="5c614-374">Because cold startup is a problem predominantly for client applications, this technology has not been included in Windows Server, which includes only components that are essential to a server.</span></span> <span data-ttu-id="5c614-375">プリフェッチは、Windows Server の最新バージョンで利用可能になり、個々の Web サイトの起動を最適化できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-375">Prefetching is now available in the latest version of Windows Server, where it can optimize the launch of individual websites.</span></span>

<span data-ttu-id="5c614-376">Windows サーバーの場合、プリフェッチャーはデフォルトでは有効になっていません。</span><span class="sxs-lookup"><span data-stu-id="5c614-376">For Windows Server, the prefetcher is not enabled by default.</span></span> <span data-ttu-id="5c614-377">高密度 Web ホスティング用のプリフェッチャーを有効にして構成するには、コマンド・ラインで以下のコマンド・セットを実行します。</span><span class="sxs-lookup"><span data-stu-id="5c614-377">To enable and configure the prefetcher for high-density web hosting, run the following set of commands at the command line:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

<span data-ttu-id="5c614-378">次に、プリフェッチャーをASP.NETアプリケーションと統合するには、次のコードを Web.config ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="5c614-378">Then, to integrate the prefetcher with ASP.NET applications, add the following to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="5c614-379">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="5c614-379">ASP.NET Web Forms</span></span>

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a><span data-ttu-id="5c614-380">厳密に型指定されたデータ コントロール</span><span class="sxs-lookup"><span data-stu-id="5c614-380">Strongly Typed Data Controls</span></span>

<span data-ttu-id="5c614-381">ASP.NET 4.5 では、Web フォームにはデータを操作するためのいくつかの機能強化が含まれています。</span><span class="sxs-lookup"><span data-stu-id="5c614-381">In ASP.NET 4.5, Web Forms includes some improvements for working with data.</span></span> <span data-ttu-id="5c614-382">最初の改善点は、厳密に型指定されたデータ コントロールです。</span><span class="sxs-lookup"><span data-stu-id="5c614-382">The first improvement is strongly typed data controls.</span></span> <span data-ttu-id="5c614-383">以前のバージョンのASP.NETの Web フォーム コントロールの場合は *、Eval*とデータ 連結式を使用して、データ バインド値を表示します。</span><span class="sxs-lookup"><span data-stu-id="5c614-383">For Web Forms controls in previous versions of ASP.NET, you display a data-bound value using *Eval* and a data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

<span data-ttu-id="5c614-384">双方向のデータ バインディングの場合は *、Bind*を使用します。</span><span class="sxs-lookup"><span data-stu-id="5c614-384">For two-way data binding, you use *Bind*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

<span data-ttu-id="5c614-385">実行時に、これらの呼び出しは、リフレクションを使用して、指定されたメンバーの値を読み取り、その結果をマークアップに表示します。</span><span class="sxs-lookup"><span data-stu-id="5c614-385">At run time, these calls use reflection to read the value of the specified member and then display the result in the markup.</span></span> <span data-ttu-id="5c614-386">この方法により、任意の未定データに対するデータバインドが容易になります。</span><span class="sxs-lookup"><span data-stu-id="5c614-386">This approach makes it easy to data bind against arbitrary, unshaped data.</span></span>

<span data-ttu-id="5c614-387">ただし、このようなデータバインディング式は、メンバー名の IntelliSense、ナビゲーション (定義へ移動など)、コンパイル時のこれらの名前のチェックなどの機能をサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="5c614-387">However, data-binding expressions like this don't support features like IntelliSense for member names, navigation (like Go To Definition), or compile-time checking for these names.</span></span>

<span data-ttu-id="5c614-388">この問題に対処するために、ASP.NET 4.5 では、コントロールがバインドされているデータのデータ型を宣言する機能が追加されています。</span><span class="sxs-lookup"><span data-stu-id="5c614-388">To address this issue, ASP.NET 4.5 adds the ability to declare the data type of the data that a control is bound to.</span></span> <span data-ttu-id="5c614-389">これは、新しい*ItemType*プロパティを使用して行います。</span><span class="sxs-lookup"><span data-stu-id="5c614-389">You do this using the new *ItemType* property.</span></span> <span data-ttu-id="5c614-390">このプロパティを設定すると、データ バインディング式のスコープで 2 つの新しい型指定された変数を使用できます: *Item*と*BindItem*。</span><span class="sxs-lookup"><span data-stu-id="5c614-390">When you set this property, two new typed variables are available in the scope of data-binding expressions: *Item* and *BindItem*.</span></span> <span data-ttu-id="5c614-391">変数は厳密に型指定されているため、Visual Studio の開発エクスペリエンスの利点を最大限に活用できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-391">Because the variables are strongly typed, you get the full benefits of the Visual Studio development experience.</span></span>

<span data-ttu-id="5c614-392">双方向のデータ 連結式の場合は *、BindItem*変数を使用します。</span><span class="sxs-lookup"><span data-stu-id="5c614-392">For two-way data-binding expressions, use the *BindItem* variable:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

<span data-ttu-id="5c614-393">データ バインディングをサポートする ASP.NET Web フォーム フレームワークのほとんどのコントロールは *、ItemType*プロパティをサポートするように更新されました。</span><span class="sxs-lookup"><span data-stu-id="5c614-393">Most controls in the ASP.NET Web Forms framework that support data binding have been updated to support the *ItemType* property.</span></span>

<a id="_Toc318097387"></a>
### <a name="model-binding"></a><span data-ttu-id="5c614-394">モデル バインド</span><span class="sxs-lookup"><span data-stu-id="5c614-394">Model Binding</span></span>

<span data-ttu-id="5c614-395">モデル バインドは、Web フォーム コントロールASP.NETのデータ バインディングを拡張して、コードに焦点を当てたデータ アクセスを操作します。</span><span class="sxs-lookup"><span data-stu-id="5c614-395">Model binding extends data binding in ASP.NET Web Forms controls to work with code-focused data access.</span></span> <span data-ttu-id="5c614-396">このメソッドには *、ObjectDataSource*コントロールとモデル バインドの概念ASP.NET MVC に組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="5c614-396">It incorporates concepts from the *ObjectDataSource* control and from model binding in ASP.NET MVC.</span></span>

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a><span data-ttu-id="5c614-397">データの選択</span><span class="sxs-lookup"><span data-stu-id="5c614-397">Selecting data</span></span>

<span data-ttu-id="5c614-398">モデル バインドを使用してデータを選択するようにデータ コントロールを構成するには、コントロールの*SelectMethod*プロパティをページのコード内のメソッドの名前に設定します。</span><span class="sxs-lookup"><span data-stu-id="5c614-398">To configure a data control to use model binding to select data, you set the control's *SelectMethod* property to the name of a method in the page's code.</span></span> <span data-ttu-id="5c614-399">データ コントロールは、ページのライフ サイクルで適切なタイミングでメソッドを呼び出し、返されたデータを自動的にバインドします。</span><span class="sxs-lookup"><span data-stu-id="5c614-399">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="5c614-400">明示的に呼び出す必要はありません、 *DataBind*メソッドです。</span><span class="sxs-lookup"><span data-stu-id="5c614-400">There's no need to explicitly call the *DataBind* method.</span></span>

<span data-ttu-id="5c614-401">次の例では *、GetCategories*という名前のメソッドを使用するように*GridView*コントロールが構成されています。</span><span class="sxs-lookup"><span data-stu-id="5c614-401">In the following example, the *GridView* control is configured to use a method named *GetCategories*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

<span data-ttu-id="5c614-402">GetCategories*GetCategories*メソッドは、ページのコードで作成します。</span><span class="sxs-lookup"><span data-stu-id="5c614-402">You create the *GetCategories* method in the page's code.</span></span> <span data-ttu-id="5c614-403">単純な選択操作の場合、メソッドはパラメーターを必要としないし *、IEnumerable*または*IQueryable*オブジェクトを返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-403">For a simple select operation, the method needs no parameters and should return an *IEnumerable* or *IQueryable* object.</span></span> <span data-ttu-id="5c614-404">新しい*ItemType*プロパティが設定されている場合[(厳密に](#_Toc318097386)型指定されたデータ 連結式を有効にする)、これらのインターフェイスのジェネリック バージョン ( *IEnumerable&lt;&gt; T*または*IQueryable&lt;T&gt;*) が返され *、ItemType*プロパティの型に一致する*T*パラメーター (たとえば *、IQueryable&lt;Category)&gt;* が返されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-404">If the new *ItemType* property is set (which enables strongly typed data-binding expressions, as explained under [Strongly Typed Data Controls](#_Toc318097386) earlier), the generic versions of these interfaces should be returned — *IEnumerable&lt;T&gt;* or *IQueryable&lt;T&gt;*, with the *T* parameter matching the type of the *ItemType* property (for example, *IQueryable&lt;Category&gt;*).</span></span>

<span data-ttu-id="5c614-405">次の例は *、GetCategories*メソッドのコードを示しています。</span><span class="sxs-lookup"><span data-stu-id="5c614-405">The following example shows the code for a *GetCategories* method.</span></span> <span data-ttu-id="5c614-406">この例では、Northwind サンプル データベースでエンティティ フレームワーク コードファースト モデルを使用します。</span><span class="sxs-lookup"><span data-stu-id="5c614-406">This example uses the Entity Framework Code First model with the Northwind sample database.</span></span> <span data-ttu-id="5c614-407">このコードは、クエリが*Include*メソッドを使用して各カテゴリの関連製品の詳細を返すようになります。</span><span class="sxs-lookup"><span data-stu-id="5c614-407">The code makes sure that the query returns details of the related products for each category by way of the *Include* method.</span></span> <span data-ttu-id="5c614-408">(これにより、マークアップの*TemplateField*要素は[、n+1 を選択](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)しなくても、各カテゴリの製品の数を表示します。</span><span class="sxs-lookup"><span data-stu-id="5c614-408">(This ensures that the *TemplateField* element in the markup displays the count of products in each category without requiring an [n+1 select](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

<span data-ttu-id="5c614-409">ページが実行されると *、GridView*コントロールは*GetCategories*メソッドを自動的に呼び出し、構成されたフィールドを使用して返されたデータを表示します。</span><span class="sxs-lookup"><span data-stu-id="5c614-409">When the page runs, the *GridView* control calls the *GetCategories* method automatically and renders the returned data using the configured fields:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

<span data-ttu-id="5c614-410">select メソッドは*IQueryable*オブジェクトを返すため *、GridView*コントロールはクエリを実行する前に、さらに操作できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-410">Because the select method returns an *IQueryable* object, the *GridView* control can further manipulate the query before executing it.</span></span> <span data-ttu-id="5c614-411">たとえば *、GridView*コントロールは、並べ替えとページングのクエリ式を実行する前に返された*IQueryable*オブジェクトに追加できるため、これらの操作は基になる LINQ プロバイダーによって実行されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-411">For example, the *GridView* control can add query expressions for sorting and paging to the returned *IQueryable* object before it is executed, so that those operations are performed by the underlying LINQ provider.</span></span> <span data-ttu-id="5c614-412">この場合、Entity Framework は、これらの操作がデータベースで実行されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5c614-412">In this case, Entity Framework will ensure those operations are performed in the database.</span></span>

<span data-ttu-id="5c614-413">並べ替えとページングを許可するように変更された*GridView*コントロールの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="5c614-413">The following example shows the *GridView* control modified to allow sorting and paging:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

<span data-ttu-id="5c614-414">これで、ページが実行されると、コントロールは、データの現在のページのみが表示され、選択した列の順序が設定されていることを確認できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-414">Now when the page runs, the control can make sure that only the current page of data is displayed and that it's ordered by the selected column:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

<span data-ttu-id="5c614-415">返されたデータをフィルター処理するには、select メソッドにパラメーターを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-415">To filter the returned data, parameters have to be added to the select method.</span></span> <span data-ttu-id="5c614-416">これらのパラメーターは、実行時にモデル バインドによって設定され、データを返す前にクエリを変更するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-416">These parameters will be populated by the model binding at run time, and you can use them to alter the query before returning the data.</span></span>

<span data-ttu-id="5c614-417">たとえば、クエリ文字列にキーワードを入力して、ユーザーが商品をフィルター処理できるようにするとします。</span><span class="sxs-lookup"><span data-stu-id="5c614-417">For example, assume that you want to let users filter products by entering a keyword in the query string.</span></span> <span data-ttu-id="5c614-418">メソッドにパラメーターを追加し、パラメーター値を使用するようにコードを更新できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-418">You can add a parameter to the method and update the code to use the parameter value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

<span data-ttu-id="5c614-419">このコードには、*キーワード*に値が指定されている場合に*Where*式が含まれ、クエリ結果が返されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-419">This code includes a *Where* expression if a value is provided for *keyword* and then returns the query results.</span></span>

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a><span data-ttu-id="5c614-420">値プロバイダー</span><span class="sxs-lookup"><span data-stu-id="5c614-420">Value providers</span></span>

<span data-ttu-id="5c614-421">前の例は *、キーワード*パラメーターの値がどこから来ているかについては具体的ではありませんでした。</span><span class="sxs-lookup"><span data-stu-id="5c614-421">The previous example was not specific about where the value for the *keyword* parameter was coming from.</span></span> <span data-ttu-id="5c614-422">この情報を示すために、パラメーター属性を使用できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-422">To indicate this information, you can use a parameter attribute.</span></span> <span data-ttu-id="5c614-423">この例では *、名前空間\*\*にあるクラスを*使用できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-423">For this example, you can use the *QueryStringAttribute* class that's in the *System.Web.ModelBinding* namespace:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

<span data-ttu-id="5c614-424">これは、実行時にクエリ文字列から*キーワード*パラメーターに値をバインドしようとするモデル バインドを指示します。</span><span class="sxs-lookup"><span data-stu-id="5c614-424">This instructs model binding to try to bind a value from the query string to the *keyword* parameter at run time.</span></span> <span data-ttu-id="5c614-425">(この場合は型変換を実行する必要がありますが、この場合は行いません)。値を指定できず、型が null 非許容型の場合は、例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="5c614-425">(This might involve performing type conversion, although it doesn't in this case.) If a value cannot be provided and the type is non-nullable, an exception is thrown.</span></span>

<span data-ttu-id="5c614-426">これらのメソッドの値のソースは値プロバイダーと呼ばれ、使用する値プロバイダーを示すパラメーター属性は値プロバイダー属性と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="5c614-426">The sources of values for these methods are referred to as value providers, and the parameter attributes that indicate which value provider to use are referred to as value provider attributes.</span></span> <span data-ttu-id="5c614-427">Web フォームには、クエリ文字列、Cookie、フォーム値、コントロール、ビューステート、セッション状態、プロファイル プロパティなど、Web フォーム アプリケーションにおける一般的なユーザー入力ソースの値プロバイダと対応する属性が含まれます。</span><span class="sxs-lookup"><span data-stu-id="5c614-427">Web Forms will include value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="5c614-428">カスタム値プロバイダーを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="5c614-428">You can also write custom value providers.</span></span>

<span data-ttu-id="5c614-429">既定では、パラメーター名は値プロバイダー コレクション内の値を検索するキーとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-429">By default, the parameter name is used as the key to find a value in the value provider collection.</span></span> <span data-ttu-id="5c614-430">この例では、コードはキーワードという名前のクエリ文字列値を検索します (例: ~/default.aspx?キーワード=chef)。</span><span class="sxs-lookup"><span data-stu-id="5c614-430">In the example, the code will look for a query-string value named keyword (for example, ~/default.aspx?keyword=chef).</span></span> <span data-ttu-id="5c614-431">カスタム キーを引数としてパラメーター属性に渡すことによって、カスタム キーを指定できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-431">You can specify a custom key by passing it as an argument to the parameter attribute.</span></span> <span data-ttu-id="5c614-432">たとえば、q という名前のクエリ文字列変数の値を使用するには、次のようにします。</span><span class="sxs-lookup"><span data-stu-id="5c614-432">For example, to use the value of the query-string variable named q, you could do this:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

<span data-ttu-id="5c614-433">このメソッドがページのコード内にある場合、ユーザーはクエリ文字列を使用してキーワードを渡すことによって結果をフィルター処理できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-433">If this method is in the page's code, users can filter the results by passing a keyword using the query string:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

<span data-ttu-id="5c614-434">モデル バインドでは、値の読み取り、null 値のチェック、適切な型への変換、変換が成功したかどうかの確認、およびクエリ内の値の使用など、手作業でコーディングする必要がある多くのタスクが実行されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-434">Model binding accomplishes many tasks that you would otherwise have to code by hand: reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="5c614-435">モデル バインドの結果、コードが非常に少なくなり、アプリケーション全体で機能を再利用できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-435">Model binding results in far less code and in the ability to reuse the functionality throughout your application.</span></span>

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a><span data-ttu-id="5c614-436">コントロールの値によるフィルター処理</span><span class="sxs-lookup"><span data-stu-id="5c614-436">Filtering by values from a control</span></span>

<span data-ttu-id="5c614-437">例を拡張して、ユーザーがドロップダウン リストからフィルター値を選択できるようにするとします。</span><span class="sxs-lookup"><span data-stu-id="5c614-437">Suppose you want to extend the example to let the user choose a filter value from a drop-down list.</span></span> <span data-ttu-id="5c614-438">次のドロップダウン リストをマークアップに追加し *、SelectMethod*プロパティを使用して別のメソッドからデータを取得するように構成します。</span><span class="sxs-lookup"><span data-stu-id="5c614-438">Add the following drop-down list to the markup and configure it to get its data from another method using the *SelectMethod* property:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

<span data-ttu-id="5c614-439">通常は、一致する製品が見つからない場合にコントロールにメッセージを表示するように *、GridView*コントロールに*空のデータ テンプレート*要素も追加します。</span><span class="sxs-lookup"><span data-stu-id="5c614-439">Typically you would also add an *EmptyDataTemplate* element to the *GridView* control so that the control will display a message if no matching products are found:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

<span data-ttu-id="5c614-440">ページ コードで、ドロップダウン リストの新しい select メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="5c614-440">In the page code, add the new select method for the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

<span data-ttu-id="5c614-441">最後に *、GetProducts*の選択メソッドを更新して、ドロップダウン リストから選択したカテゴリの ID を含む新しいパラメーターを取得します。</span><span class="sxs-lookup"><span data-stu-id="5c614-441">Finally, update the *GetProducts* select method to take a new parameter that contains the ID of the selected category from the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

<span data-ttu-id="5c614-442">ページが実行されると、ユーザーはドロップダウン リストからカテゴリを選択でき *、GridView*コントロールは自動的に再バインドされ、フィルター処理されたデータが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-442">Now when the page runs, users can select a category from the drop-down list, and the *GridView* control is automatically re-bound to show the filtered data.</span></span> <span data-ttu-id="5c614-443">モデル バインドは、選択メソッドのパラメーターの値を追跡し、ポストバック後にパラメーター値が変更されたかどうかを検出するためです。</span><span class="sxs-lookup"><span data-stu-id="5c614-443">This is possible because model binding tracks the values of parameters for select methods and detects whether any parameter value has changed after a postback.</span></span> <span data-ttu-id="5c614-444">その場合、モデル バインドは、関連付けられたデータ コントロールを強制的にデータにバインドします。</span><span class="sxs-lookup"><span data-stu-id="5c614-444">If so, model binding forces the associated data control to re-bind to the data.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a><span data-ttu-id="5c614-445">HTML エンコードされたデータ バインディング式</span><span class="sxs-lookup"><span data-stu-id="5c614-445">HTML Encoded Data-Binding Expressions</span></span>

<span data-ttu-id="5c614-446">データ 連結式の結果を HTML エンコードできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-446">You can now HTML-encode the result of data-binding expressions.</span></span> <span data-ttu-id="5c614-447">コロンを追加する (:)データ バインディング式を&lt;マークする %# プレフィックスの末尾に次の値を指定します。</span><span class="sxs-lookup"><span data-stu-id="5c614-447">Add a colon (:) to the end of the &lt;%# prefix that marks the data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a><span data-ttu-id="5c614-448">控えめな検証</span><span class="sxs-lookup"><span data-stu-id="5c614-448">Unobtrusive Validation</span></span>

<span data-ttu-id="5c614-449">クライアント側の検証ロジックに控えめな JavaScript を使用するように、組み込みの検証コントロールを構成できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-449">You can now configure the built-in validator controls to use unobtrusive JavaScript for client-side validation logic.</span></span> <span data-ttu-id="5c614-450">これにより、ページ マークアップでインライン表示される JavaScript の量が大幅に減少し、ページ全体のサイズが小さくなります。</span><span class="sxs-lookup"><span data-stu-id="5c614-450">This significantly reduces the amount of JavaScript rendered inline in the page markup and reduces the overall page size.</span></span> <span data-ttu-id="5c614-451">バリデータ コントロールの控えめな JavaScript を構成するには、次のいずれかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-451">You can configure unobtrusive JavaScript for validator controls in any of these ways:</span></span>

- <span data-ttu-id="5c614-452">Web.config ファイルの*&lt;appSettings&gt;* 要素に次の設定を追加してグローバルに実行します。</span><span class="sxs-lookup"><span data-stu-id="5c614-452">Globally by adding the following setting to the *&lt;appSettings&gt;* element in the Web.config file:</span></span> 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- <span data-ttu-id="5c614-453">静的な*System.Web.UI.ValidationSettings.UnobsiveValidationMode*プロパティを*控えめな検証モードに*設定することでグローバルに (通常、Global.asax ファイルの*アプリケーション\_開始*メソッドで)。</span><span class="sxs-lookup"><span data-stu-id="5c614-453">Globally by setting the static *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* property to *UnobtrusiveValidationMode.WebForms* (typically in the *Application\_Start* method in the Global.asax file).</span></span>
- <span data-ttu-id="5c614-454">*ページ*クラスの新しい*UnobtrusiveValidationMode*プロパティを *[控えめな検証モード]* に設定してページを個別に指定します。</span><span class="sxs-lookup"><span data-stu-id="5c614-454">Individually for a page by setting the new *UnobtrusiveValidationMode* property of the *Page* class to *UnobtrusiveValidationMode.WebForms*.</span></span>

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a><span data-ttu-id="5c614-455">HTML5 の更新プログラム</span><span class="sxs-lookup"><span data-stu-id="5c614-455">HTML5 Updates</span></span>

<span data-ttu-id="5c614-456">HTML5 の新機能を利用するために、Web フォーム サーバー コントロールに対していくつかの改良が加えられた。</span><span class="sxs-lookup"><span data-stu-id="5c614-456">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>

- <span data-ttu-id="5c614-457">*TextBox*コントロールの*TextMode*プロパティは、*電子メール*、*日時*などの新しい HTML5 入力タイプをサポートするように更新されました。</span><span class="sxs-lookup"><span data-stu-id="5c614-457">The *TextMode* property of the *TextBox* control has been updated to support the new HTML5 input types like *email*, *datetime*, and so on.</span></span>
- <span data-ttu-id="5c614-458">*FileUpload*コントロールは、この HTML5 機能をサポートするブラウザーからの複数のファイルアップロードをサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-458">The *FileUpload* control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
- <span data-ttu-id="5c614-459">検証コントロールで HTML5 入力要素の検証がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-459">Validator controls now support validating HTML5 input elements.</span></span>
- <span data-ttu-id="5c614-460">URL を表す属性を持つ新しい HTML5 要素は、runat="サーバー" をサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-460">New HTML5 elements that have attributes that represent a URL now support runat="server".</span></span> <span data-ttu-id="5c614-461">その結果、アプリケーションルートを表す ~ 演算子のように、URL パスでASP.NET規約を使用できます (たとえば、&lt;ビデオ runat="サーバー" src="~/myVideo.wmv" /&gt;)。</span><span class="sxs-lookup"><span data-stu-id="5c614-461">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat="server" src="~/myVideo.wmv" /&gt;).</span></span>
- <span data-ttu-id="5c614-462">*UPDATEPanel*コントロールは、HTML5 入力フィールドの投稿をサポートするように修正されました。</span><span class="sxs-lookup"><span data-stu-id="5c614-462">The *UpdatePanel* control has been fixed to support posting HTML5 input fields.</span></span>

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a><span data-ttu-id="5c614-463">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="5c614-463">ASP.NET MVC 4</span></span>

<span data-ttu-id="5c614-464">ASP.NET MVC 4 ベータ版は、Visual Studio 11 ベータ版に含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-464">ASP.NET MVC 4 Beta is now included with Visual Studio 11 Beta.</span></span> <span data-ttu-id="5c614-465">ASP.NETMVCは、モデル ビュー コントローラー (MVC) パターンを活用して、高度にテスト可能で保守が容易な Web アプリケーションを開発するためのフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="5c614-465">ASP.NET MVC is a framework for developing highly testable and maintainable Web applications by leveraging the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="5c614-466">ASP.NET MVC 4 では、モバイル Web 用のアプリケーションを簡単に構築でき、任意のデバイスにアクセスできる HTTP サービスを構築するのに役立つ ASP.NET Web API が含まれています。</span><span class="sxs-lookup"><span data-stu-id="5c614-466">ASP.NET MVC 4 makes it easy to build applications for the mobile Web and includes ASP.NET Web API, which helps you build HTTP services that can reach any device.</span></span> <span data-ttu-id="5c614-467">詳細については、「 mvc [4 リリース ノートASP.NET](mvc4-release-notes.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c614-467">For more information, see the [ASP.NET MVC 4 Release Notes](mvc4-release-notes.md).</span></span>

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a><span data-ttu-id="5c614-468">ASP.NET Web ページ 2</span><span class="sxs-lookup"><span data-stu-id="5c614-468">ASP.NET Web Pages 2</span></span>

<span data-ttu-id="5c614-469">新機能には、次のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="5c614-469">New features include the following:</span></span>

- <span data-ttu-id="5c614-470">新しいサイト テンプレートと更新されたサイト テンプレート。</span><span class="sxs-lookup"><span data-stu-id="5c614-470">New and updated site templates.</span></span>
- <span data-ttu-id="5c614-471">検証ヘルパーを使用してサーバー側およびクライアント側の*検証*を追加します。</span><span class="sxs-lookup"><span data-stu-id="5c614-471">Adding server-side and client-side validation using the *Validation* helper.</span></span>
- <span data-ttu-id="5c614-472">アセットマネージャーを使用してスクリプトを登録する機能。</span><span class="sxs-lookup"><span data-stu-id="5c614-472">The ability to register scripts using an assets manager.</span></span>
- <span data-ttu-id="5c614-473">OAuth と OpenID を使用して、Facebook やその他のサイトからのログインを有効にします。</span><span class="sxs-lookup"><span data-stu-id="5c614-473">Enabling logins from Facebook and other sites using OAuth and OpenID.</span></span>
- <span data-ttu-id="5c614-474">マップ ヘルパーを使用して*マップ*を追加します。</span><span class="sxs-lookup"><span data-stu-id="5c614-474">Adding maps using the *Maps* helper.</span></span>
- <span data-ttu-id="5c614-475">Web ページ アプリケーションを並べて実行する。</span><span class="sxs-lookup"><span data-stu-id="5c614-475">Running Web Pages applications side-by-side.</span></span>
- <span data-ttu-id="5c614-476">モバイル デバイス用のページのレンダリング。</span><span class="sxs-lookup"><span data-stu-id="5c614-476">Rendering pages for mobile devices.</span></span>

<span data-ttu-id="5c614-477">これらの機能と全ページのコード例の詳細については、「 [Web ページ 2 のトップ機能 」](https://go.microsoft.com/fwlink/?LinkID=227824)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c614-477">For more information about these features and full-page code examples, see [The Top Features in Web Pages 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).</span></span>

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a><span data-ttu-id="5c614-478">ビジュアルウェブ開発者 11 ベータ版</span><span class="sxs-lookup"><span data-stu-id="5c614-478">Visual Web Developer 11 Beta</span></span>

<span data-ttu-id="5c614-479">このセクションでは、Web 開発の改善について説明します 11 ベータ版と Visual Studio 2012 リリース候補の Web 開発します。</span><span class="sxs-lookup"><span data-stu-id="5c614-479">This section provides information about improvements for web development in Visual Web Developer 11 Beta and Visual Studio 2012 Release Candidate.</span></span>

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a><span data-ttu-id="5c614-480">Visual Studio 2010 と Visual Studio 2012 リリース候補との間のプロジェクト共有 (プロジェクトの互換性)</span><span class="sxs-lookup"><span data-stu-id="5c614-480">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>

<span data-ttu-id="5c614-481">Visual Studio 2012 リリース候補まで、Visual Studio の新しいバージョンで既存のプロジェクトを開くと、変換ウィザードが起動しました。</span><span class="sxs-lookup"><span data-stu-id="5c614-481">Until Visual Studio 2012 Release Candidate, opening an existing project in a newer version of Visual Studio launched the Conversion Wizard.</span></span> <span data-ttu-id="5c614-482">これにより、プロジェクトのコンテンツ (資産) とソリューションを、下位互換性のない新しい形式にアップグレードする必要がありました。</span><span class="sxs-lookup"><span data-stu-id="5c614-482">This forced an upgrade of the content (assets) of a project and solution to new formats that were not backward compatible.</span></span> <span data-ttu-id="5c614-483">したがって、変換後は、Visual Studio の古いバージョンでプロジェクトを開くことができなかった。</span><span class="sxs-lookup"><span data-stu-id="5c614-483">Therefore, after the conversion you could not open the project in the older version of Visual Studio.</span></span>

<span data-ttu-id="5c614-484">多くのお客様は、これが正しいアプローチではないと私たちに言いました。</span><span class="sxs-lookup"><span data-stu-id="5c614-484">Many customers have told us that this was not the right approach.</span></span> <span data-ttu-id="5c614-485">Visual Studio 11 ベータ版では、Visual Studio 2010 SP1 を使用したプロジェクトとソリューションの共有をサポートするようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-485">In Visual Studio 11 Beta, we now support sharing projects and solutions with Visual Studio 2010 SP1.</span></span> <span data-ttu-id="5c614-486">つまり、Visual Studio 2012 リリース候補で 2010 プロジェクトを開く場合でも、Visual Studio 2010 SP1 でプロジェクトを開くことができることを意味します。</span><span class="sxs-lookup"><span data-stu-id="5c614-486">This means that if you open a 2010 project in Visual Studio 2012 Release Candidate, you will still be able to open the project in Visual Studio 2010 SP1.</span></span>

> [!NOTE]
> <span data-ttu-id="5c614-487">いくつかの種類のプロジェクトは、Visual Studio 2010 SP1 と Visual Studio 2012 リリース候補の間で共有することはできません。</span><span class="sxs-lookup"><span data-stu-id="5c614-487">A few types of projects cannot be shared between Visual Studio 2010 SP1 and Visual Studio 2012 Release Candidate.</span></span> <span data-ttu-id="5c614-488">これには、古いプロジェクト (MVC 2 ASP.NET プロジェクトなど) や特別な目的 (セットアップ プロジェクトなど) 用のプロジェクトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5c614-488">These include some older projects (such as ASP.NET MVC 2 projects) or projects for special purposes (such as Setup projects).</span></span>

<span data-ttu-id="5c614-489">Visual Studio 11 ベータ版で初めて Visual Studio 2010 SP1 Web プロジェクトを開くと、次のプロパティがプロジェクト ファイルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-489">When you open a Visual Studio 2010 SP1 Web project for the first time in Visual Studio 11 Beta, the following properties are added to the project file:</span></span>

- <span data-ttu-id="5c614-490">ファイルアップグレードフラグ</span><span class="sxs-lookup"><span data-stu-id="5c614-490">FileUpgradeFlags</span></span>
- <span data-ttu-id="5c614-491">アップグレードバックアップロケーション</span><span class="sxs-lookup"><span data-stu-id="5c614-491">UpgradeBackupLocation</span></span>
- <span data-ttu-id="5c614-492">オールドツールバージョン</span><span class="sxs-lookup"><span data-stu-id="5c614-492">OldToolsVersion</span></span>
- <span data-ttu-id="5c614-493">VisualStudioVersion</span><span class="sxs-lookup"><span data-stu-id="5c614-493">VisualStudioVersion</span></span>
- <span data-ttu-id="5c614-494">ツールパス</span><span class="sxs-lookup"><span data-stu-id="5c614-494">VSToolsPath</span></span>

<span data-ttu-id="5c614-495">プロジェクト ファイルをアップグレードするプロセスでは、アップグレードフラグ、アップグレードバックアップロケーション、およびオールドツールバージョンが使用されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-495">FileUpgradeFlags, UpgradeBackupLocation, and OldToolsVersion are used by the process that upgrades the project file.</span></span> <span data-ttu-id="5c614-496">Visual Studio 2010 でのプロジェクトの操作に影響はありません。</span><span class="sxs-lookup"><span data-stu-id="5c614-496">They have no impact on working with the project in Visual Studio 2010.</span></span>

<span data-ttu-id="5c614-497">現在のプロジェクトの Visual Studio のバージョンを示す MSBuild 4.5 で使用される新しいプロパティです。</span><span class="sxs-lookup"><span data-stu-id="5c614-497">VisualStudioVersion is a new property used by MSBuild 4.5 that indicates the version of Visual Studio for the current project.</span></span> <span data-ttu-id="5c614-498">このプロパティは MSBuild 4.0 (Visual Studio 2010 SP1 で使用される MSBuild のバージョン) には存在しないため、プロジェクト ファイルに既定値を挿入します。</span><span class="sxs-lookup"><span data-stu-id="5c614-498">Because this property didn't exist in MSBuild 4.0 (the version of MSBuild that Visual Studio 2010 SP1 uses), we inject a default value into the project file.</span></span>

<span data-ttu-id="5c614-499">プロパティは、MSBuildExtensionsPath32 設定で表されるパスからインポートする正しい .targets ファイルを決定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-499">The VSToolsPath property is used to determine the correct .targets file to import from the path represented by the MSBuildExtensionsPath32 setting.</span></span>

<span data-ttu-id="5c614-500">また、インポート要素に関連するいくつかの変更もあります。</span><span class="sxs-lookup"><span data-stu-id="5c614-500">There are also some changes related to Import elements.</span></span> <span data-ttu-id="5c614-501">これらの変更は、Visual Studio の両方のバージョン間の互換性をサポートするために必要です。</span><span class="sxs-lookup"><span data-stu-id="5c614-501">These changes are required in order to support compatibility between both versions of Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="5c614-502">プロジェクトが 2 つの異なるコンピューターで Visual Studio 2010 SP1 と Visual Studio 11 Beta の間で\_共有されている場合、およびプロジェクトにアプリケーション データ フォルダーにローカル データベースが含まれている場合は、データベースで使用される SQL Server のバージョンが両方のコンピューターにインストールされていることを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-502">If a project is being shared between Visual Studio 2010 SP1 and Visual Studio 11 Beta on two different computers, and if the project includes a local database in the App\_Data folder, you must make sure that the version of SQL Server used by the database is installed on both computers.</span></span>

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a><span data-ttu-id="5c614-503">ASP.NET 4.5 Web サイト テンプレートの設定変更</span><span class="sxs-lookup"><span data-stu-id="5c614-503">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>

<span data-ttu-id="5c614-504">Visual Studio 2012 リリース候補の Web サイト テンプレートを使用して作成されたサイトの既定の*Web.config*ファイルに対して、次の変更が行われました。</span><span class="sxs-lookup"><span data-stu-id="5c614-504">The following changes have been made to the default *Web.config* file for site that are created using website templates in Visual Studio 2012 Release Candidate:</span></span>

- <span data-ttu-id="5c614-505">`<httpRuntime>`要素では、`encoderType`属性が既定で設定され、ASP.NETに追加された AntiXSS 型が使用されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-505">In the `<httpRuntime>` element, the `encoderType` attribute is now set by default to use the AntiXSS types that were added to ASP.NET.</span></span> <span data-ttu-id="5c614-506">詳細については[、AntiXSS ライブラリを](#_Toc318097382)参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c614-506">For details, see [AntiXSS Library](#_Toc318097382).</span></span>
- <span data-ttu-id="5c614-507">また、`<httpRuntime>`要素では、`requestValidationMode`属性は「4.5」に設定されています。</span><span class="sxs-lookup"><span data-stu-id="5c614-507">Also in the `<httpRuntime>` element, the `requestValidationMode` attribute is set to "4.5".</span></span> <span data-ttu-id="5c614-508">これは、既定では、要求の検証は遅延 ("遅延") 検証を使用するように構成されていることを意味します。</span><span class="sxs-lookup"><span data-stu-id="5c614-508">This means that by default, request validation is configured to use deferred ("lazy") validation.</span></span> <span data-ttu-id="5c614-509">詳細については、「[新しいASP.NET要求検証機能](#_Toc318097379)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c614-509">For details, see [New ASP.NET Request Validation Features](#_Toc318097379).</span></span>
- <span data-ttu-id="5c614-510">セクション`<modules>`の要素に`<system.webServer>`属性が`runAllManagedModulesForAllRequests`含まれていません。</span><span class="sxs-lookup"><span data-stu-id="5c614-510">The `<modules>` element of the `<system.webServer>` section does not contain a `runAllManagedModulesForAllRequests` attribute.</span></span> <span data-ttu-id="5c614-511">(既定値は false です)。つまり、SP1 に更新されていないバージョンの IIS 7 を使用している場合、新しいサイトでのルーティングに問題がある可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-511">(Its default value is false.) This means that if you are using a version of IIS 7 that has not been updated to SP1, you might have issues with routing in a new site.</span></span> <span data-ttu-id="5c614-512">詳細については、「 [IIS 7 でのASP.NET ルーティングのネイティブ サポート](#Native_Support_In_IIS7_For_ASPNET_Routine)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c614-512">For more information, see [Native Support in IIS 7 for ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine).</span></span>

<span data-ttu-id="5c614-513">これらの変更は、既存のアプリケーションには影響しません。</span><span class="sxs-lookup"><span data-stu-id="5c614-513">These changes do not affect existing applications.</span></span> <span data-ttu-id="5c614-514">ただし、既存の Web サイトと、新しいテンプレートを使用して ASP.NET 4.5 用に作成した新しい Web サイトとの動作の違いを表している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-514">However, they might represent a difference in behavior between existing websites and new websites that you create for ASP.NET 4.5 using the new templates.</span></span>

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a><span data-ttu-id="5c614-515">IIS 7 でのASP.NET ルーティングのネイティブ サポート</span><span class="sxs-lookup"><span data-stu-id="5c614-515">Native Support in IIS 7 for ASP.NET Routing</span></span>

<span data-ttu-id="5c614-516">これは、ASP.NETに対する変更ではなく、SP1 更新プログラムが適用されていない IIS 7 のバージョンを使用している場合に影響を与える可能性のある、新しい Web サイト プロジェクトのテンプレートの変更です。</span><span class="sxs-lookup"><span data-stu-id="5c614-516">This is not a change to ASP.NET as such, but a change in templates for new website projects that can affect you if you are working a version of IIS 7 that has not had the SP1 update applied.</span></span>

<span data-ttu-id="5c614-517">ASP.NETでは、ルーティングをサポートするために、アプリケーションに次の構成設定を追加できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-517">In ASP.NET, you can add the following configuration setting to applications in order to support routing:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

<span data-ttu-id="5c614-518">**runAllManagedModulesForAllRequests**が true の場合`http://mysite/myapp/home`、URL に *.aspx* *、.mvc、* または同様の拡張子がない場合でも、URL のような URL はASP.NETに行きます。</span><span class="sxs-lookup"><span data-stu-id="5c614-518">When **runAllManagedModulesForAllRequests** is true, a URL like `http://mysite/myapp/home` goes to ASP.NET, even though there is no *.aspx*, *.mvc*, or similar extension on the URL.</span></span>

<span data-ttu-id="5c614-519">IIS 7 に対して行われた更新により **、runAllManagedModulesForAllRequests**設定は不要になり、ネイティブでASP.NET ルーティングをサポートします。</span><span class="sxs-lookup"><span data-stu-id="5c614-519">An update that was made to IIS 7 makes the **runAllManagedModulesForAllRequests** setting unnecessary and supports ASP.NET routing natively.</span></span> <span data-ttu-id="5c614-520">(更新プログラムの詳細については、「Microsoft サポート技術情報」を参照してください特定[の IIS 7.0 または IIS 7.5 ハンドラーが、URL がピリオドで終わる要求を処理できる更新プログラム](https://support.microsoft.com/kb/980368)です。</span><span class="sxs-lookup"><span data-stu-id="5c614-520">(For information about the update, see the Microsoft Support article [An update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).)</span></span>

<span data-ttu-id="5c614-521">Web サイトが IIS 7 で実行されており、IIS が更新されている場合は **、runAllManagedModulesForAllRequests**を true に設定する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5c614-521">If your website is running on IIS 7 and if IIS has been updated, you do not need to set **runAllManagedModulesForAllRequests** to true.</span></span> <span data-ttu-id="5c614-522">実際には、要求に不要な処理オーバーヘッドが追加されるため、true に設定することはお勧めしません。</span><span class="sxs-lookup"><span data-stu-id="5c614-522">In fact, setting it to true is not recommended, because it adds unnecessary processing overhead to request.</span></span> <span data-ttu-id="5c614-523">この設定が true の場合 *、.htm* *、.jpg、* およびその他の静的ファイルを含むすべての要求も、ASP.NET要求パイプラインを通過します。</span><span class="sxs-lookup"><span data-stu-id="5c614-523">When this setting is true, all requests, including those for *.htm*, *.jpg*, and other static files, also go through the ASP.NET request pipeline.</span></span>

<span data-ttu-id="5c614-524">Visual Studio 2012 RC で提供されるテンプレートを使用して新しい ASP.NET 4.5 Web サイトを作成する場合、Web サイトの構成には**runAllManagedModulesForAllRequests**設定は含まれません。</span><span class="sxs-lookup"><span data-stu-id="5c614-524">If you create a new ASP.NET 4.5 website using the templates that are provided in Visual Studio 2012 RC, the configuration for the website does not include the **runAllManagedModulesForAllRequests** setting.</span></span> <span data-ttu-id="5c614-525">これは、デフォルトでは設定が false であることを意味します。</span><span class="sxs-lookup"><span data-stu-id="5c614-525">This means that by default the setting is false.</span></span>

<span data-ttu-id="5c614-526">SP1 がインストールされていない Windows 7 で Web サイトを実行すると、IIS 7 には必要な更新プログラムは含まれません。</span><span class="sxs-lookup"><span data-stu-id="5c614-526">If you then run the website on Windows 7 without SP1 installed, IIS 7 will not include the required update.</span></span> <span data-ttu-id="5c614-527">その結果、ルーティングは機能せず、エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-527">As a consequence, routing will not work and you will see errors.</span></span> <span data-ttu-id="5c614-528">ルーティングが機能しない問題が発生した場合は、次のいずれかの操作を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="5c614-528">If you have a problem where routing does not work, you can do either the following:</span></span>

- <span data-ttu-id="5c614-529">Windows 7 を SP1 に更新し、IIS 7 に更新プログラムを追加します。</span><span class="sxs-lookup"><span data-stu-id="5c614-529">Update Windows 7 to SP1, which will add the update to IIS 7.</span></span>
- <span data-ttu-id="5c614-530">上記のマイクロソフト サポート資料に記載されている更新プログラムをインストールします。</span><span class="sxs-lookup"><span data-stu-id="5c614-530">Install the update that's described in the Microsoft Support article listed previously.</span></span>
- <span data-ttu-id="5c614-531">その Web サイトの Web.config ファイルで **、runAllManagedModulesForAllRequests**を true に設定します。</span><span class="sxs-lookup"><span data-stu-id="5c614-531">Set **runAllManagedModulesForAllRequests** to true in that website's Web.config file.</span></span> <span data-ttu-id="5c614-532">これは、要求に多少のオーバーヘッドを追加することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="5c614-532">Note that this will add some overhead to requests.</span></span>

<a id="_Toc318097397"></a>
### <a name="html-editor"></a><span data-ttu-id="5c614-533">HTML エディター</span><span class="sxs-lookup"><span data-stu-id="5c614-533">HTML Editor</span></span>

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a><span data-ttu-id="5c614-534">スマートタスク</span><span class="sxs-lookup"><span data-stu-id="5c614-534">Smart Tasks</span></span>

<span data-ttu-id="5c614-535">デザイン ビューでは、サーバー コントロールの複雑なプロパティには、ダイアログ ボックスやウィザードが関連付けられていることが多く、設定が容易になります。</span><span class="sxs-lookup"><span data-stu-id="5c614-535">In Design view, complex properties of server controls often have associated dialog boxes and wizards to make it easy to set them.</span></span> <span data-ttu-id="5c614-536">たとえば、特別なダイアログ ボックスを使用して、データ ソースを*Repeater*コントロールに追加したり *、GridView*コントロールに列を追加したりできます。</span><span class="sxs-lookup"><span data-stu-id="5c614-536">For example, you can use a special dialog box to add a data source to a *Repeater* control or add columns to a *GridView* control.</span></span>

<span data-ttu-id="5c614-537">ただし、複雑なプロパティのこの種類の UI ヘルプは、ソース ビューでは使用できません。</span><span class="sxs-lookup"><span data-stu-id="5c614-537">However, this type of UI help for complex properties has not been available in Source view.</span></span> <span data-ttu-id="5c614-538">したがって、Visual Studio 11 では、ソース ビューのスマート タスクが導入されています。</span><span class="sxs-lookup"><span data-stu-id="5c614-538">Therefore, Visual Studio 11 introduces Smart Tasks for Source view.</span></span> <span data-ttu-id="5c614-539">スマート タスクは、C# および Visual Basic エディターで一般的に使用される機能のコンテキスト対応のショートカットです。</span><span class="sxs-lookup"><span data-stu-id="5c614-539">Smart Tasks are context-aware shortcuts for commonly used features in the C# and Visual Basic editors.</span></span>

<span data-ttu-id="5c614-540">Web フォーム コントロールASP.NETの場合、スマート タスクは、要素内にカーソルがあるときに、サーバー タグに小さなグリフとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-540">For ASP.NET Web Forms controls, Smart Tasks appear on server tags as a small glyph when the insertion point is inside the element:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

<span data-ttu-id="5c614-541">スマート タスクは、グリフをクリックするか、Ctrl キーを押しながら押すと展開されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-541">The Smart Task expands when you click the glyph or press CTRL+.</span></span> <span data-ttu-id="5c614-542">(ドット)、コード エディターと同じように。</span><span class="sxs-lookup"><span data-stu-id="5c614-542">(dot), just as in the code editors.</span></span> <span data-ttu-id="5c614-543">デザイン ビューのスマート タスクに似たショートカットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-543">It then displays shortcuts that are similar to the Smart Tasks in Design view.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

<span data-ttu-id="5c614-544">たとえば、前の図のスマート タスクは、GridView タスク オプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="5c614-544">For example, the Smart Task in the previous illustration shows the GridView Tasks options.</span></span> <span data-ttu-id="5c614-545">[列を編集]を選択すると、次のダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-545">If you choose Edit Columns, the following dialog box is displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

<span data-ttu-id="5c614-546">ダイアログ ボックスに入力すると、デザイン ビューで設定できるプロパティと同じプロパティが設定されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-546">Filling in the dialog box sets the same properties you can set in Design view.</span></span> <span data-ttu-id="5c614-547">[OK] をクリックすると、コントロールのマークアップが新しい設定で更新されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-547">When you click OK, the markup for the control is updated with the new settings:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a><span data-ttu-id="5c614-548">ワイアリアサポート</span><span class="sxs-lookup"><span data-stu-id="5c614-548">WAI-ARIA support</span></span>

<span data-ttu-id="5c614-549">アクセス可能なウェブサイトを書くことはますます重要になっています。</span><span class="sxs-lookup"><span data-stu-id="5c614-549">Writing accessible websites is becoming increasingly important.</span></span> <span data-ttu-id="5c614-550">[WAI-ARIA アクセシビリティ標準](http://www.w3.org/WAI/intro/aria)は、開発者がアクセシビリティ対応のウェブサイトを作成する方法を定義します。</span><span class="sxs-lookup"><span data-stu-id="5c614-550">The [WAI-ARIA accessibility standard](http://www.w3.org/WAI/intro/aria) defines how developers should write accessible websites.</span></span> <span data-ttu-id="5c614-551">この標準は、Visual Studio で完全にサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-551">This standard is now fully supported in Visual Studio.</span></span>

<span data-ttu-id="5c614-552">たとえば、*ロール*属性に完全な IntelliSense が追加されました。</span><span class="sxs-lookup"><span data-stu-id="5c614-552">For example, the *role* attribute now has full IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

<span data-ttu-id="5c614-553">WAI-ARIA 標準では、HTML5 ドキュメントにセマンティクスを追加できる*aria という*プレフィックスが付いた属性も導入されています。</span><span class="sxs-lookup"><span data-stu-id="5c614-553">The WAI-ARIA standard also introduces attributes that are prefixed with *aria-* that let you add semantics to an HTML5 document.</span></span> <span data-ttu-id="5c614-554">Visual Studio では、次の*アリア*属性も完全にサポートされています。</span><span class="sxs-lookup"><span data-stu-id="5c614-554">Visual Studio also fully supports these *aria-* attributes:</span></span>

<span data-ttu-id="5c614-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="5c614-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span></span>

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a><span data-ttu-id="5c614-556">新しい HTML5 スニペット</span><span class="sxs-lookup"><span data-stu-id="5c614-556">New HTML5 snippets</span></span>

<span data-ttu-id="5c614-557">一般的に使用される HTML5 マークアップを簡単に作成できるように、Visual Studio には多数のスニペットが用意されています。</span><span class="sxs-lookup"><span data-stu-id="5c614-557">To make it faster and easier to write commonly used HTML5 markup, Visual Studio includes a number of snippets.</span></span> <span data-ttu-id="5c614-558">例として、ビデオ スニペットがあります。</span><span class="sxs-lookup"><span data-stu-id="5c614-558">An example is the video snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

<span data-ttu-id="5c614-559">スニペットを呼び出すには、IntelliSense で要素が選択されたときに Tab キーを 2 回押します。</span><span class="sxs-lookup"><span data-stu-id="5c614-559">To invoke the snippet, press Tab twice when the element is selected in IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

<span data-ttu-id="5c614-560">これにより、カスタマイズできるスニペットが生成されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-560">This produces a snippet that you can customize.</span></span>

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a><span data-ttu-id="5c614-561">ユーザー コントロールに抽出する</span><span class="sxs-lookup"><span data-stu-id="5c614-561">Extract to user control</span></span>

<span data-ttu-id="5c614-562">大規模な Web ページでは、個々の部分をユーザー コントロールに移動することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5c614-562">In large web pages, it can be a good idea to move individual pieces into user controls.</span></span> <span data-ttu-id="5c614-563">この形式のリファクタリングは、ページの読みやすさを向上させ、ページ構造を簡略化するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="5c614-563">This form of refactoring can help increase the readability of the page and can simplify the page structure.</span></span>

<span data-ttu-id="5c614-564">このことを簡単にするため、ソース ビューで Web フォーム ページを編集するときに、ページ内のテキストを選択して右クリックし、[ユーザーコントロールに抽出] を選択します。</span><span class="sxs-lookup"><span data-stu-id="5c614-564">To make this easier, when you edit Web Forms pages in Source view, you can now select text in a page, right-click it, and then choose Extract to User Control:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a><span data-ttu-id="5c614-565">属性内のコード ナゲットの IntelliSense</span><span class="sxs-lookup"><span data-stu-id="5c614-565">IntelliSense for code nuggets in attributes</span></span>

<span data-ttu-id="5c614-566">Visual Studio は、すべてのページまたはコントロールでサーバー側コード ナゲット用の IntelliSense を常に提供してきました。</span><span class="sxs-lookup"><span data-stu-id="5c614-566">Visual Studio has always provided IntelliSense for server-side code nuggets in any page or control.</span></span> <span data-ttu-id="5c614-567">現在、Visual Studio には、HTML 属性のコード ナゲット用 IntelliSense も含まれています。</span><span class="sxs-lookup"><span data-stu-id="5c614-567">Now Visual Studio includes IntelliSense for code nuggets in HTML attributes as well.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

<span data-ttu-id="5c614-568">これにより、データ 連結式を簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-568">This makes it easier to create data-binding expressions:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a><span data-ttu-id="5c614-569">開始タグまたは終了タグの名前を変更すると、一致するタグの名前が自動的に変更される</span><span class="sxs-lookup"><span data-stu-id="5c614-569">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>

<span data-ttu-id="5c614-570">HTML 要素の名前を変更すると (*たとえば、div*タグを*ヘッダー*タグに変更した場合)、対応する開始タグまたは終了タグもリアルタイムで変更されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-570">If you rename an HTML element (for example, you change a *div* tag to be a *header* tag), the corresponding opening or closing tag also changes in real time.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

<span data-ttu-id="5c614-571">これは、終了タグを変更したり、間違ったタグを変更するのを忘れた場合のエラーを回避するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="5c614-571">This helps avoid the error where you forget to change a closing tag or change the wrong one.</span></span>

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a><span data-ttu-id="5c614-572">イベント ハンドラの生成</span><span class="sxs-lookup"><span data-stu-id="5c614-572">Event handler generation</span></span>

<span data-ttu-id="5c614-573">Visual Studio には、ソース ビューにイベント ハンドラーを記述して手動でバインドするための機能が含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-573">Visual Studio now includes features in Source view to help you write event handlers and bind them manually.</span></span> <span data-ttu-id="5c614-574">ソース ビューでイベント名を編集している場合、IntelliSense&lt;は 、&gt;正しいシグネチャを持つページのコードにイベント ハンドラーを作成する新しいイベントの作成を表示します。</span><span class="sxs-lookup"><span data-stu-id="5c614-574">If you are editing an event name in Source view, IntelliSense displays &lt;Create New Event&gt;, which will create an event handler in the page's code that has the right signature:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

<span data-ttu-id="5c614-575">既定では、イベント ハンドラーは、イベント処理メソッドの名前にコントロールの ID を使用します。</span><span class="sxs-lookup"><span data-stu-id="5c614-575">By default, the event handler will use the control's ID for the name of the event-handling method:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

<span data-ttu-id="5c614-576">結果のイベント ハンドラーは次のようになります (この場合は C# で)。</span><span class="sxs-lookup"><span data-stu-id="5c614-576">The resulting event handler will look like this (in this case, in C#):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a><span data-ttu-id="5c614-577">スマートインデント</span><span class="sxs-lookup"><span data-stu-id="5c614-577">Smart indent</span></span>

<span data-ttu-id="5c614-578">空の HTML 要素の中で Enter キーを押すと、エディターは挿入ポイントを適切な場所に置きます。</span><span class="sxs-lookup"><span data-stu-id="5c614-578">When you press Enter while inside an empty HTML element, the editor will put the insertion point in the right place:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

<span data-ttu-id="5c614-579">この位置で Enter キーを押すと、終了タグが下に移動され、開始タグと一致するようにインデントされます。</span><span class="sxs-lookup"><span data-stu-id="5c614-579">If you press Enter in this location, the closing tag is moved down and indented to match the opening tag.</span></span> <span data-ttu-id="5c614-580">挿入ポイントもインデントされます。</span><span class="sxs-lookup"><span data-stu-id="5c614-580">The insertion point is also indented:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="5c614-581">ステートメントの自動削減入力</span><span class="sxs-lookup"><span data-stu-id="5c614-581">Auto-reduce statement completion</span></span>

<span data-ttu-id="5c614-582">Visual Studio の IntelliSense リストは、入力内容に基づいてフィルター処理されるようになったので、関連するオプションのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-582">The IntelliSense list in Visual Studio now filters based on what you type so that it displays only relevant options:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

<span data-ttu-id="5c614-583">また、IntelliSense リスト内の個々の単語のタイトルの大文字と小文字に基づいてフィルター処理を行います。</span><span class="sxs-lookup"><span data-stu-id="5c614-583">IntelliSense also filters based on the title case of the individual words in the IntelliSense list.</span></span> <span data-ttu-id="5c614-584">たとえば、"dl" と入力すると、dl と asp:DataList の両方が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-584">For example, if you type "dl", both dl and asp:DataList are displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

<span data-ttu-id="5c614-585">この機能を使用すると、既知の要素のステートメント補完を取得する時間が短縮されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-585">This feature makes it faster to get statement completion for known elements.</span></span>

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a><span data-ttu-id="5c614-586">JavaScript エディター</span><span class="sxs-lookup"><span data-stu-id="5c614-586">JavaScript Editor</span></span>

<span data-ttu-id="5c614-587">Visual Studio 2012 リリース候補の JavaScript エディターは完全に新しいものであり、Visual Studio での JavaScript の操作のエクスペリエンスを大幅に向上させます。</span><span class="sxs-lookup"><span data-stu-id="5c614-587">The JavaScript editor in Visual Studio 2012 Release Candidate is completely new and it greatly improves the experience of working with JavaScript in Visual Studio.</span></span>

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a><span data-ttu-id="5c614-588">コードのアウトライン表示</span><span class="sxs-lookup"><span data-stu-id="5c614-588">Code outlining</span></span>

<span data-ttu-id="5c614-589">すべての関数に対してアウトライン領域が自動的に作成されるようになり、現在のフォーカスに関連しないファイルの一部を折りたたむようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-589">Outlining regions are now automatically created for all functions, allowing you to collapse parts of the file that aren't pertinent to your current focus.</span></span>

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a><span data-ttu-id="5c614-590">かっこの一致</span><span class="sxs-lookup"><span data-stu-id="5c614-590">Brace matching</span></span>

<span data-ttu-id="5c614-591">左または右中かっこにカーソルを置くと、対応するカーソルが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-591">When you put the insertion point on an opening or closing brace, the editor highlights the matching one.</span></span>

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a><span data-ttu-id="5c614-592">定義へ移動</span><span class="sxs-lookup"><span data-stu-id="5c614-592">Go to Definition</span></span>

<span data-ttu-id="5c614-593">[定義へ移動] コマンドを使用すると、関数または変数のソースにジャンプできます。</span><span class="sxs-lookup"><span data-stu-id="5c614-593">The Go to Definition command lets you jump to the source for a function or variable.</span></span>

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a><span data-ttu-id="5c614-594">ECMAスクリプト5サポート</span><span class="sxs-lookup"><span data-stu-id="5c614-594">ECMAScript5 support</span></span>

<span data-ttu-id="5c614-595">エディターは、JavaScript 言語を記述する標準の最新バージョンである ECMAScript5 の新しい構文と API をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="5c614-595">The editor supports the new syntax and APIs in ECMAScript5, the latest version of the standard that describes the JavaScript language.</span></span>

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a><span data-ttu-id="5c614-596">ドム インテライセンス</span><span class="sxs-lookup"><span data-stu-id="5c614-596">DOM IntelliSense</span></span>

<span data-ttu-id="5c614-597">DOM API 用 IntelliSense は、*クエリセレクタ*、DOM ストレージ、クロスドキュメント メッセージング、*キャンバス*など、多くの新しい HTML5 API をサポートし、改善されました。</span><span class="sxs-lookup"><span data-stu-id="5c614-597">IntelliSense for DOM APIs has been improved, with support for many new HTML5 APIs including *querySelector*, DOM Storage, cross-document messaging, and *canvas*.</span></span> <span data-ttu-id="5c614-598">DOM IntelliSense は、ネイティブ タイプ ライブラリ定義ではなく、単一の単純な JavaScript ファイルによって駆動されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-598">DOM IntelliSense is now driven by a single simple JavaScript file, rather than by a native type library definition.</span></span> <span data-ttu-id="5c614-599">これにより、拡張または置換が容易になります。</span><span class="sxs-lookup"><span data-stu-id="5c614-599">This makes it easy to extend or replace.</span></span>

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a><span data-ttu-id="5c614-600">VSDOC シグネチャのオーバーロード</span><span class="sxs-lookup"><span data-stu-id="5c614-600">VSDOC signature overloads</span></span>

<span data-ttu-id="5c614-601">次の例に示すように、新しい*&lt;シグネチャ&gt;* 要素を使用して、JavaScript 関数の個別のオーバーロードに対して詳細な IntelliSense コメントを宣言できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-601">Detailed IntelliSense comments can now be declared for separate overloads of JavaScript functions by using the new *&lt;signature&gt;* element, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a><span data-ttu-id="5c614-602">暗黙的な参照</span><span class="sxs-lookup"><span data-stu-id="5c614-602">Implicit references</span></span>

<span data-ttu-id="5c614-603">JavaScript ファイルを中央のリストに追加し、そのファイルのリストに暗黙的に含めることができるので、その内容は IntelliSense で取得できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-603">You can now add JavaScript files to a central list that will be implicitly included in the list of files that any given JavaScript file or block references, meaning you'll get IntelliSense for its contents.</span></span> <span data-ttu-id="5c614-604">たとえば、jQuery ファイルをファイルの中央のリストに追加すると、明示的に参照したかどうかにかかわらず(///&lt;参照/&gt;を使用して)、ファイルの任意の JavaScript ブロック内の jQuery 関数の IntelliSense を取得できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-604">For example, you can add jQuery files to the central list of files, and you'll get IntelliSense for jQuery functions in any JavaScript block of file, whether you've referenced it explicitly (using /// &lt;reference /&gt;) or not.</span></span>

<a id="_Toc318097415"></a>
### <a name="css-editor"></a><span data-ttu-id="5c614-605">CSS エディター</span><span class="sxs-lookup"><span data-stu-id="5c614-605">CSS Editor</span></span>

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="5c614-606">ステートメントの自動削減入力</span><span class="sxs-lookup"><span data-stu-id="5c614-606">Auto-reduce statement completion</span></span>

<span data-ttu-id="5c614-607">CSS の IntelliSense リストは、選択したスキーマでサポートされている CSS プロパティと値に基づいてフィルター処理されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-607">The IntelliSense list for CSS now filters based on the CSS properties and values supported by the selected schema.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

<span data-ttu-id="5c614-608">IntelliSense では、タイトルケース検索もサポートしています。</span><span class="sxs-lookup"><span data-stu-id="5c614-608">IntelliSense also supports title case searches:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a><span data-ttu-id="5c614-609">階層インデント</span><span class="sxs-lookup"><span data-stu-id="5c614-609">Hierarchical indentation</span></span>

<span data-ttu-id="5c614-610">CSS エディタではインデントを使用して階層的なルールを表示し、カスケードルールの論理的な編成方法の概要を示します。</span><span class="sxs-lookup"><span data-stu-id="5c614-610">The CSS editor uses indentation to display hierarchical rules, which gives you an overview of how the cascading rules are logically organized.</span></span> <span data-ttu-id="5c614-611">次の例では、セレクター#listはリストのカスケード子であり、インデントされます。</span><span class="sxs-lookup"><span data-stu-id="5c614-611">In the following example, the #list a selector is a cascading child of list and is therefore indented.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

<span data-ttu-id="5c614-612">次の例は、より複雑な継承を示しています。</span><span class="sxs-lookup"><span data-stu-id="5c614-612">The following example shows more complex inheritance:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

<span data-ttu-id="5c614-613">規則のインデントは、その親規則によって決まります。</span><span class="sxs-lookup"><span data-stu-id="5c614-613">The indentation of a rule is determined by its parent rules.</span></span> <span data-ttu-id="5c614-614">階層インデントは既定で有効になっていますが、[オプション] ダイアログ ボックス (メニュー バーの [ツール]、[ オプション] ) を無効にできます。</span><span class="sxs-lookup"><span data-stu-id="5c614-614">Hierarchical indentation is enabled by default, but you can disable it the Options dialog box (Tools, Options from the menu bar):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a><span data-ttu-id="5c614-615">CSS ハックのサポート</span><span class="sxs-lookup"><span data-stu-id="5c614-615">CSS hacks support</span></span>

<span data-ttu-id="5c614-616">何百もの実世界の CSS ファイルを分析すると、CSS のハッキングは非常に一般的であり、現在 Visual Studio は最も広く使用されているファイルをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="5c614-616">Analysis of hundreds of real-world CSS files shows that CSS hacks are very common, and now Visual Studio supports the most widely used ones.</span></span> <span data-ttu-id="5c614-617">このサポートには、IntelliSense と星形の\*検証 (\_) とアンダースコア ( ) プロパティ のハックが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5c614-617">This support includes IntelliSense and validation of the star (\*) and underscore (\_) property hacks:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

<span data-ttu-id="5c614-618">一般的なセレクターハックもサポートされているため、適用しても階層インデントが維持されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-618">Typical selector hacks are also supported so that hierarchical indentation is maintained even when they are applied.</span></span> <span data-ttu-id="5c614-619">Internet Explorer 7 をターゲットにするための一般的なセレクタ ハックは、セレクタの先頭に*\*:first-child + html*を付ける方法です。</span><span class="sxs-lookup"><span data-stu-id="5c614-619">A typical selector hack used to target Internet Explorer 7 is to prepend a selector with *\*:first-child + html*.</span></span> <span data-ttu-id="5c614-620">このルールを使用すると、階層インデントが維持されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-620">Using that rule will maintain the hierarchical indentation:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a><span data-ttu-id="5c614-621">ベンダー固有のスキーマ (-moz-, -webkit)</span><span class="sxs-lookup"><span data-stu-id="5c614-621">Vendor specific schemas (-moz-, -webkit)</span></span>

<span data-ttu-id="5c614-622">CSS3 では、さまざまな時間に異なるブラウザーによって実装された多くのプロパティが導入されています。</span><span class="sxs-lookup"><span data-stu-id="5c614-622">CSS3 introduces many properties that have been implemented by different browsers at different times.</span></span> <span data-ttu-id="5c614-623">以前は、開発者はベンダ固有の構文を使用して、特定のブラウザー用のコードを作成する必要が出ていた。</span><span class="sxs-lookup"><span data-stu-id="5c614-623">This previously forced developers to code for specific browsers by using vendor-specific syntax.</span></span> <span data-ttu-id="5c614-624">これらのブラウザー固有のプロパティは、IntelliSense に含まれるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-624">These browser-specific properties are now included in IntelliSense.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a><span data-ttu-id="5c614-625">コメントとコメント解除のサポート</span><span class="sxs-lookup"><span data-stu-id="5c614-625">Commenting and uncommenting support</span></span>

<span data-ttu-id="5c614-626">コード エディターで使用するのと同じショートカット (Ctrl+ K、C をコメントに、Ctrl + K キーを押してコメントを解除する) を使用して CSS ルールをコメント化したり、コメントを解除したりできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-626">You can now comment and uncomment CSS rules using the same shortcuts that you use in the code editor (Ctrl+K,C to comment and Ctrl+K,U to uncomment).</span></span>

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a><span data-ttu-id="5c614-627">Color picker</span><span class="sxs-lookup"><span data-stu-id="5c614-627">Color picker</span></span>

<span data-ttu-id="5c614-628">以前のバージョンの Visual Studio では、色に関連する属性の IntelliSense は、名前付きの色の値のドロップダウン リストで構成されていました。</span><span class="sxs-lookup"><span data-stu-id="5c614-628">In previous versions of Visual Studio, IntelliSense for color-related attributes consisted of a drop-down list of named color values.</span></span> <span data-ttu-id="5c614-629">このリストは、フル機能のカラー ピッカーに置き換えられました。</span><span class="sxs-lookup"><span data-stu-id="5c614-629">That list has been replaced by a full-featured color picker.</span></span>

<span data-ttu-id="5c614-630">カラー値を入力すると、カラー ピッカーが自動的に表示され、以前に使用した色のリストと、その後に既定のカラー パレットが表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-630">When you enter a color value, the color picker is displayed automatically and presents a list of previously used colors followed by a default color palette.</span></span> <span data-ttu-id="5c614-631">マウスまたはキーボードを使用して色を選択できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-631">You can select a color using the mouse or the keyboard.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

<span data-ttu-id="5c614-632">リストは、完全なカラーピッカーに拡張できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-632">The list can be expanded into a complete color picker.</span></span> <span data-ttu-id="5c614-633">ピッカーでは、不透明度スライダを移動すると、色を RGBA に自動的に変換してアルファ チャンネルを制御できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-633">The picker lets you control the alpha channel by automatically converting any color into RGBA when you move the opacity slider:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a><span data-ttu-id="5c614-634">スニペット</span><span class="sxs-lookup"><span data-stu-id="5c614-634">Snippets</span></span>

<span data-ttu-id="5c614-635">CSS エディタのスニペットを使用すると、クロスブラウザ スタイルを簡単かつ迅速に作成できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-635">Snippets in the CSS editor make it easier and faster to create cross-browser styles.</span></span> <span data-ttu-id="5c614-636">ブラウザー固有の設定を必要とする多くの CSS3 プロパティは、スニペットにロールされています。</span><span class="sxs-lookup"><span data-stu-id="5c614-636">Many CSS3 properties that require browser-specific settings have now been rolled into snippets.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

<span data-ttu-id="5c614-637">CSS スニペットは、IntelliSense リストを示すアットマーク (@)を入力することで、高度なシナリオ (CSS3 メディア クエリなど) をサポートします。</span><span class="sxs-lookup"><span data-stu-id="5c614-637">CSS snippets support advanced scenarios (like CSS3 media queries) by typing the at-symbol (@), which shows the IntelliSense list.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

<span data-ttu-id="5c614-638">値を選択@mediaして Tab キーを押すと、CSS エディターによって次のスニペットが挿入されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-638">When you select @media value and press Tab, the CSS editor inserts the following snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

<span data-ttu-id="5c614-639">コードのスニペットと同様に、独自の CSS スニペットを作成できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-639">As with snippets for code, you can create your own CSS snippets.</span></span>

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a><span data-ttu-id="5c614-640">カスタム領域</span><span class="sxs-lookup"><span data-stu-id="5c614-640">Custom regions</span></span>

<span data-ttu-id="5c614-641">コード エディターで既に使用できる名前付きコード領域が、CSS 編集で使用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-641">Named code regions, which are already available in the code editor, are now available for CSS editing.</span></span> <span data-ttu-id="5c614-642">これにより、関連するスタイル ブロックを簡単にグループ化できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-642">This lets you easily group related style blocks.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

<span data-ttu-id="5c614-643">領域が折りたたまれている場合、領域の名前が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-643">When a region is collapsed it displays the name of the region:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a><span data-ttu-id="5c614-644">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="5c614-644">Page Inspector</span></span>

<span data-ttu-id="5c614-645">ページ インスペクターは、Visual Studio IDE で Web ページ (HTML、Web フォーム、ASP.NET MVC、または Web ページ) をレンダリングし、ソース コードと結果の出力の両方を確認できるツールです。</span><span class="sxs-lookup"><span data-stu-id="5c614-645">Page Inspector is a tool that renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) in the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="5c614-646">ページインスペクタでは、ASP.NETページのページインスペクターを使用して、ブラウザにレンダリングされる HTML マークアップを生成したサーバー側コードを特定できます。</span><span class="sxs-lookup"><span data-stu-id="5c614-646">For ASP.NET pages, Page Inspector lets you determine which server-side code has produced the HTML markup that is rendered to the browser.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

<span data-ttu-id="5c614-647">ページインスペクターの詳細については、次のチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c614-647">For more information about Page Inspector, please see the following tutorials:</span></span>

- <span data-ttu-id="5c614-648">[ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)でのページ インスペクターの使用</span><span class="sxs-lookup"><span data-stu-id="5c614-648">Using Page Inspector in [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span></span>
- <span data-ttu-id="5c614-649">Web フォームでのページインスペクタ[ASP.NET使用](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span><span class="sxs-lookup"><span data-stu-id="5c614-649">Using Page Inspector in [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span></span>

<a id="_Toc318097425"></a>
### <a name="publishing"></a><span data-ttu-id="5c614-650">置換</span><span class="sxs-lookup"><span data-stu-id="5c614-650">Publishing</span></span>

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a><span data-ttu-id="5c614-651">発行プロファイル</span><span class="sxs-lookup"><span data-stu-id="5c614-651">Publish profiles</span></span>

<span data-ttu-id="5c614-652">Visual Studio 2010 では、Web アプリケーション プロジェクトの発行情報はバージョン管理に格納されず、他のユーザーと共有するためのものではありません。</span><span class="sxs-lookup"><span data-stu-id="5c614-652">In Visual Studio 2010, publishing information for Web application projects is not stored in version control and is not designed for sharing with others.</span></span> <span data-ttu-id="5c614-653">Visual Studio 2012 リリース候補では、発行プロファイルの形式が変更されました。</span><span class="sxs-lookup"><span data-stu-id="5c614-653">In Visual Studio 2012 Release Candidate, the format of the publish profile has been changed.</span></span> <span data-ttu-id="5c614-654">チームアーティファクトが作成され、MSBuild に基づくビルドから簡単に活用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-654">It has been made a team artifact, and it is now easy to leverage from builds based on MSBuild.</span></span> <span data-ttu-id="5c614-655">ビルド構成情報は[発行]ダイアログ ボックスにあり、発行前にビルド構成を簡単に切り替えることができます。</span><span class="sxs-lookup"><span data-stu-id="5c614-655">Build configuration information is in the Publish dialog box so that you can easily switch build configurations before publishing.</span></span>

<span data-ttu-id="5c614-656">発行プロファイルは、発行プロファイル フォルダーに格納されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-656">Publish profiles are stored in the PublishProfiles folder.</span></span> <span data-ttu-id="5c614-657">フォルダの場所は、使用しているプログラミング言語によって異なります。</span><span class="sxs-lookup"><span data-stu-id="5c614-657">The location of the folder depends on what programming language you are using:</span></span>

- <span data-ttu-id="5c614-658">C#: プロパティ\発行プロファイル</span><span class="sxs-lookup"><span data-stu-id="5c614-658">C#: Properties\PublishProfiles</span></span>
- <span data-ttu-id="5c614-659">ビジュアル ベーシック: マイ プロジェクト\発行プロファイル</span><span class="sxs-lookup"><span data-stu-id="5c614-659">Visual Basic: My Project\PublishProfiles</span></span>

<span data-ttu-id="5c614-660">各プロファイルは MSBuild ファイルです。</span><span class="sxs-lookup"><span data-stu-id="5c614-660">Each profile is an MSBuild file.</span></span> <span data-ttu-id="5c614-661">発行中に、このファイルはプロジェクトの MSBuild ファイルにインポートされます。</span><span class="sxs-lookup"><span data-stu-id="5c614-661">During publishing, this file is imported into the project's MSBuild file.</span></span> <span data-ttu-id="5c614-662">Visual Studio 2010 では、発行プロセスまたはパッケージ プロセスに変更を加える場合は **、ProjectName**.wpp.targets という名前のファイルにカスタマイズを配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-662">In Visual Studio 2010, if you want to make changes to the publish or package process, you have to put your customizations in a file named **ProjectName**.wpp.targets.</span></span> <span data-ttu-id="5c614-663">これは引き続きサポートされていますが、カスタマイズを発行プロファイル自体に配置できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-663">This is still supported, but you can now put your customizations in the publish profile itself.</span></span> <span data-ttu-id="5c614-664">これにより、カスタマイズはそのプロファイルにのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="5c614-664">That way, the customizations will be used only for that profile.</span></span>

<span data-ttu-id="5c614-665">MSBuild の発行プロファイルを利用できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-665">You can now also leverage publish profiles from MSBuild.</span></span> <span data-ttu-id="5c614-666">これを行うには、プロジェクトをビルドするときに次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="5c614-666">To do so, use the following command when you build the project:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

<span data-ttu-id="5c614-667">project.csproj 値はプロジェクトのパスであり、プロファイル名はパブリッシュするプロファイルの名前です。</span><span class="sxs-lookup"><span data-stu-id="5c614-667">The project.csproj value is the path of the project, and ProfileName is the name of the profile to publish.</span></span> <span data-ttu-id="5c614-668">または *、PublishProfile*プロパティのプロファイル名を渡す代わりに、発行プロファイルへの完全パスを渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="5c614-668">Alternatively, instead of passing the profile name for the *PublishProfile* property, you can pass in the full path to the publish profile.</span></span>

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a><span data-ttu-id="5c614-669">プリコンパイルとマージのASP.NET</span><span class="sxs-lookup"><span data-stu-id="5c614-669">ASP.NET precompilation and merge</span></span>

<span data-ttu-id="5c614-670">Web アプリケーション プロジェクトの場合、Visual Studio 2012 リリース候補は、プロジェクトを発行またはパッケージ化するときにサイトのコンテンツをプリコンパイルし、マージできる [パッケージ/発行 Web プロパティ] ページにオプションを追加します。</span><span class="sxs-lookup"><span data-stu-id="5c614-670">For Web application projects, Visual Studio 2012 Release Candidate adds an option on the Package/Publish Web properties page that lets you precompile and merge your site's content when you publish or package the project.</span></span> <span data-ttu-id="5c614-671">これらのオプションを表示するには、ソリューション エクスプローラーでプロジェクトを右クリックし、[プロパティ] を選択して、[パッケージ化/発行 Web] プロパティ ページを選択します。</span><span class="sxs-lookup"><span data-stu-id="5c614-671">To see these options, right-click the project in Solution Explorer, choose Properties, and then choose the Package/Publish Web property page.</span></span> <span data-ttu-id="5c614-672">次の図は、[このアプリケーションを公開前にプリコンパイルする] オプションを示しています。</span><span class="sxs-lookup"><span data-stu-id="5c614-672">The following illustration shows the Precompile this application before publishing option.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

<span data-ttu-id="5c614-673">このオプションを選択すると、Web アプリケーションを発行またはパッケージ化するたびに、Visual Studio によってアプリケーションがプリコンパイルされます。</span><span class="sxs-lookup"><span data-stu-id="5c614-673">When this option is selected, Visual Studio precompiles the application whenever you publish or package the web application.</span></span> <span data-ttu-id="5c614-674">サイトのプリコンパイル方法やアセンブリのマージ方法を制御する場合は、[詳細設定] ボタンをクリックしてこれらのオプションを構成します。</span><span class="sxs-lookup"><span data-stu-id="5c614-674">If you want to control how the site is precompiled or how assemblies are merged, click the Advanced button to configure those options.</span></span>

<a id="_Toc318097428"></a>
### <a name="iis-express"></a><span data-ttu-id="5c614-675">IIS Express</span><span class="sxs-lookup"><span data-stu-id="5c614-675">IIS Express</span></span>

<span data-ttu-id="5c614-676">Visual Studio で Web プロジェクトをテストするための既定の Web サーバーが IIS エクスプレスになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-676">The default web server for testing web projects in Visual Studio is now IIS Express.</span></span> <span data-ttu-id="5c614-677">開発中のローカル Web サーバーの場合は、Visual Studio 開発サーバーが依然としてオプションですが、IIS Express が推奨されるサーバーになりました。</span><span class="sxs-lookup"><span data-stu-id="5c614-677">The Visual Studio Development Server is still an option for local web server during development, but IIS Express is now the recommended server.</span></span> <span data-ttu-id="5c614-678">Visual Studio 11 ベータ版で IIS エクスプレスを使用するエクスペリエンスは、Visual Studio 2010 SP1 での使用と非常によく似ています。</span><span class="sxs-lookup"><span data-stu-id="5c614-678">The experience of using IIS Express in Visual Studio 11 Beta is very similar to using it in Visual Studio 2010 SP1.</span></span>

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a><span data-ttu-id="5c614-679">免責事項</span><span class="sxs-lookup"><span data-stu-id="5c614-679">Disclaimer</span></span>

<span data-ttu-id="5c614-680">このドキュメントは暫定版であり、ここで説明するソフトウェアの最終的な商業リリースより前に大幅に変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-680">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="5c614-681">このドキュメントに含まれる情報は、取り上げている問題についての、公開時点における Microsoft Corporation の見解を表します。</span><span class="sxs-lookup"><span data-stu-id="5c614-681">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="5c614-682">Microsoft は変化する市場状況に対応する必要があるため、これを Microsoft による確約と解釈しないでください。Microsoft は、記載されている情報の公開後の正確さを保証できません。</span><span class="sxs-lookup"><span data-stu-id="5c614-682">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="5c614-683">このホワイト ペーパーは、情報提供のみを目的としています。</span><span class="sxs-lookup"><span data-stu-id="5c614-683">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="5c614-684">マイクロソフトは、このドキュメント内の情報に関して、明示的、暗黙的、または法的ないかなる保証も行いません。</span><span class="sxs-lookup"><span data-stu-id="5c614-684">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="5c614-685">お客様ご自身の責任において、適用されるすべての著作権関連法規に従ったご使用を願います。</span><span class="sxs-lookup"><span data-stu-id="5c614-685">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="5c614-686">このソフトウェアおよびマニュアルのいかなる部分も、米国 Microsoft Corporation の書面による許諾を受けることなく、その目的を問わず、どのような形態であっても、複製または譲渡することは禁じられています。ここでいう形態とは、複写や記録など、電子的な、または物理的なすべての手段を含みます。</span><span class="sxs-lookup"><span data-stu-id="5c614-686">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="5c614-687">Microsoft は、このマニュアルに記載されている内容に関し、特許、特許申請、商標、著作権、またはその他の無体財産権を有する場合があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-687">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="5c614-688">別途マイクロソフトのライセンス契約上に明示の規定がない限り、このドキュメントはこれらの特許、商標、著作権、またはその他の無体財産権に関する権利をお客様に許諾するものではありません。</span><span class="sxs-lookup"><span data-stu-id="5c614-688">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="5c614-689">特に記載されていない限り、ここに記載されている会社、組織、製品、ドメイン名、電子メールアドレス、ロゴ、人物、場所、イベントは架空のものであり、実際の会社、組織、製品、ドメイン名、電子メールアドレス、ロゴ、人物、人物、場所、またはイベントとの関連付けは意図されていないか、または推測されるべきである。</span><span class="sxs-lookup"><span data-stu-id="5c614-689">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="5c614-690">(C) 2012 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="5c614-690">© 2012 Microsoft Corporation.</span></span> <span data-ttu-id="5c614-691">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="5c614-691">All rights reserved.</span></span>

<span data-ttu-id="5c614-692">Microsoft および Windows は、米国および他の国における Microsoft Corporation の登録商標または商標です。</span><span class="sxs-lookup"><span data-stu-id="5c614-692">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="5c614-693">本ドキュメントで説明する実際の製造元および製品名は、それぞれの所有者の商標である場合があります。</span><span class="sxs-lookup"><span data-stu-id="5c614-693">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
