---
title: MPEG-2 平移扫描示例
description: MPEG-2 平移扫描示例
keywords:
- alpha-blend 组合 WDK DirectX VA，MPEG-2 平移扫描示例
- 混合图片 WDK DirectX VA，MPEG-2 平移扫描示例
- PictureSourceRect16thPel
- MPEG-2 平移扫描示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c3d77d6ac1adfcf4e9519a0c5fc6bb0a6c01f80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836517"
---
# <a name="mpeg-2-pan-scan-example"></a>MPEG-2 平移扫描示例


## <span id="ddk_mpeg_2_pan_scan_example_gg"></span><span id="DDK_MPEG_2_PAN_SCAN_EXAMPLE_GG"></span>


当使用 [**DXVA \_ BlendCombination**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的 **PictureSourceRect16thPel** 成员来选择由 mpeg-2 视频平移扫描参数指定的区域时，可以使用以下表达式计算 **PictureSourceRect16thPel** 成员的值。 当使用 **PictureSourceRect16thPel** 时，这些值不应违反 alpha blend 组合缓冲区所述的限制。 有关详细信息，请参阅 DXVA BlendCombination 结构的 " **备注** " 部分 \_ 。

某些 MPEG-2 平移扫描参数可能会违反这些约束，特别是在某些 MPEG-2 DVD 内容中，需要对 **PictureSourceRect16thPel** 进行一些调整。

-   **left** = 8 x (*水平 \_ 大小*  -  *显示 \_ 水平 \_ 大小*) *帧 \_ 中心 \_ 水平 \_ 偏移*

-   **top** = 8 x (*垂直 \_ 大小-显示 \_ 垂直 \_ 大小*) *帧 \_ 中心 \_ 垂直 \_ 偏移*

-   **向右**  = **左**+ (16 x *显示 \_ 水平 \_ 大小*) 

-   **下**  = **顶部**+ (16 x *显示 \_ 垂直 \_ 大小*) 

DXVA BlendCombination 结构的 **PictureDestinationRect** 成员 \_ 通常将使用以下值：

-   **left** = 0 或 8 (如 [DVD 704 范围内的非平移扫描图片示例](dvd-704-wide-non-pan-scan-example.md)) 

-   **top** = 0

-   **向右**  = **左**  + *显示 \_ 水平 \_ 大小*

-   **下**  = **顶部**  + *显示 \_ 垂直 \_ 大小*

 

