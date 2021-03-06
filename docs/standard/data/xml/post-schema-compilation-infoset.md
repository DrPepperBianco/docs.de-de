---
title: Post-Schema-Compilation-Infoset
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
- cpp
ms.assetid: 7f1bc7f4-401b-459f-9078-f099cc711fde
caps.latest.revision: "3"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 77fe1790a4ff2f910a740e969e458549f1fd9642
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="post-schema-compilation-infoset"></a>Post-Schema-Compilation-Infoset
Die [World Wide Web Consortium (W3C) XML-Schemaempfehlung](http://go.microsoft.com/fwlink/?linkid=45242) wird der Informationssatz (Infoset), die für die Pre-Schema-Validierung und Post-Schema-Kompilierung verfügbar gemacht werden muss. Das XML-SOM (Schema Object Model) zeigt dieses Offenlegen vor und nachdem die <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A>-Methode vom <xref:System.Xml.Schema.XmlSchemaSet> aufgerufen wird an.  
  
 Das Pre-Schema-Validation-Infoset wird während der Bearbeitung des Schemas erstellt. Das Post-Schema-Compilation-Infoset wird nach dem Aufrufen der <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A>-Methode vom <xref:System.Xml.Schema.XmlSchemaSet> während der Kompilierung des Schemas erstellt und als Eigenschaften verfügbar gemacht.  
  
 Das SOM ist das Objektmodell, das das Pre-Schema-Validation-Infoset und das Post-Schema-Compilation-Infoset darstellt. Es besteht aus den Klassen im <xref:System.Xml.Schema?displayProperty=nameWithType>-Namespace. Alle Lese- und Schreibeigenschaften der Klassen im <xref:System.Xml.Schema>-Namespace gehören zum Pre-Schema-Validation-Infoset, während alle schreibgeschützten Eigenschaften der Klassen im <xref:System.Xml.Schema>-Namespace zum Post-Schema-Compilation-Infoset gehören. Die Ausnahme zu dieser Regel bilden die folgenden Eigenschaften, die sowohl Eigenschaften des Pre-Schema-Validation-Infosets als auch des Post-Schema-Compilation-Infosets sind.  
  
|Klasse|Eigenschaft|  
|-----------|--------------|  
|<xref:System.Xml.Schema.XmlSchemaObject>|<xref:System.Xml.Schema.XmlSchemaObject.Parent%2A>|  
|<xref:System.Xml.Schema.XmlSchema>|<xref:System.Xml.Schema.XmlSchema.AttributeFormDefault%2A>, <xref:System.Xml.Schema.XmlSchema.BlockDefault%2A>, <xref:System.Xml.Schema.XmlSchema.ElementFormDefault%2A>, <xref:System.Xml.Schema.XmlSchema.FinalDefault%2A>, <xref:System.Xml.Schema.XmlSchema.TargetNamespace%2A>|  
|<xref:System.Xml.Schema.XmlSchemaExternal>|<xref:System.Xml.Schema.XmlSchemaExternal.Schema%2A>|  
|<xref:System.Xml.Schema.XmlSchemaAttributeGroup>|<xref:System.Xml.Schema.XmlSchemaAttributeGroup.AnyAttribute%2A>|  
|<xref:System.Xml.Schema.XmlSchemaParticle>|<xref:System.Xml.Schema.XmlSchemaParticle.MaxOccurs%2A>, <xref:System.Xml.Schema.XmlSchemaParticle.MinOccurs%2A>|  
|<xref:System.Xml.Schema.XmlSchemaComplexType>|<xref:System.Xml.Schema.XmlSchemaComplexType.AnyAttribute%2A>|  
  
 Beispielsweise verfügen die <xref:System.Xml.Schema.XmlSchemaElement>-Klasse und die <xref:System.Xml.Schema.XmlSchemaComplexType>-Klasse beide über die `BlockResolved`-Eigenschaft und die `FinalResolved`-Eigenschaft. Diese Eigenschaften werden verwendet, um die Werte für die `Block`-Eigenschaft und `Final`-Eigenschaft aufzunehmen, nachdem das Schema kompiliert und überprüft wurde. `BlockResolved` und `FinalResolved` sind schreibgeschützte Eigenschaften, die Teil des Post-Schema-Compilation-Infoset sind.  
  
 Das folgende Beispiel zeigt die nach dem Validieren des Schemas festgelegte <xref:System.Xml.Schema.XmlSchemaElement.ElementSchemaType%2A>-Eigenschaft der <xref:System.Xml.Schema.XmlSchemaElement>-Klasse. Vor der Validierung enthält die Eigenschaft einen `null`-Verweis, und der <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> ist auf den Namen des entsprechenden Typs festgelegt. Nach der Validierung wird der <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> in einen gültigen Typ aufgelöst, und das Typobjekt ist über die <xref:System.Xml.Schema.XmlSchemaElement.ElementSchemaType%2A>-Eigenschaft verfügbar.  
  
 [!code-cpp[PsciSample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/PsciSample/CPP/PsciSample.cpp#1)]
 [!code-csharp[PsciSample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/PsciSample/CS/PsciSample.cs#1)]
 [!code-vb[PsciSample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/PsciSample/VB/PsciSample.vb#1)]  
  
## <a name="see-also"></a>Siehe auch  
 [XML Schema Object Model (SOM) (XML-Schemaobjektmodell (SOM))](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)
