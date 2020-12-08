---
title: DVD 720 像素宽度示例
description: DVD 720 像素宽度示例
keywords:
- alpha-blend 组合 WDK DirectX VA，DVD 720-范围示例
- 混合图片 WDK DirectX VA，DVD 720-范围示例
- DVD 720-范围示例 WDK DirectX VA
- 720-内部示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 203b159f01425a3b9e95074aa982e3de184eff93
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809105"
---
# <a name="dvd-720-wide-example"></a>DVD 720 像素宽度示例


## <span id="ddk_dvd_720_wide_example_gg"></span><span id="DDK_DVD_720_WIDE_EXAMPLE_GG"></span>


使用带720宽度的 DVD 中的 MPEG-2 的图片使用由 [**DXVA \_ BlendCombination**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的 **PictureSourceRect16thPel** 成员指定的图片源矩形值 (的亮度样本间距解析) 的第一十六个值：

-   **left** = 0

-   **向右**  = **左**+ (16 X *水平 \_ 大小*) = 11520

通常，使用下列目标矩形值：

-   **left** = 0

-   **向右**  = **左**  + *水平 \_ 大小*= 720

 

