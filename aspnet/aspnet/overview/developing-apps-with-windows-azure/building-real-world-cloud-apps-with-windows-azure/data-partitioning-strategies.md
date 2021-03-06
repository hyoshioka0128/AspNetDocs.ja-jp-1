---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
title: データのパーティション分割戦略 (Azure を使用した実際のクラウドアプリの構築) |Microsoft Docs
author: MikeWasson
description: Azure 電子ブックを使用した実際のクラウドアプリの構築は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 13のパターンとベストプラクティスについて説明します。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 513837a7-cfea-4568-a4e9-1f5901245d24
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
msc.type: authoredcontent
ms.openlocfilehash: efc3fa0255aa765e515412c5fa4098303a9d9234
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500836"
---
# <a name="data-partitioning-strategies-building-real-world-cloud-apps-with-azure"></a>データのパーティション分割戦略 (Azure を使用した実際のクラウドアプリの構築)

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[修正 It プロジェクトをダウンロード](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)するか[、電子書籍をダウンロード](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)します

> Azure 電子ブック**を使用した実際のクラウドアプリの構築**は、Scott Guthrie によって開発されたプレゼンテーションに基づいています。 ここでは、クラウド用の web アプリの開発を成功させるのに役立つ13のパターンとプラクティスについて説明します。 シリーズの詳細については、[最初の章](introduction.md)を参照してください。

前に、web サーバーを追加したり削除したりすることにより、クラウドアプリケーションの web 層を簡単に拡張できるようになりました。 しかし、すべてが同じデータストアに到達した場合は、アプリケーションのボトルネックがフロントエンドからバックエンドに移動し、データ層のスケーリングが最も困難になります。 この章では、データを複数のリレーショナルデータベースにパーティション分割したり、リレーショナルデータベースストレージを他のデータストレージオプションと組み合わせたりして、データ層をスケーラブルにする方法について説明します。

パーティション構成は、前に説明したのと同じ理由で事前に設定することをお勧めします。アプリが運用環境にある場合、データストレージ戦略を変更するのは非常に困難です。 さまざまなアプローチについて事前に検討している場合は、アプリのデータとデータアクセスコードを再編成している間に、アプリがクラッシュしたり、長時間にダウンしたりすることを避けることができます。

## <a name="the-three-vs-of-data-storage"></a>データストレージの3対3

パーティション分割戦略とその必要があるかどうかを判断するには、データに関して次の3つの点を考慮してください。

- ボリューム–最終的に格納されるデータ量を確認できます。 数ギガバイトでしょうか。 数百ギガバイトですか? 何? ペタバイト規模?
- ベロシティ–データが拡張される速度を指定します。 大量のデータを生成していない内部アプリケーションですか。 お客様が画像とビデオをアップロードする外部アプリ
- さまざま–どのような種類のデータを格納しますか。 リレーショナル、画像、キーと値のペア、ソーシャルグラフ

大量のボリューム、ベロシティ、またはさまざまなものがあると思われる場合は、どのような種類のパーティション構成を使用するかを慎重に検討する必要があります。これにより、アプリの規模が拡大したときに効率と効率が向上し、ボトルネックが発生しないようにすることができます。

基本的に、パーティション分割には次の3つの方法があります。

- 垂直的パーティション分割
- 行方向のパーティション分割
- ハイブリッドパーティション分割

## <a name="vertical-partitioning"></a>垂直的パーティション分割

Vertical portioning は、列によってテーブルを分割するのと似ています。1つの列セットが1つのデータストアに格納され、別の列セットが別のデータストアに移動します。

たとえば、アプリがユーザーに関するデータ (画像など) を格納しているとします。

![データ テーブル](data-partitioning-strategies/_static/image1.png)

このデータをテーブルとして表現し、さまざまな種類のデータを確認すると、左側の3つの列には、リレーショナルデータベースによって効率的に格納できる文字列データが含まれていることがわかります。右側の2つの列は、実質的には c を表すバイト配列です。イメージファイルからの ome。 画像ファイルのデータはリレーショナルデータベースに格納することができ、多くのユーザーがデータをファイルシステムに保存する必要がないためです。 ファイルシステムが必要な量のデータを格納できない場合や、別のバックアップおよび復元システムを管理したくない場合があります。 この方法は、オンプレミスのデータベースや、クラウドデータベースの少量のデータに適しています。 オンプレミス環境では、DBA があらゆることを処理できるようにする方が簡単な場合があります。

しかし、クラウドデータベースでは、ストレージの負荷が比較的高く、大量のイメージによって、データベースのサイズが、効率よく動作できる制限を超えて増加する可能性があります。 これらの問題に対処するには、データを垂直方向にパーティション分割します。つまり、データテーブルの列ごとに最適なデータストアを選択します。 この例に最適な方法は、文字列データをリレーショナルデータベースに格納し、イメージを Blob storage に格納することです。

![データテーブルの垂直方向のパーティション分割](data-partitioning-strategies/_static/image2.png)

データベースではなく Blob storage にイメージを格納することは、オンプレミス環境よりもクラウドでより実用的です。これは、ファイルサーバーのセットアップや、リレーショナルデータベースの外部に格納されたデータのバックアップと復元の管理について心配する必要がないためです。これは、Blob ストレージサービスによって自動的に処理されます。

これは、Fix It アプリで実装したパーティション分割アプローチであり、 [Blob storage の章](unstructured-blob-storage.md)にあるコードを確認します。 このパーティション構成を使用しない場合、平均イメージサイズが 3 mb であることを前提として、修正プログラムの It アプリでは、データベースの最大サイズである 150 gb に達する前に、4万のタスクについてのみ保存できます。 イメージを削除した後、データベースには複数のタスクを10回格納できます。行方向のパーティション構成の実装について考える前に、もっと長くすることができます。 また、アプリケーションの規模が拡大するにつれて、ストレージのニーズの大部分が非常に安価な Blob ストレージになるため、コストが増大します。

## <a name="horizontal-partitioning-sharding"></a>水平的パーティション分割 (シャーディング)

水平 portioning は、行ごとにテーブルを分割するのと似ています。1つの行セットを1つのデータストアに格納し、別の行セットを別のデータストアに移動します。

同じデータセットを使用する場合は、別の方法として、異なるデータベースに顧客名の異なる範囲を格納する方法があります。

![行方向にパーティション分割されたデータテーブル](data-partitioning-strategies/_static/image3.png)

ホットスポットを避けるために、データが均等に分散されていることを確認するために、シャーディングスキームに細心の注意を払う必要があります。 この単純な例では、姓の最初の文字を使用した場合、その要件を満たしていません。これは、多くの人間が、特定の共通文字で始まる姓を持っているためです。 一部のデータベースは非常に大きくなり、ほとんどは小さいままになるため、予想よりも早くテーブルサイズの制限に達しました。

行方向のパーティション分割の下側では、すべてのデータに対してクエリを実行するのが困難な場合があります。 この例では、アプリケーションによって格納されているすべてのデータを取得するために、最大26個の異なるデータベースからクエリを作成する必要があります。

## <a name="hybrid-partitioning"></a>ハイブリッドパーティション分割

垂直方向と水平方向のパーティション分割を組み合わせることができます。 たとえば、データの例では、イメージを Blob ストレージに格納し、文字列データを水平方向にパーティション分割することができます。

![データテーブルハイブリッドパーティション](data-partitioning-strategies/_static/image4.png)

## <a name="partitioning-a-production-application"></a>運用アプリケーションのパーティション分割

概念的には、パーティション構成がどのように動作するかを簡単に確認できますが、パーティション構成によってコードの複雑さが増し、多くの新しい複雑さが発生します。 イメージを blob ストレージに移動する場合、ストレージサービスがダウンしている場合はどうすればよいですか。 Blob のセキュリティをどのように処理しますか? データベースと blob ストレージが同期していない場合はどうなりますか。 シャーディングの場合、すべてのデータベースに対してクエリをどのように処理するのでしょうか。

このような複雑さは、運用環境に移行する前に計画している限り、管理しやすくなっています。 そのような作業を行っていなかった多くの人は、後で必要としていました。 平均では、お客様のアドバイザリチーム (CAT) チームは、アプリが非常に大きな形で終了している顧客から毎月 panicked の電話を受けることができ、この計画は行われませんでした。 次のようなものがあります。 "Help! すべてを1つのデータストアに配置します。また、45日では、空き領域が不足します。 また、データストアへのアクセス方法に多数のビジネスロジックが組み込まれていて、アプリを使用している顧客がいる場合は、移行中に1日にダウンするのは得策ではありません。 最終的には、ダウンタイムなしでお客様のデータをすぐにパーティション分割できるように、herculean の取り組みを進めていきます。 非常に魅力的で、非常に恐ろしいものであり、避けることができる場合には何もする必要はありません。 これを事前に検討してアプリに統合することで、アプリが後で拡大した場合に、より簡単に生活できるようになります。

## <a name="summary"></a>まとめ

効果的なパーティション構成を使用すると、クラウドアプリでボトルネックを発生させることなく、クラウド内のペタバイト単位のデータに拡張できます。 また、アプリケーションをオンプレミスのデータセンターで実行していた場合と同じように、大規模なコンピューターや広範なインフラストラクチャについては、事前に支払う必要がありません。 クラウドでは、必要に応じて容量を段階的に追加することができ、使用した分だけ料金がかかります。

次の[章](unstructured-blob-storage.md)では、Blob storage にイメージを格納することで、It アプリの修正によって列方向のパーティション分割がどのように実装されるかを説明します。

## <a name="resources"></a>リソース

パーティション分割の方法の詳細については、次のリソースを参照してください。

ドキュメント

- [Windows Azure Cloud Services で大規模なサービスを設計するためのベストプラクティス](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 マーク Simm と Michael Thomassy によるホワイトペーパー。
- [Microsoft のパターンとプラクティス-クラウド設計パターン](https://msdn.microsoft.com/library/dn568099.aspx)。 「データのパーティション分割のガイダンス、シャーディングパターン」を参照してください。

ビデオ:

- [フェイルセーフ: スケーラブルで回復力のある Cloud Services を構築](https://channel9.msdn.com/Series/FailSafe)します。 Ulrich Homann、Marc Mercuri、Mark Simm による9パートシリーズ。 高度な概念とアーキテクチャの原則を、非常にアクセスしやすく興味深い方法で紹介します。実際の顧客との Microsoft カスタマーアドバイザリチーム (CAT) エクスペリエンスによってストーリーが描画されます。 エピソード7のパーティション分割の説明を参照してください。
- [大規模なビルド: Windows Azure のお客様から学んだ教訓-パート I](https://channel9.msdn.com/Events/Build/2012/3-029)。マーク Simm は、19:49 から始まるパーティション分割スキーム、シャーディング戦略、シャーディングの実装方法、フェデレーションの SQL Database について説明します。 フェイルセーフシリーズに似ていますが、さらに詳細な方法について説明します。

サンプル コード:

- [Windows Azure のクラウドサービスの基礎](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 シャード化データベースを含むサンプルアプリケーション。 実装されているシャーディングスキームの詳細については、Windows Azure ブログの「 [DAL –シャーディング OF RDBMS](https://blogs.msdn.com/b/windowsazure/archive/2013/09/05/dal-sharding-of-rdbms.aspx) 」を参照してください。

> [!div class="step-by-step"]
> [前へ](data-storage-options.md)
> [次へ](unstructured-blob-storage.md)
