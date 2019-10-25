---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报\_CONFIGCAPS
description: KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报\_在 KSPROPERTY\_CAMERACONTROL 中定义的 CONFIGCAPS 属性 ID 用于查询 ROI 功能的。
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
ms.openlocfilehash: 2731b0512dfc024b99dab0e4a4df51d472938163
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823986"
---
# <a name="ksproperty_cameracontrol_extended_roi_configcaps"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报\_CONFIGCAPS

**KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报\_** 在 KSPROPERTY\_CAMERACONTROL 中定义的 CONFIGCAPS 属性 ID [ **\_扩展\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举用于查询 ROI功能.

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
<th>控件</th>
<th>在任务栏的搜索框中键入</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>Filter</p></td>
<td><p>同步（只读）</p></td>
</tr>
</tbody>
</table>

若要使用驱动程序查询投资回报率功能，请将**KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报\_CONFIGCAPS**扩展属性控件连同标准 KSCAMERA\_EXTENDEDPROP 一起发送到驱动程序[ **\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构后跟一个[**KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPSHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcapsheader)结构，后跟一个或多个[**KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcaps)构造. 以下列表说明了具有两个投资回报 config cap 的数据结构。

-   **KSCAMERA\_EXTENDEDPROP\_标头**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPSHEADER** （ConfigCapCount = 2）

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS**

下表包含**KSCAMERA\_\_EXTENDEDPROP**的说明和要求，其中使用**KSPROPERTY\_CAMERACONTROL\_扩展\_ROI\_CONFIGCAPS**扩展 ROI 控件的属性。

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
<td><p>版本</p></td>
<td><p>这必须为1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> （0xffffffff），</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>这必须是 sizeof （<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong> + Sizeof （<strong>KSCAMERA_EXTENDEDPROP_ROI_CONFIGCAPSHEADER</strong>） + sizeof （<strong>KSCAMERA_EXTENDEDPROP_ROI_CONFIGCAPS</strong>） * ConfigCapCount。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这必须是0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个只读字段。 这必须是0。</p></td>
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
