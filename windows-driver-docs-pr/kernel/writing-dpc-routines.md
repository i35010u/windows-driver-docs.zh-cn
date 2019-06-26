---
title: 编写 DPC 例程
description: 编写 DPC 例程
ms.assetid: a0b93b71-7ee3-4626-b0b8-5dd6e19fba0d
keywords:
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
- DpcForIsr
- CustomDpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff6608a865f911452a7ae83301a2f10cdb4eba97
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374110"
---
# <a name="writing-dpc-routines"></a>编写 DPC 例程





主要职责[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)并[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)例程就确保下一步设备 I/O 操作立即启动并完成当前的 IRP。

完成的任何其他工作*DpcForIsr*或*CustomDpc*例程依赖于驱动程序的设计和设备的性质。 例如， *DpcForIsr*或*CustomDpc*例程还可以执行以下任一：

-   重试已超时或失败的操作。

-   调用[ **IoAllocateErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateerrorlogentry)，将设置为报告设备 I/O 错误，并调用的错误日志数据包[ **IoWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iowriteerrorlogentry)。

    有关处理的 I/O 错误的详细信息，请参阅[日志记录错误](logging-errors.md)。

-   如果驱动程序使用[缓冲 I/O](methods-for-accessing-data-buffers.md)，或如果 IRP 指定的设备管理操作，在从设备中读取到系统缓冲区的数据传输**Irp-&gt;AssociatedIrp.SystemBuffer**之前完成 IRP。

-   如果驱动程序使用[直接 I/O](methods-for-accessing-data-buffers.md)和必须中断大型传输成较小片段，保存有关刚完成每个部分传输操作中，状态计算下一个部分传输范围，并使用驱动程序提供[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)例程进行编程的下一个部分传输操作设备。

    即使使用缓冲的 I/O 的驱动程序可能要拆分的传输请求，如果其设备具有有限的传输功能。

-   如果驱动程序使用基于数据包的 DMA，调用[ **FlushAdapterBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pflush_adapter_buffers)每个设备传输操作中，并调用后[ **FreeAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)或[ **FreeMapRegisters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_map_registers)当完成一系列部分传输并满足完整传输请求。

    如果单个 DMA 操作中，仅部分满足请求的传输*DpcForIsr*或*CustomDpc*例程是通常负责设置一个或多个 DMA 操作，直到指定的 IRP已完全传输的字节数。

    有关使用 DMA 的详细信息，请参阅[适配器对象和 DMA](adapter-objects-and-dma.md)。

-   如果驱动程序使用通过编程方式设置 I/O (PIO)，则调用[ **KeFlushIoBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keflushiobuffers)如果当前 IRP 请求读取每个传输操作的末尾。

    如果单个 PIO 操作中，仅部分满足请求的传输*DpcForIsr*或*CustomDpc*例程是通常负责设置直到 IRP 的一个或多个传输操作已完全传输指定的字节数。

    有关使用 PIO 的详细信息，请参阅[使用直接 I/O](using-direct-i-o.md)。

-   如果非 WDM 驱动程序有[ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程，调用[ **IoFreeController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iofreecontroller)请求的操作何时完成。

请注意， *DpcForIsr*或*CustomDpc*例程通常执行大部分驱动程序的设备 I/O 处理，以满足 Irp。 这些例程还分享一些负责队列 Irp 到设备与驱动程序的调度例程。

请考虑以下常规设计指导原则。

-   任何*DpcForIsr*或*CustomDpc*例程应调用[ **IoStartNextPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)只要它可以安全地进行此调用： 即，而无需可能会导致驱动程序的资源冲突或争用条件[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程或任何其他例程*StartIo*例程将导致向运行。

-   如果驱动程序管理其自己的队列，Irp，其*DpcForIsr*或*CustomDpc*例程应通知驱动程序，只要是下一步 IRP 的取消排队并设置下一个请求设备安全的。

一个*DpcForIsr*或*CustomDpc*例程必须调用**IoStartNextPacket**，否则通知适当的驱动程序例程或当设备 I/O 处理的下一个请求可以启动。 具体取决于驱动程序和其设备，这可能是之前顺利*DpcForIsr*或*CustomDpc*例程完成与当前的 IRP [ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)，或此例程完成当前的 IRP，并返回控件之前立即发生。

 

 




