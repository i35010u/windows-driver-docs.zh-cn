---
title: 显示驱动程序中的多监视器支持
description: 显示驱动程序中的多监视器支持
ms.assetid: ba15af67-94c0-4c37-8b3d-b1472e731d88
keywords:
- 显示驱动程序 WDK Windows 2000 中，多个监视器
- 多个监视器 WDK
- 多监视器系统 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eabd4c7b8fc341cb3c8119a056be4c30b2942415
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372830"
---
# <a name="multiple-monitor-support-in-the-display-driver"></a>显示驱动程序中的多监视器支持


## <span id="ddk_multiple_monitor_support_in_the_display_driver_gg"></span><span id="DDK_MULTIPLE_MONITOR_SUPPORT_IN_THE_DISPLAY_DRIVER_GG"></span>


由 Windows 2000 和更高版本; 提供多监视器支持因此，显示驱动程序编写器必须实现任何特殊代码，以提供此支持。

显示器驱动程序必须实现而无需使用全局变量。 所有状态必须都存在于*PDEV*的特定显示驱动程序。 将调用 GDI [ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)为创建的微型端口驱动程序的每个硬件设备扩展。

若要在多监视器系统中跟踪窗口中更改，驱动程序可以请求 GDI 使用桌面坐标创建 WNDOBJ 对象。 该驱动程序将这是通过调用[ **EngCreateWnd** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatewnd)使用标志 WO\_RGN\_桌面\_坐标系。 请参阅[跟踪的窗口更改](tracking-window-changes.md)有关详细信息。

在多监视器系统中，GDI 将存储设备的桌面中位置**dmPosition**的成员[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构。

 

 





