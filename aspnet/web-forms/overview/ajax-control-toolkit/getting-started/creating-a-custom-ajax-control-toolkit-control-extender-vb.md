---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: カスタム AJAX コントロール ツールキット コントロール エクステンダ (VB) を作成する |マイクロソフトドキュメント
author: rick-anderson
description: カスタム エクステンダを使用すると、新しいクラスを作成しなくても、ASP.NET コントロールの機能をカスタマイズおよび拡張できます。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: adce8e23ccf0a3364ee85534e98f8ea67ae4718d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543679"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a><span data-ttu-id="44269-103">カスタム AJAX Control Toolkit コントロール エクステンダーを作成する (VB)</span><span class="sxs-lookup"><span data-stu-id="44269-103">Creating a Custom AJAX Control Toolkit Control Extender (VB)</span></span>

<span data-ttu-id="44269-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="44269-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="44269-105">カスタム エクステンダを使用すると、新しいクラスを作成しなくても、ASP.NET コントロールの機能をカスタマイズおよび拡張できます。</span><span class="sxs-lookup"><span data-stu-id="44269-105">Custom Extenders enable you to customize and extend the capabilities of ASP.NET controls without having to create new classes.</span></span>

<span data-ttu-id="44269-106">このチュートリアルでは、カスタム AJAX コントロール ツールキット コントロール エクステンダーを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="44269-106">In this tutorial, you learn how to create a custom AJAX Control Toolkit control extender.</span></span> <span data-ttu-id="44269-107">TextBox にテキストを入力するときにボタンの状態を無効から有効にする、シンプルで便利な新しいエクステンダを作成します。</span><span class="sxs-lookup"><span data-stu-id="44269-107">We create a simple, but useful, new extender that changes the state of a Button from disabled to enabled when you type text into a TextBox.</span></span> <span data-ttu-id="44269-108">このチュートリアルを読んだ後、独自のコントロール エクステンダを使用して ASP.NET AJAX ツールキットを拡張できるようになります。</span><span class="sxs-lookup"><span data-stu-id="44269-108">After reading this tutorial, you will be able to extend the ASP.NET AJAX Toolkit with your own control extenders.</span></span>

<span data-ttu-id="44269-109">カスタム コントロール エクステンダは、Visual Studio または Visual Web 開発者を使用して作成できます (Visual Web 開発者の最新バージョンを使用していることを確認してください)。</span><span class="sxs-lookup"><span data-stu-id="44269-109">You can create custom control extenders using either Visual Studio or Visual Web Developer (make sure that you have the latest version of Visual Web Developer).</span></span>

## <a name="overview-of-the-disabledbutton-extender"></a><span data-ttu-id="44269-110">無効ボタン エクステンダーの概要</span><span class="sxs-lookup"><span data-stu-id="44269-110">Overview of the DisabledButton Extender</span></span>

<span data-ttu-id="44269-111">新しいコントロール エクステンダは、DisabledButton エクステンダーという名前です。</span><span class="sxs-lookup"><span data-stu-id="44269-111">Our new control extender is named the DisabledButton extender.</span></span> <span data-ttu-id="44269-112">このエクステンダには、次の 3 つのプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="44269-112">This extender will have three properties:</span></span>

- <span data-ttu-id="44269-113">ターゲット コントロール ID - コントロールが拡張するテキスト ボックス。</span><span class="sxs-lookup"><span data-stu-id="44269-113">TargetControlID - The TextBox that the control extends.</span></span>
- <span data-ttu-id="44269-114">ターゲットボタンIID - 無効または有効になっているボタン。</span><span class="sxs-lookup"><span data-stu-id="44269-114">TargetButtonIID - The Button that is disabled or enabled.</span></span>
- <span data-ttu-id="44269-115">無効テキスト - ボタンに最初に表示されるテキスト。</span><span class="sxs-lookup"><span data-stu-id="44269-115">DisabledText - The text that is initially displayed in the Button.</span></span> <span data-ttu-id="44269-116">入力を開始すると、ボタンにはボタンテキストプロパティの値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="44269-116">When you start typing, the Button displays the value of the Button Text property.</span></span>

<span data-ttu-id="44269-117">テキスト ボックスとボタン コントロールに無効ボタン エクステンダーをフックします。</span><span class="sxs-lookup"><span data-stu-id="44269-117">You hook the DisabledButton extender to a TextBox and Button control.</span></span> <span data-ttu-id="44269-118">テキストを入力する前に、ボタンは無効になっており、テキスト ボックスとボタンは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="44269-118">Before you type any text, the Button is disabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

<span data-ttu-id="44269-119">([フルサイズの画像を表示するには クリック](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="44269-119">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))</span></span>

<span data-ttu-id="44269-120">テキストの入力を開始すると、ボタンが有効になり、テキスト ボックスとボタンは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="44269-120">After you start typing text, the Button is enabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

<span data-ttu-id="44269-121">([フルサイズの画像を表示するには クリック](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="44269-121">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))</span></span>

<span data-ttu-id="44269-122">コントロール エクステンダを作成するには、次の 3 つのファイルを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44269-122">To create our control extender, we need to create the following three files:</span></span>

- <span data-ttu-id="44269-123">DisabledButtonExtender.vb - このファイルは、エクステンダの作成を管理し、デザイン時にプロパティを設定できるようにするサーバー側のコントロール クラスです。</span><span class="sxs-lookup"><span data-stu-id="44269-123">DisabledButtonExtender.vb - This file is the server-side control class that will manage creating your extender and allow you to set the properties at design-time.</span></span> <span data-ttu-id="44269-124">また、エクステンダに設定できるプロパティも定義します。</span><span class="sxs-lookup"><span data-stu-id="44269-124">It also defines the properties that can be set on your extender.</span></span> <span data-ttu-id="44269-125">これらのプロパティには、コードを使用して、デザイン時にアクセスし、DisableButtonBehavior.js ファイルで定義されているプロパティと一致するプロパティを一致させます。</span><span class="sxs-lookup"><span data-stu-id="44269-125">These properties are accessible via code and at design time and match properties defined in the DisableButtonBehavior.js file.</span></span>
- <span data-ttu-id="44269-126">無効なボタン動作.js -- このファイルは、すべてのクライアント スクリプト ロジックを追加する場所です。</span><span class="sxs-lookup"><span data-stu-id="44269-126">DisabledButtonBehavior.js -- This file is where you will add all of your client script logic.</span></span>
- <span data-ttu-id="44269-127">このクラスは、デザイン時機能を有効にします。</span><span class="sxs-lookup"><span data-stu-id="44269-127">DisabledButtonDesigner.vb - This class enables design-time functionality.</span></span> <span data-ttu-id="44269-128">コントロール エクステンダーが Visual Studio/Visual Web 開発者デザイナーで正しく動作するようにするには、このクラスが必要です。</span><span class="sxs-lookup"><span data-stu-id="44269-128">You need this class if you want the control extender to work correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="44269-129">そのため、コントロール エクステンダは、サーバー側コントロール、クライアント側の動作、およびサーバー側のデザイナー クラスで構成されます。</span><span class="sxs-lookup"><span data-stu-id="44269-129">So a control extender consists of a server-side control, a client-side behavior, and a server-side designer class.</span></span> <span data-ttu-id="44269-130">これらの 3 つのファイルをすべて作成する方法については、以下のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="44269-130">You learn how to create all three of these files in the following sections.</span></span>

## <a name="creating-the-custom-extender-website-and-project"></a><span data-ttu-id="44269-131">カスタム エクステンダ Web サイトとプロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="44269-131">Creating the Custom Extender Website and Project</span></span>

<span data-ttu-id="44269-132">最初の手順は、Visual Studio/Visual Web 開発者でクラス ライブラリ プロジェクトと Web サイトを作成することです。</span><span class="sxs-lookup"><span data-stu-id="44269-132">The first step is to create a class library project and website in Visual Studio/Visual Web Developer.</span></span> <span data-ttu-id="44269-133">クラス ライブラリ プロジェクトでカスタム エクステンダーを作成し、Web サイトでカスタム エクステンダーをテストします。</span><span class="sxs-lookup"><span data-stu-id="44269-133">We�ll create the custom extender in the class library project and test the custom extender in the website.</span></span>

<span data-ttu-id="44269-134">ウェブサイトから始めましょう。</span><span class="sxs-lookup"><span data-stu-id="44269-134">Let�s start with the website.</span></span> <span data-ttu-id="44269-135">Web サイトを作成するには、次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="44269-135">Follow these steps to create the website:</span></span>

1. <span data-ttu-id="44269-136">メニュー オプションの **[ファイル]、[ 新しい Web サイト**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="44269-136">Select the menu option **File, New Web Site**.</span></span>
2. <span data-ttu-id="44269-137">**[ASP.NET Web サイト]** テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="44269-137">Select the **ASP.NET Web Site** template.</span></span>
3. <span data-ttu-id="44269-138">新しいウェブサイトに*名前を付ける Web サイト1.*</span><span class="sxs-lookup"><span data-stu-id="44269-138">Name the new website *Website1*.</span></span>
4. <span data-ttu-id="44269-139">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="44269-139">Click the **OK** button.</span></span>

<span data-ttu-id="44269-140">次に、コントロール エクステンダのコードを含むクラス ライブラリ プロジェクトを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44269-140">Next, we need to create the class library project that will contain the code for the control extender:</span></span>

1. <span data-ttu-id="44269-141">メニュー オプションの **[ファイル]、[追加]、[新しいプロジェクト**] の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="44269-141">Select the menu option **File, Add, New Project**.</span></span>
2. <span data-ttu-id="44269-142">クラス**ライブラリ**テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="44269-142">Select the **Class Library** template.</span></span>
3. <span data-ttu-id="44269-143">新しいクラス ライブラリに**CustomExtenders**という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="44269-143">Name the new class library with the name **CustomExtenders**.</span></span>
4. <span data-ttu-id="44269-144">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="44269-144">Click the **OK** button.</span></span>

<span data-ttu-id="44269-145">これらの手順を完了すると、ソリューション エクスプローラーウィンドウは図 1 のようになります。</span><span class="sxs-lookup"><span data-stu-id="44269-145">After you complete these steps, your Solution Explorer window should look like Figure 1.</span></span>

<span data-ttu-id="44269-146">[![Web サイトおよびクラス ライブラリ プロジェクトを使用したソリューション](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="44269-146">[![Solution with website and class library project](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="44269-147">**図 01**: Web サイトとクラス ライブラリ プロジェクトを含むソリューション ([フルサイズの画像を表示するには クリック](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="44269-147">**Figure 01**: Solution with website and class library project([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))</span></span>

<span data-ttu-id="44269-148">次に、必要なすべてのアセンブリ参照をクラス ライブラリ プロジェクトに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44269-148">Next, you need to add all of the necessary assembly references to the class library project:</span></span>

1. <span data-ttu-id="44269-149">CustomExtenders プロジェクトを右クリックし、メニュー オプションの **[参照の追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="44269-149">Right-click the CustomExtenders project and select the menu option **Add Reference**.</span></span>
2. <span data-ttu-id="44269-150">[.NET] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="44269-150">Select the .NET tab.</span></span>
3. <span data-ttu-id="44269-151">次のアセンブリへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="44269-151">Add references to the following assemblies:</span></span>

    1. <span data-ttu-id="44269-152">System.Web.dll</span><span class="sxs-lookup"><span data-stu-id="44269-152">System.Web.dll</span></span>
    2. <span data-ttu-id="44269-153">System.Web.Extensions.dll</span><span class="sxs-lookup"><span data-stu-id="44269-153">System.Web.Extensions.dll</span></span>
    3. <span data-ttu-id="44269-154">System.Design.dll</span><span class="sxs-lookup"><span data-stu-id="44269-154">System.Design.dll</span></span>
    4. <span data-ttu-id="44269-155">システム.Web.エクステンション.デザイン.dll</span><span class="sxs-lookup"><span data-stu-id="44269-155">System.Web.Extensions.Design.dll</span></span>
4. <span data-ttu-id="44269-156">[参照] タブを選択します。</span><span class="sxs-lookup"><span data-stu-id="44269-156">Select the Browse tab.</span></span>
5. <span data-ttu-id="44269-157">アセンブリへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="44269-157">Add a reference to the AjaxControlToolkit.dll assembly.</span></span> <span data-ttu-id="44269-158">このアセンブリは、AJAX コントロール ツールキットをダウンロードしたフォルダーにあります。</span><span class="sxs-lookup"><span data-stu-id="44269-158">This assembly is located in the folder where you downloaded the AJAX Control Toolkit.</span></span>

<span data-ttu-id="44269-159">プロジェクトを右クリックし、[プロパティ] を選択して [参照設定] タブをクリックすると、すべての正しい参照が追加されたことを確認できます (図 2 参照)。</span><span class="sxs-lookup"><span data-stu-id="44269-159">You can verify that you have added all of the right references by right-clicking your project, selecting Properties, and clicking the References tab (see Figure 2).</span></span>

<span data-ttu-id="44269-160">[![必要な参照を含む参照フォルダ](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="44269-160">[![References folder with required references](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)</span></span>

<span data-ttu-id="44269-161">**図 02**: 参照が必須のフォルダ ([フルサイズの画像を表示する をクリック](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="44269-161">**Figure 02**: References folder with required references([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))</span></span>

## <a name="creating-the-custom-control-extender"></a><span data-ttu-id="44269-162">カスタム コントロール エクステンダの作成</span><span class="sxs-lookup"><span data-stu-id="44269-162">Creating the Custom Control Extender</span></span>

<span data-ttu-id="44269-163">クラス ライブラリができたので、エクステンダー コントロールの構築を開始できます。</span><span class="sxs-lookup"><span data-stu-id="44269-163">Now that we have our class library, we can start building our extender control.</span></span> <span data-ttu-id="44269-164">カスタム エクステンダー コントロール クラスの裸のボーンから始めましょう (リスト 1 を参照)。</span><span class="sxs-lookup"><span data-stu-id="44269-164">Let�s start with the bare bones of a custom extender control class (see Listing 1).</span></span>

<span data-ttu-id="44269-165">**リスト 1 - マイカスタムエクステンダー.vb**</span><span class="sxs-lookup"><span data-stu-id="44269-165">**Listing 1 - MyCustomExtender.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

<span data-ttu-id="44269-166">リスト 1 のコントロール エクステンダー クラスについて、いくつかの点が分かります。</span><span class="sxs-lookup"><span data-stu-id="44269-166">There are several things that you notice about the control extender class in Listing 1.</span></span> <span data-ttu-id="44269-167">まず、クラスが基本の ExtenderControlBase クラスから継承していることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="44269-167">First, notice that the class inherits from the base ExtenderControlBase class.</span></span> <span data-ttu-id="44269-168">すべての AJAX コントロール ツールキットエクステンダー コントロールは、この基本クラスから派生します。</span><span class="sxs-lookup"><span data-stu-id="44269-168">All AJAX Control Toolkit extender controls derive from this base class.</span></span> <span data-ttu-id="44269-169">たとえば、基本クラスには、各コントロール エクステンダの必須プロパティである TargetID プロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="44269-169">For example, the base class includes the TargetID property that is a required property of every control extender.</span></span>

<span data-ttu-id="44269-170">次に、このクラスには、クライアント スクリプトに関連する次の 2 つの属性が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="44269-170">Next, notice that the class includes the following two attributes related to client script:</span></span>

- <span data-ttu-id="44269-171">WebResource - ファイルをアセンブリに埋め込みリソースとして含めます。</span><span class="sxs-lookup"><span data-stu-id="44269-171">WebResource - Causes a file to be included as an embedded resource in an assembly.</span></span>
- <span data-ttu-id="44269-172">クライアント スクリプト リソース - アセンブリからスクリプト リソースを取得します。</span><span class="sxs-lookup"><span data-stu-id="44269-172">ClientScriptResource - Causes a script resource to be retrieved from an assembly.</span></span>

<span data-ttu-id="44269-173">属性は、カスタム エクステンダーがコンパイルされるときに、アセンブリに MyControlBehavior.js JavaScript ファイルを埋め込むために使用されます。</span><span class="sxs-lookup"><span data-stu-id="44269-173">The WebResource attribute is used to embed the MyControlBehavior.js JavaScript file into the assembly when the custom extender is compiled.</span></span> <span data-ttu-id="44269-174">属性は、カスタム エクステンダーが Web ページで使用されている場合にアセンブリから MyControlBehavior.js スクリプトを取得するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="44269-174">The ClientScriptResource attribute is used to retrieve the MyControlBehavior.js script from the assembly when the custom extender is used in a web page.</span></span>

<span data-ttu-id="44269-175">Web リソース属性とクライアントスクリプトリソース属性が機能するには、埋め込みリソースとして JavaScript ファイルをコンパイルする必要があります。</span><span class="sxs-lookup"><span data-stu-id="44269-175">In order for the WebResource and ClientScriptResource attributes to work, you must compile the JavaScript file as an embedded resource.</span></span> <span data-ttu-id="44269-176">[ソリューション エクスプローラー] ウィンドウでファイルを選択し、プロパティ シートを開き、"**ビルド アクション**" プロパティに値*埋め込みリソース*を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="44269-176">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property.</span></span>

<span data-ttu-id="44269-177">コントロール エクステンダにも、ターゲット コントロールタイプ属性が含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="44269-177">Notice that the control extender also includes a TargetControlType attribute.</span></span> <span data-ttu-id="44269-178">この属性は、コントロール エクステンダーによって拡張されるコントロールの種類を指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="44269-178">This attribute is used to specify the type of control that is extended by the control extender.</span></span> <span data-ttu-id="44269-179">リスト 1 の場合、コントロール エクステンダを使用して TextBox を拡張します。</span><span class="sxs-lookup"><span data-stu-id="44269-179">In the case of Listing 1, the control extender is used to extend a TextBox.</span></span>

<span data-ttu-id="44269-180">最後に、カスタム エクステンダに MyProperty という名前のプロパティが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="44269-180">Finally, notice that the custom extender includes a property named MyProperty.</span></span> <span data-ttu-id="44269-181">プロパティは、エクステンダー コントロールプロパティ属性でマークされています。</span><span class="sxs-lookup"><span data-stu-id="44269-181">The property is marked with the ExtenderControlProperty attribute.</span></span> <span data-ttu-id="44269-182">GetPropertyValue() メソッドと SetPropertyValue() メソッドは、サーバー側のコントロール エクステンダーからクライアント側の動作にプロパティ値を渡すために使用されます。</span><span class="sxs-lookup"><span data-stu-id="44269-182">The GetPropertyValue() and SetPropertyValue() methods are used to pass the property value from the server-side control extender to the client-side behavior.</span></span>

<span data-ttu-id="44269-183">先に進んで、私たちのDisabledボタンエクステンダーのコードを実装しましょう。</span><span class="sxs-lookup"><span data-stu-id="44269-183">Let�s go ahead and implement the code for our DisabledButton extender.</span></span> <span data-ttu-id="44269-184">このエクステンダーのコードは、リスト 2 にあります。</span><span class="sxs-lookup"><span data-stu-id="44269-184">The code for this extender can be found in Listing 2.</span></span>

<span data-ttu-id="44269-185">**リスト 2 - 無効なボタンエクステンダー.vb**</span><span class="sxs-lookup"><span data-stu-id="44269-185">**Listing 2 - DisabledButtonExtender.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

<span data-ttu-id="44269-186">リスト 2 の DisabledButton エクステンダーには、ターゲット ボタン ID と無効テキストという名前の 2 つのプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="44269-186">The DisabledButton extender in Listing 2 has two properties named TargetButtonID and DisabledText.</span></span> <span data-ttu-id="44269-187">プロパティに適用される ID 参照プロパティは、ボタン コントロールの ID 以外のこのプロパティを割り当てることを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="44269-187">The IDReferenceProperty applied to the TargetButtonID property prevents you from assigning anything other than the ID of a Button control to this property.</span></span>

<span data-ttu-id="44269-188">属性は、このエクステンダーに DisabledButtonBehavior.js という名前のファイルにあるクライアント側の動作を関連付けます。</span><span class="sxs-lookup"><span data-stu-id="44269-188">The WebResource and ClientScriptResource attributes associate a client-side behavior located in a file named DisabledButtonBehavior.js with this extender.</span></span> <span data-ttu-id="44269-189">この JavaScript ファイルについては、次のセクションで説明します。</span><span class="sxs-lookup"><span data-stu-id="44269-189">We discuss this JavaScript file in the next section.</span></span>

## <a name="creating-the-custom-extender-behavior"></a><span data-ttu-id="44269-190">カスタム エクステンダー動作の作成</span><span class="sxs-lookup"><span data-stu-id="44269-190">Creating the Custom Extender Behavior</span></span>

<span data-ttu-id="44269-191">コントロール エクステンダのクライアント側コンポーネントは動作と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="44269-191">The client-side component of a control extender is called a behavior.</span></span> <span data-ttu-id="44269-192">ボタンを無効にして有効にするための実際のロジックは、DisabledButton 動作に含まれています。</span><span class="sxs-lookup"><span data-stu-id="44269-192">The actual logic for disabling and enabling the Button is contained in the DisabledButton behavior.</span></span> <span data-ttu-id="44269-193">この動作の JavaScript コードは、リスト 3 に含まれています。</span><span class="sxs-lookup"><span data-stu-id="44269-193">The JavaScript code for the behavior is included in Listing 3.</span></span>

<span data-ttu-id="44269-194">**リスト 3 - 無効なボタン.js**</span><span class="sxs-lookup"><span data-stu-id="44269-194">**Listing 3 - DisabledButton.js**</span></span>

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

<span data-ttu-id="44269-195">リスト 3 の JavaScript ファイルには、無効なボタン動作という名前のクライアント側クラスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="44269-195">The JavaScript file in Listing 3 contains a client-side class named DisabledButtonBehavior.</span></span> <span data-ttu-id="44269-196">このクラスには、サーバー側のツインと同様に、ターゲット ボタン ID と無効テキストという名前の 2\_つのプロパティが含\_まれており、ターゲット ボタン\_ID/セット\_ターゲット ボタン ID を使用してアクセスし、無効なテキスト/設定無効テキストを取得できます。</span><span class="sxs-lookup"><span data-stu-id="44269-196">This class, like its server-side twin, includes two properties named TargetButtonID and DisabledText which you can access using get\_TargetButtonID/set\_TargetButtonID and get\_DisabledText/set\_DisabledText.</span></span>

<span data-ttu-id="44269-197">initialize() メソッドは、キーアップ イベント ハンドラを動作のターゲット要素に関連付けます。</span><span class="sxs-lookup"><span data-stu-id="44269-197">The initialize() method associates a keyup event handler with the target element for the behavior.</span></span> <span data-ttu-id="44269-198">この動作に関連付けられたテキスト ボックスに文字を入力するたびに、keyup ハンドラーが実行されます。</span><span class="sxs-lookup"><span data-stu-id="44269-198">Each time you type a letter into the TextBox associated with this behavior, the keyup handler executes.</span></span> <span data-ttu-id="44269-199">keyup ハンドラは、動作に関連付けられた TextBox にテキストが含まれているかどうかに応じて、Button を有効または無効にします。</span><span class="sxs-lookup"><span data-stu-id="44269-199">The keyup handler either enables or disables the Button depending on whether the TextBox associated with the behavior contains any text.</span></span>

<span data-ttu-id="44269-200">リスト 3 の JavaScript ファイルは、埋め込みリソースとしてコンパイルする必要があります。</span><span class="sxs-lookup"><span data-stu-id="44269-200">Remember that you must compile the JavaScript file in Listing 3 as an embedded resource.</span></span> <span data-ttu-id="44269-201">[ソリューション エクスプローラー] ウィンドウでファイルを選択し、プロパティ シートを開き、"*埋め込みリソース*" プロパティを **[ビルド アクション**] プロパティに割り当てます (図 3 参照)。</span><span class="sxs-lookup"><span data-stu-id="44269-201">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property (see Figure 3).</span></span> <span data-ttu-id="44269-202">このオプションは、Visual Studio と Visual Web 開発者の両方で使用できます。</span><span class="sxs-lookup"><span data-stu-id="44269-202">This option is available in both Visual Studio and Visual Web Developer.</span></span>

<span data-ttu-id="44269-203">[![埋め込みリソースとしての JavaScript ファイルの追加](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="44269-203">[![Adding a JavaScript file as an embedded resource](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)</span></span>

<span data-ttu-id="44269-204">**図 03**: JavaScript ファイルを埋め込みリソースとして追加する ([フルサイズの画像を表示する をクリック](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="44269-204">**Figure 03**: Adding a JavaScript file as an embedded resource([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))</span></span>

## <a name="creating-the-custom-extender-designer"></a><span data-ttu-id="44269-205">カスタム エクステンダー デザイナーの作成</span><span class="sxs-lookup"><span data-stu-id="44269-205">Creating the Custom Extender Designer</span></span>

<span data-ttu-id="44269-206">エクステンダーを完成させるために作成する必要がある最後のクラスが 1 つあります。</span><span class="sxs-lookup"><span data-stu-id="44269-206">There is one last class that we need to create to complete our extender.</span></span> <span data-ttu-id="44269-207">リスト 4 でデザイナー クラスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44269-207">We need to create the designer class in Listing 4.</span></span> <span data-ttu-id="44269-208">このクラスは、Visual Studio/Visual Web 開発者デザイナーでエクステンダーが正しく動作するようにするために必要です。</span><span class="sxs-lookup"><span data-stu-id="44269-208">This class is required to make the extender behave correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="44269-209">**リスト 4 - 無効なボタンデザイナー.vb**</span><span class="sxs-lookup"><span data-stu-id="44269-209">**Listing 4 - DisabledButtonDesigner.vb**</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

<span data-ttu-id="44269-210">リスト 4 のデザイナーを、無効ボタン エクステンダーとデザイナー属性に関連付けます。次のように、デザイナー属性を DisabledExtender クラスに適用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44269-210">You associate the designer in Listing 4 with the DisabledButton extender with the Designer attribute.You need to apply the Designer attribute to the DisabledButtonExtender class like this:</span></span>

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a><span data-ttu-id="44269-211">カスタム エクステンダの使用</span><span class="sxs-lookup"><span data-stu-id="44269-211">Using the Custom Extender</span></span>

<span data-ttu-id="44269-212">DisabledButton コントロール エクステンダーの作成が完了したので、ASP.NETの Web サイトで使用する時間です。</span><span class="sxs-lookup"><span data-stu-id="44269-212">Now that we have finished creating the DisabledButton control extender, it is time to use it in our ASP.NET website.</span></span> <span data-ttu-id="44269-213">まず、カスタム エクステンダをツールボックスに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44269-213">First, we need to add the custom extender to the toolbox.</span></span> <span data-ttu-id="44269-214">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="44269-214">Follow these steps:</span></span>

1. <span data-ttu-id="44269-215">ソリューション エクスプローラー ウィンドウでページをダブルクリックして、ASP.NET ページを開きます。</span><span class="sxs-lookup"><span data-stu-id="44269-215">Open an ASP.NET page by double-clicking the page in the Solution Explorer window.</span></span>
2. <span data-ttu-id="44269-216">ツールボックスを右クリックし、メニュー オプションの [**アイテムの選択]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="44269-216">Right-click the toolbox and select the menu option **Choose Items**.</span></span>
3. <span data-ttu-id="44269-217">[ツールボックス項目の選択] ダイアログで、CustomExtenders.dll アセンブリを参照します。</span><span class="sxs-lookup"><span data-stu-id="44269-217">In the Choose Toolbox Items dialog, browse to the CustomExtenders.dll assembly.</span></span>
4. <span data-ttu-id="44269-218">**[OK]ボタン**をクリックしてダイアログを閉じます。</span><span class="sxs-lookup"><span data-stu-id="44269-218">Click the **OK** button to close the dialog.</span></span>

<span data-ttu-id="44269-219">これらの手順を完了すると、DisabledButton コントロール エクステンダーがツールボックスに表示されます (図 4 参照)。</span><span class="sxs-lookup"><span data-stu-id="44269-219">After you complete these steps, the DisabledButton control extender should appear in the toolbox (see Figure 4).</span></span>

<span data-ttu-id="44269-220">[![ツールボックスの [無効にする] ボタン](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="44269-220">[![DisabledButton in the toolbox](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)</span></span>

<span data-ttu-id="44269-221">**図 04**: ツールボックス内の [無効] ボタン ([フルサイズの画像を表示する をクリック](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png)します)</span><span class="sxs-lookup"><span data-stu-id="44269-221">**Figure 04**: DisabledButton in the toolbox([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))</span></span>

<span data-ttu-id="44269-222">次に、新しいASP.NETページを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44269-222">Next, we need to create a new ASP.NET page.</span></span> <span data-ttu-id="44269-223">次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="44269-223">Follow these steps:</span></span>

1. <span data-ttu-id="44269-224">という名前の新しいASP.NET ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="44269-224">Create a new ASP.NET page named ShowDisabledButton.aspx.</span></span>
2. <span data-ttu-id="44269-225">スクリプト マネージャーをページにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="44269-225">Drag a ScriptManager onto the page.</span></span>
3. <span data-ttu-id="44269-226">TextBox コントロールをページ上にドラッグします。</span><span class="sxs-lookup"><span data-stu-id="44269-226">Drag a TextBox control onto the page.</span></span>
4. <span data-ttu-id="44269-227">ボタン コントロールをページにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="44269-227">Drag a Button control onto the page.</span></span>
5. <span data-ttu-id="44269-228">[プロパティ] ウィンドウで、"ボタン ID" プロパティを値<em>btnSave</em>に変更し、Text プロパティを値 [*\*保存 ]* に変更します。</span><span class="sxs-lookup"><span data-stu-id="44269-228">In the Properties window, change the Button ID property to the value <em>btnSave</em> and the Text property to the value *Save\**.</span></span>

<span data-ttu-id="44269-229">標準のテキスト ボックス コントロールとボタン コントロールASP.NETページを作成しました。</span><span class="sxs-lookup"><span data-stu-id="44269-229">We created a page with a standard ASP.NET TextBox and Button control.</span></span>

<span data-ttu-id="44269-230">次に、無効ボタン エクステンダーを使用してテキスト ボックス コントロールを拡張する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44269-230">Next, we need to extend the TextBox control with the DisabledButton extender:</span></span>

1. <span data-ttu-id="44269-231">エクステンダー ウィザード ダイアログを開くには、[**エクステンダーの追加**] タスク オプションを選択します (図 5 参照)。</span><span class="sxs-lookup"><span data-stu-id="44269-231">Select the **Add Extender** task option to open the Extender Wizard dialog (see Figure 5).</span></span> <span data-ttu-id="44269-232">ダイアログには、カスタムの DisabledButton エクステンダーが含まれていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="44269-232">Notice that the dialog includes our custom DisabledButton extender.</span></span>
2. <span data-ttu-id="44269-233">無効ボタン エクステンダを選択し **、[OK] ボタン**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="44269-233">Select the DisabledButton extender and click the **OK** button.</span></span>

<span data-ttu-id="44269-234">[![エクステンダー ウィザード ダイアログ](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="44269-234">[![The Extender Wizard dialog](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)</span></span>

<span data-ttu-id="44269-235">**図 05**: エクステンダ ウィザード ダイアログ ([フルサイズの画像を表示する をクリック](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="44269-235">**Figure 05**: The Extender Wizard dialog([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))</span></span>

<span data-ttu-id="44269-236">最後に、無効ボタン エクステンダーのプロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="44269-236">Finally, we can set the properties of the DisabledButton extender.</span></span> <span data-ttu-id="44269-237">TextBox コントロールのプロパティを変更することで、DisabledButton エクステンダーのプロパティを変更できます。</span><span class="sxs-lookup"><span data-stu-id="44269-237">You can modify the properties of the DisabledButton extender by modifying the properties of the TextBox control:</span></span>

1. <span data-ttu-id="44269-238">デザイナーでテキスト ボックスを選択します。</span><span class="sxs-lookup"><span data-stu-id="44269-238">Select the TextBox in the Designer.</span></span>
2. <span data-ttu-id="44269-239">[プロパティ] ウィンドウで、[エクステンダー] ノードを展開します (図 6 を参照)。</span><span class="sxs-lookup"><span data-stu-id="44269-239">In the Properties window, expand the Extenders node (see Figure 6).</span></span>
3. <span data-ttu-id="44269-240">値を*割*り当てるに保存する、無効テキストプロパティと*値 btn保存*にプロパティに保存します。</span><span class="sxs-lookup"><span data-stu-id="44269-240">Assign the value *Save* to the DisabledText property and the value *btnSave* to the TargetButtonID property.</span></span>

<span data-ttu-id="44269-241">[![エクステンダー プロパティの設定](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="44269-241">[![Setting extender properties](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)</span></span>

<span data-ttu-id="44269-242">**図 06**: エクステンダープロパティの設定 ([フルサイズの画像を表示する をクリック](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="44269-242">**Figure 06**: Setting extender properties([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))</span></span>

<span data-ttu-id="44269-243">ページを (F5 キーを押して) 実行すると、Button コントロールは最初は無効になります。</span><span class="sxs-lookup"><span data-stu-id="44269-243">When you run the page (by hitting F5), the Button control is initially disabled.</span></span> <span data-ttu-id="44269-244">TextBox にテキストを入力し始めるとすぐに、Button コントロールが有効になります (図 7 参照)。</span><span class="sxs-lookup"><span data-stu-id="44269-244">As soon as you start entering text into the TextBox, the Button control is enabled (see Figure 7).</span></span>

<span data-ttu-id="44269-245">[![無効ボタン エクステンダーの動作](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="44269-245">[![The DisabledButton extender in action](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)</span></span>

<span data-ttu-id="44269-246">**図 07**: DisabledButton エクステンダーの動作 ([フルサイズの画像を表示する をクリック](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="44269-246">**Figure 07**: The DisabledButton extender in action([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))</span></span>

## <a name="summary"></a><span data-ttu-id="44269-247">まとめ</span><span class="sxs-lookup"><span data-stu-id="44269-247">Summary</span></span>

<span data-ttu-id="44269-248">このチュートリアルの目的は、カスタム エクステンダー コントロールを使用して AJAX コントロール ツールキットを拡張する方法を説明することです。</span><span class="sxs-lookup"><span data-stu-id="44269-248">The goal of this tutorial was to explain how you can extend the AJAX Control Toolkit with custom extender controls.</span></span> <span data-ttu-id="44269-249">このチュートリアルでは、単純な DisabledButton コントロール エクステンダーを作成しました。</span><span class="sxs-lookup"><span data-stu-id="44269-249">In this tutorial, we created a simple DisabledButton control extender.</span></span> <span data-ttu-id="44269-250">このエクステンダーを実装するには、無効なボタンエクステンダー クラス、無効なボタン動作の JavaScript 動作、および無効なボタンデザイナー クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="44269-250">We implemented this extender by creating a DisabledButtonExtender class, a DisabledButtonBehavior JavaScript behavior, and a DisabledButtonDesigner class.</span></span> <span data-ttu-id="44269-251">カスタム コントロール エクステンダを作成するときは、常に同様の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="44269-251">You follow a similar set of steps whenever you create a custom control extender.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="44269-252">前へ</span><span class="sxs-lookup"><span data-stu-id="44269-252">Previous</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
