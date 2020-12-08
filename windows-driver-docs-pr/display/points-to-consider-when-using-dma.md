---
title: 使用 DMA 时需要注意的要点
description: 使用 DMA 时需要注意的要点
keywords:
- 总线主控 DMA WDK 音频微型端口，注意事项
- DMA 总线-主 WDK 视频微型端口，注意事项
- 并发 DMA WDK 视频微型端口
- VideoPortStartDma
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3deda9c0909c718ad0d4085ef63e7a90d0282dc1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795557"
---
# <a name="points-to-consider-when-using-dma"></a>使用 DMA 时需要注意的要点


## <span id="ddk_points_to_consider_when_using_dma_gg"></span><span id="DDK_POINTS_TO_CONSIDER_WHEN_USING_DMA_GG"></span>


本部分提供了在你计划在微型端口驱动程序中使用 DMA 操作时要考虑的一些重要事项。

### <a name="span-idadditional_notes_on_videoportstartdmaspanspan-idadditional_notes_on_videoportstartdmaspanadditional-notes-on-videoportstartdma"></a><span id="additional_notes_on_videoportstartdma"></span><span id="ADDITIONAL_NOTES_ON_VIDEOPORTSTARTDMA"></span>VideoPortStartDma 上的其他说明

显示驱动程序通常会将传输请求发送到微型端口驱动程序，这实际上会执行这些 DMA 传输。 显示驱动程序无法假定只是因为其 DMA 引擎处于空闲状态，因此传输请求中的所有数据都已传输。 这是因为微型端口驱动程序需要多次调用 [**VideoPortStartDma**](/windows-hardware/drivers/ddi/video/nf-video-videoportstartdma) 和 [**VideoPortCompleteDma**](/windows-hardware/drivers/ddi/video/nf-video-videoportcompletedma) ，以便进行大型传输请求。 在两个这类 DMA 操作之间，硬件的 DMA 引擎处于空闲状态，即使有其他数据需要传输也是如此。 小型端口驱动程序负责在传输请求完全完成时通知显示驱动程序。

**VideoPortStartDma** 的 *上下文* 参数应指向非分页内存，如硬件扩展中的内存。 此参数将传递给微型端口驱动程序的 [**HwVidExecuteDma**](/windows-hardware/drivers/ddi/video/nc-video-pexecute_dma) 回调例程，该例程在 IRQL 调度 \_ 级别运行。

### <a name="span-iddma_and_interruptsspanspan-iddma_and_interruptsspandma-and-interrupts"></a><span id="dma_and_interrupts"></span><span id="DMA_AND_INTERRUPTS"></span>DMA 和中断

对于很多设备，当硬件 DMA 操作完成时，将生成一个中断。 视频微型端口驱动程序的中断服务例程 (ISR) 应将 DPC 例程排队以获取更多与 DMA 相关的任务。 请勿在 ISR 中调用视频端口驱动程序的 DMA 功能，因为这些功能只能在 IRQL 调度级别或以下位置调用 \_ 。

即使在 **VideoPortStartDma** 函数尚未返回的情况下，也可以安全地检查在上述 DPC 例程中传输的大小，因为 **VideoPortStartDma** 的 *pLength* 参数指向的变量已在调用 *HwVidExecuteDma* 时进行了更新。

### <a name="span-idlogical_addresses_versus_physical_addressesspanspan-idlogical_addresses_versus_physical_addressesspanlogical-addresses-versus-physical-addresses"></a><span id="logical_addresses_versus_physical_addresses"></span><span id="LOGICAL_ADDRESSES_VERSUS_PHYSICAL_ADDRESSES"></span>逻辑地址与物理地址

视频端口驱动程序的 DMA 实现使用逻辑地址（即 DMA 硬件使用的地址）的概念。 逻辑地址可能不同于物理地址。 视频端口驱动程序提供的 DMA 函数将考虑任何特定于平台的内存限制。 出于此原因，请务必使用视频端口驱动程序 DMA 功能，而不是使用此类内核模式函数作为 [**MmGetPhysicalAddress**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmgetphysicaladdress)。 有关逻辑地址的详细信息，请参阅 [适配器对象和 DMA](../kernel/introduction-to-adapter-objects.md) 。

### <a name="span-idconcurrent_dmaspanspan-idconcurrent_dmaspanconcurrent-dma"></a><span id="concurrent_dma"></span><span id="CONCURRENT_DMA"></span>并发 DMA

对于支持并发 DMA 传输的设备，无论是在支持同时读取和写入的 DMA 控制器上，还是在两个单独的 DMA 控制器上，微型端口驱动程序应为每个并发路径获取一个单独的 DMA 适配器对象。 例如，如果设备具有两个并行工作的 DMA 控制器，则微型端口驱动程序应对 **VideoPortGetDmaAdapter** 进行两次调用，从而获取指向两副总裁 \_ DMA \_ 适配器结构的指针。 此后，每当微型端口驱动程序对特定 DMA 控制器进行 DMA 传输请求时，它应使用该请求中的相应指针。

 

