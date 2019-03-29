---
title: DVD 352 像素宽度示例
description: DVD 352 像素宽度示例
ms.assetid: 22047c8e-30e3-4204-9f7d-b8b97be668ae
keywords:
- alpha 混合组合 WDK DirectX VA，DVD 352 范围示例
- 混合型的图片 WDK DirectX VA，DVD 352 范围示例
- DVD 352 范围示例 WDK DirectX VA
- 352 范围示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70453151dcb33539955ccb5bdf2050cf6f568001
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565298"
---
# <a name="dvd-352-wide-example"></a>DVD 352 像素宽度示例


## <span id="ddk_dvd_352_wide_example_gg"></span><span id="DDK_DVD_352_WIDE_EXAMPLE_GG"></span>


DVD 可以使用 352 范围图片，可以通过使用被拉伸到的宽度为 704 **PictureSourceRect16thPel**的成员[ **DXVA\_BlendCombination** ](https://msdn.microsoft.com/library/windows/hardware/ff563120)（在六分之一亮度示例间距分辨率的） 的结构。

**PictureSourceRect16thPel**成员定义一个具有以下值的源矩形：

-   **left** = 0

-   **右**= 16 X (**左** + *水平\_大小*) = 5632

**PictureDestinationRect**的成员[ **DXVA\_BlendCombination** ](https://msdn.microsoft.com/library/windows/hardware/ff563120)结构定义使用的两个备用目标矩形以下值：

1.  一个具有以下值的目标矩形：
    -   **left** = 8
    -   **右** = **左**+ (2 X*水平\_大小*) = 712

2.  一个具有以下值的目标矩形：
    -   **left** = 0
    -   **右**= left + (2 倍*水平\_大小*) = 704

在第二种情况下，该矩形为由**GraphicDestinationRect** DXVA 成员\_BlendCombination 结构移置开左侧的八个补偿移动的图片目标

以下两个替代方法的第二部分创建用于显示的目标区域。

 

 





