---
title: 使用 DMA 时需要注意的要点
description: 使用 DMA 时需要注意的要点
ms.assetid: 7bbd11d2-858c-4ed6-81a4-74ba003e7dcd
keywords:
- 主总线 DMA WDK 微型端口注意事项
- DMA 总线 master WDK 微型端口注意事项
- 并发 DMA WDK 视频微型端口
- VideoPortStartDma
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe26c24fa604001e8db28b8b6230e2c7063e7bff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365696"
---
# <a name="points-to-consider-when-using-dma"></a>使用 DMA 时需要注意的要点


## <span id="ddk_points_to_consider_when_using_dma_gg"></span><span id="DDK_POINTS_TO_CONSIDER_WHEN_USING_DMA_GG"></span>


本部分提供了一些重要事项需要考虑你是否打算在您的微型端口驱动程序中使用 DMA 运算。

### <a name="span-idadditionalnotesonvideoportstartdmaspanspan-idadditionalnotesonvideoportstartdmaspanadditional-notes-on-videoportstartdma"></a><span id="additional_notes_on_videoportstartdma"></span><span id="ADDITIONAL_NOTES_ON_VIDEOPORTSTARTDMA"></span>有关 VideoPortStartDma 的其他说明

显示驱动程序通常将传输请求发送到的微型端口驱动程序，实际上将执行这些 DMA 传输。 显示驱动程序不能假定，只是因为其 DMA 引擎处于空闲状态，传输请求中的所有数据已都转移。 这是因为微型端口驱动程序需要调用[ **VideoPortStartDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstartdma)并[ **VideoPortCompleteDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportcompletedma)多个时间对于大型传输请求。 硬件的 DMA 引擎是闲置的两个此类 DMA 操作，即使可能有其他要传输的数据。 它是微型端口驱动程序的责任转移请求已完全完成时通知显示驱动程序。

*上下文*的参数**VideoPortStartDma**应指向未分页的内存，如硬件扩展中的内存。 此参数将传递给微型端口驱动程序[ **HwVidExecuteDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pexecute_dma) IRQL 调度时运行的回调例程\_级别。

### <a name="span-iddmaandinterruptsspanspan-iddmaandinterruptsspandma-and-interrupts"></a><span id="dma_and_interrupts"></span><span id="DMA_AND_INTERRUPTS"></span>DMA 和中断

对于许多设备，硬件 DMA 操作完成时生成中断。 微型端口驱动程序的中断服务例程 (ISR) 应队列进一步 DMA 相关任务的 DPC 例程。 不要调用的视频端口驱动程序的 DMA 函数中 ISR 由于他们只能在调用或以下的 IRQL 调度\_级别。

则可以安全地检查大小正在传输在前面提到的 DPC 例程中，即使**VideoPortStartDma**函数尚未返回，因为指向的变量*pLength*的自变量**VideoPortStartDma**已更新时*HwVidExecuteDma*调用。

### <a name="span-idlogicaladdressesversusphysicaladdressesspanspan-idlogicaladdressesversusphysicaladdressesspanlogical-addresses-versus-physical-addresses"></a><span id="logical_addresses_versus_physical_addresses"></span><span id="LOGICAL_ADDRESSES_VERSUS_PHYSICAL_ADDRESSES"></span>与物理地址的逻辑地址

视频端口驱动程序的 DMA 实现使用这一概念的逻辑地址，这是 DMA 硬件使用的地址。 逻辑地址可不同于物理地址。 视频端口驱动程序提供 DMA 函数考虑到任何特定于平台的内存限制。 出于此原因，务必要使用的视频端口驱动程序 DMA 函数而不是作为此类内核模式函数[ **MmGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmgetphysicaladdress)。 请参阅[适配器对象和 DMA](https://docs.microsoft.com/windows-hardware/drivers/kernel/adapter-objects-and-dma)逻辑地址有关的详细信息。

### <a name="span-idconcurrentdmaspanspan-idconcurrentdmaspanconcurrent-dma"></a><span id="concurrent_dma"></span><span id="CONCURRENT_DMA"></span>并发 DMA

对于支持并发 DMA 传输的设备，DMA 控制器上，支持同时读取和写入操作，或者在两个单独 DMA 控制器上微型端口驱动程序应获取每个并发路径的单独 DMA 适配器对象。 例如，如果设备具有两个并行工作的 DMA 控制器，微型端口驱动程序应进行两次调用**VideoPortGetDmaAdapter**，从而获取两个副总裁的指针\_DMA\_适配器结构。 之后，每当微型端口驱动程序发出 DMA 传输请求的特定 DMA 控制器，它应使用适当的指针在该请求。

 

 





