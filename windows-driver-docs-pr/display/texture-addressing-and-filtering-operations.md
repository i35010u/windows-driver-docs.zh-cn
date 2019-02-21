---
title: 纹理寻址和筛选操作
description: 纹理寻址和筛选操作
ms.assetid: d468c83e-2e9c-4e4b-885e-0427714dd8a3
keywords:
- 多个纹理 WDK Direct3D 寻址
- 多个纹理 WDK Direct3D 筛选
- 多个纹理 WDK Direct3D 值混合处理
- 混合 WDK Direct3D
- 纹理管理 WDK Direct3D 寻址
- 管理 WDK Direct3D 纹理筛选
- 纹理管理 WDK Direct3D 值混合处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 209bd66b2de11c79d532f36ca089ad995c572f17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524678"
---
# <a name="texture-addressing-and-filtering-operations"></a>纹理寻址和筛选操作


## <span id="ddk_texture_addressing_and_filtering_operations_gg"></span><span id="DDK_TEXTURE_ADDRESSING_AND_FILTERING_OPERATIONS_GG"></span>


在 Direct3D 中，纹理寻址、 筛选和混合操作执行的名为一个单独的逻辑单元[纹理阶段](texture-stages.md)。 寻址和筛选操作此处所述因为其形成逻辑分组独立于混合操作。 有关纹理操作的详细信息，请参阅 DirectX SDK 文档中的 D3DTEXTUREOP 枚举类型。

尽管寻址和采样操作可以定义与混合 DirectX 6.0 及更高版本中的操作结合使用，更高版本的 DirectX 中它们可能是独立于混合操作。 下表中所列的纹理阶段状态用于设置纹理寻址和筛选纹理管道中每个阶段的操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DTSS_ANISOTROPY</p></td>
<td align="left"><p>指定各向异性筛选比率限制。 它指定最大各向异性筛选此纹理采样期间要应用的纵横比。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_MAGFILTER</p></td>
<td align="left"><p>定义用于示例纹理筛选器的类型时它们要放大的 （即，当一个纹素获取拉伸到多个呈现图面上像素为单位）。 D3DTEXTUREMAGFILTER 中列举了可用于纹理放大的筛选器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTSS_MAXMIPLEVEL</p></td>
<td align="left"><p>指定要使用的最大 MIP 映射级别。 它指示该纹理应永远不会采样 MIP 贴图级别大于另一个用。 因此，最大维度为 2<sup>MAXMIPLEVEL</sup>。 零表示没有任何限制。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_MINFILTER</p></td>
<td align="left"><p>定义它们时使用的筛选类型示例纹理<em>缩小</em>，也就是说，一个纹理映射到小于一个屏幕像素。 D3DTEXTUREMINFILTER 中列举了可用于缩小纹理的筛选器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTSS_MIPFILTER</p></td>
<td align="left"><p>定义类型的筛选，它用于层之间的 MIP 映射的示例。 D3DTEXTUREMIPFILTER 中列举了可用于此筛选器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_MIPLEVEL</p></td>
<td align="left"><p>允许应用程序时的硬件不能设置 MIP 级别。 这是重写时的 MIP 级别由硬件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTSS_MIPMAPLODBIAS</p></td>
<td align="left"><p>是指定 MIP 映射级别 (lod) 偏差的 D3DVALUE。 此偏置影响 MIP 映射级别计算，允许的纹理 （和更多的别名），根据需要增加或减少模糊。 单位为在 MIP 级别。</p>
<p>当前 WHQL/DCT 测试需要 MIP 映射 LOD 偏置的范围为 3.0-3.0 中运行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_TEXCOORDINDEX</p></td>
<td align="left"><p>指定纹理坐标集的索引。 该整数指示寻址单元应从中采样的纹理坐标集的索引。 这些坐标列出在传入灵活顶点格式 (<a href="fvf--flexible-vertex-format-.md" data-raw-source="[FVF](fvf--flexible-vertex-format-.md)">FVF</a>) 按数字顺序，其中零是 DirectX 组标准的纹理坐标，一种是使用第二个纹理的顶点数据协调组，依次类推。 这样，若要共享集所需的纹理坐标的纹理。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  要 Direct3D 符合规范，驱动程序所需以正确解析最多八个纹理坐标集，即使该设备只能循环访问和使用的定义中的坐标数**dwFVFCaps**。 该驱动程序必须使用 D3DTSS\_TEXCOORDINDEX 获取要用于纹理的右坐标。

 

 

 





