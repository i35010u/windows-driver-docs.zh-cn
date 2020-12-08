---
title: 反交错和帧速率转换
description: 反交错和帧速率转换
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，帧速率转换
- 视频加速 WDK DirectX，帧速率转换
- VA WDK DirectX，帧速率转换
- DirectX 视频加速 WDK Windows 2000 显示，取消隔行扫描
- 视频加速 WDK DirectX，取消隔行扫描
- VA WDK DirectX，取消隔行扫描
- 取消隔行扫描 WDK DirectX VA
- 帧速率转换 WDK DirectX VA
- 取消隔行扫描 WDK DirectX VA，关于取消隔行扫描
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ac789f78ce4385aaf867ce6db21364ae6cd7615
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809571"
---
# <a name="deinterlacing-and-frame-rate-conversion"></a>反交错和帧速率转换


## <span id="ddk_deinterlacing_and_frame_rate_conversion_gg"></span><span id="DDK_DEINTERLACING_AND_FRAME_RATE_CONVERSION_GG"></span>


DirectDraw 和图形设备驱动程序之间的 DDI 扩展了 DirectX VA，以支持视频内容的取消隔行扫描和帧速率转换，方法是使用 DirectDraw DDI 和 Direct3D DDI 的内核模式部分。 取消隔行扫描和帧速率转换接口与所有视频演示机制无关。

取消隔行扫描或帧速率转换过程的输出始终为渐进帧。

若要使用此接口，必须满足以下要求：

-   Deinterlaced 输出必须位于目标 DirectDraw 表面中。 此要求会排除所有硬件覆盖解决方案。

-   图形引擎和硬件覆盖（如果存在）必须支持最少 bob 和编织取消隔行扫描功能。

-   此 DDI 适用于 Microsoft Windows XP SP1 和更高版本。

本部分涵盖了以下主题：

[反交错模式](deinterlace-modes.md)

[帧速率转换模式](frame-rate-conversion-modes.md)

[Bob 反交错](bob-deinterlacing.md)

[将反交错 DDI 映射到 DirectDraw 和 DirectX VA](mapping-the-deinterlace-ddi-to-directdraw-and-directx-va.md)

[要进行反交错和帧速率转换的视频内容](video-content-for-deinterlace-and-frame-rate-conversion.md)

[64 位操作系统上的反交错](deinterlacing-on-64-bit-operating-systems.md)

[合并反交错和视频子流合成内容](combining-deinterlacing-and-video-substream-compositing.md)

[反交错的示例函数](sample-functions-for-deinterlacing.md)

 

 





