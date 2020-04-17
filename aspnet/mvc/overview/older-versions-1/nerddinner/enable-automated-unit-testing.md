---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 自動単体テストを有効にする |マイクロソフトドキュメント
author: rick-anderson
description: ステップ 12 は、NerdDinner 機能を検証する一連の自動単体テストを開発する方法を示しています。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 7fe84efd9e4cc359c19d5ab9e22c579b80207e9c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541469"
---
# <a name="enable-automated-unit-testing"></a>自動化された単体テストを有効にする

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、mvc 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)の手順 12 ASP.NETです。
> 
> 手順 12 は、NerdDinner の機能を検証する自動単体テストのスイートを開発する方法を示し、将来アプリケーションを変更および改善する自信を与えます。
> 
> mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。

## <a name="nerddinner-step-12-unit-testing"></a>NerdDinner ステップ 12: 単体テスト

NerdDinnerの機能を検証し、将来アプリケーションを変更して改善する自信を与えてくれる自動単体テストのスイートを開発しましょう。

### <a name="why-unit-test"></a>なぜ単体テスト?

ある朝、仕事にドライブであなたが取り組んでいるアプリケーションについてのインスピレーションの突然のフラッシュがあります。 アプリケーションを劇的に改善する変更が実装できることが分かります。 コードをクリーンアップしたり、新しい機能を追加したり、バグを修正したりするリファクタリングである場合があります。

コンピュータに到着したときに直面する質問は、「この改善を行うことはどのくらい安全ですか?」 変更を行うことに副作用がある場合や何かを壊した場合はどうなりますか? 変更は簡単で、実装に数分しかかからず、すべてのアプリケーション シナリオを手動でテストするのに数時間かかる場合はどうでしょうか。 シナリオをカバーするのを忘れて、壊れたアプリケーションが実稼働に入った場合はどうなりますか? この改善を行うことは本当にすべての努力の価値がありますか?

自動単体テストを使用すると、アプリケーションを継続的に強化し、作業中のコードを恐れないようにするセーフティ ネットを提供できます。 機能を迅速に検証する自動テストを実施することで、自信を持ってコーディングし、改善を行う力を与え、他の方法では快適に感じがなかった可能性があります。 彼らはまた、よりメンテナンスしやすく、寿命が長いソリューションを作成するのに役立ち、投資収益率がはるかに高くなります。

ASP.NET MVC フレームワークを使用すると、単体テスト アプリケーションの機能を簡単かつ自然に実行できます。 また、テストファーストベースの開発を可能にするテスト駆動開発 (TDD) ワークフローも可能になります。

### <a name="nerddinnertests-project"></a>オタクディナー.テストプロジェクト

このチュートリアルの最初に NerdDinner アプリケーションを作成すると、アプリケーション プロジェクトと一緒に作業する単体テスト プロジェクトを作成するかどうかを尋ねるダイアログ が表示されました。

![](enable-automated-unit-testing/_static/image1.png)

"はい、単体テスト プロジェクトを作成します" オプション ボタンを選択した状態で、その結果、"NerdDinner.Tests" プロジェクトがソリューションに追加されました。

![](enable-automated-unit-testing/_static/image2.png)

NerdDinner.Tests プロジェクトは NerdDinner アプリケーション プロジェクト アセンブリを参照し、アプリケーションの機能を検証する自動テストを簡単に追加できます。

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>Dinner モデル クラスの単体テストの作成

モデルレイヤーを構築したときに作成した Dinner クラスを検証する NerdDinner.Tests プロジェクトにいくつかのテストを追加しましょう。

まず、テスト プロジェクト内に新しいフォルダーを作成する "モデル" モデル関連のテストを配置します。 次に、フォルダーを右クリックし、[**新&gt;しいテストの追加**] メニュー コマンドを選択します。 これにより、[新しいテストの追加] ダイアログが表示されます。

「単体テスト」を作成し、「DinnerTest.cs」という名前を付けます。

![](enable-automated-unit-testing/_static/image3.png)

「OK」ボタンをクリックすると、Visual Studio はプロジェクトにDinnerTest.csファイルを追加 (および開く) します。

![](enable-automated-unit-testing/_static/image4.png)

既定の Visual Studio 単体テスト テンプレートには、その中にボイラー プレート コードがたくさん含まれています。 以下のコードを含むだけで、それをクリーンアップしてみましょう:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

上記の DinnerTest クラスの [TestClass] 属性は、テストを含むクラスとして識別し、オプションのテスト初期化コードとティアダウン コードを含みます。 テスト内にテストを定義するには、テストに [TestMethod] 属性を持つパブリック メソッドを追加します。

以下は、Dinnerクラスを追加する2つのテストのうちの最初のテストです。 最初のテストでは、すべてのプロパティが正しく設定されずに新しい Dinner が作成された場合、Dinner が無効であることを確認します。 2 番目のテストでは、Dinner に有効な値を持つすべてのプロパティが設定されている場合に、Dinner が有効であることを確認します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

上記のテスト名は非常に明示的です (やや冗長です)。 これは、何百、何千もの小さなテストを作成することになり、それぞれの意図と動作を簡単に特定できるようにするためです(特にテストランナーの失敗のリストを調べている場合)。 テスト名は、テストする機能の名前に付ける必要があります。 上記では、「名詞\_は\_動詞」の命名パターンを使用しています。

「アヤア」テストパターンを使用してテストを構築しています。

- 配置: テスト対象のユニットをセットアップします。
- 行動:テスト対象のユニットを行使し、結果をキャプチャする
- アサート: 動作を確認する

テストを書くとき、個々のテストがあまりにも多くのことを避けたいと思います。 代わりに、各テストでは単一の概念のみを検証する必要があります (これにより、失敗の原因を特定することがはるかに容易になります)。 良いガイドラインは、テストごとに 1 つのアサート ステートメントのみを実行することです。 テスト メソッドに複数の assert ステートメントがある場合は、すべてのステートメントが同じ概念をテストするために使用されていることを確認します。 疑わしい場合は、別のテストを行います。

### <a name="running-tests"></a>テストの実行

Visual Studio 2008 プロフェッショナル (および上位エディション) には、IDE 内で Visual Studio 単体テスト プロジェクトを実行するために使用できる組み込みのテスト ランナーが含まれています。 **[ソリューション内のすべての&gt;テスト&gt;**] メニュー コマンドを選択 (または Ctrl R、A と入力) して、すべての単体テストを実行できます。 または、特定のテストクラスまたはテストメソッド内にカーソルを配置し、[**現在のコンテキストでテスト&gt;-&gt;テスト- テスト**]メニューコマンドを使用して(またはCtrl R、Tを入力)単体テストのサブセットを実行することもできます。

DinnerTest クラス内にカーソルを置き、"Ctrl R, T" と入力して、定義した 2 つのテストを実行してみましょう。 これを行うと、Visual Studio 内に "テスト結果" ウィンドウが表示され、テストの実行結果が表示されます。

![](enable-automated-unit-testing/_static/image5.png)

*注: VS テスト結果ウィンドウには、既定では [クラス名] 列は表示されません。これを追加するには、[テスト結果] ウィンドウ内を右クリックし、[列の追加と削除] メニュー コマンドを使用します。*

2 つのテストは、実行に要する秒数のほんの一部に過ぎません。 ここでは、特定のルール検証を検証する追加のテストを作成し、Dinner クラスに追加した 2 つのヘルパー メソッドである IsUserHost() と IsUserRegistered() を取り上げ、それらを拡張できます。 Dinner クラスに対してこれらのすべてのテストを実施すると、将来、新しいビジネス ルールと検証を追加する方がはるかに簡単で安全になります。 Dinner に新しいルール ロジックを追加し、数秒以内に以前のロジック機能が破損していないことを確認できます。

説明的なテスト名を使用すると、各テストで確認されている内容をすばやく理解しやすくなります。 **[ツール]&gt;メニュー**の [オプション] メニューコマンドを使用して、[テスト ツール -&gt;テスト実行] 構成画面を開き、[失敗した単体テスト結果または決定的な単体テストの結果をダブルクリックすると、テストの失敗点が表示される] チェック ボックスをオンにすることをお勧めします。 これにより、テスト結果ウィンドウで失敗をダブルクリックし、アサートの失敗にすぐにジャンプすることができます。

### <a name="creating-dinnerscontroller-unit-tests"></a>ディナーコントローラ単体テストの作成

ここで、DinnersController の機能を検証する単体テストをいくつか作成しましょう。 まず、テスト プロジェクト内の "コントローラー" フォルダーを右クリックし、[**新&gt;しいテストの追加**] メニュー コマンドを選択します。 「単体テスト」を作成し、"DinnersControllerTest.cs"という名前を付けます。

DinnersController で Details() アクション メソッドを検証する 2 つのテスト メソッドを作成します。 最初の方法では、既存の Dinner が要求されたときにビューが返されることを確認します。 2 つ目は、存在しない Dinner が要求されたときに "NotFound" ビューが返されることを確認します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

上記のコードはクリーンコンパイルします。 ただし、テストを実行すると、両方とも失敗します。

![](enable-automated-unit-testing/_static/image6.png)

エラー メッセージを見ると、DinnersRepository クラスがデータベースに接続できなかったため、テストが失敗した理由がわかります。 NerdDinner アプリケーションは、NerdDinner アプリケーション プロジェクトの \App\_データ ディレクトリの下に存在するローカル SQL Server Express ファイルへの接続文字列を使用しています。 NerdDinner.Tests プロジェクトは、アプリケーション プロジェクトの次に別のディレクトリでコンパイルおよび実行されるため、接続文字列の相対パスの場所が正しくありません。

この問題*を修正するには、SQL* Express データベース ファイルをテスト プロジェクトにコピーし、テスト プロジェクトの App.config に適切なテスト接続文字列を追加します。 これにより、上記のテストのブロック解除と実行が行われます。

しかし、実際のデータベースを使用してコードを単体テストすると、多くの課題が伴います。 具体的な内容は次のとおりです。

- 単体テストの実行時間が大幅に遅くなります。 テストの実行にかかる時間が長いほど、頻繁にテストを実行する可能性は低くなります。 理想的には、単体テストを数秒で実行し、プロジェクトのコンパイルと同じくらい自然に行うようにします。
- テスト内のセットアップとクリーンアップのロジックが複雑になります。 各単体テストを分離し、他の単体テストに依存しない (副作用や依存関係がない) 必要があります。 実際のデータベースに対して作業するときは、状態に注意し、テストの間にリセットする必要があります。

これらの問題を回避し、テストで実際のデータベースを使用する必要を回避するのに役立つ"依存関係の注入"と呼ばれるデザイン パターンを見てみましょう。

### <a name="dependency-injection"></a>依存関係の挿入

今、ディナーコントローラは、ディナーリポジトリクラスにしっかりと「結合」されています。 「結合」とは、クラスが明示的に別のクラスに依存して動作する状況を指します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

DinnerRepository クラスはデータベースへのアクセスを必要とするため、DinnersController クラスが DinnersController に対して持つ緊密に結合された依存関係は、DinnersController アクション メソッドをテストするためにデータベースを持つ必要があります。

この問題を回避するには、"依存関係の注入" というデザイン パターンを使用して、依存関係 (データ アクセスを提供するリポジトリ クラスなど) が、それらを使用するクラス内で暗黙的に作成されなくなるアプローチです。 代わりに、コンストラクター引数を使用して、依存関係を使用するクラスに明示的に渡すことができます。 依存関係がインターフェイスを使用して定義されている場合、単体テスト シナリオの "fake" 依存関係実装を柔軟に渡すことができます。 これにより、実際にはデータベースへのアクセスを必要としないテスト固有の依存関係の実装を作成できます。

この動作を確認するには、DinnersController で依存関係の注入を実装してみましょう。

#### <a name="extracting-an-idinnerrepository-interface"></a>IDinner リポジトリ インターフェイスの抽出

最初の手順は、私たちのコントローラが Dinners を取得して更新するために必要なリポジトリ コントラクトをカプセル化する新しい IDinnerRepository インターフェイスを作成することです。

このインターフェイス コントラクトを手動で定義するには、\Models フォルダーを右クリックし、[**追加 -&gt;新しい項目]** メニュー コマンドを選択し、IDinnerRepository.csという名前の新しいインターフェイスを作成します。

または、Visual Studio Professional (および上位エディション) に組み込まれているリファクタリング ツールを使用して、既存の DinnerRepository クラスからインターフェイスを自動的に抽出して作成することもできます。 VS を使用してこのインターフェイスを抽出するには、DinnerRepository クラスのテキスト エディターにカーソルを置いて右クリックし、**リファクタリング&gt;- インターフェイスの抽出**メニュー コマンドを選択します。

![](enable-automated-unit-testing/_static/image7.png)

これにより、「インターフェイスの抽出」ダイアログが起動し、作成するインタフェースの名前を入力するよう促されます。 これは、IDinnerRepository にデフォルト設定され、インターフェイスに追加する既存の DinnerRepository クラスのすべてのパブリック メソッドを自動的に選択します。

![](enable-automated-unit-testing/_static/image8.png)

"OK" ボタンをクリックすると、Visual Studio は新しい IDinnerRepository インターフェイスをアプリケーションに追加します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

既存の DinnerRepository クラスが、インターフェイスを実装するように更新されます。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>コンストラクタの注入をサポートするために DinnersController を更新しています

新しいインターフェイスを使用するように DinnersController クラスを更新します。

現在、DinnersController は、"dinnerRepository" フィールドが常に DinnerRepository クラスになるようにハードコーディングされています。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

"dinnerRepository" フィールドが Dinner リポジトリではなく IDinnerRepository 型になるように変更します。 次に、2 つのパブリック DinnersController コンストラクターを追加します。 コンストラクタの 1 つを使用すると、引数として IDinnerRepository を渡すことができます。 もう 1 つは、既存の DinnerRepository 実装を使用する既定のコンストラクターです。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

既定では、既定ASP.NET MVC は既定のコンストラクターを使用してコントローラー クラスを作成するため、実行時に DinnersController は DinnerRepository クラスを使用してデータ アクセスを実行し続けます。

しかし、パラメータコンストラクタを使用して「偽の」ディナーリポジトリの実装に合格するように、単体テストを更新できるようになりました。 この"fake"dinnerリポジトリは、実際のデータベースへのアクセスを必要とせず、代わりにインメモリサンプルデータを使用します。

#### <a name="creating-the-fakedinnerrepository-class"></a>クラスを作成する

クラスを作成してみましょう。

まず、NerdDinner.Tests プロジェクト内に 「Fakes」ディレクトリを作成し、そのディレクトリに新しい FakeDinnerRepository クラスを追加します (フォルダーを右クリックして **[Add-&gt;New Class]** を選択します)。

![](enable-automated-unit-testing/_static/image9.png)

コードを更新して、FakeDinnerRepository クラスが IDinnerRepository インターフェイスを実装するようにします。 その後、それを右クリックして、コンテキストメニューコマンド「インターフェイスIDinnerRepositoryを実装する」を選択することができます。

![](enable-automated-unit-testing/_static/image10.png)

これにより、Visual Studio は、既定の "スタブ アウト" 実装を使用して、すべての IDinnerRepository インターフェイス メンバーを FakeDinnerRepository クラスに自動的に追加します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

その後、FakeDinnerRepository の実装を更新して、コンストラクタ引数として渡された&lt;メモリ&gt;内リストディナーコレクションをオフにします。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

これで、データベースを必要とせず、代わりに Dinner オブジェクトのメモリ内リストを処理できる偽の IDinnerRepository 実装が用意されています。

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>単体テストでのフェイクディナーリポジトリの使用

データベースが使用できなかったために、以前に失敗した DinnersController 単体テストに戻りましょう。 以下のコードを使用して、サンプルのメモリ内のディナー データが入力された FakeDinnerRepository を DinnersController に使用するようにテスト メソッドを更新できます。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

そして今、これらのテストを実行すると、両方とも合格します。

![](enable-automated-unit-testing/_static/image11.png)

何よりも、実行にほんの数秒しかかからず、複雑なセットアップ/クリーンアップロジックは必要ありません。 実際のデータベースに接続しなくても、DinnersController アクション メソッド のコード (リスト、ページング、詳細、作成、更新、削除など) をすべて単体テストできるようになりました。

| **サイドトピック: 依存関係の注入フレームワーク** |
| --- |
| 手動依存性注入 (上記のように) の実行は正常に動作しますが、アプリケーション内の依存関係とコンポーネントの数が増えると、保守が困難になります。 .NET には、依存関係管理の柔軟性をさらに高めるいくつかの依存関係挿入フレームワークが存在します。 これらのフレームワークは、"制御の反転" (IoC) コンテナーとも呼ばれ、実行時にオブジェクトに依存関係を指定および渡すための追加のレベルの構成サポートを可能にするメカニズムを提供します (ほとんどの場合、コンストラクターの挿入を使用)。 NET で最も人気のある OSS 依存性の注入/ IOC フレームワークの一部: AutoFac、 Ninject、 Spring.NET、構造マップ、ウィンザー。 ASP.NET MVC は、開発者がコントローラの解決とインスタンス化に参加できるようにする機能拡張 API を公開し、このプロセス内で依存関係の挿入 /IoC フレームワークをクリーンに統合できるようにします。 DI/IOC フレームワークを使用すると、DinnersController から既定のコンストラクタを削除することもできます。 NerdDinner アプリケーションでは、依存関係の挿入/IOC フレームワークを使用しません。 しかし、NerdDinnerのコードベースと機能が成長した場合、将来のために考慮できるものです。 |

### <a name="creating-edit-action-unit-tests"></a>編集アクション単体テストの作成

次に、DinnersController の編集機能を検証する単体テストをいくつか作成します。 まず、編集アクションの HTTP-GET バージョンをテストします。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

有効なディナーが要求されたときに、DinnerFormViewModel オブジェクトによってバックアップされたビューがレンダリングされることを確認するテストを作成します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

ただし、テストを実行すると、Edit メソッドが dinner.IsHostedBy() チェックを実行するために User.Identity.Name プロパティにアクセスしたときに null 参照例外がスローされるため、テストが失敗することがわかります。

コント ローラーの基本クラスの User オブジェクトは、ログインしているユーザーに関する詳細をカプセル化し、実行時にコントローラーを作成するときにASP.NET MVC によって設定されます。 Web サーバー環境の外部で DinnersController をテストしているため、User オブジェクトが設定されていません (したがって、null 参照例外)。

### <a name="mocking-the-useridentityname-property"></a>User.Identity.Nameプロパティのモック

モック フレームワークは、テストをサポートする依存オブジェクトの偽のバージョンを動的に作成できるようにすることで、テストを容易にします。 たとえば、Edit アクション テストでモック フレームワークを使用して、DinnersController がシミュレートされたユーザー名を検索するために使用できるユーザー オブジェクトを動的に作成できます。 これにより、テストを実行するときに null 参照がスローされるのを回避できます。

ASP.NET MVC で使用できる .NET モック フレームワークはたくさんあります (ここでは、その一覧を参照[http://www.mockframeworks.com/](http://www.mockframeworks.com/)できます)。 NerdDinnerアプリケーションのテストでは、"Moq"と呼ばれるオープンソースのモックフレームワークを使用[http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)します。

ダウンロードしたら、NerdDinner.Tests プロジェクトの参照を Moq.dll アセンブリに追加します。

![](enable-automated-unit-testing/_static/image12.png)

次に、ユーザー名をパラメーターとして受け取り、DinnersController インスタンスのUser.Identity.Nameプロパティを "モック" する "CreateDinnersControllerAs(ユーザー名)" ヘルパー メソッドをテスト クラスに追加します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

上記では、Moq を使用して ControllerContext オブジェクトを偽装するモック オブジェクトを作成しています (これは、ユーザー、要求、応答、セッションなどのランタイム オブジェクトを公開するために、mvc がコントローラー クラスに渡ASP.NETものです)。 モックの "SetupGet" メソッドを呼び出して、ControllerContext のHttpContext.User.Identity.Nameプロパティがヘルパー メソッドに渡したユーザー名文字列を返す必要があることを示しています。

任意の数の ControllerContext プロパティとメソッドをモックできます。 これを説明するために、Request.IsAuthenticated プロパティの SetupGet() 呼び出しも追加しました (これは、以下のテストでは実際には必要ではありませんが、要求プロパティをモックする方法を説明するのに役立ちます)。 完了したら、ControllerContext モックのインスタンスを DinnersController ヘルパー メソッドが返すに割り当てます。

このヘルパー メソッドを使用して、さまざまなユーザーが関与する編集シナリオをテストする単体テストを記述できるようになりました。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

そして今、我々はテストを実行すると、彼らは合格します:

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>テストモデル() シナリオ

編集アクションの HTTP-GET バージョンをカバーするテストを作成しました。 ここで、HTTP-POST バージョンの編集アクションを検証するテストをいくつか作成しましょう。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

このアクションメソッドでサポートする興味深い新しいテストシナリオは、コントローラの基本クラスでの UpdateModel() ヘルパーメソッドの使用です。 このヘルパー メソッドを使用して、フォームポストの値を Dinner オブジェクトインスタンスにバインドしています。

以下に、使用する UpdateModel() ヘルパー メソッドに対してフォームポスト値を指定する方法を示す 2 つのテストを示します。 この操作を行うには、FormCollection オブジェクトを作成して設定し、コントローラーの "ValueProvider" プロパティに割り当てます。

最初のテストでは、正常に保存されたブラウザーが詳細アクションにリダイレクトされることを確認します。 2 番目のテストでは、無効な入力がポストされると、アクションが再び編集ビューを再表示し、エラー メッセージが表示されることを確認します。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>テストのラップアップ

ここでは、単体テスト のコントローラー クラスに関連する中心的な概念について説明しました。 これらの手法を使用して、アプリケーションの動作を検証する数百の簡単なテストを簡単に作成できます。

コントローラとモデルのテストでは実際のデータベースは必要ないので、非常に高速で簡単に実行できます。 数秒で何百もの自動テストを実行し、変更が何かを壊したかどうかについてすぐにフィードバックを得ることができます。 これは、アプリケーションを継続的に改善し、リファクタリングし、洗練するための自信を提供するのに役立ちます。

この章の最後のトピックとしてテストを取り上げますが、テストは開発プロセスの最後に行う必要があるからです。 それどころか、開発プロセスでできるだけ早く自動テストを記述する必要があります。 これにより、開発中にすぐにフィードバックを得ることができ、アプリケーションのユースケースシナリオについて慎重に考え、クリーンな層と結合を念頭に置いてアプリケーションを設計するガイドを得ることができます。

本書の後の章では、テスト駆動開発 (TDD) と、ASP.NET MVC での使用方法について説明します。 TDD は、結果として得られるコードが満たすテストを最初に記述する反復的なコーディング方法です。 TDD を使用すると、実装しようとしている機能を検証するテストを作成して、各機能を開始します。 単体テストを最初に記述すると、機能と機能がどのように機能するかを明確に理解できます。 テストが記述された後 (そして失敗したことを確認した場合) にのみ、テストで検証される実際の機能を実装します。 機能の動作のユース ケースについて考える時間は既に費やされているため、要件と実装の最善の方法について理解を深める必要があります。 実装が完了したら、テストを再実行し、機能が正しく動作するかどうかのフィードバックをすぐに得ることができます。 第 10 章で TDD について詳しく説明します。

### <a name="next-step"></a>次の手順

いくつかの最終的なコメントをまとめる。

> [!div class="step-by-step"]
> [前へ](use-ajax-to-implement-mapping-scenarios.md)
> [次へ](nerddinner-wrap-up.md)
