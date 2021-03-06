---
title: "Übersicht über die ContextMenu-Komponente (Windows Forms)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: ContextMenu
helpviewer_keywords:
- ContextMenu component [Windows Forms], about ContextMenu component
- context menus [Windows Forms], ContextMenu component
- shortcut menus [Windows Forms], ContextMenu component
ms.assetid: 49d6398f-d3c4-4679-84fa-1de07b68b05e
caps.latest.revision: "15"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: b0db67e8da97f380c3bb2eb9aab951628c4b6487
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="contextmenu-component-overview-windows-forms"></a>Übersicht über die ContextMenu-Komponente (Windows Forms)
> [!IMPORTANT]
>  Obwohl <xref:System.Windows.Forms.MenuStrip> und <xref:System.Windows.Forms.ContextMenuStrip> ersetzt und funktionell die <xref:System.Windows.Forms.MainMenu> und <xref:System.Windows.Forms.ContextMenu> Steuerelemente von früheren Versionen <xref:System.Windows.Forms.MainMenu> und <xref:System.Windows.Forms.ContextMenu> für Abwärtskompatibilität und für zukünftige Verwendung beibehalten werden, falls gewünscht.  
  
 Mit dem Windows Forms <xref:System.Windows.Forms.ContextMenu> Komponente, können Sie Benutzer bereitstellen, ein leicht zugänglichen Kontextmenü mit häufig verwendeten Befehlen, die dem ausgewählten Objekt zugeordnet sind. Die Elemente in einem Kontextmenü sind häufig eine Teilmenge der Elemente aus den Hauptmenüs, die an anderer Stelle in der Anwendung angezeigt werden. Benutzer kann ein Kontextmenü mit der rechten Maustaste des Mauszeiger in der Regel zugreifen. In Windows Forms sind Kontextmenüs Steuerelementen zugeordnet.  
  
## <a name="key-properties"></a>Wichtige Eigenschaften  
 Sie können ein Kontextmenü mit einem Steuerelement zuordnen, indem Sie des Steuerelements <xref:System.Windows.Forms.Control.ContextMenu%2A> Eigenschaft, um die <xref:System.Windows.Forms.ContextMenu> Komponente. Ein einzelnes Kontextmenü kann mehreren Steuerelementen zugeordnet werden, aber jedes Steuerelement nur ein Kontextmenü haben kann.  
  
 Die wichtigste Eigenschaft die <xref:System.Windows.Forms.ContextMenu> Komponente ist die <xref:System.Windows.Forms.Menu.MenuItems%2A> Eigenschaft. Sie können Menüelemente hinzufügen, indem Sie programmgesteuert erstellen <xref:System.Windows.Forms.MenuItem> -Objekte und durch Hinzufügen, damit die <xref:System.Windows.Forms.Menu.MenuItemCollection> des Kontextmenüs. Da die Elemente in einem Kontextmenü in der Regel aus anderen Menüs gezeichnet werden, werden Sie am häufigsten Elemente ein Kontextmenü hinzugefügt durch Kopieren.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Forms.ContextMenu>  
 <xref:System.Windows.Forms.MenuStrip>  
 <xref:System.Windows.Forms.ContextMenuStrip>
