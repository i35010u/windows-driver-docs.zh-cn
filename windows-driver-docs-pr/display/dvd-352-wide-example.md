---
title: DVD 352 像素宽度示例
description: DVD 352 像素宽度示例
keywords:
- alpha-blend 组合 WDK DirectX VA，DVD 352-范围示例
- 混合图片 WDK DirectX VA，DVD 352-范围示例
- DVD 352-范围示例 WDK DirectX VA
- 352-内部示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e98060bf630c071f6728a708f6c25603100bc75
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809111"
---
# <a name="dvd-352-wide-example"></a>DVD 352 像素宽度示例


## <span id="ddk_dvd_352_wide_example_gg"></span><span id="DDK_DVD_352_WIDE_EXAMPLE_GG"></span>


DVD 可以使用352范围的图片，可以通过使用 [**DXVA \_ BlendCombination**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的 **PictureSourceRect16thPel** 成员将其延伸到宽度704， (以亮度样本间距) 的第16倍。

**PictureSourceRect16thPel** 成员定义具有以下值的源矩形：

-   **left** = 0

-   **right** = 16 X (**左**  +  *水平 \_ 大小*) = 5632

[**DXVA \_ BlendCombination**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的 **PictureDestinationRect** 成员定义了两个具有以下值的备选目标矩形：

1.  具有以下值的目标矩形：
    -   **left** = 8
    -   **向右**  = **left** + (2 X *水平 \_ 大小*) = 712

2.  具有以下值的目标矩形：
    -   **left** = 0
    -   **right** = left + (2 X *水平 \_ 大小*) = 704

在第二种情况下，DXVA BlendCombination 结构的 **GraphicDestinationRect** 成员所指示的矩形 \_ 将被替换为八的左侧，以补偿已移动的图片目标

这两个替代方法中的第二个仅创建用于显示的目标区域。

 

