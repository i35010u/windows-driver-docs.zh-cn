---
title: 视频端口扩展背景信息
description: 视频端口扩展背景信息
keywords:
- DirectX VPE 支持 WDK DirectDraw，关于视频端口扩展
- 绘制 VPEs WDK DirectDraw，关于视频端口扩展
- DirectDraw VPEs WDK Windows 2000 显示，关于视频端口扩展
- 视频端口扩展 WDK DirectDraw，关于视频端口扩展
- VPEs WDK DirectDraw，关于视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 813cda2244ff96349c932d7a8b885a9131aeb48e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806367"
---
# <a name="video-port-extensions-background"></a>视频端口扩展背景信息


## <span id="ddk_video_port_extensions_background_gg"></span><span id="DDK_VIDEO_PORT_EXTENSIONS_BACKGROUND_GG"></span>


 (VPE) 技术的视频端口扩展是 DirectDraw 扩展，它支持从视频解码器直接进行硬件连接，并在图形框架缓冲区中进行 autoflipping。

当视频数据置于帧缓冲区中时，可以使用视频覆盖来显示它。 图形系统中的视频覆盖会告诉数字到模拟转换器 (DAC) 在通常不会显示的区域中显示数据。 使用叠加的效率非常高，因为无需使用 blitting 来使数据可见，并且可以在比可见框架缓冲区更高的颜色深度查看视频数据。

硬件视频端口是一个视频流传送选项，可以使用它来代替 PCI 或 AGP 总线。 对于应与需要 PCI 带宽的其他应用程序同时运行的应用程序，使用硬件视频端口可确保解码器和 VGA 图形控制器之间的低延迟视频传输更有利。 此路由与 PCI 总线解决方案并无灵活性，因为它将解码器与特定的图形芯片集联系在一起，但如果需要，它还可以绕过 PCI 总线。

内核 [模式视频传输](kernel-mode-video-transport.md) 部分中描述的内核模式视频传输功能还支持 VPE，以确保改进视频播放质量和增强视频捕获支持。 为了支持 Windows 2000 和更高版本下的 VPE，驱动程序必须支持内核模式视频传输。

VPE 仅支持基于硬件的数据连接。 内核模式视频传输支持直接访问数据传输。

VPE 不是 WDM 技术。 在 Windows 2000 和更高版本中，WDM 用于其他外围设备，但不适用于显示驱动程序。

由于 VPE 支持是最新版本的 DirectX 的一部分，因此应用程序可以利用这些功能，确保解决方案适用于在 Windows 2000 和更高版本下支持 VPE 的任何图形卡。

 

 





