# <a name="contribute-to-the-aspnet-documentation"></a><span data-ttu-id="d2e04-101">ASP.NET ドキュメントに貢献する</span><span class="sxs-lookup"><span data-stu-id="d2e04-101">Contribute to the ASP.NET documentation</span></span>

<span data-ttu-id="d2e04-102">このドキュメントでは、[ASP.NET ドキュメント サイト](https://docs.microsoft.com/aspnet/)でホストされている記事とコード サンプルに貢献するためのプロセスを説明します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-102">This document covers the process for contributing to the articles and code samples that are hosted on the [ASP.NET documentation site](https://docs.microsoft.com/aspnet/).</span></span> <span data-ttu-id="d2e04-103">誤字修正と新しい記事の貢献を歓迎します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-103">Typo corrections and new articles are welcome contributions.</span></span>

## <a name="how-to-make-a-simple-correction-or-suggestion"></a><span data-ttu-id="d2e04-104">簡単な修正や提案を行う方法</span><span class="sxs-lookup"><span data-stu-id="d2e04-104">How to make a simple correction or suggestion</span></span>

<span data-ttu-id="d2e04-105">記事は、マークダウン ファイルとしてリポジトリに格納されます。</span><span class="sxs-lookup"><span data-stu-id="d2e04-105">Articles are stored in the repository as Markdown files.</span></span> <span data-ttu-id="d2e04-106">マークダウン ファイルの内容に対する簡単な変更は、ブラウザー ウィンドウの右上隅にある **[Edit]\(編集\)** リンクを選択して、ブラウザーで行います。</span><span class="sxs-lookup"><span data-stu-id="d2e04-106">Simple changes to the content of a Markdown file are made in the browser by selecting the **Edit** link in the upper-right corner of the browser window.</span></span> <span data-ttu-id="d2e04-107">(ナローブラウザーウィンドウで、 **[オプション]** バーを展開して **[編集]** リンクを表示します)。指示に従ってプル要求 (PR) を作成します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-107">(In a narrow browser window, expand the **options** bar to see the **Edit** link.) Follow the directions to create a pull request (PR).</span></span> <span data-ttu-id="d2e04-108">PR をレビューし、受け入れるか変更を提案します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-108">We will review the PR and accept it or suggest changes.</span></span>

## <a name="how-to-make-a-more-complex-submission"></a><span data-ttu-id="d2e04-109">もっと複雑な提案を行う方法</span><span class="sxs-lookup"><span data-stu-id="d2e04-109">How to make a more complex submission</span></span>

<span data-ttu-id="d2e04-110">[Git と GitHub.com](https://guides.github.com/activities/hello-world/) の基本的な理解が必要です。</span><span class="sxs-lookup"><span data-stu-id="d2e04-110">You need a basic understanding of [Git and GitHub.com](https://guides.github.com/activities/hello-world/).</span></span>

* <span data-ttu-id="d2e04-111">既存の記事の変更や新しい記事の作成など、行いたいことを説明した[問題](https://github.com/dotnet/AspNetDocs/issues/new)を開きます。</span><span class="sxs-lookup"><span data-stu-id="d2e04-111">Open an [issue](https://github.com/dotnet/AspNetDocs/issues/new) describing what you want to do, such as changing an existing article or creating a new one.</span></span> <span data-ttu-id="d2e04-112">多くの場合、GitHub は新しいトピックの提案のアウトラインを要求します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-112">We often request an outline for a new topic suggestion.</span></span> <span data-ttu-id="d2e04-113">多くの時間を費やす前に、チームの承認を待ちます。</span><span class="sxs-lookup"><span data-stu-id="d2e04-113">Wait for approval from the team before you invest much time.</span></span>
* <span data-ttu-id="d2e04-114">[Dotnet/AspNetDocs](https://github.com/dotnet/AspNetDocs/)リポジトリをフォークし、変更のためのブランチを作成します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-114">Fork the [dotnet/AspNetDocs](https://github.com/dotnet/AspNetDocs/) repository and create a branch for your changes.</span></span>
* <span data-ttu-id="d2e04-115">変更内容の PR をマスターに送信します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-115">Submit a PR to master with your changes.</span></span>
* <span data-ttu-id="d2e04-116">PR にラベル "cla-required" が割り当てられた場合、[貢献者使用許諾契約書 (CLA) を作成します](https://cla.dotnetfoundation.org/)。</span><span class="sxs-lookup"><span data-stu-id="d2e04-116">If your PR has the label 'cla-required' assigned, [complete the Contribution License Agreement (CLA)](https://cla.dotnetfoundation.org/).</span></span>
* <span data-ttu-id="d2e04-117">PR のフィードバックに対応します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-117">Respond to PR feedback.</span></span>

<span data-ttu-id="d2e04-118">このプロセスで新しい記事が公開された例については、.NET Docs リポジトリの[問題 &num;67](https://github.com/dotnet/docs/issues/67) と[Pull Request &num;798](https://github.com/dotnet/docs/pull/798) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d2e04-118">For an example where this process led to publication of a new article, see [Issue &num;67](https://github.com/dotnet/docs/issues/67) and [Pull Request &num;798](https://github.com/dotnet/docs/pull/798) in the .NET Docs repository.</span></span> <span data-ttu-id="d2e04-119">新しい記事は「[XML コメントによるコードの文書化](https://docs.microsoft.com/dotnet/articles/csharp/codedoc)」です。</span><span class="sxs-lookup"><span data-stu-id="d2e04-119">The new article is [Documenting your code](https://docs.microsoft.com/dotnet/articles/csharp/codedoc).</span></span>

## <a name="docs-authoring-pack-extension-in-visual-studio-code"></a><span data-ttu-id="d2e04-120">Visual Studio Code での Docs Authoring 拡張機能</span><span class="sxs-lookup"><span data-stu-id="d2e04-120">Docs Authoring Pack extension in Visual Studio Code</span></span>

<span data-ttu-id="d2e04-121">Visual Studio Code を使用して ASP.NET ドキュメントに貢献する場合は、[Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) 拡張機能をインストールすることで生産性を高めることができます。</span><span class="sxs-lookup"><span data-stu-id="d2e04-121">If you use Visual Studio Code to contribute to the ASP.NET documentation, you can boost your productivity by installing the [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) extension.</span></span> <span data-ttu-id="d2e04-122">拡張機能では、Markdown の lint 処理、コードのスペル チェック、および記事のテンプレートを支援する各種のツールが提供されています。</span><span class="sxs-lookup"><span data-stu-id="d2e04-122">The extension provides a variety of tools that helps with Markdown linting, code spell checking, and article templates.</span></span>

## <a name="markdown-syntax"></a><span data-ttu-id="d2e04-123">Markdown の構文</span><span class="sxs-lookup"><span data-stu-id="d2e04-123">Markdown syntax</span></span>

<span data-ttu-id="d2e04-124">記事は [DocFx-flavored Markdown](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html) で書かれており、これは [GitHub flavored Markdown (GFM)](https://guides.github.com/features/mastering-markdown/) のスーパーセットです。</span><span class="sxs-lookup"><span data-stu-id="d2e04-124">Articles are written in [DocFx-flavored Markdown](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html), which is a superset of [GitHub-flavored Markdown (GFM)](https://guides.github.com/features/mastering-markdown/).</span></span> <span data-ttu-id="d2e04-125">ASP.NET のドキュメントで一般的に使用されている UI 機能の DFM 構文の例については、.NET Docs リポジトリスタイルガイドの[メタデータと Markdown テンプレート](https://github.com/dotnet/docs/blob/master/styleguide/template.md)に関する記述を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d2e04-125">For examples of DFM syntax for UI features commonly used in the ASP.NET documentation, see [Metadata and Markdown Template](https://github.com/dotnet/docs/blob/master/styleguide/template.md) in the .NET Docs repository style guide.</span></span>

## <a name="folder-structure-conventions"></a><span data-ttu-id="d2e04-126">フォルダー構造の規則</span><span class="sxs-lookup"><span data-stu-id="d2e04-126">Folder structure conventions</span></span>

<span data-ttu-id="d2e04-127">マークダウン ファイルごとに、画像用のフォルダーとサンプル コード用のフォルダーが存在する場合があります。</span><span class="sxs-lookup"><span data-stu-id="d2e04-127">For each Markdown file, a folder for images and a folder for sample code may exist.</span></span> <span data-ttu-id="d2e04-128">記事が[signalr/概要/詳細/依存関係の挿入](https://github.com/dotnet/AspNetDocs/blob/master/aspnet/signalr/overview/advanced/dependency-injection.md)である場合、イメージは signalr/[概要/詳細/依存関係挿入/\_静的](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/signalr/overview/advanced/dependency-injection/_static)であり、サンプルアプリプロジェクトファイルは[signalr/概要/高度/依存関係挿入/サンプル](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/signalr/overview/advanced/dependency-injection/samples)にあります。</span><span class="sxs-lookup"><span data-stu-id="d2e04-128">If the article is [signalr/overview/advanced/dependency-injection.md](https://github.com/dotnet/AspNetDocs/blob/master/aspnet/signalr/overview/advanced/dependency-injection.md), the images are in [signalr/overview/advanced/dependency-injection/\_static](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/signalr/overview/advanced/dependency-injection/_static) and the sample app project files are in [signalr/overview/advanced/dependency-injection/samples](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/signalr/overview/advanced/dependency-injection/samples).</span></span> <span data-ttu-id="d2e04-129">*Signalr/概要/詳細/依存関係挿入 md*ファイルのイメージは、次の Markdown によって表示されます。</span><span class="sxs-lookup"><span data-stu-id="d2e04-129">An image in the *signalr/overview/advanced/dependency-injection.md* file is rendered by the following Markdown:</span></span>

```md
![description of image for alt attribute](dependency-injection/_static/image1.png)
```

<span data-ttu-id="d2e04-130">すべての画像に[代替 (alt) テキスト](https://wikipedia.org/wiki/Alt_attribute)が必要です。</span><span class="sxs-lookup"><span data-stu-id="d2e04-130">All images should have [alternative (alt) text](https://wikipedia.org/wiki/Alt_attribute).</span></span> <span data-ttu-id="d2e04-131">代替テキストの指定に関するアドバイスについては、「[WebAIM: Alternative Text](https://webaim.org/techniques/alttext/)」(WebAIM: 代替テキスト) などのオンライン リソースを参照してください。</span><span class="sxs-lookup"><span data-stu-id="d2e04-131">For advice on specifying alt text, see online resources, such as [WebAIM: Alternative Text](https://webaim.org/techniques/alttext/).</span></span>

<span data-ttu-id="d2e04-132">マークダウン ファイル名と画像ファイル名には、小文字を使用します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-132">Use lowercase for Markdown file names and image file names.</span></span>

## <a name="internal-links"></a><span data-ttu-id="d2e04-133">内部リンク</span><span class="sxs-lookup"><span data-stu-id="d2e04-133">Internal links</span></span>

<span data-ttu-id="d2e04-134">内部リンクでは、xref リンクでターゲット記事の `uid` を使用する必要があります (リンク テキストは、リンクされたコンテンツのタイトルに設定されます)。</span><span class="sxs-lookup"><span data-stu-id="d2e04-134">Internal links should use the `uid` of the target article with an xref link (link text is set to the linked content's title):</span></span>

```md
<xref:uid_of_the_topic>
```

<span data-ttu-id="d2e04-135">記事のタイトルがリンク テキストに適さない場合は (たとえば、文の単語や語句がリンク テキストである場合)、次のように xref リンクとリンク テキストを指定します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-135">If the title of the article is unsuitable for link text (for example, a word or phrase in a sentence is the link text), specify the xref link and link text with the following:</span></span>

```md
[link text](xref:uid_of_the_topic)
```

<span data-ttu-id="d2e04-136">詳細については、「[DocFX Cross Reference](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#cross-reference)」(DocFX の相互参照) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d2e04-136">For more information, see the [DocFX Cross Reference](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#cross-reference).</span></span>

## <a name="images-and-screenshots"></a><span data-ttu-id="d2e04-137">画像とスクリーンショット</span><span class="sxs-lookup"><span data-stu-id="d2e04-137">Images and screenshots</span></span>

<span data-ttu-id="d2e04-138">次の場合を除き、記事に画像を含めないでください。</span><span class="sxs-lookup"><span data-stu-id="d2e04-138">Don't include images with articles, except:</span></span>

* <span data-ttu-id="d2e04-139">基本的なオンボード (初心者向け) チュートリアル。</span><span class="sxs-lookup"><span data-stu-id="d2e04-139">In basic onboarding (beginner) tutorials.</span></span>
* <span data-ttu-id="d2e04-140">わかりやすくするために画像が必要な場合。</span><span class="sxs-lookup"><span data-stu-id="d2e04-140">When an image is needed for clarity.</span></span>

<span data-ttu-id="d2e04-141">このような制限により、リポジトリのサイズが小さくなります。</span><span class="sxs-lookup"><span data-stu-id="d2e04-141">These restrictions reduce the size of the repository.</span></span>

<span data-ttu-id="d2e04-142">省略可能な手順として、ドキュメントで使用されている画像とスクリーンショットが圧縮されていることを確認します。これは、ファイルのサイズとページ読み込みのパフォーマンスに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="d2e04-142">As an optional step, ensure that any images and screenshots used in the documentation are compressed, which helps with file size and page load performance.</span></span> <span data-ttu-id="d2e04-143">一般的なツールとしては、TinyPNG ([TinyPNG Web サイト](https://tinypng.com/) または [TinyPNG API](https://tinypng.com/developers) を使用) または [Image Optimizer](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ImageOptimizer) Visual Studio 拡張機能などがあります。</span><span class="sxs-lookup"><span data-stu-id="d2e04-143">A few popular tools include TinyPNG (using the [TinyPNG website](https://tinypng.com/) or the [TinyPNG API](https://tinypng.com/developers)) or the [Image Optimizer](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ImageOptimizer) Visual Studio extension.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="d2e04-144">コード スニペット</span><span class="sxs-lookup"><span data-stu-id="d2e04-144">Code snippets</span></span>

<span data-ttu-id="d2e04-145">記事には、ポイントを説明するためのコード スニペットが含まれることがよくあります。</span><span class="sxs-lookup"><span data-stu-id="d2e04-145">Articles frequently contain code snippets to illustrate points.</span></span> <span data-ttu-id="d2e04-146">DFM では、マークダウン ファイルにコードをコピーすること、または別のコード ファイルを参照することができます。</span><span class="sxs-lookup"><span data-stu-id="d2e04-146">DFM allows you to copy code into the Markdown file or refer to a separate code file.</span></span> <span data-ttu-id="d2e04-147">コードのエラーの可能性を最小限にするため、可能な限り別のコード ファイルを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d2e04-147">We prefer to use separate code files whenever possible to minimize the chance of errors in the code.</span></span> <span data-ttu-id="d2e04-148">コードファイルは、前のサンプルプロジェクトで説明したフォルダー構造を使用してリポジトリに格納されます。</span><span class="sxs-lookup"><span data-stu-id="d2e04-148">The code files are stored in the repository using the folder structure described earlier for sample projects.</span></span>

<span data-ttu-id="d2e04-149">次の例では、[configuration/index.md](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#code-snippet) ファイルで使用する *DFM コード スニペットの構文*を示します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-149">The following examples illustrate [DFM code snippet syntax](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#code-snippet) for use in a *configuration/index.md* file.</span></span>

<span data-ttu-id="d2e04-150">コード ファイル全体をスニペットとしてレンダリングするには:</span><span class="sxs-lookup"><span data-stu-id="d2e04-150">To render an entire code file as a snippet:</span></span>

```md
[!code-csharp[](configuration/index/sample/Program.cs)]
```

<span data-ttu-id="d2e04-151">行番号を使用してファイルの一部をスニペットとして表示するには:</span><span class="sxs-lookup"><span data-stu-id="d2e04-151">To render a portion of a file as a snippet by using line numbers:</span></span>

```md
[!code-csharp[](configuration/index/sample/Program.cs?range=1-10,20,30,40-50]
[!code-html[](configuration/index/sample/Views/Home/Index.cshtml?range=1-10,20,30,40-50]
```

<span data-ttu-id="d2e04-152">C# のスニペットについては、[C# の領域](https://docs.microsoft.com/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region)に関する記事を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d2e04-152">For C# snippets, reference a [C# region](https://docs.microsoft.com/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region).</span></span> <span data-ttu-id="d2e04-153">可能な場合は常に、行番号ではなく領域を使用してください。コード ファイル内の行番号は変更されることがよくあり、Markdown での行番号の参照と同期されなくなるためです。</span><span class="sxs-lookup"><span data-stu-id="d2e04-153">Whenever possible, use regions rather than line numbers because line numbers in a code file tend to change and become out of sync with line number references in Markdown.</span></span> <span data-ttu-id="d2e04-154">C# の領域は入れ子にすることができます。</span><span class="sxs-lookup"><span data-stu-id="d2e04-154">C# regions can be nested.</span></span> <span data-ttu-id="d2e04-155">外側の領域を参照している場合、内側の `#region` および `#endregion` ディレクティブはスニペットには表示されません。</span><span class="sxs-lookup"><span data-stu-id="d2e04-155">If referencing the outer region, the inner `#region` and `#endregion` directives aren't rendered in a snippet.</span></span>

<span data-ttu-id="d2e04-156">C# の "snippet_Example" という名前の領域を表示するには:</span><span class="sxs-lookup"><span data-stu-id="d2e04-156">To render a C# region named "snippet_Example":</span></span>

```md
[!code-csharp[](configuration/index/sample/Program.cs?name=snippet_Example)]
```

<span data-ttu-id="d2e04-157">レンダリングされたスニペットで選択されている行を強調表示するには (通常は黄色の背景色でレンダリングされます):</span><span class="sxs-lookup"><span data-stu-id="d2e04-157">To highlight selected lines in a rendered snippet (usually renders as yellow background color):</span></span>

```md
[!code-csharp[](configuration/index/sample/Program.cs?name=snippet_Example&highlight=1-3,10,20-25)]
[!code-csharp[](configuration/index/sample/Program.cs?range=10-20&highlight=1-3]
[!code-html[](configuration/index/sample/Views/Home/Index.cshtml?range=10-20&highlight=1-3]
[!code-javascript[](configuration/index/sample/UsingOptionsSample.csproj?range=10-20&highlight=1-3]
```

## <a name="test-changes-with-docfx"></a><span data-ttu-id="d2e04-158">DocFX で変更をテストする</span><span class="sxs-lookup"><span data-stu-id="d2e04-158">Test changes with DocFX</span></span>

<span data-ttu-id="d2e04-159">[DocFX コマンド ライン ツール](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html#2-use-docfx-as-a-command-line-tool)を使用して変更をテストします。このツールは、ローカルにホストされたバージョンのサイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-159">Test your changes with the [DocFX command-line tool](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html#2-use-docfx-as-a-command-line-tool), which creates a locally hosted version of the site.</span></span> <span data-ttu-id="d2e04-160">DocFX では、docs.microsoft.com 用に作成されたスタイルやサイトの拡張機能はレンダリングされません。</span><span class="sxs-lookup"><span data-stu-id="d2e04-160">DocFX doesn't render style and site extensions created for docs.microsoft.com.</span></span>

<span data-ttu-id="d2e04-161">DocFX には次のものが必要です。</span><span class="sxs-lookup"><span data-stu-id="d2e04-161">DocFX requires:</span></span>

* <span data-ttu-id="d2e04-162">Windows 上の .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="d2e04-162">.NET Framework on Windows.</span></span>
* <span data-ttu-id="d2e04-163">Linux または macOS 用の Mono。</span><span class="sxs-lookup"><span data-stu-id="d2e04-163">Mono for Linux or macOS.</span></span>

### <a name="windows-instructions"></a><span data-ttu-id="d2e04-164">Windows での手順</span><span class="sxs-lookup"><span data-stu-id="d2e04-164">Windows instructions</span></span>

* <span data-ttu-id="d2e04-165">*DocFX リリース*から [docfx.zip](https://github.com/dotnet/docfx/releases) をダウンロードして解凍します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-165">Download and unzip *docfx.zip* from [DocFX releases](https://github.com/dotnet/docfx/releases).</span></span>
* <span data-ttu-id="d2e04-166">DocFX を PATH に追加します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-166">Add DocFX to your PATH.</span></span>
* <span data-ttu-id="d2e04-167">コマンドシェルで、 *docfx. json*ファイルが含まれている*aspnet*フォルダーに移動し、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-167">In a command shell, navigate to the *aspnet* folder that contains the *docfx.json* file and run the following command:</span></span>

  ```console
  docfx --serve
  ```

* <span data-ttu-id="d2e04-168">ブラウザーで、`http://localhost:8080/group1-dest/` に移動します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-168">In a browser, navigate to `http://localhost:8080/group1-dest/`.</span></span>

### <a name="mono-instructions"></a><span data-ttu-id="d2e04-169">Mono での説明</span><span class="sxs-lookup"><span data-stu-id="d2e04-169">Mono instructions</span></span>

* <span data-ttu-id="d2e04-170">Homebrew を使用して Mono をインストールします。</span><span class="sxs-lookup"><span data-stu-id="d2e04-170">Install Mono via Homebrew:</span></span>

  ```console
  brew install mono
  ```

* <span data-ttu-id="d2e04-171">[最新バージョンの DocFX](https://github.com/dotnet/docfx/releases) をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="d2e04-171">Download the [latest version of DocFX](https://github.com/dotnet/docfx/releases).</span></span>
* <span data-ttu-id="d2e04-172">アーカイブを *$HOME/bin/docfx* に抽出します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-172">Extract the archive to *$HOME/bin/docfx*.</span></span>
* <span data-ttu-id="d2e04-173">bash シェルで **docfx** の別名を 2 つ作成します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-173">Create a pair of aliases for **docfx** in a bash shell.</span></span> <span data-ttu-id="d2e04-174">最初の別名は、ドキュメントを構築するために使います。</span><span class="sxs-lookup"><span data-stu-id="d2e04-174">The first alias is used to build the documentation.</span></span> <span data-ttu-id="d2e04-175">2 番目の別名は、ドキュメントを構築して提供するために使います。</span><span class="sxs-lookup"><span data-stu-id="d2e04-175">The second alias is used to build and serve the documentation.</span></span>

  ```console
  alias docfx='mono $HOME/bin/docfx/docfx.exe'
  alias docfx-serve='mono $HOME/bin/docfx/docfx.exe --serve'
  ```

* <span data-ttu-id="d2e04-176">コマンドシェルで、 *docfx. json*ファイルが含まれている*aspnet*フォルダーに移動し、次のコマンドを実行して、そのエイリアスを使用してドキュメントをビルドおよび提供します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-176">In a command shell, navigate to the *aspnet* folder that contains the *docfx.json* file  and run the following command to build and serve the docs via its alias:</span></span>

  ```console
  docfx-serve
  ```

* <span data-ttu-id="d2e04-177">ブラウザーで、`http://localhost:8080/group1-dest/` に移動します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-177">In a browser, navigate to `http://localhost:8080/group1-dest/`.</span></span>

## <a name="voice-and-tone"></a><span data-ttu-id="d2e04-178">スタイルとトーン</span><span class="sxs-lookup"><span data-stu-id="d2e04-178">Voice and tone</span></span>

<span data-ttu-id="d2e04-179">目標は、できるかぎり幅広いユーザーにわかりやすいドキュメントを作成することです。</span><span class="sxs-lookup"><span data-stu-id="d2e04-179">Our goal is to write documentation that is easily understandable by the widest possible audience.</span></span> <span data-ttu-id="d2e04-180">そのため、寄稿者に従っていただきたい書き方のガイドラインが設けられています。</span><span class="sxs-lookup"><span data-stu-id="d2e04-180">To that end, we established guidelines for writing style that we ask our contributors to follow.</span></span> <span data-ttu-id="d2e04-181">詳細については、「.NET リポジトリの[音声とトーンのガイドライン](https://github.com/dotnet/docs/blob/master/styleguide/voice-tone.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d2e04-181">For more information, see [Voice and tone guidelines](https://github.com/dotnet/docs/blob/master/styleguide/voice-tone.md) in the .NET repository.</span></span>

## <a name="microsoft-writing-style-guide"></a><span data-ttu-id="d2e04-182">Microsoft 文書作成スタイル ガイド</span><span class="sxs-lookup"><span data-stu-id="d2e04-182">Microsoft Writing Style Guide</span></span>

<span data-ttu-id="d2e04-183">[Microsoft 文書作成スタイル ガイド](https://docs.microsoft.com/style-guide/welcome/)では、ASP.NET Core のドキュメントを含むあらゆる形式の技術コミュニケーションに対する文書作成スタイルと用語のガイダンスが提供されています。</span><span class="sxs-lookup"><span data-stu-id="d2e04-183">The [Microsoft Writing Style Guide](https://docs.microsoft.com/style-guide/welcome/) provides writing style and terminology guidance for all forms of technology communication, including the ASP.NET Core documentation.</span></span>

## <a name="redirects"></a><span data-ttu-id="d2e04-184">リダイレクト</span><span class="sxs-lookup"><span data-stu-id="d2e04-184">Redirects</span></span>

<span data-ttu-id="d2e04-185">記事を削除する、記事のファイル名を変更する、または記事を別のフォルダーに移動する場合は、記事にブックマークを設定している人が *404 Not Found* エラーを受け取らないように、リダイレクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="d2e04-185">If you delete an article, change its file name, or move it to a different folder, create a redirect so that people who bookmarked the article don't receive a *404 Not Found* error.</span></span> <span data-ttu-id="d2e04-186">[マスター リダイレクト ファイル](https://github.com/dotnet/AspNetDocs/blob/master/.openpublishing.redirection.json)にリダイレクトを追加してください。</span><span class="sxs-lookup"><span data-stu-id="d2e04-186">Add redirects to the [master redirect file](https://github.com/dotnet/AspNetDocs/blob/master/.openpublishing.redirection.json).</span></span>
