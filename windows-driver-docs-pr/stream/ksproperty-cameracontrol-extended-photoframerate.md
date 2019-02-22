---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOFRAMERATE
description: 照相机照片模式为顺序模式时，此属性将获取捕获帧速率。
ms.assetid: F1269FED-EFB3-4F21-B0EC-F88949D6EEBC
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOFRAMERATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOFRAMERATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: ec9b29f4cd5f7b29bbdc3f4463d71409ad550458
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524039"
---
# <a name="kspropertycameracontrolextendedphotoframerate"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOFRAMERATE

照相机照片模式为顺序模式时，此属性将获取捕获帧速率。

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
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

（操作数据） 的属性值包含[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和一个[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。 作为中的值返回的照片帧速率，单位为每秒帧数**KSCAMERA\_EXTENDEDPROP\_值**。

没有标志中的设置**标志**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)此属性。

Total 属性数据的大小**sizeof**(KSCAMERA\_EXTENDEDPROP\_标头) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_值)。 **大小**的成员[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)设置为此属性的总数据大小。

此属性控制是同步的不取消。

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
<td>版本</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>此应用程序的照片 pin 的 pin ID。</td>
</tr>
<tr class="odd">
<td>尺寸</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) +</p>
<p>sizeof(KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td><p>尝试读取帧速率生成一个错误值。</p>
<p>否则为为 0。</p></td>
</tr>
<tr class="odd">
<td>功能</td>
<td>0</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>0</td>
</tr>
</tbody>
</table>

帧速率值中设置**比率**的成员[ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)。 **Ratio.HighPart**包含的帧速率分子和**Ratio.LowPart**包含帧速率的分母。

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

## <a name="see-also"></a>另请参阅

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
