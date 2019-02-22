---
title: 示例 6 停止跟踪会话
description: 示例 6 停止跟踪会话
ms.assetid: a8520531-bebb-4334-9dc3-d50f4a851e7e
keywords:
- 跟踪会话 WDK，停止
- 停止跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aef4eae6325a2827594a5626d98ec15dadb60d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548093"
---
# <a name="example-6-stopping-a-trace-session"></a>示例 6:停止跟踪会话


## <span id="ddk_stopping_a_trace_session_tools"></span><span id="DDK_STOPPING_A_TRACE_SESSION_TOOLS"></span>


以下命令停止 MyTrace 跟踪会话：

```
tracelog -stop MyTrace
```

在响应中，跟踪日志显示跟踪会话的属性。

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

若要验证是否已停止跟踪会话，请使用列表 (**tracelog-l**) 或查询 (**tracelog-q**) 命令。

 

 





