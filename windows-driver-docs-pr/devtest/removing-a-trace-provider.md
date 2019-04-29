---
title: 删除跟踪提供程序
description: 删除跟踪提供程序
ms.assetid: 3ea38137-9196-46a6-8cb5-04722cd43086
keywords:
- 跟踪提供程序 WDK
- 提供程序 WDK 软件跟踪
- 跟踪会话 WDK，提供程序
- 删除跟踪提供程序
- 禁用跟踪提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 870f5b3c071c51123331ca58c502895f300899bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360735"
---
# <a name="removing-a-trace-provider"></a>删除跟踪提供程序


TraceView 窗口不能用于删除或禁用正在运行的跟踪会话的跟踪提供程序。 但是，可以删除提供程序，在创建跟踪会话时之前 TraceView 已启动。

在创建跟踪会话，使用以下过程删除跟踪提供程序：

1.  上**文件**菜单上，单击**新建日志会话**。

2.  在中**名称**列表中，单击你想要删除的提供程序。

3.  单击**删除提供程序**。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

此外可以通过在命令提示符窗口中键入以下命令启动 TraceView 的会话中禁用跟踪提供程序。

```
traceview -disable SessionName -guid {#GUID | GUIDFile}
```

但是，此命令会使 TraceView，若要停止跟踪会话。 若要继续，请使用 **traceview-启动 * * * SessionName*命令来重新启动跟踪会话。 有关详细信息，请参阅[ **TraceView 控制命令**](traceview-control-commands.md)。

 

 





