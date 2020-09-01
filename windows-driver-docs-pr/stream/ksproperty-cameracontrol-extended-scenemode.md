---
title: 'KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE (驱动程序定义模式) '
description: 场景模式属性选择驱动程序定义的模式，该模式表示预设控件的集合。
ms.assetid: 32C350FF-AA54-4F28-8AD2-341A31648B60
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
ms.openlocfilehash: e5a67f4ad23e592e71ba9a7175d4fef28721a0d7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189741"
---
# <a name="ksproperty_cameracontrol_extended_scenemode-driver-defined-mode"></a>KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ SCENEMODE (驱动程序定义模式) 

场景模式属性选择驱动程序定义的模式，该模式表示预设控件的集合。 驱动程序确定分配到场景模式的预设，并在选定场景时启用这些控制设置。

## <a name="usage-summary-table"></a>使用情况摘要表

| 获取 | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|--|--|--|--|--|
| 是 | 是 | 筛选器 | [**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) | [**KSCAMERA_EXTENDEDPROP_HEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

属性值 (操作数据) 包含 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构和 [**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value) 结构。 **KSCAMERA \_ EXTENDEDPROP \_ 值**是必需的，但**值**成员被忽略。

总的属性数据大小为 **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ 标头) + **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ VALUE) 。 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含驱动程序支持的下列一种或多种场景模式的按位 "或" 组合。

| 场景模式 | 说明 |
|--|--|
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 自动 | 自动气味模式。 控件处于自动设置状态。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 宏 | ) 定义了宏场景模式 (驱动程序。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 纵向 | 纵向场景模式 () 定义驱动程序。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 运动 | 运动场景模式 () 定义驱动程序。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 雪 | 定义)  (驱动程序的雪场景模式。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 夜景 | 夜间场景模式 () 定义驱动程序。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 海滩 | 海滩场景模式 (驱动程序定义) 。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 日落 | ) 定义的 (驱动程序的日落场景模式。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ CANDLELIGHT | Candlelight 场景模式 () 定义驱动程序。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ 横向 | 横向场景模式 () 定义驱动程序。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ NIGHTPORTRAIT | 夜间)  (驱动程序定义的夜间模式场景模式。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ BACKLIT | Backlit 场景模式 () 定义驱动程序。 |
| KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ | 控件是手动更改的，未设置预定义的场景模式。 |

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的场景模式。 照相机的默认场景模式始终是 KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ AUTO。

此属性控件是异步的，不可取消。

## <a name="remarks"></a>备注

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY \_ 类型 \_ GET 请求时，驱动程序会将 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 的成员设置为以下项。

| 成员 | Value |
|--|--|
| 版本 | 1 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)  |
| 大小 | sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE)  |
| 结果 | 0 |
| 功能 | 支持 KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL &#x7c; (场景模式值)  |
| Flags | 当前场景模式值设置 (仅) 一个值 |

如果之前未设置任何场景模式，则 **Flags** 设置为 KSCAMERA \_ EXTENDEDPROP \_ SCENEMODE \_ AUTO (默认) 。

### <a name="setting-the-property"></a>设置属性

如果设置了属性，则 KSPROPERTY \_ 类型 \_ 集请求， [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要启用的场景模式。

## <a name="requirements"></a>要求

**版本：** 可用开始 Windows 8。1

**标头：** Ksmedia (包含 Ksmedia) 

## <a name="see-also"></a>另请参阅

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)