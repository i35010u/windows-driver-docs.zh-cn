---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报率\_CONFIGCAPS
description: KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报率\_CONFIGCAPS KSPROPERTY 中定义的属性 ID\_CAMERACONTROL\_扩展\_属性枚举用于查询的投资回报率的功能。
ms.assetid: 29722CE2-81D3-453E-82C5-98C8E7115448
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ROI_CONFIGCAPS 流式处理媒体设备
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
ms.openlocfilehash: 9975dab538daa1f2b07d01d69efdeda8091d3519
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377913"
---
# <a name="kspropertycameracontrolextendedroiconfigcaps"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报率\_CONFIGCAPS

**KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报率\_CONFIGCAPS**中定义的属性 ID [ **KSPROPERTY\_CAMERACONTROL\_扩展\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举用于查询的投资回报率功能。

## <a name="usage-summary-table"></a>使用率摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>范围</th>
<th>控件</th>
<th>在任务栏的搜索框中键入</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>Filter</p></td>
<td><p>同步 （只读）</p></td>
</tr>
</tbody>
</table>

若要查询的驱动程序的投资回报率功能**KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报率\_CONFIGCAPS**扩展的属性控制发送到与该驱动程序标准[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构跟[ **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPSHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcapsheader)结构后, 跟一个或多个[ **KSCAMERA\_EXTENDEDPROP\_投资回报率\_CONFIGCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcaps)结构。 以下列表说明了具有两个投资回报率配置顶端的数据结构。

-   **KSCAMERA\_EXTENDEDPROP\_HEADER**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPSHEADER** (ConfigCapCount = 2)

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS**

下表包含的说明和要求**KSCAMERA\_EXTENDEDPROP\_标头**结构字段时使用**KSPROPERTY\_CAMERACONTROL\_扩展\_ROI\_CONFIGCAPS**扩展的投资回报率控件的属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>这必须是 1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xFFFFFFFF)</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong> + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_CONFIGCAPSHEADER</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_CONFIGCAPS</strong>) * ConfigCapCount。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这必须是 0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是 0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是只读的字段。 这必须是 0。</p></td>
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
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
