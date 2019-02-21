---
title: 取消隔行和帧速率转换
description: 取消隔行和帧速率转换
ms.assetid: 73435a68-532a-4a15-b2b9-a6165cadb8fe
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，帧速率转换
- 视频加速 WDK DirectX，帧速率转换
- VA WDK DirectX，帧速率转换
- DirectX 视频加速 WDK Windows 2000 显示，请去隔行
- 视频加速 WDK DirectX 去隔行
- VA WDK DirectX 去隔行
- 去隔行 WDK DirectX VA
- 帧速率转换 WDK DirectX VA
- 逐行 WDK DirectX va，因此有关去隔行扫描
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e31311751b166968cf89e08fb39eac0c4be0e425
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522210"
---
# <a name="deinterlacing-and-frame-rate-conversion"></a>取消隔行和帧速率转换


## <span id="ddk_deinterlacing_and_frame_rate_conversion_gg"></span><span id="DDK_DEINTERLACING_AND_FRAME_RATE_CONVERSION_GG"></span>


DirectDraw 和图形设备驱动程序之间 DDI 扩展了 DirectX VA 使用 DirectDraw DDI 和 Direct3D DDI 的内核模式部分支持的视频内容的去隔行和帧速率转换。 取消隔行扫描和帧速率转换接口的所有视频演示文稿机制无关。

去隔行或帧速率转换过程的输出始终是渐进式帧。

若要使用此接口，必须满足以下要求：

-   Deinterlaced 的输出必须以物理方式位于目标 DirectDraw 图面。 此要求可以阻止所有硬件覆盖解决方案。

-   图形引擎和硬件 overlay，如果存在，必须支持至少 bob 和 weave 实现去隔行功能。

-   此 DDI 适用于 Microsoft Windows XP SP1 和更高版本。

本部分介绍以下主题：

[取消隔行扫描模式](deinterlace-modes.md)

[帧速率转换模式](frame-rate-conversion-modes.md)

[Bob 去隔行](bob-deinterlacing.md)

[映射到 DirectDraw 和 DirectX VA DDI 取消隔行扫描](mapping-the-deinterlace-ddi-to-directdraw-and-directx-va.md)

[取消隔行扫描和帧速率转换的视频内容](video-content-for-deinterlace-and-frame-rate-conversion.md)

[在 64 位操作系统上去隔行](deinterlacing-on-64-bit-operating-systems.md)

[组合去隔行和视频子流组合](combining-deinterlacing-and-video-substream-compositing.md)

[有关去隔行示例函数](sample-functions-for-deinterlacing.md)

 

 





