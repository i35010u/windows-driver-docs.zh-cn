---
title: 使用 WDF 开发驱动程序
description: 本主题提供了用于开发 (KMDF) 驱动程序的内核模式驱动程序框架的框架对象的高级概述。
ms.assetid: 421b7eb8-11d3-4a37-8ae8-e2d3d216c9c7
keywords:
- 内核模式驱动程序 WDK KMDF，开发步骤
- KMDF WDK，开发步骤
- 内核模式驱动程序框架 WDK，开发步骤
- 基于框架的驱动程序 WDK KMDF，开发步骤
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b6187f0a96e6cc2aaec0226d9d3282cd2bf5e8c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187747"
---
# <a name="using-wdf-to-develop-a-driver"></a>使用 WDF 开发驱动程序


本主题提供了用于开发 (KMDF) 驱动程序的内核模式驱动程序框架的框架对象的高级概述。 除了指出的情况外，你将使用相同的对象在 UMDF 版本2中从开始开发用户模式驱动程序框架 (UMDF) 驱动程序。

Windows 驱动程序框架 (WDF) 驱动程序由基于框架的驱动程序所使用的[Windows 驱动程序框架对象](./introduction-to-framework-objects.md)定义的[**DriverEntry 例程**](./driverentry-for-kmdf-drivers.md)和一组事件回调函数组成。 回调函数调用框架导出的对象方法。 Windows 驱动程序工具包 (WDK) 包含示例 WDF 驱动程序，用于演示如何实现驱动程序的事件回调函数。 你可以从 [Windows 开发人员中心-硬件](https://go.microsoft.com/fwlink/p/?linkid=256387)下载这些示例。 有关可用示例的详细信息，请参阅 [KMDF 驱动程序](sample-kmdf-drivers.md) 和 [示例 UMDF 驱动程序](sample-umdf-drivers.md)示例。

创建 WDF 驱动程序时，通常会执行以下操作：

-   使用 *框架驱动程序对象* 来表示您的驱动程序。

    驱动程序的 [**DriverEntry 例程**](./driverentry-for-kmdf-drivers.md) 必须调用 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 以创建表示该驱动程序的框架驱动程序对象。 **WdfDriverCreate**方法还会注册驱动程序的[*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数即插即用，该函数 (PnP) 管理器报告驱动程序支持的设备是否存在。

-   使用 *框架设备对象* 支持驱动程序中的 PnP 和电源管理。

    所有驱动程序都必须调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) ，以便为驱动程序支持的每个设备创建框架设备对象。 设备可以是插入到计算机中的一片硬件，也可以是仅限软件的设备。 框架设备对象支持 PnP 和电源管理操作，驱动程序可以注册事件回调函数，以便在设备进入或离开其工作状态时通知驱动程序。

    有关框架设备对象的详细信息，请参阅 [在您的驱动程序中支持 PnP 和电源管理](supporting-pnp-and-power-management-in-your-driver.md)。

-   使用 *框架队列对象* 和 *框架请求对象* 来支持驱动程序中的 i/o 操作。

    从应用程序或其他驱动程序接收读取、写入或设备 i/o 控制请求的所有驱动程序都必须调用 [**WdfIoQueueCreate**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate) ，以创建表示 i/o 队列的框架队列对象。 通常，驱动程序会为每个 i/o 队列注册一个或多个 [请求处理程序](request-handlers.md) 。 当 i/o 管理器向驱动程序发送 i/o 请求时，框架将为请求创建一个框架请求对象，将该请求对象放置在 i/o 队列中，并调用驱动程序的一个请求处理程序来通知驱动程序请求可用。 该驱动程序将获取 i/o 请求，并可以重新排队、完成、取消或转发该请求。

    有关使用框架的队列对象和请求对象的详细信息，请参阅 [框架队列对象](framework-queue-objects.md) 和 [框架请求对象](framework-request-objects.md)。

-   使用 *框架中断对象* 来处理设备中断。

    处理设备中断的驱动程序必须调用 [**WdfInterruptCreate**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) ，以便为每个中断创建框架中断对象并注册回调函数。 这些回调函数启用和禁用中断，并充当中断服务例程 (ISR) ，并为中断 (DPC) 延迟过程调用。

    有关框架中断对象的详细信息，请参阅 [处理硬件中断](handling-hardware-interrupts.md)。

-   KMDF 驱动程序可以使用框架的 *dma 启用码* 对象和 *dma 事务对象* 来处理设备 (DMA) 操作的直接内存访问。

    如果 KMDF 驱动程序的设备支持 DMA 操作，驱动程序应调用 [**WdfDmaEnablerCreate**](/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate) 来创建 dma 启用程序对象，并使用 [**WdfDmaTransactionCreate**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate) 创建一个或多个 dma 事务对象。 DMA transaction 对象定义用于计划设备硬件执行 DMA 操作的 [*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) 回调函数。

    有关支持 DMA 操作的详细信息，请参阅 [在基于框架的驱动程序中处理 Dma 操作](handling-dma-operations-in-kmdf-drivers.md)。

-   使用框架的 *i/o 目标对象* 将 i/o 请求发送到其他驱动程序。

    若要将 i/o 请求传递到其他驱动程序 (通常是驱动程序堆栈) 中的下一个较低驱动程序，则驱动程序将请求发送到 i/o 目标对象。

    有关 i/o 目标对象的详细信息，请参阅 [使用 I/o 目标](using-i-o-targets.md)。

-   KMDF 驱动程序可以使用框架的 *wmi 提供程序对象* 和 *wmi 实例对象* 来支持 (WMI) 功能 Windows Management Instrumentation。

    大多数 KMDF 驱动程序应支持 WMI，并应调用 [**WdfWmiInstanceCreate**](/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancecreate) 来注册发送或接收 WMI 数据的回调函数。

    有关 WMI 的详细信息，请参阅 [在基于框架的驱动程序中支持 WMI](supporting-wmi-in-kmdf-drivers.md)。

-   使用框架的同步功能。

    所有驱动程序都必须了解多处理器同步问题，并应使用框架提供的 [同步技术](./using-automatic-synchronization.md) 。

-   使用框架提供的其他对象和功能。

    该框架提供了驱动程序可以使用的其他对象。 有关这些对象的详细信息，请参阅 [WDF 支持对象](./using-memory-buffers.md)。

 

