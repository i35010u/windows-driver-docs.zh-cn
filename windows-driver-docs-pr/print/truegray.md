---
title: TrueGray
description: TrueGray
keywords:
- 微型驱动程序 WDK Pscript，TrueGray 功能
- TrueGray 功能
- RGB 颜色 WDK 打印机
- 灰色颜色空间 WDK Pscript
- ADTrueGray
- 颜色检查 WDK Pscript
- 检查 RGB 颜色
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a36ef2f47308e29ea2aecee35d3e4555b283ac8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788253"
---
# <a name="truegray"></a>TrueGray





TrueGray 功能检查文本和矢量图形中的 RGB 颜色，但不检查位图中的颜色。 对于灰色 (颜色，其红色、绿色和蓝色值相等) ，TrueGray 功能在打印前将颜色从 RGB 颜色空间转换为彩色打印机的灰色颜色空间。 此功能不适用于单色打印机。

TrueGray 功能使用私有 *PPD* 关键字 \* **ADTrueGray**，以允许 PScript 微型驱动程序编写器启用或禁用此功能。

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
<td><p><em><strong>ADTrueGray</strong>： True</p></td>
<td><p>默认情况下，此打印机已启用 TrueGray 功能。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ADTrueGray </strong> ： False</p></td>
<td><p>默认情况下，此打印机已禁用 TrueGray 功能。</p></td>
</tr>
</tbody>
</table>

 

当用户界面指示已启用 TrueGray 功能时，驱动程序将检测到 RGB 颜色（R = G = B），并满足以下条件之一：

-   当 ICM 处理关闭时

-   当主机上执行 ICM 处理并且目标颜色配置文件为 RGB 数据时，转换后的颜色为 R ' = G ' = B ' (，这不同于原始颜色) 

-   通常使用基于 CIE 的颜色空间完成 ICM 处理并且原始颜色为 R = G = B 时

不会尝试检测 CMYK 颜色中的灰色。 这是在主机上执行 ICM 颜色处理时通常使用的颜色空间。

 

 




