---
title: gRPC ストリーミングサービスと繰り返し使用するフィールド-WCF 開発者向け gRPC
description: GRPC を使用してデータのコレクションを渡す方法として、繰り返しフィールドとストリーミングサービスを比較します。
ms.date: 09/02/2019
ms.openlocfilehash: f2f13776586607ed489c45ebb324c0c5713bed99
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73966917"
---
# <a name="grpc-streaming-services-versus-repeated-fields"></a>gRPC streaming services と繰り返されるフィールド

gRPC サービスには、データセットを返すための2つの方法、またはオブジェクトの一覧が用意されています。 プロトコルバッファーメッセージの指定では、別のメッセージ内のメッセージのリストまたは配列を宣言するために `repeated` キーワードを使用します。 GRPC サービスの仕様では、`stream` キーワードを使用して、複数のメッセージを個別に送信して処理できる、長時間実行される永続的な接続を宣言します。 `stream` 機能は、通知やログメッセージなどの長時間実行されるテンポラルデータにも使用できますが、この章では、1つのデータセットを返すための使用方法を検討します。

使用する必要があるのは、データセット全体のサイズ、クライアントまたはサーバー側でデータセットを作成するのにかかった時間、および最初の項目が使用可能になったらすぐにデータセットのコンシューマーがアクションを開始できるかどうかなど、さまざまな要因によって異なります。またはは、役に立つすべてのデータセットを必要とします。

## <a name="when-to-use-repeated-fields"></a>`repeated` フィールドを使用する場合

サイズが制限され、短時間で完全に生成できるデータセットの場合 (1 秒未満の場合など) は、通常の Protobuf メッセージで `repeated` フィールドを使用する必要があります。 たとえば、e コマースシステムでは、注文内の項目のリストを作成するのは簡単であり、リストが非常に大きくなるとは限りません。 `repeated` フィールドを持つ1つのメッセージを返すのは、`stream` を使用する場合よりもはるかに高速であり、ネットワークオーバーヘッドが少なくなります。

クライアントが処理を開始する前にすべてのデータを必要とし、データセットがメモリに構築するのに十分な大きさである場合は、サーバーのメモリにデータセットの実際の作成速度が遅い場合でも、`repeated` フィールドの使用を検討してください。

## <a name="when-to-use-stream-methods"></a>`stream` メソッドを使用する場合

メッセージオブジェクトが非常に大きくなる可能性があるデータセットは、ストリーミング要求または応答を使用して転送することをお勧めします。 メモリ内に大きなオブジェクトを構築し、それをネットワークに書き込んで、リソースを解放する方が効率的です。 このアプローチにより、サービスのスケーラビリティが向上します。

同様に、制約のないサイズのデータセットをストリーム経由で送信して、メモリが不足しないようにする必要があります。

コンシューマーが個々の項目を個別に処理できるデータセットの場合、進行状況をエンドユーザーに示すことができる場合は、ストリームの使用を検討する必要があります。 これにより、アプリケーションのパフォーマンスが低下する可能性がありますが、アプリケーションの全体的なパフォーマンスに対してバランスを取る必要があります。

また、ストリームが役に立つ可能性があるもう1つのシナリオは、メッセージが複数のサービスにわたって処理される場所です。 チェーン内の各サービスが1つのストリームを返す場合、ターミナルサービス (つまり、チェーン内の最後のサービス) は、処理して元の要求元に渡すことができるメッセージを返すことができます。これは、ストリームを返すか、または結果は1つの応答メッセージになります。 このアプローチは、Map/Reduce のようなパターンに適しています。

>[!div class="step-by-step"]
>[前へ](migrate-duplex-services.md)
>[次へ](client-libraries.md)
