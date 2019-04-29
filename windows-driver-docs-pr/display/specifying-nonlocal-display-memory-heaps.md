---
title: 指定非本地显示内存堆
description: 指定非本地显示内存堆
ms.assetid: 4320b6e7-81ef-4bb4-bda8-680467b6421f
keywords:
- 堆 WDK DirectDraw
- 显示内存 WDK DirectDraw 堆
- 非本地显示内存 WDK DirectDraw 堆
- AGP WDK DirectDraw 堆
- 绘制 AGP 支持 WDK DirectDraw，堆
- DirectDraw AGP 支持 WDK Windows 2000 显示堆
- WDK DirectDraw AGP，堆内存
- 线性堆 WDK DirectDraw
- 物理堆 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d76dad4381703ce654ae57316690131a12338cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376033"
---
# <a name="specifying-nonlocal-display-memory-heaps"></a>指定非本地显示内存堆


## <span id="ddk_specifying_nonlocal_display_memory_heaps_gg"></span><span id="DDK_SPECIFYING_NONLOCAL_DISPLAY_MEMORY_HEAPS_GG"></span>


DirectDraw 驱动程序控制 AGP 的内存量通过返回堆中的可用和到哪些表面[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)结构，它是传递的回 DirectDraw。 该驱动程序标识非本地堆，通过指定 VIDMEM\_ISNONLOCAL 标志**dwFlags**的成员[ **VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)数据结构介绍在堆。 此外，驱动程序可以选择通过指定 VIDMEM 启用组合的非本地堆上内存写入\_除了 VIDMEM ISWC 标志\_ISNONLOCAL。

它负责的大小 （线性或矩形）、 属性 （写入组合） 和图面类型堆不应而且不能用于向 DirectDraw 描述 AGP 兼容 DirectDraw 驱动程序。 但是，它不是驱动程序的责任才能实际保留到它的堆集或提交内存的地址空间。 这是由 DirectDraw 处理驱动程序的代表。 DirectDraw 隐藏从驱动程序管理 AGP 内存的详细信息。

在指定非本地显示内存堆时，驱动程序指定的开始地址没有任何意义。 DirectDraw 请求创建堆时，将由操作系统确定的起始地址重新映射表 (GART) 线性和物理，非本地堆的这两个图形地址。 因此，该驱动程序可以返回任何值的起始地址。 对于矩形堆，此起始地址将忽略 DirectDraw。 指定的宽度和高度均受 DirectDraw 需求来确定内存要求。 对于线性堆，起始地址具有的含义，但仅的范围内使用它来计算堆的大小。

DirectDraw 确定 (fpEnd-fpStart) 通过线性堆 + 1 （请注意，指定的结束地址不在堆结束后的第一个字节的堆中的最后一个字节） 的大小。 在这种情况下，只要时 DirectDraw 减去结束地址从该地址，并加上 1，结果是在堆的最大大小，则可以指定任何起始地址。

在需要 （如分配图面） 时，物理内存仅提交到 AGP 堆，尽管是一定不能指定非常大的非本地堆。 此类堆使用共享的地址空间，即便物理内存的其他重要资源是已提交。

它还是值得注意 DirectDraw 和 Windows 操作系统会施加的 AGP 在任何给定时间可以是已提交的内存量的策略限制。 这是有必要阻止系统的其余部分的资源不足。 因此，它是很有可能的非本地显示内存图面，即使非本地堆不会完全提交失败的请求。

当 DirectDraw 已确定正确的地址 （线性和物理） 堆的时它将其存储在其堆描述符。 DirectDraw 还提供了一种机制来在初始化时，这些地址的通知驱动程序。 如何做到这一点是特定于平台：

-   Microsoft Windows 2000 及更高版本，这通过[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)调用使用 GUID\_UpdateNonLocalHeap GUID。 当此 GUID 传递给*DDGetDriverInfo*，堆数据传入[ **DD\_UPDATENONLOCALHEAPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551748)数据结构。

 

 





