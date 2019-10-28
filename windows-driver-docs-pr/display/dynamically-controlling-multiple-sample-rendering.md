---
title: 动态控制多重采样渲染
description: 动态控制多重采样渲染
ms.assetid: cd0bea22-29e8-40f7-987b-5c36765e5677
keywords:
- 多示例渲染 WDK DirectX 9.0，动态控制
- 呈现 multisamples WDK DirectX 9.0，动态控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7513bd1e01dc6f5599a13319264550f65ca430d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839710"
---
# <a name="dynamically-controlling-multiple-sample-rendering"></a>动态控制多重采样渲染


## <span id="ddk_dynamically_controlling_multiple_sample_rendering_gg"></span><span id="DDK_DYNAMICALLY_CONTROLLING_MULTIPLE_SAMPLE_RENDERING_GG"></span>


DirectX 9.0 版本驱动程序可以支持在呈现基元之间交替启用和禁用多样本呈现功能。 为了报告驱动程序的设备是否支持此功能，驱动程序在 D3DCAPS9 结构的**RasterCaps**成员中设置 D3DPRASTERCAPS\_多级采样\_切换功能位。 驱动程序将返回 D3DCAPS9 结构，以响应**GetDriverInfo2**查询，如[报告 DirectX 8.0 Style Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述的那样返回 D3DCAPS8 结构。 支持[GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。

若要在开始场景状态和结束场景状态之间切换打开和关闭多样本渲染，驱动程序会在其[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数的[命令流](command-stream.md)中接收 D3DDP2OP\_RENDERSTATE 操作代码。 驱动程序处理与此操作代码关联的[**D3DHAL\_DP2RENDERSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)结构的**RENDERSTATE**成员的 D3DRS\_MULTISAMPLEANTIALIAS 呈现状态。 驱动程序确定是要启用还是禁用从 D3DHAL\_DP2RENDERSTATE 的**dwState**成员中的布尔值进行的多示例呈现。 如果值为**TRUE，则**表示启用， **FALSE**表示禁用。

如果设置了 D3DPRASTERCAPS\_多级\_切换功能位，则驱动程序可以接收 D3DRENDERSTATE\_SCENECAPTURE 呈现状态之间的 D3DRS\_MULTISAMPLEANTIALIAS 呈现状态，该状态**将指定为**开始-场景信息和**FALSE**表示最终场景信息。

 

 





