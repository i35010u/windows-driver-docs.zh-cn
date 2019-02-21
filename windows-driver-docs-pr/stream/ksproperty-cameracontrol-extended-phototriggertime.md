---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTRIGGERTIME
description: 此属性控制照相机驱动程序的触发时间。 触发时间用于确定照片序列参考框架。
ms.assetid: C0DE5F4D-9566-4D8C-9061-D397577E89E2
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8a42aee278a9c178608c607987c050074a3aa534
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556085"
---
# <a name="kspropertycameracontrolextendedphototriggertime"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTRIGGERTIME

此属性控制照相机驱动程序的触发时间。 触发时间用于确定照片序列参考框架。

## <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

（操作数据） 的属性值包含[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和一个[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。 设置照片的触发时间，以 100 纳秒为单位，或将其返回为中的值**KSCAMERA\_EXTENDEDPROP\_值**。

Total 属性数据的大小**sizeof**(KSCAMERA\_EXTENDEDPROP\_标头) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_值)。 **大小**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)设置为此属性的总数据大小。

设置触发时间或已清除使用下列任一标记中**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)。

| 触发器时标志                           | 描述                     |
|---------------------------------------------|---------------------------------|
| KSPROPERTY\_照相机\_PHOTOTRIGGERTIME\_清除 | 清除触发器时设置。 |
| KSPROPERTY\_照相机\_PHOTOTRIGGERTIME\_设置   | 设置新的触发器时间值。   |

此属性控制是同步的不取消...

## <a name="remarks"></a>备注

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY\_类型\_GET 请求，该驱动程序设置的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)到以下。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>值</th>
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
<td>尺寸</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) +</p>
<p>sizeof(KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td><p>尝试读取的最大帧速率生成一个错误值。</p>
<p>否则为为 0。</p></td>
</tr>
<tr class="odd">
<td>功能</td>
<td>0</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>设置或清除标志</td>
</tr>
</tbody>
</table>

触发时间当前未设置为任何时间值，如果**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)必须包含KSPROPERTY\_照相机\_PHOTOTRIGGERTIME\_清除值。

### <a name="setting-the-property"></a>将属性设置

当设置此属性时， **ull**的成员[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)将包含触发器时间值。 触发时间是设置或清除根据操作标志。 当该标志是 KSPROPERTY\_照相机\_PHOTOTRIGGERTIME\_清除中的值**KSCAMERA\_EXTENDEDPROP\_值**不使用，并且将被忽略。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>从开始提供 Windows 8.1。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>
