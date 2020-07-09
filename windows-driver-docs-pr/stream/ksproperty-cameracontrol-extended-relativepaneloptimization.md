---
title: KSPROPERTY_CAMERACONTROL_EXTENDED_RELATIVEPANELOPTIMIZATION
description: KSPROPERTY_CAMERACONTROL_EXTENDED_RELATIVEPANELOPTIMIZATION 是一种属性 ID，用于通知驱动程序相对于应用程序的活动显示，照相机是否正面朝上。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_RELATIVEPANELOPTIMIZATION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_RELATIVEPANELOPTIMIZATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/07/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: e52042089d4ca186758016a0cec77c04366e8fba
ms.sourcegitcommit: ff2f72fe98f6ba559c1c01b17d25c773df7337c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86060858"
---
# <a name="ksproperty_cameracontrol_extended_relativepaneloptimization"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ RELATIVEPANELOPTIMIZATION

**KSPROPERTY \_CAMERACONTROL \_ EXTENDED \_ RELATIVEPANELOPTIMIZATION**是一种属性 ID，用于通知驱动程序是否正面朝上（相对于应用程序的活动显示）。 设置新的 WinRT API 属性 PanelBasedOptimizationControl 时，Windows 将设置该属性。

有关设置 KSProperty 控件的示例，请参阅 GitHub 上的[AVStream 相机示例驱动程序](https://github.com/microsoft/Windows-driver-samples/tree/master/avstream/avscamera)。

## <a name="usage-summary-table"></a>使用情况摘要表

| 获取 | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|--|--|--|--|--|
| 是 | 是 | 筛选 | [KSPROPERTY](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)) | [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

## <a name="remarks"></a>备注

属性请求包含[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[KSCAMERA_EXTENDEDPROP_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。

属性数据的总大小为 `sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE)` 。

[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

下面是可放置在 KSCAMERA_EXTENDEDPROP_HEADER 中的标志 **。Flags**和**KSCAMERA_EXTENDEDPROP_HEADER。功能**字段。

| 相对面板优化模式 | 说明 |
|--|--|
| KSCAMERA \_ EXTENDEDPROP \_ RELATIVEPANELOPTIMIZATION \_ OFF | 照相机将使用正常的操作模式 |
| KSCAMERA \_ EXTENDEDPROP \_ RELATIVEPANELOPTIMIZATION \_ | 相机将使用与 "值" 字段中所述位置相关的优化 |
| KSCAMERA \_ EXTENDEDPROP \_ RELATIVEPANELOPTIMIZATION \_ DYNAMIC | 在流式处理时，可以动态调整照相机位置提示，而不 glitching 流 |

**KSCAMERA_EXTENDEDPROP_RELATIVEPANELOPTIMIZATION**始终是同步控件。

任何应用程序都可以读取属性，但只有打开了照相机才能进行独占访问的应用才能写入属性值。

如果在没有独占模式访问权限的情况下尝试写入属性，将返回合适的错误代码。

在将此 DDI 映射到 PanelBasedOptimizationControl 的情况下，使用 PanelBasedOptimizationControl 的应用程序将设置 Panel 值，Windows 将在内部使用该值对有效负载的 " [**KSCAMERA_EXTENDEDPROP_VALUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value) " 字段进行编程。

Windows 将控制 "**功能**" 和 "**标志**" 字段。

如果驱动程序在照相机设备正在流式传输时接收到设置操作，并且未设置标志*KSCAMERA \_ EXTENDEDPROP \_ RELATIVEPANELOPTIMIZATION \_ DYNAMIC**，则驱动程序将返回基于状态的错误。

下表包含在使用元数据控件时对[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的要求。

| 成员 | 说明 |
|--|--|
| 版本 | 这必须为1。 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE （0xFFFFFFFF） |
| 大小 | 这必须是 sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VALUE） |
| 结果 | 指示上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。 |
| 功能 | 必须是前面定义的受**支持的** ***KSCAMERA_EXTENDEDPROP_RELATIVEPANELOPTIMIZATION_XXX***标志。 |
| Flags | 这是一个读/写字段。 这可以是**KSCAMERA_EXTENDEDPROP_RELATIVEPANELOPTIMIZATION_ON**或上面定义**KSCAMERA_EXTENDEDPROP_RELATIVEPANELOPTIMIZATION_OFF**标志。 |

如果在[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的 "**标志**" 字段中指定了 " **KSCAMERA \_ EXTENDEDPROP \_ RELATIVEPANELOPTIMIZATION \_ ** "，则 "**值**" 字段必须为相机当前所面向的相对方向指定 PLD。

这可以是用于 ACPI PLD 的任何枚举值，但大多数情况下，最常见的是**前端**、**备份**或**未知**。

如果为 SET 操作指定了**KSCAMERA \_ EXTENDEDPROP \_ RELATIVEPANELOPTIMIZATION \_ OFF** ，则忽略**值**字段。

对于 GET 操作，驱动程序必须返回当前为相机编程的方向。

如果指定**KSCAMERA \_ EXTENDEDPROP \_ RELATIVEPANELOPTIMIZATION \_ OFF** ，或者未设置任何值，则必须返回设备的默认 PLD。

如果指定了**KSCAMERA \_ EXTENDEDPROP \_ RELATIVEPANELOPTIMIZATION \_ ON** ，则必须返回最新设置的值。

## <a name="requirements"></a>要求

**标头：** ksmedia （包括 ksmedia）
