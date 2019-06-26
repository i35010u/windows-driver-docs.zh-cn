---
title: 设置多个渲染器目标和深度模具
description: 设置多个渲染器目标和深度模具
ms.assetid: 98acd448-0b65-4a3a-9e95-8e753729a7d7
keywords:
- 呈现器目标 WDK DirectX 9.0 中，多个
- 多个呈现器目标 WDK DirectX 9.0
- 深度模具 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c40ad3691dc2d992b14c7bd064a33fe9c66b4e7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365564"
---
# <a name="setting-multiple-render-targets-and-depth-stencils"></a>设置多个渲染器目标和深度模具


## <span id="ddk_setting_multiple_render_targets_and_depth_stencils_gg"></span><span id="DDK_SETTING_MULTIPLE_RENDER_TARGETS_AND_DEPTH_STENCILS_GG"></span>


DirectX 9.0 版本驱动程序必须处理 D3DDP2OP\_SETRENDERTARGET2 和 D3DDP2OP\_SETDEPTHSTENCIL 操作代码中其[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数，即使它不支持[多个目标上呈现，同时](rendering-to-multiple-targets-simultaneously.md)。 [**D3DHAL\_DP2SETRENDERTARGET2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2setrendertarget2)并[ **D3DHAL\_DP2SETDEPTHSTENCIL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2setdepthstencil)结构分别执行这些代码在[命令流](command-stream.md)。

 

 





