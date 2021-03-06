---
title: Guide pratique pour s'abonner et se désabonner d’événements (guide de programmation C#)
ms.date: 07/20/2015
helpviewer_keywords:
- event handlers [C#], creating
- Code Editor, event handlers
- events [C#], creating using the IDE
ms.assetid: 6319f39f-282c-4173-8a62-6c4657cf51cd
ms.openlocfilehash: e27473ca34f634f4a3125a2e87e6d0ef918a6f9d
ms.sourcegitcommit: 6eac9a01ff5d70c6d18460324c016a3612c5e268
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2018
ms.locfileid: "45675858"
---
# <a name="how-to-subscribe-to-and-unsubscribe-from-events-c-programming-guide"></a>Guide pratique pour s'abonner et se désabonner d’événements (guide de programmation C#)
Vous vous abonnez à un événement publié par une autre classe lorsque vous voulez écrire du code personnalisé qui doit être appelé quand cet événement est déclenché. Par exemple, vous pouvez vous abonner à l’événement `click` d’un bouton pour permettre à votre application de réagir lorsque l’utilisateur clique sur le bouton.  
  
### <a name="to-subscribe-to-events-by-using-the-visual-studio-ide"></a>Pour s’abonner aux événements à l’aide de l’IDE de Visual Studio  
  
1.  Si vous ne voyez pas la fenêtre **Propriétés**, en mode **Création**, cliquez sur le formulaire ou le contrôle pour lequel vous voulez créer un gestionnaire d’événements, puis sélectionnez **Propriétés**.  
  
2.  En haut de la fenêtre **Propriétés**, cliquez sur l’icône **Événements**.  
  
3.  Double-cliquez sur l’événement que vous voulez créer, par exemple l’événement `Load`.  
  
     Visual C# crée une méthode de gestionnaire d’événements vide et l’ajoute à votre code. Vous pouvez également ajouter le code manuellement en mode **Code**. Par exemple, les lignes de code suivantes déclarent une méthode de gestionnaire d’événements qui est appelée lorsque la classe `Form` déclenche l’événement `Load`.  
  
     [!code-csharp[csProgGuideEvents#11](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-subscribe-to-and-unsubscribe-from-events_1.cs)]  
  
     La ligne de code qui est nécessaire pour s’abonner à l’événement est aussi générée automatiquement dans la méthode `InitializeComponent`, dans le fichier Form1.Designer.cs de votre projet. Elle ressemble à ceci :  
  
    ```csharp
    this.Load += new System.EventHandler(this.Form1_Load);  
    ```  
  
### <a name="to-subscribe-to-events-programmatically"></a>Pour s’abonner aux événements par programmation  
  
1.  Définissez une méthode de gestionnaire d’événements dont la signature correspond à la signature du délégué de l’événement. Par exemple, si l’événement est basé sur le type délégué <xref:System.EventHandler>, le code suivant représente le stub de méthode :  
  
    ```csharp
    void HandleCustomEvent(object sender, CustomEventArgs a)  
    {  
       // Do something useful here.  
    }  
    ```  
  
2.  Utilisez l’opérateur d’assignation d’addition (`+=`) pour attacher votre gestionnaire d’événements à l’événement. Dans l’exemple suivant, nous allons supposer qu’un objet nommé `publisher` a un événement nommé `RaiseCustomEvent`. Notez que la classe d’abonné nécessite une référence à la classe d’éditeur pour s’abonner à ses événements.  
  
    ```csharp
    publisher.RaiseCustomEvent += HandleCustomEvent;  
    ```  
  
     Notez que la syntaxe précédente est une nouveauté du langage C# 2.0. Elle équivaut exactement à la syntaxe du C# 1.0, dans laquelle le délégué d’encapsulation doit être explicitement créé à l’aide du mot clé `new` :  
  
    ```csharp
    publisher.RaiseCustomEvent += new CustomEventHandler(HandleCustomEvent);  
    ```  
  
     Vous pouvez également ajouter un gestionnaire d’événements à l’aide d’une expression lambda :  
  
    ```csharp
    public Form1()  
    {  
        InitializeComponent();  
        // Use a lambda expression to define an event handler.  
        this.Click += (s,e) => { MessageBox.Show(  
           ((MouseEventArgs)e).Location.ToString());};  
    }  
    ```  
  
     Pour plus d’informations, consultez [Guide pratique pour utiliser des expressions lambda en dehors de LINQ](../../../csharp/programming-guide/statements-expressions-operators/how-to-use-lambda-expressions-outside-linq.md).  
  
### <a name="to-subscribe-to-events-by-using-an-anonymous-method"></a>Pour s’abonner aux événements à l’aide d’une méthode anonyme  
  
-   Si vous savez que vous n’aurez pas à vous désabonner d’un événement, vous pouvez utiliser l’opérateur d’assignation d’addition (`+=`) pour attacher une méthode anonyme à l’événement. Dans l’exemple suivant, nous supposons qu’un objet nommé `publisher` a un événement nommé `RaiseCustomEvent`, et qu’une classe `CustomEventArgs` a également été définie pour contenir des informations d’événements spécialisés. Notez que la classe d’abonné nécessite une référence à `publisher` pour s’abonner à ses événements.  
  
    ```csharp
    publisher.RaiseCustomEvent += delegate(object o, CustomEventArgs e)  
    {  
      string s = o.ToString() + " " + e.ToString();  
      Console.WriteLine(s);  
    };  
    ```  
  
     Il est important de noter que vous ne pourrez pas vous désabonner facilement d’un événement si vous avez utilisé une fonction anonyme pour vous y inscrire. Pour vous désinscrire dans ce scénario, accédez au code dans lequel vous vous êtes abonné à l’événement, stockez la méthode anonyme dans une variable de délégué, puis ajoutez le délégué à l’événement. En général, nous recommandons de ne pas utiliser de fonctions anonymes pour vous abonner aux événements si vous devez vous en désabonner plus tard dans votre code. Pour plus d’informations sur les fonctions anonymes, consultez [Fonctions anonymes](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md).  
  
## <a name="unsubscribing"></a>Désabonnement  
 Pour éviter que votre gestionnaire d’événements ne soit appelé lorsque l’événement est déclenché, désabonnez-vous de l’événement. Pour empêcher les fuites de ressources, vous devez vous désabonner des événements avant d’éliminer un objet d’abonné. Tant que vous êtes abonné à un événement, le délégué de multidiffusion qui se trouve sous l’événement, dans l’objet de publication, comporte une référence au délégué qui encapsule le gestionnaire d’événements de l’abonné. Tant que l’objet de publication contient cette référence, le garbage collection ne supprime pas l’objet d’abonné.  
  
#### <a name="to-unsubscribe-from-an-event"></a>Pour se désabonner d’un événement  
  
-   Utilisez l’opérateur d’assignation de soustraction (`-=`) pour vous désabonner d’un événement :  
  
    ```csharp
    publisher.RaiseCustomEvent -= HandleCustomEvent;  
    ```  
  
     Lorsque tous les abonnés se sont désabonnés d’un événement, l’instance d’événement de la classe d’éditeur est définie sur `null`.  
  
## <a name="see-also"></a>Voir aussi

- [Événements](../../../csharp/programming-guide/events/index.md)  
- [event](../../../csharp/language-reference/keywords/event.md)  
- [Comment : publier des événements conformes aux indications du .NET Framework](../../../csharp/programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md)  
- [-=, opérateur (référence C#)](../../language-reference/operators/subtraction-assignment-operator.md)  
- [+= (opérateur)](../../../csharp/language-reference/operators/addition-assignment-operator.md)