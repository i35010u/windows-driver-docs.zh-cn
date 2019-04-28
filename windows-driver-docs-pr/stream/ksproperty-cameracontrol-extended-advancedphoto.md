---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_ADVANCEDPHOTO
description: KSPROPERTY\_CAMERACONTROL\_扩展\_ADVANCEDPHOTO 用于控制照片 HDR，flash 没有闪存，和超高低浅合成驱动程序。 这是照片 pin 仅 pin 级别控制。
ms.assetid: 88C14C9E-8675-42BF-A606-64232ABD4FD1
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ADVANCEDPHOTO 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ADVANCEDPHOTO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 840fa4452e61c1725555dcbfdcc1725204c93c3b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348044"
---
# <a name="kspropertycameracontrolextendedadvancedphoto"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_ADVANCEDPHOTO


KSPROPERTY\_CAMERACONTROL\_扩展\_ADVANCEDPHOTO 用于控制照片 HDR，flash 没有闪存，和超高低浅合成驱动程序。 这是照片 pin 仅 pin 级别控制。

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

 

以下是标志，它们可以位于 KSCAMERA\_EXTENDEDPROP\_标头。Flags 字段控件照片 HDR，闪存没有闪存，和超高低浅合成。 默认值应为 KSCAMERA\_EXTENDEDPROP\_ADVANCEDPHOTO\_OFF。

```cpp
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_OFF             0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_AUTO            0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_HDR             0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_FNF             0x0000000000000004
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ULTRALOWLIGHT   0x0000000000000008
```

如果该驱动程序支持此控件，它必须支持 KSCAMERA\_EXTENDEDPROP\_ADVANCEDPHOTO\_OFF。

如果该驱动程序不支持任何高级照片捕获，驱动程序不应实现此控件。

此控件的组调用不起作用时照片 pin 是 KSSTATE\_运行状态。 该驱动程序应拒绝集呼叫情况照片 pin 处于运行状态，并返回状态下，接收\_无效\_设备\_状态。 在 GET 调用中，驱动程序应返回 Flags 字段中的当前设置。

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
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_OFF</p></td>
<td><p>这是必需的功能。 指定时，应在驱动程序中不执行任何高级的照片。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_AUTO</p></td>
<td><p>此功能是可选的。 当指定为单独，支持此类功能的驱动程序将确定照片 HDR，应执行任何 Flash 或超高低浅合成的 Flash 基于场景分析。 此标志与 OFF 标志互斥，可以用于其他标志。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_HDR</p></td>
<td><p>此功能是可选的。 当单独指定，支持此类功能的驱动程序将执行照片 HDR。 此标志是与除自动之外的其他标志互斥。 时与自动一起指定，该驱动程序将确定是否应执行 HDR 照片基于场景分析。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_FNF</p></td>
<td><p>此功能是可选的。 时单独，指定驱动程序将执行此类功能的支持 flash 没有立刻正式投入工作。 此标志是与除自动之外的其他标志互斥。 时与自动一起指定，该驱动程序将确定是否应执行任何 flash flash 基于场景分析。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ULTRALOWLIGHT</p></td>
<td><p>此功能是可选的。 当单独指定，支持此类功能的驱动程序将执行超高低浅合成。 此标志是与除自动之外的其他标志互斥。 时与自动一起指定，该驱动程序将确定是否应执行超高低浅合成根据场景分析。</p></td>
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
<td><p>必须将 Pin 与关联的 ID 照片 pin。</p></td>
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
<td><p>必须是支持 KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ * 标志上面定义的按位 OR。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是上面定义的 KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ * 任何的标志一个。</p></td>
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
