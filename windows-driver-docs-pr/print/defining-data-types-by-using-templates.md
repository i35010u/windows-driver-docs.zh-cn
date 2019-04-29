---
title: 使用模板定义数据类型
description: 使用模板定义数据类型
ms.assetid: 9768f0da-b6cb-4f92-9ab4-2c95fedcb44c
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，使用模板中定义的数据类型
- 定义数据类型 WDK GDL
- 数据类型的模板 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d4b6cd1794aee2465f77c2c39bd647a1be7b988
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357651"
---
#  <a name="defining-data-types-by-using-templates"></a>使用模板定义数据类型


所有数据类型、 基元和复合类型，必须通过使用模板都定义。 任何属性模板定义的数据类型后，可以声明其值要使用的特定数据类型 **\*ValueType**指令。 此指令的值是数据类型模板的名称。

当分析器筛选器遇到的一个属性实例的 GDL 数据条目时，它将尝试将解析为该数据类型定义的语法规则根据该条目的值部分。 如果成功，分析器筛选器将分解为其基元 XML 等效的数据类型的数据类型和输出中相应的 XML 的那些值。 生成的 XML 表示复合数据类型将保留原始的数据类型定义的逻辑结构。 复合数据类型的子元素的名称定义的数据类型模板中定义的标记。 此命名使人读取器或软件的客户端 XML 快照能够轻松地查找和标识复合数据类型中的每个值。

模板指定为*数据类型的模板*（一个定义的数据类型） 设置**\*类型：数据类型**指令。 在数据类型模板中识别的指令是：

**\*ValueType:***\[数据类型的模板名称\]*。 此指令声明要作为特定的数据类型的属性的值。  **\*ValueType**指令可以出现仅在属性模板中。 (属性模板是使用模板**\*类型：属性**指令)。

**\*数据类型：** *符号*。 此指令具有以下值之一：传递、 XML\_类型、 XSD\_定义，枚举器，筛选\_类型、 数组、 复合或多个\_个性。

**\*ElementType:** *列表*。 此指令定义的模板数据类型名称的列表。

**\*RequiredDelimiter:** *分隔符*。 此指令定义具有带引号的字符串的分隔符。

**\*OptionalDelimiter:** *分隔符*。 此指令定义一个可选分隔符使用带引号的字符串。

**\*ArrayLabel:** *符号*。 此指令定义具有带引号的字符串数组标签。

**\*ElementTags:** *列表*。 此指令定义要用于元素标记的符号的列表。

**\*EnumeratorList:** *列表*。 此指令定义符号用于枚举器列表的列表。

**\*XSDTypeDefinition:** *符号*。 此指令定义的任意值，括&lt;Begin/EndValue&gt;元素，用于进行 XSD 的类型定义。

**\*ComplexType？:** *布尔*。 此指令定义或不是复杂类型。 如果值为 **，则返回 TRUE**，类型是复杂; 否则为类型是简单类型。

**\*ArraySize:** *整数*。 此指令定义数组的范围。 可以使用最多两个整数来指定数组范围。

**\*XMLDataType:** *字符串*。 此指令定义具有带引号的字符串的 XML 数据类型。

**FilterTypeName:** *字符串*。 此指令只需使用带引号的字符串，这样就可以定义筛选器类型名称。

**\*MaxValue:** *整数*。 此指令定义 GDL 整数值的最大大小。

**\*MinLength:** *整数*。 此指令定义通过使用一个非负 GDL 整数值的最小长度。

**\*MaxLength:** 整数。 此指令定义通过使用一个非负 GDL 整数值的最大长度。

**请注意**  在数据类型的所有模板中识别并不是所有指令。

 

一般情况下，如果没有模板可以绑定到 GDL 属性条目，该属性的值将激发而无需 CDATA 节内的任何更改在快照中。 作为元素内容 （即，子元素） 的属性元素应位于 CDATA。

例如，假设分析器不能找到说明了以下 GDL 属性项的模板。

```cpp
*ModelName: "OEMName LaserJet "
```

然后，该条目将显示在快照中，如下所示。

```cpp
    <GDL_ATTRIBUTE Name="*ModelName" 
        <![CDATA["OEMName LaserJet "]]></GDL_ATTRIBUTE>
```

 

 




