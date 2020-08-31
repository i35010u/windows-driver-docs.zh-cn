---
title: 通过 StretchBlt 提供多重采样支持
description: 通过 StretchBlt 提供多重采样支持
ms.assetid: c829c612-d09d-4a33-a117-e50b9ed57251
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多级显示，StretchBlt
- 以多级显示方式呈现 WDK DirectX 8.0，StretchBlt
- 呈现 multisamples WDK DirectX 8.0，StretchBlt
- stretch array.blit 操作 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc3526e9e33bc2b20d2a1f614c0af7f65ea1453f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063860"
---
# <a name="multisample-support-through-stretchblt"></a>通过 StretchBlt 提供多重采样支持


## <span id="ddk_multisample_support_through_stretchblt_gg"></span><span id="DDK_MULTISAMPLE_SUPPORT_THROUGH_STRETCHBLT_GG"></span>


尽管不是用于支持多级采样的建议机制，但驱动程序可以通过呈现到大的后台缓冲区并执行 stretch blt 将大容量后台处理重采样到较低的解析主缓冲区来实现多级性支持。 但是，如果这是驱动程序支持多级的机制，则驱动程序必须 \_ 在 D3D8CAPS 结构的 **RasterCaps** 成员中设置新的功能位 D3DPRASTERCAPS STRETCHBLTMULTISAMPLE。 有关 D3DCAPS8 的说明，请参阅 DirectX 8.0 SDK 文档。

当驱动程序设置 D3DPRASTERCAPS \_ STRETCHBLTMULTISAMPLE 位时，它表示：

-   在呈现同一场景时，将导致应用程序的请求失败，以启用和禁用全场景抗锯齿。 也就是说，它无法在呈现单个场景的过程中打开**BOOL**和关闭 D3DRS \_ MULTISAMPLEANTIALIAS 设备渲染状态 (D3DRENDERSTATETYPE) 的 BOOL 值。 请注意，更改 D3DRS MULTISAMPLEANTIALIAS 的 **BOOL** 值的请求 \_ 对于不同场景不能失败。 也就是说，如果 \_ 一个场景的 D3DRS MULTISAMPLEANTIALIAS 为 **TRUE** ，则对于另一个场景，可能为 **FALSE** 。

-   无响应应用程序的请求，以在多级呈现目标中修改样本。 也就是说，它不会响应将 D3DRS \_ MULTISAMPLEMASK 设备渲染状态的位掩码设置 (D3DRENDERSTATETYPE) 。

需要注意的是，如果驱动程序使用 stretch blt 在全屏模式下执行页面翻转，则驱动程序应在[**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat) **MultiSampleCaps**结构的**wFlipMSTypes**成员中指定支持的样本计数，而不是在执行翻转时指定**wBltMSTypes**成员。

 

