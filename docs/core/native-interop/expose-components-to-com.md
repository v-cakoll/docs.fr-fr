---
title: Exposition de composants .NET Core à COM
ms.date: 07/12/2019
helpviewer_keywords:
- exposing .NET Core components to COM
- interoperation with unmanaged code, exposing .NET Core components
- COM interop, exposing COM components
ms.assetid: 21271167-fe7f-46ba-a81f-a6812ea649d4
author: jkoritzinsky
ms.author: jekoritz
ms.openlocfilehash: 33574eeac5b1f7aa2067b1974f3f2e68fb22e8ff
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577171"
---
# <a name="exposing-net-core-components-to-com"></a>Exposition de composants .NET Core à COM

Dans .NET Core, le processus d’exposition de vos objets .NET à COM a été considérablement simplifié par rapport au .NET Framework. Le processus suivant vous guide tout au long de l’exposition d’une classe à COM. Ce didacticiel vous montre comment effectuer les opérations suivantes :

- Exposer une classe à COM à partir de .NET Core.
- Générer un serveur COM dans le cadre de la génération de votre bibliothèque .NET Core.
- Générer automatiquement un manifeste de serveur côte à côte pour COM sans registre.

## <a name="prerequisites"></a>Prérequis

- Installez le [SDK .NET Core 3.0 Preview 7](https://www.microsoft.com/net/core) ou une version plus récente.

## <a name="create-the-library"></a>Créer la bibliothèque

La première étape consiste à créer la bibliothèque.

1. Créez un dossier, puis exécutez-y `dotnet new classlib`.
2. Ouvrez `Class1.cs`.
3. Ajoutez `using System.Runtime.InteropServices;` en haut du fichier.
4. Créez une interface nommée `IServer`. Par exemple : [!code-csharp[The IServer interface](~/samples/core/extensions/COMServerDemo/COMContract/IServer.cs)]
5. Ajoutez l’attribut `[Guid("<IID>")]` à l’interface, avec le GUID d’interface pour l’interface COM que vous implémentez. Par exemple, `[Guid("fe103d6e-e71b-414c-80bf-982f18f6c1c7")]`. Notez que ce GUID doit être unique, car il s’agit du seul identificateur de cette interface pour COM. Dans Visual Studio, vous pouvez générer un GUID en accédant à Outils > Créer un GUID pour ouvrir l’outil Créer un GUID.
6. Ajoutez l’attribut `[InterfaceType]` à l’interface et spécifiez les interfaces COM de base que votre interface doit implémenter.
7. Créez une classe nommée `Server` qui implémente `IServer`.
8. Ajoutez l’attribut `[Guid("<CLSID>")]` à la classe, avec le GUID de l’identificateur de classe pour la classe COM que vous implémentez. Par exemple, `[Guid("9f35b6f5-2c05-4e7f-93aa-ee087f6e7ab6")]`. Comme avec le GUID d’interface, ce GUID doit être unique, car il est le seul identificateur de cette interface pour COM.
9. Ajoutez l’attribut `[ComVisible(true)]` à la fois à l’interface et à la classe.

> [!IMPORTANT]
> Contrairement au .NET Framework, .NET Core vous oblige à spécifier le CLSID des classes que vous voulez rendre activables via COM.

## <a name="generate-the-com-host"></a>Générer l’hôte COM

1. Ouvrez le fichier projet `.csproj` et ajoutez `<EnableComHosting>true</EnableComHosting>` à l’intérieur d’une balise `<PropertyGroup></PropertyGroup>`.
2. Générez le projet.

La sortie résultante a un fichier `ProjectName.dll`, `ProjectName.deps.json`, `ProjectName.runtimeconfig.json` et `ProjectName.comhost.dll`.

## <a name="register-the-com-host-for-com"></a>Inscrire l’hôte COM pour COM

Ouvrez une invite de commandes avec élévation de privilèges et exécutez `regsvr32 ProjectName.comhost.dll`. Ceci inscrit tous vos objets .NET exposés auprès de COM.

## <a name="enabling-regfree-com"></a>Activation de COM sans registre

1. Ouvrez le fichier projet `.csproj` et ajoutez `<EnableRegFreeCom>true</EnableRegFreeCom>` à l’intérieur d’une balise `<PropertyGroup></PropertyGroup>`.
2. Générez le projet.

La sortie résultante a un fichier `ProjectName.X.manifest`. Ce fichier est le manifeste côte à côte à utiliser avec COM sans registre.

## <a name="sample"></a>Exemple

Un [exemple de serveur COM](https://github.com/dotnet/samples/tree/master/core/extensions/COMServerDemo) entièrement fonctionnel se trouve dans le dépôt dotnet/samples sur GitHub.

## <a name="additional-notes"></a>Remarques supplémentaires

Contrairement au .NET Framework, .NET Core ne prend pas en charge la génération d’une bibliothèque de types COM à partir d’un assembly .NET Core. Vous devez écrire manuellement un fichier IDL ou un en-tête C++ pour les déclarations natives de vos interfaces.

En outre, le chargement du .NET Framework et de .NET Core dans le même processus n’est pas pris en charge : par conséquent, le chargement d’un serveur COM .NET Core dans un processus client COM .NET Framework ou vice versa n’est pas pris en charge.