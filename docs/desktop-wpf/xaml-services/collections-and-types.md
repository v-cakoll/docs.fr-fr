---
title: Collections et types de collections pour XAML
ms.date: 03/30/2017
ms.assetid: 58f8e7c6-9a41-4f25-8551-c042f1315baa
ms.openlocfilehash: 2ec58026c605df31489c8aab4c4cc714dab11474
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2020
ms.locfileid: "82071296"
---
# <a name="collections-and-collection-types-for-xaml"></a>Collections et types de collecte pour XAML

Cet article décrit comment définir les propriétés des types qui sont destinés à soutenir une collection, et à soutenir la syntaxe XAML pour instantanéiser les éléments de collecte comme des enfants élément d’un élément objet parent ou élément de propriété.

## <a name="xaml-collection-concepts"></a>XAML Collection Concepts

Conceptuellement, toute relation dans XAML où il y a plusieurs articles d’enfant dans le cadre d’un élément d’objet XAML ou d’un élément de propriété XAML doit être mise en œuvre comme collection. Cette collection doit être associée à une propriété XAML particulière du type XAML qui est le parent dans cette relation. La propriété doit être une collection parce qu’un processeur XAML s’attend à attribuer chaque article en majoration pour être un élément nouvellement ajouté de la propriété de collecte de soutien.

Au niveau de la langue XAML, les exigences exactes du support de collecte ne sont pas entièrement définies. Le concept selon lequel une collection peut être soit une liste, soit un dictionnaire (mais pas les deux) est défini au niveau de la langue XAML, mais que les types de support représentent des listes ou des dictionnaires n’est pas défini par la langue XAML.

Dans .NET XAML Services, le concept de support de collecte XAML est plus clairement défini en termes de types de support .NET. Plus précisément, le support XAML pour les collections est basé sur plusieurs concepts .NET et API qui sont utilisés pour les listes et les dictionnaires en général .NET programmation.

1. L’interface <xref:System.Collections.IList> indique une collection de liste.

2. L’interface <xref:System.Collections.IDictionary> indique une collection de dictionnaires.

3. <xref:System.Array>représente un tableau, et <xref:System.Collections.IList> un tableau prend en charge les méthodes.

Dans chacun de ces concepts de collecte, un processeur .NET `Add` XAML Services XAML s’attend à appeler la méthode sur un cas spécifique du type de propriété de collecte. Ou, dans un scénario de sérialisation, un processeur XAML produit des instances discrètes de type XAML pour chaque élément trouvé dans la liste, le dictionnaire ou le tableau en fonction du concept spécifique de chaque collection d'" Articles ". Ces éléments <xref:System.Collections.IList.Item%2A?displayProperty=nameWithType>sont les: ; <xref:System.Collections.IDictionary.Item%2A?displayProperty=nameWithType>; <xref:System.Array.System%23Collections%23IList%23Item%2A?displayProperty=nameWithType> l’explicite <xref:System.Array>pour .

## <a name="generic-collections"></a>Collections génériques

Les collections génériques peuvent être utiles pour la programmation générale .NET, et peuvent également être utilisées pour les propriétés de collecte XAML. Cependant, les interfaces <xref:System.Collections.Generic.IList%601> génériques et <xref:System.Collections.Generic.IDictionary%602> ne sont pas identifiés par les processeurs XAML .NET XAML Services comme étant équivalents à la non-générique <xref:System.Collections.IList> ou <xref:System.Collections.IDictionary>. Plutôt que de mettre en œuvre les interfaces, une <xref:System.Collections.Generic.List%601> approche <xref:System.Collections.Generic.Dictionary%602>recommandée pour les types de propriété de collecte générique est de dériver des classes ou . Ces classes implémentent les interfaces non génériques et incluent ainsi le support attendu pour les collections XAML dans la mise en œuvre de base.

## <a name="read-only-collections-and-initialization-logic"></a>Lire-Seulement Collections et Initialisation Logique

Dans la programmation .NET, il est un modèle de conception commun pour faire n’importe quelle propriété qui détient une valeur d’une collection comme une collection de lecture seulement. Ce modèle permet à l’instance qui possède la propriété de collecte de mieux contrôler ce qui arrive à la collection. Plus précisément, le modèle empêche le remplacement accidentel de l’ensemble de la collection préexistante en fixant la propriété. Dans ce modèle, tout accès à la collection par les appelants devrait plutôt être fait en appelant des <xref:System.Collections.IList>méthodes ou des propriétés telles que supportées par le type de collection et / ou les interfaces de collecte pertinentes telles que .

L’utilisation de ce modèle implique que toute classe qui expose une propriété de collecte de lecture seulement doit d’abord initialiser cette propriété pour tenir une collection vide. Typiquement, l’initialisation est effectuée dans le cadre du comportement de construction pour la classe. Pour être utile pour XAML, il est important que cette logique soit toujours référencée par le constructeur sans paramètres, parce que XAML appelle généralement le constructeur sans paramètres avant de traiter les propriétés (propriétés de collecte ou autrement).

## <a name="xaml-type-system-support-and-collections"></a>Support et collections XAML Type System

Au-delà de la mécanique de base de l’analyse de XAML et le peuplement ou la sérialisation des propriétés de collection, le système de type XAML tel qu’il est mis en œuvre dans .NET XAML Services comprend plusieurs caractéristiques de conception qui se rapportent aux collections dans XAML.

1. <xref:System.Xaml.XamlType.IsCollection%2A>retourne vrai si le type XAML est soutenu par un type qui fournit le support de collecte XAML.

2. <xref:System.Xaml.XamlType.IsDictionary%2A>et <xref:System.Xaml.XamlType.IsArray%2A> peut identifier en outre le mode de collecte que prend en charge le type XAML. Pour les processeurs XAML personnalisés qui sont basés sur .NET XAML <xref:System.Xaml.XamlWriter> Services et le système de type XAML, mais pas basé sur les implémentations existantes, sachant quel mode de collecte est utilisé pourrait être nécessaire afin de savoir quelle méthode invoquer pour le traitement de collecte.

3. Chacune des valeurs de propriété précédentes <xref:System.Xaml.XamlType.LookupCollectionKind%2A> est potentiellement influencée par des remplacements de sur un type XAML.
