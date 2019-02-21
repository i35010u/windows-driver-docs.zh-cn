---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSSTATE
description: KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSSTATE KSPROPERTY 中定义的属性 ID\_CAMERACONTROL\_扩展\_属性枚举用于获取驱动程序中的焦点状态。 这是只读的筛选器级别的属性。
ms.assetid: 53D54443-59AD-4078-BD13-CB193B89E488
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSSTATE 流式处理媒体设备
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
ms.openlocfilehash: 981d72690cd96122cb5017f0c8e78f54ba5c22b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542461"
---
# <a name="kspropertycameracontrolextendedfocusstate"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSSTATE

**KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSSTATE**中定义的属性 ID [ **KSPROPERTY\_CAMERACONTROL\_扩展\_属性**](https://msdn.microsoft.com/library/windows/hardware/dn917962)枚举用于从驱动程序获取焦点状态。 这是只读的筛选器级别的属性。

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

有关[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)，标志值包含由照相机驱动程序返回的焦点状态。 这是同步 get 唯一控件。 中提供了可用的焦点状态值[ **KSCAMERA\_EXTENDEDPROP\_FOCUSSTATE** ](https://msdn.microsoft.com/library/windows/hardware/dn925132)枚举。

下表包含的说明和要求**KSCAMERA\_EXTENDEDPROP\_标头**结构字段时使用焦点状态的控件。

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
<td><p>这必须是 1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xFFFFFFFF)</p></td>
</tr>
<tr class="odd">
<td><p>尺寸</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>)</p></td>
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
<td><p>这是只读的字段。 其中包含由驱动程序返回的焦点状态。 有关焦点状态的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/dn925132" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_FOCUSSTATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn925132)"> <strong>KSCAMERA_EXTENDEDPROP_FOCUSSTATE</strong> </a>主题。</p></td>
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
