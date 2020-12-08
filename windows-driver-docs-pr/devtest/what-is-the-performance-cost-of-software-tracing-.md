---
title: 软件跟踪的性能成本是多少
description: 软件跟踪的性能成本是多少
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2abbc2e13f471f8e040f5c8c89cd07877a1d1d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810705"
---
# <a name="what-is-the-performance-cost-of-software-tracing"></a>软件跟踪的性价比如何？


通常，软件跟踪的性能成本非常小。 代码已最小化，缓冲区会有效地进行管理，并以二进制格式编写消息。 此外，格式化跟踪消息（这是一种大性能排出）会推迟，直到用户选择格式化和显示跟踪消息。

使用 [WPP 软件跟踪](wpp-software-tracing.md) 宏将软件跟踪添加到驱动程序时，几乎没有任何性能开销，除非为跟踪会话启用了提供程序。

在软件跟踪代码的 If 语句中，WPP 宏的数量为三个条件检查。 除非启用了提供程序，否则这些检查将阻止生成任何跟踪消息。 WPP 宏生成以下形式的代码：

```
If (WPP_CHECK_INIT && WPP_LEVEL_FLAGS_ENABLED) {
    Call trace_message_routine
}
```

在此生成的代码中，WPP \_ 检查 \_ INIT 包含一个条件检查。 \_ \_ \_ 如果只有一个级别或标志筛选器，则启用 WPP 级别标志，其中包含一个条件检查。 否则， \_ 启用 WPP 级别 \_ 标志， \_ 其中包含两个条件检查。

有关如何排除 WPP \_ 检查 \_ INIT 检查以获得更好性能的详细信息，请参阅是否 [可以优化 wpp 宏在跟踪之前生成的条件检查](can-i-optimize-the-conditional-checks-that-the-wpp-macros-produce-befo.md)。

> [!NOTE]
> 如果使用 WPP 软件跟踪以外的方法来实现驱动程序中的软件跟踪，则可能会产生一些性能开销。 此效果取决于实现方法。
