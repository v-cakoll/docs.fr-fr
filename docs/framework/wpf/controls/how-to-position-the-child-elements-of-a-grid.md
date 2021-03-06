---
title: "Comment : positionner les éléments enfants d'une grille"
description: Découvrez comment utiliser les méthodes d’obtention et de définition définies sur une grille Windows Presentation Foundation pour positionner des éléments enfants.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Grid control [WPF], positioning child elements
ms.assetid: 27b3ba9b-ad32-44e2-bcab-a79d573a463c
ms.openlocfilehash: 926d223097dd21dd0292c9523903b4be8aba8ba9
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2020
ms.locfileid: "87167390"
---
# <a name="how-to-position-the-child-elements-of-a-grid"></a>Comment : positionner les éléments enfants d'une grille
Cet exemple montre comment utiliser les méthodes d’obtention et de définition définies sur <xref:System.Windows.Controls.Grid> pour positionner des éléments enfants.  
  
## <a name="example"></a>Exemple  
 L’exemple suivant définit un <xref:System.Windows.Controls.Grid> élément parent ( `grid1` ) qui comporte trois colonnes et trois lignes. Un <xref:System.Windows.Shapes.Rectangle> élément enfant ( `rect1` ) est ajouté à la <xref:System.Windows.Controls.Grid> position de colonne zéro, à la position de ligne zéro. <xref:System.Windows.Controls.Button>les éléments représentent des méthodes qui peuvent être appelées pour repositionner l' <xref:System.Windows.Shapes.Rectangle> élément dans le <xref:System.Windows.Controls.Grid> . Quand un utilisateur clique sur un bouton, la méthode associée est activée.  
  
 [!code-xaml[gridGetSetMethods](~/samples/snippets/csharp/VS_Snippets_Wpf/gridGetSetMethods/CSharp/Window1.xaml)]  
  
 L’exemple de code-behind suivant gère les méthodes que <xref:System.Windows.Controls.Primitives.ButtonBase.Click> déclenchent les événements de bouton. L’exemple écrit ces appels de méthode aux <xref:System.Windows.Controls.TextBlock> éléments qui utilisent des méthodes d’extraction associées pour générer en sortie les nouvelles valeurs de propriété sous forme de chaînes.  
  
 [!code-csharp[gridGetSetMethods#2](~/samples/snippets/csharp/VS_Snippets_Wpf/gridGetSetMethods/CSharp/Window1.xaml.cs#2)]
 [!code-vb[gridGetSetMethods#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/gridGetSetMethods/VisualBasic/Window1.xaml.vb#2)]  
 Voici le résultat final !

 ![une capture d’écran illustre une interface utilisateur WPF avec deux colonnes, la partie droite a une grille 3 x 3 et la gauche a des boutons pour déplacer un rectangle de couleur entre les colonnes et les lignes de la grille](././media/grid-methods-sample.png)
  
## <a name="see-also"></a>Voir aussi

- <xref:System.Windows.Controls.Grid>
- [Vue d'ensemble de Panel](panels-overview.md)
