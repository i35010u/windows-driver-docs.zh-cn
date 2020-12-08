---
title: 视频内存管理和 GPU 计划
description: 视频内存管理和 GPU 计划
keywords:
- 显示驱动程序模型 WDK Windows Vista，视频内存管理
- Windows Vista 显示器驱动程序模型 WDK，视频内存管理
- 视频内存管理 WDK 显示
- GPU 计划 WDK 显示
- 显示驱动程序模型 WDK Windows Vista，GPU 计划
- Windows Vista 显示器驱动程序模型 WDK，GPU 计划
- 用户模式显示驱动程序 WDK Windows Vista，视频内存管理
- 微型端口驱动程序 WDK 显示，视频内存管理
- 用户模式显示驱动程序 WDK Windows Vista，GPU 计划
- 微型端口驱动程序 WDK 显示，GPU 计划
ms.date: 01/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4aebed64072cecca66e47341691f0ac3b21820b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802513"
---
# <a name="video-memory-management-and-gpu-scheduling"></a>视频内存管理和 GPU 计划


## <span id="ddk_video_memory_management_and_gpu_scheduling_gg"></span><span id="DDK_VIDEO_MEMORY_MANAGEMENT_AND_GPU_SCHEDULING_GG"></span>

视频内存管理器当前在以下 OS 文件中实现： 

* dxgkrnl.sys
* dxgmms1.sys
* dxgmms2.sys

这些文件仅在操作系统安装过程中可用，不能作为单独的下载提供。 这些文件的设计目的只是与随附它们的其他操作系统文件一起工作。 Microsoft 不支持这些文件之间的不匹配版本，通常不起作用。

以下各节介绍 (GPU) 计划模型的视频内存管理和图形处理单元：

[处理内存段](handling-memory-segments.md)

[处理命令和 DMA 缓冲区](handling-command-and-dma-buffers.md)

[GDI 硬件加速](gdi-hardware-acceleration.md)

[视频内存供应和回收](video-memory-offer-and-reclaim.md)

[GPU 抢占](gpu-preemption.md)

 

 





