---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
title: SQL Server でのメンバーシップスキーマの作成 (C#) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、まず、SqlMembershipProvider を使用するために必要なスキーマをデータベースに追加する方法を調べます。 その後、私たちは...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: b4ac129d-1b8e-41ca-a38f-9b19d7c7bb0e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 8160c422d7a20b7c6954f960e73d5d59f7b90a5f
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044741"
---
# <a name="creating-the-membership-schema-in-sql-server-c"></a>SQL Server でメンバーシップ スキーマを作成する (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_CS.zip) または [PDF のダウンロード](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_cs.pdf)

> このチュートリアルでは、まず、SqlMembershipProvider を使用するために必要なスキーマをデータベースに追加する方法を調べます。 ここでは、スキーマの主要なテーブルを調べ、その目的と重要性について説明します。 このチュートリアルでは、メンバーシップフレームワークが使用するプロバイダーを ASP.NET アプリケーションに通知する方法について説明します。

## <a name="introduction"></a>概要

前の2つのチュートリアルでは、フォーム認証を使用して web サイトの訪問者を識別しています。 フォーム認証フレームワークを使用すると、開発者は、ユーザーを web サイトに簡単に記録し、認証チケットを使用してページにアクセスしてそれらを記憶することが容易になります。 クラスには、 `FormsAuthentication` チケットを生成して訪問者の cookie に追加するためのメソッドが含まれています。 は、 `FormsAuthenticationModule` すべての受信要求を調べ、有効な認証チケットがある場合は、オブジェクトとオブジェクトを作成し、 `GenericPrincipal` 現在の `FormsIdentity` 要求に関連付けます。 フォーム認証は、ログイン時に訪問者に認証チケットを付与するメカニズムであり、後続の要求ではそのチケットを解析してユーザーの id を決定します。 Web アプリケーションでユーザーアカウントをサポートするには、ユーザーストアを実装し、資格情報を検証し、新しいユーザーを登録し、その他のユーザーアカウント関連タスクを無数に登録する機能を追加する必要があります。

ASP.NET 2.0 より前の開発者は、これらのユーザーアカウント関連のタスクをすべて実装するためのフックを使用していました。 幸い、ASP.NET チームはこの欠点を認識し、ASP.NET 2.0 を使用してメンバーシップフレームワークを導入しました。 メンバーシップフレームワークは、ユーザーアカウント関連の主要なタスクを実現するためのプログラムインターフェイスを提供する、.NET Framework のクラスのセットです。 このフレームワークは、 [プロバイダーモデル](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)の上に構築されています。これにより、開発者は、カスタマイズされた実装を標準化された API に組み込むことができます。

<a id="Tutorial1"></a>[*セキュリティの基本と ASP.NET のサポート*](../introduction/security-basics-and-asp-net-support-cs.md)に関するチュートリアルで説明したように、.NET Framework には、とという2つの組み込みのメンバーシッププロバイダーが付属して [`ActiveDirectoryMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) [`SqlMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) います。 その名前が示すように、では `SqlMembershipProvider` Microsoft SQL Server データベースがユーザーストアとして使用されます。 アプリケーションでこのプロバイダーを使用するには、ストアとして使用するデータベースをプロバイダーに指示する必要があります。 ご想像のとおり、では、 `SqlMembershipProvider` ユーザーストアデータベースに特定のデータベーステーブル、ビュー、およびストアドプロシージャがあることが想定されています。 この予想されるスキーマを選択したデータベースに追加する必要があります。

このチュートリアルでは、まず、を使用するために必要なスキーマをデータベースに追加する方法を調べ `SqlMembershipProvider` ます。 ここでは、スキーマの主要なテーブルを調べ、その目的と重要性について説明します。 このチュートリアルでは、メンバーシップフレームワークが使用するプロバイダーを ASP.NET アプリケーションに通知する方法について説明します。

それでは始めましょう。

## <a name="step-1-deciding-where-to-place-the-user-store"></a>手順 1: ユーザーストアを配置する場所を決定する

ASP.NET アプリケーションのデータは、通常、データベース内の複数のテーブルに格納されます。 データベーススキーマを実装する場合 `SqlMembershipProvider` は、メンバーシップスキーマをアプリケーションデータと同じデータベースに配置するか、別のデータベースに配置するかを決定する必要があります。

次の理由から、アプリケーションデータと同じデータベースにメンバーシップスキーマを配置することをお勧めします。

- **保守性** ' データが1つのデータベースにカプセル化されているアプリケーションは、2つの異なるデータベースを持つアプリケーションよりも理解、保守、配置が容易になります。
- **リレーショナル整合性** ' アプリケーションテーブルと同じデータベース内のメンバーシップ関連テーブルを検索することによって、メンバーシップ関連テーブルの主キーと関連アプリケーションテーブルの間に [外部キー制約](http://en.wikipedia.org/wiki/Foreign_key) を設定することができます。

ユーザーストアとアプリケーションデータを別々のデータベースに分離することは、それぞれが別々のデータベースを使用し、共通のユーザーストアを共有する必要がある複数のアプリケーションがある場合に、意味があります。

### <a name="creating-a-database"></a>データベースの作成

2番目のチュートリアルで作成したアプリケーションは、まだデータベースを必要としていません。 ただし、ここではユーザーストアに対して1つが必要です。 1つを作成し、プロバイダーが必要とするスキーマを追加してみましょう `SqlMembershipProvider` (手順2を参照)。

> [!NOTE]
> このチュートリアルシリーズでは、 [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) データベースを使用して、アプリケーションテーブルとスキーマを格納し `SqlMembershipProvider` ます。 この決定は次の2つの理由で行われました。まず、コストがかからないことから、Express Edition は、SQL Server 2005 の読み取り専用のバージョンです。2つ目は、SQL Server 2005 Express Edition データベースを web アプリケーションのフォルダーに直接配置し `App_Data` て、データベースと web アプリケーションを1つの ZIP ファイルにパッケージ化し、特別なセットアップ手順や構成オプションを使用せずに再展開するたいしたです。 Express Edition 以外のバージョンの SQL Server を使用したい場合は、無料でご利用いただけます。 手順はほぼ同じです。 スキーマは、 `SqlMembershipProvider` Microsoft SQL Server 2000 およびそれ以降のすべてのバージョンで動作します。

ソリューションエクスプローラーからフォルダーを右クリックし、[ `App_Data` 新しい項目の追加] を選択します。 (プロジェクトにフォルダーが表示されない場合は、 `App_Data` ソリューションエクスプローラーでプロジェクトを右クリックし、[ASP.NET フォルダーの追加] を選択して、を選択し `App_Data` ます)。[新しい項目の追加] ダイアログボックスで、という名前の新しい SQL Database を追加することを選択し `SecurityTutorials.mdf` ます。 このチュートリアルでは、 `SqlMembershipProvider` このデータベースにスキーマを追加します。以降のチュートリアルでは、アプリケーションデータをキャプチャするための追加のテーブルを作成します。

[![SecurityTutorials .mdf データベースという名前の新しい SQL Database を App_Data フォルダーに追加します。](creating-the-membership-schema-in-sql-server-cs/_static/image2.png)](creating-the-membership-schema-in-sql-server-cs/_static/image1.png)

**図 1**: データベースという名前の新しい SQL Database を `SecurityTutorials.mdf` フォルダーに追加する `App_Data` ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image3.png)されます)

フォルダーにデータベースを追加すると、そのデータベースが [ `App_Data` データベースエクスプローラー] ビューに自動的に追加されます。 (Express Edition 以外のバージョンの Visual Studio では、データベースエクスプローラーはサーバーエクスプローラーと呼ばれます)。データベースエクスプローラーにアクセスし、先ほど追加したデータベースを展開し `SecurityTutorials` ます。 画面にデータベースエクスプローラーが表示されない場合は、[表示] メニューの [データベースエクスプローラー] をクリックするか、Ctrl + Alt + S キーを押します。 図2に示すように、 `SecurityTutorials` データベースは空であり、テーブル、ビュー、およびストアドプロシージャは含まれていません。

[![SecurityTutorials データベースは現在空です](creating-the-membership-schema-in-sql-server-cs/_static/image5.png)](creating-the-membership-schema-in-sql-server-cs/_static/image4.png)

**図 2**: `SecurityTutorials` データベースが現在空です ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image6.png)されます)

## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>手順 2: `SqlMembershipProvider` データベースへのスキーマの追加

では、 `SqlMembershipProvider` ユーザーストアデータベースにインストールする特定のテーブル、ビュー、およびストアドプロシージャのセットが必要です。 これらの必要なデータベースオブジェクトは、 [ `aspnet_regsql.exe` ツール](https://msdn.microsoft.com/library/ms229862.aspx)を使用して追加できます。 このファイルは、フォルダーにあり `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\` ます。

> [!NOTE]
> このツールには、 `aspnet_regsql.exe` コマンドライン機能とグラフィカルユーザーインターフェイスの両方が用意されています。 グラフィカルインターフェイスは、ユーザーにとってわかりやすく、このチュートリアルで検証するものです。 コマンドラインインターフェイスは、 `SqlMembershipProvider` ビルドスクリプトや自動テストのシナリオなどで、スキーマの追加を自動化する必要がある場合に便利です。

この `aspnet_regsql.exe` ツールは、指定された SQL Server データベースに対して *ASP.NET アプリケーションサービス* を追加または削除するために使用されます。 ASP.NET アプリケーションサービスには、およびのスキーマと、 `SqlMembershipProvider` `SqlRoleProvider` 他の ASP.NET 2.0 フレームワークの SQL ベースのプロバイダーのスキーマが含まれています。 このツールには、次の2つの情報を提供する必要があり `aspnet_regsql.exe` ます。

- アプリケーションサービスを追加または削除するかどうかを指定します。
- アプリケーションサービススキーマの追加または削除の対象となるデータベース

データベースの使用を確認するプロンプトで、データベース `aspnet_regsql.exe` が存在するサーバーの名前、データベースに接続するためのセキュリティ資格情報、およびデータベース名を入力するように求められます。 Express Edition 以外の SQL Server を使用している場合は、この情報が既にわかっている必要があります。これは、ASP.NET web ページでデータベースを操作するときに接続文字列を使用して入力する必要がある情報と同じです。 ただし、フォルダー内の SQL Server 2005 Express Edition データベースを使用する場合は、サーバーとデータベースの名前を確認すること `App_Data` が少し複雑になります。

次のセクションでは、フォルダー内の SQL Server 2005 Express Edition データベースのサーバー名とデータベース名を簡単に指定する方法について説明し `App_Data` ます。 を使用していない場合は SQL Server 2005 Express Edition 「アプリケーションサービスのインストール」のセクションに進んでください。

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theapp_datafolder"></a>フォルダー内の SQL Server 2005 Express Edition データベースのサーバー名とデータベース名を確認する `App_Data`

このツールを使用するに `aspnet_regsql.exe` は、サーバー名とデータベース名を把握しておく必要があります。 サーバー名が `localhost\InstanceName` です。 最も可能性が高いのは、 *InstanceName* が `SQLExpress` です。 ただし、SQL Server 2005 Express Edition 手動でインストールした場合 (つまり、Visual Studio のインストール時に自動的にインストールしなかった場合)、別のインスタンス名を選択した可能性があります。

データベース名は、特定するのが少し厄介です。 フォルダー内のデータベース `App_Data` には、通常、データベースファイルへのパスと共に、 [グローバル一意識別子](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) を含むデータベース名が付けられます。 を使用してアプリケーションサービススキーマを追加するには、このデータベース名を決定する必要があり `aspnet_regsql.exe` ます。

データベース名を確認する最も簡単な方法は、SQL Server Management Studio を使用してデータベース名を調べることです。 SQL Server Management Studio には SQL Server 2005 データベースを管理するためのグラフィカルインターフェイスが用意されていますが、SQL Server 2005 の Express Edition には付属していません。 SQL Server Management Studio の無償 Express Edition を [ダウンロードでき](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) ます。

> [!NOTE]
> また、Express Edition 以外の SQL Server 2005 がデスクトップにインストールされている場合は、Management Studio の完全バージョンがインストールされている可能性があります。 完全バージョンを使用してデータベース名を決定するには、次に示す Express Edition の手順に従います。

まず、Visual studio を終了して、データベースファイル上の Visual Studio によって設定されたロックが閉じられていることを確認します。 次に、SQL Server Management Studio を起動し、 `localhost\InstanceName` SQL Server 2005 Express Edition のデータベースに接続します。 既に説明したように、インスタンス名はである可能性が `SQLExpress` あります。 [認証] オプションで、[Windows 認証] を選択します。

[![SQL Server 2005 Express Edition インスタンスに接続する](creating-the-membership-schema-in-sql-server-cs/_static/image8.png)](creating-the-membership-schema-in-sql-server-cs/_static/image7.png)

**図 3**: SQL Server 2005 Express Edition インスタンスに接続する ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image9.png)されます)

SQL Server 2005 Express Edition インスタンスに接続すると、データベース、セキュリティ設定、サーバーオブジェクトなどのフォルダーが Management Studio に表示されます。 [データベース] タブを展開すると、データベース `SecurityTutorials.mdf` がデータベースインスタンスに登録されて *いない* ことがわかります。最初にデータベースをアタッチする必要があります。

[データベース] フォルダーを右クリックし、コンテキストメニューの [アタッチ] をクリックします。 これにより、[データベースのアタッチ] ダイアログボックスが表示されます。 ここで、[追加] ボタンをクリックして `SecurityTutorials.mdf` データベースを参照し、[OK] をクリックします。 図4は、データベースが選択された後の [データベースのアタッチ] ダイアログボックスを示し `SecurityTutorials.mdf` ています。 図5は、データベースが正常にアタッチされた後の Management Studio のオブジェクトエクスプローラーを示しています。

[![SecurityTutorials .mdf データベースをアタッチします。](creating-the-membership-schema-in-sql-server-cs/_static/image11.png)](creating-the-membership-schema-in-sql-server-cs/_static/image10.png)

**図 4**: データベースをアタッチ `SecurityTutorials.mdf` [する (クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image12.png)されます)

[![SecurityTutorials .mdf データベースが Databases フォルダーに表示されます。](creating-the-membership-schema-in-sql-server-cs/_static/image14.png)](creating-the-membership-schema-in-sql-server-cs/_static/image13.png)

**図 5**: `SecurityTutorials.mdf` データベースが Databases フォルダーに表示される ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image15.png)されます)

図5に示すように、データベースには `SecurityTutorials.mdf` abstruse という名前が付けられています。 覚えやすい名前に変更してください (より簡単な型)。 データベースを右クリックし、コンテキストメニューの [名前の変更] をクリックして、名前を変更し `SecurityTutorialsDatabase` ます。 このようにしても、ファイル名は変更されません。データベースが SQL Server するために使用する名前だけが変更されます。

[![データベースの名前を SecurityTutorialsDatabase に変更します。](creating-the-membership-schema-in-sql-server-cs/_static/image17.png)](creating-the-membership-schema-in-sql-server-cs/_static/image16.png)

**図 6**: データベースの名前をに変更する `SecurityTutorialsDatabase` ([クリックしてフルサイズのイメージを表示する](creating-the-membership-schema-in-sql-server-cs/_static/image18.png))

この時点で、データベースファイルのサーバー名とデータベース名が `SecurityTutorials.mdf` `localhost\InstanceName` `SecurityTutorialsDatabase` それぞれとになります。 これで、ツールを使用してアプリケーションサービスをインストールする準備が整いました `aspnet_regsql.exe` 。

### <a name="installing-the-application-services"></a>アプリケーションサービスのインストール

ツールを起動するには、[ `aspnet_regsql.exe` スタート] メニューにアクセスし、[実行] を選択します。 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe`テキストボックスに「」と入力し、[OK] をクリックします。 または、エクスプローラーを使用して適切なフォルダーにドリルダウンし、ファイルをダブルクリックし `aspnet_regsql.exe` ます。 どちらの方法でも、同じ結果が得られます。

`aspnet_regsql.exe`コマンドライン引数を指定せずにツールを実行すると、ASP.NET SQL Server セットアップウィザードのグラフィカルユーザーインターフェイスが起動します。 ウィザードを使用すると、指定したデータベースの ASP.NET アプリケーションサービスを簡単に追加または削除できます。 図7に示すように、ウィザードの最初の画面には、ツールの目的が示されています。

[![ASP.NET SQL Server セットアップウィザードを使用してメンバーシップスキーマを追加する](creating-the-membership-schema-in-sql-server-cs/_static/image20.png)](creating-the-membership-schema-in-sql-server-cs/_static/image19.png)

**図 7**: ASP.NET SQL Server セットアップウィザードを使用してメンバーシップスキーマを追加する ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image21.png)されます)

ウィザードの2番目の手順では、アプリケーションサービスを追加するのか削除するのかを確認するメッセージが表示されます。 に必要なテーブル、ビュー、ストアドプロシージャを追加する必要があるため、[ `SqlMembershipProvider` アプリケーションサービスの SQL Server を構成する] オプションを選択します。 後で、データベースからこのスキーマを削除する場合は、このウィザードを再実行しますが、代わりに [既存のデータベースからアプリケーションサービス情報を削除する] オプションを選択します。

[![[アプリケーションサービスの SQL Server を構成する] オプションを選択します。](creating-the-membership-schema-in-sql-server-cs/_static/image23.png)](creating-the-membership-schema-in-sql-server-cs/_static/image22.png)

**図 8**: [アプリケーションサービスの SQL Server を構成する] オプションを選択[する (クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image24.png)されます)

3番目の手順では、データベース情報の入力が求められます。これには、サーバー名、認証情報、およびデータベース名が表示されます。 このチュートリアルに従って、にデータベースを追加し、にアタッチして、名前をに変更した場合は `SecurityTutorials.mdf` `App_Data` `localhost\InstanceName` `SecurityTutorialsDatabase` 、次の値を使用します。

- サーバー: `localhost\InstanceName`
- Windows 認証
- データベース `SecurityTutorialsDatabase`

[![データベース情報を入力してください](creating-the-membership-schema-in-sql-server-cs/_static/image26.png)](creating-the-membership-schema-in-sql-server-cs/_static/image25.png)

**図 9**: データベース情報を入力[する (クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image27.png)されます)

データベース情報を入力したら、[次へ] をクリックします。 最後の手順では、実行される手順の概要を示します。 [次へ] をクリックしてアプリケーションサービスをインストールし、[完了] をクリックしてウィザードを完了します。

> [!NOTE]
> Management Studio を使用してデータベースをアタッチし、データベースファイルの名前を変更した場合は、Visual Studio を再度開く前に、データベースをデタッチして Management Studio を閉じるようにしてください。 データベースをデタッチするには、 `SecurityTutorialsDatabase` データベース名を右クリックし、[タスク] メニューの [デタッチ] をクリックします。

ウィザードが完了したら、Visual Studio に戻り、データベースエクスプローラーに移動します。 [テーブル] フォルダーを展開します。 名前がプレフィックスで始まる一連のテーブルが表示さ `aspnet_` れます。 同様に、さまざまなビューやストアドプロシージャは、[ビュー] フォルダーと [ストアドプロシージャ] フォルダーにあります。 これらのデータベースオブジェクトは、アプリケーションサービススキーマを構成します。 ここでは、手順 3. でメンバーシップとロール固有のデータベースオブジェクトについて説明します。

[![さまざまなテーブル、ビュー、ストアドプロシージャがデータベースに追加されました。](creating-the-membership-schema-in-sql-server-cs/_static/image29.png)](creating-the-membership-schema-in-sql-server-cs/_static/image28.png)

**図 10**: さまざまなテーブル、ビュー、ストアドプロシージャがデータベースに追加されました ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image30.png)されます)

> [!NOTE]
> `aspnet_regsql.exe`ツールのグラフィカルユーザーインターフェイスによって、アプリケーションサービススキーマ全体がインストールされます。 しかし、コマンドラインから実行する場合は、 `aspnet_regsql.exe` インストールする特定のアプリケーションサービスコンポーネント (または削除) を指定できます。 したがって、およびプロバイダーに必要なテーブル、ビュー、およびストアドプロシージャだけを追加する場合は、 `SqlMembershipProvider` `SqlRoleProvider` `aspnet_regsql.exe` コマンドラインからを実行します。 または、によって使用される T-sql 作成スクリプトの適切なサブセットを手動で実行することもでき `aspnet_regsql.exe` ます。 これらのスクリプトは、、、、、 `WINDIR%\Microsoft.Net\Framework\v2.0.50727\` などの名前のフォルダーにあり `InstallCommon.sql` `InstallMembership.sql` `InstallRoles.sql` `InstallProfile.sql` `InstallSqlState.sql` ます。

この時点で、に必要なデータベースオブジェクトが作成されました `SqlMembershipProvider` 。 ただし、を使用する必要があることをメンバーシップフレームワークに指示する必要があります (つまり、を使用する必要があり `SqlMembershipProvider` `ActiveDirectoryMembershipProvider` ます)。また、でデータベースを使用する必要があり `SqlMembershipProvider` `SecurityTutorials` ます。 ここでは、使用するプロバイダーを指定する方法と、手順 4. で選択したプロバイダーの設定をカスタマイズする方法について説明します。 しかし、まず、作成したデータベースオブジェクトについて詳しく見ていきましょう。

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>手順 3: スキーマのコアテーブルを確認する

ASP.NET アプリケーションでメンバーシップとロールのフレームワークを使用する場合、実装の詳細はプロバイダーによってカプセル化されます。 今後のチュートリアルでは、これらのフレームワークとのインターフェイスとして、.NET Framework の `Membership` クラスとクラスを使用し `Roles` ます。 これらの高レベルの Api を使用する場合、実行されるクエリや、およびによって変更されるテーブルなど、下位レベルの詳細について心配する必要はありません `SqlMembershipProvider` `SqlRoleProvider` 。

これにより、手順2で作成したデータベーススキーマを調べることなく、メンバーシップとロールのフレームワークを自信を持って使用することができます。 ただし、アプリケーションデータを格納するテーブルを作成する場合は、ユーザーまたはロールに関連するエンティティの作成が必要になることがあります。 `SqlMembershipProvider` `SqlRoleProvider` アプリケーションデータテーブルと、手順 2. で作成したテーブルとの間で外部キー制約を確立するときに、スキーマとスキーマについての知識を持つことができます。 さらに、まれに、ユーザーとロールのストアを、クラスまたはクラスを使用するのではなく、データベースレベルで直接やり取りすることが必要になる場合があり `Membership` `Roles` ます。

### <a name="partitioning-the-user-store-into-applications"></a>ユーザーストアをアプリケーションにパーティション分割する

メンバーシップとロールのフレームワークは、1人のユーザーとロールストアをさまざまなアプリケーション間で共有できるように設計されています。 メンバーシップまたはロールのフレームワークを使用する ASP.NET アプリケーションでは、使用するアプリケーションパーティションを指定する必要があります。 つまり、複数の web アプリケーションで同じユーザーおよびロールストアを使用できます。 図11は、HRSite、顧客サイト、SalesSite という3つのアプリケーションにパーティション分割されているユーザーとロールのストアを示しています。 これら3つの web アプリケーションはそれぞれ独自のユーザーとロールを持っていますが、ユーザーアカウントとロール情報は、物理的に同じデータベーステーブルに格納されています。

[![ユーザーアカウントが複数のアプリケーションでパーティション分割される場合がある](creating-the-membership-schema-in-sql-server-cs/_static/image32.png)](creating-the-membership-schema-in-sql-server-cs/_static/image31.png)

**図 11**: ユーザーアカウントが複数のアプリケーションでパーティション分割されている場合 ([クリックすると、フルサイズの画像が表示](creating-the-membership-schema-in-sql-server-cs/_static/image33.png)されます)

これらのパーティションは、テーブルによって `aspnet_Applications` 定義されます。 データベースを使用してユーザーアカウント情報を格納する各アプリケーションは、このテーブルの行によって表されます。 `aspnet_Applications`テーブルには、、、、およびの4つの列があり `ApplicationId` `ApplicationName` `LoweredApplicationName` `Description` ます。 `ApplicationId` の型は [`uniqueidentifier`](https://msdn.microsoft.com/library/ms187942.aspx) で、テーブルの主キーです。は、 `ApplicationName` アプリケーションごとにわかりやすい一意の名前を提供します。

その他のメンバーシップおよびロールに関連するテーブルは、のフィールドにリンクし `ApplicationId` `aspnet_Applications` ます。 たとえば、 `aspnet_Users` 各ユーザーアカウントのレコードを含むテーブルには、 `ApplicationId` テーブルの外部キーフィールド (ditto) があり `aspnet_Roles` ます。 `ApplicationId`これらのテーブルのフィールドは、ユーザーアカウントまたはロールが属しているアプリケーションパーティションを指定します。

### <a name="storing-user-account-information"></a>ユーザーアカウント情報の保存

ユーザーアカウント情報は、との2つのテーブルに格納され `aspnet_Users` `aspnet_Membership` ます。 このテーブルには、 `aspnet_Users` 重要なユーザーアカウント情報を保持するフィールドが含まれています。 最も関連する3つの列は次のとおりです。

- `UserId`
- `UserName`
- `ApplicationId`

`UserId` は主キー (型 `uniqueidentifier` ) です。 `UserName` の型はで、 `nvarchar(256)` パスワードと共に、ユーザーの資格情報が構成されます。 (ユーザーのパスワードはテーブルに格納され `aspnet_Membership` ます) `ApplicationId` 。ユーザーアカウントをの特定のアプリケーションにリンク `aspnet_Applications` します。 列と列には複合[ `UNIQUE` 制約](https://msdn.microsoft.com/library/ms191166.aspx)があり `UserName` `ApplicationId` ます。 これにより、特定のアプリケーションで各ユーザー名が一意であることが保証されますが、同じ `UserName` を異なるアプリケーションで使用することができます。

この表には、 `aspnet_Membership` ユーザーのパスワード、電子メールアドレス、最後にログインした日付と時刻などの追加のユーザーアカウント情報が含まれています。 テーブルとテーブルのレコードの間には1対1の対応があり `aspnet_Users` `aspnet_Membership` ます。 このリレーションシップは `UserId` `aspnet_Membership` 、テーブルの主キーとして機能するのフィールドによって保証されます。 テーブルと同様に `aspnet_Users` 、には、 `aspnet_Membership` `ApplicationId` この情報を特定のアプリケーションパーティションに結び付けるフィールドが含まれています。

### <a name="securing-passwords"></a>パスワードのセキュリティ保護

パスワード情報はテーブルに格納され `aspnet_Membership` ます。 では、 `SqlMembershipProvider` 次の3つの方法のいずれかを使用して、パスワードをデータベースに格納できます。

- [**クリア**]-パスワードはプレーンテキストとしてデータベースに格納されます。 このオプションを使用しないことを強くお勧めします。 データベースが侵害された場合、データベースへのアクセスが許可されているハッカーがデータベースに侵入したとしても、すべてのユーザーの資格情報が存在することになります。
- **ハッシュ** -パスワードは、一方向のハッシュアルゴリズムとランダムに生成された salt 値を使用してハッシュされます。 このハッシュ値 (salt) は、データベースに格納されます。
- **暗号化** -パスワードの暗号化されたバージョンがデータベースに格納されます。

使用されるパスワードストレージ手法は、「 `SqlMembershipProvider` 」で指定した設定によって異なり `Web.config` ます。 ここでは、手順 4. の設定のカスタマイズについて説明 `SqlMembershipProvider` します。 既定の動作では、パスワードのハッシュが保存されます。

パスワードを格納する列は、、 `Password` 、 `PasswordFormat` および `PasswordSalt` です。 `PasswordFormat` は、 `int` パスワードの格納に使用される方法を示す値を持つ型のフィールドです。このフィールドの値は、クリアの場合は0、ハッシュの場合は1、暗号化されている場合は2です。 `PasswordSalt` では、使用されるパスワードストレージ手法に関係なく、ランダムに生成された文字列が割り当てられます。の値 `PasswordSalt` は、パスワードのハッシュを計算するときにのみ使用されます。 最後に、 `Password` この列には、実際のパスワードデータ、プレーンテキストのパスワード、パスワードのハッシュ、または暗号化されたパスワードが含まれます。

表1は、パスワード MySecret を格納するときに、これら3つの列がさまざまなストレージ手法でどのように表示されるかを示しています。 .

| **ストレージ手法 &lt; \_ o3a \_ p/&gt;** | **パスワード &lt; \_ o3a \_ p/&gt;** | **PasswordFormat &lt; \_ o3a \_ p/&gt;** | **PasswordSalt &lt; \_ o3a \_ p/&gt;** |
| --- | --- | --- | --- |
| Clear | MySecret! | 0 | tTnkPlesqissc2y2SMEygA = = |
| ハッシュ | 2oXm6sZHWbTHFgjgkGQsc2Ec9ZM = | 1 | wFgjUfhdUFOCKQiI61vtiQ = = |
| Encrypted | 62RZgDvhxykkqsMchZ0Yly7HS6onhpaoCYaRxV8g0F4CW56OXUU3e7Inza9j9BKp | 2 | LSRzhGS/aa/oqAXGLHJNBw = = |

**表 1**: パスワード Mysecret を保存するときのパスワード関連のフィールドの値の例

> [!NOTE]
> によって使用される特定の暗号化アルゴリズムまたはハッシュアルゴリズム `SqlMembershipProvider` は、要素の設定によって決まり `<machineKey>` ます。 <a id="Tutorial3"></a> [*「フォーム認証の構成」と「高度なトピック*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)」のチュートリアルの手順3で、この構成要素について説明しました。

### <a name="storing-roles-and-role-associations"></a>ロールとロールの関連付けの格納

ロールフレームワークを使用すると、開発者は一連のロールを定義し、ユーザーがどのロールに属しているかを指定できます。 この情報は、との2つのテーブルを通じてデータベースにキャプチャされ `aspnet_Roles` `aspnet_UsersInRoles` ます。 テーブル内の各レコードは、 `aspnet_Roles` 特定のアプリケーションのロールを表します。 テーブルと同様に、テーブルには、ここ `aspnet_Users` で `aspnet_Roles` 説明する3つの列があります。

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId` は主キー (型 `uniqueidentifier` ) です。 `RoleName` は `nvarchar(256)` 型です。 と `ApplicationId` は、ユーザーアカウントをの特定のアプリケーションにリンクし `aspnet_Applications` ます。 `UNIQUE`列と列には複合制約があるため `RoleName` `ApplicationId` 、特定のアプリケーションで各ロール名が一意であることが保証されます。

この `aspnet_UsersInRoles` テーブルは、ユーザーとロールの間のマッピングとして機能します。 2つの列とがあり、 `UserId` `RoleId` 両方とも複合主キーを構成しています。

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>手順 4: プロバイダーを指定し、その設定をカスタマイズする

メンバーシップやロールのフレームワークなど、プロバイダーモデルをサポートするすべてのフレームワーク-実装の詳細がないため、その責任をプロバイダークラスに委任します。 メンバーシップフレームワークの場合、 `Membership` クラスはユーザーアカウントを管理するための API を定義しますが、ユーザーストアと直接対話することはありません。 `Membership`クラスのメソッドは、構成されたプロバイダーに要求を渡すのではなく、を使用し `SqlMembershipProvider` ます。 クラスのメソッドのいずれかを呼び出すと、 `Membership` メンバーシップフレームワークは、の呼び出しをデリゲートすることをどのように認識し `SqlMembershipProvider` ますか。

`Membership`クラスには、メンバーシップフレームワークで使用できるすべての登録済みプロバイダークラスへの参照を含む[ `Providers` プロパティ](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx)があります。 登録された各プロバイダーには、関連付けられた名前と型があります。 名前には、コレクション内の特定のプロバイダーを参照するためのわかりやすい方法が用意されて `Providers` いますが、型はプロバイダークラスを識別します。 さらに、登録された各プロバイダーには、構成設定が含まれる場合があります。 メンバーシップフレームワークの構成設定には、 `passwordFormat` やなどが含ま `requiresUniqueEmail` れます。 によって使用される構成設定の完全な一覧については、表2を参照してください `SqlMembershipProvider` 。

`Providers`プロパティの内容は、web アプリケーションの構成設定によって指定されます。 既定では、すべての web アプリケーションには型のという名前のプロバイダーがあり `AspNetSqlMembershipProvider` `SqlMembershipProvider` ます。 この既定のメンバーシッププロバイダーは、に登録されてい `machine.config` ます (にあり `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG)` ます)。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample1.xml)]

上のマークアップが示すように、 [ `<membership>` 要素](https://msdn.microsoft.com/library/1b9hw62f.aspx)はメンバーシップフレームワークの構成設定を定義しますが、 [ `<providers>` 子要素](https://msdn.microsoft.com/library/6d4936ht.aspx)は登録されたプロバイダーを指定します。 プロバイダーは、要素または要素を使用して追加または削除できます。現在登録されている [`<add>`](https://msdn.microsoft.com/library/whae3t94.aspx) [`<remove>`](https://msdn.microsoft.com/library/aykw9a6d.aspx) すべての [`<clear>`](https://msdn.microsoft.com/library/t062y6yc.aspx) プロバイダーを削除するには、要素を使用します。 上のマークアップに示されているように、には `machine.config` 型のという名前のプロバイダーが追加され `AspNetSqlMembershipProvider` `SqlMembershipProvider` ます。

要素には、 `name` 属性と属性に加え `type` `<add>` て、さまざまな構成設定の値を定義する属性が含まれています。 表2に、使用可能な `SqlMembershipProvider` 固有の構成設定とそれぞれの説明を示します。

> [!NOTE]
> 表2に示されている既定値は、クラスで定義されている既定値を示し `SqlMembershipProvider` ます。 のすべての構成設定が `AspNetSqlMembershipProvider` クラスの既定値に対応しているわけではないことに注意 `SqlMembershipProvider` してください。 たとえば、メンバーシッププロバイダーで指定されていない場合、 `requiresUniqueEmail` 設定の既定値は true です。 ただし、は、 `AspNetSqlMembershipProvider` の値を明示的に指定することによって、この既定値をオーバーライドし `false` ます。

| **&lt; \_ O3a \_ p/の設定&gt;** | **説明 &lt; \_ o3a \_ p/&gt;** |
| --- | --- |
| `ApplicationName` | メンバーシップフレームワークによって、単一のユーザーストアを複数のアプリケーションでパーティション分割できることを思い出してください。 この設定は、メンバーシッププロバイダーによって使用されるアプリケーションパーティションの名前を示します。 この値が明示的に指定されていない場合は、実行時にアプリケーションの仮想ルートパスの値に設定されます。 |
| `commandTimeout` | SQL コマンドのタイムアウト値を秒単位で指定します。 既定値は 30 です。 |
| `connectionStringName` | `<connectionStrings>`ユーザーストアデータベースへの接続に使用する要素内の接続文字列の名前。 この値は必須です。 |
| `description` | 登録されているプロバイダーについてのわかりやすい説明を提供します。 |
| `enablePasswordRetrieval` | ユーザーが忘れたパスワードを取得できるかどうかを指定します。 既定値は `false` です。 |
| `enablePasswordReset` | ユーザーがパスワードのリセットを許可されているかどうかを示します。 既定値は `true` です。 |
| `maxInvalidPasswordAttempts` | 指定されたユーザーがロックアウトされるまでに、特定のユーザーに対して失敗したログイン試行の最大回数 `passwordAttemptWindow` 。既定値は5です。 |
| `minRequiredNonalphanumericCharacters` | ユーザーのパスワードに表示する必要がある英数字以外の文字の最小数。 この値は 0 ~ 128 の範囲で指定する必要があります。既定値は1です。 |
| `minRequiredPasswordLength` | パスワードに必要な最小文字数。 この値は 0 ~ 128 の範囲で指定する必要があります。既定値は7です。 |
| `name` | 登録されているプロバイダーの名前。 この値は必須です。 |
| `passwordAttemptWindow` | 失敗したログイン試行が追跡される時間 (分単位)。 この指定した期間内にユーザーが無効なログイン資格情報を指定した場合は `maxInvalidPasswordAttempts` 、ロックアウトされます。既定値は10です。 |
| `PasswordFormat` | パスワードの格納形式: `Clear` 、 `Hashed` 、または `Encrypted` 。 既定値は、`Hashed` です。 |
| `passwordStrengthRegularExpression` | 指定されている場合、この正規表現を使用して、新しいアカウントを作成するとき、またはパスワードを変更するときに、ユーザーが選択したパスワードの強度を評価します。 既定値は空の文字列です。 |
| `requiresQuestionAndAnswer` | パスワードを取得またはリセットするときに、ユーザーがセキュリティの質問に答える必要があるかどうかを指定します。 既定値は `true` です。 |
| `requiresUniqueEmail` | 特定のアプリケーションパーティション内のすべてのユーザーアカウントが一意の電子メールアドレスを持つ必要があるかどうかを示します。 既定値は `true` です。 |
| `type` | プロバイダーの種類を指定します。 この値は必須です。 |

**表 2**: メンバーシップと `SqlMembershipProvider` 構成設定

に加え `AspNetSqlMembershipProvider` て、他のメンバーシッププロバイダーは、同様のマークアップをファイルに追加することによって、アプリケーションごとに登録でき `Web.config` ます。

> [!NOTE]
> ロールフレームワークはほぼ同じように機能します。には既定の登録済みロールプロバイダーがあり、登録され `machine.config` たプロバイダーはのアプリケーションごとにカスタマイズできます `Web.config` 。 ロールフレームワークとその構成マークアップについては、今後のチュートリアルで詳しく説明します。

### <a name="customizing-thesqlmembershipprovidersettings"></a>設定のカスタマイズ `SqlMembershipProvider`

既定 () では、 `SqlMembershipProvider` `AspNetSqlMembershipProvider` 属性がに設定されてい `connectionStringName` `LocalSqlServer` ます。 プロバイダーと同様に、 `AspNetSqlMembershipProvider` 接続文字列名 `LocalSqlServer` はで定義され `machine.config` ます。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample2.xml)]

ご覧のとおり、この接続文字列では | にある SQL 2005 Express Edition データベースが定義されています。DataDirectory | aspnetdb.mdf。 String |DataDirectory |実行時にはディレクトリを指すように変換さ `~/App_Data/` れるので、データベースパス |DataDirectory | aspnetdb.mdf はに変換さ `~/App_Data` / `aspnet.mdf` れます。

アプリケーションのファイルでメンバーシッププロバイダー情報を指定しなかった場合、 `Web.config` アプリケーションは既定の登録されたメンバーシッププロバイダーであるを使用し `AspNetSqlMembershipProvider` ます。 データベースが存在しない場合は、 `~/App_Data/aspnet.mdf` ASP.NET ランタイムによって自動的に作成され、アプリケーションサービススキーマが追加されます。 ただし、データベースを使用するので `aspnet.mdf` はなく、 `SecurityTutorials.mdf` 手順 2. で作成したデータベースを使用します。 この変更は、次の2つの方法のいずれかで行うことができます。

- の<strong>値を指定します</strong> <strong>`LocalSqlServer`</strong> 。<strong>接続文字列名</strong> <strong>`Web.config`</strong><strong>.</strong> の接続文字列名の値を上書きすることにより `LocalSqlServer` `Web.config` 、既定の登録済みメンバーシッププロバイダー () を使用して、 `AspNetSqlMembershipProvider` データベースと正しく連携させることができ `SecurityTutorials.mdf` ます。 で指定された構成設定を使用してコンテンツを作成する場合は、この方法が適してい `AspNetSqlMembershipProvider` ます。 この手法の詳細については、 [Scott Guthrie](https://weblogs.asp.net/scottgu/)のブログ記事「 [SQL Server 2000 または SQL Server 2005 を使用するように ASP.NET 2.0 アプリケーションサービスを構成する](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)」を参照してください。
- <strong>型の新しい登録済みプロバイダーを追加します</strong> <strong>`SqlMembershipProvider`</strong> 。<strong>およびを構成</strong> <strong>`connectionStringName`</strong> します。を<strong>指すように設定します</strong> <strong>`SecurityTutorials.mdf`</strong> 。<strong>データベース。</strong> この方法は、データベース接続文字列に加えて他の構成プロパティをカスタマイズする場合に便利です。 独自のプロジェクトでは、柔軟性と読みやすさのため、常にこの方法を使用します。

データベースを参照する新しい登録済みプロバイダーを追加する前に `SecurityTutorials.mdf` 、まずのセクションに適切な接続文字列値を追加する必要があり `<connectionStrings>` `Web.config` ます。 次のマークアップは、 `SecurityTutorialsConnectionString` フォルダー内の SQL Server 2005 Express Edition データベースを参照するという名前の新しい接続文字列を追加し `SecurityTutorials.mdf` `App_Data` ます。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample3.xml)]

> [!NOTE]
> 代替データベースファイルを使用する場合は、必要に応じて接続文字列を更新します。 正しい接続文字列を形成する方法の詳細については、 [ConnectionStrings.com](http://www.connectionstrings.com/)を参照してください。

次に、次のメンバーシップ構成マークアップをファイルに追加し `Web.config` ます。 このマークアップは、という名前の新しいプロバイダーを登録 `SecurityTutorialsSqlMembershipProvider` します。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample4.xml)]

上のマークアップでは、プロバイダーを登録するだけでなく `SecurityTutorialsSqlMembershipProvider` 、を `SecurityTutorialsSqlMembershipProvider` 既定のプロバイダーとして定義して `defaultProvider` います (要素の属性を使用 `<membership>` )。 メンバーシップフレームワークは複数の登録済みプロバイダーを持つことができることを思い出してください。 `AspNetSqlMembershipProvider`はの最初のプロバイダーとして登録されるため `machine.config` 、特に指定しない限り、既定のプロバイダーとして機能します。

現在、アプリケーションには、とという2つの登録済みプロバイダーがあり `AspNetSqlMembershipProvider` `SecurityTutorialsSqlMembershipProvider` ます。 ただし、プロバイダーを登録する前に、要素の直前に `SecurityTutorialsSqlMembershipProvider` [ `<clear />` 要素](https://msdn.microsoft.com/library/t062y6yc.aspx)を追加することで、以前に登録されたすべてのプロバイダーを消去でき `<add>` ます。 これにより、登録されている `AspNetSqlMembershipProvider` プロバイダーの一覧からがクリアされます。つまり、が登録されている `SecurityTutorialsSqlMembershipProvider` 唯一のメンバーシッププロバイダーになります。 この方法を使用した場合は、を既定のプロバイダーとしてマークする必要はありません。これは、登録されている `SecurityTutorialsSqlMembershipProvider` 唯一のメンバーシッププロバイダーであるためです。 の使用方法の詳細について `<clear />` は、「 [ `<clear />` プロバイダーを追加するとき](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)のの使用」を参照してください。

`SecurityTutorialsSqlMembershipProvider`の設定は、 `connectionStringName` 追加された `SecurityTutorialsConnectionString` 接続文字列名を参照し、その `applicationName` 設定が securitytutorials の値に設定されていることに注意してください。 また、この `requiresUniqueEmail` 設定はに設定されてい `true` ます。 他のすべての構成オプションは、の値と同じ `AspNetSqlMembershipProvider` です。 必要に応じて、ここで自由に構成を変更することができます。 たとえば、1つではなく2つの英数字以外の文字を必要とすることによって、または7ではなく8文字になるようにパスワードの長さを増やすことで、パスワードの強度を強化することができます。

> [!NOTE]
> メンバーシップフレームワークによって、単一のユーザーストアを複数のアプリケーションでパーティション分割できることを思い出してください。 メンバーシッププロバイダーの設定は、 `applicationName` ユーザーストアを操作するときにプロバイダーが使用するアプリケーションを示します。 `applicationName`が明示的に設定されていない場合は、 `applicationName` 実行時に web アプリケーションの仮想ルートパスに割り当てられるため、構成設定の値を明示的に設定することが重要です。 アプリケーションの仮想ルートパスが変更されない限り、これは問題なく動作しますが、アプリケーションを別のパスに移動した場合は、 `applicationName` 設定も変更されます。 この場合、メンバーシッププロバイダーは、以前に使用されていたものとは異なるアプリケーションパーティションを使用して作業を開始します。 移動前に作成されたユーザーアカウントは別のアプリケーションパーティションに存在するため、これらのユーザーはサイトにログインできなくなります。 この問題の詳細については、「 [ `applicationName` ASP.NET 2.0 のメンバーシップとその他のプロバイダーを構成するときに常にプロパティを設定する](https://weblogs.asp.net/scottgu/443634)」を参照してください。

## <a name="summary"></a>まとめ

この時点で、構成済みのアプリケーションサービス () を持つデータベースがあり、 `SecurityTutorials.mdf` メンバーシップフレームワークが登録したプロバイダーを使用するように web アプリケーションを構成しました `SecurityTutorialsSqlMembershipProvider` 。 この登録されたプロバイダーの種類は `SqlMembershipProvider` で、が `connectionStringName` 適切な接続文字列 () に設定され、 `SecurityTutorialsConnectionString` その値が明示的に設定されてい `applicationName` ます。

これで、アプリケーションからメンバーシップフレームワークを使用する準備ができました。 次のチュートリアルでは、新しいユーザーアカウントを作成する方法について説明します。 次に、ユーザーの認証、ユーザーベースの承認の実行、およびデータベースへの追加のユーザー関連情報の格納について説明します。

プログラミングを楽しんでください。

### <a name="further-reading"></a>もっと読む

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [`applicationName`ASP.NET 2.0 メンバーシップとその他のプロバイダーを構成する場合は、常にプロパティを設定する](https://weblogs.asp.net/scottgu/443634)
- [SQL Server 2000 または SQL Server 2005 を使用するように ASP.NET 2.0 アプリケーションサービスを構成する](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [Express Edition のダウンロード SQL Server Management Studio](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [ASP.NET 2.0 のメンバーシップ、ロール、およびプロファイルを調べています](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [`<add>`メンバーシップのプロバイダーの要素](https://msdn.microsoft.com/library/whae3t94.aspx)
- [`<membership>`要素](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [`<providers>`メンバーシップの要素](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [使用 `<clear />` (プロバイダーを追加するときに)](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [を直接操作する `SqlMembershipProvider`](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>このチュートリアルに含まれるトピックのビデオトレーニング

- [ASP.NET メンバーシップについて理解する](../../../videos/authentication/understanding-aspnet-memberships.md)
- [メンバーシップ スキーマと連動するように SQL を構成する](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [既定のメンバーシップ スキーマのメンバーシップ設定を変更する](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 、またはブログでにアクセスでき [http://ScottOnWriting.NET](http://scottonwriting.net/) ます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは Alicja Maziarz でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、に行をドロップ [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com) します。

> [!div class="step-by-step"]
> [次へ](creating-user-accounts-cs.md)
