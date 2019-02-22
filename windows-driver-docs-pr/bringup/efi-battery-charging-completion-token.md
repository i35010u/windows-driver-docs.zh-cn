---
title: EFI_BATTERY_CHARGING_COMPLETION_TOKEN
description: EFI_BATTERY_CHARGING_COMPLETION_TOKEN
ms.assetid: 1151643e-8b22-4034-b043-ac4d44c01082
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e9e931cccf04e2d90410c85c249815302c9eb29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548271"
---
# <a name="efibatterychargingcompletiontoken"></a>EFI\_电池\_正在充电\_完成\_令牌


此结构定义使用的完成令牌[EFI\_电池\_正在充电\_协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)。

## <a name="syntax"></a>语法


```cpp
typedef struct _EFI_BATTERY_CHARGING_COMPLETION_TOKEN {
  EFI_EVENT Event;
  EFI_BATTERY_CHARGING_STATUS Status;
} EFI_BATTERY_CHARGING_COMPLETION_TOKEN;
```

## <a name="members"></a>成员


<a href="" id="event"></a>**事件**  
要发出信号后费用请求完成的事件。 事件的类型必须为 EVT\_通知\_信号。

<a href="" id="status"></a>**状态**  
已完成的操作的结果。

## <a name="remarks"></a>备注


EFI\_电池\_正在充电\_完成\_中返回标记*CompletionToken*参数[EFI\_电池\_收费\_协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)。

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题

[EFI\_BATTERY\_CHARGING\_PROTOCOL.ChargeBattery](efi-battery-charging-protocolchargebattery.md)  

[EFI\_电池\_正在充电\_状态](efi-battery-charging-status.md)  
