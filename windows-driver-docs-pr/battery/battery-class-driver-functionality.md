---
title: 电池类驱动程序功能
description: 电池类驱动程序功能
ms.assetid: cd7536d9-bcf1-4674-8ebf-af2b888a0f0a
keywords:
- 电池类驱动程序 WDK，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b724319a72a710bfb3efe7e98bae3620fabf517
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364770"
---
# <a name="battery-class-driver-functionality"></a>电池类驱动程序功能


## <span id="ddk_battery_class_driver_functionality_dg"></span><span id="DDK_BATTERY_CLASS_DRIVER_FUNCTIONALITY_DG"></span>


内核模式下电池类驱动程序，battc.sys，提供独立于设备的电池支持和导出的所有特定于设备的电池 miniclass 驱动程序用于支持例程。

电池类驱动程序负责 miniclass 驱动程序的以下任务：

-   执行大部分 miniclass 驱动程序初始化，包括为 miniclass 驱动程序的类数据分配系统资源和空间

-   处理设备控制 Irp ([**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control))，用于指定电池类 Ioctl。 （请参阅适用于这些 Ioctl 有关的信息的 Microsoft Windows SDK。）

-   序列化到电池设备请求

-   管理操作系统的 DC 电源策略

-   如果卸载 miniclass 驱动程序，则，释放系统资源

-   处理某些标准电池 WMI 类

请参阅[电池 Miniclass 驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_battery/)有关电池类驱动程序将导出到电池 miniclass 驱动程序的例程的说明。

 

 




