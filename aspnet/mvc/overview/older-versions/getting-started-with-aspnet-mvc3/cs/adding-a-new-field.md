---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: ムービーモデルとテーブルに新しいフィールドを追加する (C#) |Microsoft Docs
author: Rick-Anderson
description: このチュートリアルでは、Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 40b02a2f608f07091ce6b5339688a1e6290e2e37
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434842"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table-c"></a>Movie モデルとテーブルに新しいフィールドを追加する (C#)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > このチュートリアルの更新バージョンは、ASP.NET MVC 5 と Visual Studio 2013 を使用する[こちらで](../../../getting-started/introduction/getting-started.md)入手できます。 より安全で、より簡単にフォローし、より多くの機能を紹介します。
> 
> 
> このチュートリアルでは、Microsoft Visual Studio の無料バージョンである Microsoft Visual Web Developer 2010 Express Service Pack 1 を使用した ASP.NET MVC Web アプリケーションの構築の基本について説明します。 開始する前に、以下に示す前提条件がインストールされていることを確認してください。 これらのすべてをインストールするには、[ [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)] リンクをクリックします。 または、次のリンクを使用して、前提条件を個別にインストールすることもできます。
> 
> - [Visual Studio Web Developer Express SP1 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 ツールの更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(ランタイム + ツールのサポート)
> 
> Visual Web Developer 2010 ではなく Visual Studio 2010 を使用している場合は、次のリンクをクリックして必要なコンポーネントをインストールします: [Visual studio 2010 の前提条件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> このトピックには、ソースC#コードが含まれる Visual Web Developer プロジェクトが用意されています。 [バージョンをC#ダウンロード](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)します。 Visual Basic を希望する場合は、このチュートリアルの[Visual Basic バージョン](../vb/intro-to-aspnet-mvc-3.md)に切り替えてください。

このセクションでは、モデルクラスにいくつかの変更を加え、モデルの変更に合わせてデータベーススキーマを更新する方法について説明します。

## <a name="adding-a-rating-property-to-the-movie-model"></a>ムービー モデルへの評価プロパティの追加

まず、既存の `Movie` クラスに新しい `Rating` プロパティを追加します。 *Movie.cs*ファイルを開き、次のように `Rating` プロパティを追加します。

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

完成した `Movie` クラスは次のコードのようになります。

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

[**デバッグ**&gt;**ビルドのムービー** ] メニューコマンドを使用して、アプリケーションを再コンパイルします。

`Model` クラスを更新したので、新しい `Rating` プロパティをサポートするために、 *\Views\Movies\Index.cshtml*および *\Views\Movies\Create.cshtml* view テンプレートも更新する必要があります。

*\Views\Movies\Index.cshtml*ファイルを開き、 **Price**列の直後に `<th>Rating</th>` 列見出しを追加します。 次に、テンプレートの末尾付近に `<td>` 列を追加して、`@item.Rating` 値を表示します。 更新されたインデックスの例を次に示し*ます。 cshtml* view テンプレートは次のようになります。

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

次に、 *\Views\Movies\Create.cshtml*ファイルを開き、フォームの末尾付近に次のマークアップを追加します。 新しいムービーを作成するときに評価を指定できるように、テキストボックスが表示されます。

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a>モデルとデータベーススキーマの違いの管理

これで、新しい `Rating` プロパティをサポートするようにアプリケーションコードが更新されました。

次に、アプリケーションを実行し、 */ムービー*の URL に移動します。 ただし、この操作を行うと、次のエラーが表示されます。

![](adding-a-new-field/_static/image1.png)

このエラーが表示されるのは、アプリケーションの更新された `Movie` モデルクラスが、既存のデータベースの `Movie` テーブルのスキーマとは異なるようになったためです。 (データベース テーブルに `Rating` 列はありません)。

既定では、このチュートリアルの前に示したように Entity Framework Code First を使用してデータベースを自動的に作成すると、データベースのスキーマが生成元のモデルクラスと同期しているかどうかを追跡できるように Code First、データベースにテーブルが追加されます。 同期されていない場合は、Entity Framework によってエラーがスローされます。 これにより、開発時に問題を簡単に追跡できるようになります。これは、実行時に (あいまいなエラーによって) 検出された場合にのみ発生します。 同期チェック機能により、エラーメッセージが表示されます。

このエラーを解決するには、次の2つの方法があります。

1. Entity Framework に、新しいモデル クラス スキーマに基づいてデータベースを自動的にドロップさせ、再作成させます。 この方法は、テストデータベースに対してアクティブな開発を行う場合に非常に便利です。これにより、モデルとデータベーススキーマを一緒に迅速に進化させることができます。 ただし、この欠点は、データベース内の既存のデータが失われているため、運用データベースでこのアプローチを使用したく*ない*ということです。
2. モデル クラスに一致するように、既存のデータベースのスキーマを明示的に変更します。 この手法の長所は、データが維持されることです。 この変更は手動で行うことも、データベース変更スクリプトを作成して行うこともできます。

このチュートリアルでは、最初の方法を使用します。モデルが変更されるたびに、データベースを自動的に再作成 Code First Entity Framework します。

## <a name="automatically-re-creating-the-database-on-model-changes"></a>モデルの変更時にデータベースを自動的に再作成する

アプリケーションのモデルを変更するたびに、Code First によってデータベースが自動的に削除され、再作成されるようにアプリケーションを更新してみましょう。

> [!NOTE] 
> 
> **警告**データベースを自動的に削除して再作成するには、この方法を有効にする必要があります。この方法では、開発またはテストデータベースを使用していて、実際のデータが含まれている実稼働データベースでは使用し*ません*。 実稼働サーバーで使用すると、データが失われる可能性があります。

**ソリューションエクスプローラー**で、[*モデル*] フォルダーを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。

![](adding-a-new-field/_static/image2.png)

クラスに "Moの初期化子" という名前を指定します。 次のコードを含むように `MovieInitializer` クラスを更新します。

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

`MovieInitializer` クラスは、モデルクラスが変更された場合に、モデルによって使用されるデータベースを削除し、自動的に再作成する必要があることを指定します。 コードには、作成 (または再作成) のたびにデータベースに自動的に追加される既定のデータを指定する `Seed` メソッドが含まれています。 これにより、モデルを変更するたびに手動でデータを入力することなく、いくつかのサンプルデータをデータベースに読み込むことができます。

`MovieInitializer` クラスの定義が完了したので、アプリケーションを実行するたびに、モデルクラスがデータベースのスキーマと異なるかどうかを確認します。 そのような場合は、初期化子を実行して、モデルに一致するデータベースを再作成してから、サンプルデータをデータベースに設定できます。

`MvcMovies` プロジェクトのルートにある*global.asax*ファイルを開きます。

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

*Global.asax*ファイルには、プロジェクトのアプリケーション全体を定義するクラスが含まれており、アプリケーションの最初の起動時に実行される `Application_Start` イベントハンドラーが含まれています。

ファイルの先頭に2つの using ステートメントを追加してみましょう。 最初のは Entity Framework 名前空間を参照し、2番目のは `MovieInitializer` クラスが存在する名前空間を参照します。

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

次に示すように、`Application_Start` メソッドを見つけて、メソッドの先頭に `Database.SetInitializer` の呼び出しを追加します。

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

追加した `Database.SetInitializer` ステートメントは、スキーマとデータベースが一致しない場合に、`MovieDBContext` インスタンスで使用されているデータベースを自動的に削除して再作成する必要があることを示しています。 また、先ほど見たように、`MovieInitializer` クラスに指定されているサンプルデータもデータベースに設定します。

*Global.asax*ファイルを閉じます。

アプリケーションを再実行し、 */ムービー*の URL に移動します。 アプリケーションが起動すると、モデル構造がデータベーススキーマと一致しなくなったことが検出されます。 新しいモデル構造と一致するようにデータベースが自動的に再作成され、データベースにサンプルムービーが挿入されます。

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

新しいムービーを追加するには、 **[新規作成]** リンクをクリックします。 評価を追加できることに注意してください。

[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)

**Create** をクリックしてください。 新しいムービー (評価を含む) がムービーの一覧に表示されるようになりました。

[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)

このセクションでは、モデルオブジェクトを変更し、データベースと変更の同期を維持する方法について説明しました。 また、新しく作成されたデータベースにサンプルデータを設定して、シナリオを試す方法についても学習しました。 次に、より高度な検証ロジックをモデルクラスに追加し、一部のビジネスルールを適用できるようにする方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](examining-the-edit-methods-and-edit-view.md)
> [次へ](adding-validation-to-the-model.md)
