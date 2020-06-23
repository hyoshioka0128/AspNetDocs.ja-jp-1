---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Azure の Web ロールで SignalR パフォーマンスカウンターを使用する |Microsoft Docs
author: guardrex
description: Azure の Web ロールに SignalR パフォーマンスカウンターをインストールして使用する方法について説明します。
keywords: ASP .NET、signalr、パフォーマンスカウンター、azure web ロール
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 3de42435887113f93c6b8c36145793952af4d735
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240640"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a>Azure の Web ロールで SignalR パフォーマンスカウンターを使用する

作成者: [Luke Latham](https://github.com/guardrex)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

SignalR パフォーマンスカウンターは、Azure の Web ロールでアプリのパフォーマンスを監視するために使用されます。 カウンターは Microsoft Azure 診断によってキャプチャされます。 SignalR パフォーマンスカウンターは、スタンドアロンまたはオンプレミスのアプリと同じツールで*signalr.exe*を使用して Azure にインストールします。 Azure ロールは一時的なものであるため、スタートアップ時に SignalR パフォーマンスカウンターをインストールして登録するようにアプリを構成します。

## <a name="prerequisites"></a>必須コンポーネント

* Visual Studio 2015 または[2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
* [MICROSOFT AZURE sdk For Visual Studio](https://azure.microsoft.com/downloads/) **メモ: sdk のインストール後にコンピューターを再起動します。**
* Microsoft Azure サブスクリプション: 無料の Azure 試用版アカウントにサインアップするには、「 [Azure 無料試用版](https://azure.microsoft.com/free/dotnet/)」を参照してください。

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a>SignalR パフォーマンスカウンターを公開する Azure Web ロールアプリケーションの作成

1. Visual Studio を開きます。

2. Visual Studio で、 **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に選択します。

3. [**新しいプロジェクト**] ダイアログボックスで、左側にある [ **Visual C#**  >  **cloud** ] カテゴリを選択し、[ **Azure cloud services** ] テンプレートを選択します。 アプリに**SignalRPerfCounters**という名前を指定し、[ **OK]** を選択します。

   ![新しいクラウドアプリケーション](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > **クラウド**テンプレートカテゴリまたは**azure クラウドサービス**テンプレートが表示されない場合は、Visual Studio 2017 の**Azure 開発**ワークロードをインストールする必要があります。 [**新しいプロジェクト**] ダイアログの左下にある [ **Visual Studio インストーラーを開く**] リンクをクリックして Visual Studio インストーラーを開きます。 **Azure 開発**ワークロードを選択し、[**変更**] を選択して、ワークロードのインストールを開始します。
   >
   > ![Visual Studio インストーラーでの Azure 開発ワークロード](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. [**新しい Microsoft Azure クラウドサービス**] ダイアログで [ **ASP.NET Web Role** ] を選択し、[>] をクリックして、プロジェクトにロールを追加します。 **[OK]** を選択します。

   ![ASP.NET Web ロールの追加](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. [ **New ASP.NET Web Application-WebRole1** ] ダイアログボックスで、[ **MVC** ] テンプレートを選択し、[ **OK]** を選択します。

   ![MVC と Web API の追加](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. **ソリューションエクスプローラー**で、 **WebRole1**の下の*diagnostics.wadcfgx*ファイルを開きます。

   ![ソリューションエクスプローラー diagnostics.wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. ファイルの内容を次の構成に置き換え、ファイルを保存します。

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. [**ツール**] [NuGet パッケージマネージャー] から**パッケージマネージャーコンソール**を開き  >  **NuGet Package Manager**ます。 次のコマンドを入力して、最新バージョンの SignalR および SignalR utilities パッケージをインストールします。

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. SignalR パフォーマンスカウンターを起動またはリサイクルするときに、ロールインスタンスにインストールするようにアプリを構成します。 **ソリューションエクスプローラー**で、 **WebRole1**プロジェクトを右クリックし、[新しいフォルダーの**追加**] を選択し  >  **New Folder**ます。 新しいフォルダーに「*スタートアップ*」という名前を指定します。

   ![スタートアップフォルダーの追加](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. **SignalR**ファイル*signalr.exe*を \<project folder> /SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils. \<version> から (パッケージと共に追加して)signalr.exeコピーします。/ツールを使用して、前の手順で作成した*スタートアップ*フォルダーを表示します。

11. **ソリューションエクスプローラー**で、 *Startup*フォルダーを右クリックし、[ **Add**  >  **既存項目**の追加] を選択します。 表示されるダイアログで、[ *signalr.exe*を選択し、[**追加**] を選択します。

    ![プロジェクトへの signalr.exe の追加](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. 作成した*スタートアップ*フォルダーを右クリックします。 [ **Add**  >  **新しい項目**の追加] を選択します。 [**全般**] ノードを選択し、[**テキストファイル**] を選択して、新しい項目に「 *signalrperfcounterinstall. cmd*」という名前を指定します。 このコマンドファイルは、SignalR パフォーマンスカウンターを web ロールにインストールします。

    ![SignalR パフォーマンスカウンターのインストールバッチファイルの作成](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. Visual Studio によって*Signalrperfcounterinstall .cmd*ファイルが作成されると、自動的にメインウィンドウに表示されます。 ファイルの内容を次のスクリプトに置き換え、ファイルを保存して閉じます。 このスクリプトは*signalr.exe*を実行します。これにより、ロールインスタンスに SignalR パフォーマンスカウンターが追加されます。

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. **ソリューションエクスプローラー**で*signalr.exe*ファイルを選択します。 ファイルの**プロパティ**で、[**出力ディレクトリにコピー** ] を [**常にコピー**する] に設定します。

    ![出力ディレクトリにコピーするように設定する (常にコピーする)](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. 前の手順を繰り返して、 *Signalrperfcounterinstall. .cmd*ファイルを実行します。

16. *Signalrperfcounterinstall. .cmd*ファイルを右クリックし、[ファイル**を開くアプリケーション**の選択] を選択します。 表示されるダイアログで、[**バイナリエディター** ] を選択し、[ **OK]** を選択します。

    ![バイナリエディターで開く](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. バイナリエディターで、ファイル内の先頭バイトを選択して削除します。 ファイルを保存して閉じます。

    ![先頭バイトの削除](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. サービスの開始時に、 *Servicedefinition*を開き、 *Signalrperfcounterinstall. .cmd*ファイルを実行するスタートアップタスクを追加します。

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. を開き、 `Views/Shared/_Layout.cshtml` ファイルの末尾から jQuery バンドルスクリプトを削除します。

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. サーバーでメソッドを連続して呼び出す JavaScript クライアントを追加 `increment` します。 を開き、 `Views/Home/Index.cshtml` 内容を次のコードに置き換えます。

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. *ハブ*という名前の**WebRole1**プロジェクトに新しいフォルダーを作成します。 **ソリューションエクスプローラー**で [*ハブ*] フォルダーを右クリックし、[新しい項目の**追加**] を選択し  >  **New Item**ます。 [**新しい項目の追加**] ダイアログボックスで、[ **Web**  >  **SignalR** ] カテゴリを選択し、 **SignalR Hub クラス (v2)** 項目テンプレートを選択します。 新しいハブに*MyHub.cs*という名前を指定し、[**追加**] を選択します。

    ![[新しい項目の追加] ダイアログボックスの [ハブ] フォルダーに SignalR Hub クラスを追加する](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. *MyHub.cs*はメインウィンドウで自動的に開きます。 内容を次のコードに置き換え、ファイルを保存して閉じます。

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. *[Crank.exe](signalr-connection-density-testing-with-crank.md)* は、SignalR codebase で提供される接続密度テストツールです。 クランクは永続的な接続を必要とするため、テスト時に使用するためにサイトに追加します。 *PersistentConnections*という名前の**WebRole1**プロジェクトに新しいフォルダーを追加します。 このフォルダーを右クリックし、[クラスの**追加**] を選択し  >  **Class**ます。 新しいクラスファイルに*MyPersistentConnections.cs*という名前を指定し、[**追加**] を選択します。

24. Visual Studio によって、メインウィンドウで*MyPersistentConnections.cs*ファイルが開きます。 内容を次のコードに置き換え、ファイルを保存して閉じます。

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. クラスを使用する `Startup` と、OWIN の起動時に SignalR オブジェクトが開始されます。 *Startup.cs*を開くか作成し、内容を次のコードに置き換えます。

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    上記のコードでは、 `OwinStartup` 属性は、このクラスを OWIN を開始するようにマークします。 `Configuration`メソッドは SignalR を開始します。

26. **F5**キーを押して、Microsoft Azure Emulator でアプリケーションをテストします。

    > [!NOTE]
    > **MapSignalR**で**FileLoadException**が発生した場合は、 *web.config*のバインドリダイレクトを次のように変更します。

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. 約1分待ちます。 Visual Studio で Cloud Explorer ツールウィンドウを開き (**View**  >  **Cloud Explorer**の表示)、パスを展開し `(Local)/Storage Accounts/(Development)/Tables` ます。 **WADPerformanceCountersTable**をダブルクリックします。 テーブルデータに SignalR カウンターが表示されます。 テーブルが表示されない場合は、Azure Storage 資格情報の再入力が必要になることがあります。 場合によっては、[**更新**] ボタンを選択して**Cloud Explorer**のテーブルを表示するか、[テーブルを開く] ウィンドウの [**更新**] ボタンを選択してテーブル内のデータを表示する必要があります。

    ![Visual Studio での WAD パフォーマンスカウンターテーブルの選択 Cloud Explorer](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![WAD パフォーマンスカウンターテーブルで収集されたカウンターの表示](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. クラウドでアプリケーションをテストするには、 **serviceconfiguration.cscfg**ファイルを更新し、を `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 有効な Azure Storage アカウントの接続文字列に設定します。

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. アプリケーションを Azure サブスクリプションにデプロイします。 アプリケーションを Azure にデプロイする方法の詳細については、「[クラウドサービスを作成およびデプロイする方法](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)」を参照してください。

30. 数分待ちます。 **Cloud Explorer**で、上記で構成したストレージアカウントを探し、 `WADPerformanceCountersTable` その中のテーブルを見つけます。 テーブルデータに SignalR カウンターが表示されます。 テーブルが表示されない場合は、Azure Storage 資格情報の再入力が必要になることがあります。 場合によっては、[**更新**] ボタンを選択して**Cloud Explorer**のテーブルを表示するか、[テーブルを開く] ウィンドウの [**更新**] ボタンを選択してテーブル内のデータを表示する必要があります。

このチュートリアルで使用されている元のコンテンツの[Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard)に感謝します。
