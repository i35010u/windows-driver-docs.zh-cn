---
title: WIA\_IPA\_项\_标志
description: WIA\_IPA\_项\_标志属性包含 WIA 项的描述性标志。
ms.assetid: ee25fb38-eafa-49a9-83ab-4f99bc25f4e9
keywords:
- WIA_IPA_ITEM_FLAGS 成像设备
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
ms.openlocfilehash: 56dde9f5e26f242ef54a2cb0d2805d7808661405
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369507"
---
# <a name="wiaipaitemflags"></a>WIA\_IPA\_项\_标志


WIA\_IPA\_项\_标志属性包含 WIA 项的描述性标志。

## <span id="ddk_wia_ipa_item_flags_si"></span><span id="DDK_WIA_IPA_ITEM_FLAGS_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

WIA 项标志是否与中相同*lObjectFlags*的参数[ **wiasCreateDrvItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549160)服务实用工具函数。 WIA 服务创建和维护 WIA\_IPA\_项\_标志属性。

应用程序读取 WIA\_IPA\_项\_标志以确定 WIA 项的描述性标志值。

下表介绍 Windows Vista 和更高版本的操作系统中已过时，但使用 Microsoft Windows XP 有效的标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeAnalyze</strong></p></td>
<td><p>支持的 WIA 项<strong>IWiaItem::AnalyzeItem</strong>方法，Microsoft Windows SDK 文档中所述。 此项还支持自动子项生成，可帮助你检测区域或 decomposepages。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeBurst</strong></p></td>
<td><p>仅文件夹。 <strong>WiaItemTypeBurst</strong>指示持续时间序列中，采用此文件夹中的图像。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeHasAttachments</strong></p></td>
<td><p>支持的附件和当前包含附件的 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeHPanorama</strong></p></td>
<td><p>表示水平全景图像的 WIA 项。 此标志是仅对项还具有的有效<strong>WiaItemTypeFolder</strong>标志设置。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeTwainCapabilityPassThrough</strong></p></td>
<td><p><strong>WiaItemTypeTwainCapabilityPassThrough</strong>指示 WIA 设备能够接收来自 TWAIN 兼容性层 TWAIN 功能数据。 如果设置此标志，TWAIN 兼容性层并不了解任何 TWAIN 功能将传递到 WIA 驱动程序。 此标志为仅对 WIA 驱动程序的根项目有效。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeVideo</strong></p></td>
<td><p>支持流式处理视频的 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeVPanorama</strong></p></td>
<td><p>表示垂直全景图像的 WIA 项。 <strong>WiaItemTypeVPanorama</strong>仅对项也具有有效<strong>WiaItemTypeFolder</strong>标志设置。</p></td>
</tr>
</tbody>
</table>

 

下表介绍在 Windows Vista、 Windows XP 和更高版本操作系统中有效的标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeAudio</strong></p></td>
<td><p>支持音频的 WIA 项。 <strong>WiaItemTypeAudio</strong>仅对项也具有有效<strong>WiaItemTypeFile</strong>标志设置。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeDeleted</strong></p></td>
<td><p>WIA 项标记为删除，已被删除、 不存在，或具有无效的内容。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeDevice</strong></p></td>
<td><p>表示连接的设备的 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeDisconnected</strong></p></td>
<td><p>表示断开连接的设备的 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeFile</strong></p></td>
<td><p>支持文件传输的 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeFolder</strong></p></td>
<td><p>是一个文件夹的 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeFree</strong></p></td>
<td><p>WIA 未初始化或已被删除的项。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeGenerated</strong></p></td>
<td><p>WIA 应用程序或驱动程序已生成的项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeImage</strong></p></td>
<td><p>为图像文件的 WIA 项。 <strong>WiaItemTypeImage</strong>仅对项也具有有效<strong>WiaItemTypeFile</strong>标志设置。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeRoot</strong></p></td>
<td><p>WIA 是 WIA 驱动程序，它是所有的设备支持的功能项的父级的根项的项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeStorage</strong></p></td>
<td><p><strong>WiaItemTypeImage</strong>表示文件夹项的其他存储。 WIA 驱动程序指定的映像和文件夹方面其项。 不存在任何 WIA 属性，用于描述存储项 （如剩余存储空间、 写入速度或媒体类型） 的特征。 可以添加特定于供应商的属性公开此信息。 这些属性是只能访问应用程序或编写可以识别它们的扩展。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeTransfer</strong></p></td>
<td><p>可用于将数据传输的 WIA 项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeTwainCapabilityPassThrough</strong></p></td>
<td><p>WIA 设备能够接收来自 TWAIN 兼容性层 TWAIN 功能数据。 如果<strong>WiaItemTypeTwainCapabilityPassThrough</strong> ，则 TWAIN 兼容性层并不了解任何 TWAIN 功能将被传递到 WIA 驱动程序。 此标志为仅对 WIA 驱动程序的根项目有效。</p></td>
</tr>
</tbody>
</table>

 

下表介绍在 Windows Vista 和更高版本的操作系统仅中有效的标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeDocument</strong></p></td>
<td><p><strong><em>WiaItemTypeDocument</em></strong>  <em>已过时，不应使用。</em></p>
<p>WIA 项是一个文档中的文档文件格式<a href="wia-ipa-format.md" data-raw-source="[&lt;strong&gt;WIA_IPA_FORMAT&lt;/strong&gt;](wia-ipa-format.md)"> <strong>WIA_IPA_FORMAT</strong> </a>属性包含。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeProgrammableDataSource</strong></p></td>
<td><p>WIA 项是可编程数据源并遵循一组预定义的配置规则，基于<a href="wia-ipa-item-category.md" data-raw-source="[&lt;strong&gt;WIA_IPA_ITEM_CATEGORY&lt;/strong&gt;](wia-ipa-item-category.md)"> <strong>WIA_IPA_ITEM_CATEGORY</strong> </a>属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeMask</strong></p></td>
<td><p>对于所有其他的标志掩码定义的标志值。 此标志不是项类型本身。</p></td>
</tr>
<tr class="even">
<td><p><strong>WiaItemTypeRemoved</strong></p></td>
<td><p>WIA 项已从项树中删除。</p></td>
</tr>
<tr class="odd">
<td><p><strong>WiaItemTypeRoot</strong></p></td>
<td><p>WIA 项是 WIA 驱动程序，它是所有设备支持的功能项父级的根项目。</p></td>
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
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPA\_格式**](wia-ipa-format.md)

[**WIA\_IPA\_项\_类别**](wia-ipa-item-category.md)

[**wiasCreateDrvItem**](https://msdn.microsoft.com/library/windows/hardware/ff549160)

 

 






