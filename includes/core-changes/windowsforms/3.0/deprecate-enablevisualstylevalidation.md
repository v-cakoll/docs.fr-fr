---
ms.openlocfilehash: 84b6bfc32f5a73597b227098e5aee1e3450cf85b
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74644011"
---
### <a name="switchsystemwindowsformsenablevisualstylevalidation-compatibility-switch-not-supported"></a><span data-ttu-id="24cd8-101">Commutateur de compatibilité Switch. System. Windows. Forms. EnableVisualStyleValidation non pris en charge</span><span class="sxs-lookup"><span data-stu-id="24cd8-101">Switch.System.Windows.Forms.EnableVisualStyleValidation compatibility switch not supported</span></span>

<span data-ttu-id="24cd8-102">Le commutateur de compatibilité `Switch.System.Windows.Forms.EnableVisualStyleValidation` n’est pas pris en charge dans Windows Forms sur .NET Core 3,0.</span><span class="sxs-lookup"><span data-stu-id="24cd8-102">The `Switch.System.Windows.Forms.EnableVisualStyleValidation` compatibility switch is not supported in Windows Forms on .NET Core 3.0.</span></span>

#### <a name="change-description"></a><span data-ttu-id="24cd8-103">Modifier la description</span><span class="sxs-lookup"><span data-stu-id="24cd8-103">Change description</span></span>

<span data-ttu-id="24cd8-104">Dans .NET Framework, le commutateur de compatibilité `Switch.System.Windows.Forms.EnableVisualStyleValidation` permettait à une application de refuser la validation des styles visuels fournis sous forme numérique.</span><span class="sxs-lookup"><span data-stu-id="24cd8-104">In .NET Framework, the `Switch.System.Windows.Forms.EnableVisualStyleValidation` compatibility switch allowed an application to opt out of validation of visual styles supplied in a numeric form.</span></span>

<span data-ttu-id="24cd8-105">Dans .NET Core, le commutateur `Switch.System.Windows.Forms.EnableVisualStyleValidation` n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="24cd8-105">In .NET Core, the `Switch.System.Windows.Forms.EnableVisualStyleValidation` switch is not supported.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="24cd8-106">Version introduite</span><span class="sxs-lookup"><span data-stu-id="24cd8-106">Version introduced</span></span>

<span data-ttu-id="24cd8-107">3,0 Preview 9</span><span class="sxs-lookup"><span data-stu-id="24cd8-107">3.0 Preview 9</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="24cd8-108">Action recommandée</span><span class="sxs-lookup"><span data-stu-id="24cd8-108">Recommended action</span></span>

<span data-ttu-id="24cd8-109">Supprimez le commutateur.</span><span class="sxs-lookup"><span data-stu-id="24cd8-109">Remove the switch.</span></span> <span data-ttu-id="24cd8-110">Le commutateur n’est pas pris en charge et aucune autre fonctionnalité n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="24cd8-110">The switch is not supported, and no alternative functionality is available.</span></span>

#### <a name="category"></a><span data-ttu-id="24cd8-111">Category</span><span class="sxs-lookup"><span data-stu-id="24cd8-111">Category</span></span>

<span data-ttu-id="24cd8-112">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="24cd8-112">Windows Forms</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="24cd8-113">API affectées</span><span class="sxs-lookup"><span data-stu-id="24cd8-113">Affected APIs</span></span>

- <span data-ttu-id="24cd8-114">Aucun</span><span class="sxs-lookup"><span data-stu-id="24cd8-114">None</span></span>

<!-- 

### Affected APIs

- Not detectable via API analysis

-->