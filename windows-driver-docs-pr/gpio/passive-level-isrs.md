---
title: 被动级别 ISR
description: 作为一个选项，从 Windows 8、 内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序可以注册其中断服务例程 (Isr) 在被动级别运行。
ms.assetid: E7556046-D85C-4CD1-8C27-578BF5CAFF2B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4530aab95ee8564db0230bcaccca66efbd588aa9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326123"
---
# <a name="passive-level-isrs"></a>被动级别 ISR


作为一个选项，从 Windows 8、 内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序可以注册其中断服务例程 (Isr) 在被动级别运行。

有关被动级别 Isr KMDF 和 UMDF 驱动程序的详细信息，请参阅以下主题：

-   [支持被动级别中断](https://msdn.microsoft.com/library/windows/hardware/hh451035)
-   [访问硬件和处理中断](https://msdn.microsoft.com/library/windows/hardware/hh439560)

如果外围设备使用常规用途的 I/O (GPIO) pin 进行中继到处理器的中断请求，Windows 中断抽象方便地允许忽略特定于硬件的详细信息的 GPIO 控制器到此设备的驱动程序属于此 pin。 内核的陷阱处理程序运行以响应 GPIO 中继中断时从设备请求，此处理程序会自动清除或掩码，为必需的 GPIO 硬件寄存器中的中断。 此外，内核的陷阱处理程序直接调用设备的 ISR 或安排此 ISR 在另一个线程中运行。

通常情况下，内存映射的 GPIO 硬件寄存器，在这种情况下内核的陷阱处理程序可以直接访问它们在 DIRQL。 但是，在硬件注册外围设备的设备可能不是内存映射，在这种情况下，外围设备驱动程序必须使用 I/O 请求来对其进行访问。 如果外围设备驱动程序 ISR 因此，必须运行在 IRQL = 被动\_级别，以便它可以使用 I/O 请求提示中断或执行初始服务的中断。 被动级别 ISR 都可以同步发送的 I/O 请求，并如有必要，阻塞，直到完成该请求。

若要生成的边缘触发中断请求信号的外围设备支持被动级别 ISR，内核的陷阱处理程序清除在 GPIO 插针，挂起的中断，然后安排 ISR 在被动级别内核线程中运行。

若要支持外围设备的生成级别触发中断请求信号被动级别 ISR，内核的陷阱处理程序会屏蔽在 GPIO 插针，挂起的中断，然后安排 ISR 在被动级别内核线程中运行。 ISR 负责清除外围设备中的中断请求。 ISR 返回后，内核线程解除屏蔽 GPIO pin 处中断。

因为中断前 ISR 仍保持掩码返回时，设备的被动级别 ISR 应执行仅限初始服务的中断，然后返回以避免延迟被动级别 Isr 为其他设备。 通常情况下，该驱动程序应推迟到中断工作线程，其运行速度比 ISR 较低优先级的其他中断相关处理

 

 




