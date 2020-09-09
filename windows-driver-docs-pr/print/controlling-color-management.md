---
title: 控制颜色管理
description: 控制颜色管理
ms.assetid: cb210b8d-fee1-4904-8c50-f03d2445085e
keywords:
- 颜色管理 WDK 打印，控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a6891fd7149d1bd3f7efeae95845a29b1085a7c
ms.sourcegitcommit: 51cba71be022c726c04c29ba5c0360860b65d7a4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89562217"
---
# <a name="controlling-color-management"></a>控制颜色管理





打印机的颜色管理可由应用程序、系统 (GDI) 、驱动程序或设备硬件控制。 驱动程序通过检查传递到其图形 DDI 绘图函数实现的 [**BRUSHOBJ**](/windows/win32/api/winddi/ns-winddi-brushobj) 和 [**XLATEOBJ**](/windows/win32/api/winddi/ns-winddi-xlateobj) 结构中的标志，来确定哪个组件正在管理颜色更正。 定义以下标志：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BRUSHOBJ 中的 BR_DEVICE_ICM</p>
<p>XLATEOBJ 中的 XO_DEVICE_ICM</p></td>
<td><p>驱动程序或设备正在执行颜色管理。</p></td>
</tr>
<tr class="even">
<td><p>BRUSHOBJ 中的 BR_HOST_ICM</p>
<p>XLATEOBJ 中的 XO_HOST_ICM</p></td>
<td><p>应用程序或系统 (GDI) 正在执行颜色管理。</p></td>
</tr>
</tbody>
</table>

 

以下主题介绍了这些颜色管理方案的驱动程序支持：

[系统控制](system-control.md)

[驱动程序控制和设备控制](driver-control-and-device-control.md)

[支持 CMYK 色彩空间](supporting-cmyk-color-space.md)

[JPEG 和 PNG 图像的颜色管理](color-management-of-jpeg-and-png-images.md)

 

