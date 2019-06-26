---
title: 为视频处理创建渲染目标图面
description: 为视频处理创建渲染目标图面
ms.assetid: f18b348d-837a-4e1b-b91a-40593661bd56
keywords:
- 视频处理 WDK DirectX VA，呈现目标图面
- 呈现目标图面 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f8c3226e5f6c621ebfeaad5c0b65624b2df8f69
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370233"
---
# <a name="creating-a-render-target-surface-for-video-processing"></a>为视频处理创建渲染目标图面


Microsoft Direct3D 运行时将调用用户模式显示驱动程序[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数来创建呈现目标的视频处理的图面。 用户模式显示驱动程序确定它应创建视频处理是否存在从呈现目标图面**VideoProcessRenderTarget**中的位域标志**标志**的成员[ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构*pResource*参数**CreateResource**指向。 用户模式显示驱动程序可以使用此呈现器目标的视频处理但不必对三维效果。 用户模式显示驱动程序可以执行常规 RGB 三维呈现器目标图面上的视频处理。 但是，用户模式显示驱动程序可以经常 YUV 格式的三维硬件不能支持的呈现器目标作为输出。

该驱动程序应支持的视频处理有效的呈现器目标作为仅图面类型如下：

-   使用创建的 RGB 或 YUV 表面**VideoProcessRenderTarget**位域标志。

-   使用创建的 RGB 表面**RenderTarget**位域标志。

-   使用创建的 RGB 纹理**RenderTarget**并**纹理**位域标志。

 

 





