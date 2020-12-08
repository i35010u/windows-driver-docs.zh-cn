---
title: 删除跟踪提供程序
description: 删除跟踪提供程序
keywords:
- 跟踪提供程序 WDK
- 提供程序 WDK 软件跟踪
- 跟踪会话 WDK，提供程序
- 删除跟踪提供程序
- 禁用跟踪提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cd0721ddec8f19cfee03496dc76fd19d3cf71ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837305"
---
# <a name="removing-a-trace-provider"></a>删除跟踪提供程序


不能使用 "TraceView" 窗口从正在运行的跟踪会话中删除或禁用跟踪提供程序。 但是，你可以在创建跟踪会话时，以及在启动 TraceView 之前删除该提供程序。

创建跟踪会话时，请使用以下过程删除跟踪提供程序：

1.  在 " **文件** " 菜单上，单击 " **创建新的日志会话**"。

2.  在 " **名称** " 列表中，单击要删除的提供程序。

3.  单击 " **删除提供程序**"。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

还可以通过在命令提示符窗口中键入以下命令，在 TraceView 启动的会话中禁用跟踪提供程序。

```
traceview -disable SessionName -guid {#GUID | GUIDFile}
```

但是，此命令会导致 TraceView 停止跟踪会话。 若要继续，请使用 **traceview-start**_SessionName_ 命令重新启动跟踪会话。 有关详细信息，请参阅 [**TraceView Control 命令**](traceview-control-commands.md)。

 

 





