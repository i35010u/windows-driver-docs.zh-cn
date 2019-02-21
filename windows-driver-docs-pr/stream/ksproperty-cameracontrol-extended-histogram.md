---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_直方图
description: KSPROPERTY\_CAMERACONTROL\_扩展\_直方图是将用于控制驱动程序产生的直方图元数据的属性 ID。 这是预览针仅 pin 级别控制。
ms.assetid: 638AA1AA-F8E5-4FD7-9283-CF1F23266474
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_HISTOGRAM 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_HISTOGRAM
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: b8d49557c2d767d44bb3e58bc75091be2e2f7719
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541636"
---
# <a name="kspropertycameracontrolextendedhistogram"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_直方图


**KSPROPERTY\_CAMERACONTROL\_扩展\_直方图**将用于控制驱动程序产生的直方图元数据的属性 id。 这是预览针仅 pin 级别控制。

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

 

以下标志可以置于**KSCAMERA\_EXTENDEDPROP\_标头。标志**字段来控制驱动程序中的直方图元数据。 默认值是**直方图\_OFF**。

```cpp
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_OFF      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_ON       0x0000000000000001
```

前，必须使用此控件[ **KSPROPERTY\_CAMERACONTROL\_扩展\_元数据**](ksproperty-cameracontrol-extended-metadata.md)控制以确保适当大小的元数据缓冲区分配。

如果设置为**直方图\_OFF**，驱动程序不应在预览针上提供直方图元数据。 该驱动程序不应在其元数据缓冲区大小要求中包括直方图元数据大小。

如果设置为**直方图\_ON**，驱动程序应在预览针时传递的直方图元数据。 该驱动程序必须在其元数据缓冲区大小要求包括直方图元数据大小。

如果该驱动程序没有生成直方图的元数据的功能，该驱动程序不应实现此控件。 如果该驱动程序支持此控件，它必须支持[ **KSPROPERTY\_CAMERACONTROL\_扩展\_元数据**](ksproperty-cameracontrol-extended-metadata.md)控件。

**设置**调用此控件不起作用时预览针处于任何状态高于 KSSTATE\_停止状态。 该驱动程序应拒绝**设置**调用收到如果预览版未处于停止状态，并返回**状态\_无效\_设备\_状态**。 在中**获取**调用时，驱动程序应返回中的当前设置**标志**字段。

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
<td><p>版本</p></td>
<td><p>这必须是 1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>必须将 Pin 与关联的 ID 预览针。</p></td>
</tr>
<tr class="odd">
<td><p>尺寸</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>)。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示最后一个错误结果<strong>设置</strong>操作。 如果没有<strong>设置</strong>操作发生，这必须是 0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须为 0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是任一<strong>KSCAMERA_EXTENDEDPROP_HISTOGRAM_ *</strong>上面定义的标志。</p></td>
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
