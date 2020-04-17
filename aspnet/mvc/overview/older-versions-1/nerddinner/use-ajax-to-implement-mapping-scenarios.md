---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: AJAX を使用したマッピング シナリオの実装 |マイクロソフトドキュメント
author: rick-anderson
description: ステップ 11 は、AJAX マッピング サポートを NerdDinner アプリケーションに統合する方法を示し、ディナーを作成、編集、または表示しているユーザーが l..
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: f2e2640eb421d5ee8006915f46cbe1090b8d21ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542587"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a><span data-ttu-id="f26e0-103">AJAX を使用し、マッピング シナリオを実装する</span><span class="sxs-lookup"><span data-stu-id="f26e0-103">Use AJAX to Implement Mapping Scenarios</span></span>

<span data-ttu-id="f26e0-104">[マイクロソフト](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f26e0-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f26e0-105">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="f26e0-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="f26e0-106">これは、MVC 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)の手順 11 ASP.NETします。</span><span class="sxs-lookup"><span data-stu-id="f26e0-106">This is step 11 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="f26e0-107">ステップ 11 は、AJAX マッピング サポートを NerdDinner アプリケーションに統合する方法を示し、ディナーの作成、編集、または表示を行うユーザーがディナーの場所をグラフィカルに表示できるようにします。</span><span class="sxs-lookup"><span data-stu-id="f26e0-107">Step 11 shows how to integrate AJAX mapping support into our NerdDinner application, enabling users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>
> 
> <span data-ttu-id="f26e0-108">mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f26e0-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a><span data-ttu-id="f26e0-109">NerdDinner ステップ 11: AJAX マップの統合</span><span class="sxs-lookup"><span data-stu-id="f26e0-109">NerdDinner Step 11: Integrating an AJAX Map</span></span>

<span data-ttu-id="f26e0-110">AJAX マッピングのサポートを統合することで、アプリケーションをもう少し視覚的にわくわくします。</span><span class="sxs-lookup"><span data-stu-id="f26e0-110">We'll now make our application a little more visually exciting by integrating AJAX mapping support.</span></span> <span data-ttu-id="f26e0-111">これにより、ディナーの作成、編集、または表示を行っているユーザーが、夕食の場所をグラフィカルに表示できるようになります。</span><span class="sxs-lookup"><span data-stu-id="f26e0-111">This will enable users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>

### <a name="creating-a-map-partial-view"></a><span data-ttu-id="f26e0-112">マップ部分ビューの作成</span><span class="sxs-lookup"><span data-stu-id="f26e0-112">Creating a Map Partial View</span></span>

<span data-ttu-id="f26e0-113">アプリケーション内のいくつかの場所でマッピング機能を使用します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-113">We are going to use mapping functionality in several places within our application.</span></span> <span data-ttu-id="f26e0-114">コード DRY を維持するために、複数のコント ローラーアクションとビューで再利用できる単一の部分テンプレート内の共通のマップ機能をカプセル化します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-114">To keep our code DRY we'll encapsulate the common map functionality within a single partial template that we can re-use across multiple controller actions and views.</span></span> <span data-ttu-id="f26e0-115">この部分ビューに "map.ascx" という名前を付け、\Views\Dinners ディレクトリ内に作成します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-115">We'll name this partial view "map.ascx" and create it within the \Views\Dinners directory.</span></span>

<span data-ttu-id="f26e0-116">map.ascx 部分を作成するには、\Views\Dinners ディレクトリを右クリックし、[追加-&gt;表示] メニュー コマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-116">We can create the map.ascx partial by right-clicking on the \Views\Dinners directory and choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="f26e0-117">ビューに "Map.ascx" という名前を付け、それを部分的なビューとして確認し、厳密に型指定された "Dinner" モデル クラスを渡すことを示します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-117">We'll name the view "Map.ascx", check it as a partial view, and indicate that we are going to pass it a strongly-typed "Dinner" model class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

<span data-ttu-id="f26e0-118">「追加」ボタンをクリックすると、部分テンプレートが作成されます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-118">When we click the "Add" button our partial template will be created.</span></span> <span data-ttu-id="f26e0-119">次に、次の内容を含む Map.ascx ファイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-119">We'll then update the Map.ascx file to have the following content:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

<span data-ttu-id="f26e0-120">最初&lt;のスクリプト&gt;参照は、Microsoft 仮想アース 6.2 マッピング ライブラリを指します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-120">The first &lt;script&gt; reference points to the Microsoft Virtual Earth 6.2 mapping library.</span></span> <span data-ttu-id="f26e0-121">2&lt;番目&gt;のスクリプト参照は、一般的な Javascript マッピング ロジックをカプセル化する map.js ファイルを指します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-121">The second &lt;script&gt; reference points to a map.js file that we will shortly create which will encapsulate our common Javascript mapping logic.</span></span> <span data-ttu-id="f26e0-122">&lt;div id="theMap"&gt;要素は、仮想地球がマップをホストするために使用するHTMLコンテナです。</span><span class="sxs-lookup"><span data-stu-id="f26e0-122">The &lt;div id="theMap"&gt; element is the HTML container that Virtual Earth will use to host the map.</span></span>

<span data-ttu-id="f26e0-123">その後、このビュー&lt;に&gt;固有の 2 つの JavaScript 関数を含む埋め込みスクリプト ブロックがあります。</span><span class="sxs-lookup"><span data-stu-id="f26e0-123">We then have an embedded &lt;script&gt; block that contains two JavaScript functions specific to this view.</span></span> <span data-ttu-id="f26e0-124">最初の関数は、jQuery を使用して、ページがクライアント側スクリプトを実行する準備ができたときに実行される関数をワイヤアップします。</span><span class="sxs-lookup"><span data-stu-id="f26e0-124">The first function uses jQuery to wire-up a function that executes when the page is ready to run client-side script.</span></span> <span data-ttu-id="f26e0-125">これは、仮想アース マップ コントロールを読み込むために Map.js スクリプト ファイル内で定義する LoadMap() ヘルパー関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-125">It calls a LoadMap() helper function that we'll define within our Map.js script file to load the virtual earth map control.</span></span> <span data-ttu-id="f26e0-126">2 番目の関数は、場所を識別するピンをマップに追加するコールバック イベント ハンドラーです。</span><span class="sxs-lookup"><span data-stu-id="f26e0-126">The second function is a callback event handler that adds a pin to the map that identifies a location.</span></span>

<span data-ttu-id="f26e0-127">クライアント側スクリプト ブロック内でサーバー側&lt;の %= %&gt;ブロックを使用して、JavaScript にマップする Dinner の緯度と経度を埋め込む方法に注目してください。</span><span class="sxs-lookup"><span data-stu-id="f26e0-127">Notice how we are using a server-side &lt;%= %&gt; block within the client-side script block to embed the latitude and longitude of the Dinner we want to map into the JavaScript.</span></span> <span data-ttu-id="f26e0-128">これは、クライアント側スクリプトで使用できる動的な値を出力する場合に便利な手法です (値を取得するためにサーバーに個別の AJAX コールバックを必要とせず、高速に実行できます)。</span><span class="sxs-lookup"><span data-stu-id="f26e0-128">This is a useful technique to output dynamic values that can be used by client-side script (without requiring a separate AJAX call back to the server to retrieve the values – which makes it faster).</span></span> <span data-ttu-id="f26e0-129">%= &lt;%&gt;ブロックは、ビューがサーバーでレンダリングしているときに実行されるため、HTML の出力は JavaScript 値が埋め込まれた状態になります (例: var latitude = 47.64312;)。</span><span class="sxs-lookup"><span data-stu-id="f26e0-129">The &lt;%= %&gt; blocks will execute when the view is rendering on the server – and so the output of the HTML will just end up with embedded JavaScript values (for example: var latitude = 47.64312;).</span></span>

### <a name="creating-a-mapjs-utility-library"></a><span data-ttu-id="f26e0-130">Map.js ユーティリティ ライブラリの作成</span><span class="sxs-lookup"><span data-stu-id="f26e0-130">Creating a Map.js utility library</span></span>

<span data-ttu-id="f26e0-131">ここで、マップの JavaScript 機能をカプセル化するために使用できる Map.js ファイルを作成しましょう (そして、上記の LoadMap メソッドと LoadPin メソッドを実装します)。</span><span class="sxs-lookup"><span data-stu-id="f26e0-131">Let's now create the Map.js file that we can use to encapsulate the JavaScript functionality for our map (and implement the LoadMap and LoadPin methods above).</span></span> <span data-ttu-id="f26e0-132">これを行うには、プロジェクト内の \Scripts ディレクトリを右クリックし、[新しい項目の&gt;追加] メニュー コマンドを選択し、JScript 項目を選択して "Map.js" という名前を付けます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-132">We can do this by right-clicking on the \Scripts directory within our project, and then choose the "Add-&gt;New Item" menu command, select the JScript item, and name it "Map.js".</span></span>

<span data-ttu-id="f26e0-133">以下は、マップを表示し、夕食のために場所のピンを追加するために仮想地球と対話する Map.js ファイルに追加する JavaScript コードです。</span><span class="sxs-lookup"><span data-stu-id="f26e0-133">Below is the JavaScript code we'll add to the Map.js file that will interact with Virtual Earth to display our map and add locations pins to it for our dinners:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a><span data-ttu-id="f26e0-134">マップを作成フォームと編集フォームと統合する</span><span class="sxs-lookup"><span data-stu-id="f26e0-134">Integrating the Map with Create and Edit Forms</span></span>

<span data-ttu-id="f26e0-135">マップのサポートを既存の作成および編集のシナリオと統合します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-135">We'll now integrate the Map support with our existing Create and Edit scenarios.</span></span> <span data-ttu-id="f26e0-136">良いニュースは、これは非常に簡単で、コントローラコードを変更する必要がないということです。</span><span class="sxs-lookup"><span data-stu-id="f26e0-136">The good news is that this is pretty easy to-do, and doesn't require us to change any of our Controller code.</span></span> <span data-ttu-id="f26e0-137">作成ビューと編集ビューでは、ディナー フォーム UI を実装するための共通の "DinnerForm" 部分ビューが共有されるため、マップを 1 か所に追加して、作成シナリオと編集シナリオの両方で使用できます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-137">Because our Create and Edit views share a common "DinnerForm" partial view to implement the dinner form UI, we can add the map in one place and have both our Create and Edit scenarios use it.</span></span>

<span data-ttu-id="f26e0-138">必要なのは、\Views\Dinners\DinnerForm.ascx 部分ビューを開き、新しいマップを部分的に含むように更新することだけです。</span><span class="sxs-lookup"><span data-stu-id="f26e0-138">All we need to-do is to open the \Views\Dinners\DinnerForm.ascx partial view and update it to include our new map partial.</span></span> <span data-ttu-id="f26e0-139">以下は、マップが追加されると、更新された DinnerForm の外観です (注: 簡潔にするために、以下のコード スニペットから HTML フォーム要素を省略します)。</span><span class="sxs-lookup"><span data-stu-id="f26e0-139">Below is what the updated DinnerForm will look like once the map is added (note: the HTML form elements are omitted from the code snippet below for brevity):</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

<span data-ttu-id="f26e0-140">上記の DinnerForm の一部は、モデル型として "DinnerFormViewModel" 型のオブジェクトを取ります (これは、Dinner オブジェクトと、国のドロップダウン リストを設定するための SelectList の両方が必要であるためです)。</span><span class="sxs-lookup"><span data-stu-id="f26e0-140">The DinnerForm partial above takes an object of type "DinnerFormViewModel" as its model type (because it needs both a Dinner object, as well as a SelectList to populate the dropdownlist of countries).</span></span> <span data-ttu-id="f26e0-141">私たちのマップの部分は、モデルタイプとしてタイプ"Dinner"のオブジェクトを必要とするので、マップの部分をレンダリングするときにDinnerFormViewModelのDinnerサブプロパティだけを渡しています。</span><span class="sxs-lookup"><span data-stu-id="f26e0-141">Our Map partial just needs an object of type "Dinner" as its model type, and so when we render the map partial we are passing just the Dinner sub-property of DinnerFormViewModel to it:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

<span data-ttu-id="f26e0-142">部分に追加した JavaScript 関数は、jQuery を使用して"アドレス" HTML テキスト ボックスに "ぼかし" イベントを添付します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-142">The JavaScript function we've added to the partial uses jQuery to attach a "blur" event to the "Address" HTML textbox.</span></span> <span data-ttu-id="f26e0-143">ユーザーがテキスト ボックス内でクリックまたはタブを表示したときに発生する "フォーカス" イベントを聞いたことがあるでしょう。</span><span class="sxs-lookup"><span data-stu-id="f26e0-143">You've probably heard of "focus" events that fire when a user clicks or tabs into a textbox.</span></span> <span data-ttu-id="f26e0-144">反対は、ユーザーがテキスト ボックスを終了したときに発生する "ぼかし" イベントです。</span><span class="sxs-lookup"><span data-stu-id="f26e0-144">The opposite is a "blur" event that fires when a user exits a textbox.</span></span> <span data-ttu-id="f26e0-145">上記のイベント ハンドラーは、この場合に緯度と経度のテキスト ボックスの値をクリアし、マップ上の新しい住所の場所をプロットします。</span><span class="sxs-lookup"><span data-stu-id="f26e0-145">The above event handler clears the latitude and longitude textbox values when this happens, and then plots the new address location on our map.</span></span> <span data-ttu-id="f26e0-146">map.js ファイル内で定義したコールバック イベント ハンドラは、指定したアドレスに基づいて仮想アースから返された値を使用して、フォーム上の経度と緯度のテキストボックスを更新します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-146">A callback event handler that we defined within the map.js file will then update the longitude and latitude textboxes on our form using values returned by virtual earth based on the address we gave it.</span></span>

<span data-ttu-id="f26e0-147">そして今、我々は再びアプリケーションを実行し、「ホストディナー」タブをクリックすると、我々は私たちの標準的なDinnerフォーム要素と一緒に表示されるデフォルトのマップが表示されます:</span><span class="sxs-lookup"><span data-stu-id="f26e0-147">And now when we run our application again and click the "Host Dinner" tab we'll see a default map displayed along with our standard Dinner form elements:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

<span data-ttu-id="f26e0-148">住所を入力してタブを離すと、マップが動的に更新されて場所が表示され、イベント ハンドラーは緯度/経度のテキスト ボックスに位置値を設定します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-148">When we type in an address, and then tab away, the map will dynamically update to display the location, and our event handler will populate the latitude/longitude textboxes with the location values:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

<span data-ttu-id="f26e0-149">新しいディナーを保存し、編集のために再度開くと、ページが読み込まれるときにマップの場所が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-149">If we save the new dinner and then open it again for editing, we'll find that the map location is displayed when the page loads:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

<span data-ttu-id="f26e0-150">住所フィールドが変更されるたびに、地図と緯度/経度の座標が更新されます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-150">Every time the address field is changed, the map and the latitude/longitude coordinates will update.</span></span>

<span data-ttu-id="f26e0-151">これで、マップに Dinner の場所が表示されるので、[緯度] フォームフィールドと [経度] フォームフィールドを非表示のテキスト ボックスから非表示の要素に変更することもできます (住所が入力されるたびにマップが自動的に更新されるため)。</span><span class="sxs-lookup"><span data-stu-id="f26e0-151">Now that the map displays the Dinner location, we can also change the Latitude and Longitude form fields from being visible textboxes to instead be hidden elements (since the map is automatically updating them each time an address is entered).</span></span> <span data-ttu-id="f26e0-152">これを行うには、HTML.TextBox() HTML ヘルパーの使用から Html.Hidden() ヘルパー メソッドの使用に切り替えます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-152">To-do this we'll switch from using the Html.TextBox() HTML helper to using the Html.Hidden() helper method:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

<span data-ttu-id="f26e0-153">そして今、私たちのフォームはもう少しユーザーフレンドリーで、生の緯度/経度を表示しないようにします(それでも各 Dinnerをデータベースに保存しています)。</span><span class="sxs-lookup"><span data-stu-id="f26e0-153">And now our forms are a little more user-friendly and avoid displaying the raw latitude/longitude (while still storing them with each Dinner in the database):</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a><span data-ttu-id="f26e0-154">詳細ビューとのマップの統合</span><span class="sxs-lookup"><span data-stu-id="f26e0-154">Integrating the Map with the Details View</span></span>

<span data-ttu-id="f26e0-155">作成および編集のシナリオとマップが統合されたので、詳細シナリオと統合してみましょう。</span><span class="sxs-lookup"><span data-stu-id="f26e0-155">Now that we have the map integrated with our Create and Edit scenarios, let's also integrate it with our Details scenario.</span></span> <span data-ttu-id="f26e0-156">必要なのは% Html.RenderPartial("マップ")を呼び出す&lt;ことだけです。詳細&gt;ビュー内の %</span><span class="sxs-lookup"><span data-stu-id="f26e0-156">All we need to-do is to call &lt;% Html.RenderPartial("map"); %&gt; within the Details view.</span></span>

<span data-ttu-id="f26e0-157">以下は、完全な詳細ビュー(マップ統合を使用)のソースコードがどのようなものかです。</span><span class="sxs-lookup"><span data-stu-id="f26e0-157">Below is what the source code to the complete Details view (with map integration) looks like:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

<span data-ttu-id="f26e0-158">そして今、ユーザーが/Dinners/Details/[id]URL に移動すると、夕食の詳細、地図上のディナーの場所(上にマウスを置くとディナーのタイトルとその住所が表示されるプッシュピンが付いています)が表示され、RSVPへのAJAXリンクがあります。</span><span class="sxs-lookup"><span data-stu-id="f26e0-158">And now when a user navigates to a /Dinners/Details/[id] URL they'll see details about the dinner, the location of the dinner on the map (complete with a push-pin that when hovered over displays the title of the dinner and the address of it), and have an AJAX link to RSVP for it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a><span data-ttu-id="f26e0-159">データベースとリポジトリでのロケーション検索の実装</span><span class="sxs-lookup"><span data-stu-id="f26e0-159">Implementing Location Search in our Database and Repository</span></span>

<span data-ttu-id="f26e0-160">AJAX の実装を終了するには、アプリケーションのホーム ページにマップを追加して、ユーザーが近くのディナーをグラフィカルに検索できるようにします。</span><span class="sxs-lookup"><span data-stu-id="f26e0-160">To finish off our AJAX implementation, let's add a Map to the home page of the application that allows users to graphically search for dinners near them.</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

<span data-ttu-id="f26e0-161">まず、データベースとデータ リポジトリ層内でサポートを実装し、Dinners の場所ベースの半径検索を効率的に実行します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-161">We'll begin by implementing support within our database and data repository layer to efficiently perform a location-based radius search for Dinners.</span></span> <span data-ttu-id="f26e0-162">[SQL 2008 の新しい地理空間機能](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx)を使用してこれを実装することも、代わりに、ここで記事で説明した SQL 関数アプローチを使用することもできます。 [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx)[http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span><span class="sxs-lookup"><span data-stu-id="f26e0-162">We could use the new [geospatial features of SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) to implement this, or alternatively we can use a SQL function approach that Gary Dryden discussed in article here: [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) and Rob Conery blogged about using with LINQ to SQL here: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span></span>

<span data-ttu-id="f26e0-163">この手法を実装するには、Visual Studio 内で "サーバー エクスプ ローラー" を開き、 NerdDinner データベースを選択し、その下にある "関数" サブノードを右クリックし、新しい "スカラー値関数" を作成することを選択します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-163">To implement this technique, we will open the "Server Explorer" within Visual Studio, select the NerdDinner database, and then right-click on the "functions" sub-node under it and choose to create a new "Scalar-valued function":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

<span data-ttu-id="f26e0-164">次の DistanceBetween 関数を貼り付けます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-164">We'll then paste in the following DistanceBetween function:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

<span data-ttu-id="f26e0-165">次に、"NearestDinners" と呼ぶ新しいテーブル値関数を SQL Server に作成します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-165">We'll then create a new table-valued function in SQL Server that we'll call "NearestDinners":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

<span data-ttu-id="f26e0-166">この「NearestDinners」テーブル関数は、DistanceBetween ヘルパー関数を使用して、私たちが提供する緯度と経度から100マイル以内のすべてのディナーを返します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-166">This "NearestDinners" table function uses the DistanceBetween helper function to return all Dinners within 100 miles of the latitude and longitude we supply it:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

<span data-ttu-id="f26e0-167">この関数を呼び出すには、まず 、\Models ディレクトリ内の NerdDinner.dbml ファイルをダブルクリックして、LINQ to SQL デザイナーを開きます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-167">To call this function, we'll first open up the LINQ to SQL designer by double-clicking on the NerdDinner.dbml file within our \Models directory:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

<span data-ttu-id="f26e0-168">次に、NearestDinners 関数と DistanceBetween 関数を LINQ to SQL デザイナーにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="f26e0-168">We'll then drag the NearestDinners and DistanceBetween functions onto the LINQ to SQL designer, which will cause them to be added as methods on our LINQ to SQL NerdDinnerDataContext class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

<span data-ttu-id="f26e0-169">次に、NearestDinner 関数を使用して、指定した場所から 100 マイル以内にある今後のディナーを返す DinnerRepository クラスで"FindByLocation" クエリ メソッドを公開できます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-169">We can then expose a "FindByLocation" query method on our DinnerRepository class that uses the NearestDinner function to return upcoming Dinners that are within 100 miles of the specified location:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a><span data-ttu-id="f26e0-170">JSON ベースの AJAX 検索アクション メソッドの実装</span><span class="sxs-lookup"><span data-stu-id="f26e0-170">Implementing a JSON-based AJAX Search Action Method</span></span>

<span data-ttu-id="f26e0-171">新しい FindByLocation() リポジトリ メソッドを利用して、マップの設定に使用できる Dinner データのリストを返すコントローラー アクション メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-171">We'll now implement a controller action method that takes advantage of the new FindByLocation() repository method to return back a list of Dinner data that can be used to populate a map.</span></span> <span data-ttu-id="f26e0-172">このアクションメソッドは、クライアント上のJavaScriptを使用して簡単に操作できるように、JSON(JavaScriptオブジェクト表記法)形式でディナーデータを返すようにします。</span><span class="sxs-lookup"><span data-stu-id="f26e0-172">We'll have this action method return back the Dinner data in a JSON (JavaScript Object Notation) format so that it can be easily manipulated using JavaScript on the client.</span></span>

<span data-ttu-id="f26e0-173">これを実装するには、\Controllersディレクトリを右クリックし、&gt;コントローラメニューコマンドを選択して、新しい「SearchController」クラスを作成します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-173">To implement this, we'll create a new "SearchController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span> <span data-ttu-id="f26e0-174">次に、次のように新しい SearchController クラス内に "SearchByLocation" アクション メソッドを実装します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-174">We'll then implement a "SearchByLocation" action method within the new SearchController class like below:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

<span data-ttu-id="f26e0-175">検索コントローラーの SearchByLocation アクション メソッドは、内部的に近くのディナーのリストを取得するために DinnerRepository の FindByLocation メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-175">The SearchController's SearchByLocation action method internally calls the FindByLocation method on DinnerRepository to get a list of nearby dinners.</span></span> <span data-ttu-id="f26e0-176">ただし、Dinner オブジェクトをクライアントに直接返すのではなく、代わりに JsonDinner オブジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-176">Rather than return the Dinner objects directly to the client, though, it instead returns JsonDinner objects.</span></span> <span data-ttu-id="f26e0-177">JsonDinnerクラスは、ディナープロパティのサブセットを公開します(たとえば、セキュリティ上の理由から、夕食にRSVPを持っている人の名前は開示されません)。</span><span class="sxs-lookup"><span data-stu-id="f26e0-177">The JsonDinner class exposes a subset of Dinner properties (for example: for security reasons it doesn't disclose the names of the people who have RSVP'd for a dinner).</span></span> <span data-ttu-id="f26e0-178">また、ディナーに存在しない RSVPCount プロパティも含まれており、特定のディナーに関連付けられている RSVP オブジェクトの数をカウントして動的に計算されます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-178">It also includes an RSVPCount property that doesn't exist on Dinner– and which is dynamically calculated by counting the number of RSVP objects associated with a particular dinner.</span></span>

<span data-ttu-id="f26e0-179">次に、コントローラー基本クラスで Json() ヘルパーメソッドを使用して、JSON ベースのワイヤー形式を使用してディナーのシーケンスを返します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-179">We are then using the Json() helper method on the Controller base class to return the sequence of dinners using a JSON-based wire format.</span></span> <span data-ttu-id="f26e0-180">JSON は、単純なデータ構造を表す標準のテキスト形式です。</span><span class="sxs-lookup"><span data-stu-id="f26e0-180">JSON is a standard text format for representing simple data-structures.</span></span> <span data-ttu-id="f26e0-181">次に、2 つの JsonDinner オブジェクトの JSON 形式のリストがアクション メソッドから返された場合の例を示します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-181">Below is an example of what a JSON-formatted list of two JsonDinner objects looks like when returned from our action method:</span></span>

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a><span data-ttu-id="f26e0-182">jQuery を使用して JSON ベースの AJAX メソッドを呼び出す</span><span class="sxs-lookup"><span data-stu-id="f26e0-182">Calling the JSON-based AJAX method using jQuery</span></span>

<span data-ttu-id="f26e0-183">これで、NerdDinner アプリケーションのホーム ページを更新して、SearchController の SearchByLocation アクション メソッドを使用する準備ができました。</span><span class="sxs-lookup"><span data-stu-id="f26e0-183">We are now ready to update the home page of the NerdDinner application to use the SearchController's SearchByLocation action method.</span></span> <span data-ttu-id="f26e0-184">これを行うには、/Views/ホーム/Index.aspxビューテンプレートを開き、テキストボックス、検索ボタン、マップ、およびdinnerListというdiv&lt;&gt;要素を持つテンプレートを更新します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-184">To-do this, we'll open the /Views/Home/Index.aspx view template and update it to have a textbox, search button, our map, and a &lt;div&gt; element named dinnerList:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

<span data-ttu-id="f26e0-185">次に、ページに 2 つの JavaScript 関数を追加できます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-185">We can then add two JavaScript functions to the page:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

<span data-ttu-id="f26e0-186">最初の JavaScript 関数は、ページが最初に読み込まれたときにマップを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-186">The first JavaScript function loads the map when the page first loads.</span></span> <span data-ttu-id="f26e0-187">2 番目の JavaScript 関数は、検索ボタンで JavaScript のクリック イベント ハンドラーをワイヤリングします。</span><span class="sxs-lookup"><span data-stu-id="f26e0-187">The second JavaScript function wires up a JavaScript click event handler on the search button.</span></span> <span data-ttu-id="f26e0-188">ボタンが押されると、Map.jsファイルに追加する FindDinnersGivenLocation() JavaScript 関数を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-188">When the button is pressed it calls the FindDinnersGivenLocation() JavaScript function which we'll add to our Map.js file:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

<span data-ttu-id="f26e0-189">この関数はマップを呼び出します。入力した場所に中央に移動するには、仮想地球コントロール上のFind()を使用します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-189">This FindDinnersGivenLocation() function calls map.Find() on the Virtual Earth Control to center it on the entered location.</span></span> <span data-ttu-id="f26e0-190">仮想アース マップ サービスが戻ると、マップが返されます。Find() メソッドは、最後の引数として渡したコールバック メソッドを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-190">When the virtual earth map service returns, the map.Find() method invokes the callbackUpdateMapDinners callback method we passed it as the final argument.</span></span>

<span data-ttu-id="f26e0-191">メソッドは、実際の作業が行われる場所です。</span><span class="sxs-lookup"><span data-stu-id="f26e0-191">The callbackUpdateMapDinners() method is where the real work is done.</span></span> <span data-ttu-id="f26e0-192">jQuery の $.post() ヘルパー メソッドを使用して、SearchController の SearchByLocation() アクション メソッドに対する AJAX 呼び出しを実行します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-192">It uses jQuery's $.post() helper method to perform an AJAX call to our SearchController's SearchByLocation() action method – passing it the latitude and longitude of the newly centered map.</span></span> <span data-ttu-id="f26e0-193">これは、$.post() ヘルパーメソッドが完了したときに呼び出されるインライン関数を定義し、SearchByLocation() アクションメソッドから返される JSON 形式のディナー結果は、"ディナー" という変数を使用して渡されます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-193">It defines an inline function that will be called when the $.post() helper method completes, and the JSON-formatted dinner results returned from the SearchByLocation() action method will be passed it using a variable called "dinners".</span></span> <span data-ttu-id="f26e0-194">その後、返された各ディナーのforeachを行い、ディナーの緯度と経度やその他のプロパティを使用して、地図に新しいピンを追加します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-194">It then does a foreach over each returned dinner, and uses the dinner's latitude and longitude and other properties to add a new pin on the map.</span></span> <span data-ttu-id="f26e0-195">また、マップの右側にあるディナーの HTML リストにディナーエントリを追加します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-195">It also adds a dinner entry to the HTML list of dinners to the right of the map.</span></span> <span data-ttu-id="f26e0-196">次に、プッシュピンと HTML リストの両方に対してホバー イベントをワイヤアップし、ユーザーがホバーしたときにディナーの詳細が表示されるようにします。</span><span class="sxs-lookup"><span data-stu-id="f26e0-196">It then wires-up a hover event for both the pushpins and the HTML list so that details about the dinner are displayed when a user hovers over them:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

<span data-ttu-id="f26e0-197">そして今、私たちは、アプリケーションを実行し、ホームページにアクセスすると、我々は地図が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-197">And now when we run the application and visit the home-page we'll be presented with a map.</span></span> <span data-ttu-id="f26e0-198">都市の名前を入力すると、マップは近くの今後のディナーを表示します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-198">When we enter the name of a city the map will display the upcoming dinners near it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

<span data-ttu-id="f26e0-199">夕食の上にマウスを置くと、それについての詳細が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f26e0-199">Hovering over a dinner will display details about it.</span></span>

<span data-ttu-id="f26e0-200">バブルまたは HTML リストの右側にある Dinner のタイトルをクリックすると、夕食に移動します。</span><span class="sxs-lookup"><span data-stu-id="f26e0-200">Clicking the Dinner title either in the bubble or on the right-hand side in the HTML list will navigate us to the dinner – which we can then optionally RSVP for:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a><span data-ttu-id="f26e0-201">次の手順</span><span class="sxs-lookup"><span data-stu-id="f26e0-201">Next Step</span></span>

<span data-ttu-id="f26e0-202">これで、NerdDinner アプリケーションのすべてのアプリケーション機能を実装しました。</span><span class="sxs-lookup"><span data-stu-id="f26e0-202">We've now implemented all the application functionality of our NerdDinner application.</span></span> <span data-ttu-id="f26e0-203">それでは、自動単体テストを有効にする方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="f26e0-203">Let's now look at how we can enable automated unit testing of it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f26e0-204">[前へ](use-ajax-to-deliver-dynamic-updates.md)
> [次へ](enable-automated-unit-testing.md)</span><span class="sxs-lookup"><span data-stu-id="f26e0-204">[Previous](use-ajax-to-deliver-dynamic-updates.md)
[Next](enable-automated-unit-testing.md)</span></span>
