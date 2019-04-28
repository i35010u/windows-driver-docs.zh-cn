---
title: KSPROPERTY\_CAMERACONTROL\_EXTENDED\_VIDEOHDR
description: KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOHDR 用于启用或禁用该驱动程序的高动态范围 (HDR) 视频。 这是视频的 pin 的 pin 级别控制。
ms.assetid: AC798BF1-4E1A-48D8-8F56-986F89D9C153
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOHDR 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOHDR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0e8b124f0d13ce5e5ba68c3db7037b68db2c8d80
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341858"
---
# <a name="kspropertycameracontrolextendedvideohdr"></a>KSPROPERTY\_CAMERACONTROL\_EXTENDED\_VIDEOHDR

KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOHDR 用于启用或禁用该驱动程序的高动态范围 (HDR) 视频。 这是视频的 pin 的 pin 级别控制。

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
<td><p>Pin</p></td>
<td><p>同步</p></td>
</tr>
</tbody>
</table>

以下标志可放置在 KSCAMERA\_EXTENDEDPROP\_标头。若要控制视频 HDR 标志字段。 默认情况下，驱动程序应设置为 VIDEOHDR\_OFF。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOHDR_OFF      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_VIDEOHDR_ON       0x0000000000000001 
#define KSCAMERA_EXTENDEDPROP_VIDEOHDR_AUTO     0x0000000000000002 
```

如果该驱动程序支持此控件，它必须支持 VIDEOHDR\_ON/VIDEOHDR\_OFF。

如果该驱动程序不支持视频 HDR，驱动程序不应实现此控件。

此控件用作对该驱动程序的提示。 如果设置为 VIDEOHDR\_，驱动程序应执行视频 HDR 作为最大努力。

此控件的组调用不起作用时视频的 pin 是 KSSTATE\_运行状态。 该驱动程序应拒绝集呼叫情况视频插针是处于运行状态，并返回状态下，接收\_无效\_设备\_状态。 在 GET 调用中，驱动程序应返回标志字段中的当前设置。

下表介绍标志功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOHDR_OFF</p></td>
<td><p>这是必需的功能。 指定，在驱动程序和驱动程序中禁用 HDR 视频应在视频流上执行视频 HDR。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOHDR_ON</p></td>
<td><p>这是必需的功能。 指定时，的视频驱动程序和驱动程序中启用 HDR 应作为最大努力执行视频 HDR。 此标志为 VIDEOHDR_AUTO 和 VIDEOHDR_OFF 标志与互斥。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOHDR_AUTO</p></td>
<td><p>此功能是可选的。 如果指定，支持此类功能的驱动程序将确定是否应执行视频 HDR 根据场景分析。 此标志为 VIDEOHDR_ON 和 VIDEOHDR_OFF 标志与互斥。</p></td>
</tr>
</tbody>
</table>

下表包含的说明和要求[KSCAMERA\_EXTENDEDPROP\_标头](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段时使用的控件。

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
<td><p>必须将 Pin 与关联的 ID 视频的 pin。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE)。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示最后一个设置操作的错误结果。 如果未设置操作发生，这必须为 0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须是支持 KSCAMERA_EXTENDEDPROP_VIDEOHDR_ * 标志上面定义的按位 OR。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是上面定义的 KSCAMERA_EXTENDEDPROP_VIDEOHDR_ * 任何的标志一个。</p></td>
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
