---
title: 将跟踪会话分组
description: 将跟踪会话分组
keywords:
- TraceView WDK，分组会话
- 分组跟踪会话
- 跟踪会话 WDK，组
- 多个跟踪会话 WDK TraceView
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34f63817fb4f1c9e2669561dfe8ed5e29924e624
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831569"
---
# <a name="grouping-trace-sessions"></a>将跟踪会话分组


可以将多个正在运行的跟踪会话或多个现有跟踪日志显示合并到一个跟踪会话组中。 执行此操作时，分组会话或日志中的跟踪消息将一起显示在一个 [跟踪消息列表](trace-message-lists.md) 窗格中。

跟踪会话组作为单一会话进行管理。 例如，如果停止作为组的一部分的跟踪会话，TraceView 将停止组中的所有跟踪会话。 同样，如果 [筛选跟踪消息](filtering-trace-messages.md)，则筛选器将应用于组中的所有跟踪消息。 但是，您仍可以更改单个跟踪会话或其提供程序的属性，但它是组的一部分。

跟踪会话的分组不会影响 [事件跟踪日志 ( .etl) 文件](trace-log.md)、TraceView 列表 () 文件或跟踪会话的 TraceView 摘要 ( 文件。 这些文件记录每个会话中的数据，就好像会话未分组一样。

本节包括：

[创建跟踪会话组](creating-trace-session-groups.md)

[将跟踪会话取消分组](ungrouping-trace-sessions.md)

[保存组日志](saving-a-group-log.md)

[分组的限制](limitations-of-grouping.md)

 

 





