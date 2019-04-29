---
title: 使用 WDF 开发驱动程序
description: 本主题提供将用于开发的内核模式驱动程序框架 (KMDF) 驱动程序的 framework 对象的高级概述。
ms.assetid: 421b7eb8-11d3-4a37-8ae8-e2d3d216c9c7
keywords:
- 内核模式驱动程序 WDK KMDF，开发步骤
- KMDF WDK，开发步骤
- 内核模式驱动程序框架 WDK，开发步骤
- 基于框架的驱动程序 WDK KMDF，开发步骤
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e27575d44a27f611034e3c70b9b75e9d1160a14d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391833"
---
# <a name="using-wdf-to-develop-a-driver"></a>使用 WDF 开发驱动程序


本主题提供将用于开发的内核模式驱动程序框架 (KMDF) 驱动程序的 framework 对象的高级概述。 除特别指明，您将使用相同的对象来开发启动 UMDF 版本 2 中的用户模式驱动程序框架 (UMDF) 驱动程序。

Windows 驱动程序框架 (WDF) 驱动程序组成[ **DriverEntry 例程**](https://msdn.microsoft.com/library/windows/hardware/ff540807)和一系列事件回叫函数，通过定义[Windows 驱动程序框架对象](wdf-objects.md)基于框架的驱动程序使用。 回调函数调用 framework 导出的对象方法。 Windows Driver Kit (WDK) 包含演示如何实现驱动程序的事件回调函数的示例 WDF 驱动程序。 您可以下载这些示例来自[Windows 开发人员中心-硬件](https://go.microsoft.com/fwlink/p/?linkid=256387)。 提供哪些示例的信息，请参阅[示例 KMDF 驱动程序](sample-kmdf-drivers.md)并[样本 UMDF 驱动程序](sample-umdf-drivers.md)。

创建 WDF 驱动程序时，通常将执行以下操作：

-   使用*framework 驱动程序对象*来表示您的驱动程序。

    在驱动程序[ **DriverEntry 例程**](https://msdn.microsoft.com/library/windows/hardware/ff540807)必须调用[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)创建表示一个框架驱动程序对象驱动程序。 **WdfDriverCreate**方法还会注册的驱动程序[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数，框架将调用每个时间 Plug and Play （即插即用）管理器报告的驱动程序支持的设备存在。

-   使用*framework 设备对象*若要在您的驱动程序支持即插即用和电源管理。

    所有驱动程序必须调用[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)创建每个设备驱动程序支持的框架设备对象。 设备可以是一个插入到计算机的硬件，也可以是纯软件设备。 Framework 设备对象支持即插即用和电源管理操作和驱动程序可以注册事件回叫函数，当设备进入或离开其工作状态时通知该驱动程序。

    有关框架设备对象的详细信息，请参阅[支持即插即用和您的驱动程序中的电源管理](supporting-pnp-and-power-management-in-your-driver.md)。

-   使用*framework 队列对象*并*framework 请求对象*以支持您的驱动程序中的 I/O 操作。

    所有驱动程序的已接收的读取、 写入或设备的 I/O 控制请求从应用程序或其他驱动程序必须调用[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)创建表示 I/O 队列的队列对象的框架。 通常情况下，驱动程序注册一个或多个[请求处理程序](request-handlers.md)为每个 I/O 队列。 I/O 管理器将 I/O 请求发送到该驱动程序，框架创建请求一个框架请求对象、 将请求对象放入 I/O 队列中，并调用其中一个驱动程序的请求处理程序来通知该驱动程序请求可用。 驱动程序获取的 I/O 请求并可以重新排队、 完成、 取消，或将请求转发。

    有关使用框架的队列对象和请求对象的详细信息，请参阅[Framework 队列对象](framework-queue-objects.md)并[Framework 请求对象](framework-request-objects.md)。

-   使用*framework 中断对象*处理设备中断。

    处理设备中断的驱动程序必须调用[ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)创建每个中断 framework 中断对象以及如何注册回调函数。 这些回调函数启用和禁用中断并充当中断服务例程 (ISR) 并延迟过程调用 (DPC) 的中断。

    有关框架中断对象的详细信息，请参阅[处理硬件中断](handling-hardware-interrupts.md)。

-   KMDF 驱动程序可以使用的框架*DMA 促成因素对象*并*DMA 事务对象*处理设备的直接内存访问 (DMA) 操作。

    如果 KMDF 驱动程序的设备支持 DMA 操作，该驱动程序应调用[ **WdfDmaEnablerCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546983)创建 DMA 启用程序对象和[ **WdfDmaTransactionCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547027)创建一个或多个 DMA 事务对象。 DMA 事务对象定义[ *EvtProgramDma* ](https://msdn.microsoft.com/library/windows/hardware/ff541816)程序设备硬件执行 DMA 操作的回调函数。

    有关支持 DMA 的操作的详细信息，请参阅[基于 Framework 的驱动程序中处理 DMA 操作](handling-dma-operations-in-kmdf-drivers.md)。

-   使用框架*I/O 目标对象*将 I/O 请求发送到其他驱动程序。

    若要将输入/输出请求传递给其他驱动程序 （通常的下一个较低驱动程序在驱动程序堆栈中），您的驱动程序将请求发送到 I/O 目标对象。

    有关 I/O 目标对象的详细信息，请参阅[使用 I/O 目标](using-i-o-targets.md)。

-   KMDF 驱动程序可以使用的框架*WMI 提供程序对象*并*WMI 实例对象*必须支持 Windows Management Instrumentation (WMI) 的功能。

    大多数 KMDF 驱动程序应支持 WMI 和应调用[ **WdfWmiInstanceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff551178)注册回叫函数，发送或接收 WMI 数据。

    有关 WMI 的详细信息，请参阅[中基于框架的驱动程序支持 WMI](supporting-wmi-in-kmdf-drivers.md)。

-   使用框架的同步功能。

    所有驱动程序必须能够识别多处理器同步问题，并应使用[同步技术](synchronization-techniques-for-wdf-drivers.md)framework 提供的。

-   使用其他对象和该框架提供的功能。

    该框架提供您的驱动程序可以使用的其他对象。 有关这些对象的详细信息，请参阅[WDF 支持对象](wdf-support-objects.md)。

 

 





