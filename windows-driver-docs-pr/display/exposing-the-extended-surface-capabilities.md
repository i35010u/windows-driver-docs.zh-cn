---
title: 公开扩展的表面功能
description: 公开扩展的表面功能
ms.assetid: 833171f0-e86a-46c9-9596-87b9b292c03c
keywords:
- 绘图图面上的扩展的功能 WDK DirectDraw、 公开
- 显示扩展的 DirectDraw 表面功能 WDK Windows 2000 公开
- 扩展 WDK DirectDraw 表面功能公开
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db1f1b89d3f6c2d508036d42090dab67f855784c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519245"
---
# <a name="exposing-the-extended-surface-capabilities"></a>公开扩展的表面功能


## <span id="ddk_exposing_the_extended_surface_capabilities_gg"></span><span id="DDK_EXPOSING_THE_EXTENDED_SURFACE_CAPABILITIES_GG"></span>


[ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)结构包含[ **DDSCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff550286)字段的驱动程序填充以指示其支持哪些类型的图面。 当这些 caps 报告给应用程序时，将返回略有不同的结构，DDCAPS。 从驱动程序的 DDCORECAPS 和使用查询其他结构生成此 DDCAPS 结构[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)接口。 对于 DirectX 的最新版本，包含应用程序可见 DDCAPS [ **DDSCAPS2** ](https://msdn.microsoft.com/library/windows/hardware/ff550292)成员。 从 DDCORECAPS 结构中的 DDSCAPS 成员构造此 DDCAPS2 成员和**ddsCapsMore**的成员[ **DD\_MORESURFACECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff551659)结构。

DD\_MORESURFACECAPS 结构在驱动程序初始化时使用的驱动程序从查询*DdGetDriverInfo*调用。 中定义的相应 GUID *ddrawint.h*，是 GUID\_DDMoreSurfaceCaps。

响应的 GUID\_DDMoreSurfaceCaps 查询完全是可选的。 它旨在允许驱动程序执行两个不同的事情：

-   公开扩展驱动程序可以创建显示内存中的图面功能。

-   Express DirectDraw 图面上这些扩展功能的新堆限制。

第一项已在上一节中提及，并很容易理解。 第二项是更复杂，读者应熟悉的意义**ddsCaps**并**ddsCapsAlt**的成员[ **VIDEOMEMORY**](https://msdn.microsoft.com/library/windows/hardware/ff570171)结构中所述[内存堆分配](memory-heap-allocation.md)，然后才能读取下一节。

 

 





