---
title: 功能属性
description: 功能属性
keywords:
- 打印机属性 WDK Unidrv，功能
- 功能 attribues WDK Unidrv
- 打印机功能 WDK Unidrv，属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4513f7081ae8c11ca2da192e5e67dae7ea4416d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836063"
---
# <a name="feature-attributes"></a>功能属性





指定打印机功能时，可以使用属性为 Unidrv 提供以下信息：

-   表示功能的显示名称的文本字符串。

-   与该功能关联的打印机选项集。

-   指示该功能是始终存在还是可安装的布尔值。

-   如果自定义功能，则为功能类型和优先级，指示在哪个属性表上显示该功能及其相对优先级。

下表按字母顺序列出了特征特性，并描述了它们的参数。

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
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><em>ConcealFromUI?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示是否应在用户界面中显示该功能。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>，这意味着将显示该功能。</p>
<p>仅当功能只有一个选项 (例如，一种解决方法) ，因此不能进行用户修改，或者，如果通过设置其他功能的选项来控制功能的选项，则应为 <strong>TRUE</strong> 。</p>
<p>如果将<strong> </em> ConcealFromUI</strong>特性设置为<strong>TRUE</strong>，则 Unidrv 或 PrintConfig 会将 psk： DISPLAYUI 元素添加到 PrintCapabilities XML 中该项的功能元素。</p></td>
</tr>
<tr class="even">
<td><p><strong><em>ConflictPriority</strong></p></td>
<td><p>表示功能优先级的数值，其中1表示最高优先级。</p></td>
<td><p>可选。 请参阅 <a href="feature-conflict-priority.md" data-raw-source="[Feature Conflict Priority](feature-conflict-priority.md)">功能冲突优先级</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>DefaultOption</strong></p></td>
<td><p>功能的一个选项的名称。</p></td>
<td><p>可选。 如果未指定，则默认情况下，功能项中列出的第一个选项 <em> 为默认值。 对于 PaperSize 功能，"Unidrv" 的默认选项是 "A4" 作为 "指标区域设置" 和 "字母"。 如果默认 PaperSize 不存在，则 Unidrv 将使用由 *<strong>DefaultOption</strong> 关键字指定的 PaperSize 选项。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>FeatureType</strong></p></td>
<td><p>DOC_PROPERTY</p>
<p>JOB_PROPERTY</p>
<p>PRINTER_PROPERTY</p>
<p>如果 DOC_PROPERTY 或 JOB_PROPERTY，则会将此功能分配给文档属性表。 如果 PRINTER_PROPERTY，则会将此功能分配给打印机属性表。</p></td>
<td><p>对于自定义功能是必需的。 对于标准功能是可选的。 如果未指定，则默认情况下将 DOC_PROPERTY 标准功能的默认值，除非另有说明。</p>
<p>如果 PRINTER_PROPERTY，则功能的选项值将保存在注册表中。 如果 DOC_PROPERTY 或 JOB_PROPERTY，则功能的选项值将与文档一起保存。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>HelpIndex</strong></p></td>
<td><p>数值，表示<strong>由 * 帮助</strong>文件 <a href="root-level-only-attributes.md" data-raw-source="[root-level-only attribute](root-level-only-attributes.md)">根级别属性</a>指定的帮助文件中的索引。</p></td>
<td><p> (也是 <a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。 ) </p></td>
</tr>
<tr class="even">
<td><p><strong></em>安装?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示是否可安装该功能。  (<strong>FALSE</strong> 表示始终安装。 ) </p>
<p>有关详细信息，请参阅 <a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装的功能和选项</a>。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。 如果 <strong>为 TRUE</strong>，则除指定的第一个选项外，所有功能的选项都是可安装的。 如果 <strong>为 FALSE</strong>，则还必须始终安装该功能的至少一个选项。  (也是 <a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。 ) </p></td>
</tr>
<tr class="odd">
<td><p><strong><em>InstallableFeatureName</strong></p></td>
<td><p>显示的文本字符串，询问用户是否实际安装了可安装的功能。</p>
<p>有关详细信息，请参阅 <a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装的功能和选项</a>。</p></td>
<td><p>如果 * 可<strong>安装？</strong> 为 <strong>TRUE</strong> 且未指定 *<strong>rcInstallableFeatureNameID</strong> ，则为必需。  (也是 <a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。 ) </p></td>
</tr>
<tr class="even">
<td><p><strong></em>“属性”</strong></p></td>
<td><p>用作该功能在打印机属性表上的显示名称的文本字符串。</p></td>
<td><p>可选。 如果未指定，则 <em> 必须指定<strong>rcNameID</strong> 。  (也是 <a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。 ) </p></td>
</tr>
<tr class="odd">
<td><p><strong></em>选项</strong></p></td>
<td><p>选项参数，如 <a href="option-entry-format.md" data-raw-source="[Option Entry Format](option-entry-format.md)">选项输入格式</a>中所述。</p></td>
<td><p>必需。 <strong> <em> </strong> 对与该功能关联的每个选项使用选项条目。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>rcIconID</strong></p></td>
<td><p>与该功能关联的图标资源的资源 ID。</p></td>
<td><p>可选。 如果未指定，则 Unidrv 不在打印机属性表上显示该功能的图标。  (也是 <a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。 ) </p></td>
</tr>
<tr class="odd">
<td><p><strong><em>rcInstallableFeatureNameID</strong></p></td>
<td><p>显示的文本字符串的资源 ID，询问用户是否实际安装了可安装的功能。</p>
<p>有关详细信息，请参阅 <a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装的功能和选项</a>。</p></td>
<td><p>如果 * 可<strong>安装？</strong> 为 <strong>TRUE</strong> 且未指定 *<strong>InstallableFeatureName</strong> ，则为必需。  (也是 <a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。 ) </p></td>
</tr>
<tr class="even">
<td><p><strong></em>rcNameID</strong></p></td>
<td><p>表示功能名称的字符串资源的资源 ID。  (零不是有效的资源 ID。 ) </p></td>
<td><p>可选。 如果未指定，则 <em> 必须指定<strong>名称</strong>。  (也是 <a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">选项属性</a>。 ) </p></td>
</tr>
<tr class="odd">
<td><p><strong></em>UpdateQualityMacro?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示是否在指定质量设置的条件语句中包含功能 (参见 <a href="controlling-image-quality.md" data-raw-source="[Controlling Image Quality](controlling-image-quality.md)">控制图像质量</a>) 。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。  (如果此功能包含在指定质量设置的条件语句中，则该值将强制为 <strong>TRUE</strong> 。 ) </p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 




