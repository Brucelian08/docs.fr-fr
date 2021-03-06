---
title: Conception de constructeurs
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- member design guidelines, constructors
- constructors, design guidelines
- instance constructors
- type constructors
- virtual members
- constructors, types
- default constructors
- static constructors
ms.assetid: b4496afe-5fa7-4bb0-85ca-70b0ef21e6fc
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6ad920c8028b102a13fdfe928d21768538e25b0f
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/08/2018
ms.locfileid: "44180447"
---
# <a name="constructor-design"></a>Conception de constructeurs
Il existe deux types de constructeurs : tapez des constructeurs et des constructeurs d’instance.  
  
 Constructeurs de type sont statiques et sont exécutés par le CLR avant que le type est utilisé. Constructeurs d’instance exécuté lorsqu’une instance d’un type est créée.  
  
 Constructeurs de type ne peut pas prendre tous les paramètres. Constructeurs d’instance peuvent. Constructeurs d’instance qui ne prennent pas tous les paramètres sont souvent appelées des constructeurs par défaut.  
  
 Constructeurs sont le moyen le plus naturel pour créer des instances d’un type. La plupart des développeurs recherche et essayez d’utiliser un constructeur avant d’autres méthodes de création d’instances (par exemple, les méthodes de fabrique).  
  
 **✓ CONSIDER** fournissant simple, dans l’idéal, par défaut, les constructeurs.  
  
 Un constructeur simple possède un très petit nombre de paramètres, et tous les paramètres sont des primitives ou des énumérations. Ces constructeurs simples faciliter l’utilisation de l’infrastructure.  
  
 **✓ CONSIDER** à l’aide d’une méthode de fabrique statique au lieu d’un constructeur si la sémantique de l’opération requise ne correspond pas directement à la construction d’une nouvelle instance, ou si les règles de conception du constructeur vous semblent pas naturelles.  
  
 **✓ DO** utiliser les paramètres du constructeur en tant que raccourcis pour définir les propriétés principales.  
  
 Il doit y avoir aucune différence sémantique entre l’utilisation du constructeur vide suivi de certains jeux de propriétés et à l’aide d’un constructeur avec plusieurs arguments.  
  
 **✓ DO** utiliser le même nom pour les paramètres du constructeur et une propriété si les paramètres du constructeur sont utilisés pour définir simplement la propriété.  
  
 Doit être la seule différence entre ces paramètres et les propriétés de mise en majuscules.  
  
 **✓ DO** travail minimal dans le constructeur.  
  
 Constructeurs doivent rien faire d’autre que de capture les paramètres du constructeur. Le coût de tout autre traitement doit être différé jusqu'à ce que nécessaire.  
  
 **✓ DO** lever des exceptions à partir des constructeurs d’instance, le cas échéant.  
  
 **✓ DO** déclarer explicitement le constructeur public par défaut dans les classes, si un tel constructeur est nécessaire.  
  
 Si vous ne déclarez explicitement tous les constructeurs sur un type, nombreux langages (tel que c#) ajoute automatiquement un constructeur public par défaut. (Les classes abstraites obtenir un constructeur protégé.)  
  
 Ajout d’un constructeur paramétrable à une classe empêche le compilateur d’ajouter le constructeur par défaut. Cela entraîne souvent des modifications avec rupture accidentelle.  
  
 **X AVOID** définition explicite des constructeurs par défaut sur les structures.  
  
 Cela accélère la création de tableau, car si le constructeur par défaut n’est pas défini, il n’a pas à être exécuté sur tous les emplacements dans le tableau. Notez que de nombreux compilateurs, y compris C#, ne pas autoriser les structs peuvent avoir des constructeurs sans paramètre pour cette raison.  
  
 **X AVOID** appel des membres virtuels sur un objet à l’intérieur de son constructeur.  
  
 Appeler un membre virtuel entraîne le remplacement de la plus dérivé à appeler, même si le constructeur du type plus dérivé n'a pas été entièrement encore été exécuté.  
  
### <a name="type-constructor-guidelines"></a>Instructions de constructeur de type  
 **✓ DO** rendre les constructeurs statiques privé.  
  
 Un constructeur statique, également appelé constructeur de classe, est utilisé pour initialiser un type. Le CLR appelle le constructeur statique avant la création de la première instance du type ou de tous les membres statiques sur ce type sont appelées. L’utilisateur n’a aucun contrôle sur quand le constructeur statique est appelé. Si un constructeur statique n’est pas privé, elle peut être appelée par du code autre que le CLR. Selon les opérations effectuées dans le constructeur, cela peut provoquer un comportement inattendu. Le compilateur c# force les constructeurs statiques privées.  
  
 **X DO NOT** lever des exceptions à partir des constructeurs statiques.  
  
 Si une exception est levée à partir d’un constructeur de type, le type n’est pas utilisable dans le domaine d’application actuel.  
  
 **✓ CONSIDER** initialiser les champs statiques inline au lieu d’utiliser explicitement des constructeurs statiques, car le runtime peut optimiser les performances des types qui n’ont pas un constructeur statique explicitement défini.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Tous droits réservés.*  
  
 *Réimprimé avec l’autorisation de Pearson Education, Inc. et extrait de [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) par Krzysztof Cwalina et Brad Abrams, publié le 22 octobre 2008 par Addison-Wesley Professional dans le cadre de la série sur le développement Microsoft Windows.*  
  
## <a name="see-also"></a>Voir aussi

- [Instructions de conception des membres](../../../docs/standard/design-guidelines/member.md)  
- [Règles de conception de .NET Framework](../../../docs/standard/design-guidelines/index.md)
