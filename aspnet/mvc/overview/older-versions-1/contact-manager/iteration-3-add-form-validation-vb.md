---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: '繰り返し #3 – フォーム検証を追加する (VB) |Microsoft Docs'
author: microsoft
description: 3 番目のイテレーションでは、基本的なフォーム検証を追加します。 ユーザーは、必要なフォームのフィールドを完了しなくても、フォームを送信できないようにようにします。 私たちも emai を検証しています.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 73b307f53875abe84b592c75b1ff614ffd9d8b82
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65123977"
---
# <a name="iteration-3--add-form-validation-vb"></a><span data-ttu-id="bcdde-105">繰り返し #3 – フォーム検証を追加する (VB)</span><span class="sxs-lookup"><span data-stu-id="bcdde-105">Iteration #3 – Add form validation (VB)</span></span>

<span data-ttu-id="bcdde-106">によって[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="bcdde-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="bcdde-107">コードをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="bcdde-107">Download Code</span></span>](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> <span data-ttu-id="bcdde-108">3 番目のイテレーションでは、基本的なフォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="bcdde-109">ユーザーは、必要なフォームのフィールドを完了しなくても、フォームを送信できないようにようにします。</span><span class="sxs-lookup"><span data-stu-id="bcdde-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="bcdde-110">また、電子メール アドレスと電話番号を検証しました。</span><span class="sxs-lookup"><span data-stu-id="bcdde-110">We also validate email addresses and phone numbers.</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="bcdde-111">ASP.NET MVC 連絡先管理アプリケーション (VB) の構築</span><span class="sxs-lookup"><span data-stu-id="bcdde-111">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="bcdde-112">このチュートリアル シリーズでは、開始から終了に全体連絡先管理アプリケーションを構築します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="bcdde-113">Contact Manager アプリケーションは、ユーザーの一覧については店舗連絡先情報の名前、電話番号、電子メール アドレスにするようにことができます。</span><span class="sxs-lookup"><span data-stu-id="bcdde-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="bcdde-114">複数のイテレーションにおける、アプリケーションを構築します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="bcdde-115">反復処理ごとに、アプリケーション徐々 に向上します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="bcdde-116">この複数のイテレーションのアプローチの目的は、各変更の理由を理解するためです。</span><span class="sxs-lookup"><span data-stu-id="bcdde-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="bcdde-117">繰り返し #1 - は、アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="bcdde-118">最初のイテレーションを作成、連絡先マネージャー最も簡単な方法で考えられるします。</span><span class="sxs-lookup"><span data-stu-id="bcdde-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="bcdde-119">基本的なデータベース操作のサポートを追加します。作成、読み取り、更新、および削除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="bcdde-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="bcdde-120">繰り返し #2 - は、素敵に見えるアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="bcdde-121">このイテレーションで、アプリケーションの見た目を向上させる、既定の ASP.NET MVC ビュー マスター ページを変更し、カスケード スタイル シート。</span><span class="sxs-lookup"><span data-stu-id="bcdde-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="bcdde-122">繰り返し #3 - フォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="bcdde-123">3 番目のイテレーションでは、基本的なフォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="bcdde-124">ユーザーは、必要なフォームのフィールドを完了しなくても、フォームを送信できないようにようにします。</span><span class="sxs-lookup"><span data-stu-id="bcdde-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="bcdde-125">また、電子メール アドレスと電話番号を検証しました。</span><span class="sxs-lookup"><span data-stu-id="bcdde-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="bcdde-126">繰り返し #4 - は、アプリケーションを疎結合を作成します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="bcdde-127">この 4 番目のイテレーションで、保守し、Contact Manager アプリケーションの変更を容易にできるようにするソフトウェア設計パターンをいくつかの利点を実行します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="bcdde-128">たとえば、Repository パターンと依存関係の注入パターンを使用するようにアプリケーションをリファクタリングします。</span><span class="sxs-lookup"><span data-stu-id="bcdde-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="bcdde-129">繰り返し #5 - 単体テストを作成します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="bcdde-130">5 番目のイテレーションでアプリケーションと簡単に維持単体テストを追加して変更します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="bcdde-131">データ モデル クラスの模擬テストを実行し、コント ローラーと検証ロジックの単体テストをビルドします。</span><span class="sxs-lookup"><span data-stu-id="bcdde-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="bcdde-132">繰り返し #6 - は、テスト駆動開発を使用します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="bcdde-133">この 6 番目のイテレーションでは、アプリケーションに新しい機能を追加には、まず単体テストの記述、単体テストに対してコードを記述します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="bcdde-134">このイテレーションは、連絡先グループを追加します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="bcdde-135">繰り返し #7 - Ajax 機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="bcdde-136">7 番目のイテレーションで改良、応答性と、アプリケーションのパフォーマンスの Ajax のサポートを追加します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="bcdde-137">このイテレーション</span><span class="sxs-lookup"><span data-stu-id="bcdde-137">This Iteration</span></span>

<span data-ttu-id="bcdde-138">Contact Manager アプリケーションの 2 番目のイテレーションでは、基本的なフォーム検証を追加します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="bcdde-139">により、ユーザーが必要なフォーム フィールドの値を入力しなくても、連絡先を送信できないようにします。</span><span class="sxs-lookup"><span data-stu-id="bcdde-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="bcdde-140">また、電話番号、電子メール アドレスが (図 1 参照) を検証しました。</span><span class="sxs-lookup"><span data-stu-id="bcdde-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>

<span data-ttu-id="bcdde-141">[![[新しいプロジェクト] ダイアログ ボックス](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bcdde-141">[![The New Project dialog box](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span></span>

<span data-ttu-id="bcdde-142">**図 01**:検証を使用して、フォーム ([フルサイズの画像を表示する をクリックします](iteration-3-add-form-validation-vb/_static/image2.png))。</span><span class="sxs-lookup"><span data-stu-id="bcdde-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-vb/_static/image2.png))</span></span>

<span data-ttu-id="bcdde-143">このイテレーションでは、コント ローラー アクションに直接検証ロジックを追加します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="bcdde-144">一般に、これは、ASP.NET MVC アプリケーションに検証を追加することをお勧めの方法ではありません。</span><span class="sxs-lookup"><span data-stu-id="bcdde-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="bcdde-145">別のアプリケーションの検証ロジックを配置するほうが効果的[サービス層](http://martinfowler.com/eaaCatalog/serviceLayer.html)します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="bcdde-146">次のイテレーションは、アプリケーションを保守しやすくなりますように Contact Manager アプリケーションをリファクタリングします。</span><span class="sxs-lookup"><span data-stu-id="bcdde-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="bcdde-147">このイテレーションで、簡単に記述するすべての検証コードを手動で。</span><span class="sxs-lookup"><span data-stu-id="bcdde-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="bcdde-148">自分たちの検証コードを記述する、する代わりに、検証フレームワークの利点を取得できます。 します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="bcdde-149">たとえば、ASP.NET MVC アプリケーションの検証ロジックを実装するために、Microsoft エンタープライズ ライブラリ検証アプリケーション ブロック (VAB) を使用できます。</span><span class="sxs-lookup"><span data-stu-id="bcdde-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="bcdde-150">詳細については、検証アプリケーション ブロックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="bcdde-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="bcdde-151">ビューを作成する検証の追加</span><span class="sxs-lookup"><span data-stu-id="bcdde-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="bcdde-152">検証ロジックを作成ビューに追加することで開始 s を使用できます。</span><span class="sxs-lookup"><span data-stu-id="bcdde-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="bcdde-153">さいわい、Visual Studio を使用したビューを作成する、生成されたため、ビューを作成する既に含まれていますすべての検証メッセージを表示するために必要なユーザー インターフェイス ロジック。</span><span class="sxs-lookup"><span data-stu-id="bcdde-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="bcdde-154">リスト 1 で、作成ビューが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bcdde-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="bcdde-155">**Listing 1 - \Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="bcdde-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

<span data-ttu-id="bcdde-156">フィールドの検証エラー クラスは、Html.ValidationMessage() ヘルパーによってレンダリングされる出力のスタイル設定に使用されます。</span><span class="sxs-lookup"><span data-stu-id="bcdde-156">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="bcdde-157">入力検証エラー クラスは、Html.TextBox() ヘルパーによって表示されるテキスト ボックス (入力) のスタイル設定に使用されます。</span><span class="sxs-lookup"><span data-stu-id="bcdde-157">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="bcdde-158">検証の概要-エラー クラスは、Html.ValidationSummary() ヘルパーによって表示される順序なしリストをスタイル設定に使用されます。</span><span class="sxs-lookup"><span data-stu-id="bcdde-158">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="bcdde-159">検証エラー メッセージの外観をカスタマイズするには、このセクションで説明されているスタイル シートのクラスを変更することができます。</span><span class="sxs-lookup"><span data-stu-id="bcdde-159">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>

## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="bcdde-160">検証ロジックを追加する、アクションの作成</span><span class="sxs-lookup"><span data-stu-id="bcdde-160">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="bcdde-161">現在のところ、作成ビューは検証エラー メッセージをすべてのメッセージを生成するためのロジックを作成していないために表示されません。</span><span class="sxs-lookup"><span data-stu-id="bcdde-161">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="bcdde-162">検証エラー メッセージを表示するためには、ModelState にエラー メッセージを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bcdde-162">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="bcdde-163">UpdateModel() メソッドのエラー メッセージに追加 ModelState 自動的にフォーム フィールドの値をプロパティに割り当てエラーがある場合にします。</span><span class="sxs-lookup"><span data-stu-id="bcdde-163">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="bcdde-164">たとえば、"apple"の文字列を DateTime 値を受け入れる BirthDate プロパティに割り当てるしようとした場合、UpdateModel() メソッドに追加しますエラー ModelState。</span><span class="sxs-lookup"><span data-stu-id="bcdde-164">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>

<span data-ttu-id="bcdde-165">リスト 2 で修正された Create() メソッドには、新しい連絡先は、データベースに挿入される前に、Contact クラスのプロパティを検証する新しいセクションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bcdde-165">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="bcdde-166">**2 - Controllers\ContactController.vb (検証で作成) を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="bcdde-166">**Listing 2 - Controllers\ContactController.vb (Create with validation)**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

<span data-ttu-id="bcdde-167">検証のセクションでは、次の 4 つの個別の検証規則を適用します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-167">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="bcdde-168">FirstName プロパティ、長さが 0 より大きい必要があります (およびスペースのみが構成することができません)</span><span class="sxs-lookup"><span data-stu-id="bcdde-168">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="bcdde-169">LastName プロパティの長さが 0 より大きい必要があります (およびスペースのみが構成することができません)</span><span class="sxs-lookup"><span data-stu-id="bcdde-169">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="bcdde-170">電話プロパティに値が設定されている場合 (長さが 0 より大きい値を持つ) 電話プロパティ正規表現と一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bcdde-170">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="bcdde-171">電子メール プロパティに値が設定されている場合 (長さが 0 より大きい値を持つ) し、電子メールのプロパティが正規表現に一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bcdde-171">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="bcdde-172">検証規則違反がある場合に、エラー メッセージが AddModelError() メソッドのヘルプで ModelState に追加されます。</span><span class="sxs-lookup"><span data-stu-id="bcdde-172">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="bcdde-173">ModelState にメッセージを追加する場合は、プロパティの名前と、検証エラー メッセージのテキストを提供します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-173">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="bcdde-174">このエラー メッセージは、Html.ValidationSummary() および Html.ValidationMessage() ヘルパー メソッドによって、ビューに表示されます。</span><span class="sxs-lookup"><span data-stu-id="bcdde-174">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="bcdde-175">検証規則が実行された後は、ModelState の IsValid プロパティがチェックします。</span><span class="sxs-lookup"><span data-stu-id="bcdde-175">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="bcdde-176">ModelState に検証エラー メッセージが追加されたときに、IsValid プロパティが false を返します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-176">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="bcdde-177">検証に失敗した場合は、エラー メッセージを使用したフォームを作成するが再表示されます。</span><span class="sxs-lookup"><span data-stu-id="bcdde-177">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="bcdde-178">正規表現のリポジトリから電話番号、電子メール アドレスを検証するための正規表現が表示されました [*http://regexlib.com*](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="bcdde-178">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>

## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="bcdde-179">編集の操作に検証ロジックを追加します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-179">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="bcdde-180">Edit() アクションでは、連絡先を更新します。</span><span class="sxs-lookup"><span data-stu-id="bcdde-180">The Edit() action updates a Contact.</span></span> <span data-ttu-id="bcdde-181">Edit() アクションは、Create() アクションと正確に同じ検証を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bcdde-181">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="bcdde-182">同じ検証コードを複製するのではなく Create() と Edit() の両方のアクションが同じ検証メソッドを呼び出せるように、連絡先のコント ローラーをリファクタリングする必要があります。</span><span class="sxs-lookup"><span data-stu-id="bcdde-182">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="bcdde-183">変更後にお問い合わせくださいコント ローラー クラスは、リスト 3 に含まれます。</span><span class="sxs-lookup"><span data-stu-id="bcdde-183">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="bcdde-184">このクラスには、Create() と Edit() の両方のアクション内で呼び出される新しい ValidateContact() メソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="bcdde-184">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="bcdde-185">**Listing 3 - Controllers\ContactController.vb**</span><span class="sxs-lookup"><span data-stu-id="bcdde-185">**Listing 3 - Controllers\ContactController.vb**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a><span data-ttu-id="bcdde-186">まとめ</span><span class="sxs-lookup"><span data-stu-id="bcdde-186">Summary</span></span>

<span data-ttu-id="bcdde-187">このイテレーションでは、Contact Manager アプリケーションを基本的なフォーム検証を追加しました。</span><span class="sxs-lookup"><span data-stu-id="bcdde-187">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="bcdde-188">この検証ロジックでは、ユーザーが新しい連絡先を送信したり、FirstName および LastName プロパティの値を指定せず、既存の連絡先を編集できないようにします。</span><span class="sxs-lookup"><span data-stu-id="bcdde-188">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="bcdde-189">さらに、ユーザーは、有効な電話番号と電子メール アドレスを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bcdde-189">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="bcdde-190">このイテレーションで最も簡単な方法で、Contact Manager アプリケーションに検証ロジックをしました。</span><span class="sxs-lookup"><span data-stu-id="bcdde-190">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="bcdde-191">ただしに、コント ローラー ロジック、検証ロジックを混在させる問題が発生私たちにとって長期的にします。</span><span class="sxs-lookup"><span data-stu-id="bcdde-191">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="bcdde-192">アプリケーションの保守し、時間の経過と共に変更をより困難になります。</span><span class="sxs-lookup"><span data-stu-id="bcdde-192">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="bcdde-193">次のイテレーションで、検証ロジックとデータベース アクセス ロジックをコント ローラーからにリファクタリングされます。</span><span class="sxs-lookup"><span data-stu-id="bcdde-193">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="bcdde-194">柔軟に結合し、保守性がアプリケーションを作成することを有効にするソフトウェア設計の原則をいくつかの利点がご説明しましょう。</span><span class="sxs-lookup"><span data-stu-id="bcdde-194">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bcdde-195">[前へ](iteration-2-make-the-application-look-nice-vb.md)
> [次へ](iteration-4-make-the-application-loosely-coupled-vb.md)</span><span class="sxs-lookup"><span data-stu-id="bcdde-195">[Previous](iteration-2-make-the-application-look-nice-vb.md)
[Next](iteration-4-make-the-application-loosely-coupled-vb.md)</span></span>
