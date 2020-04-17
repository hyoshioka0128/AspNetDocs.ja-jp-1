---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: コンボ ボックス コントロールを使用する方法 (C#) |マイクロソフトドキュメント
author: rick-anderson
description: コンボ ボックスは、ユーザーが選択できるオプションのリストとテキスト ボックスの柔軟性を組み合わせたASP.NET AJAX コントロールです。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 2adb9663cb7bdc38f28a127f7932f45a3447d1de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543806"
---
# <a name="how-do-i-use-the-combobox-control-c"></a>コンボ ボックス コントロールを使用する方法 (C#)

[マイクロソフト](https://github.com/microsoft)

> コンボ ボックスは、ユーザーが選択できるオプションのリストとテキスト ボックスの柔軟性を組み合わせたASP.NET AJAX コントロールです。

このチュートリアルの目的は、AJAX コントロール ツールキットコンボ ボックス コントロールについて説明することです。 コンボ ボックスは、標準のASP.NETドロップダウン リスト コントロールとテキスト ボックス コントロールの組み合わせのように機能します。 既存の項目リストから選択するか、新しい項目を入力することができます。

ComboBox はオートコンプリート コントロール エクステンダに似ていますが、コントロールはさまざまなシナリオで使用されます。 オートコンプリート エクステンダは、Web サービスに対して一致するエントリを取得するクエリを実行します。 これに対し、ComboBox コントロールは項目のセットで初期化されます。 オートコンプリート エクステンダを使用すると、コンボ ボックス コントロールを使用しながら、大量のデータ セット (数百万台の自動車部品) を操作する場合に意味があります。

## <a name="selecting-from-a-static-list-of-items"></a>アイテムの静的リストからの選択

コンボ ボックス コントロールの使用の簡単なサンプルから始めましょう。 ドロップダウン リストに項目の静的な一覧を表示するとします。 ただし、リストが完全でない可能性を開いたままにしておきたい場合は、次の手順に示します。 ユーザーがリストにカスタム値を入力できるようにする場合。

新しい web フォーム ページASP.NET作成し、ページでコンボ ボックス コントロールを使用します。 新しいASP.NET ページをプロジェクトに追加し、デザイン ビューに切り替えます。

ページで ComboBox コントロールを使用する場合は、ページに ScriptManager コントロールを追加する必要があります。 ScriptManager コントロールを [AJAX 拡張機能] タブの下からデザイナー画面にドラッグします。 ページの上部に ScriptManager コントロールを追加する必要があります。開いているサーバー側&lt;フォーム&gt;タグのすぐ下に追加できます。

次に、コンボ ボックス コントロールをページにドラッグします。 他の AJAX コントロール ツールキット コントロールとコントロール エクステンダ (図 1 を参照) と共に、ツールボックスで ComboBox コントロールを見つけることができます。

[![名刺を作成するための簡単なフォーム](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**図 01**: ツールボックスから ComboBox コントロールを選択する ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-cs/_static/image2.png)します)

コンボ ボックス コントロールを使用して、選択肢の静的な一覧を表示します。 ユーザーは、マイルド、ミディアム、ホットの 3 つの選択肢から、食品の特定のレベルのスパイシーを選択できます (図 2 参照)。

[![項目の静的リストからの選択](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**図 02**: 項目の静的な一覧から選択する ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-cs/_static/image4.png)して)

これらの選択肢を ComboBox コントロールに追加するには、2 つの方法があります。 まず、デザイン ビューでコントロールの上にマウス を置くときに[オプションの編集]タスク オプションを選択し、アイテム エディタを開きます (図 3 参照)。

[![コンボ ボックス項目の編集](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**図 03**: コンボ ボックス項目の編集 ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-cs/_static/image6.png))

2 番目のオプションは、ソース ビューで、開始と終了&lt;の間の項目の&gt;リストを追加します。 リスト 1 のページには、項目の一覧を含む更新された ComboBox が含まれています。

**リスト 1 - 静的.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

リスト 1 でページを開くと、コンボ ボックスから既存のオプションのいずれかを選択できます。 つまり、コンボ ボックスは、ドロップダウン リスト コントロールと同じように機能します。

ただし、既存のリストにない新しい選択肢 (スーパースパイシーなど) を入力することもできます。 したがって、コンボ ボックスもテキスト ボックス コントロールのように動作します。

既存のアイテムを選択するか、カスタム アイテムを入力するかにかかわらず、フォームを送信すると、選択した項目がラベル コントロールに表示されます。 フォームを送信すると、btnSubmit\_Click ハンドラが実行され、ラベルが更新されます (図 4 参照)。

[![選択した項目の表示](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**図04**: 選択した項目を表示する ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-cs/_static/image8.png))

コンボ ボックス (ComboBox) コントロールは、フォームの送信後に選択した項目を取得するための DropDownList コントロールと同じプロパティをサポートしています。

- 選択項目.テキスト - 選択した項目の Text プロパティの値を表示します。
- SelectedItem.Value - 選択した項目の Value プロパティの値を表示するか、コンボ ボックスに入力されたテキストを表示します。
- 選択値 - このプロパティを使用して、既定の (初期) 選択された項目を指定できる点を除いて、SelectedItem.Value と同じです。

コンボ ボックスにカスタム選択を入力すると、カスタムの選択肢が SelectedItem.Text プロパティと SelectedItem.Value プロパティの両方に割り当てられます。

## <a name="selecting-the-list-of-items-from-the-database"></a>データベースから項目のリストを選択する

コンボ ボックス (ComboBox) コントロールに表示される項目の一覧をデータベースから取得できます。 たとえば、コンボ ボックスを SqlDataSource コントロール、オブジェクトデータ ソース コントロール、LinqDataSource、またはエンティティデータ ソースにバインドできます。

コンボ ボックス (ComboBox) コントロールに映画の一覧を表示するとします。 映画の一覧を Movies データベース テーブルから取得する場合。 次の手順に従います。

1. という名前のページを作成します。
2. ツールボックスの [AJAX 拡張機能] タブの下にあるページに ScriptManager をドラッグして、ScriptManager コントロールをページに追加します。
3. ページにコンボ ボックス (ComboBox) コントロールを追加します。
4. デザイン ビューで、コンボ ボックス コントロールの上にマウス を移動し、[**データ ソースの選択]** タスク オプションを選択します (図 5 参照)。 データ ソース構成ウィザードが起動します。
5. [**データ ソースの選択]** の手順&lt;で、[新&gt;しいデータ ソース] オプションを選択します。
6. [**データ ソースの種類の選択]** ステップで、[データベース] を選択します。
7. [**データ接続の選択]** ステップで、データベース (例: MoviesDB.mdf) を選択します。
8. [**接続文字列をアプリケーション構成ファイルに保存する**] ステップで、接続文字列を保存するオプションを選択します。
9. 「**ステートメントの選択」ステップで**、Movies データベース表を選択し、すべての列を選択します。
10. **[クエリのテスト**] ステップで、[完了] ボタンをクリックします。
11. データ**ソースの選択**手順に戻り、表示するフィールドの [タイトル] 列とデータ フィールドの [Id] 列を選択します (図を参照)。
12. [OK] をクリックしてウィザードを閉じます。

[![データ ソースの選択](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**図 05**: データ ソースの選択 ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-cs/_static/image10.png))

[![データテキストと値フィールドの選択](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**図 06**: データ テキストと値のフィールドを選択する ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-cs/_static/image12.png)して )

上記の手順を完了すると、コンボ ボックスは、ムービー データベース テーブルから映画を表す SqlDataSource コントロールにバインドされます。 ページのソースはリスト 2 のようになります (書式設定を少しクリーンアップしました)。

**リスト 2 - 映画.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

コントロールには、コントロールを指すデータ ソース ID プロパティがあることに注意してください。 ブラウザーでページを開くと、データベースからムービーの一覧が表示されます (図 7 参照)。 リストからムービーを選択するか、または ComboBox にムービーを入力して新しいムービーを入力できます。

[![映画の一覧を表示する](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**図 07**: 動画の一覧を表示する ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-cs/_static/image14.png))

## <a name="setting-the-dropdownstyle"></a>ドロップダウンスタイルの設定

コンボ ボックス の動作を変更するには、コンボ ボックスのドロップダウンスタイルプロパティを使用できます。 このプロパティは、次の値を受け取ります。

- ドロップダウン - (既定値) コンボ ボックス (ComboBox) 矢印をクリックすると、ドロップダウン リストが表示され、カスタム値を入力できます。
- シンプル - コンボボックスは、自動的にドロップダウンリストを表示し、カスタム値を入力することができます。
- ドロップダウン リスト - コンボ ボックスは、ドロップダウン リスト コントロールと同じように機能します。

ドロップダウンとシンプルの違いは、項目のリストが表示される場合です。 Simple の場合、コンボ ボックスにフォーカスを移動すると、すぐにリストが表示されます。 ドロップダウンの場合は、矢印をクリックして項目の一覧を表示する必要があります。

ドロップダウン リストの値を使用すると、コンボ ボックス コントロールは標準のドロップダウン リスト コントロールと同じように動作します。 しかし、ここで重要な違いがあります。 古いバージョンの Internet Explorer では、無限の z インデックスを持つ DropDownList コントロールが表示されるため、コントロールはその前に配置されたコントロールの前に表示されます。 コンボ ボックス&lt;は HTML&gt;&lt;選択&gt;タグの代わりに HTML div タグを表示するため、コンボ ボックスは z の順序を正しく考慮します。

## <a name="setting-the-autocompletemode"></a>オートコンプリートモードの設定

コンボ ボックスのオートコンプリート モード プロパティを使用して、コンボ ボックスにテキストを入力したときに発生する動作を指定します。 このプロパティは、次の値を受け入れます。

- なし - (既定値) コンボ ボックス (ComboBox) はオートコンプリート動作を提供しません。
- 提案 - コンボ ボックス (ComboBox) コントロールは一覧を表示し、一致する項目をリストに強調表示します (図 8 参照)。
- 追加 - ComboBox はリストを表示せず、入力した項目に一致する項目をリストから追加します (図 9 参照)。
- SuggestAppend - コンボ ボックス (ComboBox) コントロールは、リストを表示し、入力した項目に一致する項目をリストから追加します (図 10 参照)。

[![コンボボックスが提案を行います](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**図08**: コンボボックスが提案を行う([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-cs/_static/image16.png))

[![一致するテキストを追加するコンボ ボックス](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**図 09**: ComboBox が一致するテキストを追加します ([フルサイズの画像を表示する をクリック](how-do-i-use-the-combobox-control-cs/_static/image18.png)します)

[![コンボ ボックス (コンボ ボックス) の提案と追加](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**図10**: コンボボックスの提案と追加([フルサイズの画像を表示するをクリック](how-do-i-use-the-combobox-control-cs/_static/image20.png))

## <a name="summary"></a>まとめ

このチュートリアルでは、ComboBox コントロールを使用して、固定された項目のセットを表示する方法を学習しました。 ComboBox コントロールを静的な項目セットとデータベース テーブルの両方にバインドしました。 最後に、コンボ ボックスの動作を変更する方法を学習しました。

> [!div class="step-by-step"]
> [次へ](how-do-i-use-the-combobox-control-vb.md)
