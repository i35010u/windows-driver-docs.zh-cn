---
title: 设置多个渲染器目标和深度模具
description: 设置多个渲染器目标和深度模具
ms.assetid: 98acd448-0b65-4a3a-9e95-8e753729a7d7
keywords:
- 呈现目标 WDK DirectX 9.0，多个
- 多个呈现目标 WDK DirectX 9。0
- 深度模具 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adf1296028e2f553eb872c54171e813c5d409c3e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066644"
---
# <a name="setting-multiple-render-targets-and-depth-stencils"></a>设置多个渲染器目标和深度模具


## <span id="ddk_setting_multiple_render_targets_and_depth_stencils_gg"></span><span id="DDK_SETTING_MULTIPLE_RENDER_TARGETS_AND_DEPTH_STENCILS_GG"></span>


DirectX 9.0 版本驱动程序必须处理 \_ \_ 其 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 函数中的 D3DDP2OP SETRENDERTARGET2 和 D3DDP2OP SETDEPTHSTENCIL 操作代码，即使该驱动程序不支持 [同时呈现到多个目标](rendering-to-multiple-targets-simultaneously.md)。 [**D3DHAL \_DP2SETRENDERTARGET2**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setrendertarget2) 和 [**D3DHAL \_ DP2SETDEPTHSTENCIL**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setdepthstencil) 结构分别遵循 [命令流](command-stream.md)中的这些代码。

 

