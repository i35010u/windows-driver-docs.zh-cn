---
title: 移植步骤
description: 移植步骤
ms.assetid: D8B7E534-7CFC-45EC-93E9-4B046598D82B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9600d83828d16d36e3773a7e4e0d5120c5d531f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391875"
---
# <a name="steps-in-porting"></a>移植步骤


具体取决于驱动程序的类型，移植过程涉及到执行以下步骤：

1.  [端口 DriverEntry 例程](porting-driver-entry.md)并添加代码以创建 WDFDRIVER 对象。
2.  [端口 AddDevice 例程](porting-adddevice-to-evtdriverdeviceadd.md)到[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调，并添加代码以创建 WDFDEVICE 对象。
3.  添加对的支持[中断](porting-interrupt-functionality.md)如果驱动程序支持中断处理。

此时，你可以执行剩余步骤以增量方式和按任意顺序测试和调试每次添加之后。 例如，您可以首先实现 I/O 队列并插和电源管理使用 framework 的默认设置。 调试过的基本 I/O 支持后，可以添加对更广泛即插即用和电源管理请求的支持。 剩余的步骤如下所示：

-   添加对的支持[插和电源管理](porting-pnp-and-power-management-functionality.md)。
-   添加[I/O 支持](porting-i-o-handling.md)。
-   添加对的支持[DMA](porting-dma.md)，则设备将执行 DMA。<sup>†</sup>
-   [WMI 代码移植](porting-wmi-code.md)。<sup>†</sup>
-   代码移植到[处理框架不代表 KMDF 驱动程序处理的请求](requests-that-kmdf-does-not-support.md)。<sup>†</sup>
-   [修订 INF](installation-procedure.md)安装驱动程序。

† 此功能才可用内核模式驱动程序框架 (KMDF) 驱动程序。

但如前所述，在本部分中的信息适用于所有类型的驱动程序 （PDO、 FDO 和筛选器执行操作）。 但是，如果要将迁移到 KMDF 总线驱动程序 (PDO)，您还需要端口设备枚举代码。 有关枚举设备的信息，请参阅[枚举的总线上设备](enumerating-the-devices-on-a-bus.md)。

描述各种 WDF 对象、 方法和事件的回调函数映射到公共 WDM 对象和函数的方法的参考信息，请参阅[KMDF 摘要和 WDM 等效项](summary-of-kmdf-and-wdm-equivalents.md)。

 

 





