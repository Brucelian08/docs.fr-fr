---
title: '&lt;configuration&gt; élément'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration
helpviewer_keywords:
- <configuration> element
- configuration element
- container tags, <configuration> element
ms.assetid: 2ec1c9dc-2e5c-4ef0-9958-81670ab88449
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: c5146ed8326b12e90d0fe6247b0c4aba3a69dd77
ms.sourcegitcommit: efff8f331fd9467f093f8ab8d23a203d6ecb5b60
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/03/2018
ms.locfileid: "43485779"
---
# <a name="configuration-element"></a>\<configuration > élément

Élément racine de chaque fichier de configuration utilisé par le Common Language Runtime et les applications .NET Framework.

**\<configuration>**

## <a name="syntax"></a>Syntaxe

```xml
<configuration>
  <!-- Configuration settings -->
</configuration>
```

## <a name="attributes"></a>Attributs

Aucun.

## <a name="parent-element"></a>Élément parent

Aucun.

## <a name="child-elements"></a>Éléments enfants

|     | Description |
| --- | ----------- |
| [**\<assemblyBinding >**](~/docs/framework/configure-apps/file-schema/assemblybinding-element-for-configuration.md) | Spécifie la stratégie de liaison de l’assembly au niveau de la configuration.|
| [**\<démarrage >** schéma des paramètres](~/docs/framework/configure-apps/file-schema/startup/index.md) | Tous les éléments du schéma des paramètres de démarrage. |
| [**\<runtime >** schéma des paramètres](~/docs/framework/configure-apps/file-schema/runtime/index.md) | Tous les éléments dans le schéma des paramètres d’exécution. |
| [**\<System.Runtime.Remoting >** schéma des paramètres](https://msdn.microsoft.com/dc2d1e62-9af7-4ca1-99fd-98b93bb4db9e) | Tous les éléments dans le schéma de paramètres de communication à distance. |
| [**\<system.Net >** schéma des paramètres](~/docs/framework/configure-apps/file-schema/network/index.md) | Tous les éléments du schéma des paramètres réseau. |
| [**\<cryptographySettings >** schéma des paramètres](~/docs/framework/configure-apps/file-schema/cryptography/index.md) | Tous les éléments du schéma des paramètres de chiffrement. |
| [**\<configuration >** schéma des Sections](~/docs/framework/configure-apps/file-schema/configuration-sections-schema.md) | Tous les éléments dans le schéma de paramètres de section de configuration. |
| [Schéma des paramètres de trace et de débogage](~/docs/framework/configure-apps/file-schema/trace-debug/index.md) | Tous les éléments du schéma des paramètres de trace et debug. |
| [Schéma de paramètres de Configuration ASP.NET](https://msdn.microsoft.com/library/b5ysx397(v=vs.100).aspx) | Tous les éléments dans le schéma de configuration ASP.NET, qui inclut des éléments de configuration des applications et sites Web ASP.NET. Utilisé dans *Web.config* fichiers. |
| [**\<webServices >** schéma des paramètres](https://msdn.microsoft.com/f84d6d55-1add-4eb7-ae46-33df5833ea2e) | Tous les éléments du schéma des paramètres Web services. |
| [Schéma des paramètres web](~/docs/framework/configure-apps/file-schema/web/index.md) | Tous les éléments du schéma des paramètres Web, qui inclut des éléments pour la configuration d'ASP.NET en vue d'une utilisation avec une application hôte telle qu'IIS. Utilisé dans *aspnet.config* fichiers. |

## <a name="remarks"></a>Notes

Chaque fichier de configuration doit contenir exactement un  **\<configuration >** élément.

## <a name="see-also"></a>Voir aussi

[Schéma de fichier de configuration pour le .NET Framework](~/docs/framework/configure-apps/file-schema/index.md)
