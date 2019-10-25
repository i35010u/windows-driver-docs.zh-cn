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
ms.openlocfilehash: cef336b8f7c71520e31ed801186dca6bd5df5515
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835565"
---
# <a name="writing-dpc-routines"></a>编写 DPC 例程





[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)和[*CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)例程的主要职责是确保接下来的设备 i/o 操作立即启动并完成当前 IRP。

任何*DpcForIsr*或*CustomDpc*例程执行的其他工作取决于驱动程序的设计和设备的特性。 例如， *DpcForIsr*或*CustomDpc*例程还可以执行以下任一操作：

-   请重试超时或失败的操作。

-   调用[**IoAllocateErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateerrorlogentry)，设置错误日志数据包以报告设备 i/o 错误，并调用[**IoWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry)。

    有关处理 i/o 错误的详细信息，请参阅[日志记录错误](logging-errors.md)。

-   如果驱动程序使用[缓冲 i/o](methods-for-accessing-data-buffers.md)，或者 IRP 指定设备控制操作，请在完成 irp 之前，将从设备读入的数据从设备传输到系统缓冲区（ **&gt;在 AssociatedIrp**中）。

-   如果驱动程序使用[直接 i/o](methods-for-accessing-data-buffers.md)并且必须将大型传输拆分为较小的部分，请保存有关每个刚完成的部分传输操作的状态，并计算下一个部分传输范围，并使用驱动程序提供的[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)用于对设备进行下一次部分传输操作的例程。

    即使使用缓冲 i/o 的驱动程序，如果其设备的传输功能有限，也可能必须拆分传输请求。

-   如果驱动程序使用基于数据包的 DMA，请在每次设备传输操作后调用[**FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) ，并在完成部分传输序列和完全传输请求后调用[**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)或[**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers) 。得到.

    如果仅通过单个 DMA 操作来满足请求的传输，则*DpcForIsr*或*CustomDpc*例程通常负责设置一个或多个 DMA 操作，直到 IRP 的指定字节数已完全传输。

    有关使用 DMA 的详细信息，请参阅[适配器对象和 DMA](adapter-objects-and-dma.md)。

-   如果驱动程序使用程控 i/o （PIO），并且当前 IRP 请求读取，请在每个传输操作结束时调用[**KeFlushIoBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers) 。

    如果仅通过单个 PIO 操作来满足请求的传输，则*DpcForIsr*或*CustomDpc*例程通常负责设置一个或多个传输操作，直到 IRP 指定的字节数已满此前.

    有关使用 PIO 的详细信息，请参阅[使用直接 i/o](using-direct-i-o.md)。

-   如果非 WDM 驱动程序具有[*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程，则在请求的操作完成时调用[**IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller) 。

请注意， *DpcForIsr*或*CustomDpc*例程通常会执行大多数驱动程序的设备 I/o 处理以满足 irp。 这些例程还分担了用驱动程序的调度例程将 Irp 排队到设备的一些责任。

请考虑以下常规设计准则。

-   任何*DpcForIsr*或*CustomDpc*例程只要能够安全地进行此调用，就应该立即调用[**IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) ：也就是说，不可能与驱动程序的[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程或任何*StartIo*例程将导致运行的其他例程。

-   如果驱动程序管理自己的 Irp 队列，则它的*DpcForIsr*或*CustomDpc*例程应立即通知驱动程序，因为可以安全地取消下一个 IRP 的排队并为下一个请求设置设备。

*DpcForIsr*或*CustomDpc*例程必须调用**IoStartNextPacket**，否则，在可以启动下一个请求的设备 i/o 处理时，通知相应的驱动程序例程。 根据驱动程序及其设备，这可能会在*DpcForIsr*或*CustomDpc*例程完成当前 irp with [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)之前发生，也可以在此例程完成当前 irp 之前立即发生。返回控件。

 

 




