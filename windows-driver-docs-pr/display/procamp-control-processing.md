---
title: ProcAmp 控制处理
description: ProcAmp 控制处理
ms.assetid: feb66d91-1b25-415b-83f4-a75361b9dc11
keywords:
- DirectX 视频加速 WDK Windows 2000 显示 ProcAmp
- 视频加速 WDK DirectX ProcAmp
- VA WDK DirectX ProcAmp
- ProcAmp WDK DirectX VA
- 有关 ProcAmp 控制处理的 procAmp WDK DirectX VA，
- VMR WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9826277c1a8d27f92088485b743437a43fedfae4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554643"
---
# <a name="procamp-control-processing"></a>ProcAmp 控制处理


## <span id="ddk_procamp_control_processing_gg"></span><span id="DDK_PROCAMP_CONTROL_PROCESSING_GG"></span>


ProcAmp 控件 DDI 扩展了 DirectX VA，以支持 ProcAmp 控件和图形设备驱动程序的后续处理的视频内容。 ProcAmp 控件 DDI 是视频混合呈现器之间的接口 (*VMR*) 及图形设备驱动程序。 DDI 映射到现有的 DirectDraw 和 DirectX VA DDI。 DDI 不是可通过访问**IAMVideoAccelerator**接口。 ProcAmp 控件 DDI 现已推出 Microsoft DirectX 版本 9.0。

如果驱动程序支持的压缩的视频加速解码，VMR 将调用要创建两个 DirectX VA 设备，一个用来执行实际的视频解码工作，而另一个要用于严格 ProcAmp 调整的驱动程序。

本部分介绍以下主题：

[8 位 YUV 颜色空间中的处理](processing-in-the-8-bit-yuv-color-space.md)

[VMR 视频处理](vmr-video-processing.md)

[映射到 DirectDraw 和 DirectX VA ProcAmp 控件 DDI](mapping-the-procamp-control-ddi-to-directdraw-and-directx-va.md)

[ProcAmp 属性](procamp-properties.md)

[ProcAmp 控制的示例函数](sample-functions-for-procamp-control.md)

 

 





