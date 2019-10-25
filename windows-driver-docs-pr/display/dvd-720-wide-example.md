---
title: DVD 720 像素宽度示例
description: DVD 720 像素宽度示例
ms.assetid: 02761bf5-afae-4f38-9178-6a721fcad84e
keywords:
- alpha-blend 组合 WDK DirectX VA，DVD 720-范围示例
- 混合图片 WDK DirectX VA，DVD 720-范围示例
- DVD 720-范围示例 WDK DirectX VA
- 720-内部示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75ca20241b9588a4a0a4fa1361487628cce21853
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838978"
---
# <a name="dvd-720-wide-example"></a>DVD 720 像素宽度示例


## <span id="ddk_dvd_720_wide_example_gg"></span><span id="DDK_DVD_720_WIDE_EXAMPLE_GG"></span>


使用带720宽度照片的 DVD 上的 MPEG-2 使用由[**DXVA\_BlendCombination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的**PictureSourceRect16thPel**成员指定的图片源矩形值（采用亮度样本间距的一-第16位）解决方法）：

-   **left** = 0

-   **right** = **left** + （16 X*水平\_大小*） = 11520

通常，使用下列目标矩形值：

-   **left** = 0

-   **right** = **左** + *水平\_大小*= 720

 

 





