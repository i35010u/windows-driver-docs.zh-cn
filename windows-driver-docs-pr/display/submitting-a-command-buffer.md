---
title: 提交命令缓冲区
description: 提交命令缓冲区
ms.assetid: 3622697a-3989-4756-89d4-c67c81815d49
keywords:
- 命令缓冲区 WDK 显示，提交
- 提交命令缓冲区 WDK 显示
- 传递命令缓冲区 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 473ec72edca76056ae70e81df6c665021669acac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829427"
---
# <a name="submitting-a-command-buffer"></a>提交命令缓冲区


## <span id="ddk_submitting_a_command_buffer_gg"></span><span id="DDK_SUBMITTING_A_COMMAND_BUFFER_GG"></span>


若要通过 Windows Vista 图形堆栈传递命令缓冲区，必须执行以下序列操作：

1.  如果 Direct3D 运行时调用以下用户模式显示驱动程序函数之一来执行指定的操作，则用户模式显示驱动程序将启动命令缓冲区提交：

    -   用于显示图形的[**当前**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present)函数。
    -   用于提交硬件命令的[**Flush**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_flush)函数。
    -   用于锁定在当前命令批处理中使用的资源的[**锁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)函数。

    请注意，每当命令缓冲区已满时，用户模式显示驱动程序也始终会启动命令缓冲区提交。

2.  用户模式显示驱动程序调用 Direct3D 运行时的[**pfnRenderCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)函数来向运行时提交命令缓冲区。

3.  DirectX 图形内核子系统调用显示微型端口驱动程序的[**DxgkDdiRender**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)或[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)函数来验证命令缓冲区，以硬件的格式写入 DMA 缓冲区，并生成一个分配列表，其中描述了使用的图面。 请注意，DMA 缓冲区尚未进行修补（即分配的物理地址）。
    **请注意**   如果运行时通过调用用户模式显示驱动程序的[**当前**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present)函数来启动命令缓冲区提交，图形子系统将调用显示微型端口驱动程序的[**DxgkDdiPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)函数，而不是[**DxgkDdiRender**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_render)或[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)。

     

4.  视频内存管理器调用显示微型端口驱动程序的[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数来创建特殊用途的 DMA 缓冲区（称为分页缓冲区），该缓冲区用于移动 DMA 缓冲区随附的分配列表中指定的分配和从 GPU 可访问的内存。 有关详细信息，请参阅[分页视频内存资源](paging-video-memory-resources.md)。

5.  GPU 计划程序调用显示微型端口驱动程序的[**DxgkDdiPatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)函数，以将物理地址分配给 DMA 缓冲区中的资源。 不过，计划程序不需要调用**DxgkDdiPatch**来将物理地址分配给分页缓冲区，因为分页缓冲区的物理地址是在[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)调用期间传入和分配的。

6.  GPU 计划程序调用显示微型端口驱动程序的[**DxgkDdiSubmitCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)函数，请求驱动程序将分页缓冲区排队到 GPU 执行单元。

7.  GPU 计划程序调用显示微型端口驱动程序的[**DxgkDdiSubmitCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)函数，请求驱动程序将 DMA 缓冲区排队到 GPU 执行单元。 提交到 GPU 的每个 DMA 缓冲区都包含一个隔离标识符。 GPU 完成处理 DMA 缓冲区后，GPU 将生成一个中断。

8.  显示微型端口驱动程序会在其[**DxgkDdiInterruptRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)函数中通知中断。 显示微型端口驱动程序应从 GPU 读取刚完成的 DMA 缓冲区的防护标识符。

9.  显示微型端口驱动程序应调用[**DxgkCbNotifyInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt)函数，以通知 GPU 计划程序已完成 DMA 缓冲区。

10. 显示微型端口驱动程序应调用[**DxgkCbQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_queue_dpc)函数以对延迟的过程调用（DPC）进行排队。

11. 将通知显示微型端口驱动程序的 DPC 处理大多数 DMA 缓冲区处理。

 

 





