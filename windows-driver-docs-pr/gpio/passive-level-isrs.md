---
title: 被动级别 ISR
description: 从 Windows 8 开始，内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序可以选择将其中断服务例程注册 (Isr) 以在被动级别运行。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0180c26be224da5a9a65b46bce18e6297039e06
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827203"
---
# <a name="passive-level-isrs"></a>被动级别 ISR


从 Windows 8 开始，内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序可以选择将其中断服务例程注册 (Isr) 以在被动级别运行。

有关 KMDF 和 UMDF 驱动程序的被动级别 Isr 的详细信息，请参阅以下主题：

-   [支持被动级别中断](../wdf/supporting-passive-level-interrupts.md)
-   [访问硬件和处理中断](../wdf/accessing-hardware-and-handling-interrupts.md)

如果外围设备使用常规用途 i/o (GPIO) pin 来向处理器中继中断请求，则 Windows 中断抽象可方便地使此设备的驱动程序忽略此 pin 所属的 GPIO 控制器的特定于硬件的详细信息。 当内核陷阱处理程序运行以响应来自设备的 GPIO 中继中断请求时，此处理程序将根据需要自动清除或屏蔽 GPIO 硬件注册中的中断。 此外，内核陷阱处理程序要么直接调用设备的 ISR，要么计划此 ISR 在另一个线程中运行。

通常，GPIO 硬件寄存器是内存映射的，在这种情况下，内核陷阱处理程序可以在 DIRQL 上直接访问它们。 但是，外围设备的硬件寄存器可能未进行内存映射，在这种情况下，外设驱动程序必须使用 i/o 请求来访问它们。 如果是这样，则外设驱动程序的 ISR 必须以 IRQL = 被动级别运行， \_ 以便它可以使用 i/o 请求来静默中断，或者执行中断的初始维护。 被动级别 ISR 可以同步发送 i/o 请求，如有必要，在请求完成前阻止。

若要为外设提供支持边缘触发的中断请求信号的被动级别 ISR，内核陷阱处理程序将清除 GPIO pin 中的挂起中断，然后将 ISR 计划为在被动级别内核线程中运行。

若要为外设提供支持的被动级别 ISR，使其生成级别触发的中断请求信号，内核陷阱处理程序会在 GPIO pin 处屏蔽挂起中断，然后将 ISR 计划为在被动级别内核线程中运行。 ISR 负责在外围设备中清除中断请求。 ISR 返回后，内核线程会将中断解除在 GPIO pin 上。

由于在 ISR 返回之前中断会保持屏蔽状态，因此设备的被动级别 ISR 应仅执行中断的初始维护，然后返回以避免延迟其他设备的被动级别 Isr。 通常，驱动程序应将与中断相关的其他处理延迟为中断工作线程，该线程的运行优先级低于 ISR。

 

