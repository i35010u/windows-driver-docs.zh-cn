---
title: 视频内存管理和 GPU 计划
description: 视频内存管理和 GPU 计划
ms.assetid: 33fc9f0a-57ed-479f-9cb0-3f3f540047ab
keywords:
- 显示驱动程序模型 WDK Windows Vista 视频内存管理
- Windows Vista 显示器驱动程序模型 WDK，视频内存管理
- 视频内存管理 WDK 显示
- GPU 计划 WDK 显示
- 显示驱动程序模型 WDK Windows Vista 中，GPU 计划
- Windows Vista 显示器驱动程序模型 WDK，GPU 计划
- 用户模式显示驱动程序 WDK Windows Vista 中，视频内存管理
- 微型端口驱动程序 WDK 显示视频内存管理
- 用户模式显示驱动程序 WDK Windows Vista 中，GPU 计划
- 微型端口驱动程序 WDK 显示，GPU 计划
ms.date: 01/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 986f7e00453d6cefab58fa6759f62801c1bf2acc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365059"
---
# <a name="video-memory-management-and-gpu-scheduling"></a>视频内存管理和 GPU 计划


## <span id="ddk_video_memory_management_and_gpu_scheduling_gg"></span><span id="DDK_VIDEO_MEMORY_MANAGEMENT_AND_GPU_SCHEDULING_GG"></span>

在以下操作系统文件中当前实现的视频内存管理器： 

* dxgkrnl.sys
* dxgmms1.sys
* dxgmms2.sys

这些文件都仅可用作 OS 安装，并作为单独的下载不可用的一部分。 这些文件仅用于与其他附带有它们的操作系统文件一起处理。 这些文件之间的不匹配版本不受 Microsoft，并定期不起作用。

以下部分介绍的视频内存管理和计划模型的图形处理单元 (GPU):

[处理内存段](handling-memory-segments.md)

[处理命令和 DMA 缓冲区](handling-command-and-dma-buffers.md)

[GDI 硬件加速](gdi-hardware-acceleration.md)

[视频内存产品/服务和回收](video-memory-offer-and-reclaim.md)

[GPU 抢占](gpu-preemption.md)

 

 





