---
title: 仅在根级别的属性
description: 仅在根级别的属性
ms.assetid: 1b3d74b9-4cf4-4303-92ae-b93b3f9b7f7c
keywords:
- 仅限根级别属性 WDK Unidrv
- 常规打印机属性 WDK Unidrv，仅限根级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bdc070685c8330b63289f20725f26c12dbcde67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533943"
---
# <a name="root-level-only-attributes"></a>仅在根级别的属性





仅在根级别的属性是[常规属性](general-attributes.md)，用于描述资源文件、 帮助文件或其他包含的 GPD 文件的名称作为此类特定于驱动程序的特征以及使用的驱动程序规范主单位、 版本号和字符代码页。

仅限根级别的其他属性指定此类特定于设备的特征为打印机的名称、 类型、 最大复制容量和字体盒的槽数。

这些属性称为仅限根级别的属性，因为它们必须始终放置在根级别 GPD 文件 (即，而不是在大括号)。

下表列出了仅在根级别的属性。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名称</th>
<th>AttributeParameter</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>CodePage</strong></p></td>
<td><p>Microsoft Windows SDK 文档中所述的数字值的 Windows 代码页标识符。</p></td>
<td><p>可选。 如果未指定，则使用 Unicode。 代码页被应用到所有显示的字符串。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>FontCartSlots</strong></p></td>
<td><p>表示提供的打印机的字体磁带盒插槽数的数字值。</p></td>
<td><p>可选。 如果未指定，默认值为零。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>GPDFileName</strong></p></td>
<td><p>带引号的文本字符串，表示 GPD 文件名称 （不带路径）。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>GPDFileVersion</strong></p></td>
<td><p>带引号的文本字符串，表示当前 GPD 文件版本。 建议的格式是<em>MajorVersion</em>。<em>MinorVersion</em>，如&quot;1.0&quot;。</p></td>
<td><p>可选。 如果指定，此字符串将显示在 Unidrv&#39;关于对话框的 s。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>GPDSpecVersion</strong></p></td>
<td><p>带引号的文本字符串，表示当前 GPD 规范版本。 所需格式为<em>MajorVersion</em>。<em>MinorVersion</em>，如&quot;1.0&quot;。</p></td>
<td><p>必需。 必须在 GPD 文件中，在任何注释前的第一个条目。</p>
<p>此值必须是&quot;1.0&quot;适用于 Windows 2000。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>HelpFile</strong></p></td>
<td><p>包含名称的自定义的帮助文件，扩展名为.hlp 带引号的字符串。</p></td>
<td><p>可选。 如果包含，它可以添加主题或覆盖 Unidrv 中的现有主题&#39;s 帮助文件。 指定了帮助文件索引<em>HelpIndex 属性的功能和选项。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>Include</strong></p></td>
<td><p>带引号的字符串，其中包含一个额外的 GPD 文件的名称。</p></td>
<td><p>已过时。 此条目已重新定义为<a href="preprocessor-directives.md" data-raw-source="[preprocessor directive](preprocessor-directives.md)">预处理器指令</a>。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>InstalledOptionName</strong></p></td>
<td><p>带引号的字符串会显示以指示安装的功能或选项安装。 通常情况下，此字符串是&quot;已安装&quot;，但可以指定任何适当的字符串。</p></td>
<td><p>需要<em>可安装？ 是<strong>TRUE</strong>的任何功能或选项 (请参阅<a href="feature-attributes.md" data-raw-source="[Feature Attributes](feature-attributes.md)">功能属性</a>)，并且如果 *<strong>rcInstalledOptionNameID</strong>未指定。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>MasterUnits</strong></p></td>
<td><p>对表示打印机&#39;s<a href="master-units.md" data-raw-source="[master units](master-units.md)">掌握单位</a>。</p></td>
<td><p>必需。 若要减少潜在舍入误差，使用相同的值，为指定的解析单元中字体指标数据<em> <strong>MasterUnits</strong>。 (请参阅 Unidrv 字体中的指标<a href="customized-font-management.md" data-raw-source="[Customized Font Management](customized-font-management.md)">自定义字体管理</a>。)</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MaxCopies</strong></p></td>
<td><p>打印机能够支持包含数字值，该值表示最大副本数。</p></td>
<td><p>可选。 如果未指定，默认值为 1。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>ModelName</strong></p></td>
<td><p>带引号的文本字符串表示的打印机模型名称。</p></td>
<td><p>如果使用 *<strong>rcModelNameID</strong>未指定。 字符串必须与 setup.inf 名称匹配。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>NotInstalledOptionName</strong></p></td>
<td><p>带引号的字符串会显示以指示安装的功能或选项未安装。 通常情况下，此字符串是&quot;未安装&quot;，但可以指定任何适当的字符串。</p></td>
<td><p>需要<em><strong>可安装？</strong>是<strong>TRUE</strong>为任何功能或选项 (请参阅<a href="feature-attributes.md" data-raw-source="[Feature Attributes](feature-attributes.md)">功能属性</a>)，并且如果 *<strong>rcNotInstalledOptionNameID</strong>未指定。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>个性</strong></p></td>
<td><p>带引号的字符串表示打印机所使用的打印机语言。</p></td>
<td><p>可选。 如果指定，该字符串被显示目录服务。 另请参阅<em>rcPersonalityID。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PrinterType</strong></p></td>
<td><p>页中，串行端口或 TTY</p></td>
<td><p>必需。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>PrintRate</strong></p></td>
<td><p>数字值，该值表示单色打印速度。 通过指定单位 *<strong>PrintRateUnit</strong>。</p></td>
<td><p>可选。 如果未指定，默认值为 0。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PrintRatePPM</strong></p></td>
<td><p>表示的打印速度，以每分钟页数的数字值。</p></td>
<td><p>可选。 如果未指定，默认值为 0。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>PrintRateUnit</strong></p></td>
<td><p></p>
PPM 页面/分为单位 CPS-字符/sec。 LPM 行/分为单位 IPM-英寸/最小值。（对于绘图仪是 IPM）</td>
<td><p>如果使用 *<strong>PrintRate</strong>指定。 指定的单元应匹配的打印机类型。 例如，应为页面打印机指定 PPM。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>rcInstalledOptionNameID</strong></p></td>
<td><p>安装显示以指示安装的功能或选项的字符串资源的资源 ID。 通常情况下，此字符串是&quot;已安装&quot;，但可以指定任何适当的字符串。</p></td>
<td><p>需要<em>可安装？ 是<strong>TRUE</strong>的任何功能或选项 (请参阅<a href="feature-attributes.md" data-raw-source="[Feature Attributes](feature-attributes.md)">功能属性</a>)，并且如果 *<strong>InstalledOptionName</strong>未指定。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>rcNotInstalledOptionNameID</strong></p></td>
<td><p>未安装的显示以指示安装的功能或选项的字符串资源的资源 ID。 通常情况下，此字符串是&quot;未安装&quot;，但可以指定任何适当的字符串。</p></td>
<td><p>需要<em><strong>可安装？</strong>是<strong>TRUE</strong>为任何功能或选项 (请参阅<a href="feature-attributes.md" data-raw-source="[Feature Attributes](feature-attributes.md)">功能属性</a>)，并且如果 *<strong>NotInstalledOptionName</strong>未指定。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>rcPersonalityID</strong></p></td>
<td><p>表示打印机所使用的打印机语言的字符串资源的资源 ID。</p></td>
<td><p>可选。 如果指定，该字符串被显示目录服务。 另请参阅<em>个性。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>rcPrinterIconID</strong></p></td>
<td><p>表示与打印机相关联的图标的 RC_ICON 资源的资源 ID。</p></td>
<td><p>可选。 如果未指定，将显示默认打印机图标。 建议所有 RC_ICON 资源 Id 为连续从 1 开始都编号。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ResourceDLL</strong></p></td>
<td><p>带引号的字符串，其中包含的名称，而无需的资源 DLL 的路径信息。</p></td>
<td><p>可选。 请参阅<a href="using-resource-dlls-in-a-minidriver.md" data-raw-source="[Using Resource DLLs in a Minidriver](using-resource-dlls-in-a-minidriver.md)">微型驱动程序中使用资源 Dll</a>。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

Windows Vista 新的仅限根级别属性的信息，请参阅[Root-Level-Only GPD 属性于 Windows Vista 的新](new-root-level-only-gpd-attributes-for-windows-vista.md)并[新 Root-Level-Only PPD 属性适用于 Windows Vista 的](new-root-level-only-ppd-attributes-for-windows-vista.md)。

 

 




