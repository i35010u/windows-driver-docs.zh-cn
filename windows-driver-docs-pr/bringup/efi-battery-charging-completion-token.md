---
title: EFI_BATTERY_CHARGING_COMPLETION_TOKEN
description: EFI_BATTERY_CHARGING_COMPLETION_TOKEN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae1354038ecfa11f6d0158207cb074654be78326
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789119"
---
# <a name="efi_battery_charging_completion_token"></a>EFI \_ 电池 \_ 充电 \_ 完成 \_ 令牌


此结构定义 [EFI \_ 电池 \_ 充电协议使用的完成令牌 \_ 。ChargeBattery](efi-battery-charging-protocolchargebattery.md)。

## <a name="syntax"></a>语法


```cpp
typedef struct _EFI_BATTERY_CHARGING_COMPLETION_TOKEN {
  EFI_EVENT Event;
  EFI_BATTERY_CHARGING_STATUS Status;
} EFI_BATTERY_CHARGING_COMPLETION_TOKEN;
```

## <a name="members"></a>成员


<a href="" id="event"></a>**引发**  
完成计费请求后发出信号的事件。 事件类型必须是 ".EVT \_ 通知" \_ 。

<a href="" id="status"></a>**状态值**  
已完成的操作的结果。

## <a name="remarks"></a>备注


Efi \_ 电池 \_ 充电 \_ 完成 \_ 令牌在 *CompletionToken* [efi \_ 电池 \_ 充电协议的 CompletionToken 参数中返回 \_ 。ChargeBattery](efi-battery-charging-protocolchargebattery.md)。

## <a name="requirements"></a>要求


**标头：** 用户生成

## <a name="related-topics"></a>相关主题

[EFI \_ 电池 \_ 充电 \_ 协议。ChargeBattery](efi-battery-charging-protocolchargebattery.md)  

[EFI \_ 电池 \_ 充电 \_ 状态](efi-battery-charging-status.md)  
