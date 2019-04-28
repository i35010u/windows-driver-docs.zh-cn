---
title: GDL 架构
description: GDL 架构
ms.assetid: 1020bec8-3b34-4391-9e75-9ffcd8b07785
keywords:
- GDL WDK 架构
- 架构 WDK GDL
- 架构 WDK GDL，示例
- 构造 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f4f642c799cab763952b8b66e9e6d6843e3205a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346575"
---
# <a name="gdl-schemas"></a>GDL 架构


GDL 分析器，可创建和实现数据驱动的架构。 提供一个架构，则分析器执行验证架构，并将数据转换。

一个*架构*介绍的结构和相关联的 GDL 源文件中的数据格式。 可以在 GDL 源数据文件本身内定义架构，也可以是单独 GDL 源数据文件引用的文件。 该架构定义可以出现在每个构造，并可以定义每个属性的时间量的数据条目。 例如，可能会定义构造来描述一个人。 您可能希望构造来包含此人的姓名、 出生日期、 高度、 权重、 家庭地址和雇用的一些信息。

GDL 数据可能类似于下面的代码示例。

```cpp
*Person: person_ID
{
  *Name:
  *Birthdate:
  *Height:
  *Weight:
  *HomeAddress:
  *EmploymentInfo:
} 
```

因为\*HomeAddress 和\*EmploymentInfo 表示信息的逻辑分组，它们还可以定义为构造，如以下代码示例所示。

```cpp
*HomeAddress:
{
  *StreetAddress:
  *Apt_Number:
  *City:
  *State:
  *Zip:
}

*EmploymentInfo:
{
  *Employer:
  *Address:
  *Position:
  *Salary:
  *StartDate:
}
```

GDL 构造，如前面的示例中所示未定义其结构和内容的任何语法规则。 例如，可能有的两个实例\*Person 构造，来指定\*千克和其他指定的权重\*中磅的权重。 这些多个实例可能会导致不一致。

GDL 架构提供的方法来正式指定的结构和传入的数据必须符合的内容。 分析器将针对此架构验证数据并如果数据的结构不符合的架构，则发出警告。 可以指定是否条目是必需或可选 （如 Apt) 或是否可将条目多次定义。 例如， \*Apt\_数可能是可选并且由一个人可以保留两个作业。

架构允许条目来共享和继承的定义。 例如，对于架构定义\*解决\*EmploymentInfo 可由共享\*HomeAddress。 架构允许新的定义来派生自现有定义。 这两个地址构造不需要是完全相同，因为它们可以是派生自公共继承的定义的变体。

架构可以用于指定给定的属性值的格式。 例如，架构可以要求 MM DD YYYY 格式指定日期值。 您还可以将分解为其构成组件的复杂值表达式并将其显示快照中的分析器。 例如，客户端应用程序可能想分解为三个单独的字段，如以下代码示例所示的日期。

```cpp
*Date:
{
  *Month: Jan
  *Day: 1
  *Year: 2001
}
```

架构的支持继承的功能有其他影响。 继承自然地，可保持兼容性的同时扩展架构。 如果没有自动将派生自另一个架构，符合的派生架构的数据文件的架构也符合原始架构。 此继承，供应商可以自定义其架构 (和暗示其数据文件) 同时保留与主架构 （和所有应用程序需要与主架构的一致性） 的兼容性。 在实践中，供应商必须仅引用定义主架构的文件并创建新的定义继承主架构中定义的。 供应商不需要使主架构的私有副本，或修改主架构以任何方式。 这种情况下可确保供应商不需要执行任何操作，如果随后修改主架构。

如前面的示例所示，继承，可分解的常见模式，并避免不必要的重复的定义和随附的维护。 因此，架构以及它们所代表的数据集可以和构思和逻辑结构。

有关如何使用基于继承的架构的详细信息，请参阅[GDL 模板](gdl-template-structure.md)。

 

 




