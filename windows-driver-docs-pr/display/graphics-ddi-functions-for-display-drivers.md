---
title: 显示驱动程序的图形 DDI 函数
description: 显示驱动程序的图形 DDI 函数
keywords:
- 显示驱动程序 WDK Windows 2000，图形
- 图形 DDI 函数 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 347c643bb77b595937442029a981338434c1f45f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825731"
---
# <a name="graphics-ddi-functions-for-display-drivers"></a>显示驱动程序的图形 DDI 函数


## <span id="ddk_graphics_ddi_functions_for_display_drivers_gg"></span><span id="DDK_GRAPHICS_DDI_FUNCTIONS_FOR_DISPLAY_DRIVERS_GG"></span>


基于 Microsoft NT 的操作系统显示驱动程序必须实现多个图形 DDI 函数。 尽管编写一个大写的现有 GDI 功能的驱动程序将变得更小且更易于编写，但您应该确保您的驱动程序还实现了比 GDI 更有效的操作。

显示驱动程序图形 DDI 函数分为三个组，其中每个组在以下主题中进行了讨论：

1.  [每个显示器驱动程序所需的图形 DDI 函数](required-display-driver-functions.md)。

2.  [在某些情况下需要图形 DDI 函数](conditionally-required-display-driver-functions.md)。

3.  [可选的图形 DDI 函数](optional-display-driver-functions.md)。

 

 





