---
title: 解决 GDL 配置冲突
description: 解决 GDL 配置冲突
ms.assetid: 02a2da63-0b7f-4aa9-b3c3-72784f409d94
keywords:
- GDL WDK 配置
- 配置 WDK GDL，无效的配置
- 配置 WDK GDL，冲突
- 无效 GDL 配置 WDK
- 配置 WDK GDL，解决冲突
- 解决 GDL 配置冲突 WDK GDL
- ConflictPriority 指令 WDK GDL
- FeatureType 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d73673105fbd89d939c89d5da54db30f942a801
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546834"
---
# <a name="resolving-gdl-configuration-conflicts"></a>解决 GDL 配置冲突


尽管 GDL 分析器将自动修改配置，以避免违反了约束，但请记住以下信息，以便让分析器知道你的意图。

例如，如果传递到分析器函数中的配置包含 Weather.Rain、 Today.Sunday、 Health.Well 的参数设置，从上一节的无效组合可以解决通过任何一种将设置更改在此约束中名为的参数。 分析器必须确定哪些参数的设置更改。 在许多情况下，您可能知道应更改哪些设置。 通常情况下，更重要的参数保留不变。 在这种情况下可通过将参数更改为天气删除冲突： 阳光明媚，今天： 星期一或运行状况： 病假分别。 大多数人会愿意立即第二，首先，更改天气也希望避免更改运行状况。

\*ConflictPriority 指令使您能够指定哪些参数，以更改冲突有关的首选项。 \*ConflictPriority 接受一个正整数值，指定每个参数的相对重要性。 当两个或多个参数会发生冲突时，分析器将修改具有低优先级参数的参数的设置。 此指令符合最高优先级项都标有最小序号的常见的用法。 因此，应分配的最高优先级参数\*ConflictPriority:1. 为选择的值\*ConflictPriority： 不需要是连续的但它们应该是唯一的。 \*ConflictPriority 应显示为子条目的\*功能构造。

\*FeatureType 指令还会影响参数的优先级。 \*FeatureType 是实际的 GPD/Unidrv 特定关键字。 对于非 Unidrv 客户端，您必须只需设置\*的 FeatureType:参数\_属性。 此设置将在以后避免意外的行为。 \*FeatureType 应显示为子条目的\*功能构造。

当 GDL 更改参数的设置来解决冲突时，它将使用默认设置，除非也限制。 在某些情况下，你可能想分析器来解析不同配置下的冲突时使用不同的默认设置。 若要设置这种不同的默认设置，定义多个\*DefaultOption 指令在交换机和用例的指令或一组嵌套的 Switch Case 指令中。 分析器将评估以确定使用的开关和当前配置的情况\*DefaultOption 使用。 冲突解决程序算法确定具有最高优先级 （即，最小序号） 启动的参数的设置，因为具有比计算参数的优先级较低的优先级参数的设置是未知的。 必须确保任何开关构造围绕\*DefaultOption 指令使用具有更高的优先级的参数 （即，较小序号） 比其默认值通过使用正在定义的参数\*DefaultOption。 如果不遵循此规则，分析器函数将失败。 由于此困难，因此应避免插入\*DefaultOption 到开关和用例构造如有可能。

**ResolveConstraint()** 显式检查约束冲突的配置以及解决该冲突，如果发现任何可以调用分析器接口函数。 新的配置将返回给调用方。 调用方可以检查可接受性的配置，或者可以使用配置来获取[快照](gdl-snapshots.md)。 快照指示哪些参数设置约束下在其创建中指定的配置。 此信息可能非常有用的客户端的创建用户界面。

 

 




