---
title: 示例10启动 Real-Time 跟踪会话
description: 示例10启动 Real-Time 跟踪会话
keywords:
- 跟踪会话 WDK，实时
- 实时跟踪会话 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b324bb8454b23040d4f23dd4fbb9ec628c02fe35
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839759"
---
# <a name="example-10-starting-a-real-time-trace-session"></a>示例 10：启动实时跟踪会话


## <span id="ddk_starting_a_real_time_trace_session_tools"></span><span id="DDK_STARTING_A_REAL_TIME_TRACE_SESSION_TOOLS"></span>


下面的命令启动一个实时跟踪会话，在该会话中，跟踪消息将直接发送到跟踪使用者，而不是发送到日志文件。

```
tracelog -start MyTrace guid MyProvider.guid -rt
```

您可以使用相同的参数来自定义用于跟踪日志会话的实时跟踪会话，但影响日志文件的参数除外。 这包括对特殊跟踪会话和专用跟踪会话的实时跟踪。 但是，因为 Tracelog 是 [跟踪控制器](trace-controller.md)而不是 [跟踪使用者](trace-consumer.md)，所以不能使用 Tracelog 来查看在实时跟踪会话期间生成的跟踪消息。 相反，请使用跟踪使用者（如 [Tracefmt](tracefmt.md)）或使用 [TraceView](traceview.md)，后者既是跟踪控制器又是跟踪使用者。

下面的命令使用 Tracefmt 从 MyTrace 实时跟踪会话设置跟踪消息的格式，将其显示在命令提示符窗口中，并将其保存到文本文件中供以后检查。 有关命令语法的详细信息，请参阅 [Tracefmt](tracefmt.md)。

```
tracefmt -rt MyTrace -p c:\tracing -o mytrace.txt
```

 

 





