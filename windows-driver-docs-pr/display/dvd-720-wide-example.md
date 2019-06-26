---
title: DVD 720 像素宽度示例
description: DVD 720 像素宽度示例
ms.assetid: 02761bf5-afae-4f38-9178-6a721fcad84e
keywords:
- alpha 混合组合 WDK DirectX VA，DVD 720 范围示例
- 混合型的图片 WDK DirectX VA，DVD 720 范围示例
- DVD 720 范围示例 WDK DirectX VA
- 720 范围示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cb407c8b9227735aa09b56bfb795e181c77b638
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380231"
---
# <a name="dvd-720-wide-example"></a>DVD 720 像素宽度示例


## <span id="ddk_dvd_720_wide_example_gg"></span><span id="DDK_DVD_720_WIDE_EXAMPLE_GG"></span>


使用 DVD 上的 mpeg-2 720 范围图片使用图片源矩形值指定的**PictureSourceRect16thPel**的成员[ **DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_blendcombination)结构 （在六分之一亮度示例间距分辨率的） 使用以下值：

-   **left** = 0

-   **右** = **左**+ (16 X*水平\_大小*) = 11520

通常情况下，使用以下目标矩形值：

-   **left** = 0

-   **right** = **left** + *horizontal\_size* = 720

 

 





