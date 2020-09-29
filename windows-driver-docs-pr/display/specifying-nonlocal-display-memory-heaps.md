---
title: 指定非本地显示内存堆
description: 指定非本地显示内存堆
ms.assetid: 4320b6e7-81ef-4bb4-bda8-680467b6421f
keywords:
- 堆 WDK DirectDraw
- 显示内存 WDK DirectDraw，堆
- 非本地显示内存 WDK DirectDraw，堆
- AGP WDK DirectDraw，堆
- 绘制 AGP 支持 WDK DirectDraw，堆
- DirectDraw AGP 支持 WDK Windows 2000 显示，堆
- 内存 WDK DirectDraw AGP、堆
- 线性堆 WDK DirectDraw
- 物理堆 DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ab38dc619e7833e02fabaf6895399c22a52e16
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423898"
---
# <a name="specifying-nonlocal-display-memory-heaps"></a>指定非本地显示内存堆


## <span id="ddk_specifying_nonlocal_display_memory_heaps_gg"></span><span id="DDK_SPECIFYING_NONLOCAL_DISPLAY_MEMORY_HEAPS_GG"></span>


DirectDraw 驱动程序通过返回 [**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-dd_halinfo) 结构中传递回 DirectDraw 的堆，来控制有多少 AGP 内存可用。 驱动程序通过 \_ 在描述堆的[**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory)数据结构的**DWFLAGS**成员中指定 VIDMEM ISNONLOCAL 标志来标识非本地的堆。 而且，驱动程序还可以选择 \_ 在 VIDMEM ISNONLOCAL 之外指定 VIDMEM ISWC 标志来启用对非本地堆的内存写入组合 \_ 。

需要将 AGP 兼容的 DirectDraw 驱动程序的责任描述为 DirectDraw (线性或矩形) 的大小、 (写入合并) 的特性和不应和不能用于的接口类型。 但是，驱动程序不负责为堆保留地址空间，也不会向其提交内存。 此方法由 DirectDraw 代表驱动程序处理。 DirectDraw 隐藏了从驱动程序管理 AGP 内存的详细信息。

指定非本地显示内存堆时，驱动程序指定的起始地址是无意义的。 起始地址，在 DirectDraw 请求创建堆时，由操作系统确定非本地堆 (GART) 线性和物理的图形地址重新映射表。 因此，驱动程序可以返回起始地址的任何值。 对于矩形堆，DirectDraw 将忽略此起始地址。 指定的宽度和高度是 DirectDraw 需要确定内存要求的全部。 对于线性堆，开始地址有意义，只是它用于计算堆大小的程度。

DirectDraw 通过 (fpEnd-fpStart) + 1 (确定线性堆的大小，请注意指定的结束地址是堆中的最后一个字节，而不是堆) 结尾之后的第一个字节。 因此，只要 DirectDraw 从结束地址中减去该地址并增加1，就可以指定任何起始地址，结果就是堆的最大大小。

虽然物理内存仅在需要时才会提交给 AGP 堆 (即，因为在) 中分配了表面，因此，不需要指定非常大的非本地堆，这一点很重要。 此类堆使用共享地址空间和其他重要资源，即使在物理内存提交之前也是如此。

另外，请务必注意，DirectDraw 和 Windows 操作系统对可在任意给定时间提交的 AGP 内存量施加策略限制。 这对于防止系统的其余部分所需的资源不足。 因此，非本地显示内存表面的请求会失败，即使未完全提交非本地堆也是如此。

当 DirectDraw 确定了正确的地址 (线性和物理) 堆时，它会将它们存储在其堆描述符中。 DirectDraw 还提供了一种机制，用于在初始化时通知驱动程序这些地址。 此操作的执行方式是特定于平台的：

-   在 Microsoft Windows 2000 及更高版本上，使用 GUID UpdateNonLocalHeap GUID 通过 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 调用来完成此操作 \_ 。 将此 GUID 传递到 *DDGetDriverInfo*时，会在 [**DD \_ UPDATENONLOCALHEAPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_updatenonlocalheapdata) 数据结构中传递堆数据。

 

