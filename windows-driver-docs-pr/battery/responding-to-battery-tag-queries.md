---
title: 响应电池标记查询
description: 响应电池标记查询
ms.assetid: ac22a1d3-413c-4991-ac9c-fbfb2c6f16c6
keywords:
- 电池标记 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7b0f4e7aa61fe4b3488193fa4f722396245afbb
ms.sourcegitcommit: 7a7e61b4147a4aa86bf820fd0b0c7681fe17e544
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056857"
---
# <a name="responding-to-battery-tag-queries"></a>响应电池标记查询


## <span id="ddk_responding_to_battery_tag_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_TAG_QUERIES_DG"></span>


电池标记是由 miniclass 驱动程序初始化并递增的 ULONG 计数器。 电池类驱动程序调用 [*BatteryMiniQueryTag*](/windows/desktop/api/batclass/nc-batclass-bclass_query_tag_callback) 来请求标记的当前值。

此 miniclass 驱动程序例程的声明如下所示：

```cpp
typedef
NTSTATUS
(*BCLASS_QUERY_TAG)(
    IN PVOID Context,
    OUT PULONG BatteryTag
    );
```

*上下文*参数是指向上下文区域的指针，该上下文区域由 miniclass 驱动程序分配，并在 \_ \_ 设备初始化 ([**BatteryClassInitializeDevice**](/windows/desktop/api/batclass/nf-batclass-batteryclassinitializedevice)) 时，将其传递到电池微型端口信息结构中的类驱动程序。 *BatteryTag*值由 miniclass 驱动程序创建和维护。

每次插入电池时，miniclass 驱动程序都必须递增标记的值，无论这是新电池还是以前出现的相同电池。

如果没有电池存在，或者如果 miniclass 驱动程序无法确定是否存在电池，则 miniclass 驱动程序应返回 " \_ 无 \_ 此类设备" 状态， \_ 并将标记的值设置为 "电池 \_ 标记 \_ 无效"。

类驱动程序在内部和对 miniclass 驱动程序的调用中使用电池标记来识别电池的特定实例。 Miniclass 驱动程序应检查要传递给每个标准例程的电池标记的值，以确保它与当前电池对应。 如果标记不正确，则 miniclass 驱动程序应返回 " \_ 无 \_ 此类设备" 状态 \_ 。

 

