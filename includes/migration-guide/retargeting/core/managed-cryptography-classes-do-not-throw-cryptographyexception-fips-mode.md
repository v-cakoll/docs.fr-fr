---
ms.openlocfilehash: 2b768047a8b08501a8de4666d240072318427f28
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803458"
---
### <a name="managed-cryptography-classes-do-not-throw-a-cryptographyexception-in-fips-mode"></a>Les classes de chiffrement managées ne lèvent pas d’exception de chiffrement en mode FIPS

|   |   |
|---|---|
|Détails|Dans .NET Framework 4.7.2 et versions antérieures, les classes de fournisseur de chiffrement managées comme <xref:System.Security.Cryptography.SHA256Managed> lèvent une <xref:System.Security.Cryptography.CryptographicException> quand les bibliothèques de chiffrement système sont configurées en mode FIPS. Ces exceptions sont levées parce que les versions managées ne sont pas sous la certification 140-2 FIPS (Federal Information Processing Standards), et dans le but de bloquer les algorithmes de chiffrement qui n’étaient pas considérés comme approuvés selon les règles FIPS.  Étant donné que peu de développeurs ont leurs ordinateurs de développement en mode FIPS, ces exceptions sont fréquemment levées sur les systèmes de production uniquement. Les applications qui ciblent .NET Framework 4.8 et versions ultérieures basculent automatiquement vers la stratégie plus récente et plus souple afin qu’une <xref:System.Security.Cryptography.CryptographicException> ne soit plus levée par défaut dans ces cas précis. Les classes de chiffrement managées redirigent plutôt les opérations de chiffrement vers une bibliothèque de chiffrement système. Ce changement de stratégie supprime efficacement une différence pouvant potentiellement prêter à confusion entre les environnements de développement et les environnements de production, et permet d’exécuter les composants natifs et les composants managés sous la même stratégie de chiffrement.|
|Suggestion|Si ce comportement est indésirable, vous pouvez choisir de ne plus y adhérer et restaurer le comportement précédent pour qu’une <xref:System.Security.Cryptography.CryptographicException> soit levée en mode FIPS en ajoutant le paramètre de configuration [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) suivant dans la section [<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) de votre fichier de configuration d’application :<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.UseLegacyFipsThrow=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>Si votre application cible .NET Framework 4.7.2 ou antérieur, vous pouvez aussi choisir d’adhérer à ce changement en ajoutant le paramètre de configuration [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) suivant dans la section [<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) de votre fichier de configuration d’application :<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Security.Cryptography.UseLegacyFipsThrow=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|Portée|Microsoft Edge|
|Version|4.8|
|Type|Reciblage|
|API affectées|<ul><li><xref:System.Security.Cryptography.AesManaged?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.MD5Cng?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.MD5CryptoServiceProvider?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RC2CryptoServiceProvider?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RijndaelManaged?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RIPEMD160Managed?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.SHA1Managed?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.SHA256Managed?displayProperty=nameWithType></li></ul>|
