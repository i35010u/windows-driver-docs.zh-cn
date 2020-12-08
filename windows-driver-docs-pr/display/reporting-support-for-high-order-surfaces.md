---
title: 报告高阶图面的支持
description: 报告高阶图面的支持
keywords:
- DirectX 8.0 发行说明了 WDK Windows 2000 显示、高顺序曲面、报告支持
- 高顺序图面 WDK DirectX 8.0，报告支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25b091e730895cddfd75f00ba385abbe26b20f8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786871"
---
# <a name="reporting-support-for-high-order-surfaces"></a>报告高阶图面的支持


## <span id="ddk_reporting_support_for_high_order_surfaces_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_HIGH_ORDER_SURFACES_GG"></span>


驱动程序使用 D3DCAPS8 结构的 **DevCaps** 字段中的四个新功能位报告其对高顺序曲面的支持。 这些标志如下所示：

### <a name="span-idd3ddevcaps_quinticrtpatchesspanspan-idd3ddevcaps_quinticrtpatchesspand3ddevcaps_quinticrtpatches"></a><span id="d3ddevcaps_quinticrtpatches"></span><span id="D3DDEVCAPS_QUINTICRTPATCHES"></span>D3DDEVCAPS \_ QUINTICRTPATCHES

设备支持 quintic béziers 和 B 样条。

### <a name="span-idd3ddevcaps_rtpatchesspanspan-idd3ddevcaps_rtpatchesspand3ddevcaps_rtpatches"></a><span id="d3ddevcaps_rtpatches"></span><span id="D3DDEVCAPS_RTPATCHES"></span>D3DDEVCAPS \_ RTPATCHES

设备支持矩形和三角修补程序。

### <a name="span-idd3ddevcaps_rtpatchhandlezerospanspan-idd3ddevcaps_rtpatchhandlezerospand3ddevcaps_rtpatchhandlezero"></a><span id="d3ddevcaps_rtpatchhandlezero"></span><span id="D3DDEVCAPS_RTPATCHHANDLEZERO"></span>D3DDEVCAPS \_ RTPATCHHANDLEZERO

如果设置了此设备功能，则硬件体系结构不需要缓存任何信息，也不需要缓存 (句柄零) 的未缓存修补程序与缓存的修补程序有效。 请注意，D3DDEVCAPS \_ RPATCHHANDLERZERO 并不意味着可以绘制句柄为零的修补程序。 无论是否设置了此上限，都可以始终绘制句柄零修补程序。

### <a name="span-idd3ddevcaps_npatchesspanspan-idd3ddevcaps_npatchesspand3ddevcaps_npatches"></a><span id="d3ddevcaps_npatches"></span><span id="D3DDEVCAPS_NPATCHES"></span>D3DDEVCAPS \_ NPATCHES

设备支持 n-修补程序。

 

 





