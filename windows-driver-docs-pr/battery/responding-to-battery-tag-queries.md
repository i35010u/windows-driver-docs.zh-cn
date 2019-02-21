---
title: 响应电池标记查询
description: 响应电池标记查询
ms.assetid: ac22a1d3-413c-4991-ac9c-fbfb2c6f16c6
keywords:
- 电池标记 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 676e5b55603f5749d5ee3422a9e44f3dceca276a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523867"
---
# <a name="responding-to-battery-tag-queries"></a>响应电池标记查询


## <span id="ddk_responding_to_battery_tag_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_TAG_QUERIES_DG"></span>


电池标记是 ULONG 计数初始化和递增 miniclass 驱动程序。 电池类驱动程序调用[ *BatteryMiniQueryTag* ](https://msdn.microsoft.com/library/windows/hardware/ff536275)请求标记的当前值。

此 miniclass 驱动程序例程声明，如下所示：

```cpp
typedef
NTSTATUS
(*BCLASS_QUERY_TAG)(
    IN PVOID Context,
    OUT PULONG BatteryTag
    );
```

*上下文*参数是指向 miniclass 驱动程序分配和传递给电池中的类驱动程序的上下文区域\_微型端口\_在设备初始化 (信息结构[**BatteryClassInitializeDevice**](https://msdn.microsoft.com/library/windows/hardware/ff536266))。 *BatteryTag*值是由创建和维护 miniclass 驱动程序。

每次插入电池，miniclass 驱动程序必须递增的值的标记，而不管是否这是新电池或以前存在于同一个电池。

如果没有电池存在，或者如果 miniclass 驱动程序无法确定电池是否存在，则 miniclass 驱动程序应返回状态\_没有\_SUCH\_设备和设置，则值为电池标记\_标记\_无效。

类驱动程序使用电池标记在内部，然后对 miniclass 驱动程序的调用中标识电池的特定实例。 Miniclass 驱动程序应检查传递给其标准的例程，以确保它对应于当前的电池的每个电池标记的值。 如果标记不正确，则 miniclass 驱动程序应返回状态\_否\_SUCH\_设备。

 

 




