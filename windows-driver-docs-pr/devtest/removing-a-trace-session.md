---
title: 删除跟踪会话
description: 删除跟踪会话
keywords:
- 跟踪会话 WDK，删除
- 删除跟踪会话
- TraceView WDK，删除跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 417f6d9f0c8c75f2b13ee44be886538380e05a2d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839743"
---
# <a name="removing-a-trace-session"></a>删除跟踪会话


从 "TraceView" 窗口中 *删除* 跟踪会话时，TraceView 将从显示的底部窗格中删除表示跟踪会话的行 [，并从](trace-session-list.md) 显示的底部窗格中删除关联的 [跟踪消息列表](trace-message-lists.md) 。 若要删除跟踪会话，请执行以下操作：

1.  在 "跟踪会话" 列表中，右键单击跟踪会话所在行的任何单元格。

2.  单击 " **删除日志会话**"。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

你可以从 "跟踪会话" 列表中删除实时跟踪会话或跟踪日志会话。

若要删除实时跟踪会话，必须 [停止](stopping-a-trace-session.md) 会话 (也就是说，必须) 禁用所有提供程序。 如果会话中的任何提供程序仍在运行 (即启用) ，则 " **删除日志会话** " 命令将灰显。

 

 





