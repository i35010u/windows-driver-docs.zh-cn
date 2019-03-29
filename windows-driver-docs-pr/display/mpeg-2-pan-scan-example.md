---
title: MPEG-2 平移扫描示例
description: MPEG-2 平移扫描示例
ms.assetid: 6ce4722c-5406-4b29-9171-ecab049320e7
keywords:
- alpha 混合组合 WDK DirectX va，因此 mpeg-2 平移扫描示例
- 混合型的图片 WDK DirectX va，因此 mpeg-2 平移扫描示例
- PictureSourceRect16thPel
- MPEG 2 平移扫描示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a367dbac7ed5f8a20060b8e26068157d703e12b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575258"
---
# <a name="mpeg-2-pan-scan-example"></a>MPEG-2 平移扫描示例


## <span id="ddk_mpeg_2_pan_scan_example_gg"></span><span id="DDK_MPEG_2_PAN_SCAN_EXAMPLE_GG"></span>


当**PictureSourceRect16thPel**的成员[ **DXVA\_BlendCombination** ](https://msdn.microsoft.com/library/windows/hardware/ff563120)结构用于选择由 mpeg-2 视频平移扫描指定的区域参数、 的值**PictureSourceRect16thPel**可以使用以下表达式计算成员。 这些值应违反时使用的 alpha 混合组合缓冲区所述的限制**PictureSourceRect16thPel**。 有关详细信息，请参阅**备注**部分，了解 DXVA\_BlendCombination 结构。

带有某些 mpeg-2 平移扫描参数并，特别是，一些 mpeg-2 DVD 内容，需要一些调整到可能违反这些约束**PictureSourceRect16thPel**。

-   **左**= 8 x (*水平\_大小* - *显示\_水平\_大小*)-*帧\_centre\_水平\_偏移量*

-   **顶部**= 8 x (*垂直\_size-显示\_垂直\_大小*)-*帧\_中心\_垂直\_偏移量*

-   **右** = **左**+ (16 x*显示\_水平\_大小*)

-   **底部** = **顶部**+ (16 x*显示\_垂直\_大小*)

**PictureDestinationRect** DXVA 成员\_BlendCombination 结构然后通常使用以下值：

-   **左**= 0 或 8 (如[DVD 704 级非-平移-扫描图片示例](dvd-704-wide-non-pan-scan-example.md))

-   **top** = 0

-   **right** = **left** + *display\_horizontal\_size*

-   **bottom** = **top** + *display\_vertical\_size*

 

 





