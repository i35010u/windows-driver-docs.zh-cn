---
title: DVD 704 像素宽度非平移扫描示例
description: DVD 704 像素宽度非平移扫描示例
ms.assetid: df335e5e-4f7c-440a-88ef-00f6e0f916e2
keywords:
- alpha-blend 组合 WDK DirectX VA，DVD 704 范围内的非平移扫描示例
- 混合图片 WDK DirectX VA，DVD 704 范围内的非平移扫描示例
- DVD 704 范围内的非平移扫描示例 WDK DirectX VA
- 704范围内非平移扫描示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b044ca93b058c5fc3671e888cfcdb091b187bec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839725"
---
# <a name="dvd-704-wide-non-pan-scan-example"></a>DVD 704 像素宽度非平移扫描示例


## <span id="ddk_dvd_704_wide_non_pan_scan_example_gg"></span><span id="DDK_DVD_704_WIDE_NON_PAN_SCAN_EXAMPLE_GG"></span>


在用于704的图片的 DVD 上使用 MPEG-2 时，需要一个超出解码图片边界的源矩形（如果使用[Mpeg-2 平移扫描示例](mpeg-2-pan-scan-example.md)中所述的方法）。 在这种情况下，DVD 指定的*显示\_水平\_大小*超过720，超过解码图片的*水平\_大小*704。 当源矩形超过解码图片的边界时，主机软件解码器负责裁剪源矩形，使其不会到达分配的源区域外，并用于管理要调整的目标矩形。裁剪。

源矩形由[**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的**PictureSourceRect16thPel**成员定义（采用亮度样本间距解析的第一样本），值为：

-   **left** = 0

-   **right** = 16 X （**左** + *水平\_大小*） = 11264

图片目标矩形由[**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的**PictureDestinationRect**成员（在亮度样本间距的一-第16位）定义，方法如下：

1.  具有以下值的矩形：
    -   **left** = （*显示\_水平\_大小*-ˆ "*水平\_大小*）/2 = 8
    -   **right** = **左** + *水平\_大小*= 712

2.  具有以下值的矩形：
    -   **left** = 0
    -   **right** = **左** + *水平\_大小*= 704

在第二种情况下， [**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的**GraphicDestinationRect**成员所指示的矩形将被八个样本左移，以弥补移动的图片目标。

这两个替代方法中的第二个仅创建用于显示的目标区域。

 

 





