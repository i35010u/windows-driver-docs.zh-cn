---
title: 为基于数据包的 DMA 设置系统 DMA 控制器
description: 为基于数据包的 DMA 设置系统 DMA 控制器
ms.assetid: 3a646169-1ea3-4844-b771-d08f4ddec460
keywords:
- 系统 DMA WDK 内核，基于数据包
- 基于数据包的 DMA WDK 内核
- DMA 传输 WDK 内核，基于数据包
- AllocateAdapterChannel
- MapTransfer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87946c145368ad58f3122b76b86265d3252a28ea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836336"
---
# <a name="setting-up-the-system-dma-controller-for-packet-based-dma"></a>为基于数据包的 DMA 设置系统 DMA 控制器





当[**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)将控制权移交给驱动程序的[*AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程时，驱动程序 "拥有" 系统 DMA 控制器和一组映射寄存器。 然后，驱动程序必须为传输操作设置 DMA 控制器，如下图所示。

![阐释系统 dma 控制器编程的关系图](images/3dmaptsf.png)

如果驱动程序具有[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程，则[**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)会将*PIrp*参数中 **&gt;DeviceObject CurrentIrp**的指针传递到*AdapterControl*例程。 然而，如果驱动程序管理自己的 Irp 队列，则驱动程序应在其传递到*AdapterControl*的上下文中包含一个指向当前 IRP 的指针。

如上图所示，驱动程序的*AdapterControl*例程将设置 DMA 传输，如下所示：

1.  *AdapterControl*例程获取开始传输的地址。 为了满足 IRP 的初始传输要求， *AdapterControl*例程会调用[**MmGetMdlVirtualAddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)，并将一个指针传递到 MDL **&gt;MdlAddress**上的 MDL，后者描述了此 DMA 传输的缓冲区。

    **MmGetMdlVirtualAddress**返回一个虚拟地址，驱动程序可以使用该地址作为要开始传输的系统物理地址的索引。

    如果 IRP 需要多个传输操作，则驱动程序将计算更新的起始地址，如本节后面部分所述。

2.  *AdapterControl*例程保存**MmGetMdlVirtualAddress**返回的地址，或在步骤1中计算的地址。 此地址是[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)的必需参数（*CurrentVa*）。

3.  *AdapterControl*例程调用**MapTransfer**来设置系统 DMA 控制器，同时提供以下参数：

    -   IoGetDmaAdapter 返回的适配器对象指针[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)

    -   当前 IRP **&gt;MdlAddress**的 MDL 到 Mdl 的指针（*Mdl*）

    -   通过**AllocateAdapterChannel**传递到驱动程序的*AdapterControl*例程的*MapRegisterBase*句柄

    -   如果这是第一次调用 IRP 的**MapTransfer** ，则为**MmGetMdlVirtualAddress**返回的值（*CurrentVa*）

        否则，驱动程序将提供更新的*CurrentVa*值，指示下一次传输操作应在缓冲区中的哪个位置启动。

    -   指向变量的指针（*长度*），指示此传输的字节数

        如果驱动程序可以通过单个调用**MapTransfer**传输所有请求的数据，并且对其 DMA 操作没有特定于设备的约束，则可以将*LENGTH*设置为 IRP 的驱动程序 i/o 堆栈位置中的**长度**值。 在大多数情况下，长度（以字节为单位）可以是（页\_大小 \* 由[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)返回的*NumberOfMapRegisters* ）。 否则，驱动程序必须拆分请求（如[拆分传输请求](splitting-dma-transfer-requests.md)中所述），并且必须更新当前 IRP 对**MapTransfer**的后续调用中的*长度*值。

    -   布尔值（*WriteToDevice*），指示传输操作的方向（将数据从系统内存传输到设备时为 TRUE）

    **MapTransfer**返回一个逻辑地址。 使用系统 DMA 的驱动程序必须忽略此值。

4.  *AdapterControl*例程为 DMA 操作设置设备。

5.  *AdapterControl*例程返回**KeepObject**。

当设备指示其当前 DMA 操作已完成时，驱动程序应调用[**FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)，通常从驱动程序的[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程调用。

完成 DMA 操作的*DpcForIsr*例程或其他驱动程序例程会调用**FlushAdapterBuffers** ，以确保将系统 DMA 控制器中缓存的所有数据读入系统内存或写出到设备。 如果需要重新编程系统 DMA 控制器为当前 IRP 传输更多数据，则同一例程还必须再次调用**MapTransfer** 。 同样，它必须在每次传输操作之后再次调用**FlushAdapterBuffers** 。

如果对于当前 IRP，驱动程序必须多次调用**MapTransfer** ，则它会在每次调用中提供相同的适配器对象指针、 *Mdl*指针、 *MapRegisterBase*句柄和传输方向。 但是，驱动程序必须先更新*CurrentVa*和*Length*参数，然后再进行第二次调用和对**MapTransfer**的后续调用。 若要计算每个参数的更新值，请使用以下公式：

-   *CurrentVa* = *CurrentVa* + （在前面对**MapTransfer**的调用中请求的*长度*）

-   *长度*= 最小值（要传输的剩余**长度**，（页\_大小 \* 由**IoGetDmaAdapter**返回的*NumberOfMapRegisters* ））

每个驱动程序应保持其 DMA 传输的上下文信息取决于其特定设备的需求。 典型上下文可能包括 MDL 中的当前虚拟地址（*CurrentVa*）、目前传输的字节数、传输的剩余字节数、可能是指向当前 IRP 的指针，以及驱动程序编写器认为的任何其他信息有利于.

请求的传输完成后，或者如果驱动程序必须返回 IRP 的错误状态，则驱动程序应立即调用[**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel) ，以释放系统 DMA 控制器以使其他驱动程序和此驱动程序可供使用。

 

 




