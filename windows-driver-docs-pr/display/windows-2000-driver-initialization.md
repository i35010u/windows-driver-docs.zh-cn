---
title: Windows 2000 驱动程序初始化
description: Windows 2000 驱动程序初始化
ms.assetid: 82222357-1e5a-4aec-879a-68f19f3faa4f
keywords:
- DirectDraw 驱动程序初始化 WDK Windows 2000 显示，Windows 2000
- Windows 2000 显示器驱动程序型号 WDK，DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 610e680d4a7a2b23d8fc4ccdc605e3d7c24c0c11
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91424014"
---
# <a name="windows-2000-driver-initialization"></a>Windows 2000 驱动程序初始化


## <span id="ddk_windows_2000_driver_initialization_gg"></span><span id="DDK_WINDOWS_2000_DRIVER_INITIALIZATION_GG"></span>


在 Windows 2000 和更高版本中，仅当应用程序请求时才检索驱动程序信息。 换句话说，为了响应 Microsoft DirectDraw 应用程序创建 DirectDraw 对象实例的请求，图形引擎会调用驱动程序函数以初始化 DirectDraw 驱动程序。

从 Windows 2000 开始，将在启动时和每次模式更改之后完成此序列。 这会产生副作用。 在 Windows 98/Me 上，驱动程序通常有两种操作模式： GDI 模式和 DirectDraw 模式。 如果 DirectDraw 正在运行，则它不会允许 GDI 缓存位图，而是在处于 GDI 模式) 时，将所有内存都提供给 DirectDraw (，反之亦然。 此行为会导致 (的窗口应用程序，如使用 DirectX) 的网页受到影响。 因此，在 Windows 2000 和更高版本中，需要 GDI 和 DirectDraw 来与如何使用内存进行合作。 Windows 驱动程序开发工具包 (DDK) 附带的 Permedia3 示例驱动程序提供了如何执行此操作的示例。  (在 Windows 驱动程序工具包 WDK 之前的 DDK \[ \] 。 ) 

驱动程序初始化顺序是通过调用以下函数来实现的：

-   [**DrvGetDirectDrawInfo**](/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo) 检索有关硬件功能的信息。 GDI 调用此函数两次：

    -   第一次调用确定显示内存堆的大小和驱动程序支持的 Fourcc 数目。 GDI 对于*pvmList*和*pdwFourCC*参数均为**NULL** 。 驱动程序只应初始化并返回 *pdwNumHeaps* 和 *pdwNumFourCC* 参数。
    -   在 GDI 分配显示内存和 FOURCC 内存后，会根据第一次调用 *pdwNumHeaps* 和 *pdwNumFourCC* 参数中返回的值来执行第二次调用。 在第二次调用中，驱动程序应初始化并返回 *pdwNumHeaps*、 *pvmList*、 *pdwNumFourCC*和 *pdwFourCC* 参数。

    GDI 分配并零初始化 [**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-dd_halinfo) 结构到 *pHalInfo* 点。 *DrvGetDirectDrawInfo* 函数应填写 DD HALINFO 结构的相关成员 \_ 以及特定于驱动程序的信息：

    -   驱动程序应初始化 [**VIDEOMEMORYINFO**](/windows/win32/api/ddrawint/ns-ddrawint-videomemoryinfo) 结构的相应成员，以描述显示的内存的一般格式。 请参阅 [显示内存](display-memory.md)。
    -   驱动程序应初始化 [**DDCORECAPS**](/windows/win32/api/ddrawi/ns-ddrawi-ddcorecaps) 结构的相应成员，以描述 DirectDraw 的驱动程序核心功能。
    -   如果驱动程序支持通过将 GUID 发送到驱动程序的 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 回调查询的任何 DirectX 功能，则驱动程序必须将 **GetDriverInfo** 成员初始化为指向驱动程序的 *DdGetDriverInfo* 回调，并 \_ 在 **GETDRIVERINFOSET**中设置 DDHALINFO dwFlags 位。
    -   驱动程序必须将 **dwSize** 设置为 [**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-dd_halinfo) 结构的大小（以字节为单位）。
-   运行时使用[**DrvEnableDirectDraw**](/windows/win32/api/winddi/nf-winddi-drvenabledirectdraw)来启用 DirectDraw 硬件并确定驱动程序的某些回调支持。 GDI 分配并零初始化 [**DD \_ 回调**](/windows/win32/api/ddrawint/ns-ddrawint-dd_callbacks)、 [**dd \_ SURFACECALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_surfacecallbacks)和 [**dd \_ PALETTECALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_palettecallbacks) 参数结构。 对于它实现的每个回调，驱动程序应执行以下操作：

    -   将相应结构的相应成员设置为指向回调。
    -   \_*XXX* \_ 在相应结构的**dwFlags**成员中设置相应的 DDHAL xxx*xxx*位。

    驱动程序可以实现其 *DrvEnableDirectDraw* 函数，以指示它支持 [使用 DrvEnableDirectDraw 的 DirectDraw 回调支持](directdraw-callback-support-using-drvenabledirectdraw.md)中列出的回调函数。

    驱动程序的 *DrvEnableDirectDraw* 实现还可以专门将硬件资源（如显示内存）专用于 DirectDraw。

-   [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 检索驱动程序支持的其他回调函数和功能。

    如果不为**NULL**，则通过驱动程序的[**DrvGetDirectDrawInfo**](/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo)在[**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-dd_halinfo)结构中返回**GetDriverInfo**回调。 GDI 分配并初始化[**dd \_ GETDRIVERINFODATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_getdriverinfodata)结构，并为**dd \_ GETDRIVERINFODATA** reference 部分中所述的每个 guid 调用*DdGetDriverInfo* 。 所有 Guid 都是在 *ddrawint*中定义的。

    驱动程序可以实现它的 *DdGetDriverInfo* 函数，以指示它支持 DirectDraw 中指定的回调函数 [和使用 DdGetDriverInfo 的 Direct3D 回调支持](directdraw-and-direct3d-callback-support-using-ddgetdriverinfo.md)。

锁定表面内存 (整个表面或部分表面) 确保应用程序和硬件无法同时获取对表面内存的访问。 这可防止应用程序写入到表面内存时出现错误。 此外，应用程序不能翻页，直到表面内存解除锁定。

 

