---
title: USB 视频类驱动程序概述
description: USB 视频类驱动程序概述
ms.assetid: 890d448e-bfee-462d-8cce-a2cca42f2f6d
keywords:
- USB 视频类驱动程序 WDK AVStream，关于 USB 视频类驱动程序
- 视频类驱动程序 WDK USB，关于 USB 视频类驱动程序
- UVC 驱动程序 WDK AVStream，关于 USB 视频类驱动程序
- 用户模式客户端 WDK USB 视频类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a674d7f7fcdb6bf1961e57761e70708124073c1
ms.sourcegitcommit: baf3075858705d4c78d4ea4b0869bf6291bcb823
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2020
ms.locfileid: "85112129"
---
# <a name="usb-video-class-driver-overview"></a>USB 视频类驱动程序概述

如果要为网络摄像机或数字摄像机提供驱动程序，请考虑使用系统提供的通用串行总线（USB）视频类驱动程序，Usbvideo.sys。 USB 视频类（UVC）驱动程序是 Microsoft 提供的 AVStream 微型驱动程序，为 USB 视频类设备提供驱动程序支持。 如果设备使用 UVC，则无需提供自己的驱动程序。 相反，设备会自动与系统提供的驱动程序一起工作。

在 USB 视频类模型中，供应商不编写驱动程序;相反，供应商根据视频实现[论坛](https://www.usb.org/documents)网站上的*视频设备规范文档的通用串行总线设备类定义*中的指南来实现视频流式处理硬件。 UVC 驱动程序会直接查询硬件以获取其功能，然后驱动设备，而无需专用驱动程序。

你可以根据需要扩展 UVC 驱动程序功能来添加特定于供应商的处理。

下表显示了对不同版本的 Windows 中的 UVC 的支持：

| UVC 版本 | Windows Vista/XP | Windows 7 | Windows 8 |
|--|--|--|--|
| USB Video 类1.5 （视频编解码器） | 不支持 | 不支持 | 支持 |
| USB 视频类1。1 | 不支持 | 支持 | 支持 |
| USB 视频类1。0 | 支持 | 支持 | 支持 |

从 Windows 8 开始，支持 h.264 视频编解码器（编码器/解码器）。 Node.js 是一种开放标准，可用于减少网络带宽和存储空间的使用。 这会提高给定比特率的视频质量。 有关详细信息，请参阅[USB H-p 视频相机支持](usb-h-264-video-cameras-support.md)。 另请参阅[适用于 h-p 的 USB 视频类的 Microsoft 建议的扩展](https://docs.microsoft.com/previous-versions/windows/hardware/download/dn550976(v=vs.85))。

以下列表显示了使用 Usbvideo.sys 驱动程序的一些优点：

- 无需安装 CD

- 无驱动程序写入成本

- 无维护成本

- 供应商添加功能的机会

- 更轻松地通过公共符号进行调试

- 使用驱动程序验证程序

- 适用于已检查的 OS 版本

- 符合 ACPI 电源管理

- 符合选择性挂起电源管理

- 支持媒体基础和 DirectShow 中的多媒体 Api

系统提供的 Usbvideo.sys 驱动程序在不同版本的 Windows 中支持以下 UVC 功能：

| UVC 功能 | Windows Vista/XP | Windows 7 | Windows 8 |
|--|--|--|--|
| 单个视频控制界面和一个或多个视频流式处理接口 | 支持 | 支持 | 支持 |
| 标准单位和终端，包括扩展单元 | 支持 | 支持 | 支持 |
| 对于 UVC 规范中定义的所有三个方法，仍支持图像捕获 | 支持 | 支持 | 支持 |
| 大容量和同步设备 | 支持 | 支持 | 支持 |
| 使用探测提交控件进行流式处理参数协商 | 支持 | 支持 | 支持 |
| 压缩格式： MJPEG、DV | 支持 | 支持 | 支持 |
| 未压缩格式： YUY2、NV12 | 支持 | 支持 | 支持 |
| 支持捕获和呈现设备 | 支持 | 支持 | 支持 |
| 压缩格式： MPEG2TS | 不支持 | 不支持 | 不支持 |
| 基于流和基于帧的格式 | 不支持 | 支持 | 支持 |
| H.264 视频编解码器 | 不支持 | 不支持 | 支持 |

## <a name="customizing-the-uvc-driver"></a>自定义 UVC 驱动程序

可以通过提供[扩展插件单元](introduction-to-usb-video-class-extension-units.md)，自定义对 UVC 的支持。 扩展单元在设备和供应商提供的应用程序之间提供专用控制通道。

## <a name="additional-resources"></a>其他资源

若要测试 UVC 实现，可以使用以下工具：

- GraphEdit

- KsStudio

- USBView

有关这些工具的详细信息，请参阅[AVStream 测试和调试](avstream-testing-and-debugging.md)。

可在[Usb 实现论坛](https://www.usb.org/documents)网站上找到 Usb 视频类1.1 的规格。
