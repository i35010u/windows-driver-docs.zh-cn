---
title: 设置和取消电池通知
description: 设置和取消电池通知
keywords:
- 电池通知 WDK
- 电池 miniclass 驱动程序 WDK，通知
- 通知 WDK 电池
- 电池类驱动程序 WDK，通知
- 取消电池通知
- 停止电池通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db788f334e915d84a992994034c9d2afb90de109
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798661"
---
# <a name="setting-and-canceling-battery-notification"></a>设置和取消电池通知


## <span id="ddk_setting_and_canceling_battery_notification_dg"></span><span id="DDK_SETTING_AND_CANCELING_BATTERY_NOTIFICATION_DG"></span>


Miniclass 驱动程序提供 [*BatteryMiniSetStatusNotify*](/windows/win32/api/batclass/nc-batclass-bclass_set_status_notify_callback) 例程，以便类驱动程序可以请求特定条件的通知。 例程声明如下：

```cpp
typedef
NTSTATUS
(*BCLASS_SET_STATUS_NOTIFY)(
    IN PVOID Context,
    IN ULONG BatteryTag,
    IN PBATTERY_NOTIFY BatteryNotify
    );
```

*上下文* 参数是指向上下文区域的指针，该上下文区域由 miniclass 驱动程序分配，并在 \_ 设备初始化时在电池微型端口信息结构中传递给类驱动程序 \_ 。 *BatteryTag* 参数是之前由 [*BatteryMiniQueryTag*](/windows/win32/api/batclass/nc-batclass-bclass_query_tag_callback)返回的值。

*BatteryNotify* 参数包含一组指示电池电源条件的标志，以及一个用于定义可接受电池容量范围的一对 ULONG 值。 当电池不再满足指定的电源条件或其容量高于或低于指定的范围时，miniclass 驱动程序应调用 [**BatteryClassStatusNotify**](/windows/win32/api/batclass/nf-batclass-batteryclassstatusnotify)。

*BatteryMiniSetStatusNotify* 对于 \_ \_ 无法确定用于此电池的任何条件或触发器值，BatteryMiniSetStatusNotify 应返回状态。

类驱动程序调用 [*BatteryMiniDisableStatusNotify*](/windows/win32/api/batclass/nc-batclass-bclass_disable_status_notify_callback) 例程来取消 BatteryMiniSetStatusNotify 以前请求的电池状态更改的通知。 此例程声明如下：

```cpp
typedef
NTSTATUS
(*BCLASS_DISABLE_STATUS_NOTIFY)(
    IN PVOID Context
    );
```

*上下文* 参数是一个指针，指向由 miniclass 驱动程序分配的上下文区域，并将其传递给 \_ 设备初始化时的电池微型端口信息结构中的类驱动程序 \_ 。

Miniclass 驱动程序可以忽略两个例程的功能，并且 \_ 不支持返回状态 \_ 。 然而，提供 *BatteryMiniSetStatusNotify* 例程的 miniclass 驱动程序必须提供相应的 *BatteryMiniDisableStatusNotify* 例程，反之亦然。

 

