---
title: 在驱动程序中使用 GUID
description: 在驱动程序中使用 GUID
keywords:
- 全局唯一标识符 WDK 内核
- Guid WDK 内核
- 标识符 WDK Guid
- 标头文件 WDK Guid
- 内核模式驱动程序 WDK，Guid
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42f6c915108554cdee57f0e25143a3839bb4cc66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808671"
---
# <a name="using-guids-in-drivers"></a>在驱动程序中使用 GUID





驱动程序和其他系统组件使用 *全局唯一标识符* (guid) 来识别各种项目。 系统组件为项（如 [设备安装程序类](../install/overview-of-device-setup-classes.md)、PnP 事件、WMI 事件和静态图像事件）定义 guid。 驱动程序编写器可以为项（如 [设备接口类](../install/overview-of-device-interface-classes.md)、自定义 PnP 事件和自定义 WMI 事件）创建 guid。 驱动程序和应用程序包括用于定义它们所使用的 Guid 的标头文件。

本节包括下列主题：

[定义和导出新 GUID](defining-and-exporting-new-guids.md)

[在驱动程序代码中包含 GUID](including-guids-in-driver-code.md)

有关在用户模式应用程序中使用 Guid 的信息，请参阅 Microsoft Windows SDK 文档。

 

