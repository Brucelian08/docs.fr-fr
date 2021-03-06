---
title: Tableau des types intégraux (référence C#)
description: Vue d’ensemble des types intégraux C# intégrés
ms.date: 08/20/2018
helpviewer_keywords:
- integral types, C#
- Visual C#, integral types
- types [C#], integral types
- ranges of integral types [C#]
ms.assetid: 62e86126-46ff-40b0-9028-e61d7558268c
ms.openlocfilehash: 4ac16d185a52cdb03fcb22f57ebf7506f2fb2745
ms.sourcegitcommit: 64f4baed249341e5bf64d1385bf48e3f2e1a0211
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44078846"
---
# <a name="integral-types-table-c-reference"></a>Tableau des types intégraux (référence C#)

Le tableau suivant indique les tailles et les plages des types intégraux, qui constituent un sous-ensemble des types simples.  
  
|Type|Plage|Size|  
|----------|-----------|----------|  
|[sbyte](sbyte.md)|-128 à 127|Entier 8 bits signé|  
|[byte](byte.md)|0 à 255|Entier 8 bits non signé|  
|[char](char.md)|U+0000 à U+ffff|Caractère Unicode 16 bits|  
|[short](short.md)|de -32 768 à 32 767|Entier 16 bits signé|  
|[ushort](ushort.md)|0 à 65 535|Entier 16 bits non signé|  
|[int](int.md)|-2,147,483,648 en 2,147,483,647|Entier 32 bits signé|  
|[uint](uint.md)|de 0 à 4 294 967 295|Entier 32 bits non signé|  
|[long](long.md)|-9 223 372 036 854 775 808 à 9 223 372 036 854 775 807|Entier 64 bits signé|  
|[ulong](ulong.md)|de 0 à 18 446 744 073 709 551 615|Entier 64 bits non signé|  

## <a name="remarks"></a>Notes
  
Si la valeur représentée par un littéral entier dépasse <xref:System.UInt64.MaxValue?displayProperty=nameWithType>, une erreur de compilation [CS1021](../../misc/cs1021.md) se produit.

Utilisez la classe <xref:System.Numerics.BigInteger?displayProperty=nameWithType> pour représenter un entier signé arbitrairement grand.
  
## <a name="see-also"></a>Voir aussi

- [Référence C#](../index.md)
- [Guide de programmation C#](../../programming-guide/index.md)
- [Mots clés C#](index.md)
- [Tableaux de référence des types](reference-tables-for-types.md)
- [Tableau des types virgule flottante](floating-point-types-table.md)
- [Tableau des valeurs par défaut](default-values-table.md)
- [Tableau des formats des résultats numériques](formatting-numeric-results-table.md)
- [Tableaux des types intégrés](built-in-types-table.md)
