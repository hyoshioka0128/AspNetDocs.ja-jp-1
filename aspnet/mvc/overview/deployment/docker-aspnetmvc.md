---
uid: mvc/overview/deployment/docker-aspnetmvc
title: Windows コンテナーへの ASP.NET MVC アプリケーションの移行
description: 既存の ASP.NET MVC アプリケーションを取得し、Windows Docker コンテナーで実行する方法について説明します。
keywords: ウィンドウズ コンテナー、ドッカー、ASP.NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: 2c3aefab16673f4d4dd28c74319903fbd25a9e7e
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675195"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a>Windows コンテナーへの ASP.NET MVC アプリケーションの移行

Windows コンテナーで既存の .NET Framework ベース アプリケーションを実行するとき、アプリに変更を加える必要はありません。 Windows コンテナーでアプリを実行するには、アプリを含む Docker イメージを作成し、コンテナーを起動します。 このトピックでは、既存の [ASP.NET MVC アプリケーション](http://www.asp.net/mvc)を取得し、Windows コンテナーに展開する方法について説明します。

既存の ASP.NET MVC アプリから開始し、Visual Studio を使用して発行したアセットをビルドします。 Docker を使用し、アプリを含み、これを実行するイメージを作成します。 Windows コンテナーで実行されているサイトに移動し、アプリが動作していることを確認します。

この記事では、Docker の基本的な理解ができていることを前提としています。 Docker の詳細は、「[Docker Overview (Docker の概要)](https://docs.docker.com/engine/understanding-docker/)」で確認できます。

コンテナーで実行するアプリは、質問にランダムに回答する単純な Web サイトです。 このアプリは基本的な MVC アプリケーションであり、認証やデータベース ストレージはないため Web 層をコンテナーに移動することに集中できます。 今後のトピックで、コンテナー化されたアプリケーションに永続的な記憶域を移動して管理する方法を説明します。

アプリケーションを移行する手順は次のとおりです。

1. [イメージのアセットをビルドする発行タスクを作成します。](#publish-script)
1. [アプリケーションを実行する Docker イメージをビルドします。](#build-the-image)
1. [イメージを実行する Docker コンテナーを開始します。](#start-a-container)
1. [ブラウザーを使用してアプリケーションを検証します。](#verify-in-the-browser)

[完成したアプリケーション](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator)が GitHub にあります。

## <a name="prerequisites"></a>前提条件

開発用コンピューターには、次のソフトウェアが必要です。

- [Windows 10 記念日の更新プログラム](https://www.microsoft.com/software-download/windows10/)(またはそれ以降) または[Windows サーバー 2016](https://www.microsoft.com/cloud-platform/windows-server) (またはそれ以降)
- [Docker for Windows](https://docs.docker.com/docker-for-windows/) - バージョン Stable 1.13.0 または 1.12 Beta 26 (以降のバージョン)
- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> Windows Server 2016 を使用している場合は、「[コンテナー ホストの展開 - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment)」の指示に従ってください。

Docker をインストールして起動したら、トレイ アイコンを右クリックし、 **[Switch to Windows containers]\(Windows コンテナーに切り替える\)** を選択します。 これは、Windows に基づいて Docker イメージを実行するために必要です。 このコマンドの実行には数秒かかります。

![ウィンドウズコンテナ][windows-container]

## <a name="publish-script"></a>発行スクリプト

Docker イメージに読み込む必要があるすべてのアセットを 1 か所に収集します。 Visual Studio の **[発行]** コマンドを使用してアプリの発行プロファイルを作成できます。 このプロファイルですべてのアセットを 1 つのディレクトリ ツリーに集めます。このチュートリアルの後半で、そのディレクトリ ツリーをターゲット イメージにコピーします。

**発行の手順**

1. Visual Studio で Web プロジェクトを右クリックし、**[発行]** を選択します。
1. [**カスタム プロファイル] ボタン**をクリックし、方法として **[ファイル システム**] を選択します。
1. ディレクトリを選択します。 規則により、ダウンロードしたサンプルには `bin\Release\PublishOutput` が使用されます。

![接続の発行][publish-connection]

**[設定**] タブの **[ファイル発行オプション]** セクションを開**きます。** この最適化は、Docker コンテナー内のビューをコンパイルすることを意味し、プリコンパイル済みのビューをコピーすることになります。

![パブリッシュ設定][publish-settings]

**[発行]** をクリックすると、Visual Studio で必要なすべてのアセットがコピー先フォルダーにコピーされます。

## <a name="build-the-image"></a>イメージをビルドする

Docker イメージを定義する*Dockerfile*という名前の新しいファイルを作成します。 *Dockerfile*には、最終的なイメージを構築するための指示が含まれ、基本イメージ名、必要なコンポーネント、実行するアプリ、およびその他の構成イメージが含まれています。 *Dockerfile*は、イメージを`docker build`作成するコマンドへの入力です。

この演習では[、Docker Hub](https://hub.docker.com/r/microsoft/aspnet/)にあるイメージに基`microsoft/aspnet`づいてイメージをビルドします。
基本イメージである `microsoft/aspnet` は、Windows Server イメージです。 これには、Windows サーバー コア、IIS、および ASP.NET 4.7.2 が含まれています。 このイメージをコンテナー内で実行すると、IIS とインストールされている Web サイトが自動的に起動します。

イメージを作成する Dockerfile は、次のようになります。

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

この Dockerfile には `ENTRYPOINT` コマンドが存在しません。 これは必要ありません。 IIS を使用して Windows サーバーを実行する場合、IIS プロセスは、aspnet ベース イメージで開始するように構成されているエントリ ポイントです。

Docker ビルド コマンドを実行し、ASP.NET アプリを実行するイメージを作成します。 これを行うには、プロジェクトのディレクトリで PowerShell ウィンドウを開き、ソリューション ディレクトリに次のコマンドを入力します。

```console
docker build -t mvcrandomanswers .
```

このコマンドは、Dockerfile の指示を使用して新しいイメージを構築し、イメージを mvcrandomanswers として命名 (-t タグ付け) します。 その手順には、[Docker Hub](http://hub.docker.com) から基本イメージをプルし、それからそのイメージにアプリを追加する作業が含まれることがあります。

そのコマンドの完了後、`docker images` コマンドを実行して新しいイメージの情報を参照できます。

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

IMAGE ID はコンピューターによって異なります。 では、アプリを実行しましょう。

## <a name="start-a-container"></a>コンテナーの開始

コンテナーを開始するには、次の `docker run` コマンドを実行します。

```console
docker run -d --name randomanswers mvcrandomanswers
```

`-d` 引数は、デタッチ モードでイメージを開始するよう Docker に指示します。 つまり、Docker イメージは現在のシェルから切断された状態で実行されます。

多くの docker の例では、-p を使用してコンテナーとホスト ポートをマップします。 デフォルトの aspnet イメージは、ポート 80 でリッスンして公開するようにコンテナーを既に構成しています。

`--name randomanswers` は、実行するコンテナーに名前を付けます。 この名前は、ほとんどのコマンドでコンテナー ID の代わりに使用できます。

`mvcrandomanswers` は、開始するイメージの名前です。

## <a name="verify-in-the-browser"></a>ブラウザーでの確認

コンテナーが開始されたら、例に示すように、`http://localhost`実行中のコンテナーに接続します。 その URL をブラウザーに入力すると、実行中のサイトが表示されます。

> [!NOTE]
> 一部の VPN またはプロキシ ソフトウェアが原因でサイトに移動できない場合があります。
> コンテナーが動作していることを確認するために、それらを一時的に無効にできます。

GitHub のサンプル ディレクトリに含まれる [PowerShell スクリプト](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1)は、これらのコマンドを実行します。 PowerShell ウィンドウを開き、ソリューション ディレクトリに移動して、次のように入力します。

```console
./run.ps1
```

上記のコマンドは、イメージをビルドし、コンピューター上のイメージの一覧を表示し、コンテナーを起動します。

コンテナーを停止するには、`docker stop` コマンドを実行します。

```console
docker stop randomanswers
```

コンテナーを削除するには、`docker rm` コマンドを実行します。

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Windows コンテナーへの切り替え"
[publish-connection]: media/aspnetmvc/PublishConnection.png "ファイル システムへの発行"
[publish-settings]: media/aspnetmvc/PublishSettings.png "パブリッシュ設定"
