---
title: Lecture et écriture de schémas XML
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: b5757c4a-ea59-467e-ac62-be2bfe24eb77
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 241ff40448c3dca2846f9e420dc7df41427dc79d
ms.sourcegitcommit: 6eac9a01ff5d70c6d18460324c016a3612c5e268
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2018
ms.locfileid: "45592229"
---
# <a name="reading-and-writing-xml-schemas"></a>Lecture et écriture de schémas XML
L'API Modèle Objet du schéma (SOM) peut permettre de lire et écrire des schémas de langage XSD (XML Schema Definition) dans des fichiers ou d'autres sources et de générer un cache de schéma XML à l'aide des classes de l'espace de noms <xref:System.Xml.Schema?displayProperty=nameWithType> correspondant aux structures définies dans la recommandation du W3C (World Wide Web Consortium) sur les schémas XML.  
  
## <a name="reading-and-writing-xml-schemas"></a>Lecture et écriture de schémas XML  
 La classe <xref:System.Xml.Schema.XmlSchema> fournit les méthodes <xref:System.Xml.Schema.XmlSchema.Read%2A> et <xref:System.Xml.Schema.XmlSchema.Write%2A> pour lire et écrire des schémas XML. La méthode <xref:System.Xml.Schema.XmlSchema.Read%2A> retourne un objet <xref:System.Xml.Schema.XmlSchema> représentant le schéma XML et prend un objet <xref:System.Xml.Schema.ValidationEventHandler> facultatif comme paramètre pour traiter les avertissements et erreurs de validation de schéma rencontrées lors de la lecture d'un schéma XML.  
  
 La méthode <xref:System.Xml.Schema.XmlSchema.Write%2A> écrit des schémas XML dans des objets <xref:System.IO.Stream>, <xref:System.IO.TextWriter> et <xref:System.Xml.XmlWriter> et peut prendre un <xref:System.Xml.XmlNamespaceManager> facultatif comme paramètre. Un objet <xref:System.Xml.XmlNamespaceManager> permet de traiter les espaces de noms rencontrés dans un schéma XML. Pour plus d’informations sur la classe <xref:System.Xml.XmlNamespaceManager>, consultez [Gestion d’espaces de noms dans un document XML](../../../../docs/standard/data/xml/managing-namespaces-in-an-xml-document.md).  
  
 L'exemple de code suivant illustre la lecture et l'écriture de schémas XML à partir de et vers un fichier. Il prend le fichier `example.xsd`, le lit dans un objet <xref:System.Xml.Schema.XmlSchema> à l'aide de la méthode `static`<xref:System.Xml.Schema.XmlSchema.Read%2A>, puis l'écrit dans la console et dans un nouveau fichier `new.xsd`. Il fournit également un objet <xref:System.Xml.Schema.ValidationEventHandler> comme paramètre à la méthode `static`<xref:System.Xml.Schema.XmlSchema.Read%2A> pour traiter les avertissements ou erreurs de validation de schéma rencontrés pendant la lecture du schéma XML. Si l'objet <xref:System.Xml.Schema.ValidationEventHandler> n'est pas spécifié (`null`), aucun avertissement ou aucune erreur n'est signalée.  
  
 [!code-cpp[XmlSchemaReadWriteExample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaReadWriteExample/CPP/XmlSchemaReadWriteExample.cpp#1)]
 [!code-csharp[XmlSchemaReadWriteExample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaReadWriteExample/CS/XmlSchemaReadWriteExample.cs#1)]
 [!code-vb[XmlSchemaReadWriteExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaReadWriteExample/VB/XmlSchemaReadWriteExample.vb#1)]  
  
 L'exemple prend le fichier `example.xsd` comme entrée.  
  
```xml  
<?xml version="1.0"?>  
<xs:schema id="play" targetNamespace="http://tempuri.org/play.xsd" elementFormDefault="qualified" xmlns="http://tempuri.org/play.xsd" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <xs:element name='myShoeSize'>  
        <xs:complexType>  
            <xs:simpleContent>  
                <xs:extension base='xs:decimal'>  
                    <xs:attribute name='sizing' type='xs:string' />  
                </xs:extension>  
            </xs:simpleContent>  
        </xs:complexType>  
    </xs:element>  
</xs:schema>  
```  
  
## <a name="see-also"></a>Voir aussi

- [Vue d’ensemble du modèle d’objet de schéma XML](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)  
- [Création de schémas XML](../../../../docs/standard/data/xml/building-xml-schemas.md)  
- [Parcours des schémas XML](../../../../docs/standard/data/xml/traversing-xml-schemas.md)  
- [Modification de schémas XML](../../../../docs/standard/data/xml/editing-xml-schemas.md)  
- [Inclusion ou importation de schémas XML](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)  
- [XmlSchemaSet pour la compilation de schémas](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)  
- [Infoset de post-compilation de schéma](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)  
- [Gestion d’espaces de noms dans un document XML](../../../../docs/standard/data/xml/managing-namespaces-in-an-xml-document.md)
