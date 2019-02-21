---
title: 确定顶点缓冲区数据格式
description: 确定顶点缓冲区数据格式
ms.assetid: e10604f9-e800-40ff-a0e1-0f9389340e9c
keywords:
- 顶点格式 WDK Direct3D
- 灵活的顶点格式 WDK Direct3D
- FVF WDK Direct3D
- 顶点缓冲区 WDK Direct3D
- Direct3D WDK Windows 2000 显示，灵活顶点格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c47237926cb89856faa121f573acb58e34cb3ca8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526709"
---
# <a name="determining-the-vertex-buffer-data-format"></a>确定顶点缓冲区数据格式


## <span id="ddk_determining_the_vertex_buffer_data_format_gg"></span><span id="DDK_DETERMINING_THE_VERTEX_BUFFER_DATA_FORMAT_GG"></span>


若要识别顶点缓冲区中的数据的格式，驱动程序应确定以下信息：

-   纹理维度 (一维、 二维、 三维或 4 D)

-   FVF 数据中存在的组件

-   组件的顺序，都存在

### <a name="span-idfvftexturedimensionspanspan-idfvftexturedimensionspanfvf-texture-dimension"></a><span id="fvf_texture_dimension"></span><span id="FVF_TEXTURE_DIMENSION"></span>FVF 纹理维度

该驱动程序应确定 D3DTEXTURETRANSFORMFLAGS 纹理坐标计数标志从纹理维度 (D3DTTFF\_计数*n*、 DirectX SDK 文档中所述)。 向发出信号计数标记号，多少纹理坐标都存在。 请注意，这不会不一定等同于维度的纹理本身，如以下各节中所述。

### <a name="span-idnonprojectedtexturesspanspan-idnonprojectedtexturesspannonprojected-textures"></a><span id="nonprojected_textures"></span><span id="NONPROJECTED_TEXTURES"></span>Nonprojected 的纹理

下面的列表 nonprojected 的纹理：

-   D3DTTFF\_COUNT1 指示光栅器应该获得 1d 纹理坐标。

-   D3DTTFF\_数 2 指示光栅器应该获得 2D 纹理坐标。

-   D3DTTFF\_COUNT3 指示光栅器应该获得三维纹理坐标。

-   D3DTTFF\_COUNT4 指示光栅器应该获得 4d 纹理坐标。

### <a name="span-idprojectedtexturesspanspan-idprojectedtexturesspanprojected-textures"></a><span id="projected_textures"></span><span id="PROJECTED_TEXTURES"></span>预计的纹理

如果要使用投影的纹理，D3DTTFF\_预计标志设置为指示是否要作为被除数由最后一个纹理坐标 (计数<sup>th</sup>) 的纹理坐标集的元素。 因此，对于 2D 预计纹理，计数为 3，因为前两个元素除以第三，从而导致 2D 纹理查找两个浮点值。 也就是说，这两个 D3DTTFF\_数 2 和 D3DTTFF\_COUNT3 |D3DTTFF\_预计引用 2D 纹理。

### <a name="span-idddkfvfvertexdatacomponentsggspanspan-idddkfvfvertexdatacomponentsggspanfvf-vertex-data-components"></a><span id="ddk_fvf_vertex_data_components_gg"></span><span id="DDK_FVF_VERTEX_DATA_COMPONENTS_GG"></span>FVF 顶点数据组件

该驱动程序确定哪些组件都存在通过分析中指定的标志**dwVertexType**的成员[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff545957)结构。 下表指示可以在中设置的位字段**dwVertexType**和它们标识的组件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DFVF_DIFFUSE</p></td>
<td align="left"><p>每个顶点都有漫射颜色。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_SPECULAR</p></td>
<td align="left"><p>每个顶点都有的反射颜色。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX0</p></td>
<td align="left"><p>顶点数据不提供任何纹理坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX1</p></td>
<td align="left"><p>每个顶点都有一个组纹理坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX2</p></td>
<td align="left"><p>每个顶点都有两个集的纹理坐标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX3</p></td>
<td align="left"><p>每个顶点都有三个纹理坐标集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX4</p></td>
<td align="left"><p>每个顶点都有四个纹理坐标集。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX5</p></td>
<td align="left"><p>每个顶点都有五个集的纹理坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX6</p></td>
<td align="left"><p>每个顶点都有六个纹理坐标集。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_TEX7</p></td>
<td align="left"><p>每个顶点都有七个纹理坐标集。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DFVF_TEX8</p></td>
<td align="left"><p>每个顶点都有八个纹理坐标集。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DFVF_XYZRHW</p></td>
<td align="left"><p>每个顶点<em>x、 y、 z</em>，并<em>w</em>坐标。</p></td>
</tr>
</tbody>
</table>

 

只有一个 D3DFVF\_TEX *n*设置标志。

### <a name="span-idddkfvfvertexcomponentorderingggspanspan-idddkfvfvertexcomponentorderingggspanfvf-vertex-component-ordering"></a><span id="ddk_fvf_vertex_component_ordering_gg"></span><span id="DDK_FVF_VERTEX_COMPONENT_ORDERING_GG"></span>FVF 顶点组件排序

Microsoft Direct3D 提供了驱动程序和其组件进行排序，如下图中所示的顶点数据。

![说明灵活顶点格式 (fvf) 顶点组件排序的关系图](images/fvf.png)

Direct3D 始终发送*x、 y、 z*并*w*值; 仅发送的剩余数据所要求的应用程序。 请注意，此图假定 2D 纹理坐标，虽然 1d，3D，和 4d 纹理也是最新的 DirectX 版本有效。

在上图中所示，顶点数据由以下组件构成：

1.  位置 (*x、 y、 z、 w*) （必需）

    第一个顶点组件是顶点的识别位置的四个 D3DVALUEs。 Direct3D 始终设置 D3DFVF\_XYZRHW 位**dwVertexType**。

2.  漫射颜色 （可选）。

    如果存在，该组件是一个 D3DCOLOR 值，指定针对此顶点的漫射颜色。 Direct3D 设置 D3DFVF\_位的漫射**dwVertexType**存在此组件时。

3.  （可选） 的反射颜色。

    如果存在，该组件是一个 D3DCOLOR 值，指定针对此顶点的反射颜色。 Direct3D 设置 D3DFVF\_位的反射**dwVertexType**存在此组件时。

4.  纹理数据 （可选）。

    此部分根据纹理维度而有所不同。 纹理中每个维度，D3DVALUE 指定的每个*u*， *v*， *w*，或者*q*组件 （请参阅 FVF 纹理的说明维度）。 例如，如果要使用 2D nonprojected 的纹理，每个纹理的两个 D3DVALUEs 所需指定顶点*u、 v*值为每个纹理总的最多八种纹理。 数*u、 v*是对存在*n*，其中*n*对应于 D3DFVF\_TEX*n*标志中设置**dwVertexType**。 例如，如果 D3DFVF\_中设置 TEX3 **dwVertexType**，然后三个*u、 v*对提供的每个顶点。

FVF 数据始终严格打包;也就是说，顶点缓冲区中未显式指定的组件上不浪费任何内存。 例如，当**dwVertexType**是 (D3DFVF\_XYZRHW |D3DFVF\_TEX2)，并且纹理维度是 2D，则每个顶点缓冲区中的包含八个紧密 D3DVALUEs。 这些名称指定的位置 (*x、 y、 z、 w*) 和纹理坐标 （tu₀、 tv₀、 tu₁、 tv₁） 这两个纹理下, 图中所示：

![说明这两个纹理的位置和纹理坐标的关系图](images/vbuf.png)

在上图假定有只有两个纹理坐标。 提供给该驱动程序的顶点数据始终是转换和照明。 该驱动程序永远不会收到的法向。 FVF 纹理坐标集内的所有数据都是 IEEE 单精度浮点数。 有关实现的详细信息，请参阅*Perm3*示例驱动程序。 有关 FVF 详细信息，请参阅 DirectX SDK 文档。

> [!NOTE] 
> Microsoft Windows Driver Kit (WDK) 不包含 3Dlabs Permedia3 示例显示器驱动程序 (*Perm3.h*)。 你可以获取从 Windows Server 2003 SP1 驱动程序开发工具包 (DDK)，可以从 DDK-WDHC 网站的 Windows 驱动程序开发工具包页面下载此示例驱动程序。
