---
title: 公开扩展图面功能
description: 公开扩展图面功能
ms.assetid: 833171f0-e86a-46c9-9596-87b9b292c03c
keywords:
- 绘图图面上的扩展的功能 WDK DirectDraw、 公开
- 显示扩展的 DirectDraw 表面功能 WDK Windows 2000 公开
- 扩展 WDK DirectDraw 表面功能公开
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36f362f261552349b741c3fd7c58347d1b833def
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381890"
---
# <a name="exposing-the-extended-surface-capabilities"></a>公开扩展图面功能


## <span id="ddk_exposing_the_extended_surface_capabilities_gg"></span><span id="DDK_EXPOSING_THE_EXTENDED_SURFACE_CAPABILITIES_GG"></span>


[ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)结构包含[ **DDSCAPS** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))字段的驱动程序填充以指示其支持哪些类型的图面。 当这些 caps 报告给应用程序时，将返回略有不同的结构，DDCAPS。 从驱动程序的 DDCORECAPS 和使用查询其他结构生成此 DDCAPS 结构[ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)接口。 对于 DirectX 的最新版本，包含应用程序可见 DDCAPS [ **DDSCAPS2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))成员。 从 DDCORECAPS 结构中的 DDSCAPS 成员构造此 DDCAPS2 成员和**ddsCapsMore**的成员[ **DD\_MORESURFACECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_moresurfacecaps)结构。

DD\_MORESURFACECAPS 结构在驱动程序初始化时使用的驱动程序从查询*DdGetDriverInfo*调用。 中定义的相应 GUID *ddrawint.h*，是 GUID\_DDMoreSurfaceCaps。

响应的 GUID\_DDMoreSurfaceCaps 查询完全是可选的。 它旨在允许驱动程序执行两个不同的事情：

-   公开扩展驱动程序可以创建显示内存中的图面功能。

-   Express DirectDraw 图面上这些扩展功能的新堆限制。

第一项已在上一节中提及，并很容易理解。 第二项是更复杂，读者应熟悉的意义**ddsCaps**并**ddsCapsAlt**的成员[ **VIDEOMEMORY**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_videomemory)结构中所述[内存堆分配](memory-heap-allocation.md)，然后才能读取下一节。

 

 





