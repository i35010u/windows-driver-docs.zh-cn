---
title: 支持单像素宽度反锯齿线条
description: 支持单像素宽度反锯齿线条
ms.assetid: f1e0df18-25d8-4ebd-b920-5cfbe5acf096
keywords:
- 单像素宽行 WDK DirectX 9.0
- 别名单像素宽行 WDK DirectX 9.0
- 消除锯齿单个像素宽行 WDK DirectX 9.0
- 行抗锯齿 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0519b825c24134f49a3f910cd9ac0a99bc987329
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361237"
---
# <a name="supporting-single-pixel-wide-antialiased-lines"></a>支持单像素宽度反锯齿线条


## <span id="ddk_supporting_single_pixel_wide_antialiased_lines_gg"></span><span id="DDK_SUPPORTING_SINGLE_PIXEL_WIDE_ANTIALIASED_LINES_GG"></span>


DirectX 9.0 版本驱动程序支持单个像素宽行别名或消除锯齿的。 该驱动程序通过设置 D3DLINECAPS 来指示消除锯齿的支持\_消除锯齿功能位**LineCaps** D3DCAPS9 结构中的成员。 该驱动程序在响应中返回 D3DCAPS9 结构**GetDriverInfo2**查询类似于如何返回 D3DCAPS8 结构，如中所述[报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 此查询的支持中所述[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

若要启用行抗锯齿功能，该驱动程序收到 D3DDP2OP\_RENDERSTATE 操作代码中[命令流](command-stream.md)的其[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数。 该驱动程序处理 D3DRS\_ANTIALIASEDLINEENABLE 呈现中的状态**RenderState**的成员[ **D3DHAL\_DP2RENDERSTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)结构，它是与此操作代码相关联。 该驱动程序确定是否要启用或禁用行中的布尔值的抗锯齿**dwState** D3DHAL 成员\_DP2RENDERSTATE。 该值 **，则返回 TRUE**意味着若要启用并**FALSE**意味着若要禁用。 默认情况下，此呈现器状态的值设置为**FALSE**。

D3DRS\_ANTIALIASEDLINEENABLE 呈现状态适用于绘制透明框架模式，以及线条图形基元类型中的三角形。

在呈现到多个示例呈现器目标，该驱动程序必须忽略启用行抗锯齿和呈现所有行使用别名的请求。

 

 





