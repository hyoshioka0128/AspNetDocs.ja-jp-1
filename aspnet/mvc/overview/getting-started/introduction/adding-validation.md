---
uid: mvc/overview/getting-started/introduction/adding-validation
title: 検証の追加 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 9f35ca15-e216-4db6-9ebf-24380b0f31b4
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-validation
msc.type: authoredcontent
ms.openlocfilehash: 4e2d83cdff8599d74182da1be1aaabd1a431799c
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044351"
---
# <a name="adding-validation"></a>検証の追加

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

このセクションでは、モデルに検証ロジックを追加 `Movie` し、ユーザーがアプリケーションを使用してムービーを作成または編集しようとするたびに、検証規則が適用されるようにします。

## <a name="keeping-things-dry"></a>ドライを維持する

ASP.NET MVC の核となる設計の原則の1つは、 [ドライ](http://en.wikipedia.org/wiki/Don't_repeat_yourself) ( &quot; DRY 原則 &quot; ) です。 ASP.NET MVC を使用すると、機能または動作を一度だけ指定し、アプリケーション内のすべての場所に反映させることができます。 これにより、記述する必要があるコードの量が減り、記述するコードの記述がエラーを起こしやすくなり、保守が容易になります。

ASP.NET MVC と Entity Framework Code First によって提供される検証のサポートは、ドライの原則が動作する好例です。 (モデルクラス内の) 1 つの場所で検証規則を宣言によって指定すると、アプリケーション内のすべての場所で規則が適用されます。

ムービーアプリケーションでこの検証サポートを利用する方法を見てみましょう。

## <a name="adding-validation-rules-to-the-movie-model"></a>ムービーモデルへの検証規則の追加

まず、検証ロジックをクラスに追加し `Movie` ます。

*Movie.cs* ファイルを開きます。 [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)名前空間にが含まれていないことに注意 `System.Web` してください。 DataAnnotations には、任意のクラスまたはプロパティに宣言して適用できる、組み込みの検証属性セットが用意されています。 (書式設定に役立ち、検証を行わない [データ型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) のような書式属性も含まれています)。

次に、 `Movie` 組み込み [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 、 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)、および検証属性を利用するようにクラスを更新し [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) ます。 クラスを `Movie` 次のように置き換えます。

[!code-csharp[Main](adding-validation/samples/sample1.cs?highlight=5,13-15,18-19,22-23)]

属性は、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 文字列の最大長を設定し、データベースにこの制限を設定するため、データベーススキーマが変更されます。 **サーバーエクスプローラー**で**ムービー**テーブルを右クリックし、[**テーブル定義を開く**] をクリックします。

![](adding-validation/_static/image1.png)

上の図では、すべての文字列フィールドが [NVARCHAR (MAX)](https://technet.microsoft.com/library/ms186939.aspx)に設定されていることがわかります。 ここでは、移行を使用してスキーマを更新します。 ソリューションをビルドし、[ **パッケージマネージャーコンソール** ] ウィンドウを開き、次のコマンドを入力します。

[!code-console[Main](adding-validation/samples/sample2.cmd)]

このコマンドが終了すると、Visual Studio は、指定された名前 () を使用して新しい派生クラスを定義するクラスファイルを開き、 `DbMigration` `DataAnnotations` メソッド内に `Up` スキーマ制約を更新するコードを表示できます。

[!code-csharp[Main](adding-validation/samples/sample3.cs)]

`Genre`フィールドが null 許容ではなくなりました (つまり、値を入力する必要があります)。 `Rating`フィールドの最大長は5で、 `Title` 最大長は60です。 の最小の長さが3で、の `Title` 範囲が `Price` スキーマの変更を作成しませんでした。

ムービースキーマを確認します。

![](adding-validation/_static/image2.png)

文字列フィールドに新しい長さの制限が表示 `Genre` され、null 値を許容するかどうかがチェックされなくなりました。

検証属性では、適用対象のモデル プロパティに適用する動作を指定します。 `Required` および `MinimumLength` 属性は、プロパティに値が必要であることを示します。ただし、この検証を満たすためにユーザーが空白を入力することは禁止されていません。 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)属性は、入力できる文字を制限するために使用されます。 上記のコードで、`Genre` と `Rating` は、文字のみを使用する必要があります (空白、数字、特殊文字は使用できません)。 属性は、 [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 指定された範囲内のに値を制限します。 `StringLength` 属性では、文字列プロパティの最大長を設定でき、オプションとして最小長も設定できます。 値型 (など `decimal, int, float, DateTime` ) は本質的に必須であり、属性を必要としません `Required` 。

Code First により、アプリケーションがデータベースに変更を保存する前に、モデルクラスで指定した検証規則が確実に適用されます。 たとえば、次のコードでは、いくつかの必要なプロパティ値が不足しているため、メソッドが呼び出されたときに [Dbentityvalidationexception](https://msdn.microsoft.com/library/system.data.entity.validation.dbentityvalidationexception(v=vs.103).aspx) 例外がスローされ `SaveChanges` `Movie` ます。

[!code-csharp[Main](adding-validation/samples/sample4.cs)]

上記のコードでは、次の例外がスローされます。

*1つ以上のエンティティの検証に失敗しました。詳細については、' EntityValidationErrors ' プロパティを参照してください。*

.NET Framework によって検証規則が自動的に適用されるため、アプリケーションの堅牢性が向上します。 また、ユーザーが何かを検証することを忘れてしまい、データベースに不適切なデータが誤って格納されることもなくなります。

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC の検証エラー UI

アプリケーションを実行し、 */ムービー* の URL に移動します。

新しいムービーを追加するには、[ **新規作成** ] リンクをクリックします。 フォームに無効な値をいくつか入力します。 jQuery クライアント側の検証でエラーが検出されるとすぐに、エラー メッセージが表示されます。

![8_validationErrors](adding-validation/_static/image3.png)

> [!NOTE]
> 小数点にコンマ (",") を使用する英語以外のロケールの jQuery 検証をサポートするには、このチュートリアルで前述したように、NuGet グローバライズを含める必要があります。

フォームが赤い枠線の色を自動的に使用して、無効なデータを含むテキストボックスが強調表示され、それぞれの横に適切な検証エラーメッセージが出力されていることに注目してください。 エラーは、(JavaScript と jQuery を使用している) クライアント側とサーバー側 (ユーザーが JavaScript を無効にしている場合) の両方に適用されます。

実際の利点は、 `MoviesController` この検証 UI を有効にするため *に、* クラス内の1行のコードを変更する必要がないということです。 このチュートリアルで前に作成したコントローラーとビューにより、`Movie` モデル クラスのプロパティで検証属性を使って指定した検証規則が自動的に取得されます。 `Edit` アクション メソッドを使って検証をテストします。同じ検証が適用されます。

クライアント側の検証エラーがなくなるまで、フォーム データはサーバーに送信されません。 これを確認するには、HTTP Post メソッドにブレークポイントを挿入するか、 [fiddler ツール](http://fiddler2.com/fiddler2/)を使用するか、または IE [F12 開発者ツール](https://msdn.microsoft.com/ie/aa740478)を使用します。

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Create View および Create Action メソッドでの検証の実行方法

コントローラーまたはビューのコードを更新しなくても検証 UI が生成する仕組みが気になるかもしれません。 次の一覧では、クラス内のメソッドがどのように表示されるかを示し `Create` `MovieController` ます。 これらは、このチュートリアルの前の手順で作成した方法から変更されていません。

[!code-csharp[Main](adding-validation/samples/sample5.cs)]

最初の (HTTP GET の) `Create` アクション メソッドは、初期の作成フォームを表示します。 2 番目の (`[HttpPost]`) バージョンは、フォームの送信を処理します。 2番目の `Create` 方法 (バージョン) では、 `HttpPost` ムービーに `ModelState.IsValid` 検証エラーがあるかどうかが確認されます。 このプロパティを取得すると、オブジェクトに適用されているすべての検証属性が評価されます。 オブジェクトに検証エラーがある場合、 `Create` メソッドはフォームを再作成します。 エラーがない場合、メソッドはデータベースに新しいムービーを保存します。 このムービーの例では、 **クライアント側で検証エラーが検出された場合、フォームはサーバーにポストされません。2番目の** `Create` **メソッドは呼び出されません**。 ブラウザーで JavaScript を無効にすると、クライアント検証が無効になり、HTTP POST メソッドによって、 `Create` `ModelState.IsValid` ムービーに検証エラーがあるかどうかが確認されます。

`HttpPost Create` メソッドにブレークポイントを設定し、メソッドが呼び出されないことを確認できます。検証エラーが検出された場合、クライアント側の検証はフォームのデータを送信しません。 ブラウザーで JavaScript を無効にすると、エラーのあるフォームが送信され、ブレークポイントがヒットします。 JavaScript がなくても完全な検証が行われます。 次の図は、Internet Explorer で JavaScript を無効にする方法を示しています。

![](adding-validation/_static/image5.png)

![](adding-validation/_static/image6.png)

次の図では、FireFox ブラウザーで JavaScript を無効にする方法を示します。

![](adding-validation/_static/image7.png)

次の図では、Chrome ブラウザーで JavaScript を無効にする方法を示します。

![](adding-validation/_static/image8.png)

次に示すのは、このチュートリアルの前半でスキャフォールディングした *作成. cshtml* ビューテンプレートです。 これは、前に示した両方のアクション メソッドで、初期フォームの表示と、エラー発生時のフォームの再表示に使われます。

[!code-cshtml[Main](adding-validation/samples/sample6.cshtml?highlight=16-17)]

コードでヘルパーを使用して、 `Html.EditorFor` 各プロパティの要素を出力する方法に注目して `<input>` `Movie` ください。 このヘルパーの横には、ヘルパーメソッドの呼び出しが `Html.ValidationMessageFor` あります。 これらの2つのヘルパーメソッドは、コントローラーによってビュー (この場合はオブジェクト) に渡されるモデルオブジェクトを操作 `Movie` します。 これらは、モデルで指定された検証属性を自動的に検索し、必要に応じてエラーメッセージを表示します。

この方法の非常によい点は、コントローラーも `Create` ビュー テンプレートも、適用される実際の検証規則や、表示される特定のエラー メッセージについて、何も知らないことです。 検証規則とエラー文字列は、`Movie` クラスでのみ指定されています。 同じ検証規則が、`Edit` ビューおよびモデルを編集する他のユーザー作成のビュー テンプレートに、自動的に適用されます。

後で検証ロジックを変更する場合は、検証属性をモデル (この例ではクラス) に追加するだけで、正確に1つの場所で検証を行うことができ `movie` ます。 アプリケーションの異なる部分で規則の適用方法が一貫しない可能性を心配する必要はありません。すべての検証ロジックは 1 か所で定義され、すべての場所で使われます。 これにより、コードの簡潔さが保たれ、簡単に維持や更新できます。 これは、 *ドライ* の原則を完全に受け入れることを意味します。

## <a name="using-datatype-attributes"></a>DataType 属性の使用

*Movie.cs* ファイルを開き、`Movie` クラスを調べます。 名前空間には、 [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 組み込みの検証属性のセットに加えて、書式設定属性が用意されています。 [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)リリース日と価格フィールドに列挙値が既に適用されています。 次のコードは、 `ReleaseDate` `Price` 適切な属性を持つプロパティとプロパティを示して [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) います。

[!code-csharp[Main](adding-validation/samples/sample7.cs)]

[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性は、ビューエンジンがデータを書式設定するためのヒントのみを提供します (また、URL の場合は、 `<a>` 電子メールの場合はなどの属性を提供し `<a href="mailto:EmailAddress.com">` ます)。 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)属性を使用して、データの形式を検証できます。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性は、データベースの組み込み型よりも具体的なデータ型を指定するために使用されます。これらは検証属性では***ありません***。 この例では、追跡する必要があるのは、日付と時刻ではなく、日付のみです。 [DataType 列挙型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)は、 *Date、Time、PhoneNumber、Currency、EmailAddress*など、多くのデータ型に対応しています。 また、`DataType` 属性を使用して、アプリケーションで型固有の機能を自動的に提供することもできます。 たとえば、EmailAddress に `mailto:` 対してリンクを作成[DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)し、[データ型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)に対して日付セレクターを指定することができます。 [HTML5](http://html5.org/)をサポートするブラウザーで日付を指定できます。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性は、html 5 ブラウザーが理解できる html 5[データ](http://ejohn.org/blog/html-5-data-attributes/)("*データダッシュ*" と読みます) 属性を出力します。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性は検証を提供しません。

`DataType.Date` は、表示される日付の書式を指定しません。 既定では、データフィールドは、サーバーの [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)に基づく既定の形式に従って表示されます。

`DisplayFormat` 属性は、日付の書式を明示的に指定するために使用されます。

[!code-csharp[Main](adding-validation/samples/sample8.cs)]

この設定では、 `ApplyFormatInEditMode` 編集のためにテキストボックスに値を表示するときに、指定した書式設定も適用する必要があることを指定します。 (たとえば、通貨値の場合、テキストボックスに通貨記号を編集する必要がないなどの一部のフィールドには必要ありません)。

[Displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性は単独で使用できますが、通常は[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性も使用することをお勧めします。 属性は、 `DataType` 画面に表示する方法とは対照的に、データの *セマンティクス* を伝達します。また、次のような利点があり `DisplayFormat` ます。

- ブラウザーでは、HTML5 機能を有効にすることができます (たとえば、カレンダーコントロール、ロケールに適した通貨記号、電子メールリンクなどを表示します)。
- 既定では、ブラウザーは [ロケール](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)に基づいて正しい形式を使用してデータを表示します。
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性を使用すると、MVC でデータを表示するための適切フィールドテンプレートを選択できます (それ自体で使用されている場合、 [displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)は文字列テンプレートを使用します)。 詳細については、「Brad Wilson の [ASP.NET MVC 2 テンプレート](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)」を参照してください。 (ただし、MVC 2 用に記述されていますが、この記事は現在のバージョンの ASP.NET MVC にも当てはまります)。

日付フィールドで属性を使用する場合は、 `DataType` `DisplayFormat` フィールドが Chrome ブラウザーで正しく表示されるように属性も指定する必要があります。 詳細については、 [この StackOverflow スレッド](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)を参照してください。

> [!NOTE]
> jQuery validation は、 [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 属性と [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)では機能しません。 たとえば、次のコードでは、指定した範囲内の日付であっても、クライアント側の検証エラーが常に表示されます。
> 
> [!code-csharp[Main](adding-validation/samples/sample9.cs)]
> 
> [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)属性と[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)を使用するには、jQuery の日付検証を無効にする必要があります。 一般に、モデルでハード日付をコンパイルすることはお勧めしません。そのため、 [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 属性と [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx) を使用しないことをお勧めします。

次のコードは、1 行で複数の属性を組み合わせる例です。

[!code-csharp[Main](adding-validation/samples/sample10.cs?highlight=4,6,10,12)]

このシリーズの次のパートでは、アプリケーションを確認し、自動的に生成される `Details` および `Delete` メソッドに対していくつかの改良を行います。

> [!div class="step-by-step"]
> [前へ](adding-a-new-field.md)
> [次へ](examining-the-details-and-delete-methods.md)
