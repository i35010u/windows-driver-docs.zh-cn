---
title: 存储筛选器驱动程序的 IoCompletion 例程
description: 存储筛选器驱动程序的 IoCompletion 例程
ms.assetid: 1a27598b-7113-4f95-8777-bbb10003c268
keywords:
- 存储筛选器驱动程序 WDK，IoCompletion
- 筛选器驱动程序 WDK 存储，IoCompletion
- SFD WDK 存储，IoCompletion
- IoCompletion
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a3a64897fd0589da19d26e364fb7aa17cfaeb86
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188791"
---
# <a name="storage-filter-drivers-iocompletion-routines"></a>存储筛选器驱动程序的 IoCompletion 例程

如果 (端口、类和其他筛选器驱动程序（如果有任何) 调用[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)），则会调用存储筛选器驱动程序的[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。 存储筛选器驱动程序的 *IoCompletion* 例程 (SFD) 应返回 **STATUS_MORE_PROCESSING_REQUIRED** ，以防完成了驱动程序分配的 irp 的处理; 如果 SFD 在完成前将重新使用 irp，则保留原始 irp。

与任何其他较高级别的驱动程序一样，SFD 的[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程负责调用[**IoFreeIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp) ，以释放使用[**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)或[**IoBuildAsynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)创建的驱动程序*调度*例程的任何 IRP。

根据其设备，SFD 可能会*为其发送*到下一个较低驱动程序的 Irp 提供[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。 特别是，以非标准格式检索并处理数据的设备可能需要 SFD 从其*IoCompletion*例程调用*TranslateDataIn*例程，以便将来自此类设备的请求传输到系统内存。

请注意 *，在任意* 线程上下文中，将在 IRQL = = DISPATCH_LEVEL 和。 因此，驱动程序返回数据的缓冲区必须位于非分页池中，或者必须被锁定并可使用映射的非分页系统空间虚拟地址进行访问。 若要详细了解如何安全地访问以引发的 IRQL 提供的用户提供的缓冲区，请参阅 [访问数据缓冲区的方法](../kernel/methods-for-accessing-data-buffers.md)。

通常情况下，存储筛选器驱动程序应提供具有与类驱动程序的*IoCompletion*例程相同的功能的[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，该例程用于筛选器驱动程序使用 SRBs 和 CDBs 设置的 irp。 因此，存储筛选器驱动程序可能有任何或所有 *ReleaseQueue*、 *InterpretRequestSense*或 *RetryRequest* 例程，可以从存储类驱动程序的 *IoCompletion* 例程调用这些例程。

有关 *InterpretRequestSense*、 *RetryRequest*和 *ReleaseQueue* 例程的详细信息，请参阅 [存储类驱动程序](introduction-to-storage-class-drivers.md)。 有关 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程一般要求的详细信息，请参阅 [使用 IoCompletion 例程](../kernel/using-iocompletion-routines.md)。