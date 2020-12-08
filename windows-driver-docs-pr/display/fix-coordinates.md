---
title: FIX 坐标
description: FIX 坐标
keywords:
- surface 协商 WDK GDI，修复坐标
- 分数协调 WDK GDI
- 修复协调 WDK GDI
- 贝塞尔曲线 WDK GDI
- 线条 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f7a47a9d395207d410a4d0fdd1fe5adadc7d41f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838079"
---
# <a name="fix-coordinates"></a>FIX 坐标


## <span id="ddk_fix_coordinates_gg"></span><span id="DDK_FIX_COORDINATES_GG"></span>


图形 DDIs 使用小坐标，可以在一个像素的第16部分中指定设备图面上的位置。  (在矢量设备上，小数位坐标比设备分辨率要精确得多十六倍。 ) 分数坐标以签名的28.4 位修复表示法形式表示为32位数字。 在此表示法中，最高序位28位表示坐标的整数部分，最低4位表示小数部分。 例如，0x0000003C 等于 + 3.7500，0xFFFFFFE8 等于-1.5000。

修复坐标表示线条和贝塞尔曲线的控制点。 对于某些对象，如矩形剪辑区域，GDI 使用已签名的32位整数表示坐标。 因为坐标是28位的数量，所以整数坐标的最大5位全部为清除或全部设置。

 

 





