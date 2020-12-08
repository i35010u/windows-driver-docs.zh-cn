---
title: 处理视频帧
description: 处理视频帧
keywords:
- 视频处理 WDK DirectX VA，视频帧处理
- 视频帧处理 WDK DirectX VA
- 帧 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0478ccdf55a638d3db031a05414cebfdc7275b46
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792945"
---
# <a name="processing-video-frames"></a>处理视频帧


Microsoft Direct3D runtime 调用用户模式显示驱动程序的 [**VideoProcessBeginFrame**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_videoprocessbeginframe) 和 [**VideoProcessEndFrame**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_videoprocessendframe) 函数，以指示这些函数调用之间的时间段，用户模式显示驱动程序可以处理视频帧。 在用户模式显示驱动程序可以处理任何视频帧之前，Microsoft Direct3D 运行时必须调用用户模式显示驱动程序的 [**SetVideoProcessRenderTarget**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setvideoprocessrendertarget) 函数，以设置视频处理的呈现目标图面。 但是，对 *SetVideoProcessRenderTarget* 的调用只能出现在开始框架和结束帧时间段之外。

设置用于视频处理的渲染目标图面后，用户模式显示驱动程序可以接收对其 [**VideoProcessBlt**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_videoprocessblt) 函数的调用，以处理开始帧和结束帧时间段之间的视频帧。

 

