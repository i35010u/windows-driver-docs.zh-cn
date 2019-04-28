---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOSTABILIZATION
description: 此扩展的属性控件用来控制驱动程序中的数字视频防抖动\\MFT0。
ms.assetid: 60F7D1B2-02F1-459A-8F6A-FC61D65705E1
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOSTABILIZATION 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOSTABILIZATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: e9564f4d5bf27437b18ca386db43b636618b83df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341877"
---
# <a name="kspropertycameracontrolextendedvideostabilization"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOSTABILIZATION

此扩展的属性控件用来控制驱动程序中的数字视频防抖动\\MFT0。

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

以下标志可以放入 KSCAMERA\_EXTENDEDPROP\_标头。标志字段标志来控制驱动程序中的数字视频防抖动\\MFT0。 默认情况下，该驱动程序应具有视频防抖动。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_OFF       0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_ON        0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_AUTO      0x0000000000000002
```

如果该驱动程序不支持数字视频防抖动，驱动程序不应实现此控件。

如果该驱动程序支持此控件，它必须支持 VIDEOSTABILIZATION\_ON\\OFF。

此控件的组调用不起作用时视频的 pin 处于任何状态高于 KSSTATE\_停止状态。 该驱动程序应拒绝集呼叫情况视频 pin 未处于停止状态，并返回状态下，接收\_无效\_设备\_状态。 在 GET 调用中，驱动程序应返回 Flags 字段中的当前设置。

在配置文件的上下文中使用此控件时，该配置文件应作为对质量模式的驱动程序的提示。 该驱动程序可以确定是否以优化为较低的延迟或高质量视频防抖动开启时根据的配置文件选择，例如，视频会议或高质量视频录制。

> [!NOTE]
> PROPSETID\_VIDCAP\_CAMERACONTROL\_视频\_稳定将不推荐使用适用于 Windows 10。

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
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_OFF</p></td>
<td><p>这是必需的功能。 如果指定，数字视频防抖动 driver\MFT0 中禁用。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_ON</p></td>
<td><p>这是必需的功能。 如果指定，在 driver\MFT0 中启用数字视频防抖动并填充设置默认自定大小是由驱动程序。 此标志是互斥独占使用的自动和关闭标志。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_AUTO</p></td>
<td><p>此功能是可选的。 如果指定，支持此类功能的驱动程序将确定是否应执行视频防抖动多少稳定应用场景分析及捕获方案。 此标志为 ON 和 OFF 标志与互斥。</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> 具体取决于实现，overscanned 的缓冲区可能是由驱动程序在内部或分配管道。

如果 overscanned 的缓冲区，并将其分配由驱动程序的常规媒体类型和 overscanned 的媒体类型都应播发驱动程序。 MFT0 应该播发的常规媒体类型。 MFT0 应后设置 MFT0 的输出媒体类型中的正则媒体类型，选择相应的 overscanned 的媒体从驱动程序的类型作为其输入的媒体类型，播发的媒体类型，如果视频防抖动开启。 如果视频防抖动处于关闭状态，MFT0 应选择常规媒体类型作为其输入的媒体类型。 MFT0 应返回 MF\_E\_视频防抖动开启时，INVALIDMEDIATYPE 如果 overscanned 的媒体类型设置为其输出媒体类型。

如果驱动程序分配 overscanned 的缓冲区，驱动程序和 MFT0 应该播发的常规媒体类型。 MFT0 应定期媒体类型设置的这两个输入的媒体类型和输出媒体类型。

若要支持基于效果视频防抖动 （即，视频防抖动完成驱动程序中既 MFT0 中），驱动程序和 MFT0 此外必须播发无论 overscanned 的媒体类型。 在这种情况下，由驱动程序和 MFT0 公开这两种常规和 overscanned 媒体类型。 将应用以下规则以确保基于影响和驱动程序\\MFT0 基于视频防抖动是否正常工作。

-   如果 overscanned 的媒体类型设置为 MFT0 输出媒体类型时驱动程序\\MFT0 基于视频防抖动上，MFT0 应返回 MF\_E\_INVALIDMEDIATYPE。

-   如果正则媒体类型设置为 MFT0 输出媒体类型，该应用程序应返回开启效果的尝试中出现错误基于视频防抖动，如果基于效果视频防抖动只能采用 overscanned 的媒体类型。

下表包含的说明和要求[KSCAMERA\_EXTENDEDPROP\_标头](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段，使用视频防抖动控件时。

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
<td><p>必须将 Pin 与关联的 ID 视频的 pin。</p></td>
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
<td><p>如上文所定义，这必须是受支持的 KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_XXX 标志的按位 OR。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是上面定义的 KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_XXX 任何的标志一个。</p></td>
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
