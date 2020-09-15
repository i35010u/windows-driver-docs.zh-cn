---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FOCUSSTATE
description: '\_ \_ \_ KSPROPERTY CAMERACONTROL 扩展属性枚举中定义的 KSPROPERTY CAMERACONTROL 扩展 FOCUSSTATE 属性 \_ ID \_ \_ 用于从驱动程序获取焦点状态。 这是一个只读筛选器级属性。'
ms.assetid: 53D54443-59AD-4078-BD13-CB193B89E488
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSSTATE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSSTATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 08c9ee92539b9e748d30bb9a1e5171a4c1421dfb
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107124"
---
# <a name="ksproperty_cameracontrol_extended_focusstate"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FOCUSSTATE

[**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 属性**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举中定义的**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FOCUSSTATE**属性 ID 用于从驱动程序获取焦点状态。 这是一个只读筛选器级属性。

## <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>范围</th>
<th>控制</th>
<th>类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>筛选器</p></td>
<td><p>同步 (只读) </p></td>
</tr>
</tbody>
</table>

对于 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)，标志值包含照相机驱动程序返回的焦点状态。 这是一个同步仅获取控件。 在 [**KSCAMERA \_ EXTENDEDPROP \_ FOCUSSTATE**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate) 枚举中提供了可用的焦点状态值。

下表包含使用焦点状态控件时 **KSCAMERA \_ EXTENDEDPROP \_ 标头** 结构字段的说明和要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>这必须为1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须 <strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xffffffff) ，</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>) </p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>此属性必须为 0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>此属性必须为 0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>此字段为只读字段。 这包含驱动程序返回的焦点状态。 有关焦点状态的详细信息，请参阅 <a href="/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_FOCUSSTATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate)"><strong>KSCAMERA_EXTENDEDPROP_FOCUSSTATE</strong></a> 主题。</p></td>
</tr>
</tbody>
</table>

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>