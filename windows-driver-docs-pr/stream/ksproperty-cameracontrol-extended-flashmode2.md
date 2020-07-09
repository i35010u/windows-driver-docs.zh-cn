---
title: KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ FLASHMODE （助手 flash）
description: '\_扩展 FLASHMODE 的 KSPROPERTY CAMERACONTROL \_ 属性， \_ 以支持助理 flash。'
ms.assetid: 413B3A02-498A-4C5A-8940-9A0D10D6CE81
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE (assistant flash)
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8899984231eb045492411750238dd7f300c66f47
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128878"
---
# <a name="ksproperty_cameracontrol_extended_flashmode"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FLASHMODE

扩展** \_ \_ \_ FLASHMODE 的 KSPROPERTY CAMERACONTROL**属性，以支持助理 flash。

## <a name="usage-summary-table"></a>使用情况摘要表

| 范围 | 控制 | 类型 |
|--|--|--|
| 版本 1 | 筛选 | 同步 |

功能标志的定义如下。

```cpp
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_ON               0x0000000000000080
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_AUTO             0x0000000000000100
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_OFF              0x0000000000000000
```

**KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ 助手 \_ 开启**

此标志指示 "AF 助手" 指示灯处于开启状态。

**KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ 助手 \_ 自动**

此标志类似于**助手 \_ ON**标志。 照相机驱动程序不会始终打开 AF 助手灯，而是根据当前的照明条件来确定是否应打开 AF 助手灯。

**KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ 助手 \_ OFF**

此标志指示 AF 助手 light 处于关闭状态。

使用**KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ FLASHMODE**属性时， [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的说明与 Windows 8.1 DDI 相同。

## <a name="requirements"></a>要求

**标头：** Ksmedia （包括 Ksmedia）
