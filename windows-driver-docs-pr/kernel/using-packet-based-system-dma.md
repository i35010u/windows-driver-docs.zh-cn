---
title: 使用基于数据包的系统 DMA
description: 使用基于数据包的系统 DMA
ms.assetid: 5d175193-4a28-49fd-80b5-18f116232c6e
keywords:
- 系统 DMA WDK 内核，基于数据包
- 基于数据包的 DMA WDK 内核
- DMA 传输 WDK 内核，基于数据包
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 592acd1025443207d7c83a105e31721814f98bb1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835926"
---
# <a name="using-packet-based-system-dma"></a>使用基于数据包的系统 DMA





使用基于数据包的 DMA 的从属设备的驱动程序在处理请求 DMA 传输的 IRP 时，调用以下一般的支持例程顺序：

-   在尝试分配系统 DMA 控制器之前[**KeFlushIoBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers) （有关详细信息，请参阅[维护缓存一致性](maintaining-cache-coherency.md)）

-   当驱动程序准备好将其设备用于 DMA 并且需要系统 DMA 控制器时， [**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)

    **AllocateAdapterChannel**调用驱动程序的[*AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程。

-   [**MmGetMdlVirtualAddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)获取 MDL 的索引，需要作为首次调用**MapTransfer**时的参数

-   用于对系统 DMA 控制器进行程序传输操作的[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)

    如[拆分传输请求](splitting-dma-transfer-requests.md)中所述，驱动程序可能需要多次调用**MapTransfer**以传输所有请求的数据。

-   [**FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)在每次进行 DMA 传输操作后（从从属设备到/）

    如果驱动程序必须多次调用**MapTransfer**以传输所有请求的数据，则必须多次调用**FlushAdapterBuffers** ，因为它调用**MapTransfer**。

-   一旦传输了所有请求的数据，或者如果由于设备 i/o 错误而导致 IRP 失败， [**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)

[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)返回的适配器对象指针是每个例程的必需参数（ **KeFlushIoBuffers**和**MmGetMdlVirtualAddress**除外），这需要指向 Irp 上传递的 MDL **&gt;MdlAddress**。

各个驱动程序会在不同的点调用此支持例程序列，这取决于每个驱动程序的实现方式，以便为其设备提供服务。 例如，一个驱动程序的[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程可能会调用**AllocateAdapterChannel**，另一个驱动程序可能会从从驱动程序创建的联锁队列中删除 irp 的例程进行此调用，并且仍有另一个驱动程序可以使此当其从属 DMA 设备指示它已准备好传输数据时调用。

 

 




