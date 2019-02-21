---
title: 通过 StretchBlt 多重采样支持
description: 通过 StretchBlt 多重采样支持
ms.assetid: c829c612-d09d-4a33-a117-e50b9ed57251
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，呈现，multisample StretchBlt
- 多重采样呈现 WDK DirectX 8.0 StretchBlt
- 呈现 multisamples WDK DirectX 8.0，StretchBlt
- 拉伸位块操作 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b43d65a06e4bf45f3830e13b3bdd789fef8f41a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544268"
---
# <a name="multisample-support-through-stretchblt"></a>通过 StretchBlt 多重采样支持


## <span id="ddk_multisample_support_through_stretchblt_gg"></span><span id="DDK_MULTISAMPLE_SUPPORT_THROUGH_STRETCHBLT_GG"></span>


尽管不建议使用的机制支持多重采样，驱动程序可以通过呈现到大型的后台缓冲区来实现多级取样支持和执行为拉伸 blt 以对大型后重新抽样缓冲区为主低的分辨率。 但是，如果这是所依据的驱动程序支持多重采样的机制，该驱动程序必须设置的新功能位 D3DPRASTERCAPS\_中的 STRETCHBLTMULTISAMPLE **RasterCaps** D3D8CAPS 结构中的成员。 D3DCAPS8 的说明，请参阅 DirectX 8.0 SDK 文档。

当驱动程序设置 D3DPRASTERCAPS\_STRETCHBLTMULTISAMPLE 位，则表明它：

-   无法完成请求从应用程序启用和禁用完整场景抗锯齿而呈现相同的场景。 即，它将失败请求，以启用和禁用**BOOL** D3DRS 值\_MULTISAMPLEANTIALIAS 设备呈现在一个场景的呈现过程的状态 (D3DRENDERSTATETYPE)。 请注意，若要更改的请求**BOOL** D3DRS 值\_MULTISAMPLEANTIALIAS 不得不同场景的失败。 也就是说，如果 D3DRS\_MULTISAMPLEANTIALIAS 是**TRUE**对于一个场景，它可以是**FALSE**的另一个场景。

-   是无响应的请求从应用程序可以修改多重采样呈现目标中的示例。 也就是说，它不响应 D3DRS 位掩码设置\_MULTISAMPLEMASK 设备呈现状态 (D3DRENDERSTATETYPE)。

务必要注意，如果驱动程序将使用为拉伸 blt 执行页面翻转在全屏模式下，该驱动程序应指定受支持的示例中的计数**wFlipMSTypes**的成员[ **DDPIXELFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff550274)的**MultiSampleCaps**结构，而不**wBltMSTypes**正在执行翻转作为成员。

 

 





