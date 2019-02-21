---
title: 分组的限制
description: 分组的限制
ms.assetid: 2cc49522-a504-43d7-b36b-297cd6c3f307
keywords:
- 分组跟踪会话
- 跟踪会话 WDK，组
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 248124b5f9863e0b256ce13bd3577013ae3590fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540800"
---
# <a name="limitations-of-grouping"></a>分组的限制

本主题介绍中 TraceView 分组功能的限制。

### <a name="span-idworkspacesandgroupsspanspan-idworkspacesandgroupsspanworkspaces-and-groups"></a><span id="workspaces_and_groups"></span><span id="WORKSPACES_AND_GROUPS"></span>工作区和组

无法在工作区中保存跟踪会话组。 如果你尝试 TraceView 将显示"不能保存工作区设置的分组的会话"。 错误消息...

### <a name="span-idremovingtracesessiongroupsspanspan-idremovingtracesessiongroupsspanremoving-trace-session-groups"></a><span id="removing_trace_session_groups"></span><span id="REMOVING_TRACE_SESSION_GROUPS"></span>删除跟踪会话组

无法删除从一个跟踪会话组[跟踪会话列表](trace-session-list.md)，即使组中的所有会话已都停止。 然后再删除组，必须取消分组跟踪会话。

### <a name="span-idtracemessageorderinagroupspanspan-idtracemessageorderinagroupspantrace-message-order-in-a-group"></a><span id="trace_message_order_in_a_group"></span><span id="TRACE_MESSAGE_ORDER_IN_A_GROUP"></span>在组中的跟踪消息顺序

跟踪会话列表中的跟踪消息到达受影响的消息速率、 缓冲区大小，并刷新计时器为每个跟踪会话，因为在同一时间到达不同会话中的跟踪消息可能实际上发生在非常不同的时间。 对于更准确的视图中，将输出文件合并为每个跟踪会话并对它们进行排序**系统时间**列。
