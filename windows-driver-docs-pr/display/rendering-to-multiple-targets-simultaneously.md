---
title: 同时呈现到多个目标
description: 同时呈现到多个目标
ms.assetid: 72c56ea6-d5da-420a-91f4-c7fa09daf67e
keywords:
- 呈现多个目标 WDK DirectX 9.0
- 多个呈现器目标 WDK DirectX 9.0
- 同时呈现器目标 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 274a1282a81fdcaef07cde5fc8f3871ee8ef4a6a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543369"
---
# <a name="rendering-to-multiple-targets-simultaneously"></a>同时呈现到多个目标


## <span id="ddk_rendering_to_multiple_targets_simultaneously_gg"></span><span id="DDK_RENDERING_TO_MULTIPLE_TARGETS_SIMULTANEOUSLY_GG"></span>


DirectX 9.0 版本驱动程序可以呈现为多个目标同时如果驱动程序指出其设备支持多个呈现器目标。 若要指示设备支持的呈现器目标的数，该驱动程序设置此数字中**NumSimultaneousRTs** D3DCAPS9 结构中的成员。 该驱动程序必须设置为 1，此数字，如果仅支持到单个目标的呈现。 该驱动程序在响应中返回 D3DCAPS9 结构**GetDriverInfo2**查询类似于如何返回 D3DCAPS8 结构，如中所述[报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 此查询的支持中所述[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

呈现器目标在多个呈现器目标组必须具有相同的维度，但可以具有不同的图面上格式。

驱动程序收到 D3DDP2OP\_SETRENDERTARGET2 操作代码，如果应用程序请求多个组中设置的其中一个呈现器目标的颜色缓冲区。

如果 DirectX 9.0 驱动程序支持多个目标上呈现，同时，它必须支持某些功能，并且可以支持扩展的功能。 以下主题介绍了这些必需和可选功能：

[多个呈现器目标所需的功能](required-features-for-multiple-render-targets.md)

[多个可选功能呈现器目标](optional-features-for-multiple-render-targets.md)

 

 





