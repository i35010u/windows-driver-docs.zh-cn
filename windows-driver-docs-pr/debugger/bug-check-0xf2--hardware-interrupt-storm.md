---
title: Bug 检查 0xF2 HARDWARE_INTERRUPT_STORM
description: HARDWARE_INTERRUPT_STORM bug 检查的值为0x000000F2。 这表示内核检测到中断风暴。
keywords:
- Bug 检查 0xF2 HARDWARE_INTERRUPT_STORM
- HARDWARE_INTERRUPT_STORM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- HARDWARE_INTERRUPT_STORM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 84f0532d8aa6f276247f47563c184657ce303d0a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819237"
---
# <a name="bug-check-0xf2-hardware_interrupt_storm"></a>Bug 检查0xF2：硬件 \_ 中断 \_ 风暴


硬件 \_ 中断 \_ 风暴 bug 检查的值为0x000000F2。 这表示内核检测到中断风暴。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="hardware_interrupt_storm-parameters"></a>硬件 \_ 中断 \_ 风暴参数


| 参数 | 描述                                                                               |
|-----------|-------------------------------------------------------------------------------------------|
| 1         | ISR 中 (或第一个 ISR) 连接到 storming 中断向量的地址 |
| 2         | ISR 上下文值                                                                         |
| 3         | Storming 中断向量中断对象的地址                         |
| 4         | 如果 ISR 未链接，则为 0x1; 如果 ISR 链接，则0x2                                  |

 

<a name="cause"></a>原因
-----

此错误检测表明内核检测到中断风暴。 中断风暴定义为处于断言状态的触发中断信号级别。 这对于系统来说是致命的，系统将硬挂起，或者 "总线锁定"。

这可能是由以下原因导致的：

-   设备驱动程序在被告知后，一段硬件不会释放其中断信号。
-   设备驱动程序不会指示其硬件释放中断信号，因为它不相信中断是从其硬件发起的。
-   即使中断并非从其硬件启动，设备驱动程序也会声明该中断。 请注意，仅当多个设备共享同一 IRQ 时才会发生这种情况。
-   ELCR (edge 级别控制寄存器) 设置不正确。
-   边缘和级别中断触发的设备共享 IRQ。

所有这些情况都会使你的系统立即挂起。 此错误检查不是硬挂起系统，因为在许多情况下，它可以识别错误。

发生错误检测时，将在屏幕上显示包含 ISR (中断服务例程) 的模块。 下面是你将看到的内容的示例：

```console
*** STOP: 0x000000F2 (0xFCA7C55C, 0x817B9B28, 0x817D2AA0, 0x00000002)
An interrupt storm has caused the system to hang.
*** Address FCA7C55C base at FCA72000, Datestamp 3A72BDEF - ACPI.sys
```

如果第四个参数是0x00000001，则指向的模块很可能是发生的原因。 驱动程序已损坏，或者硬件出现故障。

如果第四个参数是0x00000002，则指向的模块是链中的第一个 ISR，并且永远不能保证成为原因。

<a name="resolution"></a>解决方法
----------

重复发生此错误检查的用户应尝试隔离此问题，方法是在此示例中查找该模块是其驱动 (程序所用的同一 IRQ 上的设备，这是 ACPI 使用) 的同一个 IRQ。

 

 




