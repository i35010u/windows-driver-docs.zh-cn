---
title: DVD 720 范围示例
description: DVD 720 范围示例
ms.assetid: 02761bf5-afae-4f38-9178-6a721fcad84e
keywords:
- alpha 混合组合 WDK DirectX VA，DVD 720 范围示例
- 混合型的图片 WDK DirectX VA，DVD 720 范围示例
- DVD 720 范围示例 WDK DirectX VA
- 720 范围示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77e102ece3b39d64aea00ce195f064f4a79166df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554456"
---
# <a name="dvd-720-wide-example"></a>DVD 720 范围示例


## <span id="ddk_dvd_720_wide_example_gg"></span><span id="DDK_DVD_720_WIDE_EXAMPLE_GG"></span>


使用 DVD 上的 mpeg-2 720 范围图片使用图片源矩形值指定的**PictureSourceRect16thPel**的成员[ **DXVA\_BlendCombination**](https://msdn.microsoft.com/library/windows/hardware/ff563120)结构 （在六分之一亮度示例间距分辨率的） 使用以下值：

-   **left** = 0

-   **右** = **左**+ (16 X*水平\_大小*) = 11520

通常情况下，使用以下目标矩形值：

-   **left** = 0

-   **right** = **left** + *horizontal\_size* = 720

 

 





