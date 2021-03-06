---
title: Sérialisation de base, exemple de technologie
description: Cet exemple illustre la capacité du CLR à sérialiser un graphique d’objets en mémoire dans un flux. Cet exemple peut utiliser SoapFormatter ou BinaryFormatter.
ms.date: 03/30/2017
ms.assetid: 9d824e16-08d1-4a36-bc7f-2388c1f75f34
ms.openlocfilehash: 3f2273e6afb3a72f9734444ffe92d30871fb762b
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2020
ms.locfileid: "84276567"
---
# <a name="basic-serialization-technology-sample"></a>Sérialisation de base, exemple de technologie

[Charger l’exemple](https://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Runtime%20Serialization/Basic.zip.exe)

Cet exemple montre la capacité du Common Language Runtime à sérialiser un graphique d'objets en mémoire dans un flux. Cet exemple peut utiliser <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> ou <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> pour la sérialisation. Une liste liée, remplie de données, est sérialisée ou désérialisée dans un flux de fichiers ou à partir de celui-ci. Dans les deux cas, la liste est affichée afin que vous puissiez consulter les résultats. Il s'agit d'une liste liée de type `LinkedList`, un type défini par cet exemple.

Pour plus d'informations sur la sérialisation, consultez les commentaires inclus dans les fichiers de code source et dans les fichiers build-proj.

### <a name="to-build-the-sample-using-the-command-prompt"></a>Pour générer l'exemple à partir de l'invite de commandes

1. Accédez à l'un des sous-répertoires spécifiques aux différents langages dans le répertoire Technologies\Serialization\Runtime Serialization\Basic, à l'aide de l'invite de commandes.

2. Tapez **msbuild SerializationCS.sln**, **msbuild SerializationJSL.sln** ou **msbuild SerializationVB.sln** sur la ligne de commande, selon votre choix de langage de programmation.

### <a name="to-build-the-sample-using-visual-studio"></a>Pour générer l'exemple à l'aide de Visual Studio

1. Ouvrez l’Explorateur de fichiers et accédez à l’un des sous-répertoires spécifiques au langage de l’exemple.

2. Double-cliquez sur l'icône du fichier SerializationCS.sln, SerializationJSL.sln ou SerializationVB.sln, selon votre choix de langage de programmation, pour ouvrir le fichier dans Visual Studio.

3. Dans le menu **Générer**, sélectionnez **Générer la solution**.

 L'exemple d'application est généré dans le sous-répertoire \bin ou \bin\Debug par défaut.

### <a name="to-run-the-sample"></a>Exécution de l'exemple

1. Accédez au répertoire qui contient le fichier exécutable créé.

2. Tapez **Serialization.exe**, ainsi que les valeurs de paramètres souhaitées, sur la ligne de commande.

  > [!NOTE]
  > Cet exemple génère une application console. Vous devez la lancer à l'aide de l'invite de commandes pour pouvoir afficher sa sortie.

## <a name="remarks"></a>Remarques

L'exemple d'application accepte des paramètres de ligne de commande indiquant le test à exécuter. Pour sérialiser une liste de 10 nœuds dans un fichier nommé **Test.xml** à l’aide du formateur SOAP, utilisez les paramètres **sx Test.xml 10**.

Par exemple :

```console
Serialize.exe -sx Test.xml 10
```

Pour désérialiser le fichier **Test.xml** de l’exemple précédent, utilisez les paramètres **dx Test.xml**.

Par exemple :

```console
Serialize.exe -dx Test.xml
```

Dans les deux exemples précités, la lettre "x" dans le commutateur de ligne de commande indique que vous souhaitez effectuer une sérialisation SOAP XML. Vous pouvez utiliser à la place la lettre "b" pour effectuer une sérialisation binaire. Si vous souhaitez effectuer une sérialisation avec un très grand nombre de nœuds, il peut être intéressant de rediriger la sortie de console vers un fichier.

Par exemple :

```console
Serialize.exe -sb Test.bin 10000 >somefile.txt
```

Les éléments de la liste suivante décrivent brièvement les classes et les technologies utilisées par cet exemple.

- Sérialisation du runtime

  - <xref:System.Runtime.Serialization.IFormatter>Utilisé pour faire référence à un <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> objet ou <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> .

  - <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>Utilisé pour sérialiser une liste liée dans un flux au format binaire. Le formateur binaire utilise un format reconnu uniquement par le type <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>. Toutefois, les données sont concises.

  - <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>Utilisé pour sérialiser une liste liée dans un flux au format SOAP. SOAP est un format standard.

- E/S de flux

  - <xref:System.IO.Stream> Utilisé pour effectuer la sérialisation et la désérialisation. Le flux spécifique utilisé dans cet exemple est de type <xref:System.IO.FileStream>. Toutefois, la sérialisation peut être utilisée avec n'importe quel type dérivé de <xref:System.IO.Stream>.

  - <xref:System.IO.File> Utilisé pour créer des objets <xref:System.IO.FileStream> afin de lire et de créer des fichiers sur le disque.

  - <xref:System.IO.FileStream> Utilisé pour sérialiser et désérialiser des listes liées.

## <a name="see-also"></a>Voir aussi

- <xref:System.IO>
- <xref:System.IO.File>
- <xref:System.IO.FileStream>
- <xref:System.IO.Stream>
- <xref:System.Random>
- <xref:System.Runtime.Serialization>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>
- <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>
- <xref:System.Runtime.Serialization.IFormatter>
- <xref:System.SerializableAttribute>
- <xref:System.Xml.Serialization>
- [Sérialisation de base](basic-serialization.md)
- [Sérialisation binaire](binary-serialization.md)
- [Contrôle de la sérialisation XML à l’aide d’attributs](controlling-xml-serialization-using-attributes.md)
- [Introduction à la sérialisation XML](introducing-xml-serialization.md)
- [Sérialisation](index.md)
- [Sérialisation XML et SOAP](xml-and-soap-serialization.md)
