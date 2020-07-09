---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOMODE
description: 此属性设置或检索照相机的照片模式设置。
ms.assetid: C9596B85-A07B-4DF7-852F-C9EBF43E1E44
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: cb615a6005a28ee8c031e8748a908ea0d7d063d0
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128886"
---
# <a name="ksproperty_cameracontrol_extended_photomode"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOMODE

此属性设置或检索照相机的照片模式设置。

## <a name="usage-summary-table"></a>使用情况摘要表

| 获取 | 设置 | 目标 | 属性描述符类型 | 属性值类型 |
|--|--|--|--|--|
| 是 | 是 | 筛选 | [**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) | [**KSCAMERA_EXTENDEDPROP_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

属性值（操作数据）包含[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[**KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)结构。 这两个指定了在设置序列模式时的照片模式和历史记录帧计数。

所需的照片模式是在[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员中设置的。 照片模式设置为以下其中一项。

| 照片模式 | 说明 |
|--|--|
| KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE \_ NORMAL | 正常静止照片操作 |
| KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE \_ 序列 | 照片序列捕获操作 |

总属性数据大小为**sizeof**（KSCAMERA \_ EXTENDEDPROP \_ 标头） + **sizeof**（KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE）。 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

> [!NOTE]
> 设置照片模式是一种异步控制操作，并且 \_ \_ \_ 必须在[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员中设置 KSCAMERA EXTENDEDPROP cap ASYNCCONTROL。

## <a name="remarks"></a>备注

当响应 KSPROPERTY \_ 类型 \_ GET 请求时，驱动程序会将[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的成员设置为以下项。

| 成员 | 值 |
|--|--|
| 版本 | 1 |
| PinId | 照片 pin 的 pin ID |
| 大小 | sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_PHOTOMODE） |
| 结果 | 尝试获取照片模式数据时导致的错误值。 否则为 0。 |
| 功能 | KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |
| Flags | 当前照片模式 |

## <a name="requirements"></a>要求

**版本：** 可用开始 Windows 8。1

**标头：** Ksmedia （包括 Ksmedia）

## <a name="see-also"></a>另请参阅

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
