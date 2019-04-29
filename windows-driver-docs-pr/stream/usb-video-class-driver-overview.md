---
title: USB 视频类驱动程序概述
description: USB 视频类驱动程序概述
ms.assetid: 890d448e-bfee-462d-8cce-a2cca42f2f6d
keywords:
- USB 视频类驱动程序 WDK AVStream 有关 USB 视频类驱动程序
- 有关 USB 视频类驱动程序的视频类驱动程序 WDK USB
- 有关 USB 视频类驱动程序 UVC 驱动程序 WDK AVStream
- 用户模式下客户端 WDK USB 视频类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a4595ae0a06228deb9872bbf14bb37d9cc068f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382548"
---
# <a name="usb-video-class-driver-overview"></a>USB 视频类驱动程序概述


如果要为网络摄像机或数码摄录机提供了驱动程序，请考虑使用系统提供通用串行总线 (USB) 视频类驱动程序，Usbvideo.sys。 USB 视频类 (UVC) 驱动程序是提供 USB 视频类设备驱动程序支持由 Microsoft 提供 AVStream 微型驱动程序。 当你的设备使用 UVC 时，您不需要提供您自己的驱动程序。 相反，设备会自动与系统提供的驱动程序。

在 USB 视频类模型中，供应商不编写驱动程序;相反，供应商实现根据中的指导原则的视频流式处理硬件[通用串行总线的设备类定义视频设备规范](https://go.microsoft.com/fwlink/p/?linkid=516989)。 UVC 驱动程序查询直接以获取其功能的硬件，然后驱动器在设备与所需的任何专有驱动程序。

可以选择性地扩展 UVC 驱动程序的功能，以添加特定于供应商的处理。

下表显示不同版本的 Windows 中对 UVC 的支持：

| UVC 版本                             | Windows Vista/XP | Windows 7     | Windows 8 |
|-----------------------------------------|------------------|---------------|-----------|
| USB 视频类 1.5 （H.264 视频编解码器） | 不支持    | 不支持 | 支持 |
| USB 视频类 1.1                     | 不支持    | 支持     | 支持 |
| USB 视频类 1.0                     | 支持        | 支持     | 支持 |

 

从 Windows 8 开始，支持 H.264 视频编解码器 （编码器/解码器）。 H.264 是允许高效视频压缩技术减少网络带宽和存储空间使用的开放标准。 这会导致给定的比特率更高的视频质量。 有关详细信息，请参阅[USB H.264 视频摄像机支持](usb-h-264-video-cameras-support.md)。 另请参阅[Microsoft 建议的 H.264 USB 视频类扩展](https://go.microsoft.com/fwlink/p/?LinkId=233063)。

以下列表显示了使用 Usbvideo.sys 驱动程序的一些优势：

-   安装所需的任何 CD
-   编写成本没有驱动程序
-   无需维护成本
-   供应商将功能添加的机会
-   更轻松地使用公共符号进行调试
-   适用于驱动程序验证程序
-   适用于检查 OS 内部版本号
-   符合 ACPI 电源管理
-   符合选择性挂起电源管理
-   在 Media Foundation 和 DirectShow 中支持多媒体 Api

系统提供 Usbvideo.sys 驱动程序的 Windows 不同版本中支持以下 UVC 功能：

| UVC 功能                                                                        | Windows Vista/XP | Windows 7     | Windows 8     |
|------------------------------------------------------------------------------------|------------------|---------------|---------------|
| 单一视频控件接口和一个或多个视频流式处理接口          | 支持        | 支持     | 支持     |
| 标准单位和终端，包括扩展单位                            | 支持        | 支持     | 支持     |
| 仍为 UVC 规范中定义的所有三个方法的的映像捕获支持 | 支持        | 支持     | 支持     |
| 大容量并同步设备                                                       | 支持        | 支持     | 支持     |
| 流式处理参数协商使用探测提交控件                        | 支持        | 支持     | 支持     |
| 压缩的格式：MJPEG, DV                                                      | 支持        | 支持     | 支持     |
| 未压缩的格式：YUY2 NV12                                                   | 支持        | 支持     | 支持     |
| 支持同时捕获和呈现的设备                                           | 支持        | 支持     | 支持     |
| 压缩的格式：MPEG2TS                                                         | 不支持    | 不支持 | 不支持 |
| 基于 Stream 的和基于帧的格式                                               | 不支持    | 支持     | 支持     |
| H.264 视频编解码器                                                                  | 不支持    | 不支持 | 支持     |

 

## <a name="customizing-the-uvc-driver"></a>自定义 UVC 驱动程序


可以通过提供自定义支持 UVC[插件的扩展单元](introduction-to-usb-video-class-extension-units.md)。 扩展单元提供的设备和供应商提供的应用程序之间的专用的控制通道。

## <a name="additional-resources"></a>其他资源


若要测试 UVC 实现，可以使用以下工具：

-   GraphEdit
-   KsStudio
-   USBView

有关这些工具的详细信息，请参阅[AVStream 测试和调试](avstream-testing-and-debugging.md)。

您可以下载压缩的一组规范从 USB 视频类 1.1[设备类页](https://go.microsoft.com/fwlink/p/?linkid=517016)USB 实现论坛网站上。

 

 




