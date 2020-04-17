---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
title: 'イテレーション #1 – アプリケーションの作成 (C#) |マイクロソフトドキュメント'
author: rick-anderson
description: '最初のイテレーションでは、できるだけ簡単な方法で連絡先マネージャーを作成します。 基本的なデータベース操作のサポートを追加します: 作成、読み取り、更新、および D..'
ms.author: riande
ms.date: 02/20/2009
ms.assetid: db0f160b-901c-46d3-865e-7ab6cd4ed68d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
msc.type: authoredcontent
ms.openlocfilehash: ecc3c1201c784e20c6b2601735bee3d4ce721f22
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542548"
---
# <a name="iteration-1--create-the-application-c"></a>繰り返し #1 – アプリケーションを作成する (C#)

[マイクロソフト](https://github.com/microsoft)

[コードをダウンロード](iteration-1-create-the-application-cs/_static/contactmanager_1_cs1.zip)

> 最初のイテレーションでは、できるだけ簡単な方法で連絡先マネージャーを作成します。 基本的なデータベース操作のサポートを追加: 作成、読み取り、更新、および削除 (CRUD) 。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>MVC アプリケーション (VB) ASP.NET連絡先管理の構築

この一連のチュートリアルでは、最初から最後まで連絡先管理アプリケーション全体を構築します。 連絡先マネージャー アプリケーションでは、連絡先の情報 (名前、電話番号、電子メール アドレス) を保存できます。

複数のイテレーションでアプリケーションをビルドします。 各反復処理で、アプリケーションを徐々に改善します。 この複数の反復アプローチの目的は、各変更の理由を理解できるようにすることです。

- イテレーション #1 - アプリケーションを作成します。 最初のイテレーションでは、できるだけ簡単な方法で連絡先マネージャーを作成します。 基本的なデータベース操作のサポートを追加: 作成、読み取り、更新、および削除 (CRUD) 。

- イテレーション #2 - アプリケーションを見栄えよくします。 このイテレーションでは、既定の ASP.NET MVC ビュー マスター ページとカスケード スタイル シートを変更することで、アプリケーションの外観を向上させます。

- イテレーション #3 - フォームの検証を追加します。 3 回目のイテレーションでは、基本的なフォーム検証を追加します。 必須のフォームフィールドに入力せずにフォームを送信できないようにします。 また、メールアドレスと電話番号も検証します。

- イテレーション #4 - アプリケーションを疎結合にします。 この 4 回目のイテレーションでは、いくつかのソフトウェア設計パターンを利用して、Contact Manager アプリケーションの保守と変更を容易にします。 たとえば、リポジトリ パターンと依存関係の挿入パターンを使用するようにアプリケーションをリファクタリングします。

- イテレーション #5 - 単体テストを作成します。 5 回目のイテレーションでは、単体テストを追加することで、アプリケーションの保守と変更を容易にします。 データ モデル クラスをモックし、コントローラーと検証ロジックの単体テストをビルドします。

- イテレーション #6 - テスト駆動型開発を使用します。 この 6 回目のイテレーションでは、単体テストを最初に記述し、単体テストに対してコードを記述することで、アプリケーションに新しい機能を追加します。 このイテレーションでは、連絡先グループを追加します。

- イテレーション #7 - Ajax 機能を追加します。 7 回目のイテレーションでは、Ajax のサポートを追加することで、アプリケーションの応答性とパフォーマンスを向上させます。

## <a name="this-iteration"></a>このイテレーション

この最初のイテレーションでは、基本的なアプリケーションをビルドします。 目的は、可能な限り最速かつ簡単な方法で連絡先マネージャーを構築することです。 後のイテレーションでは、アプリケーションの設計を改善します。

連絡先マネージャー アプリケーションは、データベース駆動型の基本的なアプリケーションです。 このアプリケーションを使用して、新しい連絡先の作成、既存の連絡先の編集、および連絡先の削除を行うことができます。

このイテレーションでは、次の手順を実行します。

1. ASP.NET MVC アプリケーション
2. 連絡先を保存するデータベースを作成する
3. Microsoft エンティティ フレームワークを使用して、データベースのモデル クラスを生成します。
4. データベース内のすべての連絡先を一覧表示できるコントローラーアクションとビューを作成します。
5. データベースに新しい連絡先を作成できるコントローラーアクションとビューを作成する
6. データベース内の既存の連絡先を編集できるコントローラーアクションとビューを作成する
7. コントローラアクションと、データベース内の既存の連絡先を削除できるビューを作成する

## <a name="software-prerequisites"></a>ソフトウェアの必要なコンポーネント

ASP.NET MVC アプリケーションでは、コンピューターに Visual Studio 2008 または Visual Web 開発者 2008 がインストールされている必要があります (Visual Web 開発者は Visual Studio の拡張機能の一部を含まない Visual Studio の無料バージョンです)。 次のアドレスから、Visual Studio 2008 またはビジュアル Web 開発者の試用版をダウンロードできます。

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> ビジュアル Web 開発者を使用する ASP.NET MVC アプリケーションの場合、Visual Web 開発者サービス パック 1 がインストールされている必要があります。 サービス パック 1 を使用しない場合、Web アプリケーション プロジェクトを作成することはできません。

MVC フレームワークASP.NET。 次のアドレスからASP.NET MVC フレームワークをダウンロードできます。

[https://www.asp.net/mvc](../../../index.md)

このチュートリアルでは、Microsoft エンティティ フレームワークを使用してデータベースにアクセスします。 エンティティ フレームワークは、.NET Framework 3.5 サービス パック 1 に含まれています。 このサービス パックは、次の場所からダウンロードできます。

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;dプレイラン=エン](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

これらの各ダウンロードを 1 つずつ実行する代わりに、Web プラットフォーム インストーラ (Web PI) を利用できます。 Web PI は、次のアドレスからダウンロードできます。

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NETMVCプロジェクト

MVC Web アプリケーション プロジェクトASP.NET。 Visual Studio を起動し、メニュー オプションの **[ファイル]、[新しいプロジェクト] の順に**選択します。 **[新しいプロジェクト]** ダイアログが表示されます (図 1 参照)。 **Web**プロジェクトの種類と**ASP.NET MVC Web アプリケーション**テンプレートを選択します。 新しいプロジェクト*に名前を付け、[OK]* ボタンをクリックします。

**[新しいプロジェクト**] ダイアログの右上にあるドロップダウン リストから [.NET Framework 3.5] が選択されていることを確認します。 それ以外の場合は、mvc Web アプリケーション テンプレートASP.NETは表示されません。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image1.jpg)](iteration-1-create-the-application-cs/_static/image1.png)

**図 01**: [新しいプロジェクト] ダイアログ ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image2.png))

MVC アプリケーションASP.NET、[**単体テスト プロジェクトの作成**] ダイアログ ボックスが表示されます。 このダイアログ ボックスを使用して、ASP.NET MVC アプリケーションを作成するときに単体テスト プロジェクトを作成し、ソリューションに追加することを指定できます。 このイテレーションでは単体テストをビルドしませんが、後のイテレーションで**単体テスト**を追加する予定なので、単体テスト プロジェクトを作成するオプションを選択する必要があります。 新しいASP.NET MVC プロジェクトを作成するときにテスト プロジェクトを追加する方が、ASP.NET MVC プロジェクトが作成された後にテスト プロジェクトを追加するよりもはるかに簡単です。

> [!NOTE] 
> 
> Visual Web 開発者はテスト プロジェクトをサポートしていないため、Visual Web Developer を使用する場合は[単体テスト プロジェクトの作成]ダイアログ ボックスは表示されません。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image2.jpg)](iteration-1-create-the-application-cs/_static/image3.png)

**図 02**: [単体テスト プロジェクトの作成] ダイアログ ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image4.png)します )

ASP.NET MVC アプリケーションが Visual Studio ソリューション エクスプローラー ウィンドウに表示されます (図 3 参照)。 [ソリューション エクスプローラ] ウィンドウが表示されない場合は、メニュー オプションの **[表示] を**選択してこのウィンドウを開くことができます。 ソリューションには、ASP.NET MVC プロジェクトとテスト プロジェクトの 2 つのプロジェクトが含まれていることに注意してください。 ASP.NET MVC プロジェクトは連絡先マネージャーと名前を付け、テスト プロジェクトは、連絡先マネージャー.テストという名前です。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image3.jpg)](iteration-1-create-the-application-cs/_static/image5.png)

**図 03**: ソリューション エクスプローラ ウィンドウ ([フルサイズの画像を表示するには、ここをクリック](iteration-1-create-the-application-cs/_static/image6.png)します)

## <a name="deleting-the-project-sample-files"></a>プロジェクトサンプルファイルの削除

mvc プロジェクト テンプレートASP.NETには、コントローラーとビューのサンプル ファイルが含まれています。 新しいASP.NET MVC アプリケーションを作成する前に、これらのファイルを削除する必要があります。 [ソリューション エクスプローラ] ウィンドウでファイルまたはフォルダを削除するには、ファイルまたはフォルダを右クリックし、メニュー オプションの **[削除**] を選択します。

ASP.NET MVC プロジェクトから次のファイルを削除する必要があります。

- \コントローラ\ホームコントローラ.cs

- \ビュー\ホーム\について.aspx

- \ビュー\ホーム\インデックス.aspx

テスト プロジェクトから次のファイルを削除する必要があります。

\コントローラー\ホームコントローラーテスト.cs

## <a name="creating-the-database"></a>データベースの作成

連絡先マネージャー アプリケーションは、データベース駆動型の Web アプリケーションです。 連絡先情報を保存するためにデータベースを使用します。

マイクロソフトの SQL Server、Oracle、MySQL、および IBM DB2 データベースを含む最新のデータベースを使用して、mvc フレームワークをASP.NETします。 このチュートリアルでは、SQL Server データベースを使用します。 Visual Studio をインストールすると、無料バージョンの SQL Server データベースであるマイクロソフト SQL Server Express をインストールするオプションが提供されます。

[ソリューション エクスプローラ] ウィンドウで [App\_Data] フォルダを右クリックし、メニュー オプションの **[追加]、[ 新しい項目]** の順に選択して、新しいデータベースを作成します。 [**新しい項目の追加]** ダイアログで、[**データ**] カテゴリと **[SQL Server データベース]** テンプレートを選択します (図 4 参照)。 新しいデータベースに名前を付け、[OK] ボタンをクリックします。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image4.jpg)](iteration-1-create-the-application-cs/_static/image7.png)

**図 04**: 新しい MICROSOFT SQL Server Express データベースを作成する ([フルサイズの画像を表示するには クリック](iteration-1-create-the-application-cs/_static/image8.png))

新しいデータベースを作成すると、ソリューション エクスプローラー ウィンドウの\_[アプリ データ] フォルダーにデータベースが表示されます。 をダブルクリックして、サーバー エクスプ ローラー ウィンドウを開き、データベースに接続します。

> [!NOTE] 
> 
> サーバー エクスプローラ ウィンドウは、Visual Web 開発者の場合はデータベース エクスプローラ ウィンドウと呼ばれます。

[サーバー エクスプローラー] ウィンドウを使用して、データベース テーブル、ビュー、トリガ、ストアド プロシージャなどの新しいデータベース オブジェクトを作成できます。 [テーブル] フォルダを右クリックし、メニュー オプションの **[新しいテーブルの追加]** を選択します。 データベース テーブル デザイナが表示されます (図 5 参照)。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image5.jpg)](iteration-1-create-the-application-cs/_static/image9.png)

**図 05**: データベース テーブル デザイナ ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image10.png)します )

次の列を含むテーブルを作成する必要があります。

<a id="0.1_table01"></a>

| **列名** | **[データ型]** | **NULL を許可する** |
| --- | --- | --- |
| Id | INT | False |
| FirstName | nvarchar(50) | False |
| LastName | nvarchar(50) | False |
| Phone | nvarchar(50) | False |
| Email | nvarchar(255) | False |

最初の列である Id 列は特別です。 ID 列を ID 列と主キー列としてマークする必要があります。 列が ID 列であることを示すには、列のプロパティを展開して (図 6 の下部を参照)、下にスクロールして、ID 仕様プロパティです。 **(Is Identity)** プロパティを値**Yes**に設定します。

列を主キー列としてマークするには、列を選択し、キーのアイコンが表示されたボタンをクリックします。 列が主キー列としてマークされると、列の横にキーのアイコンが表示されます (図 6 参照)。

テーブルの作成が完了したら、[保存] ボタン (フロッピーのアイコンが付いたボタン) をクリックして、新しいテーブルを保存します。 新しいテーブルに連絡先という名前*を付けます*。

連絡先データベース テーブルの作成が完了したら、テーブルにいくつかのレコードを追加する必要があります。 サーバー エクスプローラ ウィンドウで連絡先テーブルを右クリックし、メニュー オプションの **[テーブル データの表示**] を選択します。 表示されるグリッドに 1 つまたは複数の連絡先を入力します。

## <a name="creating-the-data-model"></a>データ モデルの作成

ASP.NET MVC アプリケーションは、モデル、ビュー、およびコント ローラーで構成されます。 まず、前のセクションで作成した連絡先テーブルを表す Model クラスを作成します。

このチュートリアルでは、Microsoft エンティティ フレームワークを使用して、データベースからモデル クラスを自動的に生成します。

> [!NOTE] 
> 
> ASP.NET MVC フレームワークは、マイクロソフト エンティティ フレームワークに関連付けられてはなりません。 ASP.NET MVC は、NHibernate、LINQ to SQL、またはADO.NETなどの代替データベース アクセス テクノロジで使用できます。

データ モデル クラスを作成するには、次の手順に従います。

1. ソリューション エクスプローラ ウィンドウで Models フォルダを右クリックし **、[追加]、[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログが表示されます (図 6 参照)。
2. [**データ**] カテゴリと **[エンティティ データ モデルADO.NET**テンプレートを選択します。 データ モデルに*名前を付け*、[**追加**] ボタンをクリックします。 エンティティ データ モデル ウィザードが表示されます (図 7 を参照)。
3. [**モデルコンテンツの選択]** ステップで、[**データベースから生成]** を選択します (図 7 を参照)。
4. [**データ接続の選択]** ステップで、ContactManagerDB.mdf データベースを選択し、エンティティ接続設定の*名前を*入力します (図 8 を参照)。
5. [**データベース オブジェクトの選択]** ステップで、[テーブル] というラベルのチェック ボックスをオンにします (図 9 を参照)。 データ モデルには、データベースに含まれるすべてのテーブルが含まれます (連絡先テーブルは 1 つだけです)。 名前空間を入力*してモデルを作成*します。 [完了] をクリックしてウィザードを完了します。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image6.jpg)](iteration-1-create-the-application-cs/_static/image11.png)

**図 06**: [新しい項目の追加] ダイアログ ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image12.png)して)

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image7.jpg)](iteration-1-create-the-application-cs/_static/image13.png)

**図07**: モデルコンテンツの選択 ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image14.png))

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image8.jpg)](iteration-1-create-the-application-cs/_static/image15.png)

**図 08**: データ接続を選択する ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image16.png)して )

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image9.jpg)](iteration-1-create-the-application-cs/_static/image17.png)

**図 09**: データベース オブジェクトを選択する ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image18.png)します )

エンティティ データ モデル ウィザードを完了すると、エンティティ データ モデル デザイナーが表示されます。 デザイナーは、モデル化されている各テーブルに対応するクラスを表示します。 連絡先という名前のクラスが 1 つ表示されます。

エンティティ データ モデル ウィザードは、データベース テーブル名に基づいてクラス名を生成します。 ほとんどの場合、ウィザードによって生成されるクラスの名前を変更する必要があります。 デザイナーで連絡先クラスを右クリックし、メニュー オプションの名前の**変更**を選択します。 クラスの名前を連絡先 (複数形) から連絡先 (単数) に変更します。 クラス名を変更すると、クラスは図 10 のようになります。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image10.jpg)](iteration-1-create-the-application-cs/_static/image19.png)

**図10**: コンタクトクラス ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image20.png))

この時点で、データベース モデルを作成しました。 Contact クラスを使用して、データベース内の特定の取引先担当者レコードを表すことができます。

## <a name="creating-the-home-controller"></a>ホームコントローラの作成

次のステップは、ホームコントローラーを作成することです。 ホーム コント ローラーは、ASP.NET MVC アプリケーションで呼び出される既定のコント ローラーです。

[ソリューション エクスプローラー] ウィンドウで [コントローラー] フォルダーを右クリックし、メニュー オプション**の [追加]、[コントローラー** ] を選択して、ホーム コントローラー クラスを作成します (図 11 を参照)。 [作成]、[更新]、[**詳細シナリオ] の [アクション メソッドの追加]** というチェックボックスが表示されていることに注目してください。 **[追加**] ボタンをクリックする前に、このチェックボックスがオンになっていることを確認します。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image11.jpg)](iteration-1-create-the-application-cs/_static/image21.png)

**図11**: ホームコントローラの追加 ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image22.png))

ホーム コントローラーを作成すると、リスト 1 でクラスが取得されます。

**リスト 1 - コントローラ\ホームコントローラ.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample1.cs)]

## <a name="listing-the-contacts"></a>連絡先の一覧表示

連絡先データベーステーブルのレコードを表示するには、Index() アクションとインデックスビューを作成する必要があります。

ホームコントローラには、既に Index() アクションが含まれています。 このメソッドを変更して、リスト 2 のように見せる必要があります。

**リスト 2 - コントローラ\ホームコントローラ.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample2.cs)]

リスト 2 の Home コントローラー クラスには、エンティティ\_という名前のプライベート フィールドが含まれていることに注意してください。 エンティティ\_フィールドは、データ モデルのエンティティを表します。 エンティティ フィールド\_を使用して、データベースと通信します。

Index() メソッドは、連絡先データベース テーブルのすべての連絡先を表すビューを返します。 式\_エンティティ。連絡先のリストを汎用リストとして返します。

インデックス コントローラを作成したので、次にインデックス ビューを作成する必要があります。 Index ビューを作成する前に、メニュー オプションの **[ビルド]、[ ソリューションのビルド**] の順に選択してアプリケーションをコンパイルします。 [ビューの**追加]** ダイアログに表示されるモデル クラスのリストを表示するには、ビューを追加する前に、常にプロジェクトをコンパイルする必要があります。

Index() メソッドを右クリックし、メニュー オプションの**ビューの追加**を選択して、インデックス ビューを作成します (図 12 を参照)。 このメニュー オプションを選択すると、[**ビューの追加]** ダイアログが開きます (図 13 を参照)。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image12.jpg)](iteration-1-create-the-application-cs/_static/image23.png)

**図 12**: インデックス ビューの追加 ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image24.png))

[**ビューの追加]** ダイアログで、[厳密に**型指定されたビューを作成**する] チェック ボックスをオンにします。 データ クラスの表示を選択します。 これらのオプションを選択すると、連絡先レコードの一覧を表示するビューが生成されます。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image13.jpg)](iteration-1-create-the-application-cs/_static/image25.png)

**図 13**: [ビューの追加] ダイアログ ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image26.png)します)

**[追加**] ボタンをクリックすると、リスト 3 のインデックス ビューが生成されます。 ファイルの&lt;先頭に表示される&gt;%@ ページ % ディレクティブに注意してください。 インデックス&lt;ビューは、ビュー ページ IEnumerable&lt;連絡先マネージャー.モデル&gt;&gt;クラスから継承します。 つまり、ビューの Model クラスは、取引先担当者エンティティの一覧を表します。

Index ビューの本文には、Model クラスで表される各連絡先を反復処理する foreach ループが含まれています。 Contact クラスの各プロパティの値は、HTML テーブル内に表示されます。

**リスト 3 - ビュー\ホーム\インデックス.aspx (未変更)**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample3.aspx)]

インデックスビューに1つの変更を加える必要があります。 詳細ビューを作成していないため、[詳細] リンクを削除できます。 インデックス ビューから次のコードを検索して削除します。

{ id=項目。ID })&gt;

インデックス ビューを変更した後、連絡先マネージャー アプリケーションを実行できます。 メニュー オプションの [デバッグ]、[デバッグの開始] の順に選択するか、単に F5 キーを押します。 アプリケーションを初めて実行するときには、図 14 のダイアログが表示されます。 デバッグを**有効にするには、[Web.config ファイルを変更する**] オプションを選択し、[OK] ボタンをクリックします。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image14.jpg)](iteration-1-create-the-application-cs/_static/image27.png)

**図 14**: デバッグを有効にする ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image28.png))

インデックス ビューは、既定で返されます。 このビューには、Contacts データベース テーブルのすべてのデータが一覧表示されます (図 15 を参照)。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image15.jpg)](iteration-1-create-the-application-cs/_static/image29.png)

**図15**: インデックスビュー ([フルサイズ画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image30.png))

インデックス ビューには、ビューの下部に [新規作成] というラベルのリンクが含まれていることに注意してください。 次のセクションでは、新しい連絡先を作成する方法について説明します。

## <a name="creating-new-contacts"></a>新しい連絡先の作成

ユーザーが新しい連絡先を作成できるようにするには、ホームコントローラに2つのCreate()アクションを追加する必要があります。 新しい連絡先を作成するための HTML フォームを返す Create() アクションを 1 つ作成する必要があります。 新しい連絡先の実際のデータベース挿入を実行する 2 番目の Create() アクションを作成する必要があります。

ホームコントローラに追加する必要がある新しいCreate() メソッドは、リスト4に含まれています。

**リスト 4 - コントローラ\HomeController.cs (作成メソッドを使用)**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample4.cs)]

最初の Create() メソッドは HTTP GET を使用して呼び出すことができますが、2 番目の Create() メソッドは HTTP POST によってのみ呼び出すことができます。 つまり、2 番目の Create() メソッドは、HTML フォームをポストするときにのみ呼び出すことができます。 最初の Create() メソッドは、単に新しい連絡先を作成するための HTML フォームを含むビューを返します。 2 番目の Create() メソッドは、データベースに新しい連絡先を追加する、はるかに興味深いものです。

2 番目の Create() メソッドが変更され、Contact クラスのインスタンスを受け入れることに注意してください。 HTML フォームからポストされたフォーム値は、mvc フレームワークASP.NETによって自動的にこの Contact クラスにバインドされます。 HTML 作成フォームの各フォーム フィールドは、Contact パラメーターのプロパティに割り当てられます。

連絡先パラメーターが [バインド] 属性で装飾されていることに注意してください。 [Bind] 属性は、バインドから取引先担当者 Id プロパティを除外するために使用されます。 Id プロパティは Id プロパティを表すため、Id プロパティを設定する必要はありません。

Create() メソッドの本文では、新しい連絡先をデータベースに挿入するためにエンティティ フレームワークが使用されます。 新しい連絡先が既存の連絡先のセットに追加され、SaveChanges() メソッドが呼び出され、これらの変更が基になるデータベースにプッシュバックされます。

2 つの Create() メソッドのいずれかを右クリックし、メニューオプションの**ビューを追加**(図 16 を参照) を選択すると、新しい連絡先を作成するための HTML フォームを生成できます。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image16.jpg)](iteration-1-create-the-application-cs/_static/image31.png)

**図 16**: 作成ビューの追加 ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image32.png))

[**ビューの追加**] ダイアログで、ビュー コンテンツの**ContactManager.Models.Contact**クラスと **[作成**] オプションを選択します (図 17 を参照)。 **[追加**] ボタンをクリックすると、作成ビューが自動的に生成されます。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image17.jpg)](iteration-1-create-the-application-cs/_static/image33.png)

**図 17**: ページが爆発するのを見る ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image34.png)して )

作成ビューには、Contact クラスの各プロパティのフォーム フィールドが含まれます。 作成ビューのコードは、リスト 5 に含まれています。

**リスト 5 - ビュー\ホーム\作成.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample5.aspx)]

Create() メソッドを変更して Create ビューを追加した後、連絡先マネージャ アプリケーションを実行して新しい連絡先を作成できます。 [インデックス] ビューに表示される **[新規作成**] リンクをクリックして、[作成] ビューに移動します。 図 18 に表示されます。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image18.jpg)](iteration-1-create-the-application-cs/_static/image35.png)

**図18**: 作成ビュー ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image36.png))

## <a name="editing-contacts"></a>連絡先の編集

取引先担当者レコードを編集するための機能を追加することは、新しい取引先担当者レコードを作成するための機能を追加するのとよく似ています。 まず、2 つの新しい Edit メソッドをホーム コント ローラー クラスに追加する必要があります。 これらの新しい Edit() メソッドは、リスト 6 に含まれています。

**リスト 6 - コントローラ\HomeController.cs (編集メソッドを使用)**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample6.cs)]

最初の Edit() メソッドは、HTTP GET 操作によって呼び出されます。 Id パラメーターは、編集中の取引先担当者レコードの Id を表すこのメソッドに渡されます。 エンティティ フレームワークは、ID に一致する取引先担当者を取得するために使用されます。レコードを編集するための HTML フォームを含むビューが返されます。

2 番目の Edit() メソッドは、データベースに対して実際の更新を実行します。 このメソッドは、Contact クラスのインスタンスをパラメーターとして受け取ります。 ASP.NET MVC フレームワークは、フォーム フィールドを編集フォームからこのクラスに自動的にバインドします。 連絡先を編集するときに[Bind]属性を含まないことに注意してください(Id プロパティの値が必要です)。

エンティティ フレームワークは、変更された連絡先をデータベースに保存するために使用されます。 元の連絡先は、まずデータベースから取得する必要があります。 次に、エンティティ フレームワークの適用プロパティChanges() メソッドが呼び出され、連絡先への変更を記録します。 最後に、エンティティ フレームワークの SaveChanges() メソッドが呼び出され、基になるデータベースに対する変更を永続化します。

Edit() メソッドを右クリックし、メニュー オプションのビューを追加を選択すると、Edit フォームを含むビューを生成できます。 [ビューの追加] ダイアログで **、ContactManager.Models.Contact**クラスとビュー コンテンツの**編集**を選択します (図 19 参照)。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image19.jpg)](iteration-1-create-the-application-cs/_static/image37.png)

**図 19**: 編集ビューの追加 ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image38.png))

[追加] ボタンをクリックすると、新しい編集ビューが自動的に生成されます。 生成される HTML フォームには、Contact クラスの各プロパティに対応するフィールドが含まれています (リスト 7 を参照)。

**リスト 7 - ビュー\ホーム\編集.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>連絡先の削除

連絡先を削除する場合は、ホームコントローラークラスに2つのDelete()アクションを追加する必要があります。 最初の Delete() アクションは、削除確認フォームを表示します。 2 番目の Delete() アクションは、実際の削除を実行します。

> [!NOTE] 
> 
> 後で、イテレーション #7では、Ajax 削除の 1 ステップをサポートするように連絡先マネージャーを変更します。

2 つの新しい Delete() メソッドは、リスト 8 に含まれています。

**リスト 8 - コントローラ\ホームコントローラ.cs (メソッドの削除)**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample8.cs)]

最初の Delete() メソッドは、データベースから連絡先レコードを削除するための確認フォームを返します (図20 を参照)。 2 番目の Delete() メソッドは、データベースに対して実際の削除操作を実行します。 元の連絡先がデータベースから取得されると、データベースの削除を実行するために、エンティティ フレームワーク DeleteObject() メソッドと SaveChanges() メソッドが呼び出されます。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image20.jpg)](iteration-1-create-the-application-cs/_static/image39.png)

**図20**: 削除確認ビュー ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image40.png))

インデックス ビューを変更して、取引先担当者レコードを削除するためのリンクを含める必要があります (図 21 を参照)。 編集リンクを含む同じテーブルセルに次のコードを追加する必要があります。

アイテムを指定します。ID }) %&gt;

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image21.jpg)](iteration-1-create-the-application-cs/_static/image41.png)

**図21**: 編集リンクを含むインデックスビュー ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image42.png))

次に、削除確認ビューを作成する必要があります。 ホームコントローラークラスで Delete() メソッドを右クリックし、メニューオプションのビューを追加を選択します。 [ビューの追加] ダイアログが表示されます (図 22 を参照)。

リスト ビュー、作成ビュー、および編集ビューの場合とは異なり、[ビューの追加] ダイアログには、削除ビューを作成するオプションがありません。 代わりに、**連絡先マネージャー.Models.Contact**データ クラスと**空**のビュー コンテンツを選択します。 [空のビュー コンテンツ] オプションを選択すると、自分でビューを作成する必要があります。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image22.jpg)](iteration-1-create-the-application-cs/_static/image43.png)

**図22**: 削除確認ビューの追加 ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image44.png))

削除ビューの内容は、リスト 9 に含まれています。 このビューには、特定の連絡先を削除するかどうかを確認するフォームが含まれています (図 21 参照)。

**リスト 9 - ビュー\ホーム\削除.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>デフォルトコントローラの名前の変更

連絡先を操作するためのコントローラクラスの名前が HomeController クラスという名前になっているのは、気になるかもしれません。 コントローラは連絡先コントローラという名前であってはならないのですか?

この問題は簡単に修正できます。 まず、ホーム コントローラの名前をリファクタリングする必要があります。 Visual Studio コード エディタで HomeController クラスを開き、クラスの名前を右クリックし、メニュー オプション**の [リファクタリング、名前の変更]** を選択します。 このメニュー オプションを選択すると、[名前の変更] ダイアログボックスが開きます。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image23.jpg)](iteration-1-create-the-application-cs/_static/image45.png)

**図 23**: コントローラ名のリファクタリング ([フルサイズの画像を表示するには、ここをクリック](iteration-1-create-the-application-cs/_static/image46.png)します)

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image24.jpg)](iteration-1-create-the-application-cs/_static/image47.png)

**図 24**: [名前の変更] ダイアログを使用する ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image48.png)します )

コントローラー クラスの名前を変更すると、Visual Studio は Views フォルダー内のフォルダーの名前も更新します。 \ビュー\ホーム フォルダーの名前を \ビュー\連絡先フォルダーに変更します。

この変更を行うと、アプリケーションにはホーム コントローラーがなくなります。 アプリケーションを実行すると、図 25 のエラー ページが表示されます。

[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-1-create-the-application-cs/_static/image25.jpg)](iteration-1-create-the-application-cs/_static/image49.png)

**図 25**: デフォルトコントローラなし ([フルサイズの画像を表示する をクリック](iteration-1-create-the-application-cs/_static/image50.png))

ホーム コントローラの代わりに連絡先コントローラを使用するには、Global.asax ファイルの既定のルートを更新する必要があります。 Global.asax ファイルを開き、デフォルト ルートで使用される既定のコントローラを変更します (リスト 10 を参照)。

**リスト 10 - Global.asax.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample10.cs)]

これらの変更を行うと、連絡先マネージャーが正常に実行されます。 これで、既定のコント ローラーとして連絡先コント ローラー クラスを使用します。

## <a name="summary"></a>まとめ

この最初のイテレーションでは、できるだけ高速に基本的な Contact Manager アプリケーションを作成しました。 Visual Studio を利用して、コントローラーとビューの初期コードを自動的に生成しました。 また、Entity Framework を利用してデータベース モデル クラスを自動的に生成しました。

現在、連絡先マネージャアプリケーションを使用して、連絡先レコードの一覧表示、作成、編集、および削除を行うことができます。 つまり、データベース駆動型 Web アプリケーションで必要となる基本的なデータベース操作をすべて実行できます。

残念ながら、私たちのアプリケーションはいくつかの問題を抱えています。 まず、私はこれを認めるため、連絡先マネージャアプリケーションは、最も魅力的なアプリケーションではありません。 それはいくつかの設計作業を必要とします。 次のイテレーションでは、既定のビュー マスター ページとカスケード スタイル シートを変更して、アプリケーションの外観を改善する方法について説明します。

第二に、フォームの検証は実装していません。 たとえば、フォーム フィールドに値を入力せずに [連絡先の作成] フォームを送信できないようにする方法はありません。 また、無効な電話番号やメールアドレスを入力することもできます。 繰り返し#3でフォーム検証の問題に取り組み始めます。

最後に、最も重要なのは、Contact Manager アプリケーションの現在のイテレーションを簡単に変更または維持できないことです。 たとえば、データベース アクセス ロジックは、コントローラー アクションに直にベイク処理されます。 つまり、コントローラを変更せずにデータ アクセス コードを変更することはできません。 以降のイテレーションでは、Contact Manager の変更に対する耐性を高めるために実装できるソフトウェア設計パターンについて説明します。

> [!div class="step-by-step"]
> [次へ](iteration-2-make-the-application-look-nice-cs.md)
