---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: EF 5 mvc 4 のチュートリアル」の章を構築ダウンロード |Microsoft Docs
author: Rick-Anderson
description: Contoso University のサンプルの web アプリケーションでは、Entity Framework 5 Code First と Visual Studio を使用して ASP.NET MVC 4 アプリケーションを作成する方法について説明しています.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 1138f1512690e01a09c73623c0d8db4a31eb921b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65129841"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a><span data-ttu-id="54c33-103">EF 5 mvc 4 のチュートリアル」の章を構築ダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="54c33-103">Building the Chapter Downloads for the EF 5 MVC 4 Tutorials</span></span>

<span data-ttu-id="54c33-104">によって[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="54c33-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[<span data-ttu-id="54c33-105">完成したプロジェクトのダウンロード</span><span class="sxs-lookup"><span data-stu-id="54c33-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="54c33-106">Contoso University のサンプルの web アプリケーションでは、Entity Framework 5 Code First と Visual Studio 2012 を使用して ASP.NET MVC 4 アプリケーションを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="54c33-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="54c33-107">チュートリアル シリーズについては、[シリーズの最初のチュートリアル](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="54c33-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

## <a name="building-the-chapter-downloads"></a><span data-ttu-id="54c33-108">章ダウンロードの構築</span><span class="sxs-lookup"><span data-stu-id="54c33-108">Building the Chapter Downloads</span></span>

1. <span data-ttu-id="54c33-109">ダウンロードしてプロジェクト サンプルの zip ファイルを解凍します。</span><span class="sxs-lookup"><span data-stu-id="54c33-109">Download and unzip the  project sample zip file.</span></span> <span data-ttu-id="54c33-110">解凍したダウンロード パッケージに追加の zip ファイル、各章の完了のいずれかが表示されます。</span><span class="sxs-lookup"><span data-stu-id="54c33-110">In the unzipped download package, you will find additional zip files, one for the completion of each chapter.</span></span>
2. <span data-ttu-id="54c33-111">目的の zip ファイルを右クリック**プロパティ**、 をクリックし、**ブロックの解除**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="54c33-111">Right click on the desired zip file, click **Properties**, and click the **Unblock** button.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. <span data-ttu-id="54c33-112">ファイルを解凍します。</span><span class="sxs-lookup"><span data-stu-id="54c33-112">Unzip the file.</span></span>
4. <span data-ttu-id="54c33-113">ダブルクリックして、 *CUx.sln*ファイルを Visual Studio を起動します。</span><span class="sxs-lookup"><span data-stu-id="54c33-113">Double-click the *CUx.sln* file to launch Visual Studio.</span></span>
5. <span data-ttu-id="54c33-114">**ツール** メニューのをクリックして**NuGet パッケージ マネージャー**、し**パッケージ マネージャー コンソール**します。</span><span class="sxs-lookup"><span data-stu-id="54c33-114">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. <span data-ttu-id="54c33-115">パッケージ マネージャー コンソール (PMC) をクリックして**復元**します。</span><span class="sxs-lookup"><span data-stu-id="54c33-115">In the Package Manager Console (PMC), click **Restore**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. <span data-ttu-id="54c33-116">Visual Studio を終了します。</span><span class="sxs-lookup"><span data-stu-id="54c33-116">Exit Visual Studio.</span></span>
8. <span data-ttu-id="54c33-117">上記の手順で終了するソリューション ファイルを開き、Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="54c33-117">Restart Visual Studio, opening the solution file you closed in the step above.</span></span>
9. <span data-ttu-id="54c33-118">パッケージ マネージャー コンソール (PMC) を入力、`Update-Database`コマンド。</span><span class="sxs-lookup"><span data-stu-id="54c33-118">In the Package Manager Console (PMC), enter the `Update-Database` command:</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > <span data-ttu-id="54c33-119">: 次のエラーが発生した場合</span><span class="sxs-lookup"><span data-stu-id="54c33-119">If you get the following error:</span></span>  
    >   
    >  <span data-ttu-id="54c33-120">*'データベースの更新' という用語はコマンドレット、関数、スクリプト ファイル、または操作可能なプログラムの名前として認識されません。名前のスペルを確認するか、パスが正しいことを確認し、もう一度お試しパスが含まれている場合。*</span><span class="sxs-lookup"><span data-stu-id="54c33-120">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*</span></span>  
    > <span data-ttu-id="54c33-121">終了し、Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="54c33-121">Exit and restart Visual Studio.</span></span>

    <span data-ttu-id="54c33-122">各移行を実行し、seed メソッドが実行されます。</span><span class="sxs-lookup"><span data-stu-id="54c33-122">Each migration will run, then the seed method will run.</span></span> <span data-ttu-id="54c33-123">アプリを実行できます。</span><span class="sxs-lookup"><span data-stu-id="54c33-123">You can now run the app.</span></span>

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [<span data-ttu-id="54c33-124">前へ</span><span class="sxs-lookup"><span data-stu-id="54c33-124">Previous</span></span>](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
