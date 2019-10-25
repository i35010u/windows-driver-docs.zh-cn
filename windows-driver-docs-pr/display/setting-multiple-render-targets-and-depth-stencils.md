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
ms.openlocfilehash: d50c7aeddb97ce5a3ea3ca4d293592e658604db2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825811"
---
# <a name="setting-multiple-render-targets-and-depth-stencils"></a>设置多个渲染器目标和深度模具


## <span id="ddk_setting_multiple_render_targets_and_depth_stencils_gg"></span><span id="DDK_SETTING_MULTIPLE_RENDER_TARGETS_AND_DEPTH_STENCILS_GG"></span>


DirectX 9.0 版本驱动程序必须在其[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数中处理 D3DDP2OP\_SETRENDERTARGET2 和 D3DDP2OP\_SETDEPTHSTENCIL 操作代码，即使该驱动程序不支持[同时呈现到多个目标](rendering-to-multiple-targets-simultaneously.md). [**D3DHAL\_DP2SETRENDERTARGET2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setrendertarget2)和[**D3DHAL\_DP2SETDEPTHSTENCIL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setdepthstencil)结构分别遵循[命令流](command-stream.md)中的这些代码。

 

 





