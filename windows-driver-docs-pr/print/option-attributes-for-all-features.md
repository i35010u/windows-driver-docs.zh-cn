---
title: 所有功能的选项属性
description: 所有功能的选项属性
ms.assetid: 0d269fdf-f4a1-431a-9f07-044289b9f0fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b980d1a091135d1455a162edcba7be0a9c5cdbf
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802445"
---
# <a name="option-attributes-for-all-features"></a>所有功能的选项属性





下表按字母顺序列出了适用于所有功能的 [选项属性](option-attributes.md) ，并介绍了其参数。

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
<td><p><em><strong>Command</strong></p></td>
<td><p><strong>CmdSelect</strong> <a href="option-selection-command.md" data-raw-source="[option selection command](option-selection-command.md)">选项选择命令</a>，指定必须发送到打印机才能选择选项的命令字符串。</p></td>
<td><p>必需。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>DisabledFeatures</strong></p></td>
<td><p>功能名称字符串列表，用于标识在选择该选项时应禁用的功能。</p>
<p>当前支持双工和逐份功能。 此选项特性必须用于将 FeatureType 设置为 PRINTER_PROPERTY 的功能。</p></td>
<td><p>可选。</p>
<p>列出的功能不能 <em> <strong>"可安装"</strong>设置为 " <strong>TRUE</strong>"。 有关详细信息，请参阅 <a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装的功能和选项</a>。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>HelpIndex</strong></p></td>
<td><p>数值，表示由 "帮助文件 <em> <strong>HelpFile</strong><a href="root-level-only-attributes.md" data-raw-source="[root-level-only attribute](root-level-only-attributes.md)">根级别" 属性</a>指定的帮助文件中的索引。</p></td>
<td><p> (也是 <a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能属性</a>。 ) </p>
<p>索引值不能为零或-1。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>安装?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>，指示选项是否可安装。  (<strong>FALSE</strong> 表示始终安装。 ) </p>
<p>有关详细信息，请参阅 <a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装的功能和选项</a>。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。  (也是 <a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能属性</a>。 ) </p></td>
</tr>
<tr class="odd">
<td><p><em><strong>InstallableFeatureName</strong></p></td>
<td><p>显示的文本字符串，询问用户是否实际安装了 "可安装" 选项。</p>
<p>有关详细信息，请参阅 <a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装的功能和选项</a>。</p></td>
<td><p>如果 * 可<strong>安装？</strong> 为 <strong>TRUE</strong> 且未指定 *<strong>rcInstallableFeatureNameID</strong> ，则为必需。  (也是 <a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能属性</a>。 ) </p></td>
</tr>
<tr class="even">
<td><p></em><strong>名称</strong></p></td>
<td><p>用作选项在打印机属性表上的显示名称的文本字符串。</p></td>
<td><p>可选。 如果未指定，则 <em> 必须指定<strong>rcNameID</strong> 。  (也是 <a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能属性</a>。 ) </p></td>
</tr>
<tr class="odd">
<td><p></em><strong>OptionID</strong></p></td>
<td><p>数值，表示 Unidrv 存储在打印机的 <a href="https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew)"><strong>DEVMODEW</strong></a> 结构中的唯一选项标识符。 仅用于 PaperSize、InputSlot、半色调和媒体的功能。 值分别存储在 DEVMODE 结构的 <strong>dmPaperSize</strong>、 <strong>dmDefaultSource</strong>、 <strong>dmDitherType</strong>或 <strong>dmMediaType</strong> 成员中。</p></td>
<td><p>可选。 如果未指定，Unidrv 将 (256) 指定标识符值 &gt; 。 若要避免与 Unidrv 分配的标识符冲突，指定的值必须大于512。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>rcIconID</strong></p></td>
<td><p>与选项关联的图标资源的资源 ID。</p></td>
<td><p>可选。 如果未指定，则 Unidrv 不显示打印机属性表上的选项的图标。  (也是 <a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能属性</a>。 ) </p></td>
</tr>
<tr class="odd">
<td><p></em><strong>rcInstallableFeatureNameID</strong></p></td>
<td><p>显示的文本字符串的资源 ID，询问用户是否实际安装了可安装的选项。</p>
<p>有关详细信息，请参阅 <a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">处理可安装的功能和选项</a>。</p></td>
<td><p>如果 <em> <strong>"可安装"</strong>为<strong>TRUE</strong>且未指定 *<strong>InstallableFeatureName</strong> ，则是必需的。  (也是 <a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能属性</a>。 ) </p></td>
</tr>
<tr class="even">
<td><p></em><strong>rcNameID</strong></p></td>
<td><p>表示选项名称的字符串资源的资源 ID。</p></td>
<td><p>可选。 如果未指定，则必须指定 *<strong>名称</strong> 。  (也是 <a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">功能属性</a>。 ) </p>
<p>对于 PaperSize 功能的 <a href="standard-options.md" data-raw-source="[standard options](standard-options.md)">标准选项</a> ，将此特性设置为 RCID_DMPAPER_SYSTEM_NAME 会导致 Unidrv 使用预定义的选项名称字符串。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 




