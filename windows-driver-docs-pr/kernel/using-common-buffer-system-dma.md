---
title: 使用公用缓冲区系统 DMA
description: 使用公用缓冲区系统 DMA
ms.assetid: ee060aa4-2db4-4bd2-b107-b71acced97fd
keywords:
- 系统 DMA WDK 内核，公共缓冲区
- 常见缓冲区 DMA WDK 内核
- DMA 传输 WDK 内核，公共缓冲区
- AllocateCommonBuffer
- 自动初始化模式 WDK DMA
- 连续 DMA WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f911395ef65d3db05304a2dad7553f077e7a7226
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190029"
---
# <a name="using-common-buffer-system-dma"></a>使用公用缓冲区系统 DMA





使用系统 DMA 控制器的自动初始化模式的驱动程序必须为缓冲区分配内存，以便可以从中执行 DMA 传输。驱动程序调用[**AllocateCommonBuffer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer)来获取此缓冲区，通常来自处理[**IRP \_ MN \_ 开始 \_ 设备**](./irp-mn-start-device.md)请求的[*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程。 下图显示了驱动程序如何分配缓冲区，以及如何将其虚拟地址范围映射到系统物理内存。

![阐释驱动程序如何为系统 dma 分配公用缓冲区的关系图](images/3hlsysbf.png)

如上图所示，驱动程序执行以下步骤来为系统 DMA 分配缓冲区：

1.  驱动程序调用 [**AllocateCommonBuffer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer)，并将指针传递到 [**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)返回的适配器对象，以及为其缓冲区请求的长度（以字节为单位）。 若要经济地使用内存，缓冲区的输入 *长度* 值应小于或等于页面 \_ 大小，或者应该是页面大小的整数倍 \_ 。

2.  如果 **AllocateCommonBuffer** 返回一个 **空** 指针，则驱动程序应释放它已声明的任何系统资源，并 \_ \_ 在响应 **IRP \_ MN \_ START \_ 设备** 请求时返回状态资源不足。

    否则， **AllocateCommonBuffer** 将在系统虚拟地址空间中分配所请求的内存量，并将两个不同类型的指针返回到该缓冲区：

    -   上图) 中的缓冲区 (BufferLogicalAddress 的 *LogicalAddress* ，驱动程序必须为其提供存储，但此后应该忽略它

    -   缓冲区的虚拟地址 (上图中的 BufferVirtualAddress) ，驱动程序也必须存储该地址，以便能够为 DMA 操作生成描述其缓冲区的 MDL

    驱动程序应将这些指针存储在设备扩展或其他驱动程序分配的内存中。

3.  驱动程序调用 [**IoAllocateMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl) 为缓冲区分配 MDL。 驱动程序传递由**AllocateCommonBuffer**返回的缓冲区的*VirtualAddress*和其缓冲区的*长度*，以分配 MDL。

4.  驱动程序调用 [**MmBuildMdlForNonPagedPool**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool) ，并使用 **IoAllocateMdl** 返回的指针将其常驻缓冲区的虚拟地址范围映射到系统物理内存。

分配公用缓冲区并映射其虚拟地址范围之后，从属设备的驱动程序可以开始处理请求 DMA 传输的 IRP。 为此，该驱动程序将调用以下常规的支持例程顺序：

1.  在驱动程序编写器自行决定的情况下， [**RtlMoveMemory**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlmovememory) 将数据从锁定的用户缓冲区复制到驱动程序分配的用于传输到设备的公用缓冲区

2.  当驱动程序准备好将其设备用于 DMA 并且需要系统 DMA 控制器时， **AllocateAdapterChannel**

3.  [**MapTransfer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)，具有描述驱动程序分配的公用缓冲区的 MDL，用于为传输操作设置系统 DMA 控制器

    请注意，驱动程序只调用一次 **MapTransfer** ，将系统 DMA 控制器设置为使用其公共缓冲区。 在传输过程中，驱动程序可以调用 [**ReadDmaCounter**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pread_dma_counter) 来确定要传输的字节数，如有必要，可调用 **RtlMoveMemory** 将更多的数据复制到用户缓冲区或从用户缓冲区复制更多数据。

4.  当驱动程序完成与从属设备的 DMA 传输时， [**FlushAdapterBuffers**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)

5.  一旦传输了所有请求的数据，或由于设备 i/o 错误而导致 IRP 失败， [**FreeAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)

**IoGetDmaAdapter**返回的适配器对象指针是每个支持例程（ **RtlMoveMemory**除外）的必需参数。

各个驱动程序会在不同的点调用此支持例程序列，这取决于每个驱动程序的实现方式，以便为其设备提供服务。 例如，一个驱动程序的 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程可能会调用 **AllocateAdapterChannel**，另一个驱动程序可能会从从驱动程序创建的联锁队列中删除 irp 的例程进行此调用，并且仍有另一个驱动程序可以在其从属 DMA 设备指示它已准备好传输数据时进行此调用。

 

