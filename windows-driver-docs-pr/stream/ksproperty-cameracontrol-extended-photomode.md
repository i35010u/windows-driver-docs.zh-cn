---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE
description: 此属性设置或检索用于相机的照片模式设置。
ms.assetid: C9596B85-A07B-4DF7-852F-C9EBF43E1E44
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE 流式处理媒体设备
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
ms.openlocfilehash: ff3effb2bbb7b0fff2ed6f3cd5c7e70702aed116
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327021"
---
# <a name="kspropertycameracontrolextendedphotomode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOMODE

此属性设置或检索用于相机的照片模式设置。

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

（操作数据） 的属性值包含[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和一个[ **KSCAMERA\_EXTENDEDPROP\_PHOTOMODE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)结构。 这些名称序列模式设置时指定的照片模式和历史记录帧计数。

在中设置所需的照片模式**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)。 照片模式设置为以下值之一。

| 照片模式                                  | 描述                      |
|---------------------------------------------|----------------------------------|
| KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_正常   | 正常仍照片操作     |
| KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_序列 | 照片序列在捕获操作 |

Total 属性数据的大小**sizeof**(KSCAMERA\_EXTENDEDPROP\_标头) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_PHOTOMODE)。 **大小**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)设置为此属性的总数据大小。

> [!NOTE]
> 设置照片模式是一个异步控制操作和 KSCAMERA\_EXTENDEDPROP\_CAPS\_必须在设置 ASYNCCONTROL**功能**隶属[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)。

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
<th>ReplTest1</th>
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
<p>sizeof(KSCAMERA_EXTENDEDPROP_PHOTOMODE)</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td><p>尝试获取照片模式数据生成一个错误值。</p>
<p>否则为为 0。</p></td>
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
<td><p>Version</p></td>
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

[**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
