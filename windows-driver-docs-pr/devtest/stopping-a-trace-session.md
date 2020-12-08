---
title: 停止跟踪会话
description: 停止跟踪会话
keywords:
- 跟踪会话 WDK，停止
- 停止跟踪会话
- TraceView WDK，停止跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acc97a06b7b907163b152ee09c47c28a1200a36c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819671"
---
# <a name="stopping-a-trace-session"></a>停止跟踪会话


*停止* 跟踪会话时，TraceView 会禁用跟踪提供程序，将缓冲区中的所有未发送跟踪消息刷新到 TraceView 显示和跟踪日志中，然后停止跟踪会话。 若要停止跟踪会话，请执行以下操作：

1.  在 " [跟踪会话" 列表](trace-session-list.md)中，右键单击跟踪会话所在行的任何单元格。

2.  单击 " **停止跟踪**"。

短暂暂停后，" **状态** " 列的值将从 " **正在运行** " 更改为 "正在 **停止** "，然后更改为 " **已停止**"。 跟踪会话停止时，可以将 [其从显示中删除](removing-a-trace-session.md)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

TraceView 只能停止它启动的跟踪会话。 若要停止其他跟踪会话，请使用 **traceview**_SessionName_ 命令。 有关此命令的详细信息，请参阅 [**TraceView Control 命令**](traceview-control-commands.md)。

停止跟踪会话不会从显示中删除会话，也不会删除任何跟踪日志。

TraceView 使用 **EnableTrace** 函数停止跟踪会话。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 





