---
title: Intégration de WPF et WF en XAML
ms.date: 03/30/2017
ms.assetid: a4f53b48-fc90-4315-bca0-ba009562f488
ms.openlocfilehash: b8015e5c526f58875beb58ab48a21c050bdc8a06
ms.sourcegitcommit: 42ed59871db1f29a32b3d8e7abeb20e6eceeda7c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/10/2019
ms.locfileid: "74960086"
---
# <a name="wpf-and-windows-workflow-foundation-integration-in-xaml"></a>Intégration de WPF et de Windows Workflow Foundation en XAML

Cet exemple montre comment créer une application qui utilise des fonctionnalités Windows Presentation Foundation (WPF) et Windows Workflow Foundation (WF) dans un document XAML unique. Pour ce faire, l’exemple utilise Windows Workflow Foundation et l’extensibilité XAML.

## <a name="sample-details"></a>Détails de l'exemple

 Le fichier ShowWindow.xaml désérialise dans une activité <xref:System.Activities.Statements.Sequence> avec deux variables String manipulées par les activités de la séquence : `ShowWindow` et `WriteLine`. L'activité <xref:System.Activities.Statements.WriteLine> renvoie dans la fenêtre de console l'expression qu'elle assigne à la propriété <xref:System.Activities.Statements.WriteLine.Text%2A>. L’activité `ShowWindow` affiche une fenêtre WPF dans le cadre de sa logique d’exécution. Le <xref:System.Activities.ActivityContext.DataContext%2A> de la fenêtre inclut les variables déclarées dans la séquence. Les contrôles de la fenêtre déclarée dans l'activité `ShowWindow` utilisent la liaison de données pour manipuler ces variables. Enfin, la fenêtre contient un contrôle bouton. L'événement `Click` pour le bouton est géré par <xref:System.Activities.ActivityDelegate> nommé `MarkupExtension` qui contient une activité `CloseWindow`. `MarkUpExtension` appelle l'activité contenue qui fournit, comme contexte, tous les objets identifiés par `x:Name`, ainsi que le <xref:System.Activities.ActivityContext.DataContext%2A> de la fenêtre. Ainsi, le `CloseWindow.InArgument<Window>` peut être lié à l'aide d'une expression qui référence le nom de la fenêtre.

 L’activité `ShowWindow` dérive de la classe <xref:System.Activities.AsyncCodeActivity%601> pour afficher une fenêtre WPF et se termine lorsque la fenêtre est fermée. La propriété `Window` est de type `Func<Window>` qui autorise la création de la fenêtre à la demande pour chaque exécution de l'activité. La propriété `Window` utilise un <xref:System.Xaml.XamlDeferringLoader> pour activer ce modèle d'évaluation différé. Le `FuncFactoryDeferringLoader` permet la capture d'un `XamlReader` pendant la sérialisation, puis sa lecture pendant l'exécution de l'activité.

 Une activité bien écrite ne bloque jamais le thread de planificateur. Toutefois, l'activité `ShowWindow` ne peut pas se terminer tant que la fenêtre qu'elle affiche n'est pas fermée. L'activité `ShowWindow` parvient à ce comportement en dérivant de <xref:System.Activities.AsyncCodeActivity>, en appelant la méthode <xref:System.Activities.WorkflowInvoker.BeginInvoke%2A> dans la méthode <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> et en affichant la fenêtre de façon modale. Le délégué est appelé via le <xref:System.ServiceModel.InstanceContext.SynchronizationContext%2A> WPF. L'activité `ShowWindow` assigne la propriété <xref:System.Activities.ActivityContext.DataContext%2A> à la propriété `Window.DataContext` pour fournir un accès des contrôles liés aux données aux variables dans la portée.

 Le dernier point intéressant dans cet exemple est un <xref:System.Workflow.ComponentModel.Serialization.MarkupExtension> appelé `DelegateActivityExtension`. La méthode `ProvideValue` de cette extension de balisage retourne un délégué qui appelle une activité incorporée. Cette activité s’exécute dans un environnement qui comprend le contexte de données WPF et toute `x:Name` valeurs dans la portée. Dans la méthode `GenericInvoke`, cet environnement est fourni à l'activité via une extension <xref:System.Activities.Hosting.SymbolResolver>. Cette extension est ajoutée à un <xref:System.Activities.WorkflowInvoker> utilisé ensuite pour appeler l’activité incorporée chaque fois que le délégué de l’extension de balisage est appelé.

> [!NOTE]
> Le concepteur par défaut ne prend pas en charge l'activité ShowWindow ; ainsi, le fichier ShowWindow.Xaml ne s'affiche pas correctement dans le concepteur.

## <a name="run-the-sample"></a>Exécuter l'exemple

1. À l’aide de Visual Studio, ouvrez le fichier solution WPFWFIntegration. sln.

2. Pour générer la solution, appuyez sur **Ctrl**+**MAJ**+**B**.

3. Pour exécuter la solution, appuyez sur **F5**.

4. Tapez vos prénom et nom dans la boîte de dialogue.

5. Fermez la boîte de dialogue et la console répète votre nom.

> [!IMPORTANT]
> Les exemples peuvent déjà être installés sur votre ordinateur. Recherchez le répertoire (par défaut) suivant avant de continuer.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Si ce répertoire n’existe pas, accédez à [Windows Communication Foundation (WCF) et Windows Workflow Foundation (WF) exemples pour .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) pour télécharger tous les exemples Windows Communication Foundation (WCF) et [!INCLUDE[wf1](../../../../includes/wf1-md.md)]. Cet exemple se trouve dans le répertoire suivant.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\WPFWFIntegration`
