---
title: -rootnamespace
ms.date: 03/13/2018
f1_keywords:
- /rootnamespace
- rootnamespace
helpviewer_keywords:
- /rootnamespace compiler option [Visual Basic]
- -rootnamespace compiler option [Visual Basic]
- rootnamespace compiler option [Visual Basic]
ms.assetid: e9245edf-6bef-420d-a7c7-324117752783
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 13bce09ca9fd1ae9ebb919a9245d8ccf87fbde1d
ms.sourcegitcommit: 6eac9a01ff5d70c6d18460324c016a3612c5e268
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/17/2018
ms.locfileid: "45692682"
---
# <a name="-rootnamespace"></a>-rootnamespace
Spécifie un espace de noms pour toutes les déclarations de type.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
-rootnamespace:namespace  
```  
  
## <a name="arguments"></a>Arguments  
  
|Terme|Définition|  
|---|---|  
|`namespace`|Le nom de l’espace de noms dans lequel encadrer toutes les déclarations de type pour le projet actuel.|  
  
## <a name="remarks"></a>Notes  
 Si vous utilisez le fichier exécutable de Visual Studio (Devenv.exe) pour compiler un projet créé dans l’environnement de développement intégré Visual Studio, utilisez `-rootnamespace` pour spécifier la valeur de la <xref:VSLangProj80.VBProjectProperties3.RootNamespace%2A> propriété. Consultez [commutateurs de ligne de commande Devenv](/visualstudio/ide/reference/devenv-command-line-switches) pour plus d’informations.  
  
 Utiliser le common language runtime MSIL Disassembler (`Ildasm.exe`) pour afficher les noms d’espace de noms dans votre fichier de sortie.  
  
|Pour définir - rootnamespace dans l’environnement de développement intégré Visual Studio|  
|---|  
|1.  Sélectionnez un projet dans l' **Explorateur de solutions**. Dans le menu **Projet**, cliquez sur **Propriétés**. <br />2.  Cliquez sur l’onglet **Application** .<br />3.  Modifiez la valeur dans le **racine Namespace** boîte.|  
  
## <a name="example"></a>Exemple  
 Le code suivant compile `In.vb` et englobe toutes les déclarations de type dans l’espace de noms `mynamespace`.  
  
```console
vbc -rootnamespace:mynamespace in.vb  
```  
  
## <a name="see-also"></a>Voir aussi

- [Compilateur de ligne de commande de Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)  
- [Ildasm.exe (désassembleur IL)](../../../framework/tools/ildasm-exe-il-disassembler.md)  
- [Exemples de lignes de commande de compilation](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
