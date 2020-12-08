---
title: 为视频处理创建渲染目标图面
description: 为视频处理创建渲染目标图面
keywords:
- 视频处理 WDK DirectX VA，呈现目标图面
- 呈现目标面 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1580ff987cb19b44b2de7fbcd4a14b49eccdc49
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834611"
---
# <a name="creating-a-render-target-surface-for-video-processing"></a>为视频处理创建渲染目标图面


Microsoft Direct3D runtime 调用用户模式显示驱动程序的 [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource) 函数来创建用于视频处理的呈现目标图面。 用户模式显示驱动程序确定它应创建用于视频处理的渲染目标图面，使其在 **CREATERESOURCE** 的 *PResource* 参数的 [**D3DDDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的 **Flags** 成员中存在 **VideoProcessRenderTarget** 位域标志。 用户模式显示驱动程序可以将此呈现目标用于视频处理，但不一定要用于三维。 用户模式显示驱动程序可以对常规 RGB 三维呈现器目标表面执行视频处理。 但是，用户模式显示驱动程序通常会输出到 YUV 格式，而3-d 硬件无法将这些格式支持为呈现器目标。

下面是驱动程序应支持的只是视频处理的有效渲染目标的表面类型：

-   用 **VideoProcessRenderTarget** 位域标志创建的 RGB 或 YUV 面。

-   用 **RenderTarget** 位域标志创建的 RGB 图面。

-   用 **RenderTarget** 和 **纹理** 位域标志创建的 RGB 纹理。

 

