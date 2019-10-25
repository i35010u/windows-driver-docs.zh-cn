---
title: 设备工作状态 D0
description: 设备工作状态 D0
ms.assetid: 6b0ec03a-eaf1-4c96-aaae-dfe821583787
keywords:
- 设备电源状态 WDK 内核
- Dx 命名 WDK 电源管理
- 设备工作状态 WDK 电源管理
- 持续电能 WDK 内核
- 延迟 WDK 电源管理
- 工作状态 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6783e4f03c64c4d490cd86eaf015fc9d21b0bd05
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836926"
---
# <a name="device-working-state-d0"></a>设备工作状态 D0





在 D0 设备电源状态中，设备已完全打开且正常工作。 在此状态下，设备驱动程序可以与设备交互以执行 i/o 操作，并且设备可能会产生中断。 如果设备具有映射到内存或 i/o 地址空间的硬件寄存器，则驱动程序可以访问这些寄存器。

从 Windows 8 开始，设备驱动程序可以将[被动级别中断服务例程](using-passive-level-interrupt-handling-routines.md)（ISR）连接到设备中断。 无论设备是否处于 D0，设备都可以生成中断。 当处于低功耗 Dx 状态时，设备可以生成一个中断来充当触发器，使设备返回到 D0。 设备进入 D0 后，会计划在 IRQL = 被动\_级别运行 ISR。 在 Windows 的早期版本（包括 Windows 7）中，如果设备处于 D0 以外的设备电源状态，则不能生成中断。

仅当设备驱动程序在充当设备的电源策略所有者时，通过调用[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)例程启动转换时，才能从 D0 转换为低功耗 Dx 状态。 当电源管理器通过以下方式响应此呼叫：发送 power IRP （[**IRP\_MN\_设置\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)）、设备驱动程序、总线驱动程序和平台固件（通过[Windows ACPI 驱动](acpi-driver.md)程序，ACPI）合作处理此 IRP 用于更改设备的电源状态。

设备硬件通常会监视一组内部事件，这些事件可以生成运行时中断或唤醒信号，具体取决于设备的配置方式。 驱动程序实现一个代码路径来响应中断，另一个用于响应唤醒事件。 如果中断代码路径不需要处理唤醒事件，并且唤醒代码路径不需要处理中断，则可以简化驱动程序代码。 作为最佳做法，驱动程序应该将设备配置为仅在设备处于 D0 状态时才生成中断，并且仅在设备处于低功耗 Dx 状态时才生成唤醒信号。 通常，驱动程序将设备配置为在设备退出 D0 之前生成唤醒信号，并将设备配置为在设备进入 D0 后立即生成中断。

通常，设备在对其硬件重置信号进行断言后进入 D0 状态。 事实上，适用于 PCI 和 PCI Express 的总线规范需要此行为。

以下是 D0 状态的特征：

<a href="" id="power-consumption"></a>**功率消耗**  
设备的最高连续功率消耗。

<a href="" id="device-context"></a>**设备上下文**  
保留所有上下文。

<a href="" id="device-driver-behavior"></a>**设备驱动程序行为**  
正常操作。

<a href="" id="restore-time"></a>**还原时间**  
不适用。

<a href="" id="wake-up-capability"></a>**唤醒功能**  
不适用。

 

 




