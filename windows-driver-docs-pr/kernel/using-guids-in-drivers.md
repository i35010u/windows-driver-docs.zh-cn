---
title: 在驱动程序中使用 GUID
description: 在驱动程序中使用 GUID
ms.assetid: b70a2f64-dd7b-4d76-a4cf-dcb60ce0585c
keywords:
- 全局唯一标识符 WDK 内核
- Guid WDK 内核
- 标识符 WDK Guid
- 标头文件 WDK Guid
- 内核模式驱动程序 WDK，Guid
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 442f0cc2afc80e910b6d96e3895245576cbb913a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184971"
---
# <a name="using-guids-in-drivers"></a>在驱动程序中使用 GUID





驱动程序和其他系统组件使用 *全局唯一标识符* (guid) 来识别各种项目。 系统组件为项（如 [设备安装程序类](../install/overview-of-device-setup-classes.md)、PnP 事件、WMI 事件和静态图像事件）定义 guid。 驱动程序编写器可以为项（如 [设备接口类](../install/overview-of-device-interface-classes.md)、自定义 PnP 事件和自定义 WMI 事件）创建 guid。 驱动程序和应用程序包括用于定义它们所使用的 Guid 的标头文件。

本节包括下列主题：

[定义和导出新 GUID](defining-and-exporting-new-guids.md)

[在驱动程序代码中包含 GUID](including-guids-in-driver-code.md)

有关在用户模式应用程序中使用 Guid 的信息，请参阅 Microsoft Windows SDK 文档。

 

