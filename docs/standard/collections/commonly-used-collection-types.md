---
title: Types de collections couramment utilisés
description: Découvrez les types de collections couramment utilisés dans .NET, tels que les tables de hachage, les files d’attente, les piles, les conteneurs, les dictionnaires et les listes.
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- collections [.NET Framework], generic
- objects [.NET Framework], grouping in collections
- generics [.NET Framework], collections
- IList interface, grouping data in collections
- IDictionary interface, grouping data in collections
- grouping data in collections, generic collection types
- Collections classes
- generic collections
ms.assetid: f5d4c6a4-0d7b-4944-a9fb-3b12d9ebfd55
ms.openlocfilehash: d0f2abc71524408c2bd2fa35a1a2dde0e664d273
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600839"
---
# <a name="commonly-used-collection-types"></a>Types de collections couramment utilisés
Les types de collections sont des variations courantes des collections de données, telles que les tables de hachage, les files d’attente, les piles, les conteneurs, les dictionnaires et les listes.  
  
 Les collections sont basées sur l'interface <xref:System.Collections.ICollection>, <xref:System.Collections.IList> ou <xref:System.Collections.IDictionary>, ou sur leurs équivalents génériques. Les interfaces <xref:System.Collections.IList> et <xref:System.Collections.IDictionary> sont toutes deux dérivées de l'interface <xref:System.Collections.ICollection>. Par conséquent, toutes les collections sont basées directement ou indirectement sur l'interface <xref:System.Collections.ICollection>. Dans les collections basées sur l' <xref:System.Collections.IList> interface (telles que <xref:System.Array> , <xref:System.Collections.ArrayList> ou <xref:System.Collections.Generic.List%601> ) ou directement sur l' <xref:System.Collections.ICollection> interface (telles que,,, <xref:System.Collections.Queue> <xref:System.Collections.Concurrent.ConcurrentQueue%601> <xref:System.Collections.Stack> <xref:System.Collections.Concurrent.ConcurrentStack%601> ou <xref:System.Collections.Generic.LinkedList%601> ), chaque élément contient uniquement une valeur. Dans les collections basées sur l'interface <xref:System.Collections.IDictionary> (telles que les classes <xref:System.Collections.Hashtable> et <xref:System.Collections.SortedList>, les classes génériques <xref:System.Collections.Generic.Dictionary%602> et <xref:System.Collections.Generic.SortedList%602>) ou sur les classes <xref:System.Collections.Concurrent.ConcurrentDictionary%602>, chaque élément contient à la fois une clé et une valeur.  La classe <xref:System.Collections.ObjectModel.KeyedCollection%602> est unique, car il s'agit d'une liste de valeurs auxquelles sont incorporées des clés. Son comportement est donc celui d'une liste ou d'un dictionnaire.  
  
 Les collections génériques conviennent le mieux au typage fort. Toutefois, si votre langage ne prend pas en charge les génériques, l'espace de noms <xref:System.Collections> contient des collections de base, telles que <xref:System.Collections.CollectionBase>, <xref:System.Collections.ReadOnlyCollectionBase> et <xref:System.Collections.DictionaryBase>, qui sont des classes de base abstraites pouvant être étendues pour créer des classes de collection fortement typées. Quand un accès efficace à une collection multithread est requis, utilisez les collections génériques de l'espace de noms <xref:System.Collections.Concurrent>.  
  
 Les collections peuvent varier, en fonction de la façon dont les éléments sont stockés et triés, ainsi que de la façon dont les recherches et les comparaisons sont effectuées. La classe <xref:System.Collections.Queue> et la classe générique <xref:System.Collections.Generic.Queue%601> fournissent des listes premier entré, premier sorti (FIFO), alors que la classe <xref:System.Collections.Stack> et la classe générique <xref:System.Collections.Generic.Stack%601> fournissent des listes dernier entré, premier sorti (LIFO). La classe <xref:System.Collections.SortedList> et la classe générique <xref:System.Collections.Generic.SortedList%602> fournissent des versions triées de la classe <xref:System.Collections.Hashtable> et de la classe générique <xref:System.Collections.Generic.Dictionary%602>. Les éléments d'un <xref:System.Collections.Hashtable> ou d'un <xref:System.Collections.Generic.Dictionary%602> sont accessibles uniquement via la clé de l'élément, alors que les éléments d'un <xref:System.Collections.SortedList> ou d'un <xref:System.Collections.ObjectModel.KeyedCollection%602> sont accessibles aussi bien via la clé que l'index de l'élément. Les index de toutes les collections sont de base zéro, à l'exception de <xref:System.Array>, qui acceptent les tableaux qui ne sont pas de base zéro.  
  
 La fonctionnalité LINQ to Objects permet d'utiliser des requêtes LINQ pour accéder aux objets en mémoire tant que le type d'objet implémente l'interface <xref:System.Collections.IEnumerable> ou <xref:System.Collections.Generic.IEnumerable%601>. Les requêtes LINQ fournissent un modèle commun pour accéder aux données ; sont généralement plus concises et lisibles que les boucles standard, `foreach` et fournissent des fonctionnalités de filtrage, de classement et de regroupement. Les requêtes LINQ peuvent également améliorer les performances. Pour plus d’informations, consultez [LINQ to Objects (C#)](../../csharp/programming-guide/concepts/linq/linq-to-objects.md), [LINQ to Objects (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md) et [Parallel LINQ (PLINQ)](../parallel-programming/introduction-to-plinq.md).  
  
## <a name="related-topics"></a>Rubriques connexes  
  
|Intitulé|Description|  
|-----------|-----------------|  
|[Collections et structures de données](index.md)|Présente les différents types de collection disponibles dans le .NET Framework, notamment les piles, les files d’attente, les listes, les tableaux et les dictionnaires.|  
|[Types de collections Hashtable et Dictionary](hashtable-and-dictionary-collection-types.md)|Décrit les fonctionnalités des types de dictionnaires basés sur le hachage génériques et non génériques.|  
|[Types de collections triées](sorted-collection-types.md)|Décrit les classes qui fournissent une fonctionnalité de tri pour les listes et les ensembles.|  
|[Génériques](../generics/index.md)|Décrit la fonctionnalité génériques, notamment les collections, délégués et interfaces génériques fournis par le .NET Framework. Fournit des liens vers de la documentation sur les fonctionnalités pour C#, Visual Basic et Visual C++, ainsi que vers des technologies de prise en charge comme la réflexion.|  
  
## <a name="reference"></a>Informations de référence  
 <xref:System.Collections?displayProperty=nameWithType>  
  
 <xref:System.Collections.Generic?displayProperty=nameWithType>  
  
 <xref:System.Collections.ICollection?displayProperty=nameWithType>  
  
 <xref:System.Collections.Generic.ICollection%601?displayProperty=nameWithType>  
  
 <xref:System.Collections.IList?displayProperty=nameWithType>  
  
 <xref:System.Collections.Generic.IList%601?displayProperty=nameWithType>  
  
 <xref:System.Collections.IDictionary?displayProperty=nameWithType>  
  
 <xref:System.Collections.Generic.IDictionary%602?displayProperty=nameWithType>
