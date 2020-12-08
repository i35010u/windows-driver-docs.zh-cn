---
title: W 缓冲
description: W 缓冲
keywords:
- Direct3D WDK Windows 2000 显示，w-缓冲
- w-缓冲 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25ef63483971f4f68631e0b2f93e8262add79991
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806317"
---
# <a name="w-buffering"></a>W 缓冲


## <span id="ddk_w_buffering_gg"></span><span id="DDK_W_BUFFERING_GG"></span>


通常，z 缓冲在 z 缓冲区中使用透视正确的 *z* 进行深度比较和存储，因为这是一个 z，光栅器迭代器必须生成该 *z* 才能维护平面多边形。 某些实现可以通过用表示为 *w* 或 *z* 的深度信息填充 z 缓冲区来执行隐藏的图面消除法。 这就是所谓的 w 缓冲。 这可以通过以下方式实现：将经典转换和 lit 顶点结构中指定的顶点 1/w 项线性插入 (TLVERTEX) ，计算每个像素的倒数，然后将此 *w* 值用于深度比较并有条件地将其存储到深度缓冲区。 有关 TLVERTEX 的详细信息，请参阅 Direct3D SDK 文档。

通常，硬件会在缓冲区中存储浮点值。 以下是常见的精度格式：

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
<td align="left"><p>24位</p></td>
<td align="left"><p>不含低字节尾数的 IEEE 单精度浮点数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>32 位</p></td>
<td align="left"><p>标准 IEEE 单精度浮点型。</p></td>
</tr>
</tbody>
</table>

 

传统的 z 缓冲是针对使用 CAD 或创作工具的技术市场开发的，其中，查看卷/工作区的范围是已知的且有限的。 因此，存储的深度值范围可以是有限的，因此，最远/接近 (的距离与远处和附近的修剪面) 会按2到10的顺序排列。

为此类应用程序设计的典型硬件会循环访问正确的 z，并将其直接存储到 z 缓冲区。 由于涉及到数学，因此不会在 z 缓冲范围内均匀分布这种透视正确的 z。 使用最远/接近于100的比率会导致在场景深度范围的前10% 上使用的深度缓冲区范围90%。 虽然这对于工具来说是足够的，但对于带外场景的娱乐或视觉模拟的典型应用程序，在1000到1或10000到1之间的比率非常接近。 在1000到1的 r 中，在深度的前两个百分比使用范围的98%。 这可能会导致在远处对象中出现隐藏面项目，尤其是在使用16位深度缓冲时。

相反，当使用 *w* (或眼睛相关 *z*) 时，可以在世界空间中的最远和远处剪裁平面之间更均匀地分配缓冲区位。 主要优势在于，从远处到接近的比率不再是问题，因此，应用程序能够支持最大的英里数，但仍能在眼睛的英寸范围内获得合理的准确深度缓冲。

 

 





