---
title: Exemple de classe COM - Guide de programmation C#
ms.date: 07/20/2015
helpviewer_keywords:
- examples [C#], COM classes
- COM, exposing Visual C# objects to
ms.assetid: 6504dea9-ad1c-4993-a794-830fec5270af
ms.openlocfilehash: 6051ff91d13a3cb3ca6229d813db34dd6a9f3af6
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241849"
---
# <a name="example-com-class-c-programming-guide"></a>Exemple de classe COM (Guide de programmation C#)
Voici un exemple de classe pouvant être exposée en tant qu’objet COM. Après avoir placé ce code dans un fichier .cs et l’avoir ajouté à votre projet, affectez la valeur **True** à la propriété **Inscrire pour COM Interop**. Pour plus d’informations, consultez [Guide pratique pour inscrire un composant pour COM Interop](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w29wacsy(v=vs.100)).
  
 L’exposition d’objets Visual C# à COM nécessite de déclarer une interface de classe, une interface d’événements si nécessaire, et la classe proprement dite. Les membres de classe doivent suivre ces règles pour être visibles par COM :  
  
- La classe doit être publique.  
  
- Les propriétés, méthodes et événements doivent être publics.  
  
- Les propriétés et méthodes doivent être déclarées dans l’interface de classe.  
  
- Les événements doivent être déclarés dans l’interface d’événement.  
  
 Les autres membres publics de la classe qui ne sont pas déclarés dans ces interfaces ne seront pas visibles par COM, mais ils seront visibles par d’autres objets .NET.  
  
 Pour exposer des propriétés et des méthodes à COM, vous devez les déclarer sur l’interface de classe, les marquer avec un attribut `DispId` et les implémenter dans la classe. L’ordre dans lequel les membres sont déclarés dans l’interface est l’ordre utilisé pour la vtable COM.  
  
 Pour exposer des événements à partir de votre classe, vous devez les déclarer sur l’interface d’événement et les marquer avec un attribut `DispId`. La classe ne doit pas implémenter cette interface.  
  
 La classe implémente l’interface de classe ; elle peut implémenter plusieurs interfaces, mais la première implémentation sera l’interface de classe par défaut. Implémentez ici les méthodes et propriétés exposées à COM. Elles doivent être marquées comme publiques et doivent correspondre aux déclarations dans l’interface de classe. Vous devez aussi déclarer ici les événements déclenchés par la classe. Ils doivent être marqués comme publics et doivent correspondre aux déclarations dans l’interface d’événement.  
  
## <a name="example"></a>Exemple  
 [!code-csharp[csProgGuideInterop#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInterop/CS/ExampleCOM.cs#8)]  
  
## <a name="see-also"></a>Voir aussi

- [Guide de programmation C#](../index.md)
- [Interopérabilité](./index.md)
- [Générer, page du Concepteur de projets (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp)
