---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ OPTIMIZATIONHINT （应用程序性能策略）
description: 照相机驱动程序可以根据应用程序提供的提示来优化其捕获操作。 此属性通知驱动程序根据可能使用最多的操作来设置其性能策略。
ms.assetid: FEA3D355-B490-4E67-905D-EE5507E91150
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
ms.openlocfilehash: c47be5b181c94a60a788fa16c68a34c7cb43d107
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128893"
---
# <a name="ksproperty_cameracontrol_extended_optimizationhint-application-performance-strategy"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ OPTIMIZATIONHINT （应用程序性能策略）

照相机驱动程序可以根据应用程序提供的提示来优化其捕获操作。 此属性通知驱动程序根据可能使用最多的操作来设置其性能策略。 例如，当针对照片进行了优化时，照相机驱动程序可以对传感器进行编程以优化传感器的曝光速度和分辨率，以降低从照片捕获触发器到映像捕获的延迟。 同样，在对视频进行优化时，照相机驱动程序可以对传感器编程更高的帧速率，但会降低分辨率。

## <a name="usage-summary-table"></a>使用情况摘要表

| 获取 | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|--|--|--|--|--|
| 是 | 是 | 筛选 | [**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) | [**KSCAMERA_EXTENDEDPROP_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

属性值（操作数据）包含[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[**KSCAMERA \_ EXTENDEDPROP \_ 值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。

总属性数据大小为**sizeof**（KSCAMERA \_ EXTENDEDPROP \_ 标头） + **sizeof**（KSCAMERA \_ EXTENDEDPROP \_ VALUE）。 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含以下一个或多个优化提示的按位 "或" 组合。

| 优化提示 | 说明 |
|--|--|
| KSCAMERA \_ EXTENDEDPROP \_ 优化 \_ 照片 | 为照片优化了相机操作 |
| KSCAMERA \_ EXTENDEDPROP \_ 优化 \_ 视频 | 相机操作经过优化，可用于视频 |

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的优化（一个值）。

默认优化类型为 "KSCAMERA \_ EXTENDEDPROP \_ 优化 \_ 照片"。 如果相机驱动程序支持此属性，则必须同时支持这两种优化类型。

此属性控件是同步的，不可取消。

## <a name="remarks"></a>备注

### <a name="optimization-modes"></a>优化模式

**KSCAMERA \_ EXTENDEDPROP \_ 优化 \_ 照片**

所有相机驱动程序都必须处于此模式下，直到明确知道使用 KSCAMERA \_ EXTENDEDPROP \_ 优化 \_ 视频模式为止。 此模式的目的是针对照片操作优化相机硬件。 视频操作在此模式下仍必须正常运行。

**KSCAMERA \_ EXTENDEDPROP \_ 优化 \_ 视频**

此模式表示相机可能会用于视频操作。 照相机驱动程序应该优化此模式的视频操作硬件。 照片操作必须正常运行，但对于视频操作，资源使用优先级。

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY \_ 类型 \_ GET 请求时，驱动程序会将[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的成员设置为以下项。

| 成员 | 值 |
|--|--|
| 版本 | 1 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE （0xFFFFFFFF） |
| 大小 | sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VALUE） |
| 结果 | 0 |
| 功能 | 支持的优化值 |
| Flags | 当前优化值设置 |

如果以前未设置优化模式，则驱动程序会将**标志**设置为 KSCAMERA \_ EXTENDEDPROP \_ 优化 \_ 照片（默认值）。

### <a name="setting-the-property"></a>设置属性

如果设置了属性，则 KSPROPERTY \_ 类型 \_ 集请求， [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要设置的优化模式。

## <a name="requirements"></a>要求

**版本：** 可用开始 Windows 8。1

**标头：** Ksmedia （包括 Ksmedia）

## <a name="see-also"></a>另请参阅

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA \_ EXTENDEDPROP \_ 值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
