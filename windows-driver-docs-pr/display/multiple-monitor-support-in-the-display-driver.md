---
title: 显示驱动程序中的多监视器支持
description: 显示驱动程序中的多监视器支持
ms.assetid: ba15af67-94c0-4c37-8b3d-b1472e731d88
keywords:
- 显示驱动程序 WDK Windows 2000，多监视器
- 多监视器 WDK
- 多监视器系统 WDK Windows 2000 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbcea252b29e9fbf92975ef1ef3cfffbd7358679
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91424000"
---
# <a name="multiple-monitor-support-in-the-display-driver"></a>显示驱动程序中的多监视器支持


## <span id="ddk_multiple_monitor_support_in_the_display_driver_gg"></span><span id="DDK_MULTIPLE_MONITOR_SUPPORT_IN_THE_DISPLAY_DRIVER_GG"></span>


Windows 2000 和更高版本提供了多监视器支持;因此，显示器驱动程序编写者不得实现任何特殊代码来提供此支持。

必须在不使用全局变量的情况下实现显示器驱动程序。 特定显示驱动程序的 *PDEV* 中必须存在所有状态。 GDI 将为由视频微型端口驱动程序创建的每个硬件设备扩展调用 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 。

为了跟踪多监视器系统中的窗口更改，驱动程序可以请求使用 "GDI" 创建具有桌面坐标的 WNDOBJ 对象。 驱动程序通过使用标志 WO [**EngCreateWnd**](/windows/win32/api/winddi/nf-winddi-engcreatewnd) \_ RGN \_ DESKTOP oozie.coord.application.path 调用 EngCreateWnd 来实现此功能 \_ 。 有关详细信息，请参阅 [跟踪窗口更改](tracking-window-changes.md) 。

在多监视器系统中，GDI 将设备的桌面位置存储在[**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devicemodew)结构的**dmPosition**成员中。

 

