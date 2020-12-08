---
title: 多个渲染器目标的可选功能
description: 多个渲染器目标的可选功能
keywords:
- 呈现多个目标 WDK DirectX 9.0，可选功能
- 多个呈现目标 WDK DirectX 9.0，可选功能
- 同时呈现目标 WDK DirectX 9.0，可选功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d60171c329a70635dbbe4682315fa9bf4a123e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803573"
---
# <a name="optional-features-for-multiple-render-targets"></a>多个渲染器目标的可选功能


## <span id="ddk_optional_features_for_multiple_render_targets_gg"></span><span id="DDK_OPTIONAL_FEATURES_FOR_MULTIPLE_RENDER_TARGETS_GG"></span>


支持同时呈现到多个目标的 DirectX 9.0 版本驱动程序可以支持扩展功能。 如果驱动程序支持这些扩展功能，则它必须通过在 D3DCAPS9 结构的 **PrimitiveMiscCaps** 成员中报告功能位来指出此类支持。 该驱动程序可以支持以下扩展功能：

-   为多呈现器目标组中的呈现器目标设置独立位深度。 呈现目标可以具有不同的格式;但是，除非支持此功能，否则呈现器目标必须具有相同的位深度。 \_必须设置 D3DPMISCCAPS MRTINDEPENDENTBITDEPTHS 功能位以指示支持独立位深度。

-   执行操作-除了 z 和模具测试外，还会在像素着色器操作后在多个呈现器目标组中执行呈现目标。 例如，除非支持此功能，否则在执行像素着色器操作之后，驱动程序不能仿色、alpha 测试、应用雾化、混合或执行光栅操作。 D3DPMISCCAPS \_ MRTPOSTPIXELSHADERBLENDING 功能位必须设置为指示支持 postpixel 着色器操作。

    如果设置了 D3DPMISCCAPS \_ MRTPOSTPIXELSHADERBLENDING，则显示设备必须将以下状态应用到同时呈现的所有呈现器目标：

    -   Alpha blend。 设置 oCi 以使颜色值与第 i 个呈现器目标混合。
    -   Alpha 测试。 将 oC0 设置为进行比较;如果比较失败，将取消所有呈现器目标的像素。
    -   雾化. 将雾化应用于呈现目标 0;其他呈现目标未定义。 驱动程序可以使用相同的状态对所有呈现目标应用雾化。
    -   递. 未定义。
-   \_为多呈现器目标组中的呈现目标 (D3DRS COLORWRITEENABLE) 应用独立的颜色写入掩码。 \_必须设置 D3DPMISCCAPS INDEPENDENTWRITEMASKS 功能位以指示支持独立的颜色写入掩码。 如果 \_ 设置了 D3DPMISCCAPS INDEPENDENTWRITEMASKS，则独立的颜色写入掩码的可用数目等于) D3DCAPS9 结构的 **NumSimultaneousRTs** 成员的多个呈现器目标 (组中的呈现器目标的最大数目。

请注意，支持像素着色器版本3.0 和更高版本的显示设备的驱动程序必须指示它支持多个呈现器目标的扩展功能。 有关详细信息，请参阅 [Shader 3 支持的报告功能](reporting-capabilities-for-shader-3-support.md)。

 

 





