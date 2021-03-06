---
title: in, modificateur de paramètre (référence C#)
ms.date: 03/06/2018
helpviewer_keywords:
- parameters [C#], in
- in parameters [C#]
ms.openlocfilehash: 54abd5192d0d9bb49be0a9feb8e5e4eaeb691a0c
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43512013"
---
# <a name="in-parameter-modifier-c-reference"></a>in, modificateur de paramètre (référence C#)

Le mot clé `in` entraîne le passage des arguments par référence. Il est similaire aux mots clés [ref](ref.md) ou [out](out-parameter-modifier.md), sauf que les arguments `in` ne peuvent pas être modifiés par la méthode appelée. Alors que les arguments `ref` peuvent être modifiés, les arguments `out` doivent être modifiés par l’appelant, et ces modifications sont observables dans le contexte d’appel.

[!code-csharp-interactive[cs-in-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/InParameterModifier.cs#1)]  

L’exemple précédent montre que le modificateur `in` n’est généralement pas nécessaire sur le site d’appel. Il l’est uniquement dans la déclaration de méthode.

> [!NOTE] 
> Le mot clé `in` peut également être utilisé avec un paramètre de type générique pour spécifier que le paramètre de type est contravariant, dans le cadre d’une instruction `foreach` ou d’une clause `join` dans une requête LINQ. Pour plus d’informations sur l’utilisation du mot clé `in` dans ces contextes, consultez [in](in.md), qui fournit des liens vers toutes ces utilisations.
  
 Les variables passées comme des arguments `in` doivent être initialisées avant d’être passées dans un appel de méthode. Toutefois, la méthode appelée ne peut pas attribuer de valeur ou modifier l’argument.  
  
 Bien que les mots clés `in`, `ref` et `out` entraînent un comportement différent au moment de l’exécution, ils ne sont pas considérés comme faisant partie de la signature de la méthode au moment de la compilation. Par conséquent, les méthodes ne peuvent pas être surchargées si la seule différence est que l’une d’elles accepte un argument `ref` ou `in` et que l’autre accepte un argument `out`. Le code suivant, par exemple, ne se compilera pas :  
  
```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded 
    // methods that differ only on in, ref and out".
    public void SampleMethod(in int i) { }
    public void SampleMethod(ref int i) { }
}
```
  
Une surcharge basée sur la présence de `in` est autorisée :  
  
```csharp
class InOverloads
{
    public void SampleMethod(in int i) { }
    public void SampleMethod(int i) { }
}
```

## <a name="overload-resolution-rules"></a>Règles de résolution de surcharge

Vous pouvez comprendre les règles de résolution de surcharge pour les méthodes par valeur par rapport à celles qui utilisent des arguments `in` en comprenant pourquoi on utilise des arguments `in`. Vous pouvez optimiser les performances en définissant des méthodes à l’aide de paramètres `in`. Certains arguments de type `struct` peuvent être volumineux et, quand les méthodes sont appelées dans des boucles serrées ou des chemins de code critiques, le coût de la copie de ces structures est crucial. Les méthodes déclarent des paramètres `in` pour spécifier que des arguments peuvent être passés par référence en toute sécurité, car la méthode appelée ne modifie pas l’état de l’argument. Le passage de ces arguments par référence permet d’éviter une copie (potentiellement) coûteuse. 

La spécification de `in` pour des arguments au niveau de l’appel de site est généralement facultative. Il n’existe aucune différence sémantique entre le passage d’arguments par valeur et leur passage par référence à l’aide du modificateur `in`. Le modificateur `in` sur le site d’appel est facultatif, car vous n’avez pas besoin d’indiquer que la valeur de l’argument peut être changée. Vous ajoutez explicitement le modificateur `in` sur le site d’appel pour vérifier que l’argument est passé par référence, non par valeur. L’utilisation explicite de `in` a les deux effets suivants :

Tout d’abord, la spécification de `in` sur le site d’appel force le compilateur à sélectionner une méthode définie avec un paramètre `in` correspondant. Sinon, quand deux méthodes diffèrent uniquement par la présence de `in`, la surcharge par valeur convient mieux.

Ensuite, la spécification de `in` déclare votre intention de passer un argument par référence. L’argument utilisé avec `in` doit représenter un emplacement directement référençable. Les mêmes règles générales pour les arguments `out` et `ref` s’appliquent : vous ne pouvez pas utiliser de constantes, de propriétés ordinaires ou d’autres expressions qui produisent des valeurs. Sinon, l’omission de `in` sur le site d’appel informe le compilateur que vous l’autorisez à créer une variable temporaire à passer par référence en lecture seule à la méthode. Le compilateur crée une variable temporaire pour surmonter plusieurs restrictions avec les arguments `in` :

- Une variable temporaire autorise des constantes au moment de la compilation comme paramètres `in`.
- Une variable temporaire autorise des propriétés ou d’autres expressions pour les paramètres `in`.
- Une variable temporaire autorise des arguments pour lesquels il existe une conversion implicite de type d’argument en type de paramètre.

Dans toutes les instances précédentes, le compilateur crée une variable temporaire qui stocke la valeur de la constante, la propriété ou une autre expression.

Le code suivant illustre ces règles :

```csharp
static void Method(in int argument)
{
    // implementation removed
}

Method(5); // OK, temporary variable created.
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // OK, temporary int created with the value 0
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // passed by readonly reference
Method(in i); // passed by readonly reference, explicitly using `in`
```

Supposons à présent qu’une autre méthode utilisant des arguments par valeur est disponible. Les résultats changent comme illustré dans le code suivant :

```csharp
static void Method(int argument)
{
    // implementation removed
}

static void Method(in int argument)
{
    // implementation removed
}

Method(5); // Calls overload passed by value
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // Calls overload passed by value.
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // Calls overload passed by value
Method(in i); // passed by readonly reference, explicitly using `in`
```

Le seul appel de méthode dans lequel l’argument est passé par référence est le dernier.

> [!NOTE]
> Le code précédent utilise `int` comme type d’argument par souci de simplicité. Comme `int` n’est pas plus volumineux qu’une référence dans la plupart des ordinateurs modernes, il n’y aucun avantage à passer un seul `int` comme référence en lecture seule. 

## <a name="limitations-on-in-parameters"></a>Limitations sur les paramètres `in`

Vous ne pouvez pas utiliser les mots clés `in`, `ref` ou `out` pour les types de méthodes suivants :  
  
- Méthodes async, que vous définissez à l’aide du modificateur [async](async.md).  
- Les méthodes Iterator, qui incluent une instruction [yield return](yield.md) ou `yield break`.  

## <a name="c-language-specification"></a>Spécification du langage C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Voir aussi

- [Référence C#](../index.md)  
- [Guide de programmation C#](../../programming-guide/index.md)  
- [Mots clés C#](index.md)  
- [Paramètres de méthodes](method-parameters.md)  
- [Sémantique de référence avec les types valeur](../../reference-semantics-with-value-types.md)  
