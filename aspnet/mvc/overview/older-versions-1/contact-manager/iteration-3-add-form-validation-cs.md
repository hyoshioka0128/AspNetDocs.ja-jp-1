---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: 'イテレーション #3 – フォームの検証を追加する (C#) |マイクロソフトドキュメント'
author: rick-anderson
description: 3 回目のイテレーションでは、基本的なフォーム検証を追加します。 必須のフォームフィールドに入力せずにフォームを送信できないようにします。 また、emai..
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: c8442574d4901045f044f53ea12cd8330e8eaaa3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542379"
---
# <a name="iteration-3--add-form-validation-c"></a><span data-ttu-id="480f0-105">繰り返し #3 – フォーム検証を追加する (C#)</span><span class="sxs-lookup"><span data-stu-id="480f0-105">Iteration #3 – Add form validation (C#)</span></span>

<span data-ttu-id="480f0-106">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="480f0-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="480f0-107">コードをダウンロード</span><span class="sxs-lookup"><span data-stu-id="480f0-107">Download Code</span></span>](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> <span data-ttu-id="480f0-108">3 回目のイテレーションでは、基本的なフォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="480f0-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="480f0-109">必須のフォームフィールドに入力せずにフォームを送信できないようにします。</span><span class="sxs-lookup"><span data-stu-id="480f0-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="480f0-110">また、メールアドレスと電話番号も検証します。</span><span class="sxs-lookup"><span data-stu-id="480f0-110">We also validate email addresses and phone numbers.</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="480f0-111">MVC アプリケーション (C#) ASP.NET連絡先管理の構築</span><span class="sxs-lookup"><span data-stu-id="480f0-111">Building a Contact Management ASP.NET MVC Application (C#)</span></span>

<span data-ttu-id="480f0-112">この一連のチュートリアルでは、最初から最後まで連絡先管理アプリケーション全体を構築します。</span><span class="sxs-lookup"><span data-stu-id="480f0-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="480f0-113">連絡先マネージャー アプリケーションでは、連絡先の情報 (名前、電話番号、電子メール アドレス) を保存できます。</span><span class="sxs-lookup"><span data-stu-id="480f0-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="480f0-114">複数のイテレーションでアプリケーションをビルドします。</span><span class="sxs-lookup"><span data-stu-id="480f0-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="480f0-115">各反復処理で、アプリケーションを徐々に改善します。</span><span class="sxs-lookup"><span data-stu-id="480f0-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="480f0-116">この複数の反復アプローチの目的は、各変更の理由を理解できるようにすることです。</span><span class="sxs-lookup"><span data-stu-id="480f0-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="480f0-117">イテレーション #1 - アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="480f0-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="480f0-118">最初のイテレーションでは、できるだけ簡単な方法で連絡先マネージャーを作成します。</span><span class="sxs-lookup"><span data-stu-id="480f0-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="480f0-119">基本的なデータベース操作のサポートを追加: 作成、読み取り、更新、および削除 (CRUD) 。</span><span class="sxs-lookup"><span data-stu-id="480f0-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="480f0-120">イテレーション #2 - アプリケーションを見栄えよくします。</span><span class="sxs-lookup"><span data-stu-id="480f0-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="480f0-121">このイテレーションでは、既定の ASP.NET MVC ビュー マスター ページとカスケード スタイル シートを変更することで、アプリケーションの外観を向上させます。</span><span class="sxs-lookup"><span data-stu-id="480f0-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="480f0-122">イテレーション #3 - フォームの検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="480f0-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="480f0-123">3 回目のイテレーションでは、基本的なフォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="480f0-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="480f0-124">必須のフォームフィールドに入力せずにフォームを送信できないようにします。</span><span class="sxs-lookup"><span data-stu-id="480f0-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="480f0-125">また、メールアドレスと電話番号も検証します。</span><span class="sxs-lookup"><span data-stu-id="480f0-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="480f0-126">イテレーション #4 - アプリケーションを疎結合にします。</span><span class="sxs-lookup"><span data-stu-id="480f0-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="480f0-127">この 4 回目のイテレーションでは、いくつかのソフトウェア設計パターンを利用して、Contact Manager アプリケーションの保守と変更を容易にします。</span><span class="sxs-lookup"><span data-stu-id="480f0-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="480f0-128">たとえば、リポジトリ パターンと依存関係の挿入パターンを使用するようにアプリケーションをリファクタリングします。</span><span class="sxs-lookup"><span data-stu-id="480f0-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="480f0-129">イテレーション #5 - 単体テストを作成します。</span><span class="sxs-lookup"><span data-stu-id="480f0-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="480f0-130">5 回目のイテレーションでは、単体テストを追加することで、アプリケーションの保守と変更を容易にします。</span><span class="sxs-lookup"><span data-stu-id="480f0-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="480f0-131">データ モデル クラスをモックし、コントローラーと検証ロジックの単体テストをビルドします。</span><span class="sxs-lookup"><span data-stu-id="480f0-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="480f0-132">イテレーション #6 - テスト駆動型開発を使用します。</span><span class="sxs-lookup"><span data-stu-id="480f0-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="480f0-133">この 6 回目のイテレーションでは、単体テストを最初に記述し、単体テストに対してコードを記述することで、アプリケーションに新しい機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="480f0-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="480f0-134">このイテレーションでは、連絡先グループを追加します。</span><span class="sxs-lookup"><span data-stu-id="480f0-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="480f0-135">イテレーション #7 - Ajax 機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="480f0-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="480f0-136">7 回目のイテレーションでは、Ajax のサポートを追加することで、アプリケーションの応答性とパフォーマンスを向上させます。</span><span class="sxs-lookup"><span data-stu-id="480f0-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="480f0-137">このイテレーション</span><span class="sxs-lookup"><span data-stu-id="480f0-137">This Iteration</span></span>

<span data-ttu-id="480f0-138">連絡先マネージャー アプリケーションのこの 2 回目のイテレーションでは、基本的なフォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="480f0-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="480f0-139">必須フォームフィールドの値を入力せずに、連絡先を送信できないようにします。</span><span class="sxs-lookup"><span data-stu-id="480f0-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="480f0-140">電話番号と電子メール アドレスも検証します (図 1 参照)。</span><span class="sxs-lookup"><span data-stu-id="480f0-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>

<span data-ttu-id="480f0-141">[![[New Project]\(新しいプロジェクト\) ダイアログ ボックス](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="480f0-141">[![The New Project dialog box](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span></span>

<span data-ttu-id="480f0-142">**図 01**: 検証を行うフォーム ([フルサイズの画像を表示する をクリック](iteration-3-add-form-validation-cs/_static/image2.png)して )</span><span class="sxs-lookup"><span data-stu-id="480f0-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-cs/_static/image2.png))</span></span>

<span data-ttu-id="480f0-143">このイテレーションでは、コント ローラー アクションに直接検証ロジックを追加します。</span><span class="sxs-lookup"><span data-stu-id="480f0-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="480f0-144">一般に、これはASP.NET MVC アプリケーションに検証を追加する推奨される方法ではありません。</span><span class="sxs-lookup"><span data-stu-id="480f0-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="480f0-145">アプリケーションの検証ロジックを別の[サービス層](http://martinfowler.com/eaaCatalog/serviceLayer.html)に配置する方が良い方法です。</span><span class="sxs-lookup"><span data-stu-id="480f0-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="480f0-146">次のイテレーションでは、アプリケーションをより保守しやすくするために、Contact Manager アプリケーションをリファクタリングします。</span><span class="sxs-lookup"><span data-stu-id="480f0-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="480f0-147">このイテレーションでは、単純な処理を行うために、すべての検証コードを手入力で記述します。</span><span class="sxs-lookup"><span data-stu-id="480f0-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="480f0-148">検証コードを自分で記述する代わりに、検証フレームワークを利用できます。</span><span class="sxs-lookup"><span data-stu-id="480f0-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="480f0-149">たとえば、Microsoft エンタープライズ ライブラリ検証アプリケーション ブロック (VAB) を使用して、ASP.NET MVC アプリケーションの検証ロジックを実装できます。</span><span class="sxs-lookup"><span data-stu-id="480f0-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="480f0-150">検証アプリケーション ブロックの詳細については、次の項目を参照してください。</span><span class="sxs-lookup"><span data-stu-id="480f0-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="480f0-151">作成ビューへの検証の追加</span><span class="sxs-lookup"><span data-stu-id="480f0-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="480f0-152">まず、検証ロジックを作成ビューに追加します。</span><span class="sxs-lookup"><span data-stu-id="480f0-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="480f0-153">さいわい、Visual Studio で作成ビューを生成したので、作成ビューには検証メッセージを表示するために必要なすべてのユーザー インターフェイス ロジックが既に含まれています。</span><span class="sxs-lookup"><span data-stu-id="480f0-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="480f0-154">作成ビューはリスト 1 に含まれています。</span><span class="sxs-lookup"><span data-stu-id="480f0-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="480f0-155">**リスト 1 - \ビュー\連絡先\作成.aspx**</span><span class="sxs-lookup"><span data-stu-id="480f0-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

<span data-ttu-id="480f0-156">HTML フォームのすぐ上に表示される Html.ValidationSummary() ヘルパー メソッドの呼び出しに注意してください。</span><span class="sxs-lookup"><span data-stu-id="480f0-156">Notice the call to the Html.ValidationSummary() helper method that appears immediately above the HTML form.</span></span> <span data-ttu-id="480f0-157">検証エラー メッセージがある場合、このメソッドは、箇条書きリストに検証メッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="480f0-157">If there are validation error messages, then this method displays validation messages in a bulleted list.</span></span>

<span data-ttu-id="480f0-158">さらに、各フォーム フィールドの横に表示される Html.ValidationMessage() の呼び出しも確認してください。</span><span class="sxs-lookup"><span data-stu-id="480f0-158">Notice, furthermore, the calls to Html.ValidationMessage() that appear next to each form field.</span></span> <span data-ttu-id="480f0-159">ヘルパーは、個々 の検証エラー メッセージを表示します。</span><span class="sxs-lookup"><span data-stu-id="480f0-159">The ValidationMessage() helper displays an individual validation error message.</span></span> <span data-ttu-id="480f0-160">リスト 1 の場合、検証エラーが発生するとアスタリスクが表示されます。</span><span class="sxs-lookup"><span data-stu-id="480f0-160">In the case of Listing 1, an asterisk is displayed when there is a validation error.</span></span>

<span data-ttu-id="480f0-161">最後に、ヘルパーによって表示されるプロパティに関連付けられた検証エラーが発生すると、Html.TextBox() ヘルパーはカスケード スタイル シート クラスを自動的にレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="480f0-161">Finally, the Html.TextBox() helper automatically renders a Cascading Style Sheet class when there is a validation error associated with the property displayed by the helper.</span></span> <span data-ttu-id="480f0-162">Html.TextBox() ヘルパーは **、入力検証エラー**という名前のクラスをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="480f0-162">The Html.TextBox() helper renders a class named **input-validation-error**.</span></span>

<span data-ttu-id="480f0-163">新しいASP.NET MVC アプリケーションを作成すると、Site.css という名前のスタイル シートが自動的にコンテンツ フォルダーに作成されます。</span><span class="sxs-lookup"><span data-stu-id="480f0-163">When you create a new ASP.NET MVC application, a style sheet named Site.css is created in the Content folder automatically.</span></span> <span data-ttu-id="480f0-164">このスタイル シートには、検証エラー メッセージの外観に関連する CSS クラスの次の定義が含まれています。</span><span class="sxs-lookup"><span data-stu-id="480f0-164">This style sheet contains the following definitions for CSS classes related to the appearance of validation error messages:</span></span>

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

<span data-ttu-id="480f0-165">フィールド検証エラー クラスは、Html.ValidationMessage() ヘルパーによってレンダリングされる出力のスタイルを設定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="480f0-165">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="480f0-166">入力検証エラー クラスは、Html.TextBox() ヘルパーによってレンダリングされるテキストボックス (入力) のスタイルを設定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="480f0-166">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="480f0-167">検証サマリー エラー クラスは、Html.ValidationSummary() ヘルパーによって表示される順序なしリストのスタイルを設定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="480f0-167">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="480f0-168">このセクションで説明するスタイル シート クラスを変更して、検証エラー メッセージの外観をカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="480f0-168">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>

## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="480f0-169">作成アクションへの検証ロジックの追加</span><span class="sxs-lookup"><span data-stu-id="480f0-169">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="480f0-170">現時点では、メッセージを生成するロジックを記述していないため、Create ビューに検証エラー メッセージが表示されることはありません。</span><span class="sxs-lookup"><span data-stu-id="480f0-170">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="480f0-171">検証エラー メッセージを表示するには、ModelState にエラー メッセージを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="480f0-171">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="480f0-172">UpdateModel() メソッドは、フォーム フィールドの値をプロパティに割り当てる際にエラーが発生すると、ModelState にエラー メッセージを自動的に追加します。</span><span class="sxs-lookup"><span data-stu-id="480f0-172">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="480f0-173">たとえば、DateTime 値を受け取る誕生日プロパティに文字列 "apple" を割り当てようとすると、UpdateModel() メソッドはモデル状態にエラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="480f0-173">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>

<span data-ttu-id="480f0-174">リスト 2 で変更された Create() メソッドには、新しい連絡先がデータベースに挿入される前に、Contact クラスのプロパティを検証する新しいセクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="480f0-174">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="480f0-175">**リスト 2 - コント ローラー\ContactController.cs (検証を使用して作成)**</span><span class="sxs-lookup"><span data-stu-id="480f0-175">**Listing 2 - Controllers\ContactController.cs (Create with validation)**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

<span data-ttu-id="480f0-176">検証セクションでは、次の 4 つの異なる検証規則が適用されます。</span><span class="sxs-lookup"><span data-stu-id="480f0-176">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="480f0-177">FirstName プロパティの長さは 0 より大きくする必要があります (スペースだけで構成することはできません)。</span><span class="sxs-lookup"><span data-stu-id="480f0-177">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="480f0-178">LastName プロパティの長さが 0 より大きい必要があります (スペースだけで構成することはできません)。</span><span class="sxs-lookup"><span data-stu-id="480f0-178">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="480f0-179">Phone プロパティに値が設定されている場合 (長さが 0 より大きい場合)、Phone プロパティは正規表現と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="480f0-179">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="480f0-180">Email プロパティに値 (長さが 0 より大きい値) がある場合、Email プロパティは正規表現と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="480f0-180">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="480f0-181">検証規則違反がある場合は、エラー メッセージが追加されます、 AddModelError() メソッドの助けを借りて、 ModelState です。</span><span class="sxs-lookup"><span data-stu-id="480f0-181">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="480f0-182">ModelState にメッセージを追加する場合は、プロパティの名前と検証エラー メッセージのテキストを指定します。</span><span class="sxs-lookup"><span data-stu-id="480f0-182">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="480f0-183">このエラー メッセージは、ヘルパー メソッドによってビューに表示されます。</span><span class="sxs-lookup"><span data-stu-id="480f0-183">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="480f0-184">検証規則が実行された後、モデル状態の IsValid プロパティがチェックされます。</span><span class="sxs-lookup"><span data-stu-id="480f0-184">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="480f0-185">検証エラー メッセージが ModelState に追加された場合、IsValid プロパティは false を返します。</span><span class="sxs-lookup"><span data-stu-id="480f0-185">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="480f0-186">検証が失敗した場合、エラー メッセージと共に作成フォームが再表示されます。</span><span class="sxs-lookup"><span data-stu-id="480f0-186">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="480f0-187">私は、正規表現リポジトリから電話番号とメールアドレスを検証するための正規表現を取得しました。[*http://regexlib.com*](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="480f0-187">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>

## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="480f0-188">編集アクションへの検証ロジックの追加</span><span class="sxs-lookup"><span data-stu-id="480f0-188">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="480f0-189">Edit() アクションは連絡先を更新します。</span><span class="sxs-lookup"><span data-stu-id="480f0-189">The Edit() action updates a Contact.</span></span> <span data-ttu-id="480f0-190">Edit() アクションは、Create() アクションとまったく同じ検証を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="480f0-190">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="480f0-191">同じ検証コードを複製するのではなく、Create() アクションと Edit() アクションの両方が同じ検証メソッドを呼び出すように、連絡先コントローラーをリファクタリングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="480f0-191">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="480f0-192">変更された連絡先コントローラー クラスは、リスト 3 に含まれています。</span><span class="sxs-lookup"><span data-stu-id="480f0-192">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="480f0-193">このクラスには、Create() アクションと Edit() アクションの両方で呼び出される新しい ValidateContact() メソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="480f0-193">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="480f0-194">**リスト 3 - コントローラー\コンタクトコントローラー.cs**</span><span class="sxs-lookup"><span data-stu-id="480f0-194">**Listing 3 - Controllers\ContactController.cs**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="480f0-195">まとめ</span><span class="sxs-lookup"><span data-stu-id="480f0-195">Summary</span></span>

<span data-ttu-id="480f0-196">このイテレーションでは、連絡先マネージャー アプリケーションに基本的なフォーム検証を追加しました。</span><span class="sxs-lookup"><span data-stu-id="480f0-196">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="480f0-197">この検証ロジックにより、ユーザーは、FirstName プロパティと LastName プロパティに値を指定せずに、新しい連絡先を送信したり、既存の連絡先を編集したりできなくなります。</span><span class="sxs-lookup"><span data-stu-id="480f0-197">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="480f0-198">さらに、ユーザーは有効な電話番号と電子メールアドレスを入力する必要があります。</span><span class="sxs-lookup"><span data-stu-id="480f0-198">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="480f0-199">このイテレーションでは、可能な限り簡単な方法で、Contact Manager アプリケーションに検証ロジックを追加しました。</span><span class="sxs-lookup"><span data-stu-id="480f0-199">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="480f0-200">しかし、検証ロジックをコントローラロジックに組み込むと、長期的に問題が発生します。</span><span class="sxs-lookup"><span data-stu-id="480f0-200">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="480f0-201">アプリケーションは、時間の経過と同時に保守や変更が難しくなります。</span><span class="sxs-lookup"><span data-stu-id="480f0-201">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="480f0-202">次のイテレーションでは、検証ロジックとデータベース アクセス ロジックをコントローラからリファクタリングします。</span><span class="sxs-lookup"><span data-stu-id="480f0-202">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="480f0-203">いくつかのソフトウェア設計原則を活用して、より緩やかに結合され、保守性の高いアプリケーションを作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="480f0-203">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="480f0-204">[前へ](iteration-2-make-the-application-look-nice-cs.md)
> [次へ](iteration-4-make-the-application-loosely-coupled-cs.md)</span><span class="sxs-lookup"><span data-stu-id="480f0-204">[Previous](iteration-2-make-the-application-look-nice-cs.md)
[Next](iteration-4-make-the-application-loosely-coupled-cs.md)</span></span>
