---
title: MPEG 和渐进式内容
description: MPEG 和渐进式内容
ms.assetid: 6973011a-dcee-4411-9382-8c0af2bd85b1
keywords:
- MPEG WDK 的视频端口扩展
- 渐进式内容标识 WDK 的视频端口扩展
- PROGRESSIVE_FRAME
- TOP_FIELD_FIRST
- REPEAT_FIRST_FIELD
- DirectX VPE 支持 WDK DirectDraw、 渐进式内容标识
- 绘制 VPEs WDK DirectDraw，渐进式内容标识
- DirectDraw VPEs WDK Windows 2000 显示，渐进式内容标识
- 视频端口扩展 WDK DirectDraw，渐进式内容标识
- VPEs WDK DirectDraw，渐进式内容标识
- 3 2 的下拉式 WDK 的视频端口扩展
- 标识渐进式内容
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 867da7bac3ce569becb1388d4e8afcd9b4a90f7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519423"
---
# <a name="mpeg-and-progressive-content"></a>MPEG 和渐进式内容


## <span id="ddk_mpeg_and_progressive_content_gg"></span><span id="DDK_MPEG_AND_PROGRESSIVE_CONTENT_GG"></span>


MPEG 2 语法提供了标识渐进式内容和 3:2 下拉列表所需的信息。 此信息存储在以下的 1 位标志中每个帧的标头：

-   渐进式\_帧：当 **，则返回 TRUE**，这表示的两个字段 （帧） 实际上是从相同的时间即时 （渐进式电影）。 当**FALSE**，这表示字段可能是帧时间间隔 （交错视频） 的一半。

-   顶部\_字段\_第一个：指示哪个字段出现在时间中的第一个。

-   重复\_第一个\_字段：指示是否应为 3:2 下拉方式重复字段。

使用 VPE 和 DirectDraw 最新的 DirectX 版本下，视频可以始终使用显示获得尽可能好的质量如果这些标志或派生自这些标志的信号可以传递到在每个字段的基础上的系统。 交错的视频还可以通过 DirectShow，与新标志在媒体示例中，以指示未压缩视频媒体示例是完整的框架或字段，以及任何其他信息支持。 如中所述[VPE 与显示交错视频](displaying-interleaved-video-with-vpe.md)部分中，可以指示 DirectShow 基于每个帧来通过使用基于帧的媒体示例或基于字段的媒体示例的显示模式之间切换。

 

 





