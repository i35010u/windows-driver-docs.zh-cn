---
title: 报告高阶图面的支持
description: 报告高阶图面的支持
ms.assetid: cf214ed7-2c06-4dc6-8c73-c2a3f51332ab
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，请报告支持的高顺序应用层
- 靠前的图面 WDK DirectX 8.0，reporting 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 633b7d35177d76c9092c8eef1e4bc0f0aff0c120
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383249"
---
# <a name="reporting-support-for-high-order-surfaces"></a>报告高阶图面的支持


## <span id="ddk_reporting_support_for_high_order_surfaces_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_HIGH_ORDER_SURFACES_GG"></span>


驱动程序报告其支持对于使用中的四个新功能位的高顺序图面**DevCaps** D3DCAPS8 结构的字段。 这些标志如下所示：

### <a name="span-idd3ddevcapsquinticrtpatchesspanspan-idd3ddevcapsquinticrtpatchesspand3ddevcapsquinticrtpatches"></a><span id="d3ddevcaps_quinticrtpatches"></span><span id="D3DDEVCAPS_QUINTICRTPATCHES"></span>D3DDEVCAPS\_QUINTICRTPATCHES

设备支持 quintic béziers 和 B 样条。

### <a name="span-idd3ddevcapsrtpatchesspanspan-idd3ddevcapsrtpatchesspand3ddevcapsrtpatches"></a><span id="d3ddevcaps_rtpatches"></span><span id="D3DDEVCAPS_RTPATCHES"></span>D3DDEVCAPS\_RTPATCHES

设备支持矩形和三角形的修补程序。

### <a name="span-idd3ddevcapsrtpatchhandlezerospanspan-idd3ddevcapsrtpatchhandlezerospand3ddevcapsrtpatchhandlezero"></a><span id="d3ddevcaps_rtpatchhandlezero"></span><span id="D3DDEVCAPS_RTPATCHHANDLEZERO"></span>D3DDEVCAPS\_RTPATCHHANDLEZERO

当此设备功能设置了、 硬件体系结构不需要缓存的任何信息有效缓存的绘制未缓存的修补程序 （处理零）。 请注意该 D3DDEVCAPS\_RPATCHHANDLERZERO 并不意味着可以绘制句柄为零的修补程序。 此最大值或不设置是否始终可绘制句柄零修补程序。

### <a name="span-idd3ddevcapsnpatchesspanspan-idd3ddevcapsnpatchesspand3ddevcapsnpatches"></a><span id="d3ddevcaps_npatches"></span><span id="D3DDEVCAPS_NPATCHES"></span>D3DDEVCAPS\_NPATCHES

设备支持 n 修补程序。

 

 





