---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_ISO
description: 此属性选择相机的 ISO 设置。 ISO 设置是从一组预置中选择的，或者设置为 "自动"。
ms.assetid: 8BA03479-2AB8-4390-83F0-84C3519DB991
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ISO 流媒体设备
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
ms.openlocfilehash: 332dec4a04f76d0228009e2991269ba8843a1098
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844844"
---
# <a name="ksproperty_cameracontrol_extended_iso"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_ISO


此属性选择相机的 ISO 设置。 ISO 设置是从一组预置中选择的，或者设置为 "自动"。

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

 

属性值（操作数据）包含[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)结构。 **KSCAMERA\_EXTENDEDPROP\_值**是必需的，但未使用。

总属性数据大小为**sizeof**（KSCAMERA\_EXTENDEDPROP\_标头） + **sizeof**（KSCAMERA\_EXTENDEDPROP\_值）。 [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含以下一个或多个 ISO 设置的按位 "或" 组合。

| ISO                                | 描述                   |
|------------------------------------|-------------------------------|
| KSCAMERA\_EXTENDEDPROP\_ISO\_自动  | ISO 设置为自动。 |
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

 

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含照相机的当前 ISO 设置。 照相机驱动程序可能支持 ISO 设置的一个子集。 如果支持此属性控制，则驱动程序必须支持 KSCAMERA\_EXTENDEDPROP\_ISO\_自动。

此属性控件是异步的，不可取消。

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
<td><p>sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VALUE）</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |（支持 ISO 设置）。</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前 ISO 值设置（仅一个值）。</td>
</tr>
</tbody>
</table>

 

如果以前没有设置 ISO，则 "**标志**" 设置为 "KSCAMERA\_EXTENDEDPROP\_ISO\_自动（默认）"。

### <a name="setting-the-property"></a>设置属性

设置属性时，KSPROPERTY\_类型\_SET 请求， [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要启用的 ISO 设置。

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

[KSCAMERA\_EXTENDEDPROP\_标头](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[KSCAMERA\_EXTENDEDPROP\_值](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
