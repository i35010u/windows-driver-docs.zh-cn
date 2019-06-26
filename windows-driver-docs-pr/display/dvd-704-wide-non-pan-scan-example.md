---
title: DVD 704 像素宽度非平移扫描示例
description: DVD 704 像素宽度非平移扫描示例
ms.assetid: df335e5e-4f7c-440a-88ef-00f6e0f916e2
keywords:
- alpha 混合组合 WDK DirectX VA，DVD 704 级非平移扫描示例
- 混合型的图片 WDK DirectX VA，DVD 704 级非平移扫描示例
- DVD 704 级非平移扫描示例 WDK DirectX VA
- 704 级非平移扫描示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74907e4fdb08c739780ad420b8fe69a9c1b477b6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380234"
---
# <a name="dvd-704-wide-non-pan-scan-example"></a>DVD 704 像素宽度非平移扫描示例


## <span id="ddk_dvd_704_wide_non_pan_scan_example_gg"></span><span id="DDK_DVD_704_WIDE_NON_PAN_SCAN_EXAMPLE_GG"></span>


使用 DVD 上的 mpeg-2 704 范围图片要求超过了已解码的图片的边界的源矩形 (如果使用的方法中所述[mpeg-2 平移扫描示例](mpeg-2-pan-scan-example.md))。 在这种情况下，指定 DVD*显示\_水平\_大小*的超过了已解码的图片的 720*水平\_大小*的 704。 当源矩形超过解码图片的边界时，主机软件解码器是负责为裁剪源矩形，使其达到分配的源区域之外，并管理目标矩形以进行调整的裁剪。

定义源矩形**PictureSourceRect16thPel**的成员[ **DXVA\_BlendCombination** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_blendcombination)结构 (中的六分之一亮度示例间距解决方法） 使用以下值：

-   **left** = 0

-   **右**= 16 X (**左** + *水平\_大小*) = 11264

由定义图片目标矩形**PictureDestinationRect**的成员[ **DXVA\_BlendCombination** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_blendcombination)结构 （在亮度示例间距分辨率的六分之一) 通过以下两种备选方案之一：

1.  使用以下值矩形：
    -   **左**= (*显示\_水平\_大小*âˆ'*水平\_大小*) / 2 = 8
    -   **right** = **left** + *horizontal\_size* = 712

2.  使用以下值矩形：
    -   **left** = 0
    -   **right** = **left** + *horizontal\_size* = 704

在第二种情况下，该矩形为由**GraphicDestinationRect**的成员[ **DXVA\_BlendCombination** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_blendcombination)结构移置开到由八个示例来弥补移动的图片目标的左侧。

以下两个替代方法的第二部分创建用于显示的目标区域。

 

 





