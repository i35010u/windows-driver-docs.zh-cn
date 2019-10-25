---
title: 运动补偿回调
description: 运动补偿回调
ms.assetid: a1f748e4-0d62-4543-a409-bb9ec02a7d77
keywords:
- 绘制 WDK DirectDraw，运动补偿
- DirectDraw WDK Windows 2000 显示，动作补偿
- 运动补偿 WDK
- 压缩的视频解码 WDK DirectDraw
- 视频解码 WDK DirectDraw
- 解码 WDK DirectDraw
- 回调函数 WDK DirectDraw 运动补偿
- 数字视频解码 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5aaa2a3313c503e02cc89f4f393b26eb42f6b1dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840557"
---
# <a name="motion-compensation-callbacks"></a>运动补偿回调


## <span id="ddk_motion_compensation_callbacks_gg"></span><span id="DDK_MOTION_COMPENSATION_CALLBACKS_GG"></span>


[DirectX 视频加速](directx-video-acceleration.md)利用了 DirectDraw 驱动程序中提供的以下运动补偿回调函数来加速数字视频解码处理，并支持使用 alpha 混合作为 DVD 子画面支持

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

运动补偿回调函数包含 DirectX 视频加速接口的设备驱动程序端。 运动补偿回调函数由[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的成员指定。 以下步骤演示如何访问运动补偿回调函数：

1.  从**IAMVideoAccelerator：： GetVideoAcceleratorGUIDs**接收的 guid 来源于设备驱动程序的[*DdMoCompGetGuids*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)。

2.  对下游输入插针的**IAMVideoAccelerator：： GetUncompFormatsSupported**的调用将从设备驱动程序的[*DdMoCompGetFormats*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getformats)返回数据。

3.  相关处理开始时，解码器的**IAMVideoAcceleratorNotify：： GetCreateVideoAcceleratorData**的输出插针中的[**DXVA\_ConnectMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)数据结构被传递到设备驱动程序的[*DdMoCompCreate*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)，它通知解码器有关视频加速对象的信息。

4.  从**IAMVideoAccelerator：： GetCompBufferInfo**返回的数据源自设备驱动程序的[*DdMoCompGetBuffInfo*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_getcompbuffinfo)。

5.  使用**IAMVideoAccelerator：： Execute**发送的缓冲区由设备驱动程序的[*DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)接收。

6.  使用**IAMVideoAccelerator：： QueryRenderStatus**会调用设备驱动程序的[*DdMoCompQueryStatus*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)。 DDERR\_WASSTILLDRAWING 的返回*代码将被*主机解码器视为来自**IAMVideoAccelerator：： QueryRenderStatus**的 E\_的返回代码。

7.  发送到**IAMVideoAccelerator：： BeginFrame**的数据由设备驱动程序的[*DdMoCompBeginFrame*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_beginframe)接收。 需要从*DdMoCompBeginFrame*中获取 DDERR\_WASSTILLDRAWING 的返回代码，以使主机解码器在响应**IAMVideoAccelerator：： BeginFrame**时，为使 E\_处于挂起状态。

8.  发送到**IAMVideoAccelerator：： EndFrame**的数据由设备驱动程序的[*DdMoCompEndFrame*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_endframe)接收。

9.  在相关处理结束时，使用设备驱动程序的[*DdMoCompDestroy*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)通知驱动程序当前的视频加速对象将不再可用，以便驱动程序可以执行任何必要的清理。

 

 





