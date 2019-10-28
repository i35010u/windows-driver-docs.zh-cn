---
title: WIA\_IPA\_项\_标志
description: WIA\_IPA\_ITEM\_FLAGS 属性包含 WIA 项的描述性标志。
ms.assetid: ee25fb38-eafa-49a9-83ab-4f99bc25f4e9
keywords:
- WIA_IPA_ITEM_FLAGS 图像设备
topic_type:
- apiref
api_name:
- WIA_IPA_ITEM_FLAGS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5831b399849d5f8e32fbdab76352980e2a291122
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840693"
---
# <a name="wia_ipa_item_flags"></a>WIA\_IPA\_项\_标志


WIA\_IPA\_ITEM\_FLAGS 属性包含 WIA 项的描述性标志。

## <span id="ddk_wia_ipa_item_flags_si"></span><span id="DDK_WIA_IPA_ITEM_FLAGS_SI"></span>


属性类型： VT\_I4

有效值： WIA\_的\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

WIA 项标志与[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)服务实用工具函数的*lObjectFlags*参数中的标志相同。 WIA 服务创建并维护 WIA\_IPA\_项\_FLAGS 属性。

应用程序读取 WIA\_IPA\_项\_标志来确定 WIA 项的描述性标志值。

下表介绍了 Windows Vista 和更高版本的操作系统中过时的、但与 Microsoft Windows XP 有效的标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>旗帜</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeAnalyze</strong></p></td>
<td><p>支持<strong>IWiaItem：： AnalyzeItem</strong>方法的 WIA 项，如 Microsoft Windows SDK 文档中所述。 此项还支持自动子项生成，这有助于检测区域或 decomposepages。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeBurst</strong></p></td>
<td><p>仅适用于文件夹。 <strong>WiaItemTypeBurst</strong>指示此文件夹中的图像是按连续时间顺序拍摄的。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeHasAttachments</strong></p></td>
<td><p>支持附件但当前包含附件的 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeHPanorama</strong></p></td>
<td><p>表示水平全景图像的 WIA 项。 此标志仅对还设置了<strong>WiaItemTypeFolder</strong>标志的项有效。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeTwainCapabilityPassThrough</strong></p></td>
<td><p><strong>WiaItemTypeTwainCapabilityPassThrough</strong>指示 WIA 设备能够从 twain 兼容层接收 twain 功能数据。 如果设置了此标志，则 TWAIN 兼容层不理解的任何 TWAIN 功能都将被传递到 WIA 驱动程序。 此标志仅对 WIA 驱动程序的根项有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeVideo</strong></p></td>
<td><p>支持流式处理视频的 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeVPanorama</strong></p></td>
<td><p>表示垂直全景图像的 WIA 项。 <strong>WiaItemTypeVPanorama</strong>仅对还设置了<strong>WiaItemTypeFolder</strong>标志的项有效。</p></td>
</tr>
</tbody>
</table>

 

下表描述了在 Windows Vista、Windows XP 和更高版本的操作系统中有效的标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>旗帜</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeAudio</strong></p></td>
<td><p>支持音频的 WIA 项。 <strong>WiaItemTypeAudio</strong>仅对还设置了<strong>WiaItemTypeFile</strong>标志的项有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeDeleted</strong></p></td>
<td><p>标记为删除、的 WIA 项已被删除、不存在或具有无效内容。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeDevice</strong></p></td>
<td><p>表示已连接设备的 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeDisconnected</strong></p></td>
<td><p>表示已断开连接的设备的 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeFile</strong></p></td>
<td><p>支持文件传输的 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeFolder</strong></p></td>
<td><p>作为文件夹的 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeFree</strong></p></td>
<td><p>未初始化或已被删除的 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeGenerated</strong></p></td>
<td><p>应用程序或驱动程序生成的 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeImage</strong></p></td>
<td><p>作为图像文件的 WIA 项。 <strong>WiaItemTypeImage</strong>仅对还设置了<strong>WiaItemTypeFile</strong>标志的项有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeRoot</strong></p></td>
<td><p>Wia 项是 WIA 驱动程序的根项，它是设备支持的所有功能项的父项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeStorage</strong></p></td>
<td><p><strong>WiaItemTypeImage</strong>指示文件夹项的其他存储。 WIA 驱动程序在映像和文件夹方面指定其项目。 不存在用于描述存储项特征的 WIA 属性（如剩余存储空间、写入速度或媒体类型）。 你可以添加公开此信息的供应商特定的属性。 只有编写的应用程序或扩展能识别这些属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeTransfer</strong></p></td>
<td><p>可用于传输数据的 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeTwainCapabilityPassThrough</strong></p></td>
<td><p>能够从 TWAIN 兼容层接收 TWAIN 功能数据的 WIA 设备。 如果设置了<strong>WiaItemTypeTwainCapabilityPassThrough</strong> ，则 twain 兼容层不理解的任何 twain 功能都将被传递到 WIA 驱动程序。 此标志仅对 WIA 驱动程序的根项有效。</p></td>
</tr>
</tbody>
</table>

 

下表描述了仅在 Windows Vista 和更高版本的操作系统中有效的标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>旗帜</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeDocument</strong></p></td>
<td><p><strong><em>WiaItemTypeDocument</em></strong> <em>已过时，不应使用。</em></p>
<p>WIA 项是<a href="wia-ipa-format.md" data-raw-source="[&lt;strong&gt;WIA_IPA_FORMAT&lt;/strong&gt;](wia-ipa-format.md)"><strong>WIA_IPA_FORMAT</strong></a>属性包含的一种文档格式的文档文件。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeProgrammableDataSource</strong></p></td>
<td><p>WIA 项是一个可编程数据源，并遵循一组预定义的配置规则，这些规则基于<a href="wia-ipa-item-category.md" data-raw-source="[&lt;strong&gt;WIA_IPA_ITEM_CATEGORY&lt;/strong&gt;](wia-ipa-item-category.md)"><strong>WIA_IPA_ITEM_CATEGORY</strong></a>属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeMask</strong></p></td>
<td><p>所有其他已定义的标志值的标志掩码。 此标志本身不是项类型。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeRemoved</strong></p></td>
<td><p>WIA 项已从项树中移除。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeRoot</strong></p></td>
<td><p>WIA 项是 WIA 驱动程序的根项，它是设备支持的所有功能项的父项。</p></td>
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
<td><p>标头</p></td>
<td>Wiadef （包括 Wiadef）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_IPA\_格式**](wia-ipa-format.md)

[**WIA\_IPA\_项\_类别**](wia-ipa-item-category.md)

[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)

 

 






