---
title: 'Comment : obtenir un certificat (WCF)'
ms.date: 03/30/2017
helpviewer_keywords:
- certificates [WCF], obtaining
ms.assetid: d53762fd-15ea-42dc-b0ea-6a6597aa23f7
ms.openlocfilehash: d020f3e97023d07abb572d30dd53896bfec1da46
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597018"
---
# <a name="how-to-obtain-a-certificate-wcf"></a>Comment : obtenir un certificat (WCF)
Pour utiliser l’une des fonctionnalités de Windows Communication Foundation (WCF) de qui utilisent des certificats X. 509, vous devez tout d’abord obtenir des certificats.  
  
### <a name="to-obtain-an-x509-certificate"></a>Pour obtenir un certificat X.509  
  
1. Choisissez l’un des éléments suivants :  
  
    - Achetez un certificat auprès d'une autorité de certification, telle que VeriSign, Inc.  
  
    - Installez votre propre service de certificats et faites en sorte qu'une autorité de certification signe les certificats. Windows Server 2003, Windows 2000 Server, Windows 2000 Server Datacenter et Windows 2000 Datacenter Server incluent tous les services de certificats qui prennent en charge l’infrastructure de clé publique (PKI). Dans Windows Server 2008, utilisez le rôle [services de certificats Active Directory](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731564(v=ws.10)) pour gérer une autorité de certification.  
  
    - Installez votre propre service de certificats et ne faites pas signer les certificats.  
  
    > [!NOTE]
    > Quelle que soit la méthode adoptée, le destinataire de la demande SOAP contenant le certificat X.509 doit approuver ce dernier. Cela signifie que le certificat X.509 ou un émetteur dans la chaîne de certificats se trouve dans le magasin de certificats Personnes de confiance et que le certificat X.509 ne se trouve pas dans le magasin de certificats non fiables.  
  
## <a name="see-also"></a>Voir aussi

- [Working with Certificates](working-with-certificates.md)
- [Guide pratique pour créer des certificats temporaires à utiliser au cours du développement](how-to-create-temporary-certificates-for-use-during-development.md)
