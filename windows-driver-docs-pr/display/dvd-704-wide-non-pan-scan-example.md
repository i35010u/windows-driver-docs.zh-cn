---
title: DVD 704 像素宽度非平移扫描示例
description: DVD 704 像素宽度非平移扫描示例
keywords:
- alpha-blend 组合 WDK DirectX VA，DVD 704 范围内的非平移扫描示例
- 混合图片 WDK DirectX VA，DVD 704 范围内的非平移扫描示例
- DVD 704 范围内的非平移扫描示例 WDK DirectX VA
- 704范围内非平移扫描示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ebaed98cc320400777cdd033f950f9856a4de94
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809103"
---
# <a name="dvd-704-wide-non-pan-scan-example"></a>DVD 704 像素宽度非平移扫描示例


## <span id="ddk_dvd_704_wide_non_pan_scan_example_gg"></span><span id="DDK_DVD_704_WIDE_NON_PAN_SCAN_EXAMPLE_GG"></span>


如果使用 [mpeg-2 Pan-Scan 示例](mpeg-2-pan-scan-example.md)) 中所述的方法，则在 DVD 上使用适用于704的图片的 mpeg-2 需要一个超出解码图片边界的源矩形 (。 在这种情况下，DVD 指定的 *显示 \_ 水平 \_ 大小* 为720，超过解码图片的 *水平 \_ 大小* 704。 当源矩形超过解码图片的边界时，主机软件解码器负责裁剪源矩形，使其不会到达已分配的源区域外，并用于管理目标矩形以调整剪辑。

源矩形由 [**DXVA \_ BlendCombination**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的 **PictureSourceRect16thPel** 成员定义 (的亮度样本间距解析) 的第一十六个，具有以下值：

-   **left** = 0

-   **right** = 16 X (**左**  +  *水平 \_ 大小*) = 11264

图片目标矩形是由 [**DXVA \_ BlendCombination**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的 **PictureDestinationRect** 成员定义的， (采用以下两种替代方法之一) ：

1.  具有以下值的矩形：
    -   **left** = (*显示 \_ 水平 \_ 大小* -ˆ " *水平 \_ 大小*) /2 = 8
    -   **向右**  = **左**  + *水平 \_ 大小*= 712

2.  具有以下值的矩形：
    -   **left** = 0
    -   **向右**  = **左**  + *水平 \_ 大小*= 704

在第二种情况下， [**DXVA \_ BlendCombination**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的 **GraphicDestinationRect** 成员所指示的矩形将被替换为八个样本的左侧，以弥补移动的图片目标。

这两个替代方法中的第二个仅创建用于显示的目标区域。

 

