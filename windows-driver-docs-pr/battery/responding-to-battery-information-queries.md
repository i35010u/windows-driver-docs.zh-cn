---
title: 响应电池信息查询
description: 响应电池信息查询
keywords:
- 电池信息 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c5ffbae6cdee7f3c1fac0fc8ab5caecfd27f38d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798667"
---
# <a name="responding-to-battery-information-queries"></a>响应电池信息查询


## <span id="ddk_responding_to_battery_information_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_INFORMATION_QUERIES_DG"></span>


电池类驱动程序调用 [*BatteryMiniQueryInformation*](/windows/win32/api/batclass/nc-batclass-bclass_query_information_callback) 例程以获取有关当前电池的各种信息。 此例程声明如下：

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

*上下文* 参数是指向上下文区域的指针，该上下文区域由 miniclass 驱动程序分配，并在设备初始化时在 [**电池 \_ 微型端口 \_ 信息**](/windows/win32/api/batclass/ns-batclass-battery_miniport_info)结构中传递给类驱动程序。 *BatteryTag* 参数是之前由 [*BatteryMiniQueryTag*](/windows/win32/api/batclass/nc-batclass-bclass_query_tag_callback)返回的值。

*Level* 参数指定所请求的信息类型。 Miniclass 驱动程序将信息格式化为 [**电池 \_ 信息**](/previous-versions/ff536283(v=vs.85)) 结构，并将其返回到 *缓冲区* 提供的地址，并在 *ReturnedLength* 中将其指向其长度的指针。

Miniclass 驱动程序应准备好处理以下请求：

-   电池功能，化学，容量，低容量警报级别，保留费用

-   温度，以十分开氏度为单位

-   估计剩余运行时间（以秒为单位）

-   设备名称

-   制造商电池型号名称

-   制造日期

-   唯一 ID

-   序列号

某些电池不能报告所有这些信息。 \_ \_ \_ 对于设备无法提供的任何信息，miniclass 驱动程序应返回状态 "无效设备请求"。

 

