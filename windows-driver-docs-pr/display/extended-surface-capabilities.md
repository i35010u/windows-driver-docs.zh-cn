---
title: 扩展图面功能
description: 扩展图面功能
ms.assetid: daa1a310-1cea-48ca-a373-a496b997424f
keywords:
- 绘制扩展 surface 功能 WDK DirectDraw，关于扩展 surface 功能
- DirectDraw 扩展 surface 功能 WDK Windows 2000 显示，关于扩展 surface 功能
- 扩展 surface 功能 WDK DirectDraw，关于扩展 surface 功能
- surface DirectDraw，扩展功能
- 绘制扩展 surface 功能 WDK DirectDraw
- DirectDraw 扩展 surface 功能 WDK Windows 2000 显示
- 扩展 surface 功能 WDK DirectDraw
- DDSCAPS2
- DD_MORESURFACECAPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da2b9f32c859d2db7d3434db36360bd4579960f4
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065856"
---
# <a name="extended-surface-capabilities"></a>扩展图面功能


## <span id="ddk_extended_surface_capabilities_gg"></span><span id="DDK_EXTENDED_SURFACE_CAPABILITIES_GG"></span>


从 Microsoft DirectX 6.0 开始，Microsoft DirectDraw 包含先前版本中的表面功能。 这些扩展功能要求添加几个新结构，尤其是 [**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85)) 和 [**DD \_ MORESURFACECAPS**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_moresurfacecaps) 结构。 DDSCAPS2 结构包含最初在[**DDSCAPS**](/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))结构中找到的**dwCaps**成员，还包含三个新成员： **dwCaps2**、 **dwCaps3**和**dwCaps4**。 在 DirectDraw 中，只有 **dwCaps2** 用于 DirectX 6.0。 **DDSCAPS2**结构的最后三个成员也按 DDSCAPSEX 结构进行了相同的排列。

 

