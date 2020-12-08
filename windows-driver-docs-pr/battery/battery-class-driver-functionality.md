---
title: 电池类驱动程序功能
description: 电池类驱动程序功能
keywords:
- 电池类驱动程序 WDK，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09029e68579410e1cf2e5012a7151f047345749b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798697"
---
# <a name="battery-class-driver-functionality"></a>电池类驱动程序功能


## <span id="ddk_battery_class_driver_functionality_dg"></span><span id="DDK_BATTERY_CLASS_DRIVER_FUNCTIONALITY_DG"></span>


内核模式电池类驱动程序（battc.sys）提供与设备无关的电池支持和导出支持例程，供所有设备特定电池 miniclass 驱动程序使用。

电池类驱动程序负责 miniclass 驱动程序的以下任务：

-   执行大部分 miniclass 驱动程序初始化，包括为 miniclass 驱动程序的类数据分配系统资源和空间

-   处理设备控制 Irp ([**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md)) 指定电池类 IOCTLs。  (参阅 Microsoft Windows SDK 了解有关这些 IOCTLs 的信息。 ) 

-   将请求序列化到电池设备

-   管理操作系统的 DC 电源策略

-   如果卸载了 miniclass 驱动程序，则释放系统资源

-   处理某些标准电池 WMI 类

有关电池类驱动程序导出到电池 Miniclass 驱动程序的例程的说明，请参阅 [电池 Miniclass 驱动程序例程](/windows-hardware/drivers/ddi/_battery/) 。

 

