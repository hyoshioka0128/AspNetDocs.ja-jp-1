---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
title: 多数のユーザーアカウントを選択するインターフェイスを構築する (VB) |Microsoft Docs
author: rick-anderson
description: このチュートリアルでは、ページ分割されたフィルター可能なグリッドを使用してユーザーインターフェイスを作成します。 特に、ユーザーインターフェイスは、一連のリンクボタンで構成されています。
ms.author: riande
ms.date: 04/01/2008
ms.assetid: da53380c-a16b-41c7-a20d-24343c735c52
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
msc.type: authoredcontent
ms.openlocfilehash: 625e27442c790e7a7228b8f78b8a40dbee8e3b03
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044585"
---
# <a name="building-an-interface-to-select-one-user-account-from-many-vb"></a>多くの中からユーザー アカウントを 1 つ選択するインターフェイスを構築する (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[コードのダウンロード](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.12.zip) または [PDF のダウンロード](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_vb.pdf)

> このチュートリアルでは、ページ分割されたフィルター可能なグリッドを使用してユーザーインターフェイスを作成します。 特に、ユーザーインターフェイスは、ユーザー名の開始文字に基づいて結果をフィルター処理するための一連のリンクボタンと、一致するユーザーを表示する GridView コントロールで構成されています。 まず、GridView のすべてのユーザーアカウントを一覧表示します。 次に、手順3では、[LinkButtons] フィルターを追加します。 手順 4. では、フィルター処理された結果がページングされます。 手順 2. ~ 4. で作成したインターフェイスは、その後のチュートリアルで特定のユーザーアカウントの管理タスクを実行するために使用されます。

## <a name="introduction"></a>概要

<a id="_msoanchor_1"></a>[*ユーザーへのロールの割り当て*](../roles/assigning-roles-to-users-vb.md)に関するチュートリアルでは、管理者がユーザーを選択してロールを管理するための基本的なインターフェイスを作成しました。 具体的には、インターフェイスは、すべてのユーザーのドロップダウンリストを管理者に提示します。 このようなインターフェイスは、ユーザーアカウントが1つしかない場合に適していますが、数百または数千のアカウントを持つサイトでは扱いにくいものです。 ページ分割されたフィルター可能なグリッドは、大規模なユーザーベースを持つ web サイトに適したユーザーインターフェイスです。

このチュートリアルでは、このようなユーザーインターフェイスを作成します。 特に、ユーザーインターフェイスは、ユーザー名の開始文字に基づいて結果をフィルター処理するための一連のリンクボタンと、一致するユーザーを表示する GridView コントロールで構成されています。 まず、GridView のすべてのユーザーアカウントを一覧表示します。 次に、手順3では、[LinkButtons] フィルターを追加します。 手順 4. では、フィルター処理された結果がページングされます。 手順 2. ~ 4. で作成したインターフェイスは、その後のチュートリアルで特定のユーザーアカウントの管理タスクを実行するために使用されます。

それでは始めましょう。

## <a name="step-1-adding-new-aspnet-pages"></a>手順 1: 新しい ASP.NET ページを追加する

このチュートリアルと次の2つでは、管理に関連するさまざまな機能について説明します。 これらのチュートリアル全体で検討したトピックを実装するには、一連の ASP.NET ページが必要です。 これらのページを作成し、サイトマップを更新してみましょう。

まず、という名前のプロジェクトに新しいフォルダーを作成し `Administration` ます。 次に、2つの新しい ASP.NET ページをフォルダーに追加し、各ページをマスターページとリンクし `Site.master` ます。 ページに名前を指定します。

- `ManageUsers.aspx`
- `UserInformation.aspx`

また、web サイトのルートディレクトリにとという2つのページを追加し `ChangePassword.aspx` `RecoverPassword.aspx` ます。

この4つのページには、この時点で2つのコンテンツコントロールが含まれている必要があります。1つは、マスターページの ContentPlaceHolders `MainContent` と `LoginContent` です。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample1.aspx)]

これらのページの ContentPlaceHolder に対して、マスターページの既定のマークアップを表示し `LoginContent` ます。 そのため、コンテンツコントロールの宣言型マークアップを削除し `Content2` ます。 その後、ページのマークアップにはコンテンツコントロールを1つだけ含める必要があります。

フォルダー内の ASP.NET ページ `Administration` は、管理ユーザー専用です。 ロールの作成と管理に関するチュートリアルで、システムに管理者ロールを追加しました <a id="_msoanchor_2"></a> [*Creating and Managing Roles*](../roles/creating-and-managing-roles-vb.md) 。この2つのページへのアクセスをこのロールに制限します。 これを行うには、 `Web.config` フォルダーにファイルを追加 `Administration` し、その要素を構成して `<authorization>` 管理者ロールのユーザーを許可し、他のユーザーを拒否します。

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample2.xml)]

この時点で、プロジェクトのソリューションエクスプローラーは、図1に示すスクリーンショットのようになります。

[![4つの新しいページと Web.config ファイルが Web サイトに追加されました。](building-an-interface-to-select-one-user-account-from-many-vb/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image1.png)

**図 1**: 4 つの新しいページと1つの `Web.config` ファイルが Web サイトに追加された ([クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-vb/_static/image3.png)されます)

最後に、サイトマップ () を更新して、 `Web.sitemap` ページにエントリを追加し `ManageUsers.aspx` ます。 ロールのチュートリアル用に追加した後に、次の XML を追加し `<siteMapNode>` ます。

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample3.xml)]

サイトマップが更新されたら、ブラウザーを使用してサイトにアクセスします。 図2に示すように、左側のナビゲーションには管理チュートリアルの項目が含まれるようになりました。

[![サイトマップには、ユーザー管理という名前のノードが含まれています。](building-an-interface-to-select-one-user-account-from-many-vb/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image4.png)

**図 2**: サイトマップに、[ユーザーの管理] という名前のノードが含まれている ([クリックしてフルサイズの画像を表示する](building-an-interface-to-select-one-user-account-from-many-vb/_static/image6.png))

## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>手順 2: GridView 内のすべてのユーザーアカウントを一覧表示する

このチュートリアルの最終的な目的は、管理者が管理対象のユーザーアカウントを選択できる、ページングされたフィルター処理されたグリッドを作成することです。 まず、GridView の *すべて* のユーザーを一覧表示しましょう。 この操作が完了したら、フィルター処理とページングのインターフェイスと機能を追加します。

フォルダー内のページを開き、 `ManageUsers.aspx` `Administration` gridview を追加します。その後、 `ID` をに設定し `UserAccounts` ます。ここでは、クラスのメソッドを使用して、一連のユーザーアカウントを GridView にバインドするコードを記述し `Membership` `GetAllUsers` ます。 前のチュートリアルで説明したように、メソッドはオブジェクト `GetAllUsers` のコレクションであるオブジェクトを返し `MembershipUserCollection` `MembershipUser` ます。 コレクション内の各には、、、 `MembershipUser` などのプロパティが含まれ `UserName` `Email` `IsApproved` ます。

GridView で目的のユーザーアカウント情報を表示するには、GridView のプロパティを False に設定し、、、およびの `AutoGenerateColumns` 各プロパティに対して、、、およびの各 `UserName` プロパティと CheckBoxFields の boundfields を追加し `Email` `Comment` `IsApproved` `IsLockedOut` `IsOnline` ます。 この構成は、コントロールの宣言型マークアップまたは [フィールド] ダイアログボックスを使用して適用できます。 図3は、[フィールドの自動生成] チェックボックスがオフになっていて、BoundFields と CheckBoxFields が追加および構成された後の [フィールド] ダイアログボックスのスクリーンショットを示しています。

[![3つの BoundFields と3つの CheckBoxFields を GridView に追加します。](building-an-interface-to-select-one-user-account-from-many-vb/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image7.png)

**図 3**: 3 つの boundfields と3つの CheckBoxFields を GridView に追加[する (クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-vb/_static/image9.png)されます)

GridView を構成した後、その宣言型マークアップが次のようになっていることを確認します。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample4.aspx)]

次に、ユーザーアカウントを GridView にバインドするコードを記述する必要があります。 このタスクを実行するという名前のメソッドを作成し、 `BindUserAccounts` `Page_Load` 最初のページにアクセスしたときにイベントハンドラーから呼び出します。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample5.vb)]

ブラウザーでページをテストしてみましょう。 図4に示すように、GridView には、 `UserAccounts` システム内のすべてのユーザーのユーザー名、電子メールアドレス、およびその他の関連するアカウント情報が表示されます。

[![ユーザーアカウントが GridView に一覧表示されます。](building-an-interface-to-select-one-user-account-from-many-vb/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image10.png)

**図 4**: GridView にユーザーアカウントが表示される ([クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-vb/_static/image12.png)されます)

## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>手順 3: ユーザー名の最初の文字で結果をフィルター処理する

現在、 `UserAccounts` GridView には *すべて* のユーザーアカウントが表示されます。 数百または数千のユーザーアカウントを持つ web サイトでは、表示されているアカウントをユーザーがすばやく省いできるようにすることが重要です。 これは、ページにフィルターリンクボタンを追加することによって実現できます。 ページに 27 LinkButtons を追加してみましょう。1つはアルファベットの各文字につき1つの LinkButton です。 ビジターが All LinkButton をクリックすると、GridView にすべてのユーザーが表示されます。 ユーザーが特定の文字をクリックすると、ユーザー名が選択した文字で始まるユーザーのみが表示されます。

最初のタスクでは、27 LinkButton コントロールを追加します。 1つの方法として、27リンクボタンを宣言によって一度に1つ作成する方法があります。 より柔軟な方法は、LinkButton をレンダリングするを持つ Repeater コントロールを使用して、 `ItemTemplate` フィルター処理オプションを配列としてリピータにバインドすることです `String` 。

まず、GridView の上のページに Repeater コントロールを追加し `UserAccounts` ます。 Repeater のプロパティを設定して、 `ID` `FilteringUI` `ItemTemplate` `Text` と `CommandName` プロパティが現在の配列要素にバインドされている LinkButton をレンダリングするようにリピータのテンプレートを構成します。 ユーザーへのロールの割り当てに関するチュートリアルで説明したように <a id="_msoanchor_3"></a> [*Assigning Roles to Users*](../roles/assigning-roles-to-users-vb.md) 、これは databinding 構文を使用して実現でき `Container.DataItem` ます。 `SeparatorTemplate`各リンクの間に垂直線を表示するには、Repeater を使用します。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample6.aspx)]

このリピータに必要なフィルター処理オプションを設定するには、という名前のメソッドを作成し `BindFilteringUI` ます。 `Page_Load`最初のページの読み込み時に、イベントハンドラーからこのメソッドを呼び出すようにしてください。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample7.vb)]

このメソッドは、配列内の各要素について、配列内の要素としてフィルター処理オプションを指定し `String` `filterOptions` ます。 Repeater は、 `Text` `CommandName` 配列要素の値に割り当てられたプロパティとプロパティを使用して LinkButton をレンダリングします。

図5は、 `ManageUsers.aspx` ブラウザーを使用して表示するときのページを示しています。

[![リピータには、27フィルターリンクボタンが一覧表示されます。](building-an-interface-to-select-one-user-account-from-many-vb/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image13.png)

**図 5**: リピータは、27フィルターリンクボタンを一覧表示しています ([クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-vb/_static/image15.png)されます)

> [!NOTE]
> ユーザー名は、数字や句読点を含む任意の文字で始めることができます。 これらのアカウントを表示するために、管理者は All LinkButton オプションを使用する必要があります。 または、LinkButton を追加して、番号で始まるすべてのユーザーアカウントを返すこともできます。 この作業をリーダーの演習として残しておきます。

フィルターリンクボタンのいずれかをクリックすると、ポストバックが発生し、リピータのイベントが発生し `ItemCommand` ますが、結果をフィルター処理するコードをまだ記述していないため、グリッドは変わりません。 クラスには、ユーザー `Membership` 名が指定した検索パターンに一致するユーザーアカウントを返す[ `FindUsersByName` メソッド](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx)が含まれています。 このメソッドを使用すると、ユーザー名が、クリックされたフィルター選択された LinkButton ので指定された文字で始まるユーザーアカウントだけを取得でき `CommandName` ます。

まず、 `ManageUser.aspx` ページの分離コードクラスを更新して、このプロパティにプロパティが含まれるようにし `UsernameToMatch` ます。このプロパティには、ポストバック間でユーザー名フィルター文字列が保持されます。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample8.vb)]

プロパティは、 `UsernameToMatch` `ViewState` キー ' UsernameToMatch ' を使用してコレクションに割り当てられている値を格納します。 このプロパティの値が読み込まれると、コレクション内に値が存在するかどうかが確認されます。存在し `ViewState` ない場合は、既定値である空の文字列が返されます。 プロパティは、共通のパターンを示してい `UsernameToMatch` ます。つまり、プロパティに対する変更がポストバック間で保持されるように、状態を表示するための値を保持します。 このパターンの詳細については、「 [ASP.NET ビューステート](https://msdn.microsoftn-us/library/ms972976.aspx)について」を参照してください。

次に、を呼び出すのではなく、を呼び出し `BindUserAccounts` `Membership.GetAllUsers` `Membership.FindUsersByName` 、 `UsernameToMatch` SQL のワイルドカード文字 (%) を付加してプロパティの値を渡すように、メソッドを更新します。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample9.vb)]

ユーザー名が A で始まるユーザーだけを表示するには、プロパティをに設定し `UsernameToMatch` てを呼び出し `BindUserAccounts` ます。これにより、ユーザー名がで `Membership.FindUsersByName("A%")` 始まるすべてのユーザーが返されます。同様に、 *すべて* のユーザーを返すには、 `UsernameToMatch` メソッドが呼び出されるように、プロパティに空の文字列を割り当て `BindUserAccounts` `Membership.FindUsersByName("%")` て、その結果、すべてのユーザーアカウントを返します。

リピータのイベントのイベントハンドラーを作成 `ItemCommand` します。 このイベントは、フィルターリンクボタンの1つがクリックされたときに発生します。クリックされた LinkButton の `CommandName` 値がオブジェクトを介して渡され `RepeaterCommandEventArgs` ます。 プロパティに適切な値を割り当て `UsernameToMatch` てから、メソッドを呼び出す必要があり `BindUserAccounts` ます。 が All の場合は `CommandName` 、 `UsernameToMatch` すべてのユーザーアカウントが表示されるように、に空の文字列を割り当てます。 それ以外の場合は、 `CommandName` 値をに割り当てます。 `UsernameToMatch`

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample10.vb)]

このコードを使用して、フィルター処理機能をテストします。 ページに最初にアクセスしたときに、すべてのユーザーアカウントが表示されます (図5を参照)。 A LinkButton をクリックすると、ポストバックが発生し、結果がフィルター処理されて、で始まるユーザーアカウントのみが表示されます。

[![[フィルターリンク] ボタンを使用して、ユーザー名が特定の文字で始まるユーザーを表示します。](building-an-interface-to-select-one-user-account-from-many-vb/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image16.png)

**図 6**: [フィルターリンク] ボタンを使用して、ユーザー名が特定の文字で始まるユーザーを表示する ([クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-vb/_static/image18.png)されます)

## <a name="step-4-updating-the-gridview-to-use-paging"></a>手順 4: ページングを使用するように GridView を更新する

図5および6に示されている GridView には、メソッドから返されるすべてのレコードが一覧表示され `FindUsersByName` ます。 数百または数千のユーザーアカウントがある場合は、すべてのアカウントを表示すると情報が過負荷になる可能性があります (すべての LinkButton をクリックした場合や、最初にページにアクセスしたときに発生した場合のように)。 より管理しやすいチャンクでユーザーアカウントを表示するには、一度に10個のユーザーアカウントを表示するように GridView を構成してみましょう。

GridView コントロールでは、次の2種類のページングが提供されます。

- **既定のページング** -実装は簡単ですが、非効率的です。 簡単に言うと、既定のページングでは、GridView はデータソースの *すべて* のレコードを想定しています。 次に、適切なレコードのページのみが表示されます。
- **カスタムページング** -実装にはより多くの作業が必要ですが、既定のページングよりも効率的です。これは、カスタムページングでは、表示するレコードの正確なセットのみを返すためです。

既定のページングとカスタムページングのパフォーマンスの違いは、何千ものレコードをページングする場合に非常に大きくなる可能性があります。 このインターフェイスは、数百または数千のユーザーアカウントがあると仮定して構築されているため、カスタムページングを使用します。

> [!NOTE]
> 既定のページングとカスタムページングの違い、およびカスタムページングの実装に関連する課題の詳細については、「 [大量のデータを効率的にページング](https://asp.net/learn/data-access/tutorial-25-vb.aspx)する」を参照してください。 既定のページングとカスタムページングのパフォーマンスの違いの分析については、「 [SQL Server 2005 を使用した ASP.NET のカスタムページング](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)」を参照してください。

カスタムページングを実装するには、まず、GridView によって表示されるレコードの正確なサブセットを取得するためのメカニズムが必要です。 幸いにも、 `Membership` クラスのメソッドには、 `FindUsersByName` ページインデックスとページサイズを指定できるオーバーロードがあり、その範囲内にあるユーザーアカウントのみが返されます。

特に、このオーバーロードには次のシグネチャがあり [`FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)`](https://msdn.microsoft.com/library/fa5st8b2.aspx) ます。

*PageIndex*パラメーターは、返されるユーザーアカウントのページを指定します。*pageSize*は、1ページあたりに表示するレコードの数を示します。 *Totalrecords*パラメーターは、 `ByRef` ユーザーストア内のユーザーアカウントの合計数を返すパラメーターです。

> [!NOTE]
> によって返されるデータ `FindUsersByName` は、ユーザー名で並べ替えられます。並べ替えの基準はカスタマイズできません。

GridView は、ObjectDataSource コントロールにバインドされている場合にのみ、カスタムページングを使用するように構成できます。 ObjectDataSource コントロールでカスタムページングを実装するには、開始行インデックスと表示するレコードの最大数を渡す2つの方法が必要です。また、そのスパン内に含まれるレコードの詳細なサブセットを返します。およびは、ページングされているレコードの合計数を返すメソッドです。 オーバーロードは、 `FindUsersByName` ページインデックスとページサイズを受け入れ、パラメーターを使用してレコードの合計数を返し `ByRef` ます。 ここでは、インターフェイスが一致していません。

1つの方法として、ObjectDataSource が想定するインターフェイスを公開するプロキシクラスを作成してから、メソッドを内部的に呼び出し `FindUsersByName` ます。 この記事で使用するもう1つの方法として、独自のページングインターフェイスを作成し、GridView の組み込みページングインターフェイスではなくそれを使用する方法があります。

### <a name="creating-a-first-previous-next-last-paging-interface"></a>最初、前、次、最後のページングインターフェイスを作成する

最初、前、次のリンクボタンと最後のリンクボタンを使用して、ページングインターフェイスを作成してみましょう。 最初の LinkButton がクリックされると、ユーザーはデータの最初のページに移動しますが、Previous は前のページに戻ります。 同様に、[次へ] と [最後] では、ユーザーをそれぞれ次のページと最後のページに移動します。 GridView の下に4つの LinkButton コントロールを追加し `UserAccounts` ます。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample11.aspx)]

次に、LinkButton の各イベントのイベントハンドラーを作成し `Click` ます。

図7は、Visual Web Developer デザインビューを通じて表示する場合の4つの LinkButtons を示しています。

[![GridView の下に、First、Previous、Next、および Last LinkButtons を追加します。](building-an-interface-to-select-one-user-account-from-many-vb/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image19.png)

**図 7**: GridView の下に First、Previous、Next、および Last linkbuttons を追加[する (クリックすると、フルサイズのイメージが表示](building-an-interface-to-select-one-user-account-from-many-vb/_static/image21.png)されます)

### <a name="keeping-track-of-the-current-page-index"></a>現在のページインデックスを追跡する

ユーザーが最初にページにアクセスする `ManageUsers.aspx` か、いずれかのフィルターボタンをクリックすると、GridView に最初のデータページが表示されます。 ただし、ユーザーがナビゲーションリンクボタンのいずれかをクリックしたときに、ページインデックスを更新する必要があります。 ページインデックスとページごとに表示するレコード数を維持するには、次の2つのプロパティをページの分離コードクラスに追加します。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample12.vb)]

プロパティと同様に、 `UsernameToMatch` `PageIndex` プロパティはその値をビューステートに永続化します。 読み取り専用プロパティは、ハードコーディングされた `PageSize` 値10を返します。 このプロパティを更新してと同じパターンを使用し、ページに `PageIndex` `ManageUsers.aspx` アクセスするユーザーがページごとに表示するユーザーアカウントの数を指定できるようにするには、関心のある読者を招待します。

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>現在のページのレコードだけを取得し、ページインデックスを更新し、ページングインターフェイスリンクボタンを有効または無効にします。

ページングインターフェイスが配置され、 `PageIndex` プロパティとプロパティが追加されたので `PageSize` 、 `BindUserAccounts` 適切なオーバーロードを使用するようにメソッドを更新する準備ができました `FindUsersByName` 。 また、表示されるページに応じて、このメソッドでページングインターフェイスを有効または無効にする必要があります。 データの最初のページを表示する場合は、最初のリンクと前のリンクを無効にする必要があります。最後のページを表示する場合は、[次へ] と [最後] を無効にする必要があります。

`BindUserAccounts` メソッドを次のコードで更新します。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample13.vb)]

ページングされるレコードの合計数は、メソッドの最後のパラメーターによって決定されることに注意 `FindUsersByName` してください。 指定されたページのユーザーアカウントが返された後、データの最初のページまたは最後のページが表示されているかどうかに応じて、4つのリンクボタンが有効または無効になります。

最後の手順では、4つの LinkButtons イベントハンドラーのコードを記述し `Click` ます。 これらのイベントハンドラーは、プロパティを更新 `PageIndex` した後、 `BindUserAccounts` First、Previous、および Next の各イベントハンドラーの呼び出しを使用して、GridView にデータを再バインドする必要があります。 ただし、最後の `Click` LinkButton のイベントハンドラーは少し複雑になります。これは、最後のページインデックスを決定するために表示されるレコードの数を確認する必要があるためです。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample14.vb)]

図8と9は、カスタムページングインターフェイスが動作していることを示しています。 図8は、 `ManageUsers.aspx` すべてのユーザーアカウントの最初のデータページを表示するときのページを示しています。 表示されるのは、13個のアカウントのうち10個だけであることに注意してください。 次のリンクまたは最後のリンクをクリックすると、ポストバックが発生し、が1に更新され、 `PageIndex` ユーザーアカウントの2番目のページがグリッドにバインドされます (図9を参照)。

[![最初の10個のユーザーアカウントが表示されます。](building-an-interface-to-select-one-user-account-from-many-vb/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image22.png)

**図 8**: 最初の10個のユーザーアカウントが表示される ([クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-vb/_static/image24.png)されます)

[![次のリンクをクリックすると、ユーザーアカウントの2ページ目が表示されます。](building-an-interface-to-select-one-user-account-from-many-vb/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image25.png)

**図 9**: 次のリンクをクリックすると、ユーザーアカウントの2ページ目が表示されます ([クリックすると、フルサイズの画像が表示](building-an-interface-to-select-one-user-account-from-many-vb/_static/image27.png)されます)

## <a name="summary"></a>まとめ

管理者は、多くの場合、アカウントの一覧からユーザーを選択する必要があります。 前のチュートリアルでは、ユーザーに設定されたドロップダウンリストの使用について説明しましたが、この方法はうまくいきません。 このチュートリアルでは、結果がページングされた GridView に表示されるフィルター可能なインターフェイスである、より優れた代替方法について説明します。 このユーザーインターフェイスを使用すると、管理者は数千単位で1つのユーザーアカウントをすばやく効率的に検索して選択できます。

プログラミングを楽しんでください。

### <a name="further-reading"></a>もっと読む

このチュートリアルで説明しているトピックの詳細については、次のリソースを参照してください。

- [SQL Server 2005 を使用した ASP.NET のカスタムページング](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [大量のデータを効率的にページングする](https://asp.net/learn/data-access/tutorial-25-vb.aspx)
- [独自の Web サイト管理ツールのロール](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>著者について

1998以降、Microsoft の Web テクノロジを使用して、Scott Mitchell (複数の ASP/創設者4GuysFromRolla.com の執筆者) が Microsoft の Web テクノロジを使用しています。 Scott は、独立したコンサルタント、トレーナー、およびライターとして機能します。 彼の最新の書籍は *[、ASP.NET 2.0 を24時間以内に教え](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ています。 Scott は [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 、またはブログでにアクセスでき [http://ScottOnWriting.NET](http://scottonwriting.net/) ます。

### <a name="special-thanks-to"></a>ありがとうございました。

このチュートリアルシリーズは、役に立つ多くのレビュー担当者によってレビューされました。 このチュートリアルのリードレビューアーは Alicja Maziarz でした。 今後の MSDN 記事を確認することに興味がありますか? その場合は、の行をドロップします。

> [!div class="step-by-step"]
> [前へ](unlocking-and-approving-user-accounts-cs.md)
> [次へ](recovering-and-changing-passwords-vb.md)
