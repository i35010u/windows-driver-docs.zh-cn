---
title: XR 布局
description: XR 布局
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，XR 布局
- 扩展格式 WDK Windows 7 显示，XR 布局
- XR 布局 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e50246ac33da1115eb91483fb24b7f06e1fd22e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839565"
---
# <a name="xr-layout"></a>XR 布局


本部分仅适用于 Windows 7 及更高版本的操作系统。

XR 是定点1.9 格式。 该值由-0.5 偏差，这会导致动态范围为大约 \[ 0.5 到 1.5 \] 。 固定点表示法表示将小数点向右移动一个位置的2倍。

每个 XR 元素都占有 1 32 位 DWORD，此 DWORD 按照下表中所示进行布局，而不考虑主机 CPU 字节序。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Bits 31:30</th>
<th align="left">Bits 29:20</th>
<th align="left">Bits 19:10</th>
<th align="left">Bits 9:0</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Alpha 通道</p></td>
<td align="left"><p>蓝通道</p></td>
<td align="left"><p>绿色通道</p></td>
<td align="left"><p>红色通道</p></td>
</tr>
</tbody>
</table>

 

每个红色、绿色和蓝色通道的布局如下表所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位9</th>
<th align="left">Bits 8:0</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1位整数部分</p></td>
<td align="left"><p>9位小数部分</p></td>
</tr>
</tbody>
</table>

 

 

 





