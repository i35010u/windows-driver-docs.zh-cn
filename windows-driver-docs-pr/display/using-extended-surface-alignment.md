---
title: 使用扩展图面对齐
description: 使用扩展图面对齐
ms.assetid: ae4a6820-b9be-4dd2-95d8-6030b3b63826
keywords:
- 绘制扩展 WDK DirectDraw 图面上对齐
- DirectDraw 扩展图面上的对齐方式 WDK Windows 2000 显示
- WDK DirectDraw，扩展对齐方式的图面
- 扩展 WDK DirectDraw 图面上对齐
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 558476c8d9962edba606a6b1e2f0ba8c523ffd9d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370617"
---
# <a name="using-extended-surface-alignment"></a>使用扩展图面对齐


## <span id="ddk_using_extended_surface_alignment_gg"></span><span id="DDK_USING_EXTENDED_SURFACE_ALIGNMENT_GG"></span>


若要启用扩展的图面上对齐功能，DirectDraw 驱动程序必须在初始化时执行以下任务：

-   该驱动程序必须指定[ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)函数，在[ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构 DirectDraw 可若要获取的其他信息的调用。

-   *DdGetDriverInfo*回调调用时所使用 GUID\_GetHeapAlignment GUID 指定。 该驱动程序必须填写[ **DD\_GETHEAPALIGNMENTDATA** ](https://docs.microsoft.com/windows/desktop/api/dmemmgr/ns-dmemmgr-_dd_getheapalignmentdata)结构，然后将复制到此结构**lpvData**隶属[ **DD\_GETDRIVERINFODATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)结构。

该驱动程序应填写[ **DDSCAPS** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))结构指向在[ **HEAPALIGNMENT** ](https://docs.microsoft.com/windows/desktop/api/dmemmgr/ns-dmemmgr-_heapalignment)结构与逻辑或的 DDSCAPS\_xxxx 标志为任何类型的图面，需要在此堆中的对齐方式。 如果设置 DDSCAPS 中的一位，则表示在相应的对齐方式限制 DirectDraw 遵守规定[ **SURFACEALIGNMENT** ](https://docs.microsoft.com/windows/desktop/api/dmemmgr/ns-dmemmgr-_surfacealignment)结构成员。 DDSCAPS\_翻转位并**FlipTarget**成员不适用于图面，将返回缓冲区中主翻转链接，即，有可能主要 （可见） 的图面。 以下列表显示当前允许的图面可以指定的对齐方式的功能集：

-   DDSCAPS\_OFFSCREENPLAIN

-   DDSCAPS\_EXECUTEBUFFER

-   DDSCAPS\_覆盖

-   DDSCAPS\_纹理

-   DDSCAPS\_ZBUFFER

-   DDSCAPS\_ALPHA

-   DDSCAPS\_FLIP

**请注意**  针对中的条目的新表面的功能进行了比较 DirectDraw [ **HEAPALIGNMENT** ](https://docs.microsoft.com/windows/desktop/api/dmemmgr/ns-dmemmgr-_heapalignment)结构中指定它们的顺序。 例如，图面与 DDSCAPS\_MIPMAP |DDSCAPS\_纹理 |DDSCAPS\_翻转集对齐根据**纹理**HEAPALIGNMENT 的成员结构，因为这是一种对齐方式是指定的位的第一个适用功能 (即， **纹理**出现前**FlipTarget** HEAPALIGNMENT 结构中)。 **FlipTarget**在此示例中不被视为成员。 因为主翻转链中的后台缓冲区都标有 DDSCAPS\_翻转，并可以为其指定一种对齐方式的任何其他位，此类面对齐根据**FlipTarget**成员。 图面，可能无法成为主翻转链 （拥有相同的像素格式和作为主表面的大小） 的成员还根据对齐**FlipTarget**成员。

 

 

 





