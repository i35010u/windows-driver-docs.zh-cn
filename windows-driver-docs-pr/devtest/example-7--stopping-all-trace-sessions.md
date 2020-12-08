---
title: 示例7停止所有跟踪会话
description: 示例7停止所有跟踪会话
keywords:
- 跟踪会话 WDK，停止
- 停止跟踪会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f39304b96a81e660221e86ee8e2b80df1d78f567
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804279"
---
# <a name="example-7-stopping-all-trace-sessions"></a>示例 7：停止所有跟踪会话


## <span id="ddk_stopping_all_trace_sessions_tools"></span><span id="DDK_STOPPING_ALL_TRACE_SESSIONS_TOOLS"></span>


以下命令停止计算机上的所有跟踪会话：

```
tracelog -x
```

作为响应，Tracelog 会列出计算机上运行的每个跟踪会话，并询问你是否要停止会话。 例如：

```
Do you want to stop the "My Trace" session (Y or N)?
```

若要停止会话，请键入 **Y**。Tracelog 然后列出会话的属性以及以下消息：

```
The "MyTrace" session has been stopped
```

 

 





