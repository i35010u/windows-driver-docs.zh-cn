---
title: Windows 2000 驱动程序初始化
description: Windows 2000 驱动程序初始化
ms.assetid: 82222357-1e5a-4aec-879a-68f19f3faa4f
keywords:
- DirectDraw 驱动程序初始化 WDK Windows 2000 显示，Windows 2000
- Windows 2000 显示器驱动程序模型 WDK、 DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a20c1dfd1acbf0e4c24de8079477a340ee385c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391131"
---
# <a name="windows-2000-driver-initialization"></a>Windows 2000 驱动程序初始化


## <span id="ddk_windows_2000_driver_initialization_gg"></span><span id="DDK_WINDOWS_2000_DRIVER_INITIALIZATION_GG"></span>


在 Windows 2000 及更高版本，当应用程序请求仅检索驱动程序信息。 换而言之，在对 Microsoft DirectDraw 应用程序的请求创建 DirectDraw 对象的实例的响应，图形引擎调用驱动程序函数来初始化 DirectDraw 驱动程序。

从 Windows 2000 开始，在启动时和每个模式更改之后执行此序列。 这有副作用。 在 Windows 98 上 / 我，驱动程序通常有两种操作模式-GDI 模式和 DirectDraw 模式。 如果 DirectDraw 正在运行，不允许在 GDI 位图缓存，而提供的所有内存到 DirectDraw （反之亦然在 GDI 模式下）。 此行为导致有窗口应用程序 （例如使用 DirectX 的网页） 以会受到影响。 因此，在 Windows 2000 及更高版本，GDI 和 DirectDraw 需要有关如何使用内存进行协作。 Permedia3 示例驱动程序附带的 Windows 驱动程序开发工具包 (DDK) 具有如何执行此操作的示例。 (在 DDK 前面带有 Windows Driver Kit \[WDK\]。)

驱动程序初始化序列被通过调用以下函数：

-   [**DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)来检索有关的硬件功能的信息。 GDI 两次调用此函数：

    -   第一次调用确定显示内存堆和驱动程序支持的 Fourcc 数的大小。 将传递 GDI **NULL**两个*pvmList*并*pdwFourCC*参数。 该驱动程序应初始化并返回*pdwNumHeaps*并*pdwNumFourCC*仅参数。
    -   第二个调用了 GDI 分配显示内存和 FOURCC 内存中首次调用返回的值后*pdwNumHeaps*并*pdwNumFourCC*参数。 该驱动程序应在第二个调用中，初始化并返回*pdwNumHeaps*， *pvmList*， *pdwNumFourCC*，以及*pdwFourCC*参数。

    GDI 分配并初始化为零[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)向其结构*pHalInfo*点。 *DrvGetDirectDrawInfo*函数应填写相关的 DD 成员\_HALINFO 结构的特定于驱动程序的信息：

    -   该驱动程序应初始化的适当成员[ **VIDEOMEMORYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff570172)结构来描述的显示器的内存的一般格式。 请参阅[显示内存](display-memory.md)。
    -   该驱动程序应初始化的适当成员[ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)结构来描述 DirectDraw 到驱动程序的核心功能。
    -   如果该驱动程序支持的任何查询发送到驱动程序的 GUID 的 DirectX 功能[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)回调，该驱动程序必须初始化**GetDriverInfo**要指向的驱动程序的成员*DdGetDriverInfo*回调和集 DDHALINFO\_GETDRIVERINFOSET 位**dwFlags**。
    -   该驱动程序必须设置**dwSize**到的大小，以字节为单位的[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)结构。
-   [**DrvEnableDirectDraw** ](https://msdn.microsoft.com/library/windows/hardware/ff556208)由运行时启用 DirectDraw 硬件，并确定某些驱动程序的回调的支持。 GDI 分配并初始化为零[ **DD\_回调**](https://msdn.microsoft.com/library/windows/hardware/ff550485)， [ **DD\_SURFACECALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551721)，和[ **DD\_PALETTECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551681)参数结构。 该驱动程序应执行以下操作为每个实现这些回调：

    -   设置要指向回调适当结构的相应成员。
    -   设置相应 DDHAL\_*XXX*\_*XXX*位**dwFlags**适当结构的成员。

    该驱动程序可以实现其*DrvEnableDirectDraw*函数来指示它支持中列出的回调函数[DirectDraw 回调支持使用 DrvEnableDirectDraw](directdraw-callback-support-using-drvenabledirectdraw.md)。

    驱动程序的*DrvEnableDirectDraw*实现还可以将专用硬件资源，如以仅供 DirectDraw 显示内存。

-   [**DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)来检索其他回调函数和驱动程序支持的功能。

    如果不是**NULL**，则**GetDriverInfo**回调中返回[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)由驱动程序的结构[ **DrvGetDirectDrawInfo**](https://msdn.microsoft.com/library/windows/hardware/ff556229)。 GDI 分配并初始化[ **DD\_GETDRIVERINFODATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551550)结构和调用*DdGetDriverInfo*为每个中所述的Guid**DD\_GETDRIVERINFODATA**引用部分。 在中定义所有 Guid *ddrawint.h*。

    该驱动程序可以实现其*DdGetDriverInfo*函数来指示它支持中所指定的回调函数[DirectDraw 和 Direct3D 回调支持使用 DdGetDriverInfo](directdraw-and-direct3d-callback-support-using-ddgetdriverinfo.md)。

锁定的图面上的内存 (是否整个图面或图面的一部分) 可确保应用程序和硬件不能在同一时间获得的访问权限的图面上的内存。 这可以防止错误发生时应用程序写入图面上的内存。 此外，应用程序不能分页翻转，直到图面上的内存解锁。

 

 





