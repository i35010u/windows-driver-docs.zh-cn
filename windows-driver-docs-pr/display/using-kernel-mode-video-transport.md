---
title: 使用内核模式视频传输
description: 使用内核模式视频传输
ms.assetid: 0be84371-f7d5-42bb-b164-80fcf1b58d95
keywords:
- 绘制内核模式视频传输 WDK DirectDraw 接口有关内核模式视频传输
- 有关内核模式视频传输 DirectDraw 内核模式视频传输 WDK Windows 2000 显示
- 有关内核模式视频传输的内核模式视频传输 WDK DirectDraw
- 视频传输内核模式 WDK DirectDraw，有关内核模式视频传输
- 视频捕获 WDK 视频传输内核模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4489f46b0d9ae1db85dfe0abb542f5dfb5870f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388992"
---
# <a name="using-kernel-mode-video-transport"></a>使用内核模式视频传输


## <span id="ddk_using_kernel_mode_video_transport_gg"></span><span id="DDK_USING_KERNEL_MODE_VIDEO_TRANSPORT_GG"></span>


内核模式视频传输功能可通过[视频捕获驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff568699)与链接*dxapi.lib*，这可以让它以便稍后调用*dxapi.sys*。 仅当加载 DirectDraw，此功能才可用。

视频捕获 （适用于硬件解码器） 的驱动程序使用[ **DxApi** ](https://msdn.microsoft.com/library/windows/hardware/ff557364)提供内核模式 DirectDraw 访问 DxApi 接口回调函数的函数。 **DxApi**函数是接受函数标识符、 输入的缓冲区和大小，并输出缓冲区和大小的单个入口点。 此函数的大小和格式的输入和输出缓冲区的行为取决于指定的函数标识符。 **DxApi**中定义函数和其函数标识符*ddkmapi.h*。

DirectShow 或其他客户端访问提供的微型端口驱动程序通过 DirectDraw DxApi 接口回调函数。 DxApi 接口回调函数中定义*dxmini.h*。

若要使用的内核模式视频传输接口，视频捕获驱动程序必须首先收到用户模式下的每个 DirectDraw 对象、 图面上和它需要使用 VPE 对象的句柄。 有关捕获和 MPEG 模型中，这些句柄传递使用其现有的 Api。 如果驱动程序需要使用此功能，但不是流类驱动程序，用户模式组件可以检索使用的句柄[IDirectDrawKernel](https://msdn.microsoft.com/library/windows/hardware/ff567398)并[IDirectDrawSurfaceKernel](https://msdn.microsoft.com/library/windows/hardware/ff567409) COM 接口并将其传递到驱动程序。 中标识的 COM 接口和类的方法*ddkernel.h*。

 

 





