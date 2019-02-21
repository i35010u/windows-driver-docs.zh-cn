---
title: Alpha 混合组合
description: Alpha 混合组合
ms.assetid: 567810da-ad8d-4ceb-b914-868632384d09
keywords:
- alpha 混合组合 WDK DirectX VA
- 混合型的图片 WDK DirectX VA
- alpha 混合组合 WDK DirectX va，因此有关 alpha 混合组合
- 混合型的图片 WDK DirectX va，因此有关 alpha 混合组合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e2689975c2d301be5c5b547d35404a910dc077c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521619"
---
# <a name="alpha-blend-combination"></a>Alpha 混合组合


## <span id="ddk_alpha_blend_combination_gg"></span><span id="DDK_ALPHA_BLEND_COMBINATION_GG"></span>


当[bDXVA\_Func 变量](bdxva-func-variable.md)是等于 3，指定的操作是 alpha 混合的组合。 Alpha 混合组合采用上次加载的 alpha 混合源信息并将它与引用图片将创建用于显示混合的图片相结合。

指定的 alpha 混合组合缓冲区**dwTypeIndex**的成员[ **DXVA\_BufferDescription** ](https://msdn.microsoft.com/library/windows/hardware/ff563122)结构用来生成一种混合来自源图片和 alpha 值混合处理信息的图片。 在的源和目标图片不在 4:4:4 格式、 混合 AYUV alpha 值混合处理面或等效项中的信息的图形的每个第二个示例 （适用于示例中，第一个、 第三、 第五个等） 应用到 （更低分辨率) 源色度信息垂直或水平方向，在适用时生成混合的结果。

使用以下结构来实现 alpha 混合组合。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结构</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563122" data-raw-source="[&lt;strong&gt;DXVA_BufferDescription&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563122)"><strong>DXVA_BufferDescription</strong></a></p></td>
<td align="left"><p>指定要使用的 alpha 混合组合缓冲区。 此缓冲区控制混合图片从源图片和 alpha 值混合处理信息的生成。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563120" data-raw-source="[&lt;strong&gt;DXVA_BlendCombination&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563120)"><strong>DXVA_BlendCombination</strong></a></p></td>
<td align="left"><p>指定如何从 alpha 混合组合缓冲区生成混合型的图片。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563126" data-raw-source="[&lt;strong&gt;DXVA_ConfigAlphaCombine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563126)"><strong>DXVA_ConfigAlphaCombine</strong></a></p></td>
<td align="left"><p>建立的配置方式 alpha 混合的组合操作是要执行。</p></td>
</tr>
</tbody>
</table>

 

 

 





