---
title: Sérialisation XML et SOAP
ms.date: 03/30/2017
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- serialization, SOAP
- serialization, about serialization
- XML serialization
- serialization
ms.assetid: 832ac524-21bc-419a-a27b-ca8bfc45840f
ms.openlocfilehash: 366a4a42ff0bf968e51e11a66fa81566a47c86ea
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/08/2018
ms.locfileid: "44179427"
---
# <a name="xml-and-soap-serialization"></a>Sérialisation XML et SOAP

La sérialisation XML convertit (sérialise) les champs et les propriétés publics d'un objet ou les paramètres et valeurs de retour des méthodes, en un flux de données XML conforme à un document de langage XSD (XML Schema Definition) spécifique. La sérialisation XML permet d'obtenir des classes fortement typées avec des propriétés et des champs publics convertis au format série (dans ce cas, XML) pour le stockage ou le transport.

XML étant une norme ouverte, le flux de données XML peut être traité si nécessaire par toute application, quelle que soit la plateforme. Par exemple, les services Web XML créés à l'aide d'ASP.NET utilisent la classe <xref:System.Xml.Serialization.XmlSerializer> pour créer des flux de données XML qui passent des données entre des applications de services Web XML sur Internet ou des intranets. Inversement, la désérialisation utilise le flux de données XML et reconstruit l'objet.

La sérialisation XML peut également être utilisée pour sérialiser des objets en flux XML se conformant à la spécification SOAP. SOAP est un protocole basé sur XML, conçu spécifiquement pour transporter des appels de procédure à l'aide de XML.

Pour sérialiser ou désérialiser des objets, utilisez la classe <xref:System.Xml.Serialization.XmlSerializer>. Pour créer les classes à sérialiser, utilisez l'outil XML Schema Definition.

## <a name="in-this-section"></a>Dans cette section

[Introduction à la sérialisation XML](introducing-xml-serialization.md)  
Fournit une définition générale de la sérialisation, en particulier de la sérialisation XML.

[Guide pratique pour sérialiser un objet](how-to-serialize-an-object.md)  
Fournit des instructions pas à pas pour sérialiser un objet.

[Guide pratique pour désérialiser un objet](how-to-deserialize-an-object.md)  
Fournit des instructions pas à pas pour désérialiser un objet.

[Exemples de sérialisation XML](examples-of-xml-serialization.md)  
Fournit des exemples qui illustrent les points essentiels de la sérialisation XML.

[Outil XML Schema Definition et sérialisation XML](the-xml-schema-definition-tool-and-xml-serialization.md)  
Décrit comment utiliser l'outil XML Schema Definition pour créer des classes qui respectent un schéma de langage XSD particulier ou pour générer un schéma XML à partir d'un fichier .dll.

[Contrôle de la sérialisation XML à l’aide d’attributs](controlling-xml-serialization-using-attributes.md)  
Décrit comment contrôler la sérialisation à l'aide d'attributs.

[Attributs qui contrôlent la sérialisation XML](attributes-that-control-xml-serialization.md)  
Répertorie les attributs utilisés pour contrôler la sérialisation XML.

[Guide pratique pour spécifier un nom d’élément différent pour un flux XML](how-to-specify-an-alternate-element-name-for-an-xml-stream.md)  
Présente un scénario avancé illustrant comment générer plusieurs flux de données XML en substituant la sérialisation.

[Guide pratique pour contrôler la sérialisation de classes dérivées](how-to-control-serialization-of-derived-classes.md)  
Fournit un exemple de procédure de contrôle de la sérialisation de classes dérivées.

[Guide pratique pour qualifier des noms d’éléments XML et des noms d’attributs XML](how-to-qualify-xml-element-and-xml-attribute-names.md)  
Décrit comment définir et contrôler la manière dont les espaces de noms XML sont utilisés dans le flux de données XML.

[Sérialisation XML avec les services web XML](xml-serialization-with-xml-web-services.md)  
Explique la manière dont la sérialisation XML est utilisée dans les services Web XML.

[Guide pratique pour sérialiser un objet en tant que flux XML encodé selon le protocole SOAP](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)  
Décrit comment utiliser le <xref:System.Xml.Serialization.XmlSerializer> classe pour créer des flux XML SOAP encodés qui est conforme à la section 5 du document World Wide Web Consortium (W3C) intitulée [Simple objet Access Protocol (SOAP) 1.1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/).

[Guide pratique pour remplacer la sérialisation XML encodée selon le protocole SOAP](how-to-override-encoded-soap-xml-serialization.md)  
Décrit le processus permettant de substituer la sérialisation XML d'objets sous forme de messages SOAP.

[Attributs qui contrôlent la sérialisation encodée selon le protocole SOAP](attributes-that-control-encoded-soap-serialization.md)  
Répertorie les attributs utilisés pour contrôler la sérialisation encodée selon le protocole SOAP.

[\<system.xml.serialization>, élément](system-xml-serialization-element.md)  
Élément de configuration de niveau supérieur permettant de contrôler la sérialisation XML.

[\<dateTimeSerialization>, élément](datetimeserialization-element.md)  
Contrôle le mode de sérialisation d'objets <xref:System.DateTime>.

[\<schemaImporterExtensions>, élément](schemaimporterextensions-element.md)  
Contient des types utilisés par la classe <xref:System.Xml.Serialization.XmlSchemaImporter>.

[\<Ajouter > élément pour \<schemaImporterExtensions >](add-element-for-schemaimporterextensions.md)  
Ajoute des types utilisés par la classe <xref:System.Xml.Serialization.XmlSchemaImporter>.

## <a name="related-sections"></a>Rubriques connexes

[Technologies de développement avancées](https://msdn.microsoft.com/library/c4a7e341-f0c6-4df4-a74f-223387ac6e4e)  
Fournit des liens vers d'autres informations sur les tâches et les techniques de développement sophistiquées dans le .NET Framework.

[Création de services Web XML à l’aide de clients de service Web XML et ASP.NET](https://msdn.microsoft.com/library/1e64af78-d705-4384-b08d-591a45f4379c)  
Fournit des rubriques qui décrivent et expliquent comment programmer des services Web XML à l'aide d'ASP.NET.

## <a name="see-also"></a>Voir aussi

- [Sérialisation binaire](binary-serialization.md)
