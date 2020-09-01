---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 投资回报 \_ CONFIGCAPS
description: '\_ \_ \_ \_ KSPROPERTY CAMERACONTROL 扩展属性枚举中定义的 KSPROPERTY CAMERACONTROL 扩展 ROI CONFIGCAPS 属性 \_ ID \_ \_ 用于查询 ROI 功能。'
ms.assetid: 29722CE2-81D3-453E-82C5-98C8E7115448
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ROI_CONFIGCAPS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ROI_CONFIGCAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5253e98423a153072be2832135a321d84d192962
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188132"
---
# <a name="ksproperty_cameracontrol_extended_roi_configcaps"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 投资回报 \_ CONFIGCAPS

[**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 属性**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举中定义的**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ ROI \_ CONFIGCAPS**属性 ID 用于查询 ROI 功能。

## <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>作用域</th>
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

若要使用驱动程序查询投资回报率功能，请将**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 投资回报 \_ CONFIGCAPS**扩展属性控件连同标准[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构一起发送到驱动程序，后面跟有一个或多个[**KSCAMERA EXTENDEDPROP \_ \_ roi \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcaps) [**CONFIGCAPSHEADER 结构。 \_ \_ \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcapsheader) 以下列表说明了具有两个投资回报 config cap 的数据结构。

-   **KSCAMERA \_ EXTENDEDPROP \_ 标头**

-   **KSCAMERA \_EXTENDEDPROP \_ ROI \_ CONFIGCAPSHEADER** (ConfigCapCount = 2) 

-   **KSCAMERA \_ EXTENDEDPROP \_ 投资回报 \_ CONFIGCAPS**

-   **KSCAMERA \_ EXTENDEDPROP \_ 投资回报 \_ CONFIGCAPS**

下表包含了在使用扩展 ROI 控制的**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ roi \_ CONFIGCAPS**属性时， **KSCAMERA \_ EXTENDEDPROP \_ 标头**结构字段的说明和要求。

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
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong> + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_CONFIGCAPSHEADER</strong>) + Sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_CONFIGCAPS) </strong> * ConfigCapCount。</p></td>
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
<td><p>此字段为只读字段。 此属性必须为 0。</p></td>
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