---
title: 使用扩展图面对齐
description: 使用扩展图面对齐
ms.assetid: ae4a6820-b9be-4dd2-95d8-6030b3b63826
keywords:
- 绘制扩展图面对齐 WDK DirectDraw
- DirectDraw 扩展图面对齐 WDK Windows 2000 显示器
- surface DirectDraw，扩展对齐
- 扩展的图面对齐 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e662531f492283ea3106121d288511e1ed0138cf
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717566"
---
# <a name="using-extended-surface-alignment"></a>使用扩展图面对齐


## <span id="ddk_using_extended_surface_alignment_gg"></span><span id="DDK_USING_EXTENDED_SURFACE_ALIGNMENT_GG"></span>


若要启用扩展的图面对齐功能，DirectDraw 驱动程序必须在初始化时执行以下任务：

-   驱动程序必须在[**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_halinfo)结构中指定[**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)函数，而 DirectDraw 可以调用该函数以获取其他信息。

-   用指定的 GUID GetHeapAlignment GUID 调用 *DdGetDriverInfo* 回调 \_ 。 驱动程序必须填写[**dd \_ GETHEAPALIGNMENTDATA**](/windows/win32/api/dmemmgr/ns-dmemmgr-_dd_getheapalignmentdata)结构，然后将该结构复制到[**Dd \_ GETDRIVERINFODATA**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)结构的**lpvData**成员。

对于需要在此堆中进行对齐的任何类型的图面，驱动程序应填写[**HEAPALIGNMENT**](/windows/win32/api/dmemmgr/ns-dmemmgr-_heapalignment)结构中指向的[**DDSCAPS**](/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))结构，并为其提供 DDSCAPS XXXX 标志的逻辑或 \_ 。 如果设置了 DDSCAPS 中的某个位，则 DirectDraw 会按相应 [**SURFACEALIGNMENT**](/windows/win32/api/dmemmgr/ns-dmemmgr-_surfacealignment) 结构成员中表示的对齐限制来遵守美国。 "DDSCAPS \_ 翻转位" 和 " **FlipTarget** " 成员应用于在主翻转链中为后台缓冲区的曲面，即，可能的主 (可见) 图面。 以下列表显示了当前允许为其指定对齐方式的一组 surface 功能：

-   DDSCAPS \_ OFFSCREENPLAIN

-   DDSCAPS \_ EXECUTEBUFFER

-   DDSCAPS \_ 覆盖

-   DDSCAPS \_ 纹理

-   DDSCAPS \_ ZBUFFER

-   DDSCAPS \_ ALPHA

-   DDSCAPS \_ 翻转

**注意**   DirectDraw 会按照指定的顺序对[**HEAPALIGNMENT**](/windows/win32/api/dmemmgr/ns-dmemmgr-_heapalignment)结构中的条目进行比较。 例如，使用 DDSCAPS MIPMAP 的图面 \_ |DDSCAPS \_ 纹理 |DDSCAPS \_ 翻转集根据 HEAPALIGNMENT 结构的 **纹理** 成员对齐，因为这是指定了对齐方式的第一个适用的功能位 (即， **纹理** 显示在 HEAPALIGNMENT 结构) 中的 **FlipTarget** 之前。 在此示例中，不考虑 **FlipTarget** 成员。 因为主翻转链中的后台缓冲区标记有 DDSCAPS \_ 反向，并且没有另一个可指定对齐的其他位，所以，此类面根据 **FlipTarget** 成员对齐。 可能会成为主翻转链的成员的图面（ (与主表面相同的像素格式和大小相同的图面) 也会根据 **FlipTarget** 成员对齐。

 

 

