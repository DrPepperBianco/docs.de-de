---
title: "Lambdaausdrücke in PLINQ und TPL"
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
- Func delegate, creating with lambda expression
- Action delegate, creating with lambda expression
- lambda expressions, with Action and Func
ms.assetid: 645b2c17-29d0-4ffa-8684-430743cc2f2d
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 79ab0f4427e0f37259f88cd3ec0762d1582481f1
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="lambda-expressions-in-plinq-and-tpl"></a>Lambdaausdrücke in PLINQ und TPL
Die Task Parallel Library (TPL) enthält viele Methoden, die eines der <xref:System.Func%601?displayProperty=nameWithType> oder <xref:System.Action?displayProperty=nameWithType> -Familie Delegaten als Eingabeparameter. Sie verwenden diese Delegaten zur Übergabe der benutzerdefinierten Programmlogik an die parallele Schleife, Aufgabe oder Abfrage. In den Codebeispielen für TPL und PLINQ werden Lambdaausdrücke verwendet, um Instanzen dieser Delegaten als Inlinecodeblöcke zu erstellen. Dieses Thema bietet eine kurze Einführung in Func und Action und zeigt, wie Sie Lambdaausdrücke in der Task Parallel Library und in PLINQ verwenden.  
  
 **Hinweis** Weitere Informationen zu Delegaten im Allgemeinen finden Sie unter [Delegaten (C#-Programmierhandbuch)](../../csharp/programming-guide/delegates/index.md) und [Delegaten (Visual Basic)](../../visual-basic/programming-guide/language-features/delegates/index.md). Weitere Informationen zu Lambdaausdrücken in C# und [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] finden Sie unter [Lambda-Ausdrücke (C#-Programmierhandbuch)](~/docs/csharp/programming-guide/statements-expressions-operators/lambda-expressions.md) und [Lambda-Ausdrücke (Visual Basic)](~/docs/visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
## <a name="func-delegate"></a>Func-Delegat  
 Ein `Func`-Delegat kapselt eine Methode, die einen Wert zurückgibt. In einer Func-Signatur gibt der letzte bzw. der am weitesten rechts stehende Typparameter immer den Rückgabetyp an. Eine häufige Ursache von Compilerfehlern ist der Versuch für die Übergabe in zwei Eingabeparameter für ein <xref:System.Func%602?displayProperty=nameWithType>; tatsächlich dieses Typs akzeptiert nur ein Eingabeparameter. Die Framework-Klassenbibliothek definiert 17 Versionen von `Func`: <xref:System.Func%601?displayProperty=nameWithType>, <xref:System.Func%602?displayProperty=nameWithType>, <xref:System.Func%603?displayProperty=nameWithType>, usw. bis über <xref:System.Func%6017?displayProperty=nameWithType>.  
  
## <a name="action-delegate"></a>Action-Delegat  
 Ein <xref:System.Action?displayProperty=nameWithType> Delegat kapselt eine Methode (Sub in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]), die keinen Wert zurückgibt, oder gibt ["void"](~/docs/csharp/language-reference/keywords/void.md). In einer Signatur vom Typ „Action“ stellen die Typparameter nur Eingabeparameter dar. Die .NET Framework-Klassenbibliothek definiert wie bei Func 17 Versionen von Action, von einer Version ohne Typparameter bis zu einer Version mit 16 Typparametern.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel veranschaulicht die <xref:System.Threading.Tasks.Parallel.ForEach%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%601%7D%2CSystem.Func%7B%60%600%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%601%2C%60%601%7D%2CSystem.Action%7B%60%601%7D%29?displayProperty=nameWithType> Methode veranschaulicht, wie Delegaten Func und Action mithilfe von Lambda-Ausdrücken ausgedrückt werden.  
  
 [!code-csharp[System.Threading.Tasks.Parallel#02](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.threading.tasks.parallel/cs/parallelforeach.cs#02)]
 [!code-vb[System.Threading.Tasks.Parallel#02](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.threading.tasks.parallel/vb/parallelforeach.vb#02)]  
  
## <a name="see-also"></a>Siehe auch  
 [Parallele Programmierung](../../../docs/standard/parallel-programming/index.md)
