---
title: 示例 WDM 设备对象
description: 示例 WDM 设备对象
ms.assetid: 8da56415-5018-468c-99c7-3969e5c00285
keywords:
- 设备对象 WDK 内核示例
- 鼠标 WDK 内核
- 键盘 WDK 内核
- 功能的设备对象 WDK 内核
- FDO WDK 内核
- 物理设备对象 WDK 内核
- PDOs WDK 内核
- 筛选器 DOs WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73cd60fc30e362259d8721461ba247c2ba264d1a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576956"
---
# <a name="example-wdm-device-objects"></a>示例 WDM 设备对象





下图说明了该设备对象表示在图演示前面所示的键盘和鼠标设备[键盘和鼠标的硬件配置](sample-device-and-driver-configuration.md#keyboard-and-mouse-hardware-configurations)。 在图演示所示的键盘和鼠标的驱动程序[键盘和鼠标的驱动程序层](sample-device-and-driver-configuration.md#keyboard-and-mouse-driver-layers)创建这些设备对象通过调用 I/O 支持例程 ([**IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)).

![键盘和鼠标设备对象](images/2sampdos.png)

对于键盘和鼠标的设备，其相应的端口和类驱动程序创建设备对象。 端口驱动程序创建一个物理设备对象 (PDO) 来表示的物理端口。 每个类驱动程序创建其自己的功能的设备对象 (FDO) 来表示为目标的键盘或鼠标设备的 I/O 请求。

每个类驱动程序调用到下一步低级驱动程序的设备对象，获取一个指针，因此类驱动程序可以在上面的驱动程序，可以是端口驱动程序链接本身的 I/O 支持例程。 然后在类驱动程序可以发送到目标 PDO 表示其物理设备的端口驱动程序的 I/O 请求。

添加到配置中的可选筛选器驱动程序将创建一个筛选器设备对象 （筛选器执行操作）。 类驱动程序，如可选筛选器驱动程序本身链接到设备堆栈中的下一步低驱动程序，并将发送到下一步低驱动程序的目标 PDO 的 I/O 请求。

如中所示的以前[键盘和鼠标的驱动程序层](sample-device-and-driver-configuration.md#keyboard-and-mouse-driver-layers)图，每个端口驱动程序是总线 （最低级别） 驱动程序，因此每个端口驱动程序的生成中断的设备必须设置中断对象并将注册 ISR.

双设备端口驱动程序，如键盘和键盘和鼠标的硬件配置中所示，如果每个设备使用不同的中断向量的辅助设备控制器的 i8042 驱动程序。 编写此类的驱动程序，可以实现为每个设备的单独 Isr 或实现这两种设备单一 ISR。

 

 




