---
title: 移植步骤
description: 移植步骤
ms.assetid: D8B7E534-7CFC-45EC-93E9-4B046598D82B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8912af4f0d2ee87b7460ec0f582cc68486b3857f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845214"
---
# <a name="steps-in-porting"></a>移植步骤


根据驱动程序的类型，移植涉及执行以下步骤：

1.  [移植 DriverEntry 例程](porting-driver-entry.md)并添加代码以创建 WDFDRIVER 对象。
2.  将[AddDevice 例程移植](porting-adddevice-to-evtdriverdeviceadd.md)到[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调，并添加代码以创建 WDFDEVICE 对象。
3.  如果驱动程序支持中断处理，则添加对[中断](porting-interrupt-functionality.md)的支持。

此时，您可以在每次添加之后以任何顺序、测试和调试的顺序执行剩余步骤。 例如，可以通过实现 i/o 队列并使用即插即用和电源管理的框架默认值开始。 调试基本 i/o 支持后，可以添加对更广泛的即插即用和电源管理请求的支持。 其余步骤如下所示：

-   添加对[即插即用和电源管理](porting-pnp-and-power-management-functionality.md)的支持。
-   添加[i/o 支持](porting-i-o-handling.md)。
-   如果设备执行 DMA，则添加对[dma](porting-dma.md)的支持。<sup>†</sup>
-   [端口 WMI 代码](porting-wmi-code.md)。<sup>†</sup>
-   用于[处理框架不代表 KMDF 驱动程序处理的请求的](requests-that-kmdf-does-not-support.md)端口代码。<sup>†</sup>
-   [修改](installation-procedure.md)安装驱动程序的 INF。

†此功能仅适用于内核模式驱动程序框架（KMDF）驱动程序。

除非另行说明，否则本部分中的信息适用于所有类型的驱动程序（PDO、FDO 和筛选器）。 但是，如果要将总线驱动程序（PDO）移植到 KMDF，则还需要移植设备枚举代码。 有关枚举设备的信息，请参阅[枚举总线上的设备](enumerating-the-devices-on-a-bus.md)。

有关描述各种 WDF 对象、方法和事件回调函数映射到常见 WDM 对象和函数的方式的参考信息，请参阅[KMDF 和 WDM 等效项的摘要](summary-of-kmdf-and-wdm-equivalents.md)。

 

 





