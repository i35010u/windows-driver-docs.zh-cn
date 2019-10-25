---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE
description: 此属性设置或检索照相机的照片模式设置。
ms.assetid: C9596B85-A07B-4DF7-852F-C9EBF43E1E44
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30ac87621ead72243c7e3eb2aca0ddab26229070
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824042"
---
# <a name="ksproperty_cameracontrol_extended_photomode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE

此属性设置或检索照相机的照片模式设置。

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

属性值（操作数据）包含[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)结构。 这两个指定了在设置序列模式时的照片模式和历史记录帧计数。

所需的照片模式在[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员中设置。 照片模式设置为以下其中一项。

| 照片模式                                  | 描述                      |
|---------------------------------------------|----------------------------------|
| KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_正常   | 正常静止照片操作     |
| KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_序列 | 照片序列捕获操作 |

总属性数据大小为**sizeof**（KSCAMERA\_EXTENDEDPROP\_标头） + **sizeof**（KSCAMERA\_EXTENDEDPROP\_PHOTOMODE）。 [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

> [!NOTE]
> 设置 "照片" 模式是一种异步控制操作，并且必须在[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员中设置 KSCAMERA\_EXTENDEDPROP\_cap\_ASYNCCONTROL。

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
<p>sizeof （KSCAMERA_EXTENDEDPROP_PHOTOMODE）</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td><p>尝试获取照片模式数据时导致的错误值。</p>
<p>否则为0。</p></td>
</tr>
<tr class="odd">
<td>功能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前照片模式。</td>
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
<td><p>版本</p></td>
<td><p>可从 Windows 8.1 开始。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
