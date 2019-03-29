---
title: 反交错模式
description: 反交错模式
ms.assetid: 0418ab48-94f3-4914-b07a-ed22dc893544
keywords:
- 取消隔行扫描 WDK DirectX va，因此模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 621c85b229f6b57f51c778a0148962e85095545d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569285"
---
# <a name="deinterlace-modes"></a>反交错模式


## <span id="ddk_deinterlace_modes_gg"></span><span id="DDK_DEINTERLACE_MODES_GG"></span>


以下是 DDI 可以支持取消隔行扫描模式的示例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">模式</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="bob-deinterlacing.md" data-raw-source="[Bob](bob-deinterlacing.md)">Bob</a> （行加倍）</p></td>
<td align="left"><p>此模式下使用位块传输 (blt)。 此模式下应始终可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>简单切换自适应</p></td>
<td align="left"><p>两个相邻字段低动作是否为该字段中，检测到或 bobbing 如果检测到高运动的任一混合。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>动作矢量 Steered</p></td>
<td align="left"><p>动作矢量图面中的不同对象的用于内插发生之前对齐单个移动到时间轴。</p></td>
</tr>
<tr class="even">
<td align="left"><p>高级 3D 自适应</p></td>
<td align="left"><p>完成一些是专有硬件的自适应过程生成缺少的行。 该进程可能会使用多个引用示例来帮助生成缺少的行。 在过去或将来可能引用示例。 三维线性筛选属于此类别。</p></td>
</tr>
</tbody>
</table>

 

 

 





