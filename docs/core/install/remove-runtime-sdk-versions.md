---
title: Supprimer le SDK et le runtime .NET Core
description: Cet article explique comment déterminer quelles versions du runtime .NET Core et du SDK sont actuellement installées, puis comment les supprimer sous Windows, Mac et Linux.
author: thraka
ms.author: adegeo
ms.date: 04/28/2020
zone_pivot_groups: operating-systems-set-one
ms.openlocfilehash: f1482c243ba22fa81c69ede847a0f6b36a9cb83c
ms.sourcegitcommit: d7666f6e49c57a769612602ea7857b927294ce47
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82595782"
---
# <a name="how-to-remove-the-net-core-runtime-and-sdk"></a><span data-ttu-id="d79a5-103">Guide pratique pour supprimer un SDK et un Runtime .NET Core</span><span class="sxs-lookup"><span data-stu-id="d79a5-103">How to remove the .NET Core Runtime and SDK</span></span>

<span data-ttu-id="d79a5-104">Si vous avez installé plusieurs versions mises à jour du SDK et du Runtime .NET Core au fil du temps, vous voulez peut-être maintenant supprimer les versions anciennes de .NET Core installées sur votre machine.</span><span class="sxs-lookup"><span data-stu-id="d79a5-104">Over time, as you install updated versions of the .NET Core runtime and SDK, you may want to remove outdated versions of .NET Core from your machine.</span></span> <span data-ttu-id="d79a5-105">La suppression de versions antérieures du Runtime peut entraîner un changement de Runtime sélectionné pour exécuter les applications de framework partagé, comme cela est expliqué dans l’article sur la [sélection de la version de .NET Core](../versions/selection.md).</span><span class="sxs-lookup"><span data-stu-id="d79a5-105">Removing older versions of the runtime may change the runtime chosen to run shared framework applications, as detailed in the article on [.NET Core version selection](../versions/selection.md).</span></span>

## <a name="should-i-remove-a-version"></a><span data-ttu-id="d79a5-106">Dois-je supprimer une version ?</span><span class="sxs-lookup"><span data-stu-id="d79a5-106">Should I remove a version?</span></span>

<span data-ttu-id="d79a5-107">Compte tenu des comportements de [sélection de la version de .NET Core](../versions/selection.md) et de la compatibilité des Runtimes .NET Core entre les mises à jour, vous pouvez supprimer en toute sécurité les versions précédentes.</span><span class="sxs-lookup"><span data-stu-id="d79a5-107">The [.NET Core version selection](../versions/selection.md) behaviors and the runtime compatibility of .NET Core across updates enables safe removal of previous versions.</span></span> <span data-ttu-id="d79a5-108">Les mises à jour du Runtime .NET Core sont toutes compatibles au sein d’une même version principale (par exemple, 1.x et 2.x).</span><span class="sxs-lookup"><span data-stu-id="d79a5-108">.NET Core runtime updates are compatible within a major version 'band' such as 1.x and 2.x.</span></span> <span data-ttu-id="d79a5-109">De plus, avec les versions récentes du SDK .NET Core, vous pouvez généralement continuer à créer des applications qui ciblent des versions précédentes du Runtime de manière compatible.</span><span class="sxs-lookup"><span data-stu-id="d79a5-109">Additionally, newer releases of the .NET Core SDK generally maintain the ability to build applications that target previous versions of the runtime in a compatible manner.</span></span>

<span data-ttu-id="d79a5-110">En règle générale, vous avez uniquement besoin de la dernière version du SDK et de la dernière version des correctifs pour les Runtimes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="d79a5-110">In general, you only need the latest SDK and latest patch version of the runtimes required for your application.</span></span> <span data-ttu-id="d79a5-111">Les instances dans lesquelles vous pouvez conserver des versions antérieures du kit de développement logiciel (SDK) ou du runtime incluent la gestion des applications *Project. JSON*.</span><span class="sxs-lookup"><span data-stu-id="d79a5-111">Instances where you might want to keep older SDK or runtime versions include maintaining *project.json*-based applications.</span></span> <span data-ttu-id="d79a5-112">Si votre application ne nécessite pas de versions antérieures du SDK ou du Runtime pour une raison particulière, vous pouvez supprimer les versions antérieures en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="d79a5-112">Unless your application has specific reasons for earlier SDKs or runtimes, you may safely remove older versions.</span></span>

## <a name="determine-what-is-installed"></a><span data-ttu-id="d79a5-113">Déterminer ce qui est installé</span><span class="sxs-lookup"><span data-stu-id="d79a5-113">Determine what is installed</span></span>

<span data-ttu-id="d79a5-114">À compter de .NET Core 2.1, l’interface CLI .NET fournit des commandes qui vous permettent de répertorier toutes les versions du SDK et du Runtime installées sur votre machine.</span><span class="sxs-lookup"><span data-stu-id="d79a5-114">Starting with .NET Core 2.1, the .NET CLI has options you can use to list the versions of the SDK and runtime that are installed on your machine.</span></span>  <span data-ttu-id="d79a5-115">Utilisez [`dotnet --list-sdks`](../tools/dotnet.md#options) pour afficher la liste des kits de développement logiciel (SDK) installés sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d79a5-115">Use [`dotnet --list-sdks`](../tools/dotnet.md#options) to see the list of SDKs installed on your machine.</span></span> <span data-ttu-id="d79a5-116">Utilisez [`dotnet --list-runtimes`](../tools/dotnet.md#options) pour afficher la liste des runtimes installés sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d79a5-116">Use [`dotnet --list-runtimes`](../tools/dotnet.md#options) to see the list of runtimes installed on your machine.</span></span> <span data-ttu-id="d79a5-117">Pour plus d’informations, consultez [Comment vérifier que .net Core est déjà installé](how-to-detect-installed-versions.md).</span><span class="sxs-lookup"><span data-stu-id="d79a5-117">For more information, see [How to check that .NET Core is already installed](how-to-detect-installed-versions.md).</span></span>

## <a name="uninstall-net-core"></a><span data-ttu-id="d79a5-118">Désinstaller .NET Core</span><span class="sxs-lookup"><span data-stu-id="d79a5-118">Uninstall .NET Core</span></span>

::: zone pivot="os-windows"

<span data-ttu-id="d79a5-119">.NET Core utilise la boîte de dialogue **applications Windows &** pour supprimer les versions du runtime et du kit de développement logiciel (SDK) .net core.</span><span class="sxs-lookup"><span data-stu-id="d79a5-119">.NET Core uses the Windows **Apps & features** dialog to remove versions of the .NET Core runtime and SDK.</span></span> <span data-ttu-id="d79a5-120">La figure suivante illustre la boîte de dialogue **applications & fonctionnalités** .</span><span class="sxs-lookup"><span data-stu-id="d79a5-120">The following figure shows the **Apps & features** dialog.</span></span> <span data-ttu-id="d79a5-121">Vous pouvez rechercher le **Kit de développement logiciel (SDK) principal** pour filtrer et afficher les versions installées de .net core.</span><span class="sxs-lookup"><span data-stu-id="d79a5-121">You can search for **core sdk** to filter and show installed versions of .NET Core.</span></span>

![Ajout/Suppression de programmes pour supprimer .NET Core](./media/remove-runtime-sdk-versions/programs-and-features.png)

<span data-ttu-id="d79a5-123">Sélectionnez la version que vous souhaitez supprimer de votre machine et cliquez sur **Désinstaller**.</span><span class="sxs-lookup"><span data-stu-id="d79a5-123">Select any versions you want to remove from your machine and click **Uninstall**.</span></span>

::: zone-end

::: zone pivot="os-linux"

<span data-ttu-id="d79a5-124">Sur Linux, il y a davantage d’options pour désinstaller le SDK ou le Runtime .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d79a5-124">There are more options to uninstall .NET Core (either SDK or runtime) on Linux.</span></span> <span data-ttu-id="d79a5-125">La meilleure méthode pour désinstaller .NET Core est de reprendre celle que vous aviez utilisée pour installer .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d79a5-125">The best way for you to uninstall .NET Core is to mirror the action you used to install .NET Core.</span></span> <span data-ttu-id="d79a5-126">Les différences de processus sont fonction de la distribution que vous avez choisie et de la méthode d’installation.</span><span class="sxs-lookup"><span data-stu-id="d79a5-126">The specifics depend on your chosen distribution and the installation method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d79a5-127">Pour les installations Red Hat, consultez le [guide de prise en main de Red Hat](https://access.redhat.com/documentation/en-us/net_core/2.0/html/getting_started_guide/gs_install_dotnet#install_register_rehel) afin d’obtenir des informations sur l’installation et la désinstallation de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d79a5-127">For Red Hat installations, consult the [Red Hat Getting Started Guide](https://access.redhat.com/documentation/en-us/net_core/2.0/html/getting_started_guide/gs_install_dotnet#install_register_rehel) for information on installing and uninstalling .NET Core.</span></span>

<span data-ttu-id="d79a5-128">À compter de .NET Core 2,1, il n’est pas nécessaire de désinstaller le kit SDK .NET Core lors de sa mise à niveau à l’aide d’un gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="d79a5-128">Starting with .NET Core 2.1, there's no need to uninstall the .NET Core SDK when upgrading it using a package manager.</span></span> <span data-ttu-id="d79a5-129">Les commandes `update` ou `refresh` du gestionnaire de package suppriment automatiquement l’ancienne version une fois l’installation d’une version plus récente terminée.</span><span class="sxs-lookup"><span data-stu-id="d79a5-129">The package manager `update` or `refresh` commands will automatically remove the older version upon the successful installation of a newer version.</span></span>

<span data-ttu-id="d79a5-130">Si vous avez utilisé un gestionnaire de package pour installer .NET Core, réutilisez-le pour désinstaller le SDK ou le Runtime .NET.</span><span class="sxs-lookup"><span data-stu-id="d79a5-130">If you installed .NET Core using a package manager, you use that same package manager to uninstall .NET SDK or runtime.</span></span> <span data-ttu-id="d79a5-131">Les installations .NET Core prennent en charge la plupart des gestionnaires de package courants.</span><span class="sxs-lookup"><span data-stu-id="d79a5-131">.NET Core installations support most popular package managers.</span></span> <span data-ttu-id="d79a5-132">Consultez la documentation du gestionnaire de package de votre distribution pour obtenir une syntaxe précise dans votre environnement :</span><span class="sxs-lookup"><span data-stu-id="d79a5-132">Consult the documentation for your distribution's package manager for the precise syntax in your environment:</span></span>

- <span data-ttu-id="d79a5-133">[apt-get(8)](https://linux.die.net/man/8/apt-get) est utilisé sur les systèmes Debian, y compris Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d79a5-133">[apt-get(8)](https://linux.die.net/man/8/apt-get) is used by Debian based systems, including Ubuntu.</span></span>
- <span data-ttu-id="d79a5-134">[yum(8)](https://linux.die.net/man/8/yum) est utilisé sur les systèmes Fedora, CentOS et Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="d79a5-134">[yum(8)](https://linux.die.net/man/8/yum) is used on Fedora, CentOS, and Oracle Linux.</span></span>
- <span data-ttu-id="d79a5-135">[zypper(8)](https://en.opensuse.org/SDB:Zypper_manual_(plain)) est utilisé sur les systèmes openSUSE et SLES (SUSE Linux Enterprise System).</span><span class="sxs-lookup"><span data-stu-id="d79a5-135">[zypper(8)](https://en.opensuse.org/SDB:Zypper_manual_(plain)) is used on openSUSE and SUSE Linux Enterprise System (SLES).</span></span>
- <span data-ttu-id="d79a5-136">[dnf(8)](https://dnf.readthedocs.io/en/latest/command_ref.html) est utilisé sur les systèmes Fedora.</span><span class="sxs-lookup"><span data-stu-id="d79a5-136">[dnf(8)](https://dnf.readthedocs.io/en/latest/command_ref.html) is used on Fedora.</span></span>

<span data-ttu-id="d79a5-137">Dans presque tous les cas, la commande de suppression d’un package est `remove`.</span><span class="sxs-lookup"><span data-stu-id="d79a5-137">In almost all cases, the command to remove a package is `remove`.</span></span>

<span data-ttu-id="d79a5-138">Avec la plupart des gestionnaires de package, le nom du package utilisé pour installer le SDK .NET Core est `dotnet-sdk`, suivi du numéro de version.</span><span class="sxs-lookup"><span data-stu-id="d79a5-138">The package name for the .NET Core SDK installation for most package managers is `dotnet-sdk`, followed by the version number.</span></span> <span data-ttu-id="d79a5-139">À partir de la version 2.1.300 du SDK .NET Core et de la version `2.1` du Runtime, il suffit d’indiquer les numéros des versions principale et mineure. Par exemple, le SDK .NET Core version 2.1.300 peut être référencé en tant que package `dotnet-sdk-2.1`.</span><span class="sxs-lookup"><span data-stu-id="d79a5-139">Starting with the version 2.1.300 of the .NET Core SDK and version `2.1` of the runtime, only the major and minor version numbers are necessary: for example, the .NET Core SDK version 2.1.300 can be referenced as the package `dotnet-sdk-2.1`.</span></span> <span data-ttu-id="d79a5-140">Pour les versions antérieures, la chaîne de version complète doit être indiquée. Par exemple, le SDK .NET Core version 2.1.200 doit être référencé par `dotnet-sdk-2.1.200`.</span><span class="sxs-lookup"><span data-stu-id="d79a5-140">Prior versions require the entire version string: for example, `dotnet-sdk-2.1.200` would be required for version 2.1.200 of the .NET Core SDK.</span></span>

<span data-ttu-id="d79a5-141">Sur les machines où est installé le Runtime uniquement, sans le SDK, le nom du package est `dotnet-runtime-<version>` pour le Runtime .NET Core, et `aspnetcore-runtime-<version>` pour la pile de Runtime entière.</span><span class="sxs-lookup"><span data-stu-id="d79a5-141">For machines that have installed only the runtime, and not the SDK, the package name is `dotnet-runtime-<version>` for the .NET Core runtime, and `aspnetcore-runtime-<version>` for the entire runtime stack.</span></span>

<span data-ttu-id="d79a5-142">Les installations de .NET Core antérieures à 2,0 n’ont pas désinstallé l’application hôte lors de la désinstallation du kit de développement logiciel (SDK) à l’aide du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="d79a5-142">.NET Core installations earlier than 2.0 didn't uninstall the host application when the SDK was uninstalled using the package manager.</span></span> <span data-ttu-id="d79a5-143">Avec `apt-get`, la commande est la suivante :</span><span class="sxs-lookup"><span data-stu-id="d79a5-143">Using `apt-get`, the command is:</span></span>

```bash
apt-get remove dotnet-host
```

<span data-ttu-id="d79a5-144">Notez qu’aucune version n’est attachée `dotnet-host`à.</span><span class="sxs-lookup"><span data-stu-id="d79a5-144">Note that there's no version attached to `dotnet-host`.</span></span>

<span data-ttu-id="d79a5-145">Si vous avez effectué l’installation à l’aide d’un tarball, vous devez supprimer .NET Core manuellement.</span><span class="sxs-lookup"><span data-stu-id="d79a5-145">If you installed using a tarball, you must remove .NET Core using the manual method.</span></span>

<span data-ttu-id="d79a5-146">Sur Linux, vous devez supprimer les kits de développement logiciel (SDK) et les runtimes séparément, en supprimant les répertoires avec version.</span><span class="sxs-lookup"><span data-stu-id="d79a5-146">On Linux, you must remove the SDKs and runtimes separately, by removing the versioned directories.</span></span> <span data-ttu-id="d79a5-147">Leur suppression supprime le kit de développement logiciel (SDK) et le runtime du disque.</span><span class="sxs-lookup"><span data-stu-id="d79a5-147">Removing them deletes the SDK and runtime from disk.</span></span> <span data-ttu-id="d79a5-148">Par exemple, pour supprimer la version 1.0.1 du SDK et du Runtime, utilisez les commandes bash suivantes :</span><span class="sxs-lookup"><span data-stu-id="d79a5-148">For example, to remove the 1.0.1 SDK and runtime, you would use the following bash commands:</span></span>

```bash
version="1.0.1"
sudo rm -rf /usr/local/share/dotnet/sdk/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.NETCore.App/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.All/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.App/$version
sudo rm -rf /usr/local/share/dotnet/host/fxr/$version
```

<span data-ttu-id="d79a5-149">Les répertoires parents du SDK et du Runtime sont répertoriés dans la sortie à l’aide des commandes `dotnet --list-sdks` et `dotnet --list-runtimes`, comme illustré plus haut.</span><span class="sxs-lookup"><span data-stu-id="d79a5-149">The parent directories for the SDK and runtime are listed in the output from the `dotnet --list-sdks` and `dotnet --list-runtimes` command, as shown in the earlier table.</span></span>

::: zone-end

::: zone pivot="os-macos"

<span data-ttu-id="d79a5-150">Sur Mac, vous devez supprimer les kits de développement logiciel (SDK) et les runtimes séparément, en supprimant les répertoires avec version.</span><span class="sxs-lookup"><span data-stu-id="d79a5-150">On Mac, you must remove the SDKs and runtimes separately, by removing the versioned directories.</span></span> <span data-ttu-id="d79a5-151">Leur suppression supprime le kit de développement logiciel (SDK) et le runtime du disque.</span><span class="sxs-lookup"><span data-stu-id="d79a5-151">Removing them deletes the SDK and runtime from disk.</span></span> <span data-ttu-id="d79a5-152">Par exemple, pour supprimer la version 1.0.1 du SDK et du Runtime, utilisez les commandes bash suivantes :</span><span class="sxs-lookup"><span data-stu-id="d79a5-152">For example, to remove the 1.0.1 SDK and runtime, you would use the following bash commands:</span></span>

```bash
version="1.0.1"
sudo rm -rf /usr/local/share/dotnet/sdk/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.NETCore.App/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.All/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.App/$version
sudo rm -rf /usr/local/share/dotnet/host/fxr/$version
```

<span data-ttu-id="d79a5-153">Les répertoires parents du SDK et du Runtime sont répertoriés dans la sortie à l’aide des commandes `dotnet --list-sdks` et `dotnet --list-runtimes`, comme illustré plus haut.</span><span class="sxs-lookup"><span data-stu-id="d79a5-153">The parent directories for the SDK and runtime are listed in the output from the `dotnet --list-sdks` and `dotnet --list-runtimes` command, as shown in the earlier table.</span></span>

::: zone-end

## <a name="net-core-uninstall-tool"></a><span data-ttu-id="d79a5-154">Outil de désinstallation de .NET Core</span><span class="sxs-lookup"><span data-stu-id="d79a5-154">.NET Core Uninstall Tool</span></span>

<span data-ttu-id="d79a5-155">L' [outil de désinstallation de .net Core](../additional-tools/uninstall-tool.md) () vous permet de supprimer des kits de développement logiciel (`dotnet-core-uninstall`SDK) .net Core et des runtimes d’un système.</span><span class="sxs-lookup"><span data-stu-id="d79a5-155">The [.NET Core Uninstall Tool](../additional-tools/uninstall-tool.md) (`dotnet-core-uninstall`) lets you remove .NET Core SDKs and runtimes from a system.</span></span> <span data-ttu-id="d79a5-156">Une collection d’options est disponible pour spécifier les versions à désinstaller.</span><span class="sxs-lookup"><span data-stu-id="d79a5-156">A collection of options is available to specify which versions should be uninstalled.</span></span>

## <a name="visual-studio-dependency-on-net-core-sdk-versions"></a><span data-ttu-id="d79a5-157">Dépendance Visual Studio sur les versions de kit SDK .NET Core</span><span class="sxs-lookup"><span data-stu-id="d79a5-157">Visual Studio dependency on .NET Core SDK versions</span></span>

<span data-ttu-id="d79a5-158">Avant Visual Studio 2019 version 16,3, les programmes d’installation Visual Studio appelaient le programme d’installation de kit SDK .NET Core autonome.</span><span class="sxs-lookup"><span data-stu-id="d79a5-158">Before Visual Studio 2019 version 16.3, Visual Studio installers called the standalone .NET Core SDK installer.</span></span> <span data-ttu-id="d79a5-159">Par conséquent, les versions du kit de développement logiciel (SDK) s’affichent dans la boîte de dialogue **applications Windows & fonctionnalités** .</span><span class="sxs-lookup"><span data-stu-id="d79a5-159">As a result, the SDK versions appear in the Windows **Apps & features** dialog.</span></span> <span data-ttu-id="d79a5-160">La suppression des kits de développement logiciel (SDK) .NET Core qui ont été installés par Visual Studio à l’aide du programme d’installation autonome peut arrêter Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d79a5-160">Removing .NET Core SDKs that were installed by Visual Studio using the standalone installer may break Visual Studio.</span></span> <span data-ttu-id="d79a5-161">Si Visual Studio rencontre des problèmes après avoir désinstallé les kits de développement logiciel (SDK), exécutez la réparation sur cette version spécifique de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d79a5-161">If Visual Studio has problems after you uninstall SDKs, run Repair on that specific version of Visual Studio.</span></span> <span data-ttu-id="d79a5-162">Le tableau suivant présente certaines des dépendances Visual Studio sur les versions de kit SDK .NET Core :</span><span class="sxs-lookup"><span data-stu-id="d79a5-162">The following table shows some of the Visual Studio dependencies on .NET Core SDK versions:</span></span>

| <span data-ttu-id="d79a5-163">Version de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d79a5-163">Visual Studio version</span></span>           | <span data-ttu-id="d79a5-164">Version de kit SDK .NET Core</span><span class="sxs-lookup"><span data-stu-id="d79a5-164">.NET Core SDK version</span></span>          |
|---------------------------------|--------------------------------|
| <span data-ttu-id="d79a5-165">Visual Studio 2019 version 16.2</span><span class="sxs-lookup"><span data-stu-id="d79a5-165">Visual Studio 2019 version 16.2</span></span> | <span data-ttu-id="d79a5-166">Kit SDK .NET Core 2.2.4 XX, 2.1.8 XX</span><span class="sxs-lookup"><span data-stu-id="d79a5-166">.NET Core SDK 2.2.4xx, 2.1.8xx</span></span> |
| <span data-ttu-id="d79a5-167">Visual Studio 2019 version 16.1</span><span class="sxs-lookup"><span data-stu-id="d79a5-167">Visual Studio 2019 version 16.1</span></span> | <span data-ttu-id="d79a5-168">Kit SDK .NET Core 2.2.3 XX, 2.1.7 XX</span><span class="sxs-lookup"><span data-stu-id="d79a5-168">.NET Core SDK 2.2.3xx, 2.1.7xx</span></span> |
| <span data-ttu-id="d79a5-169">Visual Studio 2019 version 16,0</span><span class="sxs-lookup"><span data-stu-id="d79a5-169">Visual Studio 2019 version 16.0</span></span> | <span data-ttu-id="d79a5-170">Kit SDK .NET Core 2.2.2 XX, 2.1.6 XX</span><span class="sxs-lookup"><span data-stu-id="d79a5-170">.NET Core SDK 2.2.2xx, 2.1.6xx</span></span> |
| <span data-ttu-id="d79a5-171">Visual Studio 2017 version 15,9</span><span class="sxs-lookup"><span data-stu-id="d79a5-171">Visual Studio 2017 version 15.9</span></span> | <span data-ttu-id="d79a5-172">Kit SDK .NET Core 2.2.1 XX, 2.1.5 XX</span><span class="sxs-lookup"><span data-stu-id="d79a5-172">.NET Core SDK 2.2.1xx, 2.1.5xx</span></span> |
| <span data-ttu-id="d79a5-173">Visual Studio 2017 version 15.8</span><span class="sxs-lookup"><span data-stu-id="d79a5-173">Visual Studio 2017 version 15.8</span></span> | <span data-ttu-id="d79a5-174">Kit SDK .NET Core 2.1.4 XX</span><span class="sxs-lookup"><span data-stu-id="d79a5-174">.NET Core SDK 2.1.4xx</span></span>          |

<span data-ttu-id="d79a5-175">À compter de Visual Studio 2019 version 16,3, Visual Studio est payant de sa propre copie du kit SDK .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d79a5-175">Starting with Visual Studio 2019 version 16.3, Visual Studio is in charge of its own copy of the .NET Core SDK.</span></span> <span data-ttu-id="d79a5-176">Pour cette raison, vous ne voyez plus ces versions du kit de développement logiciel (SDK) dans la boîte de dialogue **applications & fonctionnalités** .</span><span class="sxs-lookup"><span data-stu-id="d79a5-176">For that reason, you no longer see those SDK versions in the **Apps & features** dialog.</span></span>

## <a name="remove-the-nuget-fallback-folder"></a><span data-ttu-id="d79a5-177">Supprimer le dossier NuGet Fallback</span><span class="sxs-lookup"><span data-stu-id="d79a5-177">Remove the NuGet fallback folder</span></span>

<span data-ttu-id="d79a5-178">Avant le kit de développement logiciel (SDK) .NET Core 3,0, les programmes d’installation kit SDK .NET Core utilisaient un dossier nommé *NuGetFallbackFolder* pour stocker un cache de packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="d79a5-178">Before .NET Core 3.0 SDK, the .NET Core SDK installers used a folder named *NuGetFallbackFolder* to store a cache of NuGet packages.</span></span> <span data-ttu-id="d79a5-179">Ce cache a été utilisé pendant des opérations `dotnet restore` telles `dotnet build /t:Restore`que ou.</span><span class="sxs-lookup"><span data-stu-id="d79a5-179">This cache was used during operations such as `dotnet restore` or `dotnet build /t:Restore`.</span></span> <span data-ttu-id="d79a5-180">Le *NuGetFallbackFolder* se trouve dans *C:\Program Files\dotnet\sdk* sur Windows et sur */usr/local/share/dotnet/SDK* sur MacOS.</span><span class="sxs-lookup"><span data-stu-id="d79a5-180">The *NuGetFallbackFolder* is located at *C:\Program Files\dotnet\sdk* on Windows and at */usr/local/share/dotnet/sdk* on macOS.</span></span>

<span data-ttu-id="d79a5-181">Vous souhaiterez peut-être supprimer ce dossier, si :</span><span class="sxs-lookup"><span data-stu-id="d79a5-181">You may want to remove this folder, if:</span></span>

- <span data-ttu-id="d79a5-182">Vous développez uniquement à l’aide du kit de développement logiciel (SDK) .NET Core 3,0 ou des versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="d79a5-182">You're only developing using .NET Core 3.0 SDK or later versions.</span></span>
- <span data-ttu-id="d79a5-183">Vous développez à l’aide de kit SDK .NET Core versions antérieures à 3,0, mais vous pouvez travailler en ligne.</span><span class="sxs-lookup"><span data-stu-id="d79a5-183">You're developing using .NET Core SDK versions earlier than 3.0, but you can work online.</span></span>

<span data-ttu-id="d79a5-184">Si vous souhaitez supprimer le dossier NuGet Fallback, vous pouvez le supprimer, mais vous aurez besoin de privilèges d’administrateur pour le faire.</span><span class="sxs-lookup"><span data-stu-id="d79a5-184">If you want to remove the NuGet fallback folder, you can delete it, but you'll need admin privileges to do so.</span></span>

<span data-ttu-id="d79a5-185">Il n’est pas recommandé de supprimer le dossier *dotnet* .</span><span class="sxs-lookup"><span data-stu-id="d79a5-185">It's not recommended to delete the *dotnet* folder.</span></span> <span data-ttu-id="d79a5-186">Cela entraînerait la suppression de tous les outils globaux que vous avez déjà installés.</span><span class="sxs-lookup"><span data-stu-id="d79a5-186">Doing so would remove any global tools you've previously installed.</span></span> <span data-ttu-id="d79a5-187">En outre, sur Windows :</span><span class="sxs-lookup"><span data-stu-id="d79a5-187">Also, on Windows:</span></span>

- <span data-ttu-id="d79a5-188">Vous allez rompre la version 16,3 et les versions ultérieures de Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="d79a5-188">You'll break Visual Studio 2019 version 16.3 and later versions.</span></span> <span data-ttu-id="d79a5-189">Vous pouvez exécuter la **réparation** pour récupérer.</span><span class="sxs-lookup"><span data-stu-id="d79a5-189">You can run **Repair** to recover.</span></span>
- <span data-ttu-id="d79a5-190">S’il existe kit SDK .NET Core entrées dans la boîte de dialogue **applications & fonctionnalités** , elles seront orphelines.</span><span class="sxs-lookup"><span data-stu-id="d79a5-190">If there are .NET Core SDK entries in the **Apps & features** dialog, they'll be orphaned.</span></span>