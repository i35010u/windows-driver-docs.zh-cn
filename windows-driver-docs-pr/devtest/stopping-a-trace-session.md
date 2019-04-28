---
title: 停止跟踪会话
description: 停止跟踪会话
ms.assetid: 648bf805-4266-4db5-aef6-414c5f37d1a3
keywords:
- 跟踪会话 WDK，停止
- 停止跟踪会话
- TraceView WDK，停止跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2dc5a0671cb01c676c8d4afd74d6d8b80c94cae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345783"
---
# <a name="stopping-a-trace-session"></a>停止跟踪会话


当您*停止*跟踪会话，TraceView 禁用跟踪提供程序，将任何未发送的跟踪消息从缓冲区刷新到 TraceView 显示和跟踪日志，然后停止跟踪会话。 若要停止跟踪会话，请执行以下操作：

1.  在中[跟踪会话列表](trace-session-list.md)，用鼠标右键单击行的任何单元格，为跟踪会话。

2.  单击**停止跟踪**。

短暂暂停的值之后**状态**列会更改从**运行**到**停止**然后**已停止**。 当停止跟踪会话时，你可以[从显示中删除](removing-a-trace-session.md)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

TraceView 可以停止它启动跟踪会话。 若要停止其他跟踪会话，请使用 **traceview-停止 * * * SessionName*命令。 有关此命令的详细信息，请参阅[ **TraceView 控制命令**](traceview-control-commands.md)。

停止跟踪会话不会从显示中删除该会话或删除的任何跟踪日志。

使用 TraceView **EnableTrace**函数以停止跟踪会话。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 





