---
title: 'Procédure : créer un formulaire MDI avec la fusion des menus et des contrôles ToolStrip'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- toolbars [Windows Forms]
- ToolStripPanel control [Windows Forms]
- ToolStrip control [Windows Forms]
- MenuStrip control [Windows Forms]
ms.assetid: 64992ed9-44af-4baf-b45f-863e6ab35711
ms.openlocfilehash: 0edcc27968c55908cda0e881ed66f83323316711
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591308"
---
# <a name="how-to-create-an-mdi-form-with-menu-merging-and-toolstrip-controls"></a>Procédure : créer un formulaire MDI avec la fusion des menus et des contrôles ToolStrip
L'espace de noms <xref:System.Windows.Forms?displayProperty=nameWithType> prend en charge plusieurs applications MDI (Multiple Document Interface) et le contrôle <xref:System.Windows.Forms.MenuStrip> prend en charge la fusion de menus. Les formulaires MDI peuvent également contenir des contrôles <xref:System.Windows.Forms.ToolStrip>.  
  
 Il existe une prise en charge étendue pour cette fonctionnalité dans Visual Studio.  
  
 Consultez également [procédure pas à pas : Création d’un formulaire MDI avec la fusion de menus et des contrôles ToolStrip](walkthrough-creating-an-mdi-form-with-menu-merging-and-toolstrip-controls.md).  
  
## <a name="example"></a>Exemple  
 L'exemple de code suivant montre comment utiliser des contrôles <xref:System.Windows.Forms.ToolStripPanel> avec un formulaire MDI. Le formulaire prend également en charge la fusion de menus avec les menus enfants.  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.MdiForm#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.MdiForm/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.MdiForm#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.MdiForm/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>Compilation du code  
 Cet exemple de code nécessite :  
  
- Références aux assemblys System.Drawing et System.Windows.Forms.  
  
## <a name="see-also"></a>Voir aussi

- [Contrôle ToolStrip](toolstrip-control-windows-forms.md)
