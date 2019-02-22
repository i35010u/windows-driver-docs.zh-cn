---
title: 标准功能
description: 标准功能
ms.assetid: 5cd90992-5ab8-4cb3-89b0-19e58e55b652
keywords:
- 打印机功能 WDK Unidrv，标准
- 标准功能，WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fd594419c0b56da317510885aa600983e84469c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546820"
---
# <a name="standard-features"></a>标准功能





标准功能都[打印机功能](printer-features.md)通常提供的大多数打印机。 它们由 GPD 语言可识别的预定义名称标识。 (Stdnames.gpd，它提供与 Microsoft Windows 驱动程序工具包中包含表示这些名称的字符串的资源标识符\[WDK\]。)某些标准功能所需，并且必须指定每个打印机。 其他人是可选的。

下表列出了所有标准功能，按字母顺序，并指示每个功能是否接受标准选项或自定义的选项。 包含了打印架构的关键字的功能是 gpd 分析功能，将自动映射到打印架构的关键字。 您还可以映射 GPD 功能到打印架构关键字手动使用 PrintSchemaKeywordMap 属性。 打印架构记录在 Microsoft Windows SDK 中。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>功能名称</th>
<th>默认打印架构功能关键字</th>
<th>描述</th>
<th>标准选项</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>逐份打印</strong></p></td>
<td><p><strong>DocumentCollate</strong></p></td>
<td><p>页的排序规则</p></td>
<td><p>请参阅<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>不允许使用自定义的选项。</p></td>
<td><p>可选。 如果未指定，Unidrv 不支持页排序规则。</p></td>
</tr>
<tr class="even">
<td><p><strong>ColorMode</strong></p></td>
<td><p><strong>PageOutputColor</strong></p></td>
<td><p>彩色打印模式</p></td>
<td><p>无。 自定义的所有选项。 另请参阅<a href="option-attributes-for-the-colormode-feature.md" data-raw-source="[Option Attributes for the ColorMode Feature](option-attributes-for-the-colormode-feature.md)">ColorMode 功能的选项属性</a>。</p></td>
<td><p>可选。 如果未指定，Unidrv 单平面，1 位每像素的格式呈现图像。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Duplex</strong></p></td>
<td><p><strong>JobDuplexAllDocumentsContiguously</strong></p></td>
<td><p>双面打印</p></td>
<td><p>请参阅<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>不允许使用自定义的选项。</p></td>
<td><p>可选。 如果未指定，Unidrv 执行仅单面打印。</p></td>
</tr>
<tr class="even">
<td><p><strong>Halftone</strong></p></td>
<td><p>任何默认的关键字。 使用 PrintSchemaKeywordMap 属性分配一个打印架构功能关键字。</p></td>
<td><p>半色调功能</p></td>
<td><p>请参阅<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>允许自定义的选项。</p>
<p>另请参阅<a href="option-attributes-for-the-halftone-feature.md" data-raw-source="[Option Attributes for the Halftone Feature](option-attributes-for-the-halftone-feature.md)">半色调功能的选项属性</a>。</p></td>
<td><p>可选。 如果未指定，Unidrv 选择 GDI 支持半色调方法。</p>
<p>另请参阅<a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv 与半色调</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>InputBin</strong></p></td>
<td><p><strong>JobInputBin</strong></p></td>
<td><p>类型的送纸盒</p></td>
<td><p>请参阅<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>允许自定义的选项。</p>
<p>另请参阅<a href="option-attributes-for-the-inputbin-feature.md" data-raw-source="[Option Attributes for the InputBin Feature](option-attributes-for-the-inputbin-feature.md)">InputBin 功能的选项属性</a>。</p></td>
<td><p>必需。</p>
<p>自定义的送纸器名称必须是 24 个字符或更少。</p></td>
</tr>
<tr class="even">
<td><p><strong>MediaType</strong></p></td>
<td><p><strong>PageMediaType</strong></p></td>
<td><p>类型的打印介质</p></td>
<td><p>请参阅<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>允许自定义的选项。</p></td>
<td><p>可选。 如果未指定，打印机&#39;始终使用 s 默认介质。</p></td>
</tr>
<tr class="odd">
<td><p><strong>内存</strong></p></td>
<td><p>任何默认的关键字。 使用 PrintSchemaKeywordMap 属性分配打印架构功能关键字。</p></td>
<td><p>打印机内存配置</p></td>
<td><p>自定义的所有选项。 另请参阅<a href="option-attributes-for-the-memory-feature.md" data-raw-source="[Option Attributes for the Memory Feature](option-attributes-for-the-memory-feature.md)">内存功能的选项属性</a>。</p></td>
<td><p>可选。 如果指定，Unidrv 尝试来跟踪内存使用情况。</p>
<p>默认 * 的 FeatureType 值是 PRINTER_PROPERTY。</p></td>
</tr>
<tr class="even">
<td><p><strong>方向</strong></p></td>
<td><p><strong>PageOrientation</strong></p></td>
<td><p>不同方向的纸张</p></td>
<td><p>请参阅<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>不允许使用自定义的选项。</p></td>
<td><p>可选。 如果未指定，默认方向为纵向。</p>
<p>适用于 Windows 7 <strong>MxdcGetPDEVAdjustment</strong>函数具有横向旋转的新参数。 有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff557558" data-raw-source="[&lt;strong&gt;MxdcXDCGetPDEVAdjustment&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557558)"> <strong>MxdcXDCGetPDEVAdjustment</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutputBin</strong></p></td>
<td><p><strong>JobOutputBin</strong></p></td>
<td><p>类型的输出纸盒</p></td>
<td><p>无。 自定义的所有选项。</p>
<p>另请参阅<a href="option-attributes-for-the-outputbin-feature.md" data-raw-source="[Option Attributes for the OutputBin Feature](option-attributes-for-the-outputbin-feature.md)">OutputBin 功能的选项属性</a>。</p></td>
<td><p>可选。 如果未指定，Unidrv 不会尝试选择收纸器。</p></td>
</tr>
<tr class="even">
<td><p><strong>PageProtect</strong></p></td>
<td><p><strong>JobPageProtection</strong></p></td>
<td><p>使当前打印页的保护</p></td>
<td><p>请参阅<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>不允许使用自定义的选项。</p></td>
<td><p>可选。 如果未指定，默认值为 OFF。 Unidrv 仅启用页保护，如果打印机内存不足，不可用。 默认 * 的 FeatureType 值是 PRINTER_PROPERTY。 另请参阅 * PageProtectMem。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PaperSize</strong></p></td>
<td><p><strong>PageMediaSize</strong></p></td>
<td><p>纸张大小</p></td>
<td><p>请参阅<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>允许自定义的选项。</p>
<p>另请参阅<a href="option-attributes-for-the-papersize-feature.md" data-raw-source="[Option Attributes for the PaperSize Feature](option-attributes-for-the-papersize-feature.md)">PaperSize 功能的选项属性</a>。</p></td>
<td><p>必需。 必须指定至少一个选项。 CUSTOMSIZE 选项允许打印机用户指定纸张大小。</p></td>
</tr>
<tr class="even">
<td><p><strong>RESDLL</strong></p></td>
<td><p>此功能不能映射到打印架构关键字。</p></td>
<td><p>资源 Dll</p></td>
<td><p>自定义的所有选项。</p>
<p>请参阅<a href="using-resource-dlls-in-a-minidriver.md" data-raw-source="[Using Resource DLLs in a Minidriver](using-resource-dlls-in-a-minidriver.md)">微型驱动程序中使用资源 Dll</a>。</p></td>
<td><p>可选。 另请参阅 * 项 ResourceDLL。</p></td>
</tr>
<tr class="odd">
<td><p><strong>解决方法</strong></p></td>
<td><p><strong>PageResolution</strong></p></td>
<td><p>打印的解决方法</p></td>
<td><p>自定义的所有选项。 另请参阅<a href="option-attributes-for-the-resolution-feature.md" data-raw-source="[Option Attributes for the Resolution Feature](option-attributes-for-the-resolution-feature.md)">解析功能的选项属性</a>。</p></td>
<td><p>必需。 必须指定至少一个选项。</p></td>
</tr>
<tr class="even">
<td><p><strong>Stapling</strong></p></td>
<td><p><strong>JobStapleAllDocuments</strong></p></td>
<td><p>装订功能</p></td>
<td><p>自定义的所有选项。</p></td>
<td><p>可选。 如果指定，目录服务指示打印机支持装订。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

## <a name="related-topics"></a>相关主题
[示例 GPD 文件](sample-gpd-files.md)  
[V4 打印机驱动程序本地化](v4-driver-localization.md)  



