---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOTEMPORALDENOISING
description: KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOTEMPORALDENOISING 用于对驱动程序的 control 权限视频临时噪声抑制。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOTEMPORALDENOISING 流式处理媒体设备
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
ms.openlocfilehash: 2da1efe08dab339ed6e58d5f0a913685794e0638
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341844"
---
# <a name="kspropertycameracontrolextendedvideotemporaldenoising"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOTEMPORALDENOISING

KSPROPERTY\_CAMERACONTROL\_扩展\_VIDEOTEMPORALDENOISING 用于对驱动程序的 control 权限视频临时噪声抑制。

## <a name="overview"></a>概述

非最优光条件中的照相机系统时，图像信号处理器 (ISP) 中的 3A 统计逻辑将往往会增加模拟和数字提高增加的照相机系统，以弥补 photons 达到缺乏浅敏感性在施加的捕获帧速率的传感器。 这具有副作用的放大单次触发干扰，这会增加生成的传感器的帧中的感知的干扰。 这仍然可以明显甚至通过 ISP 管道处理完之后。

除了更改与色度和亮度异常，由于此单次触发干扰的随机特性场景图像的像素值的临时 incoherence 时尤其明显在视频中 （预览或记录），并可能会导致非常糟糕的用户的体验。

视频临时噪声抑制 (VTD) 的目的是解决干扰并且减少累积并合并来自多个帧，以生成更简洁的输出帧时间约束的上下文中的信息的干扰性像素的临时 incoherence 其中帧延迟如使用视频源的相关问题。

这种额外处理是指以实时的方式使用非常小的延迟，以提高图像质量，而不会阻止用户不能正常工作照相机和而无需任何后续处理步骤执行。

## <a name="usage-summary-table"></a>使用率摘要表

| 范围 | 控件 | 在任务栏的搜索框中键入 |
| --- | --- | --- |
| 版本 1 | Filter | 同步 |

以下是标志，它们可以位于 KSCAMERA\_EXTENDEDPROP\_标头。标记字段以控制视频临时噪声抑制该驱动程序。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO   0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF    0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON     0x0000000000000004
```

如果该驱动程序支持此控件，它必须至少支持是 VIDEOTEMPORALDENOISING_AUTO 或同时 VIDEOTEMPORALDENOISING_ON 和 VIDEOTEMPORALDENOISING_OFF。

如果该驱动程序不支持视频临时噪声抑制，驱动程序不应实现此控件。

这是可以在所有受支持的插针从流式处理动态控制同步控件。  

下表介绍标志功能。

| Flag | 描述 |
| --- | --- |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO | 如果不支持 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF 和 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON，这是必需的功能。 指定时，视频临时噪声抑制是自动启用或禁用所有驱动程序和流式处理中的可见范围的浅的像素的会影响所有支持 pin。 虽然这不为在所有时间的帧的实际处理提供保证，这意味着，可能需要在实施者的 discretions 给定通过 ISP 的视频信号。 |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF | 如果 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO 不支持的和可选的如果是，这是必需的功能。 指定时，视频临时噪声抑制中禁用该驱动程序在所有时为所有受支持的插针流式处理中的可见范围的浅的像素。 |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON | 如果 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO 不支持的和可选的如果是，这是必需的功能。 指定时，视频临时噪声抑制中启用了该驱动程序在所有时为所有受支持的插针流式处理中的可见范围的浅的像素。 |

下表包含的说明和要求[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段时使用的控件。

| 成员 | 描述 |
| --- | --- |
| Version | 必须为 1。 |
| PinId | 必须是 KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)。 |
| 大小 | 必须是 sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE)。 |
| 结果 | 指示最后一个设置操作的错误结果。  如果未设置操作发生，这必须为 0。 |
| 功能 | 必须是支持 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ * 标志上面定义的按位 OR。 |
| Flags | 这是读/写字段。  这必须是上面定义的 KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_XXX 标志之一。 请注意，这些标志是互斥的并且不能在任何按位 OR 组合设置。 |

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
