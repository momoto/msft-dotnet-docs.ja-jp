---
title: '方法: Windows フォームの RichTextBox コントロールを使用してインデント、ぶら下げインデント、箇条書き段落を設定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- text boxes [Windows Forms], setting indents
- .rtf files [Windows Forms], formatting in RichTextBox control
- examples [Windows Forms], text boxes
- RTF files [Windows Forms], formatting in RichTextBox control
- RichTextBox control [Windows Forms], setting indents and bullets
- text boxes [Windows Forms], bullets
ms.assetid: abfb40e6-5642-4691-8ec1-9d9ae91688dc
ms.openlocfilehash: 9d095e3561cd346e6dbd99d1be7468f6ad5725a6
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960453"
---
# <a name="how-to-set-indents-hanging-indents-and-bulleted-paragraphs-with-the-windows-forms-richtextbox-control"></a>方法: Windows フォームの RichTextBox コントロールを使用してインデント、ぶら下げインデント、箇条書き段落を設定する
Windows フォーム<xref:System.Windows.Forms.RichTextBox>コントロールには、表示するテキストを書式設定するためのさまざまなオプションがあります。 プロパティを設定することにより、 <xref:System.Windows.Forms.RichTextBox.SelectionBullet%2A>選択した段落を箇条書きとして書式設定できます。 また、 <xref:System.Windows.Forms.RichTextBox.SelectionIndent%2A>、 <xref:System.Windows.Forms.RichTextBox.SelectionRightIndent%2A>、および<xref:System.Windows.Forms.RichTextBox.SelectionHangingIndent%2A>の各プロパティを使用して、コントロールの左端と右端、および他のテキスト行の左端を基準とした段落のインデントを設定することもできます。  
  
### <a name="to-format-a-paragraph-as-a-bulleted-list"></a>段落を箇条書きとして書式設定するには  
  
1. <xref:System.Windows.Forms.RichTextBox.SelectionBullet%2A> プロパティを `true`に設定します。  
  
    ```vb  
    RichTextBox1.SelectionBullet = True  
    ```  
  
    ```csharp  
    richTextBox1.SelectionBullet = true;  
    ```  
  
    ```cpp  
    richTextBox1->SelectionBullet = true;  
    ```  
  
### <a name="to-indent-a-paragraph"></a>段落にインデントを設定するには  
  
1. プロパティを<xref:System.Windows.Forms.RichTextBox.SelectionIndent%2A> 、コントロールの左端とテキストの左端の間の距離をピクセル単位で表す整数に設定します。  
  
2. <xref:System.Windows.Forms.RichTextBox.SelectionHangingIndent%2A>プロパティを、段落内のテキストの最初の行の左端と同じ段落内の後続の行の左端の間の距離をピクセル単位で表す整数に設定します。 <xref:System.Windows.Forms.RichTextBox.SelectionHangingIndent%2A>プロパティの値は、最初の行の下に折り返された段落内の行にのみ適用されます。  
  
3. プロパティを<xref:System.Windows.Forms.RichTextBox.SelectionRightIndent%2A> 、コントロールの右端とテキストの右端との間の距離をピクセル単位で表す整数に設定します。  
  
    ```vb  
    RichTextBox1.SelectionIndent = 8  
    RichTextBox1.SelectionHangingIndent = 3  
    RichTextBox1.SelectionRightIndent = 12  
    ```  
  
    ```csharp  
    richTextBox1.SelectionIndent = 8;  
    richTextBox1.SelectionHangingIndent = 3;  
    richTextBox1.SelectionRightIndent = 12;  
    ```  
  
    ```cpp  
    richTextBox1->SelectionIndent = 8;  
    richTextBox1->SelectionHangingIndent = 3;  
    richTextBox1->SelectionRightIndent = 12;  
    ```  
  
    > [!NOTE]
    > これらすべてのプロパティは、選択したテキストを含む段落に影響し、現在の挿入ポイントの後に入力されるテキストにも影響します。 たとえば、ユーザーが段落内の単語を選択して、インデントを調整すると、新しい設定はその単語を含む段落全体に適用され、選択した段落の後に入力される段落にも適用されます。 プログラムによるテキストの選択の詳細<xref:System.Windows.Forms.TextBoxBase.Select%2A>については、「」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox コントロール](richtextbox-control-windows-forms.md)
- [Windows フォームで使用するコントロール](controls-to-use-on-windows-forms.md)
