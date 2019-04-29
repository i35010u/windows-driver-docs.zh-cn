---
title: 显示驱动程序的图形 DDI 函数
description: 显示驱动程序的图形 DDI 函数
ms.assetid: 9edd06bd-7aac-4015-864d-b08f3e3a79fd
keywords:
- 显示驱动程序 WDK Windows 2000 中，图形
- 显示图形 DDI 函数 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a70805ffca90452973707c91398aad21403694c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374605"
---
# <a name="graphics-ddi-functions-for-display-drivers"></a>显示驱动程序的图形 DDI 函数


## <span id="ddk_graphics_ddi_functions_for_display_drivers_gg"></span><span id="DDK_GRAPHICS_DDI_FUNCTIONS_FOR_DISPLAY_DRIVERS_GG"></span>


Microsoft 基于 NT 的操作系统显示驱动程序必须实现多个图形 DDI 函数。 尽管编写利用现有的 GDI 功能的驱动程序会更小且更易于编写，但应确保您的驱动程序还实现它可以比 GDI 更有效地执行这些操作。

显示驱动程序图形 DDI 函数划分为三个组，其中每个以下主题中所述：

1.  [所需的每个显示器驱动程序的图形 DDI 函数](required-display-driver-functions.md)。

2.  [在某些情况下所需的图形 DDI 函数](conditionally-required-display-driver-functions.md)。

3.  [是可选的图形 DDI 函数](optional-display-driver-functions.md)。

 

 





