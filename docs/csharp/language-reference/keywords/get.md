---
title: get (référence C#)
ms.date: 03/10/2017
f1_keywords:
- get_CSharpKeyword
- get
helpviewer_keywords:
- get keyword [C#]
ms.assetid: a52de048-fbe0-41b0-82ec-8e4ac04d3a71
ms.openlocfilehash: 182f7164ad929232c185903a3dbf024a2e5d22a7
ms.sourcegitcommit: 6eac9a01ff5d70c6d18460324c016a3612c5e268
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/17/2018
ms.locfileid: "45592830"
---
# <a name="get-c-reference"></a>get (référence C#)

Le mot clé `get` définit une méthode *Accessor* dans une propriété ou un indexeur qui retourne la valeur de la propriété ou l’élément de l’indexeur. Pour plus d’informations, consultez [Propriétés](../../../csharp/programming-guide/classes-and-structs/properties.md), [Propriétés implémentées automatiquement](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md) et [Indexeurs](../../../csharp/programming-guide/indexers/index.md).  
  
L’exemple suivant définit un accesseur `get` et un accesseur `set` pour une propriété nommée `Seconds`. Il utilise un champ privé nommé `_seconds` pour stocker la valeur de la propriété.  
 
 [!code-csharp[get#1](../../../../samples/snippets/csharp/language-reference/keywords/get/get-1.cs)]  
  
Souvent, l’accesseur `get` se compose d’une seule instruction qui retourne une valeur, comme dans l’exemple précédent. À compter de C# 7.0, vous pouvez implémenter l’accesseur `get` comme membre expression-bodied. L’exemple suivant implémente l’accesseur `get` et l’accesseur `set` en tant que membres expression-bodied.

 [!code-csharp[get#3](../../../../samples/snippets/csharp/language-reference/keywords/get/get-3.cs)]   
 
Pour les cas simples dans lesquels les accesseurs `get` et `set` d’une propriété n’effectuent aucune autre opération que la définition ou la récupération d’une valeur dans un champ de stockage privé, vous pouvez tirer parti de la prise en charge par le compilateur C# des propriétés implémentées automatiquement. L’exemple suivant implémente `Hours` en tant que propriété implémentée automatiquement. 
  
 [!code-csharp[get#2](../../../../samples/snippets/csharp/language-reference/keywords/get/get-2.cs)]  
  
## <a name="c-language-specification"></a>Spécification du langage C#

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Voir aussi

- [Référence C#](../../../csharp/language-reference/index.md)  
- [Guide de programmation C#](../../../csharp/programming-guide/index.md)  
- [Mots clés C#](../../../csharp/language-reference/keywords/index.md)
- [Propriétés](../../../csharp/programming-guide/classes-and-structs/properties.md)
