---
title: 拆分 DMA 传输请求
description: 拆分 DMA 传输请求
ms.assetid: 7d5b1649-1021-4876-a9c0-e6b156785ef2
keywords:
- I/o WDK 内核，拆分传输请求
- 拆分传输请求
- 传输请求拆分 WDK 内核
- 数据传输 WDK 内核，拆分请求
- 传输数据 WDK 内核，拆分请求
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 661170e3746f274b54a45b8fcc4048564cb8cef1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190673"
---
# <a name="splitting-dma-transfer-requests"></a>拆分 DMA 传输请求





任何驱动程序都可能需要拆分传输请求并执行多个 DMA 传输操作来满足给定的 IRP，具体取决于以下各项：

-   [**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)返回的[映射寄存器](map-registers.md)的数目

-   要传输的数据的字节数，包含在 IRP 的驱动程序 i/o 堆栈位置的 **长度** 成员中

-   驱动程序要从中传输数据的缓冲区的页边界数，以系统物理内存表示。

-   驱动程序 DMA 操作的设备特定约束。 例如，系统 "AT" 磁盘驱动程序必须将传输请求拆分到超过256个扇区，因为磁盘控制器的限制。

驱动程序可以确定由 IRP 指定的所有数据传输所需的映射寄存器的数目，如下所示：

1.  调用 [**MmGetMdlVirtualAddress**](./mm-bad-pointer.md)，将指针传递到 ** &gt; MdlAddress**的 MDL，以获取缓冲区的起始虚拟地址。 请注意，驱动程序不能尝试使用此虚拟地址来访问内存。 **MmGetMdlVirtualAddress**返回的值是 MDL 的索引，不一定是有效地址。

2.  将所返回的索引和 **Length** 的值的值传递到 " [**地址" 和 "大小" \_ \_ \_ 以 \_ 跨 \_ 页**](./mm-bad-pointer.md) 宏。

如果**ADDRESS \_ 和 \_ SIZE \_ \_ \_ **返回的值超过了**IoGetDmaAdapter**返回的*NUMBEROFMAPREGISTERS*值，则驱动程序将无法在单个 DMA 操作中传输所有请求的数据。 相反，它必须执行以下操作：

1.  将缓冲区拆分为多个部分，以适合可用映射寄存器的数量，)  (和任何特定于设备的 DMA 约束。

2.  执行满足传输请求所需的任意 DMA 操作。

例如，假设 "**地址" \_ 和 "大小" 为 " \_ \_ \_ 跨 \_ 页**" 指示需要十二个映射寄存器才能满足传输请求，但**IoGetDmaAdapter**返回的*NumberOfMapRegisters*值只是5。  (假设没有特定于设备的 DMA 约束。 ) 在这种情况下，驱动程序必须执行三个 DMA 传输操作，调用 [**MapTransfer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer) 三次以传输 IRP 请求的所有数据。

系统的 DMA 设备驱动程序使用各种技术来拆分 DMA 传输，而没有足够的映射寄存器来满足具有单个 i/o 操作的 IRP 的需要。 使用以下方法之一：

1.  调用 [**IoAllocateMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl) 可分配描述部分用户缓冲区的 MDL。

2.  调用 [**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) 锁定用户缓冲区的部分。

3.  传输此部分缓冲区的数据。

4.  调用 [**MmUnlockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) 并执行以下操作之一：
    -   如果在步骤1中分配的驱动程序足够大，以便进行下一次传输，请调用 [**MmPrepareMdlForReuse**](./mm-bad-pointer.md) 并重复步骤2到4。
    -   否则，请调用 [**IoFreeMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreemdl) 并重复步骤1到4。

5.  传输所有数据后，调用 [**MmUnlockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) 和 [**IoFreeMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreemdl) 。

如果最高级别的驱动程序无法在内存有限的计算机中使用 [**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) 锁定整个用户缓冲区，则可以执行以下操作：

1.  调用 [**IoBuildSynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest) 以分配部分传输 IRP 并锁定部分用户缓冲区。 锁定区域通常是 **页面 \_ 大小** 的倍数，或调整大小以适合基础设备的传输容量。

2.  对于部分传输 IRP，请调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，并调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 以等待驱动程序设置的事件对象与其部分传输 IRP 关联（如果驱动程序返回状态为 "挂起"） \_ 。

3.  当它重新获得控制时，请重复步骤1和步骤2，直到传输所有数据，然后完成原始 IRP。

当存储类驱动程序拆分基本 SCSI 端口/微型端口驱动程序的大型传输请求时，它将为传输请求的每个部分分配其他 IRP。 它为每个驱动程序分配的 IRP 注册一个 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，以跟踪完整传输请求的状态，并释放已分配给驱动程序的 irp。 然后，它使用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将这些 irp 发送到端口驱动程序。

仅当类驱动程序可以确定可用于端口驱动程序的映射寄存器数量时，其他类/端口驱动程序才可以使用此方法。 端口驱动程序必须将此配置信息存储到配对类驱动程序的注册表中，否则成对驱动程序必须使用内部设备 i/o 控制请求来定义专用接口，以将有关可用映射寄存器数量的配置信息从端口驱动程序传递到类驱动程序。

整体驱动程序 (也就是说，不属于 DMA 设备的类/端口对) 的驱动程序必须将大型传输请求拆分为其本身。 此类驱动程序通常会将大请求拆分为多个部分，并执行一系列 DMA 操作来满足 IRP 的要求。

如果传输请求太大，无法处理基础设备驱动程序，则较高级别的驱动程序可以调用 [**MmGetMdlVirtualAddress**](./mm-bad-pointer.md) 和 [**IoBuildPartialMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl)，然后为底层设备驱动程序设置部分传输的 irp 序列。

 

