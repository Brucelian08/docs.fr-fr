---
title: Mid, instruction (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.MidB
- vb.Mid
helpviewer_keywords:
- substrings [Visual Basic], Mid statement
- strings [Visual Basic], substrings
- Mid statement [Visual Basic]
- strings [Visual Basic], replacing
ms.assetid: 2b82d7a8-9646-4cb0-bec5-80abc98297bf
ms.openlocfilehash: a653e63ded04616b6b0c6bdfb26a0a673d9299fc
ms.sourcegitcommit: 5bbfe34a9a14e4ccb22367e57b57585c208cf757
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/17/2018
ms.locfileid: "45749933"
---
# <a name="mid-statement"></a>Mid, instruction
Remplace un nombre spécifié de caractères dans un `String` variable avec des caractères à partir d’une autre chaîne.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
Mid( _  
   ByRef Target As String, _  
   ByVal Start As Integer, _  
   Optional ByVal Length As Integer _  
) = StringExpression  
```  
  
## <a name="parts"></a>Composants  
 `Target`  
 Obligatoire. Nom de la `String` variable à modifier.  
  
 `Start`  
 Obligatoire. `Integer` expression. Position du caractère dans `Target` où commence le remplacement de texte. `Start` utilise un index de base un.  
  
 `Length`  
 Facultatif. `Integer` expression. Nombre de caractères à remplacer. Si omis, tous les `String` est utilisé.  
  
 `StringExpression`  
 Obligatoire. `String` Expression qui remplace une partie de `Target`.  
  
## <a name="exceptions"></a>Exceptions  
  
|Type d'exception|Condition|  
|--------------------|---------------|  
|<xref:System.ArgumentException>|`Start` < = 0 ou `Length` < 0.|  
  
## <a name="remarks"></a>Notes  
 Le nombre de caractères remplacés est toujours inférieur ou égal au nombre de caractères dans `Target`.  
  
 Visual Basic a un <xref:Microsoft.VisualBasic.Strings.Mid%2A> (fonction) et un `Mid` instruction. Ces éléments fonctionnent à la fois sur un nombre spécifié de caractères dans une chaîne, mais la `Mid` fonction retourne les caractères lors de la `Mid` instruction remplace les caractères. Pour plus d'informations, consultez <xref:Microsoft.VisualBasic.Strings.Mid%2A>.  
  
> [!NOTE]
>  La `MidB` instruction des versions antérieures de Visual Basic remplace une sous-chaîne en octets, plutôt que des caractères. Il est utilisé principalement pour la conversion de chaînes dans les applications de jeu codés sur deux octets. Toutes les chaînes Visual Basic sont au format Unicode, et `MidB` n’est plus pris en charge.  
  
## <a name="example"></a>Exemple  
 Cet exemple utilise la `Mid` instruction pour remplacer un nombre spécifié de caractères dans une variable de chaîne avec des caractères à partir d’une autre chaîne.  
  
 [!code-vb[VbVbalrStrings#5](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/mid-statement_1.vb)]  
  
## <a name="requirements"></a>Configuration requise  
 **Namespace :** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **Module :** `Strings`  
  
 **Assembly :** [!INCLUDE[vbprvbruntime](~/includes/vbprvbruntime-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 <xref:Microsoft.VisualBasic.Strings.Mid%2A>  
 [Chaînes](../../../visual-basic/programming-guide/language-features/strings/index.md)  
 [Introduction aux chaînes en Visual Basic](../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
