---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: AJAX を使用して動的更新を配信する |マイクロソフトドキュメント
author: rick-anderson
description: ステップ 10 は、ディナーの詳細に統合された Ajax ベースのアプローチを使用して、RSVP にログインしたユーザーがディナーに参加するサポートを実装します。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541248"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a>AJAX を使用し、動的更新を配信する

[マイクロソフト](https://github.com/microsoft)

[PDF のダウンロード](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> これは、MVC 1 を使用して小さいが完全な Web アプリケーションを構築する方法を説明する無料の["NerdDinner" アプリケーション チュートリアル](introducing-the-nerddinner-tutorial.md)のステップ 10 ASP.NETです。
> 
> ステップ 10 では、ディナーの詳細ページに統合された Ajax ベースのアプローチを使用して、RSVP にログインしたユーザーのサポートを実装します。
> 
> mvc 3 ASP.NET使用している場合は、MVC 3 または[MVC ミュージック ストア](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)[チュートリアルの概要に](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)従うことをお勧めします。

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>NerdDinner ステップ 10: RsAP を有効にする AJAX が受け入れる

それでは、RSVPにログインしているユーザーが夕食会に出席することに興味を持つサポートを実装しましょう。 夕食の詳細ページに統合された AJAX ベースのアプローチを使用して、これを有効にします。

### <a name="indicating-whether-the-user-is-rsvpd"></a>ユーザーが RSVP'd であるかどうかを示す

ユーザーは */Dinners/Details/[id]* URL にアクセスして、特定のディナーの詳細を確認できます。

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

Details() アクションメソッドは次のように実装されています。

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

RSVP サポートを実装する最初のステップは、(以前に構築したDinner.cs部分クラス内で) Dinner オブジェクトに "IsUserRegistered(ユーザー名)" ヘルパー メソッドを追加することです。 このヘルパー メソッドは、ユーザーが現在、Dinner の RSVP の有無に応じて true または false を返します。

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

その後、Details.aspx ビュー テンプレートに次のコードを追加して、ユーザーがイベントに登録されているかどうかを示す適切なメッセージを表示できます。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

そして今、ユーザーが夕食を訪問すると、彼らはこのメッセージが表示されます:

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

そして、彼らは夕食を訪問すると、彼らは次のメッセージが表示されますのために登録されていません:

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>登録アクション メソッドの実装

ここで、詳細ページから、ディナーに RSVP にユーザーを有効にするために必要な機能を追加してみましょう。

これを実装するには、\Controllersディレクトリを右クリックし、&gt;コントローラメニューコマンドを選択して、新しい "RSVPController"クラスを作成します。

新しい RSVPController クラス内に、引数として Dinner の ID を取得し、適切な Dinner オブジェクトを取得し、ログインしているユーザーが現在登録しているユーザーの一覧に含まれているかどうかを確認し、RSVP オブジェクトを追加しない場合は、そのクラスに "Register" アクション メソッドを実装します。

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

アクションメソッドの出力として単純な文字列を返す方法の上に注意してください。 このメッセージをビューテンプレートに埋め込むこともできますが、とても小さいため、コントローラの基本クラスで Content() ヘルパーメソッドを使用し、上記のような文字列メッセージを返します。

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>AJAX を使用して RSVPForEvent アクション メソッドを呼び出す

AJAX を使用して、詳細ビューから Register アクション メソッドを呼び出します。 これを実装することは非常に簡単です。 最初に、2 つのスクリプト ライブラリ参照を追加します。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

最初のライブラリは、AJAX クライアント側スクリプト ライブラリASP.NETコアを参照します。 このファイルは約 24 k のサイズ (圧縮) で、コア クライアント側の AJAX 機能が含まれています。 2 番目のライブラリには、MVC の組み込みの AJAX ヘルパー メソッド (まもなく使用) ASP.NET統合するユーティリティ関数が含まれています。

その後、先ほど追加したビュー テンプレート コードを更新して、"このイベントに登録されていません" というメッセージを出力する代わりに、プッシュされたときに RSVPForEvent アクション メソッドを呼び出す AJAX 呼び出しを実行するリンクをレンダリングします。

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

上記で使用した Ajax.ActionLink() ヘルパー メソッドは、MVC ASP.NET組み込まれており、標準ナビゲーションを実行する代わりに、リンクがクリックされたときにアクション メソッドに AJAX 呼び出しを行う点を除いて、Html.ActionLink() ヘルパー メソッドに似ています。 上記では、「RSVP」コントローラ上の"登録"アクションメソッドを呼び出し、それに「id」パラメータとしてDinnerIDを渡しています。 最後に渡す AjaxOptions パラメータは、アクション メソッドから返されたコンテンツを取得し、ID が&lt;&gt; "rsvpmsg" であるページの HTML div 要素を更新することを示します。

そして今、ユーザーがディナーを閲覧すると、彼らはまだ登録されていません、彼らはそれのためにRSVPへのリンクが表示されます:

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

彼らは「このイベントのRSVP」リンクをクリックすると、RSVPコントローラ上の登録アクションメソッドにAJAX呼び出しを行い、それが完了すると、次のような更新されたメッセージが表示されます。

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

この AJAX 呼び出しを行う際に関係するネットワーク帯域幅とトラフィックは、実際には軽量です。 ユーザーが [このイベントの RSVP] リンクをクリックすると、次のような */Dinners/Register/1* URL に対して、小さな HTTP POST ネットワーク要求が送信されます。

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

そして、私たちの登録アクションメソッドからの応答は、単純です:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

この軽量の呼び出しは高速であり、低速のネットワークでも動作します。

### <a name="adding-a-jquery-animation"></a>jQuery アニメーションの追加

実装した AJAX 機能は、適切かつ高速に機能します。 しかし、RSVP リンクが新しいテキストに置き換えられたことにユーザーが気付かないほど高速に発生する場合があります。 結果をもう少し明確にするために、更新メッセージに注意を引く簡単なアニメーションを追加できます。

既定のASP.NET MVC プロジェクト テンプレートには、優れた (そして非常に人気のある) オープンソースの JavaScript ライブラリが含まれています。 jQuery は、素敵な HTML DOM の選択やエフェクトライブラリなど、多くの機能を提供します。

jQuery を使用するには、まずスクリプト参照を追加します。 サイト内のさまざまな場所で jQuery を使用するため、Site.master マスター ページ ファイル内にスクリプト参照を追加して、すべてのページで使用できるようにします。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*ヒント: Vs 2008 SP1 用の JavaScript インテリセンス修正プログラムがインストールされていることを確認してください。ダウンロードは次のどこからでも行うことができます。http://tinyurl.com/vs2008javascripthotfix*

JQuery を使用して記述されたコードは、CSS セレクタを使用して 1 つ以上の HTML 要素を取得する、グローバルな "$()" JavaScript メソッドを使用することがよくあります。 たとえば *、$("#rsvpmsg")は*rsvpmsg の ID を持つ HTML 要素を選択し *、$(".something") は*"何か" CSS クラス名を持つすべての要素を選択します。 また、次のようなセレクタークエリを使用して、「チェックされたすべてのラジオボタンを返す」のようなより高度なクエリを書くことができます: *@type$("input[@checked=radio][])*

要素を選択したら、メソッドを呼び出して、要素を非表示にするようなアクションを実行できます *#rsvpmsg。*

RSVP のシナリオでは、"rsvpmsg" div&lt;&gt;を選択し、そのテキスト コンテンツのサイズをアニメーション化する"AnimateRSVPMessage"という名前の単純な JavaScript 関数を定義します。 次のコードは、テキストを小さく開始し、400 ミリ秒の時間枠を超えて増加させます。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

AJAX 呼び出しが正常に完了した後に呼び出されるこの JavaScript 関数を、Ajax.ActionLink() ヘルパー メソッドに渡して (AjaxOptions "OnSuccess" イベント プロパティを使用して) ワイヤアップできます。

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

そして今、「このイベントのRSVP」リンクがクリックされ、AJAXコールが正常に完了すると、送信されたコンテンツメッセージはアニメーション化され、大きくなります。

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

"OnSuccess" イベントを提供するだけでなく、AjaxOptions オブジェクトは、処理できる OnBegin イベント、OnFailure イベント、および OnComplete イベントを公開します。

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>クリーンアップ - RSVP 部分ビューのリファクタリング

詳細ビュー テンプレートは少し長くなり始めていますが、残業は少し理解しにくくなります。 コードの読みやすさを向上させるために、詳細ページのすべての RSVP ビュー コードをカプセル化する部分ビュー RSVPStatus.ascx を作成して完了します。

これを行うには、\Views\Dinners フォルダを右クリックし、[追加-&gt;表示] メニュー コマンドを選択します。 厳密に型指定された ViewModel として Dinner オブジェクトを取得します。 その後、Details.aspx ビューから RSVP コンテンツをコピー/貼り付けることができます。

これを完了したら、編集と削除のリンク ビュー コードをカプセル化する別の部分ビュー (EditAndDeleteLinks.ascx) も作成しましょう。 また、Dinner オブジェクトを厳密に型指定された ViewModel として取得し、Details.aspx ビューから編集と削除のロジックをコピー/貼り付けます。

詳細ビュー テンプレートには、次の 2 つの Html.RenderPartial() メソッド呼び出しを下部に含めることができます。

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

これにより、コードの読み取りや保守がきれいになります。

### <a name="next-step"></a>次の手順

ここで、AJAX をさらに活用して、アプリケーションに対話的なマッピングサポートを追加する方法を見てみましょう。

> [!div class="step-by-step"]
> [前へ](secure-applications-using-authentication-and-authorization.md)
> [次へ](use-ajax-to-implement-mapping-scenarios.md)
