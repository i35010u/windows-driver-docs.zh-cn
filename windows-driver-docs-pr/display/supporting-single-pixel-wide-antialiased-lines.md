---
title: 支持单像素宽度反锯齿线条
description: 支持单像素宽度反锯齿线条
ms.assetid: f1e0df18-25d8-4ebd-b920-5cfbe5acf096
keywords:
- 单像素宽线条 WDK DirectX 9。0
- 别名单像素宽线条 WDK DirectX 9。0
- 消除锯齿单像素宽线条 WDK DirectX 9。0
- 线条抗锯齿-WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11570ccc8f296be57ca8efe8575fef44f11329b5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825600"
---
# <a name="supporting-single-pixel-wide-antialiased-lines"></a>支持单像素宽度反锯齿线条


## <span id="ddk_supporting_single_pixel_wide_antialiased_lines_gg"></span><span id="DDK_SUPPORTING_SINGLE_PIXEL_WIDE_ANTIALIASED_LINES_GG"></span>


DirectX 9.0 版本驱动程序可以支持单像素宽的行，这些行可能是别名或消除锯齿。 该驱动程序通过在 D3DCAPS9 结构的**LineCaps**成员中设置 D3DLINECAPS\_消除锯齿功能位来指示消除了支持。 驱动程序将返回 D3DCAPS9 结构，以响应**GetDriverInfo2**查询，如[报告 DirectX 8.0 Style Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述的那样返回 D3DCAPS8 结构。 支持[GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。

若要启用行抗锯齿，驱动程序将接收其[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数的[命令流](command-stream.md)中的 D3DDP2OP\_RENDERSTATE 操作代码。 驱动程序处理与此操作代码关联的[**D3DHAL\_DP2RENDERSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)结构的**RENDERSTATE**成员的 D3DRS\_ANTIALIASEDLINEENABLE 呈现状态。 驱动程序确定是启用还是禁用 D3DHAL\_DP2RENDERSTATE 的**dwState**成员中的布尔值的行抗锯齿。 如果值为**TRUE，则**表示启用， **FALSE**表示禁用。 默认情况下，此呈现状态值设置为**FALSE**。

D3DRS\_ANTIALIASEDLINEENABLE 渲染状态适用于在线框模式下绘制的三角形以及线条绘制基元类型。

在呈现为多示例呈现器目标时，驱动程序必须忽略请求以启用行抗锯齿，并呈现所有化名为别名的行。

 

 





