---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTHUMBNAIL
description: 此属性获取或设置照相机的缩略图功能。
ms.assetid: 859620FD-02ED-4AA1-83B7-B92517F23B0C
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: ca52ff00eaa31ff4a8d5203bc540b6e3d93142ea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824035"
---
# <a name="ksproperty_cameracontrol_extended_photothumbnail"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTHUMBNAIL

此属性获取或设置照相机的缩略图功能。 如果提供了缩放比例，则按所选比例启用缩略图。

## <a name="usage-summary-table"></a>使用情况摘要表

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

属性值（操作数据）包含[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。 **KSCAMERA\_EXTENDEDPROP\_值**是必需的，但**值**成员被忽略。

总属性数据大小为**sizeof**（KSCAMERA\_EXTENDEDPROP\_标头） + **sizeof**（KSCAMERA\_EXTENDEDPROP\_值）。 [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含一个或多个支持的下列缩放值的按位 "或" 组合。

| 缩略图刻度标志                            | 描述                            |
|-------------------------------------------------|----------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_禁用 | 缩略图处于禁用状态。               |
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_2X      | 缩略图分辨率为 X/2 和 Y/2。   |
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_2X      | 缩略图分辨率为 X/4 和 Y/4。   |
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_8X      | 缩略图分辨率为 X/8 和 Y/8。   |
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_16X     | 缩略图分辨率为 X/16 和 Y/16。 |

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的缩略图比例值。 如果未启用缩略图生成，则在**Flags**中仅设置 KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_DISABLE。

此属性控件是异步的，不可取消。

## <a name="remarks"></a>备注

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY\_类型\_GET 请求时，驱动程序会将[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的成员设置为以下项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>版本</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>照片 pin 的 pin ID。</td>
</tr>
<tr class="odd">
<td>Size</td>
<td><p>sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VALUE）</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td><p>尝试获取缩略图设置时导致的错误值。</p></td>
</tr>
<tr class="odd">
<td>功能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |（支持缩略图刻度值）。</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前缩略图值设置（只有一个值）。</td>
</tr>
</tbody>
</table>

### <a name="setting-the-property"></a>设置属性

设置属性时，KSPROPERTY\_类型\_SET request， [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含一个缩略图刻度标志。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>可从 Windows 8.1 开始。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
