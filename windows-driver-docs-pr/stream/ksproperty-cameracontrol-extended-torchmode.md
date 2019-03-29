---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_TORCHMODE
description: Torch 模式确定如何在低光条件中使用的照相机闪光灯。
ms.assetid: FB168F4E-EBF9-4925-B4F1-BC9305DB0109
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: e8ef78649edfb16c3771e8ab9651a88917531646
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419567"
---
# <a name="kspropertycameracontrolextendedtorchmode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_TORCHMODE

Torch 模式确定如何在低光条件中使用的照相机闪光灯。 立刻正式投入工作以便自动聚焦等操作的足够浅不断提供较低强度光源。

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
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

（操作数据） 的属性值包含[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和一个[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。

Total 属性数据的大小**sizeof**(KSCAMERA\_EXTENDEDPROP\_标头) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_值)。 **大小**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)设置为此属性的总数据大小。

**功能**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)包含一个或多个以下的按位 OR 组合torch 驱动程序支持的模式。

| Torch 模式                                              | 描述                                      |
|---------------------------------------------------------|--------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_VIDEOTORCH\_OFF                 | Torchlight 处于关闭状态。                               |
| KSCAMERA\_EXTENDEDPROP\_VIDEOTORCH\_ON                  | Torchlight 上处于默认强度级别。 |
| KSCAMERA\_EXTENDEDPROP\_VIDEOTORCH\_ON\_ADJUSTABLEPOWER | Torchlight 上处于特定电源级别。      |

**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)包含 torch 模式当前设置为照相机。 用于相机的默认 torch 模式是 KSCAMERA\_EXTENDEDPROP\_VIDEOTORCH\_OFF 和驱动程序必须支持此 torch 模式。

此属性控制是同步的不取消。

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
<th>ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>版本</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0XFFFFFFFF)。</td>
</tr>
<tr class="odd">
<td>大小</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>Torch 支持的模式值。</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前 torch 模式值设置 （只有一个值）。</td>
</tr>
</tbody>
</table>

Torch 模式时 KSCAMERA\_EXTENDEDPROP\_VIDEOTORCH\_ON\_ADJUSTABLEPOWER， **Value.ull**隶属[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)包含强度的级别值介于 0-100。 强度为 0 表示最小级别，强度为 100 表示最高亮度级别。

如果没有场景之前设置模式，然后**标志**设置为 KSCAMERA\_EXTENDEDPROP\_VIDEOTORCH\_OFF （默认）。

### <a name="setting-the-property"></a>将属性设置

设置该属性是，KSPROPERTY\_类型\_集请求**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)将包含要设置的 torch 模式。 **Value.ull**的成员[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)将包含要设置的强度级别**标志**是 KSCAMERA\_EXTENDEDPROP\_VIDEOTORCH\_ON\_ADJUSTABLEPOWER。

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
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_VALUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
