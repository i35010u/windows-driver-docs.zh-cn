---
title: TrueGray
description: TrueGray
ms.assetid: d6fef790-79d9-4ea7-8e1d-bca8837108de
keywords:
- 微型驱动程序 WDK Pscript，TrueGray 功能
- TrueGray 功能
- RGB 颜色 WDK 打印机
- gray 颜色空间 WDK Pscript
- ADTrueGray
- 检查 WDK Pscript 的颜色
- 检查 RGB 颜色
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb50f3a47009a33b06cfb6388926557d8154ffe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384951"
---
# <a name="truegray"></a>TrueGray





TrueGray 功能检查 RGB 颜色的文本和矢量图形，但不是位图。 对于为灰色 （即，其红色、 绿色和蓝色值相等的颜色） 的颜色，TrueGray 功能将打印它们之前转换为 RGB 颜色空间中以彩色打印机灰颜色空间的颜色。 此功能不可用的单色打印机。

TrueGray 功能使用一个私有*PPD*关键字\* **ADTrueGray**，允许 PScript 微型驱动程序编写器来启用或禁用此功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>关键字和值</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>ADTrueGray</strong>:True</p></td>
<td><p>此打印机的默认情况下启用 TrueGray 功能。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ADTrueGray</strong>:False</p></td>
<td><p>默认情况下，此打印机，TrueGray 功能处于禁用状态。</p></td>
</tr>
</tbody>
</table>

 

当用户界面指示是否启用了 TrueGray 功能时，驱动程序检测到的 RGB 颜色的 R 的 = G = B，并且以下条件之一为 true:

-   当 ICM 处理处于关闭状态

-   当 ICM 处理在主机上执行和目标颜色配置文件是 RGB 数据和转换后的颜色是 R' = G = B 的 (即，不同于原始颜色)

-   通常情况下会完成 ICM 处理使用 CIE 基于颜色空间和原始颜色是 R = G = B

不会尝试检测 CMYK 颜色中的灰色。 这是正常情况下使用 ICM 颜色处理则在执行时在主机上的颜色空间。

 

 




