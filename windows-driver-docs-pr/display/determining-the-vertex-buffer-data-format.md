---
title: 确定顶点缓冲区数据格式
description: 确定顶点缓冲区数据格式
keywords:
- 顶点格式 WDK Direct3D
- 灵活顶点格式 WDK Direct3D
- FVF WDK Direct3D
- 顶点缓冲 WDK Direct3D
- Direct3D WDK Windows 2000 显示，灵活顶点格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13353b92d4c3ae350749320dd181c71cae67498f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809521"
---
# <a name="determining-the-vertex-buffer-data-format"></a>确定顶点缓冲区数据格式


## <span id="ddk_determining_the_vertex_buffer_data_format_gg"></span><span id="DDK_DETERMINING_THE_VERTEX_BUFFER_DATA_FORMAT_GG"></span>


为了识别顶点缓冲区中数据的格式，驱动程序应确定以下信息：

-   纹理的维度 (1D、2D、3D 或 4D) 

-   FVF 数据中存在的组件

-   存在的组件的顺序

### <a name="span-idfvf_texture_dimensionspanspan-idfvf_texture_dimensionspanfvf-texture-dimension"></a><span id="fvf_texture_dimension"></span><span id="FVF_TEXTURE_DIMENSION"></span>FVF 纹理尺寸

驱动程序应根据 \_ DIRECTX SDK 文档) 中所述的 D3DTEXTURETRANSFORMFLAGS 纹理坐标计数标志 (D3DTTFF 计数 *n* 来确定纹理的维度。 计数标志的数量表示存在多少纹理坐标。 请注意，这并不一定等于纹理本身的维度，如以下各节中所述。

### <a name="span-idnonprojected_texturesspanspan-idnonprojected_texturesspannonprojected-textures"></a><span id="nonprojected_textures"></span><span id="NONPROJECTED_TEXTURES"></span>Nonprojected 纹理

下面列出了 nonprojected 纹理：

-   D3DTTFF \_ COUNT1 指示光栅区应有一维纹理坐标。

-   D3DTTFF \_ COUNT2 指示光栅图应需要2d 纹理坐标。

-   D3DTTFF \_ COUNT3 指示光栅图应需要3d 纹理坐标。

-   D3DTTFF \_ COUNT4 指示光栅化程序应期待4d 纹理坐标。

### <a name="span-idprojected_texturesspanspan-idprojected_texturesspanprojected-textures"></a><span id="projected_textures"></span><span id="PROJECTED_TEXTURES"></span>投影纹理

如果使用的是投影纹理，则 \_ 会将 D3DTTFF 投影标志设置为指示纹理坐标将除以纹理坐标集) 元素的最后一个<sup>th</sup> (计数。 因此，对于2D 投影纹理，计数将为三个，因为前两个元素除以第三个元素，因此，两个浮点数用于2D 纹理查找。 也就是说，D3DTTFF \_ COUNT2 和 D3DTTFF \_ COUNT3 |D3DTTFF \_ 投影引用2d 纹理。

### <a name="span-idddk_fvf_vertex_data_components_ggspanspan-idddk_fvf_vertex_data_components_ggspanfvf-vertex-data-components"></a><span id="ddk_fvf_vertex_data_components_gg"></span><span id="DDK_FVF_VERTEX_DATA_COMPONENTS_GG"></span>FVF 顶点数据组件

驱动程序通过分析 [**D3DHAL \_ DRAWPRIMITIVES2DATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)结构的 **dwVertexType** 成员中指定的标志来确定哪些组件是存在的。 下表显示了可在 **dwVertexType** 中设置的位域以及它们标识的组件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DFVF_DIFFUSE</p></td>
<td align="left"><p>每个顶点都有漫射色。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_SPECULAR</p></td>
<td align="left"><p>每个顶点都有反射颜色。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX0</p></td>
<td align="left"><p>没有与顶点数据一起提供的纹理坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX1</p></td>
<td align="left"><p>每个顶点都有一组纹理坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX2</p></td>
<td align="left"><p>每个顶点都有两组纹理坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX3</p></td>
<td align="left"><p>每个顶点都有三组纹理坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX4</p></td>
<td align="left"><p>每个顶点都有四组纹理坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX5</p></td>
<td align="left"><p>每个顶点都有五组纹理坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX6</p></td>
<td align="left"><p>每个顶点都有六组纹理坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX7</p></td>
<td align="left"><p>每个顶点都有七组纹理坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX8</p></td>
<td align="left"><p>每个顶点都有八组纹理坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_XYZRHW</p></td>
<td align="left"><p>每个顶点具有 <em>x、y、z</em>和 <em>w</em> 坐标。</p></td>
</tr>
</tbody>
</table>

 

仅设置了一个 D3DFVF \_ TEX *n* 标志。

### <a name="span-idddk_fvf_vertex_component_ordering_ggspanspan-idddk_fvf_vertex_component_ordering_ggspanfvf-vertex-component-ordering"></a><span id="ddk_fvf_vertex_component_ordering_gg"></span><span id="DDK_FVF_VERTEX_COMPONENT_ORDERING_GG"></span>FVF 顶点组件排序

Microsoft Direct3D 为驱动程序提供了其组件按顺序排列的顶点数据，如下图所示。

![说明灵活顶点格式的关系图 (fvf) 顶点组件排序](images/fvf.png)

Direct3D 始终发送 *x、y、z* 和 *w* 值;其余数据只会根据应用程序的需要发送。 请注意，此图假设二维、三维和4D 纹理对于最新的 DirectX 版本也是有效的。

如上图所示，顶点数据由以下组件组成：

1.  位置 (*x、y、z 和 w*)  (必需) 

    第一个顶点组件是四个 D3DVALUEs，用于标识顶点的位置。 Direct3D 始终 \_ 在 **dwVertexType** 中设置 D3DFVF XYZRHW 位。

2.  漫射色 (可选) 。

    如果存在，则此组件为 D3DCOLOR 值，该值指定此顶点的漫射颜色。 \_当存在此组件时，Direct3D 在 **dwVertexType** 中设置 D3DFVF 漫射位。

3.   (可选) 的反射颜色。

    如果存在，则此组件为指定该顶点的反射颜色的 D3DCOLOR 值。 \_当存在此组件时，Direct3D 在 **dwVertexType** 中设置 D3DFVF 反光位。

4.  纹理数据 (可选) 。

    此部分根据纹理的维度而有所不同。 对于纹理中的每个维度，D3DVALUE 指定每个 *u*、 *v*、 *w* 或 *q* 组件 (查看 FVF 纹理尺寸) 的说明。 例如，如果使用的是 2D nonprojected 纹理，则需要为每个纹理指定顶点的 *u，v 值（* 最多8个纹理）。 存在 *u，v* 对的数量为 *n*，其中 *n* 对应于 \_ **dwVertexType** 中设置的 D3DFVF TEX *n* 标志。 例如，如果 D3DFVF \_ TEX3 设置为 **dwVertexType**，则每个顶点都提供三个 *u，v* 对。

FVF 数据始终紧密打包;也就是说，没有在顶点缓冲区中显式指定的组件上浪费内存。 例如，当 **dwVertexType** 为 (D3DFVF \_ XYZRHW |D3DFVF \_ TEX2) ，纹理维度为2d，缓冲区中的每个顶点都包含八个紧密打包的 D3DVALUEs。 它们指定两种纹理的位置 (*x、y、z、w*) 和纹理坐标 (tu ₀、tv ₀、tu ₁、tv ₁) 如下图所示：

![说明两个纹理的位置和纹理坐标的关系图](images/vbuf.png)

在上图中，假定只有两个纹理坐标。 提供给驱动程序的顶点数据始终转换并发亮。 驱动程序从不接收法线。 FVF 纹理坐标集中的所有数据都是单精度 IEEE 浮点数。 有关实现的详细信息，请参阅 *Perm3* 示例驱动程序。 有关 FVF 的详细信息，请参阅 DirectX SDK 文档。

> [!NOTE] 
> Microsoft Windows 驱动程序工具包 (WDK) 不包含 *Perm3*)  (的 3Dlabs Permedia3 示例显示驱动程序。 你可以从 Windows Server 2003 SP1 驱动程序开发工具包获取此示例驱动程序 (DDK) ，你可以从 WDHC 网站的 "Windows 驱动程序开发工具包" 页下载该驱动程序。
