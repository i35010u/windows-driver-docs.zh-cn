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
ms.openlocfilehash: e0b65a37d0bf0134105190c7a20925230b3527a3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390448"
---
# <a name="setting-multiple-render-targets-and-depth-stencils"></a>设置多个渲染器目标和深度模具


## <span id="ddk_setting_multiple_render_targets_and_depth_stencils_gg"></span><span id="DDK_SETTING_MULTIPLE_RENDER_TARGETS_AND_DEPTH_STENCILS_GG"></span>


DirectX 9.0 版本驱动程序必须处理 D3DDP2OP\_SETRENDERTARGET2 和 D3DDP2OP\_SETDEPTHSTENCIL 操作代码中其[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)函数，即使它不支持[多个目标上呈现，同时](rendering-to-multiple-targets-simultaneously.md)。 [**D3DHAL\_DP2SETRENDERTARGET2** ](https://msdn.microsoft.com/library/windows/hardware/ff545785)并[ **D3DHAL\_DP2SETDEPTHSTENCIL** ](https://msdn.microsoft.com/library/windows/hardware/ff545724)结构分别执行这些代码在[命令流](command-stream.md)。

 

 





