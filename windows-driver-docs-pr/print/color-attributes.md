---
title: 颜色属性
description: 颜色属性
ms.assetid: c8de0186-9cf5-43e5-81e7-33351a34c13c
keywords:
- 颜色属性 WDK Unidrv
- 常规打印机属性 WDK Unidrv，颜色
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a684f9b77abcac72a79a5c326f7cd6250abe15c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351909"
---
# <a name="color-attributes"></a>颜色属性





颜色属性是[常规打印属性](general-printing-attributes.md)，用于指定用于控制彩色打印的特征。

下表列出了颜色属性。

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
<td><p><strong><em>ChangeColorModeOnDoc?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>。 指示是否可以不会产生副作用的文档的各个页面间更改打印机的颜色模式。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>，则返回 TRUE</strong>。 Unidrv 使用此值来优化打印速度。 其他信息，请参阅此表后面的说明。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>CyanInMagentaDye</strong></p></td>
<td><p>从 0 到 1000，指示在洋红色彩色青色污染百分比的数字值。 值为 100 次的污染百分比。 例如，8.4%污染指定为 840 和 10%为 1000年。</p></td>
<td><p>可选。 如果未指定，使用 Unidrv 提供默认值。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>CyanInYellowDye</strong></p></td>
<td><p>从 0 到 1000，指示在黄色彩色青色污染百分比的数字值。 值为 100 次的污染百分比。 例如，8.4%污染指定为 840 和 10%为 1000年。</p></td>
<td><p>可选。 如果未指定，使用 Unidrv 提供默认值。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>EnableGDIColorMapping</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>。 指示是否 GDI 应执行 gamut 映射从显示到打印机颜色空间。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。 如果<strong>，则返回 TRUE</strong>，Unidrv 中设置 HT_FLAG_DO_DEVCLR_XFORM 标志<a href="https://msdn.microsoft.com/library/windows/hardware/ff566484" data-raw-source="[&lt;strong&gt;GDIINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566484)"> <strong>GDIINFO</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>MagentaInCyanDye</strong></p></td>
<td><p>从 0 到 1000，指示在青色彩色洋红色污染百分比的数字值。 值为 100 次的污染百分比。 例如，8.4%污染指定为 840 和 10%为 1000年。</p></td>
<td><p>可选。 如果未指定，使用 Unidrv 提供默认值。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>MagentaInYellowDye</strong></p></td>
<td><p>从 0 到 1000，指示在黄色彩色洋红色污染百分比的数字值。 值为 100 次的污染百分比。 例如，8.4%污染指定为 840 和 10%为 1000年。</p></td>
<td><p>可选。 如果未指定，使用 Unidrv 提供默认值。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>YellowInCyanDye</strong></p></td>
<td><p>从 0 到 1000，指示在青色彩色的黄色污染百分比的数字值。 值为 100 次的污染百分比。 例如，8.4%污染指定为 840 和 10%为 1000年。</p></td>
<td><p>可选。 如果未指定，使用 Unidrv 提供默认值。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>YellowInMagentaDye</strong></p></td>
<td><p>从 0 到 1000，指示在洋红色彩色的黄色污染百分比的数字值。 值为 100 次的污染百分比。 例如，8.4%污染指定为 840 和 10%为 1000年。</p></td>
<td><p>可选。 如果未指定，使用 Unidrv 提供默认值。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  时 **\*ChangeColorModeOnDoc？** 颜色属性设置为**TRUE**，颜色优化已启用。 如果此属性设置为**FALSE**，不执行任何优化。 启用颜色优化时，假脱机文件中的颜色存在导致假脱机文件要播放的颜色;缺少的假脱机文件中的颜色会导致假脱机文件在单色播放。
如果要创建呈现插件，以生成颜色水印 Unidrv，需要注意该颜色优化会导致颜色水印黑白文档在打印时以黑白模式打印。 若要确保正确颜色水印打印彩色和黑白文档，请禁用颜色优化。

控制颜色优化 **\*ChangeColorModeOnDoc？** 还可以通过设置控制颜色特性**dwColorOptimization**隶属[ **特性\_INFO\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff545091)或[**属性\_信息\_3** ](https://msdn.microsoft.com/library/windows/hardware/ff545093)结构。 此外可以通过使用控制颜色优化[ **GdiEndPageEMF** ](https://msdn.microsoft.com/library/windows/hardware/ff549468)函数。

 

有关此页上列出的颜色特性的示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




