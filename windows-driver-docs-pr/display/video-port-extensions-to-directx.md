---
title: DirectX 的视频端口扩展
description: DirectX 的视频端口扩展
keywords:
- DirectX VPE 支持 WDK DirectDraw
- 绘制 VPEs WDK DirectDraw
- DirectDraw VPEs WDK Windows 2000 显示
- 视频端口扩展 WDK DirectDraw
- VPEs WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 455f461dfe250ce1b830334ae827d7fda81993c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806365"
---
# <a name="video-port-extensions-to-directx"></a>DirectX 的视频端口扩展


## <span id="ddk_video_port_extensions_to_directx_gg"></span><span id="DDK_VIDEO_PORT_EXTENSIONS_TO_DIRECTX_GG"></span>


具有硬件视频端口的设备的驱动程序开发人员应实现 (VPE) 到 Microsoft DirectX 的视频端口扩展。 VGA 图形控制器上的硬件视频端口可提供一种快速的机制，用于将数据获取到帧缓冲区。 硬件视频端口是视频设备之间的专用连接，通常是硬件移动图片专家组 (MPEG) 设备或国家电视标准委员会 (NTSC) 解码器和视频卡之间。 这种专用连接 (H 同步) 和垂直同步 (V 同步) 信息与视频数据一起传输。 硬件视频端口和覆盖层可以使用此同步信息在多个缓冲区之间自动切换，并写入到一个表面，重叠显示另一个表面。 这允许无需任何应用程序，即可自由显示视频。

VPE 允许客户端（通常为 Microsoft DirectShow）来协商 MPEG 或 NTSC 解码器与硬件视频端口之间的连接。 VPE 还允许客户端控制视频流中的效果，包括裁剪和缩放。 VPE 实现仅应执行客户端请求的操作;例如，它应仅在客户端请求裁剪时进行裁剪。

Microsoft DirectDraw VPE 对象监视传入信号，并使用通过其接口方法设置的参数将图像数据传递到帧缓冲区，以修改图像、执行翻转或执行其他服务。 VPE 对象不会控制视频解码器或视频源。

VPEs 与 Microsoft Windows 2000 和更高版本的视频端口系统模块无关， *videoprt.sys*。

 

 





