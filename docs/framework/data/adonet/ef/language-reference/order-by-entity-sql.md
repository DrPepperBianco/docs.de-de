---
title: ORDER BY (Entity SQL)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c0b61572-ecee-41eb-9d7f-74132ec8a26c
caps.latest.revision: "3"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: dotnet
ms.openlocfilehash: e4ef6edfc56fe73cd509d466fcc26cdb24069c9f
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="order-by-entity-sql"></a>ORDER BY (Entity SQL)
Legt die Sortierreihenfolge für Objekte fest, die von einer SELECT-Anweisung zurückgegeben werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
[ ORDER BY   
   {  
      order_by_expression [SKIP n] [LIMIT n]  
      [ COLLATE collation_name ]  
      [ ASC | DESC ]  
   }  
   [ ,…n ]   
]  
```  
  
## <a name="arguments"></a>Argumente  
 `order_by_expression`  
 Ein gültiger Abfrageausdruck, der eine Eigenschaft angibt, nach der sortiert werden soll. Es können mehrere Sortierausdrücke angegeben werden. Die Reihenfolge der Sortierausdrücke in der ORDER BY-Klausel definiert den Aufbau des sortierten Resultsets.  
  
 COLLATE {collation_name}  
 Gibt an, dass die ORDER BY-Operation nach der in `collation_name`angegebenen Sortierreihenfolge ausgeführt werden soll. COLLATE ist nur für Zeichenfolgenausdrücke anwendbar.  
  
 ASC  
 Gibt an, dass die Werte der angegebenen Eigenschaft in aufsteigender Reihenfolge (vom kleinsten zum größten Wert) sortiert werden sollen. Dies ist die Standardeinstellung.  
  
 DESC  
 Gibt an, dass die Werte der angegebenen Eigenschaft in absteigender Reihenfolge (vom größten zum kleinsten Wert) sortiert werden sollen.  
  
 LIMIT `n`  
 Nur die ersten `n` -Elemente werden ausgewählt.  
  
 SKIP `n`  
 Überspringt die ersten `n` -Elemente.  
  
## <a name="remarks"></a>Hinweise  
 Die ORDER BY-Klausel wird logisch auf das Ergebnis der SELECT-Klausel angewendet. In der ORDER BY-Klausel kann auf Elemente in der Auswahlliste verwiesen werden, indem deren Aliase verwendet werden. Die ORDER BY-Klausel kann auch auf andere Variablen verweisen, die sich aktuell im Gültigkeitsbereich befinden. Wenn die SELECT-Klausel jedoch mit einem DISTINCT-Modifizierer angegeben wurde, kann von der ORDER BY-Klausel nur auf Aliase der SELECT-Klausel verwiesen werden.  
  
 `SELECT c AS c1 FROM cs AS c ORDER BY c1.e1, c.e2`  
  
 Jeder Ausdruck in der ORDER BY-Klausel muss zu einem Typ ausgewertet werden, der bzgl. geordneter Ungleichheit ("kleiner als", "größer als" usw.) verglichen werden kann. Bei diesen Typen handelt es sich im Allgemeinen um skalare primitive Typen wie Zahlen, Zeichenfolgen und Datumsangaben. "RowTypes" vergleichbarer Typen sind ebenfalls in der Reihenfolge vergleichbar.  
  
 Wenn Code eine geordnete Menge durchläuft, wird, anders als bei einer Projektion in der obersten Ebene, die Reihenfolge bei der Ausgabe möglicherweise nicht erhalten.  
  
```  
-- In the following sample, order is guaranteed to be preserved:  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  
  
```  
-- In the following query ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
 Verwenden Sie folgendes Muster, um eine geordnete UNION, UNION ALL, EXCEPT oder INTERSECT-Operation durchzuführen:  
  
```  
SELECT ...  
FROM ( UNION/EXCEPT/INTERSECT operation )  
ORDER BY ...  
```  
  
## <a name="restricted-keywords"></a>Eingeschränkte Schlüsselwörter  
 Die folgenden Schlüsselwörter müssen bei der Verwendung in einer `ORDER BY` -Klausel in Anführungszeichen gesetzt werden:  
  
-   CROSS  
  
-   FULL  
  
-   KEY  
  
-   NACH-LINKS  
  
-   ORDER  
  
-   OUTER  
  
-   NACH-RECHTS  
  
-   ROW  
  
-   VALUE  
  
## <a name="ordering-nested-queries"></a>Reihenfolge geschachtelter Abfragen  
 In Entity Framework kann ein geschachtelter Ausdruck an jeder Stelle in der Abfrage verwendet werden. Die Reihenfolge einer geschachtelten Abfrage wird nicht beibehalten.  
  
```  
-- The following query will order the results by the last name.  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  
  
```  
-- In the following query, ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## <a name="example"></a>Beispiel  
 In der folgenden [!INCLUDE[esql](../../../../../../includes/esql-md.md)] -Abfrage wird der ORDER BY-Operator verwendet, um die für von der SELECT-Anweisung zurückgegebene Objekte zu verwendende Sortierreihenfolge anzugeben. Diese Abfrage beruht auf dem "AdventureWorks Sales"-Modell. Führen Sie folgende Schritte aus, um diese Abfrage zu kompilieren und auszuführen:  
  
1.  Verwenden Sie das Verfahren unter [How to: Execute a Query that Returns StructuralType Results](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Übergeben Sie die folgende Abfrage als Argument an die `ExecuteStructuralTypeQuery` -Methode:  
  
 [!code-csharp[DP EntityServices Concepts 2#ORDERBY](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#orderby)]  
  
## <a name="see-also"></a>Siehe auch  
 [Abfrageausdrücke](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expressions-entity-sql.md)  
 [Entity SQL-Referenz](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)  
 [SKIP](../../../../../../docs/framework/data/adonet/ef/language-reference/skip-entity-sql.md)  
 [LIMIT](../../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md)  
 [TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md)
