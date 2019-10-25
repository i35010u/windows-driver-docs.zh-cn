---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOCONFIRMATION
description: KSPROPERTY\_CAMERACONTROL 中定义的 KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOCONFIRMATION 属性 ID\_扩展\_属性枚举用于设置和获取照片确认驱动程序中的设置。
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
ms.openlocfilehash: 11c84800d68f581c430166ecfa16be2f5b67ce82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844774"
---
# <a name="ksproperty_cameracontrol_extended_photoconfirmation"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOCONFIRMATION

[**KSPROPERTY\_CAMERACONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)中定义的**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOCONFIRMATION**属性 ID\_用于设置和获取驱动程序中的照片确认设置。

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

对于[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)，以下标志值用于打开或关闭照片确认。 默认情况下，驱动程序应设置**KSPROPERTY\_PHOTOCONFIRMATION\_** 。 标志值的定义如下。

```cpp
#define KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_OFF     0x0000000000000000 
#define KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_ON      0x0000000000000001
```

如果照片确认设置为**KSCAMERA\_EXTENDEDPROP\_PHOTOCONFIRMATION\_关闭**，则驱动程序预览 pin 不得生成 photo 帧或生成[**KSCAMERA\_元数据\_PHOTOCONFIRMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)包含照片确认元数据的结构。 如果照片确认设置为**KSCAMERA\_EXTENDEDPROP\_PHOTOCONFIRMATION\_** ，则驱动程序预览 pin 必须生成照片帧并生成**KSCAMERA\_元数据\_PHOTOCONFIRMATION**包含照片确认元数据的结构。

下表包含了在使用**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOCONFIRMATION**时， **KSCAMERA\_EXTENDEDPROP\_标头**结构字段的说明和要求知识产权.

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
<td><p>版本</p></td>
<td><p>这必须为1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> （0xffffffff），</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>这必须是 sizeof （<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>） + Sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>）。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这包含上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的任何<strong>KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_Xxx</strong>标志。</p></td>
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
