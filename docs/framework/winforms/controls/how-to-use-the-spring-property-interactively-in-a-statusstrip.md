---
title: 'Procédure : utiliser la propriété Spring dans un StatusStrip de manière interactive'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- StatusStrip control [Windows Forms]
- ToolStrip control [Windows Forms]
- status bars [Windows Forms], examples
- Spring property [Windows Forms]
ms.assetid: 18bde842-a93c-48dd-9db3-15738a1775ce
ms.openlocfilehash: 8750c48d08161260a1dba6ab69098980f25a5d55
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65589647"
---
# <a name="how-to-use-the-spring-property-interactively-in-a-statusstrip"></a>Procédure : utiliser la propriété Spring dans un StatusStrip de manière interactive
Vous pouvez utiliser la propriété <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> pour positionner un contrôle <xref:System.Windows.Forms.ToolStripStatusLabel> dans un contrôle <xref:System.Windows.Forms.StatusStrip>. La propriété <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> détermine si le contrôle <xref:System.Windows.Forms.ToolStripStatusLabel> remplit automatiquement l'espace disponible sur le contrôle <xref:System.Windows.Forms.StatusStrip>.  
  
## <a name="example"></a>Exemple  
 L'exemple de code suivant montre comment utiliser la propriété <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> pour positionner un contrôle <xref:System.Windows.Forms.ToolStripStatusLabel> dans un contrôle <xref:System.Windows.Forms.StatusStrip>. Le gestionnaire d'événements <xref:System.Windows.Forms.ToolStripItem.Click> exécute une opération « ou exclusif » (XOR) pour faire basculer la valeur de la propriété <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A>.  
  
 Pour utiliser cet exemple de code, compilez et exécutez l’application, puis cliquez sur **Middle (Spring)** sur le <xref:System.Windows.Forms.StatusStrip> contrôle pour faire basculer la valeur de la <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> propriété.  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.Misc#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.Misc#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#1)]  
[!code-csharp[System.Windows.Forms.ToolStrip.Misc#50](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#50)]
[!code-vb[System.Windows.Forms.ToolStrip.Misc#50](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#50)]  
  
## <a name="compiling-the-code"></a>Compilation du code  
 Cet exemple nécessite :  
  
- des références aux assemblys System.Design, System.Drawing et System.Windows.Forms.  
  
## <a name="see-also"></a>Voir aussi

- <xref:System.Windows.Forms.ToolStripStatusLabel>
- <xref:System.Windows.Forms.StatusStrip>
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.ToolStripItem>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [Contrôle ToolStrip](toolstrip-control-windows-forms.md)
