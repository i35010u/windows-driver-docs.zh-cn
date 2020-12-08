---
title: 纹理寻址和筛选操作
description: 纹理寻址和筛选操作
keywords:
- 多纹理 WDK Direct3D，寻址
- 多纹理 WDK Direct3D，筛选
- 多纹理 WDK Direct3D，混合
- 混合 WDK Direct3D
- 纹理管理 WDK Direct3D，寻址
- 纹理管理 WDK Direct3D，筛选
- 纹理管理 WDK Direct3D，混合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eadf7873a284605b4bf884b12896ef045021c396
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838941"
---
# <a name="texture-addressing-and-filtering-operations"></a>纹理寻址和筛选操作


## <span id="ddk_texture_addressing_and_filtering_operations_gg"></span><span id="DDK_TEXTURE_ADDRESSING_AND_FILTERING_OPERATIONS_GG"></span>


在 Direct3D 中，纹理寻址、筛选和混合操作由称为 [纹理贴图](texture-stages.md)的单独逻辑单元执行。 此处描述了寻址和筛选操作，因为它们构成了独立于混合操作的逻辑分组。 有关纹理操作的详细信息，请参阅 DirectX SDK 文档中的 D3DTEXTUREOP 枚举类型。

尽管寻址和采样操作是在 DirectX 6.0 及更高版本中与混合操作一起定义的，但在更高版本的 DirectX 中，它们可能与混合操作无关。 下表中列出的纹理阶段状态用于为纹理管道中的每个阶段设置纹理寻址和筛选操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3DTSS_ANISOTROPY</p></td>
<td align="left"><p>指定各向异性筛选比率限制。 它指定在此纹理采样期间要应用的各向异性筛选的最大纵横比。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_MAGFILTER</p></td>
<td align="left"><p>定义用于在放大纹理时 (的筛选器的类型，即当某个纹素延伸到多个呈现图面像素) 时。 可用于纹理放大的筛选器在 D3DTEXTUREMAGFILTER 中进行枚举。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTSS_MAXMIPLEVEL</p></td>
<td align="left"><p>指定要使用的最大 MIP 地图级别。 它表示，此纹理绝不应为指定的更大的 MIP map 级别采样。 因此，最大维度为 2<sup>MAXMIPLEVEL</sup>。 零表示没有限制。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_MINFILTER</p></td>
<td align="left"><p>定义用于在 <em>缩小</em>时采样纹理的筛选类型，即，将一个纹素映射到小于一个屏幕像素。 在 D3DTEXTUREMINFILTER 中枚举可用于缩小纹理的筛选器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTSS_MIPFILTER</p></td>
<td align="left"><p>定义用于在 MIP map 的各层之间采样的筛选类型。 可用于此的筛选器在 D3DTEXTUREMIPFILTER 中进行枚举。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_MIPLEVEL</p></td>
<td align="left"><p>允许应用程序在硬件不能时设置 MIP 级别。 当 MIP 级别由硬件确定时，此方法将被重写。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DTSS_MIPMAPLODBIAS</p></td>
<td align="left"><p>是一个 D3DVALUE，它指定 (LOD) 偏差的详细信息映射级别。 此偏向会影响 MIP map level 计算，允许纹理 (和更多的) 的模糊量更多或更少。 单位在 MIP 级别。</p>
<p>当前的 WHQL/DCT 测试要求 MIP map LOD 偏量在-3.0 到3.0 的范围内操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DTSS_TEXCOORDINDEX</p></td>
<td align="left"><p>指定纹理坐标集的索引。 此整数指示用于寻址单元的纹理坐标集的索引。 这些坐标以传入的灵活顶点格式列出 (<a href="fvf--flexible-vertex-format-.md" data-raw-source="[FVF](fvf--flexible-vertex-format-.md)">FVF</a>) 顶点数据按数值顺序显示，其中0是标准的一组纹理坐标，一个是另一个纹理坐标集，依此类推。 这允许纹理根据需要共享纹理坐标集。</p></td>
</tr>
</tbody>
</table>

 

**注意**   若要符合 Direct3D 的要求，驱动程序必须正确分析多达八个纹理坐标集，即使设备只能循环访问并使用在 **dwFVFCaps** 中定义的坐标数。 驱动程序必须使用 D3DTSS \_ TEXCOORDINDEX 来抓住要用于纹理的右坐标。

 

 

 





