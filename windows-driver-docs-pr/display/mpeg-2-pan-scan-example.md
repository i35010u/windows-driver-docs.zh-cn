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
ms.openlocfilehash: d91ffd7b8f5257b26163b50036a7bdcc1a276db7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840550"
---
# <a name="mpeg-2-pan-scan-example"></a>MPEG-2 平移扫描示例


## <span id="ddk_mpeg_2_pan_scan_example_gg"></span><span id="DDK_MPEG_2_PAN_SCAN_EXAMPLE_GG"></span>


当使用[**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的**PictureSourceRect16thPel**成员来选择由 mpeg-2 视频平移扫描参数指定的区域时，可以计算**PictureSourceRect16thPel**成员的值使用以下表达式。 当使用**PictureSourceRect16thPel**时，这些值不应违反 alpha blend 组合缓冲区所述的限制。 有关详细信息，请参阅 DXVA\_BlendCombination 结构的 "**备注**" 部分。

某些 MPEG-2 平移扫描参数可能会违反这些约束，特别是在某些 MPEG-2 DVD 内容中，需要对**PictureSourceRect16thPel**进行一些调整。

-   **left** = 8 x （*水平\_大小* - *显示\_水平\_大小*）-*框架\_中心\_水平\_偏移*

-   **top** = 8 x （*垂直\_大小-显示\_垂直\_大小*）-*框架\_中心\_垂直\_偏移*

-   **right** = **left** + （16 x *\_水平\_大小*）

-   **底端** = **top** + （16 x *\_垂直\_大小*）

然后，DXVA\_BlendCombination 结构的**PictureDestinationRect**成员通常将使用以下值：

-   **left** = 0 或8（如[DVD 704-宽非平移扫描图片示例](dvd-704-wide-non-pan-scan-example.md)中所示）

-   **top** = 0

-   **右** = **左** + *显示\_水平\_大小*

-   **底端** = **顶部** + *显示\_垂直\_大小*

 

 





