---
title: SPB 控制器驱动程序概述
description: SPB 控制器是一个设备，该设备控制简单外设总线 (SPB) 并可向连接到 SPB 的外围设备传输数据以及从其传输数据。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c8f9726efe38a3b42dc74cbb8d0c3fb0801c867
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811823"
---
# <a name="overview-of-spb-controller-drivers"></a>SPB 控制器驱动程序概述

SPB 控制器是一个设备，该设备控制[简单外设总线](/previous-versions/hh450903(v=vs.85)) (SPB) 并可向连接到 SPB 的外围设备传输数据以及从其传输数据。 SPB 控制器的硬件供应商会提供 SPB 控制器驱动程序来管理控制器中的硬件功能。

从 Windows 8 开始，SPB framework 扩展 (SpbCx) 简化了 (SPBs) 的 [简单外围总线](/previous-versions/hh450903(v=vs.85)) 的控制器驱动程序的开发。 SpbCx 是系统提供的针对 [内核模式驱动程序框架](../wdf/index.md) 的扩展 (KMDF) 。 SPB 控制器设备的硬件供应商提供控制器驱动程序来执行所有硬件特定的驱动程序操作。 此驱动程序与 SpbCx 通信以执行特定于 SPB 控制器的操作，并直接与 KMDF 进行通信以执行一般的驱动程序操作。

例如，SPB 控制器驱动程序通常会调用 KMDF 中的 [**WdfDeviceInitSetPnpPowerEventCallbacks**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks) 方法来注册来接收电源事件回调，并调用 [**WdfInterruptCreate**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) 方法将驱动程序的中断服务例程连接 (ISR) 从 SPB 控制器中断。 为了执行特定于 SPB 的操作，SPB 控制器通过 [SpbCx 设备驱动程序接口](/previous-versions/hh698219(v=vs.85)) 与 SpbCx 通信， (DDI) 。

SpbCx 会和 SBP 控制器驱动程序，用于处理连接到 SPB 的外围设备的 i/o 请求。 SpbCx 执行由 SPB 控制器驱动程序公用的处理任务。 这些任务包括管理 SPB 控制器的 i/o 请求队列。 这些队列包含来自管理连接到总线的外围设备的驱动程序的 i/o 请求。 SPB 控制器驱动程序执行处理这些请求所需的所有特定于硬件的操作。

下图显示了 SPB 控制器驱动程序和 SpbCx。

![spb 组件框图](images/spbmodules.png)

SPB 控制器驱动程序和 SpbCx 都在内核模式下运行，并通过 SpbCx DDI 相互通信。 SPB 控制器驱动程序调用由 SpbCx 实现的驱动程序支持方法。 SpbCx 调用由 SPB 控制器驱动程序实现的事件回调函数。

将 i/o 请求发送到 SPB 控制器的驱动程序为使用 [内核模式驱动程序框架](../wdf/index.md) (KMDF) 的内核模式驱动程序，或使用 [用户模式驱动程序框架](/previous-versions/ff554928(v=vs.85)) (UMDF) 的用户模式驱动程序。 这些驱动程序可以发送读写请求，以便将数据传入和传出由 SPB 连接的外围设备。 此外，驱动程序可以将 i/o 控制 (IOCTL 发送) 请求来执行 SPB 特定的操作。

SPB 控制器驱动程序直接访问 SPB 控制器设备的硬件寄存器，以启动与连接到 SPB 的外围设备之间的数据传输。 对于诸如 i2c 这样的 SPB，这些数据传输的速度相对较慢。 尽管 SPB 控制器的硬件寄存器可能是内存映射的，但必须通过 SPB 串行访问外围设备的寄存器。

为了响应将数据传入或传出连接到 SPB 的外围设备的 i/o 请求，SPB 控制器驱动程序将启动总线传输，将 i/o 请求标记为挂起，并返回而不等待传输完成。 稍后，当 SPB 控制器硬件完成了传输时，控制器会向中断发出信号，而 SPB 控制器驱动程序中的 ISR 将完成挂起的 i/o 请求，或在请求的 i/o 操作中启动下一次传输。

只有驱动程序可以将 i/o 请求直接发送到 SPB 控制器。 当用户模式应用程序在连接到 SPB 的外设之间传输数据时，应用程序必须依赖于 SPB 外围设备驱动程序，以将相应的读取或写入请求发送到 SPB 控制器。
