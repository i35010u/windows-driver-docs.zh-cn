---
title: 使用常见缓冲区总线 Master DMA
description: 使用常见缓冲区总线 Master DMA
ms.assetid: 55b5d819-e257-4863-b02a-5eeb83f72c65
keywords:
- 连续 DMA WDK 内核
- 常见缓冲区 DMA WDK 内核
- DMA 传输 WDK 内核，常见的缓冲区
- 主总线 DMA WDK 内核
- DMA 传输 WDK 内核，总线 master DMA
- 适配器对象 WDK 内核，总线 master DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: eee81671cc1e0125112803c23cfc76109a2377ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521622"
---
# <a name="using-common-buffer-bus-master-dma"></a>使用常见缓冲区总线 Master DMA





如中所述[使用总线 Master DMA](using-bus-master-dma.md)、 总线 master DMA 设备的某些驱动程序以独占方式，使用常见缓冲区 DMA 和一些使用常见缓冲区 DMA 数据包基于 DMA 与结合使用。

经济实惠的方式使用常见缓冲区 DMA。 设置常见缓冲区可以占用部分 （或全部，具体取决于请求的缓冲区大小） 与该适配器对象，表示主机总线适配器相关联的映射寄存器。

设置常见缓冲区区域经济方面，如通过使用**页上\_大小**区块或单个分配，使可供基于数据包的 DMA 操作的详细映射寄存器。 它还留出更多可用的系统内存用于其他目的，这将产生更好的整体驱动程序和系统性能。

若要为总线 master DMA 设置常见缓冲区，总线 master DMA 设备驱动程序必须调用[ **AllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff540575)返回的适配器对象指针[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)。 通常情况下，驱动程序，可以从此调用其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程对于[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。 仅当它将使用缓冲区重复其 DMA 操作而驱动程序保持加载状态，驱动程序应分配常见缓冲区。 下图说明了此类调用到**AllocateCommonBuffer**。

![说明的总线 master dma 的常见缓冲区分配的关系图](images/3halcbff.png)

请求的缓冲区，作为 LengthForBuffer 上, 图中所示的大小确定多少映射寄存器必须用于提供常见的缓冲区的虚拟到逻辑映射。 使用[**字节\_TO\_页**](https://msdn.microsoft.com/library/windows/hardware/ff540709)宏来确定页面所需的最大数目 (**字节\_TO\_页**(*LengthForBuffer*))。 此值不能大于*NumberOfMapRegisters*返回的[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)。

此外，调用方必须提供以下：

-   一个布尔值，该值指示是否应启用缓存

    **请注意**将忽略此值。 操作系统确定是否启用常见是要分配的缓冲区中的内存缓存。 该决定取决于处理器体系结构和设备总线。 

    使用基于 x86 的、 基于 x64 和基于 Itanium 处理器的计算机，启用了内存缓存。 

    在使用 ARM 或基于 ARM 64 的处理器的计算机，操作系统不会自动启用的所有设备的内存缓存。 系统依赖于每个设备，以确定设备是否缓存连贯的 ACPI_CCA 方法。 

-   指向驱动程序定义的变量将包含设备可访问的基*逻辑地址*缓冲区 (上图中 BufferLogicalAddress) 从返回**AllocateCommonBuffer**

如果调用成功， **AllocateCommonBuffer**返回的缓冲区 (BufferVirtualAddress 上图中)，该驱动程序必须保存在其设备扩展中，控制器的驱动程序可以访问基虚拟地址扩展或其他驱动程序可访问驻留的存储区域 （非分页缓冲池分配驱动程序）。

**AllocateCommonBuffer**将返回**NULL**如果它不能为缓冲区分配内存。 返回基虚拟地址是否**NULL**、 驱动程序要么必须以独占方式使用系统的基于数据包的 DMA 支持或驱动程序时不能**IRP\_MN\_启动\_设备**请求，返回状态\_不足\_资源。

否则，该驱动程序可以使用分配的常见缓冲区作为驱动程序和适配器访问的存储区域 DMA 传输。

当 PnP 管理器发送 IRP 停止或删除设备时，该驱动程序必须调用[ **FreeCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff546511)释放它已经分配了每个常见缓冲区。

 

 




