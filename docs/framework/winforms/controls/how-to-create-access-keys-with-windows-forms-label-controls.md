---
title: "Gewusst wie: Erstellen von Zugriffstasten mit Windows Forms-Steuerelementen"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- controls [Windows Forms], access keys
- dialog box controls [Windows Forms], mnemonics
- access keys [Windows Forms], creating for controls
- Label control [Windows Forms], creating access keys
- mnemonics [Windows Forms], adding to dialog box controls
- mnemonics
- Windows Forms controls, access keys
- UseMnemonic property [Windows Forms], Label control
- keyboard shortcuts [Windows Forms], creating for controls
- access keys [Windows Forms], Windows Forms
ms.assetid: 5ee8f823-80be-4a4f-96a4-412671e2e306
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 6a856090a76f484c21c1d9982d67e9fdf21e8451
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-create-access-keys-with-windows-forms-label-controls"></a>Gewusst wie: Erstellen von Zugriffstasten mit Windows Forms-Steuerelementen
Windows Forms <xref:System.Windows.Forms.Label> Steuerelemente können zum Definieren von Zugriffstasten für andere Steuerelemente verwendet werden. Wenn Sie eine Zugriffstaste in ein Label-Steuerelement definieren, kann der Benutzer drücken Sie die ALT-Taste plus das Zeichen, die für die Sicherung um an das Steuerelement den Fokus zu verschieben, die sie in der Aktivierreihenfolge folgt. Da Bezeichnungen den Fokus erhalten können, wird den Fokus automatisch auf das nächste Steuerelement in der Aktivierreihenfolge verschoben. Verwenden Sie dieses Verfahren, Textfelder, Kombinationsfelder, Listenfelder und Datenblätter Zugriffstasten zuweisen.  
  
### <a name="to-assign-an-access-key-to-a-control-with-a-label"></a>Zuweisen eine Zugriffstaste zu einem Steuerelement mit einer Bezeichnung  
  
1.  Zeichnen Sie zuerst die Bezeichnung, und zeichnen Sie dann die Steuerelemente.  
  
     - oder -   
  
     Zeichnen Sie die Steuerelemente in beliebiger Reihenfolge, und legen Sie die <xref:System.Windows.Forms.Control.TabIndex%2A> -Eigenschaft des Bezeichnungsfelds bis eins weniger als die anderen Steuerelement.  
  
2.  Legen Sie die Bezeichnung <xref:System.Windows.Forms.Label.UseMnemonic%2A> Eigenschaft `true`.  
  
3.  Verwenden Sie ein kaufmännisches und-Zeichen (&) in der Bezeichnung <xref:System.Windows.Forms.Label.Text%2A> Eigenschaft, um den Zugriffsschlüssel für die Bezeichnung zuweisen. Weitere Informationen finden Sie unter [Erstellen von Zugriffstasten für Windows Forms-Steuerelemente](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md).  
  
    > [!NOTE]
    >  Möglicherweise möchten und-Zeichen in ein Label-Steuerelement, statt Sie zu verwenden, um das Erstellen von Zugriffstasten. Dies kann auftreten, wenn Sie ein Bezeichnungsfeld-Steuerelement an ein Feld in einem Recordset binden, in denen Daten für das kaufmännische und-Zeichen umfassen. Wenn kaufmännische und-Zeichen in ein Label-Steuerelement anzeigen möchten, legen Sie die <xref:System.Windows.Forms.Label.UseMnemonic%2A> Eigenschaft `false`. Wenn Sie und-Zeichen und außerdem eine Zugriffstaste möchten, legen Sie die <xref:System.Windows.Forms.Label.UseMnemonic%2A> Eigenschaft `true` und geben Sie den Zugriffsschlüssel ein kaufmännisches und-Zeichen (&) und das kaufmännische und-Zeichen, das mit zwei kaufmännische und-Zeichen angezeigt.  
  
    ```vb  
    Label1.UseMnemonic = True  
    Label1.Text = "&Print"  
    Label2.UseMnemonic = True  
    Label2.Text = "&Copy && Paste"  
    ```  
  
    ```csharp  
    label1.UseMnemonic = true;  
    label1.Text = "&Print";  
    label2.UseMnemonic = true;  
    label2.Text = "&Copy && Paste";  
    ```  
  
    ```cpp  
    label1->UseMnemonic = true;  
    label1->Text = "&Print";  
    label2->UseMnemonic = true;  
    label2->Text = "&Copy && Paste";  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Gewusst wie: Anpassen der Größe des Label-Steuerelements in Windows Forms an seinen Inhalt](../../../../docs/framework/winforms/controls/how-to-size-a-windows-forms-label-control-to-fit-its-contents.md)  
 [Übersicht über das Label-Steuerelement](../../../../docs/framework/winforms/controls/label-control-overview-windows-forms.md)  
 [Label-Steuerelement](../../../../docs/framework/winforms/controls/label-control-windows-forms.md)
