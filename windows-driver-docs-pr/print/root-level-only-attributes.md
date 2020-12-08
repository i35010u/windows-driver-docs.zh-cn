---
title: 仅限根级别的属性
description: 仅限根级别的属性
keywords:
- 仅限根级别的属性 WDK Unidrv
- 常规打印机属性 WDK Unidrv，仅限根级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c37d1793ffb405a98db33c8caa1944547dfecb6f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807011"
---
# <a name="root-level-only-attributes"></a>仅限根级别的属性





仅限根级别的属性是 [常规属性](general-attributes.md) ，这些属性将此类特定于驱动程序的特征描述为资源文件、帮助文件或其他包含的 GPD 文件的名称，以及驱动程序的主单元、版本号和字符代码页的规格。

其他仅限根级别的属性将此类特定于设备的特性指定为打印机的名称、类型、最大复制容量和字体盒槽数。

这些属性被称为仅限根级别的属性，因为它们必须始终放在 GPD 文件中的根级别 (即，不在大括号) 内。

下表列出了仅限根级别的属性。

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
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>Ansi</strong></p></td>
<td><p>数值 Windows 代码页标识符，如 Microsoft Windows SDK 文档中所述。</p></td>
<td><p>可选。 如果未指定，则使用 Unicode。 代码页应用于所有显示的字符串。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>FontCartSlots</strong></p></td>
<td><p>数值，表示打印机提供的字体盒插槽的数目。</p></td>
<td><p>可选。 如果未指定，则默认值为零。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>GPDFileName</strong></p></td>
<td><p>用引用的文本字符串表示 GPD 文件名， (没有路径) 。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>GPDFileVersion</strong></p></td>
<td><p>表示当前 GPD 文件版本的带引号的文本字符串。 建议的格式为 <em>MajorVersion</em>。<em>MinorVersion</em>，例如 "1.0"。</p></td>
<td><p>可选。 如果已指定，则此字符串显示在 Unidrv 的 "关于" 对话框中。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>GPDSpecVersion</strong></p></td>
<td><p>表示当前 GPD 规范版本的带引号的文本字符串。 所需的格式为 <em>MajorVersion</em>。<em>MinorVersion</em>，例如 "1.0"。</p></td>
<td><p>必需。 必须是 GPD 文件中的第一个条目，然后才能进行任何注释。</p>
<p>对于 Windows 2000，此值必须为 "1.0"。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>帮助</strong></p></td>
<td><p>带引号的字符串，其中包含扩展名为 .hlp 的自定义帮助文件的名称。</p></td>
<td><p>可选。 如果包含，它可以在 Unidrv 的帮助文件中添加主题或覆盖现有主题。 帮助文件索引由 <em> 功能和选项的 HelpIndex 属性指定。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>包括</strong></p></td>
<td><p>带引号的字符串，其中包含其他 GPD 文件的名称。</p></td>
<td><p>已过时。 已将此项重新定义为 <a href="preprocessor-directives.md" data-raw-source="[preprocessor directive](preprocessor-directives.md)">预处理器指令</a>。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>InstalledOptionName</strong></p></td>
<td><p>用引号括起来的字符串，用于指示安装的功能或选项已安装。 通常，此字符串为 "已安装"，但可以指定任何相应的字符串。</p></td>
<td><p>如果 <em> "可安装" 为 <strong>TRUE</strong> ，则对于任何功能或选项 (参阅 <a href="feature-attributes.md" data-raw-source="[Feature Attributes](feature-attributes.md)">功能特性</a>) ，如果未指定 *<strong>rcInstalledOptionNameID</strong> ，则是必需的。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>MasterUnits</strong></p></td>
<td><p>表示打印机的 <a href="master-units.md" data-raw-source="[master units](master-units.md)">主单位</a>的配对。</p></td>
<td><p>必需。 若要减少可能的舍入错误，请在为 MasterUnits 指定的字体度量值数据中使用相同的值 <em> <strong>MasterUnits</strong>。  (参阅 <a href="customized-font-management.md" data-raw-source="[Customized Font Management](customized-font-management.md)">自定义字体管理</a>中的 Unidrv 字体指标 ) </p></td>
</tr>
<tr class="even">
<td><p></em><strong>MaxCopies</strong></p></td>
<td><p>数值，表示打印机可以支持的最大副本数。</p></td>
<td><p>可选。 如果未指定，则默认值为1。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>ModelName</strong></p></td>
<td><p>表示打印机型号名称的带引号的文本字符串。</p></td>
<td><p>如果未指定 *<strong>rcModelNameID</strong> ，则为必需。 String 必须与 setup.exe 中的名称匹配。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>NotInstalledOptionName</strong></p></td>
<td><p>用引号括起来的字符串，用于指示未安装可安装的功能或选项。 通常，此字符串为 "未安装"，但可以指定任何相应的字符串。</p></td>
<td><p>如果 <em> <strong>"可安装"</strong>为<strong>TRUE</strong> ，则对于任何功能或选项 (参阅<a href="feature-attributes.md" data-raw-source="[Feature Attributes](feature-attributes.md)">功能特性</a>) ，如果未指定 *<strong>rcNotInstalledOptionNameID</strong> ，则是必需的。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>个性</strong></p></td>
<td><p>带引号的字符串，表示打印机使用的打印机语言。</p></td>
<td><p>可选。 如果已指定，则由目录服务显示该字符串。 另请参阅 <em> rcPersonalityID。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PrinterType</strong></p></td>
<td><p>PAGE、SERIAL 或 TTY</p></td>
<td><p>必需。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>PrintRate</strong></p></td>
<td><p>表示单色打印速率的数值。 单位由 *<strong>PrintRateUnit</strong>指定。</p></td>
<td><p>可选。 如果未指定，则默认值为 0。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PrintRatePPM</strong></p></td>
<td><p>表示打印速度的数值，以每分钟的页数表示。</p></td>
<td><p>可选。 如果未指定，则默认值为 0。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>PrintRateUnit</strong></p></td>
<td><p></p>
PPM-每个页面/最小为 CPS-每秒-每秒-每秒的最小 IPM-英寸/分钟 (IPM 适用于绘图仪) </td>
<td><p>如果指定 *<strong>PrintRate</strong> ，则是必需的。 指定的单位应匹配打印机类型。 例如，应为页面打印机指定 PPM。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>rcInstalledOptionNameID</strong></p></td>
<td><p>显示用于指示安装的功能或选项的字符串资源的资源 ID。 通常，此字符串为 "已安装"，但可以指定任何相应的字符串。</p></td>
<td><p>如果 <em> "可安装" 为 <strong>TRUE</strong> ，则对于任何功能或选项 (参阅 <a href="feature-attributes.md" data-raw-source="[Feature Attributes](feature-attributes.md)">功能特性</a>) ，如果未指定 *<strong>InstalledOptionName</strong> ，则是必需的。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>rcNotInstalledOptionNameID</strong></p></td>
<td><p>显示用于指示安装的功能或选项的字符串资源的资源 ID。 通常，此字符串为 "未安装"，但可以指定任何相应的字符串。</p></td>
<td><p>如果 <em> <strong>"可安装"</strong>为<strong>TRUE</strong> ，则对于任何功能或选项 (参阅<a href="feature-attributes.md" data-raw-source="[Feature Attributes](feature-attributes.md)">功能特性</a>) ，如果未指定 *<strong>NotInstalledOptionName</strong> ，则是必需的。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>rcPersonalityID</strong></p></td>
<td><p>表示打印机使用的打印机语言的字符串资源的资源 ID。</p></td>
<td><p>可选。 如果已指定，则由目录服务显示该字符串。 另请参阅 <em> 个性。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>rcPrinterIconID</strong></p></td>
<td><p>表示与打印机关联的图标的 RC_ICON 资源的资源 ID。</p></td>
<td><p>可选。 如果未指定，则显示默认打印机图标。 建议所有 RC_ICON 的资源 Id 从1开始连续编号。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ResourceDLL</strong></p></td>
<td><p>带引号的字符串，其中包含资源 DLL 的名称，但不包含路径信息。</p></td>
<td><p>可选。 请参阅 <a href="using-resource-dlls-in-a-minidriver.md" data-raw-source="[Using Resource DLLs in a Minidriver](using-resource-dlls-in-a-minidriver.md)">在微型驱动程序中使用资源 dll</a>。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

有关 Windows vista 的新仅限根级别的属性的信息，请参阅适用于 [Windows vista 的新的仅](new-root-level-only-gpd-attributes-for-windows-vista.md) 限根级别的 GPD 属性和 [适用于 Windows vista 的新的仅限根级别的 PPD 属性](new-root-level-only-ppd-attributes-for-windows-vista.md)。

 

 




