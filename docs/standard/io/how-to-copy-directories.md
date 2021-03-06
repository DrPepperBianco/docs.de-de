---
title: 'Gewusst wie: Kopieren von Verzeichnissen'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- directory copying
- I/O [.NET Framework], copying directories
- subdirectory copying
- copying directories
- directories [.NET Framework], copying
ms.assetid: 5a969765-e5f8-4b4e-977e-90e2b0a1fe3c
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: a5602a4e227f3cd17e4a7c9a086bee69d3e3e506
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-copy-directories"></a>Gewusst wie: Kopieren von Verzeichnissen
Dieses Beispiel zeigt, wie E/A-Klassen zum synchronen Kopieren der Inhalte eines Verzeichnisses an einen anderen Speicherort verwendet werden. In diesem Beispiel kann der Benutzer angeben, ob auch die Unterverzeichnisse kopiert werden sollen. Wenn dies der Fall ist, werden die Unterverzeichnisse von der Methode in diesem Beispiel rekursiv kopiert, indem sie sich selbst so lange für jedes weitere Unterverzeichnis aufruft, bis alle kopiert wurden.  
  
 Ein Beispiel zum asynchronen Kopieren von Dateien finden Sie unter [Asynchronous File I/O](../../../docs/standard/io/asynchronous-file-i-o.md).  
  
## <a name="example"></a>Beispiel  
 [!code-csharp[System.IO.Directory_Copy#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Directory_Copy/cs/program.cs#1)]
 [!code-vb[System.IO.Directory_Copy#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Directory_Copy/vb/Program.vb#1)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.IO.FileInfo>  
 <xref:System.IO.DirectoryInfo>  
 <xref:System.IO.FileStream>  
 [Datei- und Stream-E/A](../../../docs/standard/io/index.md)  
 [Allgemeine E/A-Aufgaben](../../../docs/standard/io/common-i-o-tasks.md)  
 [Asynchrone Datei-E/A](../../../docs/standard/io/asynchronous-file-i-o.md)
