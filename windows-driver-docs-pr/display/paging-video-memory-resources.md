---
title: 分页视频内存资源
description: 分页视频内存资源
ms.assetid: e9734db6-3ad0-4c64-a9c6-15ba956b2dce
keywords:
- DMA 缓冲区 WDK 显示分页视频内存资源
- 分页显示 WDK 的视频内存资源
- 分页 WDK 显示的视频内存资源
- 分页缓冲区 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd1508f5c6999e609b8ce09f8d1f770228fe422b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547915"
---
# <a name="paging-video-memory-resources"></a>分页视频内存资源


## <span id="ddk_paging_video_memory_resources_gg"></span><span id="DDK_PAGING_VIDEO_MEMORY_RESOURCES_GG"></span>


与 Microsoft 不同[Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)，Windows Vista 显示器驱动程序模型允许更多视频内存资源来创建比可用，物理视频内存的总量这然后入和签出分页根据需要的视频内存。 换而言之，并非所有视频内存资源是在视频内存中同时。

GPU 可以在其管道中有多个 DMA 缓冲区。 这些活动的 DMA 缓冲区引用的视频内存资源必须在视频内存中。 其他空闲的视频内存资源可以出分页到系统内存。

在 GPU 之前，计划程序可以调用显示微型端口驱动程序[ **DxgkDdiSubmitCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff560790)函数提交 DMA 缓冲区到 GPU 计划程序必须确保使用的所有视频内存资源DMA 缓冲区实际上是在视频内存中。 如果某些资源不是在视频内存，它们必须从系统内存分页中。 GPU 计划程序必须在要在视频内存将从系统内存的必需的视频内存资源数据传输到视频内存中留出空间的视频内存管理器时调用。 如果视频内存需求较高，GPU 计划程序必须调用时的视频内存管理器将空闲的视频内存资源数据传输到系统内存，无法为所需的视频内存资源数据留出空间。 包含用于将数据传输视频和系统的内存之间的命令的特殊用途 DMA 缓冲区被称为分页缓冲区。 视频内存管理器会调用显示微型端口驱动程序[ **DxgkDdiBuildPagingBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff559587)函数来创建驱动程序将特定于硬件的数据传输命令写入到的分页缓冲区。

 

 





