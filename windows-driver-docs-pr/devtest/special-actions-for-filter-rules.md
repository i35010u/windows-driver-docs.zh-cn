---
title: 筛选器规则的特殊操作
description: 筛选器规则的特殊操作
keywords:
- 筛选跟踪消息，特殊操作 WDK
- 跟踪消息筛选器 WDK，特殊操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64963c00af0a1347c9cdd26b5fe29a17dab2fa67
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805679"
---
# <a name="special-actions-for-filter-rules"></a>筛选器规则的特殊操作


筛选规则的 **Action** 元素中有三个特殊值。 以下列表描述了这些操作。

<span id="Ignore"></span><span id="ignore"></span><span id="IGNORE"></span>**暂且**  
忽略规则。 此操作是删除规则的替代方法。

<span id="Discard"></span><span id="discard"></span><span id="DISCARD"></span>**去除**  
隐藏跟踪消息。 此操作仅对新消息有效。 对于日志文件中的消息，您必须保存并重新加载日志。 有关说明，请参阅下面的 "注释"。

<span id="AND"></span><span id="and"></span>**与**  
创建由和操作连接的多行规则。 对于要应用的操作，必须满足多行规则中的所有条件。 默认情况下，筛选器中的所有规则都通过或运算符连接。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

大多数筛选器规则会立即生效。 使用 **放弃** 操作的筛选规则仅对应用规则后到达的消息有效。 若要将 **丢弃** 规则应用到现有日志文件，请 [保存工作区](saving-or-resaving-a-workspace.md)， [删除跟踪会话](removing-a-trace-session.md)，然后 [打开工作区](opening-a-workspace.md)。

 

 





