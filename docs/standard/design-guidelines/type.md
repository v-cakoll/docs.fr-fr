---
title: Instructions de conception de types
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- type design guidelines
- type design guidelines, about type design guidelines
- class library design guidelines [.NET Framework], type design guidelines
- types [.NET Framework], design guidelines
ms.assetid: 6b49314e-8bba-43ea-97ca-4e0255812f95
ms.openlocfilehash: 17bd300277a039818a3d563c8f2d5f99eb2fc68d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289562"
---
# <a name="type-design-guidelines"></a>Instructions de conception de types
Du point de vue du CLR, il n’existe que deux catégories de types : les types référence et les types valeur, mais pour les besoins d’une discussion sur la conception de l’infrastructure, nous dipartissons les types en groupes plus logiques, chacun avec ses propres règles de conception spécifiques.

 Les classes sont le cas général de types référence. Ils constituent la majeure partie des types dans la majorité des infrastructures. Les classes ont eu la popularité de l’ensemble complet des fonctionnalités orientées objet qu’elles prennent en charge et de leur applicabilité générale. Les classes de base et les classes abstraites sont des groupes logiques spéciaux liés à l’extensibilité.

 Les interfaces sont des types qui peuvent être implémentés par les types référence et les types valeur. Ils peuvent ainsi servir de racines de hiérarchies polymorphes de types référence et de types valeur. En outre, les interfaces peuvent être utilisées pour simuler plusieurs héritages, ce qui n’est pas pris en charge en mode natif par le CLR.

 Les structs sont le cas général des types valeur et doivent être réservés pour les petits types simples, similaires aux primitives de langage.

 Les enums sont un cas spécial de types valeur utilisés pour définir des jeux de valeurs courts, tels que les jours de la semaine, les couleurs de la console, etc.

 Les classes statiques sont des types destinés à être des conteneurs pour des membres statiques. Ils sont généralement utilisés pour fournir des raccourcis vers d’autres opérations.

 Les délégués, les exceptions, les attributs, les tableaux et les collections sont tous des cas spéciaux de types référence destinés à des utilisations spécifiques, et les recommandations relatives à leur conception et à leur utilisation sont décrites ailleurs dans ce document.

 ✔️ Assurez-vous que chaque type est un ensemble bien défini de membres associés, et pas seulement une collection aléatoire de fonctionnalités non liées.

## <a name="in-this-section"></a>Dans cette section
 [Choix entre une classe et une structure](choosing-between-class-and-struct.md) [abstraite conception](abstract-class.md) d’une classe [statique](static-class.md) conception d' [interface](interface.md) conception d’une [structure](struct.md) [enum](enum.md) conception des [types imbriqués](nested-types.md) *parties © 2005, 2009 Microsoft Corporation. Tous droits réservés.*

 *Réimprimé avec l’autorisation de Pearson Education, Inc. et extrait de [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) par Krzysztof Cwalina et Brad Abrams, publié le 22 octobre 2008 par Addison-Wesley Professional dans le cadre de la série sur le développement Microsoft Windows.*

## <a name="see-also"></a>Voir aussi

- [Directives de conception d’infrastructure](index.md)
