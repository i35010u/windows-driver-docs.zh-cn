---
title: 支持单像素宽度反锯齿线条
description: 支持单像素宽度反锯齿线条
keywords:
- 单像素宽线条 WDK DirectX 9。0
- 别名单像素宽线条 WDK DirectX 9。0
- 消除锯齿单像素宽线条 WDK DirectX 9。0
- 线条抗锯齿-WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 596625440281131897284960347f9ed7cc197c2c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838983"
---
# <a name="supporting-single-pixel-wide-antialiased-lines"></a>支持单像素宽度反锯齿线条


## <span id="ddk_supporting_single_pixel_wide_antialiased_lines_gg"></span><span id="DDK_SUPPORTING_SINGLE_PIXEL_WIDE_ANTIALIASED_LINES_GG"></span>


DirectX 9.0 版本驱动程序可以支持单像素宽的行，这些行可能是别名或消除锯齿。 该驱动程序通过 \_ 在 D3DCAPS9 结构的 **LineCaps** 成员中设置 D3DLINECAPS 消除锯齿功能位，指示消除了支持。 驱动程序将返回 D3DCAPS9 结构，以响应 **GetDriverInfo2** 查询，如 [报告 DirectX 8.0 Style Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述的那样返回 D3DCAPS8 结构。 支持 [GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。

若要启用行抗锯齿功能，驱动程序将接收 \_ 其 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数的 [命令流](command-stream.md)中的 D3DDP2OP RENDERSTATE 操作代码。 驱动程序处理 \_ 与此操作代码关联的 [**D3DHAL \_ DP2RENDERSTATE**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)结构的 **RenderState** 成员的 D3DRS ANTIALIASEDLINEENABLE 呈现状态。 驱动程序确定是启用还是禁用 D3DHAL DP2RENDERSTATE 的 **dwState** 成员中的布尔值的行抗锯齿 \_ 。 如果值为 **TRUE，则** 表示启用， **FALSE** 表示禁用。 默认情况下，此呈现状态值设置为 **FALSE**。

D3DRS \_ ANTIALIASEDLINEENABLE render 状态适用于在线框模式下绘制的三角形以及线条绘制基元类型。

在呈现为多示例呈现器目标时，驱动程序必须忽略请求以启用行抗锯齿，并呈现所有化名为别名的行。

 

