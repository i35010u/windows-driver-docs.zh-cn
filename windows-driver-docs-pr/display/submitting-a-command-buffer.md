---
title: 提交命令缓冲区
description: 提交命令缓冲区
keywords:
- 命令缓冲区 WDK 显示，提交
- 提交命令缓冲区 WDK 显示
- 传递命令缓冲区 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62dc302043778bc40285cc8435d657f57c1e20a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837793"
---
# <a name="submitting-a-command-buffer"></a>提交命令缓冲区


## <span id="ddk_submitting_a_command_buffer_gg"></span><span id="DDK_SUBMITTING_A_COMMAND_BUFFER_GG"></span>


若要通过 Windows Vista 图形堆栈传递命令缓冲区，必须执行以下序列操作：

1.  如果 Direct3D 运行时调用以下用户模式显示驱动程序函数之一来执行指定的操作，则用户模式显示驱动程序将启动命令缓冲区提交：

    -   用于显示图形的 [**当前**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present) 函数。
    -   用于提交硬件命令的 [**Flush**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush) 函数。
    -   用于锁定在当前命令批处理中使用的资源的 [**锁**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock) 函数。

    请注意，每当命令缓冲区已满时，用户模式显示驱动程序也始终会启动命令缓冲区提交。

2.  用户模式显示驱动程序调用 Direct3D 运行时的 [**pfnRenderCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb) 函数来向运行时提交命令缓冲区。

3.  DirectX 图形内核子系统调用显示微型端口驱动程序的 [**DxgkDdiRender**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render) 或 [**DxgkDdiRenderKm**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm) 函数来验证命令缓冲区，以硬件的格式写入 DMA 缓冲区，并生成一个描述所使用的表面的分配列表。 请注意，DMA 缓冲区尚未进行修补 (也就是说，) 分配的物理地址。
    **注意**   如果运行时通过调用用户模式显示驱动程序的 [**当前**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present) 函数来启动了命令缓冲区提交，图形子系统将调用显示微型端口驱动程序的 [**DxgkDdiPresent**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present) 函数，而不是 [**DxgkDdiRender**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render) 或 [**DxgkDdiRenderKm**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)。

     

4.  视频内存管理器调用显示微型端口驱动程序的 [**DxgkDdiBuildPagingBuffer**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 函数来创建特殊用途的 DMA 缓冲区，这些缓冲区称为分页缓冲区，将 dma 缓冲区随附的分配列表中指定的分配移到和移出 GPU 可访问的内存。 有关详细信息，请参阅 [分页视频内存资源](paging-video-memory-resources.md)。

5.  GPU 计划程序调用显示微型端口驱动程序的 [**DxgkDdiPatch**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch) 函数，以将物理地址分配给 DMA 缓冲区中的资源。 不过，计划程序不需要调用 **DxgkDdiPatch** 来将物理地址分配给分页缓冲区，因为分页缓冲区的物理地址是在 [*DxgkDdiBuildPagingBuffer*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 调用期间传入和分配的。

6.  GPU 计划程序调用显示微型端口驱动程序的 [**DxgkDdiSubmitCommand**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand) 函数，请求驱动程序将分页缓冲区排队到 GPU 执行单元。

7.  GPU 计划程序调用显示微型端口驱动程序的 [**DxgkDdiSubmitCommand**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand) 函数，请求驱动程序将 DMA 缓冲区排队到 GPU 执行单元。 提交到 GPU 的每个 DMA 缓冲区都包含一个隔离标识符。 GPU 完成处理 DMA 缓冲区后，GPU 将生成一个中断。

8.  显示微型端口驱动程序会在其 [**DxgkDdiInterruptRoutine**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine) 函数中通知中断。 显示微型端口驱动程序应从 GPU 读取刚完成的 DMA 缓冲区的防护标识符。

9.  显示微型端口驱动程序应调用 [**DxgkCbNotifyInterrupt**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt) 函数，以通知 GPU 计划程序已完成 DMA 缓冲区。

10. 显示微型端口驱动程序应调用 [**DxgkCbQueueDpc**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_queue_dpc) 函数，以便将延迟的过程调用排队 (DPC) 。

11. 将通知显示微型端口驱动程序的 DPC 处理大多数 DMA 缓冲区处理。

 

