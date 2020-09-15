---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOCONFIRMATION
description: '\_ \_ \_ KSPROPERTY CAMERACONTROL 扩展属性枚举中定义的 KSPROPERTY CAMERACONTROL 扩展 PHOTOCONFIRMATION 属性 \_ ID \_ \_ 用于设置和获取驱动程序中的照片确认设置。'
ms.assetid: 3EF6FF15-6805-4D91-B053-1BF6C5D5BEF2
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOCONFIRMATION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOCONFIRMATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 578f885b59f61499e333dc5e4569eeac88cd3994
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104674"
---
# <a name="ksproperty_cameracontrol_extended_photoconfirmation"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOCONFIRMATION

[**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 属性**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举中定义的**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOCONFIRMATION**属性 ID 用于设置和获取驱动程序中的照片确认设置。

## <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>范围</th>
<th>控制</th>
<th>类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>筛选器</p></td>
<td><p>同步</p></td>
</tr>
</tbody>
</table>

对于 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)，以下标志值用于打开或关闭照片确认。 默认情况下，驱动程序应 **设置 \_ KSPROPERTY \_ PHOTOCONFIRMATION** 。 标志值的定义如下。

```cpp
#define KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_OFF     0x0000000000000000 
#define KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_ON      0x0000000000000001
```

如果照片确认设置为 **KSCAMERA \_ EXTENDEDPROP \_ PHOTOCONFIRMATION \_ OFF**，则驱动程序预览 pin 不得生成 photo 帧或生成包含照片确认元数据的 [**KSCAMERA \_ metadata \_ PHOTOCONFIRMATION**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation) 结构。 如果照片确认设置为 ** \_ "KSCAMERA EXTENDEDPROP \_ PHOTOCONFIRMATION \_ ON**"，则驱动程序预览 pin 必须生成一个照片帧，并生成包含照片确认元数据的 **KSCAMERA \_ metadata \_ PHOTOCONFIRMATION** 结构。

下表包含使用**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ PHOTOCONFIRMATION**属性时**KSCAMERA \_ EXTENDEDPROP \_ 标头**结构字段的说明和要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>这必须为1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须 <strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xffffffff) ，</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>) 。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这包含上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>此属性必须为 0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的任何 <strong>KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_Xxx</strong> 标志。</p></td>
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
<td><p>标头</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>