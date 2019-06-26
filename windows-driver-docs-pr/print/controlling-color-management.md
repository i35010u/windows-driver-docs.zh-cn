---
title: 控制颜色管理
description: 控制颜色管理
ms.assetid: cb210b8d-fee1-4904-8c50-f03d2445085e
keywords:
- 颜色管理 WDK 打印控制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6efc0ab1515a569ab7839db5836dac80e069d53
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374665"
---
# <a name="controlling-color-management"></a>控制颜色管理





可通过应用程序、 系统 (GDI)、 驱动程序或设备硬件控制打印机的颜色管理。 该驱动程序确定哪个组件通过检查标志中的管理颜色校正[ **BRUSHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj)并[ **XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)传递给其实现图形 DDI 绘图函数的结构。 定义以下标志：

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
<td><p>在 BRUSHOBJ BR_DEVICE_ICM</p>
<p>在 XLATEOBJ XO_DEVICE_ICM</p></td>
<td><p>颜色管理是由驱动程序或设备正在执行。</p></td>
</tr>
<tr class="even">
<td><p>在 BRUSHOBJ BR_HOST_ICM</p>
<p>在 XLATEOBJ XO_HOST_ICM</p></td>
<td><p>颜色管理正在执行的应用程序或系统 (GDI)。</p></td>
</tr>
</tbody>
</table>

 

以下主题介绍了这些颜色管理方案的驱动程序支持：

[系统控制](system-control.md)

[驱动程序控制和设备控制](driver-control-and-device-control.md)

[支持 CMYK 颜色空间](supporting-cmyk-color-space.md)

[JPEG 和 PNG 图像的颜色管理](color-management-of-jpeg-and-png-images.md)

 

 




