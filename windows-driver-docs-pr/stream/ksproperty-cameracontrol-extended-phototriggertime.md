---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTRIGGERTIME
description: 此属性控制照相机驱动程序的触发时间。 触发时间用于确定照片序列的参考框架。
ms.assetid: C0DE5F4D-9566-4D8C-9061-D397577E89E2
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME 流媒体设备
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
ms.openlocfilehash: d4905ddace589288de49af1a386138b61014bf28
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824032"
---
# <a name="ksproperty_cameracontrol_extended_phototriggertime"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTRIGGERTIME

此属性控制照相机驱动程序的触发时间。 触发时间用于确定照片序列的参考框架。

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

属性值（操作数据）包含[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。 以100毫微秒为单位的照片触发时间设置为**KSCAMERA\_EXTENDEDPROP\_值**中的值。

总属性数据大小为**sizeof**（KSCAMERA\_EXTENDEDPROP\_标头） + **sizeof**（KSCAMERA\_EXTENDEDPROP\_值）。 [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

使用[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**flags**成员中的下列标志之一设置或清除触发器时间。

| 触发时间标志                           | 描述                     |
|---------------------------------------------|---------------------------------|
| KSPROPERTY\_相机\_PHOTOTRIGGERTIME\_清晰 | 清除 "触发器时间" 设置。 |
| KSPROPERTY\_相机\_PHOTOTRIGGERTIME\_集   | 设置新的触发器时间值。   |

此属性控件是同步的，并且不可取消。

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
<td><p>sizeof （KSCAMERA_EXTENDEDPROP_HEADER） +</p>
<p>sizeof （KSCAMERA_EXTENDEDPROP_VALUE）</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td><p>尝试读取最大帧速率导致的错误值。</p>
<p>否则为0。</p></td>
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

如果触发器时间当前未设置为任何时间值，则[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员必须包含 KSPROPERTY\_照相机\_PHOTOTRIGGERTIME\_CLEAR 值。

### <a name="setting-the-property"></a>设置属性

设置属性时， [**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)中的**u)** 成员将包含触发器 time 值。 触发器时间基于操作标志进行设置或清除。 当标志为 "KSPROPERTY" 时\_照相机\_PHOTOTRIGGERTIME\_清除\_KSCAMERA 中的值，则不会使用 **\_值**，将忽略该值。

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
