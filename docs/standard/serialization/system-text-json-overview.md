---
title: Sérialiser et désérialiser JSON à l’aide de C#-.NET
description: Cette vue d’ensemble décrit les System.Text.Json fonctionnalités d’espace de noms pour sérialiser vers et désérialiser à partir de JSON dans .net.
ms.date: 01/10/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 909d979d46b30939e304af071de65d230febd92d
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2020
ms.locfileid: "83380135"
---
# <a name="json-serialization-and-deserialization-marshalling-and-unmarshalling-in-net---overview"></a>Sérialisation et désérialisation JSON (marshaling et démarshaling) dans .NET-vue d’ensemble

L' `System.Text.Json` espace de noms fournit des fonctionnalités pour sérialiser vers et désérialiser à partir de JavaScript Object Notation (JSON).

La conception de la bibliothèque met l’accent sur des performances élevées et une allocation de mémoire faible sur un ensemble complet de fonctionnalités. La prise en charge UTF-8 intégrée optimise le processus de lecture et d’écriture du texte JSON encodé au format UTF-8, qui est l’encodage le plus courant pour les données sur le Web et les fichiers sur le disque.

La bibliothèque fournit également des classes pour l’utilisation d’un modèle DOM (Document Object Model) en mémoire. Cette fonctionnalité permet un accès en lecture seule aléatoire des éléments dans un fichier JSON ou une chaîne.

## <a name="how-to-get-the-library"></a>Obtention de la bibliothèque

* La bibliothèque est intégrée dans le cadre de l’infrastructure partagée [.net Core 3,0](https://aka.ms/netcore3download) .
* Pour les autres frameworks cibles, installez le [System.Text.Json](https://www.nuget.org/packages/System.Text.Json) package NuGet. Le package prend en charge :
  * .NET Standard 2,0 et versions ultérieures
  * .NET Framework 4.7.2 et versions ultérieures
  * .NET Core 2,0, 2,1 et 2,2

## <a name="additional-resources"></a>Ressources supplémentaires

* [Comment utiliser la bibliothèque](system-text-json-how-to.md)
* [Migration à partir deNewtonsoft.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Comment écrire des convertisseurs](system-text-json-converters-how-to.md)
* [System.Text.Jsoncode source](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json)
* [System.Text.JsonRéférence d’API](xref:System.Text.Json)
* [System.Text.Json. Référence de l’API de sérialisation](xref:System.Text.Json.Serialization)
<!-- * [Roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md)-->
