---
title: <mailSettings>, élément (paramètres réseau)
description: L' <mailSettings> élément paramètres réseau configure les options d’envoi de courrier dans la .NET Framework.
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#mailSettings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings
helpviewer_keywords:
- mailSettings element
- <mailSettings> element
ms.assetid: 54f0f153-17e5-4f49-afdc-deadb940c9c1
ms.openlocfilehash: ce7b8564e4ee5ea73d42259612c077420d36645b
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504561"
---
# <a name="mailsettings-element-network-settings"></a>\<mailSettings>, élément (paramètres réseau)
Configure les options d’envoi de courrier.  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<mailSettings>**

## <a name="syntax"></a>Syntaxe  
  
```xml  
<mailSettings>
  <smtp>...</smtp>  
</mailSettings>
```  
  
## <a name="attributes-and-elements"></a>Attributs et éléments  
 Les sections suivantes décrivent des attributs, des éléments enfants et des éléments parents.  
  
### <a name="attributes"></a>Attributs  
 Aucun.  
  
### <a name="child-elements"></a>Éléments enfants  
  
|Attribut|Description|  
|---------------|-----------------|  
|[\<smtp>, Élément (paramètres réseau)](smtp-element-network-settings.md)|Configure les options de protocole de transport de messagerie simple.|  
  
### <a name="parent-elements"></a>Éléments parents  
  
|**Appartient**|**Description**|  
|-----------------|---------------------|  
|[\<system.Net>, Élément (paramètres réseau)](system-net-element-network-settings.md)|Contient des paramètres qui spécifient la manière dont .NET Framework se connecte au réseau.|  
  
## <a name="example"></a>Exemple  
 L’exemple suivant spécifie les paramètres SMTP appropriés pour envoyer des messages électroniques à l’aide des informations d’identification réseau par défaut.  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="Network">  
        <network  
          host="localhost"  
          port="25"  
          defaultCredentials="true"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Voir aussi

- <xref:System.Net.Mail.SmtpClient>
- [Schéma des paramètres réseau](index.md)
