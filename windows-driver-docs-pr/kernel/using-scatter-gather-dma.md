---
title: 使用分散/聚合 DMA
description: 使用分散/聚合 DMA
ms.assetid: dacc618f-d4d4-4c3c-a18c-baeef779e931
keywords:
- AdapterListControl 例程
- 散播/聚集 DMA WDK i/o
- PutScatterGatherList
- GetScatterGatherList
- DMA 传输 WDK 内核、散播/聚集 DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6d239451b19ac76cc6b42ff570dce61668439a9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193079"
---
# <a name="using-scattergather-dma"></a>使用分散/聚合 DMA





执行系统或总线主机的驱动程序，基于数据包的 DMA 可以使用专为散播/聚集 DMA 设计的支持例程。 驱动程序可以使用[**GetScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list)和[**PutScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list)，而不是调用[使用基于数据包的系统 Dma](using-packet-based-system-dma.md)和[基于数据包的总线主机 dma](using-packet-based-bus-master-dma.md)中所述的例程序列。

设备不需要为其驱动程序提供内置的散播/聚集支持即可使用这些例程。

使用基于数据包的 DMA 的驱动程序将调用以下常规的支持例程序列来实现散点/收集操作：

1.  [**MmGetMdlVirtualAddress**](./mm-bad-pointer.md)获取 MDL 的索引，需要在调用**GetScatterGatherList**时作为参数

2.  当驱动程序准备好将其设备用于 DMA 并且需要系统 DMA 控制器或主线-主适配器时， [**GetScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list)

    **GetScatterGatherList** 分配系统 dma 控制器或主线主机适配器，确定需要多少个映射寄存器，并在其中填充散点/集合列表，并在 DMA 控制器或适配器和映射寄存器可用时调用驱动程序的 [*AdapterListControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_list_control) 例程。

3.  一旦传输了所有请求的数据，或由于出现设备 i/o 错误， [**PutScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list)将导致 IRP 失败

    **PutScatterGatherList** 刷新适配器缓冲区，释放映射寄存器，并释放散点/集合列表。 驱动程序必须先调用 **PutScatterGatherList** ，然后才能访问缓冲区中的数据。

**IoGetDmaAdapter**返回的适配器对象指针是每个例程的必需参数（ **MmGetMdlVirtualAddress**除外），这需要指向*Irp* - &gt; **MdlAddress**上的 MDL 的指针。

**GetScatterGatherList**例程包括对**AllocateAdapterChannel**和**MapTransfer**的调用，因此，驱动程序不必进行这些调用。 例程采用以下参数：

-   指向由[**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)返回的[**DMA \_ 适配器**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_adapter)结构的指针

-   一个指针，指向 DMA 操作的目标设备对象

-   指向描述*Irp* - &gt; **MdlAddress**中的缓冲区的 MDL 的指针

-   一个指针，指向由 Mdl 描述的缓冲区中的当前虚拟地址

-   要映射的字节数

-   指向执行传输的 [*AdapterListControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_list_control) 例程的指针

-   指向要传递到 *AdapterListControl* 例程的驱动程序定义的上下文区域的指针

-   布尔值：对于到设备的传输，为**TRUE** ;否则**为 FALSE**

确定所需的映射寄存器的数目后，分配适配器通道和映射寄存器，填写散点/集合列表并准备传输， **GetScatterGatherList** 将调用驱动程序提供的 *AdapterListControl* 例程。 *AdapterListControl*例程以 IRQL = 调度级别的任意线程上下文运行 \_ 。

在对**GetScatterGatherList**的调用中，驱动程序提供的*AdapterListControl*例程不同于在以下重要方面传递给**AllocateAdapterChannel**的[*AdapterControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程：

-   *AdapterListControl*例程没有返回值，而*AdapterControl*例程则返回[**IO \_ 分配 \_ 操作**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_allocation_action)。

-   *AdapterListControl*例程的第三个参数而不是指向系统分配的映射寄存器的*MapRegisterBase*的指针，而是指向一个[**散点 \_ 集合 \_ 列表**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_scatter_gather_list)结构，驱动程序可以通过该结构执行 DMA。

-   *AdapterListControl*例程执行*AdapterControl*例程中所需的部分任务。

    *AdapterListControl*例程不调用**AllocateAdapterChannel**或**MapTransfer**。 其唯一职责是保存输入散播/聚集列表指针，设置其设备，并使用散点/集合列表执行 DMA。

散点/集合列表结构包含 **散点 \_ 集合 \_ 元素** 数组和数组中元素的数目。 数组的每个元素都提供物理上邻接的分散/收集区域的长度和起始物理地址。 驱动程序在数据传输中使用长度和地址。

无论设备是否支持散播/聚集 DMA，驱动程序都可以使用 **GetScatterGatherList** 。 对于不支持散点/集合 DMA 的设备，散点/集合列表将仅包含一个元素。

与使用[基于数据包的系统 dma](using-packet-based-system-dma.md)并[使用基于数据包的总线主机 dma](using-packet-based-bus-master-dma.md)) 一样，使用散点/收集例程可以提高 (调用**AllocateAdapterChannel**的性能。 不同于对 **AllocateAdapterChannel**的调用，可以在任何一 **次为设备** 对象将多个调用排入队列。 当驱动程序的*AdapterListControl*例程执行完毕之前，驱动程序可以再次为同一驱动程序对象上的另一个 DMA 操作调用**GetScatterGatherList** 。

当从驱动程序提供的 *AdapterListControl* 例程返回时， **GetScatterGatherList** 将保留映射寄存器，但会释放 DMA 适配器结构。

当驱动程序已满足当前 IRP 的传输请求或由于设备或总线 i/o 错误而导致 IRP 失败时，它必须先调用 **PutScatterGatherList** ，然后才能访问缓冲区中传输的数据。 **PutScatterGatherList** 刷新适配器缓冲区并释放 "映射寄存器" 和 "散点/集合" 列表。

 

