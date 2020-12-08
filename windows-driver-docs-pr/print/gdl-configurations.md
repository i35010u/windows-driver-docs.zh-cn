---
title: GDL 配置
description: GDL 配置
keywords:
- GDL WDK，配置
- 配置 WDK GDL
- 配置 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c5fd958382e5844a95f428d3fb13ceca0db7886
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835997"
---
# <a name="gdl-configurations"></a>GDL 配置


GDL 使你能够在数据中定义依赖项。 客户端不需要了解依赖关系;相反，客户端会在请求快照时指定感兴趣的配置，而分析器会生成与该配置相对应的快照。

例如，对于电话呼叫收费的价格取决于源点和目标点、在一周中的哪一天、一周中的哪一天、一周中的某一天的时间、使用的调用计划等。 所有可能的结果的价格可由大多维数组表示。 此数据可通过以下方式表示：使用 GDL 指令定义用于表示各种变量的参数，如原点和目标点、当天时间、调用计划等。 其他指令可用于为这些参数定义允许的值。 其他指令仍指定数据如何依赖于要定义的参数的值。 在以下) 示例中，表示电话呼叫成本的数据 (CostOfCall，则可以对其进行分析，并且任何客户端都可以通过创建一个配置，将所需的值分配给在 GDL 中定义的每个参数，从而获得拨打电话的成本。

例如，客户端可能会编写包含以下数据的配置。

```cpp
OriginationPoint: Seattle
DestinationPoint: SanFrancisco
LengthOfCall: 10minutes
TimeOfDay: Night
CallingPlan: OneRate
```

而且，生成的快照将包含一段数据 (所有可能的组合) ，如以下示例中所示。

```cpp
CostOfCall: $0.49
```

GDL 快照可包含包含上千个项或只包含一个项的复杂数据结构。 快照中的每一项都可以对客户端无法识别的配置具有自己的依赖项集。 客户端只需提供相关配置，GDL 分析器就会返回代表该配置的数据的快照。

此外，GDL 允许将所选配置排除为 "不允许"。 例如，打印设备可能不希望在透明媒体上允许双面打印。 GDL 分析器接口包含检测是否允许或禁止所提供配置的方法;如果不允许该配置，则该方法将最小限度地改变配置，使其允许。 有一些指令用于定义排除的配置和指令以指定参数的相对重要性，以便可以更正配置以解决冲突，并可以进行更改以使其尽可能地保留原始意向。

有关创建依赖于配置的数据的详细信息，请参阅 [创建 GDL Configuration-Dependent 数据](creating-gdl-configuration-dependent-data.md)。

 

 




