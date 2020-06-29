---
ms.openlocfilehash: 92210f6becb5a5a43893ee0fd51ef51e2ddd7f8d
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325223"
---
### <a name="kestrel-http2-disabled-over-tls-on-incompatible-windows-versions"></a><span data-ttu-id="2db7d-101">Kestrel : HTTP/2 désactivé sur TLS sur des versions de Windows incompatibles</span><span class="sxs-lookup"><span data-stu-id="2db7d-101">Kestrel: HTTP/2 disabled over TLS on incompatible Windows versions</span></span>

<span data-ttu-id="2db7d-102">Pour activer HTTP/2 sur le protocole TLS (Transport Layer Security) sur Windows, deux conditions doivent être remplies :</span><span class="sxs-lookup"><span data-stu-id="2db7d-102">To enable HTTP/2 over Transport Layer Security (TLS) on Windows, two requirements need to be met:</span></span>

- <span data-ttu-id="2db7d-103">La prise en charge de la négociation de protocole de couche application (ALPN), disponible à partir de Windows 8.1 et de Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="2db7d-103">Application-Layer Protocol Negotiation (ALPN) support, which is available starting with Windows 8.1 and Windows Server 2012 R2.</span></span>
- <span data-ttu-id="2db7d-104">Un ensemble de chiffrements compatibles avec HTTP/2, disponible à partir de Windows 10 et Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="2db7d-104">A set of ciphers compatible with HTTP/2, which is available starting with Windows 10 and Windows Server 2016.</span></span>

<span data-ttu-id="2db7d-105">Par conséquent, le comportement de Kestrel lorsque HTTP/2 sur TLS est configuré est devenu :</span><span class="sxs-lookup"><span data-stu-id="2db7d-105">As such, Kestrel's behavior when HTTP/2 over TLS is configured has changed to:</span></span>

- <span data-ttu-id="2db7d-106">Rétrograder à `Http1` et enregistrer un message au `Information` niveau lorsque [ListenOptions. HttpProtocols](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.httpprotocols) a la valeur `Http1AndHttp2` .</span><span class="sxs-lookup"><span data-stu-id="2db7d-106">Downgrade to `Http1` and log a message at the `Information` level when [ListenOptions.HttpProtocols](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.httpprotocols) is set to `Http1AndHttp2`.</span></span> <span data-ttu-id="2db7d-107">`Http1AndHttp2` est la valeur par défaut de `ListenOptions.HttpProtocols`.</span><span class="sxs-lookup"><span data-stu-id="2db7d-107">`Http1AndHttp2` is the default value for `ListenOptions.HttpProtocols`.</span></span>
- <span data-ttu-id="2db7d-108">Lève une `NotSupportedException` lorsque `ListenOptions.HttpProtocols` a la valeur `Http2` .</span><span class="sxs-lookup"><span data-stu-id="2db7d-108">Throw a `NotSupportedException` when `ListenOptions.HttpProtocols` is set to `Http2`.</span></span>

<span data-ttu-id="2db7d-109">Pour plus d’informations, consultez émettre [dotnet/aspnetcore # 23068](https://github.com/dotnet/aspnetcore/issues/23068).</span><span class="sxs-lookup"><span data-stu-id="2db7d-109">For discussion, see issue [dotnet/aspnetcore#23068](https://github.com/dotnet/aspnetcore/issues/23068).</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="2db7d-110">Version introduite</span><span class="sxs-lookup"><span data-stu-id="2db7d-110">Version introduced</span></span>

<span data-ttu-id="2db7d-111">ASP.NET Core 5,0 Preview 7</span><span class="sxs-lookup"><span data-stu-id="2db7d-111">ASP.NET Core 5.0 Preview 7</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="2db7d-112">Ancien comportement</span><span class="sxs-lookup"><span data-stu-id="2db7d-112">Old behavior</span></span>

<span data-ttu-id="2db7d-113">Le tableau suivant décrit le comportement lorsque le protocole HTTP/2 sur TLS est configuré.</span><span class="sxs-lookup"><span data-stu-id="2db7d-113">The following table outlines the behavior when HTTP/2 over TLS is configured.</span></span>

| <span data-ttu-id="2db7d-114">Protocoles</span><span class="sxs-lookup"><span data-stu-id="2db7d-114">Protocols</span></span> | <span data-ttu-id="2db7d-115">Windows 7,</span><span class="sxs-lookup"><span data-stu-id="2db7d-115">Windows 7,</span></span><br /><span data-ttu-id="2db7d-116">Windows Server 2008 R2,</span><span class="sxs-lookup"><span data-stu-id="2db7d-116">Windows Server 2008 R2,</span></span><br /><span data-ttu-id="2db7d-117">ou version antérieure</span><span class="sxs-lookup"><span data-stu-id="2db7d-117">or earlier</span></span> | <span data-ttu-id="2db7d-118">Windows 8,</span><span class="sxs-lookup"><span data-stu-id="2db7d-118">Windows 8,</span></span><br /><span data-ttu-id="2db7d-119">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="2db7d-119">Windows Server 2012</span></span> | <span data-ttu-id="2db7d-120">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="2db7d-120">Windows 8.1,</span></span><br /><span data-ttu-id="2db7d-121">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2db7d-121">Windows Server 2012 R2</span></span> | <span data-ttu-id="2db7d-122">Windows 10,</span><span class="sxs-lookup"><span data-stu-id="2db7d-122">Windows 10,</span></span><br /><span data-ttu-id="2db7d-123">Windows Server 2016,</span><span class="sxs-lookup"><span data-stu-id="2db7d-123">Windows Server 2016,</span></span><br /><span data-ttu-id="2db7d-124">ou plus récent</span><span class="sxs-lookup"><span data-stu-id="2db7d-124">or newer</span></span> |
|---------------|-----------------------------------------------|--------------------------------|-------------------------------------|------------------------------------------|
| `Http2`         | <span data-ttu-id="2db7d-125">Lever`NotSupportedException`</span><span class="sxs-lookup"><span data-stu-id="2db7d-125">Throw `NotSupportedException`</span></span>                   | <span data-ttu-id="2db7d-126">Erreur lors de la négociation TLS</span><span class="sxs-lookup"><span data-stu-id="2db7d-126">Error during TLS handshake</span></span>     | <span data-ttu-id="2db7d-127">Erreur lors de la négociation TLS&ast;</span><span class="sxs-lookup"><span data-stu-id="2db7d-127">Error during TLS handshake &ast;</span></span>     | <span data-ttu-id="2db7d-128">Aucune erreur</span><span class="sxs-lookup"><span data-stu-id="2db7d-128">No error</span></span> |
| `Http1AndHttp2` | <span data-ttu-id="2db7d-129">Rétrograder à`Http1`</span><span class="sxs-lookup"><span data-stu-id="2db7d-129">Downgrade to `Http1`</span></span>                    | <span data-ttu-id="2db7d-130">Rétrograder à`Http1`</span><span class="sxs-lookup"><span data-stu-id="2db7d-130">Downgrade to `Http1`</span></span>     | <span data-ttu-id="2db7d-131">Erreur lors de la négociation TLS&ast;</span><span class="sxs-lookup"><span data-stu-id="2db7d-131">Error during TLS handshake &ast;</span></span>     | <span data-ttu-id="2db7d-132">Aucune erreur</span><span class="sxs-lookup"><span data-stu-id="2db7d-132">No error</span></span> |

<span data-ttu-id="2db7d-133">&ast;Configurez des suites de chiffrement compatibles pour activer ces scénarios.</span><span class="sxs-lookup"><span data-stu-id="2db7d-133">&ast; Configure compatible cipher suites to enable these scenarios.</span></span>

#### <a name="new-behavior"></a><span data-ttu-id="2db7d-134">Nouveau comportement</span><span class="sxs-lookup"><span data-stu-id="2db7d-134">New behavior</span></span>

<span data-ttu-id="2db7d-135">Le tableau suivant décrit le comportement lorsque le protocole HTTP/2 sur TLS est configuré.</span><span class="sxs-lookup"><span data-stu-id="2db7d-135">The following table outlines the behavior when HTTP/2 over TLS is configured.</span></span>

| <span data-ttu-id="2db7d-136">Protocoles</span><span class="sxs-lookup"><span data-stu-id="2db7d-136">Protocols</span></span> | <span data-ttu-id="2db7d-137">Windows 7,</span><span class="sxs-lookup"><span data-stu-id="2db7d-137">Windows 7,</span></span><br /><span data-ttu-id="2db7d-138">Windows Server 2008 R2,</span><span class="sxs-lookup"><span data-stu-id="2db7d-138">Windows Server 2008 R2,</span></span><br /><span data-ttu-id="2db7d-139">ou version antérieure</span><span class="sxs-lookup"><span data-stu-id="2db7d-139">or earlier</span></span> | <span data-ttu-id="2db7d-140">Windows 8,</span><span class="sxs-lookup"><span data-stu-id="2db7d-140">Windows 8,</span></span><br /><span data-ttu-id="2db7d-141">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="2db7d-141">Windows Server 2012</span></span> | <span data-ttu-id="2db7d-142">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="2db7d-142">Windows 8.1,</span></span><br /><span data-ttu-id="2db7d-143">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2db7d-143">Windows Server 2012 R2</span></span> | <span data-ttu-id="2db7d-144">Windows 10,</span><span class="sxs-lookup"><span data-stu-id="2db7d-144">Windows 10,</span></span><br /><span data-ttu-id="2db7d-145">Windows Server 2016,</span><span class="sxs-lookup"><span data-stu-id="2db7d-145">Windows Server 2016,</span></span><br /><span data-ttu-id="2db7d-146">ou plus récent</span><span class="sxs-lookup"><span data-stu-id="2db7d-146">or newer</span></span> |
|---------------|-----------------------------------------------|--------------------------------|-------------------------------------|------------------------------------------|
| `Http2`         | <span data-ttu-id="2db7d-147">Lever`NotSupportedException`</span><span class="sxs-lookup"><span data-stu-id="2db7d-147">Throw `NotSupportedException`</span></span>                   | <span data-ttu-id="2db7d-148">Lever`NotSupportedException`</span><span class="sxs-lookup"><span data-stu-id="2db7d-148">Throw `NotSupportedException`</span></span>     | <span data-ttu-id="2db7d-149">Lever `NotSupportedException`&ast;&ast;</span><span class="sxs-lookup"><span data-stu-id="2db7d-149">Throw `NotSupportedException` &ast;&ast;</span></span>     | <span data-ttu-id="2db7d-150">Aucune erreur</span><span class="sxs-lookup"><span data-stu-id="2db7d-150">No error</span></span> |
| `Http1AndHttp2` | <span data-ttu-id="2db7d-151">Rétrograder à`Http1`</span><span class="sxs-lookup"><span data-stu-id="2db7d-151">Downgrade to `Http1`</span></span>                    | <span data-ttu-id="2db7d-152">Rétrograder à`Http1`</span><span class="sxs-lookup"><span data-stu-id="2db7d-152">Downgrade to `Http1`</span></span>     | <span data-ttu-id="2db7d-153">Rétrograder à `Http1`&ast;&ast;</span><span class="sxs-lookup"><span data-stu-id="2db7d-153">Downgrade to `Http1` &ast;&ast;</span></span>     | <span data-ttu-id="2db7d-154">Aucune erreur</span><span class="sxs-lookup"><span data-stu-id="2db7d-154">No error</span></span> |

<span data-ttu-id="2db7d-155">&ast;&ast;Configurez les suites de chiffrement compatibles et définissez le commutateur de contexte d’application `Microsoft.AspNetCore.Server.Kestrel.EnableWindows81Http2` sur `true` pour activer ces scénarios.</span><span class="sxs-lookup"><span data-stu-id="2db7d-155">&ast;&ast; Configure compatible cipher suites and set the app context switch `Microsoft.AspNetCore.Server.Kestrel.EnableWindows81Http2` to `true` to enable these scenarios.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="2db7d-156">Motif de modification</span><span class="sxs-lookup"><span data-stu-id="2db7d-156">Reason for change</span></span>

<span data-ttu-id="2db7d-157">Cette modification garantit que les erreurs de compatibilité pour HTTP/2 sur TLS sur des versions plus anciennes de Windows sont exposées le plus tôt et le plus clairement possible.</span><span class="sxs-lookup"><span data-stu-id="2db7d-157">This change ensures compatibility errors for HTTP/2 over TLS on older Windows versions are surfaced as early and as clearly as possible.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="2db7d-158">Action recommandée</span><span class="sxs-lookup"><span data-stu-id="2db7d-158">Recommended action</span></span>

<span data-ttu-id="2db7d-159">Assurez-vous que HTTP/2 sur TLS est désactivé sur les versions de Windows incompatibles.</span><span class="sxs-lookup"><span data-stu-id="2db7d-159">Ensure HTTP/2 over TLS is disabled on incompatible Windows versions.</span></span> <span data-ttu-id="2db7d-160">Windows 8.1 et Windows Server 2012 R2 ne sont pas compatibles, car ils n’ont pas les chiffrements nécessaires par défaut.</span><span class="sxs-lookup"><span data-stu-id="2db7d-160">Windows 8.1 and Windows Server 2012 R2 are incompatible since they lack the necessary ciphers by default.</span></span> <span data-ttu-id="2db7d-161">Toutefois, il est possible de mettre à jour les paramètres de configuration de l’ordinateur pour utiliser les chiffrements compatibles HTTP/2.</span><span class="sxs-lookup"><span data-stu-id="2db7d-161">However, it's possible to update the Computer Configuration settings to use HTTP/2 compatible ciphers.</span></span> <span data-ttu-id="2db7d-162">Pour plus d’informations, voir [suites de chiffrement TLS dans Windows 8.1](/windows/win32/secauthn/tls-cipher-suites-in-windows-8-1).</span><span class="sxs-lookup"><span data-stu-id="2db7d-162">For more information, see [TLS cipher suites in Windows 8.1](/windows/win32/secauthn/tls-cipher-suites-in-windows-8-1).</span></span> <span data-ttu-id="2db7d-163">Une fois configuré, vous devez activer HTTP/2 sur TLS sur Kestrel en définissant le commutateur de contexte d’application `Microsoft.AspNetCore.Server.Kestrel.EnableWindows81Http2` .</span><span class="sxs-lookup"><span data-stu-id="2db7d-163">Once configured, HTTP/2 over TLS on Kestrel must be enabled by setting the app context switch `Microsoft.AspNetCore.Server.Kestrel.EnableWindows81Http2`.</span></span> <span data-ttu-id="2db7d-164">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2db7d-164">For example:</span></span>

```csharp
AppContext.SetSwitch("Microsoft.AspNetCore.Server.Kestrel.EnableWindows81Http2", true);
```

<span data-ttu-id="2db7d-165">Aucune prise en charge sous-jacente n’a changé.</span><span class="sxs-lookup"><span data-stu-id="2db7d-165">No underlying support has changed.</span></span> <span data-ttu-id="2db7d-166">Par exemple, HTTP/2 sur TLS n’a jamais fonctionné sur Windows 8 ou Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="2db7d-166">For example, HTTP/2 over TLS has never worked on Windows 8 or Windows Server 2012.</span></span> <span data-ttu-id="2db7d-167">Cette modification modifie le mode de présentation des erreurs dans ces scénarios non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2db7d-167">This change modifies how errors in these unsupported scenarios are presented.</span></span>

#### <a name="category"></a><span data-ttu-id="2db7d-168">Category</span><span class="sxs-lookup"><span data-stu-id="2db7d-168">Category</span></span>

<span data-ttu-id="2db7d-169">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2db7d-169">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="2db7d-170">API affectées</span><span class="sxs-lookup"><span data-stu-id="2db7d-170">Affected APIs</span></span>

<span data-ttu-id="2db7d-171">Aucune</span><span class="sxs-lookup"><span data-stu-id="2db7d-171">None</span></span>

<!--

#### Affected APIs

Not detectable via API analysis

-->