---
title: 'Vorgehensweise: Suchen eines einzelnen Nachfolgers mit der Descendants-Methode (C#)'
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-csharp
ms.topic: article
ms.assetid: 6f735be9-0293-4680-8007-ca9d96bfebed
caps.latest.revision: "3"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 6dc90262318f5f31c4236318f87393749295a18a
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="how-to-find-a-single-descendant-using-the-descendants-method-c"></a>Vorgehensweise: Suchen eines einzelnen Nachfolgers mit der Descendants-Methode (C#)
Mit der <xref:System.Xml.Linq.XContainer.Descendants%2A>-Achsenmethode können Sie schnell Code zum Suchen nach einem einzelnen eindeutig benannten Element schreiben. Diese Technik ist besonders nützlich, wenn Sie einen bestimmten Nachfolger mit einem bestimmten Namen ermitteln möchten. Sie könnten den Code zwar so schreiben, dass eine Navigation zum gewünschten Element erfolgt, es ist aber häufig schneller und einfacher, den Code mit der <xref:System.Xml.Linq.XContainer.Descendants%2A>-Achse zu schreiben.  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird der <xref:System.Linq.Enumerable.First%2A>-Standardabfrageoperator verwendet.  
  
```csharp  
XElement root = XElement.Parse(@"<Root>  
  <Child1>  
    <GrandChild1>GC1 Value</GrandChild1>  
  </Child1>  
  <Child2>  
    <GrandChild2>GC2 Value</GrandChild2>  
  </Child2>  
  <Child3>  
    <GrandChild3>GC3 Value</GrandChild3>  
  </Child3>  
  <Child4>  
    <GrandChild4>GC4 Value</GrandChild4>  
  </Child4>  
</Root>");  
string grandChild3 = (string)  
    (from el in root.Descendants("GrandChild3")  
    select el).First();  
Console.WriteLine(grandChild3);  
```  
  
 Dieser Code erzeugt die folgende Ausgabe:  
  
```  
GC3 Value  
```  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird dieselbe Abfrage für XML in einem Namespace gezeigt. Weitere Informationen finden Sie unter [Working with XML Namespaces (C#) (Arbeiten mit XML-Namespaces (C#))](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md).  
  
```csharp  
XElement root = XElement.Parse(@"<aw:Root xmlns:aw='http://www.adventure-works.com'>  
  <aw:Child1>  
    <aw:GrandChild1>GC1 Value</aw:GrandChild1>  
  </aw:Child1>  
  <aw:Child2>  
    <aw:GrandChild2>GC2 Value</aw:GrandChild2>  
  </aw:Child2>  
  <aw:Child3>  
    <aw:GrandChild3>GC3 Value</aw:GrandChild3>  
  </aw:Child3>  
  <aw:Child4>  
    <aw:GrandChild4>GC4 Value</aw:GrandChild4>  
  </aw:Child4>  
</aw:Root>");  
XNamespace aw = "http://www.adventure-works.com";  
string grandChild3 = (string)  
    (from el in root.Descendants(aw + "GrandChild3")  
     select el).First();  
Console.WriteLine(grandChild3);  
```  
  
 Dieser Code erzeugt die folgende Ausgabe:  
  
```  
GC3 Value  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Basic Queries (LINQ to XML) (C#) (Standardabfragen (LINQ to XML) (C#))](../../../../csharp/programming-guide/concepts/linq/basic-queries-linq-to-xml.md)
