---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMAXFRAMERATE
description: 此属性提供照相机处于照片序列模式时的最大捕获帧速率。
ms.assetid: 49A93E02-232C-4009-8F18-75D067CA7150
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE 流媒体设备
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
ms.openlocfilehash: b3ad8b4c4104e2204f42c16e4488e3c870a2ebbd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841587"
---
# <a name="ksproperty_cameracontrol_extended_photomaxframerate"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMAXFRAMERATE

此属性提供照相机处于照片序列模式时的最大捕获帧速率。

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

属性值（操作数据）包含[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。 在 KSCAMERA 中设置或返回的最大照片帧速率，以 **\_EXTENDEDPROP\_值**形式返回。

此属性的[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**flags**成员中未设置任何标志。

总属性数据大小为**sizeof**（KSCAMERA\_EXTENDEDPROP\_标头） + **sizeof**（KSCAMERA\_EXTENDEDPROP\_值）。 [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

此属性控件是异步的，不可取消。

## <a name="remarks"></a>备注

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
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>0</td>
</tr>
</tbody>
</table>

帧速率值是在[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)的**比率**成员中设置的。 **Largeint.highpart**包含帧速率和比率的分子 **。 LowPart**包含帧速率的分母。

当驱动程序处于照片序列模式时，可能需要限制照片捕获的最大帧速率。 这是为了确保 "时间点" 捕获方案（具有一定数量的历史记录帧）包含在配置的时间范围内。 例如，根据内存限制，如果应用程序希望捕获1秒的过去历史记录，则必须将捕获速率限制为，以便只需要 N 个帧。

如果设置了此设置，则驱动程序必须使用提供的帧速率，即使照相机可以快速捕获帧，然后才能迅速捕获请求的速率。 如有必要，驱动程序可以删除额外的帧以容纳请求的速率。

将 "最大帧速率" 值设置为0（**比率**的 LowPart 的 "largeint.highpart" 和 "0"）会清除驱动程序中的 "最大帧速率" 设置，其效果与要求驱动程序尽可能快地提供框架的效果相同。  一旦帧速率设置为0，任何后续查询都将返回相机驱动程序可能的最大帧速率值。 

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
