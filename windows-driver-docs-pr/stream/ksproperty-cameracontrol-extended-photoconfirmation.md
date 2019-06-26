---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOCONFIRMATION
description: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOCONFIRMATION KSPROPERTY 中定义的属性 ID\_CAMERACONTROL\_扩展\_属性枚举是用于设置和驱动程序中获取照片确认设置。
ms.assetid: 3EF6FF15-6805-4D91-B053-1BF6C5D5BEF2
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOCONFIRMATION 流式处理媒体设备
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
ms.openlocfilehash: 65b21b0bbfe7d4e933510564abbe16154483bc0c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355363"
---
# <a name="kspropertycameracontrolextendedphotoconfirmation"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOCONFIRMATION

**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOCONFIRMATION**中定义的属性 ID [ **KSPROPERTY\_CAMERACONTROL\_扩展\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举用于设置和驱动程序中获取照片确认设置。

## <a name="usage-summary-table"></a>使用率摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>范围</th>
<th>控件</th>
<th>在任务栏的搜索框中键入</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>Filter</p></td>
<td><p>同步</p></td>
</tr>
</tbody>
</table>

有关[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)，下面的标志值用于启用或禁用照片确认。 默认情况下，该驱动程序应具有**KSPROPERTY\_PHOTOCONFIRMATION\_ON**设置。 标志值定义，如下所示。

```cpp
#define KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_OFF     0x0000000000000000 
#define KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_ON      0x0000000000000001
```

如果照片确认设置为**KSCAMERA\_EXTENDEDPROP\_PHOTOCONFIRMATION\_OFF**，不能生成照片帧或生成驱动程序预览针[ **KSCAMERA\_元数据\_PHOTOCONFIRMATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)结构，其中包含照片确认元数据。 如果照片确认设置为**KSCAMERA\_EXTENDEDPROP\_PHOTOCONFIRMATION\_ON**，驱动程序预览针必须生成照片帧并生成**KSCAMERA\_元数据\_PHOTOCONFIRMATION**结构，其中包含照片确认元数据。

下表包含的说明和要求**KSCAMERA\_EXTENDEDPROP\_标头**结构字段时使用**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOCONFIRMATION**属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>这必须是 1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xFFFFFFFF)</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>)。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这包含最后一个设置操作的错误结果。 如果未设置操作发生，这必须为 0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是 0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是任意<strong>KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_Xxx</strong>上面定义的标志。</p></td>
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
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
