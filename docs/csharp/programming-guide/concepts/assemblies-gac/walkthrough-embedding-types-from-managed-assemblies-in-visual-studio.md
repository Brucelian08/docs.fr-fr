---
title: 'Procédure pas à pas : incorporation de types provenant d’assemblys managés dans Visual Studio (C#)'
ms.date: 07/20/2015
ms.assetid: 55ed13c9-c5bb-4bc2-bcd8-0587eb568864
ms.openlocfilehash: 1900c62d1ebaf611f141f8f1bdf95f8d11f82140
ms.sourcegitcommit: 6eac9a01ff5d70c6d18460324c016a3612c5e268
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2018
ms.locfileid: "45668390"
---
# <a name="walkthrough-embedding-types-from-managed-assemblies-in-visual-studio-c"></a>Procédure pas à pas : incorporation de types provenant d’assemblys managés dans Visual Studio (C#)
Si vous incorporez des informations de type d’un assembly managé avec nom fort, vous pouvez coupler faiblement des types dans une application pour obtenir une indépendance de version. Autrement dit, votre programme peut être écrit de façon à ce qu’il utilise des types de plusieurs versions d’une bibliothèque managée sans que vous n’ayez à effectuer de recompilation pour chaque version.  
  
 L’incorporation de type est fréquemment utilisée avec COM Interop, par exemple pour une application qui utilise des objets Automation de Microsoft Office. L’incorporation des informations de type permet à la même build d’un programme de fonctionner avec différentes versions de Microsoft Office sur plusieurs ordinateurs. Toutefois, vous pouvez également utiliser l’incorporation de type avec une solution totalement managée.  
  
 Les informations de type peuvent être incorporées à partir d’un assembly doté des caractéristiques suivantes :  
  
-   L’assembly expose au moins une interface publique.  
  
-   Les interfaces incorporées sont annotées avec un attribut `ComImport` et un attribut `Guid` (et un GUID unique).  
  
-   L’assembly est annoté avec l’attribut `ImportedFromTypeLib` ou l’attribut `PrimaryInteropAssembly` et un attribut `Guid` au niveau de l’assembly. (Par défaut, les modèles de projet Visual C# incluent un attribut `Guid` au niveau de l’assembly.)  
  
 Après avoir spécifié les interfaces publiques qui peuvent être incorporées, vous pouvez créer des classes runtime qui implémentent ces interfaces. Un programme client peut ensuite incorporer les informations de type pour ces interfaces au moment de la conception en référençant l’assembly qui contient les interfaces publiques et en affectant à la propriété `Embed Interop Types` de la référence la valeur `True`. Cela revient à utiliser le compilateur de ligne de commande et à référencer l’assembly à l’aide de l’option de compilateur `/link`. Le programme client peut ensuite charger des instances de vos objets d’exécution possédant le même type que ces interfaces. Si vous créez une version de votre assembly runtime avec nom fort, le programme client n’a pas besoin d’être recompilé avec l’assembly runtime mis à jour. En revanche, le programme client continue d’utiliser la version de l’assembly runtime disponible avec les informations de type incorporées pour les interfaces publiques.  
  
 Étant donné que la fonction principale de l’incorporation de type est de prendre en charge l’incorporation d’informations de type à partir d’assemblys COM Interop, les limitations suivantes s’appliquent quand vous incorporez des informations de type dans une solution totalement managée :  
  
-   Seuls les attributs spécifiques à COM Interop sont incorporés ; les autres attributs sont ignorés.  
  
-   Si un type utilise des paramètres génériques et que le type du paramètre générique est un type incorporé, ce type ne peut pas être utilisé au-delà de la limite de l’assembly. Les exemples de passage de la limite de l’assembly incluent l’appel d’une méthode à partir d’un autre assembly ou la dérivation d’un type à partir d’un type défini dans un autre assembly.  
  
-   Les constantes ne sont pas incorporées.  
  
-   La classe <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> ne prend pas en charge un type incorporé comme clé. Vous pouvez implémenter votre propre type de dictionnaire pour prendre en charge un type incorporé comme clé.  
  
 Dans cette procédure pas à pas, vous exécuterez les étapes suivantes :  
  
-   Créer un assembly avec nom fort doté d’une interface publique contenant des informations de type qui peuvent être incorporées.  
  
-   Créer un assembly runtime avec nom fort qui implémente cette interface publique.  
  
-   Créer un programme client qui incorpore les informations de type de l’interface publique et crée une instance de la classe à partir de l’assembly runtime.  
  
-   Modifier et régénérer l’assembly runtime.  
  
-   Exécuter le programme client pour constater que la nouvelle version de l’assembly runtime est utilisée sans devoir recompiler le programme client.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="creating-an-interface"></a>Création d’une interface  
  
#### <a name="to-create-the-type-equivalence-interface-project"></a>Pour créer le projet d’interface d’équivalence des types  
  
1.  Dans Visual Studio, dans le menu **Fichier**, choisissez **Nouveau**, puis cliquez sur **Projet**.  
  
2.  Dans la boîte de dialogue **Nouveau projet**, dans le volet **Types de projets**, vérifiez que **Windows** est sélectionné. Sélectionnez **Bibliothèque de classes** dans le volet **Modèles**. Dans la zone **Nom**, tapez `TypeEquivalenceInterface`, puis cliquez sur **OK**. Le nouveau projet est créé.  
  
3.  Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le fichier Class1.cs, puis cliquez sur **Renommer**. Renommez le fichier `ISampleInterface.cs` et appuyez sur Entrée. Quand vous renommez le fichier, la classe est également renommée `ISampleInterface`. Cette classe représente l’interface publique pour la classe.  
  
4.  Cliquez avec le bouton droit sur le projet TypeEquivalenceInterface, puis cliquez sur **Propriétés**. Cliquez sur l’onglet **Générer**. Affectez au chemin de sortie un emplacement valide sur votre ordinateur de développement, tel que `C:\TypeEquivalenceSample`. Cet emplacement sera également utilisé dans une étape ultérieure de cette procédure pas à pas.  
  
5.  Tout en modifiant les propriétés de projet, cliquez sur l’onglet **Signature**. Sélectionnez l’option **Signer l’assembly**. Dans la liste **Choisir un fichier de clé de nom fort**, cliquez sur **<Nouveau...>**. Dans la zone **Nom du fichier de clé**, tapez `key.snk`. Décochez la case **Protéger mon fichier de clé par un mot de passe**. Cliquez sur **OK**.  
  
6.  Ouvrez le fichier ISampleInterface.cs. Ajoutez le code suivant au fichier de classe ISampleInterface pour créer l’interface ISampleInterface.  
  
    ```csharp  
    using System;  
    using System.Runtime.InteropServices;  
  
    namespace TypeEquivalenceInterface  
    {  
        [ComImport]  
        [Guid("8DA56996-A151-4136-B474-32784559F6DF")]  
        public interface ISampleInterface  
        {  
            void GetUserInput();  
            string UserInput { get; }  
        }  
    }  
    ```  
  
7.  Dans le menu **Outils**, cliquez sur **Créer un Guid**. Dans la boîte de dialogue **Créer un Guid**, cliquez sur **Format du Registre**, puis sur **Copier**. Cliquez sur **Quitter**.  
  
8.  Dans l’attribut `Guid`, supprimez l’exemple de GUID et collez le GUID que vous avez copié à partir de la boîte de dialogue **Créer un Guid**. Supprimez les accolades ({}) du GUID copié.  
  
9. Dans l’**Explorateur de solutions**, développez le dossier **Propriétés**. Double-cliquez sur le fichier AssemblyInfo.cs. Ajoutez l’attribut suivant au fichier.  
  
    ```csharp  
    [assembly: ImportedFromTypeLib("")]  
    ```  
  
     Enregistrez le fichier.  
  
10. Enregistrez le projet.  
  
11. Cliquez avec le bouton droit sur le projet TypeEquivalenceInterface, puis cliquez sur **Générer**. Le fichier .dll de bibliothèque de classes est compilé et enregistré dans le chemin de sortie de la génération spécifié (par exemple, C:\TypeEquivalenceSample).  
  
## <a name="creating-a-runtime-class"></a>Création d’une classe runtime  
  
#### <a name="to-create-the-type-equivalence-runtime-project"></a>Pour créer le projet d’exécution d’équivalence des types  
  
1.  Dans Visual Studio, dans le menu **Fichier**,pointez sur **Nouveau**, puis cliquez sur **Projet**.  
  
2.  Dans la boîte de dialogue **Nouveau projet**, dans le volet **Types de projets**, vérifiez que **Windows** est sélectionné. Sélectionnez **Bibliothèque de classes** dans le volet **Modèles**. Dans la zone **Nom**, tapez `TypeEquivalenceRuntime`, puis cliquez sur **OK**. Le nouveau projet est créé.  
  
3.  Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le fichier Class1.cs, puis cliquez sur **Renommer**. Renommez le fichier `SampleClass.cs` et appuyez sur Entrée. Quand vous renommez le fichier, la classe est également renommée `SampleClass`. Cette classe va implémenter l’interface `ISampleInterface`.  
  
4.  Cliquez avec le bouton droit sur le projet TypeEquivalenceRuntime, puis cliquez sur **Propriétés**. Cliquez sur l’onglet **Générer**. Affectez au chemin de sortie le même emplacement que celui que vous avez utilisé dans le projet TypeEquivalenceInterface, par exemple `C:\TypeEquivalenceSample`.  
  
5.  Tout en modifiant les propriétés de projet, cliquez sur l’onglet **Signature**. Sélectionnez l’option **Signer l’assembly**. Dans la liste **Choisir un fichier de clé de nom fort**, cliquez sur **<Nouveau...>**. Dans la zone **Nom du fichier de clé**, tapez `key.snk`. Décochez la case **Protéger mon fichier de clé par un mot de passe**. Cliquez sur **OK**.  
  
6.  Cliquez avec le bouton droit sur le projet TypeEquivalenceRuntime, puis cliquez sur **Ajouter une référence**. Cliquez sur l’onglet **Parcourir** et recherchez le dossier du chemin de sortie. Sélectionnez le fichier TypeEquivalenceInterface.dll et cliquez sur **OK**.  
  
7.  Dans l’**Explorateur de solutions**, développez le dossier **Références**. Sélectionnez la référence TypeEquivalenceInterface. Dans la fenêtre Propriétés de la référence TypeEquivalenceInterface, affectez à la propriété **Version spécifique** la valeur **False**.  
  
8.  Ajoutez le code suivant au fichier de classe SampleClass pour créer la classe SampleClass.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using TypeEquivalenceInterface;  
  
    namespace TypeEquivalenceRuntime  
    {  
        public class SampleClass : ISampleInterface  
        {  
            private string p_UserInput;  
            public string UserInput { get { return p_UserInput; } }  
  
            public void GetUserInput()  
            {  
                Console.WriteLine("Please enter a value:");  
                p_UserInput = Console.ReadLine();  
            }  
        }  
    )  
    ```  
  
9. Enregistrez le projet.  
  
10. Cliquez avec le bouton droit sur le projet TypeEquivalenceRuntime, puis cliquez sur **Générer**. Le fichier .dll de bibliothèque de classes est compilé et enregistré dans le chemin de sortie de la génération spécifié (par exemple, C:\TypeEquivalenceSample).  
  
## <a name="creating-a-client-project"></a>Création d’un projet client  
  
#### <a name="to-create-the-type-equivalence-client-project"></a>Pour créer le projet client d’équivalence des types  
  
1.  Dans Visual Studio, dans le menu **Fichier**,pointez sur **Nouveau**, puis cliquez sur **Projet**.  
  
2.  Dans la boîte de dialogue **Nouveau projet**, dans le volet **Types de projets**, vérifiez que **Windows** est sélectionné. Sélectionnez **Application console** dans le volet **Modèles**. Dans la zone **Nom**, tapez `TypeEquivalenceClient`, puis cliquez sur **OK**. Le nouveau projet est créé.  
  
3.  Cliquez avec le bouton droit sur le projet TypeEquivalenceClient, puis cliquez sur **Propriétés**. Cliquez sur l’onglet **Générer**. Affectez au chemin de sortie le même emplacement que celui que vous avez utilisé dans le projet TypeEquivalenceInterface, par exemple `C:\TypeEquivalenceSample`.  
  
4.  Cliquez avec le bouton droit sur le projet TypeEquivalenceClient, puis cliquez sur **Ajouter une référence**. Cliquez sur l’onglet **Parcourir** et recherchez le dossier du chemin de sortie. Sélectionnez le fichier TypeEquivalenceInterface.dll (pas le fichier TypeEquivalenceRuntime.dll) et cliquez sur **OK**.  
  
5.  Dans l’**Explorateur de solutions**, développez le dossier **Références**. Sélectionnez la référence TypeEquivalenceInterface. Dans la fenêtre Propriétés de la référence TypeEquivalenceInterface, affectez à la propriété **Incorporer les types d’interopérabilité** la valeur **True**.  
  
6.  Ajoutez le code suivant au fichier Program.cs pour créer le programme client.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using TypeEquivalenceInterface;  
    using System.Reflection;  
  
    namespace TypeEquivalenceClient  
    {  
        class Program  
        {  
            static void Main(string[] args)  
            {  
                Assembly sampleAssembly = Assembly.Load("TypeEquivalenceRuntime");  
                ISampleInterface sampleClass =   
                    (ISampleInterface)sampleAssembly.CreateInstance("TypeEquivalenceRuntime.SampleClass");  
                sampleClass.GetUserInput();  
                Console.WriteLine(sampleClass.UserInput);  
                Console.WriteLine(sampleAssembly.GetName().Version.ToString());  
                Console.ReadLine();  
            }  
        }  
    }  
    ```  
  
7.  Appuyez sur CTRL+F5 pour générer et exécuter le programme.  
  
## <a name="modifying-the-interface"></a>Modification de l’interface  
  
#### <a name="to-modify-the-interface"></a>Pour modifier l’interface  
  
1.  Dans Visual Studio, dans le menu **Fichier**, pointez sur **Ouvrir**, puis cliquez sur **Projet/Solution**.  
  
2.  Dans la boîte de dialogue **Ouvrir un projet**, cliquez avec le bouton droit sur le projet TypeEquivalenceInterface, puis cliquez sur **Propriétés**. Cliquez sur l’onglet **Application** . Cliquez sur le bouton **Informations de l’assembly**. Remplacez les valeurs de **Version de l’assembly** et **Version de fichier** par `2.0.0.0`.  
  
3.  Ouvrez le fichier SampleInterface.cs. Ajoutez la ligne de code suivante à l’interface ISampleInterface.  
  
    ```csharp  
    DateTime GetDate();  
    ```  
  
     Enregistrez le fichier.  
  
4.  Enregistrez le projet.  
  
5.  Cliquez avec le bouton droit sur le projet TypeEquivalenceInterface, puis cliquez sur **Générer**. Une nouvelle version du fichier .dll de bibliothèque de classes est compilée et enregistrée dans le chemin de sortie de la génération spécifié (par exemple, C:\TypeEquivalenceSample).  
  
## <a name="modifying-the-runtime-class"></a>Modification de la classe runtime  
  
#### <a name="to-modify-the-runtime-class"></a>Pour modifier la classe runtime  
  
1.  Dans Visual Studio, dans le menu **Fichier**, pointez sur **Ouvrir**, puis cliquez sur **Projet/Solution**.  
  
2.  Dans la boîte de dialogue **Ouvrir un projet**, cliquez avec le bouton droit sur le projet TypeEquivalenceRuntime, puis cliquez sur **Propriétés**. Cliquez sur l’onglet **Application** . Cliquez sur le bouton **Informations de l’assembly**. Remplacez les valeurs de **Version de l’assembly** et **Version de fichier** par `2.0.0.0`.  
  
3.  Ouvrez le fichier SampleClass.cs. Ajoutez les lignes de code suivantes à la classe SampleClass.  
  
    ```csharp  
    public DateTime GetDate()  
    {  
        return DateTime.Now;  
    }  
    ```  
  
     Enregistrez le fichier.  
  
4.  Enregistrez le projet.  
  
5.  Cliquez avec le bouton droit sur le projet TypeEquivalenceRuntime, puis cliquez sur **Générer**. Une version mise à jour du fichier .dll de bibliothèque de classes est compilée et enregistrée dans le chemin de sortie de la génération précédemment spécifié (par exemple, C:\TypeEquivalenceSample).  
  
6.  Dans l’Explorateur de fichiers, ouvrez le dossier du chemin de sortie (par exemple, C:\TypeEquivalenceSample). Double-cliquez sur le fichier TypeEquivalenceClient.exe pour exécuter le programme. Le programme reflète la nouvelle version de l’assembly TypeEquivalenceRuntime sans aucune recompilation.  
  
## <a name="see-also"></a>Voir aussi

- [/link (Options du compilateur C#)](../../../../csharp/language-reference/compiler-options/link-compiler-option.md)  
- [Guide de programmation C#](../../../../csharp/programming-guide/index.md)  
- [Programmation à l’aide d’assemblys](../../../../framework/app-domains/programming-with-assemblies.md)  
- [Assemblys et le Global Assembly Cache (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/index.md)
