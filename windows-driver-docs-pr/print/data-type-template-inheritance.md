---
title: 数据类型模板继承
description: 数据类型模板继承
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，模板继承
- 模板 WDK GDL，继承
- 继承 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b259134b1d3ec5345610b45f85ffc276b1bd633
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797347"
---
# <a name="data-type-template-inheritance"></a>数据类型模板继承


数据类型模板可以继承先前定义的数据类型模板中的属性。 所有适用于基本模板的已识别属性都将被继承。 无法在派生模板中重新定义继承的属性。

派生模板可以由其他模板继承给所需的任何级别。 若要指定要从中继承的模板，只需使用 Inherits 指令为其命名即可 \* 。 基本模板必须是数据类型模板。

用作基本模板的模板无需完全定义。 \*Virtual： **TRUE** 指令用于通知分析器模板可以部分定义。 但 (基本模板必须包含 **\* DataType** 指令。 ) 派生模板可以完成数据类型的定义。 如果派生模板无法完成数据类型的定义，则必须将其显式声明为 **虚拟**。 不继承 **虚拟** 指令。 不能使用 **\* ElementType** 或 **\* ValueType** 指令引用虚拟模板。 它们只能通过 **\* Inherits** 指令进行引用。

**注意**  如果在复合数据类型中提供 **\* ElementType** 指令时，parser 筛选器将自动为 **\* 数组大小** 指令创建默认值。 因此，可以在 **\* ElementType** (之前定义 **\* 数组大小**，方法是在模板中定义 **\* 数组大小**，该模板随后会由定义 **\* ElementType**) 的模板继承，但不允许 (也就是说，不能在 **\* 数组大小**) 之前定义 **\* elementtype** 。

 

### <a name="schemas"></a>架构

不会为不完整的数据类型模板发出架构。 若要避免冗余的架构定义，则不会为从已具有架构的模板派生的模板发出架构。 此限制消除了一种基元数据类型的多个定义，如果定义了一个基元数据类型的多个变体而没有继承帮助，则会产生这种情况。 **虚拟** 指令不影响是否发出架构。 一般用户无需了解有关何时发出架构的详细信息。 分析器筛选器会自动处理这种情况。

### <a name="binding"></a>绑定

派生模板直接继承在 **\* 继承的：** 指令引用的基模板中定义或继承的属性。 如果从另一个数据类型模板或来自特性模板的 **\* ValueType** 指令引用一个 **\* 派生的或** 基模板，则将绑定该命名模板。 没有复杂的绑定算法（如用于绑定构造模板的成员）。 这种算法没有意义，因为值没有实现间接绑定所需的名称或实例名称。

### <a name="example"></a>示例

数据类型继承用于分解多个数据类型模板所共有的属性。 在下面的示例中，基本模板定义了多个数组数据类型的通用属性。 请注意，使用了两个级别的继承。

```cpp
*Template:  GENERIC_ARRAY  *%  Basemost Template
{
    *Type:  DATATYPE
    *Virtual:  TRUE
    *DataType:   ARRAY
    *RequiredDelimiter: ","
    *OptionalDelimiter: "<20 09>"
}
*Template:  LIST_OF_TYPE  *%  first level derived Template
{
    *Inherits:  GENERIC_ARRAY
    *ArrayLabel: "LIST"
    *ArraySize: [*]
    *Virtual:  TRUE
}

*Template:  DT_INT_ARRAY  *%  first level derived Template
{
    *Inherits:  GENERIC_ARRAY
    *ElementType:  INTEGER
    *Virtual:  TRUE
}

*% ===================
*%  Second-level templates derived from LIST_OF_TYPE
*% ===================

*Template:  COLORS_LIST  
{
    *Inherits:  LIST_OF_TYPE
    *ElementType:  COLORS
    *ElementTags: (colors)
}
*Template:  STD_VAR_LIST
{
    *Inherits:  LIST_OF_TYPE
    *ElementType:  STD_VAR
    *ElementTags: (Standard_Variable)
}

*% ===================
*%  Second-level templates derived from DT_INT_ARRAY
*% ===================

*Template:  DT_POINT
{
    *Inherits:  DT_INT_ARRAY
    *ArrayLabel: "POINT"          
    *ElementTags: (X_pos, Y_pos)
    *ArraySize: 2
}
*Template:  DT_PAIR_OF_INTS
{
    *Inherits:  DT_INT_ARRAY
    *ArrayLabel: "PAIR"
    *ElementTags: (width, height)
    *ArraySize: 2
}
*Template:  RECTANGLE
{
    *Inherits:  DT_INT_ARRAY
    *ArrayLabel: "rect"
    *ElementTags: (left, top, right, bottom)
    *ArraySize: 4
}
```

 

 




