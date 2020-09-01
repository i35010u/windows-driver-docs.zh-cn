---
title: 渲染目标要求
description: 渲染目标要求
ms.assetid: 4d16819e-f209-44df-b5af-f3ff9cae256b
keywords:
- 呈现目标 WDK Direct3D
- 颜色缓冲区 WDK Direct3D
- 缓冲 WDK Direct3D
- 深度缓冲 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb6f59a0441320f14a1b0c8f5c2cdd9fa6b33894
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066406"
---
# <a name="render-target-requirements"></a>渲染目标要求


## <span id="ddk_render_target_requirements_gg"></span><span id="DDK_RENDER_TARGET_REQUIREMENTS_GG"></span>


颜色缓冲区和深度缓冲区的要求如下：

### <a name="span-idcolor_buffersspanspan-idcolor_buffersspancolor-buffers"></a><span id="color_buffers"></span><span id="COLOR_BUFFERS"></span>颜色缓冲区

如果硬件不支持还将用作纹理的呈现目标 (也就是说，设备无法 "呈现为纹理" ) ，则设备必须无法对 **IDirect3DDevice7：： SetRenderTarget** 和 **IDirect3D7：： CreateDevice** 方法进行调用。 Direct3D SDK 文档中介绍了这些方法。 呈现目标要用作纹理的事实是， \_ 在表面说明中存在 DDSCAPS 纹理标志 (参见[**DDSCAPS**](/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))结构) 的**dwCaps**成员。

### <a name="span-iddepth_buffersspanspan-iddepth_buffersspandepth-buffers"></a><span id="depth_buffers"></span><span id="DEPTH_BUFFERS"></span>深度缓冲区

如果硬件不支持呈现目标和深度缓冲区的特定组合，则在检测到此类不匹配（例如，在调用 **IDirect3D7：： CreateDevice** 和 **IDirectDrawSurface7：： AddAttachedSurface** 方法）的情况下，设备必须失败导致此情况的 API 调用失败。 Direct3D 和 DirectDraw SDK 文档集中分别介绍了这些方法。 这种不匹配的一个示例可能是呈现目标和深度缓冲区的深度不同。 不要以透明方式更改呈现器目标或深度缓冲区的格式，以使无效的组合能够正常工作。 改为在不通知 DirectX 运行时的情况下分配较高精度的深度缓冲区。

 

