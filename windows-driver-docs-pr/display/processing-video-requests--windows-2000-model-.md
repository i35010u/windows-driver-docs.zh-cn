---
title: 处理视频请求（Windows 2000 模型）
description: 处理视频请求（Windows 2000 模型）
ms.assetid: 86b3037e-2d18-46b0-8b02-c66be65a4001
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，处理请求
- 请求处理 WDK 视频微型端口
- I/o WDK 视频微型端口
- HwVidStartIO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1e0b9ded291e5e2bba556d7f88c6565a7c8830c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829681"
---
# <a name="processing-video-requests-windows-2000-model"></a>处理视频请求（Windows 2000 模型）


## <span id="ddk_processing_video_requests_windows_2000_model__gg"></span><span id="DDK_PROCESSING_VIDEO_REQUESTS_WINDOWS_2000_MODEL__GG"></span>


发出显示驱动程序通过视频端口驱动程序对**EngDeviceIoControl**的调用的所有 i/o 请求。 然后，视频端口驱动程序将调用相应的微型端口驱动程序的[*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)函数，其中包含指向每个[**视频\_请求所设置\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)结构的指针。 发送到*HwVidStartIO*的所有 VRPs 都将**IoControlCode**成员设置为 IOCTL\_视频\_*XXX*。

视频端口驱动程序还通过发送每个微型端口驱动程序的*HwVidStartIO*例程一次只发送一个 VRP 来管理所有视频微型端口驱动程序的传入请求的同步。 *HwVidStartIO*拥有每个输入 VRP，直到微型端口驱动程序完成请求的操作并返回 control。 在微型端口驱动程序完成当前 VRP 之前，视频端口驱动程序会保留给 i/o 管理器发送的任何未完成的 IRP 代码，以响应相应显示驱动程序对[**EngDeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)的后续调用。

收到视频请求后， [*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)必须检查 VRP，处理适配器上的视频请求，在 VRP 中设置相应的状态和其他信息，并返回**TRUE**。

 

 





