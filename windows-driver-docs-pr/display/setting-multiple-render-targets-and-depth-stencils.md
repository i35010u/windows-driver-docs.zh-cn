---
title: 设置多个渲染器目标和深度模具
description: 设置多个渲染器目标和深度模具
keywords:
- 呈现目标 WDK DirectX 9.0，多个
- 多个呈现目标 WDK DirectX 9。0
- 深度模具 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 043a57a1e88d3b9772d200249639ba0e3a8b2c0f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826607"
---
# <a name="setting-multiple-render-targets-and-depth-stencils"></a>设置多个渲染器目标和深度模具


## <span id="ddk_setting_multiple_render_targets_and_depth_stencils_gg"></span><span id="DDK_SETTING_MULTIPLE_RENDER_TARGETS_AND_DEPTH_STENCILS_GG"></span>


DirectX 9.0 版本驱动程序必须处理 \_ \_ 其 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 函数中的 D3DDP2OP SETRENDERTARGET2 和 D3DDP2OP SETDEPTHSTENCIL 操作代码，即使该驱动程序不支持 [同时呈现到多个目标](rendering-to-multiple-targets-simultaneously.md)。 [**D3DHAL \_DP2SETRENDERTARGET2**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setrendertarget2) 和 [**D3DHAL \_ DP2SETDEPTHSTENCIL**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setdepthstencil) 结构分别遵循 [命令流](command-stream.md)中的这些代码。

 

