---
title: DVD 352 像素宽度示例
description: DVD 352 像素宽度示例
ms.assetid: 22047c8e-30e3-4204-9f7d-b8b97be668ae
keywords:
- alpha-blend 组合 WDK DirectX VA，DVD 352-范围示例
- 混合图片 WDK DirectX VA，DVD 352-范围示例
- DVD 352-范围示例 WDK DirectX VA
- 352-内部示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68d550b9e68bcbd8a41f0be7fbb3a7d5049d97d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839728"
---
# <a name="dvd-352-wide-example"></a>DVD 352 像素宽度示例


## <span id="ddk_dvd_352_wide_example_gg"></span><span id="DDK_DVD_352_WIDE_EXAMPLE_GG"></span>


DVD 可以使用352范围的图片，通过使用[**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的**PictureSourceRect16thPel**成员（采用亮度样本间距的一-第16位），可以延伸到宽度704。

**PictureSourceRect16thPel**成员定义具有以下值的源矩形：

-   **left** = 0

-   **right** = 16 X （**左** + *水平\_大小*） = 5632

[**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的**PictureDestinationRect**成员定义了两个具有以下值的备选目标矩形：

1.  具有以下值的目标矩形：
    -   **left** = 8
    -   **right** = **左**+ （2 X*水平\_大小*） = 712

2.  具有以下值的目标矩形：
    -   **left** = 0
    -   **right** = left + （2 X*水平\_大小*） = 704

在第二种情况下，由 DXVA\_BlendCombination 结构的 " **GraphicDestinationRect** " 成员指示的矩形将向左移动8个，以补偿已移动的图片目标

这两个替代方法中的第二个仅创建用于显示的目标区域。

 

 





