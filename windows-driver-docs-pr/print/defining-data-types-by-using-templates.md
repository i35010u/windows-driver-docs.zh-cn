---
title: 使用模板定义数据类型
description: 使用模板定义数据类型
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，使用模板定义数据类型
- 定义数据类型 WDK GDL
- 数据类型模板 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf01c0cf74f8fe88f1f14492d1c12367bd0333aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797305"
---
#  <a name="defining-data-types-by-using-templates"></a>使用模板定义数据类型


所有数据类型（基元类型和复合类型）都必须使用模板定义。 定义数据类型后，任何属性模板都可以使用 **\* ValueType** 指令将其值声明为特定数据类型。 此指令的值是数据类型模板的名称。

如果分析器筛选器遇到作为属性实例的 GDL 数据输入，它将尝试根据为该数据类型定义的语法规则来分析该条目的值部分。 如果成功，则分析器筛选器会将数据类型分解为其基元 XML 等效数据类型，并在相应的 XML 中输出这些值。 生成的表示复合数据类型的 XML 将保留原始数据类型定义的逻辑结构。 复合数据类型的子元素被指定为数据类型模板中定义的标记所定义的名称。 此命名使得 XML 快照的人工读取器或软件客户端可以轻松地查找并标识复合数据类型中的每个值。

模板被指定为 *数据类型模板* (通过设置 **\* type： DATATYPE** 指令来定义数据类型) 。 在数据类型模板中识别的指令包括：

**\* ValueType：** *\[ Datatype 模板名称 \]*。 此指令将属性的值声明为特定的数据类型。 **\* ValueType** 指令只能出现在属性模板中。  (特性模板是具有 **\* TYPE： Attribute** 指令) 的模板。

**\* DataType：** *符号*。 此指令具有以下值之一： PASSTHROUGH、XML \_ 类型、XSD \_ 已定义、枚举器、筛选器 \_ 类型、数组、复合或多项 \_ 个性。

**\* ElementType：** *list*。 此指令定义模板数据类型名称的列表。

**\* RequiredDelimiter：** *分隔符*。 此指令定义带有带引号的字符串的分隔符。

**\* OptionalDelimiter：** *分隔符*。 此指令定义带有带引号的字符串的可选分隔符。

**\* ArrayLabel：** *符号*。 此指令定义带有带引号的字符串的数组标签。

**\* ElementTags：** *list*。 此指令定义用于元素标记的符号列表。

**\* EnumeratorList：** *list*。 此指令定义要用于枚举器列表的符号列表。

**\* XSDTypeDefinition：** *符号*。 此指令定义要用于 XSD 类型定义的任意值，其中包含 &lt; Begin/EndValue &gt; 元素。

**\* ComplexType？：** *boolean*。 此指令定义类型是否为复杂类型。 如果该值为 **TRUE**，则类型为 complex;否则，类型很简单。

**\* 数组大小：** *整数*。 此指令定义数组的范围。 最多可以使用两个整数来指定数组范围。

**\* XMLDataType：** *字符串*。 此指令定义带有带引号的字符串的 XML 数据类型。

**FilterTypeName：** *字符串*。 此指令使用带引号的字符串定义筛选器类型名称。

个 **\* ：** *整数*。 此指令使用 GDL 整数定义值的最大大小。

**\* MinLength：** *整数*。 此指令使用非负 GDL 整数定义值的最小长度。

**\* MaxLength：** 整数。 此指令使用非负 GDL 整数定义值的最大长度。

**注意**   并非所有指令都是在所有数据类型模板内识别的。

 

通常，如果不能将任何模板绑定到 GDL 属性项，则在快照中将发出该属性的值，而不会在 CDATA 节中进行任何更改。 CDATA 应作为元素内容驻留 (即 ATTRIBUTE 元素的子元素) 。

例如，假设分析器找不到描述以下 GDL 属性项的模板。

```cpp
*ModelName: "OEMName LaserJet "
```

然后，该条目将显示在快照中，如下所示。

```cpp
    <GDL_ATTRIBUTE Name="*ModelName" 
        <![CDATA["OEMName LaserJet "]]></GDL_ATTRIBUTE>
```

 

 




