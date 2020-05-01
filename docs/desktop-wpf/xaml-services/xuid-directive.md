---
title: x:Uid, directive
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], localizable content attribute
- XAML [XAML Services], x:Uid attribute
- x:Uid attribute [XAML Services]
- Uid attribute [XAML Services]
ms.assetid: 81defade-483b-4a89-b76d-9b25bba34010
ms.openlocfilehash: b5b480016d2183268422dea861510c6a169ac27b
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/27/2020
ms.locfileid: "82071338"
---
# <a name="xuid-directive"></a><span data-ttu-id="02cf6-102">x:Uid, directive</span><span class="sxs-lookup"><span data-stu-id="02cf6-102">x:Uid Directive</span></span>

<span data-ttu-id="02cf6-103">Fournit un identificateur unique à des éléments de balisage.</span><span class="sxs-lookup"><span data-stu-id="02cf6-103">Provides a unique identifier for markup elements.</span></span> <span data-ttu-id="02cf6-104">Dans de nombreux scénarios, cet identifiant unique est utilisé par les processus et outils de localisation XAML.</span><span class="sxs-lookup"><span data-stu-id="02cf6-104">In many scenarios, this unique identifier is used by XAML localization processes and tools.</span></span>

## <a name="xaml-attribute-usage"></a><span data-ttu-id="02cf6-105">Utilisation d'attributs XAML</span><span class="sxs-lookup"><span data-stu-id="02cf6-105">XAML Attribute Usage</span></span>

```xaml
<object x:Uid="identifier"... />
```

## <a name="xaml-values"></a><span data-ttu-id="02cf6-106">Valeurs XAML</span><span class="sxs-lookup"><span data-stu-id="02cf6-106">XAML Values</span></span>

|||
|-|-|
|`identifier`|<span data-ttu-id="02cf6-107">Une chaîne créée ou autogénérée manuellement qui doit être unique `x:Uid` dans un fichier lorsqu’elle est interprétée par un consommateur.</span><span class="sxs-lookup"><span data-stu-id="02cf6-107">A manually created or autogenerated string that should be unique in a file when it is interpreted by an `x:Uid` consumer.</span></span>|

## <a name="remarks"></a><span data-ttu-id="02cf6-108">Notes</span><span class="sxs-lookup"><span data-stu-id="02cf6-108">Remarks</span></span>

<span data-ttu-id="02cf6-109">Dans [MS-XAML], `x:Uid` est défini comme une directive.</span><span class="sxs-lookup"><span data-stu-id="02cf6-109">In [MS-XAML], `x:Uid` is defined as a directive.</span></span> <span data-ttu-id="02cf6-110">Pour plus d’informations, voir [ \[MS-XAML\] Section 5.3.6](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10)).</span><span class="sxs-lookup"><span data-stu-id="02cf6-110">For more information, see [\[MS-XAML\] Section 5.3.6](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10)).</span></span>

<span data-ttu-id="02cf6-111">`x:Uid`est discret `x:Name` à la fois en raison du scénario de localisation XAML énoncé et de sorte que les `x:Name`identificateurs qui sont utilisés pour la localisation n’ont aucune dépendance sur les implications du modèle de programmation de .</span><span class="sxs-lookup"><span data-stu-id="02cf6-111">`x:Uid` is discrete from `x:Name` both because of the stated XAML localization scenario and so that identifiers that are used for localization have no dependencies on the programming model implications of `x:Name`.</span></span> <span data-ttu-id="02cf6-112">En `x:Name` outre, est régi par le namescope XAML; cependant, `x:Uid` n’est pas régi par un concept défini par le langage XAML de l’application de la singularité.</span><span class="sxs-lookup"><span data-stu-id="02cf6-112">Also, `x:Name` is governed by the XAML namescope; however, `x:Uid` is not governed by any XAML language defined concept of uniqueness enforcement.</span></span> <span data-ttu-id="02cf6-113">Les processeurs XAML au sens large (les processeurs qui ne font pas partie `x:Uid` du processus de localisation) ne devraient pas faire respecter l’unicité des valeurs.</span><span class="sxs-lookup"><span data-stu-id="02cf6-113">XAML processors in a broad sense (processors that are not part of the localization process) are not expected to enforce uniqueness of `x:Uid` values.</span></span> <span data-ttu-id="02cf6-114">Cette responsabilité est conceptuellement à l’origine des valeurs.</span><span class="sxs-lookup"><span data-stu-id="02cf6-114">That responsibility is conceptually on the originator of the values.</span></span> <span data-ttu-id="02cf6-115">L’attente d’un caractère unique des `x:Uid` valeurs au sein d’une seule source XAML est raisonnable pour les consommateurs des valeurs, telles que les processus ou les outils dédiés à la mondialisation.</span><span class="sxs-lookup"><span data-stu-id="02cf6-115">The expectation of uniqueness of `x:Uid` values within a single XAML source is reasonable for consumers of the values, such as dedicated globalization processes or tools.</span></span> <span data-ttu-id="02cf6-116">Le modèle typique d’unicité est que les `x:Uid` valeurs sont uniques dans un fichier codé XML qui représente XAML.</span><span class="sxs-lookup"><span data-stu-id="02cf6-116">The typical uniqueness model is that `x:Uid` values are unique within an XML-encoded file that represents XAML.</span></span>

<span data-ttu-id="02cf6-117">Les outils qui ont une connaissance significative d’un `x:Uid` schéma XAML particulier peuvent choisir de s’appliquer uniquement pour les vraies chaînes localisables, au lieu de tous les cas où une valeur de chaîne de texte est rencontrée dans le balisage.</span><span class="sxs-lookup"><span data-stu-id="02cf6-117">Tools that have significant knowledge of a particular XAML schema can choose to apply `x:Uid` only for true localizable strings, instead of for all cases where a text string value is encountered in markup.</span></span>

<span data-ttu-id="02cf6-118">Les cadres peuvent spécifier une propriété particulière `x:Uid` dans leur <xref:System.Windows.Markup.UidPropertyAttribute> modèle d’objet pour être un alias pour en appliquant l’attribut au type définissant.</span><span class="sxs-lookup"><span data-stu-id="02cf6-118">Frameworks can specify a particular property in their object model to be an alias for `x:Uid` by applying the attribute <xref:System.Windows.Markup.UidPropertyAttribute> to the defining type.</span></span> <span data-ttu-id="02cf6-119">Si un cadre spécifie une propriété particulière, il n’est pas valide de spécifier à la fois `x:Uid` et le membre alias sur le même objet.</span><span class="sxs-lookup"><span data-stu-id="02cf6-119">If a framework specifies a particular property, it is not valid to specify both `x:Uid` and the aliased member on the same object.</span></span> <span data-ttu-id="02cf6-120">Si `x:Uid` les deux et le membre alias sont spécifiés, <xref:System.Xaml.XamlDuplicateMemberException> .NET XAML Services API jette généralement pour ce cas.</span><span class="sxs-lookup"><span data-stu-id="02cf6-120">If both `x:Uid` and the aliased member are specified, .NET XAML Services API typically throws <xref:System.Xaml.XamlDuplicateMemberException> for this case.</span></span>

## <a name="wpf-usage-notes"></a><span data-ttu-id="02cf6-121">Remarques sur l'utilisation de WPF</span><span class="sxs-lookup"><span data-stu-id="02cf6-121">WPF Usage Notes</span></span>

<span data-ttu-id="02cf6-122">Pour plus d’informations `x:Uid` sur le rôle de dans le processus de localisation WPF et sous la forme BAML de XAML, voir [Mondialisation pour WPF](../../framework/wpf/advanced/globalization-for-wpf.md) ou<xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A></span><span class="sxs-lookup"><span data-stu-id="02cf6-122">For more information about the role of `x:Uid` in the WPF localization process and in the BAML form of XAML, see [Globalization for WPF](../../framework/wpf/advanced/globalization-for-wpf.md) or <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A></span></span>

## <a name="see-also"></a><span data-ttu-id="02cf6-123">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="02cf6-123">See also</span></span>

- <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>
- <xref:Microsoft.Build.Tasks.Windows.UidManager>
- [<span data-ttu-id="02cf6-124">Globalisation pour WPF</span><span class="sxs-lookup"><span data-stu-id="02cf6-124">Globalization for WPF</span></span>](../../framework/wpf/advanced/globalization-for-wpf.md)