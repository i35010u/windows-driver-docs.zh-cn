---
title: GDL 架构
description: GDL 架构
keywords:
- GDL WDK，架构
- 架构 WDK GDL
- 架构 WDK GDL，示例
- 构造 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 882b4ab6761bf7af69ad27e929a5c79d2e611c1e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796947"
---
# <a name="gdl-schemas"></a>GDL 架构


使用 GDL 分析器，可以创建和实现数据驱动的架构。 提供架构时，分析器会执行验证架构并转换数据。

*架构* 描述关联的 GDL 源文件中数据的结构和格式。 可以在 GDL 源数据文件本身中定义架构，也可以将其作为 GDL 源数据文件引用的单独文件。 架构定义可以在每个构造内显示的数据条目，以及每个属性可以定义的次数。 例如，你可以定义用于描述人员的构造。 你可能希望此构造包括人员姓名、出生日期、高度、体重、家庭地址和一些雇用信息。

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

由于 \* HomeAddress 和 \* EmploymentInfo 表示信息的逻辑分组，因此也可以将它们定义为构造，如以下代码示例所示。

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

如前面的示例中所示的 GDL 构造不定义其结构和内容的语法规则。 例如，可能有两个 \* Person 构造实例，一个指定 \* 以千克为权重，另一个指定 \* 以磅为重量。 这些多个实例可能会导致不一致。

GDL 架构提供了一个方法，用于正式指定传入数据必须符合的结构和内容。 分析器将根据此架构验证数据，并在数据的数据或结构不符合架构时发出警告。 可以指定 (（如 Apt）) 是否需要项或可选项，也可以指定是否可以多次定义条目。 例如， \* Apt \_ Number 可能是可选的，并且一个人可以包含两个作业。

架构允许共享和继承项的定义。 例如， \* EmploymentInfo 中地址的架构定义 \* 可以由 HomeAddress 共享 \* 。 架构允许从现有定义派生新定义。 这两个地址构造不必完全相同，因为它们可以是派生自公共继承定义的变量。

此架构可用于指定给定属性值的格式。 例如，架构可能要求以 MM-YYYY 格式指定日期值。 您还可以让分析器将复杂值表达式分解为其构成的组件，并将它们显示在快照中。 例如，客户端应用程序可能希望日期分解为三个不同的字段，如以下代码示例所示。

```cpp
*Date:
{
  *Month: Jan
  *Day: 1
  *Year: 2001
}
```

支持继承的架构的能力具有其他含义。 继承自然使你可以扩展架构，同时保持兼容性。 如果有一个架构是从其他架构派生的，则符合派生架构的数据文件也会自动遵从原始架构。 此继承使供应商能够自定义其架构 (，并通过隐含数据文件) ，同时保持与主架构 (和需要符合主架构) 的所有应用程序的兼容性。 在实际情况下，供应商必须只引用定义主架构的文件并创建从 master 架构的定义继承的新定义。 供应商无需创建主架构的私有副本或以任何方式修改主架构。 这种情况可确保在以后修改主架构时，供应商无需执行任何操作。

如前面的示例所示，通过继承可分解常见模式，避免不必要地重复定义和伴随维护。 因此，它们所代表的架构和数据集可以很好地进行理解并以逻辑方式进行结构化。

有关如何使用基于继承的架构的详细信息，请参阅 [GDL 模板](gdl-template-structure.md)。

 

 




