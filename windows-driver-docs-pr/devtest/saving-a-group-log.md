---
title: 保存组日志
description: 保存组日志
ms.assetid: 3e572e3e-68c9-4161-97bd-f93505ead496
keywords:
- 分组跟踪会话
- 跟踪会话 WDK，组
- 正在保存跟踪组日志
- 日志文件 WDK TraceView，组日志
- 日志文件 WDK TraceView
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7f334808da0b3ae5d6c792b619d5248ec5b4eff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561573"
---
# <a name="saving-a-group-log"></a>保存组日志


跟踪会话组的成员身份不会影响事件跟踪日志 (.etl) 文件或 TraceView 跟踪会话组中列出 (.out) 文件的内容。 它们继续记录一个跟踪会话有关的数据。

若要创建的组的消息的记录，按它们出现在[跟踪消息列表](trace-message-lists.md)、 将这些消息复制组跟踪消息列表中，并将其粘贴到文档，可以保存，例如文本或电子表格文件。

因为中的消息的跟踪到达[跟踪会话列表](trace-session-list.md)受影响的消息速率、 缓冲区大小，并刷新计时器为每个跟踪会话，到达一起可能实际的不同会话中的跟踪消息发生在非常不同的时间。 有关的更准确地组合的跟踪消息，对其进行排序的时间戳 (在**系统时间**列) 的每条消息。

 

 





