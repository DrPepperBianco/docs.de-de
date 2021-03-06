---
title: 'Gewusst wie: Implementieren von PriorityBinding'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords: data binding [WPF], PriorityBinding class
ms.assetid: d63b65ab-b3e9-4322-9aa8-1450f8d89532
caps.latest.revision: "13"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 13b254867200897acad2868e396d152a5f9efcbd
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-implement-prioritybinding"></a>Gewusst wie: Implementieren von PriorityBinding
<xref:System.Windows.Data.PriorityBinding>in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] funktioniert, indem Sie eine Liste der Bindungen angeben. Die Liste der Bindungen ist von der höchsten Priorität bis zur niedrigsten Priorität geordnet. Wenn die höchste Priorität Bindung einen Wert zurückgibt besteht erfolgreich bei ihrer Verarbeitung niemals müssen die anderen Bindungen in der Liste zu verarbeiten. Es könnte sein, die Groß-/Kleinschreibung, die die höchste Priorität Bindung auszuwertende lange dauert, die höchsten Priorität, die einen Wert, erfolgreich zurückgibt verwendet werden, bis eine Bindung eine höhere Priorität erfolgreich einen Wert zurückgibt.  
  
## <a name="example"></a>Beispiel  
 Zur Veranschaulichung der Funktion wie <xref:System.Windows.Data.PriorityBinding> verwendet werden kann, die `AsyncDataSource` Objekt mit den folgenden drei Eigenschaften erstellt wurde: `FastDP`, `SlowerDP`, und `SlowestDP`.  
  
 Get-Accessor der `FastDP` gibt den Wert der `_fastDP` -Datenmember.  
  
 Get-Accessor der `SlowerDP` wartet vor der Rückgabe des Wert von 3 Sekunden die `_slowerDP` -Datenmember.  
  
 Get-Accessor der `SlowestDP` vor der Rückgabe des Wert von 5 Sekunden wartet, bis die `_slowestDP` -Datenmember.  
  
> [!NOTE]
>  In diesem Beispiel wird nur zu Demonstrationszwecken. Die [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] Richtlinien wird davon abgeraten, Definieren von Eigenschaften, die erheblich langsamer als ein Standardfeld festgelegt sind. Weitere Informationen finden Sie unter [NIB: Auswahl zwischen Eigenschaften und Methoden](http://msdn.microsoft.com/en-us/55825e8f-7e2e-448a-9505-7217cc91b1af).  
  
 [!code-csharp[PriorityBinding#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PriorityBinding/CSharp/Window1.xaml.cs#1)]
 [!code-vb[PriorityBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PriorityBinding/VisualBasic/AsyncDataSource.vb#1)]  
  
 Die <xref:System.Windows.Controls.TextBlock.Text%2A> Eigenschaft gebunden wird, für den oben `AsyncDS` mit <xref:System.Windows.Data.PriorityBinding>:  
  
 [!code-xaml[PriorityBinding#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PriorityBinding/CSharp/Window1.xaml#2)]  
  
 Wenn das Bindungsmodul verarbeitet die <xref:System.Windows.Data.Binding> Objekte, mit dem ersten Start <xref:System.Windows.Data.Binding>, das gebunden ist, um die `SlowestDP` Eigenschaft. Wenn dies <xref:System.Windows.Data.Binding> wird verarbeitet, es wird keinen Wert zurückgegeben erfolgreich, da er für 5 Sekunden deaktiviert ist <xref:System.Windows.Data.Binding> Element verarbeitet wird. Das nächste <xref:System.Windows.Data.Binding> keinen Rückgabewert erfolgreich, da es 3 Sekunden aktiviert ist. Das Bindungsmodul fährt mit der nächsten <xref:System.Windows.Data.Binding> -Element, das gebunden ist die `FastDP` Eigenschaft. Dies <xref:System.Windows.Data.Binding> gibt den Wert "Fast Value" zurück. Die <xref:System.Windows.Controls.TextBlock> zeigt jetzt den Wert "Fast".  
  
 Nach drei Sekunden verstrichen ist die `SlowerDP` Eigenschaft gibt den Wert "Langsamer Value" zurück. Die <xref:System.Windows.Controls.TextBlock> zeigt dann den Wert "langsamer".  
  
 Nach 5 Sekunden die `SlowestDP` Eigenschaft gibt den Wert "Langsamste Value" zurück. Diese Bindung hat die höchste Priorität, da er zuerst aufgelistet ist. Die <xref:System.Windows.Controls.TextBlock> zeigt jetzt den Wert "Langsamste Value".  
  
 Finden Sie unter <xref:System.Windows.Data.PriorityBinding> Informationen, was einen erfolgreiche Rückgabewert aus einer Bindung gilt.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Data.Binding.IsAsync%2A?displayProperty=nameWithType>  
 [Übersicht zur Datenbindung](../../../../docs/framework/wpf/data/data-binding-overview.md)  
 [Themen zu Vorgehensweisen](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)
