---
title: 编写 DPC 例程
description: 编写 DPC 例程
keywords:
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
- DpcForIsr
- CustomDpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23931438ed2e9d152e3c3be1a45378279a0a3c7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782577"
---
# <a name="writing-dpc-routines"></a>编写 DPC 例程





[*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)和 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)例程的主要职责是确保接下来的设备 i/o 操作立即启动并完成当前 IRP。

任何 *DpcForIsr* 或 *CustomDpc* 例程执行的其他工作取决于驱动程序的设计和设备的特性。 例如， *DpcForIsr* 或 *CustomDpc* 例程还可以执行以下任一操作：

-   请重试超时或失败的操作。

-   调用 [**IoAllocateErrorLogEntry**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateerrorlogentry)，设置错误日志数据包以报告设备 i/o 错误，并调用 [**IoWriteErrorLogEntry**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry)。

    有关处理 i/o 错误的详细信息，请参阅 [日志记录错误](logging-errors.md)。

-   如果驱动程序使用 [缓冲 i/o](methods-for-accessing-data-buffers.md)，或者 irp 指定设备控制操作，请在完成 irp 之前，传输从设备到系统缓冲区的数据从设备读入 **&gt;AssociatedIrp.SystemBuffer** 。

-   如果驱动程序使用 [直接 i/o](methods-for-accessing-data-buffers.md) 并且必须将大型传输拆分为较小的部分，请保存有关每个刚完成的部分传输操作的状态，计算下一个部分传输范围，并使用驱动程序提供的 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) 例程对设备进行下一次部分传输操作。

    即使使用缓冲 i/o 的驱动程序，如果其设备的传输功能有限，也可能必须拆分传输请求。

-   如果驱动程序使用基于数据包的 DMA，请在每次设备传输操作后调用 [**FlushAdapterBuffers**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) ，并在完成部分传输序列并满足完全传输请求时调用 [**FreeAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel) 或 [**FreeMapRegisters**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers) 。

    如果仅通过单个 DMA 操作来满足请求的传输，则 *DpcForIsr* 或 *CustomDpc* 例程通常负责设置一个或多个 DMA 操作，直到 IRP 的指定字节数已完全传输。

    有关使用 DMA 的详细信息，请参阅 [适配器对象和 DMA](./introduction-to-adapter-objects.md)。

-   如果驱动程序使用程控 i/o (PIO) ，则在每次传输操作结束时调用 [**KeFlushIoBuffers**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers) （如果当前 IRP 请求读取）。

    如果请求的传输仅部分由一项 PIO 操作满足，则 *DpcForIsr* 或 *CustomDpc* 例程通常负责设置一个或多个传输操作，直到 IRP 的指定字节数已完全传输。

    有关使用 PIO 的详细信息，请参阅 [使用直接 i/o](using-direct-i-o.md)。

-   如果非 WDM 驱动程序具有 [*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049) 例程，则在请求的操作完成时调用 [**IoFreeController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller) 。

请注意， *DpcForIsr* 或 *CustomDpc* 例程通常会执行大多数驱动程序的设备 I/o 处理以满足 irp。 这些例程还分担了用驱动程序的调度例程将 Irp 排队到设备的一些责任。

请考虑以下常规设计准则。

-   任何 *DpcForIsr* 或 *CustomDpc* 例程只要能够安全地进行此调用，就应该立即调用 [**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) ：也就是说，不可能导致资源冲突或争用条件与驱动程序的 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程，或与 *StartIo* 例程导致运行的任何其他例程。

-   如果驱动程序管理自己的 Irp 队列，则它的 *DpcForIsr* 或 *CustomDpc* 例程应立即通知驱动程序，因为可以安全地取消下一个 IRP 的排队并为下一个请求设置设备。

*DpcForIsr* 或 *CustomDpc* 例程必须调用 **IoStartNextPacket**，否则，在可以启动下一个请求的设备 i/o 处理时，通知相应的驱动程序例程。 根据驱动程序及其设备，这可能会在 *DpcForIsr* 或 *CustomDpc* 例程完成当前 irp with [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)之前发生，也可以在此例程完成当前 irp 并返回控制权之前立即发生。

 

