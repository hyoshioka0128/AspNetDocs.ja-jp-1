---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET ウェブページ (Razor) API クイック リファレンス |マイクロソフトドキュメント
author: Rick-Anderson
description: このページには、最も一般的に使用されるオブジェクト、プロパティ、および Razor 構文を使用して Web ページをプログラミングするためのメソッドの簡単な例ASP.NETリストが含まれています。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675851"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET Web ページ (Razor) API のクイック リファレンス

[Tom FitzMacken](https://github.com/tfitzmac)

> このページには、最も一般的に使用されるオブジェクト、プロパティ、および Razor 構文を使用して Web ページをプログラミングするためのメソッドの簡単な例ASP.NETリストが含まれています。
> 
> 「(v2)」と記された説明は、Web ページバージョン 2 ASP.NETで導入されました。
> 
> API リファレンス ドキュメントについては、MSDN の[ASP.NET Web ページ リファレンス ドキュメントを参照してください](https://go.microsoft.com/fwlink/?LinkId=208659)。
> 
> ## <a name="software-versions"></a>ソフトウェアバージョン
> 
> 
> - ASP.NET ウェブページ (Razor) 3
>   
> 
> このチュートリアルは、ASP.NET Web ページ 2 と ASP.NET Web ページ 1.0 でも動作します (v2 とマークされた機能を除く)。

このページには、以下のリファレンス情報が含まれています。

- [クラス](#Classes)
- [データ](#Data)
- [ヘルパー](#Helpers)
- [Validation](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>クラス

### `AppState[key], AppState[index],App`

アプリケーション内の任意のページで共有できるデータが含まれます。 次の例のように、`App`動的プロパティを使用して同じデータにアクセスできます。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

文字列値をブール値 (true/false) に変換します。 文字列が true/false を表さない場合は、false を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

文字列値を日付/時刻に変換します。 文字列`DateTime.MinValue`が日付/時刻を表さない場合は、指定された値を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

文字列値を 10 進値に変換します。 文字列が 10 進値を表さない場合は、0.0 または指定された値を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

文字列値を浮動小数点数に変換します。 文字列が 10 進値を表さない場合は、0.0 または指定された値を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

文字列値を整数に変換します。 文字列が整数を表さない場合は、0 または指定された値を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

オプションの追加パス部分を含む、ローカル ファイル パスからブラウザ互換 URL を作成します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

*値*を HTML エンコード出力としてレンダリングするのではなく、HTML マークアップとしてレンダリングします。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

値を文字列から指定した型に変換できる場合は true を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

オブジェクトまたは変数に値がない場合は true を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

要求が POST の場合は true を返します。 (初期要求は通常 GET です。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

このページに適用するレイアウト ページのパスを指定します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

現在の要求のページ、レイアウト ページ、および部分ページ間で共有されるデータが含まれます。 次の例のように、`Page`動的プロパティを使用して同じデータにアクセスできます。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(レイアウト ページ)名前付きセクションにないコンテンツ ページのコンテンツをレンダリングします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

指定されたパスとオプションの追加データを使用してコンテンツ ページをレンダリングします。 余分なパラメーターの値は、位置 (`PageData`例 1) またはキー (例 2) から取得できます。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(レイアウト ページ)名前を持つコンテンツ セクションをレンダリングします。 セクションを省略可能にするには *、必須*を false に設定します。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

HTTP クッキーの値を取得または設定します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

現在の要求でアップロードされたファイルを取得します。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

フォーム (文字列) でポストされたデータを取得します。 `Request[key]`は`Request.Form`、 と`Request.QueryString`コレクションの両方をチェックします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

URL クエリ文字列で指定されたデータを取得します。 `Request[key]`は`Request.Form`、 と`Request.QueryString`コレクションの両方をチェックします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

フォーム要素、クエリ文字列値、Cookie、またはヘッダー値の要求検証を選択的に無効にします。 要求の検証は既定で有効になっており、ユーザーがマークアップやその他の危険なコンテンツを投稿できないようにします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

HTTP サーバー ヘッダーを応答に追加します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

指定した時間のページ出力をキャッシュします。 必要に応じて、ページアクセスごとにタイムアウトをリセットするように*スライド*を設定し、ページ要求内の異なるクエリ文字列ごとに異なるバージョンのページをキャッシュするように*varyByParams*を設定します。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

ブラウザー要求を新しい場所にリダイレクトします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

ブラウザに送信される HTTP ステータス コードを設定します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

オプションの MIME タイプを使用して *、データ*の内容を応答に書き込みます。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

ファイルの内容を応答に書き込みます。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(レイアウト ページ)名前を持つコンテンツ セクションを定義します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

HTML エンコードされた文字列をデコードします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

HTML マークアップでレンダリングする文字列をエンコードします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

指定した仮想パスのサーバー物理パスを返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

URL からテキストをデコードします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

URL に入れるテキストをエンコードします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

ユーザーがブラウザーを閉じるまで存在する値を取得または設定します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

オブジェクトの値の文字列表現を表示します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

URL から追加のデータを取得します (*たとえば、/MyPage/ExtraData)。*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

指定したユーザーのパスワードを変更します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

アカウント確認トークンを使用してアカウントを確認します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

指定したユーザー名とパスワードを使用して新しいユーザー アカウントを作成します。 確認トークンを要求するには、確認トークンの要求に true*を渡します。*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

現在ログインしているユーザーの整数識別子を取得します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

現在ログインしているユーザーの名前を取得します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

ユーザーがパスワードをリセットできるように、ユーザーに電子メールで送信できるパスワード リセット トークンを生成します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

ユーザー名からユーザー ID を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

現在のユーザーがログインしている場合は true を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

ユーザーが確認済み (確認メールなど) の場合は true を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

現在のユーザーの名前が指定されたユーザー名と一致する場合は true を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

Cookie に認証トークンを設定して、ユーザーをログインします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

認証トークンの Cookie を削除して、ユーザーをログアウトします。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

ユーザーが認証されていない場合、HTTP ステータスを 401 (Unauthorized) に設定します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

現在のユーザーが指定されたロールの 1 つのメンバーでない場合は、HTTP ステータスを 401 (許可されていません) に設定します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

現在のユーザーが*username*で指定されたユーザーでない場合は、HTTP ステータスを 401 (許可されていません) に設定します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

パスワード リセット トークンが有効な場合は、ユーザーのパスワードを新しいパスワードに変更します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>Data

### `Database.Execute(SQLstatement [,parameters]`

INSERT、DELETE、または UPDATE などの*SQLstatement* (省略可能なパラメーターを使用して) を実行し、影響を受けるレコードのカウントを返します。

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

最近挿入された行から ID 列を返します。

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

指定したデータベース ファイルまたは*Web.config*ファイルの名前付き接続文字列を使用して指定されたデータベースを開きます。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

接続文字列を使用してデータベースを開きます。 (これは、接続文字列名`Database.Open`を使用する とは対照的です。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

*SQLstatement*を使用してデータベースにクエリを実行し (オプションでパラメータを渡す)、結果をコレクションとして返します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

*SQLstatement*を (オプションのパラメーターを使用して) 実行し、単一のレコードを返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

*SQLstatement*を (オプションのパラメーターを使用して) 実行し、単一の値を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>ヘルパー

### `Analytics.GetGoogleHtml(webPropertyId)`

指定した ID の Google アナリティクス JavaScript コードをレンダリングします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

指定したプロジェクトの統計カウンター分析 JavaScript コードをレンダリングします。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

指定したアカウントの Yahoo アナリティクス JavaScript コードをレンダリングします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

Bingに検索を渡します。 検索するサイトと検索ボックスのタイトルを指定するには、 および`Bing.SiteUrl``Bing.SiteTitle`のプロパティを設定します。 通常、これらのプロパティは*\_[AppStart]* ページで設定します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

グラフを初期化します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

グラフに凡例を追加します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

一連の値をグラフに追加します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

指定したデータのハッシュを返します。 既定のアルゴリズムは`sha256`です。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

Facebookユーザーがページに接続できるようにします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

ファイルをアップロードするための UI をレンダリングします。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

指定した Xbox ゲーマー タグをレンダリングします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

指定した電子メール アドレスの Gravatar イメージをレンダリングします。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

データ オブジェクトを JavaScript オブジェクト表記法 (JSON) 形式の文字列に変換します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

JSON エンコードされた入力文字列を、データベースに反復処理または挿入できるデータ オブジェクトに変換します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

指定したタイトルとオプションの URL を使用してソーシャル ネットワーク リンクをレンダリングします。

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

エラー メッセージをフォーム フィールドに関連付けます。 ヘルパーを`ModelState`使用してこのメンバーにアクセスします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

エラー メッセージをフォームに関連付けます。 ヘルパーを`ModelState`使用してこのメンバーにアクセスします。

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

検証エラーがない場合は true を返します。 ヘルパーを`ModelState`使用してこのメンバーにアクセスします。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

オブジェクトと子オブジェクトのプロパティと値をレンダリングします。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

reCAPTCHA 検証テストをレンダリングします。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

reCAPTCHA サービスの公開キーと秘密キーを設定します。 通常、これらのプロパティは*\_[AppStart]* ページで設定します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

reCAPTCHA テストの結果を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

Web ページに関するステータス情報ASP.NET表示します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

指定したユーザーの Twitter ストリームをレンダリングします。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

指定した検索テキストの Twitter ストリームをレンダリングします。

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

指定したファイルの Flash ビデオ プレーヤーを、オプションの幅と高さでレンダリングします。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

指定したファイルの Windows Media プレーヤーを、オプションの幅と高さでレンダリングします。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

指定された *.xap*ファイルの Silverlight プレーヤーを、必要な幅と高さでレンダリングします。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

オブジェクトが見つからない場合は *、key*で指定されたオブジェクトを返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

*key*で指定されたオブジェクトをキャッシュから削除します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

key*で指定*された名前の下に*値*をキャッシュに入れます。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

クエリのデータ`WebGrid`を使用して新しいオブジェクトを作成します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

HTML テーブルにデータを表示するマークアップをレンダリングします。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

オブジェクトのページャーを`WebGrid`レンダリングします。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

指定したパスからイメージを読み込みます。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

指定したイメージを透かしとして追加します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

指定したテキストをイメージに追加します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

イメージを水平方向または垂直方向に反転します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

ファイルのアップロード中に画像がページに投稿されたときにイメージを読み込みます。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

イメージのサイズを変更します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

イメージを左または右に回転します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

指定したパスにイメージを保存します。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

SMTP サーバーのパスワードを設定します。 通常は、このプロパティは*\_[AppStart]* ページで設定します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

電子メール メッセージを送信します。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

SMTP サーバー名を設定します。 通常は、このプロパティは*\_[AppStart]* ページで設定します。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

SMTP サーバーのユーザー名を設定します。 通常は、このプロパティを*\_[AppStart]* ページで設定する必要があります。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>検証

### `Html.ValidationMessage(field)`

(v2)指定したフィールドの検証エラー メッセージを表示します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

(v2)すべての検証エラーの一覧を表示します。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

(v2)指定した種類の検証に対してユーザー入力要素を登録します。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

(v2)検証エラー メッセージを書式設定できるように、クライアント側の検証用の CSS クラス属性を動的にレンダリングします。 (適切なクライアント スクリプト ライブラリを参照し、CSS クラスを定義する必要があります)。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

(v2)ユーザー入力フィールドのクライアント側検証を有効にします。 (適切なクライアント スクリプト ライブラリを参照する必要があります)。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

(v2)検証用に登録されているすべてのユーザー入力要素に有効な値が含まれている場合は、true を返します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

(v2)ユーザー入力要素の値をユーザーが指定する必要があることを指定します。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

(v2)ユーザーが各ユーザー入力要素の値を指定する必要があることを指定します。 このメソッドでは、カスタム エラー メッセージを指定することはできません。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

(v2)メソッドを使用する場合の検証テスト`Validation.Add`を指定します。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
