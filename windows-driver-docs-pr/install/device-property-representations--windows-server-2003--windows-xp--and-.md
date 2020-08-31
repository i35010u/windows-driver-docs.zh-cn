---
title: Windows Server 2003、Windows XP)  (设备属性表示形式
description: 设备属性表示形式（Windows Server 2003、Windows XP 和 Windows 2000）
ms.assetid: 124172d7-52a4-423c-a1fd-eec554f328d6
keywords:
- 设备属性 WDK 设备安装，表示形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d65fc2df55b0a5e22ab9532873738f68604f2b5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096485"
---
# <a name="device-property-representations-windows-server-2003-windows-xp-and-windows-2000"></a>设备属性表示形式（Windows Server 2003、Windows XP 和 Windows 2000）


Windows Server 2003、Windows XP 和 Windows 2000 不支持 Windows Vista 和更高版本的 Windows 支持的 [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 。 但是，统一设备属性模型中包含的大多数 [系统定义的设备属性](/previous-versions/ff553413(v=vs.85)) 具有这些早期版本的 Windows 支持的相应表示形式。 在这些早期版本的 Windows 上，表示设备属性的方式和用于访问属性的机制取决于组件类型和属性类型。 这些表示形式和机制包括：

-   设备属性由系统定义的标识符表示，该标识符作为输入参数提供给 [setupapi.log 函数](setupapi.md) 以访问设备属性。

-   设备属性没有显式表示形式。 但是，可以通过调用 Setupapi.log 函数或即插即用 (PnP) configuration manager 函数来检索与设备属性相关联的信息。

-   设备属性由可使用 Windows 注册表函数访问的注册表项值表示。

-   INF 文件条目值修改设备属性。

以下主题提供有关如何在 Windows Server 2003、Windows XP 和 Windows 2000 上访问设备属性的信息：

[用于修改设备属性的 INF 文件输入值](inf-file-entry-values-that-modify-device-properties.md)

[使用 SetupAPI 和 Configuration Manager 访问设备属性](using-setupapi-and-configuration-manager-to-access-device-properties.md)

**注意**   为了保持与这些早期版本的 Windows 的兼容性，Windows Vista 及更高版本还支持这些机制。 但是，你应该使用统一设备属性模型来访问 Windows Vista 和更高版本上的设备属性。

 

 

