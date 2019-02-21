---
title: 设备属性表示形式 (Windows Server 2003，Windows XP)
description: 设备属性表示形式 （Windows Server 2003、 Windows XP 和 Windows 2000）
ms.assetid: 124172d7-52a4-423c-a1fd-eec554f328d6
keywords:
- 设备属性 WDK 设备安装，表示形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6d874d6075034c3b18bc0fa0c5edf521488d5aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540449"
---
# <a name="device-property-representations-windows-server-2003-windows-xp-and-windows-2000"></a>设备属性表示形式 （Windows Server 2003、 Windows XP 和 Windows 2000）


不支持 Windows Server 2003、 Windows XP 和 Windows 2000[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)该 Windows Vista 和更高版本的 Windows 支持。 但是，大部分[系统定义的设备属性](https://msdn.microsoft.com/library/windows/hardware/ff553413)所包含统一的设备属性模型中具有相应的表示形式，这些早期版本的 Windows 支持。 在这些早期版本的 Windows 中，表示设备属性的方式，，种机制，用于访问属性，依赖于的组件类型和属性类型。 这些表示形式和机制包括：

-   设备属性由系统定义的输入参数中提供的标识符[SetupAPI 函数](setupapi.md)访问的设备属性。

-   设备属性不具有显式表示形式。 但是，与设备属性关联的信息可以通过对安装程序 Api 函数的调用来检索或即插即用 (PnP) 的配置管理器函数。

-   可以通过使用 Windows 注册表函数访问的注册表条目值由表示设备属性。

-   INF 文件条目的值修改设备属性。

以下主题提供有关如何访问 Windows Server 2003、 Windows XP 和 Windows 2000 上的设备属性的信息：

[INF 文件条目的值修改设备属性](inf-file-entry-values-that-modify-device-properties.md)

[使用 SetupAPI 和 Configuration Manager 以访问设备的属性](using-setupapi-and-configuration-manager-to-access-device-properties.md)

**请注意**  为了保持与这些早期版本的 Windows 兼容性，Windows Vista 和更高版本还支持这些机制。 但是，您应使用统一的设备属性模型访问在 Windows Vista 和更高版本上的设备属性。

 

 

 





