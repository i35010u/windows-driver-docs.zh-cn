---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_IRTORCHMODE
description: 此扩展属性控件由客户端用来控制 IR 相机的红外 torch 的电源级别和工作周期。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 04/03/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.custom: 19H1
ms.openlocfilehash: f8833e4b946294c4c1a9a987d4e2d0c35ee66414
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843226"
---
# <a name="ksproperty_cameracontrol_extended_irtorchmode"></a>KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE

此扩展属性控件由客户端用来控制 IR 相机的红外 torch 的电源级别和工作周期。 它连同标准[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构一起发送到驱动程序，后跟[KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构。

## <a name="usage-summary-table"></a>使用情况摘要表

| “获取” | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
| --- | --- | --- | --- | --- |
| “是” | “是” | Filter | [KSPROPERTY](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)) | [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)|

## <a name="remarks"></a>备注

属性请求包含[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构。

总的属性数据大小为 sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING）。 [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

下面是可以放置在 KSCAMERA_EXTENDEDPROP_HEADER 中的标志 **。Flags**和**KSCAMERA_EXTENDEDPROP_HEADER。功能**字段。  它们定义了 IR torch 的运行模式。

| Torch 模式                                                       | 描述                        |
|------------------------------------------------------------------|------------------------------------|
| KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF                            | Off                                |
| KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON                      | Always on                          |
| KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATING_FRAME_ILLUMINATION | 每隔一帧上的           |

KSCAMERA_EXTENDEDPROP_IRTORCHMODE 始终是一个同步控件。  当照相机未进行流式处理时，控件没有已定义的行为。

对于 GET 请求，驱动程序将设置以下字段：

- **KSCAMERA_EXTENDEDPROP_HEADER。此功能**具有上述 KSCAMERA_EXTENDEDPROP_IRTORCHMODE_*XXX*标志的位掩码，表示照相机支持的操作模式。
- **KSCAMERA_EXTENDEDPROP_HEADER。标记**为上述 KSCAMERA_EXTENDEDPROP_IRTORCHMODE_*XXX*标志之一，以指示当前运行模式。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。模式**为0。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。** 最小可用电源级别的最小值。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。最大**可用电源级别。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。单步执行**电源级别间的最小增量。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。VideoProc**到当前电源级别。 默认情况下，此值应为正面身份验证控件通常使用的相同电源级别。

对于集请求，驱动程序使用以下字段：

- **KSCAMERA_EXTENDEDPROP_HEADER。** 用于设置运行模式的标志。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。VideoProc**设置一个电源级别。  此值对 KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF 不起作用。

下表包含在使用元数据控件时[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的说明和要求。

<table>
<colgroup>
<col width="30%" />
<col width="70%" />
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
<td><p>KSCAMERA_EXTENDEDPROP_FILTERSCOPE （0xFFFFFFFF）。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>这必须是 sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （[KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)），</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>对于同步控件，此值将被忽略。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>可以是<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF</strong>、 <strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON</strong>或<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>的任意组合。  
此字段必须报告至少一项功能。  此字段必须报告 " <strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON</strong> " 或 " <strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATIVE_FRAME_ILLUMINATION</strong> "。 值<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF</strong>是可选的。
</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>必须是功能中所报告的标志之一。  默认值必须是<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON</strong>或<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>。</p></td>
</tr>
</tbody>
</table>

下表包含使用 IR torch 模式控件时[KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构字段的说明和要求。

<table>
<colgroup>
<col width="30%" />
<col width="70%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“模式”</p></td>
<td><p>用.  必须为0。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/步骤</p></td>
<td><p>最小/最大/步骤包含 IR 电源设置的最小/最大/增量。  对于 GET 操作，驱动程序必须返回这些。  （最大值–分钟）必须按步骤进行均匀地分隔。  步骤不能为零（0）。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>对于 SET 操作，VideoProc 必须指定最小/最大值/步骤参数描述的范围内的电源级别。  对于 GET 操作，驱动程序必须返回当前的电源级别。</p></td>
</tr>
<tr class="even">
<td><p>保留</p></td>
<td><p>用.  驱动程序必须忽略。</p></td>
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
