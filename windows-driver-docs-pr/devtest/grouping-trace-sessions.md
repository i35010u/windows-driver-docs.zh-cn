---
title: 将跟踪会话分组
description: 将跟踪会话分组
ms.assetid: dd9f39ee-fb93-4bf8-ac5c-5e884e57fcaa
keywords:
- TraceView WDK，对会话进行分组
- 分组跟踪会话
- 跟踪会话 WDK，组
- 多个跟踪会话 WDK TraceView
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5213575fba7d6ed92ed494d1350dfaca87d28bf5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360393"
---
# <a name="grouping-trace-sessions"></a>将跟踪会话分组


你可以组合多个正在运行的跟踪会话或多个现有的跟踪日志显示到跟踪会话组。 当你执行操作，从分组的会话的跟踪消息或日志一起显示在单个[跟踪消息列表](trace-message-lists.md)窗格。

作为单个会话，跟踪会话组进行管理。 例如，如果停止跟踪会话，这是组的一部分，TraceView 停止组中的所有跟踪会话。 同样，如果您[筛选跟踪消息](filtering-trace-messages.md)，筛选器应用于组中的所有跟踪消息。 但是，组的一部分时，仍可以更改单个跟踪会话或其提供程序的属性。

跟踪会话的分组不会影响[事件跟踪日志 (.etl) 文件](trace-log.md)、 TraceView 清单跟踪会话 (.out) 文件或 TraceView 摘要 (.sum) 文件。 这些文件，就好像不分组会话记录每个会话中的数据。

本部分包括：

[创建跟踪会话组](creating-trace-session-groups.md)

[取消组合跟踪会话](ungrouping-trace-sessions.md)

[正在保存组日志](saving-a-group-log.md)

[分组的限制](limitations-of-grouping.md)

 

 





