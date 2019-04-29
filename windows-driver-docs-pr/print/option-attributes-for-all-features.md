---
title: 所有功能的选项属性
description: 所有功能的选项属性
ms.assetid: 0d269fdf-f4a1-431a-9f07-044289b9f0fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca8ce8bb8392726042b2727072d6e8d7ab2e9526
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366325"
---
# <a name="option-attributes-for-all-features"></a>所有功能的选项属性





下表列出了，按字母顺序[选项属性](option-attributes.md)可用于所有功能，并描述其参数。

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
<td><p><em><strong>命令</strong></p></td>
<td><p>一个<strong>CmdSelect</strong> <a href="option-selection-command.md" data-raw-source="[option selection command](option-selection-command.md)">选项选择命令</a>，指定必须发送到打印机，若要选择的选项的命令字符串。</p></td>
<td><p>必需。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>DisabledFeatures</strong></p></td>
<td><p>功能名称字符串，标识应如果选择了禁用的功能的列表。</p>
<p>目前支持双工和逐份打印功能。 必须在具有设置为 PRINTER_PROPERTY 的 FeatureType 的功能中使用此选项属性。</p></td>
<td><p>可选。</p>
<p>列出的功能不能有<em><strong>可安装？</strong>设置为<strong>TRUE</strong>。 有关详细信息，请参阅<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装功能和选项</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>HelpIndex</strong></p></td>
<td><p>通过指定的帮助文件中表示索引数值<em> <strong>HelpFile</strong><a href="root-level-only-attributes.md" data-raw-source="[root-level-only attribute](root-level-only-attributes.md)">仅在根级别的属性</a>。</p></td>
<td><p>(还<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能特性</a>。)</p>
<p>索引值不能为零则为-1。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>可安装？</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否可安装选项。 (<strong>FALSE</strong>始终安装的方式。)</p>
<p>有关详细信息，请参阅<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装功能和选项</a>。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。 (还<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能特性</a>。)</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>InstallableFeatureName</strong></p></td>
<td><p>显示询问用户是否实际安装的可安装选项的文本字符串。</p>
<p>有关详细信息，请参阅<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装功能和选项</a>。</p></td>
<td><p>如果使用 *<strong>可安装？</strong>是<strong>TRUE</strong>和 *<strong>rcInstallableFeatureNameID</strong>未指定。 (还<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能特性</a>。)</p></td>
</tr>
<tr class="even">
<td><p></em><strong>名称</strong></p></td>
<td><p>用作在打印机的属性表上的选项的显示名称的文本字符串。</p></td>
<td><p>可选。 如果未指定，则<em> <strong>rcNameID</strong>必须指定。 (还<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能特性</a>。)</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>OptionID</strong></p></td>
<td><p>数字值，该值表示 Unidrv 将存储在打印机的独特选项标识符<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>结构。 仅与 PaperSize、 InputSlot、 半色调和媒体类型功能一起使用。 DEVMODE 结构中存储值<strong>dmPaperSize</strong>， <strong>dmDefaultSource</strong>， <strong>dmDitherType</strong>，或者<strong>dmMediaType</strong>成员，分别。</p></td>
<td><p>可选。 如果未指定，Unidrv 分配一个标识符的值 (&gt;256)。 若要避免冲突 Unidrv 分配标识符，指定的值必须大于 512。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>rcIconID</strong></p></td>
<td><p>与选项关联的图标资源的资源 ID。</p></td>
<td><p>可选。 如果未指定，Unidrv 不显示的图标上的打印机属性表的选项。 (还<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能特性</a>。)</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>rcInstallableFeatureNameID</strong></p></td>
<td><p>显示询问用户是否实际安装的可安装选项的文本字符串的资源 ID。</p>
<p>有关详细信息，请参阅<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装功能和选项</a>。</p></td>
<td><p>需要<em><strong>可安装？</strong>是<strong>TRUE</strong>和 *<strong>InstallableFeatureName</strong>未指定。 (还<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能特性</a>。)</p></td>
</tr>
<tr class="even">
<td><p></em><strong>rcNameID</strong></p></td>
<td><p>表示选项名称的字符串资源的资源 ID。</p></td>
<td><p>可选。 如果未指定，则 *<strong>名称</strong>必须指定。 (还<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能特性</a>。)</p>
<p>有关<a href="standard-options.md" data-raw-source="[standard options](standard-options.md)">标准选项</a>仅 PaperSize 功能，此属性设置为 RCID_DMPAPER_SYSTEM_NAME 导致 Unidrv 以使用预定义的选项名称字符串。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




