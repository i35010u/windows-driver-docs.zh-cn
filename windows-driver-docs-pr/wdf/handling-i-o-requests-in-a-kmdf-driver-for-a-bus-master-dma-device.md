---
title: 在适用于总线主控 DMA 设备的 KMDF 驱动程序中处理 I/O 请求
description: 本部分中的主题介绍了如何使用 KMDF 驱动程序来处理 i/o 请求。 如果要编写实现系统模式 DMA 的 KMDF 驱动程序，请参阅支持 System-Mode DMA。
keywords:
- DMA 操作 WDK KMDF、i/o 请求
- 总线主控 DMA WDK KMDF、i/o 请求
- I/o 请求 WDK KMDF，DMA 设备
- 请求处理 WDK KMDF，DMA 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a30b645e1ccb85d0bfe6280406bb1bf4e2e9d458
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815631"
---
# <a name="handling-io-requests-in-a-kmdf-driver-for-a-bus-master-dma-device"></a>在适用于总线主控 DMA 设备的 KMDF 驱动程序中处理 I/O 请求


\[仅适用于 KMDF\]

本部分中的主题介绍了如何使用 KMDF 驱动程序来处理 i/o 请求。 如果要编写实现系统模式 DMA 的 KMDF 驱动程序，请参阅 [支持 System-Mode DMA](supporting-system-mode-dma.md)。




在 KMDF 驱动程序中处理针对总线主机 DMA 设备的 i/o 请求需要使用驱动程序的几个事件回调函数中的代码，如下图所示：

![kmdf 驱动程序中的 dma 实现](images/dma-implementation-in-kmdf.png)

如上所示，与 DMA 相关的处理发生在四个阶段中：

1.  驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 或 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调函数必须为设备 [启用 DMA 事务](enabling-dma-transactions.md) ，以便您的驱动程序可以使用框架的 dma 功能。 如果设备和驱动程序需要访问共享内存缓冲区，则相同的回调函数还必须 [创建公用缓冲区](using-common-buffers.md) 。

2.  当驱动程序收到要求设备执行 DMA 操作的 i/o 请求时，驱动程序的 [请求处理](request-handlers.md) 程序之一必须 [创建并初始化新的 DMA 事务](creating-and-initializing-a-dma-transaction.md)。  (请注意，如果您的驱动程序 [重用 DMA 事务对象](reusing-dma-transaction-objects.md)，则驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数可以创建事务对象。 ) 然后，请求处理程序必须 [启动 DMA 事务](starting-a-dma-transaction.md) ，以便框架可以在必要时开始将事务拆分为较小的 dma 传输，并调用驱动程序的 [*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) 回调函数。

3.  驱动程序的 [*EvtProgramDma*](/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) 回调函数 [将 dma 硬件](programming-dma-hardware.md) 用于单个 dma 传输并启用设备中断。

4.  当设备中断时，框架会调用驱动程序的 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数，该函数可保存可变的设备信息并计划驱动程序的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 回调函数的执行。

    在硬件完成对每个 DMA 传输的处理之后，驱动程序的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 回调函数将 [完成每个 DMA 传输](completing-a-dma-transfer.md) 。 DMA 事务的最终传输完成后， *EvtInterruptDpc* 回调函数 [完成 dma 事务](completing-a-dma-transaction.md)。

驱动程序可以 [重复使用其 DMA 事务对象](reusing-dma-transaction-objects.md) ，以确保在内存资源不足时可以运行。

你的驱动程序可以提供一组回调函数来处理 [DMA 特定的电源管理操作](supporting-power-management-for-dma-devices.md)。

某些驱动程序使用设备和驱动程序都可以访问的 [常见缓冲区](using-common-buffers.md) 。

 

