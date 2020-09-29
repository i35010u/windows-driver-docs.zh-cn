---
title: 内存堆分配
description: 内存堆分配
ms.assetid: 669dce85-ed37-4d47-88d6-115cb3a2e419
keywords:
- 步幅 WDK DirectDraw
- 音调 WDK DirectDraw
- 偏移 WDK DirectDraw
- 绘制内存 WDK DirectDraw，堆
- DirectDraw 内存 WDK Windows 2000 显示，堆
- 内存 WDK DirectDraw，堆
- 显示内存 WDK DirectDraw，堆
- 堆 WDK DirectDraw
- 分配内存堆
- VIDEOMEMORY
- 表面 WDK DirectDraw，内存堆分配
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35ae1f7fc18afb3652dc6e214c4065a8fd75ccb6
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423545"
---
# <a name="memory-heap-allocation"></a>内存堆分配


## <span id="ddk_memory_heap_allocation_gg"></span><span id="DDK_MEMORY_HEAP_ALLOCATION_GG"></span>


若要分配图面，DirectDraw 会按驱动程序指定的顺序扫描显示内存堆。 堆在 [**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory) 结构的数组中指定。 DirectDraw 按数组中 VIDEOMEMORY 结构的顺序访问堆。 VIDEOMEMORY 结构设置堆的某些指标，例如起始和结束内存地址、描述堆访问的标志以及为此堆中放置的图面限制的使用类型。 DirectDraw 通过 suballocating 并解除分配内存（即，在每个堆的管辖区域下创建和销毁表面）来管理堆。 物理限制确定如何设置这些属性。

当尝试分配内存来响应图面创建或还原时，DirectDraw 的堆管理器将通过 [**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory) 结构进行两次传递。 VIDEOMEMORY 结构的 **ddsCaps** 成员通知 DirectDraw 堆中的内存在第一次传递中无法使用的情况。 例如，如果堆只是足以用于后台缓冲区，则可以通过设置 DDSCAPS OFFSCREENPLAIN 标志，从第一轮上排除子画面 \_ 。 这样一来，其他堆就会在屏幕上的纯文本表面上填充，同时保留后台缓冲区以便进行页翻转。

VIDEOMEMORY 结构的 **ddsCapsAlt** 成员可设置为允许第二个阶段上的子画面。 这样一来，所涉及的堆就可以允许子画面，但仅当无法在任何其他堆中创建子画面时。 请勿 \_ 在 **ddsCapsAlt**中指定 DDSCAPS OFFSCREENPLAIN 标志。 这允许以最佳方式使用堆，而不需要使用其他方法。

显示内存堆可以是线性的或矩形的，具体取决于 blitter 或现有显示驱动程序的需求。 [**VIDEOMEMORY**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory)结构的**dwFlags**成员用于指定内存分配类型。 线性堆说明每个图面的间距可以不同的内存区域。 矩形堆说明每个图面的间距是固定的。 如果需要，可以在相同的显示卡内混合和匹配这些堆。 有关详细信息，请参阅 [内存配置](memory-configurations.md)。

图面的内存 *跨度*（也称为步幅或 offset）是添加到显示内存列中的字节数，以到达以下扫描行中的同一列显示内存。 由于螺距以字节而不是像素来度量，因此，640x480x8 表面的螺距值不同于具有相同宽度和高度尺寸的图面，但不同像素格式 (以) 为单位的深度。 此外，螺距值有时会反映运行时保留为缓存的额外字节数，以及由于对齐要求而产生的额外字节数。 因此，您不能假定螺距只是图面的宽度乘以每个像素的字节数。 相反，请按下图所示，直观显示 width 和螺距之间的差异。

![说明 width 和螺距差别的示意图](images/ddfig3.png)

如前文所述，在确定螺距值时，还必须考虑对齐要求。 例如，假设每个像素一个字节 (bpp) 表面为97像素宽。 同时，假设硬件或显示器驱动程序要求 DWORD (4 字节) 对齐。 如果运行时未保留缓存字节，则跨度为100，这是大于97的下一个较大数字，可被4整除。 以下计算确定此螺距值：

```cpp
pitch = bpp * width + ( 4 - ( bpp * width) % 4 )
// that is, pitch = 97 + (4 - 1) = 100
```

 

