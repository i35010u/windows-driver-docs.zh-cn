---
title: 在驱动程序中使用 GUID
description: 在驱动程序中使用 GUID
ms.assetid: b70a2f64-dd7b-4d76-a4cf-dcb60ce0585c
keywords:
- 全局唯一标识符 WDK 内核
- Guid WDK 内核
- 标识符 WDK Guid
- 头文件 WDK Guid
- 内核模式驱动程序 WDK Guid
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0e1fd0ee1470f8d5711473a3e8af6bcace5433c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381639"
---
# <a name="using-guids-in-drivers"></a>在驱动程序中使用 GUID





驱动程序和使用其他系统组件*全局唯一标识符*(Guid) 标识的各种项。 系统组件的项定义 Guid 等[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)、 PnP WMI 事件的事件和静止图像的事件。 驱动程序编写人员可以创建 Guid 项如[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)，自定义 PnP 事件和自定义 WMI 事件。 驱动程序和应用程序包括标头文件，用于定义他们使用的 Guid。

本部分包括以下主题：

[定义和导出新的 Guid](defining-and-exporting-new-guids.md)

[驱动程序代码中包括的 Guid](including-guids-in-driver-code.md)

在用户模式应用程序中使用 Guid 的信息，请参阅 Microsoft Windows SDK 文档。

 

 




