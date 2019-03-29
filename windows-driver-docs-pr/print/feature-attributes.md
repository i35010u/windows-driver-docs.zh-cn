---
title: 功能属性
description: 功能属性
ms.assetid: ae1a489e-2554-46fc-8f2e-45128b073f91
keywords:
- 打印机属性 WDK Unidrv，功能
- 功能 attribues WDK Unidrv
- 打印机功能 WDK Unidrv，属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 455f08c3fbe61188ffb91691ed4a759e94b63102
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350352"
---
# <a name="feature-attributes"></a>功能属性





指定打印机功能，当您使用属性 Unidrv 提供以下信息：

-   表示功能的显示名称的文本字符串。

-   与功能相关联的打印机选项集。

-   一个布尔值，该值指示是否该功能将始终存在，或者是否可安装。

-   功能类型和优先级，如果该功能自定义，指示这一功能显示的属性页上，其相对优先级。

下表列出了按字母顺序的功能属性，并介绍其参数。

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
<td><p><strong><em>ConcealFromUI?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否应在用户界面中显示该功能。</p></td>
<td><p>可选。 如果未指定默认值为<strong>FALSE</strong>，这意味着该功能会显示。</p>
<p>应为<strong>，则返回 TRUE</strong>唯一或如果一项功能只提供一个选项 （例如，一个解决方法），因此用户可修改，如果设置另一项功能的选项来控制功能的选项选择。</p>
<p>如果 <strong></em>ConcealFromUI</strong>属性设置为<strong>TRUE</strong>，然后 Unidrv 或 PrintConfig 将将 psk:DisplayUI 元素添加到该项目在 PrintCapabilities XML 中的功能元素。</p></td>
</tr>
<tr class="even">
<td><p><strong><em>ConflictPriority</strong></p></td>
<td><p>表示功能的优先级，其中 1 表示最高优先级的数字值。</p></td>
<td><p>可选。 请参阅<a href="feature-conflict-priority.md" data-raw-source="[Feature Conflict Priority](feature-conflict-priority.md)">功能冲突优先级</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>DefaultOption</strong></p></td>
<td><p>该功能的选项之一的名称。</p></td>
<td><p>可选。 如果未指定，第一个选项列在<em>功能条目是默认值。 PaperSize 功能 Unidrv 的默认选项是 A4 指标的区域设置和字母的其他位置。 如果的默认 PaperSize 不存在，Unidrv 使用由指定的 PaperSize 选项 *<strong>DefaultOption</strong>关键字。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>FeatureType</strong></p></td>
<td><p>DOC_PROPERTY</p>
<p>JOB_PROPERTY</p>
<p>PRINTER_PROPERTY</p>
<p>如果 DOC_PROPERTY 或 JOB_PROPERTY，该功能将分配给文档属性表。 如果 PRINTER_PROPERTY，该功能分配给打印机属性表。</p></td>
<td><p>所需的自定义功能。 可选的标准功能。 如果未指定，标准功能的默认值是 DOC_PROPERTY，除非另有说明。</p>
<p>如果 PRINTER_PROPERTY，该功能的选项值保存在注册表中。 如果 DOC_PROPERTY 或 JOB_PROPERTY，则该功能的选项值与文档一起保存。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>HelpIndex</strong></p></td>
<td><p>通过指定的帮助文件中表示索引的数字值 *<strong>HelpFile</strong> <a href="root-level-only-attributes.md" data-raw-source="[root-level-only attribute](root-level-only-attributes.md)">仅限根级别属性</a>。</p></td>
<td><p>(还<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。)</p></td>
</tr>
<tr class="even">
<td><p><strong></em>可安装？</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否可安装该功能。 (<strong>FALSE</strong>始终安装的方式。)</p>
<p>有关详细信息，请参阅<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装功能和选项</a>。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。 如果<strong>，则返回 TRUE</strong>，所有功能的选项也是可安装，但指定的第一个除外。 如果<strong>FALSE</strong>，必须也始终安装在至少一个功能的选项。 (还<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。)</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>InstallableFeatureName</strong></p></td>
<td><p>显示询问用户是否实际安装安装的功能的文本字符串。</p>
<p>有关详细信息，请参阅<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装功能和选项</a>。</p></td>
<td><p>如果使用 *<strong>可安装？</strong>是<strong>TRUE</strong>和 *<strong>rcInstallableFeatureNameID</strong>未指定。 (还<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。)</p></td>
</tr>
<tr class="even">
<td><p><strong></em>名称</strong></p></td>
<td><p>用作在打印机的属性表上的功能的显示名称的文本字符串。</p></td>
<td><p>可选。 如果未指定，则<em> <strong>rcNameID</strong>必须指定。 (还<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。)</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>选项</strong></p></td>
<td><p>选项参数，如中所述<a href="option-entry-format.md" data-raw-source="[Option Entry Format](option-entry-format.md)">选项条目格式</a>。</p></td>
<td><p>必需。 使用<strong><em>选项</strong>条目与功能相关联的每个选项。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>rcIconID</strong></p></td>
<td><p>与功能相关联的图标资源的资源 ID。</p></td>
<td><p>可选。 如果未指定，则 Unidrv 不打印机属性页上显示的功能的图标。 (还<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。)</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>rcInstallableFeatureNameID</strong></p></td>
<td><p>显示询问用户是否实际安装安装的功能的文本字符串的资源 ID。</p>
<p>有关详细信息，请参阅<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装功能和选项</a>。</p></td>
<td><p>如果使用 *<strong>可安装？</strong>是<strong>TRUE</strong>和 *<strong>InstallableFeatureName</strong>未指定。 (还<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。)</p></td>
</tr>
<tr class="even">
<td><p><strong></em>rcNameID</strong></p></td>
<td><p>表示功能名称的字符串资源的资源 ID。 （零不是有效的资源 id。）</p></td>
<td><p>可选。 如果未指定，则<em><strong>名称</strong>必须指定。 (还<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。)</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>UpdateQualityMacro?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>，以指示是否指定质量设置的条件语句中包含的功能 (请参阅<a href="controlling-image-quality.md" data-raw-source="[Controlling Image Quality](controlling-image-quality.md)">控制图像质量</a>)。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。 (值都强制发往<strong>，则返回 TRUE</strong>如果该功能包含在指定质量设置的条件语句。)</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




