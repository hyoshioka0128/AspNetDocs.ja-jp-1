---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
title: データ注釈検証コントロールを使用した検証 (C#) |マイクロソフトドキュメント
author: rick-anderson
description: データ注釈モデル バインダーを利用して、ASP.NET MVC アプリケーション内で検証を実行します。 さまざまな種類の検証コントロールの使用方法を説明します。
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 7ca8013e-9dfc-4e33-8336-cdccfd5f9414
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
msc.type: authoredcontent
ms.openlocfilehash: 28ea52b9b412431d59d7afdd1c7cce93a50a7e2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542678"
---
# <a name="validation-with-the-data-annotation-validators-c"></a><span data-ttu-id="039d0-104">データ検証注釈コントロールの検証 (C#)</span><span class="sxs-lookup"><span data-stu-id="039d0-104">Validation with the Data Annotation Validators (C#)</span></span>

<span data-ttu-id="039d0-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="039d0-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="039d0-106">データ注釈モデル バインダーを利用して、ASP.NET MVC アプリケーション内で検証を実行します。</span><span class="sxs-lookup"><span data-stu-id="039d0-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="039d0-107">さまざまな種類の検証コントロール属性を使用し、Microsoft エンティティ フレームワークで使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="039d0-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>

<span data-ttu-id="039d0-108">このチュートリアルでは、データ注釈検証を使用して、ASP.NET MVC アプリケーションで検証を実行する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="039d0-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="039d0-109">データ注釈検証コントロールを使用する利点は、クラス プロパティに 1 つ以上の属性 (Required 属性や StringLength 属性など) を追加するだけで、検証を実行できる点です。</span><span class="sxs-lookup"><span data-stu-id="039d0-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="039d0-110">データ注釈検証コントロールを使用する前に、データ注釈モデル バインダーをダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="039d0-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="039d0-111">[CodePlex](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)Web サイトからデータ注釈モデル バインダーのサンプルをダウンロードするには、 ここをクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="039d0-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>

<span data-ttu-id="039d0-112">データ注釈モデル バインダーは Microsoft ASP.NET MVC フレームワークの公式部分ではないことを理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="039d0-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="039d0-113">データ注釈モデル バインダーは Microsoft ASP.NET MVC チームによって作成されましたが、Microsoft では、このチュートリアルで説明し、使用するデータ注釈モデル バインダーの公式製品サポートを提供していません。</span><span class="sxs-lookup"><span data-stu-id="039d0-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>

## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="039d0-114">データ注釈モデル バインダーの使用</span><span class="sxs-lookup"><span data-stu-id="039d0-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="039d0-115">ASP.NET MVC アプリケーションでデータ注釈モデル バインダーを使用するには、まず、Microsoft.Web.Mvc.DataAnnotations.dll アセンブリと System.ComponentModel.DataAnnotations.dll アセンブリへの参照を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="039d0-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="039d0-116">メニュー オプションの **[プロジェクト]、[参照の追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="039d0-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="039d0-117">次に、[**参照**] タブをクリックし、データ注釈モデル バインダーのサンプルをダウンロード (および解凍) した場所を参照します (**図 1**を参照)。</span><span class="sxs-lookup"><span data-stu-id="039d0-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image2.png)](validation-with-the-data-annotation-validators-cs/_static/image1.png)

<span data-ttu-id="039d0-118">**図 1**: データ注釈モデル バインダーへの参照の追加 ([フルサイズの画像を表示する をクリック](validation-with-the-data-annotation-validators-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="039d0-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-cs/_static/image3.png))</span></span>

<span data-ttu-id="039d0-119">アセンブリとシステム.コンポーネントモデル.データアノテーション.dll アセンブリの両方を選択し **、[OK]** ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="039d0-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>

<span data-ttu-id="039d0-120">データ注釈モデル バインダーでは、.NET Framework サービス パック 1 に含まれる System.ComponentModel.DataAnnotations.dll アセンブリを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="039d0-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="039d0-121">データ注釈モデル バインダーサンプルに含まれるバージョンの System.ComponentModel.DataAnnotations.dll アセンブリを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="039d0-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>

<span data-ttu-id="039d0-122">最後に、データ注釈モデル バインダーを Global.asax ファイルに登録する必要があります。</span><span class="sxs-lookup"><span data-stu-id="039d0-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="039d0-123">アプリケーション Start() イベント\_ハンドラに次のコード行を追加して、\_アプリケーション Start() メソッドを次のようにします。</span><span class="sxs-lookup"><span data-stu-id="039d0-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample1.cs)]

<span data-ttu-id="039d0-124">このコード行は、mvc アプリケーション全体の既定のモデル バインダーとして ataAnnotationsModelBinder ASP.NET登録します。</span><span class="sxs-lookup"><span data-stu-id="039d0-124">This line of code registers the ataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="039d0-125">データ注釈検証コントロール属性の使用</span><span class="sxs-lookup"><span data-stu-id="039d0-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="039d0-126">データ注釈モデル バインダーを使用する場合は、検証を実行するためにバリデータ属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="039d0-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="039d0-127">名前空間には、次の検証属性が含まれています。</span><span class="sxs-lookup"><span data-stu-id="039d0-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="039d0-128">Range – プロパティの値が指定した範囲の値の間に収まっているかどうかを検証できます。</span><span class="sxs-lookup"><span data-stu-id="039d0-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="039d0-129">正規表現 – プロパティの値が指定した正規表現パターンと一致するかどうかを検証できます。</span><span class="sxs-lookup"><span data-stu-id="039d0-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="039d0-130">[必須] – 必要に応じてプロパティをマークできます。</span><span class="sxs-lookup"><span data-stu-id="039d0-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="039d0-131">StringLength – 文字列プロパティの最大長を指定できます。</span><span class="sxs-lookup"><span data-stu-id="039d0-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="039d0-132">検証 – すべての検証コントロール属性の基本クラス。</span><span class="sxs-lookup"><span data-stu-id="039d0-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="039d0-133">標準の検証コントロールのいずれでも検証のニーズが満たされない場合は、基本検証属性から新しい検証属性を継承してカスタム検証属性を作成するオプションが常にあります。</span><span class="sxs-lookup"><span data-stu-id="039d0-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>

<span data-ttu-id="039d0-134">**リスト 1**の Product クラスは、これらのバリデータ属性の使用方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="039d0-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="039d0-135">[名前]、[説明]、および [単価] プロパティは必須としてマークされます。</span><span class="sxs-lookup"><span data-stu-id="039d0-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="039d0-136">Name プロパティには、10 文字未満の文字列長を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="039d0-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="039d0-137">最後に、UnitPrice プロパティは、通貨金額を表す正規表現パターンと一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="039d0-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample2.cs)]

<span data-ttu-id="039d0-138">**リスト 1**: モデル\製品.cs</span><span class="sxs-lookup"><span data-stu-id="039d0-138">**Listing 1**: Models\Product.cs</span></span>

<span data-ttu-id="039d0-139">Product クラスは、1 つの追加属性を使用する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="039d0-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="039d0-140">DisplayName 属性を使用すると、プロパティがエラー メッセージに表示されるときに、プロパティの名前を変更できます。</span><span class="sxs-lookup"><span data-stu-id="039d0-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="039d0-141">"単価フィールドが必要です" というエラー メッセージを表示する代わりに、エラー メッセージ "価格フィールドが必要です" を表示できます。</span><span class="sxs-lookup"><span data-stu-id="039d0-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="039d0-142">検証コントロールによって表示されるエラー メッセージを完全にカスタマイズする場合は、次のように、検証コントロールの ErrorMessage プロパティにカスタム エラー メッセージを割り当てることができます。`<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="039d0-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>

<span data-ttu-id="039d0-143">リスト 1 の Product クラスは **、リスト** **2**の Create() コントローラ アクションで使用できます。</span><span class="sxs-lookup"><span data-stu-id="039d0-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="039d0-144">このコントローラアクションは、モデルの状態にエラーが含まれる場合に[作成]ビューを再表示します。</span><span class="sxs-lookup"><span data-stu-id="039d0-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample3.cs)]

<span data-ttu-id="039d0-145">**リスト 2**: コントローラー\製品コントローラー.vb</span><span class="sxs-lookup"><span data-stu-id="039d0-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="039d0-146">最後に、**リスト 3**でビューを作成するには、Create() アクションを右クリックし、メニューオプションの **[ビューの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="039d0-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="039d0-147">Product クラスをモデル クラスとして使用して、厳密に型指定されたビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="039d0-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="039d0-148">[ビュー コンテンツ] ドロップダウン リストから [**作成**] を選択します (**図 2**を参照)。</span><span class="sxs-lookup"><span data-stu-id="039d0-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image5.png)](validation-with-the-data-annotation-validators-cs/_static/image4.png)

<span data-ttu-id="039d0-149">**図2**: 作成ビューの追加</span><span class="sxs-lookup"><span data-stu-id="039d0-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-cs/samples/sample4.aspx)]

<span data-ttu-id="039d0-150">**リスト 3**: ビュー\製品\作成.aspx</span><span class="sxs-lookup"><span data-stu-id="039d0-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="039d0-151">[**ビューの追加**] メニュー オプションで生成された [作成] フォームから [ID] フィールドを削除します。</span><span class="sxs-lookup"><span data-stu-id="039d0-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="039d0-152">Id フィールドは ID 列に対応するため、ユーザーがこのフィールドに値を入力できないようにします。</span><span class="sxs-lookup"><span data-stu-id="039d0-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>

<span data-ttu-id="039d0-153">製品を作成するフォームを送信し、必須フィールドの値を入力しない場合は、**図 3**の検証エラー メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="039d0-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image7.png)](validation-with-the-data-annotation-validators-cs/_static/image6.png)

<span data-ttu-id="039d0-154">**図 3**: 必須フィールドが見つからない</span><span class="sxs-lookup"><span data-stu-id="039d0-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="039d0-155">無効な通貨金額を入力すると、**図 4**のエラー メッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="039d0-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image9.png)](validation-with-the-data-annotation-validators-cs/_static/image8.png)

<span data-ttu-id="039d0-156">**図4**: 無効な通貨金額</span><span class="sxs-lookup"><span data-stu-id="039d0-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="039d0-157">エンティティ フレームワークでのデータ注釈検証コントロールの使用</span><span class="sxs-lookup"><span data-stu-id="039d0-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="039d0-158">Microsoft Entity Framework を使用してデータ モデル クラスを生成する場合は、検証コントロール属性をクラスに直接適用することはできません。</span><span class="sxs-lookup"><span data-stu-id="039d0-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="039d0-159">Entity Framework デザイナーはモデル クラスを生成するため、モデル クラスに加えた変更は、次にデザイナーで変更を加えた時点で上書きされます。</span><span class="sxs-lookup"><span data-stu-id="039d0-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="039d0-160">Entity Framework によって生成されたクラスで検証コントロールを使用する場合は、メタ データ クラスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="039d0-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="039d0-161">検証コントロールを実際のクラスに適用する代わりに、メタ データ クラスに検証コントロールを適用します。</span><span class="sxs-lookup"><span data-stu-id="039d0-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="039d0-162">たとえば、Entity Framework を使用して Movie クラスを作成したとします (**図 5**を参照)。</span><span class="sxs-lookup"><span data-stu-id="039d0-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="039d0-163">さらに、ムービータイトルとディレクターのプロパティを必要なプロパティにしたいと考えてください。</span><span class="sxs-lookup"><span data-stu-id="039d0-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="039d0-164">この場合は、**リスト 4**で部分クラスとメタ データ クラスを作成できます。</span><span class="sxs-lookup"><span data-stu-id="039d0-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image11.png)](validation-with-the-data-annotation-validators-cs/_static/image10.png)

<span data-ttu-id="039d0-165">**図 5**: エンティティ フレームワークによって生成されたムービー クラス</span><span class="sxs-lookup"><span data-stu-id="039d0-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample5.cs)]

<span data-ttu-id="039d0-166">**リスト4**: モデル\Movie.cs</span><span class="sxs-lookup"><span data-stu-id="039d0-166">**Listing 4**: Models\Movie.cs</span></span>

<span data-ttu-id="039d0-167">**リスト 4**のファイルには、ムービーとムービーメタデータという名前の 2 つのクラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="039d0-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="039d0-168">Movie クラスは部分クラスです。</span><span class="sxs-lookup"><span data-stu-id="039d0-168">The Movie class is a partial class.</span></span> <span data-ttu-id="039d0-169">これは、DataModel.Designer.vb ファイルに含まれるエンティティ フレームワークによって生成された部分クラスに対応します。</span><span class="sxs-lookup"><span data-stu-id="039d0-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="039d0-170">現在、.NET フレームワークは部分的なプロパティをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="039d0-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="039d0-171">したがって、**リスト 4**で定義されているムービー クラスのプロパティにバリデータ属性を適用することによって、DataModel.Designer.vb ファイルで定義されているムービー クラスのプロパティに検証コントロール属性を適用する方法はありません。</span><span class="sxs-lookup"><span data-stu-id="039d0-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="039d0-172">ムービー部分クラスは、MovieMetaData クラスを指すメタデータ型属性で修飾されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="039d0-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="039d0-173">クラスには、ムービー クラスのプロパティのプロキシ プロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="039d0-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="039d0-174">検証コントロール属性は、MovieMetaData クラスのプロパティに適用されます。</span><span class="sxs-lookup"><span data-stu-id="039d0-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="039d0-175">タイトル、ディレクター、および日付リリースのプロパティはすべて必須プロパティとしてマークされます。</span><span class="sxs-lookup"><span data-stu-id="039d0-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="039d0-176">Director プロパティには、5 文字未満の文字列を割り当てる必要があります。</span><span class="sxs-lookup"><span data-stu-id="039d0-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="039d0-177">最後に、"日付解放日フィールドが必要です" などのエラー メッセージを表示するには、"DateReleased/日付のリリース" プロパティに "DisplayName/ 表示名" 属性が適用されます。</span><span class="sxs-lookup"><span data-stu-id="039d0-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="039d0-178">エラーの代わりに"日付がリリースされました" フィールドが必要です。</span><span class="sxs-lookup"><span data-stu-id="039d0-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="039d0-179">MovieMetaData クラスのプロキシ プロパティは、ムービー クラスの対応するプロパティと同じ型を表す必要はありません。</span><span class="sxs-lookup"><span data-stu-id="039d0-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="039d0-180">たとえば、Director プロパティは、Movie クラスの文字列プロパティと MovieMetaData クラスのオブジェクト プロパティです。</span><span class="sxs-lookup"><span data-stu-id="039d0-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>

<span data-ttu-id="039d0-181">**図 6**のページは、ムービーのプロパティに無効な値を入力したときに返されるエラー メッセージを示しています。</span><span class="sxs-lookup"><span data-stu-id="039d0-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image13.png)](validation-with-the-data-annotation-validators-cs/_static/image12.png)

<span data-ttu-id="039d0-182">**図 6**: エンティティ フレームワークで検証コントロールを使用する ([フルサイズの画像を表示する をクリック](validation-with-the-data-annotation-validators-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="039d0-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-cs/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="039d0-183">まとめ</span><span class="sxs-lookup"><span data-stu-id="039d0-183">Summary</span></span>

<span data-ttu-id="039d0-184">このチュートリアルでは、データ注釈モデル バインダーを利用して、ASP.NET MVC アプリケーション内で検証を実行する方法を学習しました。</span><span class="sxs-lookup"><span data-stu-id="039d0-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="039d0-185">次の手順では、Required 属性や StringLength 属性など、さまざまな種類のバリデータ属性の使用方法について説明しました。</span><span class="sxs-lookup"><span data-stu-id="039d0-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="039d0-186">また、Microsoft エンティティ フレームワークを使用する際にこれらの属性を使用する方法についても説明しました。</span><span class="sxs-lookup"><span data-stu-id="039d0-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="039d0-187">[前へ](validating-with-a-service-layer-cs.md)
> [次へ](creating-model-classes-with-the-entity-framework-vb.md)</span><span class="sxs-lookup"><span data-stu-id="039d0-187">[Previous](validating-with-a-service-layer-cs.md)
[Next](creating-model-classes-with-the-entity-framework-vb.md)</span></span>
