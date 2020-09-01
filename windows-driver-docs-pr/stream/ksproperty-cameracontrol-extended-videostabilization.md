---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ VIDEOSTABILIZATION
description: 此扩展属性控件用于控制驱动程序 MFT0 中的数字视频稳定 \\ 。
ms.assetid: 60F7D1B2-02F1-459A-8F6A-FC61D65705E1
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOSTABILIZATION 流媒体设备
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
ms.openlocfilehash: b6f72f83180832a6a3730994bbb7da4b1ad1348a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188747"
---
# <a name="ksproperty_cameracontrol_extended_videostabilization"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ VIDEOSTABILIZATION

此扩展属性控件用于控制驱动程序 MFT0 中的数字视频稳定 \\ 。

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

可放置在 KSCAMERA \_ EXTENDEDPROP 标头中的以下标志 \_ 。标志字段标志以控制驱动程序 MFT0 中的数字视频稳定 \\ 。 默认情况下，驱动程序应关闭视频抖动。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_OFF       0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_ON        0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_AUTO      0x0000000000000002
```

如果驱动程序不支持数字视频防抖动，驱动程序不应实现此控制。

如果驱动程序支持此控件，则它必须支持 VIDEOSTABILIZATION \_ ON \\ OFF。

当视频 pin 处于任何高于 KSSTATE 停止状态的状态时，对此控件的设置调用不起作用 \_ 。 如果视频 pin 未处于停止状态并且返回状态 " \_ 无效设备状态"，则驱动程序应拒绝收到的设置呼叫 \_ \_ 。 在 GET 调用中，驱动程序应返回 "标志" 字段中的当前设置。

如果在配置文件的上下文中使用此控件，则该配置文件应充当质量模式的驱动程序提示。 此驱动程序可以根据所选的配置文件（例如，视频会议或高质量的视频录制），确定是根据所选的配置文件优化低延迟还是高质量。

> [!NOTE]
> \_ \_ \_ \_ 适用于 Windows 10 的 PROPSETID VIDCAP CAMERACONTROL 视频稳定性将会弃用。

下表介绍了标志功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>标志</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_OFF</p></td>
<td><p>这是必需的功能。 指定时，driver\MFT0. 中禁用数字视频抖动</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_ON</p></td>
<td><p>这是必需的功能。 指定时，将在 driver\MFT0 中启用数字视频抖动，并在驱动程序中设置默认的 overscan 填充设置。 此标志与自动和关闭标志互斥。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_AUTO</p></td>
<td><p>此功能是可选的。 如果指定此功能，则支持此类功能的驱动程序将确定是否应执行视频稳定性，并根据场景分析和捕获方案来确定要应用的稳定性。 此标志与 ON 和 OFF 标志互相排斥。</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> 根据实现，overscanned 缓冲区可能由驱动程序在内部或管道中分配。

如果驱动程序要分配 overscanned 缓冲区，驱动程序应同时播发常规媒体类型和 overscanned 媒体类型。 MFT0 应公布常规媒体类型。 在 MFT0 的输出媒体类型上设置常规媒体类型时，如果打开了视频稳定，则 MFT0 应从驱动程序将媒体类型作为其输入媒体类型来选择相应的 overscanned 媒体类型。 如果视频稳定处于关闭状态，则 MFT0 应选择常规媒体类型作为其输入媒体类型。 \_ \_ 如果在视频稳定打开时将 overscanned 媒体类型设置为其输出媒体类型，则 MFT0 应返回 MF E INVALIDMEDIATYPE。

如果 overscanned 缓冲区由驱动程序分配，则驱动程序和 MFT0 都应公布常规媒体类型。 MFT0 应为其输入媒体类型和输出媒体类型设置常规媒体类型。

为了支持基于视频抖动 (的效果，视频抖动在驱动程序和 MFT0) 中都没有完成，驱动程序和 MFT0 还必须公布 overscanned 媒体类型，而不考虑。 在这种情况下，驱动程序和 MFT0 都公开了 regular 和 overscanned 媒体类型。 以下规则将适用，以确保基于效果的和基于驱动程序 \\ MFT0 的视频抖动都能正常工作。

-   如果 overscanned 媒体类型设置为 MFT0 输出媒体类型，而基于驱动程序 \\ MFT0 的视频抖动处于开启，则 MFT0 应返回 MF \_ E \_ INVALIDMEDIATYPE。

-   如果将常规媒体类型设置为 "MFT0 output media type"，则应用程序应返回一个错误，该错误在基于视频稳定性的情况下尝试启用基于视频抖动的效果时，可能只需要 overscanned 媒体类型。

下表包含在使用视频抖动控制时 [KSCAMERA \_ EXTENDEDPROP \_ 标头](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构字段的说明和要求。

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
<td><p>必须是与视频 pin 关联的 Pin ID。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) 。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是前面定义的受支持 KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_XXX 标志的按位 "或"。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的 KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_XXX 标志之一。</p></td>
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