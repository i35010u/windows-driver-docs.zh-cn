---
title: GDL 配置
description: GDL 配置
ms.assetid: ce698737-c9d8-4502-8823-e249820a06fa
keywords:
- GDL WDK 配置
- 配置 WDK GDL
- 配置 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 990c4483698ead05304389900fe9b0bbe1bf4076
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392168"
---
# <a name="gdl-configurations"></a>GDL 配置


GDL，可在数据中定义依赖项。 客户端不需要注意的依赖项;相反，客户端指定所需的配置时请求快照和分析器会生成对应于该配置的快照。

例如，支付电话呼叫的价格取决于源和目标点、 时间和日期是星期几发起呼叫，使用时，调用计划等。 可以由大型多维数组表示所有可能结果的价格。 可以使用 GDL 指令以定义参数来表示此数据，以表示各种变量，如源和目标点、 时间、 调用计划和等等。 其他指令可以用于定义这些参数的允许的值。 仍其他指令指定的数据如何取决要定义的参数的值。 表示电话呼叫 (在下面的示例 CostOfCall) 的成本的数据以 GDL 源文件后，可以对其进行分析和任何客户端可以获取通过简单地创建分配所需的 va 的配置进行电话呼叫的成本文中 GDL 定义每个参数。

例如，客户端可能会编写包含以下数据的配置。

```cpp
OriginationPoint: Seattle
DestinationPoint: SanFrancisco
LengthOfCall: 10minutes
TimeOfDay: Night
CallingPlan: OneRate
```

生成的快照将包含一条数据 （从所有可能的组合），可能看起来如下例所示。

```cpp
CostOfCall: $0.49
```

GDL 快照可以包含与数千个项或只是一个复杂的数据结构。 快照中的每个项可以对配置的客户端并不知道有其自己的依赖项集。 客户端必须只需提供的感兴趣，配置和 GDL 分析器将返回到该配置表示相对应的数据的快照。

此外，GDL 启用所选的配置要排除作为"不允许"。 例如，打印设备可能不想要允许透明介质上的双面打印。 GDL 分析器接口有方法来检测提供的配置是允许还是不允许;如果配置不被允许，该方法使它允许按最小方式可修改该配置。 有指令定义排除的配置和指令，以便可以纠正了配置以解决冲突并可以进行更改以便在保留了原来的意图尽可能多地指定参数的相对重要性。

有关创建数据的详细信息与配置相关，请参阅[创建 GDL 配置依赖于数据](creating-gdl-configuration-dependent-data.md)。

 

 




