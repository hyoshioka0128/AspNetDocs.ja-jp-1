---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: Entity Framework のモックを作成するときに単体テストの ASP.NET Web API 2 |Microsoft Docs
author: Rick-Anderson
description: このガイダンスとアプリケーションは、Entity Framework を使用する Web API 2 アプリケーションの単体テストを作成する方法を説明します。 変更する方法を示しますが、.
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65108170"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a><span data-ttu-id="76433-104">Entity Framework のモックを作成するときに単体テストの ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="76433-104">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="76433-105">によって[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="76433-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="76433-106">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="76433-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="76433-107">このガイダンスとアプリケーションは、Entity Framework を使用する Web API 2 アプリケーションの単体テストを作成する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="76433-107">This guidance and application demonstrate how to create unit tests for your Web API 2 application that uses the Entity Framework.</span></span> <span data-ttu-id="76433-108">テストは、コンテキスト オブジェクトを渡すことを有効にするスキャフォールディングされたコント ローラーを変更する方法と Entity Framework で動作するテスト オブジェクトを作成する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="76433-108">It shows how to modify the scaffolded controller to enable passing a context object for testing, and how to create test objects that work with Entity Framework.</span></span>
>
> <span data-ttu-id="76433-109">ASP.NET Web API を使用した単体テストの概要については、次を参照してください。 [ASP.NET Web API 2 で Unit Testing](unit-testing-with-aspnet-web-api.md)します。</span><span class="sxs-lookup"><span data-stu-id="76433-109">For an introduction to unit testing with ASP.NET Web API, see [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md).</span></span>
>
> <span data-ttu-id="76433-110">このチュートリアルでは、ASP.NET Web API の基本的な概念に慣れてを前提としています。</span><span class="sxs-lookup"><span data-stu-id="76433-110">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="76433-111">入門チュートリアルについては、次を参照してください。 [ASP.NET Web API 2 の概要](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)します。</span><span class="sxs-lookup"><span data-stu-id="76433-111">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="76433-112">このチュートリアルで使用されるソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="76433-112">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="76433-113">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="76433-113">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="76433-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="76433-114">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="76433-115">このトピックの内容</span><span class="sxs-lookup"><span data-stu-id="76433-115">In this topic</span></span>

<span data-ttu-id="76433-116">このトピックは、次のセクションで構成されています。</span><span class="sxs-lookup"><span data-stu-id="76433-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="76433-117">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="76433-117">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="76433-118">コードをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="76433-118">Download code</span></span>](#download)
- [<span data-ttu-id="76433-119">単体テスト プロジェクトでアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="76433-119">Create application with unit test project</span></span>](#appwithunittest)
- [<span data-ttu-id="76433-120">モデル クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="76433-120">Create the model class</span></span>](#modelclass)
- [<span data-ttu-id="76433-121">コント ローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="76433-121">Add the controller</span></span>](#controller)
- [<span data-ttu-id="76433-122">追加の依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="76433-122">Add dependency injection</span></span>](#dependency)
- [<span data-ttu-id="76433-123">テスト プロジェクトで NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="76433-123">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="76433-124">テストのコンテキストを作成します。</span><span class="sxs-lookup"><span data-stu-id="76433-124">Create test context</span></span>](#testcontext)
- [<span data-ttu-id="76433-125">テストを作成します。</span><span class="sxs-lookup"><span data-stu-id="76433-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="76433-126">テストを実行します。</span><span class="sxs-lookup"><span data-stu-id="76433-126">Run tests</span></span>](#runtests)

<span data-ttu-id="76433-127">」の手順を既に完了している場合[ASP.NET Web API 2 で Unit Testing](unit-testing-with-aspnet-web-api.md)、セクションに進んで[コント ローラーの追加](#controller)します。</span><span class="sxs-lookup"><span data-stu-id="76433-127">If you have already completed the steps in [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), you can skip to the section [Add the controller](#controller).</span></span>

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="76433-128">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="76433-128">Prerequisites</span></span>

<span data-ttu-id="76433-129">Visual Studio 2017 Community、Professional または Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="76433-129">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="76433-130">コードをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="76433-130">Download code</span></span>

<span data-ttu-id="76433-131">ダウンロード、[完成したプロジェクト](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)します。</span><span class="sxs-lookup"><span data-stu-id="76433-131">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="76433-132">ダウンロード可能なプロジェクトには、このトピックでは、単体テストのコードが含まれています、 [ASP.NET Web API 2 の単体テスト](unit-testing-with-aspnet-web-api.md)トピック。</span><span class="sxs-lookup"><span data-stu-id="76433-132">The downloadable project includes unit test code for this topic and for the [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="76433-133">単体テスト プロジェクトでアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="76433-133">Create application with unit test project</span></span>

<span data-ttu-id="76433-134">アプリケーションを作成するときに、単体テスト プロジェクトを作成するか、単体テスト プロジェクトを既存のアプリケーションに追加します。</span><span class="sxs-lookup"><span data-stu-id="76433-134">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="76433-135">このチュートリアルでは、アプリケーションを作成するときに単体テスト プロジェクトの作成を示します。</span><span class="sxs-lookup"><span data-stu-id="76433-135">This tutorial shows creating a unit test project when creating the application.</span></span>

<span data-ttu-id="76433-136">という名前の新しい ASP.NET Web アプリケーション作成**StoreApp**します。</span><span class="sxs-lookup"><span data-stu-id="76433-136">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

<span data-ttu-id="76433-137">新しい ASP.NET プロジェクト ウィンドウで選択、**空**テンプレート フォルダーを追加し、Web API の参照をコアしします。</span><span class="sxs-lookup"><span data-stu-id="76433-137">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="76433-138">選択、**単体テストを追加**オプション。</span><span class="sxs-lookup"><span data-stu-id="76433-138">Select the **Add unit tests** option.</span></span> <span data-ttu-id="76433-139">単体テスト プロジェクトが自動的に名前付き**StoreApp.Tests**します。</span><span class="sxs-lookup"><span data-stu-id="76433-139">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="76433-140">この名前を保持することができます。</span><span class="sxs-lookup"><span data-stu-id="76433-140">You can keep this name.</span></span>

![単体テスト プロジェクトを作成します。](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

<span data-ttu-id="76433-142">アプリケーションを作成すると、表示されます - 2 つのプロジェクトが含まれている**StoreApp**と**StoreApp.Tests**します。</span><span class="sxs-lookup"><span data-stu-id="76433-142">After creating the application, you will see it contains two projects - **StoreApp** and **StoreApp.Tests**.</span></span>

<a id="modelclass"></a>
## <a name="create-the-model-class"></a><span data-ttu-id="76433-143">モデル クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="76433-143">Create the model class</span></span>

<span data-ttu-id="76433-144">StoreApp プロジェクトで、追加のクラス ファイルを**モデル**という名前のフォルダー **Product.cs**します。</span><span class="sxs-lookup"><span data-stu-id="76433-144">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="76433-145">ファイルの内容を次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="76433-145">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

<span data-ttu-id="76433-146">ソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="76433-146">Build the solution.</span></span>

<a id="controller"></a>
## <a name="add-the-controller"></a><span data-ttu-id="76433-147">コント ローラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="76433-147">Add the controller</span></span>

<span data-ttu-id="76433-148">Controllers フォルダーを右クリックして**追加**と**スキャフォールディングされた新しい項目**します。</span><span class="sxs-lookup"><span data-stu-id="76433-148">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="76433-149">Entity Framework を使用して、アクションがある Web API 2 コント ローラーを選択します。</span><span class="sxs-lookup"><span data-stu-id="76433-149">Select Web API 2 Controller with actions, using Entity Framework.</span></span>

![新しいコント ローラーを追加します。](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

<span data-ttu-id="76433-151">次の値を設定します。</span><span class="sxs-lookup"><span data-stu-id="76433-151">Set the following values:</span></span>

- <span data-ttu-id="76433-152">コント ローラー名:**「Productcontroller」**</span><span class="sxs-lookup"><span data-stu-id="76433-152">Controller name: **ProductController**</span></span>
- <span data-ttu-id="76433-153">モデル クラス:**製品**</span><span class="sxs-lookup"><span data-stu-id="76433-153">Model class: **Product**</span></span>
- <span data-ttu-id="76433-154">データ コンテキスト クラス: [選択**新しいデータ コンテキスト**ボタンの下に表示される値を設定する]</span><span class="sxs-lookup"><span data-stu-id="76433-154">Data context class: [Select **New data context** button which fills in the values seen below]</span></span>

![コント ローラーを指定します。](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

<span data-ttu-id="76433-156">クリックして**追加**自動的に生成されたコードで、コント ローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="76433-156">Click **Add** to create the controller with automatically-generated code.</span></span> <span data-ttu-id="76433-157">コードには、作成、取得、更新、Product クラスのインスタンスを削除するためのメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="76433-157">The code includes methods for creating, retrieving, updating and deleting instances of the Product class.</span></span> <span data-ttu-id="76433-158">次のコードは、メソッドの製品を追加します。</span><span class="sxs-lookup"><span data-stu-id="76433-158">The following code shows the method for add a Product.</span></span> <span data-ttu-id="76433-159">メソッドがのインスタンスを返すことに注意してください。 **IHttpActionResult**します。</span><span class="sxs-lookup"><span data-stu-id="76433-159">Notice that the method returns an instance of **IHttpActionResult**.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

<span data-ttu-id="76433-160">IHttpActionResult は、Web API 2 では、新機能の 1 つと、単体テストの開発が簡単になります。</span><span class="sxs-lookup"><span data-stu-id="76433-160">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span>

<span data-ttu-id="76433-161">次のセクションでは、容易に生成されたコードをカスタマイズしますコント ローラーにテスト オブジェクトを渡します。</span><span class="sxs-lookup"><span data-stu-id="76433-161">In the next section, you will customize the generated code to facilitate passing test objects to the controller.</span></span>

<a id="dependency"></a>
## <a name="add-dependency-injection"></a><span data-ttu-id="76433-162">追加の依存関係の挿入</span><span class="sxs-lookup"><span data-stu-id="76433-162">Add dependency injection</span></span>

<span data-ttu-id="76433-163">現時点では、「productcontroller」クラスは、ハードコーディング StoreAppContext クラス インスタンスを使用します。</span><span class="sxs-lookup"><span data-stu-id="76433-163">Currently, the ProductController class is hard-coded to use an instance of the StoreAppContext class.</span></span> <span data-ttu-id="76433-164">依存関係の挿入をという名前のパターンを使用すると、アプリケーションを変更し、ハード コーディングされた依存関係を削除します。</span><span class="sxs-lookup"><span data-stu-id="76433-164">You will use a pattern called dependency injection to modify your application and remove that hard-coded dependency.</span></span> <span data-ttu-id="76433-165">縛りをなくすことによってテストするときにモック オブジェクトに渡すことができます。</span><span class="sxs-lookup"><span data-stu-id="76433-165">By breaking this dependency, you can pass in a mock object when testing.</span></span>

<span data-ttu-id="76433-166">右クリックし、**モデル**フォルダー、という名前の新しいインターフェイスを追加および**IStoreAppContext**します。</span><span class="sxs-lookup"><span data-stu-id="76433-166">Right-click the **Models** folder, and add a new interface named **IStoreAppContext**.</span></span>

<span data-ttu-id="76433-167">このコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="76433-167">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

<span data-ttu-id="76433-168">StoreAppContext.cs ファイルを開き、次の強調表示された変更を加えます。</span><span class="sxs-lookup"><span data-stu-id="76433-168">Open the StoreAppContext.cs file and make the following highlighted changes.</span></span> <span data-ttu-id="76433-169">注意する重要な変更点は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="76433-169">The important changes to note are:</span></span>

- <span data-ttu-id="76433-170">StoreAppContext クラス IStoreAppContext インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="76433-170">StoreAppContext class implements IStoreAppContext interface</span></span>
- <span data-ttu-id="76433-171">MarkAsModified メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="76433-171">MarkAsModified method is implemented</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

<span data-ttu-id="76433-172">ProductController.cs ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="76433-172">Open the ProductController.cs file.</span></span> <span data-ttu-id="76433-173">コードを強調表示されているように、既存のコードを変更します。</span><span class="sxs-lookup"><span data-stu-id="76433-173">Change the existing code to match the highlighted code.</span></span> <span data-ttu-id="76433-174">これらの変更は StoreAppContext で依存関係を中断し、別のオブジェクト コンテキスト クラスを渡すには、他のクラスを有効にします。</span><span class="sxs-lookup"><span data-stu-id="76433-174">These changes break the dependency on StoreAppContext and enable other classes to pass in a different object for the context class.</span></span> <span data-ttu-id="76433-175">この変更は、単体テスト中に、テスト コンテキストに渡すことを有効になります。</span><span class="sxs-lookup"><span data-stu-id="76433-175">This change will enable you to pass in a test context during unit tests.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

<span data-ttu-id="76433-176">これは、もう 1 つ変更が「productcontroller」で行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="76433-176">There is one more change you must make in ProductController.</span></span> <span data-ttu-id="76433-177">**PutProduct**メソッドは、置換するエンティティの状態を設定する行が MarkAsModified メソッドの呼び出しで変更します。</span><span class="sxs-lookup"><span data-stu-id="76433-177">In the **PutProduct** method, replace the line that sets the entity state to modified with a call to the MarkAsModified method.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

<span data-ttu-id="76433-178">ソリューションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="76433-178">Build the solution.</span></span>

<span data-ttu-id="76433-179">テスト プロジェクトを設定する準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="76433-179">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="76433-180">テスト プロジェクトで NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="76433-180">Install NuGet packages in test project</span></span>

<span data-ttu-id="76433-181">空のテンプレートを使用してアプリケーションを作成するときに単体テスト プロジェクト (StoreApp.Tests) にインストールされている NuGet パッケージは含まれません。</span><span class="sxs-lookup"><span data-stu-id="76433-181">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="76433-182">Web API テンプレートなどの他のテンプレートには、単体テスト プロジェクトで NuGet パッケージ一部にはが含まれます。</span><span class="sxs-lookup"><span data-stu-id="76433-182">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="76433-183">このチュートリアルでは、Entity Framework パッケージとテスト プロジェクトに Microsoft ASP.NET Web API 2 Core パッケージを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="76433-183">For this tutorial, you must include the Entity Framework package and the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="76433-184">StoreApp.Tests プロジェクトを右クリックして**NuGet パッケージの管理**します。</span><span class="sxs-lookup"><span data-stu-id="76433-184">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="76433-185">そのプロジェクトにパッケージを追加する StoreApp.Tests プロジェクトを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="76433-185">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![パッケージを管理します。](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

<span data-ttu-id="76433-187">オンラインのパッケージから検索して、EntityFramework パッケージ (バージョン 6.0 以降) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="76433-187">From the Online packages, find and install the EntityFramework package (version 6.0 or later).</span></span> <span data-ttu-id="76433-188">EntityFramework パッケージが既にインストールされていることが表示される場合は、StoreApp.Tests プロジェクトではなく StoreApp プロジェクトを選択した可能性があります。</span><span class="sxs-lookup"><span data-stu-id="76433-188">If it appears that the EntityFramework package is already installed, you may have selected the StoreApp project instead of the StoreApp.Tests project.</span></span>

![Entity Framework を追加します。](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

<span data-ttu-id="76433-190">検索して、Microsoft ASP.NET Web API 2 コア パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="76433-190">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![web api のコア パッケージをインストールします。](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

<span data-ttu-id="76433-192">NuGet パッケージの管理ウィンドウを閉じます。</span><span class="sxs-lookup"><span data-stu-id="76433-192">Close the Manage NuGet Packages window.</span></span>

<a id="testcontext"></a>
## <a name="create-test-context"></a><span data-ttu-id="76433-193">テストのコンテキストを作成します。</span><span class="sxs-lookup"><span data-stu-id="76433-193">Create test context</span></span>

<span data-ttu-id="76433-194">という名前のクラスを追加**TestDbSet**テスト プロジェクトにします。</span><span class="sxs-lookup"><span data-stu-id="76433-194">Add a class named **TestDbSet** to the test project.</span></span> <span data-ttu-id="76433-195">このクラスは、テスト データ セットの基本クラスとして機能します。</span><span class="sxs-lookup"><span data-stu-id="76433-195">This class serves as the base class for your test data set.</span></span> <span data-ttu-id="76433-196">このコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="76433-196">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

<span data-ttu-id="76433-197">という名前のクラスを追加**TestProductDbSet**を次のコードを含むテスト プロジェクトにします。</span><span class="sxs-lookup"><span data-stu-id="76433-197">Add a class named **TestProductDbSet** to the test project which contains the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

<span data-ttu-id="76433-198">という名前のクラスを追加**TestStoreAppContext**既存のコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="76433-198">Add a class named **TestStoreAppContext** and replace the existing code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="76433-199">テストの作成</span><span class="sxs-lookup"><span data-stu-id="76433-199">Create tests</span></span>

<span data-ttu-id="76433-200">既定では、テスト プロジェクトにという名前の空のテスト ファイルが含まれます。 **UnitTest1.cs**します。</span><span class="sxs-lookup"><span data-stu-id="76433-200">By default, your test project includes an empty test file named **UnitTest1.cs**.</span></span> <span data-ttu-id="76433-201">このファイルは、テスト メソッドの作成に使用する属性を示します。</span><span class="sxs-lookup"><span data-stu-id="76433-201">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="76433-202">このチュートリアルでは、新しいテスト クラスを追加するために、このファイルを削除することができます。</span><span class="sxs-lookup"><span data-stu-id="76433-202">For this tutorial, you can delete this file because you will add a new test class.</span></span>

<span data-ttu-id="76433-203">という名前のクラスを追加**TestProductController**テスト プロジェクトにします。</span><span class="sxs-lookup"><span data-stu-id="76433-203">Add a class named **TestProductController** to the test project.</span></span> <span data-ttu-id="76433-204">このコードを次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="76433-204">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="76433-205">テストの実行</span><span class="sxs-lookup"><span data-stu-id="76433-205">Run tests</span></span>

<span data-ttu-id="76433-206">テストを実行する準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="76433-206">You are now ready to run the tests.</span></span> <span data-ttu-id="76433-207">マークされているメソッドはすべて、 **TestMethod**属性がテストされます。</span><span class="sxs-lookup"><span data-stu-id="76433-207">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="76433-208">**テスト**メニュー項目、テストを実行します。</span><span class="sxs-lookup"><span data-stu-id="76433-208">From the **Test** menu item, run the tests.</span></span>

![テストの実行](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

<span data-ttu-id="76433-210">開く、**テスト エクスプ ローラー**ウィンドウで、テストの結果を注意してください。</span><span class="sxs-lookup"><span data-stu-id="76433-210">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![テスト結果](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
