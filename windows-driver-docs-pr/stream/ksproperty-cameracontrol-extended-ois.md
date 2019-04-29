---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_OIS
description: KSPROPERTY\_CAMERACONTROL\_扩展\_OIS 是用来控制该驱动程序的光盘映像稳定 (OIS) 的属性 ID。
ms.assetid: CF4F1283-1517-4F93-8554-FBD4B068A655
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OIS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OIS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: fa074271d224a9309abe496dab95a2ab1fa68fd3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380323"
---
# <a name="kspropertycameracontrolextendedois"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_OIS

**KSPROPERTY\_CAMERACONTROL\_扩展\_OIS**是用来控制该驱动程序的光盘映像稳定 (OIS) 的属性 ID。

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

以下标志可以置于**KSCAMERA\_EXTENDEDPROP\_标头。标志**字段控件光盘映像稳定。 默认值应否则如果支持自动，则自动或 ON。

```cpp
#define KSCAMERA_EXTENDEDPROP_OIS_OFF   0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_OIS_ON    0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_OIS_AUTO  0x0000000000000002 
```

如果该驱动程序支持此控件，它必须支持 OIS\_ON 和 OIS\_OFF。

如果该驱动程序不支持光学映像稳定，驱动程序不应实现此控件。

此控件的组调用不起作用 KSSTATE 视频或照片 pin 时\_运行状态。 该驱动程序应拒绝集呼叫情况视频或照片 pin 处于运行状态，并返回状态下，接收\_无效\_设备\_状态。 在 GET 调用中，驱动程序应返回 Flags 字段中的当前设置。

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
<td><p>KSCAMERA_EXTENDEDPROP_OIS_OFF</p></td>
<td><p>这是必需的功能。 如果指定，光学映像稳定禁用驱动程序中。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_OIS_ON</p></td>
<td><p>这是必需的功能。 指定时，驱动程序中启用光盘映像稳定。 此标志为 OIS_AUTO 和 OIS_OFF 标志与互斥。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_OIS_AUTO</p></td>
<td><p>此功能是可选的。 如果指定，支持此类功能的驱动程序将确定光盘映像稳定应打开或关闭。 此标志为 OIS_ON 和 OIS_OFF 标志与互斥。</p></td>
</tr>
</tbody>
</table>

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
<td><p>这必须是 KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)。</p></td>
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
<td><p>必须是支持 KSCAMERA_EXTENDEDPROP_OIS_ * 标志上面定义的按位 OR。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是上面定义的 KSCAMERA_EXTENDEDPROP_OIS_ * 任何的标志一个。</p></td>
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
