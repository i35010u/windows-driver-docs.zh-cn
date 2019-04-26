---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_ISO
description: 此属性选择照相机的 ISO 设置。 ISO 设置是从一组预设中选择，或者设置为自动。
ms.assetid: 8BA03479-2AB8-4390-83F0-84C3519DB991
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ISO 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ISO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3a57ec270ab4f89fcaade89367884cba07c1a571
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326001"
---
# <a name="kspropertycameracontrolextendediso"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_ISO


此属性选择照相机的 ISO 设置。 ISO 设置是从一组预设中选择，或者设置为自动。

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

 

（操作数据） 的属性值包含[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和一个[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)结构。 **KSCAMERA\_EXTENDEDPROP\_值**是必需但未使用。

Total 属性数据的大小**sizeof**(KSCAMERA\_EXTENDEDPROP\_标头) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_值)。 **大小**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)设置为此属性的总数据大小。

**功能**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)包含一个或多个以下的 ISO 的按位 OR 组合设置。

| ISO                                | 描述                   |
|------------------------------------|-------------------------------|
| KSCAMERA\_EXTENDEDPROP\_ISO\_AUTO  | ISO 设置为自动。 |
| KSCAMERA\_EXTENDEDPROP\_ISO\_50    | ISO 50                        |
| KSCAMERA\_EXTENDEDPROP\_ISO\_80    | ISO 80                        |
| KSCAMERA\_EXTENDEDPROP\_ISO\_100   | ISO 100                       |
| KSCAMERA\_EXTENDEDPROP\_ISO\_200   | ISO 200                       |
| KSCAMERA\_EXTENDEDPROP\_ISO\_400   | ISO 400                       |
| KSCAMERA\_EXTENDEDPROP\_ISO\_800   | ISO 800                       |
| KSCAMERA\_EXTENDEDPROP\_ISO\_1600  | ISO 1600                      |
| KSCAMERA\_EXTENDEDPROP\_ISO\_3200  | ISO 3200                      |
| KSCAMERA\_EXTENDEDPROP\_ISO\_6400  | ISO 6400                      |
| KSCAMERA\_EXTENDEDPROP\_ISO\_12800 | ISO 12800                     |
| KSCAMERA\_EXTENDEDPROP\_ISO\_25600 | ISO 25600                     |

 

**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)包含当前的照相机的 ISO 设置。 照相机的驱动程序可能支持 ISO 设置的子集。 如果支持此属性控制，则该驱动程序必须支持 KSCAMERA\_EXTENDEDPROP\_ISO\_自动。

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
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |（ISO 设置支持）。</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前的 ISO 值设置 （只有一个值） 上。</td>
</tr>
</tbody>
</table>

 

如果没有 ISO 的先前设置，然后**标志**设置为 KSCAMERA\_EXTENDEDPROP\_ISO\_自动 （默认值）。

### <a name="setting-the-property"></a>将属性设置

设置该属性是，KSPROPERTY\_类型\_集请求**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)将包含要启用的 ISO 设置。

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

[KSCAMERA\_EXTENDEDPROP\_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[KSCAMERA\_EXTENDEDPROP\_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
