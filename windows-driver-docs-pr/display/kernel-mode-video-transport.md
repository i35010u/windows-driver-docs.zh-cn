---
title: 内核模式视频传输
description: 内核模式视频传输
ms.assetid: 3acaabc7-8d9f-441b-9170-2e5a4e0ce114
keywords:
- 绘制内核模式视频传输 WDK DirectDraw 接口有关内核模式视频传输
- 有关内核模式视频传输 DirectDraw 内核模式视频传输 WDK Windows 2000 显示
- 有关内核模式视频传输的内核模式视频传输 WDK DirectDraw
- 视频传输内核模式 WDK DirectDraw，有关内核模式视频传输
- 绘制内核模式视频传输 WDK DirectDraw
- DirectDraw 内核模式视频传输 WDK Windows 2000 显示
- 内核模式视频传输 WDK DirectDraw
- 视频传输内核模式 WDK DirectDraw
- 将 WDK DirectDraw
- 视频捕获 WDK 视频传输内核模式
- miniVDD WDK DirectDraw
- 总线控制 WDK DirectDraw
- V 同步 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e47a61baa89f585df507c30b8b10e263cee410a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522591"
---
# <a name="kernel-mode-video-transport"></a>内核模式视频传输


## <span id="ddk_kernel_mode_video_transport_gg"></span><span id="DDK_KERNEL_MODE_VIDEO_TRANSPORT_GG"></span>


本主题介绍内核模式视频传输，因为它存在于 Microsoft Windows 2000 和更高版本操作系统上。

内核模式视频传输是指中增强了视频功能的 ring 0 （内核模式） 的新 Microsoft DirectDraw 组件。 此组件可访问 DxApi 接口。 此接口添加到[微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)Windows 2000 和更高版本操作系统下。

### <a name="span-idwindows2000andlaterspanspan-idwindows2000andlaterspanwindows-2000-and-later"></a><span id="windows_2000_and_later"></span><span id="WINDOWS_2000_AND_LATER"></span>Windows 2000 及更高版本

内核模式视频传输是指一个客户端，如 Microsoft DirectShow，可用于增强视频功能的 Microsoft DirectDraw 组件。 此功能的一个主要角色是调用微型端口驱动程序，并告诉它执行硬件的视频端口，并覆盖投掷 V 同步发生时。 此功能可支持最多十个缓冲区，而不会遇到硬件限制，只要硬件视频端口支持 V 同步中断请求 (IRQ)。 DirectDraw 时客户端指定 autoflipping 和硬件不能 autoflip Microsoft DirectX 5.0 和更高版本提供的版本会自动使用此功能。

内核模式视频传输还可以确保增强型的捕获支持。 在 Microsoft Windows 98 / 我和 Microsoft Windows 2000 及更高版本中，基于 WDM 的视频捕获驱动程序运行在内核模式下直接访问帧缓冲区。 捕获驱动程序可以"手动"翻转覆盖。 Windows 2000 和更高版本的微型端口视频传输驱动程序可以提供的硬件的视频端口或显示; 从 V 同步通知它还可以获取字段极性，捕获垂直遮蔽的间隔 (VBI) 数据时非常有用。

虽然内核模式驱动程序的主要目的是增强硬件的视频端口 autoflipping 功能，但它还支持视频总线主机，可以编写在内核模式下的数据。 总线 master 可以由于模式发生变化，在图面前收到通知或因为启动全屏幕的命令提示符实例。 由于新的驱动程序支持允许总线主控形状来调用之前发生的更改，总线 master 可以关闭而不会导致问题。

 

 





