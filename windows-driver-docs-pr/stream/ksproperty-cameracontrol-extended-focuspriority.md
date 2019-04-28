---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSPRIORITY
description: KSPROPERTY\_CAMERACONTROL\_扩展\_KSPROPERTY 中定义 FOCUSPRIORITY 属性 ID\_CAMERACONTROL\_扩展\_属性枚举用于配置焦点优先级。
ms.assetid: 7E3558A1-0D0D-4470-B9C9-61EA359E92C5
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSPRIORITY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSPRIORITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5f31403dd9d5d5c4bd0afd6e1400428508547ed8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347967"
---
# <a name="kspropertycameracontrolextendedfocuspriority"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSPRIORITY


**KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSPRIORITY**属性中定义 ID [ **KSPROPERTY\_CAMERACONTROL\_扩展\_属性**](https://msdn.microsoft.com/library/windows/hardware/dn917962)枚举用于配置焦点优先级。 当焦点优先级设置时，将重点放将优先于执行，以便确保拍摄的图片始终处于焦点的图片。 否则，图片将立即执行而不考虑是否图片处于活动状态。 处理失败的焦点和超时是否是必需的行为是为该驱动程序和多达 OEM 内部。

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

 

若要配置焦点优先级**KSPROPERTY\_CAMERACONTROL\_扩展\_FOCUSPRIORITY**必须使用 ID 属性。 当焦点优先级设置时，将重点放将优先于执行，以便确保拍摄的图片始终处于焦点的图片。 如果未设置焦点优先级，图片将被立即无论图片是焦点。 在处理失败的焦点行为失败，超时由 OEM 和驱动程序的内部。

有关[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)，以下标志被定义为值。 在 get 调用中，相机驱动程序返回其当前焦点优先级配置中使用这些标志之一。 在集调用中，相机驱动程序设置新的焦点优先级配置以使用这些标志之一。

```cpp
#define KSCAMERA_EXTENDEDPROP_FOCUSPRIORITY_OFF     0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_FOCUSPRIORITY_ON      0x0000000000000001
```

**请注意**  这是一个同步控件并没有为此控件定义功能。

 

下表包含的说明和要求**KSCAMERA\_EXTENDEDPROP\_标头**时使用焦点优先级控制结构字段。

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
<td><p>这必须是 KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>)，</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这表示错误结果</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是 0，</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是上面定义的 KSCAMERA_EXTENDEDPROP_FOCUSPRIORITY_Xxx 任何的标志一个。</p></td>
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
