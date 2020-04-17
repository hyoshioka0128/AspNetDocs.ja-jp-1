---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 新しいASP.NET MVC プロジェクトを作成する |マイクロソフトドキュメント
author: rick-anderson
description: 手順 1 では、NerdDinner アプリケーションの基本構造を配置する方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541482"
---
# <a name="create-a-new-aspnet-mvc-project"></a>新しい ASP.NET MVC プロジェクトを作成する

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、mvc 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NETの手順 1 です。
> 
> 手順 1 では、NerdDinner アプリケーションの基本構造を配置する方法を示します。
> 
> mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。

## <a name="nerddinner-step-1-file-gtnew-project"></a>NerdDinner ステップ 1:&gt;ファイル - 新しいプロジェクト

NerdDinner アプリケーションは、Visual Studio 2008 または無料の Visual Web 開発者 2008 Express 内の **[ファイル -&gt;新しいプロジェクト**] メニュー項目を選択して開始します。

これにより、「新規プロジェクト」ダイアログが表示されます。 新しいASP.NETのMVCアプリケーションを作成するには、ダイアログの左側にある「Web」ノードを選択し、右側にある「ASP.NETMVC Webアプリケーション」プロジェクトテンプレートを選択します。

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*重要: MVC ASP.NETダウンロードしてインストールしたことを確認してください- そうでなければ、[新しいプロジェクト] ダイアログに表示されません。まだインストールしていない場合は[、Microsoft Web プラットフォーム インストーラー](https://www.microsoft.com/web/downloads/platform.aspx)の V2 を使用できます (ASP.NET MVC は「Web&gt;プラットフォーム - フレームワークとランタイム」セクションで利用できます)。*

新しいプロジェクトに"NerdDinner"を作成し、「OK」ボタンをクリックして作成します。

「OK」をクリックすると、Visual Studio は追加のダイアログを表示し、必要に応じて新しいアプリケーションの単体テスト プロジェクトを作成するよう求められます。 この単体テスト プロジェクトでは、アプリケーションの機能と動作を検証する自動テストを作成できます (このチュートリアルの後半で説明する方法について説明します)。

![](create-a-new-aspnet-mvc-project/_static/image2.png)

上記のダイアログボックスの「テストフレームワーク」ドロップダウンには、マシンにインストールされているMVC単体テストプロジェクトテンプレートASP.NET使用可能なすべてのデータが表示されます。 バージョンは、NUnit、MBUnit、および XUnit 用にダウンロードできます。 組み込みの Visual Studio 単体テスト フレームワークもサポートされています。

*注: Visual Studio 単体テスト フレームワークは、Visual Studio 2008 プロフェッショナルおよび上位バージョンでのみ使用できます。VS 2008 標準版またはビジュアル Web 開発者 2008 Express を使用している場合は、このダイアログを表示するには、ASP.NET MVC 用の NUnit、MBUnit または XUnit 拡張機能をダウンロードしてインストールする必要があります。テスト フレームワークがインストールされていない場合、ダイアログは表示されません。*

作成するテスト プロジェクトには既定の "NerdDinner.Tests" 名を使用し、"Visual Studio 単体テスト" フレームワーク オプションを使用します。 「OK」ボタンをクリックすると、Visual Studio は 2 つのプロジェクト (Web アプリケーション用と単体テスト用のプロジェクト) を含むソリューションを作成します。

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>NerdDinner ディレクトリ構造の確認

Visual Studio で新しい ASP.NET MVC アプリケーションを作成すると、プロジェクトにファイルとディレクトリが自動的に追加されます。

![](create-a-new-aspnet-mvc-project/_static/image4.png)

既定では、mvc プロジェクトASP.NET 6 つの最上位ディレクトリがあります。

| **ディレクトリ** | **目的** |
| --- | --- |
| **/コントローラ** | URL 要求を処理するコントローラー クラスを配置する場所 |
| **/モデル** | データを表し、操作するクラスを配置する場所 |
| **/ビュー** | 出力のレンダリングを担当する UI テンプレート ファイルを配置する場所 |
| **/スクリプト** | JavaScript ライブラリ ファイルとスクリプト (.js) を配置する場所 |
| **/コンテンツ** | CSS ファイルとイメージ ファイル、およびその他の非動的/非 JavaScript コンテンツを配置する場所 |
| **/アプリ\_データ** | 読み取り/書き込み対象のデータ ファイルを格納する場所。 |

ASP.NET MVC はこの構造体を必要としません。 実際、大規模なアプリケーションを使用する開発者は、通常、アプリケーションを複数のプロジェクトに分割して管理しやすくします (たとえば、データ モデル クラスは、Web アプリケーションとは別のクラス ライブラリ プロジェクトに配置されることがよくあります)。 しかし、既定のプロジェクト構造は、アプリケーションの問題を明確に保つために使用できる既定のディレクトリ規則を提供します。

/Controllers ディレクトリを展開すると、Visual Studio が 2 つのコント ローラー クラスを追加していることがわかります - ホーム コント ローラーとアカウント コント ローラー - 既定では、プロジェクトに。

![](create-a-new-aspnet-mvc-project/_static/image5.png)

/Views ディレクトリを展開すると、3 つのサブディレクトリ (/ホーム、/アカウント、/Shared) と、その中のいくつかのテンプレート ファイルが既定でプロジェクトに追加されています。

![](create-a-new-aspnet-mvc-project/_static/image6.png)

/Content ディレクトリと /Scripts ディレクトリを展開すると、サイト上のすべての HTML のスタイルを設定するために使用される Site.css ファイルと、アプリケーション内で AJAX と jQuery のサポートASP.NET可能な JavaScript ライブラリが見つかります。

![](create-a-new-aspnet-mvc-project/_static/image7.png)

NerdDinner.Tests プロジェクトを展開すると、コントローラー クラスの単体テストを含む 2 つのクラスが見つかります。

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Visual Studio によって追加されたこれらの既定のファイルは、作業アプリケーションの基本的な構造を提供します - ホーム ページ、ページ、アカウントログイン/ログアウト/登録ページ、および未処理のエラー ページ (すべてワイヤーアップされ、そのまま作業) を完了します。

### <a name="running-the-nerddinner-application"></a>NerdDinner アプリケーションの実行

[**デバッグ開始デバッグ]&gt;** メニュー項目または [デバッグなしのデバッグ-**&gt;デバッグなしの開始**] メニュー項目を選択して、プロジェクトを実行できます。

![](create-a-new-aspnet-mvc-project/_static/image9.png)

これにより、Visual Studio に付属の組み込みの ASP.NET Web サーバーが起動し、アプリケーションが実行されます。

![](create-a-new-aspnet-mvc-project/_static/image10.png)

以下は、新しいプロジェクトのホームページ (URL: "/") を実行する場合のページです。

![](create-a-new-aspnet-mvc-project/_static/image11.png)

[情報] タブをクリックすると、次のページが表示されます (URL: "/ホーム/約")。

![](create-a-new-aspnet-mvc-project/_static/image12.png)

右上の [ログオン] リンクをクリックすると、ログイン ページに移動します (URL: "/アカウント/LogOn")

![](create-a-new-aspnet-mvc-project/_static/image13.png)

ログインアカウントがない場合は、登録リンク(URL:"/アカウント/登録")をクリックして作成できます。

![](create-a-new-aspnet-mvc-project/_static/image14.png)

新しいプロジェクトを作成するときに、上記のホーム、概要、およびログアウト/登録機能を実装するコードが既定で追加されました。 アプリケーションの出発点として使用します。

### <a name="testing-the-nerddinner-application"></a>NerdDinner アプリケーションのテスト

プロフェッショナル エディションまたはそれ以降のバージョンの Visual Studio 2008 を使用している場合は、Visual Studio 内で組み込みの単体テスト IDE サポートを使用してプロジェクトをテストできます。

![](create-a-new-aspnet-mvc-project/_static/image15.png)

上記のオプションのいずれかを選択すると、IDE 内の [テスト結果] ウィンドウが開き、組み込み機能をカバーする新しいプロジェクトに含まれる 27 の単体テストで合格/不合格のステータスが表示されます。

![](create-a-new-aspnet-mvc-project/_static/image16.png)

このチュートリアルの後半で、自動テストについて詳しく説明し、実装するアプリケーションの機能をカバーする追加の単体テストを追加します。

### <a name="next-step"></a>次の手順

これで、基本的なアプリケーション構造が整いました。 それでは、アプリケーション[データを格納するデータベースを作成](create-a-database.md)しましょう。

> [!div class="step-by-step"]
> [前へ](introducing-the-nerddinner-tutorial.md)
> [次へ](create-a-database.md)
