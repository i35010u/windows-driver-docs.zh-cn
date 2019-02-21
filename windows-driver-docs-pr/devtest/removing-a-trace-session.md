---
title: 删除跟踪会话
description: 删除跟踪会话
ms.assetid: cc40ed01-2f1b-48b3-80da-b0711036dc77
keywords:
- 跟踪会话 WDK，删除
- 删除跟踪会话
- TraceView WDK，删除跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf3428b898e1ce93e07f072520ecdb3837152348
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519472"
---
# <a name="removing-a-trace-session"></a>删除跟踪会话


当您*删除*TraceView 窗口中的跟踪会话 TraceView 删除表示跟踪会话中的行[跟踪会话列表](trace-session-list.md)和关联[跟踪消息列表](trace-message-lists.md)从显示的底部窗格中。 若要删除的跟踪会话，请执行以下操作：

1.  在跟踪会话列表中，用鼠标右键单击行的任何单元格的跟踪会话。

2.  单击**删除日志会话**。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

可以从跟踪会话列表中删除实时跟踪会话或跟踪日志会话。

若要删除的实时跟踪会话，该会话必须处于[停止](stopping-a-trace-session.md)（即，所有提供程序必须禁用）。 如果在会话中的任何提供程序仍在运行 （也就是说，已启用），**删除日志会话**命令灰显。

 

 





