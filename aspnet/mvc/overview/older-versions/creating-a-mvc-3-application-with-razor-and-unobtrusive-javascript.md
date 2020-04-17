---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: カミソリと控えめな JavaScript を使用した MVC 3 アプリケーションの作成 |マイクロソフトドキュメント
author: rick-anderson
description: ユーザー一覧のサンプル Web アプリケーションは、Razor ビュー エンジンを使用して、ASP.NET MVC 3 アプリケーションを作成する簡単な方法を示します。 サンプル アプリケーション s..
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542457"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>Razor と控えめな JavaScript で MVC 3 を作成する

[マイクロソフト](https://github.com/microsoft)

> ユーザー一覧のサンプル Web アプリケーションは、Razor ビュー エンジンを使用して、ASP.NET MVC 3 アプリケーションを作成する簡単な方法を示します。 サンプル アプリケーションは、新しい Razor ビュー エンジンを使用して、ASP.NET MVC バージョン 3 と Visual Studio 2010 を使用して、ユーザーの作成、表示、編集、削除などの機能を含む架空のユーザー一覧 Web サイトを作成する方法を示します。
> 
> このチュートリアルでは、MVC 3 アプリケーションのユーザー一覧のサンプルをビルドするために取られた手順ASP.NET説明します。 C# と VB ソース コードを含む Visual Studio プロジェクトは、このトピックに付属しています[。](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114) このチュートリアルについて質問がある場合は[、MVC フォーラム](https://forums.asp.net/1146.aspx)に投稿してください。

## <a name="overview"></a>概要

作成するアプリケーションは、シンプルなユーザーリスト Web サイトです。 ユーザーは、ユーザー情報の入力、表示、および更新を行うことができます。

![サンプル サイト](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

VB と C# の完成したプロジェクトは[、ここから](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)ダウンロードできます。

## <a name="creating-the-web-application"></a>Web アプリケーションの作成

チュートリアルを開始するには、Visual Studio 2010 を開き *、ASP.NET MVC 3 Web アプリケーション*テンプレートを使用して新しいプロジェクトを作成します。 アプリケーション&quot;に名前を付ける&quot;Mvc3Razor .

[![新しい MVC 3 プロジェクト](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

[**新しいASP.NET MVC 3 プロジェクト**] ダイアログで、[インターネット**アプリケーション**] を選択し、Razor ビュー エンジンを選択して **、[OK]** をクリックします。

![新しいASP.NET MVC 3 プロジェクト ダイアログ](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

このチュートリアルでは、ASP.NET メンバーシップ プロバイダーを使用しませんので、ログオンとメンバーシップに関連付けられているすべてのファイルを削除できます。 **ソリューション エクスプローラ**で、次のファイルとディレクトリを削除します。

- *コントローラ\アカウントコントローラ*
- *モデル\アカウントモデル*
- *ビュー\共有\\_LogOnPartial*
- *ビュー\アカウント*(およびこのディレクトリ内のすべてのファイル)

![ソルン・エクス](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<em> \_Layout.cshtml</em>ファイルを編集し、"ログイン無効`<div>`&quot;"`logindisplay`というメッセージ<em>&quot;</em>で指定された要素内のマークアップを置き換えます。 次の例は、新しいマークアップを示しています。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>モデルの追加

**ソリューション エクスプローラ**で *、Models*フォルダを右クリックし、[**追加**] を**ポイントします**。

![新しいユーザー Mdl クラス](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

クラスに `UserModel` という名前を付けます。 *ユーザーモデル*ファイルの内容を次のコードに置き換えます。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

クラス`UserModel`はユーザーを表します。 クラスの各メンバーには[、DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間の[Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性が付けられます。 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間の属性は、Web アプリケーションのクライアント側およびサーバー側の自動検証を提供します。

クラスを`HomeController`開き、ディレクティブ`using`を追加して、 クラスと`UserModel``Users`クラスにアクセスできるようにします。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

宣言の直後`HomeController`に、次のコメントとクラスへの参照を`Users`追加します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

この`Users`クラスは、このチュートリアルで使用する、簡略化されたメモリ内データ ストアです。 実際のアプリケーションでは、データベースを使用してユーザー情報を格納します。 ファイルの最初の数行`HomeController`を次の例に示します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

次の手順でスキャフォールディング ウィザードでユーザー モデルを使用できるように、アプリケーションをビルドします。

## <a name="creating-the-default-view"></a>既定のビューの作成

次の手順では、アクション メソッドとビューを追加して、ユーザーを表示します。

既存の*ビュー\ホーム\インデックス*ファイルを削除します。 ユーザーを表示する新しい*インデックス*ファイルを作成します。

クラス内`HomeController`で、メソッドの内容を次`Index`のコードに置き換えます。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

メソッド内を右クリック`Index`し、[ビューの**追加**] をクリックします。

![ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

[**厳密に型指定されたビューを作成する]** オプションを選択します。 **データ クラスの表示**] で **、[Mvc3Razor.モデル.ユーザーモデル**] を選択します。 (**データ クラスの表示**ボックスに**Mvc3Razor.Models.UserModel**が表示されない場合は、プロジェクトをビルドする必要があります。ビュー エンジンが**Razor**に設定されていることを確認します。 **[コンテンツの表示]** を **[リスト]** に設定し、[**追加**] をクリックします。

![インデックス ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

新しいビューは、`Index`ビューに渡されるユーザー データを自動的にスキャフォールディングします。 新しく生成された*ビュー\ホーム\インデックス*ファイルを確認します。 **[新規作成]、[****編集**]、[**詳細**]、[**削除]** の各リンクは機能しませんが、ページの残りの部分は機能します。 ページを実行します。 ユーザーの一覧が表示されます。

![インデックス ページ](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

*Index.cshtml*ファイルを開き、`ActionLink`**編集**、**詳細**、および**削除**のマークアップを次のコードに置き換えます。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

ユーザー名は、**編集**リンク、**詳細**リンク、および**削除**リンクで選択したレコードを検索する ID として使用されます。

## <a name="creating-the-details-view"></a>詳細ビューの作成

次の手順では、アクション`Details`メソッドを追加し、ユーザーの詳細を表示します。

![詳細](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

ホームコントローラに`Details`次のメソッドを追加します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

メソッド内を右クリック`Details`し、[ビューの<strong>追加</strong>] を選択します。 <strong>[データ クラスの表示</strong>] ボックスに<strong>Mvc3Razor.Models.UserModel</strong>が含まれていることを確認<em>します。</em> <strong>[コンテンツの表示]</strong>を<strong>[詳細]</strong>に設定し、[<strong>追加</strong>] をクリックします。

![詳細ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

アプリケーションを実行し、詳細リンクを選択します。 自動スキャフォールディングには、モデル内の各プロパティが表示されます。

![詳細](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>編集ビューの作成

ホームコントローラに`Edit`次のメソッドを追加します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

前の手順で表示を追加し、[コンテンツの**表示**] を **[編集]** に設定します。

![編集ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

アプリケーションを実行し、いずれかのユーザーの姓名を編集します。 クラスに適用されている`DataAnnotation`制約に違反した場合、フォームを送信すると、サーバー コードによって生成される検証エラーが表示されます。 `UserModel` たとえば、フォームを送信するときに、"A"&quot; &quot;という&quot;名&quot;を "A" に変更すると、次のエラーがフォームに表示されます。

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

このチュートリアルでは、ユーザー名を主キーとして扱います。 したがって、ユーザー名のプロパティを変更することはできません。 *Edit.cshtml*ファイルで、ステートメントの直後`Html.BeginForm`に、ユーザー名を隠しフィールドに設定します。 これにより、プロパティがモデルに渡されます。 次のコードは、ステートメントの配置を`Hidden`示しています。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

ユーザー名`TextBoxFor`の`ValidationMessageFor`マークアップと マークアップを呼`DisplayFor`び出しに置き換えます。 この`DisplayFor`メソッドは、プロパティを読み取り専用要素として表示します。 完全なマークアップの例を次に示します。 オリジナル`TextBoxFor`と呼`ValidationMessageFor`び出しは、Razorの開始コメントと終了コメント文字 (`@* *@`) でコメントアウトされます。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>クライアント側検証の有効化

ASP.NET MVC 3 でクライアント側の検証を有効にするには、2 つのフラグを設定し、3 つの JavaScript ファイルを含める必要があります。

アプリケーションの*Web.config*ファイルを開きます。 アプリケーション`that ClientValidationEnabled`設定`UnobtrusiveJavaScriptEnabled`で、true に設定されていることを確認します。 ルート*Web.config*ファイルの次のフラグメントは、正しい設定を示しています。

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

true`UnobtrusiveJavaScriptEnabled`に設定すると、控えめな Ajax と控えめなクライアント検証が有効になります。 控えめな検証を使用すると、検証規則は HTML5 属性に変換されます。 HTML5 属性名は、小文字、数字、およびダッシュのみで構成できます。

true`ClientValidationEnabled`に設定すると、クライアント側の検証が有効になります。 これらのキーをアプリケーション*の Web.config*ファイルに設定すると、アプリケーション全体でクライアント検証と控えめな JavaScript が有効になります。 また、次のコードを使用して、個々のビューまたはコントローラー メソッドでこれらの設定を有効または無効にすることもできます。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

レンダリングされたビューには、複数の JavaScript ファイルを含める必要があります。 すべてのビューに JavaScript を含める簡単な方法は、ビュー *\共有\\_Layout.cshtml*ファイルに追加することです。 `<head>` * \_Layout.cshtml*ファイルの要素を次のコードに置き換えます。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

最初の 2 つの jQuery スクリプトは、マイクロソフト Ajax コンテンツ配信ネットワーク (CDN) によってホストされます。 Microsoft Ajax CDN を利用することで、アプリケーションの初回のパフォーマンスを大幅に向上させることができます。

アプリケーションを実行し、編集リンクをクリックします。 ブラウザでページのソースを表示します。 ブラウザーのソースには、フォーム`data-val`の多くの属性が表示されます (データの検証用)。 クライアント検証と控えめな JavaScript が有効になっている場合、クライアント検証規則を持つ入力フィールドには、`data-val="true"`控えめなクライアント検証をトリガーする属性が含まれます。 たとえば、モデルの`City`フィールドは[、次](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)の例に示すように、必須属性で修飾されました。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

クライアント検証ルールごとに、 という形式`data-val-rulename="message"`の属性が追加されます。 前に`City`示したフィールドの例を使用して、必須のクライアント検証規則`data-val-required`によって属性が生成&quot;され、「市区町&quot;村フィールドが必要です」というメッセージが表示されます。 アプリケーションを実行し、いずれかのユーザーを編集し、フィールドを`City`クリアします。 フィールドからタブアウトすると、クライアント側の検証エラー メッセージが表示されます。

![必要な市区町村](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

同様に、クライアント検証規則の各パラメーターに対して、 という形式`data-val-rulename-paramname=paramvalue`の属性が追加されます。 たとえば、`FirstName`プロパティには[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性が付けられており、最小長は 3、最大長は 8 を指定します。 名前のデータ`length`検証規則には、パラメーター名`max`とパラメーター値 8 があります。 次に、いずれかのユーザーを編集するときにフィールドに`FirstName`対して生成される HTML を示します。

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

控えめなクライアント検証の詳細については、Brad Wilson のブログ[の mvc 3 ASP.NETの「控えめなクライアント検証](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)」を参照してください。

> [!NOTE]
> mvc 3 Beta ASP.NETでは、クライアント側の検証を開始するためにフォームを送信する必要がある場合があります。 これは最終リリースで変更される可能性があります。

## <a name="creating-the-create-view"></a>作成ビューの作成

次の手順では、`Create`アクション メソッドとビューを追加して、ユーザーが新しいユーザーを作成できるようにします。 ホームコントローラに`Create`次のメソッドを追加します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

前の手順で表示を追加しますが、[**コンテンツの表示] を** **[作成**] に設定します。

![CREATE VIEW](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

アプリケーションを実行し、[**作成**] リンクを選択して、新しいユーザーを追加します。 この`Create`メソッドは、クライアント側およびサーバー側の検証を自動的に利用します。 Ben X&quot;&quot;などの空白を含むユーザー名を入力してみてください。 ユーザー名フィールドをタブアウトすると、クライアント側の検証エラー (`White space is not allowed`) が表示されます。

## <a name="add-the-delete-method"></a>削除メソッドを追加する

チュートリアルを完了するには、ホーム コントローラー`Delete`に次のメソッドを追加します。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

前の`Delete`手順と同様にビューを追加し、[**コンテンツの表示]** を **[削除]** に設定します。

![ビューの削除](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

これで、検証を伴うシンプルで完全な機能ASP.NET MVC 3 アプリケーションが作成されました。
