---
title: 在目标矩形中显示示例和背景颜色
description: 以下主题说明如何在目标矩形中显示与背景色的各种示例。
ms.assetid: 324fa569-4b2e-4ee1-9988-d08020df78e9
keywords:
- DeinterlaceBltEx，目标矩形
- 目标矩形 WDK DirectX VA
- 背景色选项 WDK DirectX VA
- 取消隔行扫描 WDK DirectX va，因此目标矩形
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 954b0540f29d0007988cfaef50f21084a0920b65
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323777"
---
# <a name="displaying-samples-and-background-color-in-the-target-rectangle"></a>在目标矩形中显示样本和背景色


## <span id="ddk_displaying_samples_and_background_color_in_the_target_rectangle_gg"></span><span id="DDK_DISPLAYING_SAMPLES_AND_BACKGROUND_COLOR_IN_THE_TARGET_RECTANGLE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。

在 Windows Server 2003 SP1 及更高版本的 VMR 和 Windows XP SP2 和更高版本可以指定目标矩形和背景色，以确定如何显示的视频流和子流。

VMR 指定目标矩形，以确定您的驱动程序应输出定向到的目标面中的位置。 源矩形的坐标始终被指定为源面; 中的绝对位置同样，目标矩形和目标矩形的坐标始终被指定为目标面中的绝对位置。 通常情况下，为视频流和子流的源和目标矩形是在源和目标的面; 具有相同的大小但是，这是不总是这种情况。 有关详细信息，请参阅[处理 Subrectangles](processing-subrectangles.md)。

以下主题说明如何在目标矩形中显示与背景色的各种示例：

[显示 16:9 视频 4:3 目标面中](displaying-16-9-video-within-a-4-3-destination-surface.md)

[将视频 Stream 和使用不同的纵横比的子流相结合](combining-video-stream-and-substream-with-different-aspect-ratios.md)

[将两个流与具有不同高度和宽度相结合](combining-two-streams-with-different-heights-and-widths.md)

 

 





