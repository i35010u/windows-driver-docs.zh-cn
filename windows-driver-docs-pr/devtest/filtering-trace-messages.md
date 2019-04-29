---
title: 筛选跟踪消息
description: 筛选跟踪消息
ms.assetid: 6e4be7ea-1a3f-4fb2-900d-b857cd635fde
keywords:
- TraceView WDK，筛选消息
- 筛选跟踪消息 WDK
- 筛选跟踪消息，有关筛选跟踪消息
- 跟踪消息筛选器 WDK
- 跟踪消息筛选器 WDK，有关跟踪消息筛选器
- 规则 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c83cb393620ecfd91e7cb2f9ee1541ea5439b8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387262"
---
# <a name="filtering-trace-messages"></a>筛选跟踪消息

使用软件跟踪的挑战之一是更简单、 熟悉提供程序生成的消息量。 将跟踪 TraceView 中的筛选器帮助你查找和突出显示关键消息，并隐藏其他消息。

一个*跟踪消息筛选器*是一套规则更改中跟踪消息的外观[跟踪消息列表](trace-message-lists.md)。 它适用于所有跟踪消息跟踪会话，日志显示，或跟踪会话 （或日志中） 组。 筛选器不会更改基础的跟踪提供程序或跟踪日志。

可以创建和更改跟踪消息筛选器，它完成后，运行时跟踪会话，或在查看跟踪日志。

本部分包括

[添加规则](adding-a-rule.md)

[正在删除规则](deleting-a-rule.md)

[更改规则](changing-a-rule.md)

[保存筛选器](saving-a-filter.md)

[筛选器规则元素](filter-rule-elements.md)

[筛选器规则的特殊操作](special-actions-for-filter-rules.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

大多数筛选器规则将立即生效。 筛选器使用的规则**放弃**操作是仅在应用规则后到达的消息上有效。 要应用**放弃**规则应用于现有的日志文件[保存工作区](saving-or-resaving-a-workspace.md)，[删除跟踪会话](removing-a-trace-session.md)，然后[打开工作区](opening-a-workspace.md)。

它们在筛选器中显示的顺序应用筛选器规则。 如果多个规则影响的跟踪消息，应用只会影响该消息的第一个规则。

隐式 OR 操作; 通过连接筛选器中的规则也就是说，它们将所有应用。 若要使用和操作连接规则，请选择**AND**操作。
