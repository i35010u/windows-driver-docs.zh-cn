---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMAXFRAMERATE
description: 在照片序列模式下时，此属性为相机提供最大捕获帧速率。
ms.assetid: 49A93E02-232C-4009-8F18-75D067CA7150
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 452a233fdb5ef3316d86c96875e1a331f7856c79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327215"
---
# <a name="kspropertycameracontrolextendedphotomaxframerate"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMAXFRAMERATE

在照片序列模式下时，此属性为相机提供最大捕获帧速率。

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

（操作数据） 的属性值包含[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和一个[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。 设置或返回为中的值的最大照片帧速率，单位为每秒帧数**KSCAMERA\_EXTENDEDPROP\_值**。

没有标志中的设置**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)此属性。

Total 属性数据的大小**sizeof**(KSCAMERA\_EXTENDEDPROP\_标头) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_值)。 **大小**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)设置为此属性的总数据大小。

此属性控制是异步的不取消。

## <a name="remarks"></a>备注

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
<td>Version</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>照片 pin 的 pin ID。</td>
</tr>
<tr class="odd">
<td>大小</td>
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
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>0</td>
</tr>
</tbody>
</table>

帧速率值中设置**比率**的成员[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)。 **Ratio.HighPart**包含的帧速率分子和**Ratio.LowPart**包含帧速率的分母。

照片序列模式驱动程序时，可能需要限制照片拍摄的最大帧速率。 这是为了确保"时间点"捕获的情况下，有特定数目的历史记录帧都包含在配置的时间跨度。 例如，根据内存约束，如果应用程序希望捕获 1 的第二个值得在过去的历史记录，就需要上限捕获速率，因此需要仅 N 帧数。

设置时，该驱动程序必须使用提供即使相机可快速捕获帧的帧速率则请求的速率。 如有必要，驱动程序可以删除多余的帧以容纳所请求的速率。

最大帧速率值设置为 0 (0 表示 HighPart，0 表示的 LowPart**比率**) 清除驱动程序中的最大帧速率设置，并具有相同的效果，只需要求驱动程序尽可能快提供帧。  一旦帧速率设置为 0，任何后续查询将返回的最大帧速率的值可能照相机驱动程序。 

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>从开始提供 Windows 8.1。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>
