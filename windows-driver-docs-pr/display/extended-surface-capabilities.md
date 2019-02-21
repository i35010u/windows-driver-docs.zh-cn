---
title: 扩展图面上的功能
description: 扩展图面上的功能
ms.assetid: daa1a310-1cea-48ca-a373-a496b997424f
keywords:
- 绘制扩展表面功能 WDK DirectDraw 图面上的扩展功能
- DirectDraw 扩展表面功能 WDK Windows 2000 显示，有关扩展图面上的功能
- 有关扩展的图面上功能的扩展表面功能 WDK DirectDraw
- WDK DirectDraw，扩展功能的图面
- 绘制扩展 WDK DirectDraw 表面功能
- DirectDraw 扩展 WDK Windows 2000 显示图面上的功能
- 扩展 WDK DirectDraw 表面功能
- DDSCAPS2
- DD_MORESURFACECAPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c7a1fafc74e381b65f454c1676d087c86178860
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533488"
---
# <a name="extended-surface-capabilities"></a>扩展图面上的功能


## <span id="ddk_extended_surface_capabilities_gg"></span><span id="DDK_EXTENDED_SURFACE_CAPABILITIES_GG"></span>


从 Microsoft DirectX 6.0 开始，Microsoft DirectDraw 包含图面上功能超越以前的版本中找到。 这些扩展功能需要额外的几个新的结构，专门[ **DDSCAPS2** ](https://msdn.microsoft.com/library/windows/hardware/ff550292)并[ **DD\_MORESURFACECAPS**](https://msdn.microsoft.com/library/windows/hardware/ff551659)结构。 DDSCAPS2 结构包含**dwCaps**成员最初位于[ **DDSCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff550286)结构，但还包含三个新成员： **dwCaps2**， **dwCaps3**，和**dwCaps4**。 仅**dwCaps2** DirectX 6.0 DirectDraw 中使用。 最后三个成员**DDSCAPS2**结构也相同排列 DDSCAPSEX 结构中。

 

 





