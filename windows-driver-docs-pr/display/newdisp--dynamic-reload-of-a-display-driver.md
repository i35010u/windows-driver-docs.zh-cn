---
title: 显示驱动程序的 NewDisp 动态重新加载
description: 显示驱动程序的 NewDisp 动态重新加载
ms.assetid: 0f8ac27c-8a42-4032-9974-89a7463dccbb
keywords:
- newdisp.exe
- 动态驱动程序重新加载 WDK Windows 2000 显示器
- 重新加载驱动程序动态 WDK Windows 2000 显示器
- 动态重载 WDK Windows 2000 显示器的重启防护
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63c7a57953f8b986089905ad80eb581274604612
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715162"
---
# <a name="newdisp-dynamic-reload-of-a-display-driver"></a>NewDisp：显示驱动程序的动态重新加载


## <span id="ddk_newdisp_dynamic_reload_of_a_display_driver_gg"></span><span id="DDK_NEWDISP_DYNAMIC_RELOAD_OF_A_DISPLAY_DRIVER_GG"></span>


驱动程序开发工具包 (DDK) 提供一种可在不重新启动的情况下动态重新加载显示驱动程序的工具。 此工具称为 *newdisp.exe*，它通过在更新显示器驱动程序代码时不必要地重新启动，加速了在开发期间显示驱动程序测试。

**注意**   此工具不适用于 windows Vista 和更高版本的 Windows 驱动程序工具包 (WDK) 。

 

**运行 *newdisp.exe***

1.  关闭所有 Direct3D 和 OpenGL 应用程序。

2.  将已更新的显示驱动程序的 DLL 复制到* \\ system32*目录中。

3.  运行不带任何参数) 的 *newdisp* (。

每次调用 *newdisp* 时，它会重新加载显示驱动程序。 假设在调用时不存在任何驱动程序引用， *newdisp* 将通过以下方式完成动态重载：

-   通过640x480x16 颜色调用 **ChangeDisplaySettings** ，这会导致系统加载并运行16色 VGA 显示驱动程序 dll，同时会导致旧的显示驱动程序 dll 从内存中卸载。

-   立即对原始模式执行另一个**ChangeDisplaySettings**回调，这会导致从* \\ system32*目录加载新的显示驱动程序 dll，并卸载16色 VGA 显示驱动程序 dll。

如果驱动程序具有活动的 Direct3D、 [**WNDOBJ**](/windows/win32/api/winddi/ns-winddi-_wndobj)或 [**DRIVEROBJ**](/windows/win32/api/winddi/ns-winddi-_driverobj) 对象，则存在对驱动程序实例的引用。 当 *newdisp* 在对驱动程序实例的引用存在时运行时，将永远不会卸载旧的显示驱动程序 dll，并且将永远不会加载新的显示驱动程序 dll。

*Newdisp* 依赖于动态驱动程序加载功能，该功能已添加到 Windows 2000 和更高版本，无需重新启动就重新加载驱动程序;因此，它在 Windows NT 4.0 和以前的操作系统版本上不起作用。 如果无法在图形设备上加载 VGA 驱动程序，或者本机显示驱动程序支持640x480x16 颜色模式，而不是让 VGA 驱动程序处理该模式，则它也不起作用。

请注意， *newdisp* 当前不会导致重新加载视频微型端口驱动程序。 如果更改了微型端口驱动程序，则必须重新启动系统才能进行安装和测试。

 

