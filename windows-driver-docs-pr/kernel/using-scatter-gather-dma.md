---
title: 使用分散/聚合 DMA
description: 使用分散/聚合 DMA
ms.assetid: dacc618f-d4d4-4c3c-a18c-baeef779e931
keywords:
- AdapterListControl 例程
- 散播-聚集 DMA WDK I/O
- PutScatterGatherList
- GetScatterGatherList
- DMA 传输 WDK 内核，散播-聚集 DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b2227b4bf979e90a35375764b18eb74441337da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562478"
---
# <a name="using-scattergather-dma"></a>使用分散/聚合 DMA





执行系统的驱动程序或总线 master、 基于数据包的 DMA 可以使用专门设计用于分散/聚拢 DMA 支持例程。 而不是调用的一系列中所述的例程[Using Packet-Based 系统 DMA](using-packet-based-system-dma.md)并[基于数据包的总线-Master DMA](using-packet-based-bus-master-dma.md)，驱动程序可以使用[ **GetScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff546531)并[ **PutScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff559967)。

设备不需要具有其驱动程序使用这些例程的内置散播-聚集支持。

使用基于数据包的 DMA 的驱动程序调用散播-聚集操作支持例程的以下一般规则：

1.  [**MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)进入 MDL，用作对的调用中的参数所需索引**GetScatterGatherList**

2.  [**GetScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff546531)时驱动程序已准备好编程 DMA 其设备，并且需要系统 DMA 控制器或主机总线适配器

    **GetScatterGatherList**分配系统 DMA 控制器或主机总线适配器，确定多少映射注册所需和分配它们，填充在散播-聚集列表中，并调用驱动程序的[ *AdapterListControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540513)例程 DMA 控制器或适配器和映射寄存器不可用时。

3.  [**PutScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff559967)只要所请求的所有数据已都传输或驱动程序将 IRP 因设备 I/O 错误而失败

    **PutScatterGatherList**刷新适配器缓冲区、 释放映射寄存器中，并释放分散/集中列表。 该驱动程序必须调用**PutScatterGatherList**它可以访问缓冲区中的数据之前。

所返回的适配器对象指针**IoGetDmaAdapter**是必需的参数，为每个例程除**MmGetMdlVirtualAddress**，这需要一个指向在 MDL *Irp* - &gt; **MdlAddress**。

**GetScatterGatherList**例程包括对调用**AllocateAdapterChannel**并**MapTransfer**，因此驱动程序不需要进行这些调用。 例程将执行以下内容作为参数：

-   一个指向[ **DMA\_适配器**](https://msdn.microsoft.com/library/windows/hardware/ff544062)返回的结构[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)

-   指向 DMA 操作的目标设备对象的指针

-   指向描述在缓冲区 MDL *Irp*-&gt;**MdlAddress**

-   指向描述 Mdl 缓冲区中的当前虚拟地址的指针

-   要映射的字节数

-   一个指向[ *AdapterListControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540513)执行传输例程

-   指向要传递给驱动程序定义的上下文区域的指针*AdapterListControl*例程

-   一个布尔值：**TRUE**传输给设备;**FALSE**否则为

确定所需的映射寄存器的数目之后, 分配适配器通道和映射寄存器，散播-聚集列表中填充并准备进行传输， **GetScatterGatherList**调用驱动程序提供*AdapterListControl*例程。 *AdapterListControl*例程将 IRQL 在任意线程上下文中运行 = 调度\_级别。

*AdapterListControl*例程在调用中的驱动程序提供**GetScatterGatherList**不同于[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)传递给例程**AllocateAdapterChannel**中以下重要尊重：

-   *AdapterListControl*例程采用没有返回值，而*AdapterControl*例程返回[ **IO\_分配\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff550534).

-   而不是一个指向*MapRegisterBase*系统分配的映射寄存器，到第三个参数为*AdapterListControl*例程改为指向[ **散点图\_收集\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff563664)驱动程序可以通过它执行 DMA 的结构。

-   *AdapterListControl*例程执行中所需的任务的一小部分*AdapterControl*例程。

    *AdapterListControl*例程不会调用**AllocateAdapterChannel**或**MapTransfer**。 其唯一职责是保存输入的散播-聚集列表指针，设置其设备，并使用散播-聚集列表来执行 DMA。

散播-聚集列表结构包括**散点图\_收集\_元素**数组和数组中的元素数。 数组的每个元素提供的长度和从物理上连续散播-聚集区域的物理地址。 驱动程序使用在数据传输中的长度和地址。

驱动程序可以使用**GetScatterGatherList**而不考虑其设备支持散播-聚集 DMA 的是否。 设备不支持散播-聚集 DMA，散播-聚集列表将包含仅有一个元素。

使用散播-聚集例程通过调用可以提高性能**AllocateAdapterChannel** (如前面所述[Using Packet-Based 系统 DMA](using-packet-based-system-dma.md)和[基于使用的数据包的Bus-Master DMA](using-packet-based-bus-master-dma.md))。 与对的调用不同**AllocateAdapterChannel**，对多个调用**GetScatterGatherList**可以将排队以进行设备对象一次。 驱动程序可以调用**GetScatterGatherList**再次用于在之前的相同驱动程序对象上的另一 DMA 操作其*AdapterListControl*例程已完成执行。

在从驱动程序提供返回*AdapterListControl*例程**GetScatterGatherList**保留映射注册但释放 DMA 适配器结构。

当驱动程序已满足当前 IRP 的传输请求，或者必须失败由于设备或总线 I/O 错误 IRP 时，它必须调用**PutScatterGatherList**它可以访问缓冲区中传输的数据之前。 **PutScatterGatherList**刷新适配器缓冲区并释放映射寄存器和分散/集中列表。

 

 




