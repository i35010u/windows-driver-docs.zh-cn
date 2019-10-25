---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOTEMPORALDENOISING
description: KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOTEMPORALDENOISING 用于控制驱动程序上的视频时态 Denoising。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOTEMPORALDENOISING 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOTEMPORALDENOISING
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 04/03/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 33321a84ffccf3d78e597be7e364e66fa72cd302
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837850"
---
# <a name="ksproperty_cameracontrol_extended_videotemporaldenoising"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOTEMPORALDENOISING

KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOTEMPORALDENOISING 用于控制驱动程序上的视频时态 Denoising。

## <a name="overview"></a>概述

当在不理想的情况下操作照相机系统时，图像信号处理器（ISP）的3A 统计逻辑将趋向于提高模拟和数字增益，以提高照相机系统的 photons，以弥补缺少的问题传感器处于设定的捕获帧速率。 这会产生放大的副作用，这会增加传感器生成的帧中的明显干扰。 即使已通过 ISP 管道进行处理，这仍可能会很明显。

除了使用色度和亮度 aberrations 改变场景的图像外，由于此截图干扰的随机特性，在视频（预览或录制）中，时态 incoherence 的像素值非常明显，并可能导致用户的体验不佳。

视频时态 Denoising （VTD）的目的是通过对多个帧中的信息进行累积和组合，并在帧延迟的时间约束的上下文中生成一个更清晰的输出帧，来解决干扰，并减少干扰性像素的时态 incoherence。例如，使用视频源。

这一额外的处理旨在以非常短的延迟时间执行，从而提高图像质量，而不会阻止用户正常操作相机，无需任何后处理步骤。

## <a name="usage-summary-table"></a>使用情况摘要表

| 范围 | 控件 | 在任务栏的搜索框中键入 |
| --- | --- | --- |
| 版本 1 | Filter | 同步 |

下面是可以放置在 KSCAMERA\_EXTENDEDPROP\_标头中的标志。用于控制驱动程序上视频时态 Denoising 的标志字段。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO   0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF    0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON     0x0000000000000004
```

如果驱动程序支持此控件，则它必须至少支持 VIDEOTEMPORALDENOISING_AUTO 或 VIDEOTEMPORALDENOISING_ON 和 VIDEOTEMPORALDENOISING_OFF。

如果驱动程序不支持视频时态 Denoising，则驱动程序不应实现此控制。

这是一个同步控件，可在从所有支持的 pin 进行流式处理时动态控制。  

下表介绍了标志功能。

| 旗帜 | 描述 |
| --- | --- |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO | 如果不支持 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF 和 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON，则这是必需的功能。 指定时，视频时态 Denoising 会自动在驱动程序中启用或禁用，并影响可见光线范围内的所有支持的 pin 流式处理像素。 虽然这并不保证始终能处理帧，但这意味着，如果通过 ISP 传递视频信号，则可能会在实施者的 discretions 上发生这种情况。 |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF | 如果 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO 不受支持，则这是必需的功能，如果是，则是可选的。 如果指定此项，则会在驱动程序中同时禁用视频时态 Denoising，以用于可见光线范围内的所有支持的 pin 流式处理像素。 |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON | 如果 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO 不受支持，则这是必需的功能，如果是，则是可选的。 如果指定此项，则会在驱动程序中为可见光线范围内的所有支持的 pin 流式处理像素同时启用视频时态 Denoising。 |

下表包含使用控件时[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的说明和要求。

| 成员 | 描述 |
| --- | --- |
| 版本 | 必须为1。 |
| PinId | 必须是 KSCAMERA_EXTENDEDPROP_FILTERSCOPE （0xFFFFFFFF）。 |
| Size | 必须为 sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VALUE）。 |
| 结果 | 指示上一次设置操作的错误结果。  如果未执行任何设置操作，则此必须为0。 |
| 功能 | 必须是前面定义的受支持的 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ * 标志的按位 "或"。 |
| Flags | 这是一个读/写字段。  这必须是上面定义的 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_XXX 标志之一。 请注意，这些标志是互斥的，不能用任何按位 "或" 组合来设置。 |

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
