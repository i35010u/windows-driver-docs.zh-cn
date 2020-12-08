---
title: 示例 WDM 设备对象
description: 示例 WDM 设备对象
keywords:
- 设备对象 WDK 内核，示例
- 鼠标 WDK 内核
- 键盘 WDK 内核
- 功能设备对象 WDK 内核
- FDO WDK 内核
- 物理设备对象 WDK 内核
- PDOs WDK 内核
- 筛选 DOs WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba28e3be716938d20e04ca036198102d761f9255
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793581"
---
# <a name="example-wdm-device-objects"></a>示例 WDM 设备对象





下图说明了代表键盘和鼠标设备的设备对象，该图中显示的是键盘和鼠标设备，其中显示了 [键盘和鼠标的硬件配置](sample-device-and-driver-configuration.md#keyboard-and-mouse-hardware-configurations)。 图中所示的键盘和鼠标驱动程序图说明了 [键盘和鼠标驱动程序层](sample-device-and-driver-configuration.md#keyboard-and-mouse-driver-layers) 通过调用 i/o 支持例程 ([**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)) 来创建这些设备对象。

![键盘和鼠标设备对象](images/2sampdos.png)

对于键盘和鼠标设备，它们各自的端口和类驱动程序都创建设备对象。 端口驱动程序创建 (PDO) 的物理设备对象来表示物理端口。 每个类驱动程序都创建自己的功能设备对象 (FDO) ，以将键盘或鼠标设备表示为 i/o 请求的目标。

每个类驱动程序都调用 i/o 支持例程，以获取指向下一级驱动程序的设备对象的指针，因此，该类驱动程序可以将自身链接到该驱动程序，这是端口驱动程序。 然后，类驱动程序可以将 i/o 请求发送到表示其物理设备的目标 PDO 的端口驱动程序。

添加到配置的可选筛选器驱动程序将创建筛选器设备对象 (筛选器执行) 。 与类驱动程序一样，可选筛选器驱动程序将自身链接到设备堆栈中的下一个较低的驱动程序，并将目标 PDO 的 i/o 请求发送到下一个较低版本的驱动程序。

如上图所示，每个端口 [驱动程序都](sample-device-and-driver-configuration.md#keyboard-and-mouse-driver-layers) 是一个 (最低级别) 驱动程序的总线，因此，生成中断的设备的每个端口驱动程序都必须设置中断对象 () 并注册 ISR。

双设备端口驱动程序，如 [键盘和鼠标硬件配置](sample-device-and-driver-configuration.md#keyboard-and-mouse-hardware-configurations) 中显示的键盘和辅助设备控制器的 i8042 驱动程序，如果每个设备使用不同的中断向量，则必须设置特定于设备的 *中断对象* 。 写入此类驱动程序时，可以为每个设备实现单独的 Isr，或者为这两个设备实施单个 ISR。

 

