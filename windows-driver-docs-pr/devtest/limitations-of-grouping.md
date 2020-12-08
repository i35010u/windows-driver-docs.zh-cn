---
title: 分组的限制
description: 分组的限制
keywords:
- 分组跟踪会话
- 跟踪会话 WDK，组
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fe7f54973e4a98bb274ecb65d55d5dcdd8246c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795613"
---
# <a name="limitations-of-grouping"></a>分组的限制

本主题介绍 TraceView 中的分组功能的限制。

### <a name="span-idworkspaces_and_groupsspanspan-idworkspaces_and_groupsspanworkspaces-and-groups"></a><span id="workspaces_and_groups"></span><span id="WORKSPACES_AND_GROUPS"></span>工作区和组

无法在工作区中保存跟踪会话组。 如果尝试，TraceView 将显示 "无法保存分组会话的工作区设置"。 错误消息。

### <a name="span-idremoving_trace_session_groupsspanspan-idremoving_trace_session_groupsspanremoving-trace-session-groups"></a><span id="removing_trace_session_groups"></span><span id="REMOVING_TRACE_SESSION_GROUPS"></span>删除跟踪会话组

即使组中的所有会话均已停止，也无法从 [跟踪会话列表](trace-session-list.md)中删除跟踪会话组。 删除组之前，必须取消对跟踪会话的分组。

### <a name="span-idtrace_message_order_in_a_groupspanspan-idtrace_message_order_in_a_groupspantrace-message-order-in-a-group"></a><span id="trace_message_order_in_a_group"></span><span id="TRACE_MESSAGE_ORDER_IN_A_GROUP"></span>组中的跟踪消息顺序

由于跟踪会话列表中的跟踪消息到达受每个跟踪会话的消息速率、缓冲区大小和刷新计时器的影响，因此来自同一时间的不同会话的跟踪消息实际上可能发生在很多不同的时间。 为了获得更准确的视图，请合并每个跟踪会话的输出文件，并按 **系统时间** 列对其进行排序。
