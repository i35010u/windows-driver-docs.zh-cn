---
title: 内存堆分配
description: 内存堆分配
ms.assetid: 669dce85-ed37-4d47-88d6-115cb3a2e419
keywords:
- stride WDK DirectDraw
- 宣传 WDK DirectDraw
- WDK DirectDraw 的偏移量
- 绘制内存 WDK DirectDraw，堆
- DirectDraw 内存 WDK Windows 2000 显示堆
- WDK DirectDraw，堆内存
- 显示内存 WDK DirectDraw 堆
- 堆 WDK DirectDraw
- 堆分配内存
- VIDEOMEMORY
- WDK DirectDraw，内存堆分配的图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b344b8cc4971d2ef17b2b541887e78d52dd49826
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344650"
---
# <a name="memory-heap-allocation"></a>内存堆分配


## <span id="ddk_memory_heap_allocation_gg"></span><span id="DDK_MEMORY_HEAP_ALLOCATION_GG"></span>


若要分配图面，DirectDraw 通过扫描显示内存堆、 驱动程序指定的顺序。 在一个数组中指定了堆[ **VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)结构。 DirectDraw 访问顺序的 VIDEOMEMORY 结构数组中的堆。 VIDEOMEMORY 结构描述堆的访问权限，标志设置的堆，起始和结束内存地址，例如特定度量值和哪些类型的使用情况是受限制，此堆中放置的图面。 DirectDraw 通过并和释放内存，也就是说，通过创建和销毁表面下每个堆的管辖权来管理在堆。 物理限制确定如何设置这些属性。

DirectDraw 的堆管理器可以通过两个阶段[ **VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)结构尝试分配内存以响应图面上创建或还原时。 **DdsCaps** VIDEOMEMORY 结构中的成员会通知 DirectDraw 堆中的哪些内存不能用于在第一个传递。 例如，如果堆是刚好足够放下后台缓冲区，子画面可以排除从首次通过分配通过设置 DDSCAPS\_OFFSCREENPLAIN 标志。 这样一来，其他堆填满与屏外的普通表面，同时保留后台缓冲区用于翻转页面。

**DdsCapsAlt** VIDEOMEMORY 结构中的成员可以将设置为在第二步允许子画面。 这样一来，如果无法在任何其他堆中创建 sprite，相关堆可以允许子画面，但仅。 未指定 DDSCAPS\_OFFSCREENPLAIN 标志**ddsCapsAlt**。 这使堆，以在理想情况下，未排除的其他用途。

显示内存堆可以是线性或矩形，具体取决于 blitter 或对现有的需求显示器驱动程序。 **DwFlags**的成员[ **VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)结构用于指定内存分配类型。 线性堆介绍其中的每个面间距可以是不同的内存区域。 矩形堆介绍其中的每个面音调固定的内存区域。 这些堆可以混合并匹配同一显示数据卡中，如有必要。 有关详细信息，请参阅[内存配置](memory-configurations.md)。

表面的内存*间距*（也称为 stride 或偏移量) 是以达到以下扫描线上的显示内存的同一列添加到列的显示内存的字节数。 因为间距以字节而不是像素为单位度量单位，640 x 480 x 8 面具有不同间距值比使用相同的宽度和高度维度，但不同的像素格式 （以位为单位的深度） 图面。 此外，pitch 值有时反映作为以及由于对齐需求的额外字节缓存有保留的运行时的额外字节。 因此，不能假定该间距是只是表面的宽度乘以每像素的字节数。 相反，可视化宽度和间距，如下图中所示的区别。

![说明宽度和间距之间的差异的关系图](images/ddfig3.png)

按前面所述，您必须还考虑到帐户对齐需求确定的俯仰值时。 例如，假设每个像素 (bpp) 图面一个字节是 97 像素宽。 此外，假设硬件或显示器驱动程序需要双字节 （4 字节） 对齐方式。 如果在运行时不保留缓存字节数，pitch 是 100，即的下一个更高版本编号上面 97 整除 4。 以下计算确定此间距值：

```cpp
pitch = bpp * width + ( 4 - ( bpp * width) % 4 )
// that is, pitch = 97 + (4 - 1) = 100
```

 

 





