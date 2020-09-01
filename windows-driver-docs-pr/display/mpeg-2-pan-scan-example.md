---
title: MPEG-2 平移扫描示例
description: MPEG-2 平移扫描示例
ms.assetid: 6ce4722c-5406-4b29-9171-ecab049320e7
keywords:
- alpha-blend 组合 WDK DirectX VA，MPEG-2 平移扫描示例
- 混合图片 WDK DirectX VA，MPEG-2 平移扫描示例
- PictureSourceRect16thPel
- MPEG-2 平移扫描示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b5c910b0e0b55a89357a697dcb519bf512bb08e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067316"
---
# <a name="mpeg-2-pan-scan-example"></a>MPEG-2 平移扫描示例


## <span id="ddk_mpeg_2_pan_scan_example_gg"></span><span id="DDK_MPEG_2_PAN_SCAN_EXAMPLE_GG"></span>


当使用[**DXVA \_ BlendCombination**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的**PictureSourceRect16thPel**成员来选择由 mpeg-2 视频平移扫描参数指定的区域时，可以使用以下表达式计算**PictureSourceRect16thPel**成员的值。 当使用 **PictureSourceRect16thPel**时，这些值不应违反 alpha blend 组合缓冲区所述的限制。 有关详细信息，请参阅 DXVA BlendCombination 结构的 " **备注** " 部分 \_ 。

某些 MPEG-2 平移扫描参数可能会违反这些约束，特别是在某些 MPEG-2 DVD 内容中，需要对 **PictureSourceRect16thPel**进行一些调整。

-   **left** = 8 x (*水平 \_ 大小*  -  *显示 \_ 水平 \_ 大小*) *帧 \_ 中心 \_ 水平 \_ 偏移*

-   **top** = 8 x (*垂直 \_ 大小-显示 \_ 垂直 \_ 大小*) *帧 \_ 中心 \_ 垂直 \_ 偏移*

-   **向右**  = **左**+ (16 x*显示 \_ 水平 \_ 大小*) 

-   **下**  = **顶部**+ (16 x*显示 \_ 垂直 \_ 大小*) 

DXVA BlendCombination 结构的 **PictureDestinationRect** 成员 \_ 通常将使用以下值：

-   **left** = 0 或 8 (如 [DVD 704 范围内的非平移扫描图片示例](dvd-704-wide-non-pan-scan-example.md)) 

-   **top** = 0

-   **向右**  = **左**  + *显示 \_ 水平 \_ 大小*

-   **下**  = **顶部**  + *显示 \_ 垂直 \_ 大小*

 

