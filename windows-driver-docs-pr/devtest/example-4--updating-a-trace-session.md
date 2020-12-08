---
title: 示例4更新跟踪会话
description: 示例4更新跟踪会话
keywords:
- 跟踪会话 WDK，更新
- 更新跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7edcde9dbca10581dda9065413f089715887cb4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839137"
---
# <a name="example-4-updating-a-trace-session"></a>示例 4：更新跟踪会话

## <span id="ddk_updating_a_trace_session_tools"></span><span id="DDK_UPDATING_A_TRACE_SESSION_TOOLS"></span>

当跟踪会话正在运行时，您可以更新实时或记录的跟踪会话的下列属性：

-   使用 **-f**) 将实时跟踪会话转换为跟踪日志会话 (。

-   使用 **-f**) 为现有跟踪日志会话创建新的跟踪日志 (。

-   使用 **-rt**) ，将实时跟踪消息传递添加到现有跟踪日志会话 (。

-   使用 **-max)** 更改 (的最大缓冲区数，但不能使用最小缓冲区数。

-   使用 **-ft**) 更改刷新时间间隔 (。

-   使用 tracelog) 刷新跟踪缓冲区 (**-** 。

不能使用 **tracelog** 命令更改跟踪提供程序的标志和级别。 相反，请使用 **tracelog** 命令，如 [示例5：启用跟踪提供程序](example-5--enabling-trace-providers.md)中所示。

**-Rt** 和 **-f** 参数在 **tracelog** 命令中的工作方式有所不同。 **-Rt** 参数向跟踪日志会话添加实时消息传递。 因此，新的跟踪消息将直接发送到跟踪使用者和跟踪日志。 但是，在可以将实时消息传递添加到跟踪日志会话之前，必须使用 **tracelog** 命令刷新缓冲区。 当 **-f** 参数用于更新实时跟踪会话时，它会将传递的实时消息传递替换为跟踪日志。 因此，新的跟踪消息只发送到跟踪日志;它们不再直接发送到跟踪使用者。

下面的命令将名为 "MyTrace" 的实时跟踪会话更改为跟踪日志会话。 该命令使用 **-f** 参数指定日志文件的位置 C： \\ 跟踪 \\ MyTrace。 它还使用值为 **35** 的 **-max** 参数将最大缓冲区数增加到35。

```
tracelog -update MyTrace -f c:\tracing\mytrace.etl -max 35
```

在响应中，Tracelog 显示跟踪会话的属性，其中包括刚刚更改的属性。

此命令的结果是，提供程序生成的所有新跟踪消息和在提交命令时存储在缓冲区中的任何跟踪消息仅写入日志文件。 它们不再直接发送到跟踪使用者，就像在实时跟踪会话中一样。

若要将跟踪日志添加到实时跟踪会话，以便将跟踪消息发送到跟踪使用者和跟踪日志，请包括 **-rt** 和 **-f** 参数，如以下命令中所示。

```
tracelog -update MyTrace -rt -f c:\tracing\mytrace.etl -max 35
```

你还可以在会话运行时刷新跟踪缓冲区。 这是一个不与刷新计时器协调的强制刷新。 当刷新计时器过期和跟踪会话停止时，系统将再次刷新缓冲区。

若要刷新现有跟踪会话的缓冲区，请使用 **-flush** 参数，如以下示例中所示。 **-Flush** 参数不是 **tracelog** **命令的** 子参数。

```
tracelog -flush MyTrace
```

在响应中，Tracelog 显示跟踪会话的修改后的属性。
