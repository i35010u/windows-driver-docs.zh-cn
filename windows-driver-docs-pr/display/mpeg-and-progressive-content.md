---
title: MPEG 和逐行扫描内容
description: MPEG 和逐行扫描内容
keywords:
- MPEG WDK 视频端口扩展
- 累进内容标识 WDK 视频端口扩展
- PROGRESSIVE_FRAME
- TOP_FIELD_FIRST
- REPEAT_FIRST_FIELD
- DirectX VPE 支持 WDK DirectDraw，累进内容标识
- 绘制 VPEs WDK DirectDraw，渐进内容标识
- DirectDraw VPEs WDK Windows 2000 显示，渐进内容标识
- 视频端口扩展 WDK DirectDraw，累进内容标识
- VPEs WDK DirectDraw，累进内容标识
- 3 2 下拉 WDK 视频端口扩展
- 标识渐进式内容
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c5f103e0aab3eb1196f15125dc598526d980a2c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836515"
---
# <a name="mpeg-and-progressive-content"></a>MPEG 和逐行扫描内容


## <span id="ddk_mpeg_and_progressive_content_gg"></span><span id="DDK_MPEG_AND_PROGRESSIVE_CONTENT_GG"></span>


MPEG-2 语法提供识别累进内容和3:2 下拉标记所需的信息。 此信息存储在以下1位标志中每个帧的标头中：

-   渐进式 \_ 帧：如果 **为 TRUE，则** 表示帧)  (的两个字段实际上来自同一时刻 (渐进式影片) 。 **为 FALSE** 时，这表示字段可能是帧时间的一半 (交错视频) 的一部分。

-   \_ \_ 第一个字段：指示哪个字段在第一次出现。

-   重复 \_ 第一个 \_ 字段：指示是否应为3:2 下拉字段重复字段。

在最新的 DirectX 版本下使用 VPE 和 DirectDraw 时，如果这些标志或从这些标志派生的信号可以通过每个字段传达给系统，则可以始终以最佳质量显示视频。 DirectShow 还支持隔行扫描视频，其中包含媒体示例中的新标志，用于指示未压缩的视频媒体示例是完整帧还是字段，以及任何其他信息。 如使用 [VPE 显示交错视频](displaying-interleaved-video-with-vpe.md) 部分中所述，可以通过使用基于帧的媒体示例或基于字段的媒体示例，指示 DirectShow 按帧在显示模式之间切换。

 

 





