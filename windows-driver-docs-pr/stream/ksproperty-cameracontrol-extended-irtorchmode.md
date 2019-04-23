---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_IRTORCHMODE
description: 此扩展的属性控制客户端用于控制红外线 （ir） 照相机的红外 torch 电源级别和关税重启。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE 流式处理媒体设备
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
ms.openlocfilehash: 33622352c609efc6584a22c4112f30f9d7267d52
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905268"
---
# <a name="kspropertycameracontrolextendedirtorchmode"></a>KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE

此扩展的属性控制客户端用于控制红外线 （ir） 照相机的红外 torch 电源级别和关税重启。 发送到标准以及驱动程序[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构跟[KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构。

## <a name="usage-summary-table"></a>使用率摘要表

| Get | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
| --- | --- | --- | --- | --- |
| 是 | 是 | Filter | [KSPROPERTY](https://docs.microsoft.com/previous-versions//ff564262(v=vs.85)) | [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)|

## <a name="remarks"></a>备注

属性请求包含[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和一个[KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构。

Total 属性数据大小为 sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING)。 **大小**的成员[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)设置为此属性的总数据大小。

以下是标志，它们可以放入**KSCAMERA_EXTENDEDPROP_HEADER。标志**和**KSCAMERA_EXTENDEDPROP_HEADER。功能**字段。  它们定义 IR torch 运行模式。

| Torch 模式                                                       | 描述                        |
|------------------------------------------------------------------|------------------------------------|
| KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF                            | 关闭                                |
| KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON                      | 始终可用                          |
| KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATING_FRAME_ILLUMINATION | 在每个其他帧           |

KSCAMERA_EXTENDEDPROP_IRTORCHMODE 始终是同步的控件。  照相机不流式处理时，该控件具有未定义的行为。

对于 GET 请求，驱动程序将设置以下字段：

- **KSCAMERA_EXTENDEDPROP_HEADER。功能**与上述 KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ 的位掩码*XXX*表示支持的照相机的运行模式的标志。
- **KSCAMERA_EXTENDEDPROP_HEADER。标志**上述 KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ 之一*XXX*标志以指示当前操作模式。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。模式**为 0。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。最小值**到可用的最小功率级别。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。最大**到可用的最大的功率级别。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。步骤**到电源级别之间的最小增量。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。VideoProc.ul**到当前的电源级别。 此值应默认为人脸验证控件通常使用的相同电源级别。

对于组的请求，驱动程序使用以下字段：

- **KSCAMERA_EXTENDEDPROP_HEADER。标志**设置运行模式。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。VideoProc.ul**设置功率级别。  此值不起 KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF 上。

下表包含的说明和要求[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构时使用元数据控件字段。

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
<td><p>Version</p></td>
<td><p>这必须是 1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0XFFFFFFFF)。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>This must be sizeof(KSCAMERA_EXTENDEDPROP_HEADER)+sizeof([KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)),</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>对于同步控件将忽略此值。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>可能的任意组合<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF</strong>， <strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON</strong>或<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>。  
此字段必须报告至少一个功能。  该字段必须报告<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON</strong>或<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>和 / 或。 该值<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF</strong>是可选的。
</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>必须在其中一个标志中报告功能。  默认值必须必须是<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON</strong>或<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>。</p></td>
</tr>
</tbody>
</table>

下表包含的说明和要求[KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)结构字段时使用 IR torch 模式控制。

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
<td><p>模式</p></td>
<td><p>未使用。  必须为 0。</p></td>
</tr>
<tr class="even">
<td><p>最小值/最大/步骤</p></td>
<td><p>最小值/最大/步骤包含最小值/最大/增量的红外线 （ir） 电源设置。  驱动程序必须返回它们的 GET 操作。  （最大值-最小值） 必须是整除的步骤。  步骤可能不是零 (0)。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>对于集合运算，VideoProc.Value.ul 必须指定最小值/最大/Step 参数所描述的范围内的电源级别。  对于 GET 操作，则驱动程序必须返回当前的电源级别。</p></td>
</tr>
<tr class="even">
<td><p>保留</p></td>
<td><p>未使用。  必须忽略由驱动程序。</p></td>
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
