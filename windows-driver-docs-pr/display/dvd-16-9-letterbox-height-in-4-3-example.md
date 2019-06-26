---
title: DVD 16 9 Letterbox 高度以 4 3 示例
description: DVD 16 9 Letterbox 高度以 4 3 示例
ms.assetid: 67e5e50e-5102-4392-9430-feddc9609f2e
keywords:
- alpha 混合组合 WDK DirectX VA，DVD 16 9 letterbox 高度示例
- 混合型的图片 WDK DirectX VA，DVD 16 9 letterbox 高度示例
- DVD 16 9 letterbox 高度示例 WDK DirectX VA
- 16 9 letterbox 高度示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8edc81940eaef842772bac0e45bcee38c51de915
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355232"
---
# <a name="dvd-169-letterbox-height-in-43-example"></a>4:3 画面中的 DVD 16:9 宽屏幕高度示例


## <span id="ddk_dvd_16_9_letterbox_height_in_4_3_example_gg"></span><span id="DDK_DVD_16_9_LETTERBOX_HEIGHT_IN_4_3_EXAMPLE_GG"></span>


用于的 16:9 视频 DVD 的 letterbox 组帧 4:3 显示具有以下值的源和目标的图片。

在使用以下的矩形值**PictureSourceRect16thPel**的成员[ **DXVA\_BlendCombination** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_blendcombination)源的结构图片：

-   **top** = 0

-   **底部** = **顶部**+ (16 X*垂直\_大小*) = 7680 或 9216

在使用以下的矩形值**PictureDestinationRect**的成员[ **DXVA\_BlendCombination** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_blendcombination)结构为目标图片：

-   **顶部** = *垂直\_大小*/ 8 = 60 或 72

-   **底部**= 7 X*垂直\_大小*/ 8 = 420 或 504

 

 





