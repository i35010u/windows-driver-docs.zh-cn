---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOTHUMBNAIL
description: 此属性获取或设置照相机的缩略图功能。
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
ms.openlocfilehash: 1c9ee89238a3d24a2611badd3c838a4de87ab1c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837857"
---
# <a name="ksproperty_cameracontrol_extended_photothumbnail"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOTHUMBNAIL

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
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

属性值 (操作数据) 包含 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构和 [**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value) 结构。 **KSCAMERA \_ EXTENDEDPROP \_ 值** 是必需的，但 **值** 成员被忽略。

总的属性数据大小为 **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ 标头) + **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ VALUE) 。 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的 **Size** 成员设置为此总属性数据大小。

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的 **功能** 成员包含一个或多个支持的下列缩放值的按位 "或" 组合。

| 缩略图刻度标志                            | 描述                            |
|-------------------------------------------------|----------------------------------------|
| KSCAMERA \_ EXTENDEDPROP \_ PHOTOTHUMBNAIL \_ 禁用 | 缩略图处于禁用状态。               |
| KSCAMERA \_ EXTENDEDPROP \_ PHOTOTHUMBNAIL \_ 2x      | 缩略图分辨率为 X/2 和 Y/2。   |
| KSCAMERA \_ EXTENDEDPROP \_ PHOTOTHUMBNAIL \_ 2x      | 缩略图分辨率为 X/4 和 Y/4。   |
| KSCAMERA \_ EXTENDEDPROP \_ PHOTOTHUMBNAIL \_ 8x      | 缩略图分辨率为 X/8 和 Y/8。   |
| KSCAMERA \_ EXTENDEDPROP \_ PHOTOTHUMBNAIL \_ 16X     | 缩略图分辨率为 X/16 和 Y/16。 |

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的 **Flags** 成员包含当前为相机设置的缩略图比例值。 如果未启用缩略图生成，则 \_ \_ \_ 在 **标志** 中只设置 KSCAMERA EXTENDEDPROP PHOTOTHUMBNAIL DISABLE。

此属性控件是异步的，不可取消。

## <a name="remarks"></a>备注

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY \_ 类型 \_ GET 请求时，驱动程序会将 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 的成员设置为以下项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>“值”</th>
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
<td>大小</td>
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) </p></td>
</tr>
<tr class="even">
<td>结果</td>
<td><p>尝试获取缩略图设置时导致的错误值。</p></td>
</tr>
<tr class="odd">
<td>功能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |支持)  (缩略图刻度值。</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前缩略图值设置 (仅) 一个值。</td>
</tr>
</tbody>
</table>

### <a name="setting-the-property"></a>设置属性

如果设置了属性，则 KSPROPERTY \_ 类型 \_ 集请求， [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的 **Flags** 成员将包含一个缩略图刻度标志。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
