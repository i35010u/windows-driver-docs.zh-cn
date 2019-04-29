---
title: 视频端口扩展背景信息
description: 视频端口扩展背景信息
ms.assetid: 77bed8d3-4fe5-4159-88e9-d6565aea9117
keywords:
- 有关视频端口扩展的 DirectX VPE 支持 WDK DirectDraw
- 有关视频端口扩展绘制 VPEs WDK DirectDraw
- DirectDraw VPEs WDK Windows 2000 显示，相关的视频端口扩展信息
- 有关视频端口扩展的视频端口扩展 WDK DirectDraw
- 有关视频端口扩展 VPEs WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 893d01ca1a6490c270c8825d43d4b67290f0fc9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365047"
---
# <a name="video-port-extensions-background"></a>视频端口扩展背景信息


## <span id="ddk_video_port_extensions_background_gg"></span><span id="DDK_VIDEO_PORT_EXTENSIONS_BACKGROUND_GG"></span>


视频端口扩展 (VPE) 技术是一个图形帧缓冲区中支持从视频解码器和 autoflipping 硬件直接连接的 DirectDraw 扩展插件。

当视频数据放置在帧缓冲区中时，可以使用视频覆盖层以显示它。 视频覆盖图形系统中的告知数字模拟转换器 (DAC) 不会通常显示的区域中显示的数据。 覆盖层的使用是高效，因为平面闪不需要使数据显示，并且可以在更高版本的颜色深度比可见帧缓冲区中查看视频数据。

硬件视频端口是一种视频流交付选项，可用来代替 PCI 或 AGP 总线。 对于需要与其他应用程序所需的 PCI 带宽并发运行的应用程序，最好使用硬件视频端口来确保解码器和 VGA 图形控制器之间的延迟时间短视频传输。 此路由不是灵活性不如 PCI 总线解决方案，因为它绑定到特定的图形芯片组，解码器，而它的结果如有必要，绕过 PCI 总线的机会。

内核模式的视频传输功能中, 所述[内核模式视频传输](kernel-mode-video-transport.md)部分中，还提供了对 vpe 数据以确保支持增强的视频播放质量和增强视频捕获支持。 为了支持 VPE 在 Windows 2000 及更高版本，驱动程序必须支持内核模式视频传输。

VPE 仅支持基于硬件的数据连接。 内核模式视频传输的数据传输支持直接访问。

VPE 不 WDM 技术。 在 Windows 2000 及更高版本，有关其他外围设备，而不是显示驱动程序使用 WDM。

因为 VPE 支持是最新版本的 DirectX 的一部分，应用程序可以充分利用这些功能具有保障，该解决方案适用于任何支持 VPE 在 Windows 2000 及更高版本的图形卡。

 

 





