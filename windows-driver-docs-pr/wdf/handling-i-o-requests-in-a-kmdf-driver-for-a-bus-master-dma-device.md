---
title: 在适用于总线主控 DMA 设备的 KMDF 驱动程序中处理 I/O 请求
description: 本部分中的本主题介绍如何总线 master DMA 设备的 KMDF 驱动程序处理的 I/O 请求。 如果你正在编写实现系统模式 DMA KMDF 驱动程序，请参阅支持系统模式 DMA。
ms.assetid: c94819c5-212d-404f-a7c7-b736e0832282
keywords:
- DMA 操作 WDK KMDF，I/O 请求
- 主总线 DMA WDK KMDF，I/O 请求
- I/O 请求 WDK KMDF，DMA 的设备
- 请求处理 WDK KMDF，DMA 的设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93e6da2c9b80e54ca7c5cf86a5096761b2ba6f52
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382848"
---
# <a name="handling-io-requests-in-a-kmdf-driver-for-a-bus-master-dma-device"></a>在适用于总线主控 DMA 设备的 KMDF 驱动程序中处理 I/O 请求


\[仅适用于 KMDF\]

本部分中的本主题介绍如何总线 master DMA 设备的 KMDF 驱动程序处理的 I/O 请求。 如果你正在编写实现系统模式 DMA KMDF 驱动程序，请参阅[支持系统模式 DMA](supporting-system-mode-dma.md)。




处理 I/O 请求总线 master DMA 设备 KMDF 驱动程序中的需要几个驱动程序的事件回调函数中的代码下, 图中所示：

![dma kmdf 驱动程序中实现](images/dma-implementation-in-kmdf.png)

如上所示，DMA 相关处理发生在四个阶段：

1.  您的驱动程序[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)或[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数必须[启用 DMA事务](enabling-dma-transactions.md)对于设备，以便您的驱动程序可以使用框架的 DMA 功能。 相同的回调函数还必须[创建常见缓冲区](using-common-buffers.md)如果你的设备和驱动程序需要访问的共享的内存缓冲区。

2.  当您的驱动程序收到要求执行 DMA 操作，其中一个驱动程序的设备的 I/O 请求[请求处理程序](request-handlers.md)必须[创建和初始化一个新的 DMA 事务](creating-and-initializing-a-dma-transaction.md)。 (请注意，如果您的驱动程序[重用 DMA 事务对象](reusing-dma-transaction-objects.md)，您的驱动程序[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数可以创建事务对象。)然后，请求处理程序必须[启动 DMA 事务](starting-a-dma-transaction.md)，以便可以开始分解为较小的 DMA 传送的事务，如有必要，并调用驱动程序的框架[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数。

3.  您的驱动程序[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)回调函数[程序 DMA 硬件](programming-dma-hardware.md)单一 dma 传输，并启用设备中断。

4.  设备会中断，框架将调用您的驱动程序[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数，以保存易失性的设备信息，并计划执行的驱动程序的[*EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数。

    您的驱动程序[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数[完成每个 DMA 传输](completing-a-dma-transfer.md)硬件完成处理后。 DMA 事务的最终后已完成，传输*EvtInterruptDpc*回调函数[完成 DMA 事务](completing-a-dma-transaction.md)。

您的驱动程序可能[重复使用其 DMA 事务对象](reusing-dma-transaction-objects.md)以确保当内存资源不足时可以运行。

您的驱动程序可以提供一组回调函数，用于处理[特定于 DMA 的电源管理操作](supporting-power-management-for-dma-devices.md)。

某些驱动程序[使用常见缓冲区](using-common-buffers.md)设备和驱动程序可以访问。

 

 





