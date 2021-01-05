---
title: DirectX VA 简介
description: DirectX VA 简介
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，关于 DirectX 视频加速
- 视频加速 WDK DirectX，关于 DirectX 视频加速
- VA WDK DirectX，关于 DirectX 视频加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b33256eef5f27db60fe69fe5bac7ad8ab74e9c4
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812555"
---
# <a name="introduction-to-directx-va"></a>DirectX VA 简介

DirectX 视频加速 (VA) 允许硬件加速器执行频繁执行的视频处理操作。 对于加速器而言，受限不太复杂的视频处理操作允许通过对加速器进行最小化自定义来实现各种视频标准的视频解码加速。 不经常执行且更复杂的视频处理操作（如位流分析和可变长度解码 (VLD) ）可在主机 CPU 上执行。

DirectX VA API 和相应的 [运动补偿](motion-compensation.md) DDI 为以下操作提供支持：

- 适用于的[Alpha 混合](directx-va-operations.md)，如 DVD 子画面支持。

- 对需要它的应用程序进行[加密](encryption-support.md)。

- 视频内容的[取消隔行扫描和帧速率转换](deinterlacing-and-frame-rate-conversion.md)。

- 视频内容的[ProcAmp](procamp-control-processing.md)控件和后处理。

- 保护视频内容不受未经授权的复制和[显示。](copp-processing.md)

此处提供的信息适用于应用程序和设备驱动程序开发人员。 指定的格式定义了如何在用户模式主机解码器和内核模式设备驱动程序之间交换信息。 在大多数情况下，将数据从主机传输到设备驱动程序，但在某些情况下，会以其他方向发送数据。

有关用于解码 Windows media 视频格式的示例代码，请参阅 Windows Media 移植工具包中的 Windows media 示例驱动程序。 Windows Media 移植套件用于将音频和视频转换为 Windows media 格式。

为了支持 Windows media 格式，必须使用 Windows Media 视频编解码器版本9或更高版本。 Windows XP 提供的 Windows Media 视频编解码器版本8不支持 DirectX VA。

对于使用 [取消隔行扫描 DDI](deinterlacing-and-frame-rate-conversion.md)的显示驱动程序，必须将视频内容隔行扫描并正确地标记为交错。 视频混合呈现器 (VMR) 将 VIDEOINFOHEADER2 结构与取消隔行扫描 DDI 结合使用，以进行取消隔行扫描并执行帧速率转换。 有关 VIDEOINFOHEADER2 结构的详细信息，请参阅 Windows SDK 文档。

[ProcAmp 控件 DDI](procamp-control-processing.md)扩展了 DirectX VA，以支持 ProcAmp 控制，并按图形设备驱动程序对视频内容进行处理。 DDI 映射到现有 DirectDraw 和 DirectX VA DDI。 不能通过 **IAMVideoAccelerator** 接口访问 DDI。 ProcAmp 控件 DDI 仅在 Microsoft DirectX 9.0 和更高版本中可用。

[当前标准的实现](implementation-of-current-standards.md)主题详细介绍了以下各项所需满足的硬件加速器和软件解码器要求：261、mpeg-2、MPEG-2、mpeg-2 (262) 、itu-t AVC、mpeg-2、mpeg-4 和)  (，以及 VC-1 的要求和的软件解码器要求的内容的详细信息。

DirectX VA 未提供任何工具。 有关为 Windows media 支持提供的工具的详细信息，请参阅 Windows Media 移植工具包。
