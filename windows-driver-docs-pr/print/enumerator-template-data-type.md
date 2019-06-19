---
title: 枚举器模板数据类型
description: 枚举器模板数据类型
ms.assetid: deb95ca1-05a5-47f4-8e2a-1d1aa1ae2261
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，基元
- 枚举器数据类型 WDK GDL
- ArrayLabel 指令 WDK GDL
- XMLDataType 指令 WDK GDL
- EnumeratorList 指令 WDK GDL
- ElementTags 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 701c13ccafed48b7367b5e9d1a9e1a5c54b4abd9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324266"
---
# <a name="enumerator-template-data-type"></a>枚举器模板数据类型


枚举器的数据类型具有允许的限制为一组标记的值。

\*数据类型：枚举器指示一个模板来定义枚举数据类型。 此数据类型将输出为 XML 架构简单类型声明派生自**字符串**类型具有限制，以指定每个允许的枚举器。 以下指令用于完全定义枚举器的数据类型：

-   \*XMLDataType （必需）。 若要将分配给将用于在生成的 XML 架构中定义此枚举的 XML 数据类型的 NCName。 每个枚举类型必须具有唯一的 NCName。 此名称必须是唯一的所有 XSD\_定义和枚举器类型。 若要避免冲突 GDL 分析器定义的数据类型，应避免 NCNames 开头的"GDL\_"和"GDLW\_"。

-   \*EnumeratorList （必需）。 枚举器令牌的列表。 每个标记必须是有效的 GDL 符号，并且必须符合的 XSD 架构的架构组件的值施加的任何其他要求：&lt;枚举&gt;。

-   \*ArrayLabel （可选）。 如果指定此指令，则分析器筛选器需要括在圆括号，以指定的数组标签值。

要被分析为一个枚举器的数据类型必须与令牌之一匹配的值的\*ElementTags 指令定义。

请考虑以下模板。

```cpp
*Template:  COLORS
{
    *Type:  DATATYPE
    *DataType:   ENUMERATOR
    *XMLDataType: "colors"
    *EnumeratorList: (YELLOW, MAGENTA, CYAN, BLACK, RED, GREEN, BLUE)
}
```

前面的模板将导致分析器筛选器，以创建以下 XML 架构项。

```cpp
    <simpleType name = "colors">
        <restriction base="string">
            <enumeration value="YELLOW"/>
            <enumeration value="MAGENTA"/>
            <enumeration value="CYAN"/>
            <enumeration value="BLACK"/>
            <enumeration value="RED"/>
            <enumeration value="GREEN"/>
            <enumeration value="BLUE"/>
        </restriction>
    </simpleType>
```

分析器筛选器还将创建相应的已包装的数据类型。

```cpp
    <complexType name = "GDLW_colors">
        <simpleContent>
            <extension base="gdl:colors">
                <attribute name="Name" type="string" use="optional"/>
                <attribute name="Personality" type="string" use="optional"/>
            </extension>
        </simpleContent>
    </complexType>
```

请考虑以下 GDL 条目。

```cpp
*Color: GREEN
```

并考虑 ACOLOR 模板声明 **\*颜色** GDL 属性 **\*ValueType** ，指由模板颜色，下面的代码示例显示。

```cpp
*Template:  ACOLOR
{
    *Name:  "*Color"
    *Type:  ATTRIBUTE
    *ValueType:  COLORS
    *Additive: LEAST_TO_MOST_RECENT
}
```

如果早期 GDL 条目解释使用 ACOLOR 模板生成的 XML 输出会发生。

```cpp
    <GDL_ATTRIBUTE Name="*Color"  xsi:type="GDLW_colors" >GREEN</GDL_ATTRIBUTE>
```

XML 特性**xsi: type**定义此实例 GDL\_ATTRIBUTE 元素包含模板定义的值类型表示一个 XML 默认命名空间中定义的枚举。

 

 




