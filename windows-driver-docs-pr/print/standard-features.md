---
title: 标准功能
description: 标准功能
ms.assetid: 5cd90992-5ab8-4cb3-89b0-19e58e55b652
keywords:
- 打印机功能 WDK Unidrv，standard
- 标准功能 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 646e2238dc7ad78a8cf9f9de8cabfeede14369a3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213115"
---
# <a name="standard-features"></a>标准功能





标准功能是大多数打印机通常提供的 [打印机功能](printer-features.md) 。 它们由 GPD 语言识别的预定义名称标识。 表示这些名称的字符串 (资源标识符包含在 Microsoft Windows 驱动程序工具包 WDK 随附的 gpd 中 \[ \] 。 ) 某些标准功能是必需的，并且必须为每台打印机指定。 其他选项是可选的。

下表按字母顺序列出了所有标准功能，并指示每个功能是否接受标准选项或自定义选项。 包含 Print Schema 关键字的功能 GPD 自动映射到打印架构关键字的功能。 还可以通过使用 PrintSchemaKeywordMap 属性，将 GPD 功能映射为手动打印架构关键字。 打印架构记录在 Microsoft Windows SDK。

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
<th>说明</th>
<th>标准选项</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>逐份打印</strong></p></td>
<td><p><strong>DocumentCollate</strong></p></td>
<td><p>页排序规则</p></td>
<td><p>请参阅 <a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>不允许使用自定义选项。</p></td>
<td><p>可选。 如果未指定，则 Unidrv 不支持页排序规则。</p></td>
</tr>
<tr class="even">
<td><p><strong>ColorMode</strong></p></td>
<td><p><strong>PageOutputColor</strong></p></td>
<td><p>彩色打印模式</p></td>
<td><p>无。 所有选项都是自定义的。 另请参阅 <a href="option-attributes-for-the-colormode-feature.md" data-raw-source="[Option Attributes for the ColorMode Feature](option-attributes-for-the-colormode-feature.md)">ColorMode 功能的选项属性</a>。</p></td>
<td><p>可选。 如果未指定此项，Unidrv 将以单平面1位/像素格式呈现图像。</p></td>
</tr>
<tr class="odd">
<td><p><strong>双工</strong></p></td>
<td><p><strong>JobDuplexAllDocumentsContiguously</strong></p></td>
<td><p>双面打印</p></td>
<td><p>请参阅 <a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>不允许使用自定义选项。</p></td>
<td><p>可选。 如果未指定，则 Unidrv 仅执行单面打印。</p></td>
</tr>
<tr class="even">
<td><p><strong>色</strong></p></td>
<td><p>无默认关键字。 使用 PrintSchemaKeywordMap 属性可分配 Print Schema 功能关键字。</p></td>
<td><p>半色调功能</p></td>
<td><p>请参阅 <a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>允许使用自定义选项。</p>
<p>另请参阅 <a href="option-attributes-for-the-halftone-feature.md" data-raw-source="[Option Attributes for the Halftone Feature](option-attributes-for-the-halftone-feature.md)">半色调功能的选项属性</a>。</p></td>
<td><p>可选。 如果未指定，Unidrv 将选择支持 GDI 的半色调方法。</p>
<p>另请参阅 <a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv 的半色调</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>InputBin</strong></p></td>
<td><p><strong>JobInputBin</strong></p></td>
<td><p>输入纸盒的类型</p></td>
<td><p>请参阅 <a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>允许使用自定义选项。</p>
<p>另请参阅 <a href="option-attributes-for-the-inputbin-feature.md" data-raw-source="[Option Attributes for the InputBin Feature](option-attributes-for-the-inputbin-feature.md)">InputBin 功能的选项属性</a>。</p></td>
<td><p>必需。</p>
<p>自定义的输入箱名称必须小于或等于24个字符。</p></td>
</tr>
<tr class="even">
<td><p><strong>MediaType</strong></p></td>
<td><p><strong>PageMediaType</strong></p></td>
<td><p>打印介质的类型</p></td>
<td><p>请参阅 <a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>允许使用自定义选项。</p></td>
<td><p>可选。 如果未指定，则始终使用打印机的默认介质。</p></td>
</tr>
<tr class="odd">
<td><p><strong>内存</strong></p></td>
<td><p>无默认关键字。 使用 PrintSchemaKeywordMap 属性可分配 Print Schema 功能关键字。</p></td>
<td><p>打印机内存配置</p></td>
<td><p>所有选项都是自定义的。 另请参阅 <a href="option-attributes-for-the-memory-feature.md" data-raw-source="[Option Attributes for the Memory Feature](option-attributes-for-the-memory-feature.md)">内存功能的选项属性</a>。</p></td>
<td><p>可选。 如果指定，Unidrv 将尝试跟踪内存使用情况。</p>
<p>默认值为 PRINTER_PROPERTY。</p></td>
</tr>
<tr class="even">
<td><p><strong>打印</strong></p></td>
<td><p><strong>PageOrientation</strong></p></td>
<td><p>纸张方向</p></td>
<td><p>请参阅 <a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>不允许使用自定义选项。</p></td>
<td><p>可选。 如果未指定，则默认方向为纵向。</p>
<p>对于 Windows 7， <strong>MxdcGetPDEVAdjustment</strong> 函数具有用于横向旋转的新参数。 有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment" data-raw-source="[&lt;strong&gt;MxdcXDCGetPDEVAdjustment&lt;/strong&gt;](/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)"><strong>MxdcXDCGetPDEVAdjustment</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutputBin</strong></p></td>
<td><p><strong>JobOutputBin</strong></p></td>
<td><p>输出容器类型</p></td>
<td><p>无。 所有选项都是自定义的。</p>
<p>另请参阅 <a href="option-attributes-for-the-outputbin-feature.md" data-raw-source="[Option Attributes for the OutputBin Feature](option-attributes-for-the-outputbin-feature.md)">OutputBin 功能的选项属性</a>。</p></td>
<td><p>可选。 如果未指定，则 Unidrv 不会尝试选择一个输出 bin。</p></td>
</tr>
<tr class="even">
<td><p><strong>PageProtect</strong></p></td>
<td><p><strong>JobPageProtection</strong></p></td>
<td><p>启用当前打印页保护</p></td>
<td><p>请参阅 <a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>不允许使用自定义选项。</p></td>
<td><p>可选。 如果未指定，则默认值为 OFF。 仅当有足够的打印机内存可用时，Unidrv 才会启用页面保护。 默认值为 PRINTER_PROPERTY。 另请参阅 * PageProtectMem。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PaperSize</strong></p></td>
<td><p><strong>PageMediaSize</strong></p></td>
<td><p>纸张大小</p></td>
<td><p>请参阅 <a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">标准选项</a>。</p>
<p>允许使用自定义选项。</p>
<p>另请参阅 <a href="option-attributes-for-the-papersize-feature.md" data-raw-source="[Option Attributes for the PaperSize Feature](option-attributes-for-the-papersize-feature.md)">PaperSize 功能的选项属性</a>。</p></td>
<td><p>必需。 必须至少指定一个选项。 CUSTOMSIZE 选项允许打印机用户指定纸张大小。</p></td>
</tr>
<tr class="even">
<td><p><strong>RESDLL</strong></p></td>
<td><p>此功能无法映射到打印架构关键字。</p></td>
<td><p>资源 Dll</p></td>
<td><p>所有选项都是自定义的。</p>
<p>请参阅 <a href="using-resource-dlls-in-a-minidriver.md" data-raw-source="[Using Resource DLLs in a Minidriver](using-resource-dlls-in-a-minidriver.md)">在微型驱动程序中使用资源 dll</a>。</p></td>
<td><p>可选。 另请参阅 * ResourceDLL。</p></td>
</tr>
<tr class="odd">
<td><p><strong>分辨率</strong></p></td>
<td><p><strong>PageResolution</strong></p></td>
<td><p>打印分辨率</p></td>
<td><p>所有选项都是自定义的。 另请参阅 <a href="option-attributes-for-the-resolution-feature.md" data-raw-source="[Option Attributes for the Resolution Feature](option-attributes-for-the-resolution-feature.md)">解决功能的选项属性</a>。</p></td>
<td><p>必需。 必须至少指定一个选项。</p></td>
</tr>
<tr class="even">
<td><p><strong>装订</strong></p></td>
<td><p><strong>JobStapleAllDocuments</strong></p></td>
<td><p>装订功能</p></td>
<td><p>所有选项都是自定义的。</p></td>
<td><p>可选。 如果已指定，则目录服务指示打印机支持装订。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

## <a name="related-topics"></a>相关主题
[示例 GPD 文件](sample-gpd-files.md)  
[V4 打印机驱动程序本地化](v4-driver-localization.md)