---
title: 多个渲染器目标的可选功能
description: 多个渲染器目标的可选功能
ms.assetid: 265df4d3-acc9-4978-97d1-a6f81bc7afaf
keywords:
- 呈现多个目标 WDK DirectX 9.0 中，可选功能
- 多个呈现器目标 WDK DirectX 9.0 中，可选功能
- 同时呈现器目标 WDK DirectX 9.0 中，可选功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d4919bf071b256753a16a3f85f946fe03752ae8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379843"
---
# <a name="optional-features-for-multiple-render-targets"></a>多个渲染器目标的可选功能


## <span id="ddk_optional_features_for_multiple_render_targets_gg"></span><span id="DDK_OPTIONAL_FEATURES_FOR_MULTIPLE_RENDER_TARGETS_GG"></span>


DirectX 9.0 版驱动程序支持多个目标上呈现，同时可以支持扩展的功能。 如果该驱动程序支持这些扩展功能，则必须通过报告功能中的位表示此类支持**PrimitiveMiscCaps** D3DCAPS9 结构中的成员。 该驱动程序可以支持以下扩展功能：

-   设置多个的呈现器目标组中的呈现器目标的独立位深度。 呈现器目标可以具有不同的格式;但是，除非支持此功能，呈现器目标必须具有相同的位深度。 D3DPMISCCAPS\_MRTINDEPENDENTBITDEPTHS 功能位必须设置为指示对独立位深度的支持。

-   像素着色器操作后，对多个呈现器目标组中的呈现器目标上执行操作-z 和模具测试-以外。 例如，支持此功能，除非该驱动程序不能抖动，alpha 测试应用雾，blend，或在像素着色器操作之后执行光栅操作。 D3DPMISCCAPS\_MRTPOSTPIXELSHADERBLENDING 功能位必须设置以指示对 postpixel 着色器操作的支持。

    如果 D3DPMISCCAPS\_MRTPOSTPIXELSHADERBLENDING 设置，显示设备必须应用于所有呈现器目标的同时呈现以下状态：

    -   Alpha 混合。 设置 oCi 导致要第 i 个呈现器目标与混合的颜色值。
    -   Alpha 测试。 设置用于比较发生; oC0如果比较失败，则取消所有呈现器目标像素。
    -   雾。 应用雾呈现目标 0;其他呈现器目标不确定。 该驱动程序可以应用于使用相同的状态的所有呈现器目标雾。
    -   抖动。 未定义。
-   应用独立颜色写掩码 (D3DRS\_COLORWRITEENABLE) 在多个目标的呈现器呈现目标组。 D3DPMISCCAPS\_INDEPENDENTWRITEMASKS 功能位必须设置为指示对独立的颜色写掩码的支持。 如果 D3DPMISCCAPS\_INDEPENDENTWRITEMASKS 设置，则可用的独立颜色写掩码数等于在多个呈现器目标组中呈现器目标的最大数目 ( **NumSimultaneousRTs**D3DCAPS9 结构的成员）。

请注意，用于支持像素着色器版本 3.0 及更高版本的显示设备的驱动程序必须指示它为多个呈现器目标支持的扩展的功能。 有关详细信息，请参阅[着色器 3 支持报告功能](reporting-capabilities-for-shader-3-support.md)。

 

 





