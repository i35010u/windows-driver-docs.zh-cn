---
title: 示例 7 停止所有跟踪会话
description: 示例 7 停止所有跟踪会话
ms.assetid: a832bf9a-ab7e-4ec0-823b-52bc6016e791
keywords:
- 跟踪会话 WDK，停止
- 停止跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c19fe1e8a954a13b53d52624539d6a1202dca99
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378837"
---
# <a name="example-7-stopping-all-trace-sessions"></a>示例 7：停止所有跟踪会话


## <span id="ddk_stopping_all_trace_sessions_tools"></span><span id="DDK_STOPPING_ALL_TRACE_SESSIONS_TOOLS"></span>


以下命令在计算机上停止所有跟踪会话：

```
tracelog -x
```

在响应中，跟踪日志列出了在计算机上运行每个跟踪会话，并询问您是否要停止该会话。 例如：

```
Do you want to stop the "My Trace" session (Y or N)?
```

若要停止该会话，请键入**Y**。Tracelog 然后列出以及以下消息会话的属性：

```
The "MyTrace" session has been stopped
```

 

 





