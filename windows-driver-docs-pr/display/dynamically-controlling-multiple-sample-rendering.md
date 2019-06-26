---
title: 动态控制多重采样渲染
description: 动态控制多重采样渲染
ms.assetid: cd0bea22-29e8-40f7-987b-5c36765e5677
keywords:
- 多个示例呈现 WDK DirectX 9.0 中，动态控件
- 呈现 multisamples WDK DirectX 9.0 中，动态控件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 913def1d2ce1981a8d695e7e9d508d199a9c83da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383104"
---
# <a name="dynamically-controlling-multiple-sample-rendering"></a>动态控制多重采样渲染


## <span id="ddk_dynamically_controlling_multiple_sample_rendering_gg"></span><span id="DDK_DYNAMICALLY_CONTROLLING_MULTIPLE_SAMPLE_RENDERING_GG"></span>


DirectX 9.0 版本驱动程序支持的功能或者启用和禁用多个示例之间的基元呈现的呈现。 若要报告的驱动程序的设备支持此功能，该驱动程序设置 D3DPRASTERCAPS\_MULTISAMPLE\_切换功能位**RasterCaps** D3DCAPS9 结构中的成员。 该驱动程序在响应中返回 D3DCAPS9 结构**GetDriverInfo2**查询类似于如何返回 D3DCAPS8 结构，如中所述[报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 此查询的支持中所述[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

若要切换多个示例呈现打开和关闭之间开始场景和最终场景状态，该驱动程序收到 D3DDP2OP\_RENDERSTATE 操作代码中[命令流](command-stream.md)的其[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数。 该驱动程序处理 D3DRS\_MULTISAMPLEANTIALIAS 呈现中的状态**RenderState**的成员[ **D3DHAL\_DP2RENDERSTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)结构，它是与此操作代码相关联。 该驱动程序确定是否要启用或禁用多个示例中的布尔值的呈现**dwState** D3DHAL 成员\_DP2RENDERSTATE。 该值 **，则返回 TRUE**意味着若要启用并**FALSE**意味着若要禁用。

如果 D3DPRASTERCAPS\_MULTISAMPLE\_切换功能位将设置、 驱动程序可以接收 D3DRS\_MULTISAMPLEANTIALIAS 呈现状态之间 D3DRENDERSTATE\_SCENECAPTURE 呈现指定的状态 **，则返回 TRUE**开始场景的信息并**FALSE**最终场景的信息。

 

 





