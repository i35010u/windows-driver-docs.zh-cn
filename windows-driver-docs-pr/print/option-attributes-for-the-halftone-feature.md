---
title: 半色调功能的选项属性
description: 半色调功能的选项属性
ms.assetid: a188908a-ddf7-4b4d-a46d-e3550ffb0418
keywords:
- 半色调功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79dc34cc07fc6010ee40067f72d4f0359b841d2c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363375"
---
# <a name="option-attributes-for-the-halftone-feature"></a>半色调功能的选项属性





下表列出了与半色调功能关联的属性。 有关半色调功能的详细信息，请参阅[标准功能](standard-features.md)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名称</th>
<th>特性参数</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>HTCallbackID</strong></p></td>
<td><p>正的数字值传递给呈现插件的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern" data-raw-source="[&lt;strong&gt;IPrintOemUni::HalftonePattern&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)"> <strong>IPrintOemUni::HalftonePattern</strong> </a>方法作为其<em>dwCallbackID</em>参数。</p></td>
<td><p>需要<strong>IPrintOemUni::HalftonePattern</strong>提供方法。 请参阅<a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv 与半色调</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>HTNumPatterns</strong></p></td>
<td><p>表示提供的半色调模式数的数字值。</p>
<p>请参阅<a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv 与半色调</a>。</p></td>
<td><p>可选。 可以是 1 或 3，3，表示红色、 绿色和蓝色，按此顺序的单独模式。 如果未指定，默认值为 1。 可以通过使用<em> <strong>rcHTPatternID</strong>或 *<strong>HTCallbackID</strong>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>HTPatternSize</strong></p></td>
<td><p><a href="pairs.md" data-raw-source="[Pair](pairs.md)">对</a>的数值表示宽度和高度，以像素为单位指定的模式<em> <strong>rcHTPatternID</strong>。</p></td>
<td><p>如果使用 *<strong>rcHTPatternID</strong>指定。 最大模式大小是对 （256、 256）。 宽度和高度，相乘，必须为 dword 值整除，对于存储为 4。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>rcHTPatternID</strong></p></td>
<td><p>表示半色调模式数据 RC_HTPATTERN 资源的资源标识符。</p></td>
<td><p>如果在资源 DLL 中提供的半色调模式的要求。 请参阅<a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv 与半色调</a>。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

有关使用这些属性的详细信息，请参阅[Unidrv 与半色调](halftoning-with-unidrv.md)。 这些属性不用于[微型驱动程序提供半色调](minidriver-supplied-halftoning.md)。

 

 




