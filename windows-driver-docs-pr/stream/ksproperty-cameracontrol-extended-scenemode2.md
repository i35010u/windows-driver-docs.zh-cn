---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE
description: KSPROPERTY\_CAMERACONTROL 中定义的 KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE 属性 ID\_扩展\_属性枚举为 Oem 提供微调场景模式的功能以及任何其他 ISP 控制参数。
ms.assetid: CB3F89AD-4B53-4E47-B60E-4B584DB8418B
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE 流媒体设备
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
ms.openlocfilehash: 73795fac93c1b22ff4d8ea43df3a0ec100162ad2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823941"
---
# <a name="ksproperty_cameracontrol_extended_scenemode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE

KSPROPERTY\_CAMERACONTROL 中定义的**KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE**属性 ID [ **\_扩展\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举为 oem 提供了根据需要微调场景模式以及任何其他 ISP 控制参数。

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
<td><p>异步</p></td>
</tr>
</tbody>
</table>

在某些情况下，场景模式用作指导照相机系统优化其操作的提示。 场景模式和其他 ISP 控制（如白平衡、ISO、曝光时间和 EV 补偿）必须能够独立工作，而不会相互影响。

-   更改任何其他 ISP 控制参数不得更改现有场景模式。 修改其他 ISP 参数之后，驱动程序不需要将场景模式改为手动。

-   设置自动场景模式不得更改任何其他 ISP 控件的现有设置。 对于任何其他 ISP 控件，驱动程序无需恢复为完全自动模式。

**KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_自动**

此标志指示自动场景模式。 照相机驱动程序将根据场景自动确定最佳场景模式设置，并根据场景的需要优化各种 ISP 设置。

**KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_手册**

此标志不适用。

**KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_宏\\纵向\\运动\\的\\BACKLIT**

这些标志指示相应的场景模式（如定义）。 照相机驱动程序将使用指定为提示的场景模式来根据需要优化各种 ISP 设置（例如，对于晚间，ISP 设置针对夜间环境进行了优化）。

下表包含在使用**KSPROPERTY\_CAMERACONTROL\_EXTENDED\_SCENEMODE**属性时， [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的说明和要求。 对于**KSPROPERTY\_CAMERACONTROL\_扩展\_SCENEMODE**，将忽略[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。

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
<td><p>这必须为1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> （0xffffffff）。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>这必须是 sizeof （<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>） + Sizeof （<strong>KSCAMERA_EXTENDEDPROP_VALUE</strong>）。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这指示上次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。 值0指示未检测到任何错误。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是<strong>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL</strong>的按位 "或"，以及以上定义的任何受支持场景模式。 如果照相机驱动程序支持此控件，则必须支持<strong>KSCAMERA_EXTENDEDPROP_SCENEMODE_AUTO</strong> 。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这可以是上面所示的任何受支持场景模式。</p></td>
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
