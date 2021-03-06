---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: キャッシュ |マイクロソフトドキュメント
author: rick-anderson
description: キャッシュの理解は、パフォーマンスの高いアプリケーションのASP.NETにとって重要です。 ASP.NET 1.x では、キャッシュ用に 3 つの異なるオプションが提供されました。出力キャッシュ,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: a199a9c0352dfb054e8d4e5e67652db9bd38851c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542938"
---
# <a name="caching"></a>キャッシュ

[マイクロソフト](https://github.com/microsoft)

> キャッシュの理解は、パフォーマンスの高いアプリケーションのASP.NETにとって重要です。 ASP.NET 1.x では、キャッシュ用に 3 つの異なるオプションが提供されました。出力キャッシュ、フラグメント キャッシュ、およびキャッシュ API を使用します。

キャッシュの理解は、パフォーマンスの高いアプリケーションのASP.NETにとって重要です。 ASP.NET 1.x では、キャッシュ用に 3 つの異なるオプションが提供されました。出力キャッシュ、フラグメント キャッシュ、およびキャッシュ API を使用します。 ASP.NET 2.0 ではこれら 3 つのメソッドすべてが提供されますが、いくつかの重要な追加機能が追加されています。 いくつかの新しいキャッシュ依存関係があり、開発者はカスタムキャッシュの依存関係を作成するオプションを持つようになりました。 キャッシュの構成もASP.NET 2.0 で大幅に改善されました。

## <a name="new-features"></a>新機能

## <a name="cache-profiles"></a>キャッシュ プロファイル

キャッシュ プロファイルを使用すると、開発者は、個々のページに適用できる特定のキャッシュ設定を定義できます。 たとえば、12 時間後にキャッシュから有効期限が切れるページがある場合、それらのページに適用できるキャッシュ プロファイルを簡単に作成できます。 新しいキャッシュ プロファイルを追加するには、&lt;構成ファイルの&gt;outputCacheSettings セクションを使用します。 たとえば、次の例は *、2day*というキャッシュ プロファイルの構成で、キャッシュ期間を 12 時間に設定します。

[!code-xml[Main](caching/samples/sample1.xml)]

このキャッシュ プロファイルを特定のページに適用するには、次に示すように@ OutputCache ディレクティブの CacheProfile 属性を使用します。

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>カスタム キャッシュの依存関係

ASP.NET 1.x 開発者は、カスタム キャッシュの依存関係を求めて発言しました。 ASP.NET 1.x では、CacheDependency クラスがシールされ、開発者が独自のクラスを派生させることができなかった。 ASP.NET 2.0 では、この制限は削除され、開発者は独自のカスタム キャッシュ依存関係を自由に開発できます。 CacheDependency クラスを使用すると、ファイル、ディレクトリ、またはキャッシュ キーに基づいてカスタム キャッシュ依存関係を作成できます。

たとえば、次のコードは、Web アプリケーションのルートにある stuff.xml というファイルに基づいて、新しいカスタム キャッシュ依存関係を作成します。

[!code-csharp[Main](caching/samples/sample3.cs)]

このシナリオでは、stuff.xml ファイルが変更されると、キャッシュされた項目は無効になります。

キャッシュ キーを使用してカスタム キャッシュ依存関係を作成することもできます。 このメソッドを使用すると、キャッシュ キーを削除すると、キャッシュされたデータが無効になります。 次の例を使って説明します。

[!code-csharp[Main](caching/samples/sample4.cs)]

上記の項目を無効にするには、キャッシュキーとして機能するようにキャッシュに挿入された項目を削除します。

[!code-csharp[Main](caching/samples/sample5.cs)]

キャッシュ キーとして機能する項目のキーは、キャッシュ キーの配列に追加される値と同じである必要があります。

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>ポーリングベースの SQL キャッシュ依存関係 (テーブルベースの依存関係とも呼ばれます)

SQL Server 7 および 2000 では、SQL キャッシュの依存関係にポーリング ベースのモデルを使用します。 ポーリング ベースのモデルでは、テーブル内のデータが変更されたときにトリガーされるデータベース テーブルのトリガーを使用します。 このトリガーは、定期的にチェックASP.NET通知テーブルの**changeId**フィールドを更新します。 **changeId**フィールドが更新された場合、ASP.NETはデータが変更されたことを認識し、キャッシュされたデータを無効にします。

> [!NOTE]
> SQL Server 2005 ではポーリング ベースのモデルを使用することもできますが、ポーリング ベースのモデルは最も効率的なモデルではないため、SQL Server 2005 ではクエリ ベースのモデル (後述) を使用することをお勧めします。

ポーリング ベースのモデルを使用する SQL キャッシュ依存関係が正しく機能するためには、テーブルで通知が有効になっている必要があります。 これは、プログラムで\_実行できます。

次のコマンド ラインは、SQL キャッシュ依存関係の*dbase*という名前の SQL Server インスタンスにある Northwind データベースに Products テーブルを登録します。

[!code-console[Main](caching/samples/sample6.cmd)]

上記のコマンドで使用されるコマンド ライン スイッチの説明を次に示します。

| **コマンド ライン スイッチ** | **目的** |
| --- | --- |
| -S *server* | サーバー名を指定します。 |
| -ed | データベースで SQL キャッシュ依存関係を有効にすることを指定します。 |
| -d *\_データベース名* | SQL キャッシュの依存関係を有効にする必要があるデータベース名を指定します。 |
| -E | データベースに接続するときに\_aspnet regsql が Windows 認証を使用するように指定します。 |
| -et | SQL キャッシュの依存関係に対してデータベース テーブルを有効にすることを指定します。 |
| -t *\_テーブル名* | SQL キャッシュの依存関係を有効にするデータベース テーブルの名前を指定します。 |

> [!NOTE]
> aspnet\_regsql.exe には、他にもスイッチがあります。 完全なリストについては、aspnet\_regsql.exe を実行してください 。? コマンド ラインから。

このコマンドを実行すると、SQL Server データベースに次の変更が加えられます。

- テーブルが追加されました。 **\_** このテーブルには、SQL キャッシュ依存関係が有効になっているデータベースのテーブルごとに 1 行が含まれます。
- 次のストアド プロシージャは、データベース内に作成されます。

| \_ストアド プロシージャ | テーブルを\_照会し、SQL キャッシュ依存関係に対して有効になっているすべてのテーブルと各テーブルの変更 ID の値を返します。 このストアド プロシージャは、データが変更されたかどうかを判断するポーリングに使用されます。 |
| --- | --- |
| \_ストアド プロシージャ | テーブルを照会して SQL キャッシュ依存関係に対応したすべてのテーブルを返し\_、SQL キャッシュ依存関係に対して有効なすべてのテーブルを返します。 |
| \_ストアド プロシージャ | 通知テーブルに必要なエントリを追加して、SQL キャッシュ依存関係のテーブルを登録し、トリガーを追加します。 |
| ストアド\_プロシージャ | 通知テーブルのエントリを削除して、SQL キャッシュ依存関係のテーブルの登録を解除し、トリガーを削除します。 |
| \_ストアド プロシージャ | 変更されたテーブルの changeId をインクリメントして通知テーブルを更新します。 ASP.NETはこの値を使用して、データが変更されたかどうかを判断します。 以下に示すように、このストアド プロシージャは、テーブルが有効なときに作成されたトリガーによって実行されます。 |

- **_テーブル\__ 名\_と\_\_** 呼ばれる SQL Server トリガー AspNet SqlCache通知トリガーがテーブルに作成されます。 このトリガーは、テーブルに\_対して挿入、更新、または削除が実行されたときにストアド プロシージャを実行します。
- **ASPNet\_変更通知\_受信通知のみアクセス**と呼ばれる SQL Server ロールがデータベースに追加されます。

**ASPNet\_変更通知\_受信通知のみアクセス**SQL サーバー ロールは、ASPNet\_SqlCache ポーリング ストアド プロシージャに対する EXEC アクセス許可を持っています。 ポーリング モデルが正しく動作するには、プロセス アカウントを aspnet\_変更通知\_受信通知のみアクセス ロールに追加する必要があります。 aspnet\_regsql.exe ツールは、この操作を行いません。

### <a name="configuring-polling-based-sql-cache-dependencies"></a>ポーリング ベースの SQL キャッシュ依存関係の構成

ポーリング ベースの SQL キャッシュの依存関係を構成するために必要な手順がいくつかあります。 最初の手順は、上記で説明したように、データベースとテーブルを有効にすることです。 その手順が完了すると、構成の残りの部分は次のようになります。

- ASP.NET構成ファイルを構成する。
- を設定します。

### <a name="configuring-the-aspnet-configuration-file"></a>ASP.NET構成ファイルの構成

前の&lt;モジュールで説明したように接続文字列を追加するだけでなく、次に示すように sqlCacheDependency&gt;&lt;&gt;要素を使用してキャッシュ要素を構成する必要があります。

[!code-xml[Main](caching/samples/sample7.xml)]

この構成により *、pubs*データベースに対する SQL キャッシュの依存関係が有効になります。 sqlCacheDependency&lt;&gt;要素のポーリング時間属性は、既定で 60000 ミリ秒または 1 分に設定されることに注意してください。 (この値は 500 ミリ秒未満にすることはできません。この例では、add&lt;&gt;要素は新しいデータベースを追加し、pollTime をオーバーライドして 9000000 ミリ秒に設定します。

#### <a name="configuring-the-sqlcachedependency"></a>を設定します。

次の手順では、SqlCache 依存関係を構成します。 これを実現する最も簡単な方法は、@ Outcache ディレクティブで SqlDependency 属性の値を次のように指定することです。

[!code-aspx[Main](caching/samples/sample8.aspx)]

上記の @ OutputCache ディレクティブでは *、pubs*データベースの*authors*テーブルに対して SQL キャッシュ依存関係が構成されています。 複数の依存関係は、次のようにセミコロンで区切って設定できます。

[!code-aspx[Main](caching/samples/sample9.aspx)]

SqlCacheDependency を構成するもう 1 つの方法は、プログラムで行う方法です。 次のコードは *、pubs*データベースの*authors*テーブルに新しい SQL キャッシュ依存関係を作成します。

[!code-csharp[Main](caching/samples/sample10.cs)]

SQL キャッシュ依存関係をプログラムで定義する利点の 1 つは、発生する可能性のある例外を処理できることです。 たとえば、通知が有効になっていないデータベースに対して SQL キャッシュ依存関係を定義しようとすると **、例外が**スローされます。 その場合は **、SqlCacheDependencyAdmin.EnableNotifications**メソッドを呼び出してデータベース名を渡すことで、データベースの通知を有効にしようとすることができます。

同様に、通知が有効になっていないテーブルに対して SQL キャッシュ依存関係を定義しようとすると、**テーブルが**スローされます。 その**後、データベース**名とテーブル名を渡すメソッドを呼び出すことができます。

次のコード サンプルは、SQL キャッシュの依存関係を構成するときに例外処理を適切に構成する方法を示しています。

[!code-csharp[Main](caching/samples/sample11.cs)]

詳細:[https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>クエリ ベースの SQL キャッシュの依存関係 (SQL Server 2005 のみ)

SQL キャッシュの依存関係に SQL Server 2005 を使用する場合、ポーリング ベースのモデルは必要ありません。 SQL Server 2005 で SQL Server 2005 を使用すると、SQL Server 2005 クエリ通知を使用して SQL Server インスタンスへの SQL 接続を介して直接 SQL キャッシュの依存関係が通信します (これ以上の構成は必要ありません)。

クエリ ベースの通知を有効にする最も簡単な方法は、データ ソース オブジェクトの**SqlCacheDependency**属性を**CommandNotification**に設定し **、EnableCaching**属性を**true**に設定することで宣言的に有効にすることです。 このメソッドを使用すると、コードは必要ありません。 データ ソースに対して実行されたコマンドの結果が変更されると、キャッシュ データが無効になります。

次の例では、SQL キャッシュの依存関係に対してデータ ソース コントロールを構成します。

[!code-aspx[Main](caching/samples/sample12.aspx)]

この場合 **、SelectCommand**で指定されたクエリが、最初とは異なる結果を返す場合、キャッシュされた結果は無効になります。

また、 **@ OutputCache**ディレクティブの**SqlDependency**属性を**CommandNotification**に設定することで、すべてのデータ ソースが SQL キャッシュの依存関係に対して有効にされるように指定することもできます。 以下の例は、これを示しています。

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> SQL Server 2005 でのクエリ通知の詳細については、SQL Server オンライン ブックを参照してください。

クエリ ベースの SQL キャッシュ依存関係を構成するもう 1 つの方法は、SqlCacheDependency クラスを使用してプログラムで行う方法です。 次のコード サンプルは、これを実現する方法を示しています。

[!code-csharp[Main](caching/samples/sample14.cs)]

詳細:[https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>キャッシュ後置換

ページをキャッシュすると、Web アプリケーションのパフォーマンスが大幅に向上します。 ただし、キャッシュするページの大部分と、ページ内の一部のフラグメントを動的にする必要がある場合もあります。 たとえば、一定期間完全に静的なニュース記事のページを作成する場合、ページ全体をキャッシュするように設定できます。 ページリクエストごとに変更された回転広告バナーを含める場合は、広告を含むページの一部を動的にする必要があります。 ページをキャッシュして、一部のコンテンツを動的に置換できるようにするには、キャッシュ後の置換ASP.NET使用できます。 ポストキャッシュ置換では、ページ全体がキャッシュ対象外としてマークされた特定の部分でキャッシュされます。 広告バナーの例では、AdRotator コントロールを使用すると、キャッシュ後の置換を利用して、ユーザーごとに動的に作成され、ページの更新ごとに広告を動的に作成できます。

キャッシュ後置換を実装する方法は 3 つあります。

- 宣言的に、置換コントロールを使用します。
- プログラムで、代替コントロール API を使用します。
- 暗黙的に、AdRotator コントロールを使用します。

### <a name="substitution-control"></a>代替制御

ASP.NET Substitution コントロールは、キャッシュではなく動的に作成されるキャッシュされたページのセクションを指定します。 ページ上の動的コンテンツを表示する場所に、置換コントロールを配置します。 実行時に、代入コントロールは MethodName プロパティで指定したメソッドを呼び出します。 このメソッドは文字列を返す必要があり、その後、置換コントロールの内容を置き換えます。 メソッドは、コントロールを含む Page コントロールまたはユーザー コントロールの静的メソッドである必要があります。 代替コントロールを使用すると、クライアント側のキャッシュ機能がサーバーのキャッシュ可能に変更され、ページがクライアントにキャッシュされません。 これにより、以降のページ要求がメソッドを再度呼び出して動的コンテンツを生成することが保証されます。

### <a name="substitution-api"></a>置換 API

キャッシュされたページの動的コンテンツをプログラムで作成するには、ページ コードで[WriteSubstitution](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx)メソッドを呼び出して、メソッドの名前をパラメーターとして渡します。 動的コンテンツの作成を処理するメソッドは、単一の[HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)パラメーターを受け取り、文字列を返します。 戻り文字列は、指定された場所で置き換えられるコンテンツです。 宣言によって代入コントロールを使用する代わりに WriteSubstitution メソッドを呼び出す利点は、Page オブジェクトまたは UserControl オブジェクトの静的メソッドを呼び出す代わりに、任意のオブジェクトのメソッドを呼び出すことができることです。

WriteSubstitution メソッドを呼び出すと、クライアント側のキャッシュ機能がサーバーのキャッシュ可能に変更され、ページがクライアントにキャッシュされません。 これにより、以降のページ要求がメソッドを再度呼び出して動的コンテンツを生成することが保証されます。

### <a name="adrotator-control"></a>アドローテーションコントロール

AdRotator サーバー コントロールは、キャッシュ後の置換を内部的にサポートしています。 ページに AdRotator コントロールを配置すると、親ページがキャッシュされているかどうかに関係なく、要求ごとに固有の広告がレンダリングされます。 その結果、AdRotator コントロールを含むページは、サーバー側のキャッシュのみです。

## <a name="controlcachepolicy-class"></a>クラス

クラスを使用すると、ユーザー コントロールを使用してフラグメント キャッシュをプログラムで制御できます。 ASP.NET、ユーザー コントロールを[インスタンス](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx)内に埋め込みます。 クラスは、出力キャッシュが有効になっているユーザー コントロールを表します。

[コントロールの](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx)[プロパティ](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx)にアクセスすると、常に有効なコントロールキャッシュ ポリシー オブジェクトが取得されます。 ただし、[ユーザー コントロール](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx)[コントロールのプロパティ](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx)にアクセスする場合は、ユーザー コントロールが既に BasePartialCachingControl コントロールによってラップされている場合にのみ有効な ControlCachePolicy オブジェクトを受け取ります。 ラップされていない場合、プロパティによって返される ControlCachePolicy オブジェクトは、関連付けられた BasePartialCachingControl がないため、操作しようとすると例外をスローします。 UserControl インスタンスが例外を生成せずにキャッシュをサポートしているかどうかを確認するには[、SupportsCaching](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx)プロパティを調べます。

クラスを使用すると、出力キャッシュを有効にする方法の 1 つです。 出力キャッシュを有効にする方法を次に示します。

- 宣言型シナリオで出力キャッシュを有効にするには、 [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx)ディレクティブを使用します。
- 分離コード ファイル内のユーザー コントロールのキャッシュを有効にするには[、PartialCachingAttribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx)属性を使用します。
- クラスを使用して、前のメソッドのいずれかを使用してキャッシュが有効で[、System.Web.UI.TemplateControl.LoadControl](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx)メソッドを使用して動的に読み込まれた BasePartialCachingControl インスタンスを操作するプログラムシナリオでキャッシュ設定を指定します。

コントロールのライフ サイクルの Init ステージと PreRender ステージの間でのみ、ControlCachePolicy インスタンスを正常に操作できます。 プリレンダリング フェーズの後に ControlCachePolicy オブジェクトを変更すると、コントロールのレンダリング後に行われた変更が実際にキャッシュ設定に影響を与えることができないため、ASP.NET例外がスローされます (コントロールはレンダリング ステージ中にキャッシュされます)。 最後に、ユーザー コントロール インスタンス (および ControlCachePolicy オブジェクト) は、実際にレンダリングされた場合にのみプログラムによる操作に使用できます。

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>キャッシュ構成の変更 - &lt;&gt;キャッシュ要素

ASP.NET 2.0 のキャッシュ設定にはいくつかの変更があります。 キャッシュ&lt;&gt;要素は ASP.NET 2.0 で新しく追加され、構成ファイルでキャッシュ構成を変更できます。 次の属性を使用できます。

| **要素** | **説明** |
| --- | --- |
| **キャッシュ** | 省略可能な要素です。 グローバル アプリケーション キャッシュ設定を定義します。 |
| **Outputcache** | 省略可能な要素です。 アプリケーション全体の出力キャッシュ設定を指定します。 |
| **outputCacheSettings** | 省略可能な要素です。 アプリケーションのページに適用できる出力キャッシュ設定を指定します。 |
| **sqlCacheDependency** | 省略可能な要素です。 ASP.NET アプリケーションの SQL キャッシュ依存関係を構成します。 |

### <a name="the-ltcachegt-element"></a>&lt;キャッシュ&gt;要素

キャッシュ&gt;要素では、次の属性&lt;を使用できます。

| **属性** | **説明** |
| --- | --- |
| **メモリコレクションを無効にします。** | オプション**のブール属性**。 コンピューターのメモリ不足時に発生するキャッシュ メモリ コレクションが無効かどうかを示す値を取得または設定します。 |
| **無効にする有効期限** | オプション**のブール属性**。 キャッシュの有効期限が無効かどうかを示す値を取得または設定します。 無効にすると、キャッシュされたアイテムは期限切れにならないし、有効期限が切れたキャッシュ項目のバックグラウンド清掃は発生しません。 |
| **プライベートバイト数の制限** | オプション**の Int64**属性。 キャッシュが期限切れアイテムのフラッシュを開始してメモリの再利用を試みる前に、アプリケーションのプライベート バイトの最大サイズを示す値を取得または設定します。 この制限には、キャッシュで使用されるメモリと、実行中のアプリケーションからの通常のメモリ オーバーヘッドの両方が含まれます。 ゼロの設定は、ASP.NETがメモリの再利用を開始するタイミングを決定するために独自のヒューリスティックを使用することを示します。 |
| **パーセンテージ物理メモリ使用制限** | オプション**の Int32**属性。 キャッシュが期限切れアイテムのフラッシュを開始し、メモリの再利用を試みる前に、アプリケーションが使用できるマシンの物理メモリの最大割合を示す値を取得または設定します。 ゼロの設定は、ASP.NETがメモリの再利用を開始するタイミングを決定するために独自のヒューリスティックを使用することを示します。 |
| **プライベートバイトポールタイム** | オプション**のタイムスパン**属性。 アプリケーションのプライベート バイトメモリ使用量のポーリング間隔を示す値を取得または設定します。 |

### <a name="the-ltoutputcachegt-element"></a>&lt;出力キャッシュ&gt;要素

次の属性は、outputCache&lt;&gt;要素に使用できます。

|       <strong>属性</strong>        |                                                                                                                                                                                                                                                       <strong>説明</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>出力キャッシュを有効にする</strong>    |                                                                                                                                                          オプション<strong>のブール属性</strong>。 ページ出力キャッシュを有効または無効にします。 無効にすると、プログラム設定や宣言設定に関係なく、ページはキャッシュされません。 既定値は<strong>true です</strong>。                                                                                                                                                           |
|  <strong>フラグメントキャッシュを有効にします。</strong>   |                                                オプション<strong>のブール属性</strong>。 アプリケーション フラグメント キャッシュを有効または無効にします。 無効にすると、使用される[@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx)ディレクティブやキャッシュ プロファイルに関係なく、ページはキャッシュされません。 上位プロキシ サーバーとブラウザー クライアントがページ出力をキャッシュに入れないことを示すキャッシュ コントロール ヘッダーが含まれます。 デフォルト値は<strong>false</strong>です。                                                 |
| <strong>ヘッダーを送ります。</strong> |                                                                                                                                                      オプション<strong>のブール属性</strong>。 キャッシュ<strong>コントロール:プライベート</strong>ヘッダーが出力キャッシュ モジュールによって既定で送信されるかどうかを示す値を取得または設定します。 デフォルト値は<strong>false</strong>です。                                                                                                                                                      |
|      <strong>を省略します。</strong>      | オプション<strong>のブール属性</strong>。 応答の Http "<strong>Vary: \</強い>" ヘッダーの送信を有効または無効<em>にします。既定の設定が false の場合、</em>出力キャッシュ\*ページに対して "*Vary: <strong>" ヘッダーが送信されます。Vary ヘッダーが送信されると、Vary ヘッダーで指定された内容に基づいて、異なるバージョンをキャッシュできます。たとえば<em>、Vary:User-Agent</em>は、要求を発行するユーザー エージェントに基づいて、ページの異なるバージョンを格納します。デフォルト値は **false です</strong>。 |

### <a name="the-ltoutputcachesettingsgt-element"></a>&lt;要素を出力します&gt;。

&lt;outputCacheSettings&gt;要素を使用すると、前述のようにキャッシュ プロファイルを作成できます。 要素の唯一の&lt;子要素は、キャッシュ プロファイル&lt;を構成するための&gt;outputCacheProfiles 要素です。&gt;

### <a name="the-ltsqlcachedependencygt-element"></a>要素&lt;をキャッシュします&gt;。

次の属性は&lt;、sqlCache 依存関係要素&gt;に使用できます。

| **属性** | **説明** |
| --- | --- |
| **有効** | 必須**のブール属性**。 変更がポーリングされているかどうかを示します。 |
| **投票時間** | オプション**の Int32**属性。 データベース テーブルに変更が行われる頻度を設定します。 この値は、連続するポーリング間のミリ秒数に対応します。 500 ミリ秒未満に設定することはできません。 デフォルト値は 1 分です。 |

### <a name="more-information"></a>詳細情報

キャッシュの構成に関して、いくつかの追加情報を知っておく必要があります。

- ワーカー プロセスのプライベート バイト制限が設定されていない場合、キャッシュは次のいずれかの制限を使用します。 

    - x86 2GB: 800MB または 60% の物理 RAM の、いずれかの容量が小さい
    - x86 3GB: 1800MB または物理 RAM の 60% のいずれか少ない
    - x64: 物理 RAM の 1 テラバイトまたは 60% のいずれか少ない
- ワーカー プロセスのプライベート バイト制限と&lt;キャッシュの両方のプライベート&gt;BytesLimit/ が設定されている場合、キャッシュは 2 つのうち最小値を使用します。
- 1.x と同様に、キャッシュ エントリをドロップして GC を呼び出します。次の 2 つの理由で収集します。 

    - プライベートバイト制限に非常に近い
    - 使用可能なメモリが 10% 未満または近い
- キャッシュの割合を 100 に設定&lt;することで、使用可能なメモリ不足の場合は、&gt;トリムとキャッシュを効果的に無効にできます。
- 1.x とは異なり、2.0 は最後の GC の場合、トリムを中断し、コールを収集します。Collect は、プライベート バイトまたはマネージ ヒープのサイズを(キャッシュ)メモリ制限の 1% 以上削減しませんでした。

## <a name="lab1-custom-cache-dependencies"></a>Lab1: カスタム キャッシュの依存関係

1. 新しい Web サイトを作成します。
2. cache.xml という名前の新しい XML ファイルを追加し、Web アプリケーションのルートに保存します。
3. default.aspx の分離コード\_で、次のコードを Page Load メソッドに追加します。 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. ソース ビューの default.aspx の先頭に次の項目を追加します。 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. 既定の.aspx を参照します。 時は何と言っていますか?
6. ブラウザーを更新します。 時は何と言っていますか?
7. cache.xml を開き、次のコードを追加します。 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. キャッシュ.xml を保存します。
9. ブラウザーを更新します。 時は何と言っていますか?
10. 以前にキャッシュされた値を表示するのではなく、時刻が更新された理由を説明します。

## <a name="lab-2-using-polling-based-cache-dependencies"></a>演習 2 : ポーリング ベースのキャッシュ依存関係の使用

このラボでは、前のモジュールで作成したプロジェクトを使用して、GridView コントロールと DetailsView コントロールを使用して Northwind データベース内のデータを編集できます。

1. プロジェクトを Visual Studio 2005 で開きます。
2. ノースウィンド データベース\_に対して aspnet regsql ユーティリティを実行し、データベースと Products テーブルを有効にします。 Visual Studio コマンド プロンプトから次のコマンドを使用します。 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. 次のファイルを web.config ファイルに追加します。 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. showdata.aspx という名前の新しい Web フォームを追加します。
5. 次の @ 出力キャッシュ ディレクティブを showdata.aspx ページに追加します。 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. showdata.aspx のページ\_読み込みに次のコードを追加します。 

    [!code-html[Main](caching/samples/sample21.html)]
7. showdata.aspx に新しい SqlDataSource コントロールを追加し、ノースウィンド データベース接続を使用するように構成します。 [次へ] をクリックします。
8. [製品名] と [商品 ID] チェックボックスをオンにして、[次へ] をクリックします。
9. [完了] をクリックします。
10. 新しいグリッドビューを showdata.aspx ページに追加します。
11. ドロップダウンから [SqlDataSource1] を選択します。
12. 保存して showdata.aspx を参照します。 表示された時刻をメモします。
