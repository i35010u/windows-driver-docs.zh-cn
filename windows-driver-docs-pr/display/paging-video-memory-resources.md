---
title: 分页视频内存资源
description: 分页视频内存资源
ms.assetid: e9734db6-3ad0-4c64-a9c6-15ba956b2dce
keywords:
- DMA 缓冲 WDK 显示，寻呼视频内存资源
- 分页视频内存资源 WDK 显示
- 视频内存资源分页 WDK 显示
- 分页缓冲区 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a81e45eae1b2307b73188e2703d6980346e7853
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064690"
---
# <a name="paging-video-memory-resources"></a>分页视频内存资源


## <span id="ddk_paging_video_memory_resources_gg"></span><span id="DDK_PAGING_VIDEO_MEMORY_RESOURCES_GG"></span>


与 Microsoft [windows 2000 显示器](windows-2000-display-driver-model-design-guide.md)驱动程序模型不同，Windows Vista 显示器驱动程序模型允许创建比可用的物理内存总量更多的视频内存资源，并根据需要将其进到和移出视频内存。 换句话说，并不是所有的视频内存资源同时在视频内存中进行。

GPU 在其管道中可以有多个 DMA 缓冲区。 这些活动 DMA 缓冲区引用的视频内存资源必须位于视频内存中。 其他空闲视频内存资源可分页到系统内存。

在 GPU 计划程序可以调用显示微型端口驱动程序的 [**DxgkDdiSubmitCommand**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand) 函数以将 dma 缓冲区提交到 GPU 之前，计划程序必须确保 DMA 缓冲区使用的所有视频内存资源实际上位于视频内存中。 如果某些资源不在视频内存中，则必须将其从系统内存中分页。 GPU 计划程序必须在视频内存管理器中调用，以便在视频内存中查找空间，以将所需的视频内存资源数据从系统内存传输到视频内存。 当视频内存需求较高时，GPU 计划程序必须在视频内存管理器中调用，以将空闲视频内存资源数据传输到系统内存，从而为所需的视频内存资源数据腾出空间。 包含用于在视频和系统内存之间传输数据的命令的特殊目的 DMA 缓冲区称为分页缓冲区。 视频内存管理器调用显示微型端口驱动程序的 [**DxgkDdiBuildPagingBuffer**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 函数来创建分页缓冲区，驱动程序会将其写入特定于硬件的数据传输命令。

 

