---
title: Classe XAMLServices et lecture ou écriture XAML de base
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], XamlServices class
- XamlServices class [XAML Services], how to use
ms.assetid: 6ac27fad-3687-4d7a-add1-3e90675fdfde
ms.openlocfilehash: 264a8c4abcf9a7efceb7c7accd786495d35476e5
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2020
ms.locfileid: "82071877"
---
# <a name="xamlservices-class-and-basic-xaml-reading-or-writing"></a><span data-ttu-id="a235a-102">Classe XAMLServices et lecture ou écriture XAML de base</span><span class="sxs-lookup"><span data-stu-id="a235a-102">XAMLServices class and basic XAML reading or writing</span></span>

<span data-ttu-id="a235a-103"><xref:System.Xaml.XamlServices>est une classe fournie par .NET qui peut être utilisé pour répondre aux scénarios XAML qui ne nécessitent pas un accès spécifique au flux de nœuds XAML ou à des informations système de type XAML obtenues à partir de ces nœuds.</span><span class="sxs-lookup"><span data-stu-id="a235a-103"><xref:System.Xaml.XamlServices> is a class provided by .NET that can be used to address XAML scenarios that don't require specific access to the XAML node stream or to XAML type system information obtained from those nodes.</span></span> <span data-ttu-id="a235a-104"><xref:System.Xaml.XamlServices>L’API peut être `Load` résumée comme suit : `Parse` ou `Save` pour prendre en charge un `Transform` chemin de charge XAML, pour prendre en charge un chemin d’enregistrement XAML, et pour fournir une technique qui relie un chemin de charge et de sauver le chemin.</span><span class="sxs-lookup"><span data-stu-id="a235a-104"><xref:System.Xaml.XamlServices> API can be summarized as follows: `Load` or `Parse` to support a XAML load path, `Save` to support a XAML save path, and `Transform` to provide a technique that joins a load path and save path.</span></span> <span data-ttu-id="a235a-105">`Transform` peut être utilisé pour passer d'un schéma XAML à un autre.</span><span class="sxs-lookup"><span data-stu-id="a235a-105">`Transform` can be used to change from one XAML schema to another.</span></span> <span data-ttu-id="a235a-106">Cette rubrique résume chacune de ces classifications d'API et décrit les différences qui existent entre des surcharges de méthode particulières.</span><span class="sxs-lookup"><span data-stu-id="a235a-106">This topic summarizes each of these API classifications and describes the differences between particular method overloads.</span></span>

## <a name="load"></a><span data-ttu-id="a235a-107">Load</span><span class="sxs-lookup"><span data-stu-id="a235a-107">Load</span></span>

<span data-ttu-id="a235a-108">Différentes surcharges de <xref:System.Xaml.XamlServices.Load%2A> implémentent la logique complète d'un chemin de chargement.</span><span class="sxs-lookup"><span data-stu-id="a235a-108">Various overloads of <xref:System.Xaml.XamlServices.Load%2A> implement the complete logic for a load path.</span></span> <span data-ttu-id="a235a-109">Le chemin de chargement utilise du code XAML sous une certaine forme et exporte un flux de nœud XAML.</span><span class="sxs-lookup"><span data-stu-id="a235a-109">The load path uses XAML in some form and outputs a XAML node stream.</span></span> <span data-ttu-id="a235a-110">La plupart de ces chemins de chargement utilise du code XAML sous la forme d'un fichier texte XML encodé.</span><span class="sxs-lookup"><span data-stu-id="a235a-110">Most of these load paths use XAML in an encoded XML text-file form.</span></span> <span data-ttu-id="a235a-111">Toutefois, vous pouvez aussi charger un flux général ou une source XAML préchargée qui est déjà contenue dans une implémentation de <xref:System.Xaml.XamlReader> différente.</span><span class="sxs-lookup"><span data-stu-id="a235a-111">However, you can also load a general stream, or you can load a preloaded XAML source that is already contained in a different <xref:System.Xaml.XamlReader> implementation.</span></span>

<span data-ttu-id="a235a-112">La surcharge la plus simple pour la plupart des scénarios est <xref:System.Xaml.XamlServices.Load%28System.String%29>.</span><span class="sxs-lookup"><span data-stu-id="a235a-112">The simplest overload for most scenarios is <xref:System.Xaml.XamlServices.Load%28System.String%29>.</span></span> <span data-ttu-id="a235a-113">Cette surcharge possède un paramètre `fileName` qui correspond simplement au nom d'un fichier texte contenant le code XAML à charger.</span><span class="sxs-lookup"><span data-stu-id="a235a-113">This overload has a `fileName` parameter that is simply the name of a text file that contains the XAML to load.</span></span> <span data-ttu-id="a235a-114">Elle convient particulièrement aux scénarios d'application comme pour les applications de confiance totale qui ont précédemment sérialisé l'état ou les données sur l'ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="a235a-114">This is appropriate for application scenarios such as full trust applications that have previously serialized state or data to the local computer.</span></span> <span data-ttu-id="a235a-115">Elle est également utile pour les infrastructures dans lesquelles vous définissez le modèle d'application et souhaitez charger l'un des fichiers standard qui définit le comportement de l'application, en démarrant l'interface utilisateur ou d'autres fonctions définies par l'infrastructure qui utilisent XAML.</span><span class="sxs-lookup"><span data-stu-id="a235a-115">This is also useful for frameworks where you are defining the application model and want to load one of the standard files that defines application behavior, starting UI, or other framework-defined capabilities that use XAML.</span></span>

<span data-ttu-id="a235a-116"><xref:System.Xaml.XamlServices.Load%28System.IO.Stream%29> dispose de scénarios similaires.</span><span class="sxs-lookup"><span data-stu-id="a235a-116"><xref:System.Xaml.XamlServices.Load%28System.IO.Stream%29> has similar scenarios.</span></span> <span data-ttu-id="a235a-117">Cette surcharge peut s'avérer utile si l'utilisateur choisit les fichiers à charger, car un <xref:System.IO.Stream> est une sortie fréquente d'autres API <xref:System.IO> qui peuvent accéder à un système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="a235a-117">This overload might be useful if you have the user choose files to load, because a <xref:System.IO.Stream> is a frequent output of other <xref:System.IO> APIs that can access a file system.</span></span> <span data-ttu-id="a235a-118">Vous pouvez également accéder aux sources XAML par le biais de téléchargements asynchrones ou d'autres techniques de réseau qui fournissent également un flux.</span><span class="sxs-lookup"><span data-stu-id="a235a-118">Or you could be accessing XAML sources through asynchronous downloads or other network techniques that also provide a stream.</span></span> <span data-ttu-id="a235a-119">(Le chargement d'un flux de données ou d'une source choisie par l'utilisateur peut avoir des conséquences sur la sécurité.</span><span class="sxs-lookup"><span data-stu-id="a235a-119">(Loading from a stream or user-selected source may have security implications.</span></span> <span data-ttu-id="a235a-120">Pour plus d’informations, consultez [XAML Security Considerations](security-considerations.md).)</span><span class="sxs-lookup"><span data-stu-id="a235a-120">For more information, see [XAML Security Considerations](security-considerations.md).)</span></span>

<span data-ttu-id="a235a-121"><xref:System.Xaml.XamlServices.Load%28System.IO.TextReader%29>et <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29> sont des surcharges qui s’appuient sur les lecteurs de formats de versions précédentes de .NET.</span><span class="sxs-lookup"><span data-stu-id="a235a-121"><xref:System.Xaml.XamlServices.Load%28System.IO.TextReader%29> and <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29> are overloads that rely on readers of formats from previous versions of .NET.</span></span> <span data-ttu-id="a235a-122">Pour utiliser ces surcharges, vous devriez avoir déjà `Create` créé une instance de lecteur et utiliser son API pour charger le XAML sous la forme pertinente (texte ou XML).</span><span class="sxs-lookup"><span data-stu-id="a235a-122">To use these overloads, you should have already created a reader instance and used its `Create` API to load the XAML in the relevant form (text or XML).</span></span> <span data-ttu-id="a235a-123">Si vous avez déjà déplacé des pointeurs d'enregistrement dans les autres lecteurs ou exécuté d'autres opérations les concernant, cela ne pose aucun problème.</span><span class="sxs-lookup"><span data-stu-id="a235a-123">If you have already moved record pointers in the other readers or performed other operations with them, this is not important.</span></span> <span data-ttu-id="a235a-124">La logique du chemin de chargement de <xref:System.Xaml.XamlServices.Load%2A> traite toujours l'entrée XAML entière à partir de la racine.</span><span class="sxs-lookup"><span data-stu-id="a235a-124">The load path logic from <xref:System.Xaml.XamlServices.Load%2A> always processes the entire XAML input from the root down.</span></span> <span data-ttu-id="a235a-125">Les scénarios suivants pourraient justifier l’utilisation de ces surcharges :</span><span class="sxs-lookup"><span data-stu-id="a235a-125">The following scenarios might warrant the use of these overloads:</span></span>

- <span data-ttu-id="a235a-126">les aires de conception dans lesquelles vous fournissez des fonctions d'édition XAML simples à partir d'un éditeur de texte XML existant ;</span><span class="sxs-lookup"><span data-stu-id="a235a-126">Design surfaces where you provide simple XAML editing capability from an existing XML-specific text editor.</span></span>

- <span data-ttu-id="a235a-127">les variantes des scénarios <xref:System.IO> de base dans lesquels vous utilisez les lecteurs dédiés pour ouvrir des fichiers ou des flux.</span><span class="sxs-lookup"><span data-stu-id="a235a-127">Variants of the core <xref:System.IO> scenarios, where you use the dedicated readers to open files or streams.</span></span> <span data-ttu-id="a235a-128">Votre logique procède à un contrôle ou un traitement rudimentaire du contenu avant de tenter de le charger en tant que code XAML.</span><span class="sxs-lookup"><span data-stu-id="a235a-128">Your logic performs rudimentary checking or processing of the contents before it tries to load as XAML.</span></span>

<span data-ttu-id="a235a-129">Vous pouvez charger un fichier ou un <xref:System.Xml.XmlReader>flux, ou vous pouvez charger un , , <xref:System.IO.TextReader>ou <xref:System.Xaml.XamlReader> qui enveloppe votre entrée XAML en chargeant avec les API du lecteur.</span><span class="sxs-lookup"><span data-stu-id="a235a-129">You can either load a file or stream, or you can load an <xref:System.Xml.XmlReader>, <xref:System.IO.TextReader>, or <xref:System.Xaml.XamlReader> that wraps your XAML input by loading with the reader's APIs.</span></span>

<span data-ttu-id="a235a-130">En interne, chacune des surcharges précédentes correspond finalement à <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29>, avec le <xref:System.Xml.XmlReader> passé qui est utilisé pour créer un <xref:System.Xaml.XamlXmlReader>.</span><span class="sxs-lookup"><span data-stu-id="a235a-130">Internally, each of the preceding overloads is ultimately <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29>, and the passed <xref:System.Xml.XmlReader> is used to create a new <xref:System.Xaml.XamlXmlReader>.</span></span>

<span data-ttu-id="a235a-131">La signature `Load` permettant des scénarios plus avancés est <xref:System.Xaml.XamlServices.Load%28System.Xaml.XamlReader%29>.</span><span class="sxs-lookup"><span data-stu-id="a235a-131">The `Load` signature that provides for more advanced scenarios is <xref:System.Xaml.XamlServices.Load%28System.Xaml.XamlReader%29>.</span></span> <span data-ttu-id="a235a-132">Vous pouvez utiliser cette signature pour l'un des cas suivants :</span><span class="sxs-lookup"><span data-stu-id="a235a-132">You can use this signature for one of the following cases:</span></span>

- <span data-ttu-id="a235a-133">Vous avez défini votre propre <xref:System.Xaml.XamlReader>implémentation d’un .</span><span class="sxs-lookup"><span data-stu-id="a235a-133">You've defined your own implementation of a <xref:System.Xaml.XamlReader>.</span></span>

- <span data-ttu-id="a235a-134">Vous devez spécifier des paramètres pour <xref:System.Xaml.XamlReader> qui diffèrent des paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="a235a-134">You need to specify settings for <xref:System.Xaml.XamlReader> that vary from the default settings.</span></span>

<span data-ttu-id="a235a-135">Exemples de paramètres non par défaut :</span><span class="sxs-lookup"><span data-stu-id="a235a-135">Examples of non-default settings:</span></span>

<xref:System.Xaml.XamlReaderSettings.AllowProtectedMembersOnRoot%2A>\
<xref:System.Xaml.XamlReaderSettings.BaseUri%2A>\
<xref:System.Xaml.XamlReaderSettings.IgnoreUidsOnPropertyElements%2A>\
<xref:System.Xaml.XamlReaderSettings.LocalAssembly%2A>\
<span data-ttu-id="a235a-136"><xref:System.Xaml.XamlReaderSettings.ValuesMustBeString%2A>.</span><span class="sxs-lookup"><span data-stu-id="a235a-136"><xref:System.Xaml.XamlReaderSettings.ValuesMustBeString%2A>.</span></span>

<span data-ttu-id="a235a-137">Le lecteur par défaut de <xref:System.Xaml.XamlServices> est <xref:System.Xaml.XamlXmlReader>.</span><span class="sxs-lookup"><span data-stu-id="a235a-137">The default reader for <xref:System.Xaml.XamlServices> is <xref:System.Xaml.XamlXmlReader>.</span></span> <span data-ttu-id="a235a-138">Si vous fournissez vos propres <xref:System.Xaml.XamlXmlReader> paramètres, ce qui <xref:System.Xaml.XamlXmlReaderSettings>suit sont des propriétés à définir non-default :</span><span class="sxs-lookup"><span data-stu-id="a235a-138">If you provide your own <xref:System.Xaml.XamlXmlReader> with settings, the following are properties to set non-default <xref:System.Xaml.XamlXmlReaderSettings>:</span></span>

<xref:System.Xaml.XamlXmlReaderSettings.CloseInput%2A>\
<xref:System.Xaml.XamlXmlReaderSettings.SkipXmlCompatibilityProcessing%2A>\
<xref:System.Xaml.XamlXmlReaderSettings.XmlLang%2A>\
<xref:System.Xaml.XamlXmlReaderSettings.XmlSpacePreserve%2A>

## <a name="parse"></a><span data-ttu-id="a235a-139">Analyser</span><span class="sxs-lookup"><span data-stu-id="a235a-139">Parse</span></span>

<span data-ttu-id="a235a-140"><xref:System.Xaml.XamlServices.Parse%2A> s'apparente à `Load` en ce sens que c'est une API de chemin de chargement qui crée un flux de nœud XAML à partir de l'entrée XAML.</span><span class="sxs-lookup"><span data-stu-id="a235a-140"><xref:System.Xaml.XamlServices.Parse%2A> is like `Load` because it is a load path API that creates a XAML node stream from XAML input.</span></span> <span data-ttu-id="a235a-141">Toutefois, dans ce cas, l'entrée XAML est fournie directement sous la forme d'une chaîne qui contient tout le code XAML à charger.</span><span class="sxs-lookup"><span data-stu-id="a235a-141">However, in this case, the XAML input is provided directly as a string that contains all the XAML to load.</span></span> <span data-ttu-id="a235a-142"><xref:System.Xaml.XamlServices.Parse%2A> est une approche légère plus appropriée pour les scénarios d'application que les scénarios d'infrastructure.</span><span class="sxs-lookup"><span data-stu-id="a235a-142"><xref:System.Xaml.XamlServices.Parse%2A> is a lightweight approach that is more appropriate for application scenarios than framework scenarios.</span></span> <span data-ttu-id="a235a-143">Pour plus d’informations, consultez <xref:System.Xaml.XamlServices.Parse%2A>.</span><span class="sxs-lookup"><span data-stu-id="a235a-143">For more information, see <xref:System.Xaml.XamlServices.Parse%2A>.</span></span> <span data-ttu-id="a235a-144"><xref:System.Xaml.XamlServices.Parse%2A>n’est <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29> qu’un <xref:System.IO.StringReader> appel enveloppé qui implique un interne.</span><span class="sxs-lookup"><span data-stu-id="a235a-144"><xref:System.Xaml.XamlServices.Parse%2A> is just a wrapped <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29> call that involves a <xref:System.IO.StringReader> internally.</span></span>

## <a name="save"></a><span data-ttu-id="a235a-145">Enregistrer</span><span class="sxs-lookup"><span data-stu-id="a235a-145">Save</span></span>

<span data-ttu-id="a235a-146">Diverses surcharges <xref:System.Xaml.XamlServices.Save%2A> d’implémenter le chemin d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="a235a-146">Various overloads of <xref:System.Xaml.XamlServices.Save%2A> implement the save path.</span></span> <span data-ttu-id="a235a-147">Les méthodes <xref:System.Xaml.XamlServices.Save%2A> ont toutes un graphique d'objets comme entrée et génère un flux, un fichier ou une instance <xref:System.Xml.XmlWriter>/<xref:System.IO.TextWriter> comme sortie.</span><span class="sxs-lookup"><span data-stu-id="a235a-147">All of the <xref:System.Xaml.XamlServices.Save%2A> methods all take an object graph as input and produce output as a stream, file, or <xref:System.Xml.XmlWriter>/<xref:System.IO.TextWriter> instance.</span></span>

<span data-ttu-id="a235a-148">L'objet en entrée est supposé être l'objet racine d'une représentation d'objet.</span><span class="sxs-lookup"><span data-stu-id="a235a-148">The input object is expected to be the root object of some object representation.</span></span> <span data-ttu-id="a235a-149">Il peut s'agir de la racine unique d'un objet métier, de la racine d'une arborescence d'objets pour la page d'un scénario d'interface utilisateur, de la surface de modification active d'un outil de conception ou encore d'autres concepts d'objet racine appropriés pour les scénarios.</span><span class="sxs-lookup"><span data-stu-id="a235a-149">This might be the single root of a business object, the root of an object tree for a page in a UI scenario, the working editing surface from a design tool, or other root object concepts that are appropriate for scenarios.</span></span>

<span data-ttu-id="a235a-150">Dans de nombreux scénarios, l’arbre objet que vous enregistrez est <xref:System.Xaml.XamlServices.Load%2A> lié à une opération originale qui a chargé XAML avec ou avec d’autres API mis en œuvre par un modèle de cadre/application.</span><span class="sxs-lookup"><span data-stu-id="a235a-150">In many scenarios, the object tree that you save is related to an original operation that loaded XAML either with <xref:System.Xaml.XamlServices.Load%2A> or with other API implemented by a framework/application model.</span></span> <span data-ttu-id="a235a-151">Il peut y avoir des différences capturées dans l'arborescence d'objets dues à des modifications d'état, des modifications dans lesquelles votre application a capturé des paramètres d'exécution auprès d'un utilisateur, du code XAML modifié car votre application est une aire de conception XAML, etc. Avec ou sans modification, le concept consistant à d'abord charger le code XAML à partir du balisage, puis à le réenregistrer et à comparer les deux formes de balisage XAML est parfois appelé représentation « aller-retour » du code XAML.</span><span class="sxs-lookup"><span data-stu-id="a235a-151">There might be differences captured in the object tree that are due to state changes, changes where your application captured runtime settings from a user, changed XAML because your application is a XAML design surface, etc. With or without changes, the concept of first loading XAML from markup and then saving it again and comparing the two XAML markup forms is sometimes referred as a round-trip representation of the XAML.</span></span>

<span data-ttu-id="a235a-152">Le défi lié à l'enregistrement et à la sérialisation d'un objet complexe qui est défini dans une forme de balisage réside dans l'obtention d'un équilibre entre une représentation complète sans perte d'informations et un excès de commentaires rendant le code XAML moins explicite.</span><span class="sxs-lookup"><span data-stu-id="a235a-152">The challenge with saving and serializing a complex object that is set in a markup form is in achieving a balance between full representation without information loss, versus verbosity that makes the XAML less human-readable.</span></span> <span data-ttu-id="a235a-153">De plus, différents clients pour XAML peuvent avoir des définitions ou des attentes différentes concernant la définition de l'équilibre.</span><span class="sxs-lookup"><span data-stu-id="a235a-153">Moreover, different customers for XAML might have different definitions or expectations for how that balance should be set.</span></span> <span data-ttu-id="a235a-154">Les API <xref:System.Xaml.XamlServices.Save%2A> représentent une définition de cet équilibre.</span><span class="sxs-lookup"><span data-stu-id="a235a-154">The <xref:System.Xaml.XamlServices.Save%2A> APIs represent one definition of that balance.</span></span> <span data-ttu-id="a235a-155">Les API <xref:System.Xaml.XamlServices.Save%2A> utilisent un contexte de schéma XAML disponible et les caractéristiques CLR par défaut de <xref:System.Xaml.XamlType>, de <xref:System.Xaml.XamlMember>et d'autres concepts d'intrinsèque XAML et de système de type XAML pour déterminer si certaines constructions de flux de nœud XAML peuvent être optimisées lorsqu'elles sont réenregistrées dans le balisage.</span><span class="sxs-lookup"><span data-stu-id="a235a-155">The <xref:System.Xaml.XamlServices.Save%2A> APIs use available XAML schema context and the default CLR-based characteristics of <xref:System.Xaml.XamlType>, <xref:System.Xaml.XamlMember>, and other XAML intrinsic and XAML type system concepts to determine where certain XAML node stream constructs can be optimized when they are saved back into markup.</span></span> <span data-ttu-id="a235a-156">Par exemple, les chemins d'enregistrement <xref:System.Xaml.XamlServices> peuvent utiliser un contexte de schéma XAML par défaut basé sur CLR pour résoudre <xref:System.Xaml.XamlType> pour des objets, déterminer une propriété <xref:System.Xaml.XamlType.ContentProperty%2A?displayProperty=nameWithType>, puis omettre des balises d'éléments de propriété lors de l'écriture de la propriété dans le contenu XAML de cet objet.</span><span class="sxs-lookup"><span data-stu-id="a235a-156">For example, <xref:System.Xaml.XamlServices> save paths can use CLR-based default XAML schema context to resolve <xref:System.Xaml.XamlType> for objects, can determine a <xref:System.Xaml.XamlType.ContentProperty%2A?displayProperty=nameWithType>, and then can omit property element tags when they write the property to the XAML content of the object.</span></span>

<a name="transform"></a>
## <a name="transform"></a><span data-ttu-id="a235a-157">Transformer</span><span class="sxs-lookup"><span data-stu-id="a235a-157">Transform</span></span>

<span data-ttu-id="a235a-158"><xref:System.Xaml.XamlServices.Transform%2A> convertit ou transforme le code XAML en associant un chemin de chargement et un chemin d'enregistrement dans le cadre d'une seule opération.</span><span class="sxs-lookup"><span data-stu-id="a235a-158"><xref:System.Xaml.XamlServices.Transform%2A> converts or transforms XAML by linking a load path and a save path as a single operation.</span></span> <span data-ttu-id="a235a-159">Un contexte de schéma ou un système de types de stockage différent peut être utilisé pour <xref:System.Xaml.XamlReader> et <xref:System.Xaml.XamlWriter>, ce qui est l'élément qui influence le mode de transformation du code XAML obtenu.</span><span class="sxs-lookup"><span data-stu-id="a235a-159">A different schema context or different backing type system can be used for <xref:System.Xaml.XamlReader> and <xref:System.Xaml.XamlWriter>, which is what influences how the resulting XAML is transformed.</span></span> <span data-ttu-id="a235a-160">Cela fonctionne bien pour les opérations de transformation générales.</span><span class="sxs-lookup"><span data-stu-id="a235a-160">This works well for broad transform operations.</span></span>

<span data-ttu-id="a235a-161">Pour les opérations qui reposent sur l'examen de chaque nœud dans un flux de nœud XAML, vous n'utiliseriez généralement pas <xref:System.Xaml.XamlServices.Transform%2A>.</span><span class="sxs-lookup"><span data-stu-id="a235a-161">For operations that rely on examining each node in a XAML node stream, you typically do not use <xref:System.Xaml.XamlServices.Transform%2A>.</span></span> <span data-ttu-id="a235a-162">Au lieu de cela, vous devez définir votre propre série d'opérations chemin de chargement-chemin d'enregistrement et lancer votre propre logique.</span><span class="sxs-lookup"><span data-stu-id="a235a-162">Instead you need to define your own load path-save path operation series and interject your own logic.</span></span> <span data-ttu-id="a235a-163">Dans l'un des chemins, utilisez une paire lecteur XAML/writer XAML autour de votre propre boucle de nœud.</span><span class="sxs-lookup"><span data-stu-id="a235a-163">In one of the paths, use a XAML reader/XAML writer pair around your own node loop.</span></span> <span data-ttu-id="a235a-164">Par exemple, chargez le code XAML initial à l'aide de <xref:System.Xaml.XamlXmlReader> et entrez dans les nœuds avec des appels à <xref:System.Xaml.XamlXmlReader.Read%2A> successifs.</span><span class="sxs-lookup"><span data-stu-id="a235a-164">For example, load the initial XAML using <xref:System.Xaml.XamlXmlReader> and step into the nodes with successive <xref:System.Xaml.XamlXmlReader.Read%2A> calls.</span></span> <span data-ttu-id="a235a-165">En opérant au niveau du flux de nœud XAML, vous pouvez maintenant ajuster des nœuds individuels (types, membres ou autres nœuds) pour appliquer une transformation ou laisser le nœud en l'état.</span><span class="sxs-lookup"><span data-stu-id="a235a-165">Operating at the XAML node stream level you can now adjust individual nodes (types, members, other nodes) to apply a transformation, or leave the node as-is.</span></span> <span data-ttu-id="a235a-166">Envoyez ensuite le nœud à l'API `Write` pertinente d'un <xref:System.Xaml.XamlObjectWriter> et écrivez l'objet.</span><span class="sxs-lookup"><span data-stu-id="a235a-166">Then you send the node onwards to the relevant `Write` API of a <xref:System.Xaml.XamlObjectWriter> and write out the object.</span></span> <span data-ttu-id="a235a-167">Pour plus d'informations, consultez [Understanding XAML Node Stream Structures and Concepts](understanding-xaml-node-stream-structures-and-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="a235a-167">For more information, see [Understanding XAML Node Stream Structures and Concepts](understanding-xaml-node-stream-structures-and-concepts.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a235a-168">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a235a-168">See also</span></span>

- <xref:System.Xaml.XamlObjectWriter>
- <xref:System.Xaml.XamlServices>
- [<span data-ttu-id="a235a-169">Services XAML</span><span class="sxs-lookup"><span data-stu-id="a235a-169">XAML Services</span></span>](../../../api/index.md)