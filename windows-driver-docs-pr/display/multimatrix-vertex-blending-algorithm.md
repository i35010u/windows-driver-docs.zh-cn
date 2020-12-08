---
title: 多矩阵顶点混合算法
description: 多矩阵顶点混合算法
keywords:
- multimatrix 顶点混合 WDK Direct3D，算法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee9a957e8809cafa8313cdd584dedc293efbdf33
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830637"
---
# <a name="multimatrix-vertex-blending-algorithm"></a>多矩阵顶点混合算法


## <span id="ddk_multimatrix_vertex_blending_algorithm_gg"></span><span id="DDK_MULTIMATRIX_VERTEX_BLENDING_ALGORITHM_GG"></span>


Multimatrix 顶点混合算法假设只使用两个矩阵。

更改矩阵时，请更新以下四个矩阵：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">矩阵</th>
<th align="left">计算</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>当前转换矩阵 (CTM) </p></td>
<td align="left"><p>CTM = WORLD * VIEW * PROJ</p></td>
</tr>
<tr class="even">
<td align="left"><p>辅助 CTM (父坐标) </p></td>
<td align="left"><p>CTM2 = WORLD1 * VIEW * PROJ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CTM 的反向换位</p></td>
<td align="left"><p>ITCTM = (CTM<sup>T</sup>) ⁻¹</p></td>
</tr>
<tr class="even">
<td align="left"><p>如果照明) ，则需要反向 CTM2 (</p></td>
<td align="left"><p>ITCTM2 = (CTM2<sup>T</sup>) ⁻¹</p></td>
</tr>
</tbody>
</table>

 

在某些情况下，最好先使用顶点的权重来混合矩阵，然后再执行一次 (matrix) X (顶点) 相乘。

 

 





