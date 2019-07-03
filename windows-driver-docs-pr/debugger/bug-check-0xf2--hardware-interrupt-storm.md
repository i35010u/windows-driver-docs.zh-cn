---
title: Bug 检查 0xF2 HARDWARE_INTERRUPT_STORM
description: HARDWARE_INTERRUPT_STORM bug 检查具有 0x000000F2 值。 这表示在内核检测到中断 storm。
ms.assetid: 04751AB2-E9B3-40AD-A872-8DDA9B96C6CA
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
ms.openlocfilehash: 4b0b810cecb88c29640f70ad7869e0cbf232c2a7
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518752"
---
# <a name="bug-check-0xf2-hardwareinterruptstorm"></a>Bug 检查 0xF2：硬件\_中断\_STORM


硬件\_中断\_STORM bug 检查的值为 0x000000F2。 这表示在内核检测到中断 storm。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="hardwareinterruptstorm-parameters"></a>硬件\_中断\_STORM 参数


| 参数 | 描述                                                                               |
|-----------|-------------------------------------------------------------------------------------------|
| 1         | 连接到风暴中断矢量地址 ISR （或链中的第一个 ISR） |
| 2         | ISR 上下文值                                                                         |
| 3         | 风暴中断矢量的中断对象的地址                         |
| 4         | 如果不是 ISR 0x1 链接在一起，0x2 ISR 链接                                  |

 

<a name="cause"></a>原因
-----

此检测错误指示在内核检测到中断 storm。 中断 storm 被指在断言状态保持级别触发的中断信号。 这是致命的系统将硬方式系统挂起或"总线 lock"。

这可能是由于以下：

-   硬件不会告知为此，设备驱动程序后将释放其中断信号。
-   设备驱动程序不会指示发布中断信号，因为它不认为中断启动其硬件从其硬件。
-   设备驱动程序声明中断，即使不从其硬件初始化的中断也是如此。 请注意，这仅可出现多个设备都共享相同的 IRQ 时。
-   ELCR （edge 级别控制寄存器） 设置不正确。
-   边缘和级别中断触发设备共享 IRQ。

所有这些情况下将立即硬挂起你的系统。 而不是硬挂起系统，此 bug 检查已启动，因为在许多情况下，它可以确定问题所在。

检测的错误时，屏幕上显示包含风暴 IRQ ISR （中断服务例程） 的模块。 这是你将看到的一个示例：

```console
*** STOP: 0x000000F2 (0xFCA7C55C, 0x817B9B28, 0x817D2AA0, 0x00000002)
An interrupt storm has caused the system to hang.
*** Address FCA7C55C base at FCA72000, Datestamp 3A72BDEF - ACPI.sys
```

事件的第四个参数是 0x00000001，指向模块很可能是问题所在。 该驱动程序已损坏，或者硬件工作不正常。

事件的第四个参数是 0x00000002，指向链中的第一个 ISR 并模块永远不会保证是罪魁祸首。

<a name="resolution"></a>分辨率
----------

反复遇到此错误检查，用户应尝试通过查找与为其模块是用于 （在此情况下，使用 ACPI 的 IRQ） 的驱动程序相同的 IRQ 设备来隔离问题。

 

 




