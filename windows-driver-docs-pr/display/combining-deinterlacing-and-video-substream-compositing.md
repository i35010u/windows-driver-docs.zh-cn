---
title: 组合去隔行和视频子流组合
description: 组合去隔行和视频子流组合
ms.assetid: d62fe460-104d-4aff-a88c-3dc5829321fa
keywords:
- DeinterlaceBltEx
- 取消隔行扫描 WDK DirectX VA，组合子流组合的情况下
- 组合的子流组合的情况下 WDK DirectX VA
- 视频子流组合的情况下 WDK DirectX VA
- 组合的情况下 WDK DirectX VA 的子流
- VMR WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bc6b2687d08c9b0a38c244d6a08834979bfce22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522841"
---
# <a name="combining-deinterlacing-and-video-substream-compositing"></a>组合去隔行和视频子流组合


## <span id="ddk_combining_deinterlacing_and_video_substream_compositing_gg"></span><span id="DDK_COMBINING_DEINTERLACING_AND_VIDEO_SUBSTREAM_COMPOSITING_GG"></span>


本部分仅适用于 Microsoft Windows Server 2003 Service Pack 1 (SP1) 和更高版本和 Windows XP Service Pack 2 (SP2) 和更高版本。

若要提高硬件有限的内存带宽上的视频质量，驱动程序编写人员可以实现[ **DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563927)其显示器驱动程序中的函数。 **DeinterlaceBltEx**函数组合后，YUV 颜色空间内，操作的复合视频 substreams 之上使用取消隔行扫描的操作和/或帧速率视频流将转换每个视频帧。 驱动程序编写器均支持我们鼓励**DeinterlaceBltEx**所有其取消隔行扫描模式及其驱动程序中的函数。

以下主题介绍如何支持**DeinterlaceBltEx**:

[DeinterlaceBltEx 的概述](overview-of-deinterlacebltex.md)

[报告对 DeinterlaceBltEx 的支持](reporting-support-for-deinterlacebltex.md)

[提供视频子流和目标图面](supplying-video-substream-and-destination-surfaces.md)

[支持视频子流和目标图面上的操作](supporting-operations-on-video-substream-and-destination-surfaces.md)

[显示示例和背景颜色的目标矩形中](displaying-samples-and-background-color-in-the-target-rectangle.md)

[处理 Subrectangles](processing-subrectangles.md)

[输入的缓冲区顺序](input-buffer-order.md)

[取消隔行和 64 位操作系统上的进行合成](deinterlacing-and-compositing-on-64-bit-operating-systems.md)

 

 





