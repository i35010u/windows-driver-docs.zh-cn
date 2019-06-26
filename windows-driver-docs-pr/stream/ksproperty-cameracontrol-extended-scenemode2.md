---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE
description: KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE KSPROPERTY 中定义的属性 ID\_CAMERACONTROL\_扩展\_属性枚举提供了与 Oem根据需要功能来细优化以及任何其他 ISP 控件参数的场景模式。
ms.assetid: CB3F89AD-4B53-4E47-B60E-4B584DB8418B
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: da09f764efcbae8e64916046cbaf47a50005fa09
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366501"
---
# <a name="kspropertycameracontrolextendedscenemode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE

**KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE**中定义的属性 ID [ **KSPROPERTY\_CAMERACONTROL\_扩展\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举提供 Oem 微调的功能以及任何其他 ISP 控件参数的场景模式根据需要。

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
<td><p>异步</p></td>
</tr>
</tbody>
</table>

场景模式用作提示来指导照相机系统，以优化其操作对于某些条件。 场景模式和其他 ISP 控件，如白平衡，ISO，暴露时间和 EV 补偿必须能够独立工作，而不会相互影响。

-   更改任何其他 ISP 控件参数不得更改现有的场景模式。 该驱动程序不需要修改其他 ISP 参数后，将场景模式更改为手动。

-   设置自动场景模式不得更改任何其他 ISP 控件的现有设置。 该驱动程序不需要恢复到任何其他 ISP 控件完全自动模式。

**KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_AUTO**

此标志指示自动场景模式。 照相机的驱动程序将自动确定最佳场景模式设置基于场景并优化各种 ISP 设置所需的场景。

**KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_MANUAL**

此标志不适用。

**KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_宏\\纵向\\运动\\雪\\晚上\\海滩\\停用\\CANDLELIGHT\\横向\\NIGHTPORTRAIT\\背光**

这些标志指示相应的场景模式定义。 照相机驱动程序将使用指定为提示的场景模式以根据需要优化的各种 ISP 设置 （例如，对晚上，ISP 设置针对进行了优化晚上时环境）。

下表包含的说明和要求[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段时使用**KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE**属性。 [ **KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构将忽略**KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE**。

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
<td><p>这必须是 1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xFFFFFFFF)。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_VALUE</strong>)。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这表示最后一个设置操作的错误结果。 如果未设置操作发生，这必须为 0。 值 0 指示已检测到任何错误。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是按位 OR <strong>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL</strong>和上面定义的受支持的场景模式之一。 <strong>KSCAMERA_EXTENDEDPROP_SCENEMODE_AUTO</strong>如果照相机驱动程序支持此控件必须支持。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这可以是任何如上所示的受支持的场景模式。</p></td>
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
