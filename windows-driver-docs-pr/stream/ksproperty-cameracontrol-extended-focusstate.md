---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSSTATE
description: KSPROPERTY\_CAMERACONTROL 中定义的 KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSSTATE 属性 ID\_扩展\_属性枚举用于从驱动程序获取焦点状态。 这是一个只读筛选器级属性。
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
ms.openlocfilehash: 28c7cbf816661519837be2aadef01c2d6dd31410
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844836"
---
# <a name="ksproperty_cameracontrol_extended_focusstate"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSSTATE

KSPROPERTY\_CAMERACONTROL 中定义的**KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSSTATE**属性 ID [ **\_扩展\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举用于从驱动器. 这是一个只读筛选器级属性。

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

对于[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)，标志值包含照相机驱动程序返回的焦点状态。 这是一个同步仅获取控件。 [**KSCAMERA\_EXTENDEDPROP\_FOCUSSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate)枚举中提供了可用的焦点状态值。

下表包含使用焦点状态控件时**KSCAMERA\_EXTENDEDPROP\_标头**结构字段的说明和要求。

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
<td><p>这必须是 sizeof （<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>） + Sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>）</p></td>
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
<td><p>这是一个只读字段。 这包含驱动程序返回的焦点状态。 有关焦点状态的详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_FOCUSSTATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate)"><strong>KSCAMERA_EXTENDEDPROP_FOCUSSTATE</strong></a>主题。</p></td>
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
