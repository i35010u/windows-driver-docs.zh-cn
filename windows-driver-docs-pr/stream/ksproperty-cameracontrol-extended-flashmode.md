---
title: 'KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FLASHMODE (正常和序列) '
description: Flash 属性控件为相机的正常和序列照片模式设置 flash 模式操作。
ms.assetid: A190CB91-0AC4-4ECC-8C55-F0C48CF7B190
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: d11dcf7eed95d26794337a4b29d6ffa34cf7d552
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192637"
---
# <a name="ksproperty_cameracontrol_extended_flashmode-normal-and-sequence"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FLASHMODE (正常和序列) 

Flash 属性控件为相机的正常和序列照片模式设置 flash 模式操作。

## <a name="usage-summary-table"></a>使用情况摘要表

| 获取 | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|--|--|--|--|--|
| 是 | 是 | 筛选器 | [**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) | [**KSCAMERA_EXTENDEDPROP_HEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

属性值 (操作数据) 包含 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构和 [**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value) 结构。

总的属性数据大小为 **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ 标头) + **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ VALUE) 。 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含驱动程序支持的下列一种或多种闪存模式的按位 "或" 组合。

| 闪光模式 | 说明 |
|--|--|
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ OFF | 闪光灯处于关闭状态。 |
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ | 闪光灯处于默认强度级别。 |
| \_ \_ \_ ADJUSTABLEPOWER 上的 KSCAMERA EXTENDEDPROP FLASH \_ | 闪存在特定电源级别打开。 |
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ 自动 | 闪存是根据照明条件自动进行的。 |
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ 自动 \_ ADJUSTABLEPOWER | 闪存是根据特定电源级别的照明条件自动进行的。 |

除了 KSCAMERA \_ EXTENDEDPROP \_ flash OFF 外，以下功能标志可与以前的 flash 设置组合 \_ 。

| 闪光功能 | 说明 |
|--|--|
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ REDEYEREDUCTION | 启用防红眼功能。 此标志可以与其他任何设置结合。 |
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ SINGLEFLASH | 仅将闪存设置为一个触发器。 当照相机未处于照片序列模式时，将忽略此功能。 |
| KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ MULTIFLASHSUPPORTED | 将 flash 设置为每个序列帧上的触发器。 当照相机未处于照片序列模式时，将忽略此功能。 |

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的闪光模式。

照相机的默认闪烁模式为 KSCAMERA \_ EXTENDEDPROP \_ flash \_ OFF。 如果照相机支持 flash，KSCAMERA \_ EXTENDEDPROP \_ flash \_ OFF，KSCAMERA \_ EXTENDEDPROP \_ flash \_ ON，KSCAMERA \_ EXTENDEDPROP \_ flash \_ AUTO 是必需的模式。 KSCAMERA \_ EXTENDEDPROP \_ flash \_ AUTO \_ ADJUSTABLEPOWER 和 KSCAMERA \_ EXTENDEDPROP \_ flash \_ auto \_ ADJUSTABLEPOWER 模式是可选的。

如果相机支持照片序列模式，则需要 flash 控件属性，支持 KSCAMERA \_ EXTENDEDPROP \_ flash \_ SINGLEFLASH。

此属性控件是同步的，不可取消。

## <a name="remarks"></a>备注

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY \_ 类型 \_ GET 请求时，驱动程序会将 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 的成员设置为以下项。

| 成员 | Value |
|--|--|
| 版本 | 1 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)  |
| 大小 | sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE)  |
| 结果 | 0 |
| 功能 | 支持闪存模式值 |
| Flags |  (当前 flash 模式值设置) &#x7c; (flash 功能标志)  |

如果 torch 模式为 \_ ADJUSTABLEPOWER 上的 KSCAMERA EXTENDEDPROP \_ flash 或 KSCAMERA EXTENDEDPROP \_ \_ \_ \_ flash \_ on \_ ADJUSTABLEPOWER，则 u) [** \_ KSCAMERA \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)的**EXTENDEDPROP**成员的值将包含介于 0-100 之间的强度级别值。 强度值为0，表示最小级别为100，表示最大强度级别。 如果未设置可调整的电源标志，则将在 **u) **中返回标准化强度设置的值。

如果以前未设置 flash 模式，则会将 **Flags** 设置为 KSCAMERA \_ EXTENDEDPROP \_ flash \_ OFF (默认) 。

### <a name="setting-the-property"></a>设置属性

如果设置了属性，则 KSPROPERTY \_ 类型 \_ 集请求， [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要设置的 torch 模式。 [**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)的**u) **成员将包含设置的强度级别，如果**标志**为 KSCAMERA EXTENDEDPROP ADJUSTABLEPOWER，则设置为 KSCAMERA \_ \_ \_ \_ 或 EXTENDEDPROP \_ ADJUSTABLEPOWER \_ 闪存 \_ 自动 \_ 。

## <a name="requirements"></a>要求

**版本：** 可用开始 Windows 8。1

**标头：** Ksmedia (包含 Ksmedia) 

## <a name="see-also"></a>另请参阅

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)