---
title: 扩展堆限制
description: 扩展堆限制
ms.assetid: 4f907768-670a-4ce5-b2d7-7af27baf80da
keywords:
- 绘图图面上的扩展的功能 WDK DirectDraw，堆
- DirectDraw 扩展表面功能 WDK Windows 2000 显示堆
- 扩展表面功能 WDK DirectDraw 堆
- 堆 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2d9ef2a829691e0412b581c134c966527e1e149
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353361"
---
# <a name="extended-heap-restrictions"></a>扩展堆限制


## <span id="ddk_extended_heap_restrictions_gg"></span><span id="DDK_EXTENDED_HEAP_RESTRICTIONS_GG"></span>


[ **DD\_MORESURFACECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff551659)结构是大小可变。 它始终都有**ddsCapsMore**成员，但它可能包含零个或更多**ddsExtendedHeapRestrictions**条目。 如果该驱动程序响应 GUID\_DDMoreSurfaceCaps 查询，它应返回 DD\_MORESURFACECAPS 结构，其中包含任意数量**ddsExtendedHeapRestrictions**返回作为它的项的显示内存在堆[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)结构 (DirectDraw 可保证 GUID\_DDMoreSurfaceCaps 查询发出后的驱动程序报告 DD\_HALINFO。)

该驱动程序还应填充在合适**dwSize** DD 中的值\_MORESURFACECAPS 结构。 值**dwSize**以这种方式计算：

```cpp
DDMORESURFACECAPS.dwSize = 
          (DWORD) (sizeof(DDMORESURFACECAPS) 
        + (((signed int)DDHALINFO.vmiData.dwNumHeaps) - 1) 
        * sizeof(DDSCAPSEX)*2 );
```

请注意该减去 1 的值从**dwNumHeaps**是所需帐户这一事实， [ **DD\_MORESURFACECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff551659)结构具有**ddsExtendedHeapRestrictions**是一个元素的数组的成员。 只有那些后第一个数组元素 (即，从<strong>ddsExtendedHeapRestrictions\[</strong>1<strong>\]</strong>上) 应在计算 DD的总大小计\_MORESURFACECAPS 结构。

**DdsCapsEx**并**ddsCapsExAlt**成员它们完全等同于**ddsCaps**并**ddsCapsAlt** 数组的成员[**VIDEOMEMORY** ](https://msdn.microsoft.com/library/windows/hardware/ff570171)中返回的结构**pvmList**隶属[ **VIDEOMEMORYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff570172)结构，它包含的成员作为[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)结构。 在中设置任何位**ddsCapsEx**意味着与该图面，位集不能放置在该堆中。 在中设置任何位**ddsCapsExAlt**成员意味着，不能在图面放在该堆。 首次分配图面，DirectDraw 通过所有堆时，如果发现任何堆中的任何功能位用于**ddsCaps**表面的 DDSCAPS 位 VIDEOMEMORY 结构匹配的成员，它会分配该堆中的图面。 如果此阶段中不找到任何此类堆，则 DirectDraw 使检查但相同的 pass **ddsCapsEx**字段。 如果此阶段中未能找到任何堆，则不能在任何堆中创建在图面。

 

 





