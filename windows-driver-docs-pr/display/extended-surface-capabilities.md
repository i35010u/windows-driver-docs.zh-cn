---
title: 扩展图面功能
description: 扩展图面功能
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
ms.openlocfilehash: 5527629931ceaf61c2627b457f908fa5ed842f22
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381867"
---
# <a name="extended-surface-capabilities"></a>扩展图面功能


## <span id="ddk_extended_surface_capabilities_gg"></span><span id="DDK_EXTENDED_SURFACE_CAPABILITIES_GG"></span>


从 Microsoft DirectX 6.0 开始，Microsoft DirectDraw 包含图面上功能超越以前的版本中找到。 这些扩展功能需要额外的几个新的结构，专门[ **DDSCAPS2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))并[ **DD\_MORESURFACECAPS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_moresurfacecaps)结构。 DDSCAPS2 结构包含**dwCaps**成员最初位于[ **DDSCAPS** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))结构，但还包含三个新成员： **dwCaps2**， **dwCaps3**，和**dwCaps4**。 仅**dwCaps2** DirectX 6.0 DirectDraw 中使用。 最后三个成员**DDSCAPS2**结构也相同排列 DDSCAPSEX 结构中。

 

 





