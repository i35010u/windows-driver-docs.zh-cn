---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOHDR
description: KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOHDR 用于启用或禁用驱动程序上的高动态范围（HDR）视频。 这是仅用于视频 pin 的 pin 级别控制。
ms.assetid: AC798BF1-4E1A-48D8-8F56-986F89D9C153
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOHDR 流媒体设备
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
ms.openlocfilehash: 050e2dcc7cf7315ceae4cabb6da3ae17cc910a36
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826202"
---
# <a name="ksproperty_cameracontrol_extended_videohdr"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOHDR

KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOHDR 用于启用或禁用驱动程序上的高动态范围（HDR）视频。 这是仅用于视频 pin 的 pin 级别控制。

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
<td><p>大头针</p></td>
<td><p>同步</p></td>
</tr>
</tbody>
</table>

以下标志可以放置在 KSCAMERA\_EXTENDEDPROP\_标头中。用于控制视频 HDR 的标志字段。 默认情况下，驱动程序应设置为 "VIDEOHDR\_OFF"。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOHDR_OFF      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_VIDEOHDR_ON       0x0000000000000001 
#define KSCAMERA_EXTENDEDPROP_VIDEOHDR_AUTO     0x0000000000000002 
```

如果驱动程序支持此控件，则它必须支持 VIDEOHDR\_ON/VIDEOHDR\_OFF。

如果驱动程序不支持视频 HDR，驱动程序不应实现此控制。

此控件用作驱动程序的提示。 当设置为 VIDEOHDR\_ON 时，驱动程序应作为最佳工作来执行视频 HDR。

当视频 pin KSSTATE\_运行状态时，此控件的设置调用不起作用。 如果视频 pin 处于运行状态并且返回状态\_无效\_设备\_状态，则驱动程序应拒绝收到的设置呼叫。 在 GET 调用中，驱动程序应返回 "标志" 字段中的当前设置。

下表介绍了标志功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>旗帜</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOHDR_OFF</p></td>
<td><p>这是必需的功能。 指定时，驱动程序中的视频 HDR 处于禁用状态，驱动程序不应在视频流上执行视频 HDR。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOHDR_ON</p></td>
<td><p>这是必需的功能。 指定时，驱动程序中会启用视频 HDR，驱动程序应最大程度地执行视频 HDR。 此标志与 VIDEOHDR_AUTO 和 VIDEOHDR_OFF 标志互相排斥。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOHDR_AUTO</p></td>
<td><p>此功能是可选的。 指定时，支持此类功能的驱动程序将根据场景分析确定是否应执行视频 HDR。 此标志与 VIDEOHDR_ON 和 VIDEOHDR_OFF 标志互相排斥。</p></td>
</tr>
</tbody>
</table>

下表包含使用控件时[KSCAMERA\_EXTENDEDPROP\_标头](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的说明和要求。

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
<td><p>必须是与视频 pin 关联的 Pin ID。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>这必须是 sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VALUE）。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须是前面定义的受支持的 KSCAMERA_EXTENDEDPROP_VIDEOHDR_ * 标志的按位 "或"。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的 KSCAMERA_EXTENDEDPROP_VIDEOHDR_ * 标志之一。</p></td>
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
