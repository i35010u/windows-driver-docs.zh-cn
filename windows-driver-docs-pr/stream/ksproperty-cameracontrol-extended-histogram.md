---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 直方图
description: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 直方图是用于控制驱动程序生成的直方图元数据的属性 ID。 这只是针对预览 pin 的 pin 级别控制。
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
ms.openlocfilehash: 8e773c7f22ee675bd7416259471865e7d021af14
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187375"
---
# <a name="ksproperty_cameracontrol_extended_histogram"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 直方图


**KSPROPERTY \_CAMERACONTROL \_ 扩展 \_ 直方图** 是用于控制驱动程序生成的直方图元数据的属性 ID。 这只是针对预览 pin 的 pin 级别控制。

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
<th>控制</th>
<th>类型</th>
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

 

以下标志可以放置在 **KSCAMERA \_ EXTENDEDPROP \_ 标头中。** 用于控制驱动程序中直方图元数据的标志字段。 默认为 **直方图 \_ **。

```cpp
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_OFF      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_ON       0x0000000000000001
```

必须先在 [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 元数据**](ksproperty-cameracontrol-extended-metadata.md) 控件之前使用此控件，以确保分配适当大小的元数据缓冲区。

如果设置为 **" \_ 直方图**"，驱动程序不应在预览 pin 上传递直方图元数据。 驱动程序不应在其元数据缓冲区大小要求中包含直方图元数据大小。

如果设置为 ** \_ "直方图 on**"，则驱动程序应在预览 pin 上传递直方图元数据。 驱动程序必须在其元数据缓冲区大小要求中包含直方图元数据大小。

如果驱动程序没有生成直方图元数据的功能，驱动程序不应实现此控制。 如果驱动程序支持此控件，则它还必须支持 [**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 元数据**](ksproperty-cameracontrol-extended-metadata.md) 控件。

当预览 pin 处于任何高于 KSSTATE 停止状态的状态时，此控件的 **设置** 调用不起作用 \_ 。 如果预览不处于停止状态，则驱动程序将拒绝收到的 **设置** 呼叫，并且返回 **状态 " \_ 无效 \_ 设备 \_ 状态**"。 在 **GET** 调用中，驱动程序应返回 " **标志** " 字段中的当前设置。

下表包含使用控件时 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构字段的说明和要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>说明</th>
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
<td><p>大小</p></td>
<td><p>这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>) 。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示上一次 <strong>设置</strong> 操作的错误结果。 如果未执行任何 <strong>设置</strong> 操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须为 0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的 <strong>KSCAMERA_EXTENDEDPROP_HISTOGRAM_ *</strong> 标志之一。</p></td>
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