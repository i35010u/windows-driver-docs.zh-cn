---
title: 扩展堆限制
description: 扩展堆限制
ms.assetid: 4f907768-670a-4ce5-b2d7-7af27baf80da
keywords:
- 绘制扩展 surface 功能 WDK DirectDraw，堆
- DirectDraw 扩展 surface 功能 WDK Windows 2000 显示，堆
- 扩展 surface 功能 WDK DirectDraw，堆
- 堆 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9aec16a9aae9e3161b86a01b0db162c233390ee0
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423658"
---
# <a name="extended-heap-restrictions"></a>扩展堆限制


## <span id="ddk_extended_heap_restrictions_gg"></span><span id="DDK_EXTENDED_HEAP_RESTRICTIONS_GG"></span>


[**DD \_ MORESURFACECAPS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_moresurfacecaps)结构的大小是可变的。 它始终具有 **ddsCapsMore** 成员，但它可能有零个或多个 **ddsExtendedHeapRestrictions** 条目。 如果驱动程序响应 GUID \_ DDMoreSurfaceCaps 查询，则它应返回一个 dd \_ MORESURFACECAPS 结构，该结构包含的 **ddsExtendedHeapRestrictions** 条目数量与 [**dd \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-dd_halinfo) 结构中的显示内存堆相同 (DirectDraw 保证在 \_ 驱动程序报告 dd DDMoreSurfaceCaps 后执行 GUID HALINFO 查询 \_ 。 ) 

驱动程序还应在 DD MORESURFACECAPS 结构中填写适当的 **dwSize** 值 \_ 。 按以下方式计算 **dwSize** 的值：

```cpp
DDMORESURFACECAPS.dwSize = 
          (DWORD) (sizeof(DDMORESURFACECAPS) 
        + (((signed int)DDHALINFO.vmiData.dwNumHeaps) - 1) 
        * sizeof(DDSCAPSEX)*2 );
```

请注意，必须从 **dwNumHeaps** 的值中减去1，才能考虑 [**DD \_ MORESURFACECAPS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_moresurfacecaps) 结构具有作为单元素数组的 **ddsExtendedHeapRestrictions** 成员这一事实。 只有第一个 (后面的数组元素（从) 中<strong>的 \[ ddsExtendedHeapRestrictions</strong>1 开始）才能 <strong>\]</strong> 计算 DD MORESURFACECAPS 结构的总大小 \_ 。

**DdsCapsEx**和**ddsCapsExAlt**成员与[**VIDEOMEMORY 结构的**](/windows/win32/api/ddrawint/ns-ddrawint-videomemoryinfo) **pvmList**成员中返回的[**VIDEOMEMORYINFO**](/windows/win32/api/ddrawint/ns-ddrawint-videomemory)结构数组的**ddsCaps**和**ddsCapsAlt**成员完全相似，后者包含为[**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-dd_halinfo)结构的成员。 在 **ddsCapsEx** 中设置的任何位都是指具有该位集的图面不得放置在该堆中。 **DdsCapsExAlt**成员中设置的任何位均表示该曲面不能放置在此堆中。 分配表面时，DirectDraw 首先传递所有堆，如果它找到了 VIDEOMEMORY 结构的 **ddsCaps** 成员中没有功能位与图面的 ddsCaps 位匹配的任何堆，则将在该堆中分配该图面。 如果此传递未找到此类堆，则 DirectDraw 将进行相同的传递，但会检查 **ddsCapsEx** 字段。 如果此传递无法找到任何堆，则无法在任何堆中创建该图面。

 

