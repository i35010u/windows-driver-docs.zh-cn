---
title: 数据类型模板继承
description: 数据类型模板继承
ms.assetid: c2ecc091-8fdc-4666-9cdf-629903f13f6f
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，模板继承
- 模板 WDK GDL，继承
- 继承 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6944f9d58e45413a84a02f5c71321fe492f665b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341311"
---
# <a name="data-type-template-inheritance"></a>数据类型模板继承


数据类型模板可以从以前定义的数据类型模板继承属性。 所有被识别继承适用于基本模板的属性。 在派生模板中，不能重新定义继承的属性。

可以由其他模板为所需的任何级别继承派生的模板。 若要指定要从中继承的模板，只需其命名使用\*Inherits 指令。 基模板必须是数据类型模板。

用作基模板的模板不需要完全定义。 \*虚拟：**TRUE**指令用来通知分析器模板可以部分定义。 (但是，能最基础的模板 **\*数据类型**指令。)派生的模板然后可以完成的数据类型的定义。 如果派生的模板不能完成的数据类型的定义，它必须显式声明它是能够**虚拟**。 **虚拟**指令不会继承。 不能使用引用的虚拟模板 **\*ElementType**或 **\*ValueType**指令。 可以仅通过引用 **\*Inherits**指令。

**请注意**  分析器筛选器会自动创建默认值为 **\*ArraySize**指令，如果缺少时 **\*ElementType**指令提供的复合数据类型中。 因此，  **\*ArraySize**可以定义之前 **\*ElementType** (通过定义 **\*ArraySize**中的模板随后由定义的模板继承 **\*ElementType**)，但不是允许反向 (即 **\*ElementType**不能定义之前 **\*ArraySize**)。

 

### <a name="schemas"></a>架构

架构不会发出的不完整的数据类型模板。 若要避免冗余架构定义，架构是不会发出的已有的架构的模板派生的模板。 此限制可消除多个定义的相同的基元数据类型时不继承借助定义一个基元数据类型的多个变体所产生的。 **虚拟**指令不影响是否发出架构。 一般的用户不需要了解的详细信息时，将发出一个架构。 分析器筛选器将自动处理此。

### <a name="binding"></a>绑定

定义或引用的基模板中继承的属性 **\*Inherits:** 指令直接继承的派生模板。 当由引用派生或基模板 **\*ElementType**指令从另一个数据类型的模板或 **\*ValueType**指令从属性模板绑定的命名的模板。 没有复杂绑定算法如用于绑定构造模板的成员。 此类算法是没有意义，因为值不具有名称或需实现间接绑定的实例名称。

### <a name="example"></a>示例

使用数据类型继承分离出所通用的多个数据类型模板的属性。 在以下示例中，基模板定义多个数组数据类型通用的属性。 请注意，使用两个级别的继承。

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

 

 




