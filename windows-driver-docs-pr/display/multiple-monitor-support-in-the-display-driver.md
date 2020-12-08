---
title: 显示驱动程序中的多监视器支持
description: 显示驱动程序中的多监视器支持
keywords:
- 显示驱动程序 WDK Windows 2000，多监视器
- 多监视器 WDK
- 多监视器系统 WDK Windows 2000 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fa5262035239892a9cfc9c8a178e0703d2a07f4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816313"
---
# <a name="multiple-monitor-support-in-the-display-driver"></a>显示驱动程序中的多监视器支持

Windows 2000 和更高版本提供了多监视器支持;因此，显示器驱动程序编写者不得实现任何特殊代码来提供此支持。

必须在不使用全局变量的情况下实现显示器驱动程序。 特定显示驱动程序的 *PDEV* 中必须存在所有状态。 GDI 将为由视频微型端口驱动程序创建的每个硬件设备扩展调用 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 。

为了跟踪多监视器系统中的窗口更改，驱动程序可以请求使用 "GDI" 创建具有桌面坐标的 WNDOBJ 对象。 驱动程序通过使用标志 WO [**EngCreateWnd**](/windows/win32/api/winddi/nf-winddi-engcreatewnd) \_ RGN \_ DESKTOP oozie.coord.application.path 调用 EngCreateWnd 来实现此功能 \_ 。 有关详细信息，请参阅 [跟踪窗口更改](tracking-window-changes.md) 。

在多监视器系统中，GDI 将设备的桌面位置存储在 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew)结构的 **dmPosition** 成员中。
