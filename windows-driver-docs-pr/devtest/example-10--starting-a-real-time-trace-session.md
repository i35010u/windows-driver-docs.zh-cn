---
title: 示例 10 启动实时跟踪会话
description: 示例 10 启动实时跟踪会话
ms.assetid: 1dfa8cf1-dd51-4415-b6d4-84241db2aa03
keywords:
- 跟踪会话 WDK，实时
- 实时跟踪会话 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d205ea49f63df5fcaa187f88995061aac3df90f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555674"
---
# <a name="example-10-starting-a-real-time-trace-session"></a>示例 10:启动实时跟踪会话


## <span id="ddk_starting_a_real_time_trace_session_tools"></span><span id="DDK_STARTING_A_REAL_TIME_TRACE_SESSION_TOOLS"></span>


以下命令启动实时跟踪会话--跟踪消息将直接发送到跟踪使用者而不是发送到日志文件的会话。

```
tracelog -start MyTrace guid MyProvider.guid -rt
```

可以使用相同的参数以自定义将用于跟踪日志会话，除了这些影响日志文件的参数的实时跟踪会话。 这包括实时跟踪的特殊跟踪会话和专用跟踪会话。 但是，由于 Tracelog[跟踪控制器](trace-controller.md)，而非[跟踪使用者](trace-consumer.md)，不能使用跟踪日志来查看实时跟踪会话过程中生成的跟踪消息。 相反，如使用跟踪的使用者[Tracefmt](tracefmt.md)，或使用[TraceView](traceview.md)，这是一个跟踪控制器和跟踪使用者。

以下命令使用 Tracefmt 格式从 MyTrace 实时跟踪会话的跟踪消息，显示在命令提示符窗口中，并将其保存到文本文件以供日后检查。 有关命令语法的详细信息，请参阅[Tracefmt](tracefmt.md)。

```
tracefmt -rt MyTrace -p c:\tracing -o mytrace.txt
```

 

 





