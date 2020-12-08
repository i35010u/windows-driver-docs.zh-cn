---
title: 在目标矩形中显示示例和背景色
description: 以下主题演示如何在目标矩形中显示具有背景色的各种示例。
keywords:
- DeinterlaceBltEx，目标矩形
- 目标矩形 WDK DirectX VA
- 背景颜色选项 WDK DirectX VA
- 取消隔行扫描 WDK DirectX VA，目标矩形
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 2c3f54a9c526461b513b7b988d4b8c4a4c37f6f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809213"
---
# <a name="displaying-samples-and-background-color-in-the-target-rectangle"></a>在目标矩形中显示样本和背景色


## <span id="ddk_displaying_samples_and_background_color_in_the_target_rectangle_gg"></span><span id="DDK_DISPLAYING_SAMPLES_AND_BACKGROUND_COLOR_IN_THE_TARGET_RECTANGLE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

Windows Server 2003 SP1 及更高版本和 Windows XP SP2 及更高版本上的 VMR 可以指定目标矩形和背景色，以确定视频流和 substreams 的显示方式。

VMR 指定目标矩形，以确定驱动程序应将输出定向到的目标图面中的位置。 源矩形的坐标始终指定为源图面中的绝对位置;同样，目标矩形和目标矩形的坐标始终指定为目标图面中的绝对位置。 通常，视频流和 substreams 的源和目标矩形的大小与源和目标的表面相同;但这并不总是如此。 有关详细信息，请参阅 [处理 Subrectangles](processing-subrectangles.md)。

以下主题演示如何在目标矩形中显示具有背景色的各种示例：

[在 4:3 目标图面中显示 16:9 视频](displaying-16-9-video-within-a-4-3-destination-surface.md)

[结合不同纵横比的视频流和子流](combining-video-stream-and-substream-with-different-aspect-ratios.md)

[将高度和宽度不同的两个流合并](combining-two-streams-with-different-heights-and-widths.md)

 

 





