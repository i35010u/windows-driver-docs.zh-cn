---
title: 多矩阵顶点混合算法
description: 多矩阵顶点混合算法
ms.assetid: 78ea0a92-a026-4c8d-a0ff-8be17b0a6424
keywords:
- multimatrix 顶点混合 WDK Direct3D 算法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6588bb880f2bca199fc33e9f27c001e0c6c7d32
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565240"
---
# <a name="multimatrix-vertex-blending-algorithm"></a>多矩阵顶点混合算法


## <span id="ddk_multimatrix_vertex_blending_algorithm_gg"></span><span id="DDK_MULTIMATRIX_VERTEX_BLENDING_ALGORITHM_GG"></span>


Multimatrix 顶点混合算法假定正在使用仅两个矩阵。

在矩阵更改更新以下四个矩阵：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Matrix</th>
<th align="left">计算</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>当前转换矩阵 (CTM)</p></td>
<td align="left"><p>CTM = WORLD * 视图 * PROJ</p></td>
</tr>
<tr class="even">
<td align="left"><p>辅助 CTM （父坐标表示）</p></td>
<td align="left"><p>CTM2 = WORLD1 * 视图 * PROJ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTM 反转置</p></td>
<td align="left"><p>ITCTM = (CTM<sup>T</sup>)⁻¹</p></td>
</tr>
<tr class="even">
<td align="left"><p>CTM2 （照明时需要） 的反向转置</p></td>
<td align="left"><p>ITCTM2 = (CTM2<sup>T</sup>) ⁻¹</p></td>
</tr>
</tbody>
</table>

 

在某些情况下，它可能是一种更高效，blend 矩阵第一种使用顶点的权重，然后进行只有一个 （matrix)X(vertex) 乘法。

 

 





