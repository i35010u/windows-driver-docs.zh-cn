---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_WARMSTART
description: 热启动属性控件提供的驱动程序以使照相机 pin 准备就绪，以允许无故障的操作的提示。
ms.assetid: EAC20371-6228-48F1-85FF-FAECC835B070
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART
api_type:
- NA
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 62bab08cc8f2cf01b5fb9addf6518d91f96cec48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542955"
---
# <a name="kspropertycameracontrolextendedwarmstart"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_WARMSTART

热启动属性控件提供的驱动程序以使照相机 pin 准备就绪，以允许无故障的操作的提示。

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

（操作数据） 的属性值包含[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构。

没有标志中的设置**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)此属性。

Total 属性数据的大小**sizeof**(KSCAMERA\_EXTENDEDPROP\_标头)。 **大小**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)设置为此属性的总数据大小。

热启动已启用或禁用使用下列任一标记中**功能**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header).

| 热启动标志                                  | 描述             |
|---------------------------------------------------|-------------------------|
| KSCAMERA\_EXTENDEDPROP\_WARMSTART\_模式\_已禁用 | 热启动处于禁用状态。 |
| KSCAMERA\_EXTENDEDPROP\_WARMSTART\_模式\_已启用  | 启用热启动。  |

此属性控制是异步的不取消。

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
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER)</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td><p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL | KSCAMERA_EXTENDEDPROP_WARMSTART_MODE_DISABLED</p>
<p>-或-</p>
<p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL | KSCAMERA_EXTENDEDPROP_WARMSTART_MODE_ENABLED</p></td>
</tr>
<tr class="even">
<td>Flags</td>
<td>0</td>
</tr>
</tbody>
</table>

**结果**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)始终设置为 0 表示获取操作。

## <a name="see-also"></a>另请参阅

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
