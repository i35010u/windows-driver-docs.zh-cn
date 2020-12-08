---
title: 内核模式视频传输
description: 内核模式视频传输
keywords:
- 绘制内核模式视频传输 WDK DirectDraw，关于内核模式视频传输
- DirectDraw 内核模式视频传输 WDK Windows 2000 显示，关于内核模式视频传输
- 内核模式视频传输 WDK DirectDraw，关于内核模式视频传输
- 视频传输内核模式 WDK DirectDraw，关于内核模式视频传输
- 绘制内核模式视频传输 WDK DirectDraw
- DirectDraw 内核模式视频传输 WDK Windows 2000 显示
- 内核模式视频传输 WDK DirectDraw
- 视频传输内核模式 WDK DirectDraw
- 编织 WDK DirectDraw
- 视频捕获 WDK 视频传输内核模式
- miniVDD WDK DirectDraw
- 总线控制 WDK DirectDraw
- V-同步 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 093c2cfa60b6359d4f19d24f37966951f32a7234
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832727"
---
# <a name="kernel-mode-video-transport"></a>内核模式视频传输


## <span id="ddk_kernel_mode_video_transport_gg"></span><span id="DDK_KERNEL_MODE_VIDEO_TRANSPORT_GG"></span>


本主题介绍了 Microsoft Windows 2000 及更高版本的操作系统上存在的内核模式视频传输。

内核模式视频传输是指环形 0 (内核模式) 的新的 Microsoft DirectDraw 组件，可增强视频功能。 此组件访问 DxApi 接口。 此接口将添加到 Windows 2000 和更高版本的操作系统下的 [视频微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md) 中。

### <a name="span-idwindows_2000_and_laterspanspan-idwindows_2000_and_laterspanwindows-2000-and-later"></a><span id="windows_2000_and_later"></span><span id="WINDOWS_2000_AND_LATER"></span>Windows 2000 及更高版本

内核模式视频传输指的是客户端（如 Microsoft DirectShow）可以使用的 Microsoft DirectDraw 组件来增强视频功能。 此功能的主要作用是调用微型端口驱动程序，告诉它在发生 V 同步时执行硬件视频端口和覆盖翻转。 此功能最多可支持10个缓冲区，而不会遇到硬件限制，只要硬件视频端口支持 (IRQ 的 V 同步中断请求) 。 当客户端指定 autoflipping 并且硬件无法 autoflip 时，由 Microsoft DirectX 5.0 和更高版本提供的 DirectDraw 版本自动使用此功能。

内核模式视频传输还确保增强了捕获支持。 在 Microsoft Windows 98/Me 和 Microsoft Windows 2000 及更高版本下，基于 WDM 的视频捕获驱动程序在内核模式下运行，并直接访问帧缓冲区。 捕获驱动程序可以 "手动" 翻转覆盖面。 Windows 2000 和更高版本的微型端口视频传输驱动程序可以提供来自硬件视频端口或显示器的 V 同步通知;它还可以获取字段极性，这在捕获垂直消隐间隔 (VBI) 数据时很有用。

尽管内核模式驱动程序的主要用途是增强硬件视频端口 autoflipping 的功能，但它还支持视频总线母版，可以在内核模式下写入数据。 由于模式发生更改，或在启动全屏命令提示符实例的情况下，总线主机可以在丢失表面之前通知。 由于新的驱动程序支持允许在发生更改之前调用总线主机，因此总线主机可以关闭而不会导致问题。

 

 





