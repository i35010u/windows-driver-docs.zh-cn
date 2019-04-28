---
title: XR 布局
description: XR 布局
ms.assetid: a5c5d627-8d1a-4091-a7b2-893165e7fe45
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示 XR 布局
- 扩展的格式 WDK Windows 7 显示，XR 布局
- XR 布局 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd57d97309dc269986cd3571215a3f1d1a920d06
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340064"
---
# <a name="xr-layout"></a>XR 布局


本部分仅适用于 Windows 7 和更高版本的操作系统。

XR 是定点 1.9 格式。 值偏差为-0.5，这会导致的动态范围大约\[-0.5,1.5\]。 固定的点表示形式表示小数位数为 2 倍，若要切换到右的小数点的一个位置。

每个 XR 元素占用一个 32 位 DWORD，而不考虑主机 CPU 字节顺序下表中所示的布局方式。

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
<th align="left">位 19:10</th>
<th align="left">9:0 位</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Alpha 通道</p></td>
<td align="left"><p>蓝色通道</p></td>
<td align="left"><p>绿色通道</p></td>
<td align="left"><p>红色通道</p></td>
</tr>
</tbody>
</table>

 

下表中所示，每个红色、 绿色和蓝色通道的布局方式。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">9 位</th>
<th align="left">8:0 位</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1 位整数部分</p></td>
<td align="left"><p>9 位小数部分</p></td>
</tr>
</tbody>
</table>

 

 

 





