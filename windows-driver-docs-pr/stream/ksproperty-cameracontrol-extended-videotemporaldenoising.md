---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ VIDEOTEMPORALDENOISING
description: KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ VIDEOTEMPORALDENOISING 用于控制驱动程序上的视频时态 Denoising。
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
ms.openlocfilehash: 02adafded8616aa5852f2e6d6946af5f462589f7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187373"
---
# <a name="ksproperty_cameracontrol_extended_videotemporaldenoising"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ VIDEOTEMPORALDENOISING

KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ VIDEOTEMPORALDENOISING 用于控制驱动程序上的视频时态 Denoising。

## <a name="overview"></a>概述

当在不适合的情况下操作照相机系统时，图像信号处理器 (ISP) 中的3A 统计逻辑将趋向于增加模拟和数字增益，以提高照相机系统的 photons，以弥补在施加的捕获帧速率下缺乏传感器的情况。 这会产生放大的副作用，这会增加传感器生成的帧中的明显干扰。 即使已通过 ISP 管道进行处理，这仍可能会很明显。

除了使用色度和亮度 aberrations 改变场景的图像外，由于此截图干扰的随机特性，) 在视频 (预览或记录中的的临时 incoherence，并可能会导致用户体验不佳。

视频时态 Denoising (VTD) 的目的是通过在帧延迟（如使用视频源）的情况下，通过累积并组合多个帧中的信息来解决干扰性像素并降低时态 incoherence。

这一额外的处理旨在以非常短的延迟时间执行，从而提高图像质量，而不会阻止用户正常操作相机，无需任何后处理步骤。

## <a name="usage-summary-table"></a>使用情况摘要表

| 范围 | 控制 | 类型 |
| --- | --- | --- |
| 版本 1 | 筛选器 | 同步 |

下面是可放置在 KSCAMERA \_ EXTENDEDPROP 标头中的标志 \_ 。用于控制驱动程序上视频时态 Denoising 的标志字段。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO   0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF    0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON     0x0000000000000004
```

如果驱动程序支持此控件，则它必须至少支持 VIDEOTEMPORALDENOISING_AUTO 或 VIDEOTEMPORALDENOISING_ON 和 VIDEOTEMPORALDENOISING_OFF。

如果驱动程序不支持视频时态 Denoising，则驱动程序不应实现此控制。

这是一个同步控件，可在从所有支持的 pin 进行流式处理时动态控制。  

下表介绍了标志功能。

| 标志 | 描述 |
| --- | --- |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO | 如果 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF 和 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON 不受支持，则这是必需的功能。 指定时，视频时态 Denoising 会自动在驱动程序中启用或禁用，并影响可见光线范围内的所有支持的 pin 流式处理像素。 虽然这并不保证始终能处理帧，但这意味着，如果通过 ISP 传递视频信号，则可能会在实施者的 discretions 上发生这种情况。 |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF | 如果 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO 不受支持，则这是必需的功能，如果是，则是可选的。 如果指定此项，则会在驱动程序中同时禁用视频时态 Denoising，以用于可见光线范围内的所有支持的 pin 流式处理像素。 |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON | 如果 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO 不受支持，则这是必需的功能，如果是，则是可选的。 如果指定此项，则会在驱动程序中为可见光线范围内的所有支持的 pin 流式处理像素同时启用视频时态 Denoising。 |

下表包含使用控件时 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构字段的说明和要求。

| 成员 | 说明 |
| --- | --- |
| 版本 | 必须为 1。 |
| PinId | 必须 (0xFFFFFFFF) KSCAMERA_EXTENDEDPROP_FILTERSCOPE。 |
| 大小 | 必须是 sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE ) 。 |
| 结果 | 指示上一次设置操作的错误结果。  如果未执行任何设置操作，则此必须为0。 |
| 功能 | 必须是前面定义的受支持 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ * 标志的按位 "或"。 |
| Flags | 这是一个读/写字段。  这必须是上面定义的 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_XXX 标志之一。 请注意，这些标志是互斥的，不能用任何按位 "或" 组合来设置。 |

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