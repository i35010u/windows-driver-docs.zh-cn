---
title: 'KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ OPTIMIZATIONHINT (扩展硬件优化) '
description: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ OPTIMIZATIONHINT 用于控制照片捕获与视频捕获的主要用例。 在 Windows 10 中，此控制已扩展为支持扩展的硬件优化提示。
ms.assetid: 1E2787B7-4BC2-4FBC-8909-ACB122B87F08
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 3d013228a95a30a47af7c2725ee7bd2797a203af
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190519"
---
# <a name="ksproperty_cameracontrol_extended_optimizationhint-expanded-hardware-optimization"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ OPTIMIZATIONHINT (扩展硬件优化) 

KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ OPTIMIZATIONHINT 用于控制照片捕获与视频捕获的主要用例。 在 Windows 10 中，此控制已扩展为支持扩展的硬件优化提示。

## <a name="usage-summary-table"></a>使用情况摘要表

| 作用域 | 控制 | 类型 |
|--|--|--|
| 版本 1 | 筛选器 | 同步 |

以下标志可以放置在 KSCAMERA \_ EXTENDEDPROP \_ 标头中。将字段标记为驱动程序中的硬件优化提示。

```cpp
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_DEFAULT      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_PHOTO        0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_VIDEO        0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_QUALITY      0x0000000000000004
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_LATENCY      0x0000000000000008
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_POWER        0x0000000000000010
```

将继续使用照片和视频提示来指定主用例。

对于 Windows 10，附加的位标志有助于驱动程序中质量、速度和功率消耗的折衷。 默认情况下，驱动程序应具有 KSCAMERA \_ EXTENDEDPROP \_ 优化 \_ 照片。

如果驱动程序支持此控件，则它必须支持 KSCAMERA \_ EXTENDEDPROP \_ 优化 \_ 照片和 KSCAMERA \_ EXTENDEDPROP \_ 优化 \_ 视频。

如果驱动程序不支持优化提示，驱动程序不应实现此控制。

下表介绍了标志功能。

| 标志 | 描述 |
|--|--|
| KSCAMERA_EXTENDEDPROP_OPTIMIZATION_DEFAULT | 这是必需的功能。 指定该驱动程序时，驱动程序应清除前面对驱动程序设置的提示，并应用驱动程序的默认电源、质量和延迟折衷。 |
| KSCAMERA_EXTENDEDPROP_OPTIMIZATION_PHOTO | 这是必需的功能。 当指定时，主要用例是照片捕获，驱动程序应优先处理视频录制的照片捕获。 当预览 pin 处于停止状态时，可以指定此标志，以选择传感器模式以支持照片质量，或仅在视频录制过程中以 "正在运行" 状态进行照片捕获。 当在视频录制过程中为照片捕获指定时，视频流中的故障可接受更好的照片质量。 此标志与视频标志互斥，并可与任何一个或两个质量、延迟和电源标志一起使用。 |
| KSCAMERA_EXTENDEDPROP_OPTIMIZATION_VIDEO | 这是必需的功能。 当指定时，主要用例是视频捕获，驱动程序应通过照片捕获来确定视频录制的优先级。 当预览 pin 处于停止状态时，可以指定此标志，以选择传感器模式来支持视频录制，或仅在视频录制过程中以 "正在运行" 状态进行照片捕获。 如果在视频录制过程中为照片捕获指定了，则不允许视频流中出现故障。 此标志与照片标志互斥，并可与任何一个或两个质量、延迟和电源标志一起使用。 |
| KSCAMERA_EXTENDEDPROP_OPTIMIZATION_QUALITY | 此功能是可选的。 指定时，驱动程序应为照片捕获优化图像质量，并为视频录制优化视频质量。 此标志可在照片捕获 (包括常规照片、VPS 和 PS 之前指定，无需) 和/或视频录制开始，或者当 pin 处于停止状态。 此标志可与照片标志一起使用，也可与视频标志一起使用延迟或电源标志。 |
| KSCAMERA_EXTENDEDPROP_OPTIMIZATION_LATENCY | 此功能是可选的。 指定时，驱动程序应为照片捕获和视频录制优化速度和延迟时间。 此标志可在照片捕获 (包括常规照片、VPS 和 PS 之前指定，) 和/或视频录制开始或 pin 处于停止状态。 此标志可与照片标志一起使用，也可与视频标志一起使用。 |
| KSCAMERA_EXTENDEDPROP_OPTIMIZATION_POWER | 此功能是可选的。 指定时，驱动程序应为照片捕获和视频录制优化功率消耗。 此标志可在拍照捕获之前指定 (包括常规照片、VPS 和 PS，无需历史记录) 和/或视频录制开始，或当 pin 处于停止状态。 此标志可与视频标志一起用于质量或延迟标志。 |

下表包含使用控件时 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构字段的说明和要求。

| 成员 | Value |
|--|--|
| 版本 | 1 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)  |
| 大小 | sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE)  |
| 结果 | 指示上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。 |
| 功能 | 必须是前面定义的受支持 KSCAMERA_EXTENDEDPROP_OPTIMIZATION_ * 标志的按位 "或"。 |
| Flags | 这是一个读/写字段。 这可以是上面定义的受支持 KSCAMERA_EXTENDEDPROP_OPTIMIZATION_ * 标志的任何有效组合。 |

## <a name="remarks"></a>备注

使用优化提示时，请注意以下事项：

- 质量/延迟/电源和照片/视频是两组独立提示。 可以同时指定它们，也可以在不同的时间单独指定。 设置质量/延迟/电源不会覆盖照片/视频，反之亦然。 当在不同时间指定时，驱动程序应在 GET 调用中返回这两组提示的当前设置。

- 对于质量/延迟/电源，当设置提示时，驱动程序应在其约束内优化。 如果没有可用优化，驱动程序应忽略提示。

- 如果同时为视频用例指定了两个提示，则每个提示的优化可能低于仅指定了一个提示时的时间。 更具体说来：

  - 如果同时指定了质量或功率，延迟将优先于质量或功率。 在这种情况下，质量可能低于仅指定了质量时的质量，并且功率消耗可能高于仅指定了电源的情况。

  - 如果同时指定了质量和能力，则质量可能低于仅指定了质量时的质量，并且功率消耗可能高于仅指定了电源的情况。

- 优化提示仅作为对驱动程序的提示，以便在应用程序指定的捕获方案的约束范围内提供对3A、ISP 处理、传感器选择等的处理折衷。 为了获得最佳结果，应用程序开发人员必须为特定的捕获方案选择和配置最合适的控件和 Api。 否则，单独的优化提示可能会产生降低的效果。 例如，对于高质量的照片捕获，应在某些 IHV 平台上使用 VPS 或 LowLagPhoto/TakePhoto 代替 PS 来使用质量提示。 同样，如果需要较低的延迟或功率消耗，应禁用视频稳定。

- 如果在每个功能标志下除指定的时间之外接收，将忽略优化提示。

当驱动程序上同时启用视频稳定控制时 (或自动) ：

- 该驱动程序可能会应用最低的最小视频抖动，其中包括低延迟和/或低功率视频抖动算法，以减少处理延迟和/或设置的延迟和/或电源提示。 当视频抖动设置为 AUTO 时，驱动程序可能会关闭视频稳定，以进一步降低延迟和/或功率消耗。

- 如果设置了质量提示，驱动程序可能会应用最高的高质量视频抖动来改善视频质量。

## <a name="requirements"></a>要求

**标头：** Ksmedia (包含 Ksmedia) 