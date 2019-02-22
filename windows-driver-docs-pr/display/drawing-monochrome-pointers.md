---
title: 绘制单色指针
description: 绘制单色指针
ms.assetid: b3e436d2-b804-42fb-89ca-ecf66dcb584e
keywords:
- 显示绘图指针 WDK Windows 2000
- 显示驱动程序 WDK Windows 2000 中，指针
- 显示指针 WDK Windows 2000
- 单色指针 WDK Windows 2000 显示
- 黑白指针 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c24695499781b378d0a57e6c045c786ab53d075f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544815"
---
# <a name="drawing-monochrome-pointers"></a>绘制单色指针


## <span id="ddk_drawing_monochrome_pointers_gg"></span><span id="DDK_DRAWING_MONOCHROME_POINTERS_GG"></span>


单色位图包含两个部分： 第一个定义指针; AND 掩码第二个定义 XOR 掩码。 结合这些掩码提供的每个像素的指针图像信息的两个位。 下表描述了为在和中所示的值显示的结果和 XOR 掩码。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">和掩码值</th>
<th align="left">XOR 掩码值</th>
<th align="left">显示的结果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>像素是黑色</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>像素的白色</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>像素保持不变 （透明）</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>反转像素颜色</p></td>
</tr>
</tbody>
</table>

 

此位图定义和使用情况提供黑白图像，同时为透明度和反转像素组成指针提供支持。

 

 





