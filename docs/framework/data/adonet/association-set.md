---
title: jeu d'associations
ms.date: 03/30/2017
ms.assetid: a65247b6-ce59-44ea-974c-14ae20a7995f
ms.openlocfilehash: e279322f9e950cd4359db8c6dce39bfc46d188f6
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73732375"
---
# <a name="association-set"></a>jeu d'associations
Un *ensemble d’associations* est un conteneur logique pour les instances d' [Association](association-type.md) du même type. Un ensemble d'associations n'est pas une construction de modélisation des données ; autrement dit, il ne décrit ni la structure de données ni les relations. Au lieu de cela, un ensemble d'associations fournit une construction pour un environnement d'hébergement ou de stockage (tel que le Common Language Runtime ou une base de données SQL Server) pour regrouper des instances d'association afin qu'elles puissent être mappées à un magasin de données.  
  
 Un ensemble d’associations est défini dans un [conteneur d’entités](entity-container.md), qui est un regroupement logique de jeux d' [entités](entity-set.md) et d’ensembles d’associations.  
  
 Une définition d'ensemble d'associations contient les informations suivantes :  
  
- Nom de l'ensemble d'associations. (Requis)  
  
- Association dont l'ensemble d'associations contient des instances. (Requis)  
  
- Deux [terminaisons d’ensemble d’associations](association-set-end.md).  
  
## <a name="example"></a>Exemple  
 Le diagramme suivant montre un modèle conceptuel avec deux associations : `PublishedBy` et `WrittenBy`. Bien que les informations sur les ensembles d'associations ne soient pas transmises au diagramme, le diagramme suivant montre un exemple d'ensembles d'associations et de jeux d'entités basés sur ce modèle.  
  
 ![Exemple de modèle avec trois types d’entité](./media/association-set/example-model-three-entity-types.gif)  
  
 L'exemple suivant montre un ensemble d'associations (`PublishedBy`) et deux jeux d'entités (`Books` et `Publishers`) basés sur le modèle conceptuel présenté ci-dessus. Bi dans le jeu d’entités `Books` représente une instance du type d’entité `Book` au moment de l’exécution. De même, PJ représente une instance `Publisher` dans le jeu d’entités `Publishers`. BiPj représente une instance de l’Association `PublishedBy` dans l’ensemble d’associations `PublishedBy`.  
  
 ![Capture d’écran montrant un exemple de jeu.](./media/association-set/sets-example-association.gif)  
  
 Le [Entity Framework ADO.net](./ef/index.md) utilise un langage spécifique à un domaine (DSL) appelé Conceptual Schema Definition Language ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) pour définir des modèles conceptuels. Le CSDL suivant définit un conteneur d'entités avec un ensemble d'associations pour chaque association dans le diagramme ci-dessus. Notez que le nom et l'association pour chaque ensemble d'associations sont définis à l'aide d'attributs XML.  
  
 [!code-xml[EDM_Example_Model#EntityContainerExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entitycontainerexample)]  
  
 Il est possible de définir plusieurs ensembles d’associations par Association, tant que deux ensembles d’associations ne partagent pas une [terminaison d’ensemble d’associations](association-set-end.md). Le CSDL suivant définit un conteneur d'entités avec deux ensembles d'associations pour l'association `WrittenBy`. Notez que plusieurs jeux d'entités ont été définis pour les types d'entité `Book` et `Author`, et qu'aucun ensemble d'associations ne partage une terminaison d'ensemble d'associations.  
  
 [!code-xml[EDM_Example_Model#MultipleAssociationSets](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books3.edmx#multipleassociationsets)]  
  
## <a name="see-also"></a>Voir aussi

- [Concepts clés d’Entity Data Model](entity-data-model-key-concepts.md)
- [Entity Data Model](entity-data-model.md)
- [propriété de clé étrangère](foreign-key-property.md)
