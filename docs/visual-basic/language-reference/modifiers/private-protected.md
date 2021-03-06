---
title: Protégé privé (Visual Basic)
ms.date: 05/10/2018
helpviewer_keywords:
- Private Protected keyword [Visual Basic]
- Private Protected keyword [Visual Basic], syntax
ms.openlocfilehash: 23fd6583182a1fee544d0458dc3fc390aed86b9f
ms.sourcegitcommit: 22c3c8f74eaa138dbbbb02eb7d720fce87fc30a9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/17/2018
---
# <a name="private-protected-visual-basic"></a>Protégé privé (Visual Basic)

Le `Private Protected` combinaison de mots clés est un modificateur d’accès du membre. A `Private Protected` membre est accessible par tous les membres de sa classe conteneur, ainsi que par les types dérivés de la classe conteneur, mais uniquement si elles se trouvent dans l’assembly qui le contient. 

Vous pouvez spécifier `Private Protected` uniquement sur les membres de classes ; vous ne pouvez pas appliquer `Private Protected` aux membres d’une structure, car les structures ne peuvent pas être héritées.

Le `Private Protected` modificateur d’accès est prise en charge par Visual Basic 15.5 et versions ultérieures. Pour l’utiliser, vous pouvez ajouter l’élément suivant à votre fichier projet (*.vbproj) de Visual Basic. En tant que Visual Basic 15.5 ou version ultérieure est installé sur votre système, il vous permet de tirer parti de toutes les fonctionnalités de langage pris en charge par la dernière version du compilateur Visual Basic :

```xml
<PropertyGroup>
   <LangVersion>latest</LangVersion>
</PropertyGroup>
```

> [!NOTE]
> Dans Visual Studio, en sélectionnant la touche F1 sur `private protected` fournit une aide pour soit [privé](private.md) ou [protégé](protected.md). L’IDE choisit le jeton unique sous le curseur plutôt que le mot composé.

## <a name="rules"></a>Règles

- **Contexte de déclaration.** Vous pouvez utiliser `Private Protected` uniquement au niveau de la classe. Cela signifie que le contexte de déclaration pour un `Protected` élément doit être une classe et ne peut pas être un fichier source, espace de noms, interface, un module, structure ou procédure.

## <a name="behavior"></a>Comportement

- **Niveau d’accès.** Tout le code dans une classe peut accéder à ses éléments. Le code dans n’importe quelle classe qui dérive d’une classe de base et qui est contenue dans le même assembly peut accéder à tous les `Private Protected` les éléments de la classe de base. Toutefois, le code dans n’importe quelle classe qui dérive d’une classe de base et qui est contenue dans un autre assembly Impossible d’accéder à la classe de base `Private Protected` éléments.

- **Modificateurs d’accès.** Les mots clés qui spécifient le niveau d’accès sont appelés *les modificateurs d’accès*. Pour obtenir une comparaison des modificateurs d’accès, consultez [niveaux en Visual Basic d’accès](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).
  
 Le modificateur `Private Protected` peut être utilisé dans les contextes suivants :  
  
 [La classe](../../../visual-basic/language-reference/statements/class-statement.md) d’une classe imbriquée  
  
 [Const (instruction)](../../../visual-basic/language-reference/statements/const-statement.md)  
  
 [Declare (instruction)](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Delegate, instruction](../../../visual-basic/language-reference/statements/delegate-statement.md) d’un délégué imbriqué dans une classe  
  
 [Dim (instruction)](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Enum, instruction](../../../visual-basic/language-reference/statements/enum-statement.md) d’une eumeration imbriquée dans une classe 
  
 [Event (instruction)](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Function (instruction)](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Interface, instruction](../../../visual-basic/language-reference/statements/interface-statement.md) d’une interface imbriquée dans une classe 
  
 [Property (instruction)](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Instruction de la structure](../../../visual-basic/language-reference/statements/structure-statement.md) d’une structure imbriquée dans une classe 
  
 [Sub (instruction)](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>Voir aussi

[Public](../../../visual-basic/language-reference/modifiers/public.md)  
[Protected](../../../visual-basic/language-reference/modifiers/protected.md)  
[Friend](friend.md)   
[Private](../../../visual-basic/language-reference/modifiers/private.md)  
[Protected Friend](./protected-friend.md)   
[Niveaux d’accès dans Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)  
[Procédures](../../../visual-basic/programming-guide/language-features/procedures/index.md)  
[Structures](../../../visual-basic/programming-guide/language-features/data-types/structures.md)  
[Objets et classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
