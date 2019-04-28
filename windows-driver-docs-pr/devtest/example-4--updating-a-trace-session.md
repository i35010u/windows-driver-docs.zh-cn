---
title: 示例 4： 更新跟踪会话
description: 示例 4： 更新跟踪会话
ms.assetid: d0ff9508-cc34-43eb-975f-7f5ce3c0acf6
keywords:
- 跟踪会话 WDK，更新
- 更新跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2e7c333a44a22b2d25650e2782b58d90be6145e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344643"
---
# <a name="example-4-updating-a-trace-session"></a>示例 4：更新跟踪会话

## <span id="ddk_updating_a_trace_session_tools"></span><span id="DDK_UPDATING_A_TRACE_SESSION_TOOLS"></span>

在运行时跟踪会话，您可以更新实时或记录的跟踪会话的以下属性：

-   转换到跟踪日志会话的实时跟踪会话 (通过使用 **-f**)。

-   为现有的跟踪日志会话创建新的跟踪日志 (通过使用 **-f**)。

-   添加到现有的跟踪日志会话的实时跟踪消息传递 (通过使用 **-rt**)。

-   更改最大缓冲区数 (通过使用 **-最大)**，但不是最小的缓冲区数。

-   更改的刷新时间间隔 (通过使用 **-ft**)。

-   刷新跟踪缓冲区 (通过使用**-** tracelog-刷新)。

不能使用**tracelog-更新**命令以更改标志和级别的跟踪提供程序。 请改用**tracelog-启用**命令，如中所示[示例 5:启用跟踪提供程序](example-5--enabling-trace-providers.md)。

**-Rt**并 **-f**参数中按不同方式处理**tracelog-更新**命令。 **-Rt**参数将添加到跟踪日志会话的实时消息传递。 因此，直接向跟踪使用者和写入跟踪日志发送新的跟踪消息。 但是，可以添加到跟踪日志会话的实时消息传递之前，必须将刷新缓冲区使用**tracelog-刷新**命令。 当 **-f**参数用于更新实时跟踪会话，它会替换实时消息传递给跟踪日志传送。 因此，新的跟踪消息只发送给跟踪日志中;它们将无法再直接发送到跟踪使用者。

以下命令更改到跟踪日志会话名为"MyTrace"实时跟踪会话。 该命令使用 **-f**参数来指定日志文件，c： 的位置\\跟踪\\MyTrace.etl。 它还使用 **-最大**参数的值为**35**以提高到 35 的缓冲区的最大数目。

```
tracelog -update MyTrace -f c:\tracing\mytrace.etl -max 35
```

在响应中，跟踪日志显示跟踪会话，包括刚更改的属性的属性。

由于这只对日志文件编写命令、 提供程序，生成的所有新的跟踪消息和时该命令已提交，存储在缓冲区中任何跟踪消息。 它们将无法再直接发送到跟踪使用者，如实时跟踪会话中所示。

若要将跟踪日志添加到实时跟踪会话，以便跟踪消息发送到跟踪使用者和跟踪日志，可以同时包含 **-rt**并 **-f**参数，如以下命令中所示。

```
tracelog -update MyTrace -rt -f c:\tracing\mytrace.etl -max 35
```

运行会话时，还可以刷新跟踪缓冲区。 这是不是协调与刷新计时器强制的刷新。 当刷新计时器过期时和停止跟踪会话时，系统将再次刷新缓冲区。

若要刷新现有跟踪会话的缓冲区，请使用 **-刷新**参数，如下面的示例中所示。 **-刷新**参数不是子参数的**tracelog** **-更新**命令。

```
tracelog -flush MyTrace
```

在响应中，跟踪日志显示跟踪会话的修改后的属性。
