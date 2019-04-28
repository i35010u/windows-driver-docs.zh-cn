---
title: FIX 坐标
description: FIX 坐标
ms.assetid: dfa5c61f-9464-4c63-998e-7fee21cfd278
keywords:
- 图面协商 WDK GDI，修复坐标
- 小数坐标 WDK GDI
- 修复协调 WDK GDI
- 贝塞尔曲线 WDK GDI
- 行 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 588dbdfa8a62c2de5994cefe29049184872e038b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327912"
---
# <a name="fix-coordinates"></a>FIX 坐标


## <span id="ddk_fix_coordinates_gg"></span><span id="DDK_FIX_COORDINATES_GG"></span>


图形 DDIs 使用小数部分可以指定一个第十六个像素的内的设备表面的位置的坐标。 （矢量设备上的小数部分的坐标是比设备分辨率十六倍更准确。）小数部分的坐标表示为 32 位有符号 28.4 位修复表示法中的数字。 在此表示法，最高序 28 位表示的坐标的整数部分和最低 4 位表示小数部分。 例如，0x0000003C 等于 +3.7500 和 0xFFFFFFE8 等于-1.5000。

修复坐标表示控点的直线和贝塞尔曲线。 对于某些对象，例如矩形的剪辑区域 GDI 使用有符号的 32 位整数来表示坐标。 坐标是 28 位数量，因为整数坐标的最高 5 位均为清除所有设置。

 

 





