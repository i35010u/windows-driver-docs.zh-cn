---
title: 使用基于数据包的系统 DMA
description: 使用基于数据包的系统 DMA
ms.assetid: 5d175193-4a28-49fd-80b5-18f116232c6e
keywords:
- DMA WDK 内核，基于数据包的系统
- 基于数据包的 DMA WDK 内核
- DMA 传输 WDK 内核，基于数据包的
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 758bac46c48c4dc24bbe81646acafe9d55c682fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523251"
---
# <a name="using-packet-based-system-dma"></a>使用基于数据包的系统 DMA





使用基于数据包的 DMA 的从属设备的驱动程序调用支持例程的以下一般规则，如它们处理 IRP 请求 DMA 传输：

-   [**KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041)之前尝试分配系统 DMA 控制器 (有关详细信息，请参阅[维护缓存一致性](maintaining-cache-coherency.md))

-   [**AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)时驱动程序已准备好编程 DMA 其设备，并且需要系统 DMA 控制器

    **AllocateAdapterChannel**，依次调用驱动程序的[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程。

-   [**MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)进入 MDL，作为首次调用中的参数所需索引**MapTransfer**

-   [**MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402)进行编程在传输操作的系统 DMA 控制器

    驱动程序可能需要调用**MapTransfer**不止一次传输请求的所有数据，如中所述[拆分传输请求](splitting-dma-transfer-requests.md)。

-   [**FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)恰好在每个 DMA 后传输操作向/从从属的设备

    如果驱动程序必须调用**MapTransfer**多个要传输所有请求的数据，它必须调用后**FlushAdapterBuffers**无数次，它会调用**MapTransfer**。

-   [**FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)只要已传输的所有请求的数据，或者如果该驱动程序将 IRP 因设备 I/O 错误而失败

所返回的适配器对象指针[ **IoGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff549220)是必需的参数，除非这些例程的每个**KeFlushIoBuffers**和**MmGetMdlVirtualAddress**，这要求在传递 MDL 指向**Irp-&gt;MdlAddress**。

单独的驱动程序在不同时间点，具体取决于每个驱动程序的实现来服务其设备的方式调用这一序列的支持例程。 例如，一个驱动程序的[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程可能会使对调用**AllocateAdapterChannel**，另一个驱动程序可能会进行此调用，从删除从 Irp 的例程驱动程序创建互锁队列，和另一个驱动程序可能会进行此调用时其从属 DMA 设备将指示它已准备好将数据传输。

 

 




