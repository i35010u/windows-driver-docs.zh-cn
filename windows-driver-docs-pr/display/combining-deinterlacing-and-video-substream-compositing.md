---
title: 合并反交错和视频子流合成内容
description: 合并反交错和视频子流合成内容
ms.assetid: d62fe460-104d-4aff-a88c-3dc5829321fa
keywords:
- DeinterlaceBltEx
- 取消隔行扫描 WDK DirectX VA，组合子流组合
- 组合子流合成 WDK DirectX VA
- 视频子流合成 WDK DirectX VA
- 子流合成 WDK DirectX VA
- VMR WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44175382b5677eaa8f6555121b13f65ea4f70bb8
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065676"
---
# <a name="combining-deinterlacing-and-video-substream-compositing"></a>合并反交错和视频子流合成内容


## <span id="ddk_combining_deinterlacing_and_video_substream_compositing_gg"></span><span id="DDK_COMBINING_DEINTERLACING_AND_VIDEO_SUBSTREAM_COMPOSITING_GG"></span>


本部分仅适用于 Microsoft Windows Server 2003 Service Pack 1 (SP1) 和更高版本，以及 Windows XP Service Pack 2 (SP2) 和更高版本。

若要在内存带宽有限的情况下改善硬件的视频质量，驱动程序编写器可以在其显示驱动程序中实现 [**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md) 函数。 **DeinterlaceBltEx**函数将在 YUV 颜色空间内组合在视频流顶部组合视频 substreams 的操作，这些操作包含取消隔行扫描和/或帧速率转换每个视频帧的操作。 建议驱动程序编写者为其所有取消隔行扫描模式支持其驱动程序中的 **DeinterlaceBltEx** 函数。

以下主题介绍如何支持 **DeinterlaceBltEx**：

[DeinterlaceBltEx 概述](overview-of-deinterlacebltex.md)

[报告 DeinterlaceBltEx 支持](reporting-support-for-deinterlacebltex.md)

[提供视频子流和目标图面](supplying-video-substream-and-destination-surfaces.md)

[支持视频子流和目标图面上的操作](supporting-operations-on-video-substream-and-destination-surfaces.md)

[在目标矩形中显示样本和背景色](displaying-samples-and-background-color-in-the-target-rectangle.md)

[处理子矩形](processing-subrectangles.md)

[输入缓冲区顺序](input-buffer-order.md)

[在 64 位操作系统上进行反交错与合成](deinterlacing-and-compositing-on-64-bit-operating-systems.md)

 

