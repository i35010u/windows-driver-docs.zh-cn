---
title: W 缓冲
description: W 缓冲
ms.assetid: 0f06a709-11dc-4407-a230-85a689fb46a2
keywords:
- Direct3D WDK Windows 2000 显示、 w 缓冲
- w 缓冲 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b07bc74ff476fe67d0e02bf009d754b1dbe13a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391205"
---
# <a name="w-buffering"></a>W 缓冲


## <span id="ddk_w_buffering_gg"></span><span id="DDK_W_BUFFERING_GG"></span>


通常情况下，z 缓冲使用透视校正*z*深度比较和 z 缓冲区中的存储，由于此值是*z*光栅器迭代器必须生成以维护平面多边形。 某些实现可以通过用深度信息表示为填充 z 缓冲区来执行隐藏图面上消除*w*，或*z*相对于密切关注。 这是什么方式被称为 w 缓冲。 这可以通过在经典的已转换和亮起顶点结构 (TLVERTEX) 中指定的顶点 1/w 术语线性插值计算每个像素，其倒数并使用此*w*深度比较的值和有条件地将其存储到深度缓冲区。 有关 TLVERTEX 的详细信息，请参阅 Direct3D SDK 文档。

通常情况下，硬件将浮点值存储在缓冲区中。 以下精度格式是常见：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">大小</th>
<th align="left">格式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>16 位</p></td>
<td align="left"><p>12.4</p></td>
</tr>
<tr class="even">
<td align="left"><p>24 位</p></td>
<td align="left"><p>带尾数没有低字节 IEEE 单精度浮点数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>32 位</p></td>
<td align="left"><p>标准 IEEE 单精度浮点数。</p></td>
</tr>
</tbody>
</table>

 

传统的 z 缓冲是针对使用 CAD 或创作工具，在其中查看卷/工作区是已知和有限范围的技术市场开发。 因此一定程度上允许的远端/附近比率 （距离最和剪辑平面附近） 会达到大约两到十台可以是存储的深度值的范围。

专门针对此类应用程序的典型硬件迭代角度来看更正 z，并将其存储到 z 缓冲区直接。 由于所涉及的数学原理，此透视更正 z 不均匀 z 缓冲区范围内。 在 90%的使用场景深度范围的第一个 10%的深度缓冲区范围中使用 100 条结果远端/附近的比率。 尽管这可能是足够的工具，用于娱乐或与外部场景 visual 模拟典型应用程序都要求 1000年到 1 或 1 到 10000 的远端/附近比率。 在 1 到 1000年的比率，98%的范围使用第一个的两个 %的深度。 这会导致隐藏图面上的项目中存有一定距离的对象，尤其是在使用 16 位深度缓冲区。

与此相反，当*w* (或关注相对*z*) 使用，则 bits 可以近和远剪辑之间更均匀地分配的缓冲区平面在世界空间中。 主要好处是的比率太不久不再是问题，从而允许应用程序支持最大范围的英里，但仍获得相当准确深度缓冲内英寸的关注点。

 

 





