---
title: 筛选跟踪消息
description: 筛选跟踪消息
keywords:
- TraceView WDK，筛选消息
- 筛选跟踪消息 WDK
- 筛选跟踪消息，关于筛选跟踪消息
- 跟踪消息筛选器 WDK
- 跟踪消息筛选器 WDK，关于跟踪消息筛选器
- 规则 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26b76be4c78c1f543fad2ad848755f4da9815f01
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838635"
---
# <a name="filtering-trace-messages"></a>筛选跟踪消息

使用软件跟踪的难题之一是，甚至是一个简单且熟悉的提供程序生成的消息量。 TraceView 中的跟踪消息筛选器可帮助你查找和突出显示关键消息，并隐藏其他消息。

*跟踪消息筛选器* 是一组规则，用于更改 [跟踪消息列表](trace-message-lists.md)中跟踪消息的外观。 它适用于跟踪会话、日志显示或跟踪会话 (或日志) 组中的所有跟踪消息。 筛选器不会更改基础跟踪提供程序或跟踪日志。

可以在跟踪会话正在运行时、完成后或在查看跟踪日志时创建和更改跟踪消息筛选器。

本部分包括

[添加规则](adding-a-rule.md)

[删除规则](deleting-a-rule.md)

[更改规则](changing-a-rule.md)

[保存筛选器](saving-a-filter.md)

[筛选器规则元素](filter-rule-elements.md)

[筛选器规则的特殊操作](special-actions-for-filter-rules.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

大多数筛选器规则会立即生效。 使用 **放弃** 操作的筛选规则仅对应用规则后到达的消息有效。 若要将 **丢弃** 规则应用到现有日志文件，请 [保存工作区](saving-or-resaving-a-workspace.md)， [删除跟踪会话](removing-a-trace-session.md)，然后 [打开工作区](opening-a-workspace.md)。

筛选规则按它们在筛选器中出现的顺序进行应用。 如果有多个规则影响跟踪消息，则只会应用影响消息的第一条规则。

筛选器中的规则由或操作隐式连接;也就是说，它们都适用。 若要连接规则和操作，请选择 **和** 操作。
