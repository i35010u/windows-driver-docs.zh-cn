---
title: 解决 GDL 配置冲突
description: 解决 GDL 配置冲突
keywords:
- GDL WDK，配置
- 配置 WDK GDL，配置无效
- 配置 WDK GDL，冲突
- 无效的 GDL 配置 WDK
- 配置 WDK GDL，解决冲突
- 解决 GDL 配置冲突 WDK GDL
- ConflictPriority 指令 WDK GDL
- FeatureType 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb748437abf55dc07aaf42c579b47b1914d373c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807017"
---
# <a name="resolving-gdl-configuration-conflicts"></a>解决 GDL 配置冲突


尽管 GDL 分析器会自动修改配置以避免违反约束，但请记住以下信息，以便分析器知道您的意图。

例如，如果传递到分析器函数的配置包含天气的参数设置，则为 "当前. 星期日，运行状况"。嗯，可以通过更改此约束中命名的任何一个参数的设置来解决前一节中的无效组合。 分析器必须确定要更改的参数设置。 在许多情况下，你可能会知道应该更改哪个设置。 通常，越重要的参数将保持不变。 在这种情况下，可以通过将参数更改为天气： Sunny，今日：星期一，或运行状况：病假来删除冲突。 大多数人都倾向于首先改变天气，并希望避免更改运行状况。

\*ConflictPriority 指令使你可以指定有关在冲突中更改哪个参数的首选项。 \*ConflictPriority 接受一个指定每个参数的相对重要性的正整数值。 当两个或更多参数出现冲突时，分析器将修改优先级较低的参数的参数设置。 此指令符合使用最高优先级项标记为最小序号的常见用法。 因此，应为最高优先级参数分配 \* ConflictPriority：1。 为 ConflictPriority 选择的值 \* 不需要是连续的，但它们应该是唯一的。 \*ConflictPriority 应显示为功能构造的子条目 \* 。

\*FeatureType 指令还会影响参数的优先级。 \*FeatureType 实际上是一个 GPD/Unidrv 特定的关键字。 对于非 Unidrv 客户端，必须简单地设置 \* FeatureType： PARAMETER \_ 属性。 此设置将避免将来出现意外的行为。 \*FeatureType 应显示为功能构造的子条目 \* 。

当 GDL 更改参数的设置以解决冲突时，它将使用默认设置，除非该设置也受约束。 在某些情况下，您可能希望分析器在使用不同配置解决冲突时使用不同的默认设置。 若要设置此类不同的默认设置，请在 \* switch 和 case 指令中或在一组嵌套的 Switch Case 指令中定义多个 DefaultOption 指令。 分析器将在给定当前配置的情况下计算开关和大小写，以确定 \* 要使用的 DefaultOption。 由于解析程序算法会确定参数的设置（从最高优先级 (开始，即最小序号) ），其优先级低于计算下参数优先级的参数的设置是未知的。 您必须确保任何围绕 DefaultOption 指令的 Switch 构造 \* 使用的参数的优先级高于 (的优先级，较小的序号) 大于使用 DefaultOption 定义其默认值的参数 \* 。 如果不遵守此规则，分析器函数将失败。 由于此问题，应尽量避免将 \* DefaultOption 插入到交换机和大小写结构中。

可以调用 **ResolveConstraint ( # B1** 分析器接口函数，以显式检查配置中是否存在约束冲突并解决冲突（如果找到）。 新配置将返回到调用方。 然后，调用方可以检查 acceptability 的配置，或者可以使用该配置来获取 [快照](gdl-snapshots.md)。 快照指示哪些参数设置受其创建中指定的配置约束。 此信息可能对创建用户界面的客户端很有用。

 

 




