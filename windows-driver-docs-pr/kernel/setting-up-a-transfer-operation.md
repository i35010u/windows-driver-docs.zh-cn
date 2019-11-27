---
title: 设置传输操作
description: 设置传输操作
ms.assetid: cabac16d-b946-4b96-af2c-5fd0a0d848da
keywords:
- 总线主控 DMA WDK 内核
- DMA 传输 WDK 内核，总线主机 DMA
- 适配器对象 WDK 内核，主线-主 DMA
- 逻辑地址范围 WDK DMA
- 解决 WDK DMA
- 传输操作 WDK DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9f488bf04c0bcca185c1264d09337ba6f726d48
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838436"
---
# <a name="setting-up-a-transfer-operation"></a>设置传输操作





当[**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)将控制权移交给驱动程序的[*AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程时，它已分配一组映射寄存器。 但是，驱动程序必须将当前 IRP 的传输请求的系统物理内存映射到主线主机适配器的逻辑地址范围，如下所示：

1.  使用**Irp&gt;MdlAddress**上的 MDL 调用[**MmGetMdlVirtualAddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) ，以获取应该开始传输的系统物理地址的索引。

    返回值是[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)的必需参数（*CurrentVa*）。

2.  调用**MapTransfer**将 IRP 缓冲区的系统物理地址范围映射到主线主机适配器的逻辑地址范围。

然后，该驱动程序可以为传输操作设置适配器。 下图显示了设置传输所涉及的步骤。

![说明如何设置传输操作的关系图](images/3dmabus.png)

如上图所示，驱动程序的*AdapterControl*例程将设置一个总线主控 DMA 操作，如下所示：

1.  *AdapterControl*例程获取开始传输的地址。 为了满足 IRP 的初始传输要求， *AdapterControl*例程会调用[**MmGetMdlVirtualAddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)，并将一个指针传递到 MDL **&gt;MdlAddress**上的 MDL，后者描述了此 DMA 传输的缓冲区。

    **MmGetMdlVirtualAddress**返回一个虚拟地址，驱动程序可以使用该地址作为要开始传输的系统物理地址的索引。

    如果 IRP 需要多个传输操作，则驱动程序将计算更新的起始地址，如本节后面部分所述。

2.  *AdapterControl*例程保存**MmGetMdlVirtualAddress**返回的地址，或在步骤1中计算的地址。 此地址是[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)的必需参数（*CurrentVa*）。

3.  *AdapterControl*例程将调用**MapTransfer**，这将返回一个逻辑地址，驱动程序可以在该位置对总线-主适配器进行编程，以开始传输操作。 在对**MapTransfer**的调用中，驱动程序提供以下参数：
    -   IoGetDmaAdapter 返回的适配器对象指针[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)

    -   一个指针，指向当前 IRP 的**irp&gt;MdlAddress**的 MDL

    -   通过**AllocateAdapterChannel**传递到驱动程序的*AdapterControl*例程的*MapRegisterBase*句柄（请参阅[分配主线-主适配器对象](allocating-the-bus-master-adapter-object.md)）

    -   如果这是第一次调用当前 IRP 的**MapTransfer** ，则为**MmGetMdlVirtualAddress**返回的值

        否则，驱动程序提供更新的*CurrentVa*值，指示要执行的下一个物理到逻辑映射。 （本部分稍后将介绍如何计算更新的*CurrentVa* 。）

    -   指向变量的指针（*长度*），指示此传输的字节数

        如果驱动程序具有足够的映射寄存器，可在单个 DMA 操作中传输所有请求的数据，并且对其 DMA 操作没有特定于设备的约束，则可以将该*长度*设置为 IRP 的驱动程序 i/o 堆栈位置中的**长度**值. 输入长度最多可以是（页\_大小 \* 由**IoGetDmaAdapter**返回的*NumberOfMapRegisters* ）。 否则，驱动程序必须拆分请求（如[拆分传输请求](splitting-dma-transfer-requests.md)中所述），并且必须更新当前 IRP 对**MapTransfer**的后续调用中的*长度*值。

    -   布尔值（*WriteToDevice*），指示传输操作的方向（将数据从内存传输到设备时为 TRUE）

4.  *AdapterControl*例程为 DMA 操作设置设备。

5.  *AdapterControl*例程返回**DeallocateObjectKeepRegisters**。

如果驱动程序必须多次**调用 MapTransfer**以满足当前 IRP，则它会在每次调用**MapTransfer**时提供相同的适配器对象指针、 *Mdl*指针、 *MapRegisterBase*句柄和传输方向。 但是，驱动程序必须在其第二次调用和对**MapTransfer**的后续调用中提供更新的*CurrentVa*和*Length*值。 使用以下公式计算这些值：

-   *CurrentVa* = *CurrentVa* + （在前面对**MapTransfer**的调用中请求的*长度*）

-   *长度*= 最小值（要传输的剩余**长度**，（页\_大小 \* 由**IoGetDmaAdapter**返回的*NumberOfMapRegisters* ））

每个驱动程序应保持其 DMA 传输的上下文信息取决于其特定设备的需求。 典型上下文可能包括 MDL 中的当前虚拟地址（*CurrentVa*）、目前传输的字节数、传输的剩余字节数，以及可能是指向当前 IRP 的指针。

对于具有散点/集合功能的设备驱动程序， **MapTransfer**的*长度*参数为输入参数和输出参数。 从**MapTransfer**返回时，它指示系统映射了多少字节的数据。 也就是说，*长度*的返回值与返回的逻辑地址组合在一起，指示在此 DMA 操作中，总线主适配器可用于这部分传输的逻辑地址范围。

**请注意**   在**MapTransfer**覆盖*长度*后，请遵循以下实现准则：绝不会向 IRP 的驱动程序 i/o 堆栈位置中的**长度**传递指针作为*长度*参数**MapTransfer**如果你的设备支持分散/收集。

这样做可能会销毁当前 IRP 中的值，从而无法确定驱动程序是否已传输所有请求的数据。

 

在每个 DMA 操作结束时，驱动程序必须使用有效的适配器对象指针和*MapRegisterBase*句柄调用[**FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) ，以确保所有数据都已传输，并为当前 DMA 操作。 如果驱动程序必须设置其他 DMA 操作来满足当前 IRP，则必须在每次传输操作完成后调用**FlushAdapterBuffers** 。

当所有请求的传输完成或者驱动程序必须为 IRP 返回错误状态时，驱动程序应在其最后一次调用**FlushAdapterBuffers**后立即调用[**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers) ，以获得可能的最大吞吐量总线主机适配器。 在对**FreeMapRegisters**的调用中，驱动程序必须传递在前面对**AllocateAdapterChannel**的调用中传递的适配器对象指针。

 

 




