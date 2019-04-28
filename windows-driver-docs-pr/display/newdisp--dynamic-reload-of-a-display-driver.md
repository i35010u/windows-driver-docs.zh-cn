---
title: NewDisp 动态重新加载的显示器驱动程序
description: NewDisp 动态重新加载的显示器驱动程序
ms.assetid: 0f8ac27c-8a42-4032-9974-89a7463dccbb
keywords:
- newdisp.exe
- 动态驱动程序将重新加载 WDK Windows 2000 显示
- 动态重新加载驱动程序 WDK Windows 2000 显示
- 重新启动动态重新加载 WDK Windows 2000 显示通过预防
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 326c4a27c513995c2465fd58eb0717168826021f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345525"
---
# <a name="newdisp-dynamic-reload-of-a-display-driver"></a>NewDisp：显示驱动程序的动态重新加载


## <span id="ddk_newdisp_dynamic_reload_of_a_display_driver_gg"></span><span id="DDK_NEWDISP_DYNAMIC_RELOAD_OF_A_DISPLAY_DRIVER_GG"></span>


驱动程序开发工具包 (DDK) 提供了一个工具，使显示驱动程序而无需重新启动动态重新加载。 此工具叫做*newdisp.exe*，加快了显示器驱动程序在开发过程中测试更新显示驱动程序代码时，从而不需要重新启动。

**请注意**  此工具不是在 Windows Vista 和更高版本的 Windows Driver Kit (WDK) 中可用。

 

**若要运行*newdisp.exe***

1.  关闭所有 Direct3D 和 OpenGL 应用程序。

2.  将复制到的最新的显示驱动程序的 DLL  *\\system32*目录。

3.  运行*newdisp* （不带任何参数）。

每次*newdisp*是调用，它将重新加载显示器驱动程序。 假定在调用时不存在任何驱动程序引用*newdisp*来实现功能的动态重新加载：

-   调用**ChangeDisplaySettings**使用 640 x 480 x 16 颜色，这会导致系统加载和运行 16 色 VGA 显示器驱动程序 DLL，并在相同的原因旧显示驱动程序无法从内存卸载 DLL。

-   立即执行另一个**ChangeDisplaySettings**为原始模式，这会导致新的显示驱动程序 DLL 被加载从回调 *\\system32*目录和 16 种颜色VGA 显示器驱动程序无法卸载 DLL。

对驱动程序实例的引用存在驱动程序是否 active Direct3D [ **WNDOBJ**](https://msdn.microsoft.com/library/windows/hardware/ff570599)，或[ **DRIVEROBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff556162)对象。 当*newdisp*运行时对驱动程序实例的引用存在，旧的显示器驱动程序 DLL 将永远不会被卸载，并且相应地将永远不会加载新的显示驱动程序 DLL。

*Newdisp*依赖于加载到 Windows 2000 和更高版本时避免重新启动; 重新加载该驱动程序已添加的功能的动态驱动程序因此，它不适用于在 Windows NT 4.0 和早期操作系统版本上。 它也不会不起作用的 VGA 驱动程序无法加载图形在设备上，或如果本机显示驱动程序支持的模式，640 x 480 x 16 颜色而不是让该模式由 VGA 驱动程序处理。

请注意， *newdisp*不支持的原因要重新加载的微型端口驱动程序。 如果更改微型端口驱动程序，则必须重新启动系统安装并对其进行测试。

 

 





