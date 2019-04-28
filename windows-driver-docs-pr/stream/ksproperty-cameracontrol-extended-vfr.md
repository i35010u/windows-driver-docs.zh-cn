---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_VFR
description: KSPROPERTY\_CAMERACONTROL\_扩展\_VFR 是将用于指定变量的帧速率是否所需的驱动程序上的属性 ID。
ms.assetid: 9B528421-B5AA-4092-9F7B-71A18732ABA8
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VFR 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VFR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2b4ea75cb9f6f30a1202724ca249790bea0594d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341879"
---
# <a name="kspropertycameracontrolextendedvfr"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_VFR

KSPROPERTY\_CAMERACONTROL\_扩展\_VFR 是将用于指定变量的帧速率是否所需的驱动程序上的属性 ID。 这是视频的 pin 的 pin 级别控制。 有关预览版和照片，帧速率可变性完全取决于驱动程序并不是由客户端可以控制。

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

以下标志可以置于**KSCAMERA\_EXTENDEDPROP\_标头。标志**字段，用于打开和关闭视频的变量的帧速率。 默认值为最多驱动程序。

```cpp
#define KSCAMERA_EXTENDEDPROP_VFR_OFF   0x0000000000000000  
#define KSCAMERA_EXTENDEDPROP_VFR_ON    0x0000000000000001
```
如果设置为 VFR\_，驱动程序应提供固定的帧速率视频的 pin。

如果设置为 VFR\_，帧速率由驱动程序自动确定，并且可以差异取决于捕获条件和视频的 pin 的方案。 当 VFR\_ON 设置，但允许的最大帧速率进一步由嵌入视频录制为选定的媒体类型的固定的帧速率。

如果驱动程序不支持可变帧率的视频，该驱动程序不应实现此控件，并将隐式固定的帧速率。

此控件在视频录制不支持动态切换 VFR 设置上的驱动程序没有任何影响。 该驱动程序应忽略期间活动的视频录制在这种情况下接收到的控件。

这是一个同步控件并不可取消。 没有为此控件定义功能。

下表包含的说明和要求[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段时使用的控件。

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
<td><p>这必须是与视频 pin 关联的 Pin ID。</p></td>
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
<td><p>这必须是 0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是上面定义的任何的标志一个。</p></td>
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
