---
title: 扩展图面功能
description: 扩展图面功能
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
ms.openlocfilehash: f90843a7391244cb4a1ac867446aa3202ea4fc21
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838289"
---
# <a name="extended-surface-capabilities"></a>扩展图面功能


## <span id="ddk_extended_surface_capabilities_gg"></span><span id="DDK_EXTENDED_SURFACE_CAPABILITIES_GG"></span>


从 Microsoft DirectX 6.0 开始，Microsoft DirectDraw 包含先前版本中的表面功能。 这些扩展功能要求添加几个新结构，尤其是 [**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85)) 和 [**DD \_ MORESURFACECAPS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_moresurfacecaps) 结构。 DDSCAPS2 结构包含最初在 [**DDSCAPS**](/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))结构中找到的 **dwCaps** 成员，还包含三个新成员： **dwCaps2**、 **dwCaps3** 和 **dwCaps4**。 在 DirectDraw 中，只有 **dwCaps2** 用于 DirectX 6.0。 **DDSCAPS2** 结构的最后三个成员也按 DDSCAPSEX 结构进行了相同的排列。

 

