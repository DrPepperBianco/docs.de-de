---
title: 'Gewusst wie: Speichern und Wiederverwenden von Abfragen'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: a012bd79-1809-45e3-adea-0229532396cc
caps.latest.revision: "2"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: dotnet
ms.openlocfilehash: 8170b1219bf66c1f90fb5db3143916f7a41aab94
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-store-and-reuse-queries"></a>Gewusst wie: Speichern und Wiederverwenden von Abfragen
Wenn eine Anwendung häufig strukturell ähnliche Abfragen ausführt, können Sie häufig die Leistung steigern, indem Sie die Abfrage einmal kompilieren und dann mehrmals mit verschiedenen Parametern ausführen. So können beispielsweise mithilfe einer Anwendung alle Kunden in einer bestimmten Stadt abgerufen werden, wobei die Stadt zur Laufzeit vom Benutzer in einem Formular festgelegt wird. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]unterstützt die Verwendung von *kompilierter Abfragen* für diesen Zweck.  
  
> [!NOTE]
>  Dieses Nutzungsmuster stellt die gängigste Verwendung für kompilierte Abfragen dar. Andere Ansätze sind möglich. Kompilierte Abfragen können beispielsweise als statische Member einer partiellen Klasse gespeichert werden, die den vom Entwickler erzeugten Code ergänzt.  
  
## <a name="example"></a>Beispiel  
 In vielen Szenarien möchten Sie ggf. die Abfragen über Threadbegrenzungen hinweg wiederverwenden. In solchen Fällen ist die Speicherung kompilierter Abfragen in statischen Variablen besonders effektiv. Das folgende Codebeispiel basiert auf einer `Queries`-Klasse zum Speichern kompilierter Abfragen sowie auf einer Northwind-Klasse, die einen stark typisierten <xref:System.Data.Linq.DataContext> darstellt.  
  
 [!code-csharp[DLinqQuerying#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#6)]
 [!code-vb[DLinqQuerying#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#6)]  
  
 [!code-csharp[DLinqQuerying#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#7)]
 [!code-vb[DLinqQuerying#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#7)]  
  
## <a name="example"></a>Beispiel  
 Sie können derzeit (in statischen Variablen) speichern Abfragen, Zurückgeben einer *anonymen Typ*, da der Typ keinen Namen, die als generisches Argument bereitgestellt hat. Im folgenden Beispiel wird veranschaulicht, wie sich das Problem durch Erstellen eines Typs umgehen lässt, der das Ergebnis darstellen kann. Anschließend wird dieser Typ als generisches Argument verwendet.  
  
 [!code-csharp[DLinqQuerying#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#8)]
 [!code-vb[DLinqQuerying#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#8)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Data.Linq.CompiledQuery>  
 [Abfragekonzepte](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)  
 [Abfragen der Datenbank](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md)
