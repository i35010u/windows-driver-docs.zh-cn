---
title: 处理视频帧
description: 处理视频帧
ms.assetid: 0f613186-1887-4d67-95d6-f562124c69ab
keywords:
- 视频处理 WDK DirectX VA，视频帧处理
- 视频帧处理 WDK DirectX VA
- 帧 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05a3bda696d739ec4e164110c9a10f8a93ea31e4
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066412"
---
# <a name="processing-video-frames"></a>处理视频帧


Microsoft Direct3D runtime 调用用户模式显示驱动程序的 [**VideoProcessBeginFrame**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_videoprocessbeginframe) 和 [**VideoProcessEndFrame**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_videoprocessendframe) 函数，以指示这些函数调用之间的时间段，用户模式显示驱动程序可以处理视频帧。 在用户模式显示驱动程序可以处理任何视频帧之前，Microsoft Direct3D 运行时必须调用用户模式显示驱动程序的 [**SetVideoProcessRenderTarget**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setvideoprocessrendertarget) 函数，以设置视频处理的呈现目标图面。 但是，对 *SetVideoProcessRenderTarget* 的调用只能出现在开始框架和结束帧时间段之外。

设置用于视频处理的渲染目标图面后，用户模式显示驱动程序可以接收对其 [**VideoProcessBlt**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_videoprocessblt) 函数的调用，以处理开始帧和结束帧时间段之间的视频帧。

 

