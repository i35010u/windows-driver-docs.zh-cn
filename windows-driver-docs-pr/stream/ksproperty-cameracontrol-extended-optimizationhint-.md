---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_OPTIMIZATIONHINT
description: KSPROPERTY\_CAMERACONTROL\_扩展\_OPTIMIZATIONHINT 用于控制与视频捕获照片拍摄的主要用例。 在 Windows 10 中，此控件已扩展为支持扩展的硬件优化提示。
ms.assetid: 1E2787B7-4BC2-4FBC-8909-ACB122B87F08
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: c50d0281f1136be2d273ebc736f1b35b305a87f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569397"
---
# <a name="kspropertycameracontrolextendedoptimizationhint"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_OPTIMIZATIONHINT

KSPROPERTY\_CAMERACONTROL\_扩展\_OPTIMIZATIONHINT 用于控制与视频捕获照片拍摄的主要用例。 在 Windows 10 中，此控件已扩展为支持扩展的硬件优化提示。

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
<td><p>Filter</p></td>
<td><p>同步</p></td>
</tr>
</tbody>
</table>

以下标志可放置在 KSCAMERA\_EXTENDEDPROP\_标头。标记对驱动程序中的硬件优化提示的字段。

将照片和视频提示将继续使用指定的主要用例。

适用于 Windows 10，其他位标志帮助的质量、 速度和驱动程序中的电源消耗的权衡。 默认情况下，该驱动程序应具有 KSCAMERA\_EXTENDEDPROP\_优化\_照片。

```cpp
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_DEFAULT      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_PHOTO        0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_VIDEO        0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_QUALITY      0x0000000000000004
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_LATENCY      0x0000000000000008
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_POWER        0x0000000000000010
```

f 驱动程序支持此控件，则它必须支持 KSCAMERA\_EXTENDEDPROP\_优化\_照片和 KSCAMERA\_EXTENDEDPROP\_优化\_视频。

如果该驱动程序不支持的优化提示，该驱动程序不应实现此控件。

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
<td><p>KSCAMERA_EXTENDEDPROP_OPTIMIZATION_DEFAULT</p></td>
<td><p>这是必需的功能。 指定时，该驱动程序应清除以前的提示驱动程序上设置并应用驱动程序的默认的电源、 质量、 滞后时间权衡。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_OPTIMIZATION_PHOTO</p></td>
<td><p>这是必需的功能。 指定时，主要用例是照片拍摄和驱动程序应优先照片拍摄于视频录制。 预览针期间仅录制视频为处于停止状态选择照片质量为支持的传感器模式或在照片拍摄的运行状态时，可以指定此标志。 视频录制过程中指定照片拍摄的在视频流故障时，为了更好的照片质量支持可接受。 此标志与视频标志互斥，并可与任何一个或两个的质量、 延迟和电源的标志。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_OPTIMIZATION_VIDEO</p></td>
<td><p>这是必需的功能。 指定时，主要用例是视频捕获和驱动程序应确定视频录制对照片拍摄的优先级。 预览针期间仅录制视频为处于停止状态，若要选择一个传感器模式以支持视频录制，或在照片拍摄的运行状态时，可以指定此标志。 指定时照片拍摄的视频录制期间，不允许在视频流中的故障。 此标志与照片标志互斥，并可与任何一个或两个的质量、 延迟和电源的标志。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_OPTIMIZATION_QUALITY</p></td>
<td><p>此功能是可选的。 如果指定，该驱动程序应优化照片拍摄的图像质量和视频录制的视频质量。 之前的照片拍摄 （没有历史记录框架，包括正则照片、 VPS 和 PS） 和/或视频录制将启动，或 pin 处于停止状态时，可以指定此标志。 可以使用此标志，照片标志或延迟或电源以及视频标志的标志。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_OPTIMIZATION_LATENCY</p></td>
<td><p>此功能是可选的。 指定时，该驱动程序应优化的速度和照片拍摄和视频录像所造成的延迟。 可以在照片拍摄 （没有历史记录框架，包括正则照片、 VPS 和 PS） 之前指定此标志和/或视频录制将启动，或 pin 时处于停止状态。 可以使用此标志，照片标志，或与质量或电源以及视频标志的标志。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_OPTIMIZATION_POWER</p></td>
<td><p>此功能是可选的。 如果指定，该驱动程序应优化为照片拍摄和视频录制的功率消耗。 之前的照片拍摄 （无历史记录，包括正则照片、 VPS 和 PS） 和/或视频录制将启动，或 pin 处于停止状态时，可以指定此标志。 此标志可以用于质量或延迟标志，以及视频标志。</p></td>
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
<td><p>版本</p></td>
<td><p>这必须是 1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>必须是 KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)。</p></td>
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
<td><p>必须是支持 KSCAMERA_EXTENDEDPROP_OPTIMIZATION_ * 标志上面定义的按位 OR。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是读/写字段。 这可以是任何有效的受支持 KSCAMERA_EXTENDEDPROP_OPTIMIZATION_ * 标志上面定义的组合。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>备注

使用优化提示时，请记住以下各项：

-   质量/延迟/电源和照片/视频是两个独立的提示集。 它们可以同时或单独在不同的时间一起指定。 设置质量/延迟/电源不会覆盖照片/视频，反之亦然。 当指定为在不同的时间，则驱动程序应 GET 调用中返回提示这两个集的当前设置。

-   获得质量/延迟/功能，当设置提示时，驱动程序应优化其约束内。 如果不进行优化可用，则驱动程序应忽略提示。

-   当视频的用例同时指定两个提示时，每个提示的优化可能小于指定了仅提示。 特别需要注意的是：

    -   如果同时指定质量或电源，则延迟优先于质量或电源。 在这种情况下，质量可能小于指定唯一的质量，并可能高于时指定唯一的电源的功率消耗时。

    -   当指定了质量和电源时，质量可能小于指定唯一的质量，并可能高于时指定唯一的电源的功率消耗时。

-   优化提示仅提供作为对驱动程序以便 3A，ISP 处理，传感器所选内容，等等，应用程序指定的捕获方案的约束内处理的权衡取舍的提示。 它对于应用程序开发人员选择并配置最适合的控件和 Api，可用于捕获特定方案，以便获得最佳结果至关重要。 否则，单独的优化提示可能会带来降低的影响。 例如，应使用高质量照片拍摄，VPS 或 LowLagPhoto/TakePhoto 改为 PS 为了充分利用质量某些 IHV 平台上的提示。 同样，如果需要更低的延迟或电源消耗，则应禁用视频防抖动。

-   如果收到在时间/状态在每个功能标志下指定的内容以外，应忽略的优化提示。

视频防抖动控件还启用时驱动程序 （ON 或 AUTO）：

-   该驱动程序可能会收取最低积极视频防抖动包括较低的延迟和/或低能耗视频防抖动算法来减少处理延迟和/或电源消耗如果滞后时间和/或 POWER 提示设置。 当视频防抖动设置为自动时，该驱动程序可能会关闭视频防抖动以进一步降低延迟和/或电源消耗。

-   该驱动程序可能会收取最高积极的视频防抖动时质量提示设置提高视频质量。


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
