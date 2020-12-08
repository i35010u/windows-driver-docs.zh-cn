---
title: 跟踪窗口变化
description: 跟踪窗口变化
keywords:
- 显示驱动程序 WDK Windows 2000，窗口更改
- 窗口更改跟踪 WDK Windows 2000 显示
- WNDOBJ
- 客户端区域更改 WDK Windows 2000 显示
- 可见客户端区域，WDK Windows 2000 显示
- size WDK Windows 2000 显示
- 定位 WDK Windows 2000 显示器
- 跟踪窗口更改 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ff07fa25c70a908d403aa5f94db35259899fd84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802587"
---
# <a name="tracking-window-changes"></a>跟踪窗口变化


## <span id="ddk_tracking_window_changes_gg"></span><span id="DDK_TRACKING_WINDOW_CHANGES_GG"></span>


设备驱动程序可以通过 [**WNDOBJ**](/windows/win32/api/winddi/ns-winddi-wndobj)跟踪对窗口（包括 [多监视器系统](multiple-monitor-support-in-the-display-driver.md)中的窗口）所做的更改。 WNDOBJ 是驱动程序级别的窗口对象，其中包含有关窗口的位置、大小和可见客户端区域的信息。 也就是说，通过创建对应于应用程序窗口的 WNDOBJ，驱动程序可以在该窗口中跟踪大小、位置和客户端区域更改。

应用程序使用 Win32 API 访问设备驱动程序实现的 **WNDOBJ \_ 安装程序** 功能。 通过 Win32 **ExtEscape** 函数获取访问权限。 GDI 将此转义调用传递到 [**DrvEscape**](/windows/win32/api/winddi/nf-winddi-drvescape)的设备驱动程序，由设备驱动程序实现，并使用 **WNDOBJ \_ 安装** 程序的值 *iEsc*。

应用程序调用 <strong>ExtEscape (</strong>HDC，WNDOBJ \_ 安装程序,.。。**)** ，并将句柄传递到应用程序创建的窗口 (由 **CreateWindow** 或) 通过输入缓冲区向驱动程序创建的等效 Win32 函数创建。 如果驱动程序要跟踪窗口，它将在 **ExtEscape** 调用的上下文中调用 [**EngCreateWnd**](/windows/win32/api/winddi/nf-winddi-engcreatewnd)，以为给定的窗口创建 WNDOBJ 结构。 从此时开始，对此窗口所做的任何更改都将向下传递到该驱动程序。

驱动程序应按照与下面类似的方式处理 **ExtEscape** 调用：

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

创建窗口对象涉及锁定特殊窗口资源，因此，只应在 [**DrvEscape**](/windows/win32/api/winddi/nf-winddi-drvescape)或 [**DrvSetPixelFormat**](/windows/win32/api/winddi/nf-winddi-drvsetpixelformat)中的 **WNDOBJ \_ 安装程序** 转义的上下文中调用 [**EngCreateWnd**](/windows/win32/api/winddi/nf-winddi-engcreatewnd) 。

**EngCreateWnd** 函数支持多个驱动程序的窗口跟踪。 通过 **EngCreateWnd**，每个驱动程序都标识自己的回调例程，GDI 将为相应的窗口调用更改。 例如，使用此功能可以在 OpenGL 驱动程序跟踪对 OpenGL windows 的更改时，使用实时视频驱动程序来跟踪实时视频窗口的更改。

如果在 *DrvSetPixelFormat* 或 **ExtEscape** 中创建了新的 [**WNDOBJ**](/windows/win32/api/winddi/ns-winddi-wndobj) ，则 GDI 将回发到具有最新窗口状态的驱动程序。 当 WNDOBJ 引用的窗口被销毁时，GDI 还会回叫驱动程序。

作为加速器，驱动程序可以访问 [**WNDOBJ**](/windows/win32/api/winddi/ns-winddi-wndobj) 结构的公共成员。

跟踪窗口更改涉及使用提供的三个回调函数来支持 WNDOBJ 结构。 可以通过调用 [**WNDOBJ \_ CEnumStart**](/windows/win32/api/winddi/nf-winddi-wndobj_cenumstart) 和 [**WNDOBJ \_ bEnum**](/windows/win32/api/winddi/nf-winddi-wndobj_benum) 回调函数来枚举可见客户端区域。 驱动程序可以通过调用 [**WNDOBJ \_ vSetConsumer**](/windows/win32/api/winddi/nf-winddi-wndobj_vsetconsumer) 回调函数，将其自己的数据与 WNDOBJ 关联。
