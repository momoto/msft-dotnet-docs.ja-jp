---
title: '方法: Windows フォームで実行時にイベント ハンドラーを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Windows Forms, event handling
- event handlers [Windows Forms], creating
- run time [Windows Forms], creating event handlers at
- examples [Windows Forms], event handling
- Button control [Windows Forms], event handlers
ms.assetid: 2e7c9e1a-61fe-444d-8113-3c5bacf1c8cb
ms.openlocfilehash: 440086bfd5384fc46aec2997dbdd9937f7a1b65f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964327"
---
# <a name="how-to-create-event-handlers-at-run-time-for-windows-forms"></a>方法: Windows フォームで実行時にイベント ハンドラーを作成する

Visual Studio の Windows フォームデザイナーを使用してイベントを作成するだけでなく、実行時にイベントハンドラーを作成することもできます。 これにより、プログラムが最初に起動したときにイベント ハンドラーを接続する代わりに、コード内に記述されている条件に基づいて、実行時にイベント ハンドラーを接続できます。

## <a name="create-an-event-handler-at-run-time"></a>実行時にイベントハンドラーを作成する

1. イベントハンドラーを追加するフォームを開きます。

2. 処理するイベントに対応するメソッド シグネチャを持つメソッドをフォームに追加します。

     たとえば、 <xref:System.Windows.Forms.Control.Click> <xref:System.Windows.Forms.Button>コントロールのイベントを処理する場合は、次のようなメソッドを作成します。

    ```vb
    Private Sub Button1_Click(ByVal sender As Object, ByVal e As EventArgs)
       ' Add event handler code here.
    End Sub
    ```

    ```csharp
    private void button1_Click(object sender, System.EventArgs e)
    {
    // Add event handler code here.
    }
    ```

    ```cpp
    private:
       void button1_Click(System::Object ^ sender,
          System::EventArgs ^ e)
       {
          // Add event handler code here.
       }
    ```

3. アプリケーションに応じて、イベント ハンドラーにコードを追加します。

4. イベント ハンドラーをどのフォームまたはコントロールに対して作成するかを指定します。

5. フォームのクラスのメソッドに、イベントを処理するためのイベント ハンドラーを指定するコードを追加します。 たとえば、次のコードでは、イベントハンドラー `button1_Click`が<xref:System.Windows.Forms.Button>コントロール<xref:System.Windows.Forms.Control.Click>のイベントを処理することを指定しています。

    ```vb
    AddHandler Button1.Click, AddressOf Button1_Click
    ```

    ```csharp
    button1.Click += new EventHandler(button1_Click);
    ```

    ```cpp
    button1->Click += gcnew System::EventHandler(this, &Form1::button1_Click);
    ```

     上<xref:System.ComponentModel.EventHandlerList.AddHandler%2A>の Visual Basic コードで示されているメソッドは、ボタンのクリックイベントハンドラーを確立します。

## <a name="see-also"></a>関連項目

- [Windows フォーム内でのイベント ハンドラーの作成](creating-event-handlers-in-windows-forms.md)
- [イベント ハンドラーの概要](event-handlers-overview-windows-forms.md)
- [Visual Basic での継承されたイベント ハンドラーのトラブルシューティング](../../visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)
