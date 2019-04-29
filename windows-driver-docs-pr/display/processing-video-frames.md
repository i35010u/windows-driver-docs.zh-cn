---
title: 处理视频帧
description: 处理视频帧
ms.assetid: 0f613186-1887-4d67-95d6-f562124c69ab
keywords:
- 视频处理 WDK DirectX VA 视频帧处理
- 处理 WDK DirectX VA 的视频帧
- 帧 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8f91269cc59dfb7f01eb9cb7203ce6e5e91bb71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370175"
---
# <a name="processing-video-frames"></a>处理视频帧


Microsoft Direct3D 运行时将调用用户模式显示驱动程序[ **VideoProcessBeginFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff570494)并[ **VideoProcessEndFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff570497)若要指示这些用户模式显示驱动程序可以处理的视频帧的函数调用之间的时间段的功能。 Microsoft Direct3D 运行时用户模式显示驱动程序可以处理任何视频帧之前，必须调用用户模式显示驱动程序[ **SetVideoProcessRenderTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff569695)函数来设置呈现器视频处理的目标面。 但是，在调用*SetVideoProcessRenderTarget*可仅外部出现的开始范围和结束帧时间段。

在呈现目标图面后视频处理已设置，用户模式显示驱动程序可以接收到调用其[ **VideoProcessBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff570495)函数来处理视频帧之间开始帧和最终帧时间段。

 

 





