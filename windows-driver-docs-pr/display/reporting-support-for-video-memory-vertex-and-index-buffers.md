---
title: 报告对视频内存顶点和索引缓冲区的支持
description: 报告对视频内存顶点和索引缓冲区的支持
ms.assetid: fa0d7dd5-3bed-45db-a946-0761fd631a52
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，请报告功能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b44870279b6357f38d6175e0006d768d17f0f4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545518"
---
# <a name="reporting-support-for-video-memory-vertex-and-index-buffers"></a>报告对视频内存顶点和索引缓冲区的支持


## <span id="ddk_reporting_support_for_video_memory_vertex_and_index_buffers_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_VIDEO_MEMORY_VERTEX_AND_INDEX_BUFFERS_GG"></span>


DirectX 8.0 已添加的两个新 Direct3D 功能标志标记到运行时，是否驱动程序不会或不支持的视频内存顶点和索引缓冲区。 这些标志创建之前，运行时无法确定是否该驱动程序提供了实际针对支持的视频内存顶点缓冲区或不。 因此，如果 DirectX 8.0 将导出 execute 缓冲区 （d3d 缓冲区） 创建和销毁驱动程序入口点，它应添加一个或这两个功能位 D3DDEVCAPS\_HWVERTEXBUFFER 和 D3DDEVCAPS\_HWINDEXBUFFER到**DevCaps** D3DCAPS8 结构字段通过报告**GetDriverInfo2**到运行时。 设置标志 D3DDEVCAPS\_HWVERTEXBUFFER 如果您的驱动程序支持视频的视频或非本地内存顶点缓冲区和 D3DDEVCAPS\_HWINDEXBUFFER 如果您的驱动程序支持视频的视频或非本地内存索引缓冲区。

在运行时屏蔽关闭之前这些功能位报告给应用程序 （它们不用于仅向运行时本身的应用程序） 的功能。 因此，即使您的驱动程序将它们导出这些功能不到 DirectX Caps 查看器应用程序可见。

正确支持这些功能是 Microsoft Windows 硬件质量实验室 (WHQL) 测试的一部分。

 

 





