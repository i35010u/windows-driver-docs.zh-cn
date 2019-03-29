---
title: DirectX 的视频端口扩展
description: DirectX 的视频端口扩展
ms.assetid: 42309279-e98a-4091-8f01-5d0d418e9ef2
keywords:
- DirectX VPE 支持 WDK DirectDraw
- 绘制 VPEs WDK DirectDraw
- DirectDraw VPEs WDK Windows 2000 显示
- 视频端口扩展 WDK DirectDraw
- VPEs WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd29117ae39430b4feb1ff95f982883fc772a14d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576681"
---
# <a name="video-port-extensions-to-directx"></a>DirectX 的视频端口扩展


## <span id="ddk_video_port_extensions_to_directx_gg"></span><span id="DDK_VIDEO_PORT_EXTENSIONS_TO_DIRECTX_GG"></span>


使用硬件的视频端口对设备驱动程序开发人员应实现 Microsoft DirectX 的视频端口扩展 (VPE)。 VGA 图形控制器上的硬件视频端口提供帧缓冲区中获取数据的快速机制。 硬件视频端口是视频设备，通常之间硬件移动图片专家组 (MPEG) 设备或国家/地区电视标准委员会 (NTSC) 解码器和视频卡之间的专用的连接。 此专用的连接带有水平同步 (H sync) 和视频数据的垂直同步 (V sync) 信息。 硬件的视频端口和覆盖层可以使用此同步信息自动翻转之间写入一个表面，而在覆盖区上显示的另一个的多个缓冲区。 这样无需承担应用程序无拆解的视频。

VPE 允许客户端-通常 Microsoft DirectShow-协商 MPEG 或 NTSC 解码器与硬件之间的连接的视频端口。 VPE 还允许客户端到控件中的视频流，包括剪切和缩放效果。 VPE 实现应执行操作只请求的内容的客户端;例如，它应裁剪时，才裁剪的客户端请求。

Microsoft DirectDraw VPE 对象监视传入的信号，将图像数据传递给帧缓冲区，使用参数集，但若要修改映像，其接口方法执行翻转，或者执行其他服务。 VPE 对象不控制视频解码器或视频源。

VPEs 不与 Microsoft Windows 2000 和更高版本的视频端口系统模块相关联*videoprt.sys*。

 

 





