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
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="e939d-104">Razor と控えめな JavaScript で MVC 3 を作成する</span><span class="sxs-lookup"><span data-stu-id="e939d-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="e939d-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e939d-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="e939d-106">ユーザー一覧のサンプル Web アプリケーションは、Razor ビュー エンジンを使用して、ASP.NET MVC 3 アプリケーションを作成する簡単な方法を示します。</span><span class="sxs-lookup"><span data-stu-id="e939d-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="e939d-107">サンプル アプリケーションは、新しい Razor ビュー エンジンを使用して、ASP.NET MVC バージョン 3 と Visual Studio 2010 を使用して、ユーザーの作成、表示、編集、削除などの機能を含む架空のユーザー一覧 Web サイトを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="e939d-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="e939d-108">このチュートリアルでは、MVC 3 アプリケーションのユーザー一覧のサンプルをビルドするために取られた手順ASP.NET説明します。</span><span class="sxs-lookup"><span data-stu-id="e939d-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="e939d-109">C# と VB ソース コードを含む Visual Studio プロジェクトは、このトピックに付属しています[。](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)</span><span class="sxs-lookup"><span data-stu-id="e939d-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="e939d-110">このチュートリアルについて質問がある場合は[、MVC フォーラム](https://forums.asp.net/1146.aspx)に投稿してください。</span><span class="sxs-lookup"><span data-stu-id="e939d-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="e939d-111">概要</span><span class="sxs-lookup"><span data-stu-id="e939d-111">Overview</span></span>

<span data-ttu-id="e939d-112">作成するアプリケーションは、シンプルなユーザーリスト Web サイトです。</span><span class="sxs-lookup"><span data-stu-id="e939d-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="e939d-113">ユーザーは、ユーザー情報の入力、表示、および更新を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e939d-113">Users can enter, view, and update user information.</span></span>

![サンプル サイト](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="e939d-115">VB と C# の完成したプロジェクトは[、ここから](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="e939d-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="e939d-116">Web アプリケーションの作成</span><span class="sxs-lookup"><span data-stu-id="e939d-116">Creating the Web Application</span></span>

<span data-ttu-id="e939d-117">チュートリアルを開始するには、Visual Studio 2010 を開き *、ASP.NET MVC 3 Web アプリケーション*テンプレートを使用して新しいプロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="e939d-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="e939d-118">アプリケーション&quot;に名前を付ける&quot;Mvc3Razor .</span><span class="sxs-lookup"><span data-stu-id="e939d-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="e939d-119">[![新しい MVC 3 プロジェクト](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="e939d-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="e939d-120">[**新しいASP.NET MVC 3 プロジェクト**] ダイアログで、[インターネット**アプリケーション**] を選択し、Razor ビュー エンジンを選択して **、[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e939d-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![新しいASP.NET MVC 3 プロジェクト ダイアログ](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="e939d-122">このチュートリアルでは、ASP.NET メンバーシップ プロバイダーを使用しませんので、ログオンとメンバーシップに関連付けられているすべてのファイルを削除できます。</span><span class="sxs-lookup"><span data-stu-id="e939d-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="e939d-123">**ソリューション エクスプローラ**で、次のファイルとディレクトリを削除します。</span><span class="sxs-lookup"><span data-stu-id="e939d-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="e939d-124">*コントローラ\アカウントコントローラ*</span><span class="sxs-lookup"><span data-stu-id="e939d-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="e939d-125">*モデル\アカウントモデル*</span><span class="sxs-lookup"><span data-stu-id="e939d-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="e939d-126">*ビュー\共有\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="e939d-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="e939d-127">*ビュー\アカウント*(およびこのディレクトリ内のすべてのファイル)</span><span class="sxs-lookup"><span data-stu-id="e939d-127">*Views\Account* (and all the files in this directory)</span></span>

![ソルン・エクス](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="e939d-129"><em> \_Layout.cshtml</em>ファイルを編集し、"ログイン無効`<div>`&quot;"`logindisplay`というメッセージ<em>&quot;</em>で指定された要素内のマークアップを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e939d-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="e939d-130">次の例は、新しいマークアップを示しています。</span><span class="sxs-lookup"><span data-stu-id="e939d-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="e939d-131">モデルの追加</span><span class="sxs-lookup"><span data-stu-id="e939d-131">Adding the Model</span></span>

<span data-ttu-id="e939d-132">**ソリューション エクスプローラ**で *、Models*フォルダを右クリックし、[**追加**] を**ポイントします**。</span><span class="sxs-lookup"><span data-stu-id="e939d-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![新しいユーザー Mdl クラス](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="e939d-134">クラスに `UserModel` という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="e939d-134">Name the class `UserModel`.</span></span> <span data-ttu-id="e939d-135">*ユーザーモデル*ファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e939d-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="e939d-136">クラス`UserModel`はユーザーを表します。</span><span class="sxs-lookup"><span data-stu-id="e939d-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="e939d-137">クラスの各メンバーには[、DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間の[Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性が付けられます。</span><span class="sxs-lookup"><span data-stu-id="e939d-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="e939d-138">[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間の属性は、Web アプリケーションのクライアント側およびサーバー側の自動検証を提供します。</span><span class="sxs-lookup"><span data-stu-id="e939d-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="e939d-139">クラスを`HomeController`開き、ディレクティブ`using`を追加して、 クラスと`UserModel``Users`クラスにアクセスできるようにします。</span><span class="sxs-lookup"><span data-stu-id="e939d-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="e939d-140">宣言の直後`HomeController`に、次のコメントとクラスへの参照を`Users`追加します。</span><span class="sxs-lookup"><span data-stu-id="e939d-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="e939d-141">この`Users`クラスは、このチュートリアルで使用する、簡略化されたメモリ内データ ストアです。</span><span class="sxs-lookup"><span data-stu-id="e939d-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="e939d-142">実際のアプリケーションでは、データベースを使用してユーザー情報を格納します。</span><span class="sxs-lookup"><span data-stu-id="e939d-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="e939d-143">ファイルの最初の数行`HomeController`を次の例に示します。</span><span class="sxs-lookup"><span data-stu-id="e939d-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="e939d-144">次の手順でスキャフォールディング ウィザードでユーザー モデルを使用できるように、アプリケーションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="e939d-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="e939d-145">既定のビューの作成</span><span class="sxs-lookup"><span data-stu-id="e939d-145">Creating the Default View</span></span>

<span data-ttu-id="e939d-146">次の手順では、アクション メソッドとビューを追加して、ユーザーを表示します。</span><span class="sxs-lookup"><span data-stu-id="e939d-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="e939d-147">既存の*ビュー\ホーム\インデックス*ファイルを削除します。</span><span class="sxs-lookup"><span data-stu-id="e939d-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="e939d-148">ユーザーを表示する新しい*インデックス*ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="e939d-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="e939d-149">クラス内`HomeController`で、メソッドの内容を次`Index`のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e939d-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="e939d-150">メソッド内を右クリック`Index`し、[ビューの**追加**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e939d-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="e939d-152">[**厳密に型指定されたビューを作成する]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="e939d-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="e939d-153">**データ クラスの表示**] で **、[Mvc3Razor.モデル.ユーザーモデル**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e939d-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="e939d-154">(**データ クラスの表示**ボックスに**Mvc3Razor.Models.UserModel**が表示されない場合は、プロジェクトをビルドする必要があります。ビュー エンジンが**Razor**に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e939d-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="e939d-155">**[コンテンツの表示]** を **[リスト]** に設定し、[**追加**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e939d-155">Set **View content** to **List** and then click **Add**.</span></span>

![インデックス ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="e939d-157">新しいビューは、`Index`ビューに渡されるユーザー データを自動的にスキャフォールディングします。</span><span class="sxs-lookup"><span data-stu-id="e939d-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="e939d-158">新しく生成された*ビュー\ホーム\インデックス*ファイルを確認します。</span><span class="sxs-lookup"><span data-stu-id="e939d-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="e939d-159">**[新規作成]、[\*\*\*\*編集**]、[**詳細**]、[**削除]** の各リンクは機能しませんが、ページの残りの部分は機能します。</span><span class="sxs-lookup"><span data-stu-id="e939d-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="e939d-160">ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="e939d-160">Run the page.</span></span> <span data-ttu-id="e939d-161">ユーザーの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e939d-161">You see a list of users.</span></span>

![インデックス ページ](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="e939d-163">*Index.cshtml*ファイルを開き、`ActionLink`**編集**、**詳細**、および**削除**のマークアップを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e939d-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="e939d-164">ユーザー名は、**編集**リンク、**詳細**リンク、および**削除**リンクで選択したレコードを検索する ID として使用されます。</span><span class="sxs-lookup"><span data-stu-id="e939d-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="e939d-165">詳細ビューの作成</span><span class="sxs-lookup"><span data-stu-id="e939d-165">Creating the Details View</span></span>

<span data-ttu-id="e939d-166">次の手順では、アクション`Details`メソッドを追加し、ユーザーの詳細を表示します。</span><span class="sxs-lookup"><span data-stu-id="e939d-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![詳細](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="e939d-168">ホームコントローラに`Details`次のメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="e939d-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="e939d-169">メソッド内を右クリック`Details`し、[ビューの<strong>追加</strong>] を選択します。</span><span class="sxs-lookup"><span data-stu-id="e939d-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="e939d-170"><strong>[データ クラスの表示</strong>] ボックスに<strong>Mvc3Razor.Models.UserModel</strong>が含まれていることを確認<em>します。</em></span><span class="sxs-lookup"><span data-stu-id="e939d-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="e939d-171"><strong>[コンテンツの表示]</strong>を<strong>[詳細]</strong>に設定し、[<strong>追加</strong>] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="e939d-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![詳細ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="e939d-173">アプリケーションを実行し、詳細リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="e939d-173">Run the application and select a details link.</span></span> <span data-ttu-id="e939d-174">自動スキャフォールディングには、モデル内の各プロパティが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e939d-174">The automatic scaffolding shows each property in the model.</span></span>

![詳細](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="e939d-176">編集ビューの作成</span><span class="sxs-lookup"><span data-stu-id="e939d-176">Creating the Edit View</span></span>

<span data-ttu-id="e939d-177">ホームコントローラに`Edit`次のメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="e939d-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="e939d-178">前の手順で表示を追加し、[コンテンツの**表示**] を **[編集]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="e939d-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![編集ビューの追加](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="e939d-180">アプリケーションを実行し、いずれかのユーザーの姓名を編集します。</span><span class="sxs-lookup"><span data-stu-id="e939d-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="e939d-181">クラスに適用されている`DataAnnotation`制約に違反した場合、フォームを送信すると、サーバー コードによって生成される検証エラーが表示されます。 `UserModel`</span><span class="sxs-lookup"><span data-stu-id="e939d-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="e939d-182">たとえば、フォームを送信するときに、"A"&quot; &quot;という&quot;名&quot;を "A" に変更すると、次のエラーがフォームに表示されます。</span><span class="sxs-lookup"><span data-stu-id="e939d-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="e939d-183">このチュートリアルでは、ユーザー名を主キーとして扱います。</span><span class="sxs-lookup"><span data-stu-id="e939d-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="e939d-184">したがって、ユーザー名のプロパティを変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="e939d-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="e939d-185">*Edit.cshtml*ファイルで、ステートメントの直後`Html.BeginForm`に、ユーザー名を隠しフィールドに設定します。</span><span class="sxs-lookup"><span data-stu-id="e939d-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="e939d-186">これにより、プロパティがモデルに渡されます。</span><span class="sxs-lookup"><span data-stu-id="e939d-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="e939d-187">次のコードは、ステートメントの配置を`Hidden`示しています。</span><span class="sxs-lookup"><span data-stu-id="e939d-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="e939d-188">ユーザー名`TextBoxFor`の`ValidationMessageFor`マークアップと マークアップを呼`DisplayFor`び出しに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e939d-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="e939d-189">この`DisplayFor`メソッドは、プロパティを読み取り専用要素として表示します。</span><span class="sxs-lookup"><span data-stu-id="e939d-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="e939d-190">完全なマークアップの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="e939d-190">The following example shows the completed markup.</span></span> <span data-ttu-id="e939d-191">オリジナル`TextBoxFor`と呼`ValidationMessageFor`び出しは、Razorの開始コメントと終了コメント文字 (`@* *@`) でコメントアウトされます。</span><span class="sxs-lookup"><span data-stu-id="e939d-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="e939d-192">クライアント側検証の有効化</span><span class="sxs-lookup"><span data-stu-id="e939d-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="e939d-193">ASP.NET MVC 3 でクライアント側の検証を有効にするには、2 つのフラグを設定し、3 つの JavaScript ファイルを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="e939d-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="e939d-194">アプリケーションの*Web.config*ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="e939d-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="e939d-195">アプリケーション`that ClientValidationEnabled`設定`UnobtrusiveJavaScriptEnabled`で、true に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e939d-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="e939d-196">ルート*Web.config*ファイルの次のフラグメントは、正しい設定を示しています。</span><span class="sxs-lookup"><span data-stu-id="e939d-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="e939d-197">true`UnobtrusiveJavaScriptEnabled`に設定すると、控えめな Ajax と控えめなクライアント検証が有効になります。</span><span class="sxs-lookup"><span data-stu-id="e939d-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="e939d-198">控えめな検証を使用すると、検証規則は HTML5 属性に変換されます。</span><span class="sxs-lookup"><span data-stu-id="e939d-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="e939d-199">HTML5 属性名は、小文字、数字、およびダッシュのみで構成できます。</span><span class="sxs-lookup"><span data-stu-id="e939d-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="e939d-200">true`ClientValidationEnabled`に設定すると、クライアント側の検証が有効になります。</span><span class="sxs-lookup"><span data-stu-id="e939d-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="e939d-201">これらのキーをアプリケーション*の Web.config*ファイルに設定すると、アプリケーション全体でクライアント検証と控えめな JavaScript が有効になります。</span><span class="sxs-lookup"><span data-stu-id="e939d-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="e939d-202">また、次のコードを使用して、個々のビューまたはコントローラー メソッドでこれらの設定を有効または無効にすることもできます。</span><span class="sxs-lookup"><span data-stu-id="e939d-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="e939d-203">レンダリングされたビューには、複数の JavaScript ファイルを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="e939d-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="e939d-204">すべてのビューに JavaScript を含める簡単な方法は、ビュー *\共有\\_Layout.cshtml*ファイルに追加することです。</span><span class="sxs-lookup"><span data-stu-id="e939d-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="e939d-205">`<head>` \* \_Layout.cshtml\*ファイルの要素を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e939d-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="e939d-206">最初の 2 つの jQuery スクリプトは、マイクロソフト Ajax コンテンツ配信ネットワーク (CDN) によってホストされます。</span><span class="sxs-lookup"><span data-stu-id="e939d-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="e939d-207">Microsoft Ajax CDN を利用することで、アプリケーションの初回のパフォーマンスを大幅に向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="e939d-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="e939d-208">アプリケーションを実行し、編集リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="e939d-208">Run the application and click an edit link.</span></span> <span data-ttu-id="e939d-209">ブラウザでページのソースを表示します。</span><span class="sxs-lookup"><span data-stu-id="e939d-209">View the page's source in the browser.</span></span> <span data-ttu-id="e939d-210">ブラウザーのソースには、フォーム`data-val`の多くの属性が表示されます (データの検証用)。</span><span class="sxs-lookup"><span data-stu-id="e939d-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="e939d-211">クライアント検証と控えめな JavaScript が有効になっている場合、クライアント検証規則を持つ入力フィールドには、`data-val="true"`控えめなクライアント検証をトリガーする属性が含まれます。</span><span class="sxs-lookup"><span data-stu-id="e939d-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="e939d-212">たとえば、モデルの`City`フィールドは[、次](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)の例に示すように、必須属性で修飾されました。</span><span class="sxs-lookup"><span data-stu-id="e939d-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="e939d-213">クライアント検証ルールごとに、 という形式`data-val-rulename="message"`の属性が追加されます。</span><span class="sxs-lookup"><span data-stu-id="e939d-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="e939d-214">前に`City`示したフィールドの例を使用して、必須のクライアント検証規則`data-val-required`によって属性が生成&quot;され、「市区町&quot;村フィールドが必要です」というメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e939d-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="e939d-215">アプリケーションを実行し、いずれかのユーザーを編集し、フィールドを`City`クリアします。</span><span class="sxs-lookup"><span data-stu-id="e939d-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="e939d-216">フィールドからタブアウトすると、クライアント側の検証エラー メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e939d-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![必要な市区町村](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="e939d-218">同様に、クライアント検証規則の各パラメーターに対して、 という形式`data-val-rulename-paramname=paramvalue`の属性が追加されます。</span><span class="sxs-lookup"><span data-stu-id="e939d-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="e939d-219">たとえば、`FirstName`プロパティには[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性が付けられており、最小長は 3、最大長は 8 を指定します。</span><span class="sxs-lookup"><span data-stu-id="e939d-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="e939d-220">名前のデータ`length`検証規則には、パラメーター名`max`とパラメーター値 8 があります。</span><span class="sxs-lookup"><span data-stu-id="e939d-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="e939d-221">次に、いずれかのユーザーを編集するときにフィールドに`FirstName`対して生成される HTML を示します。</span><span class="sxs-lookup"><span data-stu-id="e939d-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="e939d-222">控えめなクライアント検証の詳細については、Brad Wilson のブログ[の mvc 3 ASP.NETの「控えめなクライアント検証](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e939d-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="e939d-223">mvc 3 Beta ASP.NETでは、クライアント側の検証を開始するためにフォームを送信する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="e939d-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="e939d-224">これは最終リリースで変更される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e939d-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="e939d-225">作成ビューの作成</span><span class="sxs-lookup"><span data-stu-id="e939d-225">Creating the Create View</span></span>

<span data-ttu-id="e939d-226">次の手順では、`Create`アクション メソッドとビューを追加して、ユーザーが新しいユーザーを作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="e939d-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="e939d-227">ホームコントローラに`Create`次のメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="e939d-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="e939d-228">前の手順で表示を追加しますが、[**コンテンツの表示] を** **[作成**] に設定します。</span><span class="sxs-lookup"><span data-stu-id="e939d-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![CREATE VIEW](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="e939d-230">アプリケーションを実行し、[**作成**] リンクを選択して、新しいユーザーを追加します。</span><span class="sxs-lookup"><span data-stu-id="e939d-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="e939d-231">この`Create`メソッドは、クライアント側およびサーバー側の検証を自動的に利用します。</span><span class="sxs-lookup"><span data-stu-id="e939d-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="e939d-232">Ben X&quot;&quot;などの空白を含むユーザー名を入力してみてください。</span><span class="sxs-lookup"><span data-stu-id="e939d-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="e939d-233">ユーザー名フィールドをタブアウトすると、クライアント側の検証エラー (`White space is not allowed`) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e939d-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="e939d-234">削除メソッドを追加する</span><span class="sxs-lookup"><span data-stu-id="e939d-234">Add the Delete method</span></span>

<span data-ttu-id="e939d-235">チュートリアルを完了するには、ホーム コントローラー`Delete`に次のメソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="e939d-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="e939d-236">前の`Delete`手順と同様にビューを追加し、[**コンテンツの表示]** を **[削除]** に設定します。</span><span class="sxs-lookup"><span data-stu-id="e939d-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![ビューの削除](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="e939d-238">これで、検証を伴うシンプルで完全な機能ASP.NET MVC 3 アプリケーションが作成されました。</span><span class="sxs-lookup"><span data-stu-id="e939d-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
