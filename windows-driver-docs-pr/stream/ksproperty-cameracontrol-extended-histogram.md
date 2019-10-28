---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_直方图
description: KSPROPERTY\_CAMERACONTROL\_扩展\_直方图是一个属性 ID，将用于控制驱动程序生成的直方图元数据。 这只是针对预览 pin 的 pin 级别控制。
ms.assetid: 638AA1AA-F8E5-4FD7-9283-CF1F23266474
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_HISTOGRAM 流媒体设备
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
ms.openlocfilehash: 678986809f5efc2152997fa74f602f98a80af3ef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841599"
---
# <a name="ksproperty_cameracontrol_extended_histogram"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_直方图


**KSPROPERTY\_CAMERACONTROL\_扩展\_直方图**是一个属性 ID，将用于控制驱动程序生成的直方图元数据。 这只是针对预览 pin 的 pin 级别控制。

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

 

以下标志可以放置在**KSCAMERA\_EXTENDEDPROP\_标头中。** 用于控制驱动程序中直方图元数据的标志字段。 默认值为 "**直方图\_OFF**"。

```cpp
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_OFF      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_ON       0x0000000000000001
```

此控件必须在[**KSPROPERTY\_CAMERACONTROL\_扩展\_元数据**](ksproperty-cameracontrol-extended-metadata.md)控件之前使用，以确保分配适当大小的元数据缓冲区。

如果设置为**直方图\_关闭**，驱动程序不应在预览 pin 上传递直方图元数据。 驱动程序不应在其元数据缓冲区大小要求中包含直方图元数据大小。

如果设置为**直方图\_on**，则驱动程序应在预览 pin 上传递直方图元数据。 驱动程序必须在其元数据缓冲区大小要求中包含直方图元数据大小。

如果驱动程序没有生成直方图元数据的功能，驱动程序不应实现此控制。 如果驱动程序支持此控件，则它还必须支持[**KSPROPERTY\_CAMERACONTROL\_扩展\_元数据**](ksproperty-cameracontrol-extended-metadata.md)控件。

如果预览 pin 处于任何高于 KSSTATE\_停止状态的状态，则该控件的**设置**调用不起作用。 如果预览不处于停止状态，驱动程序应拒绝收到的**设置**呼叫，并返回**状态\_无效\_设备\_状态**。 在**GET**调用中，驱动程序应返回 "**标志**" 字段中的当前设置。

下表包含使用控件时[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的说明和要求。

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
<td><p>必须是与预览 pin 关联的 Pin ID。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>这必须是 sizeof （<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>） + Sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>）。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示上一次<strong>设置</strong>操作的错误结果。 如果未执行任何<strong>设置</strong>操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须为0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的<strong>KSCAMERA_EXTENDEDPROP_HISTOGRAM_ *</strong>标志之一。</p></td>
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
