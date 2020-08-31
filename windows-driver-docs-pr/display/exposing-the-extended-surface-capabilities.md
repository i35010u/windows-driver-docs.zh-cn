---
title: 公开扩展图面功能
description: 公开扩展图面功能
ms.assetid: 833171f0-e86a-46c9-9596-87b9b292c03c
keywords:
- 绘制扩展 surface 功能 WDK DirectDraw，公开
- DirectDraw 扩展 surface 功能，WDK Windows 2000 显示，公开
- 扩展 surface 功能 WDK DirectDraw，公开
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55c20d29310d4aee65b29e6f744ff5a699f39c76
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066712"
---
# <a name="exposing-the-extended-surface-capabilities"></a>公开扩展图面功能


## <span id="ddk_exposing_the_extended_surface_capabilities_gg"></span><span id="DDK_EXPOSING_THE_EXTENDED_SURFACE_CAPABILITIES_GG"></span>


[**DDCORECAPS**](/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)结构包含一个[**DDSCAPS**](/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))字段，驱动程序将填充该字段，以指示它们支持的表面类型。 向应用程序报告这些上限时，将返回稍微不同的结构 DDCAPS。 此 DDCAPS 结构是从驱动程序的 DDCORECAPS 和使用 [**DdGetDriverInfo**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 接口查询的其他结构生成的。 对于最新版本的 DirectX，应用程序可见的 DDCAPS 包含一个 [**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85)) 成员。 此 DDCAPS2 成员是从 DDCORECAPS 结构中的 DDSCAPS 成员和[**DD \_ MORESURFACECAPS**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_moresurfacecaps)结构的**ddsCapsMore**成员构造而来的。

在 \_ 驱动程序初始化时使用 *DdGetDriverInfo* 调用从驱动程序查询 DD MORESURFACECAPS 结构。 *Ddrawint*中定义的相应 GUID 是 guid \_ DDMoreSurfaceCaps。

响应 GUID \_ DDMoreSurfaceCaps 查询是完全可选的。 它旨在允许驱动程序执行两个不同的操作：

-   公开驱动程序可以在显示内存中创建的扩展接口功能。

-   适用于这些扩展 surface 功能的全新堆限制。

第一项已在上一节中介绍，而且非常容易理解。 第二个项更复杂，读者应熟悉[**VIDEOMEMORY**](/windows/desktop/api/ddrawint/ns-ddrawint-_videomemory)结构的**ddsCaps**和**ddsCapsAlt**成员的重要性，如[内存堆分配](memory-heap-allocation.md)中所述，然后再阅读下一节。

 

