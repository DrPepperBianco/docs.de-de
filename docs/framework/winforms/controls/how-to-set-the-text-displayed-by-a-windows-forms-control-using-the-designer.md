---
title: "Gewusst wie: Festlegen des durch ein Windows Forms-Steuerelement angezeigten Textes mithilfe des Designers"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- controls [Windows Forms], setting caption
- Windows Forms, setting the text displayed
ms.assetid: 9d18e0e0-f17f-4074-837d-e67ceeeaa89d
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: b6d49466e5dd25bbe9e97262d68f2c3fb2f8ba1a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-set-the-text-displayed-by-a-windows-forms-control-using-the-designer"></a>Gewusst wie: Festlegen des durch ein Windows Forms-Steuerelement angezeigten Textes mithilfe des Designers
Windows Forms-Steuerelemente zeigen in der Regel Text an, die mit der Hauptfunktion des Steuerelements zusammenhängt. Angenommen, ein <xref:System.Windows.Forms.Button> -Steuerelement zeigt in der Regel eine Beschriftung, der angibt, welche Aktion ausgeführt wird, wenn die Schaltfläche geklickt wird. Bei allen Steuerelementen können Sie den Text mithilfe der <xref:System.Windows.Forms.Control.Text%2A>-Eigenschaft festlegen oder zurückgeben. Sie können die Schriftart ändern, indem Sie die <xref:System.Windows.Forms.Control.Font%2A>-Eigenschaft verwenden.  
  
### <a name="to-set-the-text-and-font-with-the-designer"></a>Festlegen der Text und die Schriftart mithilfe des Designers  
  
1.  Legen Sie im Fenster Eigenschaften die <xref:System.Windows.Forms.Control.Text%2A> Eigenschaft des Steuerelements in eine entsprechende Zeichenfolge ein.  
  
     So erstellen eine unterstrichene Zugriffstaste enthält ein kaufmännisches und-Zeichen (&) vor dem Buchstaben, die die Verknüpfung als Schlüssel verwendet wird.  
  
2.  Klicken Sie im Fenster Eigenschaften auf die Schaltfläche mit den Auslassungspunkten (![von VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "VbEllipsesButton")) neben dem <xref:System.Windows.Forms.Control.Font%2A> Eigenschaft.  
  
     Wählen Sie in der standard Schriftart (Dialogfeld) Schriftart, Schriftschnitt, Größe, Auswirkungen (z. B. durchgestrichen oder unterstrichen), und Skripts, die Sie möchten.  
  
## <a name="see-also"></a>Siehe auch  
 [Gewusst wie: Festlegen des durch ein Windows Forms-Steuerelement angezeigten Texts](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)  
 [Verwenden von Schriftarten und Text](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)  
 [Beschriften einzelner Steuerelemente für Windows Forms und Konfigurieren von Shortcuts für diese Elemente](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
