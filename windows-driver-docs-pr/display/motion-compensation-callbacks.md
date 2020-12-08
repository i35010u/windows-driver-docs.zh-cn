---
title: 运动补偿回调
description: 运动补偿回调
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
ms.openlocfilehash: de359747d923ed556285ca054c93e127f0e6ee1d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838491"
---
# <a name="motion-compensation-callbacks"></a>运动补偿回调


## <span id="ddk_motion_compensation_callbacks_gg"></span><span id="DDK_MOTION_COMPENSATION_CALLBACKS_GG"></span>


[DirectX 视频加速](directx-video-acceleration.md) 利用了 DirectDraw 驱动程序中提供的以下运动补偿回调函数来加速数字视频解码处理，并支持使用 alpha 混合作为 DVD 子画面支持：

[*DdMoCompBeginFrame*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_beginframe)

[*DdMoCompCreate*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)

[*DdMoCompDestroy*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)

[*DdMoCompEndFrame*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_endframe)

[*DdMoCompGetBuffInfo*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_getcompbuffinfo)

[*DdMoCompGetFormats*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_getformats)

[*DdMoCompGetGuids*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)

[*DdMoCompGetInternalInfo*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_getinternalinfo)

[*DdMoCompQueryStatus*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)

[*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)

运动补偿回调函数包含 DirectX 视频加速接口的设备驱动程序端。 运动补偿回调函数由 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks) 结构的成员指定。 以下步骤演示如何访问运动补偿回调函数：

1.  从 **IAMVideoAccelerator：： GetVideoAcceleratorGUIDs** 接收的 guid 来源于设备驱动程序的 [*DdMoCompGetGuids*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_getguids)。

2.  对下游输入插针的 **IAMVideoAccelerator：： GetUncompFormatsSupported** 的调用将从设备驱动程序的 [*DdMoCompGetFormats*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_getformats)返回数据。

3.  在相关处理开始时，解码器的 **IAMVideoAcceleratorNotify：： GetCreateVideoAcceleratorData** 的输出插针中的 [**DXVA \_ ConnectMode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)数据结构会传递到设备驱动程序的 [*DdMoCompCreate*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_create)，这将通知解码器有关视频加速对象的信息。

4.  从 **IAMVideoAccelerator：： GetCompBufferInfo** 返回的数据源自设备驱动程序的 [*DdMoCompGetBuffInfo*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_getcompbuffinfo)。

5.  使用 **IAMVideoAccelerator：： Execute** 发送的缓冲区由设备驱动程序的 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)接收。

6.  使用 **IAMVideoAccelerator：： QueryRenderStatus** 会调用设备驱动程序的 [*DdMoCompQueryStatus*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)。 DDERR \_ WASSTILLDRAWING From *DdMoCompQueryStatus* 返回代码将被主机解码器视为 E \_ 挂自 **IAMVideoAccelerator：： QueryRenderStatus** 的返回代码。

7.  发送到 **IAMVideoAccelerator：： BeginFrame** 的数据由设备驱动程序的 [*DdMoCompBeginFrame*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_beginframe)接收。 需要在 DdMoCompBeginFrame 中使用 DDERR WASSTILLDRAWING 的返回代码，以 \_ 使 *DdMoCompBeginFrame* \_ 主机解码器在响应 **IAMVideoAccelerator：： BeginFrame** 时查看 E 挂起。

8.  发送到 **IAMVideoAccelerator：： EndFrame** 的数据由设备驱动程序的 [*DdMoCompEndFrame*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_endframe)接收。

9.  在相关处理结束时，使用设备驱动程序的 [*DdMoCompDestroy*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy) 通知驱动程序当前的视频加速对象将不再可用，以便驱动程序可以执行任何必要的清理。

 

