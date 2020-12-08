---
title: 反交错模式
description: 反交错模式
keywords:
- 取消隔行扫描 WDK DirectX VA，模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76489854559404e2ce30cc909f94159289149931
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809573"
---
# <a name="deinterlace-modes"></a>反交错模式


## <span id="ddk_deinterlace_modes_gg"></span><span id="DDK_DEINTERLACE_MODES_GG"></span>


下面是 DDI 可支持的隔行扫描模式的示例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“模式”</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="bob-deinterlacing.md" data-raw-source="[Bob](bob-deinterlacing.md)">Bob</a> (行翻倍) </p></td>
<td align="left"><p>此模式使用位块传输 (blt) 。 此模式应始终可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>简单的切换自适应</p></td>
<td align="left"><p>如果检测到此字段的低运动，则为两个相邻字段的混合，如果检测到高频动作，则为 bobbing。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>运动向量 Steered</p></td>
<td align="left"><p>图面中不同对象的运动向量用于在插值发生之前将各个运动与时间轴对齐。</p></td>
</tr>
<tr class="even">
<td align="left"><p>高级3D 自适应</p></td>
<td align="left"><p>缺少的行是通过专用于硬件的某个自适应进程生成的。 该过程可以使用多个引用示例来帮助生成缺失行。 参考示例可能在过去或将来。 三维线性筛选属于此类别。</p></td>
</tr>
</tbody>
</table>

 

 

 





