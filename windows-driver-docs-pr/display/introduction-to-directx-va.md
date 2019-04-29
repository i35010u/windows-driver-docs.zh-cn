---
title: DirectX VA 简介
description: DirectX VA 简介
ms.assetid: e7d4faf7-f6ec-49ec-8116-faeed1ddd01c
keywords:
- DirectX 视频加速 WDK Windows 2000 显示有关 DirectX 视频加速
- 视频加速 WDK DirectX，有关 DirectX 视频加速
- VA WDK DirectX，有关 DirectX 视频加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffd1bd3781b85d84f86b4a7588756e7b65bb9432
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362131"
---
# <a name="introduction-to-directx-va"></a>DirectX VA 简介


## <span id="ddk_introduction_to_directx_va_gg"></span><span id="DDK_INTRODUCTION_TO_DIRECTX_VA_GG"></span>


DirectX VA 允许将频繁地执行简单的硬件快捷键要执行的视频处理操作。 限于给快捷键不太复杂的视频处理操作允许视频解码加速度也要为与最小到加速器的自定义项的各种视频标准来完成。 视频处理操作的执行频率较低且更复杂，例如位流分析和可变长度解码 (VLD)，可以执行主机 CPU 上。

DirectX VA API 和相应[动作补偿](motion-compensation.md)DDI 提供支持以下操作：

-   [Alpha 值混合处理](https://msdn.microsoft.com/library/windows/hardware/ff538232)的目的，例如 DVD 子图支持。

-   [加密](encryption-support.md)需要它的应用程序。

-   [取消隔行和帧速率转换](deinterlacing-and-frame-rate-conversion.md)的视频内容。

-   [ProcAmp](procamp-control-processing.md)控制和后续处理的视频内容。

-   保护视频内容从未经授权的复制和显示通过[认证的输出保护协议](copp-processing.md)。

此处提供的信息也适用于应用程序和设备驱动程序开发人员。 指定的格式定义的用户模式下主机解码器和内核模式设备驱动程序之间交换信息的方式。 在大多数情况下，从主机到设备驱动程序传输数据，但在某些情况下，在另一个方向发送数据。

有关使用用于解码 Windows media 视频格式的示例代码，请参阅 Windows 媒体移植工具包中的 Windows 媒体示例驱动程序。 Windows 媒体移植工具包用于将音频和视频为 Windows media 格式转换。

有关 Windows media 格式的支持，必须使用 Windows Media 视频编解码器 9 或更高版本。 Windows Media 视频编解码器版本 8 与 Windows XP 一起提供并支持 DirectX 弗吉尼亚

使用的显示驱动程序[去隔行 DDI](deinterlacing-and-frame-rate-conversion.md)，必须隔行扫描的视频内容，并将其正确标记为隔行扫描。 视频混合呈现器 (VMR) 与取消隔行扫描 DDI 结合使用 VIDEOINFOHEADER2 结构，来取消隔行扫描，并执行帧速率转换。 VIDEOINFOHEADER2 结构的详细信息，请参阅 Windows SDK 文档。

[ProcAmp 控件 DDI](procamp-control-processing.md)扩展了 DirectX VA，以支持 ProcAmp 控件和图形设备驱动程序的后续处理的视频内容。 DDI 映射到现有的 DirectDraw 和 DirectX VA DDI。 不能通过访问 DDI **IAMVideoAccelerator**接口。 ProcAmp 控件 DDI 是在 Microsoft DirectX 9.0 和更高版本中可用。

[实施的当前标准](implementation-of-current-standards.md)主题详细介绍的硬件加速器和软件解码器要求必须满足以下、 经过运动补偿视频编解码器标准：ITU-T H.261、 mpeg-1、 mpeg-2 (H.262)、 ITU-T H.263、 MPEG 4、 MPEG 4 AVC (H.264) 和 vc-1。

提供与 DirectX 弗吉尼亚没有工具 有关为 Windows 媒体支持提供的工具的详细信息，请参阅 Windows 媒体移植工具包。

 

 





