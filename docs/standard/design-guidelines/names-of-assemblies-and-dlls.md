---
title: Noms d'assemblys et de DLL
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- names [.NET Framework], DLLs
- names [.NET Framework], assemblies
- assemblies [.NET Framework], names
- DLLs, names
ms.assetid: e800b610-31b4-4949-9c14-cb60e9f254be
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 97bd152cff53fb1c2edb107b6d6b34bd91ca1c49
ms.sourcegitcommit: 6eac9a01ff5d70c6d18460324c016a3612c5e268
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/14/2018
ms.locfileid: "45613714"
---
# <a name="names-of-assemblies-and-dlls"></a>Noms d'assemblys et de DLL
Un assembly est l’unité de déploiement et d’identité pour les programmes de code managé. Bien que les assemblys peuvent s’étendre sur un ou plusieurs fichiers, en général, un assembly effectue un mappage avec une DLL. Par conséquent, cette section décrit les conventions d’affectation de noms de seul DLL peuvent alors être mappées aux conventions d’affectation de noms d’assembly.  
  
 **✓ DO** choisissez des noms pour vos DLL d’assembly qui suggèrent des grands segments de fonctionnalités, telles que System.Data.  
  
 Noms d’assembly et les DLL n’êtes pas obligé de correspondent aux noms d’espace de noms, mais il est raisonnable de suivre le nom de l’espace de noms lorsque vous nommez des assemblys. Une règle empirique consiste à nommer la DLL basée sur le préfixe commun des espaces de noms contenus dans l’assembly. Par exemple, un assembly avec deux espaces de noms, `MyCompany.MyTechnology.FirstFeature` et `MyCompany.MyTechnology.SecondFeature`, peut être appelée `MyCompany.MyTechnology.dll`.  
  
 **✓ CONSIDER** nommer les DLL selon le modèle suivant :  
  
 `<Company>.<Component>.dll`  
  
 où `<Component>` contient une ou plusieurs clauses séparés par des points. Exemple :  
  
 `Litware.Controls.dll`.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Tous droits réservés.*  
  
 *Réimprimé avec l’autorisation de Pearson Education, Inc. et extrait de [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) par Krzysztof Cwalina et Brad Abrams, publié le 22 octobre 2008 par Addison-Wesley Professional dans le cadre de la série sur le développement Microsoft Windows.*  
  
## <a name="see-also"></a>Voir aussi

- [Règles de conception de .NET Framework](../../../docs/standard/design-guidelines/index.md)  
- [Directives de nommage](../../../docs/standard/design-guidelines/naming-guidelines.md)
