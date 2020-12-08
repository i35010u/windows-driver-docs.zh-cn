---
title: 使用内核模式视频传输
description: 使用内核模式视频传输
keywords:
- 绘制内核模式视频传输 WDK DirectDraw，关于内核模式视频传输
- DirectDraw 内核模式视频传输 WDK Windows 2000 显示，关于内核模式视频传输
- 内核模式视频传输 WDK DirectDraw，关于内核模式视频传输
- 视频传输内核模式 WDK DirectDraw，关于内核模式视频传输
- 视频捕获 WDK 视频传输内核模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2c9ef5b823c2dc65093de8bd7103f74f10d0e1a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825695"
---
# <a name="using-kernel-mode-video-transport"></a>使用内核模式视频传输


## <span id="ddk_using_kernel_mode_video_transport_gg"></span><span id="DDK_USING_KERNEL_MODE_VIDEO_TRANSPORT_GG"></span>


与 *dxapi* 链接的 [视频捕获驱动程序](../stream/video-capture-devices.md)可访问内核模式视频传输功能，该驱动程序允许稍后调用 *dxapi.sys*。 仅当加载 DirectDraw 时，此功能才可用。

硬件解码器 (视频捕获驱动程序) 使用内核模式 DirectDraw 提供的 [**DxApi**](/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi) 函数来访问 DxApi 接口回调函数。 **DxApi** 函数是接受函数标识符、输入缓冲区和大小以及输出缓冲区和大小的单个入口点。 此函数的行为以及输入和输出缓冲区的大小和格式取决于指定的函数标识符。 **DxApi** 函数及其函数标识符在 *ddkmapi* 中定义。

DirectShow 或其他客户端通过 DirectDraw 访问由视频微型端口驱动程序提供的 DxApi 接口回调函数。 DxApi 接口回调函数在 *dxmini* 中定义。

若要使用内核模式视频传输接口，视频捕获驱动程序必须首先接收到需要使用的每个 DirectDraw 对象、surface 和 VPE 对象的用户模式句柄。 对于 "捕获" 和 "MPEG" 模型，使用现有的 Api 传递这些句柄。 如果驱动程序需要此功能，但它不是流类驱动程序，则用户模式组件可以使用 [IDirectDrawKernel](/windows-hardware/drivers/ddi/index) 和 [IDirectDrawSurfaceKernel](/windows-hardware/drivers/ddi/index) COM 接口检索句柄，并将它们向下传递给驱动程序。 COM 接口及其方法在 *ddkernel* 中标识。

 

