---
title: FVF 更新
description: FVF 更新
ms.assetid: 2bbcb1fd-b29f-41f4-93eb-5bd1cde9cb20
keywords:
- FVF WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66f04e47f76ccd00df6c8c06bbab5f6336092cad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383440"
---
# <a name="fvf-update"></a>FVF 更新


## <span id="ddk_fvf_update_gg"></span><span id="DDK_FVF_UPDATE_GG"></span>


FVF 代码最初定义 DirectX 6.0 现在支持在 DirectX 7.0 中的纹理坐标集的规范。

除了正常 2D 纹理，支持在 DirectX 6.0 中，DirectX 7.0 支持一维、 3 和 4 D 纹理。 此外，还可能投影纹理。 **DwVertexType**的成员[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)可以进行检查，当[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)调用，以确定每个纹理坐标集的维度。

例如，如果有五个纹理坐标集与顶点，每个这些纹理可以是一维、 二维、 三维，或 4d 和他们可能预计的纹理。 每个纹理阶段是独立的因此维度可以是不同的每组坐标。 中包含 FVF 标志的 16 位**dwVertexType**可以检查来确定的纹理坐标的维度。

纹理坐标计数是可以介于 0 到 8 个 4-位域。 这样中单词的 16 位, 给定纹理坐标集的数量。 16 位[FVF](fvf--flexible-vertex-format-.md)代码则会分配两个的位将每个每八个纹理坐标集。 纹理坐标位的含义如下所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位
<div>
 
</div>
模式</th>
<th align="left">Decimal
<div>
 
</div>
ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>00</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>二维纹理坐标对、 u （v），如下所示 DirectX 6.0</p></td>
</tr>
<tr class="even">
<td align="left"><p>01</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>三维纹理坐标三元组、 u、 v （q）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>四维纹理坐标翻 （u、 v、 w，q）</p></td>
</tr>
<tr class="even">
<td align="left"><p>11</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>一维的纹理坐标，u</p></td>
</tr>
</tbody>
</table>

 

三维纹理坐标集可用于任何三个不同的用途： 投影纹理 (由 D3DTTFF 信号\_投影-请 D3DTEXTURETRANSFORMFLAGS 参阅 DirectX SDK 文档中)，体积纹理或将向量纹理映射为多维数据集由一组呈现状态类似于 D3DRENDERSTATE\_WRAP0 到 D3DRENDERSTATE\_WRAP7 模式已指定在纹理坐标集的基础。

与 D3DRENDERSTATE 一起使用的标志\_包装*n*呈现器的状态 1d 通过 4d 纹理坐标，分别下表中所述。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flags</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DWRAPCOORD_0</p></td>
<td align="left"><p>相同 D3DWRAP_U，指定在环绕<em>u</em>协调方向。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DWRAPCOORD_1</p></td>
<td align="left"><p>相同 D3DWRAP_V，指定在环绕<em>v</em>协调方向。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DWRAPCOORD_2</p></td>
<td align="left"><p>指定在环绕<em>w</em>协调方向。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DWRAPCOORD_3</p></td>
<td align="left"><p>指定在环绕<em>q</em>协调方向。</p></td>
</tr>
</tbody>
</table>

 

使用投影的纹理时，它们需要 RHW 值相应的纹理坐标字段，而不是从位置字段。 但是，位置字段 RHW 仍用于 w 缓冲和雾计算，必须因此提供时其中任何一个正在使用中。

 

 





