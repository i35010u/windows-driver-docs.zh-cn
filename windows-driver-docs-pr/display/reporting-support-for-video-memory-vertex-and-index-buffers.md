---
title: 报告对视频内存顶点和索引缓冲区的支持
description: 报告对视频内存顶点和索引缓冲区的支持
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，报告功能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd3f031fc6b92a5eaeae3118a4fb58ba64dfc3cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838797"
---
# <a name="reporting-support-for-video-memory-vertex-and-index-buffers"></a>报告对视频内存顶点和索引缓冲区的支持


## <span id="ddk_reporting_support_for_video_memory_vertex_and_index_buffers_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_VIDEO_MEMORY_VERTEX_AND_INDEX_BUFFERS_GG"></span>


DirectX 8.0 添加了两个新的 Direct3D 功能标志，它们会标记到运行时，无论驱动程序是否支持视频内存顶点和索引缓冲区。 创建这些标志之前，运行时无法确定驱动程序是否提供实际的视频内存顶点缓冲区支持。 因此，如果 DirectX 8.0 (d3d 缓冲区) 创建和析构驱动程序入口点导出执行缓冲区，则它应将一个或两个功能位 D3DDEVCAPS \_ HWVERTEXBUFFER 和 D3DDEVCAPS \_ HWINDEXBUFFER 添加到通过 **DevCaps** 报告到运行时的 D3DCAPS8 结构的 **GetDriverInfo2** 字段。 如果驱动程序支持视频或非 \_ 本地视频内存顶点缓冲区和 D3DDEVCAPS \_ HWINDEXBUFFER （如果驱动程序支持视频或非本地视频内存索引缓冲区），请设置标志 D3DDEVCAPS HWVERTEXBUFFER。

运行时在向应用程序报告功能之前对这些功能位进行屏蔽 (它们对应用程序的应用程序仅对运行时自身) 不起作用。 因此，即使您的驱动程序导出这些功能，这些功能也不会对 DirectX Cap 查看器应用程序可见。

更正对这些功能的支持是 Microsoft Windows 硬件质量实验室 (WHQL) 测试的一部分。

 

 





