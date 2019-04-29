---
title: 筛选器规则的特殊操作
description: 筛选器规则的特殊操作
ms.assetid: f2631f39-02bb-4bbc-b63b-6a0200d47bc8
keywords:
- 筛选跟踪消息，特殊操作 WDK
- 跟踪消息筛选器 WDK，特殊操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e8cb1db779fee081e8a4596257c8ebd71999722
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378021"
---
# <a name="special-actions-for-filter-rules"></a>筛选器规则的特殊操作


有三个中的特殊值**操作**筛选规则的元素。 以下列表介绍了这些操作。

<span id="Ignore"></span><span id="ignore"></span><span id="IGNORE"></span>**Ignore**  
将忽略该规则。 此操作是删除该规则的替代方法。

<span id="Discard"></span><span id="discard"></span><span id="DISCARD"></span>**放弃**  
隐藏的跟踪消息。 此操作是仅在新消息上有效。 对于日志文件中的消息，必须保存并重新加载日志。 有关说明，请参阅"注释"下面。

<span id="AND"></span><span id="and"></span>**AND**  
创建连接的与运算的多行规则。 要应用的操作，必须满足条件的多行规则中的所有条件。 默认情况下，通过或运算符连接筛选器中的所有规则。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

大多数筛选器规则将立即生效。 筛选器使用的规则**放弃**操作是仅在应用规则后到达的消息上有效。 要应用**放弃**规则应用于现有的日志文件[保存工作区](saving-or-resaving-a-workspace.md)，[删除跟踪会话](removing-a-trace-session.md)，然后[打开工作区](opening-a-workspace.md)。

 

 





