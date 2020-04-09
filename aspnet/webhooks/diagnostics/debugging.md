---
uid: webhooks/diagnostics/debugging
title: ASP.NET WebHook デバッグ |マイクロソフトドキュメント
author: rick-anderson
description: ASP.NETの WebHook をデバッグする方法。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 2f1f8196478e7025a0467acb945d9ed36c8fd0ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675376"
---
# <a name="aspnet-webhooks-debugging"></a>ASP.NETウェブフックデバッグ

## <a name="debugging-in-azure"></a>Azure でのデバッグ

Azure で実行している間に Web アプリケーションをデバッグするには[、「Visual Studio を使用して Azure アプリ サービスで Web アプリをトラブルシューティングする」](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)のチュートリアルを参照してください。

## <a name="debugging-with-source-and-symbols"></a>ソースとシンボルを使用したデバッグ

独自のコードをデバッグするだけでなく、Microsoft ASP.NET WebHooks に直接デバッグすることも、実際には .NET のすべてにデバッグすることもできます。 これは、ローカルでデバッグするかリモートでデバッグするかにかかわらず機能します。 まず **、Visual** Studio を構成してソースとシンボルを見つけるには、[デバッグ]、[**オプションと設定]** の順に移動します。 次のようにオプションを設定します。

![オプションと設定](_static/SourceSymbols.png)

次に、ソースとシンボルをダウンロードするための[リンクをsymbolsource.org](http://symbolsource.org)に追加します。 上記のメニューの **[シンボル**] タブに移動し、シンボルの場所として次の項目を追加します。

```
http://srv.symbolsource.org/pdb/Public
```

さらに、キャッシュ ディレクトリに短い名前が付いていることを確認します。そうしないと、ファイル名が長くなりすぎてシンボルがロードされなくなる可能性があります。 サンプル パスは次のとおりです。

```
C:\SymCache
```

設定は次のようになります。

![オプション シンボル ファイルの場所の例](_static/SymSource.png)
