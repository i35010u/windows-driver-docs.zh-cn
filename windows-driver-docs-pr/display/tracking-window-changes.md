---
title: 跟踪窗口变化
description: 跟踪窗口变化
ms.assetid: 76539ee8-439a-4c6a-b16a-3998e341f954
keywords:
- 显示驱动程序 WDK Windows 2000 中，窗口的更改
- 窗口更改跟踪 WDK Windows 2000 显示
- WNDOBJ
- 显示客户端区域更改 WDK Windows 2000
- 显示可见的客户端区域 WDK Windows 2000
- 大小 WDK Windows 2000 的屏幕
- 位置 WDK Windows 2000 时，显示
- 跟踪窗口更改 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09cf77f607cb72e75d00a46b0e4b8a89e0cf5243
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561521"
---
# <a name="tracking-window-changes"></a>跟踪窗口变化


## <span id="ddk_tracking_window_changes_gg"></span><span id="DDK_TRACKING_WINDOW_CHANGES_GG"></span>


更改为一个窗口，其中包括一个在[多监视器系统](multiple-monitor-support-in-the-display-driver.md)，可以通过将设备驱动程序通过跟踪[ **WNDOBJ**](https://msdn.microsoft.com/library/windows/hardware/ff570599)。 WNDOBJ 是包含有关位置、 大小和窗口的可见客户端区域的信息的驱动程序级别窗口对象。 也就是说，通过创建对应于应用程序窗口 WNDOBJ，驱动程序可以跟踪大小、 位置和该窗口中的客户端区域更改。

应用程序使用 Win32 API 来访问**WNDOBJ\_安装程序**由设备驱动程序实现的功能。 通过 Win32 获得访问权限后**ExtEscape**函数。 GDI 将传递到设备驱动程序与此转义调用[ **DrvEscape**](https://msdn.microsoft.com/library/windows/hardware/ff556217)，实现的设备驱动程序与**WNDOBJ\_安装**值*iEsc*。

应用程序调用<strong>ExtEscape (</strong>hdc，WNDOBJ\_安装程序...**)** ，并将句柄传递到应用程序创建窗口 (由**CreateWindow**或某些等效 Win32 函数) 通过驱动程序将输入缓冲区。 如果该驱动程序将跟踪的窗口，则会调用[ **EngCreateWnd**](https://msdn.microsoft.com/library/windows/hardware/ff564769)的上下文中**ExtEscape**调用，以创建给定窗口的 WNDOBJ 结构。 从该点开始，对该窗口的任何更改会将向下传递给驱动程序。

该驱动程序应处理**ExtEscape**调用的方式如下所示：

```cpp
ULONG DrvEscape(
  SURFOBJ *pso,
  ULONG    iEsc,
  ULONG    cjIn,
  PVOID    pvIn,
  ULONG    cjOut,
  PVOID    pvOut)
{
    WNDOBJ *pwo;
    WNDDATA *pwd;

    if (iEsc == WNDOBJ_SETUP)
    {
        pwo = EngCreateWnd(pso,*((HWND *)pvIn),&DrvVideo,
                           WO_RGN_CLIENT, 0);

    // Allocate space for caching client rects. Remember the pointer
    // in the pvConsumer field.

        pwd = EngAllocMem(0, sizeof(WNDDATA), DRIVER_TAG);
        WNDOBJ_vSetConsumer(pwo,pwd);

    // Update the rectangle list for this wndobj.

        vUpdateRects(pwo);
        return(1);
    }

}
```

创建窗口对象的过程包括锁定特殊窗口资源，因此[ **EngCreateWnd** ](https://msdn.microsoft.com/library/windows/hardware/ff564769)应仅在上下文中调用**WNDOBJ\_安装**中转义[ **DrvEscape** ](https://msdn.microsoft.com/library/windows/hardware/ff556217)或[ **DrvSetPixelFormat**](https://msdn.microsoft.com/library/windows/hardware/ff556285)。

**EngCreateWnd**函数支持多个驱动程序的窗口跟踪。 通过**EngCreateWnd**，每个驱动程序标识其自身 GDI 是对相应的窗口中的更改调用的回调例程。 例如，此功能允许实时视频驱动程序，以跟踪更改的 OpenGL 驱动程序 OpenGL windows 跟踪更改的同时实时视频 windows。

GDI 将回调到具有最新的窗口状态，如果新驱动程序[ **WNDOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570599)中创建*DrvSetPixelFormat*或**ExtEscape**. GDI 将还回调到驱动程序时由 WNDOBJ 引用窗口被破坏。

作为快捷键，驱动程序可以访问的公共成员[ **WNDOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570599)结构。

跟踪窗口中更改涉及三个回调函数提供，以支持 WNDOBJ 结构的使用。 可见的客户端区域可能会通过调用枚举[ **WNDOBJ\_cEnumStart** ](https://msdn.microsoft.com/library/windows/hardware/ff570603)并[ **WNDOBJ\_bEnum** ](https://msdn.microsoft.com/library/windows/hardware/ff570602)回调函数。 驱动程序可能会将其自己的数据与 WNDOBJ 关联通过调用[ **WNDOBJ\_vSetConsumer** ](https://msdn.microsoft.com/library/windows/hardware/ff570606)回调函数。









