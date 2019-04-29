---
title: 句柄分配示例
description: 句柄分配示例
ms.assetid: 44239e13-ebe7-48c4-83b2-40f603dc1c98
keywords:
- 多个头硬件 WDK DirectX 9.0，句柄分配
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3f708021d3e47b490be44fc2bf200f3f8bd991b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365943"
---
# <a name="example-of-handle-assignments"></a>句柄分配示例


## <span id="ddk_example_of_handle_assignments_gg"></span><span id="DDK_EXAMPLE_OF_HANDLE_ASSIGNMENTS_GG"></span>


下表显示了 Direct3D 句柄值的示例排列方式 (通过提供[ **D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840))，可能会出现在两个头方案。 所有每个标头的前端、 后和深度/模具表面具有唯一的句柄;主头必须使用所有这些句柄。 主头拥有所有纹理、 顶点缓冲区和索引缓冲区曲面。主头只能创建这些图面的句柄。

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
<td align="left"><p>主机的前台缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"></td>
<td align="left"><p>后台缓冲区用于 master</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"></td>
<td align="left"><p>Master 的深度缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>3</p></td>
<td align="left"><p>对于从属前台缓冲区</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>4</p></td>
<td align="left"><p>后台缓冲区用于从属项</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>5</p></td>
<td align="left"><p>从属的深度缓冲区</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"></td>
<td align="left"><p>纹理 1 主机</p></td>
</tr>
<tr class="even">
<td align="left"><p>7</p></td>
<td align="left"></td>
<td align="left"><p>纹理 2 主机</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"></td>
<td align="left"><p>纹理 3 主机</p></td>
</tr>
</tbody>
</table>

 

 

 





