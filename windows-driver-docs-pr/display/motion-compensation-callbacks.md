---
title: 运动补偿回调
description: 运动补偿回调
ms.assetid: a1f748e4-0d62-4543-a409-bb9ec02a7d77
keywords:
- 绘制 WDK DirectDraw，运动补偿
- DirectDraw WDK Windows 2000 显示，运动补偿
- 运动补偿 WDK
- 压缩的视频解码 WDK DirectDraw
- 视频解码 WDK DirectDraw
- 解码 WDK DirectDraw
- 回调函数 WDK DirectDraw 运动补偿
- 数字视频解码 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea8fdc7311a6466368cbe6880bcbb6eecb091e29
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372872"
---
# <a name="motion-compensation-callbacks"></a>运动补偿回调


## <span id="ddk_motion_compensation_callbacks_gg"></span><span id="DDK_MOTION_COMPENSATION_CALLBACKS_GG"></span>


[DirectX 视频加速](directx-video-acceleration.md)利用了以下运动补偿回调函数提供 DirectDraw 中加速数字视频解码的驱动程序处理，alpha 值混合处理对这些产品支持目的为 DVD子画面的支持：

[*DdMoCompBeginFrame*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_beginframe)

[*DdMoCompCreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)

[*DdMoCompDestroy*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)

[*DdMoCompEndFrame*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_endframe)

[*DdMoCompGetBuffInfo*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getcompbuffinfo)

[*DdMoCompGetFormats*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getformats)

[*DdMoCompGetGuids*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)

[*DdMoCompGetInternalInfo*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getinternalinfo)

[*DdMoCompQueryStatus*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)

[*DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)

运动补偿回调函数组成的设备驱动程序端的 DirectX 视频加速接口。 运动补偿回调函数指定的成员[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构。 以下步骤演示如何访问运动补偿回调函数：

1.  从收到的 Guid **IAMVideoAccelerator::GetVideoAcceleratorGUIDs**来源于设备驱动程序[ *DdMoCompGetGuids*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)。

2.  对下游输入 pin **IAMVideoAccelerator::GetUncompFormatsSupported**中的设备驱动程序的数据返回[ *DdMoCompGetFormats*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getformats)。

3.  在相关处理，开头[ **DXVA\_ConnectMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_connectmode)数据结构的解码器的输出插针从**IAMVideoAcceleratorNotify::GetCreateVideoAcceleratorData**传递到设备驱动程序[ *DdMoCompCreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)，这会通知有关视频加速对象的解码器。

4.  从返回的数据**IAMVideoAccelerator::GetCompBufferInfo**源自设备驱动程序[ *DdMoCompGetBuffInfo*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getcompbuffinfo)。

5.  使用发送的缓冲区**IAMVideoAccelerator::Execute**的设备驱动程序收到[ *DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)。

6.  利用**IAMVideoAccelerator::QueryRenderStatus**调用的设备驱动程序[ *DdMoCompQueryStatus*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)。 返回代码为 DDERR\_从 WASSTILLDRAWING *DdMoCompQueryStatus*将视为返回代码为 E 主机解码器\_从 PENDING **IAMVideoAccelerator::QueryRenderStatus**.

7.  发送到数据**IAMVideoAccelerator::BeginFrame**的设备驱动程序收到[ *DdMoCompBeginFrame*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_beginframe)。 返回代码为 DDERR\_WASSTILLDRAWING 需要从*DdMoCompBeginFrame*为了使电子\_PENDING 响应中的主机解码器才能看到**IAMVideoAccelerator::BeginFrame**.

8.  发送到数据**IAMVideoAccelerator::EndFrame**的设备驱动程序收到[ *DdMoCompEndFrame*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_endframe)。

9.  在相关处理的设备驱动程序的最终[ *DdMoCompDestroy* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)用于通知驱动程序，将无法再使用当前的视频加速对象，因此，可以执行该驱动程序任何必要的清理。

 

 





