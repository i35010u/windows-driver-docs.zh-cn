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
ms.openlocfilehash: 443cc4742a38c09be637d33508337d6dadfe1960
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361249"
---
# <a name="processing-video-requests-windows-2000-model"></a>处理视频请求（Windows 2000 模型）


## <span id="ddk_processing_video_requests_windows_2000_model__gg"></span><span id="DDK_PROCESSING_VIDEO_REQUESTS_WINDOWS_2000_MODEL__GG"></span>


发出显示驱动程序对 [**EngDeviceIoControl**](/windows/win32/api/winddi/nf-winddi-engdeviceiocontrol) 的调用的所有 i/o 请求都从 irp 代码映射 (参阅 [Irp 主要函数代码](../kernel/irp-major-function-codes.md)) 通过视频端口驱动程序 *VRPs* 。 然后，视频端口驱动程序将调用相应的微型端口驱动程序的 [*HwVidStartIO*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io) 函数，其中包含指向它所设置的每个 [**视频 \_ 请求 \_ 数据包**](/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet) 结构的指针。 发送到 *HwVidStartIO* 的所有 VRPs 都将 **IoControlCode** 成员设置为 IOCTL \_ 视频 \_ *XXX* 。

视频端口驱动程序还通过发送每个微型端口驱动程序的 *HwVidStartIO* 例程一次只发送一个 VRP 来管理所有视频微型端口驱动程序的传入请求的同步。 *HwVidStartIO* 拥有每个输入 VRP，直到微型端口驱动程序完成请求的操作并返回 control。 在微型端口驱动程序完成当前 VRP 之前，视频端口驱动程序会保留给 i/o 管理器发送的任何未完成的 IRP 代码，以响应相应显示驱动程序对 [**EngDeviceIoControl**](/windows/win32/api/winddi/nf-winddi-engdeviceiocontrol) 的后续调用。

收到视频请求后， [*HwVidStartIO*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io) 必须检查 VRP，处理适配器上的视频请求，在 VRP 中设置相应的状态和其他信息，并返回 **TRUE** 。

