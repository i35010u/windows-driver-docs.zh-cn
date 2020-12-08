---
title: 示例6停止跟踪会话
description: 示例6停止跟踪会话
keywords:
- 跟踪会话 WDK，停止
- 停止跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28320397e343cf0c124096402dafb22725ea7494
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804287"
---
# <a name="example-6-stopping-a-trace-session"></a>示例 6：停止跟踪会话


## <span id="ddk_stopping_a_trace_session_tools"></span><span id="DDK_STOPPING_A_TRACE_SESSION_TOOLS"></span>


以下命令停止 MyTrace 跟踪会话：

```
tracelog -stop MyTrace
```

在响应中，Tracelog 显示跟踪会话的属性。

```
Operation Status:       0L      The operation completed successfully.

Logger Name:            MyTrace
Logger Id:              2
Logger Thread Id:       000008C8
Buffer Size:            8 Kb
Maximum Buffers:        26
Minimum Buffers:        4
Number of Buffers:      6
Free Buffers:           6
Buffers Written:        1
Events Lost:            0
Log Buffers Lost:       0
Real Time Buffers Lost: 0
AgeLimit:               15
Log File Mode:          Sequential
Log Filename:           C:\Tracing\MyTrace.etl
```

若要验证是否已停止跟踪会话，请使用列表 (**tracelog-l**) 或 query (**tracelog**) 命令。

 

 





