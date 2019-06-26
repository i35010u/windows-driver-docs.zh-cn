---
title: 响应电池信息查询
description: 响应电池信息查询
ms.assetid: 5d215ff8-d41f-471e-bc54-570a94f3c23f
keywords:
- 电池信息 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9eb1df6611596377d8ad2c43a585052287290b0c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355238"
---
# <a name="responding-to-battery-information-queries"></a>响应电池信息查询


## <span id="ddk_responding_to_battery_information_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_INFORMATION_QUERIES_DG"></span>


电池类驱动程序调用[ *BatteryMiniQueryInformation* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_information_callback)例程，以获取各种有关当前的电池的信息。 此例程声明，如下所示：

```cpp
typedef 
NTSTATUS
(*BCLASS_QUERY_INFORMATION)(
    IN PVOID Context,
    IN ULONG BatteryTag,
    IN BATTERY_QUERY_INFORMATION_LEVEL Level,
    IN LONG AtRate OPTIONAL,
    OUT PVOID Buffer,
    IN ULONG BufferLength,
    OUT PULONG ReturnedLength
    );
```

*上下文*参数是指向 miniclass 驱动程序分配和传递给的类驱动程序中的上下文区域[**电池\_微型端口\_信息**](https://docs.microsoft.com/windows/desktop/api/batclass/ns-batclass-battery_miniport_info)在设备初始化结构。 *BatteryTag*参数是前面返回的值[ *BatteryMiniQueryTag*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_tag_callback)。

*级别*参数指定的请求信息的类型。 Miniclass 驱动程序作为信息的格式[**电池\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff536283)结构，并将其返回提供的地址处*缓冲区*，使用指向在其长度*ReturnedLength*。

Miniclass 驱动程序应准备好处理以下请求：

-   电池功能、 化学、 容量、 低容量警报级别和保留费用

-   以十分之一度 Kelvin 温度

-   估计剩余运行的时间 （秒）

-   设备名称

-   制造商的电池模型名称

-   制造日期

-   唯一 ID

-   序列号

某些电池不能报告此信息。 Miniclass 驱动程序应返回状态\_无效\_设备\_其设备不能提供任何信息的请求。

 

 




