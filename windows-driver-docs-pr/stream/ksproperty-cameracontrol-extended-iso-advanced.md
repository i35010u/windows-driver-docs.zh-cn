---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级
description: KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_"高级" 是一种扩展属性控件，允许更高粒度的全局 ISO 控制。
ms.assetid: A9327DB8-422B-410C-8766-D70811BA5C73
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ISO_ADVANCED 流媒体设备
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
ms.openlocfilehash: 6a9a564ba778461221d1af59b4b98d5c80595bb7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841601"
---
# <a name="ksproperty_cameracontrol_extended_iso_advanced"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级

KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_"高级" 是一种扩展属性控件，允许更高粒度的全局 ISO 控制。

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
<td><p>Pin （照片）</p></td>
<td><p>异步</p></td>
</tr>
</tbody>
</table>

新的 KSCAMERA\_EXTENDEDPROP\_ISO\_手动标志在 ksmedia\_phone 中定义，如下所示。

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_MANUAL          0x0080000000000000
```

下表包含 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级控制的[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的说明和要求。

Windows 8.1 KS\_CAMERACONTROL\_扩展\_ISO 保持不变，无需支持整数手动 ISO。 驱动程序仅支持新的 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级控制。 如果同时支持这两个控件，则管道将默认为 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级控制。

如果支持 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级控制，则驱动程序可以播发的唯一功能如下所示。

-   KSCAMERA\_EXTENDEDPROP\_ISO\_自动

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手册

-   KSCAMERA\_EXTENDEDPROP\_CAP\_ASYNCCONTROL

如果驱动程序公布了 KSCAMERA\_EXTENDEDPROP\_ISO\_手动功能标志，则它还必须在\_KSCAMERA 的最小/最大/步长值中公布受支持的 ISO 范围\_VIDEOPROCSETTING知识产权. 如果驱动程序公布的最小值为0，最大值为0，而步长值小于1，则该控件将被标记为不可用并被管道拒绝。

如果驱动程序同时支持 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_ADVANCED and KSPROPERTY\_CAMERACONTROL\_EXTENDED\_ISO，则驱动程序必须公布 KSCAMERA\_EXTENDEDPROP\_ISO\_自动为 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO\_高级和 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO。 否则，两个 ISO 控件都将被标记为不可用，并被 MF 管道拒绝。

如果驱动程序\_ISO\_\_在 KSPROPERTY CAMERACONTROL\_扩展\_ISO\_\_\_ISO\_\_KSPROPERTY\_CAMERACONTROL\_扩展\_ISO、数字 KSCAMERA\_EXTENDEDPROP\_ISO\_XXX 值（在 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO应在受支持的手动 ISO 范围内，KSCAMERA\_EXTENDEDPROP\_ISO\_手册。 此外，受支持的手动范围内的所有数字 KSCAMERA\_EXTENDEDPROP\_ISO\_XXX 值都应由 KSPROPERTY\_CAMERACONTROL\_扩展\_ISO 播发。 否则，两个 ISO 控件都可能标记为不可用并被 MF 管道拒绝。

例如，以下任何一项的功能可能被视为灾难性故障，而 MF 管道可能会拒绝该控件。

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手册（最小 = 40，最大 = 240，步骤 = 20），KSCAMERA\_EXTENDEDPROP\_ISO\_50

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手册（最小 = 40，最大 = 240，步骤 = 20），KSCAMERA\_EXTENDEDPROP\_ISO\_80

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手册（最小 = 40，最大 = 240，步骤 = 20），KSCAMERA\_EXTENDEDPROP\_ISO\_400

MF 管道接受以下任何一项的功能。

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手册（最小 = 40，最大 = 240，步骤 = 20），KSCAMERA\_EXTENDEDPROP\_ISO\_80，KSCAMERA\_EXTENDEDPROP\_ISO\_100，KSCAMERA\_EXTENDEDPROP\_ISO\_200

-   KSCAMERA\_EXTENDEDPROP\_ISO\_手册（最小 = 40，最大 = 240，步骤 = 20）

-   KSCAMERA\_EXTENDEDPROP\_ISO\_80、KSCAMERA\_EXTENDEDPROP\_ISO\_200

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
<td><p>这必须为1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是与照片 Pin 关联的 Pin ID。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>这必须是 sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING），</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这包含上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是 KSCAMERA_EXTENDEDPROP_ISO_AUTO 和/或 KSCAMERA_EXTENDEDPROP_ISO_MANUAL 和 KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL 标志。 此控件必须是异步的。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的任何 KSCAMERA_EXTENDEDPROP_ISO_XXX 标志。</p></td>
</tr>
</tbody>
</table>

 

下表包含针对 ISO DDI 的 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING 结构字段的说明和要求。 此结构在 ksmedia 中定义。

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
<td><p>“模式”</p></td>
<td><p>这是未使用的，必须为0。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/步骤</p></td>
<td><p>最小/最大/步骤包含照相机驱动程序所支持的手动 ISO 速度的最小/最大/增量。 如果支持手动 ISO，则驱动程序必须为 GET 操作返回这些。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>如果在 KSCAMERA_EXTENDEDPROP_HEADER 的 "标志" 字段中指定了 "手动"，则 VideoProc 必须指定 "最小/最大值" 参数所描述范围内的当前 ISO 速度值。</p>
<p>如果为 SET 操作指定了除 "手动" 之外的标志，则将忽略 VideoProc 字段。 对于 GET 操作，驱动程序必须始终返回当前的 ISO 速度，而不考虑。</p></td>
</tr>
<tr class="even">
<td><p>保留</p></td>
<td><p>这是未使用的。 驱动程序必须忽略此情况。</p></td>
</tr>
</tbody>
</table>

 

**获取调用**

驱动程序必须在 KSCAMERA 中公布其功能\_EXTENDEDPROP\_标头。KSCAMERA\_EXTENDEDPROP\_标头中驱动程序的功能和当前 ISO 标志。标志。如果从未发出 Get 调用之前发出过任何设置调用，则驱动程序应在 KSCAMERA\_EXTENDEDPROP\_标头中返回其默认值。随意.

如果 KSCAMERA\_EXTENDEDPROP\_ISO\_"功能" 字段中公布了 "手动" 标志，则驱动程序必须在 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING 中进一步公布受支持的范围。最小/最大/步骤。

驱动程序还必须在 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING 中报告当前使用的 ISO 速度。VideoProc。 如果以前未发出 GET 调用，则驱动程序应在 KSCAMERA 中返回其当前的 ISO 速度\_EXTENDEDPROP\_VIDEOPROCSETTING。VideoProc。

**设置调用**

KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING。VideoProc 包含所需的整数手动 ISO 速度，如果 KSCAMERA\_EXTENDEDPROP\_ISO\_\_在 KSCAMERA EXTENDEDPROP\_标题中指定。随意.

如果 KSCAMERA\_EXTENDEDPROP\_ISO\_自动标志在 KSCAMERA\_EXTENDEDPROP\_标题中指定。Flags、KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING。VideoProc 将被忽略。

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
