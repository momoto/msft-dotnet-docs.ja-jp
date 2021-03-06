---
title: カスタム アクティビティの使用
ms.date: 03/30/2017
ms.assetid: 8f356419-681a-4175-ae93-878eee970249
ms.openlocfilehash: 6ca67ef7a8c4330d0182e960fc3fdcce656976a4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962220"
---
# <a name="using-a-custom-activity"></a>カスタム アクティビティの使用
<xref:System.Activities.Activity> またはそのサブクラスから派生するアクティビティは、結合してより大規模なワークフローにしたり、コードで直接作成したりすることができます。 このトピックでは、コードまたはデザイナーで作成したワークフロー内でカスタム アクティビティを使用する方法について説明します。  
  
> [!NOTE]
> カスタムアクティビティは、それらが定義されているのと同じプロジェクトで使用できます。ただし、カスタムアクティビティとそれを使用するアクティビティの両方がコンパイルされる (つまり、ビルド処理によって生成される型によって読み込まれる) 場合は、参照元のアクティビティが読み込まれる場合に限ります。動的に (たとえば、ActivityXAMLServices を使用して)、参照されたアセンブリを別のプロジェクトに配置するか、デザイナーで生成された XAML を手動で編集してこれを有効にする必要があります。  
  
#### <a name="using-a-custom-activity-to-a-workflow-project"></a>ワークフロー プロジェクトへのカスタム アクティビティの使用  
  
1. ホスト プロジェクトから、カスタム アクティビティを含むアクティビティ ライブラリ プロジェクトへの参照を追加します。  
  
2. ソリューションをビルドします。  
  
3. デザイナーでカスタム アクティビティを使用するには、ツールボックスでカスタム アクティビティを探して、そのアクティビティをデザイナー画面にドラッグします。  
  
4. コード内でカスタム アクティビティを使用するには、カスタム アクティビティ プロジェクトを参照する Using ステートメントを追加し、そのアクティビティの新しいインスタンスを <xref:System.Activities.WorkflowInvoker.Invoke%2A> に渡します。
