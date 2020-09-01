---
title: 'KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE (ISP 控制参数) '
description: '\_ \_ \_ KSPROPERTY CAMERACONTROL 扩展属性枚举中定义的 KSPROPERTY CAMERACONTROL 扩展 SCENEMODE 属性 ID 为 \_ \_ \_ oem 提供了一些功能，可根据需要调整场景模式以及任何其他 ISP 控制参数。'
ms.assetid: CB3F89AD-4B53-4E47-B60E-4B584DB8418B
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: b7aff544212985e2236096877996bc5b5120286d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191423"
---
# <a name="ksproperty_cameracontrol_extended_scenemode-isp-control-parameters"></a>KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE (ISP 控制参数) 

[**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 属性**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举中定义的**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ SCENEMODE**属性 ID 为 oem 提供了一些功能，可根据需要调整场景模式以及任何其他 ISP 控制参数。

## <a name="usage-summary-table"></a>使用情况摘要表

| 作用域 | 控制 | 类型 |
|--|--|--|
| 版本 1 | 筛选器 | 异步 |

在某些情况下，场景模式用作指导照相机系统优化其操作的提示。 场景模式和其他 ISP 控制（如白平衡、ISO、曝光时间和 EV 补偿）必须能够独立工作，而不会相互影响。

- 更改任何其他 ISP 控制参数不得更改现有场景模式。 修改其他 ISP 参数之后，驱动程序不需要将场景模式改为手动。

- 设置自动场景模式不得更改任何其他 ISP 控件的现有设置。 对于任何其他 ISP 控件，驱动程序无需恢复为完全自动模式。

**KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 自动**

此标志指示自动场景模式。 照相机驱动程序将根据场景自动确定最佳场景模式设置，并根据场景的需要优化各种 ISP 设置。

**KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_**

此标志不适用。

**KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 宏 \\ 纵向 \\ 运动 \\ 雪 \\ 夜 \\ 沙滩 \\ 日落 \\ CANDLELIGHT \\ 横向 \\ NIGHTPORTRAIT \\ BACKLIT**

这些标志指示相应的场景模式（如定义）。 照相机驱动程序将使用指定为提示的场景模式来根据需要优化各种 ISP 设置 (例如，对于晚间，ISP 设置针对夜间环境) 进行了优化。

下表包含使用**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE**属性时[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的说明和要求。 对于**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE**，将忽略[**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。

| 成员 | Value |
|--|--|
| 版本 | 1 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)  |
| 大小 | sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE)  |
| 结果 | 这指示上次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。 值0指示未检测到任何错误。 |
| 功能 | 这必须是 **KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL** 的按位 "或"，以及以上定义的任何受支持场景模式。 如果照相机驱动程序支持此控件，则必须支持**KSCAMERA_EXTENDEDPROP_SCENEMODE_AUTO** 。 |
| Flags | 这可以是上面所示的任何受支持场景模式。 |

## <a name="requirements"></a>要求

**标头：** Ksmedia (包含 Ksmedia) 