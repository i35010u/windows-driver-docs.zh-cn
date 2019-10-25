---
title: 电池类驱动程序功能
description: 电池类驱动程序功能
ms.assetid: cd7536d9-bcf1-4674-8ebf-af2b888a0f0a
keywords:
- 电池类驱动程序 WDK，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f7b110d7992ab71b79cb3d354715dce38eb2ac1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829920"
---
# <a name="battery-class-driver-functionality"></a>电池类驱动程序功能


## <span id="ddk_battery_class_driver_functionality_dg"></span><span id="DDK_BATTERY_CLASS_DRIVER_FUNCTIONALITY_DG"></span>


内核模式电池类驱动程序（battc）提供与设备无关的电池支持和导出支持例程，供所有设备特定的电池 miniclass 驱动程序使用。

电池类驱动程序负责 miniclass 驱动程序的以下任务：

-   执行大部分 miniclass 驱动程序初始化，包括为 miniclass 驱动程序的类数据分配系统资源和空间

-   处理指定 IOCTLs 电池类的设备控制 Irp （[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)）。 （有关这些 IOCTLs 的信息，请参阅 Microsoft Windows SDK。）

-   将请求序列化到电池设备

-   管理操作系统的 DC 电源策略

-   如果卸载了 miniclass 驱动程序，则释放系统资源

-   处理某些标准电池 WMI 类

有关电池类驱动程序导出到电池 Miniclass 驱动程序的例程的说明，请参阅[电池 Miniclass 驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/_battery/)。

 

 




