---
title: DVD 16 9 黑边 Height in 4 3 示例
description: DVD 16 9 黑边 Height in 4 3 示例
keywords:
- alpha-blend 组合 WDK DirectX VA，DVD 16 9 黑边 height 示例
- 混合图片 WDK DirectX VA，DVD 16 9 黑边高度示例
- DVD 16 9 黑边 height
- 16 9 黑边高度示例 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b7b569ccc40070936a6ad5e5a9ad5bd45bc446d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809113"
---
# <a name="dvd-169-letterbox-height-in-43-example"></a>4:3 画面中的 DVD 16:9 宽屏幕高度示例


## <span id="ddk_dvd_16_9_letterbox_height_in_4_3_example_gg"></span><span id="DDK_DVD_16_9_LETTERBOX_HEIGHT_IN_4_3_EXAMPLE_GG"></span>


对于黑边组帧，使用适用于4:3 的16:9 视频对于源和目标图片具有以下值。

以下矩形值用于源图片的 [**DXVA \_ BlendCombination**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的 **PictureSourceRect16thPel** 成员中：

-   **top** = 0

-   **下**  = **top** + (16 X *垂直 \_ 大小*) = 7680 或9216

以下矩形值用于目标图片的 [**DXVA \_ BlendCombination**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)结构的 **PictureDestinationRect** 成员中：

-   **顶部**  = *垂直 \_ 大小*/8 = 60 或72

-   **底端** = 7 X *垂直 \_ 大小* /8 = 420 或504

 

