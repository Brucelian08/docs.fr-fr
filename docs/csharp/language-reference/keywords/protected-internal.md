---
title: protected internal (Référence C#)
ms.date: 11/15/2017
author: sputier
ms.openlocfilehash: 1a305cb84989f12350e2e7cc28dd18f9d0c7ae5e
ms.sourcegitcommit: 6eac9a01ff5d70c6d18460324c016a3612c5e268
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/17/2018
ms.locfileid: "45613902"
---
# <a name="protected-internal-c-reference"></a>protected internal (Référence C#)

La combinaison de mots clés `protected internal` est un modificateur d’accès de membre. Un membre interne protégé est accessible depuis l’assembly actif ou depuis des types dérivés de la classe conteneur. Pour obtenir une comparaison de `protected internal` et des autres modificateurs d’accès, consultez [Niveaux d’accessibilité](accessibility-levels.md).

## <a name="example"></a>Exemple

Un membre interne protégé d’une classe de base est accessible depuis n’importe quel type au sein de son assembly conteneur. Il est également accessible dans une classe dérivée qui se trouve dans un autre assembly seulement si l’accès s’effectue via une variable du type de la classe dérivée. Prenons l’exemple de l’extrait de code suivant :

```csharp
// Assembly1.cs
// Compile with: /target:library
public class BaseClass
{
   protected internal int myValue = 0;
}

class TestAccess
{
    void Access()
    {
        BaseClass baseObject = new BaseClass();
        baseObject.myValue = 5;
    }
}
```

```csharp
// Assembly2.cs
// Compile with: /reference:Assembly1.dll
class DerivedClass : BaseClass
{
    static void Main()
    {
        BaseClass baseObject = new BaseClass();
        DerivedClass derivedObject = new DerivedClass();

        // Error CS1540, because myValue can only be accessed by
        // classes derived from BaseClass.
        // baseObject.myValue = 10;

        // OK, because this class derives from BaseClass.
        derivedObject.myValue = 10;
    }
}
```
Cet exemple contient deux fichiers : `Assembly1.cs` et `Assembly2.cs`.
Le premier fichier contient une classe de base publique, `BaseClass`, et une autre classe, `TestAccess`. `BaseClass` possède un membre interne protégé, `myValue`, à laquelle le type `TestAccess` accède.
Dans le deuxième fichier, une tentative d’accès à `myValue` via une instance de `BaseClass` génère une erreur, tandis qu’un accès à ce membre via une instance d’une classe dérivée, `DerivedClass`, réussit.

Les membres de struct ne peuvent pas être `protected internal`, car le struct ne peut pas être hérité.

## <a name="c-language-specification"></a>spécification du langage C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Voir aussi

- [Référence C#](../index.md)
- [Guide de programmation C#](../../programming-guide/index.md)
- [Mots clés C#](index.md)
- [Modificateurs d’accès](access-modifiers.md)
- [Niveaux d’accessibilité](accessibility-levels.md)
- [Modificateurs](modifiers.md)
- [public](public.md)
- [private](private.md)
- [internal](internal.md)
- [Problèmes de sécurité pour les mots clés virtuels internes](https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-4.0/heyd8kky(v=vs.100))