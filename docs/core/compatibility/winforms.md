---
title: Modifications avec rupture Windows Forms
description: Répertorie les dernières modifications apportées à Windows Forms pour .NET Core.
ms.date: 01/08/2020
ms.openlocfilehash: bd87e438ecf9930bfcd5377f9a3799d5f3693f49
ms.sourcegitcommit: 1cbd77da54405ea7dba343ac0334fb03237d25d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84702466"
---
# <a name="breaking-changes-in-windows-forms"></a>Modifications avec rupture dans Windows Forms

La prise en charge de Windows Forms a été ajoutée à .NET Core dans la version 3,0. Cet article répertorie les modifications avec rupture pour Windows Forms par la version de .NET Core dans laquelle elles ont été introduites. Si vous effectuez la mise à niveau d’une application Windows Forms à partir d' .NET Framework ou d’une version antérieure de .NET Core (3,0 ou version ultérieure), cet article s’applique à vous.

Les modifications avec rupture suivantes sont documentées sur cette page :

| Modification avec rupture | Version introduite |
| - | :-: |
| [Contrôles de barre d’État supprimés](#removed-status-bar-controls) | 5.0 |
| [Les méthodes WinForms lèvent désormais ArgumentException](#winforms-methods-now-throw-argumentexception) | 5.0 |
| [Les méthodes WinForms lèvent désormais ArgumentNullException](#winforms-methods-now-throw-argumentnullexception) | 5.0 |
| [Les propriétés WinForms lèvent désormais ArgumentOutOfRangeException](#winforms-properties-now-throw-argumentoutofrangeexception) | 5.0 |
| [Contrôles supprimés](#removed-controls) | 3.1 |
| [Événement CellFormatting non déclenché si l’info-bulle est affichée](#cellformatting-event-not-raised-if-tooltip-is-shown) | 3.1 |
| [Control. DefaultFont remplacé par Segoe UI 9 PT](#default-control-font-changed-to-segoe-ui-9-pt) | 3.0 |
| [Modernisation du FolderBrowserDialog](#modernization-of-the-folderbrowserdialog) | 3.0 |
| [SerializableAttribute supprimé de certains types de Windows Forms](#serializableattribute-removed-from-some-windows-forms-types) | 3.0 |
| [Commutateur de compatibilité AllowUpdateChildControlIndexForTabControls non pris en charge](#allowupdatechildcontrolindexfortabcontrols-compatibility-switch-not-supported) | 3.0 |
| [Commutateur de compatibilité DomainUpDown. UseLegacyScrolling non pris en charge](#domainupdownuselegacyscrolling-compatibility-switch-not-supported) | 3.0 |
| [Commutateur de compatibilité DoNotLoadLatestRichEditControl non pris en charge](#donotloadlatestricheditcontrol-compatibility-switch-not-supported) | 3.0 |
| [Commutateur de compatibilité DoNotSupportSelectAllShortcutInMultilineTextBox non pris en charge](#donotsupportselectallshortcutinmultilinetextbox-compatibility-switch-not-supported) | 3.0 |
| [Commutateur de compatibilité DontSupportReentrantFilterMessage non pris en charge](#dontsupportreentrantfiltermessage-compatibility-switch-not-supported) | 3.0 |
| [Commutateur de compatibilité EnableVisualStyleValidation non pris en charge](#enablevisualstylevalidation-compatibility-switch-not-supported) | 3.0 |
| [Commutateur de compatibilité UseLegacyContextMenuStripSourceControlValue non pris en charge](#uselegacycontextmenustripsourcecontrolvalue-compatibility-switch-not-supported) | 3.0 |
| [Commutateur de compatibilité UseLegacyImages non pris en charge](#uselegacyimages-compatibility-switch-not-supported) | 3.0 |
| [Changement d’accès pour AccessibleObject. RuntimeIDFirstItem](#change-of-access-for-accessibleobjectruntimeidfirstitem) | 3.0 |
| [API dupliquées supprimées de Windows Forms](#duplicated-apis-removed-from-windows-forms) | 3.0 |

## <a name="net-50"></a>.NET 5,0

[!INCLUDE [winforms-deprecated-controls](../../../includes/core-changes/windowsforms/5.0/winforms-deprecated-controls.md)]

***

[!INCLUDE [invalid-args-cause-argumentexception](../../../includes/core-changes/windowsforms/5.0/invalid-args-cause-argumentexception.md)]

***

[!INCLUDE [null-args-cause-argumentnullexception](../../../includes/core-changes/windowsforms/5.0/null-args-cause-argumentnullexception.md)]

***

[!INCLUDE [invalid-args-cause-argumentoutofrangeexception](../../../includes/core-changes/windowsforms/5.0/invalid-args-cause-argumentoutofrangeexception.md)]

***

## <a name="net-core-31"></a>.NET Core 3.1

[!INCLUDE[Removed controls](~/includes/core-changes/windowsforms/3.1/remove-controls-3.1.md)]

***

[!INCLUDE[CellFormatting event](~/includes/core-changes/windowsforms/3.1/cellformatting-event-not-raised.md)]

***

## <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[Control.DefaultFont changed to Segoe UI 9pt](~/includes/core-changes/windowsforms/3.0/control-defaultfont-changed.md)]

***

[!INCLUDE[Modernization of the FolderBrowserDialog](~/includes/core-changes/windowsforms/3.0/modernized-folderbrowserdialog.md)]

***

[!INCLUDE[SerializableAttribute removed from some Windows Forms types](~/includes/core-changes/windowsforms/3.0/remove-serializationattribute.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.AllowUpdateChildControlIndexForTabControls compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-allowupdatechildcontrolindexfortabcontrols.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.DomainUpDown.UseLegacyScrolling compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyscrolling.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.DoNotLoadLatestRichEditControl compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotloadlatestricheditcontrol.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotsupportselectallshortcutinmultilinetextbox.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.DontSupportReentrantFilterMessage compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-dontsupportreentrantfiltermessage.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.EnableVisualStyleValidation compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-enablevisualstylevalidation.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.UseLegacyContextMenuStripSourceControlValue compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacycontextmenustripsourcecontrolvalue.md)]

***

[!INCLUDE[Switch.System.Windows.Forms.UseLegacyImages compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyimages.md)]

***

[!INCLUDE[Change of access for AccessibleObject.RuntimeIDFirstItem](~/includes/core-changes/windowsforms/3.0/changed-access-for-runtimeidfirstitem.md)]

***

[!INCLUDE[Duplicated APIs removed from Windows Forms](~/includes/core-changes/windowsforms/3.0/remove-duplicated-apis.md)]

***

## <a name="see-also"></a>Voir aussi

- [Portage d’une application Windows Forms vers .NET Core](../porting/winforms.md)
