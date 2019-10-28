---
title: FVF 更新
description: FVF 更新
ms.assetid: 2bbcb1fd-b29f-41f4-93eb-5bd1cde9cb20
keywords:
- FVF WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a45cf4a887f1d649332fb7d152dc5c0a15067f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838936"
---
# <a name="fvf-update"></a>FVF 更新


## <span id="ddk_fvf_update_gg"></span><span id="DDK_FVF_UPDATE_GG"></span>


最初在 DirectX 6.0 中定义的 FVF 代码现在支持 DirectX 7.0 中纹理坐标集的规范。

除了 DirectX 6.0 中支持的常规2D 纹理以外，DirectX 7.0 还支持1D、3D 和4D 纹理。 此外，可能还会投影纹理。 调用[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)时，可以检查[**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)的**dwVertexType**成员，以确定每个纹理坐标集的尺寸。

例如，如果有一个包含五个纹理坐标集的顶点，则这些纹理中的每一个都可以是一维、二维、三维或4D，它们可能会被投影纹理。 每个纹理阶段都是独立的，因此每个坐标集的尺寸都可能不同。 可以检查**dwVertexType**中包含的 FVF 标志的上限，以确定纹理坐标的尺寸。

纹理坐标计数为范围为0到8的四位数。 这会给出在单词的上16位中给定的纹理坐标集的数目。 对于八个纹理坐标集中的每个，将[FVF](fvf--flexible-vertex-format-.md)代码的上限设置为两位。 纹理坐标位的含义如下：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">小段
<div>
 
</div>
模式</th>
<th align="left">十进制
<div>
 
</div>
Value</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>–</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>二维纹理坐标对（u，v），如 DirectX 6.0 中所示</p></td>
</tr>
<tr class="even">
<td align="left"><p>01</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>三维纹理坐标三重坐标，（u，v，q）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>四维纹理坐标四维，（u，v，w，q）</p></td>
</tr>
<tr class="even">
<td align="left"><p>11</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>一维纹理坐标，u</p></td>
</tr>
</tbody>
</table>

 

3D 纹理坐标集可用于以下三种不同目的中的任何一种：投影纹理（通过 D3DTTFF 的信号发出通知\_，请参阅 DirectX SDK 文档中的 D3DTEXTURETRANSFORMFLAGS）、音量纹理或 cube 地图矢量纹理（按确定）通过一组类似于 D3DRENDERSTATE 的一组呈现状态\_WRAP0 为 D3DRENDERSTATE\_已在纹理坐标集上指定的。

下表描述了用于 D3DRENDERSTATE 的标志，这些标志分别为1D 到4D 纹理坐标的每个行的\_*n*呈现状态。

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
<td align="left"><p>与 D3DWRAP_U 相同，后者指定<em>U</em>坐标方向的环绕。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DWRAPCOORD_1</p></td>
<td align="left"><p>与 D3DWRAP_V 相同，后者指定以<em>V</em>坐标方向换行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DWRAPCOORD_2</p></td>
<td align="left"><p>指定在<em>w</em>坐标方向上环绕。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DWRAPCOORD_3</p></td>
<td align="left"><p>指定在<em>q</em>坐标方向上环绕。</p></td>
</tr>
</tbody>
</table>

 

使用投影纹理时，它们会从相应的纹理坐标字段（而不是位置字段）获取 RHW 值。 但是，"位置" 字段的 RHW 仍用于 w-缓冲和雾化计算，因此当其中任一项正在使用时，必须提供该字段。

 

 





