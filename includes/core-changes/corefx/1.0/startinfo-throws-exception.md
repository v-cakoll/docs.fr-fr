---
ms.openlocfilehash: 92c03328414410d56a2ff5f445639757367b42c7
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420424"
---
### <a name="processstartinfo-throws-invalidoperationexception-for-processes-you-didnt-start"></a><span data-ttu-id="a5d76-101">Process. StartInfo lève une exception InvalidOperationException pour les processus que vous n’avez pas démarrés</span><span class="sxs-lookup"><span data-stu-id="a5d76-101">Process.StartInfo throws InvalidOperationException for processes you didn't start</span></span>

<span data-ttu-id="a5d76-102">La lecture <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> de la propriété pour les processus que votre code n’a pas démarré lève une exception <xref:System.InvalidOperationException> .</span><span class="sxs-lookup"><span data-stu-id="a5d76-102">Reading the <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> property for processes that your code didn't start throws an <xref:System.InvalidOperationException>.</span></span>

#### <a name="change-description"></a><span data-ttu-id="a5d76-103">Description de la modification</span><span class="sxs-lookup"><span data-stu-id="a5d76-103">Change description</span></span>

<span data-ttu-id="a5d76-104">Dans .NET Framework, l’accès à la <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> propriété pour les processus que votre code n’a pas démarré retourne un <xref:System.Diagnostics.ProcessStartInfo> objet factice.</span><span class="sxs-lookup"><span data-stu-id="a5d76-104">In .NET Framework, accessing the <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> property for processes that your code didn't start returns a dummy <xref:System.Diagnostics.ProcessStartInfo> object.</span></span> <span data-ttu-id="a5d76-105">L’objet factice contient des valeurs par défaut pour toutes ses propriétés, à l’exception de <xref:System.Diagnostics.ProcessStartInfo.EnvironmentVariables> .</span><span class="sxs-lookup"><span data-stu-id="a5d76-105">The dummy object contains default values for all of its properties except <xref:System.Diagnostics.ProcessStartInfo.EnvironmentVariables>.</span></span>

<span data-ttu-id="a5d76-106">À compter de .NET Core 1,0, si vous lisez la <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> propriété d’un processus que vous n’avez pas démarré (autrement dit, en appelant <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> ), une <xref:System.InvalidOperationException> exception est levée.</span><span class="sxs-lookup"><span data-stu-id="a5d76-106">Starting in .NET Core 1.0, if you read the <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> property for a process that you didn't start (that is, by calling <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType>), an <xref:System.InvalidOperationException> is thrown.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="a5d76-107">Version introduite</span><span class="sxs-lookup"><span data-stu-id="a5d76-107">Version introduced</span></span>

<span data-ttu-id="a5d76-108">1.0</span><span class="sxs-lookup"><span data-stu-id="a5d76-108">1.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="a5d76-109">Action recommandée</span><span class="sxs-lookup"><span data-stu-id="a5d76-109">Recommended action</span></span>

<span data-ttu-id="a5d76-110">N’accédez pas à la <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> propriété pour les processus que votre code n’a pas démarré.</span><span class="sxs-lookup"><span data-stu-id="a5d76-110">Do not access the <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> property for processes that your code didn't start.</span></span> <span data-ttu-id="a5d76-111">Par exemple, ne lisez pas cette propriété pour les processus retournés par <xref:System.Diagnostics.Process.GetProcesses%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="a5d76-111">For example, don't read this property for processes returned by <xref:System.Diagnostics.Process.GetProcesses%2A?displayProperty=nameWithType>.</span></span>

#### <a name="category"></a><span data-ttu-id="a5d76-112">Category</span><span class="sxs-lookup"><span data-stu-id="a5d76-112">Category</span></span>

<span data-ttu-id="a5d76-113">Bibliothèques .NET Core</span><span class="sxs-lookup"><span data-stu-id="a5d76-113">Core .NET libraries</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="a5d76-114">API affectées</span><span class="sxs-lookup"><span data-stu-id="a5d76-114">Affected APIs</span></span>

- <xref:System.Diagnostics.Process.StartInfo?displayProperty=fullName>

<!--

#### Affected APIs

- `P:System.Diagnostics.Process.StartInfo`

-->