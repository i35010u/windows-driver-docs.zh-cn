---
title: 句柄分配示例
description: 句柄分配示例
keywords:
- 多头硬件 WDK DirectX 9.0，处理分配
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84e624adce8462e62617ca78aac22594e8cd7748
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838305"
---
# <a name="example-of-handle-assignments"></a>句柄分配示例


## <span id="ddk_example_of_handle_assignments_gg"></span><span id="DDK_EXAMPLE_OF_HANDLE_ASSIGNMENTS_GG"></span>


下表显示了通过 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)) 提供的 Direct3D 句柄值的示例布局，这些 (值可能出现在两个 head 方案中。 每个头的正面、背面和深度/模具表面都具有唯一的句柄;主头必须与所有这些句柄一起使用。 主头拥有所有纹理、顶点缓冲区和索引缓冲区图面;这些表面的句柄仅在主头上创建。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主头句柄值</th>
<th align="left">从属头句柄值</th>
<th align="left">Surface</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"></td>
<td align="left"><p>Master 的前台缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"></td>
<td align="left"><p>Master 的后台缓冲区</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"></td>
<td align="left"><p>Master 的深度缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>3</p></td>
<td align="left"><p>从属缓存前台</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>4</p></td>
<td align="left"><p>从属的后台缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>5</p></td>
<td align="left"><p>从属的深度缓冲区</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"></td>
<td align="left"><p>主节点的纹理1</p></td>
</tr>
<tr class="even">
<td align="left"><p>7</p></td>
<td align="left"></td>
<td align="left"><p>主节点的纹理2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"></td>
<td align="left"><p>主节点的纹理3</p></td>
</tr>
</tbody>
</table>

 

 

