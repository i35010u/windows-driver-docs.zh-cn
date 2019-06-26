---
title: WIA\_IPA\_项\_类别
description: WIA\_IPA\_项\_类别属性包含 WIA 项已分组的类别。
ms.assetid: 0dde5e1c-ac30-4129-96fb-89ce1950c29b
keywords:
- WIA_IPA_ITEM_CATEGORY 成像设备
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
ms.openlocfilehash: ec2f70c600199b6c0ae0872c705c3b41d6a5f07e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391433"
---
# <a name="wiaipaitemcategory"></a>WIA\_IPA\_项\_类别


WIA\_IPA\_项\_类别属性包含 WIA 项已分组的类别。

## <span id="ddk_wia_ipa_item_category_si"></span><span id="DDK_WIA_IPA_ITEM_CATEGORY_SI"></span>


属性类型：VT\_CLSID

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

WIA 微型驱动程序创建并维护此属性。

WIA 定义以下类别：

<span id="WIA_CATEGORY_BARCODE_READER"></span><span id="wia_category_barcode_reader"></span>WIA\_类别\_条形码\_读取器  
一个是可编程数据源，启用下载条形码元数据传输的条形码读取器项。

<span id="WIA_CATEGORY_ENDORSER"></span><span id="wia_category_endorser"></span>WIA\_类别\_印记签署器  
认可类别的可编程数据源项代表 imprinting 和认可，并且可以传输启用上传和下载数据内容要打印/认可。

<span id="WIA_CATEGORY_FEEDER"></span><span id="wia_category_feeder"></span>WIA\_类别\_送纸器  
送纸器项，可编程数据源，遵循标准的规则，并具有支持文档送纸器所需的 WIA 属性。

<span id="WIA_CATEGORY_FEEDER_BACK"></span><span id="wia_category_feeder_back"></span>WIA\_类别\_送纸器\_返回  
描述双工基送纸器项的后端数据源的可编程数据源项 (WIA\_类别\_送纸器)。

<span id="WIA_CATEGORY_FEEDER_FRONT"></span><span id="wia_category_feeder_front"></span>WIA\_类别\_送纸器\_前端  
描述双工基送纸器项的前端数据源的可编程数据源项 (WIA\_类别\_送纸器)。

<span id="WIA_CATEGORY_FILM"></span><span id="wia_category_film"></span>WIA\_CATEGORY\_FILM  
电影项，可编程数据源，遵循标准的规则，并具有支持电影扫描单位所需的 WIA 属性。

<span id="WIA_CATEGORY_FINISHED_FILE"></span><span id="wia_category_finished_file"></span>WIA\_类别\_已完成\_文件  
*不*可编程数据源。 设备提供已完成的文件格式或包含已完成文件格式项的文件夹项的数据。

<span id="WIA_CATEGORY_FLATBED"></span><span id="wia_category_flatbed"></span>WIA\_类别\_平板  
平板项即可编程数据源，遵循标准的规则，并具有支持平板辊扫描所需的 WIA 属性。

<span id="WIA_CATEGORY_FOLDER"></span><span id="wia_category_folder"></span>WIA\_类别\_文件夹  
文件夹存储项 （不可编程的数据源） 包含其他文件夹项和/或已完成文件。

<span id="WIA_CATEGORY_IMPRINTER"></span><span id="wia_category_imprinter"></span>WIA\_类别\_印刷器  
Imprinting 类别的可编程数据源项，它代表 imprinting 和认可，并且可以传输启用上传和下载数据内容要打印/认可。

<span id="WIA_CATEGORY_MICR_READER"></span><span id="wia_category_micr_reader"></span>WIA\_CATEGORY\_MICR\_READER  
是可编程数据源，启用下载 MICR 文本传输 （磁性墨迹字符识别） MICR 读取器项。

<span id="WIA_CATEGORY_PATCH_CODE_READER"></span><span id="wia_category_patch_code_reader"></span>WIA\_类别\_修补\_代码\_读取器  
一个是可编程数据源，启用要下载修补程序代码的元数据传输的修补程序代码读取器项。

<span id="WIA_CATEGORY_ROOT"></span><span id="wia_category_root"></span>WIA\_类别\_根  
设备的的根项。

<span id="WIA_CATEGORY_AUTO"></span><span id="wia_category_auto"></span>WIA\_CATEGORY\_AUTO  
在 Windows 7 和更高版本，[自动项](https://docs.microsoft.com/windows-hardware/drivers/image/auto-item)具有支持所需的 WIA 属性[自动配置扫描](https://docs.microsoft.com/windows-hardware/drivers/image/auto-configured-scanning)。

上述类别定义应如何处理或使用 WIA 项。 例如，如果项表示已完成的文件，可以假定数据是静态的且在设备上找到。 如果项表示送纸器，则可能会包含所需的文档送纸器属性以及文档送纸器一样运行。 有关这些类别的详细信息，请参阅[WIA 项类别](https://docs.microsoft.com/windows-hardware/drivers/image/wia-item-categories)。

下表显示了 WIA 分组类别以及其项的标志。 此表不包括所有定义 WIA 的 WIA 项标志的完整列表。 有关这些标志的完整列表，请参阅[ **WIA\_IPA\_项\_标志**](wia-ipa-item-flags.md)。

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
<p><strong>必填</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_ENDORSER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeImage</p>
<p><strong>Optional</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FEEDER</p></td>
<td><p><strong>必填</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>Optional</strong></p>
<p>WiaItemTypeFolder</p>
<p>(WIA_CATEGORY_FEEDER_FRONT 和 WIA_CATEGORY_FEEDER_BACK 项是否存在 ADF root 仅限，项)</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FEEDER_BACK</p></td>
<td><p><strong>必填</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>Optional</strong></p>
<p>无</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FEEDER_FRONT</p></td>
<td><p><strong>必填</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>Optional</strong></p>
<p>无</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FILM</p></td>
<td><p><strong>必填</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p>WiaItemTypeFolder</p>
<p><strong>Optional</strong></p>
<p>无</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FINISHED_FILE</p></td>
<td><p><strong>必填</strong></p>
<p>WiaItemTypeFile</p>
<p>WiaItemTypeTransfer</p>
<p><strong>Optional</strong></p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeAudio</p>
<p>WiaItemTypeDeleted</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FLATBED</p></td>
<td><p><strong>必填</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>Optional</strong></p>
<p>WiaItemTypeFolder</p>
<p>（在 FB 根项仅当多个扫描区域项支持）</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FOLDER</p></td>
<td><p><strong>必填</strong></p>
<p>WiaItemTypeStorage</p>
<p>WiaItemTypeFolder</p>
<p><strong>Optional</strong></p>
<p>WiaItemTypeDeleted</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_IMPRINTER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeImage</p>
<p><strong>Optional</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_MICR_READER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p><strong>必填</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_PATCH_CODE_READER</p></td>
<td><p>WiaItemTypeProgrammableDataSource</p>
<p><strong>必填</strong></p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeFile</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_ROOT</p></td>
<td><p><strong>必填</strong></p>
<p>WiaItemTypeRoot</p>
<p>WiaItemTypeFolder</p>
<p><strong>Optional</strong></p>
<p>WiaItemTypeDevice</p>
<p>WiaItemTypeDisconnected</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_AUTO</p></td>
<td><p><strong>必填</strong></p>
<p>WiaItemTypeProgrammableDataSource</p>
<p>WiaItemTypeTransfer</p>
<p>WiaItemTypeImage</p>
<p>WiaItemTypeFile</p>
<p><strong>Optional</strong></p>
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
<td><p>属性包括送纸器扫描程序控件。</p>
<p>通常包含特定于图像的和特定于文档的属性。</p></td>
<td><p>WIA 送纸器项，包括表示文档中的前端和后端页的子项。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FEEDER_BACK</p></td>
<td><p>属性包括送纸器扫描程序控件。</p>
<p>通常包含特定于图像的和特定于文档的属性。</p></td>
<td><p>表示文档的最后一页的 WIA 送纸器项。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FEEDER_FRONT</p></td>
<td><p>属性包括送纸器扫描程序控件。</p>
<p>通常包含特定于图像的和特定于文档的属性。</p></td>
<td><p>表示文档的首页的 WIA 送纸器项。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FILM</p></td>
<td><p>属性包含电影胶片扫描器控件。</p>
<p>通常包含特定于图像的和特定于文档的属性。</p></td>
<td><p>WIA 电影项，包括表示单个扫描帧的子项目。</p>
<p>但是，不能有子项<strong>WiaItemTypeFolder</strong>标志。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FINISHED_FILE</p></td>
<td><p>属性取决于当前日期为止的项类型。 例如， <strong>WiaItemTypeImage</strong>应具有一些图像项属性，例如每像素位。</p></td>
<td><p>WIA 存储项，包括表示已完成的文件内容的子项目 (即，数据文件如<em>.jpg</em>， <em>.htm</em>，并<em>.txt</em>文件)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_FLATBED</p></td>
<td><p>属性包括平板扫描仪控件。</p>
<p>通常包含特定于图像的和特定于文档的属性。</p></td>
<td><p>WIA 平板项，包括表示正在扫描在扫描程序的平板辊区域的子项。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_FOLDER</p></td>
<td><p>属性包括文件夹和设备命名、 访问权限，文档处理和文档状态。</p></td>
<td><p>表示存储单元的项。 对于使用存储的扫描程序，它们必须具有至少一个文件夹扫描程序项。 此项可以有子文件夹表示项的单个存储项。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CATEGORY_ROOT</p></td>
<td><p>属性包括设备的设备控制、 名称、 访问权限、 文档处理和设备类型。</p></td>
<td><p>仅限根项。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CATEGORY_AUTO</p></td>
<td><p>属性包括用于自动配置扫描。 有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/image/wia-properties-supported-by-an-auto-item" data-raw-source="[WIA Properties Supported by an Auto Item](https://docs.microsoft.com/windows-hardware/drivers/image/wia-properties-supported-by-an-auto-item)">WIA 属性支持的自动项</a>。</p></td>
<td><p>表示的扫描程序扫描设置自动配置 WIA 自动项。</p></td>
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
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPA\_ITEM\_FLAGS**](wia-ipa-item-flags.md)

 

 






