---
title: WIA \_ IPA \_ 项 \_ 类别
description: WIA \_ IPA \_ ITEM \_ CATEGORY 属性包含 wia 项的分组类别。
ms.assetid: 0dde5e1c-ac30-4129-96fb-89ce1950c29b
keywords:
- WIA_IPA_ITEM_CATEGORY 图像设备
topic_type:
- apiref
api_name:
- WIA_IPA_ITEM_CATEGORY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c4e484708b883ac9fa32ea9c090a7066c421d80
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103162"
---
# <a name="wia_ipa_item_category"></a>WIA \_ IPA \_ 项 \_ 类别


WIA \_ IPA \_ ITEM \_ CATEGORY 属性包含 wia 项的分组类别。

## <span id="ddk_wia_ipa_item_category_si"></span><span id="DDK_WIA_IPA_ITEM_CATEGORY_SI"></span>


属性类型： VT \_ CLSID

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

WIA 微型驱动程序创建并维护此属性。

WIA 定义以下类别：

<span id="WIA_CATEGORY_BARCODE_READER"></span><span id="wia_category_barcode_reader"></span>WIA \_ 类别 \_ 条形码 \_ 读取器  
作为可编程数据源的条码读取器项，已启用传输以下载条形码元数据。

<span id="WIA_CATEGORY_ENDORSER"></span><span id="wia_category_endorser"></span>WIA \_ 类别 \_ ENDORSER  
可编程数据源项的认可类别，该类别表示 imprinting 和认可，并且可以进行传输，以便上传和下载要打印/认可的数据内容。

<span id="WIA_CATEGORY_FEEDER"></span><span id="wia_category_feeder"></span>WIA \_ 类别 \_ 馈送器  
一个作为可编程数据源的馈送器项，遵循标准规则，并且具有支持文档送纸器所需的 WIA 属性。

<span id="WIA_CATEGORY_FEEDER_BACK"></span><span id="wia_category_feeder_back"></span>WIA \_ 类别 \_ 送 \_ 回  
一个可编程数据源项，用于描述双面打印器项 (WIA \_ 类别 \_ 送纸器) 的后端数据源。

<span id="WIA_CATEGORY_FEEDER_FRONT"></span><span id="wia_category_feeder_front"></span>WIA \_ 类别 \_ 馈送器 \_ 前面  
一个可编程数据源项，用于描述双面打印器项 (WIA \_ 类别 \_ 送纸器) 的前端数据源。

<span id="WIA_CATEGORY_FILM"></span><span id="wia_category_film"></span>WIA \_ 类别 \_ 胶片  
一个胶卷项，它是一个可编程数据源，遵循标准规则，并且具有支持胶片扫描单元所需的 WIA 属性。

<span id="WIA_CATEGORY_FINISHED_FILE"></span><span id="wia_category_finished_file"></span>WIA \_ 类别 \_ 完成 \_ 文件  
*不* 是可编程数据源。 设备以完成的文件格式或包含已完成文件格式项的文件夹项提供数据。

<span id="WIA_CATEGORY_FLATBED"></span><span id="wia_category_flatbed"></span>WIA \_ 类别 \_ 平板  
属于可编程数据源、遵循标准规则，并且具有支持平板影印扫描所需的 WIA 属性的平台项。

<span id="WIA_CATEGORY_FOLDER"></span><span id="wia_category_folder"></span>WIA \_ 类别 \_ 文件夹  
文件夹存储项 (不是包含其他文件夹项和/或已完成文件的可编程数据源) 。

<span id="WIA_CATEGORY_IMPRINTER"></span><span id="wia_category_imprinter"></span>WIA \_ 类别 \_ IMPRINTER  
可编程数据源项的 "imprinting" 类别，该类别表示 "imprinting" 和 "认可"，并且可以进行传输，以便上传和下载要打印/认可的数据内容。

<span id="WIA_CATEGORY_MICR_READER"></span><span id="wia_category_micr_reader"></span>WIA \_ 类别 \_ 磁墨 \_ 读取器  
一种 (磁性墨迹字符识别功能，) 磁墨读取器项为可编程数据源，已启用传输以下载磁墨文本。

<span id="WIA_CATEGORY_PATCH_CODE_READER"></span><span id="wia_category_patch_code_reader"></span>WIA \_ 类别 \_ 修补程序 \_ 代码 \_ 读取器  
作为可编程数据源的修补程序代码读取器项，已启用传输来下载修补程序代码元数据。

<span id="WIA_CATEGORY_ROOT"></span><span id="wia_category_root"></span>WIA \_ 类别 \_ 根  
设备的根项。

<span id="WIA_CATEGORY_AUTO"></span><span id="wia_category_auto"></span>WIA \_ 类别 \_ 自动  
在 Windows 7 和更高版本中， [自动项](./auto-item.md) 具有支持 [自动配置的扫描](./auto-configured-scanning.md)所需的 WIA 属性。

上述类别定义了应如何处理或使用 WIA 项。 例如，如果项表示一个已完成的文件，您可以假定该数据是静态的，并且位于设备上。 如果项表示进纸器，则您可以指望它包含所需的文档送纸器属性，并与文档送纸器操作。 有关这些类别的详细信息，请参阅 [WIA Item 类别](./wia-item-categories.md)。

下表显示了 WIA 分组类别及其项标志。 此表不包括 WIA 定义的所有 WIA 项标志的完整列表。 有关这些标志的完整列表，请参阅 [**WIA \_ IPA \_ ITEM \_ 标志**](wia-ipa-item-flags.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WIA 类别</th>
<th>WIA 项标志</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_CATEGORY_BARCODE_READER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p><strong>必需</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_ENDORSER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeImage</p>
<p><strong>可选</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FEEDER</p></td>
<td><p><strong>必需</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>可选</strong></p>
<p>WiaItemTypeFolder</p>
<p>仅 (ADF 根项（如果存在 WIA_CATEGORY_FEEDER_FRONT 和 WIA_CATEGORY_FEEDER_BACK 项）) </p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FEEDER_BACK</p></td>
<td><p><strong>必需</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>可选</strong></p>
<p>无</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FEEDER_FRONT</p></td>
<td><p><strong>必需</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>可选</strong></p>
<p>无</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FILM</p></td>
<td><p><strong>必需</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p>WiaItemTypeFolder</p>
<p><strong>可选</strong></p>
<p>无</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FINISHED_FILE</p></td>
<td><p><strong>必需</strong></p>
<p>WiaItemTypeFile</p>
<p>WiaItemTypeTransfer</p>
<p><strong>可选</strong></p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeAudio</p>
<p>WiaItemTypeDeleted</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FLATBED</p></td>
<td><p><strong>必需</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>可选</strong></p>
<p>WiaItemTypeFolder</p>
<p>仅当支持多个扫描区域项时，才 (FB 根项) </p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FOLDER</p></td>
<td><p><strong>必需</strong></p>
<p>WiaItemTypeStorage</p>
<p>WiaItemTypeFolder</p>
<p><strong>可选</strong></p>
<p>WiaItemTypeDeleted</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_IMPRINTER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeImage</p>
<p><strong>可选</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_MICR_READER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p><strong>必需</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_PATCH_CODE_READER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p><strong>必需</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_ROOT</p></td>
<td><p><strong>必需</strong></p>
<p>WiaItemTypeRoot</p>
<p>WiaItemTypeFolder</p>
<p><strong>可选</strong></p>
<p>WiaItemTypeDevice</p>
<p>WiaItemTypeDisconnected</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_AUTO</p></td>
<td><p><strong>必需</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>可选</strong></p>
<p><em>无</em></p></td>
</tr>
</tbody>
</table>

 

下表显示了 WIA 分组类别及其 WIA 属性和 WIA 项。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>WIA 类别</th>
<th>WIA 属性</th>
<th>WIA 项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_CATEGORY_FEEDER</p></td>
<td><p>属性包括用于送纸器-扫描器控件的属性。</p>
<p>通常包括特定于图像的属性和特定于文档的属性。</p></td>
<td><p>WIA 送纸器项，包括表示文档正面和背面的子项。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FEEDER_BACK</p></td>
<td><p>属性包括用于送纸器-扫描器控件的属性。</p>
<p>通常包括特定于图像的属性和特定于文档的属性。</p></td>
<td><p>表示文档的上一页的 WIA 送纸器项。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FEEDER_FRONT</p></td>
<td><p>属性包括用于送纸器-扫描器控件的属性。</p>
<p>通常包括特定于图像的属性和特定于文档的属性。</p></td>
<td><p>表示文档首页的 WIA 进纸器项。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FILM</p></td>
<td><p>属性包括用于胶片扫描器控件的属性。</p>
<p>通常包括特定于图像的属性和特定于文档的属性。</p></td>
<td><p>WIA 胶片项，包括代表单独扫描帧的子项。</p>
<p>但是，子项目不能具有 <strong>WiaItemTypeFolder</strong> 标志。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FINISHED_FILE</p></td>
<td><p>属性取决于所报告的项类型。 例如， <strong>WiaItemTypeImage</strong> 应具有一些图像项属性，如每个像素的位数。</p></td>
<td><p>WIA 存储项（包括表示完成的文件内容的子项） (换言之，如 <em>.jpg</em>、 <em>.htm</em>和 <em>.txt</em> 文件) 的数据文件。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FLATBED</p></td>
<td><p>属性包括用于平板扫描仪控件的属性。</p>
<p>通常包括特定于图像的属性和特定于文档的属性。</p></td>
<td><p>WIA 平板项目，其中包括表示扫描仪的平板影印上要扫描的区域的子项。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FOLDER</p></td>
<td><p>属性包括用于文件夹和设备命名的属性、访问权限、文档处理和文档状态。</p></td>
<td><p>表示存储单元的项。 对于包含存储的扫描程序，它们必须具有至少一个文件夹扫描程序项。 此项可以包含代表单个存储项的子文件夹项。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_ROOT</p></td>
<td><p>属性包括用于设备控制、名称、访问权限、文档处理和设备类型的属性。</p></td>
<td><p>仅限根项。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_AUTO</p></td>
<td><p>属性包括用于自动配置的扫描。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/image/wia-properties-supported-by-an-auto-item" data-raw-source="[WIA Properties Supported by an Auto Item](./wia-properties-supported-by-an-auto-item.md)">自动项支持的 WIA 属性</a>。</p></td>
<td><p>表示扫描仪自动配置的扫描设置的 WIA 自动项。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA \_ IPA \_ 项 \_ 标志**](wia-ipa-item-flags.md)

