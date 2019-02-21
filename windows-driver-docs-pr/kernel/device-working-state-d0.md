---
title: 设备处于工作状态 D0
description: 设备处于工作状态 D0
ms.assetid: 6b0ec03a-eaf1-4c96-aaae-dfe821583787
keywords:
- 设备电源状态 WDK 内核
- Dx 名称 WDK 电源管理
- 正常工作状态 WDK 电源管理设备
- 连续 power WDK 内核
- 延迟 WDK 电源管理
- 工作状态 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0a1621674ba0f63155e7ccd32b91da8e59007e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519427"
---
# <a name="device-working-state-d0"></a>设备处于工作状态 D0





D0 设备电源状态下，设备已完全上并正常运行。 在此状态下，设备驱动程序可以与要执行 I/O 操作的设备进行交互和设备可以生成中断。 如果该设备已映射到内存或 I/O 地址空间的硬件寄存器，驱动程序可以访问这些寄存器。

从 Windows 8 开始，可以连接的设备驱动程序[被动级别中断服务例程](using-passive-level-interrupt-handling-routines.md)(ISR) 到设备中的中断。 设备可以生成而不考虑它是否在 D0 中断。 在低功耗 Dx 状态下，设备可以生成中断，它就像一个触发器，用于将设备恢复到 D0。 ISR 计划在 IRQL 运行 = 被动\_级别后在设备进入 D0。 在早期版本的 Windows，包括 Windows 7 中，设备必须不生成中断时 D0 之外的设备电源状态。

从 D0 转换到低功耗 Dx 状态可能仅当设备驱动程序，同时充当设备的电源策略所有者启动转换通过调用[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)例程。 当电源管理器响应此调用发送开机 IRP ([**IRP\_MN\_设置\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744))，设备驱动程序、 总线驱动程序和平台固件 (通过[Windows ACPI 驱动程序](acpi-driver.md)，Acpi.sys) 以协作方式处理此 IRP，若要更改设备的电源状态。

设备硬件通常监视一组内部事件，可以生成任一运行时中断或唤醒信号，具体取决于设备的配置方式。 该驱动程序实现一个对中断，和另一个用于响应唤醒事件做出响应的代码路径。 如果中断代码路径不需要处理的唤醒事件，并且唤醒代码路径不需要处理的中断，可以简化驱动程序代码。 最佳做法是，该驱动程序应配置设备生成中断，仅当设备处于 D0，并仅当设备处于低功耗 Dx 状态时生成唤醒信号。 通常情况下，该驱动程序将设备配置为设备退出 D0，并将设备配置为在设备进入 D0 后立即生成中断之前，只需生成唤醒信号。

通常情况下，设备将添加其硬件重置信号时进入 D0 状态。 事实上，对于诸如 PCI 和 PCI Express 等总线规范需要此行为。

这些是 D0 状态的特征：

<a href="" id="power-consumption"></a>**功率消耗**  
设备连续功率消耗最高级别。

<a href="" id="device-context"></a>**设备上下文**  
保留的所有上下文。

<a href="" id="device-driver-behavior"></a>**设备驱动程序行为**  
正常操作。

<a href="" id="restore-time"></a>**还原时间**  
不适用。

<a href="" id="wake-up-capability"></a>**唤醒功能**  
不适用。

 

 




