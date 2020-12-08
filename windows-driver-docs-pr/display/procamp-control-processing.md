---
title: ProcAmp 控制处理
description: ProcAmp 控制处理
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，ProcAmp
- 视频加速 WDK DirectX，ProcAmp
- VA WDK DirectX，ProcAmp
- ProcAmp WDK DirectX VA
- ProcAmp WDK DirectX VA，关于 ProcAmp 控制处理
- VMR WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b3f94df6cef01cdf320b0e17cc99ce8699e0b02
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792957"
---
# <a name="procamp-control-processing"></a>ProcAmp 控制处理


## <span id="ddk_procamp_control_processing_gg"></span><span id="DDK_PROCAMP_CONTROL_PROCESSING_GG"></span>


ProcAmp 控件 DDI 扩展了 DirectX VA，以支持 ProcAmp 控制，并按图形设备驱动程序对视频内容进行处理。 ProcAmp 控件 DDI 是 (*VMR*) 和图形设备驱动程序的视频混合呈现器之间的接口。 DDI 映射到现有 DirectDraw 和 DirectX VA DDI。 不能通过 **IAMVideoAccelerator** 接口访问 DDI。 ProcAmp 控件 DDI 在 Microsoft DirectX 版本9.0 中提供。

如果驱动程序支持对压缩视频进行加速解码，则 VMR 将调用该驱动程序来创建两个 DirectX VA 设备，一个用于执行实际的视频解码工作，另一个用于严格用于 ProcAmp 调整。

本部分涵盖了以下主题：

[在 8 位 YUV 色彩空间中进行处理](processing-in-the-8-bit-yuv-color-space.md)

[VMR 视频处理](vmr-video-processing.md)

[将 ProcAmp 控制 DDI 映射到 DirectDraw 和 DirectX VA](mapping-the-procamp-control-ddi-to-directdraw-and-directx-va.md)

[ProcAmp 属性](procamp-properties.md)

[ProcAmp 控制的示例函数](sample-functions-for-procamp-control.md)

 

 





