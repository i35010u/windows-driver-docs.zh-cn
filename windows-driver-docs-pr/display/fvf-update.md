---
title: FVF 更新
description: FVF 更新
keywords:
- FVF WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c90bd36e5bf8736a96f9f913ee62d8a69568ef96
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839929"
---
# <a name="fvf-update"></a>FVF 更新


## <span id="ddk_fvf_update_gg"></span><span id="DDK_FVF_UPDATE_GG"></span>


最初在 DirectX 6.0 中定义的 FVF 代码现在支持 DirectX 7.0 中纹理坐标集的规范。

除了 DirectX 6.0 中支持的常规2D 纹理以外，DirectX 7.0 还支持1D、3D 和4D 纹理。 此外，可能还会投影纹理。 调用 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)时，可以检查 [**D3DHAL \_ DRAWPRIMITIVES2DATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)的 **dwVertexType** 成员，以确定每个纹理坐标集的尺寸。

例如，如果有一个包含五个纹理坐标集的顶点，则这些纹理中的每一个都可以是一维、二维、三维或4D，它们可能会被投影纹理。 每个纹理阶段都是独立的，因此每个坐标集的尺寸都可能不同。 可以检查 **dwVertexType** 中包含的 FVF 标志的上限，以确定纹理坐标的尺寸。

纹理坐标计数为范围为0到8的四位数。 这会给出在单词的上16位中给定的纹理坐标集的数目。 对于八个纹理坐标集中的每个，将 [FVF](fvf--flexible-vertex-format-.md) 代码的上限设置为两位。 纹理坐标位的含义如下：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bit
<div>
 
</div>
模式</th>
<th align="left">小数
<div>
 
</div>
“值”</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>00</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>二维纹理坐标对， (u，v) ，如 DirectX 6.0 中所示。</p></td>
</tr>
<tr class="even">
<td align="left"><p>01</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>三维纹理坐标三、 (u、v、q) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>四维纹理坐标四元 (u、v、w、q) </p></td>
</tr>
<tr class="even">
<td align="left"><p>11</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>一维纹理坐标，u</p></td>
</tr>
</tbody>
</table>

 

3D 纹理坐标集可用于以下三种不同目的中的任何一种：投影纹理 (通过 D3DTTFF 的指示 \_) ，请参阅 DirectX SDK 文档中的 D3DTEXTURETRANSFORMFLAGS，请参阅 DirectX SDK 文档中的，请参阅 DirectX SDK 文档中的 \_ \_ 。

下表描述了用于一 \_ 维到4d 纹理坐标的 D3DRENDERSTATE WRAP *n* 呈现状态的标志。

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
<td align="left"><p>与 D3DWRAP_U 相同，它指定 <em>U</em> 坐标方向的环绕。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DWRAPCOORD_1</p></td>
<td align="left"><p>与 D3DWRAP_V 相同，它指定以 <em>V</em> 坐标方向换行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DWRAPCOORD_2</p></td>
<td align="left"><p>指定在 <em>w</em> 坐标方向上环绕。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DWRAPCOORD_3</p></td>
<td align="left"><p>指定在 <em>q</em> 坐标方向上环绕。</p></td>
</tr>
</tbody>
</table>

 

使用投影纹理时，它们会从相应的纹理坐标字段（而不是位置字段）获取 RHW 值。 但是，"位置" 字段的 RHW 仍用于 w-缓冲和雾化计算，因此当其中任一项正在使用时，必须提供该字段。

 

