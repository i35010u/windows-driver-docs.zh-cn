---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ ISO \_ 高级
description: KSPROPERTY \_ CAMERACONTROL \_ extended \_ iso \_ ADVANCED 是一种扩展属性控件，允许更高粒度的更多全局 ISO 控制。
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
ms.openlocfilehash: 09c14f580aa6b8ab34f27ed9298d278064e0e615
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803465"
---
# <a name="ksproperty_cameracontrol_extended_iso_advanced"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ ISO \_ 高级

KSPROPERTY \_ CAMERACONTROL \_ extended \_ iso \_ ADVANCED 是一种扩展属性控件，允许更高粒度的更多全局 ISO 控制。

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
<td><p>固定 (照片) </p></td>
<td><p>异步</p></td>
</tr>
</tbody>
</table>

新的 KSCAMERA \_ EXTENDEDPROP \_ ISO \_ 手动标志在 ksmedia phone 中定义，如下所示 \_ 。

```cpp
#define KSCAMERA_EXTENDEDPROP_ISO_MANUAL          0x0080000000000000
```

下表包含 KSPROPERTY CAMERACONTROL EXTENDED ISO 高级控制的 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构字段的说明和要求 \_ \_ \_ \_ 。

Windows 8.1 KS \_ CAMERACONTROL \_ EXTENDED \_ iso 保持不变，无需支持整数手动 ISO。 驱动程序仅支持新的 KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ ISO \_ 高级控制。 如果同时支持这两个控件，则管道将默认为 KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ ISO \_ 高级控制。

如果支持 KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ ISO \_ 高级控制，则驱动程序可以播发的唯一功能如下。

-   KSCAMERA \_ EXTENDEDPROP \_ ISO \_ AUTO

-   KSCAMERA \_ EXTENDEDPROP \_ ISO \_ 手册

-   KSCAMERA \_ EXTENDEDPROP \_ CAP \_ ASYNCCONTROL

如果驱动程序公布了 KSCAMERA \_ EXTENDEDPROP \_ ISO \_ 手动功能标志，则它还必须在 KSCAMERA \_ 扩展 \_ 属性 VIDEOPROCSETTING 属性的最小/最大值/步长值中公布受支持的 iso 范围 \_ 。 如果驱动程序公布的最小值为0，最大值为0，而步长值小于1，则该控件将被标记为不可用并被管道拒绝。

如果驱动程序同时支持 KSPROPERTY \_ CAMERACONTROL \_ extended \_ ISO \_ advanced 和 KSPROPERTY \_ CAMERACONTROL \_ extended \_ ISO，则驱动程序必须 \_ \_ \_ 为 KSCAMERA EXTENDEDPROP \_ \_ extended \_ iso \_ advanced 和 KSPROPERTY \_ CAMERACONTROL \_ extended \_ iso 公布 KSPROPERTY CAMERACONTROL ISO AUTO。 否则，两个 ISO 控件都将被标记为不可用，并被 MF 管道拒绝。

如果驱动程序 \_ \_ \_ 在 KSPROPERTY CAMERACONTROL extended iso ADVANCED 中公布 KSCAMERA EXTENDEDPROP ISO， \_ \_ KSCAMERA EXTENDEDPROP \_ \_ extended iso 中的数字 KSPROPERTY \_ CAMERACONTROL \_ iso \_ xxx 值 \_ \_ \_ ，则 KSCAMERA EXTENDEDPROP EXTENDED iso 中公布的数值 KSPROPERTY \_ CAMERACONTROL \_ ISO \_ xxx 值 \_ \_ \_ 应位于 KSCAMERA EXTENDEDPROP \_ \_ iso 手册公布的受支持的手动 iso 范围内 \_ 。 此外， \_ 受支持的手动范围内的所有数字 KSCAMERA EXTENDEDPROP \_ iso \_ XXX 值都应该通过 KSPROPERTY \_ CAMERACONTROL \_ EXTENDED iso 播发 \_ 。 否则，两个 ISO 控件都可能标记为不可用并被 MF 管道拒绝。

例如，以下任何一项的功能可能被视为灾难性故障，而 MF 管道可能会拒绝该控件。

-   KSCAMERA \_ EXTENDEDPROP \_ iso \_ 手册 (分钟 = 40，最大值 = 240，步骤 = 20) ，KSCAMERA \_ EXTENDEDPROP \_ ISO \_ 50

-   KSCAMERA \_ EXTENDEDPROP \_ iso \_ 手册 (分钟 = 40，最大值 = 240，步骤 = 20) ，KSCAMERA \_ EXTENDEDPROP \_ ISO \_ 80

-   KSCAMERA \_ EXTENDEDPROP \_ iso \_ 手册 (分钟 = 40，最大值 = 240，步骤 = 20) ，KSCAMERA \_ EXTENDEDPROP \_ ISO \_ 400

MF 管道接受以下任何一项的功能。

-   KSCAMERA \_ EXTENDEDPROP \_ ISO \_ 手动 (min = 40，max = 240，步骤 = 20) ，KSCAMERA \_ EXTENDEDPROP \_ ISO \_ 80，KSCAMERA \_ EXTENDEDPROP \_ iso \_ 100，KSCAMERA \_ EXTENDEDPROP \_ iso \_ 200

-   KSCAMERA \_ EXTENDEDPROP \_ ISO \_ 手册 (分钟 = 40，最大值 = 240，步骤 = 20) 

-   KSCAMERA \_ EXTENDEDPROP \_ iso \_ 80，KSCAMERA \_ EXTENDEDPROP \_ iso \_ 200

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
<td><p>这必须为1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是与照片 Pin 关联的 Pin ID。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING) 。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这包含上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须 KSCAMERA_EXTENDEDPROP_ISO_AUTO 是比较和/或的 KSCAMERA_EXTENDEDPROP_ISO_MANUAL 和 KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL 标志。 此控件必须是异步的。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的任何 KSCAMERA_EXTENDEDPROP_ISO_XXX 标志。</p></td>
</tr>
</tbody>
</table>

 

下表包含 \_ ISO DDI 的 KSCAMERA EXTENDEDPROP VIDEOPROCSETTING 结构字段的说明和要求 \_ 。 此结构在 ksmedia 中定义。

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
<td><p>“模式”</p></td>
<td><p>这是未使用的，必须为0。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/步骤</p></td>
<td><p>最小/最大/步骤包含照相机驱动程序所支持的手动 ISO 速度的最小/最大/增量。 如果支持手动 ISO，则驱动程序必须为 GET 操作返回这些。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>如果在 KSCAMERA_EXTENDEDPROP_HEADER 的 "标志" 字段中指定了 "手动"，则 VideoProc 必须指定最小/最大值参数所描述范围内的当前 ISO 速度值。</p>
<p>如果为 SET 操作指定了除 "手动" 之外的标志，则将忽略 VideoProc 字段。 对于 GET 操作，驱动程序必须始终返回当前的 ISO 速度，而不考虑。</p></td>
</tr>
<tr class="even">
<td><p>预留</p></td>
<td><p>这是未使用的。 驱动程序必须忽略此情况。</p></td>
</tr>
</tbody>
</table>

 

**获取调用**

驱动程序必须在 KSCAMERA \_ EXTENDEDPROP 标头中公布其功能 \_ 。KSCAMERA \_ EXTENDEDPROP 标头中驱动程序的功能和当前 ISO 标志 \_ 。标志。如果从未发出 Get 调用之前发出过任何设置调用，则驱动程序应在 KSCAMERA \_ EXTENDEDPROP \_ 标头中返回其默认值。随意.

如果在 \_ \_ \_ "功能" 字段中公布 KSCAMERA EXTENDEDPROP ISO 手册标志，则驱动程序必须在 KSCAMERA EXTENDEDPROP VIDEOPROCSETTING 中进一步播发受支持的范围 \_ \_ 。最小/最大/步骤。

驱动程序还必须报告在 KSCAMERA EXTENDEDPROP VIDEOPROCSETTING 中使用的当前 ISO 速度 \_ \_ 。VideoProc。 如果在 GET 调用之前未发出任何 SET 调用，则驱动程序应在 KSCAMERA EXTENDEDPROP VIDEOPROCSETTING 中返回其当前的 ISO 速度 \_ \_ 。VideoProc。

**设置调用**

KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING。如果 \_ \_ \_ 在 KSCAMERA \_ EXTENDEDPROP \_ 标头中指定了 KSCAMERA EXTENDEDPROP iso 手册，VideoProc 将包含所需的整数手动 iso 速度。随意.

如果 \_ \_ \_ 在 KSCAMERA \_ EXTENDEDPROP 标头中指定 KSCAMERA EXTENDEDPROP ISO AUTO 标志，则为 \_ 。Flags，KSCAMERA \_ EXTENDEDPROP \_ VIDEOPROCSETTING。VideoProc 将被忽略。

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
