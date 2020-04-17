---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: CRUD (作成、読み取り、更新、削除) データフォームエントリのサポートを提供 |マイクロソフトドキュメント
author: rick-anderson
description: 手順 5 では、Dinners クラスを編集、作成、およびディナーを削除するためのサポートを有効にして、DinnersController クラスをさらに進める方法を示します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 2b75a7eda8bce4baa25d92626639f4d904eb363a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542626"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>CRUD (作成、読み取り、更新、削除) データ フォーム エントリ サポートを提供する

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、MVC 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)ASP.NETの手順 5 です。
> 
> 手順 5 では、Dinners クラスを編集、作成、およびディナーを削除するためのサポートを有効にして、DinnersController クラスをさらに進める方法を示します。
> 
> mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>NerdDinner ステップ 5: フォームのシナリオを作成、更新、削除する

コントローラーとビューを導入し、それらを使用して、Dinners のサイトでのリスト/詳細エクスペリエンスを実装する方法について説明しました。 次のステップは、DinnersController クラスをさらに進めて、Dinners の編集、作成、および削除のサポートも有効にすることです。

### <a name="urls-handled-by-dinnerscontroller"></a>ディナーコントローラによって処理される URL

以前は、2 つの URL のサポートを実装した DinnersController にアクション メソッドを追加しました: */Dinners*と */Dinners/詳細/[id]*。

| **URL** | **動詞** | **目的** |
| --- | --- | --- |
| */ディナー/* | GET | 今後のディナーの HTML リストを表示します。 |
| */ディナー/詳細/[id]* | GET | 特定のディナーに関する詳細を表示します。 |

次に、3 つの URL を実装するアクション メソッドを追加します: */Dinners/Edit/[id]* *、/ディナー/作成*、および */Dinners/Delete/[id]*。 これらの URL により、既存のディナーの編集、新しいディナーの作成、ディナーの削除がサポートされます。

これらの新しい URL と HTTP GET と HTTP POST の両方の動詞の相互作用をサポートします。 これらの URL に対する HTTP GET 要求は、データの最初の HTML ビュー ("編集" の場合は Dinner データが入力されたフォーム、「作成」の場合は空白のフォーム、削除の場合は削除確認画面) を表示します。 これらの URL に対する HTTP POST 要求は、Dinner リポジトリ (およびそこからデータベース) のディナー データを保存/更新/削除します。

| **URL** | **動詞** | **目的** |
| --- | --- | --- |
| */ディナー/編集/[id]* | GET | Dinner データが設定された編集可能な HTML フォームを表示します。 |
| POST | 特定の Dinner のフォームの変更をデータベースに保存します。 |
| */ディナー/作成* | GET | ユーザーが新しいディナーを定義できる空の HTML フォームを表示します。 |
| POST | 新しい Dinner を作成し、データベースに保存します。 |
| */ディナー/削除/[id]* | GET | 削除確認画面を表示します。 |
| POST | 指定されたディナーをデータベースから削除します。 |

### <a name="edit-support"></a>サポートの編集

まず、「編集」シナリオを実装します。

#### <a name="the-http-get-edit-action-method"></a>HTTP-GET 編集アクション メソッド

まず、編集アクションメソッドの HTTP "GET" 動作を実装します。 このメソッドは *、/Dinners/Edit/[id]* URL が要求されたときに呼び出されます。 実装は次のようになります。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

上記のコードでは、Dinner リポジトリを使用して Dinner オブジェクトを取得しています。 次に、Dinner オブジェクトを使用してビュー テンプレートをレンダリングします。 テンプレート名を*View()* ヘルパー メソッドに明示的に渡していないので、ビュー テンプレートを解決するために、規則ベースの既定のパスを使用します。

次に、このビュー テンプレートを作成します。 これは、Edit メソッド内で右クリックし、コンテキスト メニューの [ビューの追加] をクリックして行います。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

[ビューの追加] ダイアログでは、Dinner オブジェクトをモデルとしてビュー テンプレートに渡すことを示し、"Edit" テンプレートを自動スキャフォールディングすることを選択します。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

[追加] ボタンをクリックすると、Visual Studio は "\ビュー\Dinners" ディレクトリ内に新しい "Edit.aspx" ビュー テンプレート ファイルを追加します。 また、コード エディター内の新しい "Edit.aspx" ビュー テンプレートが開きます 。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

生成されるデフォルトの「編集」スキャフォールドに対していくつかの変更を加え、編集ビューテンプレートを更新して以下の内容を含めます (これは、公開したくないプロパティの一部を削除します)。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

アプリケーションを実行して *"/ディナー/編集/1"URL*をリクエストすると、次のページが表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

ビューで生成される HTML マークアップは、次のようになります。 標準の HTML- "&lt;保存&gt;"&lt;入力タイプ ="submit"/&gt;ボタンが押されたときに *、/Dinners/Edit/1* URL に HTTP POST を実行するフォーム要素を使用します。 HTML&lt;入力タイプ="text"/&gt;要素は、編集可能な各プロパティに対して出力されています。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.BeginForm() および Html.TextBox() Html ヘルパー メソッド

"Edit.aspx" ビュー テンプレートは、いくつかの "Html ヘルパー" メソッドを使用しています。 これらのヘルパー メソッドは、HTML マークアップを生成するだけでなく、組み込みのエラー処理と検証のサポートも提供します。

##### <a name="htmlbeginform-helper-method"></a>ヘルパー メソッド

Html.BeginForm() ヘルパー メソッドは、マークアップで&lt;&gt; HTML フォーム要素を出力するものです。 Edit.aspx ビュー テンプレートでは、このメソッドを使用するときに C# の using ステートメントを適用していることに気付くでしょう。 &lt;左中かっこはフォーム&gt;のコンテンツの先頭を示し、右中かっこは&lt;/form&gt;要素の終わりを示します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

または、このようなシナリオで「using」ステートメントのアプローチが不自然である場合は、Html.BeginForm() と Html.EndForm() の組み合わせを使用できます (これは同じことを行います)。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

パラメータを指定せずに Html.BeginForm() を呼び出すと、現在の要求の URL に HTTP-POST を実行するフォーム要素が出力されます。 そのため、編集ビューでは*&lt;フォーム アクション=""ディナー/編集/1" メソッド ="post" 要素&gt;が*生成されます。 別の URL に投稿する場合は、Html.BeginForm() に明示的なパラメータを渡す必要があります。

##### <a name="htmltextbox-helper-method"></a>ヘルパー メソッド

Edit.aspx ビューでは、Html.TextBox() ヘルパー メソッド&lt;を使用して入力タイプ="text"/&gt;要素を出力します。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

上記の Html.TextBox() メソッドは&lt;、1 つのパラメータを受け取り、出力する入力タイプ="text"/&gt;要素の id/name 属性と、テキストボックス値を設定するモデル プロパティの両方を指定するために使用されます。 たとえば、編集ビューに渡した Dinner オブジェクトには ".NET Futures" という "Title" プロパティ値が含まれるため、Html.TextBox("title") メソッド呼び出し出力:*&lt;入力 id="title" name="title" タイプ&gt;="text" 値 ="NET Futures" /*.

または、最初の Html.TextBox() パラメータを使用して要素の id/name を指定し、2 番目のパラメータとして使用する値を明示的に渡すことができます。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

出力される値に対してカスタム書式を実行する場合も多くあります。 Net に組み込まれた String.Format() 静的メソッドは、これらのシナリオに役立ちます。 Edit.aspx ビュー テンプレートは、この値を使用して、日時の秒数が表示されないように EventDate 値 (DateTime 型) を書式設定しています。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

Html.TextBox() の 3 番目のパラメータは、オプションで追加の HTML 属性を出力するために使用できます。 以下のコード スニペットは、追加の size="30" 属性と、入力型="text"/&lt;&gt;要素に対する class="mycssclass" 属性をレンダリングする方法を示しています。 クラス属性の名前をエスケープする方法に注意してください" クラス@" character because "" は C# の予約キーワードです。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>HTTP-POST 編集アクション メソッドの実装

これで、EDIT アクション メソッドの HTTP-GET バージョンが実装されました。 ユーザーが */Dinners/Edit/1* URL を要求すると、次のような HTML ページが表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

"Save" ボタンを押すと、フォームが */Dinners/Edit/1* URL にポストされ、HTTP POST 動詞を使用して HTML&lt;入力&gt;フォームの値が送信されます。 それでは、Dinnerの保存を処理する編集アクションメソッドのHTTP POST動作を実装しましょう。

まず、HTTP POST シナリオを処理することを示す "AcceptVerbs" 属性を持つ DinnersController に、オーバーロードされた "Edit" アクション メソッドを追加します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

オーバーロードされたアクション メソッドに [AcceptVerbs] 属性が適用されると、ASP.NET MVC は、着信 HTTP 動詞に応じて、適切なアクション メソッドへのディスパッチ要求を自動的に処理します。 */Dinners/Edit/[id]* URL への HTTP POST 要求は上記の Edit メソッドに送信され *、/Dinners/Edit/[id]* URL への他のすべての HTTP 動詞要求は、実装した最初の`[AcceptVerbs]`Edit メソッド (属性を持たない) に移動します。

| **サイドトピック: なぜ HTTP 動詞を介して差別化するのですか?** |
| --- |
| あなたは尋ねるかもしれません - なぜ私たちは単一のURLを使用し、HTTP動詞を介してその動作を区別するのですか? 編集変更の読み込みと保存を処理する URL を 2 つ別に持つのはなぜですか? たとえば、/Dinners/Edit/[id]は最初のフォームを表示し、/Dinners/Save/[id]はフォームポストを処理して保存しますか? 2 つの別々の URL を公開する場合の欠点は、/Dinners/Save/2 に投稿し、入力エラーのために HTML フォームを再表示する必要がある場合、エンド ユーザーはブラウザーのアドレス バーに /Dinners/Save/2 URL を持つことになります (フォームが投稿された URL であるため)。 エンドユーザーがこの再表示されたページをブラウザのお気に入りリストにブックマークしたり、URL をコピー/ペーストして友人にメールした場合、今後は動作しない URL を保存することになります (その URL は投稿値に依存するため)。 単一の URL (/Dinners/Edit/[id]など) を公開し、HTTP 動詞で処理を区別することで、エンドユーザーが編集ページをブックマークしたり、URL を他のユーザーに送信したりしても安全です。 |

#### <a name="retrieving-form-post-values"></a>フォームポスト値の取得

HTTP POST "Edit" メソッド内で、投稿されたフォームパラメータにアクセスする方法はさまざまです。 簡単な方法の 1 つは、Controller 基本クラスの Request プロパティを使用してフォーム コレクションにアクセスし、ポストされた値を直接取得することです。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

ただし、上記のアプローチは、特にエラー処理ロジックを追加すると、少し冗長です。

このシナリオの優れたアプローチは、コント ローラーの基本クラスに組み込みの*UpdateModel()* ヘルパー メソッドを活用することです。 これは、受信フォームのパラメータを使用して渡すオブジェクトのプロパティの更新をサポートしています。 リフレクションを使用してオブジェクトのプロパティ名を決定し、クライアントから送信された入力値に基づいて値を自動的に変換して値を割り当てます。

このコードを使用して HTTP-POST 編集アクションを簡略化するために UpdateModel() メソッドを使用できます。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

今、私たちは *、/ディナー/編集/1* URLを訪問し、私たちの夕食のタイトルを変更することができます:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

[保存] ボタンをクリックすると、編集アクションにフォームポストが実行され、更新された値がデータベースに保存されます。 その後、夕食の詳細 URL にリダイレクトされます (新しく保存された値が表示されます)。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>編集エラーの処理

現在の HTTP-POST 実装は、エラーがある場合を除いて正常に動作します。

ユーザーがフォームの編集を間違えた場合は、フォームを修正するための情報を示すエラー メッセージがフォームに再表示されることを確認する必要があります。 これには、エンドユーザーが不正な入力 (例: 不正な形式の日付文字列) を投稿するケースや、入力形式が有効であるがビジネス ルール違反がある場合が含まれます。 エラーが発生した場合、ユーザーが最初に入力した入力データをフォームに保存して、変更を手動で再入力する必要がないようにする必要があります。 このプロセスは、フォームが正常に完了するまで、必要に応じて何度も繰り返す必要があります。

ASP.NETMVCには、エラー処理とフォームの再表示を容易にする優れた組み込み機能がいくつか含まれています。 これらの機能を実際に表示するには、次のコードを使用して Edit アクション メソッドを更新します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

上記のコードは、以前の実装と似ていますが、現在は try/catch エラー処理ブロックをラップしています。 UpdateModel() を呼び出すときに例外が発生した場合、または DinnerRepository を保存しようとすると (この場合、保存しようとしている Dinner オブジェクトがモデル内のルール違反により無効な場合は例外が発生します)、キャッチ エラー処理ブロックが実行されます。 その中で、Dinner オブジェクトに存在するルール違反をループし、ModelState オブジェクトに追加します (これについては後で説明します)。 その後、ビューを再表示します。

この作業を見て、アプリケーションを再実行し、Dinnerを編集し、空のタイトル、"BOGUS"のEventDateを持つ、米国の国の値を持つ英国の電話番号を使用するように変更してみましょう。 "Save" ボタンを押すと、HTTP POST Edit メソッドは(エラーがあるため)Dinner を保存できないため、フォームを再表示します。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

私たちのアプリケーションは、まともなエラー経験を持っています。 無効な入力を含むテキスト要素は赤色で強調表示され、検証エラー メッセージがエンド ユーザーに表示されます。 フォームは、ユーザーが最初に入力した入力データを保持しているため、何も補充する必要はありません。

どのように、あなたは尋ねるかもしれない、これは起こったのですか? タイトル、EventDate、および ContactPhone のテキストボックスは、どのようにして赤でハイライトされ、最初に入力されたユーザー値を出力する方法を知っていますか? そして、エラーメッセージは、一番上のリストにどのように表示されますか? 良いニュースは、これは魔法によって起こらなかったということです - むしろ、入力検証とエラー処理シナリオを容易にする組み込みのASP.NETMVC機能のいくつかを使用したためです。

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>モデル状態と検証 HTML ヘルパー メソッドについて

コント ローラー クラスには、ビューに渡されるモデル オブジェクトにエラーが存在することを示す方法を提供する"ModelState" プロパティ コレクションがあります。 ModelState コレクション内のエラー エントリは、問題があるモデル プロパティの名前 ("Title"、"EventDate"、"ContactPhone"など) を識別し、人間にわかりやすいエラー メッセージを指定できるようにします (たとえば、「タイトルが必要です」)。

モデル オブジェクトのプロパティにフォーム値を割り当てようとしたときに、エラーが発生すると *、UpdateModel()* ヘルパー メソッドによって ModelState コレクションが自動的に設定されます。 たとえば、Dinner オブジェクトの EventDate プロパティの型は、DateTime です。 上記のシナリオで UpdateModel() メソッドが文字列値 "BOGUS" を割り当てることができなかった場合、UpdateModel() メソッドは、そのプロパティで割り当てエラーが発生したことを示すエントリを ModelState コレクションに追加しました。

開発者は、Dinner オブジェクトのアクティブなルール違反に基づくエントリを ModelState コレクションに設定する"catch" エラー処理ブロック内で以下のように、ModelState コレクションに明示的にエラー エントリを追加するコードを記述することもできます。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>モデル状態との Html ヘルパー統合

HTML ヘルパー メソッド ( Html.TextBox() など ) は、出力をレンダリングするときに ModelState コレクションをチェックします。 アイテムにエラーが存在する場合、ユーザーが入力した値と CSS エラー クラスがレンダリングされます。

たとえば、"編集" ビューでは、Html.TextBox() ヘルパー メソッドを使用して、Dinner オブジェクトの EventDate をレンダリングします。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

ビューがエラー シナリオでレンダリングされると、Html.TextBox() メソッドは、Dinner オブジェクトの "EventDate" プロパティに関連付けられたエラーがあるかどうかを確認するために ModelState コレクションをチェックしました。 エラーがあると判断すると、送信されたユーザー入力(「BOGUS」)が値としてレンダリングされ&lt;、cssエラークラスが入力タイプ="textbox"/&gt;マークアップに追加されました。

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

css エラークラスの外観をカスタマイズして、希望する外観にすることができます。 既定の CSS エラー クラスである "入力検証エラー" は *、\content\site.css*スタイルシートで定義されており、次のようになります。

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

この CSS ルールは、無効な入力要素が次のように強調表示される原因となります。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>ヘルパー メソッド

ヘルパー メソッド Html.ValidationMessage() を使用して、特定のモデル プロパティに関連付けられた ModelState エラー メッセージを出力できます。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

上記のコード出力: * &lt;span クラス ="フィールド検証エラー"&gt;値 'BOGUS'&lt;は無効です /span&gt;*

Html.ValidationMessage() ヘルパー メソッドは、開発者が表示されるエラー テキスト メッセージをオーバーライドできるようにする 2 番目のパラメーターもサポートしています。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

上記のコード出力: EventDate プロパティにエラーが存在する場合、既定のエラー テキストの代わりに*&lt;span class="フィールド検証エラー"&gt;\*&lt;/span&gt;* です。

##### <a name="htmlvalidationsummary-helper-method"></a>ヘルパー メソッド

Html.ValidationSummary() ヘルパー メソッドを使用すると、概要エラー メッセージを表示し、ModelState&gt;&lt;コレクション内&gt;のすべての詳細なエラー メッセージの一覧を&lt;ul&gt;&lt;li//ul に表示できます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

Html.ValidationSummary() ヘルパー メソッドは、詳細なエラーの一覧の上に表示する概要エラー メッセージを定義する、省略可能な文字列パラメーターを受け取ります。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

オプションで CSS を使用して、エラーリストの表示をオーバーライドできます。

#### <a name="using-a-addruleviolations-helper-method"></a>ヘルパー メソッドの使用

最初の HTTP-POST Edit 実装では、catch ブロック内で foreach ステートメントを使用して、Dinner オブジェクトのルール違反をループし、コントローラの ModelState コレクションに追加しました。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

このコードを少し簡潔にするため、NerdDinner プロジェクトに "ControllerHelpers" クラスを追加し、mvc ModelStateDictionary クラス ASP.NETにヘルパー メソッドを追加する "AddRule違反" 拡張メソッドを実装します。 この拡張メソッドは、ルール違反エラーの一覧を使用して ModelState ディクショナリを設定するために必要なロジックをカプセル化できます。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

その後、HTTP-POST Edit アクション メソッドを更新して、この拡張メソッドを使用して、ModelState コレクションにディナー ルール違反を設定できます。

#### <a name="complete-edit-action-method-implementations"></a>編集アクションメソッドの実装の完了

以下のコードは、編集シナリオに必要なすべてのコントローラー ロジックを実装します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

Edit の実装の良いところは、Controller クラスも View テンプレートも、Dinner モデルによって適用される特定の検証やビジネス ルールについて何も知っている必要がないことです。 将来的にはモデルにルールを追加することができ、それらをサポートするためにコントローラやビューにコード変更を加える必要はありません。 これにより、将来のアプリケーション要件を最小限のコード変更で容易に進化させる柔軟性が得られます。

### <a name="create-support"></a>サポートの作成

DinnersController クラスの "編集" 動作の実装が完了しました。 次に、ユーザーが新しい Dinners を追加できるようにする"Create"サポートを実装します。

#### <a name="the-http-get-create-action-method"></a>HTTP-GET 作成アクション メソッド

まず、作成アクション メソッドの HTTP "GET" 動作を実装します。 このメソッドは、他のユーザーが */Dinners/CREATE* URL にアクセスしたときに呼び出されます。 実装は次のようになります。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

上記のコードは、新しい Dinner オブジェクトを作成し、その EventDate プロパティを 1 週間後に割り当てます。 次に、新しい Dinner オブジェクトに基づくビューをレンダリングします。 *View()* ヘルパー メソッドに名前を明示的に渡していないので、ビュー テンプレートを解決するために、規則ベースの既定のパスを使用します。

次に、このビュー テンプレートを作成します。 これは、Create アクションメソッド内で右クリックし、「ビューの追加」コンテキストメニューコマンドを選択することで行うことができます。 [ビューの追加] ダイアログでは、Dinner オブジェクトをビュー テンプレートに渡すことを示し、"Create" テンプレートを自動スキャフォールディングすることを選択します。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

[追加] ボタンをクリックすると、新しいスキャフォールド ベースの "Create.aspx" ビューが "\Views\Dinners" ディレクトリに保存され、IDE 内で開きます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

生成されたデフォルトの"create"スキャフォールディングファイルに変更を加え、次のように変更してみましょう。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

そして今、私たちのアプリケーションを実行し、ブラウザ内で *「/Dinners /Create」URL*にアクセスすると、Createアクションの実装から以下のようなUIがレンダリングされます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>HTTP-POST 作成アクション メソッドの実装

CREATE アクション メソッドの HTTP-GET バージョンが実装されています。 ユーザーが [保存] ボタンをクリックすると、フォームのポストを実行して *、/Dinners/CREATE* URL を&lt;作成&gt;し、HTTP POST 動詞を使用して HTML 入力フォームの値を送信します。

次に、アクション作成メソッドの HTTP POST 動作を実装しましょう。 まず、HTTP POST シナリオを処理することを示す "AcceptVerbs" 属性を持つ DinnersController に、オーバーロードされた "Create" アクション メソッドを追加します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

HTTP-POST が有効な "Create" メソッド内のポストされたフォーム パラメーターにアクセスするには、さまざまな方法があります。

1 つの方法は、新しい Dinner オブジェクトを作成し *、UpdateModel()* ヘルパー メソッドを使用することです (Edit アクションで行ったように) ポストされたフォーム値を設定します。 その後、DinnerRepository に追加し、データベースに永続化し、以下のコードを使用して新しく作成された Dinner を表示するために、ユーザーを詳細アクションにリダイレクトします。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

代わりに、Create() アクションメソッドがメソッドパラメータとして Dinner オブジェクトを受け取るアプローチを使用することもできます。 ASP.NETMVC は自動的に新しい Dinner オブジェクトをインスタンス化し、フォーム入力を使用してそのプロパティを設定し、アクション メソッドに渡します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

上記のアクション メソッドは、ModelState.IsValid プロパティをチェックして、Dinner オブジェクトにフォームポスト値が正常に設定されたことを確認します。 入力変換の問題 (EventDate プロパティの "BOGUS" の文字列など) がある場合、この値は false を返し、何らかの問題がある場合はアクション メソッドがフォームを再表示します。

入力値が有効な場合、アクション メソッドは新しい Dinner を追加して DinnerRepository に保存しようとします。 この処理は try/catch ブロック内でラップされ、ビジネス ルール違反が発生した場合にフォームを再表示します (これにより、dinnerRepository.Save() メソッドが例外を発生させます)。

このエラー処理の動作を確認するには *、/Dinners/CREATE* URL をリクエストし、新しい Dinner の詳細を入力します。 入力または値が正しくないと、次のように強調表示されたエラーで作成フォームが再表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

作成フォームが編集フォームとまったく同じ検証とビジネス ルールを遵守していることに注目してください。 これは、検証ルールとビジネス ルールがモデルで定義され、アプリケーションの UI またはコントローラに埋め込まれなかったためです。 つまり、検証やビジネス ルールを 1 か所で変更/進化させ、アプリケーション全体に適用できることを意味します。 新しいルールや既存のルールの変更を自動的に反映するために、Edit または Create アクションメソッド内のコードを変更する必要はありません。

入力値を修正し、再度 [保存] ボタンをクリックすると、DinnerRepository への追加が成功し、新しい Dinner がデータベースに追加されます。 その後、新しく作成されたディナーの詳細が表示されます *。./Dinners/Details/[id]URL*にリダイレクトされます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>サポートの削除

それでは、DinnersController に "削除" サポートを追加しましょう。

#### <a name="the-http-get-delete-action-method"></a>HTTP-GET 削除アクション メソッド

まず、削除アクション メソッドの HTTP GET 動作を実装します。 このメソッドは、誰かが */Dinners/Delete/[id]* URL にアクセスしたときに呼び出されます。 実装は次のとおりです。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

アクション メソッドは、削除する Dinner の取得を試みます。 Dinner が存在する場合は、Dinner オブジェクトに基づいてビューがレンダリングされます。 オブジェクトが存在しない場合 (または既に削除されている場合)、"Details" アクション メソッド用に作成した "NotFound" ビュー テンプレートをレンダリングするビューが返されます。

Delete アクションメソッド内で右クリックし、「ビューの追加」コンテキストメニューコマンドを選択することで、「削除」ビューテンプレートを作成できます。 [ビューの追加] ダイアログでは、Dinner オブジェクトをモデルとしてビュー テンプレートに渡すことを示し、空のテンプレートを作成することを選択します。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

[追加] ボタンをクリックすると、Visual Studio は "\Views\Dinners" ディレクトリ内に新しい "Delete.aspx" ビュー テンプレート ファイルを追加します。 テンプレートに HTML とコードを追加して、次のような削除確認画面を実装します。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

上記のコードは、削除する Dinner のタイトルを表示し、エンド&lt;ユーザー&gt;がその中の [削除] ボタンをクリックした場合に POST を実行するフォーム要素を /Dinners/Delete/[id] URL に出力します。

アプリケーションを実行し、有効な Dinner オブジェクトの *"/Dinners/Delete/[id]"* URL にアクセスすると、次のように UI がレンダリングされます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **サイドトピック:なぜ私たちはPOSTを行っているのですか?** |
| --- |
| あなたは尋ねるかもしれません - なぜ私たちは削除確認画面で&lt;フォーム&gt;を作成する努力をしましたか? 実際の削除操作を実行するアクション メソッドにリンクするには、標準のハイパーリンクを使用してみませんか。 その理由は、Web クローラや検索エンジンが URL を検出し、リンクをたどったときにデータが誤って削除されるのを防ぐように注意する必要があるためです。 HTTP-GET ベースの URL は、アクセス/クロールが安全であると見なされ、HTTP-POST の URL に従わないことを想定しています。 適切なルールは、常に、HTTP-POST 要求の背後に破壊的な操作やデータ変更操作を配置することです。 |

#### <a name="implementing-the-http-post-delete-action-method"></a>HTTP-POST 削除アクション メソッドの実装

削除確認画面を表示する削除アクションメソッドの HTTP-GET バージョンが実装されました。 エンドユーザーが「削除」ボタンをクリックすると *、/Dinners/Dinner/[id]URL*にフォームポストが実行されます。

次のコードを使用して、削除アクション メソッドの HTTP "POST" 動作を実装してみましょう。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

削除アクション メソッドの HTTP-POST バージョンは、削除するディナー オブジェクトを取得しようとします。 (既に削除されているため) 見つからない場合は、"NotFound" テンプレートがレンダリングされます。 Dinner が見つかった場合は、Dinner リポジトリから削除されます。 その後、「削除済み」テンプレートをレンダリングします。

"削除済み" テンプレートを実装するには、アクション メソッドを右クリックし、[ビューの追加] コンテキスト メニューを選択します。 ビューに "Deleted" という名前を付け、空のテンプレートにします (厳密に型指定されたモデル オブジェクトは受け取りません)。 その後、HTML コンテンツを追加します。

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

そして今、私たちは、アプリケーションを実行し、有効なDinnerオブジェクトの *「/ディナー/削除/[id]」URL*にアクセスすると、次のような私たちの夕食の削除確認画面が表示されます:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

「削除」ボタンをクリックすると *、/Dinners/Delete/[id]URL*に対してHTTP-POSTが実行され、データベースからディナーが削除され、「削除済み」ビューテンプレートが表示されます。

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>モデル バインド セキュリティ

ASP.NET MVC の組み込みのモデル バインド機能を使用する 2 つの異なる方法について説明しました。 最初に UpdateModel() メソッドを使用して既存のモデル オブジェクトのプロパティを更新し、2 つ目は mvc のサポート ASP.NETを使用してアクション メソッド パラメーターとしてモデル オブジェクトを渡します。 これらの技術の両方が非常に強力で非常に便利です。

この力はまた、それに責任をもたらします。 ユーザー入力を受け入れる際には常にセキュリティについて妄想することが重要であり、オブジェクトをバインドして入力を行う場合も同様です。 HTML や JavaScript のインジェクション攻撃を避けるために、ユーザーが入力した値を常に HTML エンコードし、SQL インジェクション攻撃に注意する必要があります (注: LINQ to SQL を使用して、これらの種類の攻撃を防ぐためにパラメーターを自動的にエンコードします)。 クライアント側の検証だけに頼ることはなく、サーバー側の検証を常に使用して、偽の値を送信しようとするハッカーを防ぐ必要があります。

ASP.NET MVC のバインディング機能を使用する際に考える追加のセキュリティ項目の 1 つは、バインドするオブジェクトのスコープです。 具体的には、バインドを許可するプロパティのセキュリティへの影響を理解し、エンド ユーザーが実際に更新できるプロパティのみを更新できるようにする必要があります。

デフォルトでは、UpdateModel() メソッドは、入力フォームのパラメーター値に一致するモデル オブジェクトのすべてのプロパティを更新しようとします。 同様に、アクションメソッドのパラメータとして渡されるオブジェクトは、デフォルトで、フォームパラメータを介してすべてのプロパティを設定できます。

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>使用ごとにバインドをロックダウンする

バインディング ポリシーは、更新可能なプロパティの明示的な "include list" を提供することで、使用ごとにロックダウンできます。 これは、次のような UpdateModel() メソッドに追加の文字列配列パラメータを渡すことによって行うことができます。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

アクション メソッドのパラメーターとして渡されるオブジェクトは、次のように指定できるプロパティの "include list" を有効にする [Bind] 属性もサポートします。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>型ベースでのバインドのロック

また、バインディング規則をタイプごとにロックダウンすることもできます。 これにより、バインド規則を一度指定し、すべてのコントローラーとアクション メソッドのすべてのシナリオ (UpdateModel とアクション メソッドのパラメーター の両方のシナリオを含む) で適用できます。

型ごとのバインド規則は、型に [Bind] 属性を追加するか、またはアプリケーションの Global.asax ファイル内に登録することでカスタマイズできます (型を所有していないシナリオに便利です)。 その後、Bind 属性の Include プロパティと Exclude プロパティを使用して、特定のクラスまたはインターフェイスにバインドできるプロパティを制御できます。

NerdDinner アプリケーションの Dinner クラスにこのテクニックを使用し、バインド可能なプロパティのリストを次に制限する [Bind] 属性を追加します。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

RSVPs コレクションをバインディングを介して操作することは許可されておらず、また、DinnerID または HostedBy プロパティをバインディングによって設定することも許可していないことに注意してください。 セキュリティ上の理由から、アクションメソッド内の明示的なコードを使用してこれらの特定のプロパティを操作するだけです。

### <a name="crud-wrap-up"></a>CRUDラップアップ

ASP.NET MVC には、フォームの投稿シナリオの実装に役立つ多くの組み込み機能が含まれています。 これらの機能を使用して、DinnerRepository の上に CRUD UI サポートを提供しました。

アプリケーションを実装するために、モデルに焦点を当てたアプローチを使用しています。 つまり、すべての検証とビジネス ルールロジックは、コントローラやビューではなく、モデルレイヤー内で定義されます。 当社のコントローラクラスもビューテンプレートも、Dinnerモデルクラスによって施行されている特定のビジネスルールについて何も知りません。

これにより、アプリケーション アーキテクチャがクリーンな状態に保ち、テストが容易になります。 将来的には、モデルレイヤーにビジネスルールを追加することができ、それらをサポートするためにコントローラまたはビューに*コード変更を加える必要はありません*。 これにより、将来的にアプリケーションを進化させ、変更するための多くの俊敏性が提供されます。

DinnersController は、ディナーリスト/詳細を有効にし、サポートの作成、編集、削除を行うようになりました。 クラスの完全なコードは以下にあります。

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>次の手順

DinnersController クラス内に基本的な CRUD (作成、読み取り、更新、および削除) のサポート実装が用意されました。

次に、ViewData クラスと ViewModel クラスを使用して、フォーム上の UI をさらに豊かにする方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [次へ](use-viewdata-and-implement-viewmodel-classes.md)
