---
title: 动态控制多重采样渲染
description: 动态控制多重采样渲染
ms.assetid: cd0bea22-29e8-40f7-987b-5c36765e5677
keywords:
- 多示例渲染 WDK DirectX 9.0，动态控制
- 呈现 multisamples WDK DirectX 9.0，动态控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8013b9bc21aaa73aa667b090255081c04605f09d
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065878"
---
# <a name="dynamically-controlling-multiple-sample-rendering"></a>动态控制多重采样渲染


## <span id="ddk_dynamically_controlling_multiple_sample_rendering_gg"></span><span id="DDK_DYNAMICALLY_CONTROLLING_MULTIPLE_SAMPLE_RENDERING_GG"></span>


DirectX 9.0 版本驱动程序可以支持在呈现基元之间交替启用和禁用多样本呈现功能。 若要报告驱动程序的设备是否支持此功能，驱动程序将在 \_ \_ D3DCAPS9 结构的 **RasterCaps** 成员中设置 D3DPRASTERCAPS 的多级的切换功能位。 驱动程序将返回 D3DCAPS9 结构，以响应 **GetDriverInfo2** 查询，如 [报告 DirectX 8.0 Style Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述的那样返回 D3DCAPS8 结构。 支持 [GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。

若要在开始场景状态和结束场景状态之间切换和禁用多样本渲染，驱动程序将接收 \_ 其[**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数的[命令流](command-stream.md)中的 D3DDP2OP RENDERSTATE 操作代码。 驱动程序处理 \_ 与此操作代码关联的[**D3DHAL \_ DP2RENDERSTATE**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)结构的**RenderState**成员的 D3DRS MULTISAMPLEANTIALIAS 呈现状态。 驱动程序确定是在 D3DHAL DP2RENDERSTATE 的 **dwState** 成员中启用还是禁用多样本呈现 \_ 。 如果值为 **TRUE，则** 表示启用， **FALSE** 表示禁用。

如果设置了 D3DPRASTERCAPS 的 \_ 多级显示 \_ 切换功能位，则驱动程序可以接收 \_ D3DRENDERSTATE SCENECAPTURE 呈现状态之间的 D3DRS MULTISAMPLEANTIALIAS 呈现状态，这些状态将 \_ 为开始-场景信息指定 **TRUE** ，对结束场景信息指定 **FALSE** 。

 

