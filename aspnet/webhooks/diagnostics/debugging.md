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
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="e9bbe-103">ASP.NETウェブフックデバッグ</span><span class="sxs-lookup"><span data-stu-id="e9bbe-103">ASP.NET WebHooks debugging</span></span>

## <a name="debugging-in-azure"></a><span data-ttu-id="e9bbe-104">Azure でのデバッグ</span><span class="sxs-lookup"><span data-stu-id="e9bbe-104">Debugging in Azure</span></span>

<span data-ttu-id="e9bbe-105">Azure で実行している間に Web アプリケーションをデバッグするには[、「Visual Studio を使用して Azure アプリ サービスで Web アプリをトラブルシューティングする」](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)のチュートリアルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="e9bbe-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="e9bbe-106">ソースとシンボルを使用したデバッグ</span><span class="sxs-lookup"><span data-stu-id="e9bbe-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="e9bbe-107">独自のコードをデバッグするだけでなく、Microsoft ASP.NET WebHooks に直接デバッグすることも、実際には .NET のすべてにデバッグすることもできます。</span><span class="sxs-lookup"><span data-stu-id="e9bbe-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="e9bbe-108">これは、ローカルでデバッグするかリモートでデバッグするかにかかわらず機能します。</span><span class="sxs-lookup"><span data-stu-id="e9bbe-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="e9bbe-109">まず **、Visual** Studio を構成してソースとシンボルを見つけるには、[デバッグ]、[**オプションと設定]** の順に移動します。</span><span class="sxs-lookup"><span data-stu-id="e9bbe-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="e9bbe-110">次のようにオプションを設定します。</span><span class="sxs-lookup"><span data-stu-id="e9bbe-110">Set the options like this:</span></span>

![オプションと設定](_static/SourceSymbols.png)

<span data-ttu-id="e9bbe-112">次に、ソースとシンボルをダウンロードするための[リンクをsymbolsource.org](http://symbolsource.org)に追加します。</span><span class="sxs-lookup"><span data-stu-id="e9bbe-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="e9bbe-113">上記のメニューの **[シンボル**] タブに移動し、シンボルの場所として次の項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="e9bbe-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="e9bbe-114">さらに、キャッシュ ディレクトリに短い名前が付いていることを確認します。そうしないと、ファイル名が長くなりすぎてシンボルがロードされなくなる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e9bbe-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="e9bbe-115">サンプル パスは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="e9bbe-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="e9bbe-116">設定は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="e9bbe-116">The settings should look similar to this:</span></span>

![オプション シンボル ファイルの場所の例](_static/SymSource.png)
