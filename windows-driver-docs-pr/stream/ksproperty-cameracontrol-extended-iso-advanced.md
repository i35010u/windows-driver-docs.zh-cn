---
title: KSPROPERTY\_CAMERACONTROL\_EXTENDED\_ISO\_ADVANCED
description: KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级是允许具有更多粒度更具有全局性 ISO 控件的扩展的属性控件。
ms.assetid: A9327DB8-422B-410C-8766-D70811BA5C73
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ISO_ADVANCED 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ISO_ADVANCED
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: f0e610c54c38102ed21ee52e4a8284c2c75dc5d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325937"
---
# <a name="kspropertycameracontrolextendedisoadvanced"></a>KSPROPERTY\_CAMERACONTROL\_EXTENDED\_ISO\_ADVANCED

KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级是允许具有更多粒度更具有全局性 ISO 控件的扩展的属性控件。

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
<td><p>Pin （照片）</p></td>
<td><p>异步</p></td>
</tr>
</tbody>
</table>

新 KSCAMERA\_EXTENDEDPROP\_ISO\_手动标志定义中 ksmedia\_phone.h，如下所示。

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_MANUAL          0x0080000000000000
```

下表包含的说明和要求[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) KSPROPERTY 为结构字段\_CAMERACONTROL\_扩展\_ISO\_高级的控制。

Windows 8.1 KS\_CAMERACONTROL\_扩展\_ISO 保持不变，而无需整数手动 ISO 的支持。 该驱动程序应仅支持新 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级的控制。 如果这两种控件都受支持，管道将默认为 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级的控制。

如果 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_支持高级的控制，该驱动程序可以播发的唯一功能是以下。

-   KSCAMERA\_EXTENDEDPROP\_ISO\_AUTO

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手动

-   KSCAMERA\_EXTENDEDPROP\_CAPS\_ASYNCCONTROL

如果该驱动程序播发 KSCAMERA\_EXTENDEDPROP\_ISO\_手动功能标志，它还必须播发 KSCAMERA 的 Min/Max/步骤值中所支持的 ISO 范围\_扩展\_PROP\_VIDEOPROCSETTING 属性。 如果驱动程序播发 0 最小值和最大值为 0 或步骤值小于 1，该控件标记为不可用，并通过管道将被拒绝。

如果该驱动程序支持这两个 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级和 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO，驱动程序必须播发 KSCAMERA\_EXTENDEDPROP\_ISO\_自动为这两个 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级和 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO。 否则，这两个 ISO 控件将标记为不可用并可由 MF 管道被拒绝。

如果该驱动程序播发 KSCAMERA\_EXTENDEDPROP\_ISO\_KSPROPERTY 中手动\_CAMERACONTROL\_扩展\_ISO\_高级和数值 KSCAMERA\_EXTENDEDPROP\_ISO\_XXX 值中 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO、 数值 KSCAMERA\_EXTENDEDPROP\_ISO\_XXX 值中播发的 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO 应在支持手动 ISO 的范围内所播发的 KSCAMERA\_EXTENDEDPROP\_ISO\_手动。 此外，所有数值 KSCAMERA\_EXTENDEDPROP\_ISO\_中所支持的手动范围 XXX 值应由 KSPROPERTY 播发\_CAMERACONTROL\_扩展\_ISO。 否则，这两个 ISO 控件可能标记为不可用并可由 MF 管道被拒绝。

例如，以下任何一项功能可能会被视为灾难性故障和 MF 管道可能拒绝该控件。

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手动 (最小值 = 40，最大 = 240 步骤 = 20)，KSCAMERA\_EXTENDEDPROP\_ISO\_50

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手动 (最小值 = 40，最大 = 240 步骤 = 20)，KSCAMERA\_EXTENDEDPROP\_ISO\_80

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手动 (最小值 = 40，最大 = 240 步骤 = 20)，KSCAMERA\_EXTENDEDPROP\_ISO\_400

MF 管道接受的以下任何功能。

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手动 (最小值 = 40，最大 = 240 步骤 = 20)，KSCAMERA\_EXTENDEDPROP\_ISO\_80，KSCAMERA\_EXTENDEDPROP\_ISO\_100，KSCAMERA\_EXTENDEDPROP\_ISO\_200

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手动 (最小值 = 40，最大 = 240 步骤 = 20)

-   KSCAMERA\_EXTENDEDPROP\_ISO\_80, KSCAMERA\_EXTENDEDPROP\_ISO\_200

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
<td><p>这必须是 1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是照片 pin 与关联的 Pin ID。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof(KSCAMERA_EXTENDEDPROP_HEADER)+sizeof(KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING)，</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这包含最后一个设置操作的错误结果。 如果未设置操作发生，这必须为 0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是位或的 KSCAMERA_EXTENDEDPROP_ISO_AUTO 和/或 KSCAMERA_EXTENDEDPROP_ISO_MANUAL 和 KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL 标志。 此控件必须是异步的。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是任何上面定义的 KSCAMERA_EXTENDEDPROP_ISO_XXX 标志。</p></td>
</tr>
</tbody>
</table>

 

下表包含的说明和要求 KSCAMERA\_EXTENDEDPROP\_ISO DDI VIDEOPROCSETTING 结构字段。 此结构在 ksmedia.h 中定义。

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
<td><p>模式</p></td>
<td><p>这是未使用，必须为 0。</p></td>
</tr>
<tr class="even">
<td><p>最小值/最大/步骤</p></td>
<td><p>最小值/最大/步骤包含最小值/最大/增量的照相机的驱动程序支持的手动 ISO 速度。 如果支持手动 ISO，则驱动程序必须返回这些的 GET 操作。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>如果手动 KSCAMERA_EXTENDEDPROP_HEADER 标志字段中指定，VideoProc.Value.ul 必须指定最小值/最大/Step 参数所描述的范围内的当前 ISO 速度值。</p>
<p>如果指定除手动之外的标志，则为设置操作，则忽略 VideoProc 字段。 对于 GET 操作，该驱动程序必须始终返回当前的 ISO 速度而不考虑。</p></td>
</tr>
<tr class="even">
<td><p>保留</p></td>
<td><p>这是未使用。 这必须忽略由驱动程序。</p></td>
</tr>
</tbody>
</table>

 

**获取调用**

该驱动程序必须播发其功能在 KSCAMERA\_EXTENDEDPROP\_标头。功能和当前 ISO 标志在驱动程序中 KSCAMERA\_EXTENDEDPROP\_标头。Flags.Â 如果没有集调用不断发出 Get 调用之前驱动程序应返回其默认值在 KSCAMERA\_EXTENDEDPROP\_标头。标志。

如果 KSCAMERA\_EXTENDEDPROP\_ISO\_手动标志播发在功能字段中，该驱动程序必须进一步播发所支持的范围中 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING。最小值/最大/步骤。

该驱动程序还必须报告 KSCAMERA 中正在使用当前的 ISO 速度\_EXTENDEDPROP\_VIDEOPROCSETTING。VideoProc.Value.ul。 如果曾经已不发出任何集调用之前的 GET 调用，则驱动程序应返回其当前的 ISO 速度在 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING。VideoProc.Value.ul。

**设置调用**

KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING。如果 VideoProc.Value.ul 包含所需的整数手动 ISO 速度 KSCAMERA\_EXTENDEDPROP\_ISO\_手动指定在 KSCAMERA\_EXTENDEDPROP\_标头。标志。

如果 KSCAMERA\_EXTENDEDPROP\_ISO\_KSCAMERA 中指定自动标志\_EXTENDEDPROP\_标头。标志、 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING。VideoProc.Value.ul 将被忽略。

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
