---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: ペイパルでのチェックアウトと支払い |マイクロソフトドキュメント
author: Erikre
description: このチュートリアル シリーズ ASP.NETでは、ASP.NET 4.5 と Microsoft Visual Studio Express 2013 for.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675689"
---
# <a name="checkout-and-payment-with-paypal"></a>精算と PayPal による支払い

[エリック・レイタン](https://github.com/Erikre)著

[Wingtip Toys サンプル プロジェクト (C#) をダウンロードするか、](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)[電子書籍をダウンロード (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> このチュートリアル シリーズでは、ASP.NET 4.5 および Web 用の Visual Studio Express 2013 を使用して、ASP.NET Web フォーム アプリケーションを構築する基本について説明します。 [C# ソース コードを含む](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)Visual Studio 2013 プロジェクトは、このチュートリアル シリーズに付属しています。

このチュートリアルでは、PayPal を使用してユーザーの承認、登録、および支払いを含むように Wingtip Toys サンプル アプリケーションを変更する方法について説明します。 ログインしているユーザーのみが製品を購入する権限を持ちます。 ASP.NET 4.5 Web フォーム プロジェクト テンプレートの組み込みのユーザー登録機能には、必要なものの多くが既に含まれています。 PayPal エクスプレス チェックアウト機能を追加します。 このチュートリアルでは、PayPal開発者のテスト環境を使用しているので、実際の資金は転送されません。 チュートリアルの最後に、ショッピング カートに追加する製品を選択し、チェックアウト ボタンをクリックして、PayPal テスト Web サイトにデータを転送することで、アプリケーションをテストします。 PayPal テスト Web サイトで、出荷と支払い情報を確認し、購入を確認して完了するために、ローカルの Wingtip Toys サンプル アプリケーションに戻ります。

スケーラビリティとセキュリティに対応したオンライン ショッピングを専門とする経験豊富なサードパーティの支払いプロセッサがいくつかあります。 ASP.NET開発者は、ショッピングと購入ソリューションを実装する前に、サードパーティの支払いソリューションを利用することの利点を考慮する必要があります。

> [!NOTE] 
> 
> Wingtip Toys サンプル アプリケーションは、ASP.NET Web 開発者が利用できる特定のASP.NETの概念と機能を示すように設計されています。 このサンプル アプリケーションは、スケーラビリティとセキュリティに関して考えられるすべての状況に合わせて最適化されたものではありません。

## <a name="what-youll-learn"></a>ここでは、次の内容について学習します。

- フォルダ内の特定のページへのアクセスを制限する方法。
- 匿名ショッピング カートから既知のショッピング カートを作成する方法。
- プロジェクトの SSL を有効にする方法。
- OAuth プロバイダーをプロジェクトに追加する方法。
- PayPal テスト環境を使用して製品を購入する PayPal を使用する方法。
- **詳細ビュー**コントロールでの PayPal から詳細を表示する方法。
- PayPalから取得した詳細でWingtipのおもちゃのアプリケーションのデータベースを更新する方法。

## <a name="adding-order-tracking"></a>注文追跡の追加

このチュートリアルでは、ユーザーが作成した順序からデータを追跡する 2 つの新しいクラスを作成します。 クラスは、出荷情報、購入合計、および支払確認に関するデータを追跡します。

### <a name="add-the-order-and-orderdetail-model-classes"></a>順序および注文詳細モデル クラスの追加

このチュートリアル シリーズの前半`Category`では *、Models*フォルダーに 、、`Product`および クラスを作成して、カテゴリ、製品`CartItem`、およびショッピング カートのアイテムのスキーマを定義しました。 次に、2 つの新しいクラスを追加して、製品の注文のスキーマと注文の詳細を定義します。

1. **Models**フォルダに、 という名前の新しいクラス*Order.cs*追加します。   
   新しいクラス ファイルがエディターに表示されます。
2. 既定のコードを次のコードに置き換えます。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. *OrderDetail.cs*クラスを*Models*フォルダーに追加します。
4. 既定のコードを以下のコードに置き換えます。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

`Order`および`OrderDetail`クラスには、購買および出荷に使用する注文情報を定義するスキーマが含まれています。

さらに、エンティティ クラスを管理し、データベースへのデータ アクセスを提供するデータベース コンテキスト クラスを更新する必要があります。 これを行うには、新しく作成された Order クラス`OrderDetail`とモデル`ProductContext`クラスをクラスに追加します。

1. **ソリューション エクスプローラー**で *、ProductContext.cs*ファイルを検索して開きます。
2. 次に示すように、強調表示されたコードを*ProductContext.cs*ファイルに追加します。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

このチュートリアル シリーズで既に説明したように *、ProductContext.cs*ファイルのコードは`System.Data.Entity`、Entity Framework のすべてのコア機能にアクセスできるように名前空間を追加します。 この機能には、厳密に型指定されたオブジェクトを操作してデータを照会、挿入、更新、および削除する機能が含まれます。 クラス内の上記の`ProductContext`コードは、新しく追加`Order`されたクラスと`OrderDetail`クラスへの Entity Framework アクセスを追加します。

## <a name="adding-checkout-access"></a>チェックアウト アクセスの追加

Wingtip Toys サンプル アプリケーションを使用すると、匿名ユーザーはショッピング カートに製品を確認および追加できます。 ただし、匿名ユーザーがショッピング カートに追加した商品を購入する場合は、サイトにログオンする必要があります。 ログオンすると、チェックアウトと購入プロセスを処理する Web アプリケーションの制限されたページにアクセスできます。 これらの制限されたページは、アプリケーションの*チェックアウト*フォルダーに含まれています。

### <a name="add-a-checkout-folder-and-pages"></a>チェックアウト フォルダとページを追加する

チェックアウト フォルダーと、*その*中に、チェックアウトプロセス中に表示されるページを作成します。 これらのページは、このチュートリアルの後半で更新します。

1. **ソリューション エクスプローラ**でプロジェクト名 (**Wingtip Toys**) を右クリックし、[**新しいフォルダの追加 ]** を選択します。 

    ![PayPal でのチェックアウトと支払い - 新しいフォルダー](checkout-and-payment-with-paypal/_static/image1.png)
2. 新しいフォルダに 「チェックアウト」 という名前*を付けます*。
3. *[チェックアウト*] フォルダを右クリックし、[**Add**-&gt;**新しい項目**の追加] を選択します。 

    ![PayPal でのチェックアウトと支払い - 新しいアイテム](checkout-and-payment-with-paypal/_static/image2.png)
4. **[新しい項目の追加]** ダイアログ ボックスが表示されます。
5. 左側の **[Visual C#**  - &gt; **Web**テンプレート] グループを選択します。 次に、中央のウィンドウで [**マスター ページを含む Web フォーム**] を選択し、"CheckoutStart.aspx" という名前を*付けます*。 

    ![PayPal でのチェックアウトと支払い - 新しい項目の追加ダイアログ](checkout-and-payment-with-paypal/_static/image3.png)
6. 前と同様に、マスター ページとして*Site.Master*ファイルを選択します。
7. 上記と同じ手順を使用して、次のページを *[チェックアウト*] フォルダに追加します。   

    - レビューをチェックアウト.aspx
    - チェックアウトコンプリート.aspx
    - チェックアウトキャンセル.aspx
    - エラーをチェックアウト.aspx

### <a name="add-a-webconfig-file"></a>Web.config ファイルを追加する

新しい*Web.config*ファイルを *[チェックアウト*] フォルダに追加すると、フォルダに含まれるすべてのページへのアクセスを制限できるようになります。

1. *[チェックアウト*] フォルダを右クリックし、[**新しい項目**の**追加]** -&gt;を選択します。  
   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. 左側の **[Visual C#**  - &gt; **Web**テンプレート] グループを選択します。 次に、中央のウィンドウで **[Web 構成ファイル**] を選択し、既定の名前の*Web.config*をそのまま使用**します。**
3. *Web.config* ファイルの XML の内容を次の内容で置き換えます。  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. *Web.config* ファイルを保存します。

*Web.config*ファイルは、Web アプリケーションのすべての不明なユーザーが*チェックアウト*フォルダーに含まれるページへのアクセスを拒否する必要があることを指定します。 ただし、ユーザーがアカウントを登録し、ログオンしている場合は、既知のユーザーになり、*チェックアウト*フォルダー内のページにアクセスできます。

ASP.NET構成は階層に従い、各*Web.config*ファイルは、そのフォルダーとその下にあるすべての子ディレクトリに構成設定を適用することに注意してください。

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>プロジェクトに対して SSL を有効にする

 Secure Sockets Layer (SSL) は、Web サーバーと Web クライアント間の通信に定義されたプロトコルで、暗号化によって通信の安全性を強化することができます。 SSL を使わないと、クライアントとサーバー間で送信されるデータが、ネットワークに物理的にアクセスできる第三者によるパケット スニッフィングの標的になります。 また、プレーンな HTTP を使用すると、いくつかの一般的な認証方式の安全性も低下します。 具体的には、基本認証とフォーム認証で送信する資格情報が暗号化されません。 安全性を確保するには、これらの認証方式で SSL を使用する必要があります。 

1. **ソリューション エクスプローラー**で**WingtipToys**プロジェクトをクリックし **、F4**キーを押して **[プロパティ]** ウィンドウを表示します。
2. **SSL の有効化**を に変更します`true`。
3. 後で使用するための **SSL URL** をコピーします。   
 SSL URL は`https://localhost:44300/`、SSL Web サイトを以前に作成していなければ (以下に示す) 場合を除き、表示されます。   
    ![プロジェクト プロパティ](checkout-and-payment-with-paypal/_static/image4.png)
4. **ソリューション エクスプローラ**で **、WingtipToys**プロジェクトを右クリックし、[**プロパティ**] をクリックします。
5. 左側のタブで **[Web]** をクリックします。
6. 先ほど保存した SSL **URL を**使用するようにプロジェクト**URL**を変更します。   
    ![プロジェクトの Web プロパティ](checkout-and-payment-with-paypal/_static/image5.png)
7. **CTRL + S キーを押して**ページを保存します。
8. **Ctrl キーを押しながら F5 キー**を押して、アプリケーションを実行します。 Visual Studio により、SSL の警告を回避するためのオプションが表示されます。
9. IIS Express SSL 証明書を信頼する場合は **[はい]** をクリックして続行します。   
    ![IIS Express SSL 証明書の詳細](checkout-and-payment-with-paypal/_static/image6.png)  
  セキュリティ警告が表示されます。
10. **[はい]** をクリックしてローカルホストに証明書をインストールします。   
    ![セキュリティ警告ダイアログ ボックス](checkout-and-payment-with-paypal/_static/image7.png)  
  ブラウザー ウィンドウが表示されます。

SSL を使用して、Web アプリケーションをローカルで簡単にテストできるようになりました。

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>OAuth 2.0 プロバイダーを追加する

ASP.NET Web フォームは、メンバーシップと認証のオプションが強化されています。 OAuth もこうした強化点の 1 つです。 OAuth は、Web、モバイル、およびデスクトップのアプリケーションからシンプルで標準的な方法で安全に認証するためのオープン プロトコルです。 ASP.NET Web フォーム テンプレートは OAuth を使用して、Facebook、Twitter、Google、および Microsoft を認証プロバイダーとして公開します。 このチュートリアルでは Google のみを認証プロバイダーとして使用しますが、コードを少し変更すれば他のプロバイダーも使用できます。 他のプロバイダーを実装する手順は、このチュートリアルで説明する手順とほとんど同じです。

このチュートリアルでは、認証の他にロールを使用して権限を付与します。 `canEdit` ロールに追加したユーザーだけが連絡先を変更 (作成、編集、削除) できます。

> [!NOTE] 
> 
> Windows Live アプリケーションは、作業中の Web サイトのライブ URL のみを受け入れるため、ログインのテストにローカル Web サイトの URL を使用することはできません。

次の手順を実行することで、Google 認証プロバイダーを追加できます。

1. *アプリケーション\_の開始\スタートアップ.Auth.csファイルを*開きます。
2. `app.UseGoogleAuthentication()` メソッドのコメント文字を削除して、メソッドを次のような記述にします。 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. [Google Developers Console](https://console.developers.google.com/)にアクセスします。 Google デベロッパーの電子メール アカウント (gmail.com) でサインインする必要があります。 Google アカウントを持っていない場合は、 **[Create an account]** リンクを選択します。   
   **Google Developers Console**が表示されます。   
    ![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)
4. [**プロジェクトの作成**] ボタンをクリックし、プロジェクト名と ID を入力します (既定値を使用できます)。 次に、**契約のチェックボックス**と[**作成**]ボタンをクリックします。  

    ![グーグル - 新しいプロジェクト](checkout-and-payment-with-paypal/_static/image9.png)

    新しいプロジェクトが数秒で作成され、新しいプロジェクトのページがブラウザーに表示されます。
5. 左側のタブで**&amp;[API 認証**] をクリックし、[**資格情報**] をクリックします。
6. **[OAuth]** の下の **[新しいクライアント ID**の作成] をクリックします。   
   **[Create Client ID]** ダイアログ ボックスが表示されます。   
    ![Google - クライアント ID の作成](checkout-and-payment-with-paypal/_static/image10.png)
7. [**クライアント ID**の作成] ダイアログで、アプリケーションの種類に応える既定の Web**アプリケーション**をそのまま使用します。
8. このチュートリアルで前に使用した SSL URL に **[許可された JavaScript の配信元**] を設定します (`https://localhost:44300/`他の SSL プロジェクトを作成していない場合)。   
   この URL は、アプリケーションの発信元です。 このサンプルでは、ローカルホストテスト URL のみを入力します。 ただし、ローカルホストと本番環境を考慮して複数の URL を入力できます。
9. **[Authorized Redirect URI]** には次の値を設定します。 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   この値は、ASP.NET OAuth ユーザーが Google の OAuth サーバーとの通信に使用する URI です。 上記で使用した SSL URL`https://localhost:44300/`を覚えておいてください (他の SSL プロジェクトを作成していない場合)。
10. [クライアント ID の**作成]** ボタンをクリックします。
11. Google デベロッパー コンソールの左側のメニューで、[**同意] 画面**のメニュー項目をクリックし、メールアドレスと製品名を設定します。 フォームに入力したら、[**保存**] をクリックします。
12. **API**メニュー項目をクリックし、下にスクロールして **、Google+ API**の横にある**オフ**ボタンをクリックします。   
    このオプションを受け入れると、Google+ API が有効になります。
13. また、**バージョン 3.0.0 に Microsoft.Owin** NuGet パッケージを更新する必要があります。   
    [**ツール**] メニューの **[NuGet パッケージ マネージャー** ] を選択し、[**ソリューションの NuGet パッケージの管理**] を選択します。  
    **[NuGet パッケージの管理**] ウィンドウで **、Microsoft.Owin**パッケージを見つけてバージョン 3.0.0 に更新します。
14. Visual Studio で、`UseGoogleAuthentication`**クライアント ID**と**クライアント シークレット**をコピーして、メソッドに貼り付け *、Startup.Auth.cs*ページのメソッドを更新します。 以下に示す**クライアント ID**と**クライアント シークレット**の値はサンプルで、機能しません。 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. **Ctrl キーを押しながら F5 キー**を押して、アプリケーションをビルドして実行します。 **[Log in]** リンクをクリックします。
16. [**別のサービスを使用してログイン**] の下にある **[Google]** をクリックします。  
    ![ログイン](checkout-and-payment-with-paypal/_static/image11.png)
17. 資格情報の入力が必要な場合、Google のサイトにリダイレクトされるので、リダイレクト先のサイトで資格情報を入力します。  
    ![Google - サインイン](checkout-and-payment-with-paypal/_static/image12.png)
18. 資格情報を入力すると、作成した Web アプリケーションにアクセス許可を与えるプロンプトが表示されます。  
    ![プロジェクトのデフォルト サービス アカウント](checkout-and-payment-with-paypal/_static/image13.png)
19. **[Accept]\(受け入れる\)** をクリックします。 これで、Google アカウントを登録できる**WingtipToys**アプリケーションの **[登録**] ページにリダイレクトされます。  
    ![Google アカウントへの登録](checkout-and-payment-with-paypal/_static/image14.png)
20. Google アカウントに使用するローカルの電子メール登録名を変更できますが、通常は既定の電子メール エイリアス (認証に使用したエイリアス) を変更しません。 上記**のように[ログイン]** をクリックします。

### <a name="modifying-login-functionality"></a>ログイン機能の変更

このチュートリアル シリーズで既に説明したように、ユーザー登録機能の多くは、既定では ASP.NET Web フォーム テンプレートに含まれています。 次に、メソッドを呼び出すために既定の*Login.aspx*ページ`MigrateCart`と*Register.aspx*ページを変更します。 この`MigrateCart`メソッドは、新しくログインしたユーザーを匿名ショッピング カートに関連付けます。 ユーザーとショッピング カートを関連付けることで、Wingtip Toys サンプル アプリケーションは、ユーザーのショッピング カートを訪問の間に維持することができます。

1. **ソリューション エクスプローラ**で *、[Account]* フォルダを探して開きます。
2. Login.aspx.cs*というコード*ビハインド ページを変更して、次のように表示されるように、黄色で強調表示されたコードを含めます。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. *Login.aspx.cs*ファイルを保存します。

ここでは、メソッドの定義が存在しないという警告を`MigrateCart`無視できます。 このチュートリアルでは、後で追加します。

*Login.aspx.cs*分離コード ファイルは、LogIn メソッドをサポートしています。 Login.aspx ページを調べることで、このページには、クリックするとコードビハインドのハンドラーを`LogIn`トリガーする 「ログイン」ボタンが含まれていることがわかります。

Login.aspx.csの`Login`メソッドが呼*Login.aspx.cs*び出されると、名前の付いた`usersShoppingCart`ショッピング カートの新しいインスタンスが作成されます。 ショッピング カートの ID (GUID) が取得され、変数に`cartId`設定されます。 次に、`MigrateCart`このメソッドが呼び出`cartId`され、ログインしているユーザーの名前との両方がこのメソッドに渡されます。 ショッピング カートを移行すると、匿名ショッピング カートの識別に使用される GUID がユーザー名に置き換えられます。

ユーザーがログインしたときにショッピング カートを移行するように*Login.aspx.cs*分離コード ファイルを変更する以外に、ユーザーが新しいアカウントを作成してログインしたときにショッピング カートを移行するように*Register.aspx.cs分離ファイル*を変更する必要があります。

1. *[アカウント*] フォルダで、 という名前のコード ビハインド ファイル*Register.aspx.cs*開きます。
2. コードを黄色で含めて、コードビハインド ファイルを次のように変更します。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. *Register.aspx.cs*ファイルを保存します。 もう一度、メソッドに関する`MigrateCart`警告を無視します。

`CreateUser_Click`イベント ハンドラーで使用したコードは、`LogIn`メソッドで使用したコードと非常によく似ています。 ユーザーがサイトに登録またはログインすると、`MigrateCart`メソッドの呼び出しが行われます。

## <a name="migrating-the-shopping-cart"></a>ショッピング カートの移行

ログインと登録のプロセスが更新されましたので、このメソッドを使用してショッピング カートを移行するコードを`MigrateCart`追加できます。

1. **ソリューション エクスプローラー**で*Logic*フォルダーを見つけて *、ShoppingCartActions.cs*クラス ファイルを開きます。
2. ShoppingCartActions.cs*ファイル内*の既存のコードに黄色で強調表示されたコードを追加して *、ShoppingCartActions.cs*ファイル内のコードが次のように表示されるようにします。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

この`MigrateCart`メソッドは、既存の cartId を使用して、ユーザーのショッピング カートを検索します。 次に、コードはすべてのショッピング カートのアイテムをループ処理し、`CartId``CartItem`プロパティ (スキーマで指定された) をログイン ユーザー名に置き換えます。

### <a name="updating-the-database-connection"></a>データベース接続の更新

このチュートリアルを**使用して、事前構築された**Wingtip Toys サンプル アプリケーションを使用する場合は、既定のメンバーシップ データベースを再作成する必要があります。 既定の接続文字列を変更すると、次回アプリケーションを実行する際にメンバーシップ データベースが作成されます。

1. プロジェクトのルートにある*Web.config*ファイルを開きます。
2. 次のように表示されるように、既定の接続文字列を更新します。   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>ペイパルの統合

PayPalは、オンライン加盟店による支払いを受け付けるウェブベースの課金プラットフォームです。 このチュートリアルでは、次にPayPalのエクスプレスチェックアウト機能をアプリケーションに統合する方法について説明します。 エクスプレスチェックアウトを使用すると、顧客はPayPalを使用してショッピングカートに追加したアイテムの支払いを行うことができます。

### <a name="create-paypal-test-accounts"></a>PayPal テスト アカウントの作成

PayPal テスト環境を使用するには、開発者テスト アカウントを作成して確認する必要があります。 開発者テスト アカウントを使用して、購入者テスト アカウントと販売者テスト アカウントを作成します。 開発者テスト アカウントの資格情報では、Wingtip Toys サンプル アプリケーションが PayPal テスト環境にアクセスすることもできます。

1. ブラウザで、PayPal 開発者テストサイトに移動します。   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. PayPal デベロッパー アカウントをお持ちの場合は、[**サインアップ**] をクリックし、サインアップ手順に従って新しいアカウントを作成します。 既存の PayPal 開発者アカウントをお持ちの場合は、[ログイン] をクリックして**ログイン**します。 このチュートリアルの後で Wingtip Toys サンプル アプリケーションをテストするには、PayPal 開発者アカウントが必要になります。
3. PayPal デベロッパーアカウントにサインアップしたばかりの場合は、PayPal で PayPal 開発者アカウントを確認する必要があります。 PayPal がメールアカウントに送信した手順に従って、アカウントを確認できます。 PayPal 開発者アカウントを確認したら、PayPal 開発者テストサイトにログインし直してください。
4. PayPal デベロッパーアカウントでPayPal開発者サイトにログインした後、PayPalの購入者テストアカウントをまだお持ちでない場合は、アカウントを作成する必要があります。 購入者のテスト アカウントを作成するには、PayPal サイトで [**アプリケーション**] タブをクリックし、[**サンドボックス アカウント**] をクリックします。   
 **[サンドボックス テスト アカウント**] ページが表示されます。   

    > [!NOTE] 
    > 
    > PayPal デベロッパー サイトでは、既にマーチャント テスト アカウントが提供されています。

    ![PayPal でのチェックアウトと支払い - サンドボックス テスト アカウント](checkout-and-payment-with-paypal/_static/image15.png)
5. [サンドボックス テスト アカウント] ページで、[**アカウントの作成**] をクリックします。
6. [**テスト アカウントの作成**] ページで、任意の購入者テスト アカウントの電子メールとパスワードを選択します。   

    > [!NOTE] 
    > 
    > このチュートリアルの最後で Wingtip Toys サンプル アプリケーションをテストするには、購入者の電子メール アドレスとパスワードが必要です。

    ![PayPal でのチェックアウトと支払い - サンドボックス テスト アカウント](checkout-and-payment-with-paypal/_static/image16.png)
7. [アカウントの作成] ボタンをクリックして、購入者テスト**アカウントを作成**します。  
 [**サンドボックス テスト アカウント**] ページが表示されます。 

    ![PayPal でのチェックアウトと支払い - ペイパル アカウント](checkout-and-payment-with-paypal/_static/image17.png)
8. [**サンドボックス テスト アカウント**] ページで、**ファシリテーター**の電子メール アカウントをクリックします。  
    **プロファイル**と**通知**のオプションが表示されます。
9. [**プロファイル**] オプションを選択し **、[API 資格情報**] をクリックして、マーチャント テスト アカウントの API 資格情報を表示します。
10. TEST API の資格情報をメモ帳にコピーします。

Wingtip Toys サンプル アプリケーションから PayPal テスト環境への API 呼び出しを行うには、表示されているクラシック TEST API の認証情報 (ユーザー名、パスワード、および署名) が必要です。 次の手順で資格情報を追加します。

### <a name="add-paypal-class-and-api-credentials"></a>PayPal クラスと API 資格情報の追加

PayPal コードの大半を 1 つのクラスに配置します。 このクラスには、PayPal との通信に使用されるメソッドが含まれています。 また、このクラスに PayPal 資格情報を追加します。

1. Visual Studio 内の Wingtip Toys サンプル アプリケーション**で、Logic**フォルダーを右クリックし、[**新しい項目**の**追加** -&gt;] を選択します。   
   **[新しい項目の追加]** ダイアログ ボックスが表示されます。
2. 左側の [**インストール済み**] ウィンドウの **[Visual C#** ] で、[**コード**] を選択します。
3. 中央のペインで 、[**クラス**] を選択します。 この新しいクラス**に名前を付PayPalFunctions.cs。**
4. **[追加]** をクリックします。  
   新しいクラス ファイルがエディターに表示されます。
5. 既定のコードを以下のコードに置き換えます。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. このチュートリアルで前に表示した Merchant API の認証情報 (ユーザー名、パスワード、および署名) を追加して、PayPal テスト環境に関数呼び出しを行うことができます。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> このサンプル アプリケーションでは、資格情報を C# ファイル (.cs) に追加するだけです。 ただし、実装されたソリューションでは、構成ファイルで資格情報を暗号化することを検討する必要があります。

クラスには、ほとんどの機能が含まれています。 クラスのコードは、PayPal テスト環境からテスト購入を行うために必要なメソッドを提供します。 購入には、次の 3 つの PayPal 関数が使用されます。

- `SetExpressCheckout` 関数
- `GetExpressCheckoutDetails` 関数
- `DoExpressCheckoutPayment` 関数

この`ShortcutExpressCheckout`メソッドは、ショッピング カートからテスト購入情報と製品の詳細を収集し`SetExpressCheckout`、PayPal 関数を呼び出します。 この`GetCheckoutDetails`メソッドは、購入の詳細を確認`GetExpressCheckoutDetails`し、テスト購入を行う前にPayPal関数を呼び出します。 この`DoCheckoutPayment`メソッドは、PayPal 関数を呼び出してテスト`DoExpressCheckoutPayment`環境からテスト購入を完了します。 残りのコードは、文字列のエンコード、文字列のデコード、配列の処理、資格情報の決定など、PayPal のメソッドとプロセスをサポートします。

> [!NOTE] 
> 
> PayPalでは[、PayPalのAPI仕様](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)に基づいてオプションの購入詳細を含めることができます。 Wingtip Toys サンプル アプリケーションでコードを拡張することで、ローカライズの詳細、製品の説明、税、顧客サービス番号、その他の多くのオプション フィールドを含めることができます。

**戻**りと取り消しメソッドで指定されている URL をキャンセルするポート番号を使用します。

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

ビジュアル Web 開発者が SSL を使用して Web プロジェクトを実行する場合、通常はポート 44300 が Web サーバーに使用されます。 上に示したように、ポート番号は 44300 です。 アプリケーションを実行すると、別のポート番号が表示される場合があります。 このチュートリアルの最後で Wingtip Toys サンプル アプリケーションを正常に実行できるように、ポート番号をコードで正しく設定する必要があります。 このチュートリアルの次のセクションでは、ローカル ホストポート番号を取得し、PayPal クラスを更新する方法について説明します。

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>PayPal クラスのローカルホスト ポート番号を更新します。

Wingtip Toys サンプル アプリケーションは、PayPal テスト サイトに移動し、Wingtip Toys サンプル アプリケーションのローカル インスタンスに戻って製品を購入します。 PayPal が正しい URL に戻るには、上記の PayPal コードでローカルで実行されているサンプル アプリケーションのポート番号を指定する必要があります。

1. **ソリューション エクスプローラ**でプロジェクト名 (**WingtipToys**) を右クリックし、[**プロパティ ]** を選択します。
2. 左側の列で **、[Web]** タブを選択します。
3. **[プロジェクト URL]** ボックスからポート番号を取得します。
4. 必要に応じて *、PayPalFunctions.cs*ファイルの PayPal`NVPAPICaller`クラス ( ) で、 web アプリケーションのポート番号を使用するように、`returnURL`を`cancelURL`更新します。   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

これで、追加したコードが、ローカル Web アプリケーションの想定されるポートと一致します。 PayPal は、ローカル コンピューター上の正しい URL に戻ることができるでしょう。

### <a name="add-the-paypal-checkout-button"></a>PayPal チェックアウト ボタンを追加する

サンプル アプリケーションにプライマリ PayPal 関数が追加されましたので、これらの関数を呼び出すために必要なマークアップとコードの追加を開始できます。 まず、ショッピング カート ページにユーザーに表示されるチェックアウト ボタンを追加する必要があります。

1. *ショッピングカート.aspx*ファイルを開きます。
2. ファイルの一番下までスクロールして、コメントを`<!--Checkout Placeholder -->`見つけます。
3. マークアップが次のように置`ImageButton`き換えられるように、コメントをコントロールに置き換えます。  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. *ShoppingCart.aspx.cs*ファイルで、イベント`UpdateBtn_Click`ハンドラーがファイルの末尾に近づくと、イベント`CheckOutBtn_Click`ハンドラーを追加します。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. また *、ShoppingCart.aspx.cs*ファイルで、新しいイメージ`CheckoutBtn`ボタンが次のように参照されるように、 への参照を追加します。  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. 変更を*ShoppingCart.aspx*ファイルと*ShoppingCart.aspx.cs*ファイルの両方に保存します。
7. メニューから[ビルド**Debug**-&gt;**ウィングヒントのデバッグ] を**選択します。  
   プロジェクトは、新しく追加された**ImageButton**コントロールで再構築されます。

### <a name="send-purchase-details-to-paypal"></a>購入の詳細を PayPal に送信する

ユーザーがショッピング カート ページ (*ShoppingCart.aspx*) の **[チェックアウト**] ボタンをクリックすると、購入プロセスが開始されます。 次のコードは、製品の購入に必要な最初のPayPal関数を呼び出します。

1. *チェックアウト*フォルダから *、CheckoutStart.aspx.cs*というコードビハインド ファイルを開きます。   
   コードビハインド ファイルを開いてください。
2. 既存のコードを次のコードに置き換えます。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

アプリケーションのユーザーがショッピング カート ページの **[チェックアウト**] ボタンをクリックすると、ブラウザーは*CheckoutStart.aspx*ページに移動します。 *ページ*が読み込まれると、メソッドが`ShortcutExpressCheckout`呼び出されます。 この時点で、ユーザーは PayPal テスト Web サイトに転送されます。 PayPalサイトでは、ユーザーがPayPalの資格情報を入力し、購入の詳細を確認し、PayPal契約を受け入れ、メソッドが完了したWingtip Toys`ShortcutExpressCheckout`サンプルアプリケーションに戻ります。 メソッドが`ShortcutExpressCheckout`完了すると、メソッドで指定された*CheckoutReview.aspx*ページにユーザーがリダイレクトされます`ShortcutExpressCheckout`。 これにより、Wingtip Toys サンプル アプリケーション内から注文の詳細を確認できます。

### <a name="review-order-details"></a>注文の詳細の確認

PayPal から戻った後、Wingtip Toys サンプル アプリケーションの*CheckoutReview.aspx*ページに注文の詳細が表示されます。 このページでは、製品を購入する前に注文の詳細を確認できます。 次のようにして *、CheckoutReview.aspx*ページを作成する必要があります。

1. *チェックアウト*フォルダで *、"CheckoutReview.aspx"* という名前のページを開きます。
2. 既存のマークアップを次のように置き換えます。   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. CheckoutReview.aspx.csというコードビハインド ページ*を*開き、既存のコードを次のコードに置き換えます。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

**DetailsView**コントロールは、PayPal から返された注文の詳細を表示するために使用されます。 また、上記のコードでは、Wingtip Toys データベースに注文の詳細`OrderDetail`をオブジェクトとして保存します。 ユーザーが [**完全な注文**] ボタンをクリックすると、ユーザーは *[チェックアウト完了.aspx]* ページにリダイレクトされます。

> [!NOTE] 
> 
> **ヒント**
> 
> *CheckoutReview.aspx*ページのマークアップでは、`<ItemStyle>`タグがページの下部にある**DetailsView**コントロール内の項目のスタイルを変更するために使用されていることに注意してください。 **デザイン ビュー**でページを表示し (Visual Studio の左下隅にある **[デザイン**] を選択して) **DetailsView**コントロールを選択し、**スマート タグ**(コントロールの右上にある矢印アイコン) を選択すると **、DetailsView タスク**が表示されます。
> 
> ![PayPal でのチェックアウトと支払い - フィールドの編集](checkout-and-payment-with-paypal/_static/image18.png)
> 
> [**フィールドの編集**] を選択すると、[**フィールド**] ダイアログ ボックスが表示されます。 このダイアログ ボックスでは **、DetailsView**コントロールの表示プロパティ **(ItemStyle**など) を簡単に制御できます。
> 
> ![PayPal でのチェックアウトと支払い - フィールド ダイアログ](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>完全購入

*チェックアウトコンプリート.aspx*ページは、ペイパルから購入を行います。 前述のように、アプリケーションが*CheckoutComplete.aspx*ページに移動する前に、ユーザーが **[完全な注文**] ボタンをクリックする必要があります。

1. *[チェックアウト*] フォルダで、[*チェックアウト完了.aspx]* という名前のページを開きます。
2. 既存のマークアップを次のように置き換えます。   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. *CheckoutComplete.aspx.cs*というコードビハインド ページを開き、既存のコードを次のコードに置き換えます。   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

*[チェックアウト完了.aspx]* ページが読み込`DoCheckoutPayment`まれると、メソッドが呼び出されます。 前述のとおり、この`DoCheckoutPayment`メソッドは PayPal テスト環境からの購入を完了します。 PayPal が注文の購入を完了すると *、CheckoutComplete.aspx*ページには、購入者`ID`への支払いトランザクションが表示されます。

### <a name="handle-cancel-purchase"></a>購入のキャンセルを処理する

ユーザーが購入をキャンセルすると決定した場合、ユーザーは*CheckoutCancel.aspx*ページに移動し、注文がキャンセルされたことを確認します。

1. チェックアウト*フォルダーで* *CheckoutCancel.aspx*という名前のページを開きます。
2. 既存のマークアップを次のように置き換えます。   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>購買エラーの処理

購入プロセス中のエラーは *、CheckoutError.aspx*ページによって処理されます。 エラーが発生した場合は *、CheckoutStart.aspx*ページ *、CheckoutReview.aspx*ページ、および*チェックアウトコンプリート.aspx*ページの分離コードがそれぞれ*CheckoutError.aspx*ページにリダイレクトされます。

1. チェックアウト*フォルダーで* *CheckoutError.aspx*という名前のページを開きます。
2. 既存のマークアップを次のように置き換えます。   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

*チェックアウト処理中に*エラーが発生すると、エラーの詳細が表示されます。

## <a name="running-the-application"></a>アプリケーションの実行

アプリケーションを実行して、製品の購入方法を確認します。 PayPal テスト環境で実行されることに注意してください。 実際のお金は交換されません。

1. すべてのファイルが Visual Studio に保存されていることを確認します。
2. Web ブラウザを開き、[https://developer.paypal.com](https://developer.paypal.com/)に移動します。
3. このチュートリアルで前に作成した PayPal 開発者アカウントでログインします。  
   PayPal の開発者サンドボックスでは、エクスプレスチェックアウトをテストするためにログイン[https://developer.paypal.com](https://developer.paypal.com/)する必要があります。 これは、PayPalのサンドボックステストにのみ適用され、PayPalのライブ環境には適用されません。
4. Visual Studio で**F5**キーを押して、Wingtip Toys サンプル アプリケーションを実行します。  
   データベースの再構築後、ブラウザーが開き *、Default.aspx*ページが表示されます。
5. "Cars" などの商品カテゴリを選択し、各商品の横にある [**カートに追加**] をクリックして、ショッピング カートに 3 つの異なる製品を追加します。  
   ショッピング カートには、選択した商品が表示されます。
6. PayPal**PayPal**ボタンをクリックしてチェックアウトします。 

    ![PayPalでのチェックアウトと支払い - カート](checkout-and-payment-with-paypal/_static/image20.png)

   チェックアウトするには、Wingtip Toys サンプル アプリケーションのユーザー アカウントが必要です。
7. ページの右側にある**Google**リンクをクリックして、既存のgmail.comメールアカウントでログインします。  
   gmail.com アカウントがない場合は、[テスト](https://www.gmail.com/)目的で作成www.gmail.com。 [登録] をクリックして、標準のローカル アカウントを使用することもできます。 

    ![PayPalでのチェックアウトと支払い - ログイン](checkout-and-payment-with-paypal/_static/image21.png)
8. Gmail アカウントとパスワードでログインします。 

    ![PayPal でのチェックアウトと支払い - Gmail サインイン](checkout-and-payment-with-paypal/_static/image22.png)
9. [**ログイン**] ボタンをクリックして、Gmail アカウントを Wingtip Toys サンプル アプリケーションのユーザー名で登録します。 

    ![PayPalでのチェックアウトと支払い - アカウント登録](checkout-and-payment-with-paypal/_static/image23.png)
10. PayPal テスト サイトで、このチュートリアルで前に作成した**購入者**の電子メール アドレスとパスワードを追加し、[**ログイン**] ボタンをクリックします。 

    ![PayPal でのチェックアウトと支払い - ペイパル サインイン](checkout-and-payment-with-paypal/_static/image24.png)
11. PayPal ポリシーに同意し、[**同意して続行**] ボタンをクリックします。  
    このページは、このPayPalアカウントを初めて使用する場合にのみ表示されます。 再び、これはテストアカウントであり、実際のお金は交換されません。 

    ![ペイパルでのチェックアウトと支払い - ペイパルポリシー](checkout-and-payment-with-paypal/_static/image25.png)
12. PayPal テスト環境レビュー ページで注文情報を確認し、[**続行**] をクリックします。 

    ![PayPal によるチェックアウトと支払い - レビュー情報](checkout-and-payment-with-paypal/_static/image26.png)
13. *[CheckoutReview.aspx]* ページで、注文金額を確認し、生成された送付先住所を表示します。 次に、[**注文の完了**] ボタンをクリックします。 

    ![PayPal によるチェックアウトと支払い - オーダーレビュー](checkout-and-payment-with-paypal/_static/image27.png)
14. **[チェックアウト完了.aspx]** ページが、支払トランザクション ID と共に表示されます。 

    ![PayPal でのチェックアウトと支払い - チェックアウト完了](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>データベースの確認

アプリケーションの実行後に Wingtip Toys サンプル アプリケーション データベースで更新されたデータを確認すると、アプリケーションが製品の購入を正常に記録したことがわかります。

*Wingtiptoys.mdf*データベース ファイルに含まれるデータは、このチュートリアル シリーズで前述したように、**データベース エクスプローラー**ウィンドウ (Visual Studio の**サーバー エクスプローラー**ウィンドウ) を使用して検査できます。

1. ブラウザ ウィンドウが開いている場合は、閉じます。
2. Visual Studio で、**ソリューション エクスプローラー**の上部にある **[すべてのファイルを表示**] アイコンを選択して、[アプリ**\_データ**] フォルダーを展開できるようにします。
3. **[アプリ\_データ**] フォルダーを展開します。  
 フォルダの **[すべてのファイルを表示]** アイコンを選択する必要がある場合があります。
4. *Wingtiptoys.mdf*データベース ファイルを右クリックし、[**開く**] を選択します。  
    **サーバー エクスプローラ**が表示されます。
5. **[テーブル]** フォルダーを展開します。
6. **[受注]** テーブルを右クリックし、[**テーブル データの表示**] を選択します。  
 **[受注]** テーブルが表示されます。
7. [**支払トランザクション ID]** 列を確認して、トランザクションが正常に終了したことを確認します。 

    ![PayPal でのチェックアウトと支払い - データベースの確認](checkout-and-payment-with-paypal/_static/image29.png)
8. **[受注]** テーブル ウィンドウを閉じます。
9. サーバー エクスプローラで **、OrderDetails**テーブルを右クリックし、[**テーブル データの表示**] を選択します。
10. `OrderId` **[受注明細]** テーブルの値と`Username`値を確認します。 これらの値は **、Orders** `OrderId`テーブル`Username`に含まれる値と 値と一致します。
11. **[受注明細]** テーブル ウィンドウを閉じます。
12. Wingtip Toys データベース ファイル (*Wingtiptoys.mdf*) を右クリックし、[**接続を閉じる**] を選択します。
13. **[ソリューション エクスプローラー** ] ウィンドウが表示されない場合は、[**サーバー エクスプローラー** ] ウィンドウの下部にある [ソリューション**エクスプローラー** ] をクリックして、**ソリューション エクスプローラー**を再度表示します。

## <a name="summary"></a>まとめ

このチュートリアルでは、注文と注文の詳細スキーマを追加して、製品の購入を追跡しました。 また、Wingtip Toys サンプル アプリケーションに PayPal 機能を統合しました。

## <a name="additional-resources"></a>その他のリソース

[ASP.NET構成の概要](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[Azure アプリ サービスにメンバーシップ、OAuth、および SQL データベースを使用してセキュリティで保護されたASP.NET Web フォーム アプリを展開する](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[マイクロソフト Azure - 無料試用版](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>免責事項

このチュートリアルには、サンプル コードが含まれています。 このようなサンプルコードは、いかなる種類の保証もなく「ありがち」に提供されます。 したがって、マイクロソフトは、サンプル コードの正確性、完全性、または品質を保証しません。 お客様は、ご自身の責任でサンプルコードを使用することに同意します。 いかなる場合でも、サンプル コード、コンテンツ、サンプル コード、コンテンツ、またはサンプル コードの使用によって生じたあらゆる種類の損失または損害に関するエラーや欠落を含むが、これらに限定されないいかなる方法でも、Microsoft はユーザーに対して責任を負いません。 お客様は、ここに通知され、マイクロソフトがいかなる損失、損失の主張、傷害または損害の請求、その中に表明された見解を含むがこれらに限定されない、またはそれらに限定されないあらゆる種類の損害に対して無害にマイクロソフトを補償、保存、保持することに同意します。

> [!div class="step-by-step"]
> [前へ](shopping-cart.md)
> [次へ](membership-and-administration.md)
