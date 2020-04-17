---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 ページモデル |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NET 1.x では、開発者はインライン コード モデルと分離コード モデルのどちらかを選択しました。 分離コードは、Src attr..のいずれかを使用して実装できます。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: 6c2435a06d04209db21fb8e075f68ff0b7a9ef7e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542860"
---
# <a name="the-aspnet-20-page-model"></a><span data-ttu-id="63e3c-104">ASP.NET 2.0 ページ モデル</span><span class="sxs-lookup"><span data-stu-id="63e3c-104">The ASP.NET 2.0 Page Model</span></span>

<span data-ttu-id="63e3c-105">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="63e3c-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="63e3c-106">ASP.NET 1.x では、開発者はインライン コード モデルと分離コード モデルのどちらかを選択しました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-106">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="63e3c-107">分離コードは、@Pageディレクティブの Src 属性または分離コード属性を使用して実装できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-107">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="63e3c-108">ASP.NET 2.0 では、開発者はインライン コードと分離コードのどちらかを選択できますが、分離コード モデルが大幅に強化されています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-108">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

<span data-ttu-id="63e3c-109">ASP.NET 1.x では、開発者はインライン コード モデルと分離コード モデルのどちらかを選択しました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-109">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="63e3c-110">分離コードは、@Pageディレクティブの Src 属性または分離コード属性を使用して実装できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-110">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="63e3c-111">ASP.NET 2.0 では、開発者はインライン コードと分離コードのどちらかを選択できますが、分離コード モデルが大幅に強化されています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-111">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

## <a name="improvements-in-the-code-behind-model"></a><span data-ttu-id="63e3c-112">分離コード モデルの改善点</span><span class="sxs-lookup"><span data-stu-id="63e3c-112">Improvements in the Code-Behind Model</span></span>

<span data-ttu-id="63e3c-113">ASP.NET 2.0 の分離コード モデルの変更点を完全に理解するために、モデルを 1.x に存在する場合は、そのモデルASP.NET迅速に確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="63e3c-113">In order to fully understand the changes in the code-behind model in ASP.NET 2.0, its best to quickly review the model as it existed in ASP.NET 1.x.</span></span>

## <a name="the-code-behind-model-in-aspnet-1x"></a><span data-ttu-id="63e3c-114">ASP.NET 1.x の分離コード モデル</span><span class="sxs-lookup"><span data-stu-id="63e3c-114">The Code-Behind Model in ASP.NET 1.x</span></span>

<span data-ttu-id="63e3c-115">ASP.NET 1.x では、コード ビハインド モデルは ASPX ファイル (Web フォーム) と、プログラミング コードを含む分離コード ファイルで構成されていました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-115">In ASP.NET 1.x, the code-behind model consisted of an ASPX file (the Webform) and a code-behind file containing programming code.</span></span> <span data-ttu-id="63e3c-116">2 つのファイルは、ASPX@Pageファイル内のディレクティブを使用して接続されています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-116">The two files were connected using the @Page directive in the ASPX file.</span></span> <span data-ttu-id="63e3c-117">ASPX ページの各コントロールには、コード ビハインド ファイル内の対応する宣言がインスタンス変数として含まれています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-117">Each control on the ASPX page had a corresponding declaration in the code-behind file as an instance variable.</span></span> <span data-ttu-id="63e3c-118">分離コード ファイルには、イベント バインディング用のコードと、Visual Studio デザイナーに必要な生成コードも含まれています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-118">The code-behind file also contained code for event binding and generated code necessary for the Visual Studio designer.</span></span> <span data-ttu-id="63e3c-119">このモデルはかなりうまく機能しましたが、ASPX ページ内のすべてのASP.NET要素は、分離コード ファイル内の対応するコードを必要とするため、コードとコンテンツの実際の分離はありませんでした。</span><span class="sxs-lookup"><span data-stu-id="63e3c-119">This model worked fairly well, but because every ASP.NET element in the ASPX page required corresponding code in the code-behind file, there was no true separation of code and content.</span></span> <span data-ttu-id="63e3c-120">たとえば、デザイナーが Visual Studio IDE の外部の ASPX ファイルに新しいサーバー コントロールを追加した場合、分離コード ファイルにそのコントロールの宣言がないため、アプリケーションが中断します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-120">For example, if a designer added a new server control to an ASPX file outside of the Visual Studio IDE, the application would break due to the absence of a declaration for that control in the code-behind file.</span></span>

## <a name="the-code-behind-model-in-aspnet-20"></a><span data-ttu-id="63e3c-121">ASP.NET 2.0 の分離コード モデル</span><span class="sxs-lookup"><span data-stu-id="63e3c-121">The Code-Behind Model in ASP.NET 2.0</span></span>

<span data-ttu-id="63e3c-122">ASP.NET 2.0 はこのモデルを大幅に改善します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-122">ASP.NET 2.0 greatly improves upon this model.</span></span> <span data-ttu-id="63e3c-123">ASP.NET 2.0 では、ASP.NET 2.0 で提供される新しい*部分クラス*を使用して分離コードが実装されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-123">In ASP.NET 2.0, code-behind is implemented using the new *partial classes* provided in ASP.NET 2.0.</span></span> <span data-ttu-id="63e3c-124">ASP.NET 2.0 の分離コード クラスは、部分クラスとして定義されています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-124">The code-behind class in ASP.NET 2.0 is defined as a partial class meaning that it contains only part of the class definition.</span></span> <span data-ttu-id="63e3c-125">クラス定義の残りの部分は、実行時または Web サイトがプリコンパイルされるときに ASPX ページを使用して ASP.NET 2.0 によって動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-125">The remaining part of the class definition is dynamically generated by ASP.NET 2.0 using the ASPX page at runtime or when the Web site is precompiled.</span></span> <span data-ttu-id="63e3c-126">コード ビハインド ファイルと ASPX ページ間のリンクは、 @ Page ディレクティブを使用して確立されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-126">The link between the code-behind file and the ASPX page is still established using the @ Page directive.</span></span> <span data-ttu-id="63e3c-127">ただし、分離コード属性または Src 属性の代わりに、ASP.NET 2.0 では CodeFile 属性が使用されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-127">However, instead of a CodeBehind or Src attribute, ASP.NET 2.0 now uses the CodeFile attribute.</span></span> <span data-ttu-id="63e3c-128">継承属性は、ページのクラス名を指定するためにも使用されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-128">The Inherits attribute is also used to specify the class name for the page.</span></span>

<span data-ttu-id="63e3c-129">一般的な @ Page ディレクティブは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-129">A typical @ Page directive might look like this:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

<span data-ttu-id="63e3c-130">ASP.NET 2.0 の分離コード ファイルの一般的なクラス定義は、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-130">A typical class definition in an ASP.NET 2.0 code-behind file might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="63e3c-131">C# と Visual Basic は、現在部分クラスをサポートしている唯一のマネージ言語です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-131">C# and Visual Basic are the only managed languages that currently support partial classes.</span></span> <span data-ttu-id="63e3c-132">したがって、J# を使用する開発者は、ASP.NET 2.0 で分離コード モデルを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-132">Therefore, developers using J# will not be able to use the code-behind model in ASP.NET 2.0.</span></span>

<span data-ttu-id="63e3c-133">開発者は、作成したコードのみを含むコード ファイルを作成するため、新しいモデルは分離コード モデルを強化します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-133">The new model enhances the code-behind model because developers will now have code files that contain only the code that they have created.</span></span> <span data-ttu-id="63e3c-134">また、分離コード ファイルにはインスタンス変数の宣言がないため、コードとコンテンツを実際に分離できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-134">It also provides for a true separation of code and content because there are no instance variable declarations in the code-behind file.</span></span>

> [!NOTE]
> <span data-ttu-id="63e3c-135">ASPX ページの部分クラスはイベント バインディングが行われる場所であるため、Visual Basic の開発者は、分離コード内の Handles キーワードを使用してイベントをバインドすることで、パフォーマンスのわずかな向上を実現できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-135">Because the partial class for the ASPX page is where event binding takes place, Visual Basic developers can realize a slight performance increase by using the Handles keyword in code-behind to bind events.</span></span> <span data-ttu-id="63e3c-136">C# には、同等のキーワードはありません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-136">C# has no equivalent keyword.</span></span>

## <a name="new--page-directive-attributes"></a><span data-ttu-id="63e3c-137">新しい @ ページ ディレクティブ属性</span><span class="sxs-lookup"><span data-stu-id="63e3c-137">New @ Page Directive Attributes</span></span>

<span data-ttu-id="63e3c-138">ASP.NET 2.0 は、 @ Page ディレクティブに多くの新しい属性を追加します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-138">ASP.NET 2.0 adds many new attributes to the @ Page directive.</span></span> <span data-ttu-id="63e3c-139">次の属性は、ASP.NET 2.0 で新しく追加されています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-139">The following attributes are new in ASP.NET 2.0.</span></span>

## <a name="async"></a><span data-ttu-id="63e3c-140">Async</span><span class="sxs-lookup"><span data-stu-id="63e3c-140">Async</span></span>

<span data-ttu-id="63e3c-141">Async 属性を使用すると、非同期で実行されるページを構成できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-141">The Async attribute allows you to configure page to be executed asynchronously.</span></span> <span data-ttu-id="63e3c-142">このモジュールの後半で非同期ページを説明します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-142">Well cover asynchronous pages later in this module.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="63e3c-143">非同期タイムアウト</span><span class="sxs-lookup"><span data-stu-id="63e3c-143">AsyncTimeout</span></span>

<span data-ttu-id="63e3c-144">非同期ページのタイムアウトを指定しました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-144">Specified the timeout for asynchronous pages.</span></span> <span data-ttu-id="63e3c-145">デフォルトは 45 秒です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-145">The default is 45 seconds.</span></span>

## <a name="codefile"></a><span data-ttu-id="63e3c-146">Codefile</span><span class="sxs-lookup"><span data-stu-id="63e3c-146">CodeFile</span></span>

<span data-ttu-id="63e3c-147">コード ファイル属性は、Visual Studio 2002/2003 の分離コード属性の代わりです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-147">The CodeFile attribute is the replacement for the CodeBehind attribute in Visual Studio 2002/2003.</span></span>

### <a name="codefilebaseclass"></a><span data-ttu-id="63e3c-148">クラス</span><span class="sxs-lookup"><span data-stu-id="63e3c-148">CodeFileBaseClass</span></span>

<span data-ttu-id="63e3c-149">CodeFileBaseClass 属性は、複数のページを 1 つの基本クラスから派生させる場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-149">The CodeFileBaseClass attribute is used in cases where you want multiple pages to derive from a single base class.</span></span> <span data-ttu-id="63e3c-150">この属性を指定せずにASP.NET部分クラスを実装しているため、共有の共通フィールドを使用して ASPX ページで宣言されたコントロールを参照する基本クラスは、ASP.NETs コンパイル エンジンがページ内のコントロールに基づいて新しいメンバーを自動的に作成するため、正しく動作しません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-150">Because of the implementation of partial classes in ASP.NET, without this attribute, a base class that uses shared common fields to reference controls declared in an ASPX page would not work properly because ASP.NETs compilation engine will automatically create new members based on controls in the page.</span></span> <span data-ttu-id="63e3c-151">したがって、ASP.NETで 2 つ以上のページに共通の基本クラスを作成する場合は、CodeFileBaseClass 属性で基本クラスを定義し、その基本クラスから各ページ クラスを派生させる必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-151">Therefore, if you want a common base class for two or more pages in ASP.NET, you will need to define specify your base class in the CodeFileBaseClass attribute and then derive each pages class from that base class.</span></span> <span data-ttu-id="63e3c-152">この属性を使用する場合は、CodeFile 属性も必要です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-152">The CodeFile attribute is also required when this attribute is used.</span></span>

## <a name="compilationmode"></a><span data-ttu-id="63e3c-153">コンパイルモード</span><span class="sxs-lookup"><span data-stu-id="63e3c-153">CompilationMode</span></span>

<span data-ttu-id="63e3c-154">この属性を使用すると、ASPX ページのコンパイル モード プロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-154">This attribute allows you to set the CompilationMode property of the ASPX page.</span></span> <span data-ttu-id="63e3c-155">プロパティは、**値を含**む列挙体常に、**自動**、および**Never**です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-155">The CompilationMode property is an enumeration containing the values **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="63e3c-156">デフォルトは **[常に]** です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-156">The default is **Always**.</span></span> <span data-ttu-id="63e3c-157">**自動**設定を使用すると、可能な場合ASP.NETページが動的にコンパイルされるのを防ぐことができます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-157">The **Auto** setting will prevent ASP.NET from dynamically compiling the page if possible.</span></span> <span data-ttu-id="63e3c-158">動的コンパイルからページを除外すると、パフォーマンスが向上します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-158">Excluding pages from dynamic compilation increases performance.</span></span> <span data-ttu-id="63e3c-159">ただし、除外されるページにコンパイルする必要のあるコードが含まれている場合は、ページを参照するときにエラーがスローされます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-159">However, if a page that is excluded contains that code that must be compiled, an error will be thrown when the page is browsed.</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="63e3c-160">イベントの検証を有効にする</span><span class="sxs-lookup"><span data-stu-id="63e3c-160">EnableEventValidation</span></span>

<span data-ttu-id="63e3c-161">この属性は、ポストバック イベントとコールバック イベントを検証するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-161">This attribute specifies whether or not postback and callback events are validated.</span></span> <span data-ttu-id="63e3c-162">これが有効な場合、ポストバックイベントまたはコールバックイベントの引数がチェックされ、イベントを最初にレンダリングしたサーバー コントロールから発生していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-162">When this is enabled, arguments to postback or callback events are checked to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="63e3c-163">テーマを有効にする</span><span class="sxs-lookup"><span data-stu-id="63e3c-163">EnableTheming</span></span>

<span data-ttu-id="63e3c-164">この属性は、ASP.NETテーマをページで使用するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-164">This attribute specifies whether or not ASP.NET themes are used on a page.</span></span> <span data-ttu-id="63e3c-165">デフォルトは**false**です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-165">The default is **false**.</span></span> <span data-ttu-id="63e3c-166">ASP.NETテーマについては[、モジュール 10](profiles-themes-and-web-parts.md)で説明します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-166">ASP.NET themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="linepragmas"></a><span data-ttu-id="63e3c-167">ラインプラグマ</span><span class="sxs-lookup"><span data-stu-id="63e3c-167">LinePragmas</span></span>

<span data-ttu-id="63e3c-168">この属性は、コンパイル時に行プラグマを追加するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-168">This attribute specifies whether line pragmas should be added during compilation.</span></span> <span data-ttu-id="63e3c-169">行プラグマは、デバッガーがコードの特定のセクションをマークするために使用するオプションです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-169">Line pragmas are options used by debuggers to mark specific sections of code.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="63e3c-170">ポストバックのメンテナンススクロール位置</span><span class="sxs-lookup"><span data-stu-id="63e3c-170">MaintainScrollPositionOnPostback</span></span>

<span data-ttu-id="63e3c-171">この属性は、ポストバック間のスクロール位置を維持するために、ページに JavaScript を挿入するかどうかを指定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-171">This attribute specifies whether or not JavaScript is injected into the page in order to maintain scroll position between postbacks.</span></span> <span data-ttu-id="63e3c-172">この属性は、デフォルトでは**false**です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-172">This attribute is **false** by default.</span></span>

<span data-ttu-id="63e3c-173">この属性が**true の**場合、ASP.NET&lt;は&gt;次のようなスクリプト ブロックをポストバックに追加します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-173">When this attribute is **true**, ASP.NET will add a &lt;script&gt; block on postback that looks like this:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

<span data-ttu-id="63e3c-174">このスクリプト ブロックの src は WebResource.axd であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="63e3c-174">Note that the src for this script block is WebResource.axd.</span></span> <span data-ttu-id="63e3c-175">このリソースは物理パスではありません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-175">This resource is not a physical path.</span></span> <span data-ttu-id="63e3c-176">このスクリプトが要求されると、ASP.NET動的にスクリプトが作成されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-176">When this script is requested, ASP.NET dynamically builds the script.</span></span>

### <a name="masterpagefile"></a><span data-ttu-id="63e3c-177">マスターページファイル</span><span class="sxs-lookup"><span data-stu-id="63e3c-177">MasterPageFile</span></span>

<span data-ttu-id="63e3c-178">この属性は、現在のページのマスター ページ ファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-178">This attribute specifies the master page file for the current page.</span></span> <span data-ttu-id="63e3c-179">相対パスと絶対パスのどちらでも構いません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-179">The path can be relative or absolute.</span></span> <span data-ttu-id="63e3c-180">マスター ページについては、[モジュール 4](master-pages.md)で説明します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-180">Master pages are covered in [Module 4](master-pages.md).</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="63e3c-181">スタイルシートテーマ</span><span class="sxs-lookup"><span data-stu-id="63e3c-181">StyleSheetTheme</span></span>

<span data-ttu-id="63e3c-182">この属性を使用すると、ASP.NET 2.0 テーマで定義されたユーザー インターフェイスの外観プロパティをオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-182">This attribute allows you to override user-interface appearance properties defined by an ASP.NET 2.0 theme.</span></span> <span data-ttu-id="63e3c-183">テーマについては[、モジュール 10](profiles-themes-and-web-parts.md)で説明します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-183">Themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="theme"></a><span data-ttu-id="63e3c-184">テーマ</span><span class="sxs-lookup"><span data-stu-id="63e3c-184">Theme</span></span>

<span data-ttu-id="63e3c-185">ページのテーマを指定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-185">Specifies the theme for the page.</span></span> <span data-ttu-id="63e3c-186">StyleSheetTheme 属性に値が指定されていない場合、テーマ属性はページ上のコントロールに適用されているすべてのスタイルをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="63e3c-186">If a value is not specified for the StyleSheetTheme attribute, the Theme attribute overrides all styles applied to controls on the page.</span></span>

## <a name="title"></a><span data-ttu-id="63e3c-187">タイトル</span><span class="sxs-lookup"><span data-stu-id="63e3c-187">Title</span></span>

<span data-ttu-id="63e3c-188">ページのタイトルを設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-188">Sets the title for the page.</span></span> <span data-ttu-id="63e3c-189">ここで指定した値は、レンダリングされた&lt;ページ&gt;の title 要素に表示されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-189">The value specified here will appear in the &lt;title&gt; element of the rendered page.</span></span>

### <a name="viewstateencryptionmode"></a><span data-ttu-id="63e3c-190">を使用します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-190">ViewStateEncryptionMode</span></span>

<span data-ttu-id="63e3c-191">列挙体の値を設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-191">Sets the value for the ViewStateEncryptionMode enumeration.</span></span> <span data-ttu-id="63e3c-192">使用できる値は **、[常時]、[\*\*\*\*自動**]、[**しない**] です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-192">The available values are **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="63e3c-193">既定値は **[自動] です**。この属性が**Auto**の値に設定されている場合、ビューステートは暗号化され、コントロールは**RegisterRequiresViewStateEncryption**メソッドを呼び出して要求します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-193">The default value is **Auto**. When this attribute is set to a value of **Auto**, viewstate is encrypted is a control requests it by calling the **RegisterRequiresViewStateEncryption** method.</span></span>

## <a name="setting-public-property-values-via-the--page-directive"></a><span data-ttu-id="63e3c-194">@ Page ディレクティブを使用したパブリック プロパティ値の設定</span><span class="sxs-lookup"><span data-stu-id="63e3c-194">Setting Public Property Values via the @ Page Directive</span></span>

<span data-ttu-id="63e3c-195">ASP.NET 2.0 の @ Page ディレクティブのもう 1 つの新機能は、基本クラスのパブリック プロパティの初期値を設定する機能です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-195">Another new capability of the @ Page directive in ASP.NET 2.0 is the ability to set the initial value of public properties of a base class.</span></span> <span data-ttu-id="63e3c-196">たとえば、基本クラスに**SomeText**というパブリック プロパティがあり、ページが読み込まれたときに**Hello**に初期化するとします。</span><span class="sxs-lookup"><span data-stu-id="63e3c-196">Suppose, for example, that you have a public property called **SomeText** in your base class and you d like it to be initialized to **Hello** when a page is loaded.</span></span> <span data-ttu-id="63e3c-197">これを実現するには、@ Page ディレクティブの値を次のように設定するだけです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-197">You can accomplish this by simply setting the value in the @ Page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

<span data-ttu-id="63e3c-198">@ Page ディレクティブの**SomeText**属性は、基本クラスの SomeText プロパティの初期値を*Hello!* に設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-198">The **SomeText** attribute of the @ Page directive sets the initial value of the SomeText property in the base class to *Hello!*.</span></span> <span data-ttu-id="63e3c-199">次のビデオでは、 @ Page ディレクティブを使用して、基本クラスでパブリック プロパティの初期値を設定するチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-199">The video below is a walkthrough of setting the initial value of a public property in a base class using the @ Page directive.</span></span>

![](the-asp-net-2-0-page-model/_static/image1.png)

[<span data-ttu-id="63e3c-200">フルスクリーンビデオを開く</span><span class="sxs-lookup"><span data-stu-id="63e3c-200">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a><span data-ttu-id="63e3c-201">ページ クラスの新しいパブリック プロパティ</span><span class="sxs-lookup"><span data-stu-id="63e3c-201">New Public Properties of the Page Class</span></span>

<span data-ttu-id="63e3c-202">次のパブリック プロパティは、ASP.NET 2.0 で新しく追加されました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-202">The following public properties are new in ASP.NET 2.0.</span></span>

## <a name="apprelativetemplatesourcedirectory"></a><span data-ttu-id="63e3c-203">ディレクトリ</span><span class="sxs-lookup"><span data-stu-id="63e3c-203">AppRelativeTemplateSourceDirectory</span></span>

<span data-ttu-id="63e3c-204">ページまたはコントロールへのアプリケーション相対パスを返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-204">Returns the application-relative path to the page or control.</span></span> <span data-ttu-id="63e3c-205">たとえば、 にあるhttp://app/folder/page.aspxページの場合、プロパティは ~/folder/ を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-205">For example, for a page located at http://app/folder/page.aspx, the property returns ~/folder/.</span></span>

## <a name="apprelativevirtualpath"></a><span data-ttu-id="63e3c-206">仮想パス</span><span class="sxs-lookup"><span data-stu-id="63e3c-206">AppRelativeVirtualPath</span></span>

<span data-ttu-id="63e3c-207">ページまたはコントロールへの相対仮想ディレクトリ パスを返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-207">Returns the relative virtual directory path to the page or control.</span></span> <span data-ttu-id="63e3c-208">たとえば、 にあるhttp://app/folder/page.aspxページの場合、プロパティは ~/フォルダー/page.aspx を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-208">For example for a page located at http://app/folder/page.aspx, the property returns ~/folder/page.aspx.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="63e3c-209">非同期タイムアウト</span><span class="sxs-lookup"><span data-stu-id="63e3c-209">AsyncTimeout</span></span>

<span data-ttu-id="63e3c-210">非同期ページ処理に使用されるタイムアウトを取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-210">Gets or sets the timeout used for asynchronous page handling.</span></span> <span data-ttu-id="63e3c-211">(非同期ページについては、このモジュールの後半で説明します)。</span><span class="sxs-lookup"><span data-stu-id="63e3c-211">(Asynchronous pages will be covered later in this module.)</span></span>

## <a name="clientquerystring"></a><span data-ttu-id="63e3c-212">クライアント文字列</span><span class="sxs-lookup"><span data-stu-id="63e3c-212">ClientQueryString</span></span>

<span data-ttu-id="63e3c-213">要求された URL のクエリ文字列部分を返す読み取り専用プロパティ。</span><span class="sxs-lookup"><span data-stu-id="63e3c-213">A read-only property that returns the query string portion of the requested URL.</span></span> <span data-ttu-id="63e3c-214">この値は URL エンコードされます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-214">This value is URL encoded.</span></span> <span data-ttu-id="63e3c-215">クラスの UrlDecode メソッドを使用して、それをデコードできます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-215">You can use the UrlDecode method of the HttpServerUtility class to decode it.</span></span>

## <a name="clientscript"></a><span data-ttu-id="63e3c-216">クライアントスクリプト</span><span class="sxs-lookup"><span data-stu-id="63e3c-216">ClientScript</span></span>

<span data-ttu-id="63e3c-217">このプロパティは、クライアント側スクリプトの ASP.NETs の発行を管理するために使用できる ClientScriptManager オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-217">This property returns a ClientScriptManager object that can be used to manage ASP.NETs emission of client-side script.</span></span> <span data-ttu-id="63e3c-218">(このモジュールでは、後でクラスについて説明します)。</span><span class="sxs-lookup"><span data-stu-id="63e3c-218">(The ClientScriptManager class is covered later in this module.)</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="63e3c-219">イベントの検証を有効にする</span><span class="sxs-lookup"><span data-stu-id="63e3c-219">EnableEventValidation</span></span>

<span data-ttu-id="63e3c-220">このプロパティは、イベントの検証がポストバック イベントとコールバック イベントに対して有効かどうかを制御します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-220">This property controls whether or not event validation is enabled for postback and callback events.</span></span> <span data-ttu-id="63e3c-221">有効にすると、ポストバックイベントまたはコールバックイベントの引数が検証され、イベントを最初にレンダリングしたサーバー コントロールから発生していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-221">When enabled, arguments to postback or callback events are verified to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="63e3c-222">テーマを有効にする</span><span class="sxs-lookup"><span data-stu-id="63e3c-222">EnableTheming</span></span>

<span data-ttu-id="63e3c-223">このプロパティは、2.0 のテーマ ASP.NETをページに適用するかどうかを指定するブール値を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-223">This property gets or sets a Boolean that specifies whether or not an ASP.NET 2.0 theme applies to the page.</span></span>

## <a name="form"></a><span data-ttu-id="63e3c-224">Form</span><span class="sxs-lookup"><span data-stu-id="63e3c-224">Form</span></span>

<span data-ttu-id="63e3c-225">このプロパティは、ASPX ページの HTML フォームを HtmlForm オブジェクトとして返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-225">This property returns the HTML form on the ASPX page as an HtmlForm object.</span></span>

## <a name="header"></a><span data-ttu-id="63e3c-226">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="63e3c-226">Header</span></span>

<span data-ttu-id="63e3c-227">このプロパティは、ページ ヘッダーを含む HtmlHead オブジェクトへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-227">This property returns a reference to an HtmlHead object that contains the page header.</span></span> <span data-ttu-id="63e3c-228">返された HtmlHead オブジェクトを使用して、スタイル シートやメタ タグなどを取得/設定できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-228">You can use the returned HtmlHead object to get/set style sheets, Meta tags, etc.</span></span>

## <a name="idseparator"></a><span data-ttu-id="63e3c-229">イドセパレータ</span><span class="sxs-lookup"><span data-stu-id="63e3c-229">IdSeparator</span></span>

<span data-ttu-id="63e3c-230">この読み取り専用プロパティは、ASP.NETがページ上のコントロールの一意の ID を構築するときに、コントロール識別子を区切るために使用される文字を取得します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-230">This read-only property gets the character that is used to separate control identifiers when ASP.NET is building a unique ID for controls on a page.</span></span> <span data-ttu-id="63e3c-231">コードから直接使用するためのものではありません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-231">It is not intended to be used directly from your code.</span></span>

## <a name="isasync"></a><span data-ttu-id="63e3c-232">IsAsync</span><span class="sxs-lookup"><span data-stu-id="63e3c-232">IsAsync</span></span>

<span data-ttu-id="63e3c-233">このプロパティは、非同期ページを使用できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-233">This property allows for asynchronous pages.</span></span> <span data-ttu-id="63e3c-234">非同期ページについては、このモジュールで後述します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-234">Asynchronous pages are discussed later in this module.</span></span>

## <a name="iscallback"></a><span data-ttu-id="63e3c-235">IsCallback</span><span class="sxs-lookup"><span data-stu-id="63e3c-235">IsCallback</span></span>

<span data-ttu-id="63e3c-236">この読み取り専用プロパティは、ページがコールバックの結果である場合に**true**を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-236">This read-only property returns **true** if the page is the result of a call back.</span></span> <span data-ttu-id="63e3c-237">コールバックについては、このモジュールで後述します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-237">Call backs are discussed later in this module.</span></span>

## <a name="iscrosspagepostback"></a><span data-ttu-id="63e3c-238">ページポストバック</span><span class="sxs-lookup"><span data-stu-id="63e3c-238">IsCrossPagePostBack</span></span>

<span data-ttu-id="63e3c-239">この読み取り専用プロパティは、ページがページ間ポストバックの一部である場合は**true**を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-239">This read-only property returns **true** if the page is part of a cross-page postback.</span></span> <span data-ttu-id="63e3c-240">ページ間のポストバックについては、このモジュールの後半で説明します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-240">Cross-page postbacks are covered later in this module.</span></span>

## <a name="items"></a><span data-ttu-id="63e3c-241">アイテム</span><span class="sxs-lookup"><span data-stu-id="63e3c-241">Items</span></span>

<span data-ttu-id="63e3c-242">ページ コンテキストに格納されているすべてのオブジェクトを含む IDictionary インスタンスへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-242">Returns a reference to an IDictionary instance that contains all objects stored in the pages context.</span></span> <span data-ttu-id="63e3c-243">この IDictionary オブジェクトに項目を追加すると、コンテキストの有効期間を通じて使用できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-243">You can add items to this IDictionary object and they will be available to you throughout the lifetime of the context.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="63e3c-244">ポストバックを維持します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-244">MaintainScrollPositionOnPostBack</span></span>

<span data-ttu-id="63e3c-245">このプロパティは、ポストバックASP.NET発生した後に、ブラウザーでページのスクロール位置を維持する JavaScript を出力するかどうかを制御します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-245">This property controls whether or not ASP.NET emits JavaScript that maintains the pages scroll position in the browser after a postback occurs.</span></span> <span data-ttu-id="63e3c-246">(このプロパティの詳細については、このモジュールで前述しました)。</span><span class="sxs-lookup"><span data-stu-id="63e3c-246">(Details of this property were discussed earlier in this module.)</span></span>

## <a name="master"></a><span data-ttu-id="63e3c-247">Master</span><span class="sxs-lookup"><span data-stu-id="63e3c-247">Master</span></span>

<span data-ttu-id="63e3c-248">この読み取り専用プロパティは、マスター ページが適用されているページの MasterPage インスタンスへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-248">This read-only property returns a reference to the MasterPage instance for a page to which a master page has been applied.</span></span>

## <a name="masterpagefile"></a><span data-ttu-id="63e3c-249">マスターページファイル</span><span class="sxs-lookup"><span data-stu-id="63e3c-249">MasterPageFile</span></span>

<span data-ttu-id="63e3c-250">ページのマスター ページのファイル名を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-250">Gets or sets the master page filename for the page.</span></span> <span data-ttu-id="63e3c-251">このプロパティは、PreInit メソッドでのみ設定できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-251">This property can only be set in the PreInit method.</span></span>

## <a name="maxpagestatefieldlength"></a><span data-ttu-id="63e3c-252">フィールドの長さを変更します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-252">MaxPageStateFieldLength</span></span>

<span data-ttu-id="63e3c-253">このプロパティは、ページの状態の最大長をバイト単位で取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-253">This property gets or sets the maximum length for the pages state in bytes.</span></span> <span data-ttu-id="63e3c-254">プロパティに正の数を設定すると、ページのビューステートは複数の隠しフィールドに分割され、指定したバイト数を超えないようにします。</span><span class="sxs-lookup"><span data-stu-id="63e3c-254">If the property is set to a positive number, the pages view state will be broken up into multiple hidden fields so that it doesnt exceed the number of bytes specified.</span></span> <span data-ttu-id="63e3c-255">プロパティが負の数の場合、ビュー ステートはチャンクに分割されません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-255">If the property is a negative number, the view state will not be broken into chunks.</span></span>

## <a name="pageadapter"></a><span data-ttu-id="63e3c-256">ページアダプター</span><span class="sxs-lookup"><span data-stu-id="63e3c-256">PageAdapter</span></span>

<span data-ttu-id="63e3c-257">要求元のブラウザーのページを変更する PageAdapter オブジェクトへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-257">Returns a reference to the PageAdapter object that modifies the page for the requesting browser.</span></span>

## <a name="previouspage"></a><span data-ttu-id="63e3c-258">Previouspage</span><span class="sxs-lookup"><span data-stu-id="63e3c-258">PreviousPage</span></span>

<span data-ttu-id="63e3c-259">Server.Transfer またはページ間ポストバックの場合は、前のページへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-259">Returns a reference to the previous page in cases of a Server.Transfer or a cross-page postback.</span></span>

## <a name="skinid"></a><span data-ttu-id="63e3c-260">Skinid</span><span class="sxs-lookup"><span data-stu-id="63e3c-260">SkinID</span></span>

<span data-ttu-id="63e3c-261">ページに適用するASP.NET 2.0 スキンを指定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-261">Specifies the ASP.NET 2.0 skin to apply to the page.</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="63e3c-262">スタイルシートテーマ</span><span class="sxs-lookup"><span data-stu-id="63e3c-262">StyleSheetTheme</span></span>

<span data-ttu-id="63e3c-263">このプロパティは、ページに適用されるスタイル シートを取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-263">This property gets or sets the style sheet that is applied to a page.</span></span>

## <a name="templatecontrol"></a><span data-ttu-id="63e3c-264">テンプレートコントロール</span><span class="sxs-lookup"><span data-stu-id="63e3c-264">TemplateControl</span></span>

<span data-ttu-id="63e3c-265">ページのコントロールを含むコントロールへの参照を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-265">Returns a reference to the containing control for the page.</span></span>

## <a name="theme"></a><span data-ttu-id="63e3c-266">テーマ</span><span class="sxs-lookup"><span data-stu-id="63e3c-266">Theme</span></span>

<span data-ttu-id="63e3c-267">ページに適用されるASP.NET 2.0 テーマの名前を取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-267">Gets or sets the name of the ASP.NET 2.0 theme applied to the page.</span></span> <span data-ttu-id="63e3c-268">この値は PreInit メソッドの前に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-268">This value must be set prior to the PreInit method.</span></span>

## <a name="title"></a><span data-ttu-id="63e3c-269">タイトル</span><span class="sxs-lookup"><span data-stu-id="63e3c-269">Title</span></span>

<span data-ttu-id="63e3c-270">このプロパティは、ページ ヘッダーから取得されたページのタイトルを取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-270">This property gets or sets the title for the page as obtained from the pages header.</span></span>

## <a name="viewstateencryptionmode"></a><span data-ttu-id="63e3c-271">を使用します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-271">ViewStateEncryptionMode</span></span>

<span data-ttu-id="63e3c-272">ページのビューステート暗号化モードを取得または設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-272">Gets or sets the ViewStateEncryptionMode of the page.</span></span> <span data-ttu-id="63e3c-273">このモジュールの前のこのプロパティの詳細な説明を参照してください。</span><span class="sxs-lookup"><span data-stu-id="63e3c-273">See a detailed discussion of this property earlier in this module.</span></span>

## <a name="new-protected-properties-of-the-page-class"></a><span data-ttu-id="63e3c-274">ページ クラスの新しい保護されたプロパティ</span><span class="sxs-lookup"><span data-stu-id="63e3c-274">New Protected Properties of the Page Class</span></span>

<span data-ttu-id="63e3c-275">次に示す新しい保護された Page クラスの ASP.NET 2.0.</span><span class="sxs-lookup"><span data-stu-id="63e3c-275">The following are the new protected properties of the Page class in ASP.NET 2.0.</span></span>

## <a name="adapter"></a><span data-ttu-id="63e3c-276">アダプター</span><span class="sxs-lookup"><span data-stu-id="63e3c-276">Adapter</span></span>

<span data-ttu-id="63e3c-277">要求したデバイス上でページを表示する ControlAdapter への参照を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-277">Returns a reference to the ControlAdapter that renders the page on the device that requested it.</span></span>

## <a name="asyncmode"></a><span data-ttu-id="63e3c-278">非同期モード</span><span class="sxs-lookup"><span data-stu-id="63e3c-278">AsyncMode</span></span>

<span data-ttu-id="63e3c-279">このプロパティは、ページが非同期で処理されるかどうかを示します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-279">This property indicates whether or not the page is processed asynchronously.</span></span> <span data-ttu-id="63e3c-280">これは、コード内で直接使用するものではなく、ランタイムで使用することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-280">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="clientidseparator"></a><span data-ttu-id="63e3c-281">クライアント ID 区切り記号</span><span class="sxs-lookup"><span data-stu-id="63e3c-281">ClientIDSeparator</span></span>

<span data-ttu-id="63e3c-282">このプロパティは、コントロールの一意のクライアント ID を作成するときに区切り文字として使用される文字を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-282">This property returns the character used as a separator when creating unique client IDs for controls.</span></span> <span data-ttu-id="63e3c-283">これは、コード内で直接使用するものではなく、ランタイムで使用することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-283">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="pagestatepersister"></a><span data-ttu-id="63e3c-284">ページステートパーシスター</span><span class="sxs-lookup"><span data-stu-id="63e3c-284">PageStatePersister</span></span>

<span data-ttu-id="63e3c-285">このプロパティは、ページの PageStatePersister オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-285">This property returns the PageStatePersister object for the page.</span></span> <span data-ttu-id="63e3c-286">このプロパティは、主にASP.NETコントロール開発者によって使用されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-286">This property is primarily used by ASP.NET control developers.</span></span>

## <a name="uniquefilepathsuffix"></a><span data-ttu-id="63e3c-287">一意のファイルパスサフィックス</span><span class="sxs-lookup"><span data-stu-id="63e3c-287">UniqueFilePathSuffix</span></span>

<span data-ttu-id="63e3c-288">このプロパティは、ブラウザをキャッシュするためのファイル パスに付加される一意のサフィックスを返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-288">This property returns a unique suffix that is appended to the file path for caching browsers.</span></span> <span data-ttu-id="63e3c-289">デフォルト値は\_\_ufps= と 6 桁の数字です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-289">The default value is \_\_ufps= and a 6-digit number.</span></span>

## <a name="new-public-methods-for-the-page-class"></a><span data-ttu-id="63e3c-290">ページ クラスの新しいパブリック メソッド</span><span class="sxs-lookup"><span data-stu-id="63e3c-290">New Public Methods for the Page Class</span></span>

<span data-ttu-id="63e3c-291">次のパブリック メソッドは、ASP.NET 2.0 の Page クラスの新機能です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-291">The following public methods are new to the Page class in ASP.NET 2.0.</span></span>

## <a name="addonprerendercompleteasync"></a><span data-ttu-id="63e3c-292">コンプリーレンダリングコンプリートアシンク</span><span class="sxs-lookup"><span data-stu-id="63e3c-292">AddOnPreRenderCompleteAsync</span></span>

<span data-ttu-id="63e3c-293">このメソッドは、非同期ページ実行のイベント ハンドラー デリゲートを登録します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-293">This method registers event handler delegates for asynchronous page execution.</span></span> <span data-ttu-id="63e3c-294">非同期ページについては、このモジュールで後述します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-294">Asynchronous pages are discussed later in this module.</span></span>

## <a name="applystylesheetskin"></a><span data-ttu-id="63e3c-295">スタイルシートスキンを適用する</span><span class="sxs-lookup"><span data-stu-id="63e3c-295">ApplyStyleSheetSkin</span></span>

<span data-ttu-id="63e3c-296">ページ スタイル シートのプロパティをページに適用します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-296">Applies the properties in a pages style sheet to the page.</span></span>

## <a name="executeregisteredasynctasks"></a><span data-ttu-id="63e3c-297">登録された非同期タスクを実行します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-297">ExecuteRegisteredAsyncTasks</span></span>

<span data-ttu-id="63e3c-298">このメソッドは非同期タスクを使用します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-298">This method beings an asynchronous task.</span></span>

### <a name="getvalidators"></a><span data-ttu-id="63e3c-299">検証ツールを取得する</span><span class="sxs-lookup"><span data-stu-id="63e3c-299">GetValidators</span></span>

<span data-ttu-id="63e3c-300">指定した検証グループの検証コントロールのコレクションを返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-300">Returns a collection of validators for the specified validation group or the default validation group if none is specified.</span></span>

## <a name="registerasynctask"></a><span data-ttu-id="63e3c-301">同期タスクを登録します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-301">RegisterAsyncTask</span></span>

<span data-ttu-id="63e3c-302">このメソッドは、新しい非同期タスクを登録します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-302">This method registers a new async task.</span></span> <span data-ttu-id="63e3c-303">非同期ページについては、このモジュールの後半で説明します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-303">Asynchronous pages are covered later in this module.</span></span>

## <a name="registerrequirescontrolstate"></a><span data-ttu-id="63e3c-304">コントロール状態を登録する</span><span class="sxs-lookup"><span data-stu-id="63e3c-304">RegisterRequiresControlState</span></span>

<span data-ttu-id="63e3c-305">このメソッドは、ASP.NETページ コントロールの状態を永続化する必要があることを通知します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-305">This method tells ASP.NET that the pages control state must be persisted.</span></span>

## <a name="registerrequiresviewstateencryption"></a><span data-ttu-id="63e3c-306">を要求します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-306">RegisterRequiresViewStateEncryption</span></span>

<span data-ttu-id="63e3c-307">このメソッドは、ページの viewstate に暗号化が必要であることをASP.NETに通知します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-307">This method tells ASP.NET that the pages viewstate requires encryption.</span></span>

## <a name="resolveclienturl"></a><span data-ttu-id="63e3c-308">クライアント Url を解決します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-308">ResolveClientUrl</span></span>

<span data-ttu-id="63e3c-309">イメージなどのクライアント要求に使用できる相対 URL を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-309">Returns a relative URL that can be used for client requests for images, etc.</span></span>

## <a name="setfocus"></a><span data-ttu-id="63e3c-310">SetFocus</span><span class="sxs-lookup"><span data-stu-id="63e3c-310">SetFocus</span></span>

<span data-ttu-id="63e3c-311">このメソッドは、ページが最初に読み込まれるときに指定されたコントロールにフォーカスを設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-311">This method will set the focus to the control that is specified when the page is initially loaded.</span></span>

## <a name="unregisterrequirescontrolstate"></a><span data-ttu-id="63e3c-312">登録を解除するコントロール状態を確認します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-312">UnregisterRequiresControlState</span></span>

<span data-ttu-id="63e3c-313">このメソッドは、コントロール状態の永続化を必要としないために渡されたコントロールの登録を解除します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-313">This method will unregister the control that is passed to it as no longer requiring control state persistence.</span></span>

## <a name="changes-to-the-page-lifecycle"></a><span data-ttu-id="63e3c-314">ページのライフサイクルの変更</span><span class="sxs-lookup"><span data-stu-id="63e3c-314">Changes to the Page Lifecycle</span></span>

<span data-ttu-id="63e3c-315">ASP.NET 2.0 のページライフサイクルは劇的に変化していませんが、注意すべき新しい方法がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-315">The page lifecycle in ASP.NET 2.0 hasn't changed dramatically, but there are some new methods that you should be aware of.</span></span> <span data-ttu-id="63e3c-316">ASP.NET 2.0 ページのライフサイクルについて、以下に概説します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-316">The ASP.NET 2.0 page lifecycle is outlined below.</span></span>

## <a name="preinit-new-in-aspnet-20"></a><span data-ttu-id="63e3c-317">プレイニト(ASP.NET 2.0で新しい)</span><span class="sxs-lookup"><span data-stu-id="63e3c-317">PreInit (New in ASP.NET 2.0)</span></span>

<span data-ttu-id="63e3c-318">PreInit イベントは、開発者がアクセスできるライフサイクルの最も初期のステージです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-318">The PreInit event is the earliest stage in the lifecycle that a developer can access.</span></span> <span data-ttu-id="63e3c-319">このイベントを追加すると、プログラムによって、2.0 のテーマ、マスター ページ、ASP.NET 2.0 プロファイルのプロパティへのアクセスなどをプログラムで ASP.NET変更できます。ポストバック状態にある場合は、ライフサイクルのこの時点で Viewstate がまだコントロールに適用されていないということを理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-319">The addition of this event makes it possible to programmatically change ASP.NET 2.0 themes, master pages, access properties for an ASP.NET 2.0 profile, etc. If you are in a postback state, its important to realize that Viewstate has not yet been applied to controls at this point in the lifecycle.</span></span> <span data-ttu-id="63e3c-320">したがって、開発者がこの段階でコントロールのプロパティを変更すると、ページのライフサイクルの後半で上書きされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-320">Therefore, if a developer changes a property of a control at this stage, it will likely be overwritten later in the pages lifecycle.</span></span>

## <a name="init"></a><span data-ttu-id="63e3c-321">Init</span><span class="sxs-lookup"><span data-stu-id="63e3c-321">Init</span></span>

<span data-ttu-id="63e3c-322">Init イベントは、ASP.NET 1.x から変更されていません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-322">The Init event has not changed from ASP.NET 1.x.</span></span> <span data-ttu-id="63e3c-323">ページ上のコントロールのプロパティを読み取りまたは初期化する場所です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-323">This is where you would want to read or initialize properties of controls on your page.</span></span> <span data-ttu-id="63e3c-324">この段階では、マスターページ、テーマなどが既にページに適用されています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-324">At this stage, master pages, themes, etc. are already applied to the page.</span></span>

## <a name="initcomplete-new-in-20"></a><span data-ttu-id="63e3c-325">イニトコンプリート(2.0で新しい)</span><span class="sxs-lookup"><span data-stu-id="63e3c-325">InitComplete (New in 2.0)</span></span>

<span data-ttu-id="63e3c-326">初期化ステージの最後に InitComplete イベントが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-326">The InitComplete event is called at the end of the pages initialization stage.</span></span> <span data-ttu-id="63e3c-327">ライフサイクルのこの時点で、ページ上のコントロールにアクセスできますが、その状態はまだ設定されていません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-327">At this point in the lifecycle, you can access controls on the page, but their state has not yet been populated.</span></span>

## <a name="preload-new-in-20"></a><span data-ttu-id="63e3c-328">プリロード (2.0 での新機能)</span><span class="sxs-lookup"><span data-stu-id="63e3c-328">PreLoad (New in 2.0)</span></span>

<span data-ttu-id="63e3c-329">このイベントは、すべてのポストバック データが適用された後、ページ\_読み込みの直前に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-329">This event is called after all postback data has been applied and just prior to Page\_Load.</span></span>

## <a name="load"></a><span data-ttu-id="63e3c-330">[読み込み]</span><span class="sxs-lookup"><span data-stu-id="63e3c-330">Load</span></span>

<span data-ttu-id="63e3c-331">Load イベントは、ASP.NET 1.x から変更されていません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-331">The Load event has not changed from ASP.NET 1.x.</span></span>

## <a name="loadcomplete-new-in-20"></a><span data-ttu-id="63e3c-332">ロード完了(2.0 での新機能)</span><span class="sxs-lookup"><span data-stu-id="63e3c-332">LoadComplete (New in 2.0)</span></span>

<span data-ttu-id="63e3c-333">LoadComplete イベントは、ページ読み込みステージの最後のイベントです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-333">The LoadComplete event is the last event in the pages load stage.</span></span> <span data-ttu-id="63e3c-334">この段階では、すべてのポストバックデータとビューステートデータがページに適用されています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-334">At this stage, all postback and viewstate data has been applied to the page.</span></span>

## <a name="prerender"></a><span data-ttu-id="63e3c-335">Prerender</span><span class="sxs-lookup"><span data-stu-id="63e3c-335">PreRender</span></span>

<span data-ttu-id="63e3c-336">動的にページに追加されるコントロールに対してビューステートを適切に維持する場合は、PreRender イベントが最後に追加されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-336">If you would like for viewstate to be properly maintained for controls that are added to the page dynamically, the PreRender event is the last opportunity to add them.</span></span>

## <a name="prerendercomplete-new-in-20"></a><span data-ttu-id="63e3c-337">プレレンダリングコンプリート(2.0で新しい)</span><span class="sxs-lookup"><span data-stu-id="63e3c-337">PreRenderComplete (New in 2.0)</span></span>

<span data-ttu-id="63e3c-338">PreRenderComplete ステージで、すべてのコントロールがページに追加され、ページをレンダリングする準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-338">At the PreRenderComplete stage, all controls have been added to the page and the page is ready to be rendered.</span></span> <span data-ttu-id="63e3c-339">PreRenderComplete イベントは、ページのビューステートが保存される前に発生する最後のイベントです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-339">The PreRenderComplete event is the last event raised before the pages viewstate is saved.</span></span>

## <a name="savestatecomplete-new-in-20"></a><span data-ttu-id="63e3c-340">セーブステートコンプリート(2.0で新規)</span><span class="sxs-lookup"><span data-stu-id="63e3c-340">SaveStateComplete (New in 2.0)</span></span>

<span data-ttu-id="63e3c-341">SaveStateComplete イベントは、すべてのページのビューステートとコントロールの状態が保存された直後に呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-341">The SaveStateComplete event is called immediately after all page viewstate and control state has been saved.</span></span> <span data-ttu-id="63e3c-342">これは、ページが実際にブラウザーにレンダリングされる前の最後のイベントです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-342">This is the last event before the page is actually rendered to the browser.</span></span>

## <a name="render"></a><span data-ttu-id="63e3c-343">レンダー</span><span class="sxs-lookup"><span data-stu-id="63e3c-343">Render</span></span>

<span data-ttu-id="63e3c-344">1.x 以降、Render メソッドは変更ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="63e3c-344">The Render method has not changed since ASP.NET 1.x.</span></span> <span data-ttu-id="63e3c-345">ここで、HtmlTextWriter が初期化され、ページがブラウザーにレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-345">This is where the HtmlTextWriter is initialized and the page is rendered to the browser.</span></span>

## <a name="cross-page-postback-in-aspnet-20"></a><span data-ttu-id="63e3c-346">ASP.NET 2.0 でのページ間のポストバック</span><span class="sxs-lookup"><span data-stu-id="63e3c-346">Cross-Page Postback in ASP.NET 2.0</span></span>

<span data-ttu-id="63e3c-347">ASP.NET 1.x では、ポストバックが同じページにポストする必要がありました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-347">In ASP.NET 1.x, postbacks were required to post to the same page.</span></span> <span data-ttu-id="63e3c-348">ページ間のポストバックは許可されませんでした。</span><span class="sxs-lookup"><span data-stu-id="63e3c-348">Cross-page postbacks were not allowed.</span></span> <span data-ttu-id="63e3c-349">ASP.NET 2.0 は、IButtonControl インターフェイスを介して別のページにポストバックする機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-349">ASP.NET 2.0 adds the ability to post back to a different page via the IButtonControl interface.</span></span> <span data-ttu-id="63e3c-350">新しい IButtonControl インターフェイス (ボタン、リンク ボタン、およびサード パーティのカスタム コントロールに加えて、イメージ ボタン) を実装するすべてのコントロールは、PostBackUrl 属性を使用して、この新しい機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-350">Any control that implements the new IButtonControl interface (Button, LinkButton, and ImageButton in addition to third-party custom controls) can take advantage of this new functionality via the use of the PostBackUrl attribute.</span></span> <span data-ttu-id="63e3c-351">次のコードは、2 番目のページにポストバックする Button コントロールを示しています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-351">The following code shows a Button control that posts back to a second page.</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

<span data-ttu-id="63e3c-352">ページがポストバックされると、ポストバックを開始する Page には、2 ページ目の PreviousPage プロパティを使用してアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-352">When the page is posted back, the Page that initiates the postback is accessible via the PreviousPage property on the second page.</span></span> <span data-ttu-id="63e3c-353">この機能は、コントロールが別のページに\_ポストバックしたときに 2.0 ASP.NETページにレンダリングされる新しい WebForm DoPostBackWithOptions クライアント側の関数を介して実装されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-353">This functionality is implemented via the new WebForm\_DoPostBackWithOptions client-side function that ASP.NET 2.0 renders to the page when a control posts back to a different page.</span></span> <span data-ttu-id="63e3c-354">この JavaScript 関数は、クライアントにスクリプトを出力する新しい WebResource.axd ハンドラーによって提供されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-354">This JavaScript function is provided by the new WebResource.axd handler which emits script to the client.</span></span>

<span data-ttu-id="63e3c-355">以下のビデオは、ページ間のポストバックのチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-355">The video below is a walkthrough of a cross-page postback.</span></span>

![](the-asp-net-2-0-page-model/_static/image2.png)

[<span data-ttu-id="63e3c-356">フルスクリーンビデオを開く</span><span class="sxs-lookup"><span data-stu-id="63e3c-356">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a><span data-ttu-id="63e3c-357">ページ間ポストバックの詳細</span><span class="sxs-lookup"><span data-stu-id="63e3c-357">More Details on Cross-Page Postbacks</span></span>

### <a name="viewstate"></a><span data-ttu-id="63e3c-358">Viewstate</span><span class="sxs-lookup"><span data-stu-id="63e3c-358">Viewstate</span></span>

<span data-ttu-id="63e3c-359">ページ間ポストバック シナリオの最初のページから viewstate に何が起こるかについて、既に自問している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-359">You may have asked yourself already about what happens to the viewstate from the first page in a cross-page postback scenario.</span></span> <span data-ttu-id="63e3c-360">結局のところ、IPostBackDataHandler を実装しないコントロールはビューステートを介してその状態を保持するため、ページ間ポストバックの 2 ページ目でそのコントロールのプロパティにアクセスするには、ページのビューステートにアクセスする必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-360">After all, any control that does not implement IPostBackDataHandler will persist its state via viewstate, so to have access to the properties of that control on the second page of a cross-page postback, you must have access to the viewstate for the page.</span></span> <span data-ttu-id="63e3c-361">ASP.NET 2.0 は PREVIOUSPAGE という 2\_\_番目のページの新しい隠しフィールドを使用して、このシナリオを処理します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-361">ASP.NET 2.0 takes care of this scenario using a new hidden field in the second page called \_\_PREVIOUSPAGE.</span></span> <span data-ttu-id="63e3c-362">PREVIOUSPAGE\_\_フォーム フィールドには、最初のページのビューステートが含まれているため、2 番目のページのすべてのコントロールのプロパティにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-362">The \_\_PREVIOUSPAGE form field contains the viewstate for the first page so that you can have access to the properties of all controls in the second page.</span></span>

### <a name="circumventing-findcontrol"></a><span data-ttu-id="63e3c-363">検索コントロールの回避</span><span class="sxs-lookup"><span data-stu-id="63e3c-363">Circumventing FindControl</span></span>

<span data-ttu-id="63e3c-364">クロスページ ポストバックのビデオ チュートリアルでは、最初のページの TextBox コントロールへの参照を取得するのには FindControl メソッドを使用しました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-364">In the video walkthrough of a cross-page postback, I used the FindControl method to get a reference to the TextBox control on the first page.</span></span> <span data-ttu-id="63e3c-365">このメソッドは、この目的のためにうまく機能しますが、FindControl は高価であり、追加のコードを記述する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-365">That method works well for that purpose, but FindControl is expensive and it requires writing additional code.</span></span> <span data-ttu-id="63e3c-366">幸いにも、ASP.NET 2.0 では、この目的のために FindControl の代わりとなるものが用意されています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-366">Fortunately, ASP.NET 2.0 provides an alternative to FindControl for this purpose that will work in many scenarios.</span></span> <span data-ttu-id="63e3c-367">PreviousPageType ディレクティブを使用すると、TypeName 属性または VirtualPath 属性を使用して、前のページへの厳密に型指定された参照を持つことができます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-367">The PreviousPageType directive allows you to have a strongly-typed reference to the previous page by using either the TypeName or the VirtualPath attribute.</span></span> <span data-ttu-id="63e3c-368">TypeName 属性では、前のページの種類を指定することができますが、VirtualPath 属性を使用すると、仮想パスを使用して前のページを参照できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-368">The TypeName attribute allows you to specify the type of the previous page while the VirtualPath attribute allows you to refer to the previous page using a virtual path.</span></span> <span data-ttu-id="63e3c-369">PreviousPageType ディレクティブを設定した後、パブリック プロパティを使用してアクセスを許可するコントロールなどを公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-369">After you've set the PreviousPageType directive, you must then expose the controls, etc. to which you want to allow access using public properties.</span></span>

## <a name="lab-1-cross-page-postback"></a><span data-ttu-id="63e3c-370">ラボ 1 クロスページ ポストバック</span><span class="sxs-lookup"><span data-stu-id="63e3c-370">Lab 1 Cross-Page Postback</span></span>

<span data-ttu-id="63e3c-371">このラボでは、ASP.NET 2.0 の新しいページ間ポストバック機能を使用するアプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-371">In this lab, you will create an application that uses the new cross-page postback functionality of ASP.NET 2.0.</span></span>

1. <span data-ttu-id="63e3c-372">Visual Studio 2005 を開き、新しいASP.NET Web サイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-372">Open Visual Studio 2005 and create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="63e3c-373">page2.aspx という名前の新しい Web フォームを追加します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-373">Add a new Webform called page2.aspx.</span></span>
3. <span data-ttu-id="63e3c-374">デザイン ビューで Default.aspx を開き、ボタン コントロールと TextBox コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-374">Open the Default.aspx in Design view and add a Button control and a TextBox control.</span></span> 

    1. <span data-ttu-id="63e3c-375">ボタン コントロールに**送信ボタン**の ID を与え、テキスト ボックス コントロールに**ユーザー名**の ID を与えます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-375">Give the Button control an ID of **SubmitButton** and the TextBox control an ID of **UserName**.</span></span>
    2. <span data-ttu-id="63e3c-376">ボタンの PostBackUrl プロパティを page2.aspx に設定します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-376">Set the PostBackUrl property of the Button to page2.aspx.</span></span>
4. <span data-ttu-id="63e3c-377">ソース ビューで page2.aspx を開きます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-377">Open page2.aspx in Source view.</span></span>
5. <span data-ttu-id="63e3c-378">次に示すように、 @ PreviousPageType ディレクティブを追加します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-378">Add a @ PreviousPageType directive as shown below:</span></span>
6. <span data-ttu-id="63e3c-379">page2.aspx の分離\_コードのページ読み込みに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-379">Add the following code to the Page\_Load of page2.aspx's code-behind:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. <span data-ttu-id="63e3c-380">[ビルド] メニューの [ビルド] をクリックして、プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="63e3c-380">Build the project by clicking on Build on the Build menu.</span></span>
8. <span data-ttu-id="63e3c-381">Default.aspx の分離コードに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-381">Add the following code to the code-behind for Default.aspx:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. <span data-ttu-id="63e3c-382">page2.aspx のページ\_読み込みを次のように変更します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-382">Change the Page\_Load in page2.aspx to the following:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. <span data-ttu-id="63e3c-383">プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="63e3c-383">Build the project.</span></span>
11. <span data-ttu-id="63e3c-384">プロジェクトを実行します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-384">Run the project.</span></span>
12. <span data-ttu-id="63e3c-385">テキスト ボックスに自分の名前を入力し、ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="63e3c-385">Enter your name in the TextBox and click the button.</span></span>
13. <span data-ttu-id="63e3c-386">結果は何ですか?</span><span class="sxs-lookup"><span data-stu-id="63e3c-386">What is the result?</span></span>

## <a name="asynchronous-pages-in-aspnet-20"></a><span data-ttu-id="63e3c-387">ASP.NET 2.0 の非同期ページ</span><span class="sxs-lookup"><span data-stu-id="63e3c-387">Asynchronous Pages in ASP.NET 2.0</span></span>

<span data-ttu-id="63e3c-388">ASP.NETの競合の問題の多くは、外部呼び出し (Web サービスやデータベース呼び出しなど) の遅延、ファイル IO の待ち時間などによって発生します。ASP.NETアプリケーションに対して要求が行われると、ASP.NETはその要求を処理するためにワーカー スレッドの 1 つを使用します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-388">Many contention problems in ASP.NET are caused by latency of external calls (such as Web service or database calls), file IO latency, etc. When a request is made against an ASP.NET application, ASP.NET uses one of its worker threads to service that request.</span></span> <span data-ttu-id="63e3c-389">要求が完了し、応答が送信されるまで、その要求はそのスレッドを所有します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-389">That request owns that thread until the request is complete and the response has been sent.</span></span> <span data-ttu-id="63e3c-390">ASP.NET 2.0 では、ページを非同期に実行する機能を追加することで、このような種類の問題に関する待ち時間の問題を解決します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-390">ASP.NET 2.0 seeks to resolve latency issues with these types of issues by adding the capability to execute pages asynchronously.</span></span> <span data-ttu-id="63e3c-391">つまり、ワーカー スレッドは要求を開始し、別のスレッドに追加の実行を渡すことができるので、使用可能なスレッド プールにすばやく戻ります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-391">That means that a worker thread can start the request and then hand off additional execution to another thread, thereby returning to the available thread pool quickly.</span></span> <span data-ttu-id="63e3c-392">ファイル IO、データベース呼び出しなどが完了すると、スレッド プールから新しいスレッドを取得して要求を完了します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-392">When the file IO, database call, etc. has completed, a new thread is obtained from the thread pool to finish the request.</span></span>

<span data-ttu-id="63e3c-393">ページを非同期に実行する最初の手順は、次のように page ディレクティブの**Async**属性を設定することです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-393">The first step in making a page execute asynchronously is to set the **Async** attribute of the page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

<span data-ttu-id="63e3c-394">この属性は、ページの IHttpAsyncHandler を実装するASP.NETを指示します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-394">This attribute tells ASP.NET to implement the IHttpAsyncHandler for the page.</span></span>

<span data-ttu-id="63e3c-395">次の手順では、ページのライフサイクル内の 1 つの時点で、PreRender の前に AddOnPreRenderCompleteAsync メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-395">The next step is to call the AddOnPreRenderCompleteAsync method at a point in the lifecycle of the page prior to PreRender.</span></span> <span data-ttu-id="63e3c-396">(このメソッドは通常、ページの\_読み込みで呼び出されます)。メソッドは 2 つのパラメーターを受け取ります。を開始イベント ハンドラーとエンドイベント ハンドラー。</span><span class="sxs-lookup"><span data-stu-id="63e3c-396">(This method is typically called in Page\_Load.) The AddOnPreRenderCompleteAsync method takes two parameters; a BeginEventHandler and an EndEventHandler.</span></span> <span data-ttu-id="63e3c-397">メソッドを返す、 IAsyncResult をパラメーターとして渡します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-397">The BeginEventHandler returns an IAsyncResult which is then passed as a parameter to the EndEventHandler.</span></span>

<span data-ttu-id="63e3c-398">以下のビデオは、非同期ページ要求のチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-398">The video below is a walkthrough of an asynchronous page request.</span></span>

![](the-asp-net-2-0-page-model/_static/image3.png)

[<span data-ttu-id="63e3c-399">フルスクリーンビデオを開く</span><span class="sxs-lookup"><span data-stu-id="63e3c-399">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> <span data-ttu-id="63e3c-400">非同期ページは、EndEventHandler が完了するまでブラウザーにレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-400">An async page does not render to the browser until the EndEventHandler has completed.</span></span> <span data-ttu-id="63e3c-401">間違いなく、一部の開発者は非同期要求を非同期コールバックに似ていると考えます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-401">No doubt but that some developers will think of async requests as being similar to async callbacks.</span></span> <span data-ttu-id="63e3c-402">彼らがそうではないことを認識することが重要です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-402">It's important to realize that they are not.</span></span> <span data-ttu-id="63e3c-403">非同期要求の利点は、最初のワーカー スレッドをスレッド プールに返して新しい要求を処理できるため、IO バインドによる競合が軽減されることです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-403">The benefit to asynchronous requests is that the first worker thread can be returned to the thread pool to service new requests, thereby reducing contention due to being IO bound, etc.</span></span>

## <a name="script-callbacks-in-aspnet-20"></a><span data-ttu-id="63e3c-404">ASP.NET 2.0 のスクリプト コールバック</span><span class="sxs-lookup"><span data-stu-id="63e3c-404">Script Callbacks in ASP.NET 2.0</span></span>

<span data-ttu-id="63e3c-405">Web 開発者は、コールバックに関連付けられたちらつきを防ぐ方法を常に探してきました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-405">Web developers have always looked for ways to prevent the flickering associated with a callback.</span></span> <span data-ttu-id="63e3c-406">ASP.NET 1.x では、SmartNavigation はちらつきを避ける最も一般的な方法でしたが、クライアントでの実装が複雑なため、SmartNavigation が一部の開発者に問題を引き起こしました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-406">In ASP.NET 1.x, SmartNavigation was the most common method for avoiding flickering, but SmartNavigation caused problems for some developers because of the complexity of its implementation on the client.</span></span> <span data-ttu-id="63e3c-407">ASP.NET 2.0 は、スクリプト コールバックでこの問題を解決します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-407">ASP.NET 2.0 addresses this issue with script callbacks.</span></span> <span data-ttu-id="63e3c-408">スクリプト コールバックは、XmlHttp を使用して、JavaScript を介して Web サーバーに対して要求を行います。</span><span class="sxs-lookup"><span data-stu-id="63e3c-408">Script callbacks utilize XMLHttp to make requests against the Web server via JavaScript.</span></span> <span data-ttu-id="63e3c-409">XMLHttp 要求は、ブラウザーの DOM を介して操作できる XML データを返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-409">The XMLHttp request returns XML data that can then be manipulated via the browser's DOM.</span></span> <span data-ttu-id="63e3c-410">新しい WebResource.axd ハンドラーによって、ユーザーから XMLHttp コードが非表示になります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-410">XMLHttp code is hidden from the user by the new WebResource.axd handler.</span></span>

<span data-ttu-id="63e3c-411">スクリプト コールバックを ASP.NET 2.0 で設定するには、いくつかの手順が必要です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-411">There are several steps that are necessary in order to configure a script callback in ASP.NET 2.0.</span></span>

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a><span data-ttu-id="63e3c-412">ステップ 1 : インターフェイスを実装します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-412">Step 1 : Implement the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="63e3c-413">ASP.NETがページをスクリプト コールバックに参加していると認識するには、ICallbackEventHandler インターフェイスを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-413">In order for ASP.NET to recognize your page as participating in a script callback, you must implement the ICallbackEventHandler interface.</span></span> <span data-ttu-id="63e3c-414">これをコードビハインド ファイルで次のように行うことができます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-414">You can do this in your code-behind file like so:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

<span data-ttu-id="63e3c-415">@ Implements ディレクティブを使用して、次のようにすることもできます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-415">You can also do this using the @ Implements directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

<span data-ttu-id="63e3c-416">通常、インラインASP.NETコードを使用する場合は、 @ Implements ディレクティブを使用します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-416">You would typically use the @ Implements directive when using inline ASP.NET code.</span></span>

## <a name="step-2--call-getcallbackeventreference"></a><span data-ttu-id="63e3c-417">ステップ 2 : 呼び出しを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-417">Step 2 : Call GetCallbackEventReference</span></span>

<span data-ttu-id="63e3c-418">前述のように、XMLHttp 呼び出しは WebResource.axd ハンドラーにカプセル化されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-418">As mentioned previously, the XMLHttp call is encapsulated in the WebResource.axd handler.</span></span> <span data-ttu-id="63e3c-419">ページがレンダリングされると、ASP.NETは WebResource.axd\_によって提供されるクライアント スクリプトである WebForm DoCallback への呼び出しを追加します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-419">When your page is rendered, ASP.NET will add a call to WebForm\_DoCallback, a client script that is provided by WebResource.axd.</span></span> <span data-ttu-id="63e3c-420">\_関数は、コールバックの doPostBack\_\_関数を置き換えます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-420">The WebForm\_DoCallback function replaces the \_\_doPostBack function for a callback.</span></span> <span data-ttu-id="63e3c-421">doPostBack は\_\_、プログラムによってページ上のフォームを送信します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-421">Remember that \_\_doPostBack programmatically submits the form on the page.</span></span> <span data-ttu-id="63e3c-422">コールバック シナリオでは、ポストバックを防ぐ必要があるため\_\_、doPostBack では十分ではありません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-422">In a callback scenario, you want to prevent a postback, so \_\_doPostBack will not suffice.</span></span>

> [!NOTE]
> <span data-ttu-id="63e3c-423">\_\_doPostBack は、クライアント スクリプト コールバック シナリオでページにレンダリングされます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-423">\_\_doPostBack is still rendered to the page in a client script callback scenario.</span></span> <span data-ttu-id="63e3c-424">ただし、コールバックには使用されません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-424">However, it's not used for the callback.</span></span>

<span data-ttu-id="63e3c-425">Web フォーム\_の DoCallback クライアント側関数の引数は、通常ページ\_の読み込みで呼び出されるサーバー側関数 GetCallbackEventReference を介して提供されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-425">The arguments for the WebForm\_DoCallback client-side function are provided via the server-side function GetCallbackEventReference which would normally be called in Page\_Load.</span></span> <span data-ttu-id="63e3c-426">一般的な呼び出しは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-426">A typical call to GetCallbackEventReference might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="63e3c-427">この場合、cm はクライアントスクリプト マネージャーのインスタンスです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-427">In this case, cm is an instance of ClientScriptManager.</span></span> <span data-ttu-id="63e3c-428">このモジュールでは、後ほどクラスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-428">The ClientScriptManager class will be covered later in this module.</span></span>

<span data-ttu-id="63e3c-429">いくつかのオーバーロードされたバージョンがあります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-429">There are several overloaded versions of GetCallbackEventReference.</span></span> <span data-ttu-id="63e3c-430">この場合、引数は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-430">In this case, the arguments are as follows:</span></span>

`this`

<span data-ttu-id="63e3c-431">呼び出されているコントロールへの参照。</span><span class="sxs-lookup"><span data-stu-id="63e3c-431">A reference to the control where GetCallbackEventReference is being called.</span></span> <span data-ttu-id="63e3c-432">この場合、ページ自体です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-432">In this case, it's the page itself.</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

<span data-ttu-id="63e3c-433">クライアント側のコードからサーバー側のイベントに渡される文字列引数。</span><span class="sxs-lookup"><span data-stu-id="63e3c-433">A string argument that will be passed from the client-side code to the server-side event.</span></span> <span data-ttu-id="63e3c-434">この場合、DdlCompany と呼ばれるドロップダウンの値を渡します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-434">In this case, Im passing the value of a dropdown called ddlCompany.</span></span>

`ShowCompanyName`

<span data-ttu-id="63e3c-435">サーバー側のコールバック イベントから戻り値 (文字列) を受け取るクライアント側関数の名前。</span><span class="sxs-lookup"><span data-stu-id="63e3c-435">The name of the client-side function that will accept the return value (as string) from the server-side callback event.</span></span> <span data-ttu-id="63e3c-436">この関数は、サーバー側のコールバックが成功した場合にのみ呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-436">This function will only be called when the server-side callback is successful.</span></span> <span data-ttu-id="63e3c-437">したがって、堅牢性のために、通常は、エラーが発生した場合に実行するクライアント側関数の名前を指定する追加の文字列引数を受け取る、オーバーロードされたバージョンの GetCallbackEventReference を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="63e3c-437">Therefore, for the sake of robustness, it is generally recommended to use the overloaded version of GetCallbackEventReference that takes an additional string argument specifying the name of a client-side function to execute in the event of an error.</span></span>

`null`

<span data-ttu-id="63e3c-438">サーバーへのコールバックの前に開始したクライアント側の関数を表す文字列。</span><span class="sxs-lookup"><span data-stu-id="63e3c-438">A string representing a client-side function that it initiated before the callback to the server.</span></span> <span data-ttu-id="63e3c-439">この場合、そのようなスクリプトは存在しませんので、引数は null です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-439">In this case, there is no such script, so the argument is null.</span></span>

`true`

<span data-ttu-id="63e3c-440">コールバックを非同期に実行するかどうかを指定するブール値。</span><span class="sxs-lookup"><span data-stu-id="63e3c-440">A Boolean specifying whether or not to conduct the callback asynchronously.</span></span>

<span data-ttu-id="63e3c-441">クライアント上の Web\_フォーム DoCallback の呼び出しは、これらの引数を渡します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-441">The call to WebForm\_DoCallback on the client will pass these arguments.</span></span> <span data-ttu-id="63e3c-442">したがって、このページがクライアントで表示されるとき、そのコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-442">Therefore, when this page is rendered on the client, that code will look like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

<span data-ttu-id="63e3c-443">クライアント上の関数のシグネチャが少し異なっていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="63e3c-443">Notice that the signature of the function on the client is a bit different.</span></span> <span data-ttu-id="63e3c-444">クライアント側の関数は、5 つの文字列とブール値を渡します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-444">The client-side function passes 5 strings and a Boolean.</span></span> <span data-ttu-id="63e3c-445">追加の文字列 (上記の例では null) には、サーバー側のコールバックからのエラーを処理するクライアント側関数が含まれています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-445">The additional string (which is null in the above example) contains the client-side function that will handle any errors from the server-side callback.</span></span>

## <a name="step-3--hook-the-client-side-control-event"></a><span data-ttu-id="63e3c-446">手順 3 : クライアント側コントロール イベントをフックする</span><span class="sxs-lookup"><span data-stu-id="63e3c-446">Step 3 : Hook the Client-Side Control Event</span></span>

<span data-ttu-id="63e3c-447">上記の GetCallbackEventReference の戻り値が文字列変数に割り当てられていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="63e3c-447">Notice that the return value of GetCallbackEventReference above was assigned to a string variable.</span></span> <span data-ttu-id="63e3c-448">この文字列は、コールバックを開始するコントロールのクライアント側イベントをフックするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-448">That string is used to hook a client-side event for the control that initiates the callback.</span></span> <span data-ttu-id="63e3c-449">この例では、コールバックはページのドロップダウンによって開始されるため *、OnChange*イベントをフックしたいと思います。</span><span class="sxs-lookup"><span data-stu-id="63e3c-449">In this example, the callback is initiated by a dropdown on the page, so I want to hook the *OnChange* event.</span></span>

<span data-ttu-id="63e3c-450">クライアント側のイベントをフックするには、次のように、クライアント側のマークアップにハンドラーを追加します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-450">To hook the client-side event, simply add a handler to the client-side markup as follows:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

<span data-ttu-id="63e3c-451">*cbRef*は呼び出しからの戻り値であることを思い出してください。</span><span class="sxs-lookup"><span data-stu-id="63e3c-451">Recall that *cbRef* is the return value from the call to GetCallbackEventReference.</span></span> <span data-ttu-id="63e3c-452">このファイルには、上記の\_Web フォーム DoCallback への呼び出しが含まれています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-452">It contains the call to WebForm\_DoCallback that was shown above.</span></span>

## <a name="step-4--register-the-client-side-script"></a><span data-ttu-id="63e3c-453">手順 4 : クライアント側スクリプトを登録する</span><span class="sxs-lookup"><span data-stu-id="63e3c-453">Step 4 : Register the Client-Side Script</span></span>

<span data-ttu-id="63e3c-454">呼び出しは、サーバー側のコールバックが成功したときに**ShowCompanyName**という名前のクライアント側スクリプトが実行されることを指定したことを思い出してください。</span><span class="sxs-lookup"><span data-stu-id="63e3c-454">Recall that the call to GetCallbackEventReference specified that a client-side script called **ShowCompanyName** would be executed when the server-side callback succeeds.</span></span> <span data-ttu-id="63e3c-455">このスクリプトは、ClientScriptManager インスタンスを使用してページに追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-455">That script needs to be added to the page using a ClientScriptManager instance.</span></span> <span data-ttu-id="63e3c-456">(このモジュールでは、後でクラスについて説明します)。あなたはそうします:</span><span class="sxs-lookup"><span data-stu-id="63e3c-456">(The ClientScriptManager class will be discussed later in this module.) You do that like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a><span data-ttu-id="63e3c-457">ステップ 5 : インターフェイスのメソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-457">Step 5 : Call the Methods of the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="63e3c-458">コード内で実装する必要がある 2 つのメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-458">The ICallbackEventHandler contains two methods that you need to implement in your code.</span></span> <span data-ttu-id="63e3c-459">これらは **、コールバック イベント**と**コールバック イベントを取得します**。</span><span class="sxs-lookup"><span data-stu-id="63e3c-459">They are **RaiseCallbackEvent** and **GetCallbackEvent**.</span></span>

<span data-ttu-id="63e3c-460">**イベントは**文字列を引数として受け取り、何も返しません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-460">**RaiseCallbackEvent** takes a string as an argument and returns nothing.</span></span> <span data-ttu-id="63e3c-461">文字列引数は、クライアント側の呼び出しから Web\_フォームの DoCallback に渡されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-461">The string argument is passed from the client-side call to WebForm\_DoCallback.</span></span> <span data-ttu-id="63e3c-462">この場合、その値は ddlCompany と呼ばれるドロップダウンの*値*属性です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-462">In this case, that value is the *value* attribute of the dropdown called ddlCompany.</span></span> <span data-ttu-id="63e3c-463">サーバー側のコードは、メソッドに配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-463">Your server-side code should be placed in the RaiseCallbackEvent method.</span></span> <span data-ttu-id="63e3c-464">たとえば、コールバックが外部リソースに対して WebRequest を作成している場合、そのコードを RaiseCallbackEvent に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-464">For example, if your callback is making a WebRequest against an external resource, that code should be placed in RaiseCallbackEvent.</span></span>

<span data-ttu-id="63e3c-465">**コールバック**のコールバックのクライアントへの戻り値を処理する役割を持つイベントです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-465">**GetCallbackEvent** is responsible for processing the return of the callback to the client.</span></span> <span data-ttu-id="63e3c-466">引数を受け取らず、文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-466">It takes no arguments and returns a string.</span></span> <span data-ttu-id="63e3c-467">返される文字列は、引数としてクライアント側の関数に渡*されます。*</span><span class="sxs-lookup"><span data-stu-id="63e3c-467">The string that it returns will be passed as an argument to the client-side function, in this case *ShowCompanyName*.</span></span>

<span data-ttu-id="63e3c-468">上記の手順を完了したら、スクリプトコールバックを ASP.NET 2.0 で実行する準備が整いました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-468">Once you have completed the above steps, you are ready to perform a script callback in ASP.NET 2.0.</span></span>

![](the-asp-net-2-0-page-model/_static/image4.png)

[<span data-ttu-id="63e3c-469">フルスクリーンビデオを開く</span><span class="sxs-lookup"><span data-stu-id="63e3c-469">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/callback1.wmv)

<span data-ttu-id="63e3c-470">ASP.NETのスクリプト コールバックは、XMLHttp 呼び出しをサポートするすべてのブラウザーでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="63e3c-470">Script callbacks in ASP.NET are supported in any browser that supports making XMLHttp calls.</span></span> <span data-ttu-id="63e3c-471">これには、現在使用されているすべての最新のブラウザが含まれます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-471">That includes all of the modern browsers in use today.</span></span> <span data-ttu-id="63e3c-472">インターネット エクスプローラは XMLHttp ActiveX オブジェクトを使用し、他の最新のブラウザ (今後の IE 7 を含む) は組み込みの XMLHttp オブジェクトを使用します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-472">Internet Explorer uses the XMLHttp ActiveX object while other modern browsers (including the upcoming IE 7) use an intrinsic XMLHttp object.</span></span> <span data-ttu-id="63e3c-473">ブラウザーがコールバックをサポートしているかどうかをプログラムで判断するには **、Request.Browser.SupportCallback**プロパティを使用できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-473">To programmatically determine if a browser supports callbacks, you can use the **Request.Browser.SupportCallback** property.</span></span> <span data-ttu-id="63e3c-474">要求元のクライアントがスクリプト コールバックをサポートしている場合、このプロパティは**true**を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-474">This property will return **true** if the requesting client supports script callbacks.</span></span>

## <a name="working-with-client-script-in-aspnet-20"></a><span data-ttu-id="63e3c-475">ASP.NET 2.0 でのクライアント スクリプトの操作</span><span class="sxs-lookup"><span data-stu-id="63e3c-475">Working with Client Script in ASP.NET 2.0</span></span>

<span data-ttu-id="63e3c-476">ASP.NET 2.0 のクライアント スクリプトは、ClientScriptManager クラスを使用して管理されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-476">Client scripts in ASP.NET 2.0 are managed via the use of the ClientScriptManager class.</span></span> <span data-ttu-id="63e3c-477">クラスは、型と名前を使用してクライアント スクリプトを追跡します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-477">The ClientScriptManager class keeps track of client scripts using a type and a name.</span></span> <span data-ttu-id="63e3c-478">これにより、同じスクリプトがプログラムによってページに複数回挿入されるのを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-478">This prevents the same script from being programmatically inserted on a page more than once.</span></span>

> [!NOTE]
> <span data-ttu-id="63e3c-479">スクリプトがページに正常に登録された後、同じスクリプトを登録しようとすると、スクリプトが 2 回目に登録されなくなるだけです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-479">After a script has been successfully registered on a page, any subsequent attempt to register the same script will simply result in the script not being registered a second time.</span></span> <span data-ttu-id="63e3c-480">重複するスクリプトは追加されず、例外も発生しません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-480">No duplicate scripts are added and no exception occurs.</span></span> <span data-ttu-id="63e3c-481">不要な計算を避けるために、スクリプトが既に登録されているかどうかを判断して、スクリプトを複数回登録しないようにする方法があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-481">To avoid unnecessary computation, there are methods that you can use to determine if a script is already registered so that you do not attempt to register it more than once.</span></span>

<span data-ttu-id="63e3c-482">ClientScriptManager のメソッドは、現在のすべてのASP.NET開発者に精通している必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-482">The methods of the ClientScriptManager should be familiar to all current ASP.NET developers:</span></span>

## <a name="registerclientscriptblock"></a><span data-ttu-id="63e3c-483">クライアント スクリプト ブロックを登録します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-483">RegisterClientScriptBlock</span></span>

<span data-ttu-id="63e3c-484">このメソッドは、レンダリングされたページの先頭にスクリプトを追加します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-484">This method adds a script to the top of the rendered page.</span></span> <span data-ttu-id="63e3c-485">これは、クライアントで明示的に呼び出される関数を追加する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-485">This is useful for adding functions that will be explicitly called on the client.</span></span>

<span data-ttu-id="63e3c-486">このメソッドには、2 つのオーバーロードされたバージョンがあります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-486">There are two overloaded versions of this method.</span></span> <span data-ttu-id="63e3c-487">4つの引数のうち3つは、その中で一般的です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-487">Three of four arguments are common among them.</span></span> <span data-ttu-id="63e3c-488">これらは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-488">They are:</span></span>

`type (string)`

<span data-ttu-id="63e3c-489">***型***引数は、スクリプトの型を識別します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-489">The ***type*** argument identifies a type for the script.</span></span> <span data-ttu-id="63e3c-490">一般的には、ページの型 (this.型の GetType())。</span><span class="sxs-lookup"><span data-stu-id="63e3c-490">It is generally a good idea to use the page's type (this.GetType()) for the type.</span></span>

`key (string)`

<span data-ttu-id="63e3c-491">***キー***引数は、スクリプトのユーザー定義キーです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-491">The ***key*** argument is a user-defined key for the script.</span></span> <span data-ttu-id="63e3c-492">これは、スクリプトごとに一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-492">This should be unique for each script.</span></span> <span data-ttu-id="63e3c-493">既に追加されたスクリプトと同じキーと種類のスクリプトを追加しようとしても、スクリプトは追加されません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-493">If you attempt to add a script with the same key and type of an already added script, it will not be added.</span></span>

`script (string)`

<span data-ttu-id="63e3c-494">***script***引数は、追加する実際のスクリプトを含む文字列です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-494">The ***script*** argument is a string containing the actual script to add.</span></span> <span data-ttu-id="63e3c-495">スクリプトを作成するには、文字列ビルダーを使用し、***スクリプト引数を***割り当てるには、StringBuilder の ToString() メソッドを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="63e3c-495">It's recommended that you use a StringBuilder to create the script and then use the ToString() method on the StringBuilder to assign the ***script*** argument.</span></span>

<span data-ttu-id="63e3c-496">3 つの引数しか取りませんが、オーバーロードされた RegisterClientScriptBlock を使用する場合は&lt;、&gt;スクリプト&lt;にスクリプト&gt;要素 ( スクリプトと /script ) を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-496">If you use the overloaded RegisterClientScriptBlock that only takes three arguments, you must include script elements (&lt;script&gt; and &lt;/script&gt;) in your script.</span></span>

<span data-ttu-id="63e3c-497">4 番目の引数を取る RegisterClientScriptBlock のオーバーロードを使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-497">You may choose to use the overload of RegisterClientScriptBlock that takes a fourth argument.</span></span> <span data-ttu-id="63e3c-498">4 番目の引数は、スクリプト要素を追加するかどうかを指定ASP.NETブール型です。</span><span class="sxs-lookup"><span data-stu-id="63e3c-498">The fourth argument is a Boolean that specifies whether or not ASP.NET should add script elements for you.</span></span> <span data-ttu-id="63e3c-499">この引数が**true の**場合、スクリプトにスクリプト要素を明示的に含めないようにします。</span><span class="sxs-lookup"><span data-stu-id="63e3c-499">If this argument is **true**, your script should not include the script elements explicitly.</span></span>

<span data-ttu-id="63e3c-500">スクリプトが既に登録されているかどうかを確認するには、メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-500">Use the IsClientScriptBlockRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="63e3c-501">これにより、すでに登録されているスクリプトを再登録する試みを回避できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-501">This allows you to avoid an attempt to re-register a script that has already been registered.</span></span>

### <a name="registerclientscriptinclude-new-in-20"></a><span data-ttu-id="63e3c-502">登録クライアントスクリプトインクルード (2.0 で新しい)</span><span class="sxs-lookup"><span data-stu-id="63e3c-502">RegisterClientScriptInclude (New in 2.0)</span></span>

<span data-ttu-id="63e3c-503">タグは、外部スクリプト ファイルにリンクするスクリプト ブロックを作成します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-503">The RegisterClientScriptInclude tag creates a script block that links to an external script file.</span></span> <span data-ttu-id="63e3c-504">2 つのオーバーロードがあります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-504">It has two overloads.</span></span> <span data-ttu-id="63e3c-505">1 つはキーと URL を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-505">One takes a key and a URL.</span></span> <span data-ttu-id="63e3c-506">2 つ目は、型を指定する 3 番目の引数を追加します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-506">The second adds a third argument specifying the type.</span></span>

<span data-ttu-id="63e3c-507">たとえば、次のコードは、アプリケーションのスクリプト フォルダーのルートにある jsfunctions.js にリンクするスクリプト ブロックを生成します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-507">For example, the following code generates a script block that links to jsfunctions.js in the root of the scripts folder of the application:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

<span data-ttu-id="63e3c-508">このコードは、レンダリングされたページに次のコードを生成します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-508">This code produces the following code in the rendered page:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> <span data-ttu-id="63e3c-509">スクリプト ブロックはページの下部に表示されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-509">The script block is rendered at the bottom of the page.</span></span>

<span data-ttu-id="63e3c-510">スクリプトが既に登録されているかどうかを確認するには、メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-510">Use the IsClientScriptIncludeRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="63e3c-511">これにより、スクリプトの再登録を回避できます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-511">This allows you to avoid an attempt to re-register a script.</span></span>

## <a name="registerstartupscript"></a><span data-ttu-id="63e3c-512">登録スタートアップスクリプト</span><span class="sxs-lookup"><span data-stu-id="63e3c-512">RegisterStartupScript</span></span>

<span data-ttu-id="63e3c-513">メソッドは、メソッドと同じ引数を受け取ります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-513">The RegisterStartupScript method takes the same arguments as the RegisterClientScriptBlock method.</span></span> <span data-ttu-id="63e3c-514">RegisterStartupScript に登録されたスクリプトは、ページの読み込み後、OnLoad クライアント側イベントの前に実行されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-514">A script registered with RegisterStartupScript executes after the page loads but before the OnLoad client-side event.</span></span> <span data-ttu-id="63e3c-515">1.X では、RegisterStartupScript に登録された&lt;スクリプトは終了 /フォーム&gt;タグの直前に配置され、RegisterClientScriptBlock に登録&lt;された&gt;スクリプトは開始フォーム タグの直後に配置されました。</span><span class="sxs-lookup"><span data-stu-id="63e3c-515">In 1.X, scripts registered with RegisterStartupScript were placed just before the closing &lt;/form&gt; tag while scripts registered with RegisterClientScriptBlock were placed immediately after the opening &lt;form&gt; tag.</span></span> <span data-ttu-id="63e3c-516">ASP.NET 2.0 では、両方とも /form&lt;&gt;タグの終了直前に配置されます。</span><span class="sxs-lookup"><span data-stu-id="63e3c-516">In ASP.NET 2.0, both are placed immediately before the closing &lt;/form&gt; tag.</span></span>

> [!NOTE]
> <span data-ttu-id="63e3c-517">RegisterStartupScript を使用して関数を登録した場合、クライアント側のコードで明示的に呼び出すまで、その関数は実行されません。</span><span class="sxs-lookup"><span data-stu-id="63e3c-517">If you register a function with RegisterStartupScript, that function will not execute until you explicitly call it in client-side code.</span></span>

<span data-ttu-id="63e3c-518">IsStartupScriptRegistered メソッドを使用して、スクリプトが既に登録されているかどうかを確認し、スクリプトの再登録を回避します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-518">Use the IsStartupScriptRegistered method to determine if a script has already been registered and avoid an attempt to re-register a script.</span></span>

## <a name="other-clientscriptmanager-methods"></a><span data-ttu-id="63e3c-519">その他のクライアントスクリプト マネージャー メソッド</span><span class="sxs-lookup"><span data-stu-id="63e3c-519">Other ClientScriptManager Methods</span></span>

<span data-ttu-id="63e3c-520">クラスのその他の便利なメソッドのいくつかを次に示します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-520">Here are some of the other useful methods of the ClientScriptManager class.</span></span>

|  <span data-ttu-id="63e3c-521"><strong>イベントのリファレンス</strong></span><span class="sxs-lookup"><span data-stu-id="63e3c-521"><strong>GetCallbackEventReference</strong></span></span>   |                                                 <span data-ttu-id="63e3c-522">このモジュールの前のスクリプト コールバックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="63e3c-522">See script callbacks earlier in this module.</span></span>                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <span data-ttu-id="63e3c-523"><strong>クライアントハイパーリンク</strong></span><span class="sxs-lookup"><span data-stu-id="63e3c-523"><strong>GetPostBackClientHyperlink</strong></span></span>  |                <span data-ttu-id="63e3c-524">クライアント側のイベントからポストバックするために使用&lt;できる&gt;JavaScript 参照 (javascript: call ) を取得します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-524">Gets a JavaScript reference (javascript:&lt;call&gt;) that can be used to post back from a client-side event.</span></span>                 |
|  <span data-ttu-id="63e3c-525"><strong>イベントリファレンス</strong></span><span class="sxs-lookup"><span data-stu-id="63e3c-525"><strong>GetPostBackEventReference</strong></span></span>   |                                   <span data-ttu-id="63e3c-526">クライアントからポストバックを開始するために使用できる文字列を取得します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-526">Gets a string that can be used to initiate a post back from the client.</span></span>                                    |
|      <span data-ttu-id="63e3c-527"><strong>をクリックします。</strong></span><span class="sxs-lookup"><span data-stu-id="63e3c-527"><strong>GetWebResourceUrl</strong></span></span>       | <span data-ttu-id="63e3c-528">アセンブリに埋め込まれているリソースへの URL を返します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-528">Returns a URL to a resource that is embedded in an assembly.</span></span> <span data-ttu-id="63e3c-529">を使用して使用<strong>する</strong>必要があります。</span><span class="sxs-lookup"><span data-stu-id="63e3c-529">Must be used in conjunction with <strong>RegisterClientScriptResource</strong>.</span></span> |
| <span data-ttu-id="63e3c-530"><strong>リソースを登録します。</strong></span><span class="sxs-lookup"><span data-stu-id="63e3c-530"><strong>RegisterClientScriptResource</strong></span></span> |     <span data-ttu-id="63e3c-531">Web リソースをページに登録します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-531">Registers a Web resource with the page.</span></span> <span data-ttu-id="63e3c-532">これらは、アセンブリに埋め込まれ、新しい WebResource.axd ハンドラーによって処理されるリソースです。</span><span class="sxs-lookup"><span data-stu-id="63e3c-532">These are resources embedded in an assembly and handled by the new WebResource.axd handler.</span></span>      |
|     <span data-ttu-id="63e3c-533"><strong>隠されたフィールドを登録します。</strong></span><span class="sxs-lookup"><span data-stu-id="63e3c-533"><strong>RegisterHiddenField</strong></span></span>      |                                                 <span data-ttu-id="63e3c-534">非表示フォーム フィールドをページに登録します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-534">Registers a hidden form field with the page.</span></span>                                                 |
|  <span data-ttu-id="63e3c-535"><strong>ステートメントを登録します。</strong></span><span class="sxs-lookup"><span data-stu-id="63e3c-535"><strong>RegisterOnSubmitStatement</strong></span></span>   |                                  <span data-ttu-id="63e3c-536">HTML フォームが送信されたときに実行されるクライアント側のコードを登録します。</span><span class="sxs-lookup"><span data-stu-id="63e3c-536">Registers client-side code that executes when the HTML form is submitted.</span></span>                                   |
